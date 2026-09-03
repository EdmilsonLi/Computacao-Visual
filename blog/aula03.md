# Transformações de Intensidade no Domínio Espacial

Depois de entender como as imagens são armazenadas, o próximo passo na disciplina foi aprender a modificá-las. Hoje exploramos o **domínio espacial**, aplicando funções matemáticas direto no nível do pixel para alterar iluminação e contraste. 

Dentre as técnicas abordadas, as **transformações de intensidade** (ou processamento ponto a ponto) destacam-se pela simplicidade e eficiência, o novo valor de um pixel $s$ depende exclusivamente do valor original $r$, mapeado por uma função $s = T(r)$, sem considerar os pixels vizinhos.

Dois operadores matemáticos se destacam na forma como alteram a percepção de claro e escuro em uma imagem: a **Transformação Logarítmica** e a **Lei de Potência**.

---

## 🔍 Transformação Logarítmica

Representada pela equação $s = c \cdot \log(1 + r)$, essa função possui um comportamento bem específico:
* **Expande os tons escuros:** "Estica" as baixas intensidades, tornando visíveis os detalhes em áreas de pouca iluminação.
* **Comprime os tons claros:** Suaviza a variação nos picos de luz.

Essa técnica é essencial para visualizar dados com alta variação dinâmica, como o **Espectro de Fourier**, onde a amplitude dos valores varia drasticamente (de $0$ a $10^6$) e uma exibição linear comum esconderia quase todos os detalhes.

---

## 🎛️ Transformação de Potência (Lei de Potência / Gama)

Modelada pela fórmula $s = c \cdot r^\gamma$, o parâmetro $\gamma$ (gama) define como a curva de iluminação se comporta:
* **$\gamma < 1$:** Clareia a imagem de forma seletiva, útil para recuperar fotos subexpostas ou muito escuras.
* **$\gamma > 1$:** Escurece a imagem, sendo útil para ajustar fotos "lavadas" ou com excesso de brilho.

Além do realce estético, a **correção gama** é indispensável para calibrar monitores e sensores físicos, compensando as distorções não lineares inerentes aos próprios displays.

---

## 📊 Resumo das Transformações

| Transformação | Equação | Comportamento Principal | Aplicação Típica |
| :--- | :--- | :--- | :--- |
| **Logarítmica** | s = c &middot; log(1 + r) | Expande tons escuros e comprime tons claros | Visualização do Espectro de Fourier |
| **Gama (&gamma; &lt; 1)** | s = c &middot; r<sup>&gamma;</sup> | Clareia a imagem esticando as sombras | Fotos subexpostas / escuras |
| **Gama (&gamma; &gt; 1)** | s = c &middot; r<sup>&gamma;</sup> | Escurece a imagem comprimindo as sombras | Fotos super-expostas / "lavadas" |

Manipular a intensidade pixel a pixel demonstra como funções matemáticas simples conseguem transformar completamente a qualidade visual e a interpretação de uma imagem digital.
