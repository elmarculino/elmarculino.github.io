+++
title = "Refatoração Azure Data Factory com Bash Script"
author = ["Marco Ribeiro"]
date = 2022-10-06
draft = false
+++

Nem tudo na vida de um engenheiro de dados são flores. As vezes é necessário fazer a "difícil" escolha entre usar força bruta ou passar horas alterando manualmente pipelines de dados em interfaces ‘clica e arrasta’. Para ilustrar o problema em questão, usaremos o caso do orquestrador de pipelines de dados Azure Data Factory da Microsoft. Por trás interface gráfica todos os objetos dos pipelines são salvos em arquivos JSON....


## Alterar Path dos notebooks do Databricks para nova estrutura {#alterar-path-dos-notebooks-do-databricks-para-nova-estrutura}

Suponhamos que os notebooks do databricks foram desenvolvidos nas pastas do workspace e posteriormente foi feita a integração de um repositório git. O path necessariamente terá que ser alterado em todos os pipelines que utilizem a atividade do databricks e isso pode ser feito utilizando o comando <span class="underline"><span class="underline">sed</span></span>.

```bash
sed -i 's/"notebookPath": "\/path_antigo\/pasta_qualquer/"notebookPath": "/g' *.json
```
