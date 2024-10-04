# Projeto de Teste de Desempenho com JMeter

Este repositório contém os resultados dos testes de carga realizados em uma aplicação utilizando o [Apache JMeter](https://jmeter.apache.org/). Cada teste foi configurado com diferentes números de threads (100, 500, 1000, 2000, 2999, 3969), e os resultados são apresentados por meio de gráficos agregados, gráficos de latência, e arquivos CSV com o resumo das métricas.

## Estrutura do Repositório

- **assets/**: Contém os gráficos e resumos CSV organizados por tipo de métrica.
- **tests/**: Pasta com os dados brutos de cada teste, incluindo gráficos agregados, latência e arquivos CSV.

## Descrição dos Testes

Os testes de carga foram realizados para medir a performance da aplicação em diferentes níveis de stress, simulando múltiplos usuários simultâneos. Abaixo está uma visão geral dos resultados com base em cada número de threads.

| Threads  | Média (ms) | Min. (ms) | Máx. (ms) | Desvio Padrão | % de Erro | Vazão (req/s) | KB/s  | Sent KB/sec | Média de Bytes |
|----------|------------|-----------|-----------|---------------|-----------|---------------|-------|-------------|----------------|
| 100      | 3176       | 1586      | 5997      | 878.49        | 0.000%    | 15.71         | 107.72| 4.05        | 7021.9         |
| 500      | 7888       | 2281      | 20703     | 2450.74       | 0.000%    | 23.72         | 162.67| 6.12        | 7021.9         |
| 1000     | 6448       | 1190      | 36805     | 4039.88       | 0.000%    | 26.78         | 183.67| 6.91        | 7021.9         |
| 2000     | 23858      | 1033      | 64463     | 12797.92      | 23.600%   | 30.19         | 183.32| 6.86        | 6219.0         |
| 2999     | 38732      | 2090      | 68345     | 17109.98      | 76.559%   | 43.85         | 187.33| 6.68        | 4374.3         |
| 3969     | 45890      | 5132      | 92566     | 5340.19       | 95.742%   | 42.81         | 151.96| 4.90        | 3635.1         |

### Gráficos

#### Gráficos Agregados

Os gráficos agregados mostram a média, tempo mínimo, máximo e desvio padrão de resposta para cada teste de carga. Esses valores ajudam a identificar variações de desempenho e possíveis gargalos. 

#### Gráficos de Latência

A latência média de resposta também foi medida para cada conjunto de threads. Esses gráficos visualizam o tempo que as requisições levaram para retornar ao cliente.

### Sumários CSV

Cada teste gerou um arquivo CSV contendo o resumo detalhado das requisições, como o tempo de resposta, quantidade de requisições bem-sucedidas, falhas, etc. Esses arquivos podem ser baixados e analisados diretamente.

## Análise de Desempenho

### Análise de Erros

Conforme o número de threads aumenta, notamos um aumento significativo na porcentagem de erros:

- **Até 1000 threads**, o sistema conseguiu lidar com a carga sem erros.
- A partir de **2000 threads**, observamos **23.6% de erro**, o que pode indicar uma saturação do servidor.
- Em **2999 threads**, o erro aumentou drasticamente para **76.56%**, sugerindo que o servidor está falhando em lidar com o volume de requisições.
- No teste com **3969 threads**, o erro chegou a **95.74%**, mostrando que o sistema praticamente colapsou sob essa carga.

### Análise de Desempenho

1. **Tempo Médio de Resposta**: Aumenta significativamente com o número de threads, saindo de **3.176 ms** para **45.890 ms** no teste com 3969 threads, indicando que o servidor tem dificuldade em processar grandes volumes de requisições simultâneas.

2. **Desvio Padrão**: Também aumenta drasticamente com o número de threads. No caso de 3969 threads, o desvio padrão foi de **5340 ms**, o que reflete uma variação considerável nos tempos de resposta.

3. **Vazão**: Curiosamente, a vazão (requisições por segundo) aumentou com o número de threads até **2999 threads**, chegando a **43.85 req/s**, mas decaiu levemente para **42.81 req/s** no teste com **3969 threads**, sugerindo que o servidor começa a falhar em processar as requisições de forma eficiente.

### Conclusões

A aplicação testada demonstra bom desempenho com até **1000 threads** sem apresentar erros. A partir de **2000 threads**, o número de erros começa a crescer, atingindo um pico de **95.74%** de falhas com **3969 threads**, sugerindo que a capacidade de processamento do servidor foi ultrapassada. O aumento da **latência** e o **tempo de resposta** indicam que a aplicação não está dimensionada para suportar esse nível de carga.

Esses resultados sugerem que a aplicação pode precisar de otimizações, como balanceamento de carga, aumento de recursos de servidor, ou uso de caching, para melhorar sua performance em cenários de alto volume de acessos simultâneos.
