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
  
