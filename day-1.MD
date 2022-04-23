# Spark day-one

## Apache Hadoop [Fundamentals] (2001 - 2010)

Collection of open-source software.

- HDFS (Distributed file system) Use of commodity machines
    - Store Replicas of Data Blocks
    - Default Replication Factor is 3
    - Default block Size is 128MB
- MapReduce
    - Java lib to process HDFS data. *Parallel & Distributed Algorithm
    - Compiled before execution
- YARN - Managing Computing Resources
    - Central Resource Manager with Containers
    - DYnamically Allocate Pools of Resources

### Ecosystem of Hadoop Anial Zoo [2006 ~ 2014]

In the past there were need to use all these tech to do big data.

![](hadoop.png)

### History of Apache Hadoop & Apache Spark

- 2002: Douglas Cutting - Starting Working on Nutch
- 2003: Google Published MapuReduce Paper
- 2004: Google Published GFS (Google File System) Paper
- 2005: Nutch GFS & MapeReduce Support
- 2006: Google (Doug Cutting) shared the Hadoop to the community. Yahoo brings tge technology and scale it.
- 2008: Hadoop wins the world record system fastest in the worls (yahoo)
- 2009: Cloudera founded by Doug Cutting
- 2010: Yahoo and Facebook adoption
- 2011: Facebook, Linkedin, and other adopted (Lambda Archicteture - Nathan Marz Software Engineer at Twitter (cold and hot process))
- 2014: Apache Spark Top Level ASF (It was born as max priority) (Kappa Architecture Jay Kreeps Principal Staff Engineer)
- 2017: Less release haddop
- 2018: Dataframe & Dataset API Unified (Apache Spark 2.0 Released)
- 2019 - 2022: Apache Spark dominate the market and hadoop is not updated anymore.

## Big Data-as-a-Services [BDaaS]

It was difficult to create and configure a cluster, cloud creates cluster self service, and then Cloudreads lost the market share by firstly amazon emr and then google dataproc and azure hdinsight.

Cluster Dataproc takes 90 seconds to provision different from amazon 20min and azure hdinsight


## Data Processing Engines [TimeLine] ~Azure

![](azure-spark.png)


## Spark Services UI (Cloud)

- Azure Data Factory Mapping Data Flows (Spark encapsulated)
- AWS Glue (Spark Encapsulated)
- Cloud Data Fusion (Spark Encapsulated)

## Apache Spark [Fundamentals]

- Open-Source Distributed Cluster-Computing Framework, different from Kafka that was built for memory storage.
- Written in Scala
- Implicit Data Parallelism & Fault Tolerance
- 100x MapReduce Jobs & 10x - Disk Based Operations

### Spark History

- University of California, Berkeley's AMPLab
- Open-Sourced in 2014 - Top-Level Apache Project
- Databricks - New World Record in Large Scale Sorting [2014]
- Ali Ghodsi | Reynold Xin | Matei Zaharia - Databricks
- 1000 contributors in 2015
- RDD and Spark Streaming marked as deprecated (It was marked as low level API)
- Spark-SQL DataSets & DataFrames - Processing Structured Data
- Structured Streaming - Processing Structred Data Streams
- Core APIS: SQL, Java, Scala, Python, C#, etc... (Performance is the same because of the API)


# Apace Spark Components

Spark is a tool in and out, collect data process and output.

- Spark Application: 
- Spark Driver: (parse, binding, plano de execução)
- Spark Session: 
- Cluster Manager:

![](spark-componentes.png)


## Deployment

- Local (Not distributed everything together)
- Standalone (Separated JVM's Executor, Master, etc..) ** Better to use YARN
- Yarn Runs with YARN (Cluster) Application Master
- Kubernetes (Runs in a Kubernetes Pod) Each Workers Runs Within a Pod Context, use Kubernetes Master for Cluster Management.) Google Dataproc uses Kubernetes by default

# Partition

- 1 thread per partition
- generally fixed size 128mb per partition (s3, blob storage can be different)
- Small files will fill the partition
- Big files greater than partition will cause delay to break the file and distribute.


![](types.png)

Use DataSet when does not have standard connection. (Very rare)

## Types

RDD
- Not Recommended Approach
- Without Query Optimization using Catalyst
- Without Whole Stage Code Generation (Spark pegar conjunto de transformações e cria um chunk de código, faz o processo ser mais rápido)
- High GC Overhead
- For Apache Spark 1.X Legacy API's

DataSets

- Good in Complex ETL Pipelines
- Not good Aggregations
- Use only to develop connectors very rare

DataFrame
- Use for everything


## Logs

spark.sparkContext.setLogLevel("WARN")

## Spark-on Kubernetes

Google donate to the community spark operator.

Utilizar Imagem gcr.io/spark-operator
para criar um container da applicação.

Mascaramento de secrets pode ser feito atraves de uma secret criada no proprio kubernetes e chamar essa secret