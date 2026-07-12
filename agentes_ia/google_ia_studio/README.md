## 📑 LLM-powered Resume Screening and ATS Optimization Agent

Este projeto apresenta uma solução inteligente orientada a dados para otimizar o fluxo de triagem e análise de candidatos no recrutamento técnico. Através de um Agente de Inteligência Artificial modular baseado em Grandes Modelos de Linguagem (LLMs), o sistema automatiza a análise de aderência por meio de avaliação heurística ponderada e reestruturação de currículos para vagas específicas, com foco estrito em document-grounded generation e mitigação ativa de alucinações.

---
## 🧭 Visão Geral da Arquitetura

```text
Usuário
   │
   ▼
Google AI Studio
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
Structured Output
```

## 📐 Processamento Modular

Para maximizar a confiabilidade e evitar a degradação de performance comum em tarefas simultâneas complexas, o agente opera em um fluxo sequencial estrito dividido em 5 etapas internas:

1. **Job Analysis (Análise da Vaga):** Mapeamento de termos-chave, tecnologias obrigatórias (hard skills) e competências desejadas (soft skills).
2. **Resume Analysis (Análise do Currículo):** Varredura detalhada no histórico do candidato em busca de experiências correlatas e mapeamento de equivalências/sinônimos reais.
3. **Match Engine (Motor de Aderência):** Aplicação de regras matemáticas ponderadas sobre os dados encontrados para definição do Score.
4. **Verification (Validação de Integridade):** Camada interna de autocrítica (Verification Loop) que audita o resultado gerado contra o documento original para mitigar ativamente alucinações.
5. **JSON Formatter (Formatador de Saída):** Estruturação de todos os dados extraídos, relatórios e texto adaptado sob um esquema JSON estrito.

## 🛠️ Tecnologias e Conceitos Aplicados

- **Ambiente de Execução:** Google AI Studio (Playground)
- **Modelo de Linguagem:** Gemini 1.5 Flash (Otimizado para processamento multimodal e baixa latência)
- **Estratégias de Prompt Engineering:**
    - *Persona Definition* (Especialista em Atração de Talentos Técnicos)
    - *Sequential Workflow* (Processo de Trabalho Modular)
    - *Few-Shot Learning* (Treinamento In-Context por Exemplos)
    - *Verification Loop* (Camada Interna de Validação Antialucinação)
    - *Structured Output* (Entrega Orientada a Esquema JSON)

## 📊 Critério do Match Score

O cálculo da **Compatibilidade Estimada** baseia-se em uma heurística ponderada inspirada em regras de mercado para sistemas ATS (*Applicant Tracking Systems*):

| Critério | Peso na Nota | Descrição |
| --- | --- | --- |
| **Hard Skills** | 50% | Correspondência de tecnologias obrigatórias ou sinônimos equivalentes. |
| **Experiência** | 25% | Tempo de atuação e profundidade dos projetos correlacionados à vaga. |
| **Soft Skills** | 15% | Alinhamento de metodologias de trabalho e competências comportamentais. |
| **Certificações** | 10% | Cursos, especializações e credenciais explícitas exigidas no anúncio. |

## ⚙️ Instruções Principais do Agente (Core Agent Instructions)

Para implantar este agente no Google AI Studio, configure o modelo **Gemini 1.5 Flash**, ajuste a **Temperatura para 0.2** (reduzindo variabilidade/criatividade) e insira a estrutura abaixo no campo de **System Instructions**:

```json
{
  "system_instruction": "Você é um Especialista em Recrutamento e Seleção (Tech Recruiter) sênior de nível internacional. Sua especialidade é analisar currículos, extrair dados com precisão cirúrgica e mapear competências reais contra descrições de vagas (Job Descriptions), fornecendo relatórios analíticos e adaptando a apresentação das informações sem nunca falsificar ou inventar dados.",
  "context": "O usuário fornecerá um arquivo PDF contendo o currículo do candidato e o texto de uma vaga de emprego. O seu objetivo é processar esses dados através de um fluxo modular de trabalho para avaliar a aderência do candidato e gerar um currículo adaptado e otimizado para a vaga em questão.",
  "constraints": [
    "PROIBIDO INVENTAR OU ALUCINAR: Você não deve criar experiências, empresas, datas, projetos, tecnologias ou certificados que não estejam explicitamente mencionados no arquivo enviado.",
    "ADAPTAÇÃO BASEADA EM GROUNDING: Adaptar significa reordenar, mudar a ênfase de palavras-chave e reescrever bullet points para destacar impactos relevantes à vaga. Utilize os termos da vaga apenas quando houver equivalência real e comprovada no currículo fornecido.",
    "OMISSÃO ESTRATÉGICA: Se o currículo contiver experiências ou tecnologias totalmente irrelevantes para a vaga-alvo, reduza o espaço dedicado a elas, priorizando o que importa para o recrutador.",
    "IDIOMA: Se a vaga estiver em inglês e o currículo original em português, o novo currículo gerado e as análises devem ser traduzidos e entregues inteiramente em inglês."
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

### Passo 3: Input do Usuário e Execução

Na área central de chat do Playground:

1. Clique no ícone de **Anexo** e faça o upload do arquivo PDF do currículo original.
2. Logo abaixo do arquivo, cole a descrição textual da vaga desejada.
3. Clique em **Run** para receber a análise e o currículo estruturados em JSON.

## 📝 Exemplo de Execução Real

### 📥 Entradas Fornecidas

- **Currículo Enviado:** *"Carlos Silva. Desenvolvedor Backend com 3 anos de experiência utilizando Python e Django. Atuação na criação de APIs REST e consultas em bancos PostgreSQL. Conhecimento teórico em Docker."*
- **Descrição da Vaga:** *"Requisitos: Sólidos conhecimentos em Python, desenvolvimento de APIs robustas, modelagem SQL. Diferencial: Vivência com containers (Docker) e Metodologias Ágeis."*

### 📤 Saída Estruturada Gerada pelo Agente (JSON)

```json
z{
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

- **Caráter Heurístico:** O Match Score funciona como uma estimativa analítica baseada nas diretrizes do prompt e não possui caráter estatístico preditivo ou probabilístico.
- **Document-Grounded:** O agente atua estritamente com os dados injetados. Currículos excessivamente omitidos ou mal estruturados na origem resultarão em notas baixas de aderência, visto que o agente é impedido de inferir ou presumir competências.
- **Foco de Suporte:** A ferramenta foi projetada para atuar como um filtro inicial de triagem secundária para analistas de R&H, não substituindo entrevistas técnicas ou testes práticos.

## 🗺️ Roadmap de Evolução

- [ ]  Desenvolvimento de uma Interface Web interativa utilizando Streamlit.
- [ ]  Criação de um serviço RESTful em FastAPI para processamento via requisições de sistemas legados.
- [ ]  Implementação de um módulo de parsing nativo com pypdf para automação de leitura em lote.
- [ ]  Suporte à leitura de documentos em formato .docx.
- [ ]  Exportação do JSON adaptado diretamente para arquivos PDF formatados para impressão.

## 📄 Licença

Este projeto é distribuído sob os termos da licença MIT. Para mais informações, consulte o arquivo LICENSE.

```

```
