## 📑 LLM-powered Resume Screening and ATS Optimization Agent

Este projeto apresenta uma solução inteligente orientada a dados para otimizar o fluxo de triagem e análise de candidatos no recrutamento técnico. Através de um Agente de Inteligência Artificial baseado em Grandes Modelos de Linguagem (LLMs), o sistema automatiza a análise de aderência por meio de avaliação heurística ponderada e reestruturação de currículos para vagas específicas, com foco estrito em document-grounded generation e mitigação ativa de alucinações.

---

## 🧭 Visão Geral da Arquitetura

```text
Usuário
   │
   ├── Upload: Currículo (PDF)
   ├── Upload: Vaga (PDF)
   │
   ▼
Mascaramento de PII (local, antes do envio)
   │
   ▼
LLM (Gemini)
   │
   ├── Job Analysis
   ├── Resume Analysis
   ├── Match Engine
   ├── Verification
   └── JSON Formatter
   │
   ▼
Reidentificação de PII (local, após a resposta)
   │
   ▼
Structured Output (JSON)
```

> **Nota de transparência:** as cinco etapas acima (Job Analysis → JSON Formatter) são instruções sequenciais dentro de um único prompt e uma única chamada à API — não chamadas separadas. O modelo executa tudo em uma passada, seguindo o `processo_de_trabalho` definido no `system_instruction`. Isso é uma escolha deliberada de custo/latência; uma versão multi-chamada (com uma etapa de verificação separada, auditando o rascunho gerado) tende a reduzir ainda mais o risco de alucinação, mas ao custo de mais chamadas de API.

## 📐 Processamento Modular

O agente segue, dentro de um único prompt, um fluxo sequencial estrito dividido em 5 etapas internas:

1. **Job Analysis (Análise da Vaga):** Mapeamento de termos-chave, tecnologias obrigatórias (hard skills) e competências desejadas (soft skills).
2. **Resume Analysis (Análise do Currículo):** Varredura detalhada no histórico do candidato em busca de experiências correlatas e mapeamento de equivalências/sinônimos reais.
3. **Match Engine (Motor de Aderência):** Aplicação de regras matemáticas ponderadas sobre os dados encontrados para definição do Score.
4. **Verification (Validação de Integridade):** Camada interna de autocrítica (Verification Loop) que audita o resultado gerado contra o documento original para mitigar ativamente alucinações.
5. **JSON Formatter (Formatador de Saída):** Estruturação de todos os dados extraídos, relatórios e texto adaptado sob um esquema JSON estrito.

## 🛠️ Tecnologias e Conceitos Aplicados

- **Ambiente de Execução:** Google Colab, via SDK `google-genai`
- **Modelo de Linguagem:** `gemini-flash-latest` (alias mantido pela Google apontando para a versão estável mais recente do Gemini Flash — nomes fixos de modelo, como versões antigas do Flash, são periodicamente descontinuados para novos usuários)
- **Leitura de documentos:** `pypdf`, tanto para o currículo quanto para a vaga (ambos enviados como anexo PDF)
- **Estratégias de Prompt Engineering:**
    - *Persona Definition* (Especialista em Atração de Talentos Técnicos)
    - *Sequential Workflow* (Processo de Trabalho Modular dentro de um único prompt)
    - *Few-Shot Learning* (Treinamento In-Context por Exemplos)
    - *Verification Loop* (Camada Interna de Validação Antialucinação)
    - *Structured Output* (`response_mime_type="application/json"` + esquema descrito no `system_instruction`)

## 📊 Critério do Match Score

O cálculo da **Compatibilidade Estimada** baseia-se em uma heurística ponderada inspirada em regras de mercado para sistemas ATS (*Applicant Tracking Systems*):

| Critério | Peso na Nota | Descrição |
| --- | --- | --- |
| **Hard Skills** | 50% | Correspondência de tecnologias obrigatórias ou sinônimos equivalentes. |
| **Experiência** | 25% | Tempo de atuação e profundidade dos projetos correlacionados à vaga. |
| **Soft Skills** | 15% | Alinhamento de metodologias de trabalho e competências comportamentais. |
| **Certificações** | 10% | Cursos, especializações e credenciais explícitas exigidas no anúncio. |

> **Limitação conhecida:** o percentual final é entregue como um único número pelo modelo, sem o detalhamento por critério. Isso significa que o cálculo ponderado não é auditável a partir do JSON de saída — está sujeito à interpretação do LLM sobre os pesos, não a uma fórmula verificável.

## 🔒 Privacidade e Retenção de Dados (LGPD)

Este agente processa dados pessoais reais de candidatos (nome, e-mail, telefone, links de perfil). Duas camadas de proteção foram implementadas:

**1. Mascaramento de PII antes do envio (pseudonimização reversível)**

Antes de qualquer texto ser enviado à API do Gemini, uma função local (`anonimizar_pii`) substitui os dados pessoais identificáveis por tokens:

- Nome do candidato → `[NOME_CANDIDATO]`
- E-mail → `[EMAIL_1]`, `[EMAIL_2]`...
- Telefone → `[TELEFONE_1]`...
- Links de perfil (LinkedIn, GitHub) → `[LINK_PERFIL_1]`...

O mapeamento entre token e dado real (`mapa_pii`) permanece exclusivamente na sessão local — nunca é enviado à API. Após a resposta do modelo, uma função de reidentificação (`reidentificar`) percorre o JSON retornado e substitui os tokens pelos dados reais, já na sua máquina.

> **Limitação conhecida:** a detecção do nome do candidato usa uma heurística posicional (assume que o nome é a primeira linha do PDF), válida para o formato de currículo mais comum, mas frágil diante de layouts atípicos. Para uso em produção com currículos de formatos variados, recomenda-se substituir essa heurística por um modelo de NER dedicado (ex: spaCy `pt_core_news`), que identifica nomes por contexto linguístico em vez de posição no documento.

**2. Política de retenção da Google na API paga**

Segundo os Termos de Serviço da API Gemini, nos serviços pagos a Google não usa os prompts (incluindo instruções de sistema, arquivos e conteúdo em cache) nem as respostas para melhorar ou treinar seus modelos — diferente do comportamento padrão do nível gratuito. Ainda assim, prompts e respostas ficam registrados por um período limitado, exclusivamente para fins de detecção de violação da política de uso (moderação/abuso). Por esse motivo, o mascaramento de PII descrito acima é aplicado independentemente do tier de uso, como camada extra de proteção.

Fonte oficial: [Zero data retention in the Gemini Developer API](https://ai.google.dev/gemini-api/docs/zdr)

Para operar com **Zero Data Retention** completo (inclusive sem esse registro temporário de moderação), é necessário solicitar aprovação de projeto ZDR junto à Google ou usar Vertex AI com Data Processing Addendum contratual — recomendado antes de levar este agente para produção com candidatos reais.

## ⚙️ Instruções Principais do Agente (Core Agent Instructions)

O modelo é configurado com `temperature=0.2` (reduzindo variabilidade/criatividade) e `response_mime_type="application/json"` (forçando saída estruturada). A estrutura abaixo é usada como **System Instructions**:

```json
{
  "system_instruction": "Você é um Especialista em Recrutamento e Seleção (Tech Recruiter) sênior de nível internacional. Sua especialidade é analisar currículos, extrair dados com precisão cirúrgica e mapear competências reais contra descrições de vagas (Job Descriptions), fornecendo relatórios analíticos e adaptando a apresentação das informações sem nunca falsificar ou inventar dados.",
  "context": "O usuário fornecerá o texto de um currículo (extraído de um PDF, possivelmente com tokens de anonimização no lugar de dados pessoais) e o texto de uma vaga de emprego (também extraído de um PDF). O seu objetivo é processar esses dados através de um fluxo modular de trabalho para avaliar a aderência do candidato e gerar um currículo adaptado e otimizado para a vaga em questão.",
  "constraints": [
    "PROIBIDO INVENTAR OU ALUCINAR: Você não deve criar experiências, empresas, datas, projetos, tecnologias ou certificados que não estejam explicitamente mencionados no arquivo enviado.",
    "ADAPTAÇÃO BASEADA EM GROUNDING: Adaptar significa reordenar, mudar a ênfase de palavras-chave e reescrever bullet points para destacar impactos relevantes à vaga. Utilize os termos da vaga apenas quando houver equivalência real e comprovada no currículo fornecido.",
    "OMISSÃO ESTRATÉGICA: Se o currículo contiver experiências ou tecnologias totalmente irrelevantes para a vaga-alvo, reduza o espaço dedicado a elas, priorizando o que importa para o recrutador.",
    "IDIOMA: Se a vaga estiver em inglês e o currículo original em português, o novo currículo gerado e as análises devem ser traduzidos e entregues inteiramente em inglês.",
    "TOKENS DE ANONIMIZAÇÃO: O currículo fornecido pode conter tokens como [NOME_CANDIDATO], [EMAIL_1], [TELEFONE_1], [LINK_PERFIL_1] no lugar de dados pessoais reais. Esses tokens DEVEM ser reproduzidos exatamente como estão, sem traduzir, remover ou alterar seu formato — eles serão substituídos pelos dados reais em uma etapa posterior fora do modelo."
  ],
  "processo_de_trabalho": [
    "Etapa 1 - Job Analysis: Identifique as hard skills obrigatórias, soft skills desejadas e os termos-chave essenciais.",
    "Etapa 2 - Resume Analysis: Varra o histórico do candidato buscando experiências, tecnologias ou sinônimos que atendam aos requisitos mapeados na Etapa 1.",
    "Etapa 3 - Match Engine: Realize uma análise quantitativa ponderada (Hard Skills 50%, Experiência 25%, Soft Skills 15%, Certificações 10%), calculando a porcentagem estimada de match, separando competências encontradas e destacando as lacunas.",
    "Etapa 4 - Verification & Formatting: Redija o novo documento focando nas conquistas e tecnologias correlatas à vaga e execute uma checagem rigorosa de integridade antes de formular o JSON final."
  ],
  "verification_loop": [
    "Confirme: Nenhuma empresa externa foi adicionada ao currículo?",
    "Confirme: Nenhuma tecnologia ou ferramenta foi inventada?",
    "Confirme: Nenhuma certificação ou curso inexistente foi criado?",
    "Confirme: Todas as informações presentes no texto final possuem origem estrita e exclusiva no currículo enviado?"
  ],
  "few_shot_examples": [
    {
      "cenario_1": {
        "entrada": {
          "curriculo": "Experiência sólida na construção de painéis gerenciais utilizando Power BI para o setor financeiro.",
          "vaga": "Requisitos: Domínio em ferramentas de Business Intelligence (BI) e análise de indicadores."
        },
        "saida_esperada": {
          "competencias": "* Business Intelligence (Power BI)"
        }
      }
    },
    {
      "cenario_2": {
        "entrada": {
          "curriculo": "Conhecimento conceitual em computação em nuvem obtido através de estudos autônomos. Sem experiência prática.",
          "vaga": "Desejável: Certificação AWS Certified Cloud Practitioner ou AWS Solutions Architect."
        },
        "saida_esperada_antialucinacao": {
          "competencias": "* Fundamentos de Cloud Computing",
          "nota_de_validacao": "A certificação AWS não foi adicionada ao perfil adaptado por não constar como emitida no currículo original."
        }
      }
    }
  ],
  "output_format": {
    "type": "JSON",
    "schema": {
      "relatorio_aderencia": {
        "compatibilidade_estimada_porcentagem": "number",
        "hard_skills_encontradas": ["string"],
        "soft_skills_encontradas": ["string"],
        "lacunas_identificadas": ["string"]
      },
      "curriculo_adaptado": {
        "nome_candidato": "string",
        "dados_contato": "string",
        "resumo_profissional": "string",
        "competencias_tecnicas": ["string"],
        "experiencia_profissional": [
          {
            "cargo": "string",
            "empresa": "string",
            "periodo": "string",
            "conquistas_e_atividades": ["string"]
          }
        ],
        "educacao_e_certificacoes": ["string"]
      }
    }
  }
}
```

### Passo 3: Execução no Notebook

1. Rode as células iniciais (instalação, imports, client).
2. Ao ser solicitado, faça o **upload do PDF do currículo** do candidato.
3. Em seguida, faça o **upload do PDF da vaga** (não é mais necessário colar o texto manualmente).
4. O currículo é automaticamente mascarado (PII → tokens) antes de qualquer chamada à API.
5. A célula de geração processa os dois documentos e retorna o JSON estruturado.
6. O JSON final já vem reidentificado (com os dados reais do candidato) e é salvo/baixado localmente.

## 📝 Exemplo de Execução Real

### 📥 Entradas Fornecidas

- **Currículo Enviado:** *"Carlos Silva. Desenvolvedor Backend com 3 anos de experiência utilizando Python e Django. Atuação na criação de APIs REST e consultas em bancos PostgreSQL. Conhecimento teórico em Docker."*
- **Descrição da Vaga:** *"Requisitos: Sólidos conhecimentos em Python, desenvolvimento de APIs robustas, modelagem SQL. Diferencial: Vivência com containers (Docker) e Metodologias Ágeis."*

### 📤 Saída Estruturada Gerada pelo Agente (JSON)

```json
{
  "relatorio_aderencia": {
    "compatibilidade_estimada_porcentagem": 85,
    "hard_skills_encontradas": [
      "Python",
      "Django (Desenvolvimento de APIs REST)",
      "PostgreSQL (Modelagem SQL)",
      "Docker (Conhecimento teórico)"
    ],
    "soft_skills_encontradas": [],
    "lacunas_identificadas": [
      "Metodologias Ágeis (Não citado no documento original)",
      "Experiência prática comprovada com Docker (Apenas conceitual)"
    ]
  },
  "curriculo_adaptado": {
    "nome_candidato": "Carlos Silva",
    "dados_contato": "Extraído conforme PDF original",
    "resumo_profissional": "Desenvolvedor Backend com 3 anos de experiência especializada na linguagem Python e ecossistema Django. Histórico focado no desenvolvimento de APIs REST e manipulação de bancos de dados relacionais PostgreSQL, apresentando alinhamento com arquitetura de containers utilizando Docker.",
    "competencias_tecnicas": [
      "Python / Django",
      "APIs RESTful",
      "Banco de Dados SQL (PostgreSQL)",
      "Containers (Docker - Nível Teórico)"
    ],
    "experiencia_profissional": [
      {
        "cargo": "Desenvolvedor Backend",
        "empresa": "Empresa Extraída do PDF",
        "periodo": "Período Extraído do PDF",
        "conquistas_e_atividades": [
          "Desenvolvimento backend utilizando Python focado na construção de APIs REST estruturadas.",
          "Manipulação e modelagem de dados utilizando banco de dados SQL (PostgreSQL)."
        ]
      }
    ],
    "educacao_e_certificacoes": [
      "Dados de formação acadêmica mantidos integralmente conforme documento original"
    ]
  }
}
```

## ⚠️ Limitações da Solução

- **Caráter Heurístico:** O Match Score funciona como uma estimativa analítica baseada nas diretrizes do prompt e não possui caráter estatístico preditivo ou probabilístico, nem detalhamento auditável por critério.
- **Document-Grounded:** O agente atua estritamente com os dados injetados. Currículos excessivamente omitidos ou mal estruturados na origem resultarão em notas baixas de aderência, visto que o agente é impedido de inferir ou presumir competências.
- **Pipeline single-call:** as 5 etapas descritas na arquitetura ocorrem dentro de uma única chamada de API, não como estágios independentes auditáveis — a "verificação" é uma autoconferência do modelo sobre o próprio texto que ele acabou de gerar, não uma segunda validação independente.
- **Heurística de nome para anonimização:** assume o nome do candidato na primeira linha do PDF; pode falhar em layouts de currículo atípicos.
- **Foco de Suporte:** A ferramenta foi projetada para atuar como um filtro inicial de triagem secundária para analistas de R&H, não substituindo entrevistas técnicas ou testes práticos.

## 🗺️ Roadmap de Evolução

- [x] Upload da vaga em PDF (substituiu o texto colado manualmente).
- [x] Mascaramento de PII antes do envio à API (LGPD).
- [ ] Migrar para `response_schema` estruturado (Pydantic/`types.Schema`) em vez de depender apenas de `response_mime_type`.
- [ ] Validação determinística pós-LLM (checar se as skills listadas realmente aparecem no texto do currículo).
- [ ] Separar as etapas de Match Engine e Verification em chamadas independentes de API para verificação genuína (não autoconferência).
- [ ] Detecção de nome via NER (spaCy `pt_core_news`) em vez de heurística posicional.
- [ ] Desenvolvimento de uma Interface Web interativa utilizando Streamlit.
- [ ] Criação de um serviço RESTful em FastAPI para processamento via requisições de sistemas legados.
- [ ] Suporte à leitura de documentos em formato .docx.
- [ ] Exportação do JSON adaptado diretamente para arquivos PDF formatados para impressão.

## 📄 Licença

Este projeto é distribuído sob os termos da licença MIT. Para mais informações, consulte o arquivo LICENSE.
