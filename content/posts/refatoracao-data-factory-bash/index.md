---
title: "Refatoração Azure Data Factory com Bash Script"
author: ["Marco Ribeiro"]
date: 2022-10-06
tags: ["datafactory", "azure", "sed", "jq", "bash", "script"]
draft: false
---

Nem tudo na vida de um engenheiro de dados são flores. As vezes é necessário fazer a "difícil" escolha entre usar força bruta ou passar horas alterando manualmente pipelines de dados em interfaces ‘clica e arrasta’. Para ilustrar o problema em questão, usaremos o caso do orquestrador de pipelines de dados Azure Data Factory da Microsoft. Por trás da interface gráfica, os pipelines, linked services e data sources são salvos em arquivos JSON que se referenciam e que posteriormente são processados para a geração dos ARM Templates e implantação nos workspaces.

Para esse trabalho, os principais comandos utilizados foram **_sed_** para a substituição de strings e **_jq_** para a leitura da estrutura dos arquivos JSON diretamente no terminal. Os arquivos do Data Factory foram clonados do repositório GIT do projeto e seguintes comandos foram utilizados para a realização das alterações necessárias.


## Renomear artefatos no arquivo JSON {#renomear-artefatos-no-arquivo-json}

Para renomear um pipeline ou linked service, não basta alterar o nome do arquivo ou o seu conteúdo, é necessário fazer os dois. Por isso, para alterar o nome de diversos artefatos para, por exemplo, remover a referencia ao ambiente do nome do objeto e não ter problemas quanto o pipeline de DevOps fizer o deploy do ARM Template em um ambiente diferente.

```bash

# Remover sufixo referente ao ambiente dos pipelines
sed -i 's/_prd//g' *.json

# Renomear arquivos json das pipelines de acordo com novo nome
for i in *.json; do new=$(jq -r '.name' "${i}").json && mv "$i" "$new"; done
```


## Alterar Path dos notebooks de PRD para novo path genérico {#alterar-path-dos-notebooks-de-prd-para-novo-path-genérico}

```bash
sed -i 's/"name": "ProjetoX_PRD/"name": "ProjetoX/g' *.json
```


## Alterar linked services com referencia ao integration runtime {#alterar-linked-services-com-referencia-ao-integration-runtime}

```bash

sed -i 's/"referenceName": "IR-XPTO-PRD"/"referenceName": "ir-xpto"/g' *.json
```


## Alterar Path dos notebooks do Databricks para nova estrutura {#alterar-path-dos-notebooks-do-databricks-para-nova-estrutura}

Suponhamos que os notebooks do databricks foram desenvolvidos nas pastas do workspace e posteriormente foi feita a integração de um repositório git. O path necessariamente terá que ser alterado em todos os pipelines que utilizem a atividade do databricks e isso pode ser feito em uma linha utilizando o comando <span class="underline"><span class="underline">sed</span></span>.

```bash
sed -i 's/"notebookPath": "\/path_antigo\/pasta_qualquer/"notebookPath": "/g' *.json
```


## Consolidar diversos linked services em um {#consolidar-diversos-linked-services-em-um}

```bash
linked_services=("lks_abc1" "lks_abc_prd" "lks_abc_test" "lks_abc_generic")
for s in "${linked_services[@]}"; do
	sed -i 's/"referenceName": "'$s'"/"referenceName": "lks_abc"/g' *.json
done
```


## Remover datasets sem objetos vinculados {#remover-datasets-sem-objetos-vinculados}

```bash
datasets=$(ls dataset | sed 's/\(.*\)\..*/\1/')
for f in $datasets; do
        pipelines=$(grep -l -R '"referenceName": "'$f'",' pipeline/* | sed 's/.*\///;s/\(.*\)\..*/\1/')
        lenght=$(echo -n "$pipelines" | grep -c '^')

        if [ $lenght -eq 0 ]; then
        	rm datafactory/dataset/$f.json
        fi
done
```

É isso, apesar de termos a nossa disposição uma infinidade de ferramentas com interfaces modernas e dinâmicas, as vezes o bom e velho terminal pode te salvar horas de trabalho.
