# Data Pipeline Showcase

Este repositório demonstra a implementação de um pipeline de dados completo que conecta diferentes tecnologias para ingestão, transformação e análise de dados.

## Arquitetura do Pipeline

### Fluxo Geral
1. **Banco de Dados PostgreSQL**: Origem dos dados, onde informações são armazenadas inicialmente.
2. **Apache Airflow**: Responsável pela orquestração do pipeline e pela leitura dos dados do PostgreSQL.
3. **Snowflake (Camada STAGE)**: Recebe os dados lidos pelo Airflow para uma camada de staging.
4. **DBT (Data Build Tool)**: Realiza transformações de dados no Data Warehouse (Snowflake), organizando-os em:
   - **Stage**: Dados preparados para transformações iniciais.
   - **Dimensões**: Dados transformados em entidades dimensionais (dimensões).
   - **Fatos**: Dados processados e agregados para análises.
   - **Análises**: Resultado final para consumo por ferramentas de BI e relatórios.

### Representação Visual
```
PostgreSQL -> Airflow -> Snowflake (STAGE) -> DBT -> Snowflake (DW)
```
![Arquitetura](https://github.com/user-attachments/assets/1de26cf8-8681-4397-bf8e-94457769a11c)


### DAG no Apache Airflow
Abaixo está uma representação visual da DAG executada no Apache Airflow:

![Airflow](https://github.com/user-attachments/assets/aa010be5-5c73-4f81-a4a2-06ed86e177c5)

### Lineage do DBT
A figura abaixo demonstra a estrutura lineage configurada no DBT:

![Lineage do DBT](https://github.com/user-attachments/assets/05175138-24ff-49cd-93ac-37e41fd88065)


## Pré-requisitos

- **Apache Airflow** configurado para leitura dos dados do PostgreSQL e envio ao Snowflake.
- **Snowflake** como Data Warehouse.
- **DBT** configurado para executar transformações no Snowflake.

### Tecnologias Utilizadas
- **PostgreSQL**
- **Amazon EC2**
- **Docker**
- **Apache Airflow**
- **Snowflake**
- **DBT (Data Build Tool)**

## Estrutura do Repositório

```plaintext
├── dags/
│   ├── pipeline_dag.py       # DAG do Airflow para ingestão de dados
├── dbt/
│   ├── models/
│   │   ├── stage/            # Modelos de stage
│   │   ├── dimensions/       # Modelos de dimensões
│   │   ├── facts/            # Modelos de fatos
│   │   └── analyses/         # Modelos de análises
├── scripts/
│   ├── extract_postgres.sql  # Script de extração do PostgreSQL
│   └── load_snowflake.sql    # Script de carregamento para o Snowflake
├── README.md                 # Documentação do projeto
```

## Configuração

### 1. Banco de Dados PostgreSQL
- Certifique-se de que o PostgreSQL esteja configurado e populado com os dados iniciais.

### 2. Apache Airflow
- Configure a DAG localizada em `dags/pipeline_dag.py` para realizar:
  - Leitura dos dados do PostgreSQL.
  - Carregamento dos dados para o Snowflake na camada STAGE.

### 3. Snowflake
- Configure as credenciais e a camada STAGE para receber os dados do Airflow.

### 4. DBT
- Defina os modelos de transformação no diretório `dbt/models/`:
  - **Stage**: Processamento inicial dos dados.
  - **Dimensões**: Transformação em entidades dimensionais.
  - **Fatos**: Agregação e métricas para análises.
  - **Análises**: Dados prontos para consumo.

## Como Executar

1. **Ingestão de Dados**:
   - Inicie o Apache Airflow e execute a DAG para mover os dados do PostgreSQL para o Snowflake (STAGE).

2. **Transformação com DBT**:
   - Navegue até o diretório do DBT e execute os comandos:
     ```bash
     dbt run       # Executa os modelos
     dbt test      # Valida os modelos
     ```

3. **Análise de Dados**:
   - Conecte sua ferramenta de BI ao Snowflake e explore os dados transformados.

## Contribuição

Sinta-se à vontade para abrir issues e pull requests para melhorias ou sugestões neste projeto.

