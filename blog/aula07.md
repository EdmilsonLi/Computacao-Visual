# O Pipeline Gráfico

Dando continuidade aos nossos estudos em **Computação Visual**, a aula de hoje concentrou-se em entender o caminho percorrido por uma cena tridimensional até se transformar na imagem bidimensional exibida no ecrã. Esse fluxo sequencial de operações é conhecido como **pipeline gráfico** (ou pipeline de renderização).

---

## Arquitetura e Gargalos da Pipeline

O pipeline funciona como uma linha de montagem industrial dividida entre o processamento central e o processamento paralelo da placa gráfica:

~~~
[ Cena 3D ] ➔ (1. Aplicação - CPU) ➔ (2. Processamento Geométrico - GPU) ➔ (3. Rasterização - GPU) ➔ (4. Processamento de Pixels - GPU) ➔ [ Imagem Final ]
~~~

* **Gargalo de Desempenho (*Bottleneck*):** Como os dados fluem sequencialmente de um estágio para o outro, a velocidade global de renderização é sempre limitada pelo estágio mais lento do sistema.

---

## As Matrizes MVP e o Processamento Geométrico

1. **Model (Modelo):** Converte as coordenadas do espaço local de cada objeto para o espaço global (mundo) da cena.
2. **View (Visualização):** Transforma as coordenadas globais para o referencial da câmera virtual.
3. **Projection (Projeção):** Converte o volume 3D utilizando projeções **Perspectivas** (que simulam a visão humana com pontos de fuga) ou **Ortogonais** (sem distorção de profundidade, usadas em CAD).

Após a aplicação do MVP, ocorrem o recorte (*clipping*) de geometrias fora do *frustum* da câmera e o mapeamento de tela (*viewport mapping*).

---

## Gestão de Memória e Buffers Auxiliares

Para garantir a coerência visual e evitar falhas de renderização, a GPU utiliza uma série de buffers de apoio:

* **Z-Buffer (Depth Buffer):** Armazena a profundidade de cada pixel em relação à câmera, permitindo resolver corretamente a oclusão (objetos à frente tapam os de trás).
* **Double Buffering:** Utiliza dois buffers alternados (*front buffer* e *back buffer*). Enquanto o quadro atual é exibido na tela, o próximo é desenhado em segundo plano, eliminando oscilações e o efeito de *screen tearing*.
* **Outros Buffers:** O **Canal Alpha** gere a transparência (*blending*), o **Stencil Buffer** atua como máscara de recorte, e o **Accumulation Buffer** permite efeitos como *motion blur* e profundidade de campo.

---

## Síntese dos Componentes Gráficos

| Componente | Função Principal |
| :--- | :--- |
| **Primitiva Básica** | O triângulo (formado pela conexão de vértices e arestas) |
| **Câmera Virtual** | Definida por posição, direção, vetor *up*, FOV e planos de corte (*Near*/*Far*) |
| **Shading vs. Shadow** | *Shading* calcula o tom/cor da superfície; *Shadow* projeta as sombras |
