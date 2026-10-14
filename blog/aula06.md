# Do Espaço à Frequência

Até agora, abordamos o processamento de imagens manipulando diretamente a matriz de pixels no **domínio espacial**. No entanto, existe outro paradigma fundamental na **Computação Visual**: o **domínio da frequência**. 

Exploramos como a **Transformada de Fourier** nos permite decompor uma imagem na soma de senos e cossenos, além de entender os impactos práticos da amostragem, o **Teorema de Nyquist** e o surgimento do **aliasing**.

---

## A Transformada Discreta de Fourier 2D

A premissa estabelecida por Joseph Fourier é que qualquer sinal pode ser expresso como a soma de senos e cossenos de diferentes frequências. No caso de imagens digitais, que são matrizes 2D discretas de tamanho M x N, utilizamos a **Transformada Discreta de Fourier (DFT 2D)** para migrar do domínio espacial para o da frequência.

Ao aplicar a DFT, cada ponto no plano de frequência representa a presença de uma determinada taxa de variação espacial:
* **Baixas Frequências:** Representam regiões homogêneas, com variações suaves de intensidade (como o céu ou uma parede lisa).
* **Altas Frequências:** Representam transições bruscas e detalhes finos (como bordas, contornos e ruídos).

Uma propriedade crucial dessa mudança de domínio é o **Teorema da Convolução**: aplicar uma filtragem por convolução no domínio espacial equivale a uma simples **multiplicação direta** no domínio da frequência.

---

## Filtragem na Frequência

Manipular o espectro de frequências nos dá um controlo direto sobre o aspeto final da imagem:

* **Filtro Passa-Baixa (Low-pass Filter):** Mantém as baixas frequências e atenua as altas frequências. O resultado prático é a suavização ou **borramento (*blur*)** da imagem, já que as bordas e os detalhes finos são removidos.
* **Filtro Passa-Alta (High-pass Filter):** Atenua as baixas frequências e preserva as altas, resultando no realce dos contornos e detalhes.

---

## Teorema da Amostragem de Nyquist-Shannon

Para converter sinais contínuos do mundo físico para o ambiente digital, realizamos os processos de **amostragem** (discretização espacial) e **quantização** (discretização da amplitude).

Segundo o **Teorema de Nyquist**, para conseguir reconstruir perfeitamente um sinal sem qualquer perda de informação, a taxa de amostragem deve ser estritamente superior ao dobro da frequência máxima presente no sinal:

> **Taxa de Amostragem > 2 x Frequência Máxima**

---

## O Problema do Aliasing e o Antialiasing

Quando a taxa de amostragem é insuficiente (subamostragem), ocorre a sobreposição das cópias do sinal no domínio da frequência, gerando o **aliasing**:

* **Aliasing Espacial:** Em imagens digitais, manifesta-se através de serrilhados visíveis em linhas diagonais (*jaggies*), perda de detalhes e padrões falsos de interferência (conhecidos como **Padrão Moiré**).
* **Aliasing Temporal:** Em vídeos, produz ilusões visuais como o *efeito da roda de carroça*, onde a roda de um carro parece girar para trás devido à baixa taxa de captura de quadros.

### Como evitar com o Antialiasing?
Para prevenir o aliasing ao reduzir o tamanho de uma imagem (*downsampling*), aplica-se o **antialiasing**. O processo consiste em passar a imagem por um **filtro passa-baixa (suavização)** *antes* da reamostragem. Ao atenuar previamente as altas frequências que o novo grid de pixels não conseguiria representar, evita-se a criação de artefatos visuais falsos.

---

## Resumo

| Conceito | Descrição | Impacto Visual / Aplicação |
| :--- | :--- | :--- |
| **DFT 2D** | Converte a imagem do domínio espacial para o da frequência | Análise e filtragem baseada em taxas de variação de intensidade |
| **Filtro Passa-Baixa** | Elimina as altas frequências do espectro | Produz borramento/suavização e reduz ruído |
| **Aliasing** | Artefato gerado por subamostragem abaixo do limite de Nyquist | Produz serrilhados (*jaggies*) e padrões Moiré |
| **Antialiasing** | Filtragem passa-baixa aplicada antes do downsampling | Evita a sobreposição de frequências e reduz o serrilhado |

---

A transição entre os domínios espacial e da frequência demonstra como ferramentas matemáticas rigorosas nos permitem entender melhor as limitações do suporte digital e criar algoritmos mais eficientes de processamento de imagem!
