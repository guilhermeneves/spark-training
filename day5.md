# Day 5

Microsoft Hyperspace aplicar camada mais eficiente na gold.

Indice criado pela microsoft para performar no datalake, Pode criar o indice no DeltaLake.

Se a tabela é grande considerar, pois vai criar os indices e replicar os dados, por isso melhor colocar na gold.

## Plano Execução

Como a engine vai processar, cria um plano para executar.

1) Do Driver cria plano de execução e envia para executores é criado Jobs (sequencia de stages)
2) Stages
3) Tasks é executada single thread

![](queryplan.png)

Catalyst Optimizer só foi possível pelo dataframe pois sabia o que era o input. O RDD era um dado não estruturado e por isso não era possivel saber a entrada.

Plano Logico Fisico:
1. Estagio Analysis: Driver recebe e faz esse processo de verificar codigo, catalog, correto, tipagem, binding, verificacoes rapidas, dataframes ja executados, e tenta resolver esse plano logico
2. Plano Logico criado
3. Optimized Logical Plan (Catalyst) aplica algumas regras para melhorar o plano. WholeCodeGenOptimization, pode juntar tudo em uma wholegenstage.
4. Planos Fisicos criados (mais de um plano é criado para avaliação do optimizer)
5. Cost Based Model avalia qual o plano mais efetivo a ser executado. Não o mais rapido mas o que atende maior numero de itens
6. Select Physical Plan
7. Tungsten translate Physical plan to Javabytecode RDD's

## Query Plan Operator

- Code Gen Stage (WholeStageCodegen): Ele está agregando. Isso é bom, caso não tenha pode ser melhorado, 
- Scan (FileScanRDD): Operações que leem as fontes. Filter tenta filtrar direto na memória, isso é bom, quando usa delta, orc, normal ter esse dado. ColumnarToRow (size of files read and number of files) ajuda na conf do spark.
- Exchange: Shuffle, embaralha, movimento dos dados entre os executores. Umas das operações mais custosas. (join, repartition, coalesce (move todo o dado par 1 executor, output of csv), sort)
- Joins: 
    - BHJ: BroadcastHashJoin, troca mensagens dados os executores. abre um tunnel de cópia entre os executores
    - SHJ - One side is 3x Smaller que a média do outro lado. 
    - SortMergeJoin - MostCommon Join

## Adaptative Query Execution [AQE]

spark.sql.adaptative.enabled=true (a partir spark 3)

- CustomShuffleReader: no exemplo spark condensou o resultado em uma partição.

- Coalesce Partition

- Dynamic Switch Join


# Data Products Spotlight

Open

- Apache Kafka
- Apache Pulsar
- Apache Spark
- Apache Airflow
- Apache Pinot (Realtime OLAP ex. data from kafka)
- Trino 
- Dremio (Apache Drill under the hood)
- Yugabyte (Kubernetes postgres and cassandra distributed)

Azure

- Azure Purview (catalog)
- Azure Databricks
- Azure Synapse Analytics

AWS

- AWS MSK
- AWS Glue & DataBrew
- AWS MWAA

Google

- Cloud Data Fusion
- Data Flow (Apache Beam)
- Bigquery