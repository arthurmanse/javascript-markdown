# Estudo em JavaScript

## Operações Bitwise:


| Símbolo   | Significado | Explicação |
| :-------: | :---------: | ---------- |
| &	        |	AND	        |	Retorna 1 se cada bit for 1 |
| \|        |	OR	        |	Retorna 1 se um dos bits for 1 |
| ^	        |	XOR	        |	Retorna 1 se apenas um dos é 1 
| ~	        |	NOT	        |	Inverte todos os bits
| <<	      |	Deslocamento para esquerda	|	Muda para a esquerda empurrando zeros da direita e deixando os pedaços mais à esquerda caírem.|
| >>	      |	Deslocamento para direita	|	Muda para a direita empurrando cópias do bit mais à esquerda, e faz os bits mais à direita caírem.|
| >>>	      |	Deslocamento para direita com zeros	|	Muda para empurrando zeros da esquerda, e faz os bits mais à direita caírem. |

#### Exemplos:

```js
  5 & 1	= 1 
    0101 & 0001	= 0001

  5 | 1	= 5	
    0101 | 0001	= 0101

  5 ^ 1	= 4	
    0101 ^ 0001	= 0100
  
  ~5 	= 10	
    ~ 0101 = 1010
  
  5 << 1	= 10	
    0101 << 1	= 1010
  
  5 >> 1	= 2	
    0101 >> 1 = 0010
  
  5 >>> 1	= 2	
    0101 >>> 1 = 0010
```
***
*JavaScript* armazena números como números de ponto flutuante em 64 bits, mas todas as operações bitwise são realizadas sobre números binários de 32 bits.
Antes que uma operação serja realizada, JS converte números para 32 bits assinalados como números inteiros.
Após a operação bitwise, o resultado é convertido de volta a números de 64 bits.

### Atenção:
Os exemplos acima usam números binários de 4 bits. Por isso, **~5** retorna **10**.
Como JS trabalha com 32 bits, ele não retornará 10, mas sim -6:
```js
00000000000000000000000000000101 (5)
11111111111111111111111111111010 (~5 = -6)
```
Um número inteiro usa o bit mais à esquerda como um sinal de menos.

##### Convertendo Decimal para Binário:
```js
function dec2bin(dec) {
  return (dec >>> 0).toString(2)
}
```
##### Convertendo Binário para Decimal
```js
function bin2dec(bin) {
  return parseInt(bin, 2).toString(10)
}
```
***
Os números binários em JS são armazenados em formatos de complemento de dois. Isso significa que **um número negativo é o bitwise NOT do número +1**:
```js
00000000000000000000000000000101	|	5
11111111111111111111111111111011	|	-5
00000000000000000000000000000110	|	6
11111111111111111111111111111010	|	-6
```

## Expressões Regulares (RegEx) em JavaScript

#### O que é uma Expressão Regular?
Uma expressão regular é uma sequência de caracteres que formam um padrão de busca. Quando você busca por dados em um texto, você pode usar esse padrão de busca para descrever o que você está buscando.

Uma expressão regular pode ser um caractere único, ou um padrão mais complicado. Expressões regulares podem ser usadas para realizar todo tipo de operação de busca de texto e substituição de texto.

##### Sintaxe:
```js
/pattern/modifiers;
```

##### Exemplo:
```js
var patt = /w3schools/i
```
*"/w3schools/i"* é uma expressão regular
*"w3schools"* é um padrão (para ser usado em uma busca)
*"i"* é um modificador (modifica a busca para ser caso-insensitivo)

#### Usando Métodos de String:
Em JS, expressões regulares são frequentemente usadas com os dois métodos de string: "*search()*" e "*replace()*".

O método "*search()*" usa uma expressão para buscar por uma correspondência e retornar a posição da correspondência.

O método "*replace()*" retorna uma string modificada onde o padrão é substituído.
```js
var str = "Visit W3Schools!"
var n = str.search("W3Schools")	/ retorna 6
```
##### Com Expressão Regular:
```js	
var str = "Visit W3Schools"
var n = str.search(/w3schools/i)	/ retorna 6

var str = "Visit Microsoft!"
var res = str.replace(/microsoft/i, "W3Schools")
/ retorna "Visit W3Schools!"
```

Portando, *Expressões Regulares* podem fazer suas pesquisas muito mais poderosas (com caso insensitivo, por exemplo).

#### Modificadores de Expressão Regular:
Modificadores podem ser usados para realizar mais pesquisas globais de caso insensitivo:

| Modificador | Uso |
| :---: | --- |
|i  |	correspondência caso-insensitiva. |
|g	|	realiza uma correspondência global (encontra todos as correspondência ao invés de parar após a primeira correspondência). |
|m	|	realiza correspondência de múltiplas linhas. |
```js
var str = "\nIs th\nis it?";
var patt1 = /is/mgi;
console.log(patt1)	/ retorna "Is, is"
```
#### Padrões de Expressões Regulares:
Colchetes são usados para encontrar uma faixa de caracteres:

|Exemplo|Uso|
|:---:|---|
| [abc]	|	Encontra qualquer dos caracteres entre os colchetes |
| [0-9]	|	Encontra qualquer dos dígitos entre os colchetes. |
| (x\|y)	|	Encontra qualquer das alternativas separados com "\|" |

**Lembre-se:** só funciona com caracteres únicos, e não palavras ou números maiores que 9.

##### Metacaracteres:
Metacaracteres são caracteres com um significado especial:

|Exemplo|Uso|
|:---:|---|
\d	|	Encontra um dígito
\s	|	Encontra um caractere em espaço em branco.
\b	|	Encontra uma correspondência no começo da palavra dessa forma: \bWORD, ou no final da palavra, assim: WORD\b
\uxxxx	|	Encontra um caractere Unicode específico pelo número hexadecimal xxxx
```js
var str = "Is this all there is?"
var patt1 = /is\s/gi	/ resulta "Is, is"

var str = "HELLO, LOOK AT YOU!"
var patt1 = /\bLO/i	/ resulta "7"
```

##### Quantificadores que definem quantidades:

|Exemplo|Uso|
|:---:|---|
n+	|	Correspondem qualquer string que contém ao menos um 		n.
n*	|	Correspondem qualquer string que contém zero ou mais 		ocorrências de n.
n?	|	Correspondem qualquer string que contém zero ou Uma 			ocorrências de n.
```js
var str = "HellOoo World! Hello W3Schools!"
var patt1 = /o+/gi	/ retorna "Ooo, o, o, oo"

var str =  "Hellooo World! Hello W3Schools!"
var patt1 = /lo*/gi	/ retorna "l, looo, l, l, lo, l"

var str = "1, 10 or 1000?"
var patt1 = /10?/gi	/ retorna "1, 10, 10"
```
#### Usando o Objeto RegExp

Em JS, o objeto RegExp é um objeto de expressão regular com propriedades predefinidas e métodos.
	
##### Usando text()
É um método de expressão regular que busca uma string por um padrão, e retorna verdadeiro ou falso, dependendo do resultado.
O exemplo abaixo busca uma string pelo caractere "e":
```js
/e/.test("The best things in life are free!")
/ retorna true

/free/test("The best things in life are free!")
/ retorna true
```

##### Usando exec()
Procura uma string através de padrão especificado, e retorna o texto encontrado como um objeto (um vetor).
Se não houver correspondência, retorna um objeto vazio (null)
```js	
	var obj = /e/.exec("The best things in life are free!")
	var x = "Found " + obj[0] + " in position " + obj.index + " in the text: " + obj.input
	console.log(x) 	/ Found e in position 2 in the text: The best things in life are free!

	obj.input = The best things in life are free!
	obj.index = 2
	obj[0] = e
```

https://www.w3schools.com/jsref/jsref_obj_regexp.asp JavaScript RegExp Reference