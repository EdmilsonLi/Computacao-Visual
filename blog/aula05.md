# Detecção de Bordas: Derivadas, Filtros Espaciais e o Algoritmo de Canny

Depois de explorar a suavização e a remoção de ruídos no domínio espacial, o próximo passo essencial na **Computação Visual** é entender como destacar as estruturas da imagem. Na aula de hoje, estudamos a **detecção de bordas** (*edge detection*) — um processo fundamental para segmentação, reconhecimento de objetos e interpretação visual por computadores.

---

## 📌 O que é uma Borda?

Do ponto de vista visual, as bordas definem os limites e contornos entre regiões com propriedades distintas de iluminação. Do ponto de vista matemático, uma borda nada mais é do que uma **mudança brusca (descontinuidade)** na função de intensidade dos pixels.

Essas variações costumam ser causadas por mudanças de profundidade, orientação de superfícies, variação de cores ou sombras na cena.

---

## 📈 A Matemática por Trás dos Contornos

Como uma imagem digital é representada por uma matriz de intensidades, podemos analisá-la usando conceitos de cálculo diferencial:

* **Derivada Primeira:** Mede a taxa de variação da intensidade. Ela gera picos (extremos) onde ocorrem as transições de luz.
* **Derivada Segunda:** Avalia a aceleração dessa mudança e apresenta o efeito de **cruzamento em zero (*zero-crossing*)**, que marca o ponto exato da borda.
* **Operador Laplaciano:** É a aproximação discreta da derivada segunda em 2D. Um dos seus kernels clássicos em matrizes 3x3 é:

```text
[  0  -1   0 ]
[ -1   4  -1 ]
[  0  -1   0 ]
```

## 🛠️ Kernels de Gradiente: Roberts, Prewitt e Sobel
Para calcular o gradiente de forma discreta na imagem, utilizamos máscaras de convolução (kernels):

1. Roberts: Focado nas diagonais (45° e 135°), ideal para bordas inclinadas.
2. Prewitt: Avalia variações horizontais e verticais com pesos uniformes.
3. Sobel: Semelhante ao Prewitt, mas concede maior peso ao pixel central da direção analisada, oferecendo uma resposta ligeiramente mais suave a ruídos.

## ⚠️ O Desafio do Ruído
A operação de derivada é extremamente sensível a variações locais. Isso significa que o ruído é fortemente amplificado, gerando bordas falsas.
A solução clássica é aplicar uma suavização prévia com um Filtro Gaussiano antes de extrair os gradientes. Existe aqui um trade-off de escala:

* Filtros pequenos (sigma baixo): Mantêm detalhes finos, mas preservam mais ruído.
* Filtros grandes (sigma alto): Eliminam o ruído e destacam contornos globais, porém desvisibilizam detalhes e borram os contornos.

## 🌟 O Detector de Bordas de Canny
Considerado um dos algoritmos mais eficientes da área, o Detector de Canny resolve esse desafio em quatro etapas encadeadas:

1. Filtragem Gaussiana: Suavização inicial da imagem para remoção de ruídos.
2. Cálculo do Gradiente: Determinação da magnitude e direção das variações de intensidade.
3. Supressão de Não-Máximos: Afina as bordas detectadas, mantendo apenas os pixels que formam o "pico" da variação e zerando os arredores.
4. Limiarização por Histerese: Utiliza dois limiares (inferior L e superior H):
    * Gradientes acima de H viram bordas fortes.
    * Gradientes entre L e H (bordas fracas) só são mantidos se estiverem conectados a uma borda forte.
    * Gradientes abaixo de L são totalmente descartados.

## 📊 Comparativo dos Métodos
| Método | Tipo | Vantagem Principal | Desvantagem / Limitação | 
| - | - | - | - |
| Sobel / Prewitt | Derivada 1ª | Simplicidade e baixo custo computacional | Sensível ao ruído; gera bordas grossas |
| Laplaciano | Derivada 2ª | Detecta a posição exata pelo cruzamento em zero | Muito sensível ao ruído se usado sem pré-filtragem|
| Canny | Algoritmo Multi-estágio | Bordas finas, contínuas e alta imunidade ao ruído | Maior custo computacional e necessidade de ajuste de limiares|

A detecção de bordas reduz drasticamente a quantidade de dados a serem processados em uma imagem, mantendo apenas a informação estrutural.
