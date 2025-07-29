# Estudo em JavaScript
(Realizado através da W3School)

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
  5 & 1	= 1          // 0101 & 0001	= 0001
  5 | 1	= 5	         // 0101 | 0001	= 0101
  5 ^ 1	= 4	         // 0101 ^ 0001	= 0100
  ~5 	= 10	     // ~ 0101 = 1010
  5 << 1	= 10     // 0101 << 1	= 1010
  5 >> 1	= 2	     // 0101 >> 1 = 0010
  5 >>> 1	= 2	     // 0101 >>> 1 = 0010
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
00000000000000000000000000000101	//	5
11111111111111111111111111111011    // -5
00000000000000000000000000000110	//	6
11111111111111111111111111111010	// -6
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
var n = str.search("W3Schools")	// retorna 6
```
##### Com Expressão Regular:
```js	
var str = "Visit W3Schools"
var n = str.search(/w3schools/i)	// retorna 6

var str = "Visit Microsoft!"
var res = str.replace(/microsoft/i, "W3Schools") // retorna "Visit W3Schools!"
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
console.log(patt1)	// retorna "Is, is"
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
var patt1 = /is\s/gi	// resulta "Is, is"

var str = "HELLO, LOOK AT YOU!"
var patt1 = /\bLO/i	// resulta " 7 "
```

##### Quantificadores que definem quantidades:

|Exemplo|Uso|
|:---:|---|
n+	|	Correspondem qualquer string que contém ao menos um 		n.
n*	|	Correspondem qualquer string que contém zero ou mais 		ocorrências de n.
n?	|	Correspondem qualquer string que contém zero ou Uma 			ocorrências de n.
```js
var str = "HellOoo World! Hello W3Schools!"
var patt1 = /o+/gi	// retorna "Ooo, o, o, oo"

var str =  "Hellooo World! Hello W3Schools!"
var patt1 = /lo*/gi	// retorna "l, looo, l, l, lo, l"

var str = "1, 10 or 1000?"
var patt1 = /10?/gi	// retorna "1, 10, 10"
```
#### Usando o Objeto RegExp

Em JS, o objeto RegExp é um objeto de expressão regular com propriedades predefinidas e métodos.
	
##### Usando text()
É um método de expressão regular que busca uma string por um padrão, e retorna verdadeiro ou falso, dependendo do resultado.
O exemplo abaixo busca uma string pelo caractere "e":
```js
/e/.test("The best things in life are free!") // retorna true

/free/.test("The best things in life are free!") // retorna true
```

##### Usando exec()
Procura uma string através de padrão especificado, e retorna o texto encontrado como um objeto (um vetor).
Se não houver correspondência, retorna um objeto vazio (null)
```js	
var obj = /e/.exec("The best things in life are free!")
var x = "Found " + obj[0] + " in position " + obj.index + " in the text: " + obj.input
console.log(x) 	// Found e in position 2 in the text: The best things in life are free!

obj.input = The best things in life are free!
obj.index = 2
obj[0] = e
```

Para mais formas, acesse a [Listagem das Referências de JavaScript RegExp](https://www.w3schools.com/jsref/jsref_obj_regexp.asp) 

## Erros em JavaScript - throw, try, catch, finally

### 'try' e 'catch'
A declaração try permite que você defina um bloco de código para ser testado para erros enquando ele é executado.
A declaração catch permite que você defina um bloco de código para ser executado se um erro ocorre no bloco do "if".
As declarações try e catch vem em pares:
```js
try {
  Bloco de código para try
}
catch(err)
  Bloco de código para lidar com erros
}
```
##### Exemplo:
```js
try {
  adddlert("Welcome guest")
}
catch(err)
  document.getElementById("demo").innerHTML = err.message
}
```

### Erros em Javascript com 'throw'
Quando um erro ocorre, JS vai normalmente parar e gerar uma messagem de erro. O termo técnico para isso é: JS vai lançar uma exceção (lançar um erro).
JS vai realmente criar um objeto de Erro com duas propriedades: "name" e "message".
	
#### throw
Permite criar um erro customizado. Tecnicamente você pode "lançar uma exceção (lançar um erro)".
A exceção pode ser um Objeto, String, Número e um Booleano
```js
throw "Too big"	//	lança um texto
throw 500		//	lança um número
```
Se você usa throw juntamente com try e catch, você pode controlar o fluxo do programa e gerar messagens de erros personalizadas.

##### Exemplo de Validação de Input:
Se o valor está errado, uma exceção (err) é lançada. A exceção é captada pela declaração **catch** e uma messagem de erro personalizada é mostrada:
```js
<input id="demo" type="text">
<button type="button" onclick="myFunction()">Test Input</button>
<p id="p01"></p>

<script>
	function myFunction() {
		var message, x
		message = document.getElementById("p01")
		message.innerHTML = ""
		x = document.getElementById("demo").value
		
		try {
			if(x == "") throw "empty";
			if(isNaN(x)) throw "not a number"
			x = Number(x)
			if (x < 5) throw "too low"
			if (x > 10) throw "too high"
		}
		catch(err) {
			message.innerHTML = "Input is " + err
		}
	}	
</script>
```

##### Validação no HTML
O código acima é apenas um exemplo. Navegadores modernos vão frequentemente usar uma combinação de JS e validação HTML imbutida, usando regras de validações predefinidas por atributos do HTML.
```js
<input id="demo" type="number" min="5" max="10" step="1">
```
### finally
Permite executar códigos, após try e catch, não importando o resultado.
```js
try {
  Bloco de código para try
}
catch(err) {
  Bloco de código para lidar com erros
}
finally {
  Bloco de código para ser executado não importando o resultado de try / catch.
}
```
##### Exemplo:
```js	
function myFunction() {
  var message, x
  message = document.getElementById("p01")
  message.innerHTML = ""
  x = document.getElementbyId("demo").value
  try {
    if(x == "") throw "is empty"
    if(isNaN(x)) throw "is not a number"
    x = Number(x) 
    if(x > 10) throw "is too high"
    if(x < 5) throw "is too low"
  }
  catch(err) {
    message.innerHTML = `${x} ${err}`
  }
  finally {
    document.getElementById("demo").value = ""
  }
}
```
#### O Objeto de Erro
JavaScript tem um objeto de erro embutido que provê informações de erro quando um erro ocorre. O objeto de erro provê duas propriedades úteis: *name* e *message*.
|Propriedade|Uso|
|:---:|---|
name	|	Define ou retorna um nome de erro
message 	|	Define ou retorna uma mensagem de erro (uma string)

#### Valores de Nome de Erro
Seis diferentes valores podem retornar após uma propriedade de nome de erro:

|Valor|Uso|
|:---:|---|
EvalError		|	Um erro ocorreu na função eval() - use 			SyntaxError. As novas versões não lançam *EvalError*.
RangeError	|	Um número está "fora da faixa"
ReferenceError	|	Uma referência ilegal ocorreu
SyntaxError	|	Um erro de sintaxe ocorreu
TypeError		|	Um erro de tipagem ocorreu
URIError		|	Um erro no encodeURI() ocorreu
```js
RangeError
	var num = 1
	try {
		num.toPrecision(101)	// um número não pode ter 101 dígitos significantes.
	}
	catch(err) {
		document.getElementById("demo").innerHTML = error.name	// RangeError
	}

ReferenceError
	var x
	try {
		x = y + 1 	// y não foi declarado
	}
	catch(err) {
		document.getElementById("demo").innerHTML = err.name // ReferenceError
	}

SyntaxError
	try {
		eval("alert('Hello)")	// esquecer ' vai produzir um erro
	}
	catch(err) {
		document.getElementById("demo").innerHTML = err.name // SyntaxError
	}

TypeError
	var num = 1
	try {
		num.toUpperCase()
	}
	catch(err) {
		document.getElementById("demo").innerHTML = err.name // TypeError 
	}

URIError
	try {
		decodeURI("%%%") // não é possível decodificar sinais de porcentagem
	}
	catch(err) {
		document.getElementById("demo").innerHTML = err.name	// URIError
	}
```
***
Para mais formas, acesse a [Listagem das Referências de JavaScript Error](https://www.w3schools.com/jsref/jsref_obj_error.asp) 

## Escopo:

### Variáveis Locais:
Variáveis declaradas dentro de uma função tornam-se variáveis locais para a função, sendo de escopo de função: podendo ser acessadas apenas dentro da função.

Portanto, variáveis com o mesmo nome podem ser usadas em diferentes funções.
Variáveis locais são criadas quando uma função inicia e são deletadas quando a função é completada.

### Variáveis Globais:
São declaradas fora de uma função, tornando-se globais, ou seja: possuem escopo global e, portanto, todos os scripts e funções em uma webpage podem acessá-la
```js
var carName = "Volvo" // o código aqui pode usar carName
function myFunction() {
  // o código aqui também pode usar carName
}
```
#### Atenção: 
Em JavaScript, **objetos** e **funções** também são variáveis. O escopo determina a acessibilidade das variáveis, objetos e funções de diferentes partes do código.

Com isso, se você atribuir um valor para uma variável (como uma função por exemplo) que não tem sido declarada, ela vai automaticamente se tornar de Escopo Global.
Esse código abaixo declarará uma variável global *carName*, mesmo se o valor é atribuído dentro de uma função:

```js
myFunction()
  // código aqui pode usar carName
document.getElementById("demo").innerHTML = "I can display " + carName
function myFunction() {
  carName = "Volvo"
}
```
Isso pode mudar se usar o "Strict Mode", no qual, variáveis não declaradas não são automaticamente globais.

#### Variáveis Globais em HTML
Com JS, o escopo global é o ambiente completo do JavaScript.
Em HTML, o escopo global é o objeto **window**. Todas as variáveis globais pertencem ao objeto **window**.
```js
var carName = "Volvo" // este código pode ser usado como window.carName
```
##### Atenção: 
Não crie variáveis globais a menos que você queira. Suas variáveis globais (ou funções) podem sobrescrever variáveis da window (ou funções). Qualquer função, incluindo o objeto window, pode sobrescrever suas variáveis e funções globais.

#### A Vida Útil de Variáveis JS:
A vida útil de variáveis começam quando são declaradas. Variáveis locais são deletedas quando a função é completada. No navegador, uma variável global é deletada quando você fecha o navegador (ou a aba)

Argumentos de Função (parâmetros) trabalham como variáveis locais dentro de funções.

## IÇAMENTO
Em JS, uma variável pode ser declarada pós ela ter sido usada. Em outras palavras: uma variável pode ser usada antes de ser declarada. Ambos os resultados dâo o mesmo resultado:
```js
var x 	// declaração de x
x = 5	// atribui 5 a x
elem = document.getElementById("demo")	
elem.innerHTML = x

x = 5
elem = document.getElementById("demo")
elem.innerHTML = x
var x
```
Içamento é um comportamento padrão do JS de mover todas as declarações para o topo do escopo atual (para o topo do atual script ou da função atual)

> Keywords let e const

	As variávels definidas com const e let são içadas para o topo do bloco, mas não inicializadas. Ou seja: o bloco de código é avisada da variável, mas não pode ser usada até que tenha sido declarada.
	Usando a variável let antes que é declarada vai retornar em ReferenceError. A variável está em uma "zona morta temporal" do começo do bloco até ser declarado.

	carName = "Volvo"
	let carName	/ ReferenceError
	
Usando const antes de ser declarada, é um erro de sintaxe, e o código irá simplesmente não funcionar.
	
	carName = "Volvo"
	const carName

Atenção: JavaScript apenas iça declarações, não inicializações. Não içará se x = 5, por exemplo, mas içará que existe uma variável x.

	Portanto, sempre que possível, declare todas as variáveis no começo de cada escopo.