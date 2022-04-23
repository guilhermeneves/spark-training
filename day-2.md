# Spark day-2

- Datalake: James Dixon in 2010, Raw data storage
- Democration of Data - [Unsiloed Data]
- Data structured, unstructred and semi structured.
- Azure (Blob Storage, Azure Datalake Storage Gen2), AWS (S3 & Lake Formation) and GC`- Google Cloud Storage. All comes from hdfs, google file system.
- Datamart - Subset of Decision Support for Departments (Enviesada/tomada de decisão depártamental) / Data Warehouse - Decision Making Support for Enterprise-Level / Data Lake - Raw Data [Source of Truth]

Datawarehouse (inmon,kimball): Data silos created from datamarts, each area has one information.

Geralmente empresas seguem bottom-up Kimball. (Empresas no brasil achavam que datawarehouse iria resolver todos os problemas, mas datamart é enviessado cada área tem o seu)

- Pontos Negativos Datalake.
    - Data Swamp - Disorganized data
    - Data Governance - Management & Control of Data
    - Data Quality - Accurecy and Dataa Veracity
    - Data Security - Protecting Digital Data

### Data Lake [Use-Cases]

better work with ELT, ensure raw data to build later transformation, data warehouse, data mart, etc...

Better access datalake then sources, it's cheaper.

### Lambda Architecture

temos dois caminhos: quente (memoria) e frio (disco)

No Azure poderia ser Data Factory para batch e Event Hub para Stream.

![](azure-batch.png)
![](aws-batch.png)
![](gcp-batch.png)
![](open-batch.png)

## Data Organization Best Practices for Data Lake

Datalake is the main entry (Object Storage - LakeFs, Blobstorage, MinIO, S3, etc...) store objects in bynary scalable

- Raw Ingestion (Landing Zone): Raw without treatment schemaless env. different file formats. é recomendado gerar na forma raw (json, csv, txt) evitar levar processado.
- Transformations (Processing Zone): Files in Queue for Processing Converted & Reconcilied Big Data File Format Processing Engine Area. (Convert to parquet, delta, oprc, hudi, iceberg and dedup and other transform.)
- Business-Level (Curated Zone)

## Spark Lifecycle

Datalake (Raw Ingestion) -> Transform (Spark) -> DataWarehouse (Business Level)

### Storage Solutions for Spark

- Scalability & Performance
- Transaction Support
- Support for Diverse Data Formats
- Support for Diverse Workkload
    - SQL
    - Vatch
    - Streaming
    - ML & AI
- Openness

Data Lakehouses

- Apache Hudi (Uber): created for streaming (Less used)
- Apache Iceberg (Netflix): great for huge tables
- Delta Lake (Databricks): better to integrate with spark

![](deltalake.png)

## Delta Lake [Features]

- ACID Transactions
- Scalable Metadata Handling:Treat metadata just like data, billion of partitions.
- Time travel {Data Versioning}
- Open Format: Everything os parquet
- Unified Batch & Streaming
- Schema Enforcement & Evolution: Schema on Write and Evolution Schema.
- Audit History
- Updates & Deletes: Merge, UPdate and Deletes easily comply GDPR.


## Delta Sharing

Protocol de compartilhamento opensource. Delta Sharing Protocol (DSP)



![](delta_sharing.png )

# Delta Table

It's fast to access table between Delta 10x.

## Databricks

- Cluster:
    - Single Node: Dev/Test not scalable
    - Standard: Most Scenarios / Not good for a lot of jobs running in parallel
    - High Concurrency: Optimized to run concurrent scripts.

    - Runtime version: libs and components (DRV)

    - Autopilot: Autoscaling | Terminated After

    - WOrker and Driver conf.

    - Spot Instance: Save cost but can be required. if you need sla dont use that.

- Databricks have it dbutils
- Databricks CLI to connect.

- Databricks File System, abstração entre storage e spark (dbutils.fs.mount para criar o mount point ao inves de acessar direto o object storage, isso habilita trocar o storage com facilidade.)

Protocolo Azure Data Lake Storage Gen2 [ADSL2] mais rápido para acesso. (abfss instead of wasbs) ~5x: Quando lista o arquivo lista todos os arquivos, o abfss trabalha com bloco atomicos, ele marca a pasta para delecao ou marca ppara outro processo.

## Delta Table Logs

Contains like an index to parquet files and metadata, like min and max to optimize query.

## Strategies to read files 

- Read everything and remove all after load to delta Bronze
- Use streaming ensuring EOS, checkpointlocation

## Python on Cluster

Using python on cluster all program uses only Driver and when createDataframe distribute.

## Pyspark / Koalas / Pandas

Pyspark version > 3.2

import pyspark.pandas as ps

