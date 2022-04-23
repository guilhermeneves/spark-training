## ETL vs ELT

(ETL) Datawarehouse: Past analysis (what/why) : Dado enviesado foi transformado

(ELT): Features são mantidas.

Traditional Data Warehouse (Brings from Bill Inmon)

- EDW (Enterprise Data Warehouse)
    - Processamento acoplado no storage, não tem como separar, limitação de hardware (GB a terabytes)
    - Techniques: ETL, Business Logic, *Kimball como trazer o dado de forma efetiva, quanto mais etl mais complexo no datawarehouse. Conceito de ODS (Opreational Data Warehouse) traz apenas dados operacionais por exemplo ultima semana.
    - Design Methods
        - Bottom-Up - Data Mart [Ralph Kimball] Mercado teve uma tração mais forte que Inmon
        - Top-Down: Data warehouse [Bill Inmon]
Normalmente a parte mais cara do projeto.

## Azure SQL DB as TDW (traditional warehouse)

Diferente do AWS RDS onde é uma instancia onde você paga e a AWS gerencia. o Azure SQL DB foi desenhado para ser cloud.

É inteligente, PaaS, pouca para 0 administração, escala com zero downtime.

Features: Columnar Storage para fazer transacional e analitico. Hyperscale [100Tb]

## MDW Modern Data Warehouse

- Analytics Platform for Enterprises
- Scalability - Hor & Ver
- PaaS & SaaS
- SQL Like INterface
- Columnar Data Storage Type.

Physical Hardware (A partir de 1 Terabyte justifica o uso Synapse Analytics (MDW), até 1 terabyte considere utilizar essa opcao)
- MPP
- Loosely Coupled & Shared Nothing