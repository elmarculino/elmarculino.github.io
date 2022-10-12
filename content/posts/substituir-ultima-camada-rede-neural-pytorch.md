---
title: "Como Substituir a Última Camada de Rede Neural no PyTorch"
author: ["Marco Ribeiro"]
date: 2020-01-14
tags: ["pytorch"]
draft: false
---

Durante o desenvolvimento de uma aplicação utilizando _machine learning_ para, por exemplo, classificar imagens, não é necessário que se desenvolva uma _Convolutional Neural Network_ do zero. Isso na verdade seria uma enorme perda de tempo e recursos computacionais, além de exigir do desenvolvedor expertise em tópicos como a inicialização dos pesos na rede neural. A técnica mais utilizada hoje em dia para desenvolver esse tipo de aplicação é a utilização de _transfer learning_, a modificação de redes neurais treinadas para outros fins que são alteradas e passam por treinamento fino para executar outras atividades.

Um exemplo comum é a utilização da DCNN ImageNet, uma rede neural com 60 milhões de parametros e 500 mil neurons treinada com mais de 1,3 milhão de imagens para a classificação de 1000 diferentes classes. A idea, nesse caso, é remover a última camada da rede, treinada para a classificação das 1000 classes, e substituir por outra que será treinada com um novo dataset para um novo objetivo.

**Remover usando o index**

```python
resnet18 = models.resnet18()

cnn_modules = list(resnet18.children())[:-1]

cnn = nn.Sequential(*cnn_modules)
```

**Remover definindo ponto de corte**

```python
resnet18 = models.resnet18()

cut = next(i for i,o in enumerate(resnet18.children()) if isinstance(o,nn.AdaptiveAvgPool2d))
m_cut = resnet18[:cut]

cnn = nn.Sequential(m_cut, AdaptiveConcatPool2d())
```
