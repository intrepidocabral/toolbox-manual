
## Converter variáveis

* Converter para string: **str(var)**
```
>>> preco = 30
>>> preco = str(preco)
>>> preco
"30"
```

* Converter para inteiro: **int(var)**
```
>>> preco_como_string = "29"
>>> preco = int(preco_como_string)
>>> preco
29
```

* Converter para float: **float(var)**
```
>>> preco_como_string = "29.99"
>>> preco = float(preco_como_string)
>>> preco
29.99
```
## Verificando tipo da variavel
* Use **type(var)**
```
>>> type(preco_como_string)
<type 'str'>
>>> type(preco)
<type 'float'>
>>>
```
## Remover itens de uma lista: **remove()**

```
>>> numeros = [1,2,3]
>>> numeros.remove(1)
>>> numeros
[2, 3]
```

## Funções anônimas: **lambda arguments : expression**
```
>>> map(lambda x : x * 2, [1, 2, 3, 4])
Output [2, 4, 6, 8]
```
