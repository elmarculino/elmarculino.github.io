+++
title = "Extração de Dados do Amazon DynamoDB para Postgres/MySQL"
author = ["Marco Ribeiro"]
date = 2022-10-12
tags = ["postgres", "mysql", "dynamodb", "python", "etl"]
draft = false
+++

Um tempo atrás criei uma aplicação web para gerenciamento de contas a pagar e a receber utilizando a infraestrutura da AWS e o Amplify. Ao se criar uma API GraphQL utilizando o Amplify CLI, toda a infraestrutura necessária é criada, incluindo funções Lambda e a base de dados DynamoDB. É tudo muito lindo, mas essa praticidade tem um custo, e não poder executar consultas SQL diretamente nos dados dificulta bastante a análise de dados.

Para solucionar esse problema e cruzar os dados de contas a pagar com os de vendas, que são vem de um sistema com banco de dados Microsoft SQL, a solução mais fácil foi extrair as tabelas do DynamoDB e salvá-los em uma base Postgres (Ou qualquer banco de dados relacional que você preferir). Para isso foram utilizados os pacotes abaixo:


## Importação dos pacotes necessários {#importação-dos-pacotes-necessários}

```python
import boto3
import pandas as pd
from sqlalchemy import create_engine
```


## Criação dos objetos utilizados na extração {#criação-dos-objetos-utilizados-na-extração}

```python

engine = create_engine('postgresql://nome_usuario:senha@endereco_banco:5432/nome_base')
client = boto3.client('dynamodb')
dynamodb = boto3.resource('dynamodb', region_name="us-east-1")

# Listar tabelas
client.list_tables()
```


## Realização do leitura completa da tabela {#realização-do-leitura-completa-da-tabela}

Para esse passo foi utilizada uma função que executa o full scan da tabela. Como cada consulta tem um limite de registros retornados, é utilizada a chave 'LastEvaluatedKey', retornada a cada consulta, para solicitar do próximo batch em um loop.

```python
def table_scan(table):
    response = table.scan()
    data = response['Items']

    while 'LastEvaluatedKey' in response:
        response = table.scan(ExclusiveStartKey=response['LastEvaluatedKey'])
        data.extend(response['Items'])

    return data


table = dynamodb.Table('parcelas-xxxxstringaleatoriaxxxxx-prod')
parcelas = table_scan(table)
```


## Criação do dataframe, tratamento e gravação dos dados {#criação-do-dataframe-tratamento-e-gravação-dos-dados}

Nessa etapa é criado um dataframe Pandas para o tratamento inicial dos dados e a utilizado o método 'to_sql', que utiliza a engine do sqlalchemy criada anteriormente, para a gravação dos dados do DynamoDB na tabela SQL.

```python

# Cria um dataframe pandas com os dados da tabela
df = pd.DataFrame(contas)

# Converte os dados da colunas para o tipo desejado
df = df.astype({
    'valor':'float',
    'numeroParcela':'int',
    'quantidadeParcelas':'int'
})

# Remove colunas
df.drop(labels='__typename', axis=1, inplace=True, errors='raise')

# Grava dataframe no banco de dados
df.to_sql('parcelas', con=engine, if_exists='replace', index=False, schema='contas')
```

É isso, com os dados salvos em um banco de dados relacional é possível agora realizar consultas SQL e/ou utilizar o DBT para criar toda sorte de views e tabelas automaticamente para facilitar a análise de dados e a criação de dashboards.
