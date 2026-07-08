# Prática 01: Pré-processamento e Limiarização de Imagens Industrial

**Estudante:** Fabiana S.S
**Curso:** Inteligência Artificial / Visão Computacional - SENAI  
**Data:** Maio de 2026

---

## 1. Contextualização e Objetivo
No ambiente industrial, as imagens capturadas por câmeras em bancadas de testes ou linhas de produção frequentemente sofrem com variações de iluminação, sombras e ruídos digitais. Antes de submeter essas imagens a um modelo de Deep Learning ou detector de bordas, é mandatório realizar o pré-processamento.

O objetivo desta prática é aplicar técnicas fundamentais de Visão Computacional usando **OpenCV**, **NumPy** e **Matplotlib** para tratar e binarizar a imagem de um componente, isolando a região de interesse (objeto) do plano de fundo.

---

## 2. Análise Técnica das Etapas Implementadas

### 2.1. Conversão de Espaço de Cores (BGR para RGB e Cinza)
* **BGR para RGB:** Por padrão, o OpenCV carrega imagens no canal BGR. Para que a exibição no Matplotlib não ficasse com as cores invertidas, aplicou-se a conversão para RGB.
* **Escala de Cinza:** A conversão para tons de cinza (`cv2.COLOR_BGR2GRAY`) reduz a dimensionalidade da imagem (de 3 canais de cor para apenas 1 canal de intensidade de luminosidade). Isso otimiza o processamento computacional e elimina informações de cor que não influenciam na geometria do componente.

### 2.2. Filtragem Espacial (Suavização Gaussiana)
Para reduzir ruídos de alta frequência (pequenos pontos espalhados ou imperfeições na captura), aplicou-se o filtro **GaussianBlur**. Ele calcula uma média ponderada dos pixels vizinhos baseada em uma distribuição gaussiana, atenuando ruídos e preparando a imagem para uma binarização mais limpa.

### 2.3. Limiarização (Binarização): Simples vs. OTSU
A binarização transforma a imagem em preto e branco (0 e 255):
1. **Limiarização Simples (`cv2.THRESH_BINARY`):** Utiliza um valor de corte (threshold) fixo definido manualmente. Se o pixel for maior que o corte, vira branco; se for menor, preto. **Limitação:** Não se adapta a mudanças de iluminação do ambiente.
2. **Limiarização de OTSU (`cv2.THRESH_OTSU`):** É um algoritmo de limiarização automática. Ele analisa o histograma da imagem em escala de cinza e calcula o limiar ideal que minimiza a variância dentro de cada classe (fundo e objeto), separando-os de forma dinâmica e inteligente.

---
## 3. Interpretação dos Resultados e Conclusões

Ao analisar o painel comparativo gerado pelos subplots, as seguintes conclusões foram obtidas:

* **Efeito da Suavização:** O filtro Gaussiano foi eficiente em remover granulados da imagem original, o que evitou que "fantasmas" ou ruídos isolados fossem binarizados incorretamente nas etapas seguintes.
* **Desempenho dos Limiares:** A limiarização simples mostrou-se muito dependente do valor estático escolhido. Já o **Método de OTSU** apresentou um resultado visivelmente superior, pois conseguiu mapear o histograma global da imagem e determinar o ponto exato de transição entre o componente industrial e o fundo da bancada de testes.
* **Limitações Encontradas:** Variações extremas de iluminação (como reflexos diretos no metal do componente ou sombras projetadas) ainda representam um desafio, pois alteram o valor dos pixels fazendo com que partes do objeto sejam interpretadas como fundo (falsos negativos). Como melhoria futura, sugere-se o teste de algoritmos de **Limiarização Adaptativa**, que calculam limiares diferentes para cada região da imagem.
 --- 
# Desafio 01 - SA: Detecção e Classificação de Objetos com OpenCV
**Estudante:** Fabiana dos Santos da Silva  
**Curso:** Inteligência Artificial / Visão Computacional - SENAI  
**Data:** Junho de 2026

---

## 1. Descrição do Cenário e Objetivo
Este projeto simula um sistema de triagem visual em uma linha de produção industrial para classificar componentes (como porcas e parafusos). 

O objetivo é estruturar um pipeline prático de Visão Computacional que use técnicas de processamento de imagem e extração de características geométricas para detectar e categorizar automaticamente os objetos de forma automatizada.

---

## 2. Pipeline de Pré-processamento
Para isolar os objetos do plano de fundo, aplicamos as seguintes etapas na imagem original:
1. **Conversão para Tons de Cinza (`cv2.cvtColor`):** Reduz a complexidade de 3 canais de cor para 1 canal de intensidade.
2. **Suavização Gaussiana (`cv2.GaussianBlur`):** Filtro com kernel $5 \times 5$ para eliminar ruídos e imperfeições de captura.
3. **Limiarização Invertida de Otsu (`cv2.threshold`):** Binarização automática que calcula o melhor limiar para transformar os objetos em branco (255) e o fundo em preto (0).
4. **Operações Morfológicas de Fechamento (`cv2.morphologyEx`):** Preenche eventuais buracos ou sombras internas para consolidar a massa do objeto.

---

## 3. Detecção e Extração de Características
Utilizando a função `cv2.findContours`, o algoritmo mapeia os limites externos de cada peça detectada. A partir de cada contorno, extraímos métricas quantitativas:
* **Área (`cv2.contourArea`):** Total de pixels da peça.
* **Perímetro (`cv2.arcLength`):** Comprimento da borda.
* **Aspect Ratio (Razão de Aspecto):** Relação entre a altura e largura da caixa delimitadora (`Bounding Box`), usada para diferenciar objetos alongados de objetos simétricos.
* **Cor Média (`cv2.mean`):** Intensidade de cor sob o contorno da peça.

---

## 4. Regra de Classificação (Lógica de Negócio)
A categorização dos objetos foi programada através de regras de decisão geométricas:
* **Parafuso:** Identificado se a razão entre a altura e largura for alongada (aspect ratio alto) ou se a área for compatível com o comprimento esperado da peça.
* **Porca:** Identificada se apresentar formato mais simétrico/compacto (aspect ratio próximo a 1.0) e dimensões de área específicas.
* **Ruído/Descarte:** Áreas muito pequenas que ficam abaixo do limite de corte mínimo de pixels estabelecido.

---

## 5. Relação Teórica com Redes Neurais Convolucionais (CNNs)
Embora a abordagem com OpenCV clássico e regras manuais seja rápida e funcione muito bem para cenários controlados (como este projeto), ela se torna limitada se os objetos mudarem de ângulo, sofrerem oclusão parcial ou se a iluminação da fábrica oscilar.

Em sistemas mais complexos, uma **Rede Neural Convolucional (CNN)** automatiza esse processo: ela aprende a extrair seus próprios mapas de características visuais (bordas, texturas, formas e profundidade) diretamente através de suas camadas convolucionais durante o treinamento supervisionado, garantindo uma classificação muito mais robusto, adaptável e inteligente a variações do mundo real.

---

## 6. Análise de Limitações e Melhorias Futuras
* **Limitações:** Sombras projetadas no fundo podem se fundir com os contornos dos objetos, alterando o cálculo real da área. Objetos encostados ou sobrepostos são lidos como uma única peça grande.
* **Melhorias:** Utilização de limiarização adaptativa para ambientes com iluminação variável e aplicação do algoritmo *Watershed* para separar fisicamente objetos que estejam se tocando na esteira.

---
**Referências:**
* Documentação OpenCV - Contours & Image Processing (docs.opencv.org)
* Material de Estudos SENAI - Módulo de Visão Computacional e Deep Learning 2026.
