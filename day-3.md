# Event Stream

- É continuo e explicitamente ordenado, o que não acontece com batch que precisa ser ordenado.

- É imutável: transações logs, movimentações, novo eventos nos offsets.

- Eventos podem ser repetidos, consigo ler do inicio ao fim novamente.


É possível refatorar um serviço para event-driven.

Confluent Cloud entrega: KSQLDB, Schema Registry, Kafka Connect, além de estarem estudando entregar Zookeeperless

## Python Streaming Events Engines

- Apache Flink
- Apache Spark
- Faust, pode rodar no K8S até recomendado, no Faust não consigo fazer join entre streams, limitado a python.

KSQL entra mais como engine SQL e não é SQL ANSI.

perguntas: 
- Existe join entre streams? (corta Faust)
- Trabalha com SQL?
- Multiplos joins no mesmo processamento (corta o spark, pois apenas um join escreve resultado)

## SQL Streaming Engine

- Apache Flink (Flink SQL)
- Apache Spark (Structured Streaming)
- Apache Kafka (KSQL)
- Apache Beam (Beam SQL) - Dataflow é apache beam recomendado para GCP.

Necessário sempre janela para join em todos os cases.

## Message Delivery Guarantees [Idempotent Producers & EOS]

Idempotent = Producer to avoid duplicated

## The log structure


- Dentro do Evento eu Tenho Topico Particao e Timestamp
- Zero-Copy - Copy from Disk Buffer to Network Buffer, não tem buffer de CPU. Se habilitado SSL desabilita o zero-copy.

Topic & PArtition

Parititoning Strategy producer: Without ley - round robin else key.

## Spark Structured Streaming

Spark works microbatch (EOS) min 100ms Kafka event 10ms.

- Source: 
```
spark.readStream.format("kafka").option("subscribe","input").load()
```
- Transform:

```
.groupBy('value.cast("string") as key')
```

- Sink:
```
writeStream.format("kafka").option("topic","output")
```

- Trigger
```
.trigger("1minute").outPutMode("update")
```

- Checkpoint (lugar que vai gravar o arquivo)

```
.option("checkpointlocation","...").start()
```

## Structured Streaming

- Necessário Schema pode ler ultimo arquivo sempre e inferir os schema.
- 100ms por chunk
- naive approach: file-based streaming source, keep listing all files, muitos arquivos começa a ficar lento, por garantir EOS ele precisa ler tudo.


- Os checkpoints do stream ficam na folder checkpoint se deletar essa folder colocar option failOnDataLoss, false.

Para fazer um join é necessário colocar um waterMark (janela dos streamings em questão) join será aplicado apenas na Janela.

Watermark = Window KSQL

Late Arrival MicroBatch, quero garantir que vai ser realizado em uma janela preciso especificar em ambos o watermakr, caso não será perdido um evento do join que possa ter se atrasado por n problemas (rede., etc...)

Pode ser feito join de streaming com batch mas nao usa conceitor de watermark.