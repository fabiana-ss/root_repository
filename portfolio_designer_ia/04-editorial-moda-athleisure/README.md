# Projeto Editorial de Moda Fitness — "Urban Activewear"

**Estudo de Caso de IA Design & Growth Marketing (Projeto Fictício)**

**IA Designer & Marketing Growth:** Fabiana S.S

**Direção de Arte & Estratégia:** Creative Director & Growth Lead

**Vaga Alvo:** Designer e Social Media focado em IA, Canva para edição de vídeo.
## 📢 Disclaimer de Projeto Fictício

*Este é um projeto de demonstração técnica e portfólio profissional. Todos os ativos visuais, conceitos de marca, modelos humanas e dados de conversão apresentados foram gerados através de ferramentas avançadas de Inteligência Artificial e pós-produção manual. Nenhuma marca real ou pessoa física real foi utilizada para fins comerciais.*
## 🎯 1. Conceito da Campanha: "O Novo Elegante"

O mercado de vestuário fitness de alto padrão (*high-ticket*) demanda muito mais do que fotos comuns de academia. Marcas líderes como *Alo Yoga* e *Lululemon* vendem um estilo de vida que une **sofisticação estética, força física e conforto urbano**.

A campanha **"Urban Activewear — O Novo Elegante"** foi desenhada para o Instagram, dividida estrategicamente entre o posicionamento de marca (Feed) e anúncios de conversão de alto impacto (Stories/Ads).

### Pilares Verbais (Copywriting):

- **"A beleza está na força"** (Conceito Estático/Editorial): Foca na presença, na musculatura definida e no empoderamento estático.
- **"Elegância em movimento"** (Conceito Dinâmico/Lifestyle): Foca na fluidez, na rotina ativa urbana e na liberdade física.

  ## 🛠️ 2. O Pipeline Técnico (Ferramentas & Integração)

Para alcançar consistência de modelo, realismo têxtil e tipografia editorial impecável, estruturamos um fluxo integrado utilizando três ecossistemas de tecnologia:
Para integrar o ChatGPT (DALL-E 3) na fase inicial de geração de imagens base e manter a estrutura visual solicitada, aqui está a atualização do pipeline:

Aqui está o fluxo técnico completo, integrando as quatro ferramentas conforme solicitado:

```
┌────────────────────────┐     ┌────────────────────────┐     ┌────────────────────────┐     ┌────────────────────────┐
│   ChatGPT (DALL-E 3)   │ ──> │     Gemini Vídeo       │ ──> │         Canva          │ ──> │          GIMP          │
├────────────────────────┤     ├────────────────────────┤     ├────────────────────────┤     ├────────────────────────┤
│ Geração de imagens base│     │ Criação das cenas A, B │     │ Edição e Montagem das  │     │ Ajuste de texturas,    │
│ com consistência de    │     │ e C com animação e     │     │ cenas e finalização    │     │ remoção de cicatrizes  │
│ modelo (modelo_ia)     │     │ fluidez narrativa      │     │ do vídeo               │     │ e de marcas d'água     │
└────────────────────────┘     └────────────────────────┘     └────────────────────────┘     └────────────────────────┘

```

### Detalhamento do Pipeline

* **Geração com ChatGPT (DALL-E 3):** Responsável pela criação das bases fotorrealistas, garantindo a consistência dos traços faciais da `modelo_ia` e a fidelidade aos elementos visuais.
* **Criação de Cenas no Gemini Vídeo:** Transformação das imagens estáticas em movimento, desenvolvendo as cenas A, B e C com foco em continuidade e fluidez narrativa.
* **Edição e Finalização no Canva:** Etapa de montagem, onde as cenas são sequenciadas, recebem ajustes de *timing*, transições e elementos gráficos para consolidar o ritmo editorial.
* **Pós-Produção no GIMP:**
* **Remoção de Artefatos:** Limpeza de elementos indesejados ou marcas d'água através da ferramenta **Clonar**.
* **Texturização:** Aplicação de camada cinza $50\%$ em modo Sobrepor (*Overlay*) com ruído RGB para restaurar a textura natural.
* **Tratamento de Pele:** Uso de **Separação de Frequências** para mesclar arestas e corrigir imperfeições decorrentes de processos de *Face Restore*.

---

## 📈 3. Distribuição dos Ativos no Funil de Conversão (Growth Strategy)

Para maximizar o retorno financeiro sobre o investimento em anúncios (ROAS), distribuímos os três criativos principais em diferentes etapas do funil de vendas do Instagram:

### 🏆 Criativo 1: `feed_principal.jpg` (Meio de Funil / Consideração)

- **Formato:** Feed Retrato ($1080 \times 1350$ pixels)
- **Design:** Fonte Serifada fina, cor oliva-acinzentada integrada perfeitamente à sombra da parede de concreto. Visual minimalista, limpo e editorial.
- **Estratégia de Growth:** Focado no público que já teve contato com a marca. A pose estática, o olhar confiante direcionado à câmera e a headline "A beleza está na força" geram conexão humana profunda, aumentando o tempo de permanência no post (métrica crucial do algoritmo do Instagram).

### 🚀 Criativo 2: `stories_anuncio.jpg` (Fundo de Funil / Retargeting de Performance)

- **Formato:** Stories/Reels ($1080 \times 1920$ pixels)
- **Design:** Dupla exposição com silhueta estendida ao fundo, tipografia robusta sem-serifa em alto contraste (branco e oliva).
- **Estratégia de Growth:** Anúncio pago (Meta Ads) direto ao ponto. A composição de dupla exposição e a fonte bold geram um efeito imediato de *Thumb Stop* (faz o usuário parar de passar os Stories). Excelente para campanhas de remarketing oferecendo cupons de primeira compra.

### ☀️ Criativo 3: `variante_b.png` (Topo de Funil / Prospecção Fria)

- **Formato:** Feed ou Stories Dinâmico
- **Design:** Modelo em corrida real na estrada costeira sinuosa, contra-luz dourado natural (*Rim Light*), tipografia com rastro dinâmico que simula o vento e movimento.
- **Estratégia de Growth:** Atração de novas clientes. A imagem evoca o desejo de pertencer àquela rotina elegante. A estrada em curva guia o olhar do usuário do topo até o conjunto esportivo de forma orgânica.

## 🧪 4. Desenho Técnico do Teste A/B (Mídia Paga)

O teste A/B permite comprovar cientificamente qual criativo traz mais resultado financeiro com o menor custo de veiculação.

```
                      ┌────────────────────────────────────────┐
                      │          CAMPANHA META ADS             │
                      │  Público-Alvo: Mulheres 25-45, Fitness │
                      └──────────────────┬─────────────────────┘
                                         │
                 ┌───────────────────────┴───────────────────────┐
                 ▼                                               ▼
┌─────────────────────────────────┐             ┌─────────────────────────────────┐
│      VARIAÇÃO A (CONTROLE)      │             │     VARIAÇÃO B (DESAFIANTE)     │
├─────────────────────────────────┤             ├─────────────────────────────────┤
│ • Imagem: feed_principal.jpg    │             │ • Imagem: variante_b.png        │
│ • Foco: Conexão, Força, Estático│             │ • Foco: Movimento, Aspiração    │
│ • Headline: A beleza na força   │             │ • Headline: Elegância movimento │
└─────────────────────────────────┘             └─────────────────────────────────┘
```

### Hipótese de Growth:

> *"A Variação B (Movimento/Lifestyle ao ar livre) alcançará um CTR (*$Click-Through\ Rate$*)* $+25\%$ *maior do que a Variação A (Estúdio/Estático) para públicos frios, pois reduz o aspecto de anúncio invasivo e se camufla como conteúdo nativo de influenciadoras de bem-estar."*
> 

### Matriz de Métricas do Projeto:

- **Métrica Primária:** $CTR\ (Click-Through\ Rate)$ — Mede o poder de atração e cliques de cada criativo.
- **Métrica Secundária:** $CPA\ (Custo\ por\ Aquisição)$ — Avalia a qualidade do público atraído por cada anúncio (efetivação de compra no checkout).

