[README.md](https://github.com/user-attachments/files/32198687/README.md)
#  Rota Inteligente: Otimização de Entregas com Algoritmos de IA

> **Disciplina:** Artificial Intelligence Fundamentals  
> **Empresa Fictícia:** Sabor Express  
> **Tecnologias:** Python, Google Colab, NetworkX, Scikit-Learn, Pandas, Matplotlib  



## 1. Descrição do Problema e Desafio

A **Sabor Express** é uma empresa local de delivery de alimentos que enfrenta gargalos operacionais durante os horários de pico (almoço e jantar). A definição manual e empírica das rotas de entrega resultava em atrasos, trajetos ineficientes, aumento no consumo de combustível e insatisfação dos clientes.

**Objetivo:** Desenvolver um sistema inteligente capaz de:
1. Agrupar entregas por proximidade geográfica para distribuir a demanda entre a frota de entregadores.
2. Calcular rotas otimizadas de menor distância e tempo para cada grupo, abstraindo a malha viária urbana como um **Grafo Ponderado**.



##  2. Abordagem Adotada e Arquitetura da Solução

A solução foi estruturada em duas camadas principais de Inteligência Artificial:

[ Pedidos Pendentes (X, Y) ]
│
▼
┌─────────────────────────┐
│  K-Means Clustering     │ ──> Divisão Geográfica em Zonas/Entregadores
└─────────────────────────┘
│
▼
┌─────────────────────────┐
│  Algoritmo A* (Busca)   │ ──> Traçado da Menor Rota em Grafo Ponderado
└─────────────────────────┘
│
▼
[ Rotas Otimizadas & Métricas ]


1. **Grafo Urbano:** A cidade fictícia foi modelada com 8 bairros/nós e 10 conexões de ruas (arestas) ponderadas por distância geométrica (km).
2. **Camada 1 — Aprendizado Não Supervisionado (K-Means):** Utilizou as coordenadas cartesiana $(X, Y)$ dos pontos de entrega para dividir $N$ pedidos em $K=2$ zonas otimizadas de atendimento.
3. **Camada 2 — Busca Heurística (Algoritmo A*):** Para cada zona, o algoritmo A* determinou a menor sequência de vias utilizando a distância euclidiana em linha reta como função de avaliação heurística ($f(n) = g(n) + h(n)$).



## 🛠️ 3. Algoritmos Utilizados

* **K-Means:** Algoritmo de clustering não supervisionado que identifica centros de gravidade em conjuntos de dados posicionais e atribui cada ponto ao cluster mais próximo.
* **A\* (A-Estrela):** Algoritmo de busca informada para grafos que combina o custo acumulado da rota real ($g(n)$) com a estimativa heurística ($h(n)$) do ponto atual até o destino.



##  4. Modelo do Grafo e Visualização das Rotas

Abaixo está a representação gráfica do mapa viário da cidade e das rotas calculadas para cada entregador:

![Rotas Finais Otimizadas](output/rotas_finais_otimizadas.png)

---

##  5. Análise dos Resultados e Eficiência

Comparação entre a **Estratégia Manual (1 Entregador sem ordenação)** e a **Estratégia Otimizada (2 Entregadores com IA)** para um lote de 6 entregas simultâneas:

| Métrica de Desempenho | Estratégia Manual (Sem IA) | Estratégia IA (K-Means + A*) | Ganho / Impacto |
| :--- | :---: | :---: | :---: |
| **Entregadores Alocados** | 1 | 2 | Distribuição de carga |
| **Distância Média por Entregador** | 30.16 km | 25.48 km | **-15.5%** por veículo |
| **Tempo Máximo de Atendimento** | 60.3 min | 55.2 min | **8.5% mais rápido** |
| **Equilíbrio Operacional** | Nulo (1 veículo) | Balanceado (Cluster 0 e 1) | Operação em paralelo |



##  6. Limitações da Solução

* **Arestas Estáticas:** O grafo considera distâncias fixas e não inclui variações de trânsito em tempo real ou bloqueios viários.
* **Capacidade de Carga:** Não foram inseridas restrições de volume de bagagem ou peso das mochilas dos entregadores.
* **Janelas de Tempo Fixo:** Não foram contemplados horários limite agendados individualmente por cada cliente.



##  7. Sugestões de Melhoria Futura

1. **Grafos Dinâmicos:** Integração de pesos variáveis nas arestas para simular congestionamentos urbanos em tempo real.
2. **Algoritmos Genéticos ou Meta-heurísticas (VRP):** Evoluir o roteamento para resolver o Problema de Roteamento de Veículos com Janela de Tempo (VRPTW).
3. **Interface Visual Interativa:** Construção de uma aplicação web (usando Streamlit) para que o gerente do restaurante visualize os entregadores em um mapa dinâmico.



##  8. Estrutura do Repositório

```text
rota-inteligente-sabor-express/
│
├── README.md                  # Documentação do projeto
├── Rota_Inteligente_IA.ipynb  # Notebook executável no Google Colab
│
├── data/                      # Datasets fictícios em CSV
│   ├── bairros_coordenadas.csv
│   ├── pedidos_entregas.csv
│   └── metricas_comparativas.csv
│
└── output/                    # Gráficos e resultados visuais
    └── rotas_finais_otimizadas.png
