---
title: "Criando Um Gerador de Imagens de Placas de Carros"
author: ["Marco Ribeiro"]
draft: false
---

Para treinar um modelo de machine learning que realize o reconhecimento de caracteres, OCR, é necessário uma grande quantidade de imagens de placas. Daria um trabalho enorme conseguir milhares de imagens de carros com as placas visíveis, recortar as placas das imagens e anotar as imagens com os textos dos números das placas. Minha solução para obter essas milhares de imagens foi simplesmente gerá-las.

Como o Brasil está adotando um novo padrão de placas é necessário utilizar dois templates. O primeiro utiliza imagens de placas antigas e insere os caracteres no padrão ABC-1234, o segundo com imagens de placas novas, insere os caracteres com a nova fonte no padrão ABC1D23 com 4 letras e 3 números.

Para gerar os números de placas antigas foram utilizadas as seguintes funções:

```python
from random import randrange

letters = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
letters_len = len(letters)
def get_idx(l): return randrange(l)

def plate_number_generator():
  plate_number = ''
  for i in range(3):
    plate_number += letters[get_idx(letters_len)]
  plate_number += format(randrange(9999), '04d')
  return plate_number

def new_plate_number_generator():
  plate_number = ''
  for i in range(3):
    plate_number += letters[get_idx(letters_len)]
  plate_number += format(randrange(9), '01d')
  plate_number += letters[get_idx(letters_len)]
  plate_number += format(randrange(99), '02d')
  return plate_number

plate = plate_number_generator()
new_plate = new_plate_number_generator()
print(f'Placa antiga: {plate}')
print(f'Placa nova: {new_plate}')
```

Para gerar as imagens das placas
