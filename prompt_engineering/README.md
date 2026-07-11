# ⚖️ Compliance em IA Generativa no Direito: Framework de Mitigação de Riscos de Alucinação e Governança de Prompt V1.2

---

## 📋 Sumário

1. [Sobre o Projeto](#sobre-o-projeto)
2. [Advertências Obrigatórias](#advertências-obrigatórias)
3. [Protocolo de Validação Humana](#protocolo-de-validação-humana)
4. [Consequências do Uso Indevido](#consequências-do-uso-indevido)
5. [Cláusula de IA Responsável](#cláusula-de-ia-responsável)
6. [Limitações Técnicas Conhecidas](#limitações-técnicas-conhecidas)
7. [Framework do Prompt Anti-Alucinação V1.2](#framework-do-prompt-anti-alucinação-v12)
8. [Exemplo Prático de Uso](#exemplo-prático-de-uso)
9. [Termo de Ciência Unificado](#termo-de-ciência-unificado)
10. [Metodologia de Construção](#metodologia-de-construção)
11. [Fontes e Referências](#fontes-e-referências)
12. [Disclaimer Jurídico](#disclaimer-jurídico)
13. [Cooperação e Desenvolvimento Aberto](#cooperação-e-desenvolvimento-aberto)

---

## Sobre o Projeto

### Por que este projeto existe?

Em 2025, o Tribunal de Justiça de Santa Catarina (TJSC) aplicou multa por litigância de má-fé após identificar o uso de jurisprudências e doutrinas inexistentes em um recurso judicial. O advogado responsável admitiu ter utilizado o ChatGPT de forma inadvertida na elaboração da peça processual.

O caso expôs um problema estrutural crescente: operadores do Direito estão utilizando modelos de Inteligência Artificial Generativa como se fossem bases jurídicas confiáveis, ignorando a natureza probabilística desses sistemas e sua capacidade de produzir **"alucinações"** — informações plausíveis, porém inexistentes ou incorretas.

Este projeto surge como resposta prática a esse cenário.

### Objetivo

Fornecer um framework de engenharia de prompt com grounding jurídico estrito, voltado exclusivamente para:

- extração de informações de documentos fornecidos pelo usuário;
- organização e estruturação textual;
- auditoria de conteúdo;
- mitigação de inferências não suportadas.

### Público-Alvo

- Advogados
- Magistrados
- Promotores
- Procuradores
- Analistas jurídicos
- Compliance officers
- Estudantes de Direito
- Profissionais de Legal Ops e LawTech

---

## ⚠️ Advertências Obrigatórias

> ⚠️ **LIMITAÇÃO CRÍTICA**
>
> Este framework **não realiza pesquisa jurídica autônoma** e não deve ser utilizado como substituto de:
>
> - jurisprudência oficial;
> - doutrina validada;
> - bases primárias de Direito.
>
> Ele foi desenvolvido exclusivamente para:
>
> - extração;
> - organização;
> - estruturação;
> - auditoria textual;
>
> de documentos fornecidos diretamente pelo usuário.
>
> Modelos generativos de propósito geral **não devem ser utilizados como fonte primária autônoma de pesquisa jurídica** sem validação em repositórios oficiais.

### Repositórios Oficiais Recomendados

- STF
- STJ
- TRFs
- TJs
- DJe
- e-SAJ
- PJe
- Jusbrasil (com validação oficial posterior)

### Regra de Ouro do Compliance em IA

> *"A IA sugere. O humano valida. O profissional responde."*
>
> *"Se você não tem tempo para auditar a saída do modelo, não utilize o modelo."*

---

## 🛡️ Protocolo de Validação Humana

### Você é o responsável. Não a IA.

Este framework reduz riscos de alucinação, mas **nenhum modelo de linguagem é infalível**.

A única barreira efetiva entre uma saída plausível e um erro jurídico grave continua sendo a **validação humana qualificada**.

### Protocolo Obrigatório Antes de Qualquer Uso Profissional

| Etapa                          | Ação                                                         |
| ------------------------------ | ------------------------------------------------------------ |
| **1. Auditoria Literal**       | Conferir cada dado extraído diretamente no documento-fonte   |
| **2. Validação Cruzada**       | Verificar jurisprudências, doutrinas, números processuais e fundamentos em bases oficiais |
| **3. Juízo Crítico**           | Avaliar coerência jurídica, contextualização e plausibilidade |
| **4. Proibição de Cópia Cega** | Nunca utilizar a saída da IA sem revisão humana integral     |
| **5. Rastreabilidade**         | Exigir evidência textual correspondente para cada informação extraída |

---

## ⚖️ Consequências do Uso Indevido da IA Generativa

| Âmbito                     | Sanção Possível                                              | Base Legal                              |
| -------------------------- | ------------------------------------------------------------ | --------------------------------------- |
| **Processo Civil**         | Multa por litigância de má-fé                                | Art. 81, CPC                            |
| **Processo Penal**         | Possível responsabilização criminal conforme o caso concreto (ex.: falsidade ideológica, fraude processual ou outros tipos penais aplicáveis) | Arts. 299 e 347, CP                     |
| **Ética Profissional**     | Advertência, suspensão ou processo disciplinar perante a OAB | Estatuto da Advocacia e Código de Ética |
| **Responsabilidade Civil** | Danos materiais e morais decorrentes do uso indevido         | Arts. 186 e 927, CC                     |

### 📌 Observação Técnica

A utilização de fundamentos inexistentes, jurisprudência fictícia ou doutrina fabricada pode caracterizar violação aos deveres de lealdade processual, boa-fé objetiva e diligência profissional.

---

## ⚖️ Cláusula de IA Responsável

### Repartição de Responsabilidades

| Agente                       | Responsabilidades                                            | Não se responsabiliza por                                    |
| ---------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **Criador do Framework**     | Desenvolver técnica de mitigação de alucinação e documentar boas práticas | Uso indevido, ausência de auditoria humana ou aplicação inadequada |
| **Provedor do Modelo de IA** | Disponibilizar tecnologia e informar limitações conhecidas   | Decisões jurídicas tomadas pelo usuário                      |
| **Usuário Final**            | Validação integral, auditoria e responsabilidade profissional pelo uso final | Transferência de responsabilidade para terceiros             |

### Cláusula de Não Responsabilidade

> Este projeto **não oferece garantias**, expressas ou implícitas, quanto à precisão, completude ou adequação jurídica das saídas produzidas por modelos de Inteligência Artificial.
>
> O usuário assume **integralmente todos os riscos** decorrentes da utilização do framework, incluindo sanções processuais, disciplinares, administrativas ou civis.
>
> A alegação de *"erro da IA"* ou *"alucinação do modelo"* **não constitui justificativa válida** perante tribunais, órgãos reguladores ou entidades de classe.

### Ausência de Relação Advogado-Cliente

> Este material possui finalidade **exclusivamente educacional, tecnológica e informativa**.
>
> Sua disponibilização **não constitui**:
>
> - consultoria jurídica;
> - parecer legal;
> - patrocínio processual;
> - relação advogado-cliente.

---

## ⚠️ Limitações Técnicas Conhecidas

Mesmo com técnicas avançadas de engenharia de prompt, permanecem riscos técnicos inerentes aos modelos generativos, incluindo:

- alucinações residuais;
- perda de contexto em documentos extensos;
- inconsistências semânticas;
- falhas de OCR;
- ambiguidades linguísticas;
- variações entre modelos;
- respostas probabilísticas inconsistentes.

**Nenhum framework elimina integralmente os riscos associados à IA generativa.**

---

## 🛡️ Framework do Prompt Anti-Alucinação V1.2

```text
[INÍCIO DO PROMPT]

Função:
Atue como um [Inserir Persona] especializado em [Inserir Subárea Jurídica].

Contexto:
Analise exclusivamente o documento fornecido abaixo.

ATENÇÃO — REGRAS ABSOLUTAS CONTRA ALUCINAÇÃO:

1. Grounding Forçado
Toda resposta deve derivar EXCLUSIVAMENTE do conteúdo textual presente no documento fornecido.

2. Proibição de Inferência
Não deduza, complete, interprete criativamente ou presuma informações ausentes.

3. Regra de Ausência Obrigatória
Caso a informação não esteja expressamente presente no documento, utilize obrigatoriamente:
[NÃO INFORMADO NO DOCUMENTO]

4. Proibição de Pesquisa Externa
Não utilize conhecimento interno do modelo, internet, jurisprudência memorizada ou qualquer fonte externa.

5. Objetividade Estrita
Elimine opiniões, avaliações subjetivas, recomendações não solicitadas e linguagem persuasiva.

6. Regra de Rastreabilidade
Toda informação extraída deve ser acompanhada do trecho literal correspondente do documento-fonte.

7. Auto-Verificação Final
Revise integralmente a resposta e remova qualquer dado que não possa ser localizado textualmente no documento original.

Tarefa:
[Inserir objetivo específico]

Formato de Saída:
[Inserir estrutura obrigatória]

[DOCUMENTO]:
[Cole aqui o documento]

[FIM DO PROMPT]
```

---

## ⚖️ Termo de Ciência Unificado

Ao utilizar este framework, o usuário declara estar ciente e concordar que:

* **Modelos de linguagem de grande escala (LLMs) alucinam** — geram informação falsa com alta aparência de veracidade.
* Este framework mitiga riscos, mas não os elimina.
* A **validação humana é obrigatória**, não opcional, nos termos do protocolo estabelecido.
* A responsabilidade jurídica, ética e profissional pelo uso final da saída é **exclusiva do usuário**.
* O caso **TJSC (2025)** é precedente aplicável: *"uso inadvertido da IA"* não exime o profissional de sanções.

---

## 📚 Metodologia de Construção

Este framework foi desenvolvido com base em:

* Princípios de compliance algorítmico;
* Técnicas de *grounding* e *anti-hallucination*;
* Engenharia de prompt restritiva;
* Governança de IA aplicada ao Direito;
* Análise de falhas reais envolvendo IA generativa no ambiente jurídico.

---

## 🔗 Fontes e Referências

| Norma / Caso                                       | Dispositivo / Relevância                                     |
| :------------------------------------------------- | :----------------------------------------------------------- |
| **Estatuto da Advocacia** (Lei 8.906/94)           | Regula a atividade privativa da advocacia e responsabilidade profissional do advogado. |
| **Código de Ética e Disciplina da OAB**            | Estabelece deveres de veracidade, lealdade processual e vedação a práticas que induzam terceiros a erro. |
| **Marco Civil da Internet** (Lei 12.965/14)        | Define princípios de transparência, responsabilidade e uso da internet no Brasil. |
| **Lei Geral de Proteção de Dados** (Lei 13.709/18) | Regula tratamento de dados pessoais e exige finalidade, adequação e necessidade. |
| **Tribunal de Justiça de Santa Catarina** (2025)   | Caso de sanção processual envolvendo uso de jurisprudência inexistente atribuída ao uso de IA generativa. |

### Links de Referência

* **Caso TJSC — Jurisprudência Falsa Gerada por IA:** [Acessar Comunicado Oficial TJSC](https://www.tjsc.jus.br/web/imprensa/-/tjsc-multa-autor-de-recurso-por-jurisprudencia-falsa-gerada-por-ia)
* **Dossiê Técnico sobre Alucinações em IA no Direito:** [Acessar Artigo Completo na Apolus.ai](https://apolus.ai/blog/alucinacoes-ia-direito-dossie-completo/)

---

## 📌 Disclaimer Jurídico

Este framework constitui ferramenta auxiliar de apoio operacional e **não substitui**:

* Análise jurídica humana;
* Validação profissional;
* Pesquisa em bases oficiais;
* Revisão técnica especializada.

> ⚠️ **Aviso:** O uso responsável da Inteligência Artificial exige supervisão humana permanente, diligência profissional e auditoria documental rigorosa. A responsabilidade final pela utilização da saída produzida permanece exclusivamente com o usuário profissional.

---

## 🤝 Cooperação e Desenvolvimento Aberto

Este projeto está aberto a contribuições da comunidade, nos moldes de práticas comuns em projetos *open source* (ex.: GitHub), incluindo colaboração técnica, acadêmica e profissional.

### São bem-vindas contribuições de:

* Profissionais do Direito;
* Especialistas em Inteligência Artificial;
* Pesquisadores em governança tecnológica;
* Desenvolvedores de LegalTech;
* Instituições acadêmicas.

### Sugestões, revisões e melhorias são especialmente bem-vindas nas seguintes áreas:

1. Redução de riscos de alucinação;
2. Fortalecimento de mecanismos de rastreabilidade;
3. Boas práticas de compliance jurídico;
4. Evolução de engenharia de prompt aplicada ao Direito.

---

> *"O texto foi revisado com apoio de ferramentas de Inteligência Artificial Generativa para ortografia e estruturação textual, sob responsabilidade humana integral."*

**🚨 Você foi advertido.**
