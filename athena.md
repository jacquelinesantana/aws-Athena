# Athena

- Processa conjuntos de dados mesmo em grande escala com facilidade

- Sem servidor você não precisa se preocupar em cuidar da forma como esse serviço vai escalar por tras da AWS e também evita a necessidade ETL (Extract, Transform e  Load)

Esse acronomo indica a necessidade de extrair os dados para um local específico, transformar os dados para um formato específico ou carrega-los para um ambiente de processamento. Tudo é feito com os dados na sua origem da forma que se encontram se a obrigação de um tratamento prévio.

- Para pelo uso

- Execução em paralelo é p recurso que permite que multiplas consultas sejam feitas de forma simultanea.



## Prática:

1. escolher qual vai ser o fluxo de trabalho que vamos optar que pode ser o SQL Trino ou PySpark e o Spark SQL
   
   O que muda aqui é o tipo de consulta que vamos operar, escolha o SQL Trino para consultas simples em um S3, por exemplo. Já o PySpark e Spark para casos onde for necessário uso de linguagem Python, tivermos consultas de complexidade avançada, processamento em lote ou transformações complexas...

![e1ceacab-7286-4167-a2ab-43f47c35e7f0](file:///C:/Users/Jacqueline/Pictures/Typedown/e1ceacab-7286-4167-a2ab-43f47c35e7f0.png)

2. em Editor manter as informações que já estão lá

3. clique em configurar a saídas dos dados para um bucket, pode ser uma pasta desse mesmo bucket

4. criar o banco de dados para guardar os resultados: `CREATE DATABASE mydatabase;`

5. Segunda Query vamos criar a tabela onde vamos enviar os dados da tabela ou fonte dos dados: 

```sql
-- cria uma tabela de consulta para o Athena facilita os seguintes queries
CREATE EXTERNAL TABLE processos_pad (
    tipo STRING,
    processo STRING,
    etapa STRING,
    portaria STRING,
    basf_instauracao STRING,
    basf_resultado STRING
)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY ';'
STORED AS TEXTFILE
LOCATION 's3://bucket-logs-empresa/';
```

6. Query para consultar nessa tabela external:

```sql
-- Listar todos os processos em andamento
SELECT *
FROM processos_pad
WHERE etapa = 'Finalizado';
```

7. Segundo exemplo de consulta:

```sql
-- Listar todos os processos em andamento com apenas 2 colunas(processo e tipo)
SELECT Processo, Tipo
FROM processos_pad;
```

Exemplo do arquivo csv: arquivo.csv
