# Mecanismos de Filtragem Espacial: Do Borramento ao Filtro de Mediana

Após estudarmos as transformações pontuais de intensidade, o avanço natural no **domínio espacial** é considerar não apenas o pixel isolado, mas a sua **vizinhança**. Na aula de hoje sobre **Computação Visual**, exploramos como máscaras de convolução, conhecidas como *kernels* ou janelas de filtragem, atuam sobre a matriz de pixels para suavizar ruídos, destacar detalhes ou transformar a estrutura de uma imagem.

---

## 🎯 Vizinhança, Kernels e a Regra Imutável

Na filtragem espacial, cada pixel da nova imagem é calculado com base em uma região contígua ao seu redor (como uma janela $3 \times 3$). O *kernel* desliza sobre a imagem de entrada e combina os valores dos vizinhos.

Há uma regra fundamental no desenvolvimento desses algoritmos: **a imagem original jamais deve ser sobrescrita durante a varredura**. Como cada cálculo depende da vizinhança original, alterar um pixel *in-place* corromperia o resultado de todos os pixels seguintes. Portanto, o resultado do filtro é sempre gravado em uma nova matriz.

---

## 🌊 Filtros de Suavização (Passa-Baixa)

Os filtros passa-baixa atenuam as altas frequências — que representam transições bruscas de intensidade —, resultando no efeito de **borramento (*blur*)** e na redução de ruídos contínuos.

1. **Filtro da Média (Box Filter):** Substitui o pixel central pela média aritmética dos seus vizinhos (com pesos iguais a $\frac{1}{9}$ em um kernel $3 \times 3$). Aumentar o tamanho da janela (ex.: $5 \times 5$ ou $17 \times 17$) intensifica o nível de suavização.
2. **Filtro Gaussiano:** Utiliza uma média ponderada onde os pixels mais próximos do centro têm maior peso. Isso produz um borramento visualmente mais natural e preserva melhor as estruturas da cena.

---

## 🛡️ Filtros Não-Lineares: O Poder da Mediana

Enquanto a média recalcula a intensidade combinando valores, os filtros de **estatística de ordem** ordenam os pixels contidos na janela e selecionam uma posição específica.

O destaque dessa categoria é o **Filtro de Mediana**:

* **Remoção de Ruído Sal e Pimenta (*Salt-and-Pepper*):** Pontos pretos e brancos isolados afetam drasticamente a média simples, espalhando o ruído pela vizinhança. A mediana, ao ordenar os valores, descarta estes picos extremos de brilho ou escuridão.
* **Preservação de Bordas:** Ao contrário do borramento provocado pela média, a mediana substitui o ruído pelo valor central representativo, eliminando a interferência sem desfoque excessivo dos contornos.

Outros filtros de ordem incluem o **Filtro de Mínimo** (que expande regiões escuras) e o **Filtro de Máximo** (que expande regiões claras/dilatação).

---

## 📊 Síntese dos Filtros Espaciais

| Filtro | Tipo | Operação Principal | Aplicação Prática |
| :--- | :--- | :--- | :--- |
| **Média** | Linear | Média aritmética da vizinhança | Redução geral de ruído e suavização |
| **Gaussiano** | Linear | Média ponderada com distribuição normal | Borramento natural de fundo e pré-processamento |
| **Mediana** | Não-Linear | Seleção do valor mediano ordenado | Remoção de ruído Sal e Pimenta mantendo bordas |
| **Mínimo / Máximo** | Não-Linear | Seleção da menor / maior intensidade | Ajuste morfológico (expansão de sombras/brilhos) |

---

Entender o comportamento dessas janelas de filtragem e a resposta da vizinhança é a base para algoritmos mais complexos que exploraremos a seguir, como detecção de bordas e segmentação de objetos!
