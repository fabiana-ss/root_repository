# Case Study: Otimização de Criativos Multimodais com IA para a NexusPay 🚀

Este repositório documenta o desenvolvimento estratégico, a engenharia de prompts e a auditoria de qualidade visual (QA) para o lançamento da nova campanha de aquisição da **NexusPay** — uma plataforma SaaS B2B de automação financeira e inteligência de fluxo de caixa focada no mercado brasileiro.

---

Nota: Este é um **projeto fictício** desenvolvido como um estudo de caso para fins de portfólio, simulando um cenário real de mercado.

---

## 1. O Briefing e a Solicitação da Empresa
A diretoria de Growth da **NexusPay** apresentou um desafio de performance: reduzir o Custo por Lead (CPL) na captação de Diretores Financeiros (CFOs) e donos de médias empresas no Brasil. 

Para solucionar essa dor, fomos acionados para entregar **dois ativos visuais principais**:
1. **Criativo A (Mockup Contextualizado):** Imagem em ambiente corporativo de alto padrão (*Premium/High-Ticket*) focada em anúncios de conversão para canais de tráfego pago (Meta Ads e LinkedIn Ads)[cite: 1].
2. **Criativo B (Mockup Isométrico/Flutuante):** Um asset visual limpo, moderno e em camadas para a dobra principal (*Hero Section*) da nova Landing Page do produto[cite: 1].

**Diretrizes de Marca (Brand Kit):** Tons de azul escuro corporativo, cinza grafite e detalhes em verde neon/ciano para guiar os pontos de conversão.

---

## 2. A Estratégia de Growth por Trás do Design
Em mercados B2B tradicionais, o cansaço visual e a "fadiga do fake" (imagens de banco de dados nitidamente artificiais) destroem as taxas de clique (CTR). A nossa abordagem estratégica aplicou:
* **Eye Tracking Simplificado:** O posicionamento e o contraste do dashboard foram projetados para que o CFO bata o olho na peça e entenda a saúde financeira da empresa em menos de 3 segundos.
* **Localização Martech Extrema:** Inserção de dados monetários reais na moeda local (**R$**), menus totalmente traduzidos para o português e cenários que emulam centros financeiros como a Faria Lima (SP), aumentando a confiança e a identificação do lead com o produto.
* **Escala Criativa:** Otimização do pipeline de criação para gerar variações rápidas de público sem perder a consistência estética.

---

## 3. Engenharia de Prompts e Ecossistema de Ferramentas
Para o desenvolvimento deste projeto, adotamos uma política de **Custo Zero de Infraestrutura (Zero-Budget Martech)**, utilizando o poder dos modelos generativos de forma 100% gratuita para gerar o maior ROI possível.

### Criação dos Prompts Base
Os prompts foram estruturados e refinados utilizando a inteligência do **Google AI Studio (Gemini 3.1 Pro)** através do plano de assinatura gratuito. A gigante janela de contexto e a capacidade lógica do modelo foram cruciais para desenhar as variáveis exatas de iluminação, enquadramento e semiótica exigidas pelas campanhas.

### O Pipeline de Testes (Modelos Utilizados de Modo Gratuito):
* ChatGPT (DALL-E 3)
* Manus
* Grok
* SeeDream
* Nano Banana Pro

---

## 4. Matriz de QA e Relatório Comparativo de Modelos

Para garantir que o produto final não apresentasse falhas visuais em telas de alta resolução, rodamos os prompts em todos os ecossistemas gratuitos através de uma **Skill de Auditoria (Agente de QA)** customizada.

### Tabela Comparativa de Performance

| Ferramenta Testada     | Nitidez em Zoom (200%) | Respeito ao Brand Kit |      Legibilidade da UI      |        Desempenho Geral         |
| :--------------------- | :--------------------: | :-------------------: | :--------------------------: | :-----------------------------: |
| **ChatGPT (DALL-E 3)** |       Excelente        |       Excelente       | Altíssima (Localizado PT-BR) | **Líder de Entrega (Aprovado)** |
| **Manus**              |       Excelente        |       Excelente       |             Alta             | **Líder de Entrega (Aprovado)** |
| **Grok**               |        Regular         |          Bom          |            Média             |          Intermediário          |
| **SeeDream**           |    Ruim (Artefatos)    |        Regular        |            Baixa             |            Reprovado            |
| **Nano Banana Pro**    |   Péssimo (Manchado)   |         Ruim          |   Crítica (Texto ilegível)   |         **Ineficiente**         |

### 🔍 Diagnóstico Técnico de Ineficiência (O Caso Nano Banana Pro)
O modelo **Nano Banana Pro** se apresentou como o **mais ineficiente de todos os testados** para a categoria de mockups. A ferramenta gerou severos problemas de renderização:
* As letras da interface gráfica saíram completamente borradas, impossibilitando a leitura dos dados financeiros.
* Elementos estruturais do dispositivo (bordas do notebook) saíram cortados e com artefatos de compressão, eliminando o aspecto *premium* exigido pelo público-alvo da NexusPay.

### 🏆 Os Campeões de Resultado: ChatGPT e Manus
O **ChatGPT** e o **Manus** foram os únicos modelos capazes de processar os prompts criados no Gemini 3.1 Pro mantendo vetores limpos e letras 100% nítidas mesmo sob zoom severo, sendo os escolhidos para os entregáveis finais de produção.

---

## 5. Assets Finais Aprovados

### 📸 Criativo A — Anúncio de Performance (Gerado no ChatGPT)
*Notebook premium posicionado em escritório executivo moderno, exibindo métricas macro, alertas inteligentes de fluxo de caixa em português e saúde financeira (R$).*

![Criativo A - Anúncio](assets/feed_anuncio_final.png) *(Suba a sua imagem correspondente aqui)*

### 📐 Criativo B — Landing Page Section (Gerado no ChatGPT)
*Dashboard flutuante em perspectiva isométrica usando técnica de glassmorphism com módulos de projeção de cenários financeiros destacados sobre fundo minimalista escuro.*

![Criativo B - Landing Page](assets/hero_lp_final.png) *(Suba a sua imagem correspondente aqui)*

---