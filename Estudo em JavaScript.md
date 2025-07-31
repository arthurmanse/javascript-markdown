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

### let e const

As variávels definidas com *const* e *let* são içadas para o topo do bloco, mas não inicializadas. Ou seja: *o bloco de código é avisado da variável, mas não pode ser usada até que tenha sido declarada*.

Usando a variável **let** antes que é declarada vai retornar em *ReferenceError*. A variável está em uma "zona morta temporal" do começo do bloco até ser declarado.
```js
carName = "Volvo"
let carName	// ReferenceError
```	
Usando **const** antes de ser declarada, é um erro de sintaxe, e o código irá simplesmente não funcionar.
```js	
carName = "Volvo"
const carName
```
#### Atenção: 
JavaScript apenas iça declarações, não inicializações. Não içará se x = 5, por exemplo, mas içará que existe uma variável x.

*Portanto, sempre que possível, declare todas as variáveis no começo de cada escopo.*

## use strict

**"use strict"** define que o código em JS deverá ser executado em "modo estrito"

Não é uma declaração, mas uma expressão literal, ignorada por versões anteriores do JavaScript. 

Com o modo estrito, você não pode, por exemplo, usar variáveis não-declaradas. 	

Você pode usar modo estrito em todos seus programas. Isso ajuda a escrever um código mais limpo, como prevenir você de usar variáveis não dclaradas.

### Declarando o Modo Estrito:
O modo estrito é declarado ao adicionar "use strict" no começo de um script ou uma função.
Declarada no começo de um script, ele tem escopo global (todo o código do script executará em modo estrito)
```js
"use strict"
x = 3.14	// Causará um erro porque x não é declarado.

"use strict"
myFunction()
function myFunction() {
  y = 3.14 	// Também causará erro
}

x = 3.14	// Não causará erro
myFunction() 
function myFunction () {
  "use strict"
  y = 3.14
}
```
### Sintaxe do "use strict"
Por declarar o modo estrito, a sintaxe foi designada para ser compatível com antigas versões do JS. 

Compilando um literal numérico (4 + 5) ou uma string literal ("John Doe") em um programa JS não possui efeitos colaterais. Ele simplesmente compila para uma não-existente variável e morre.

Então "use strict" apenas importa para novos compiladores que "entendem" o significado disso.

### Por que usar o Modo Estrito?
O modo estrito torna mais fácil em escrever em um JS mais "seguro". Ele muda previamente "má sintaxes" aceitadas em erros reais.

Como exemplo, em normal JS, um erro de digitação em um nome de variável cria uma nova variável global. Em modo estrito, um desenvolvedor não receberá qualquer feedback de erro na atribuição de valores a propriedades não graváveis.

Em modo estrito, qualquer atribuição para uma propriedade não-gravável, uma propriedade apenas captadora, uma propriedade, variável ou objeto inexistente, vai lançar um erro.
	
### Não Permitido em Modo Estrito
Usar uma variável sem declará-la não é permitido.
```js
"use strict"
x = 3.14	// causará um erro
```
**Atenção: Objetos são também variáveis.**

Usando um objeto, sem declará-lo, não é permitido
```js	
"use strict"
x = {p1:10, p2:20}	// causará um erro
```
Deletar uma variável (ou objeto ou função) não é permitido
```js
"use strict"
var x = 3.14
delete x	// causará um erro.
```
Duplicando um nome de parâmetro não é permitido
```js
"use strict"
function x(p1, p1) {}	// causará um erro
```
Literais numéricas octais não são permitidas
```js
"use strict"
var x = 010	// causará um erro
```
Caracteres de escape octais, Gravações em uma propriedade de somente leitura, Gravação em uma propriedade apenas captadora, Deletar uma propriedade indeletável, Usar a palavra "eval" ou "arguments" como nomes de variáveis, Usar a declaração "with", Usar "eval()"  não funcionam em "strict mode".

A keyword "*this*" em funções se comporta diferentemente em modo estrito. 

**"this" refere-se para o objeto que chamou a função.** Se o objeto não foi especificado, funções em modo estrito retornarão "*undefined*" e funções em modo normal retornarão o objeto global (window).
```js
"use strict"
function myFunction() {
  alert(this)	/ alertará "undefined"
}
myFunction()
```
Há palavras que estão reservadas para versões futuras do JS e não podem serem usadas como nomes de variáveis em Modo Estrito:
- implements
- interface
- let
- package
- private
- protected
- public
- static
- yield
```js
"use strict"
var public = 1500 // causará erro
```
**Atenção: A diretiva do "use strict" é apenas reconhecida no começo do script ou da função.**

## THIS
```js
var person = {
  firstName: "John"
  lastName: "Doe"
  id: 5566
  fullName: function() {
    return this.firstName + " " + this.lastName
  }
}
```
**this** refere-se ao objeto no qual ele pertence. Portanto, ele tem diferentes valores dependendo sobre onde ele é usado:
1. Em um método, "this" refere-se ao objeto proprietário (como exemplo acima)
2. Sozinho, "this" refere-se ao objeto global.
3. Em uma função, "this" refere-se ao objeto global.
4. Em uma função, em modo estrito, "this" é "undefined".
5. Em um evento, "this" refere-se ao elemento que recebeu o evento.
6. Métodos como "call()", e "apply()" podem referir "this"

### this Sozinho
Quando usada sozinha, o "proprietário" é o objeto global. Em uma janela do navegador o objeto global é o [object window]. Isso também ocorre em Modo Estrito.
```js
var x = this
document.getElementById("demo") = x
```
### this em uma Função:
Em uma função em JS, o proprietário da função é a ligação padrão para "this". Então, em uma função, "this" refere-se ao objeto global [object window].

Em modo estrito, não se permite ligação. Portanto, quando usado em uma função dentro do modo estrito, "this" é "undefined".

### this em Manejamento de Eventos.
Em HTML, this refere-se ao elemento HTML que recebeu o evento.
```js
<button onclick="this.style.background='red' ">
  Click to Remove Me!
</button>	// transforma o botão vermelho ao clicar.
```

### Vinculação de Método de Objeto
Nesses exemplos, "this" é um objeto "person" (o objeto "person" é o "proprietário" da função)
```js
var person = {
  firstName: "John"
  lastName: "Doe"
  id: 5566
  myFunction: function() {
    return this
  }
}
document.getElementById("demo").innerHTML = person.myFunction()	
// retorna [object Object]
```
Em outras palavaras: this.firstName significa a propriedade firstName do objeto (person).

### Ligação de Função Explícita:
Os métodos "*call()*" e "*apply()*" são métodos de JS predefinidos. Ambos podem ser usados para chamar um método de objeto com um outro objeto como argumento.

No exemplo abaixo, quando chamamos person1.fullName com person2 como argumento, "this" vai referir para person2, mesmo se ele é método de person1:
```js
var person1 = {
    fullName: function() {
    return this.firstName + " " + this.lastName
  }
}
var person2 = {
  firstName: "John",
  lastName: "Doe",
}
person1.fullName.call(person2)	// retorna "John Doe"
```

## ARROW Function

Funções Arrow nos permite escrever sintaxes mais curtas de funções:
```js
hello = function() {
  return "Hello World"
}
```
Com Arrow Function:
```js
hello = () => {
  return "Hello World"
}
```
E fica ainda mais curto. Se a função tem apenas uma declaração, e a declaração retorna um valor, você pode remover as chaves e a keyword "return"
```js
hello = () => "Hello World!"
```
**Atenção: Isso trabalha apenas se a função tem apenas uma declaração.**

Se você tem dois parâmetros, você passa-os dentro dos parênteses:
```js
hello = (val) => "Hello " + val
document.getElementById("demo").innerHTML = hello("you")
```
Na verdade, se você tem apenas um parâmetro, você pode retirar os parâmetros:
```js  
hello = val => "Hello " + val
```
### E Sobre "this"?
O manejo de "this" é também diferente em arrow functions comparado com funções regulares. Em resumo, com funções arrow não há ligação de "this".

Em funções regulares, a keyword "this" representava o objeto que chamava a função, no qual poderia ser o "window", o documento, um botão, ou qualquer coisa.

Com arrow functions, o "this" sempre representa o objeto que definiu a arrow function.

Os exemplos abaixo chamam um método duas vezes: o primeiro quando a página carrega, e uma vez novamente quando o usuário clica um botão.

O primeiro exemplo usa uma função regular, e o segundo usa arrow functions. O resultado mostra que o primeiro exemplo retorna dois objetos diferentes (window e button), e o segundo exemplo retorna o objeto window duas vezes, porque o objeto window é o "proprietário" da função.
```js
// Função Regular:
hello = function() {
  document.getElementById("demo").innerHTML += this
}
// O objeto window chama a função
window.addEventListener("load", hello)
// Um objeto de botão chama a função:
document.getElementById("btn").addEventListener("click", hello)
// Retorna [object Window] [object HTMLButtonElement]
-----------------------------------
// Arrow Function
hello = () => {
  document.getElementById("demo").innerHTML += this
}
// o objeto window chama a função:
window.addEventListener("load", hello)
// o objeto button chama a função:
document.getElementById("btn").addEventListener("click", hello)
// Retorna [object Window] [object Window]
```
Lembre-se dessas diferenças quando você estiver trabalhando com funções. Às vezes o comportamento de funções regulares é o que você deseja, se não, use arrow functions.

## CLASSES

Foi introduzido pelo ES6. As Classes em JavaScript são modelos para Objetos em JavaScript.

### Sintaxe
Use  a keyword "**class**" para criar uma classe. Sempre adicione um método chamado "constructor()"
```js
class ClassName {
  constructor() { ... }
}

class Car {
  constructor(name, year) {
    this.name = name
    this.year = year
  }
}
```
O exemplo acima cria uma classe chamada "Car". A classe tem duas propriedades iniciais: "name" e "year".

**Atenção: Uma classe Não é um objeto. É um Modelo para objetos de JavaScript.**

### Usando uma Classe:
Quando você tem uma classe, você pode usar a classe para criar objetos:
```js
let myCar1 = new Car("Ford", 2014)
let myCar2 = new Car("Audi", 2019)
```
O exemplo acima usa a classe Car para criar dois objetos Car.

**Atenção: O método constructor é chamado automaticamente quando um novo objeto é criado.**

### O Método Constructor:
O método constructor é um método especial:
  - Tem que ter o exato nome "*constructor*"
  - É executado automaticamente quando um novo objeto é criado.
  - É usado para inicializar propriedades de objeto.

Se você não definir um método constructor, JS adicionará um método *constructor* vazio.

### Métodos de Classe
Os métodos de classe são criados com a mesma sintaxe como métodos de objetos.
Use a keyword "class" para criar uma class.

Sempre adicione um método "constructor()". Então adicione qualquer número de métodos.

#### Sintaxe:
```js
class ClassName {
  constructor() { ... }
  method_1() { ... }
  method_ 2() { ... }
  method_3() { ... }
}
```
Cria um método de Classe nomeado "age", que retorna a idade do carro:
```js
class Car {
  constructor(name, year) {
    this.name = name
    this.year = year
  }
  age()
    let date = new Date()
    return date.getFullYear() - this.year
  }
}
let myCar = new Car("Ford", 2014)
document.getrElementById("demo").innerHTML = "My car is " + myCar.age() + " years old."
```
Você pode enviar parâmetros para os métodos de Classe:
```js
class Car {
  constructor(name, year) {
    this.name = name
    this.year = year
  }
  age(x) {
    return x - this.year
  }
}

let date = new Date()
let year = date.getFullYear()

let myCar = new Car("Ford", 2014)
document.getElementById("demo").innerHTML = "My car is " + myCar.age(year) + " years old."
```

## JSON

JSON é um formato de armazenamento e transporte de dados. JSON é frequentemente usado quando dados são enviados de um servidor para a webpage.

### O Que É JSON?
- JSON significa JavaScript Object Notation
- JSON é um formato leve de intercâmbio de dados.
- JSON é uma linguagem independente *
- JSON é "auto-descritiva" e de fácil entendimento.

A sintaxe JSON é derivada da sintaxe de notação de objeto em JavaScript, mas o formato JSON é apenas textual. Os códigos para leitura e geração de dados JSON podem ser escritos em qualquer linguagem de programação.

##### Exemplo:
Essa sintaxe JSON define um objeto employees: um vetor de 3 gravações de empregados (objetos):
```js
{
  "employees":[
    {"firstName":"John", "lastName":"Doe"},
    {"firstName":"Anna", "lastName":"Smith"},
    {"firstName":"Peter", "lastName":"Jones"}
  ]
}
```
##### Formato JSON Avalia Objetos JavaScript:
O formato JSON é sintaticamente idêntico ao código de criação de objetos em JavaScript. Por isso, um programa JS pode ser facilmente converter dados JSON em objetos nativos do JS.

#### Regras de Sintaxe em JSON:
- Dados estão em pares nome/valores.
- Dados são separados por vírgulas
- Chaves abrigam objetos
- Colchetes abrigam vetores.

#### Dado JSON - Um Nome e um Valor:
Dado JSON é escrito como pares nome/valor, assim como propriedades em objetos JS.

Um par nome/valor consiste de um campo de nome (em aspas duplas), seguido por dois pontos, seguido por um valor:
```js
"firstName": "John"
```
**Atenção: Nomes JSON requerem aspas duplas. Nomes em JS não.**

#### Objetos em JSON:
Objetos JSON são escritos em chaves. Assim como em JS, objetos podem conter múltiplos pares nome/valor.
```js
{"firstName: "John", "lastName": "Doe"}
```
#### Vetores em JSON:
São escritos em colchetes:
```js
"employees":[
  {"firstName": "John", "lastName": "Doe"},
  {"firstName": "Anna", "lastName": "Smith"},
  {"firstName": "Peter", "lastName": "Jones"}
}
```

No exemplo acima, o objeto "employees" é um vetor que contém três objetos. Cada objeto é uma gravação de uma pessoa (com o primeiro e último nomes).

#### Covertendo um Texto JSON para um Objeto JavaScript:
Um uso comum de JSON é para ler dados de um servidor web, e disponibilizar os dados em uma webpage. 

Por simplicidade, isso pode ser demonstrado usando uma string como input. Primeiro, crie uma string JS contendo sintaxe JSON:
```js
var text = '{ "employees" : [' +
'{ "firstName": "John"  , "lastName": "Doe" },' +
'{ "firstName": "Anna" , "lastName": "Smith"}' +
'{ "firstName": "Peter" , "lastName": "Jones" } ]}'
```
Então, use uma função embutida do JavaScript "JSON.parse()" para converter a string em um objeto JS:
```js
var obj = JSON.parse(text)
```
Finalmente, use o novo objeto JS em sua página:
```js
<p id="demo"></p>

<script>
document.getElementById("demo").innerHTML = 
  obj.employees[1].firstName + " " + obj.employees[1].lastName
</script>
```

## Debugging com JavaScript

Erros podem (e vão) acontecer, todas as vezes que você escreve algum novo código no computador.

Códigos de programação podem conter sintaxes errôneas, ou erros lógicos. Muitos desses erros são de difícil diagnóstico. 

Frequentemente, quando códigos de programação contém erros, nada acontecerá. Não há messagens de erro, e você não terá indicações onde encontrar por tais erros. Buscando (e ajeitando) erros em códigos é chamado de "debugging" de código.

### Debuggers em JavaScript
Debugar não é fácil. Porém, felizmente, todos os navegadores modernos tem um debugger embutido para JavaScript.	

Deguggers embutidos podem ser ligados e desligados, forçando erros a serem reportados pelo usuário. Com o debugger, você pode definir pontos de interrupção (lugares onde a execução do código pode ser parada), e examinar variáveis enquanto o código está executando.

Normalmente, caso contrário, siga as etapas no final dessa página, você ativa o debugging em seu navegador com o botão F12, e seleciona "Console" no menu Debugger.

#### O Método console.log()
Se seu navegador suporta debugging, você pode usar o "console.log()" para disponibilizar os valores em JS em uma janela de debugger.

Para mais formas, acesse a [Listagem das Referências de JavaScript Console](https://www.w3schools.com/jsref/api_console.asp) 

#### Definindo Pontos de Interrupção:
Em cada breakpoint, JS vai parar a execução e permitir que você examine os valores de JS.

Após a examinação dos valores, você pode retomar a execução do código (tipicamente com um botão de play)

#### A Keyword debugger
A keyword "debugger" para a execução do JavaScript e invoca (se disponível) a função debugging.

Isso tem a mesma função de definir um breakpoint no debugger. Se nenhum debugger está disponível, a declaração debugger não terá efeito. Com o debugger ligado (F12), esse código vai parar de executar antes de executar a terceira linha.
```js
var x = 15 * 5
debugger
document.getElementById("demo").innerHTML = x
```

## Guia de Estilo em JavaScript

Atenção: Sempre use as mesmas convenções de código para todos os seus projetos em JavaScript.

Convenções código são guias de estilo para programação. Eles tipicamente cobrem:
  - Regras de nomeação e declaração para variáveis e funções.
  - Regras para o uso de espaços em branco, indentações e comentários
  - Práticas e princípios de programação.

Convenções de código: 
  - Asseguram a qualidade;
  - Desenvolve a legibilidade do código;
  - Torna o código com manutenção mais fácil.

Convenções de código podem ser regras documentadas para times que você segue, ou apenas para práticas individuais de código.

### Espaços Em Torno dos Operadores:
Sempre deixe espaços ao redor de operadores ( = + - * / ), e após vírgulas:
```js
var x = y + z
var values = ["Volvo", "Saab", "Fiat"]
```
### Indentação de Código:
Sempre use 2 espaços para indentações de blocos de código:
```js 
functon toCelsius(fahrenheit) {
  return (5 / 9) * (fahrenheit - 32)
}
```
**Atenção: Não use tabs (tabuladores) para indentação. Diferentes editores interpretam tabs diferentemente.**

### Regras de Declaração:

**Regras gerais para simples declarações:**
  - Sempre termine uma declaração simples com um ponto e vírgula.

**Regras gerais para declarações complexas (compostas):**
- Coloque uma chaves aberta no fim da primeira linha.
- Use um espaço antes das chaves abertas.
- Coloque chaves de fechamento em uma nova linha, sem espaços anteriores.
- Não termine uma declaração complexa com um ponto e vírgula.

### Regras de Objetos:
**Regras gerais para definições de objetos:**
- Coloque as chaves de abertura na mesma linha do nome do objeto.
- Use dois pontos mais um espaço entre cada propriedade e seu valor
- Use aspas em torno de valores de string, não em valores numéricos.
- Não adicione vírgula após o último par de valores de propriedade.
- Coloque a chave de fechamento em uma nova linha, sem espaço antes.
- Sempre termine uma definição de objeto com um ponto e vírgula.
```js
var person = { 
  firstName: "John",
  lastName: "Doe",
  age: 50,
  eyeColor: "blue"
};
```
Objetos encurtados podem ser compressados em uma linha, usando espaços apenas entre propriedades, dessa forma:
```js
var person = {firstName: "John", lastName: "Doe", age: 50, eyecolor: "blue"};
```
#### Comprimento de Linha < 80
Para melhor legibilidade, evite linhas mais longas que 80 caracteres. Se declarações em JS não cabem em uma linha, o melhor local para quebrar a linha é após o operador ou uma vírgula.

#### Convenções de Nomeação
Sempre usa a mesma convenção de nomeação para todo o seu código.
- Nomes de variáveis e funções escritas em camelCase
- Variáveis globais escritas em UPPERCASE (é comum, embora há quem não faça)
- Constantes (como PI) escritas em UPPERCASE

#### Hífens em HTML e CSS: 
Atributos em HTML5 podem começar com data- (data-quantify, data-price)

CSS usa hífens em property-names (font-size).

**Atenção: Hífens podem ser mal-interpretados como tentativas de subtração. Hífens não são permitidos em nomes em JS.**

Sublinhados: muitos programadores preferem usar sublinhados (date_of_birth) especialmente em databases SQL. São também usados na documentação PHP.

- PascalCase: frequentemente preferido pelos programadores em C.
- camelCase: usado pelo próprio JS, pelo jQuery, e outras bibliotecas JS.

**Atenção: Não inicie nomes com um sinal de $. Você colocará em conflito com muitos nomes de bibliotecas JS.**

#### Carregando JS em HTML:
Use sintaxe simples para scripts simples de carregamento (o atributo type não é necessário):
```js
<script src="myscript.js"></script>
```
#### Acessando Elementos em HTML
Uma consequência de usar estilos HTML desarrumados podem resultar em erros em JS. Se possível, use a mesma convenção de nomeação (como usado em JS) em HTML.

Para mais formas, acesse a [Listagem das Referências de HTML Style Guide](https://www.w3schools.com/jsref/api_console.asp) 

#### Extensões de Arquivo:
Arquivos em HTML tem uma extensão .html (.html é permitido). CSS tem .css e JS tem .js.

##### Use LowerCase Para Nomear Arquivos:
Maioria dos servidores web (Apache, Unix) são caso sensitivos sobre nomes de arquivos:

- london.jpg não pode ser acessado como London.jpg.

Outros servidores web (Microsoft, IIS) não são caso sensitivo:

- london.jpg pode ser acessado como London.jpg ou london.jpg.

Se você usar uma mistura de upper e lowercase, você tem que ser extremamente consistente. Se você mudar de um servidor web caso insensitivo, para um caso sensitivo, mesmo pequenos erros podem quebrar seu website.

Para evitar esses problemas, sempre use nomes de arquivos em lowercase (se possível).

## Boas Práticas em JavaScript

Evite variáveis globais, keyword "new", operador "==", e "eval()".

Minimize o uso de variáveis globais. Isso inclui todos tipos de dados, objetos e funções. Variáveis globais e funções podem ser sobrescritas por outros scripts. Use variáveis locais.

Sempre declare Variáveis Locais. Todas as variáveis locais usadas em uma função devem ser declaradas como variáveis locais. Variáveis locais devem ser declaradas com "var" ou "let", senão elas vão tornar-se variáveis globais.

**Atenção: Modo Estrito não permite variáveis não declaradas.**

Sempre declare no começo de cada script ou função. 

É bom também inicializar variáveis quando declara-las. 
```js
var firstName = "",
lastName = "",
price = 0,
discount = 0,
fullPrice = 0,
myArray = [],
myObject = {}
```
Nunca declare Número, String, ou Objetos Booleanos. Sempre trate esses dados como valores primitivos, e não objetos.

Não use "new Object()":
  - Use {} ao invés de "new Object()"
  - Use "" ao invés de "new String()"
  - Use 0 ao invés de new Number()
  - Use *false* ao invés de new Boolean()
  - Use [] ao invés de new Array()
  - Use /()/ ao invés de "new RegExp()"	/ new regexp object
  - Use function (){} ao invés de "new Function()"

Atenção às Conversões Automáticas de Tipo, como de strings para números, e operadores. String menos string gera NaN, por exemplo, mas somando cria-se uma concatenação.

#### Use Comparação ===
O operador de comparação == sempre converte (para tipos correspondentes) antes da comparação. O operador === força comparação de valores e tipo.

#### Use Padrões de Parâmetros:
Se uma função é chamada com um argumento errado ou faltante, o valor desse argumento é definido como *"undefined"*.

Valores indefinidos podem quebrar seu código. É um bom hábito atribuir valores padrões para argumentos.
```js
function myFunction(x, y) {
  if (y === undefined) {
    y = 0
  }
}
```
ECMAScript 2015 permite parâmetros padrões na definição de função:
```js
function (a=1, b=1) { /*código da função/* }
```
#### Sempre Termine Seus Switches com Defaults
```js
switch (new Date().getDay()) {
  case 0:
    day = "Sunday"
    break
  case 1:
    day = "Monday"
    break
  default:
    day = "Outro dia"
}
```
#### Evite Usar eval()
A função eval() é usada para executar texto como código. Em quase todos os casos, ele não deve ser necessário.

Por causa disso, ele permite código arbitrário para ser executado, o que representa um problema de segurança.

## Erros Comuns em JavaScript:

Programas JS podem gerar resultados inesperados se um programador acidentalmente usar um operador de atribuição (=), ao invés de um operador de comparação (==) em uma declaração if.

A declaração if retorna "false" (como esperado) porque x não é igual a 10.
```js
var x = 0
if (x == 10)
```
**Atenção: uma atribuição sempre retorna o valor da atribuição.**

#### Esperando Comparações Frouxas.
Em comparações regulares, tipos de dados não importam:
```js
var x = 10
var y = "10"
if (x == y) // retorna true
```
Em comparações estritas, tipos de dados importam:
```js
var x = 10
var y = "10"
if (x === y) // retorna false
```
É um erro comum esquecer que declarações "switch" usam comparações estritas.
Esse switch não irá mostrar um alerta:
```js
var x = 10
switch(x) {
  case "10": alert("Hello")
}
```
#### Confundindo Adição e Concatenação
**Adição** é sobre adicionar números.

**Concatenação** é sobre adicionar strings.

#### Mal-Entendido com Números de Ponto Flutuante.
Todos os números em JS são armazenados como números de ponto flutuante (floats) a 64-bits. Todas as linguagens de programação, incluindo JS, tem dificuldades com valores precisos de ponto flutuante.

```js
var x = 0.1
var y = 0.2
var z = x + z	// resultado não será 0.3, mas sim 0.30000000000004
```
Para resolver isso, multiplique e divida:
```js
var z = (x * 10 + y * 10) / 10	// resultado será 0.3
```
#### Mal Posicionamento do Ponto e Vírgula
Por causa de um ponto e vírgula mal colocado, esse código executará sem importar o valor de x.
```js
if (x == 19);
{
// bloco de código
}
```
**Atenção: Nunca quebre uma declaração return. Escreva a declaração na mesma linha. Declarar variáveis pode ser feito em diferentes linhas, mas o return não.**

#### Acessando Vetores com Indexação Nomeadas.
Vetores com indexações nomeadas são chamados vetores associativos (ou hashes). JS não suporta vetores com indexações nomeadas. Em JS, vetores são indexações numeradas:
```js
var person = []
person[0] = "John"
person[1] = "Doe"
person[2] = 46
var x = person.length
var y = person[0]
```
Em JS, objetos são indexações numeradas. Se você usa uma indexação nomeada, quando acessar um vetor, JS vai redefinir o vetor para um objeto padrão.

Após a redefinição automática, métodos e propriedades de vetores produzirão resultados undefined e incorretos.
```js
var person = []
person["firstName"] = "John"
person["lastName"] = "Doe"
person["age"] = 46
var x = person.length	// retorna 0
var y = person[0]	// retorna undefined
```
#### Terminando Definições com uma Vírgula:
Vírgulas finais em objetos e definições de vetores são permitidos em ECMAScript 5.
```js
points = [40, 100, 1, 5, 25, 10, ]
```
**Atenção: Internet Explorer 8 irá quebrar. E JSON não permite vírgulas finais.**

#### Undefined Não É Null
Objetos, variáveis, propriedades e métodos em JS podem ser "undefined". Além disso, objetos vazios em JS podem ter o valor "null". Isso pode criar pequenas dificuldades para testar se um objeto é vazio. 

Você pode testar se um objeto existe testando se o tipo é undefined:
```js
if (typeof myObj === "undefined")
```
Porém você não consegue testar se um objeto é null e, por isso, lançará um erro se o objeto é undefined:
```js
if (myObj === null)
```
Para resolver esse problema, você deve testar se um objeto não é null, e não é undefined. Mas ainda lançará um erro.
```js
if (myObj !== null && typeof myObj !== "undefined")
```
Por isso, você deve testar se não é "undefined" antes de testar se não é null.
```js
if (typeof myObj !== "undefined" && myObj !== null) 
// Retorna false se não existir myObj. Mas de for declarado com {} então retorna true.
```

## Performance em JavaScript:

#### Reduza a Atividade em Loops:
Cada declaração em um loop, incluindo a declaração "for", é executada por cada iteração do loop. Declarações ou atribuições que podem ser colocadas fora do loop irão fazer o loop executar mais rápido.

Faça:
```js
var i
var e = arr.length
for (i = 0; i < e; i++)
```
#### Reduza o Acesso ao DOM:
Acessar o HTML DOM é bastante lento, comparado a outras declarações JS. Se você precisa acessar um elemento do DOM muitas vezes, acesse-o uma vez apenas, e use-o como uma variável local:
```js
var obj
obj = document.getElementById("demo")
obj.innerHTML = "Hello"
```
#### Reduza o Tamanho do DOM:
Mantenha um número pequeno de elementos no HTML DOM. Isso irá sempre melhorar o carregamento de páginas, e acelerar a renderização (disponibilização da página), especificamente sobre pequenos dispositivos.

Cada tentativa de buscar o DOM irá ser beneficiada de um DOM menor. 

#### Evite Variáveis Desnecessárias:
Não crie novas variáveis se você não planeja salvar valores. 
Você poderá transformar códigos assim:
```js
var fullName = firstName + " " + lastName
document.getElementById("demo").innerHTML = fullName
```
Para assim:
```js
document.getElementById("demo").innerHTML = firstName + " " + lastName;
```
#### Atrase o Carregamento do JavaScript:
Colocar seus scripts no final do corpo da página deixa o navegador carregar a página primeiro.

Enquanto o script está sendo baixado, o navegador não irá começar qualquer outro download. Além disso, todas as atividades de análise e renderização podem ser bloqueadas.

**Atenção: A especificação HTTP define que os navegadores não devem baixar mais que dois componentes em paralelo.**

Uma alternativa é usar o **defer="true"** na tag "script". O atributo "defer" especifica que o script deve ser executado depois que a página tem finalizado a análise, mas apenas funciona para scripts externos.

Se possível, você adicionar seu script para a página pelo código, após a página ser carregada.
```js
<script>
window.onload = function() {
  var element = document.createElement("script")
  element.src = "myScript.js"
  document.body.appendChild(element)
}
</script> 
```
#### Evite Usar "with"
Tem um efeito negativo sobre a velocidade. Ele também confunde os escopos do JavaScript.

A keyword "with" não é permitida em Modo Estrito.

### Palavras Reservadas em JS:
```js
abstract	|	arguments	|	await*	|	boolean
break	|	byte	|	case	|	catch
char 	|	class* 	|	const 	|	continue
debugger |	default 	|	delete 	|	do
double 	|	else 	|	enum* 	|	eval
export* 	|	extends* 	|	false 	|	final
finally 	|	float 	|	for 	|	function
goto 	|	if 	|	implements 	|	import*
in 	|	instanceof	| 	int 	|	interface
let* 	|	long 	|	native 	|	new
null 	|	package 	|	private 	|	protected
public 	|	return 	|	short 	|	static
super* 	|	switch 	|	synchronized 	|	this
throw 	|	throws 	|	transient 	|	true
try 	|	typeof 	|	var 	|	void
volatile 	|	while 	|	with 	|	yield
```
* \* Palavras que são novas no ECMAS 5 e 6

#### Palavras Reservadas Removidas:
```js
abstract 	|	boolean 	|	byte 	|	char
double 	|	final 	|	float 	|	goto
int 	|	long 	|	native 	|	short
synchronized	| 	throws	|	transient	|	volatile
```
**Atenção: Não use essas palavras como variáveis. ECMAS 5/6 não tem suporte em todos navegadores.**

#### Palavras Reservadas em Java:
JS é frequentemente usado juntamente com Java. Você deve evitar de usar alguns objetos e propriedades Java como identificadores JS:
```js
get Class		|	java	|	JavaArray		
javaClass		|	JavaObject	|	JavaPackage
```
#### Outras Palavras Reservadas:
JS pode ser usada como linguagem de programação em muitas aplicações. Você deve também evitar de usar o nome de objetos e propriedades HTML e do Window.
```js
alert 	|	all	| 	anchor	|	anchors
area 	|	assign 	|	blur 	|	button
checkbox |	clearInterval	| 	
clearTimeout	| clientInformation	|	close 	|	closed 	|	confirm |	constructor	|	
crypto 	|	decodeURI | decodeURIComponent	|	defaultStatus	|	document |	element 	|	
elements 		|	embed |
embeds 		|	encodeURI 	|	encodeURIComponent | escape	|	event 	|	fileUpload	| 	
focus 	form	|	forms 	|	frame 	|	innerHeight |	innerWidth	|	layer 	|	layers 	|	
link |	location	|	mimeTypes 	|	navigate 	|	navigator |	frames	|	frameRate 
|	hidden 	|	history |	image	|	images 	|	offscreenBuffering 	|	open 	opener	|	
option 	|	outerHeight 	|	outerWidth |	packages		|	pageXOffset 	|	pageYOffset |	
parent	|	parseFloat	|	parseInt 	|	password |	pkcs11 	|	plugin	|	prompt 	|	
propertyIsEnum |	radio 	|	reset	|	screenX 	|	screenY 	|	scroll 	|	secure	|	
select 	|	self | setInterval		 |	setTimeout	|	status 	|
submit 	|	
taint 	|	text	|	textarea 	| top 	|	unescape 	|	untaint	|	window 	
```
#### Manejadores de Eventos HTML:
Além disso, você deveria evitar usar nomes de todos os manejadores de evento do HTML.

Exemplos:
```js
onblur	|	onclick	|	onerror	|	onfocus
onkeydown	|	onkeypress	|	onkeyup
onmouseover	|	onload	|	onmouseup
onmousedown	|	onsubmit
```

## LET

As variáveis declaradas com let não podem acessadas fora de um escopo de bloco, ou seja: fora de um bloco de código:
```js
{ 
  let x = 2
}
// x não pode ser usado aqui
```
Com isso, você pode solucionar problemas de redeclaração.
```js
var x = 10
{
  let x = 2
// aqui x é 2
}
// aqui x é 10
```
Ainda sobre a redeclaração, há o Escopo do Loop. Variáveis declaradas com let dentro de loops apenas são visíveis dentro do loop.
```js
let i = 5
for (let i = 0; i < 10; i++) {
  // argumentos
}
// Aqui "i" é 5
```
Porém, dentro do Escopo de Função, **var** e **let** são similares, não sendo visíveis fora das funções caso sejam declaradas dentro.

Além disso, var e let são também semelhantes quando declaradas fora de um bloco, ou seja: quando tem escopo global.

#### Variáveis Globais em HTML:
Em HTML, o objeto global é o *window object*. 
Variáveis globais definidas com a keyword "var" pertencem ao window object:
```js
var carName = "Volvo"
// o código aqui pode usar window.carName
```
Varáveis globais definidas com a keyword "let" não pertencem ao window object:
```js
let carName = "Volvo"
// o código aqui Não pode usar o window.carName
```
### Redeclaração:
Redeclarando uma variável JS com var é permitido em qualquer parte do programa.

Redeclarando uma variável var com let, no mesmo escopo, ou no mesmo bloco, não é permitido.
```js
var x = 2
let x = 3	// não permitido
{
  var x = 4
  var x = 5	// não é permitido por causa de let e porque var é global
}
```

O mesmo funciona o contrário: não é possível redeclarar uma variável let com var, no mesmo escopo, ou no mesmo bloco.

Redeclarar uma variável com let, em outro escopo, ou em outro escorpo, é permitido:
```js
let x = 2
{
  let x = 3
}
{
  let x = 4
}
```
#### Içamento:
Variáveis definidas com let são içadas para o topo do bloco, mas não são inicializadas. Ou seja: o bloco de código é avisado da variável, mas não pode ser usada até ser declarada.

Usando let antes que seja declarada vai resultar em um ReferenceError.

## CONST

Variáveis definidas com "const" se comportam parecidas com variáveis "let", exceto que elas não podem ser reatribuidas.
```js
const PI = 3.141592653589793
PI = 3.14		// error
PI = PI + 10	// error
```
**Atenção: Variáveis com const devem ser atribuídas com um valor quando elas são declaradas.**

Não faça:
```js
const PI
PI = 3.14159265359
```
E sim:
```js
const PI = 3.14159265359
```
#### Não-Constantes Reais:
const Não define um valor constante, mas sim uma referência constante a um valor. Por isso, ela não pode alterar valores primitivos constantes, mas pode modificar as propriedades de objetos constantes.
```js
const car = {type:"Fiat", model:"500", color:"white"}
car.color = "red"	// você pode modificar uma propriedade
car.owner = "John"	// você pode adicionar uma propriedade
```
Não pode:
```js
const car = {type:"Fiat", model:"500", color:"white"}
car = {type:"Volvo", model:"EX60", color:"red"}	// Error
```
O mesmo acontece com Vetores: você pode modificar elementos de um vetor de uma constante, mas não reatribuir um vetor de uma constante.
```js
const cars = ["Saab", "Volvo", "BMW"]
cars[0] = "Toyota"
cars.push("Audi")
```
Não pode:
```js
const cars = ["Saab", "Volvo", "BMW"]
cars = ["Toyota", "Volvo", "Audi"]	// Error
```
#### Redeclaração:
Redeclarar ou reatribuir uma já existente variável var ou let para const, no mesmo escopo, ou no mesmo bloco, não é permitido
```js
var x = 2
const x = 2		// não permitido
{
  let x = 2
  const x = 2	// não permitido
}
```
A mesma incapacidade acontece se você tentar reatribuir ou redeclarar de uma variável const já existente no mesmo escopo, ou no mesmo bloco.

Apenas é possível redeclarar com const em outro escopo, ou em outro bloco:
```js
const x = 2
{
  const x = 3	// permitido
}
{	
  const x = 4	// permitido
}
```
#### Içamento:
Semelhante a let, variáveis const são içadas ao topo do bloco, mas não inicializadas.

## VERSÕES DO JAVASCRIPT

### ES5 - JAVASCRIPT 2009

#### JSON.parse()
Um uso comum do JSON é de receber dados de um web server. Imagine que você recebeu essa string de texto de um servidor web.
```js
'{"name":"John", "age":30, "city":"New York"}'
```
A função JS "JSON.parse()" é usada para converter o texto em um objeto JS:
```js
var obj = JSON.parse('{"name":"John", "age":30, "city":"New York"}')
```
Para mais formas, acesse o [Tutorial sobre JSON](https://www.w3schools.com/js/js_json_intro.asp)

#### JSON.stringify()
Um uso comum de JSON é também de enviar dados para um servidor web. Quando enviamos dados para um servidor, os dados devem que ser uma string.

Imagine que nós tempos esse objeto:
```js
var obj = {name:"John", age:30, city:"New York"}
```
Use a função JSON.stringify() para convertê-lo em um string.
```js
var myJSON = JSON.stringify(obj)
```
O resultado será uma string seguida de uma notação JSON.
myJSON é agora uma string, pronta para ser enviada ao servidor.

#### Date.now()
Retorna o número de milissegundos desde a data zero (1 de janeiro de 1970.
```js
var timInMss = Date.now()
```
Date.now() retorna o mesmo que getTime() executado em um objeto de Data.

#### Propriedades Getters e Setters:
ES5 deixa você definir métodos de objeto com uma sintaxe que parece pegar ou definir uma propriedade.

Esse exemplo cria um getter para uma propriedade chamada fullName:
```js
// crie um objeto:
var person = {
  firstName: "John",
  lastName: "Doe",
  get fullName() {
    return this.firstName + " " + this.lastName
  }
}
```
Esse exemplo cria um setter e um getter para a propriedade "language":
```js
var person = {
  firstName: "John",
  lastName: "Doe",
  language: "NO",
  get lang() {
    return this.language
  },
  set lang(value) {
    this.language = value
  }
}
// Define uma propriedade usando um setter:
person.lang = "en"
// Disponibiliza dados do objeto usando um getter:
document.getElementById("demo").innerHTML = person.lang
```
**Atenção: sem o set, o valor final é "NO". Com o set, o person.lang = "en" torna-se "en".**

Esse exemplo abaixo usa um setter para assegurar atualizações uppercase de linguagem:
```js  
var person = {
  firstName: "John",
  lastName: "Doe",
  language: "NO",
  set lang(value) {
    this.language = value.toUpperCase()
  }
}
// Define uma propriedade usando um setter.
person.lang = "en"
// Disponibiliza dado do objeto:
document.getElementById("demo").innerHTML = person.language
// Resultado: "EN"
```
Para mais formas, acesse o [JavaScript Object Accessors](https://www.w3schools.com/js/js_object_accessors.asp)

#### Novos Métodos de Propriedade de Objetos:
"Object.defineProperty()" é um novo método de Objeto em ES5. Ele permite definir uma propriedade de objeto e/ou mudar um valor da propriedade e/ou metadados:
```js
var person = {
  firstName:"John",
  lastName: "Doe",
  language: "NO" ,
}
// Mude uma propriedade:
Object.defineProperty(person, "language", {
  value: "EN"
  writable: true
  enumerable: true 	// se for false, ele não retorna "EN"
  configurable: true
})
// Enumere propriedades:
var txt = ""
for (var x in person) {
  txt += person[x] + "<br>"
}
document.getElementById("demo").innerHTML = txt
```
Esse exemplo abaixo cria um setter e um getter para assegurar atualizações em Uppercases de language:
```js
var person = {
  firstName: "John",
  lastName: "Doe",
  language: "No"
}
// Muda uma propriedade
Object.defineProperty(person, "language", {
  get : function() { return language }
  set : function(value) { language = value.toUpperCase()}
})
// Muda a linguagem:	
person.language = "en"
document.getElementById("demo").innerHTML = person.language
// Retorna "EN"
```
ES5 adicionou vários novos Métodos de Objeto no JS:
```js
// Adiciona ou muda uma propriedade de objeto
Object.defineProperty(object, property, descriptor)

// Adiciona ou muda várias propriedades de objetos
Object.defineProperties(object, descriptors)

// Acessa propriedades
Object.getOwnPropertyDescriptor(object, property)

// Retorna todas as propriedades como um vetor:
Object.getOwnPropertyNames(object)

// Retorna propriedades enumeráveis como um vetor:
Object.keys(object)

// Acessa o prototype:
Object.getPrototypeOf(object)

// Previne de adicionar propriedades a um objeto:
Object.preventExtensions(object)

// Retorna true se propriedades podem ser adicionadas a um objeto:
Object.isExtensible(object)

// Previne mudanças de propriedades de objeto (não valores):
Object.seal(object)

// Retorna true se objeto está selado:
Object.isSealed(object)

// Previne qualquer mudanças em um objeto:
Object.freeze(object)

// Retorna true se o objeto está congelado
Object.isFrozen(object)
```

Para mais formas, acesse o [JavaScript Object ECMAScript5](https://www.w3schools.com/js/js_object_es5.asp)

#### Vírgulas no Final:
```js 
person = {
  firstName: "John",
  lastName: "Doe",
  age: 46,
}
```
Atenção: IE8 vai ter problemas. JSON não permite vírgulas no final:
```js
// Permitido
var person = '{"firstName":"John", "lastName":"Doe", "age":46}'
JSON.parse(person)	

// Não permitido:
var person = '{"firstName":"John", "lastName":"Doe", "age":46,}'
JSON.parse(person)
```
#### Palavras Reservadas como Nomes de Propriedades:
ES5 permite palavras reservadas como nomes de propriedades:
```js
var obj = {name: "John", new: "yes"}
```

### JS 2015 (ES6):

#### Loop For/Of:
A declaração JS for/of promove iterações entre os valores de um objeto. Ele permite que você realize repetições sobre estruturas de dados que são iteráveis, tais como Vetores, Strings, Maps, NodeLists, e mais.

O loop for/of tem a seguinte sintaxe:
```js
for (variável of iterável) {
  // bloco de código a ser executado
}
```

Variável: por cada iteração, o valor da próxima propriedade é atribuída para a variável. A variável pode ser declarada com const, let, ou var.

Iterável: um objeto que tem propriedades iteráveis.

Exemplo com um vetor:
```js
var cars = ["BMW", "Volvo", "Mini"]
var text = ""

for (let x of cars) {
  text += x + "<br>"
}
document.getElementById("demo").innerHTML = text
```

Atenção: Há diferenças entre o for/in e o for/of:
```js
var arr = [3, 5, 7];
arr.foo = "hello";
for (var x in arr) {
      console.log(x)
}
for (var j of arr) {
    console.log(j)
} 
// Retorna 0, 1, 2, foo
// 	3, 5, 7
```
#### Promises em JavaScript:
Um Promise é um objeto JS que conecta "Produzir Código" e "Consumir Código". 
"Produzir Código" pode tomar algum tempo e "Consumir Código" deve esperar pelo resultado.

##### Sintaxe da Promise:
```js
let myPromise = new Promise(function(myResolve, myReject) {
// "Produzir Código" (pode tomar algum tempo)
  
  myResolve() // quando der certo
  myReject()  // quando falhar
})

// "Consumir código" (Deve esperar pela final da Promise)
myPromise.then(
  function(value) { /* código se der certo */ }
  function(error) { /* código se algo falhar */ }
)
---------------
  let myPromise = new Promise(function(myResolve, myReject) {
  setTimeout(function(){ myResolve("Hello World") }, 3000)
})

myPromise.then(function(value) {
  document.getElementById("demo").innerHTML = value
})
// Resulta "Hello Word" após 3seg, ou 3000 miliseg
```
#### O Tipo Symbol
Um Símbolo JS é um tipo de dado primitivo assim como Números, Strings, ou Booleanos. Ele representa um único identificador "escondido" que nenhum outro código pode acidentalmente acessar.

Por exemplo, se diferentes codificadores desejam adicionar uma propriedade person.id para o objeto person pertencente a um código terceiro, eles poderão misturar cada um dos seus valores.

Usando Symbol() para criar um identificador único, ajuda a resolver esse problema:
```js
const person = {
  firstName: "John",
  lastName: "Doe",
  age: 50,
  eyeColor: "blue"
}
let id = Symbol('id')
person.id = 140353
```
Simbolos têm um outro uso importante. Eles podem ser usados como chaves (propriedades) em objetos. Exemplo de uso de um símbolo como chave:
```js
const obj = {}
const sym = Symbol()
obj[sym] = 'foo'
obj.bar = 'bar'

console.log(obj) // { bar: 'bar' }
console.log(sym in obj)	// true
console.log(obj[sym])	// foo
console.log(Object.keys(obj) // ['bar']
```
Note como o Símbolo não foi retornado em Object.keys(). Isso é, novamente, pelo propósito de compatibilidade com versões anteriores. Códigos antigos não avisam dos Símbolos e então eles não são retornados nesse método.

Ao primeiro olhar, parece que Símbolos podem ser usados para criar propriedades privadas sobre objetos. Muitas outras linguagens de programação tem propriedades escondidas em suas classes e essa omissão tem sido visto como uma deficiência do JS.

Infelizmente, é ainda possível para códigos que interajam com esses objetos acessar propriedades nos quais as chaves são símbolos. É até mesmo possível em situações onde o código invocado não já tenha acesso ao símbolo por si mesmo. Como exemplo, o método "Reflect.ownKeys()" é capaz de gerar uma lista de todas as chaves de um obejto, seja strings ou simbolos:
```js
function tryToAddPrivate(o) {
  o[Symbol ('Pseudo Private')] = 42
}
const obj = { prop: 'hello' }
trytoAddPrivate(obj)
console.log(Reflect.ownKeys(obj)) 	// [ 'prop', Symbol(Pseudo Private) ]
console.log(obj[Reflect.ownKeys(obj)[1]])	// 42
```
##### Prevenindo Colisões de Nomes de Propriedades:
Símbolos não podem beneficiar diretamente o JS de providenciar propriedades privadas aos objetos. No entanto, eles podem beneficiar de uma outra forma. Eles podem serem úteis em situações onde diferentes bibliotecas querem adicionar propriedades aos objetos sem o risco de haver colisões de nomes.

Considere a situação onde duas diferentes bibliotecas querem anexar algum tipo de metadado a um objeto. Talvez elas ambas querem definir algum tipo de identificador no objeto. Simplesmente usando dois caracteres de string "id" como chave, há um grande risco que múltiplas bibliotecas usarão a mesma chave.

Fazendo uso de símbolos, cada biblioteca pode gerar seus símbolos requeridos na instaciação. Portanto, os símbolos podem ser checados nos objetos, e definidos aos objetos, não importando quando um objeto é encontrado.

Por essa razão, aparenta-se que símbolos beneficiam JS. No entanto, você pode se perguntar por que não podemos apenas gerar para cada biblioteca uma string aleatória, ou usar uma string com um nome especifamente, sobre a instanciação?

Essa abordagem é realmente muito similar a abordagem com símbolos. A menos que duas bibliotecas pudessem escolher usar o mesmo nome de propriedade, então não haveria um risco de sobreposição.

Nossos nomes de propriedades com nomes únicos ainda tem uma deficiência: suas chaves são muito fáceis de encontrar, especialmente quando o código executa ou para iterar as chaves ou serializar os objetos de outra forma. 

**Considere o exemplo a seguir:**
```js
const library2property = 'LIB2-NAMESPACE-id'
function lib2tag(obj) {
  obj[library2property] = 369
}
const user = {
  name: 'Thomas Hunter II',
  age: 32	
}
lib2tag(user)
JSON.stringify(user)
// '{"name":"Thomas Hunter II", "age":32, "LIB2-NAMESPACE-id":369}'
```
Se nós tivemos usado um símbolo para um nome de propriedade do objeto, então o resultado do JSON não iria conter seu valor. Por que isso? Bem, apenas porque JS ganhou suporte para símbolos não quer dizer que a especificação JSON tem mudado. JSON apenas permite strings como chaves e JS não faz qualquer tentativa de representar propriedades de símbolos no código final do JSON.

Nós podemos corrigir facilmente o problema em que as strings de objeto de nossa biblioteca estão poluindo a saída JSON, usando "Object.defineProperty()":
```js
const library2property = uuid()
function lib2tag(obj) {
  Object.defineProperty(obj, library2property, {
    enumarable: false,
    value: 369
  })
}
const user = {
  name: 'Thomas Hunter II',
  age: 32
}
lib2tag(user)
/ '{"name":"Thomas Hunter II",
  "age":32,"f468c902-26ed-4b2e-81d6-5775ae7eec5d":369}'
console.log(JSON.stringify(user))
console.log(user[library2property])	// 369
```
Chaves de string nas quais tem sido "escondidas" através das definições de seus "enumerable" colocados para "false" se comportarem muito similarmente com chaves de símbolos. Ambos são escondidas pelo "Object.keys()" e ambos são revelados com "Reflect.ownKeys()", como visto no exemplo seguinte:
```js
const obj = {}
obj[Symbol()] = 1
Object.defineProperty(obj, 'foo', {
  enumerable: false,	
  value: 2
})
console.log(Object.keys(obj))		/ []
console.log(Reflect.ownKeys(obj))	/ ['foo', Symbol()]
console.log(JSON.stringify(obj))	/ {}
```
Nesse ponto, nós temos aproximadamente recriado símbolos. Ambos nossas strings de propriedade escondidas e símbolos são escondidos dos serializadores. Ambas propriedades podem ser extraídas usando o método "Reflect.ownKeys()" e são então não realmente privadas. Assumindo que nós usamos algum tipo de namespace / valor randômico para versões de strings nos nomes de propriedades então nós temos removido o risco de múltiplas bibliotecas acidentalmente terem um colisão de nome.

Symbols são acessíveis de três formas:
1. Symbols são acessíveis entre realms, e, por realm queremos dizer contexto. Por exemplo, sua página é um contexto de "document" enquanto, dentro dela, podemos ter um *iframe* com um contexto/realm diferente.
2. Você pode registrar Symbols globais e acessa-los por entre esses contextos também.
3. Uma das classes de Symbols é chamada de "Well-Known", eles existem entre realms, mas não são acessíveis no registro global de Symbols. 

Podemos encontrar a chave que foi associada um Symbol através do método "symbol.keyFor(symbol)" que, dado um Sumbol criado previamente, vai nos retornar a chave associada a ele.

Por fim, isso quer dizer que nada impede que outro programados, dentro de outro script da aplicação, também tenha a ideia de criar uma propriedade chamada, por exemplo, de "contador" em "painel" atribuindo um valor completamente diferente do que estamos esperando.

Portanto, evidente que isso nos causrá problemas. A cada clique agora tentaremos incrementar uma string, o que não faz muito sentido. É aí que usamos o symbol.
Podemos listar todos os símbolos que um objeto possui através da função "Object.getOwnPropertySymbols()". Vejamos um exemplo criando um novo script:
```js
Object.getOwnPropertySymbols(painel)		
  .forEach(symbol => console.log(painel[symbol])
```
#### Valores de Parâmetro Padrão:

ES6 permite que parâmetros de funções tenham valores padrões.
```js
function myFunction(x, y = 10) {
  // y é 10 se não passado ou undefined
  return x + y
}
myFunction(5)	// retorna 15
```
#### Rest Parameter da Função:

O rest parameter (...) permite a uma função lidar com um número indefinido de argumentos como um vetor:
```js
function sum(...args) {
  let sum = 0
  for (let arg of args) sum += arg 
  // cria uma variável para lidar com cada argumento do rest parameter
  return sum
}
let x = sum(4, 9, 16, 25, 29, 100, 66, 77)
```
### ECMAScript 2016:

#### Operador de Exponenciação:
O operador de exponenciação (**) calcula o primeiro operando para a potência do segundo operando:
```js
let x = 5
let z = x ** 2	// resultado é 25
```
"x ** y" produz o mesmo resultado que "Math.pow(x, y)".

#### Atribuição de Exponenciação:
O operador de atribuição de exponenciação (**=) calcula o valor de uma variável à potência do operando à direita:
```js
let x = 5
x **= 2	// resultado é 25
```
#### Array.prototype.includes:
ECMAScript 2016 introduziu "Array.prototype.includes" aos vetores. Isso permite-nos checar se um elemento está presente em um vetor:
```js
const fruits = ["Banana", "Orange", "Apple", "Mango"]
fruits.include("Mango")	/ true
```
### ECMAScript 2017

#### Entradas de Objetos no JavaScript
ECMAScript 2017 adicionou um novo método "Object.entries" para objetos:
```js
const person = {
  firstName: "John",
  lastName: "Doe",
  age: 50,
  eyeColor: "blue"
}
document.getElementById("demo").innerHTML = Object.entries(person)	
// firstName,John,lastName,Doe,age,50,eyeColor,blue
```
#### Valores de Objeto em JavaScript:
"Object.values" é similar a "Object.entries", mas retorna um único vetor de dimensão dos valores do objeto:
```js
const person = {
  firstName: "John",
  lastName: "Doe",
  age: 50,
  eyeColor: "blue"
}
document.getElementById("demo").innerHTML = Object.values(person)	
// John,Doe,50,blue
```

### ECMAScript 2018:

#### Iteração Assíncronas em JS:
ECMAScript 2018 adicionou iteráveis e iterações assíncronas. 
Com iteráveis assíncronos, podemos usar a keyword "await" em loops "for/of".
```js
for await () {}
```
#### Promise.finally:
Finalizou a implementação completa do objeto Promise com "Promise.finally":
```js
let myPromise = new Promise()

myPromise.then()
myPromise.catch()
myPromise.finally()
```
#### Rest Properties de Objetos:
Adicionou rest properties. Isso permite-nos desestruturar um objeto e coletar as sobras em um novo objeto:
```js
let { x, y, ...z } = { x: 1, y: 2, a: 3, b: 4 }
x	// 1
y	// 2
z	// {a: 3, b: 4}
```
#### Novas Características do RegExp em JS:

- Sinalizador s (dotAll)
- Unicode Property Escapes (\p{...})
- Lookbehind Assertions (?<= ) and (?<! )
- Named Capture Groups.

## Formulários:

> Validação de Formulário em JavaScript:
Validação de formulário pode ser feita peoo JS. Se um campo de formulário (fname) está vazio, essa função alerta uma mensagem e retorna falso, para previnir que o formulário seja submetido.

function validateForm() {
  var x = document.forms["myForm"]["fname"].value
  if(x == "") {
    alert("Name must be filled out")
    return false
  }
}

A função pode ser chamada quando o formulário é submetido:

<form name="myForm" action="/action_page.php" onsubmit="return validateForm()" method="post">
Name: <input type="text" name="fname">
<input type="submit" value="submit">
</form>

> Validação de Input Numérico

<input id="numb">
<button type="button" onclick="myFunction()">Submit</button>
<p id="demo"></p>

<script>	
function myFunction() {
  var x, text
  x = document.getElementById("numb").value
  
  if (isNaN(x) || x < 1 || x > 10)
    text = "Input not valid"
  } else {
    text = "Input OK"
  }
  document.getElementbyId("demo").innerHTML = text
}
</script>

> Validação de Formulário HTML Automática:
Pode ser executada automaticamente pelo navegador. Se um campo de formulário (fname) está vazio, o atributo "required" previne esse formulário seja submetido:

<form action="/action_page.php" method="post"
.		<input type="text" name="fname" required>
  <input type="submit" value="submit">
</form>

> Validação de Dados:
É um proecesso de assegurar que o input do usuário está claro, correto e útil.
Tarefas típicas de validação:
1. O usuário tem preenchido todos os campos requeridos?
2. O usuário colocou uma data válida?
3. O usuário colocou texto em um campo numérico?

Muito frequentemente, o próposito da validação de dados é assegurar o correto input do usuário.
Validação pode ser definida por muitos diferentes métodos, e implantado em muitas diferentes maneiras.

- Validação Server Side: é executado pelo web server, depois que o input tem sido enviado ao servidor.
- Validação Client Side: é executado pelo navegador, antes que o input seja enviado ao servidor web.

> Validação de Restrição do HTML:
HTML5 introduziu um novo conceito de validação HTML chamado "validação de restrição". Esse novo conceito é baseado em:
1. Validação de restrição de Atributos de Input HTML.
2. Validação de restrição de Pseudo Seletores CSS.
3. Validação de restrição de Métodos e Propriedades do DOM.

> Validação de Restrição de Atributos de Input HTML:

disabled		|	Especifica que o elemento input 			deveria estar desabilitado.
max		|	Valor máximo de um elemento input
min		|	Valor mínimo de um elemento input.
pattern		|	Padrão de valor de um input.
required		|	Campo de input é requerido.
type		|	Especifica o tipo de input.

https://www.w3schools.com/html/html_form_attributes.asp HTML Input Attributes.

> Validação de Restrição de Pseudo-Seletores CSS:

:disabled		|	Seleciona elementos input com o 			atributo "disabled" especificado.
:invalid		|	Elementos com valores inválidos.
:optional		|	Elementos sem atributo "required".
:required		|	Elementos com atributo "required".
:valid		|	Elementos com valores válidos.

https://www.w3schools.com/css/css_pseudo_classes.asp CSS Pseudo Classes.