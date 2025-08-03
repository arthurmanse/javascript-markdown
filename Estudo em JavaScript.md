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

### Validação de Formulário em JavaScript:
Validação de formulário pode ser feita pelo JS. Se um campo de formulário (fname) está vazio, essa função alerta uma mensagem e retorna falso, para previnir que o formulário seja submetido.
```js
function validateForm() {
  var x = document.forms["myForm"]["fname"].value
  if(x == "") {
    alert("Name must be filled out")
    return false
  }
}
```
A função pode ser chamada quando o formulário é submetido:
```js
<form name="myForm" action="/action_page.php" onsubmit="return validateForm()" method="post">
Name: <input type="text" name="fname">
<input type="submit" value="submit">
</form>
```
### Validação de Input Numérico
```js
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
```
### Validação de Formulário HTML Automática:
Pode ser executada automaticamente pelo navegador. Se um campo de formulário (fname) está vazio, o atributo "required" previne esse formulário seja submetido:
```js
<form action="/action_page.php" method="post"
.		<input type="text" name="fname" required>
  <input type="submit" value="submit">
</form>
```
### Validação de Dados:
É um proecesso de assegurar que o input do usuário está claro, correto e útil.
Tarefas típicas de validação:
1. O usuário tem preenchido todos os campos requeridos?
2. O usuário colocou uma data válida?
3. O usuário colocou texto em um campo numérico?

Muito frequentemente, o próposito da validação de dados é assegurar o correto input do usuário.

Validação pode ser definida por muitos diferentes métodos, e implantado em muitas diferentes maneiras.

- Validação Server Side: é executado pelo web server, depois que o input tem sido enviado ao servidor.
- Validação Client Side: é executado pelo navegador, antes que o input seja enviado ao servidor web.

### Validação de Restrição do HTML:
HTML5 introduziu um novo conceito de validação HTML chamado "validação de restrição". Esse novo conceito é baseado em:
1. Validação de restrição de Atributos de Input HTML.
2. Validação de restrição de Pseudo Seletores CSS.
3. Validação de restrição de Métodos e Propriedades do DOM.

### Validação de Restrição de Atributos de Input HTML:

|Atributos| Uso |
|:---:|---|
disabled		|	Especifica que o elemento input deveria estar desabilitado.
max		|	Valor máximo de um elemento input
min		|	Valor mínimo de um elemento input.
pattern		|	Padrão de valor de um input.
required		|	Campo de input é requerido.
type		|	Especifica o tipo de input.

**Para mais formas, acesse o [HTML Input Attributes](https://www.w3schools.com/html/html_form_attributes.asp)**

### Validação de Restrição de Pseudo-Seletores CSS:

|Atributos| Uso |
|:---:|---|
:disabled		|	Seleciona elementos input com o	atributo "disabled" especificado.
:invalid		|	Elementos com valores inválidos.
:optional		|	Elementos sem atributo "required".
:required		|	Elementos com atributo "required".
:valid		|	Elementos com valores válidos.

**Para mais formas, acesse o [CSS Pseudo Classes](https://www.w3schools.com/css/css_pseudo_classes.asp)**

## API DE VALIDAÇÃO EM JAVASCRIPT:

### Validação de Restrição em Métodos de DOM:

* **checkValidity()**	|	Retorna true se um elemento input contém dados válidos.

* **setCustomValidity()**	|	Define a propriedade validationMessage de um elemento input.
  
Se um campo de input contém um dado inválido, disponibilizando uma mensagem:
```js
<input id="id1" type="number" min="100" max="300" required>
<button onclick="myFunction()">OK</button>
<p id="demo"></p>

<script>
function myFunction() {
  var inpObj = document.getElementById("id1")
  if (!inpObj.checkValidty()) {
    document.getElementById("demo").innerHTML = inpObj.validationMessage
  } else {
    document.getElementById("demo").innerHTML = "Input OK"
  }
}
</script>
```
No exemplo acima, a condição testa se o valor não é true e retorna uma messagem do navegador (validationMessage). Essa mensagem estará na lingua em que o navegador está configurado para o usuário. O "validationMessage" é uma propriedade de apenas-leitura. 

### Validação de Restrição com Propriedades do DOM:

|Atributos| Uso |
|:---:|---|
validity		|	Contém propriedades booleanas relacionadas à validade de um elemento input.
validationMessage	|	Contém a messagem que um navegador vai mostrar quando a validade é falsa.
willValidate	|	Indica um valor booleano se um input será validado.


### Propriedades de Validade:
A propriedade de validade de um elemento input contém um número de propriedades relacionadas à validação de dados:

|Atributos| Uso |
|:---:|---|
customError	|	Define como true, se uma mensagem de validade personalizada for definida.
patternMismatch	|	Define como true, se um valor do elemento não corresponde ao seu 		atributo padrão.
rangeOverflow	|	Define como true, se um valor de elemento é maior do que seu atributo máximo.
rangeUnderflow	|	Define como true, se um valor de elemento é menor do que seu atributo mínimo.
stepMismatch	|	Define como true, se um valor do elemento é inválido por seu atributo step.
tooLong		|	Define como true, se um valor do elemento excede o atributo maxLength.
typeMismatch	|	Define como true, se um valor do elemento é inválido por seu atributo type.
valueMissing	|	Define como true, se um elemento (com atributo required) não possui valor.
valid		|	Define como true se um valor do elemento é válido.

#### Exemplos:
```js
<input id="id1" type="number" max="100">
<button onclick="myFunction()">OK</button>
<p id="demo"></p>

<script>
function myFunction() {
  var txt = ""
  if (document.getElementById("id1").validity.rangeOverflow) {
    txt = "Value too large"
  } else {
    txt = "Input OK"
  }
document.getElementById("demo").innerHTML = txt
}
</script>
```

## Objetos em JavaScript:

"Em JavaScript, objetos são reis. Se você entende objetos, você entende JavaScript."

Valores primiticos são imutáveis (eles são codificados e, portanto, não podem ser alterados).

Se x = 3.14, você pode mudar o valor de x, mas não pode mudar alterar o valor de 3.14.

### Objetos são Variáveis:
Objetos são variáveis também, porém podem conter muitos valores.

Os valores são escritos em pares "nome : valor" (nome e valor separados por dois pontos). Ou seja: um objeto é uma coleção de valores nomeados.

Os valores nomeados nos objetos são chamados de "propriedades". Os objetos escritos como valores nomeados são similares aos:
- Vetores associativos em PHP;
- Dicionários em Python;
- Tabelas Hash em C;
- Mapas Hash em Java;
- Hashes em Ruby e Perl.

### Métodos:
Métodos são ações que podem ser executadas em objetos. Propriedades de objeto podem ser tanto valores primitivos, outros objetos, e funções.

Um método de objeto é uma propriedade de objeto que contém uma definição de função.

### Criando um Objeto em JavaScript:

Há diferentes formas de criar um novo objeto:
1. Defina e crie um único objeto usando um literal de objeto.
2. Defina e crie um único objeto com a keyword "new".
3. Defina um objeto constructor, e então crie objetos do tipo construído.
4. A partir do ECMAScript 5, um objeto também pode ser criado com a função "Object.create()".

### Usando um Literal de Objeto:
A maneira mais fácil de criar um objeto é usando um literal de objeto, no qual, você tanto pode definir e criar um objeto em uma declaração.

Um Literal de Objeto é uma lista de pares de nome:valor (como "age:50") dentro de chaves { }.

### Usando a keyword "new" para criar Objetos:
```js
var person = new Object()
person.firstName = "John"
person.lastName = "Doe"
person.age = 50
person.eyeColor = "blue"
```
O exemplo acima não é necessário, além de ser mais difícil, menos legível, e mais lento do que o método em { }.

### Objetos JS são Mutáveis:
Objetos são mutáveis: eles são endereçados pela referências, e não pelo valor. Se "person" é um objeto, a declaração seguinte não criará uma cópia de "person":
```js
var x = person	// Isso não criará cópia de person.
```
O objeto x não é uma cópia de person. Ele É "person". Ambos "x" e "person" são o mesmo objeto.

Qualquer alteração em x também mudará person, pois x e person são o mesmo objeto.
```js
var person = {firstName: "John", lastName: "Doe", age: 50, eyeColor:"blue"}

var x = person
x.age = 10	/ muda x.age e x.person
```

## Propriedades de Objetos: 

Propriedades podem usualmente ser alteradas, adicionadas e deletadas, mas algumas são de apenas leitura.

### Acessando Propriedades em JavaScript:
A sintax para acessar a propriedade de um objeto é:
```js
objectName.property		/ person.age
objectName["property"]	/ person["age"]
objectName[expression]	/ x = "age"; person[x]
```
A expressão deve ser avaliada como um nome de propriedade.

### Loop for...in :

A declaração "for...in" repete através das propriedades de um objeto.

**Sintaxe:**
```js
for (variável in objeto) {
  // código para ser executado
}
```
O bloco de código dentro do loop for...in será executado uma vez para cada propriedade.
  
Iterando através das propriedades de um objeto:
```js
var person = {fname: "John", lname: "Doe", age: 25}
for (x in person) {
  txt += person[x] + " "
} // John Doe 25
```
### Adicionando Novas Propriedades:
Você pode adicionar novas propriedades a um objeto existente através de simplesmente dá-lo um valor.

Assumindo que o objeto "person" já existe - você pode então dar-lo novas propriedades:
```js
person.nationality = "English"
```
### Deletando Propriedades:
A keyword "delete" deleta uma propriedade de um objeto:
```js
var person = {firstName:"John", lastName:"Doe", age:50, eyeColor:"blue"}
delete person.age	/ ou delete person["age"]
```
A keyword "delete" deleta ambos os valores da propriedade e a propriedade por si só.
Após deletar, a propriedade não pode ser usada antes de adicionada novamente.

O operador "delete" foi projetado para ser usado em propriedades de objetos. Ele não tem efeito sobre variáveis ou funções.

O operador não deve ser usado em propriedades de objeto predefinidas em JS. Isso pode quebrar sua aplicação.

### Atributos de Propriedades:
Todas as propriedades tem um nome. Além disso, elas também tem um valor. O valor é um dos atributos da propriedade.

Outros atributos são: enumerable, configurable e writable.

Esses atributos definem como a propriedade pode ser acessada (ela é legível? ela é escrevível?).

Em JS, todos atributos podem ser lidos, mas apenas o atributo de valor pode ser mudado (e apenas se a propriedade é escrevível).

ECMAScript 5 tem métodos para ambos receber e definir todos atributos de propriedade.

### Propriedades Prototype:
Objetos em JS herdam as propriedades de seus protótipos. 

A keyword "delete" não deleta propriedades herdadas, mas se você deletar uma propriedade de protótipo, ela afetará todos os objetos herdados do protótipo.

## Métodos de Objetos:
```js
var person = {
  firstName: "John",
  lastName: "Doe",
  id: 5566,
  fullName: function() {
    return this.firstName + " " + this.lastName
  }
}
```
### Acessando Métodos de Objetos:
Você pode acessar métodos de objetos com a seguinte sintaxe:
```js
objectName.methodName()
```
Você vai tipicamente descrever fullName() como um método do objeto "person", e fullName como uma propriedade.

A propriedade "fullName" executará (como uma função) quando for invocada com ().
Esse exemplo acessa o método:
```js
name = person.fullName()
```
Se você acessar a propriedade fullName sem (), ela retornará a definição da função:
```js
name = person.fullName
/ function() { return this.firstName + " " + this.lastName; }
```
### Usando Métodos Embutidos:
Esse exemplo usa o método "toUpperCase()" do objeto String para converter um texto para caixa-alta:
```js
var message = "Hello World!"
var x = message.toUpperCase()
// O valor de x após a execução do código acima será: HELLO WORLD!
```
### Adicionando um Método ao Objeto:
```js
person.name = function () {
  return this.firstName + " " + this.lastName
}
```

## Objetos de Exibição JavaScript:
Exibindo um objeto em JS vai retornar [object Object]
```js
var person = {name:"John", age:30, city:"New York"};
document.getElementById("demo").innerHTML = person
// [object Object]
```
Algumas soluções comuns para exibir objetos em JS são:
1. Exibindo as Propriedades de Objetos pelo nome;
2. Exibindo as Propriedades de Objetos em um loop;
3. Exibindo o Objeto usando Object.values()
4. Exibindo o Objeto usando JSON.stringify()

### Exibindo Propriedades de Objeto:
As propriedades de um objeto pode ser exibilidas como uma string:
```js
var person = {name:"John", age:30, city:"New York"}
document.getElementById("demo").innerHTML = 
person.name + ", " + person.age + ", " + person.city
// John, 30, New York
```
### Exibindo o Objeto em um Loop:
As propriedades de objeto pode ser coletadas em um loop:
```js
var x, txt = ""
var person = {name:"John", age:50, city:"New York"}

for (x in person) {
  txt += person[x] + " "
}
document.getElementById("demo").innerHTML = txt
// John 50 New York
```
Atenção: Você deve usar "person[x]" no loop. "person.x" não irá funcionar (porque x é uma variável)

### Usando Object.values()
Qualquer objeto em JavaScript pode ser converido em um vetor usando "Object.values()".
```js
var person = {name:"John", age:30, city:"New York"}
var myArray = Object.values(person)

//myArray é agora um vetor, pronta para ser exibida:
// John,50,New York
```
### Usando JSON.stringify()
Qualquer objeto pode ser "stringuifado" (convertido para uma string) com a função JSON.stringify()
```js
var person = {name:"John", age:30, city: "New York"};

var myString = JSON.stringify(person);
document.getElementById("demo").innerHTML= myString;
// {"name":"John","age":50,"city":"New York"}
```
### Stringify Datas:
JSON.stringify converte datas em strings:
```js
var person = {name: "John", today: new Date()}
var myString = JSON.stringify(person)
document.getElementById("demo").innerHTML = myString
// {"name":"John","today":"2021-02-21T03:31:21.576Z"}
```
### Stringify Funções:
JSON.stringify não converterá funções:
```js
var person = {name:"John", age:function () {return 30}}
var myString = JSON.stringify(person)
document.getElementById("demo").innerHTML = myString
// {"name":"John"}
```
Isso pode ser "corrigido" se você converter a função em strings antes de "stringuifar".
```js
var person = {name:"John", age:function() {return 30}}
person.age = person.age.toString()

var myString = JSON.stringify(person)
document.getElementById("demo").innerHTML = myString
```
### Stringify Vetores:
É também possível stringify vetores em JavaScript:
```js
var arr = ["John", "Peter", "Sally", "Jane"]
var myString = JSON.stringify(arr)
document.getElementById("demo").innerHTML = myString
// ["John","Peter","Sally","Jane"]
```

## Acessores de Objetos em JavaScript:

### Acessores JavaScript (Getters e Setters)
Getters e Setters permitem-nos definir Acessores de Objetos (Propriedades Computadas).

#### Getter (a keyword get):
Esse exemplo usa uma propriedade "lang" para receber o valor da propriedade "language":
```js
var person = {
  firstName: "John",
  lastName: "Doe",
  language: "en",
  get lang() {
    return this.language
  }
}
document.getElementById("demo").innerHTML = person.lang // "en"
```
#### Setter (a keyword set)
Esse exemplo usa uma propriedade "lang" para definir o valor da propriedade "language".
```js
var person = {
  firstName: "John",
  lastName: "Doe",
  language: "",
  set lang(lang) {
    this.language = lang
  }
}
person.lang = "en"
document.getElementById("demo").innerHTML = person.language
// "en"
```
### Função ou Getter?
Uma função dentro do objeto é acessada: person.fullName().

Um getter é acesso como uma propriedade: person.fullName.

Ou seja: getters oferecem uma sintaxe mais simples.

### Qualidade de Dados:
JavaScript pode assegurar melhores qualidades de dados ao usar getters e setters.
Usando a propriedade "lang", nesse exemplo, retorna o valor da propriedade "language" em caixa-alta:
```js
var person = {
  firstName: "John",
  lastName: "Doe",
  language: "en",
  get lang() {
    return this.language.toUpperCase()
  }
}
document.getElementById("demo").innerHTML = person.lang
// "EN"	
```
Usando a propriedade "lang", nesse exemplo, armazena um valor em caixa-alta na propriedade "language":
```js
var person = {
  firstName: "John",
  lastName: "Doe",
  language: "",
  set lang(lang) {
    this.language = lang.toUpperCase()
  }
}
person.lang = "en"
document.getElementById("demo").innerHTML = person.language	
```
### Por que Usar Getters e Setters:

1. Fornece uma sintaxe mais simples;
2. Permite sintaxes iguais para propriedades e métodos;
3. Pode assegurar melhores qualidades de dados;
4. É útil em fazer coisas "por trás do cenário".

### Object.defineProperty()
O método "Object.defineProperty()" pode também ser usado para adicionar Getters e Setters:
```js
// define o objeto:
var obj = {counter: 0}

// Define os setters:
Object.defineProperty(obj, "reset", {
  get : function () {this.counter = 0}
})
Object.defineProperty(obj, "increment", {
  get : function () {this.counter++}
})
Object.defineProperty(obj, "decrement", {
  get : function () {this.counter--}
})
Object.defineProperty(obj, "add", {
  set : function (value) {this.counter += value}
})
Object.defineProperty(obj, "subtract", {
  set : function (value) {this.counter -= value}
})

// Brinque com o contador:
obj.reset
obj.add = 5
obj.subtract = 1
obj.increment
obj.decrement
obj.decrement
document.getElementById("demo").innerHTML = obj.counter
// "3"
```

## Objects Constructors:
```js
function Person(first, last, age, eye) {
  this.firstName = first
  this.lastName = last
  this.age = age
  this.eyeColor = eye
}

var myFather = new Person("John", "Doe", 50, "blue")

document.getElementById("demo").innerHTML = "My father is " + myFather.age + "."
// "My father is 50.
```
**Atenção: É considerado uma boa prática nomear funções construtoras com a primeira letra em caixa-alta.**

### Tipos de Objeto (Blueprints) (Classes)
Os exemplos dos capítulos anteriores são limitados. Eles apenas criam objetos únicos. Às vezes, nós precisamos de "blueprints" para criar muitos objetos do mesmo "tipo".

A forma que criamos um "tipo de objeto" é usando uma "função construtora de objeto".
No exemplo acima, "function Person()" é uma função construtora de objeto.

Objetos do mesmo tipo são criados por invocação da função construtora com a keyword "new".
```js
var myFather = new Person("John", "Doe", 50, "blue")
var myMother = new Person("Sally", "Rally", 48, "green")
```
### Keyword "this" em Construtores:
Em uma função construtora, this não tem um valor. Ele é um substituto para o novo objeto. O valor de this tornará-se o novo objeto quando um novo objeto é criado.

**Atenção: Note que "this" não é uma variável, mas sim um keyword. Não se pode mudar o valor de "this".**

### Adicionando uma Propriedade ao Constructor:
Você não é capaz de adicionar uma nova propriedade a um construtor de objeto da mesma forma que você adiciona uma nova propriedade a um objeto existente.

Para adicionar uma nova propriedade a um construtor, você deve adicionar à função construtora:
```js
function Person(first, last, age, eyecolor) {
  this.firstName = first
  this.lastName = last
  this.age = age
  this.eyeColor = eyecolor
  this.nationality = "English"
}
```
Dessa forma, propriedades de objetos podem ter valores padrão.

### Adicionando um Método a um Construtor:
Sua função construtora pode também definir métodos:
```js
function Person(first, last, age, eyecolor) {
  this.firstName = first
  this.lastName = last
  this.age = age
  this.eyeColor = eyecolor
  this.name = function() {return this.firstName + " " + this.lastName}
}
```
Você não pode adicionar um novo método a um objeto construtor da mesma forma que você adiciona um novo método a um objeto existente.

Adicionar métodos a um construtor de objeto deve ser feito dentro da função construtora:
```js
function Person(firstName, lastName, age, eyeColor) {
  this.firstName = firstName
  this.lastName = lastName
  this.age = age
  this.eyeColor = eyeColor
  this.changeName = function(name) {
    this.lastName = name
  }
}
```
A função changeName() atribui o valor de name (parâmetro) para a propriedade lastName de person.
```js
var myMother = new Person("Sally", "Rally", 48, "green")
myMother.changeName("Doe")

document.getElementById("demo").innerHTML = "My mother's last name is " + myMlther.lastName
// "My mother's last name is Doe"
```
JavaScript sabe qual pessoa você falando sobre ao "substituir" this com myMother.

Atenção: "Math" é um tipo JS, sendo um objeto global. A keyword "new" não pode ser usada em "Math".

Atenção: Não há razão para criar objetos complexos. Valores primitivos são muito mais rápidos.

Portanto:
Use literais de objetos { } ao invés de "new Object()".

O mesmo vale para outros valores primitivos, funções, RegExp, vetores, etc.

## Protótipos de Objetos em JS:

### Herança em Protótipos:
Todos os objetos em JavaScript herdam propriedades e métodos de um protótipo.
- Objetos de Data herdam o "Date.prototype".
- Objetos de Vetor herdam o "Array.prototype".
- Objetos "Person" herdam o "Person.prototype".

O "Object.prototype" é no topo do cadeia de herança de protótipos:
Objetos de Data, Vetores, e "Person" herdam do "Object.prototype".

### Adicionando Propriedades e Métodos aos Objetos:

- Usando a Propriedade "prototype":
A propriedade "prototype" permite adicionar novas propriedades a construtores de objetos:
```js
function Person(first, last, age, eyecolor) {
  this.firstName = first
  this.lastName = last
  this.age = age
  this.eyeColor = eyecolor
}
Person.prototype.nationality = "English"
```
A propriedade "prototype" também permite adicionar novos métodos a construtores de objetos:
```js
function Person(first, last, age, eyecolor) {
  this.firstName = first
  this.lastName = last
  this.age = age
  this.eyeColor = eyecolor
}
Person.prototype.name = function() {
  return this.firstName + " " + this.lastName
}
```
**Atenção: Apenas altere seus próprios protótipos. Nunca modifique os protótipos dos objetos padrões do JavaScript.**


## Métodos de Objeto ES5:
ES5 adicionou vários novos métodos:
```js
// Adicionar ou mudar uma propriedade de objeto:
Object.defineProperty(object, property, descriptor)

// Adicionar ou mudar várias propriedades de objeto:
Object.defineProperties(object, descriptors)

// Acessar propriedades
Object.getOwnPropertyDescriptor(object, property)

// Retorna todas propriedades como um vetor:
Object.getOwnPropertyNames(object)

// Retorna propriedades enumeradas como um vetor:
Object.keys(object)

// Acessar o protótipo:
Object.getPrototypeOf(object)

// Previne adicionar propriedades a um objeto:
Object.preventExtensions(object)

// Retorna true se propriedades podem ser adicionadas a um objeto:
Object.isExtensible(object)

// Previne mudanças de propriedades de objeto (não valores):
Object.seal(object)

// Retorna true se o objeto está selado:
Object.isSealed(object)

// Previne qualquer mudança a um objeto:
Object.freeze(object)
  
// Retorna true se object está "congelado":
Object.isFrozen(object)
```
### Mudando um Valor de Propriedade:
```js
Object.defineProperty(object, property, {value : value}}
```
**Exemplo:**
```js
var person = {
  firstName: "John",
  lastName: "Doe",
  language: "EN"
}
Object.defineProperty(person, "language", {value : "NO"})
```
### Alterando Metadados:
ES5 permite que as propriedades de metadados a seguir sejam alterados:
```js
writable: true	// valor da propriedade pode ser alterado
enumerable: true	// propriedade pode ser enumerada
configurable: true	// propriedade pode ser reconfigurada
```
ES5 permite que getters e setters sejam alterados:
```js
// definindo um getter:
get: function () { return language } 

// definindo um setter:
set: function(value) { language = value }
```
Esse exemplo faz "language" apenas-leitura:
```js
Object.defineProperty(person, "language", {writable: false})
```
Esse exemplo faz "language" não enumerável:
```js
Object.defineProperty(person, "language", {enumerable: false})
```
### Listando Todas as Propriedades:
Esse exemplo lista todas as propriedades de um objeto:
```js
var person = {
  firstName: "John",
  lastName: "Doe",
  language: "EN"
}
Object.defineProperty(person, "language", {enumerable: false})
Object.getOwnPropertyNames(person)
// firstName,lastName,language
```
### Listando Propriedades Enumeráveis:	
```js
var person = {
  firstName: "John",
  lastName: "Doe",
  language: "EN"
}
Object.defineProperty(person, "language", {enumerable: false})
Object.keys(person)
// firstName,lastName
```
### Adicionando uma Propriedade:
```js
var person = {
  firstName: "John",
  lastName: "Doe",
  language: "EN"
}
Object.defineProperty(person, "year", {value: "2008"}) 
```
**Exercício:**
```js
var person = {
    firstName: "John",
    lastName : "Doe",
    language : "EN"
};
var adt = "year"
var valor = "2008"
Object.defineProperty(person, adt, {value:valor})
var release = person[adt]

document.getElementById("demo").innerHTML = release;
// 2008
```
### Adicionando Getters e Setters:
O método Object.defineProperty() também pode ser usado para adicionar Getters e Setters:
```js  
var person = {firstName: "John", lastName: "Doe"}

Object.defineProperty(person, "fullName", {
  get : function() { return this.firstName + " " + this.lastName}
})
```
## Funções em JavaScript:
  
### Expressão de Função
Uma função pode também ser definida usando uma expressão. Uma expressão de função pode ser armezenada como uma variável:
```js
var x = function (a, b) {return a * b}
```
Após uma expressão de função ter sido armazenada em uma variável, a variável pode ser usada como função:
```js
var x = function (a, b) {return a * b};
var z = x(4, 3);
```
A função acima é realmente uma "função anônima" (uma função sem um nome). Uma função armazenada em variáveis não necessitam de nomes de funções. Elas são sempre invocadas usando o nome da variável.

**Atenção: A função acima termina com um ponto e vírgula porque é parte de uma declaração executável.**

### O Constructor Function()
Como visto nos exemplos anteriores, funções são definidas com a keyword "function".
As funções podem também ser definidas com uma função construtora embutida chamada "Function()"
```js
var myFunction = new Function("a", "b", "return a * b")
var x = myFunction(4, 3)
```
Você realmente não precisa usar a função construtora, pois funciona da mesma forma que o exemplo anterior.

**Atenção: Na maior parte do tempo, você pode evitar de usar a keyword "new" em JavaScript.**

### Funções Auto-Invocadas:
Expressões de funções podem ser "auto-invocadas". Uma expressão auto-invocada é invocada (iniciada) automaticamente, sem ser chamada.

Expressões de função executarão automaticamente se a expressão é seguida por ().
Você não pode auto-invocar uma declaração de função.

Você tem que adicionar parênteses ao redor da função para indicar que é uma expressão de função:
```js
(function () {
  document.getElementById("demo").innerHTML = 
"Hello! I called myself"
})()
// A função é executada ao carregar a página.
```
A função acima é realmente uma função anônima auto-invocadora (função sem nome):

### Funções Podem Ser Usadas Como Valores:
```js
function myFunction(a, b) {
  return a * b
}
var x = myFunction(4, 3) * 2
// 24
```
### Funções São Objetos:
O operador "typeof" em JavaScript retorna "function" para funções. Porém, funções em JS podem ser melhor descritas como objetos.

Funções tem ambos "propriedade" e "métodos".

A propriedade "arguments.length" retorna o número de argumentos recebidos quando a função foi invocada:
```js
function myFunction(a, b) {
  return arguments.length
}
// 2
```
O método "toString()" retorna a função como string:
```js
function myFunction(a, b) {
  return a * b
}
var txt = myFunction.toString()
// "function myFunction(a, b) { return a * b; }"
```
Atenção: Uma função designada para criar novos objetos é chamada de um construtor de objetos.

### Arrow Functions:
Arrow functions permitem uma sintaxe mais curta para escrever expressões de funções.
Você não precisa da keyword "function", da keyword "return", e das chaves { }.
```js
// ES5
var x = function(x, y) {
  return x * y
}

// ES6
const x = (x, y) => x * y
```
Arrow functions não possuem seus próprios "this". Eles não são bem adequados em definir métodos de objetos.

Arrow functions não são içadas. Eles devem ser definidas antes de serem usadas.
Usando const é mais seguro do que var, porque uma expressão de função está sempre em valor constante.

Você pode apenas omitir a keyword "return" e as chaves se a função é de apenas uma única declaração. Por isso, pode ser um bom hábito sempre manter assim:
```js
const x = (x, y) => { return x * y )
```

## Parâmetros de Função: 

Uma função JavaScript não executa qualquer verificação sobre valores de parâmetro (argumentos).

### Argumentos e Parâmetros:
Parâmetros de função são os nomes listados na definição de função.
Argumentos de função são os valores reais passados para a (e recebidos pela) função.
```js
function functionName(parameter1, parameter2, parameter3) {
  // código a ser executado
}
```
### Regras de Parâmetros:
Definições de função não especificam tipos de dados para parâmetros.

Funções não executam checagem de tipo sobre argumentos passados.

Funções não verificam o número de argumentos recebidos.

### Objetos de Argumentos:
Funções tem objetos embutidos chamados de objeto de argumento. Os objetos de argumento contém um vetor dos argumentos usados quando a função é invocada.

Dessa forma, você pode simplesmente usar uma função para encontrar (por exemplo) o valor mais alto em uma lista de números:
```js
x = findMax(1, 123, 500, 115, 44, 88)

function findMax() {
  var i
  var max = -Infinity
  for (i = 0; i < arguments.length; i++) {
    if (arguments[i] > max) {
      max = arguments[i]
    }
  }
  return max
}
```
Ou crie uma função para somar todos os valores de entrada:
```js
x = sumAll(1, 125, 500, 115, 44, 88) 

function sumAll() {
  var i
  var sum = 0
  for (i = 0; i < arguments.length; i++) {
    sum += arguments[i]
  }
  return sum
}
```
**Atenção: Se uma função é invocada com muitos argumentos (mais do que declarado), esses argumentos podem ser alcançados usando os objetos de argumentos.**

### Argumentos São Passados Pelo Valor:
Os parâmetros, em uma chamada de função, são argumentos de função. Os argumentos em JS são passados pelo valor: a função apenas recebe para conhecer os valores, não as localizações dos argumentos.

Se uma função altera um valor de argumento, ela não altera o valor original do parâmetro.

Alterações em argumentos não são visíveis (refletidas) fora da função.

### Objetos são Passados pela Referência:
Em JS, referências de objetos são valores. Por causa idsso, objetos se comportarão como se fossem passadas pela referência:

Se uma função altera uma propriedade de objeto, ela muda o valor original.
Alterações em propriedades de objetos são visíveis (refletidas) fora da função.

## Invocação da Função:

### Invocando uma Função como uma Função:
```js
function myFunction(a, b) {
  return a * b
}
myFunction(10, 2)	// retorna 20
```
A função acima acima não pertence a qualquer objeto. Porém, em JS sempre há um objeto padrão global.

Em HTML, o objeto global é a própria página HTML. Então a função pertence à página HTML.

Em um navegador, o objeto da página é o window do navegador. A função acima automaticamente torna-se uma função de window.

myFunction() e window.myFunction() é a mesma função:
```js
function myFunction(a, b) {
  return a * b
}
window.myFunction(10, 2) 	// retorna 20
```
**Atenção: Embora seja uma forma comum de invocar uma função JS, não é uma prática muito boa, no qual, pode gerar conflitos e bugs no objeto global.**

**Atenção: Quando uma função é chamada sem um objeto proprietário, o valor de "this" torna-se o objeto global. Com isso, evite essa prática.**

### Invocando uma Função com a Função Construtora:
Se uma função construtora é precedida com a keyword "new", ela é uma invocação construtora.

Parece que você uma nova função, mas já que em JavaScript as funções são objetos, você na verdade cria um novo objeto:
```js
// Essa é uma função construtora:
function myFunction(arg1, arg2) {
  this.firstName = arg1
  this.lastName = arg2
}

// Isso cria um novo objeto:
var x = new myFunction("John", "Doe")
x.firstName	/ retorna "John"
```
Uma invocação construtora cria um novo objeto. O novo objeto herda as propriedades e métodos de seu construtor.

**Atenção: "this" na construtora não tem um valor. O valor será o novo objeto criado quando a função é invocada.**

## Chamada da Função: 

### Método de Reuso:
Com o método "call()", você pode escrever um método que pode ser usado em diferentes objetos.

### Todas Funções são Métodos:
Em JavaScript, todas as funções são métodos de obejtos. Se uma função não é um método de um objeto JS, ela é uma função do objeto global.

O exemplo abaixo cria um objeto com 3 propriedades, firstName, lastName, fullName.
```js
var person = {
  firstName:"John",
  lastName:"Doe",
  fullName: function () {
    return this.firstName + " " + this.lastName
  }
}
person.fullName()	// retorna "John Doe"
```
No exemplo acima, o "this" pertence à função fullName. Em outras palavras, this.firstName significa a propriedade "firstName" desse objeto.

### Método call()
O método call() é um método predefinido em JavaScript.

Ele pode ser usado para invocar (chamar) um método com um objeto proprietário como um argumento (parâmetro).

**Atenção: Com call(), um objeto pode usar um método pertencente a um outro objeto.**

Esse exemplo chama o método fullName de "person", usando o "person1":
```js
var person = {
  fullName: function() {
    return this.firstName + " " + this.lastName
  }
}
var person1 = {
  firstName:"John",
  lastName:"Doe"
}
var person2 = {
  firstName:"Mary",
  lastName:"Doe"
}
person.fullName.call(person1)	// retorna "John Doe"
```
### O Método call() com Argumentos:
O método call() pode aceitar argumentos:
```js  
var person = {	
  fullName: function(city, country) {
    return this.firstName + " " + this.lastName + ", " + city + ", " + country
  }
}
var person1 = {
  firstName: "John",
  lastName: "Doe"
}
person.fullName.call(person1, "Oslo", "Norway")
```

## Function Apply:

### Método de Reuso:
Com o método "apply()", você pode escrever um método que pode ser usado em diferentes objetos.

### O Método "apply()":
O método "apply()" é similar ao método "call()".
Nesse exemplo, o método fullName de "person" é aplicado no "person1":
```js
var person = {
  fullName: function() {
    return this.firstName + " " + this.lastName
  }
}
var person1 = {
  firstName: "Mary",
  lastName: "Doe"
}
person.fullName.apply(person1)	// "Marry Doe"
```
### A Diferença Entre call() e apply()
A diferença é:

- O método "call()" pega argumentos separadamente.
- O método "apply()" pega argumentos como um vetor.

**Atenção: O método "apply()" é bastante conveniente se você quer usar um vetor ao invés de uma lista de argumentos.**

### O Método apply() com Argumentos:
O método apply() aceita argumentos em um vetor:
```js
var perosn = {
  fullName: function(city, country) {
    return this.firstName + " " + this.lastName + ", " + city + ", " + country
  }
}
var person1 = {
  firstName: "John",
  lastName: "Doe"
}
person.fullName.apply(person1, ["Oslo", "Norway"])
// John Doe, Oslo, Norway
```
### Simulando um Método Max em Vetores:
Você pode encontrar o maior número (em uma lista de números) usando o método "Math.max()":
```js
Math.max(1, 2, 3)	// retorna 3
```
Embora vetores em JS não tenham um método "max()", você pode aplicar o método "Math.max()".
```js
Math.max.apply(null, [1, 2, 3]) // retorna 3
```
O primeiro argumento (null) não importa. Não é usado nesse exemplo.
Esse exemplo dará o mesmo resultado:
```js
Math.max.apply(Math, [1, 2, 3]) // retorna 3

Math.max.apply(" ", [1, 2, 3]) // retorna 3

Math.max.apply(0, [1, 2, 3]) // retorna 3
```
### Modo Estrito
No Modo Estrito, se o primeiro argumento do método "apply()" não é um objeto, ele torna-se o proprietário (objeto) da função invocada. No modo "não-estrito", ele torna-se o objeto global.

## Fechamento em Funções JavaScript:

**Atenção: Variáveis criadas sem uma keyword de declaração (var, let ou const) são sempre globais, mesmo se elas são criadas dentro de uma função.**

### O Dilema do Contador:
Suponha que você queira usar uma variável para contar algo, e você quer que esse contador seja disponível para todas as funções.

Você poderia usar uma variável global, e uma função para incrementar o contador:
```js
var counter = 0

function add() {
  counter += 1
}

add()
add()
add()
// O contador deve agora ser 3
```
Há um problema com a solução acima: Qualquer código na página pode mudar o contador sem chamar add(). O contador deve ser local para função add() para prevenir que outro código o altere:
```js
var counter = 0

function add() {
  var counter = 0
  counter += 1
}

add() 
add()
add()
// O contador deveria ser 3, mas é 0
```
Ele não funciona por que nós exibimos o contador global ao invés do contador local.
Nós podemos remover o contador global e acessar o contador local deixando a função retorna-la:
```js
function add() {
  var counter = 0
  counter += 1
  return counter
}

add()
add()
add()
// O contador deveria ser 3, mas é 1.
```
Isso não funciona porque nós resetamos o contador local toda vez que chamamos a função.
Uma função interna do JS pode resolver isso:

### Funções Aninhadas
Todas as funções têm acesso ao escopo global. De fato, em JS, todas as funções tem acesso ao escopo acima delas.

JavaScript permite funções aninhadas. Elas tem acesso ao escopo acima delas. 
Nesse exemplo, a função interna "plus()" tem acesso à variável "counter" na função-mãe:
```js
function add() {
  var counter = 0
  function plus() { counter +=1 }
  plus ()
  return counter
}
```
Isso poderia ter resolvido o dilema do contador se pudessemos alcançar a função "plus()" a partir de fora.

Nós também precisamos encontrar uma forma de executar "counter = 0" apenas uma vez.
Vamos precisar de um fechamento.

### Fechamentos em JavaScript:
Lembra-se das funções auto-invocadas?
```js
var add = (function () {
  var counter = 0
  return function () { counter += 1; return counter}
})()
add()
add()
add()
// O contador é 3.
```
### Exemplo Explicado:
A variável "add" é atribuída ao valor de retorno de uma função auto-invocada.

A função auto-invocada apenas executa uma vez. Ela define o contador em zero, e retorna uma expressão de função. Dessa forma, "add" tornar-se uma função. 

A parte "maravilhosa" é que ela pode acessar o contador no escopo acima.
Isso é chamado de Fechamento em JavaScript. Isso torna possível para uma função ter variáveis privadas.

O contador é protegido pelo escopo da função anônima e pode apenas ser alterada usando a função "add".

**Atenção: Um Fechamento é uma função tendo acesso ao escopo acima, mesmo depois que a função-pai foi fechada.**

## Classes em JavaScript:

**Atenção: O método constructor é chamado automaticamente quando um novo objeto é criado.**

### O Método Constructor:
O método constructor é um método especial:
  
- Tem de ser do mesmo nome "constructor";
- É executado automaticamente quando um novo objeto é criado;
- É usado para inicializar propriedades de obejtos.

Se você não definir o método constructor, JS vai adicionar um método constructor vazio.

### Métodos de Classe:
São criados com a mesma sintaxe como métodos de objeto.
Use a keyword "class" para criar uma classe. Sempre adicione um método "constructor()". Então adicione qualquer número de métodos:
```js
class ClassName {
  constructor() { ... }
  method_1 { ... }
  method_2 { ... }
  method_3 { ... }
}
```
Crie um método de classe chamado "age" que retorna a idade do carro:
```js
clas Car {
  constructor(name, year) {
    this.name = name
    this.year = year
  }
  age() {
    let date = new Date()
    return date.getFullYear() - this.year
  }
}

let myCar = new Car("Ford", 2014)
document.getElementById("demo").innerHTML = "My car is " + myCar.age() + " years old."
```
Você pode enviar parâmetros para métodos de classe:
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

// o this.name é escopo local. O "year" em myCar.age(year) refere-se a variável let year de escopo global.
```
### "use strict"
A sintaxe em classes devem ser escritas em "modo estrito". Você irá receber um erro se não seguir as regras do "modo estrito".
```js
class Car {	
  constructor(name, year) {
    this.name = name
    this.year = year
  }
age() {	
  / date = new Date()  		/ não funcionará
  let date = new Date()		/ funcionará
  return date.getFullYear() - this.year
}
}
```

## Herança de Classe: 

Para criar uma herança de classe, use a keyword "extends"
Uma classe criada com uma herança de classe herda todos os métodos de uma outra classe:
```js
class Car {
  constructor(brand) {
    this.carname = brand
  }
  present() {
    return "I have a " + this.carname
  }
}

class Model extends Car {
  constructor(brand, mod) {
    super(brand)
    this.model = mod
  }
  show() {
    return this.present() + ", it is a " + this.model
  }
}

let myCar = new Model("Ford", "Mustang")
document.getElementById("demo".innerHTML = myCar.show()
```
O método "super()" refere-se à classe-pai.

Ao chamar o método "super()" no método constructor, nós chamamos o método constructor do "pai" e recebemos acesso às propriedades dos pais e métodos.

**Atenção: Herança é útil para reusabilidade de código: reusar propriedades e métodos de uma classe existente quando você cria uma nova classe.**

### Getters e Setters:
Classes também permitem usar getters e setters.

Pode ser inteligente usar getters e setters para suas propriedades, especialmente se você quer fazer algo especial com o valor antes de retorná-lo, ou antes de defini-los. 

Para adicionar getters e setters numa classe, use keywords "get" e "set".
```js
class Car {
  constructor(brand) {
    this.carname = brand
  }
  get cnam() {
    return this.carname
  }
  set cnam(x) {
    this.carname = x
  }
}

let myCar = new Car("Ford")
document.getElementById("demo").innerHTML = myCar.cnam
// "Ford"
```
**Atenção: Mesmo se o getter é um método, você não precisa usar parênteses quando quer receber um valor de propriedade.**

O nome de método getter/setter não pode ser o mesmo nome da propriedade, nesse caso "carname".

Muitos programadores usam um caractere underscore (_) antes do nome da propriedade para separar o getter/setter da propriedade real:
```js
class Car {
  constructor(brand) {
    this._carname = brand
  }
  get carname() {
    return this._carname
  }
  set carname(x) {		
    this._carname = x
  }
}

let myCar = new Car("Ford")
document.getElementById("demo").innerHTML = myCar.carname
```
Para usar um setter, use a mesma sintaxe como quando você define um valor de propriedade, sem parênteses:

Mudando o "carname" para "Volvo".
```js
class Car {
  constructor(brand, year) {
    this._carname = brand
    this.year = year
  }
  get carname() {
    return this._carname + " " + this.year
  }
  set carname(x) {
    this._carname = x
  }
}

let myCar = new Car("Ford", 2014)
myCar.carname = "Volvo"
document.getElementById("demo").innerHTML = myCar.carname
// Volvo 2014
```
### Içamento:
Diferentemente de funções, e outras declarações JS, declarações de classe não são içadas.

Isso significa que você deve declara uma classe antes de você usá-la.

**Atenção: Para outras declarações, como funções, você não receberá um erro quando tentar usar antes de ser declado, porque o comportamento padrão de declarações JS são de içamento (movendo a declaração para o topo).
**

## Métodos Estáticos:

Métodos de classe estáticas são definidos na própria classe. Você não pode chamar um método estático em um objeto, apenas numa classe de objeto.
```js
class Car {
  constructor(name) {
    this.name = name
  }
  static hello() {
    return "Hello!!"
  }
}

let myCar = new Car("Ford")

// Você pode chamar "hello()" na Classe Car:
document.getElementById("demo").innerHTML = Car.hello()

// Mas não no objeto Car:
// document.getElementById("demo").innerHTML = myCar.hello()
// Isso gerará um erro.
```
Se você quer usar o objeto myCar dentro do método "static", você pode envia-lo como um parâmetro:
```js
class Car {
  constructor(name) {
    this.name = name
  }
  static hello(x) {
    return "Hello " + x.name
  }
}
let myCar = new Car("Ford")
document.getElementById("demo").innerHTML = Car.hello(myCar)
// "Hello Ford"
```
Para chamar um método estático dentro de outro método estático da mesma classe, podemos utilizar a palavra reservada "this":
```js
class ChamadaDoMetodoEstatico {
  static metodoEstatico() {		
    return "O método estático foi chamado"
  }
  static outroMetodoEstatico() {
    return this.metodoEstatico() + " de outro método estático"
  }
}
ChamadaDoMetodoEstatico.metodoEstatico()
// "O método estático foi chamado"

ChamadaDoMetodoEstatico.outroMetodoEstatico()
// "O método estático foi chamado de outro método estático"
```
Exemplo:
```js
class Tripple {
  static tripple(n) {
  n = n || 1;
      return n * 3;
    }
}

class BiggerTripple extends Tripple {
    static tripple(n) {
      return super.tripple(n) * super.tripple(n);
    }
}

console.log(Tripple.tripple()); 		// 3
console.log(Tripple.tripple(4));		// 12	
console.log(BiggerTripple.tripple(3));	// 81
```

## ASYNC - CALLBACKS

Um Callback é uma função passada como um argumento para uma outra função. Essa técnica permite que uma função chame uma outra função.

Uma função callback pode executar após que uma outra função foi finalizada.

### Sequência de Função:
Funções em JS são executadas na sequência em que elas são chamadas, e não na sequência que elas são definidas.

Esse exemplo vai finalizar exibindo "Goodbye":
```js
function myDisplayer(some) {
  document.getElementById("demo").innerHTML = some
}

function myFirst() {
  myDisplayer("Hello")
}
function mySecond() {
  myDisplayer("Goodbye")
}

myFirst()
mySecond()
// "Goodbye"
// Ao trocar a ordem, será exibido "Hello".
```
### Controle de Sequência:
Às vezes, você gostaria de ter um melhor controle sobre quando executar uma função.Suponhamos que você queira realizar um cálculo e, então, disponibilizar o resultado.

Você poderia chamar uma função calculadora (myCalculator), salvar o resultado, e então chamar uma outra função (myDisplayer) para exibir o resultado:
```js
function myCalculator(some) {
  document.getElementById("demo").innerHTML = some
}
function myCalculator(num1, num2) {
  let sum = num1 + num2
  return sum
}

let result = myCalculator(5, 5)
myDisplayer(result)
// 10
```
Ou, você poderia chamar uma função calculadora (myCalculator) e deixar a função calculadora chamar a função de exibilização (myDisplayer):
```js
function myDisplayer(some) {
  document.getElementById("demo").innerHTML = some
}
function myCalculator(num1, num2) {
  let sum = num1 + num2
  myDisplayer(sum)
}
myCalculator(5, 5)
// 10
```
O problema com o primeiro exemplo acima é que você tem que chamar duas funções para exibir o resultado.

O problema do segundo exemplo é que você não pode prevenir a função calculadora de exibir o resultado.

### Callbacks:
Usando um callback, você pode chamar a função calculadora (myCalculator) com um callback, e permitir que a função calculadora execute o callback após o cálculo ser finalizado:
```js
function myDisplayer(some) {
    document.getElementById("demo").innerHTML = some;
}

function myCalculator(num1, num2, myCallback) {
  let sum = num1 + num2
  myCallback(sum)
}

myCalculator(5, 5, myDisplayer)
// 10
```
No exemplo acima, "myDisplayer" é o nome de uma função. Ela é passada para "myCalculator()" como um argumento.

**Atenção: Quando passar uma função como argumento, não use parênteses.**

### Quando Usar Um Callback?
Os exemplos acima não são tão interessantes. Eles são simplificados para ensinar a sintaxe callback. 

Onde callbacks realmente brilham são em funções assíncronas, onde uma função tem que esperar por uma outra função (como esperando por um arquivo para carregar).

## Assincronicidade em JavaScript:

Funções executando em paralelo com outras funções são chamadas assíncronas. Um bom exemplo é o "setTimeout()" do JavaScript.

Nos exemplos anteriores, observou-se a sintaxe de um callback. No mundo real, callbacks são mais frequentemente usados em funções assíncronas.

### Esperando por um Tempo Esgotado:
Quando usando uma função JS "setTimeout()", você pode especificar uma função callback para ser executada no tempo limite:
```js
setTimeout(myFunction, 3000)
  
function myFunction() {
  document.getElementById("demo").innerHTML = "I love you!"
}
// Definiu a função para ser executada após 3000 milissegundos (3s)
```
No exemplo acima, myFunction é usado como um callback. O nome da função é passado para setTimeout() como um argumento. 3000 é o número de milissegundos antes do tempo limite e, então, myFunction() será chamado após 3 segundos.

Ao invés de passar o nome da função como um argumento para uma outra função, você pode, ao invés disso, sempre passar uma função inteira:
```js
setTimeout(function() { myFunction("I love you") }, 3000)

function myFunction(value) {
  document.getElementById("demo").innerHTML = value
}
```
No exemplo acima, "function(){ myFunction("I love you") }" é usado como um callback, mas é uma função completa. A função completa é passada para setTimeout() como um argumento.

### Esperando por Intervalos:
Quando usar a função setInterval(), você pode especificar uma função callback para ser executada a cada intervalo:
```js
setInterval(myFunction, 1000);

function myFunction() {
  let d = new Date();
    let sgd = d.getSeconds()
    let hrs = d.getHours()
  let mnt = d.getMinutes()

    let seg = sgd > 9 ? sgd : "0"+sgd
    let hhh = hrs > 9 ? hrs : "0"+hrs
  let mmm = mnt > 9 ? mnt : "0"+mnt

    document.getElementById("demo").innerHTML=
    hhh + ":" + mmm + ":" + seg
  }
// Irá mostrar um cronômetro sendo atualizado a cada segundo.
```
No exemplo acima, myFunction é usado como um callback. O nome da função é passado para setInterval() como um argumento.

1000 é o número de milissegundos entre intervalos, então myFunction() será chamado a cada segundo.

### Esperando por Arquivos:
Se você cria uma função para carregar um recurso externo (como um script ou um arquilo), você não pode usar o conteúdo antes dele ser totalmente carregado. Isso é o momento perfeito para usar um callback.

Esse exemplo carrega um arquivo HTML (mycar.html), e exibe o arquivo HTML em uma página web, após o arquivo ser totalmente carregado:
```js
function myDisplayer(some) {		
  document.getElementById("demo").innerHTML = some
}

function getFile(myCallback) {
  let req = new XMLHttpRequest()
  req.open('GET', "mycar.html")
  req.onload = function() {
    if (req.status == 200) {
      myCallback(this.responseText)
    } else {
      myCallback("Error: " + req.status)
    }
  }
  req.send()
}

getFile(myDisplayer)
// Algumas pendências serão aprendidas em AJAX.
```
No exemplo acima, myDisplayer é usado como um callback. O nome da função é passado para getFile() como um argumento.

## Promises em JavaScript:

"Produzindo código" é código que pode tomar algum tempo.

"Consumindo código" é código que deve esperar pelo resultado. 

Uma Promise é um objeto em JavaScript que une produzir código e consumir código.

### Objeto Promise:
Um objeto promise contém ambos os códigos de produção e chamadas para o código de consumo. 

Sintaxe:
```js
let myPromise = new Promise(function(myResolve, myReject) {
  / "Produzindo código" (pode levar algum tempo)

  myResolve()	/ quando obtém sucesso
  myReject()	/ quando ocorre erro
})

/ "Consumindo código" (deve esperar pela Promise completada)
myPromise.then(
  function(value) { código se obtém sucesso },
  function(error)  { código se ontém um erro	  }
}
```
Quando o código a executar obtém o resultado, deve chamar um dos dois callbacks:

<table>
  <tr>
    <td>Sucesso</td>
    <td>myResolve(valor de resultado)</td>
  </tr>
  <tr>
      <td>Erro</td>
    <td>myReject(objeto de erro)</td>
  </tr>
</table>

### Propriedades de Objeto:
Um objeto Promise pode estar:

- Pendente,
- Completado,
- Rejeitado.

O objeto Promise suporta duas propriedades: "state" e "result". Enquanto um objeto Promise está "pendente" (trabalhando), o resultado é indefinido.

- Quando está "completado", o resultado é um valor.
- Quando é "rejeitado", o resultado é um objeto de erro.
```js
myPromise.state	
myPromise.result
"pending"	//		undefined
"fulfilled"	//	um valor de resultado
"rejected" //	um objeto de erro
``` 
**Atenção: Você não pode acessar as propriedades "state" e "result". Você deve usar um método Promise para manusear promises.**

### Como Lidar com Promises:
Aqui está como usar uma Promise:
```js
myPromise.then(
  function(value) { código se obtém sucesso },
  function(error)  {     código se obtém erro	  }
}
```
**Atenção: "Promise.then()" recebe dois argumentos, um callback para sucesso e outro para falha.**

Ambos são Opcionais, então você pode adicionar um callback para sucesso ou apenas para erros.
```js
function myDisplayer(some) {
  document.getElementById("demo").innerHTML = some
}

let myPromise = new Promise(function(myResolve, myReject) {
  let x = 0

/ O código de produção (leva algum tempo)
  if (x == 0) {
    myResolve("OK")
  } else {
    myReject("Error")
  }
})

myPromise.then(
  function(value) {myDisplayer(value)},
  function(error) {myDisplayer(error)}
)
// "OK"
```
### Exemplos de Promises:
Para demonstrar o uso de promises, nós usaremos os exemplos de callback dos capítulos anteriores:

- Esperando pelo Tempo Limite;
- Esperando por um Arquivo.

### Esperando pelo Tempo Limite:

Exemplo usando Callback:
```js
setTimeout(function() { myFunction("I love you")}, 3000)

function myFunction(value) {	
  document.getElementById("demo").innerHTML = value
}
```
Exemplo usando Promise:
```js
let myPromise = new Promise(function(myResolve, myReject) {
  setTimeout(function() { myResolve("I love you")}, 3000)
})

myPromise.then(function(value) {
  document.getElementById("demo").innerHTML = value
})
```
### Esperando por um Arquivo:

Exemplo com Callback:
```js
function getFile(myCallback) {
  let req = new XMLHttpRequest()
  req.open('GET', "mycar.html")
  req.onload = function() {
    if (req.status == 200) {
      myCallback(req.responseText)
    } else {
      myCallback("Error: " + req.status)
    }
  }
  req.send()
}
getFile(myDisplayer)
```
Exemplo usando Promise:
```js
let myPromise = new Promise(function(myResolve, myReject) {
  let req = new XMLHttpRequest()
  req.open('GET', "mycar.html")
  req.onload = function() {
    if (req.status == 200) {
      myResolve(req.response)
    } else {
      myReject("File not Found")
    }
  }
  req.send()
})

myPromise.then(
  function(value) {myDisplayer(value)},
  function(error) {myDisplayer(error)}
}
```

## ASYNC

Async e Await fazem promises mais fáceis de escrever.

"async" faz uma função retorna uma promise.

"await" faz uma função esperar por uma promise.

### Sintaxe Async:
A keyword "async" antes de uma função faz uma função retornar uma promise:
```js
async function myFunction() {
  return "Hello"
}
```
É o mesmo que:
```js
async function myFunction() {
  return Promise.resolve("Hello")
}
```
Aqui é como usar a Promise:
```js
myFunction().then(
  function(value) { / código se sucesso },
  function(error)  { / código se erro         }
}
```
Exemplo:
```js
async function myFunction() {
  return "Hello"
}
myFunction().then(
  function(value) {myDisplayer(value)},
  function(error) {myDisplayer(error)}
}	
```
Ou simplemente, desde que você espera um valor normal (uma resposta normal, não um erro):
```js
async function myFunction() {
  return "Hello"
}
myFunction().then(
  function(value) {myDisplayer(value)}
)
```
### Sintaxe Await:
A keyword "await" antes de uma função faz a função esperar por uma promise:
```js
let value = await promise
```
**Atenção: A keyword "await" pode apenas ser usada dentro de uma função "async".**

Exemplo de Sintaxe Básica:
```js
async function myDisplay() {
  let myPromise = new Promise(function(myResolve, myReject) {
    myResolve("I love you")
  })
  document.getElementById("demo").innerHTML = await myPromise
}

myDisplay()
```
Exemplo Esperando pelo Tempo Limite:
```js
async function myDisplay() {
  let myPromise = new Promise(function(myResolve, myReject) {
    setTimeout(function() { myResolve("I love you")}, 3000)
  })
  document.getElementById("demo").innerHTML = await myPromise
}

myDisplay()
```
Exemplo Esperando um Arquivo:
```js
async function getFile() {
  let myPromise = new Promise(function(myResolve, myReject) {
    let req = new XMLHttpRequest()
    req.open('GET', "mycar.html")
    req.onload = function() {
      if (req.status == 200) {myResolve(req.response)}
      else {myResolve("File not Found")}
    }
    req.send()
  })
  document.getElementById("demo").innerHTML = await myPromise
}

getFile()
```

## HTML DOM

O HTML DOM é um modelo de objeto padrão e interface de programação para HTML. Ele define:

* Os elementos HTML como Objetos;
* As propriedades de todos elementos HTML;
* Os métodos para acessar todos os elementos HTML;
* Os eventos para todos os elementos HTML.

Em outras palavras: O HTML DOM é um padrão de como receber, mudar, adicionar, ou deletar elementos HTML.

O padrão W3C DOM (World Wide Web Consortium, Document Object Model) é separado em 3 diferentes partes:

1. Core DOM - modelo padrão para todos os tipos de documentos.
2. XML DOM - modelo padrão para documentos XML.
3. HTML DOM - modelo padrão para documentos HTML.

## HTML DOM Métodos:

Os métodos de HTML DOM são ações que você pode executar em elementos HTML. As propriedades do HTML DOM são valores (de elementos HTML) que você pode definir ou alterar.

### Interface de Programação do DOM:
O HTML DOM pode ser acessado com JavaScript (e com outras linguagens de programação).
No DOM, todos elementos HTML são definidos como objetos.

A interface de programação é as propriedades e métodos de cada objeto. Uma propriedade é um valor que você receber ou definir (como alterando o conteúdo de um elemento HTML).

Um método é uma ação que você pode fazer (como adicionar ou deletar um elemento HTML).

"getElementById" é um método, enquanto "innerHTML" é uma propriedade.

### Método getElementById:
A forma mais comum de acessar um elemento HTML é usar o "id" do elemento. Nos exemplos anteriores, o método getElementById usa id="demo" para encontre o elemento.

### Propriedade innerHTML:
A maneira mais fácil de pegar o contéudo de um elemento é usando a propriedade "innerHTML".

A propriedade "innerHTML" é útil para receber ou modificar o conteúdo de elementos HTML.

**Atenção: A propriedade "innerHTML" pode ser usada para receber ou alterar qualquer elemento HTML, incluindo o <html> e o <body>.**

## Documento HTML DOM

O objeto do documento HTML DOM é o proprietário de todos os outros objetos em sua webpage.

O objeto de documento representa sua webpage. Se você quer acessar qualquer elemento em uma página HTML, você sempre começar acessando o objeto do documento.

Abaixo estão alguns exemplos de como você pode usar o objeto documento para acessar e manipular HTML.

<table>
  <tr>
    <td>document.getElementById(id)</td>
    <td>Encontra um elemento pelo elemento id.</td>
  </tr>
  <tr>
    <td>document.getElementByTagName(name)</td>
    <td>Elementos pelo nome da tag.</td>
  </tr>
  <tr>
    <td>document.getElementsByClassName(name)</td>
    <td>Elementos pela classe.</td>
  </tr>
</table>

### Alterando Elementos HTML:

|Propriedade|Uso|
|---|---|
|element.innerHTML = novo conteúdo html | Altera o HTML de um elemento.|
|element.attribute = novo valor	| Altera o valor de um atributo|
|element.style.property = novo estilo	| Altera o estilo de um elemento.|

|Métodos|Uso|
|---|---|
|element.setAttribute(atributo, valor) | Altera o valor do atributo de um elemento HTML|

### Adicionando e Deletando Elementos:

|Métodos|Uso|
|---|---|
|document.createElement(elemento)	| Cria um elemento HTML|
|document.removeChild(elemento)	| Remove um elemento HTML|
|document.appendChild(elemento)	| Adiciona um elemento HTML|
|document.replaceChild(novo, antigo) | Altera um elemento HTML|
|document.write(texto) | Escreve no fluxo de saída HTML|

###  Adicionar Manipuladores de Eventos:
```js
document.getElementById(id).onclick = function(){code}	
//Adiciona um código manipulador de evento para um evento onclick.
```
**Atenção: Busque por listas de Manipuladores de Elementos de HTML DOM.]**

## Elementos do HTML DOM:

Frequentemente, com JavaScript você deseja manipular elementos HTML. Para isso, você precisa encontrar os elementos primeiros. Há variás formas de fazer isso:

- Encontrando elementos HTML pela id.
- Encontrando elementos HTML pela tag do nome.
- Encontrando elementos HTML pelo nome da classe.
- Encontrando elementos HTML pelos seletores CSS.
- Encontrando elementos HTML pelas coleções de objeto HTML.

### Através do Nome da Tag:
Esse exemplo encontra todos os elementos <p>
```js
var x = document.getElementByTagName("p")
```
Esse exemplo encontra o elemento com id="main" e então encontra todos os elementos dentro "main".
```js
var x = document.getElementById("main")
var y = x.getElementByTagName("p")
```
### Encontrando Elemento HTML por Seletores CSS:
Se você encontrar todos os elementos HTML que correspondem um seletor CSS especificado (id, class, nomes, tipos, atributos, valores de atributos, etc), use o método "querySelectorAll()"

Esse exemplo retorna uma lista de todos os elementos <p> com class="intro".
```js
var x = document.querySelectorAll("p.intro")
```
Atenção: Esse método não funciona em IE8 e versões anteriores.

### Encontrando Elementos HTML pelas Coleções de Objeto HTML:
Esse exemplo encontra o elemento "form" com id="frm1", na coleção de formulários, e exibe todos os valores do elemento:
```js
var x = document.forms["frm1"]
var text = ""
var i
for (i = 0; i < x.length; i++) {
  text += x.elements[i].value + "<br>"
}
document.getElementById("demo").innerHTML = text
// Donald
// Duck
// Submit
```
Os seguintes objetos HTML (e coleções de objetos) são também acessíveis:

- document.anchors
- document.body
- document.documentElement
- document.embeds
- document.forms
- document.head
- document.images
- document.links
- document.scripts
- document.title

## HTML DOM - Mudando o HTML:

O HTML DOM permite que o JavaScript modifique o conteúdo de elementos HTML.

### Alterando o Fluxo de Saída HTML:
JS pode criar conteúdo dinâmico HTML:
```js
<script>
document.write(Date())
</script>
// Fri Feb 26 2021 17:02:12 GMT-0300
```
O exemplo acima escreve diretamente no fluxo de saída HTML.

**Atenção: Nunca use "document.write()" depois que o documento é carregado. Ele vai sobrescrever o documento.**

### Alterando Conteúdo HTML:
A maneira mais fácil de alterar o conteúdo de um elemento HTML é usando a propriedade "innerHTML".

Use a sintaxe:
```js
document.getElementById(id).innerHTML = new HTML
```
Outro exemplo:
```js
var element = document.getElementById("id01")
element.innerHTML = "New Heading"
```
### Alterando o Valor de um Atributo:
Use a sintaxe:
```js
document.getElementById(id).attribute = novo valor
```
Esse exemplo altera o valor de um atributo src de um elemento <img>:
```js
<img id="myImage" src="smiley.gif">

<script>
document.getElementById("myImage").src = "landscape.jpg"
</script>
```

## HTML DOM - Modificando o CSS:

Alterar o estilo de um elemento HTML use essa sintaxe:
```js
document.getElementById(id).style.property = novo estilo
```
O exemplo a seguir modifica o estilo de um elemento <p>:
```js
<p id="p2">Hello World</p>

<script>
document.getElementById("p2").style.color = "blue"
</script>
```
### Usando Eventos:
O HTML DOM permite executar códigos quando um evento ocorre. Eventos são gerados pelo navegador quando "coisas acontecem" para elementos HTML:

- Um elemento é clicado;
- A página é carregada;
- Os campos de input são modificados, etc.

Esse exemplo altera o estilo do elemento com id="id1", quando o usuário clica um botão:
```js
<button type="button" onclick="document.getElementById('id1').style.color = 'red'">Click Me!</button>
```
Para mais formas, acesse a [HTML DOM STYLE OBJECT REFERENCE](https://www.w3schools.com/jsref/dom_obj_style.asp) 

## Animação HTML DOM:

Para demonstrar como criar animações HTML com JavaScript, nós usaremos um simples webpage:
```js
<div id="animation">My animation will go here</div>
```
> Crie um Container de Animação:
Todas as animações devem ser relativos ao elemento "container".
```js
<div id="container">
  <div id="animate">My animation will go here</div>
</div>
```
### Estilize os Elementos:
O elemento container deve ser criado com estilo = "position: relative"

O elemento animation deve ser criado com estilo = "position: absolute"
```css
#container {
  width: 400px;
  height: 400px;
  position: relative;
  background: yellow;
}
#animate {
  width: 50px;
  height: 50px;
  position: absolute;
  background: red;
}
```
### Código de Animação:
Animações JavaScript são feitas por mudanças graduais de programação em um estilo do elemento.

As mudanças são chamadas por um temporizador. Quando o intervalo do temporizador é pequena, a animação parece contínua.

O código básico é:
```js
var id = setInterval(frame, 5)

function frame() {
  if ( / teste se finalizado ) {
    clearInterval(id)
  } else {
    / código para mudar o estilo do elemento
  }
}
```
### Crie a Animação Completa Usando JavaScript:
```js
var id = null
function myMove() {
  var elem = document.getElementById("animate")
  var pos = 0
  clearInterval(id)
  id = setInterval(frame, 5)
  function frame() {
    if (pos == 300) {
      clearInterval(id) 
    } else {
      pos++
      elem.style.top = pos + 'px'
      elem.style.left = pos + 'px'
    }
  }
}
```

### EVENTOS HTML DOM

Para executar um código quando um usuário clica em um elemento, adicione um código JS para um atributo de evento HTML:
```js
onclick=JavaScript
```
Exemplos:
1. Quando um usuário clica o mouse;
2. Quando uma página é carregada;
3. Quando uma imagem tem sido carregada;
4. Quando o mouse se move sobre um elemento;
5. Quando um campo de input tem sido modificado;
6. Quando um formulário HTML é submetido;
7. Quando um usuário pressiona uma tecla.

Nesse exemplo, o conteúdo do elemento ```<h1>``` é alterado quando um usuário clica sobre ele:
```js
<h1 onclick="this.innerHTML = 'Ooops!'">Click on this text</h1>
```
Nesse exemplo, uma função é chamada de um manipulador de eventos:
```js
<h1 onclick="changeText(this)">Click on this text</h1>

<script>
function changeText(id) {
  id.innerHTML = "Ooops!"
}
</script>
```
### Atributos de Evento HTML:
Para atribuir eventos a elementos HTML, você usa um atributo de evento:
```js
<button onclick="displayDate()">Try it</button>
```
No exemplo acima, uma função nomeada "displayDate" será executada quando o botão é clicado.

### Atribuindo Eventos Usando o HTML DOM:		
O HTML DOM permite atribuir eventos a elementos HTML usando JavaScript:
```js
<script>
document.getElementById("myBtn").onclick = displayDate

function displayDate() {
  document.getElementById("demo").innerHTML = Date()
}
</script>
```
**Atenção: Não coloque os (). Colocando você ativará a função automaticamente, sem pressionar o botão.**

### Alguns Atributos de Eventos HTML:

* onload / onunload: são eventos que são causados quando o usuário entra ou deixa a página.

* "onload" pode ser usado para checar o tipo do navegador do visitante e sua versão, e carregar uma versão apropriada da página baseado nessa informação.

* "onload" e "onunload" podem ser usados para lidar com cookies.

```js
<body onload="checkCookies()">
<p id="demo"></p>
<script>	
function checkCookies() {
  var text = ""
  if (navigator.cookieEnabled == true) {
    text = "Cookies are enabled."
  } else {
    text = "Cookies are not enabled."
  }
  document.getElementById("demo").innerHTML = text
}
</script>
</body>
```

* onchange é usado frequentemente em combinações com validação de campos inputs.
Ambaixo é um exemplo de como usar o "onchange". A função "upperCase()" será chamada quando um usuário altera o conteúdo de um campo input:

```js
Enter your name: 
<input type="text" id="fname" onchange="myFunction()">
<script>
function myFunction() {
  var x = document.getElementById("fname")
  x.value = x.value.toUpperCase()
}
</script>
```
* "onmouseover" e "onmouseout" podem ser usados para chamar uma função quando o mouse desliza por cima ou para fora de um elemento HTML.

* "onmousedown", "onmouseup" e "onclick" são todos partes de um "mouse-click". Primeiro, quando o botão do mouse é pressionado, o "onmousedown" é chamado, então, quando o botão do mouse é levantado "onmouseup" é chamado. Finalmente, quando o mouse-click é completado, o evento "onclick" é chamado.

Para mais formas, acesse [HTML DOM EVENT OBJECT REFERENCE](https://www.w3schools.com/jsref/dom_obj_event.asp) 

## EVENTLISTENER HTML DOM:

Adiciona-se um "ouvinte" de evento que dispara quando um usuário pressiona um botão:
```js
document.getElementById("myBtn").addEventListener("click", displayDate)
```
O método "addEventListener()" junta um manipulador de evento ao elemento especificado.
Este método une um manipulador de eventos ao elemento sem sobrescrever manipuladores de eventos existentes.

Você pode adicionar vários manipuladores de eventos a um elemento.

Você pode adicionar muitos manipuladores de eventos do mesmo tipo a um elemento, como eventos de "click duplo".

Além disso, adicionar ouvintes de eventos para qualquer objeto DOM, não apenas elementos HTML, ou seja, também para o window object.

O método torna mais fácil de controlar como o evento reage.

Quando usamos o método "addEventListener()", o JavaScript é separado da marcação HTML, para melhor legibilidade e permitir que você adicione ouvintes de eventos mesmo quando você não controla a marcação HTML.

Você pode facilmente remover um event listener usando o método "removeEventListener()".

Sintaxe:
```js
element.addEventListener(event, function, useCapture)
```
O primeiro parâmetro é o tipo do evento (como "click" ou "mousedown" ou qualquer outro Evento HTML DOM)

O segundo parâmetro é a função que você quer chamar quando o evento ocorre.

O terceiro parâmetro é um valor booleano especificando se deve ser usado o "borbulhar" do evento ou a captura de evento. Esse parâmetro é opcional.

**Atenção: Note que você não usa o prefixo "on" para o evento: use "click" ao invés de "onclick".**

### Adicione um Manipulador de Eventos

Exemplo 01:
```js
element.addEventListener("click", function(){ alert("Hello World") })
```
Exemplo 02:
```js
element.addEventListener("click", myFunction)
  
function myFunction() {
  alert("Hello World")
}
```
Você adicionar quandos Manipuladores de Eventos quiser sem sobrescrever eventos existentes:
```js
element.addEventListener("click", myFunction)
element.addEventListener("click", mySecondFuncion)
```
Você pode adicionar eventos de diferentes tipos para o mesmo elemento:
```js
element.addEventListener("mouseover", myFunction)
element.addEventListener("click", mySecondFunction)
element.addEventListener("mouseout", myThirdFunction)
```

### Adicione um Manipulador de Eventos ao Objeto window

O método "addEventListener()" pertime que você adicione event listener a qualquer objeto HTML DOM, tais como elementos HTML, documento HTML, ao objeto window, ou outros objetos que suportam eventos, como o objeto "xmlHttpRequest":
```js
window.addEventListener("resize", function(){
  document.getElementById("demo").innerHTML = Math.random()
})
// cria um número aleatório quando a janela é aumentada ou diminuída.
```
### Passando Parâmetros:
Quando passar valores de parâmetro, use uma "função anônima" que chama uma função específica com os parâmetros:
```js
element.addEventListener("click", function(){ myFunction(p1, p2) })
```

### Event Bubbling ou Event Capturing?
Há duas formas de propagação de eventos no HTML DOM, "bubbling" e "capturing".

Propagação de evento é uma forma de definir a ordem do elemento quando um evento ocorre. Se você tem um elemento ```<p>``` dentro de um elemento ```<div>```, e o usuário clica no elemento ```<p>```, qual evento "click" de elemento deve ser manipulado primeiro?

Em "bubbling", o evento do elemento mais interior é manipulado primeiro e então o mais externo: o elemento ```<p>``` vem primeiro, e então o ```<div>``` depois.

Em "capturing", o evento do elemento mais externo é manipulado primeiro.

Com o método "addEventListener()" você pode especificar o tipo de propagação usando o parâmetro "useCapture".
```js
addEventListener(event, function, useCapture)
```
O valor padrão é "false", no qual vai usar a propagação bubbling. Quando o valor é definido para "true", o evento usa a propagação "capturing".
```js
document.getElementById("myP").addEventListener("click", myFunction, true)
document.getElementById("myDiv").addEventListener("click", myFunction, true)
```
### O método removeEventListener()
Remove manipuladores de evento que tem sido unidos com o método addEventListener()
```js
element.removeEventListener("mousemove", myFunction)
```

## Navegação do HTML DOM:

Com o HTML DOM, você pode navegar pela "node tree" usando relações de nós.

De acordo com o padrão W3C HTML DOM, tudo no documento HTML é um nó:
- O documento inteiro é um nó de documento.
- Cada elemento HTML é um nó de elemento.
- O texto dentro dos elementos HTML são nódulos de texto.
- Todos os comentários são nódutos de comentários.

Com o HTML DOM, todos os nódulos na node tree podem ser acessados pelo JS.
Novos nódulos podem ser criados, e todos nódulos podem ser modificados ou deletados.

### Relações de Nódulos:
Os nós no node tree tem uma relação hierárquica para cada um.
O termo parent, child, and sibling são usados para descrever as relações.

- Em um node tree, a nó do topo chama-se root (ou root node);
- Cada nódulo tem exatamente um parent, exceto o root (que não tem parent).
- Um nódulo pode ter um número de children.
- Siblings (irmãos ou irmãs) são nódulos com o mesmo parent.
```js
<html>
  
    <head>
        <title>DOM Tutorial</title>
    </head>

    <body>
        <h1>DOM Lesson one</h1>
        <p>Hello world</p>
    </body>

</html>
```

Do HTML acima você pode ler:
  1. ```<html>``` é o root node;
  2. ```<html>``` não tem parents;
  3. ```<html>``` é o parent de ```<head>``` e ```<body>```
  4. ```<head>``` é o primeiro child de ```<html>```
  5. ```<body>``` é o último child de ```<html>```
  6. ```<head>``` tem um child: ```<title>```
  7. ```<title>``` tem um child (um text node): "DOM Tutorial"
  8. ```<body>``` tem dois child: ```<h1>``` e ```<p>```
  9. ```<h1>``` tem um child: "DOM Lesson one".
  10. ```<p>``` tem um child: "Hello world"
  11. ```<h1>``` e ```<p>``` são siblings.

### Navegando Entre Nódulos:
Você usar as seguintes propriedades de nódulos para navegar entre os nós com JavaScript:

- parentNode
- childNodes[nodenumber]
- firstChild
- lastChild
- nextSibling
- previousSibling

### "Child Nodes" e "Node Values":

Atenção: Um erro comum em processamento de DOM é esperar que um nó de elemento possua texto.
```js
<title id="demo">DOM Tutorial</title>
```
O elemento ```<title>``` não contém texto. Ele contém um nódulo de texto com o valor "DOM Tutorial".

O valor do nódulo de texto pode ser acesso pela propriedade "innerHTML". Você acessar da mesma forma por "nodeValue" do primeiro child:
```js
var myTitle = document.getElementById("demo").firstChild.nodeValue.
```
Acessando o primeiro child pode também ser feito assim:
```js
var myTitle = document.getElementById("demo").childNodes[0].nodeValue;
```
### Nódulos de DOM Root:
Há duas propriedades especiais que permitem acessar o documento completo:

- "document.body": o body do documento.
- "document.documentElement" - o documento completo.

### A Propriedade nodeName:
Especifica o nome de um nódulo:

- nodeName é de apenas-leitura;
- nodeName de um nódulo de elemento é o mesmo que tag name
- nodeName de um nódulo de atributo é o nome do atributo;
- nodeName de um nódulo de texto é sempre #text
- nodeName do nó de documento é sempre #document.

```js
<h1 id="id01">My First Page</h1>
<p id="id02"></p>

<script>
document.getElementById("id02").innerHTML = 
document.getElementById("id01").nodeName
</script>
// A tag <p> será "H1".
```
**Atenção: "nodeName" sempre contém o nome da tag em caixa-alta de um elemento HTML.**

### A Propriedade nodeValue:

Especifica o valor de um nódulo:
- nodeValue para nódulos de elementos é "null"
- nodeValue para nódulos de texto é o próprio texto.
- nodeValue para nódulos de atributo é o valor do atributo.

### A Propriedade nodeType:
É de apenas-leitura. Retorna o tipo de um nódulo:
```js
<h1 id="id01">My First Page</h1>
<p id="id02"></p>

<script>
document.getElementById("id02").innerHTML = 
document.getElementById("id01").nodeType
</script>
```
As propriedades mais importantes de nodeType são:

| | | |
|---|---|---|
ELEMENT_NODE	| 1 |  ```<h1 class="heading">W3Schools</h1>```
ATTRIBUTE_NODE	| 2 |  ```class = "heading" (descontinuado)```
TEXT_NODE	| 3 |  W3Schools
COMMENT_NODE	| 8 |  ```<!-- This is a comment -->```
DOCUMENT_NODE	| 9 |  O próprio documento HTML (o parent de ```<html>```)
DOCUMENT_TYPE_NODE | 10 |  ```<!Doctype html>```

**Atenção: Tipo 2 foi descontinuado no HTML (embora ainda funcione). Porém, não foi descontinuado no XML DOM.**

## Nódulos do DOM:

Adicionando e Removendo nódulos (Elementos HTML):

### Criando um Novo Elemento HTML (Nódulo):
Para criar um novo elemento para o HTML DOM, você deve cria um elemento (nódulo de elemento) primeiro e, então, anexar a um elemento existente.
```js
<div id="div1">
    <p id="p1">This is a paragraph.</p>
    <p id="p2">This is another paragraph.</p>
</div>

<script>
  var para = document.createElement("p")
  var node = document.createTextNode("this is new")
  para.appendChild(node)

  var element = document.getElementById("div1")
  element.appendChild(para)
</script>
```
1. O código cria um novo elemento ```<p>```
2. Para adicionar um texto para o elemento ```<p>```, você deve criar um nódulo de texto primeiro.
3. Então você deve anexar o nódulo de texto ao elemento ```<p>```
4. Finalmente, você deve anexar o novo elemento para um elemento existente.

### Criando Novos Elementos HTML - insertBefore()
O método "appendChild()" anexa o novo elemento como o último child do parent.
Se você não quer que isso aconteça, você pode usar o método "insertBefore()"
```js
<div id="div1">
    <p id="p1">This is a paragraph.</p>
  <p id="p2">This is another paragraph.</p>
</div>

<script>
var para = document.createElement("p")
var node = document.createTextNode("This is new")
para.appendChild(node)

var element = document.getElementById("div1")
var child = document.getElementById("p1")
element.insertBefore(para, child)
</script>
```
### Removendo Elementos HTML Existentes:
Use o método "remove()":
```js
<script>
var elmnt = document.getElementById("p1")
elmnt.remove()
</script>
```
**Atenção: O método remove() não funciona em navegadores antigos. Se necessário, utilize o método "removeChild()".**

### Removendo um Child Node:
Usando "removeChild()":
```js
var parent = document.getElementById("div1")
var child = document.getElementById("p1")
parent.removeChild(child)
```
### Relocando Elementos HTML:
Use o método "replaceChild()"
```js
var para = document.createElement("p")
var node = document.createTextNode("This is new")
para.apprendChild(node)

var parent = document.getElementById("div1")
var child = document.getElementById("p1")
parent.replaceChild(para, child)
// "p1" deixa de existir para dar lugar a "p" com "this is new".
```

## Coleções de HTML DOM:

### Objeto HTMLCollection:
O método "getElementsByTagName()" retorna um objeto "HTMLCollection".
Um objeto "HTMLCollection" é uma lista parecida com um vetor (coleção) de elementos HTML.

O código a seguir seleciona todos os elementos ```<p>``` em um documento.
```js
var x = document.getElementsByTagName("p")
```
Os elementos na coleção podem ser acessados por número de indexação.
Para cessar o segundo elemento ```<p>```, você pode escrever:
```js
y = x[1]
```
**Atenção: Lembre-se sempre que a indexação começa em 0.**

### HTML HTMLCollection Length:
A propriedade "length" define o número de elementos no "HTMLCollection".
```js
var myCollection = document.getElementsByTagName("p")
document.getElementById("demo").innerHTML = myCollection.length
```
No exemplo acima, cria-se uma coleção de todos os elementos ```<p>```. Então, exibe o comprimento da coleção.

A propriedade "length" é útil quando você quer repetir através dos elementos em uma coleção.

Exemplo usando repetição para modificar a cor de fundo de todos elementos ```<p>```:
```js
var myCollection = document.getElementsByTagName("p")
var i
for (i = 0; i < myCollection.length; i++) {
  myCollection[i].style.color = "red"
}
```
**Atenção: Um HTMLCollection Não é um vetor.**

Embora pareça um vetor, ele não é. Você pode aplicar repetições através da lista e referir-se aos elementos como um número.

No entanto, você não pode usar métodos de vetor, como "valueOf()", "pop()", "push()", "join()" em um HTMLCollection.

## Lista de Nódulos do HTML DOM:

### O Objecto NodeList:
Um objeto "NodeList" é uma lista (coleção) de nódulos extraídos de um documento.

Um objeto "NodeList" é quase o mesmo que um objeto "HTMLCollection". 

Alguns navegadores antigos retornam um objeto NodeList ao invés de um HTMLCollection para método como "getElementByClassName()".

Todos os navegadores retornam um objeto NodeList para a propriedade "childNodes".
A maioria dos navegadores retornam um objeto NodeList" para métodos "querySelectorAll()".

O exemplo a seguir seleciona todos os nódulos ```<p>``` em um documento:
```js
var myNodeList = document.querySelectorAll("p")
```
Os elementos no NodeList podem ser acessados pelo número de indexação. Para acessar o segundo nódulo ```<p>``` você pode escrever:
```js
y = myNodeList[1]
```
Da mesma forma que você pode usar a propriedade "length" com HTMLCollections, você também pode utilizar para NodeList.

Dessa forma, você pode utilizar para repetições e atividades explicadas no capítulo anterior.

### A Diferença Entre um HTMLCollection e um NodeList:

Um HTMLCollection é uma coleção de elementos HTML. Enquanto que um NodeList é uma coleção de nódulos do documento.

Os itens com HTMLCollection podem ser acessados pelos seus nomes, id, ou números de indexação.

Por outro lado, os itens de NodeList podem apenas ser acessados pelos seus números de indexação.

Apenas o NodeList podem conter nódulos de atributo e nódulos de texto.

**Atenção: Da mesma que HTMLCollection, NodeList também não é um vetor e, portanto, métodos de vetor não funcionarão sobre ele. **

## BROWSER OBJECT MODEL - BOM

Não há um padrão oficial para o Browser Object Model (BOM). Desde que navegadores modernos têm implementado praticamente os mesmos métodos e propriedades para interatividade JavaScript, é frequentemente referido como métodos e propriedades do BOM.

### O Objeto Window
É suportado por todos os navegadores. Ele representa a janela do navegador.

Todos os objetos globais, funções e variáveis automaticamente tornam-se membros do objeto window.

Variáveis globais são propriedades do objeto window. Funções globais são também métodos do objeto window. Até mesmo o objeto "document" (do HTML DOM) é uma propriedade do objeto window.
```js
window.document.getElementById("header")
```
É o mesmo que:
```js
document.getElementById("header")
```
### Tamanho da Janela:
Duas propriedades podem ser usadas para determinar o tamanho da janela do navegador. Ambas as propriedades retornam os tamanhos em pixels:

* "window.innerHeight" - a altura interior da janela do navegador.
* "window.innerWidth" - a largura interior da janela do navegador.

**Atenção: A janela do navegador Não inclui barras de ferramentas ou barra de rolagem.**

**Atenção: Alguns navegadores como o Internet Explorer precisam usar propriedades diferentes para lidar com essa situação. Para isso, faça essa conversão:**
```js
var w = window.innerWidth
|| document.documentElement.clientWidth
|| document.body.clientWidth

var h = window.innerHeight
|| document.documentElement.clientHeight
|| document.body.clientHeiht
```
Essa forma poderá ser usada para todos os navegadores, incluindo as versões antigas do IE.

### Outros Métodos de Window:

* "window.open()" - abre uma nova janela
* "window.close()" - fecha a janela atual.
* "window.moveTo()" - move a janela atual.
* "window.resizeTo()" - altere o tamanho da janela atual.

## WINDOW SCREEN

O objeto window.screen contém informação sobre o screen do usuário.

O objeto window.sceen pode ser escrito sem o prefixo window.

Propriedades:

- screen.width	
- screen.height
- screen.availWidth
- screen.availHeight
- screen.colorDepth
- screen.pixelDepth

### screen.width:
É uma propriedade que retorna a largura da tela do visitante em pixels:	
```js
document.getElementById("demo").innerHTML = "Screen width: " + screen.width
// Resultado: 2049
```
### screen.height:
```js
document.getElementById('demo").innerHTML = "Screen height: " + screen.height)
// Resultado: 1152
```
### Largura e Altura da Tela Disponível:
A propriedade "screen.availWidth" retorna a largura da tela do visitante, em pixels, menos características de interface, como a barra de tarefas do Windows.
```js
document.getElementById("demo").innerHTML = 
"Available Screen Widrh: " + screen.availWidth
// Resultado: 2049
```
O mesmo pode ser feito com a altura disponível:
```js
document.getElementById("demo").innerHTML = 
"Available Screen Height: " + screen.availHeight
//  Resultado: 1092
```
### Profundidade de Cor da Tela:
A propriedade "screen.colorDepth" retorna o número de bits usados para exibir uma cor:
Todos os computaodres modernos usam hardware de 24 bit ou 32 bit para resolução de cor:

* 24 bits = 	16.777.216 "cores verdadeiras" diferentes.
* 32 bits = 	4.294.967.296 "cores profundas" diferentes.
```js
document.getElementById("demo").innerHTML= 
"Screen Color Depth: " + screen.colorDepth
// Resultado: 24
```
**Atenção: Os valores #rrggbb (rgb) usados em representações HTML são "True Colors" (24 bits - 16.777.216 cores diferentes)**

### Profundidade de Pixel da Tela:
Retorna a profundidade de pixels da tela:
```js
document.getElementById("demo").innerHTML = 
"Screen Pixel Depth: " + screen.pixelDepth
// Resultado: 24
```
**Atenção: Para computadores modernos, Profundidade de Cor e Profundidade de Pixels são iguais.**

## WINDOW LOCATION

O objeto "window.location" pode ser usado para receber endereços de páginas atuais (URLs) e redirecionar o navegador para uma nova página.

### Window Location
O objeto "window.location" pode ser escrito sem o prefixo window.

Alguns exemplos:

* window.location.href  -  retorna a URL da página atual.
* window.location.hostname  -  retorna o nome de domínio do host.
* window.location.pathname  -  retorna o path e filename da página atual.
* window.location.protocol  -  retorna o protocolo web usado (http: ou https:)
* window.location.assign()  -  carrega um novo documento.

### window.location.href:
É uma propriedade que retorna a URL da página atual:
```js
document.getElementById("demo").innerHTML = 
"Page location is " + window.location.href
/ "Page location is https://www.w3schools.com/js/js_window_location.asp"
```
### window.location.hostname:
Propriedade que retorna o nome do host (da página atual).
```js
document.getElementById("demo").innerHTML = 
"Page hostname is " + window.location.hostname
/ "Page hostname is www.w3schools.com"
```
### window.location.pathname:
Retorna o pathname da página atual:
```js
document.getElementById("demo").innerHTML = 
"Page path is " + window.location.pathname
// "Page path is /js/js_window_location.asp
```
### window.location.protocol
Retorna o protocolo web da página.
```js
document.getElementById("demo").innerHTML = 
"Page protocol is " + window.location.protocol
// "Page protocol is https:"
```
### window.location.port:
Retorna o número da porta web do host (da página atual):
```js
document.getElementById("demo").innerHTML = 
"Port number is " + window.location.port
// "Port number is "
```
**Atenção: A maior parte dos navegadores não exibirão números (ou exibirá 0) de portas padrão (80 para http e 443 para https). **

### window.location.assign()
Esse método carrega um novo documento:
```html
<html>
<head>
<script>
function newDoc() {
  window.location.assign("https://www.w3schools.com")
}
</script>
</head>
<body>

<input type="button" value="Load new document" onclick="newDoc()">
</body>
</html>
<!-- Retorna o carregamento da página da w3schools.com -->
```

## WINDOW HISTORY

O objeto "window.history" contém o histórico dos navegadores.

O objeto pode ser wscrito sem o prefixo window. Para proteger a privacidade dos usuários, há limitações de como JavaScript pode acessar esse objeto.

Alguns métodos:

* "history.back()" 		- igual a clicar de volta no navegador.
* "history.forward()		- igual a clicar para frente no navegador.

### history.back()
Método que carrega a URL anterior na lista do histórico. É o mesmo que clicar no botão de voltar no navegador.
```html
<html>
<head>
<script>
  function goBack() {
    window.history.back()
  }
</script>
</head>
<body>

<input type="button" value="Back" onclick = "goBack()">

</body>
</html>
<!-- Cria um botão que ao clicar, retorna apenas uma URL no histórico. -->
```
### history.forward()
Método que carrega a próxima URL na lista do histórico. É o mesmo que clicar no botão de avançar no navegador:
```html
<html>
<head>
<script>
  function goForward() {
    window.history.forward()
  }
</script>
</head>
<body>

<input type="button" value="Forward" onclick="goForward()">

</body>
</html>
<!-- Cria um botão que ao clicar, avança apenas uma URL no histórico. --> 
```

## WINDOW NAVIGATOR:

O objeto "window.navigator" contém informações sobre o navegador do visitante. O objeto pode ser escrito sem o prefixo "window".

Alguns exemplos:

* navigator.appName
* navigator.appCodeName
* navigator.platform

### Cookies do Navegador:
A propriedade "cookieEnabled" retorna true se cookies estão habilitados, e false não estiver:
```html
<p id="demo"></p>

<script>
document.getElementById("demo").innerHTML = 
"cookiesEnabled is " + navigator.cookieEnabled
</script>
<!-- Retorna "cookiesEnabled is true" -->
```
### navigator.appName
A propriedade retorna o nome da aplicação do navegador:
```html
<p id="demo"></p>

<script>
  document.getElementById("demo").innerHTML =
  "navigator.appName is " + navigator.appName
</script>
<!-- "navigator.appName is Netscape" -->
```
**Atenção: "Netscape" é o nome da aplicação para IE1, Chrome, Firefox e Safari.**

### navigator.appCodeName
A propriedade retorna o nome do código da aplicação do navegador:
```html
<p id="demo"></p>

<script>
document.getElementById("demo").innerHTML =
"navigator.appCodeName is " + navigator.appCodeName
</script>
<!-- "navigator.appCodeName is Mozilla" -->
```
**Atenção: "Mozilla" é o nome do código da aplicação para Chrome, Firefox, IE, Safari e Opera.**

### navigator.product:
A propriedade retorna o nome do produto do motor de navegador:
```html
<p id="demo"></p>

<script>
document.getElementById("demo").innerHTML =
"navigator.product is " + navigator.product
</script>
<!-- "navigator.product is Gecko" -->
```
**Atenção: Não confie nisso. A maioria dos navegadores retornam "Gecko" como nome de produto.**

### navigator.appVersion
A propriedade retorna informações sobre a versão do navegador:
```html
<p id="demo"></p>

<script>
document.getElementById("demo").innerHTML = 	navigator.appVersion
</script>
<!-- Retorna: "5.0 (Windows)" -->
```
### navigator.userAgent
A propriedade retorna o cabeçalho do agente do usuário enviado pelo navegador ao servidor:
```html
<p id="demo"></p>

<script>
document.getElementById("demo").innerHTML =
navigator.userAgent
</script>
<!-- "Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:87.0) Gecko/20100101 Firefox/87.0" -->
```
### Cuidado !!!
A informação do objeto de navegação pode estar frequentemente errônea, e não deve ser usada para detectar a versão do navegador:

- Diferentes navegadores podem usar o mesmo nome;
- Os dados de navegação podem ser modificados pelo proprietário do navegador.
- Alguns navegadores não identificam corretamente a si mesmos para ignorar os testes do site.
- Navegadores não podem reportar novos sistemas operacionais, lançados depois do navegador.

### navigator.platform
A propriedade retorna a plataforma do navegador (o sistema operacional):
```html
<p id="demo"></p>

<script>
document.getElementById("demo").innerHTML =
navigator.platform
</script>
<!-- Win32 -->
```
### navigator.language
A propriedade retorna a linguagem do navegador:
```html
<p id="demo"></p>

<script>
document.getElementById("demo").innerHTML =
navigator.language
</script>
<!-- pt-BR -->
```
### navigator.onLine
A propriedade retorna true se o navegador está online:
```html
<p id="demo"></p>

<script>
document.getElementById("demo").innerHTML = 
navigator.onLine
</script>
<!-- true -->
```
### navigator.javaEnabled()
O método retorna true se Java está habilidade:
```html
<p id="demo"></p>

<script>
document.getElementById("demo").innerHTML =
navigator.javaEnabled()
</script>
```

## Caixas POPUP

### Caixa de Alerta:
Uma caixa de alerta é frequentemente usado se queremos ter certeza que uma informação foi recebida do usuário.

Quando um popup da caixa de alerta aparece, o usuário terá que clicar em "OK" para continuar:
```js
alert("I am an alert box!")
```
### Caixa de Confirmação:
Uma caixa de confirmão é usada frequentemente se queremos que o usuário verifique ou aceite algo.

Quando a caixa de confirmação aparece, o usuário terá que clicar ou "OK" ou "Cancel" para prosseguir.

Se o usuário clica "OK", a caixa retorna "true". Se o usuário clica "Cancel", a caixa retorna "false"
```js
if (confirm("Press a Button!")) {
  txt = "You pressed OK"
} else {
  txt = "You pressed Cancel"
}
```
### Caixa de Prompt:
Uma caixa de prompt é usada frequentemente se queremos que o usuário coloque um valor antes de entrar em uma página.

Quando a caixa de prompt, o usuário terá que clicar ou "OK" ou "Cancel" para proceder depois de colocar um valor de input.

Se o usuário clica "OK", a caixa retorna o valor de input. Se o usuário clica "Cancel", a caixa retorna null.
```html
<button onclick="myFunction()">Try it</button>
<p id="demo"></p>

<script>
function myFunction() {
  var txt = ""
  var person = prompt("Please enter your name:", "Harry Potter")
  if (person == null || person == "") {
    txt = "User cancelled the prompt."
  } else {
    txt = "Hello, " + person + "! How are you today?"
  }
  document.getElementById("demo").innerHTML = txt
}
</script>
<!-- "Hello, Arthur! How are you today!" -->
```
### Quebras de Linha:
Para exibir quebras de linhas dentro de uma caixa popup, use uma barra invertida seguido de "n":
```js
alert("Hello\nHow are You?")
```

## Eventos de Tempo:

Você pode utilizar o "setTimeout()" e "setInterval()" para executar ações de eventos de temporizador. Ambos são métodos do objeto Window do HTML DOM.

### Como Parar a Execução?
O método "clearTimeout()" para a executação de uma função especificada em setTimeout().

O método pode ser escrito sem o prefixo window. 
```js
myVar = setTimeout(function, milissegundos)
clearTimeout(myVar)
```
Se a função não já tem sido executada, você pode parar a execução chamando o método "clearTimeout()"
```html
<button onclick="myVar = setTimeout(myFunction, 3000)">Try it</button>

<button onclick="clearTimeout(myVar)">Stop it</button>
```
O exemplo acima impede a execução da função do primeiro botão.

Para parar a execução do método "setInterval()", use o método "clearInterval()". Esse método funciona semelhante ao "clearTimeout()", interrompendo a execução ao assinalar a variável que está atribuída o "setInterval()".
```js
myVar = setInterval(function, milissegundos)
clearInterval(myVar)
```
Exemplo:
```html
<p id="demo"></p>
<button onclick="clearInterval(myVar)">Stop time</button>

<script>
var myVar = setInterval(myTimer, 1000)
function myTimer() {
  var d = new Date()
  document.getElementById("demo").innerHTML = d.toLocaleTimeString()
}
</script>
```
O exemplo acima gera um contador que exibe o horário do navegador e continua atualizando a cada segundo. Então o botão para a contagem.

## Cookies:

Cookies permitem você armazenar informações do usuário em páginas web.

### O Que São Cookies?
Cookies são dados, armazenados em pequenos arquivos de texto, em seu computador.

Quando um servidor web tem enviado uma página web para um navegador, a conexão é desligada, e o servidor esquece tudo sobre o usuário.

Cookies foram inventados para resolver o problema de "como lembrar a informação sobre o usuário":

* Quando um usuário visita uma webpage, seu nome pode ser armazenado em um cookie.
* Na próxima vez que o usuário visita a página, o cookie "lembra" seu nome. 

Cookies são salvos em pares de nome-valor como:
```js
username = John Doe.
```
Quando um navegador realiza uma requisição de uma página web a partir de um servidor, cookies pertencentes à página são adicionados à requisição.

### Crie um Cookie com JavaScript:
JavaScript pode criar, ler, e deletar cookies com a propriedade "document.cookie".
Com o JavaScritp, um cookie pode ser criado assim:
```js
document.cookie = "username=John Doe"
```
Você pode também adicionar um tempo de expiração (em hora UTC). Por padrão, o cookie é deletado quando o navegador é fechado:
```js
document.cookie = "username=John Doe; expires=Thu, 18 Dec 2013 12:00:00 UTC"
```
Com um parâmetro "path", você fala ao navegagor qual path o cookie pertence. Por padrão, o cookie pertence à página atual. 

### Leia um Cookie com JavaScript:
Com JS, cookies podem ser lidos dessa forma:
```js
var x = document.cookie
```
**Atenção: "document.cookie" retornará todos os cookies em uma string tal como: "cookie1=value; cookie2=value; cookie3=value"**

### Altere um Cookie com JavaScript:
Com JavaScript você pode modificar um cookie da mesma forma que você o cria:
```js
document.cookie = "username=John Smith; expires=Thu, 18 Dec 2013 12:00:00 UTC; path=/"
```
O antigo cookie foi sobrescrito.

### Deletando um Cookie com JavaScript:
Deletar um cookie é bastante simples. Você não precisa especificar um valor de cookie quando for deletar um cookie. 

Apenas defina o parâmetro de expiração para uma data que já passou:
```js
document.cookie = "username=; expires=Thu, 01 Jan 1970 00:00:00 UTC; path=/"
```
**Atenção: Você deve definir o path do cookie para assegurar que você deletou o cookie correto. Alguns navegadores não vão permitir que você delete um cookie se você não especifica o path.**

### A String Cookie:
A propriedade "document.cookie" parece uma string de texto normal. Mas não é. Mesmo se você escrever uma string de cookie inteira para document.cookie, quando você a ler novamente, você pode apenas ver o par nome-valor dela.

Se você definir um novo cookie, antigos cookies não serão sobrescritos. O novo cookie é adicionado para document.cookie e, então, se você ler document.cookie novamente, você receberá algo assim:
```js
cookie1 = value; cookie2 = value
```
Se você quer encontrar o valor de um cookie específico, você deve escrever uma função JS que busca pelo valor do cookie na string de cookie.

### Exemplo de Cookie em JavaScript:
No exemplo a seguir, criaremos um cookie que armazena o nome de um visitante. A primeira vez que um visitante chega à uma página, será pedido que ele preencha seu nome. O nome é então armazenado em um cookie.

A próxima vez que o visitante chega a mesma página, ele receberá uma mensagem de boas-vindas.

Por exemplo, nós criaremos 3 funções em JavaScript:

1. Uma função para definir um valor de cookie.
2. Uma função para receber um valor de cookie.	
3. Uma fração para checar um valor de cookie.

### Uma Função Para Definir um Cookie:
Primeiro, nós criamos uma função que armazena o nome do visitante em uma variável de cookie:
```js
function setCookie(cname, cvalue, exdays) {
  var d = new Date()
  d.setTime(d.getTime() + (exdays*24*60*60*1000))
  var expires = "expires="+d.toUTCString()
  document.cookie = cname + "=" + cvalue + ";" + expires + ";path=/"
}
```
Explicação do exemplo:

Os parâmetros da função acima são o nome do cookie (cname), o valor do cookie (cname), e o número de dias até que o cookie deva expirar (exdays).

A função define um cookie ao adicionar junto o cookiename, o cookie value, e a string de expiração.

### Uma Função Para Receber um Cookie:

Então, criamos uma função que retorna o valor de um cookie específico:
```js
function getCookie(cname) {
  var name = cname + "="
  var decodedCookie = decodeURIComponent(document.cookie)
  var ca = decodedCookie.split(';')
  for(var i = 0; i < ca.length; i++) {
    var c = ca[i]
    while (c.charAt(0) == ' ') {
      c = c.substring(1)
    }
    if (c.indexOf(name) == 0) {
      return c.substring(name.length, c.length)
    }
  }
  return ""
}
```
Função explicada:

Pegue o cookiename como parâmetro (cname).

Crie uma variável (name) com o texto para ser buscado (cname + "=")

Decodifique a string do cookie, para manusear cookies com caracteres especiais, como '$'

Divida document.cookie em ponto e vírgulas dentro de um vetor chamado "ca" (ca = decodedCookie.split(';')).

Itere através do vetor "ca" (i = 0; i < ca.length; i++), e leia cada valor c = ca[i]).
Se o cookie é encontrado (c.indexOf(name) == 0), retorne o valor do cookie (c.substring(cname.length, c.length).

Se o cookie não é encontrado, retorne ""

### Uma Função Para Checar um Cookie:

Por último, criamos a função que checa se um cookie é definido.

Se o cookie é definido, ele exibirá uma saudação.

Se o cookie não está definido, ele exibirá uma caixa prompt perguntado pelo nome do usuário, e armazena o cookie "username" por 365 dias, ao chamar a função "setCookie":
```js
function checkCookie() {
  var username = getCookie("username")
  if (username != "") {
    alert("Welcome again " + username)
  } else {
    username = prompt("Please enter your name:", "")
    if (username != "" && username != null) {
      setCookie("username", username, 365)
    }
  }
}
```
**Atenção: Essas funções são escritas juntas, pois, funcionam juntas. Essa informação ficará salva até o navegador ser fechado e não apenas a aba.**

## Introdução ao AJAX:

AJAX é um sonho dos desenvolvedores, pois você poderá:
  
1. Ler dados de um servidor web - após a página ter sido carregada.
2. Atualizar a página web sem recarregar a página.
3. Enviar dados ao servidor web - no background.

Exemplo:
```html
<!DOCTYPE html>
<html>
<body>

<div id="demo">
  <h2>Let AJAX chenge this text</h2>
  <button type="button" onclick="loadDoc()">Change Content</button>
</div>

</body>
</html>
```
* A página contém uma seção ```<div>``` e um ```<button>```
* A seção ```<div>``` é usada para exibir informações de um servidor.
* O botão chama a função (quando clicada).
* A função requisita dados de um servidor web e a exibe:
```js
function loadDoc() {
  var xhttp = new XMLHttpRequest()
  xhttp.onreadystatechange = function() {
    if (this.readyState == 4 && this.status == 200) {
      document.getElementById("demo").innerHTML = this.responseText
    }
  }
  xhttp.open("GET", "ajax_info.txt", true)
  xhttp.send()
}
```
A função altera o conteúdo trazendo um texto de um documento requerido ao servidor.

### O Que É AJAX?
AJAX = Asynchronous JavaScript And XML.

AJAX não é uma linguagem de programação. AJAX apenas usa uma combinação de:

* Um navegador com o objeto "XMLHttpRequest" embutido (para realizar requisições de dados de um servidor web).
* JavaScript e HTML DOM (para exibir ou usar os dados).

**Atenção: AJAX é um nome errôneo. Aplicações AJAX podem usar XML para transporte de dados, mas também comum transporte de dados como textos simples ou textos JSON.**

AJAX permite que páginas web sejam atualizadas de forma assíncrona por trocas de dados com um servidor web "por trás da cena". Isso significa que é possível atualizar partes de uma página web sem recarregar a página inteira.

### Como AJAX Funciona?

1. Navegador:
  - Um evento ocorre.
  - Cria um objeto "XMLHttpRequest"
  - Envia um HttpRequest através da Internet.
2. Servidor:
  - Processa HTTPRequest;
  - Cria uma resposta e envia dados de volta ao navegador através da Internet.
3. Navegador:
  - Processa os dados retornados usando JavaScript;
  - Atualiza o conteúdo da página através da ação requisitada.

## O OBJETO XMLHttpRequest

Todos os navegadores modernos suportam o objeto XMLHttpRequest. O objeto pode ser usado para trocar daos de um servidor web "por trás das cenas". 

### Criando um Objeto XMLHttpRequest:
Todos os navegadores modernos têm esse objeto embutido.

Sintaxe para criação:
```js
variável = new XMLHttpRequest()
```
Exemplo: 
```js
var xhttp = new XMLHttpRequest()
```
### Acesso Em Vários Domínios:
Por questões de segurança, navegadores modernos não permitem acesso a varios domínios. Isso significa que tanto a página web, quanto o arquivo XML que ele tenta carregar, devem estar localizados no mesmo servidor.

Os exemplos na W3Schools todos abrem arquivos XML localizados no domínio W3Schools. Se você deseja usar o exemplo anteior em suas próprias páginas web, os arquivos XML que você carregar devem estar localizados em seu próprio servidor.

### Navegadores Modernos (Fetch API)
Navegadores modernos usam Fetch API ao invés do Objeto XMLHttpRequest.

A interface da Fetch API permite que os navegadores web façam requisições HTTP para os servidores web.

Se você usa o objeto XMLHttpRequest, Fetch pode fazer o mesmo em uma maneira mais simples.

### Navegadores Antigos (IE5 e IE6)
Esses navegadores usam um objeto ActiveX ao invés de XMLHttpRequest.
```js
variável = new ActiveXObject ("Microsoft.XMLHTTP")
```
Para lidar com IE e IE6, cheque se o navegador suporta o objeto XMLHttpRequest, ou então cire um objeto "ActiveX":
```js
if (window.XMLHttpRequest) {
  xmlhttp = new XMLHttpRequest()
} else {
  xmlhttp = new ActiveXObject("Microsoft.XMLHTTP)
}
```
### Métodos do Objeto XMLHttpRequest:

| | |
|---|---|
| new XMLHttpRequest()	|	Cria um novo objeto XMLHttpRequest
| abort()			|	Cancela a requisição atual.
| getAllResponseHeaders()	|	Retorna a informação de cabeçalho.
| getResponseHeader()	|	Retorna uma específica informação de cabeçalho.
| open(método, url, async, user, psw)	|	Especifica a requisição: Método: requisição do tipo GET ou POST. / url: o enderço do arquivo. / async: true (assíncrono) ou falso (síncrono). / user: nome opcional de usuário. / psw: senha opcional.
| send()		    	|	Envia a requisição para o servidor. Usado para requisições GET.
| send(string)		|	Envia a requisição ao servidor. Usado para requisições POST.
| setRequestHeader()	|	Adiciona um par camada/valor ao cabeçalho para ser enviado.

### Propriedades de Objeto XMLHttpRequest:

| | |
|---|---|
onreadystatechange		|	Define uma função para ser chamada quando a propriedade readyState é alterada.
readyState:		        |	Detém o status do XMLHttpRequest. 0: Requisição não inicializada. / 1: Conexão com servidor estabelecida. / 2: Requisição recebida. / 3: Processando requisição. / 4: Requisição finalizada e resposta está pronta.
responseText		|	Retorna os dados de resposta como uma string.
responseXML		    |	Retorna os dados de resposta como dados XML.
status			    |	Retorna o número-status de uma requisição: 200: "OK" / 403: "Forbidden" / 404: "Not Found".
statusText			|	Retorna o texto-status ("OK", ou "Not Found")

Para mais formas, acesse [HTTP STATUS MESSAGES](https://www.w3schools.com/tags/ref_httpmessages.asp) 

## AJAX - Enviando uma Requisição ao Servidor:

Para enviar uma requisição so servidor, usamos os métodos open() e send() do objeto XMLHttpRequest.
```js
xhttp.open("GET", "ajax_info.txt", true)
xhttp.send()
```
### GET ou POST?

GET é mais simples e mais rápido do que POST, e pode ser usado na maioria dos caso.
No entanto, sempre use requisições POST quando:

1. Um arquivo em cache não é uma opção (atualizar um arquivo ou database no servidor).
2. Enviando uma grande quantidade de dados ao servidor (POST não tem limitações de tamanho).
3. Enviando input de usuários (no qual pode conter caracteres desconhecidos), POST é mais robusto e seguro do que GET.

### Requisições GET:
```js
xhttp.open("GET", "demo_get.asp", true)
xhttp.send()
```
Se você deseja enviar informações com o método GET, adicione a informação à URL.
```js
xhttp.open("GET", "demo_get2.asp?fname=Henry&lname=Ford", true)
xhttp.send()
```
### Requisições POST:
```js
xhttp.open("POST", "demo_post.asp", true)
xhttp.send()
```
Para dados de POST, como um formulário HTML, adicione um cabeçalho HTTP com "setRequestHeader()". Especifique os dados que você quer enviar no método "send()"
```js
xhttp.open("POST", "ajax_text.asp", true)
xhttp.setRequestHeader("Content-type", "application/x-www-form-urlencoded")
xhttp.send("fname=Henry&lname=Ford")
```
```js
setRequestHeader(header, value)	
//	Adiciona cabeçados HTTP à requisição.
// * header: especifica o nome do cabeçalho.
// * value: especifica o valor do cabeçalho.
```

### A URL - Um Arquivo Em Um Servidor:

O parâmetro de url do método "open()" é um endereço para um arquivo no servidor:

```js
xhttp.open("GET", "ajax_text.asp", true)
```
O arquivo pode ser qualquer tipo de arquivo, como .txt e .xml, ou arquivos de script do servidor como .asp e .php (no qual pode executar ações no servidor antes de enviar a resposta de volta).

### Assíncrono - True ou False?
Os requerimentos de servidor devem ser enviados de forma assíncrona.
O parâmetro async do método "open()" deve ser definido para true:
```js
xhttp.open("GET", "ajax_test.asp", true)
```

Ao enviar de forma assíncrona, o JS não tem que esperar pela resposta do servidor, mas pode ao invés disso:
- executar outros scripts enquanto espera pela resposta do servidor.
- lida com a resposta depois que a resposta está pronta.

### A Propriedade onreadystatechange:

Com o objeto "XMLHttpRequest", você pode definir uma função para ser executada quando a requisição receber uma resposta.

A função é definida na propriedade "onreadystatechange" do objeto XMLHttpRequest:
```js
xhttp.onreadystatechange = function() {
  if (this.readyState == 4 && this.status == 400) {
    document.getElementByI("demo").innerHTML=	
    this.responseText
  }
}
xhttp.open("GET", "ajax_info.txt", true)
xhttp.send()
```

### A Requisição Síncrona:

Para executar uma requisição síncrona, mude o terceiro parâmetro no "open()" para false.

Às vezes, async=false é usado para testes rápidos. Você poderá encontrar algumas requisições síncronas em antigos códigos JavaScript.

Desde que o código esperará pela completação do servidor, não há necessidade por uma função "onreadystatechange":
```js
xhttp.open("GET", "ajax_info.txt", false)
xhttp.send()
document.getElementById("demo").innerHTML = 
xhttp.responseText
```
**Atenção: XMLHttpRequest síncrono (async = false) não é recomendado porque o JS parará de executar até o servidor responder que está pronto. Se o servidor está lento ou ocupado, a aplicação vai travar ou parar. Esse formato está no processo de ser removido do padrão web, mas esse processo pode tomar muitos anos. Ferramentas modernas para desenvolvedores são encorajadas a alertar sobre usar requisições síncronas e podem lançar exceções InvalidAccessError quando elas ocorrem.**

## AJAX - A Resposta do Servidor:

A propriedade "readyState" mantém o status da XMLHttpRequest.

A propriedade "onreadystatechange" define uma função para ser executada quando a "readyState" é alterada.

As propriedades "status" e "statusText" mantêm o status do objeto XMLHttpRequest.

A função "onreadystatechange" é chamada toda vez que "readyState" altera. Quando "readyState" é 4 e o status é 200, a resposta está pronta:
```js
function loadDoc() {
  var xhttp = new XMLHttpRequest()
  xhttp.onreadystatechange = function() {
    if (this.readyState == 4 && this.status == 200) {
      document.getElementById("demo").innerHTML= this.responseText
    }
  }
  xhttp.open("GET", "ajax_info.txt", true)
  xhttp.send()
}
```
**Atenção: O evento "onreadystatechange" é chamado quatro vezes (1-4), uma vez para cada mudança no readyState.**

### Usando uma Função Callback:
Uma função callback é uma função que é passada como parâmetro para uma outra função.

Se você tem mais do que uma tarefa AJAX em um website, você deveria criar uma função para executar o objeto XMLHttpRequest, e uma função callback para cada tarefa AJAX.

A chamada da função deveria conter a URL e o que a função chamar quando a resposta está pronta:
```js
onclick="loadDoc('ajax_info.txt', myFunction)"	

function loadDoc(url, cFunction) {
  var xhttp
  xhttp = new XMLHttpRequest()
  xhttp.onreadystatechange = function() {
    if (this.readyState == 4 && this.status == 200) {
      cFunction(this)
    }
  }
  xhttp.open("GET", url, true)
  xhttp.send()
}
function myFunction(xhttp) {
  document.getElementById("demo").innerHTML = 
  xhttp.responseText
}
```

### Propriedades de Resposta do Servidor:
| | |
|:---:|---|
responseText	|	recebe o dado de resposta como uma string.
responseXML 	|	recebe o dado de resposta como dado XML.

### Métodos de Resposta do Servidor:

| | |
|---|---|
getResponseHeader()	|	Retorna uma informação de cabeçalho específico de uma fonte de servidor.
getAllResponseHeaders()	|	Todas as informações de cabeçalho de uma fonte de servidor.

### responseXML:
O objeto XMLHttpRequest tem um analisador XML embutido.

A propriedade "responseXML" retorna a resposta do servidor como um objeto XML DOM.
Usando essa propriedade, você pode analisar a resposta como um objeto XML DOM:

Exemplo requerindo o arquivo "cd_catalog.xml" e analisando a resposta:
```js
var http, xmlDoc, txt, x, i
xhttp = new XMLHttpRequest()
xhttp.onreadystatechange = function() {
  if (this.readyState == 4 && this.status == 200) {
    xmlDoc = this.responseXML
    txt = ""
    x = xmlDoc.getElementByTagName("ARTIST")
    for (i = 0; i < x.length; i++) {
      txt += x[i].childNodes[0].nodeValue + "<br>"
    }
    document.getElementById("demo").innerHTML = txt
  }
}
xhttp.open("GET", "cd_catalog.xml", true)
xhttp.send()

> getAllResponseHeaders()

var xhttp = new XMLHttpRequest()
xhttp.onreadystatechange = function () {
  if (this.readyState == 4 && this.status == 200) {
      document.getElementByI("demo").innerHTML =
      this.getAllResponseHeaders()
  }
}
xhttp.open("GET", "ajax_info.txt", true)
xhttp.send()
accept-ranges: bytes age: 6005 cache-control: public,max-age=14400,public content-encoding: gzip content-length: 245 content-type: text/plain date: Thu, 04 Mar 2021 06:27:54 GMT etag: "15bfdeee0ffd21:0" last-modified: Tue, 18 Jul 2017 16:14:29 GMT server: ECS (mic/9B49) vary: Accept-Encoding x-cache: HIT x-firefox-spdy: h2 x-frame-options: SAMEORIGIN x-powered-by: ASP.NET 

// retorna informações de cabeçalho de uma fonte, como length, server-type, content-type, last-modified, etc.
```
### getResponseHeader()
```js
var xhttp = new XMLHttpRequest()
xhttp.onreadystatechange = function() {
  if (this.readyState == 4 && this.status == 200) {
      document.getElementById("demo").innerHTML = 
      this.getResponseHeader("Last-Modified")
  }
}
xhttp.open("GET", "ajax_info.txt", true)
xhttp.send()	
// Last modified: Tue, 18 Jul 2017 16:14:29 GMT
```

## AJAX XML

AJAX pode ser usado para comunicações interativas com um arquivo XML

O exemplo a seguir demonstra como uma página web pode buscar informações de um arquivo XML com AJAX:
```html
<button type="button" onclick="loadDoc()">Get my CD Collection</button>
<br><br>
<table id="demo"></table>

<script>
function loadDoc() {
  var xhttp = new XMLHttpRequest()
  xhttp.onreadystatechange = function() {
      if (this.readyState == 4 && this.status == 200) {
          myFunction(this)
      }
  }
  xhttp.open("GET", "cd_catalog.xml", true)
  xhttp.send()
}

function myFunction(xml) {
  var i
  var xmlDoc = xml.responseXML
  var table= "<tr><th>Artist</th><th>Title</th></tr>"
  var x = xmlDoc.getElementByTagName("CD")
  for (i = 0; i < x.length; i++) {
      table += "<tr><td>" + 
      x[i].getElementByTagName("ARTIST")[0].childNodes[0].nodeValue + "</td><td>" +
      x[i].getElementByTagName("TITLE")[0].childNodes[0].nodeValue + "</td></tr>"
  }
  document.getElementById("demo").innerHTML = table
}
</script>
```

### Explicação do Exemplo:
Quando um usuário clica no botão "Get CD info", a função loadDoc() é executada.

A função loadDoc() cria um objeto XMLHttpRequest, adiciona a função para ser executada quando o servidor está pronto, e envia a solicitação para o servidor.

Quando o servidor response que está pornto, uma tabela HTML é construída, nódulos (elementos) são extraídos do arquivo XML, e é finalmente atualizado o elemento "demo" com a tabela HTML preenchida com dados XML. 

## AJAX PHP - Exemplo:

AJAX é usado para criar mais aplicações interativas.

O exemplo a seguir demonstra como uma página web pode comunicar com um servidor web enquanto um usuário digita caracteres em um campo de input:
```html
<p> Suggestions: <span id="txtHint"></span></p>

<form>
First name: <input type="text" onkeyup="showHints(this.value)">
</form>	

<script>
function showHint(str) {
    if (str.length == 0) {
        document.getElementById("txtHint").innerHTML == ""
        return;
    } else {
        var xmlhttp = new XMLHttpRequest()
        xhmlhttp.onreadystatechange = function() {
            if (this.readyState == 4 && this.status == 200) {
                document.getElementById("txtHind").innerHTML = this.responseText;
            }
        }
        xmlhttp.open("GET", "gethint.php?q=" + str, true)
        xmlhttp.send()
    }
}
</script>
```

### Explicação do Código:

Primeiro, verifica se o campo de input está vazio (str.length == 0). Se ele está, limpa o conteúdo do espçao reservado ao txtHint e sai da função.

No entanto, se o campo de input não está vazio, o código faz:
1. Cria um objeto XMLHttpRequest
2. Cria a função para ser executada quando a resposta do servidor está pronta.
3. Envia a solicitação ao arquivo PHP (gethint.php) no servidor.
4. Note que o parâmetro "q" é adicionado ao "gethint.php?q="+str.
5. A variável str detém o conteúdo do campo de input.

**Atenção: O parâmetro "q" em uma URL define que o campo que será buscado e por qual critério. Por exemplo, se você desejar uma informação com "DNA" no título do artigo, nós contruiríamos a seguinte URL:**

http://api.plos.org/search?q=title:DNA

Com conhecimento de campos disponíveis, queries complexas podem ser construídas.

http://www.google.com?q=facebook

**Atenção: O mesmo código utilizado em PHP pode ser utilizado em ASP, ou seja, arquivos .asp para realizar a mesma tarefa.**

## AJAX DATABASE:

AJAX pode ser usado para comunicações interativas com um database.

O seguinte exemplo demonstrará como uma página web busca informações a partir de um database com AJAX:
```html
<style>
table,th,td {
  border: 1px solid black;
  border-collapse: collapse;
}
th,td {
  padding: 5px;
}
</style>
<body>

<h2>The XMLHttpRequest Object</h2>

<form action="">
    <select name="customers" onchange="showCustomer(this.value)">
        <option value="">Select a customer:</option>
        <option value="ALFKI">Alfred Futterkiste</option>
        <option value="NORTS">North/South</option>
        <option value="WDLZA">Wolski Zajazd</option>
    </select>
</form>
<br>
<div id="txtHint">Customer info will be listed here...</div>

<script>
function showCustomer(str) {
    var xhttp
    if (str == "") {
        document.getElementById("txtHint").innerHTML = "";
        return;
    }
    xhttp = new XMLHttpRequest()
    xhttp.onreadystatechange = function() {
        if (this.readyState == 4 && this.status == 200) {
            document.getElementById("txtHint").innerHTML = this.responseText
        }
    }
    xhttp.open("GET", "getcustomer.php?q="+str, true)
    xhttp.send()
}
</script>	
```
**Atenção: A parte destinada ao CSS está destinada para os documentos dentro do arquivo PHP, no qual, contém tabelas com identificações para estilização.**

## AJAX - Aplicações XML:

### Exibindo o Primeiro CD em um Elemento HTML div
Esse exemplo usa uma função para exibir o primeiro elemento CD em um elemento HTML com id="showCD":
```js
displayCD(0)

function displayCD(i) {
    var xmlhttp = new XMLHttpRequest()
    xmlhttp.onreadystatechange = function() {
        if (this.readyState == 4 && this.status == 200) {
            myFunction(this, i)
        }
    }
    xmlhttp.open("GET", "cd_catalog.xml", true)
    xmlhttp.send()
}

function myFunction(xml, i) {
    var xmlDoc = xml.responseXML
    document.getElementById("showCD").innerHTML = "Artist: " +
    x[i].getElementsByTagName("ARTIST")[0].childNodes[0].nodevalue + "<br>Title: " +
    x[i].getElementsByTagName("TITLE")[0].childNodes[0].nodeValue + "<br>Year: " +
    x[i].getElementsByTagName("YEAR")[0].childNodes[0].nodeValue;
}
```
**Atenção: Ao mudar o número, você pode acessar outros artistas, títulos de álbuns e ano de lançamento.**

### Navegar Entre os CDs:

Para facilitar, você criar dois botões (um "próximo", e outro "anterior") para navegar entre as informações:
```js
function next() {
    if (i < len-1) {
        i++
        displayCD(i)
    }
}
// Adiciona 1 toda vez que o botão é apertado. Subtrai 1 do length de CDs até chegar no último valor, quando não consegue mais executar.

function previous() {
    if (i > 0) {
        i--
        displayCD(i)
    }
}
```

> Mostra Informações de Álbuns Quando Clicar Sobre um CD:
```html
<p>Click on a CD to display album information>/p>
<p id="showCD"></p>
<table id=demo"></table>

<script>
var x, xmlhttp, xmlDoc
xmlhttp = new XMLHttpRequest()
xmlhttp.open("GET", "cd_catalog.xml", false)
xmlhttp.send()
xmlDoc = xmlhttp.responseXML
x = xmlDoc.getElementsByTagName("CD")
table = "<tr><th>Artist</th><th>Title</th></tr>"
for (i = 0; i < x.length; i++) {
    table += "<tr onclick='displayCD(" + i + ")'><td>
    table += x[i].getElementsByTagName("ARTIST")[0].childNodes[0].nodeValue
    table += "</td><td>
    table += x[i].getElementsByTagName("TITLE")[0].childNodes[0].nodeValue
    table += "</td></tr>"
}
document.getElementById("demo").innerHTML = table

function displayCD(i) {
    document.getElementById("showCD").innerHTML = 
    "Artist: " +
    x[i].getElementsByTagName("ARTIST")[0].childNodes[0].nodeValue +
    "<br>Title: " +
    x[i].getElementsByTagName("TITLE")[0].childNodes[0].nodeValue +
    "<br>Year: " +
    x[i].getElementsByTagName("YEAR")[0].childNodes[0].nodeValue 
}
</script>
<!-- O clique identifica o valor de "i" e retorna como parâmetro na função "displayCD(i) -->
```

## Introdução ao JSON:

Quando trocamos dados entre um navegador e um servidor, dados podem apenas ser textuais.

JSON é textom e nós podemos converter qualquer objeto JavaScript em JSON, e enviá-lo para o servidor.

Nós podemos também converter qualquer JSON convertido do servidor em objetos JS. Dessa maneira podemos trabalhar com os dados como objetos JS, com análises e traduções sem complicações.

### Enviando Dados:
```js
var myObj = {name: "John", age: 31, city: "New York"}
var myJSON = JSON.stringify(myObj)
window.location = "demo_json.php?x=" + myJSON
```
**Atenção: "?x=" ou "?q=" são exemplos de QueryStrings.**

### Recebendo Dados:
```js
var myJSON = '{"name":"John", "age":31, "city":"New York")'
var myObj = JSON.parse(myJSON)
document.getElementById("demo").innerHTML = myObj.name
// John
```
### Armazenado Dados:
Quando armazenamos dados, os dados devem estar em um certo formato, e, não importando onde você escolha armazena-lo, texto é sempre um dos formatos legais.
JSON faz isso possível para armazenar objetos JS como texto.

Exemplo de armazenagem em um armazenamento local:
```js
// armazenando:
myObj =  {name: "John", age: 31, city: "New York"};
myJSON = JSON.stringify(myObj)
localStorage.setItem("testJSON"), myJSON)

// recebendo:
text = localStorage.getItem("testJSON")
obj = JSON.parse(text)
document.getElementById("demo").innerHTML = obj.name
// John
```
### O Que É JSON?

* JSON significa JavaScript Object Notation.
* JSON é um formato leve de transferência de dados.
* JSON é "auto-descritivo" e de fácil entendimento.
* JSON é uma linguagem independente *

**Atenção: * JSON use sintaxe JavaScript, mas o formato JSON é apenas textual. Texto pode ser lido e usado como formato de dado por qualquer linguagem de programação.
**
### Por Que JSON?
Já que o formato JSON é apenas textual, ele pode ser facilmente enviado e recebido de um servidor. JavaScript possui uma função embutida para converter uma string, escrito no formato JSON, para objetos nativos do JS:
```js
JSON.parse()
```

Então, se você receber dados de um servidor, no formato JSON, você pode usa-lo como qualquer outro formato JS.

## Sintaxe de JSON

* Dados em pares de nome/valor;
* Dados separados por vírgulas;
* Chaves { } armazenam objetos;
* Colchetes [ ] armazenam vetores.

**Atenção: Nomes em JSON requerem aspas duplas (" "). Já em JavaScript isso não é necessário.**

**Atenção: Em JSON, os nomes (chaves) devem ser strings, escritos com aspas duplas: { "name":"John" }**

**Atenção: Em JSON, valores devem ser um dos seguintes tipos de dados: string, número, objeto, vetor, booleano e null. Já em JavaScript, todos esses podem, além de: funções, datas, e undefined.**

**Atenção: Como JSON é derivado de JavaScript, pouco software extra é necessário para trabalhar com JSON dentro de JS.**

**Atenção: O tipo de arquivo para arquivos JSON é ".json". O MIME-type para o texto JSON é "application/json".**

**Atenção: "MIME-type" é um mecanismo para dizer ao cliente a variedade de documentos transmitidos: a extensão de um nome de arquivo não tem significado na web. A sintaxe é "tipo/subtipo", como "text/html", "image/jpeg", "audio/ogg", "video/mp4", etc.**

## JSON vs XML

Ambos JSON e XML pode ser usados para recebimento de dados de um servidor web.
O seguinte exemplo coma ambos JSON e XML definem um objeto "employees" com um vetor de 3 empregados:

Exemplo JSON:
```js
{"employees": [
  {"firstName":"John", "lastName":"Doe"},
  {"firstName":"Anna","lastName":"Smith"},
  {"firstName":"Peter", "lastName":"Jones"}
]}
```
Exemplos XML:
```xml
<employees>
    <employee>
        <firstName>John</firstName> <lastName>Doe</lastName>
    </employee>
    <employee>
        <firstName>Anna</firstName> <lastName>Smith</lastName>
    </employee>
    <employee>
        <firstName>Peter</firstName> <lastName>Jones</lastName>
    </employee>
</employees>
```

### JSON é igual ao XML porque:

- Ambos são "auto-descritivos" (legíveis para humanos)
- Ambos são hierárquicos (valores dentro de valores)
- Ambos pode ser analisados e usados por várias linguagens de programação;
- Ambos pode ser buscados com um XMLHttpRequest.

### JSON não é igual ao XML porque:

- JSON não usa tags de finalização.
- JSON é mais curto
- JSON é mais rápido de ler e escrever.
- JSON pode usar vetores.

A grande diferença é:

XML tem que ser analisada com um XML parser. JSON pode ser analisado por uma função padrão JavaScript.

### Por que JSON é Melhor do que XML:

1. XML é muito mais difícil de analisar do que JSON.
2. JSON é analisado em objetos JavaScript prontos para uso.
3. Para aplicações AJAX, JSON é mais rápido e mais fácil do que XML:

**Usando XML:**
1. Busca um documento XML;
2. Use o XML DOM para iterar através do documento;
3. Extraia valores e armazene em variáveis.

**Usando JSON:**
1. Busque uma string JSON;
2. JSON.Parse a string JSON.


## Tipos de Dados em JSON:

1. Strings devem ser escritas em aspas duplas: { "name":"John" }
2. Números devem ser um inteiro ou de ponto flutuante: {"age":30}

3. Objetos como valores em JSON devem seguir as mesmas regras como objetos JSON.
```js
{
"employee": { "name":"John", "age":30, "city":"New York" }
}
```
4. Vetores:
```js
{
"employees": [ "John", "Anna", "Peter" ]
}
```
5. Booleanos podem ser true/false: { "sale":true }
6. Valores em JSON pode ser null: { "middlename":null }

### JSON.parse()

Ao analisar os dados com "JSON.parse()" e os dados tornam-se um objeto JavaScript.

#### Exemplo:
Imagine que recebemos esse texto de um servidor web:
```js
'{ "name":"John", "age":30, "city":"New York" }'
```
Use a função "JSON.parse()" converte texto em objeto JS:
```js
var obj = JSON.parse( '{ "name":"John", "age":30, "city":"New York" }' )
```
**Atenção: Tenha certeza que o texto está escrito em formato JSON, ou então vai retornar uma erro de sintaxe.**

Use o objeto JS em sua página:
```html
<p id="demo"></p>

<script>
document.getElementById("demo").innerHTML = obj.name + ', ' + obj.age
</script>
<!-- Retorna: "John, 30" -->
```
### JSON a partir do Servidor:
Você pode solicitar JSON de um servidor usando um requerimento AJAX. 

Enquanto a resposta do servidor é escrita em formato JSON, você pode analisar a string em objeto JavaScript.

```js
var xmlhttp = new XMLHttpRequest()
xmlhttp.onreadystatechange = function() {
    if (this.readyState == 4 && this.status == 200) {
        var myObj = JSON.parse(this.responseText) 
        document.getElementById("demo").innerHTML = myObj.name
    }
}
xmlhttp.open("GET", "json_demo.txt", true)
xmlhttp.send()
```
**Atenção: O mesmo pode ser realizado se o arquivo em texto for um vetor:**
```js
var myArr = JSON.parse(this.responseText)
document.getElementById("demo").innerHTML = myArr[0]
```

### Exceções:

#### Analisando Dados

Objetos de data não são permitidos em JSON. Se você precisa incluir uma data, escreva como string. Você pode converter de volta em um objeto de data depois:
```js
var text = '{ "name":"John", "birth":"1986-12-14", "city":"New York" }'
var obj = JSON.parse(text)
obj.birth = new Date(obj.birth)

document.getElementById("demo").innerHTML = obj.name + ", " + obj.birth
// Retorna: John, Sat Dec 13 1986 22:00:00 GMT-0200 (Horário de Verão de Brasília)
```
Ou você usar o segundo parâmetro da função JSON.parse() chamado "reviver".
O parâmetro "reviver" é uma função que verifica cada propriedade antes de retornar um valor:
```js
var text = '{ "name":"John", "birth":"1986-12-14", "city":"New York"}'
var obj = JSON.parse(text, function(key, value) {
  if (key == "birth") {
    return new Date(value)
  } else {
    return value
  }
})
document.getElementById("demo").innerHTML = obj.name + ", " = obj.birth
// Retorna "John, Sat Dec 13 1986 22:00:00 GMT-0200 (Horário de Verão de Brasília)"
```
#### Analisando Funções

Funções não são permitidas em JSON. Se você precisa incluir uma função, a escreva como uma string. Você pode converte-la novamente em uma função posteriormente:
```js
var text = '{ "name":"John", "age":"function () {return 30;}", "city":"New York"}'
var obj = JSON.parse(text)
obj.age = eval("(" + obj.age + ")")

document.getElementById("demo").innerHTML = obj.name + ", " + obj.age()
```
**Atenção: Você deveria evitar usar funções em JSON, pois as funções perderão seus escopos, e você teria que usar "eval()" para converter-las de volta em funções.**

## JSON.stringify()

Quando enviamos dados para um servidor, os dados devem ser uma string.

Converta um objeto JS em uma string com "JSON.stringify()"

### Stringify um Objeto JS:

Imagine que tens esse objeto em JavaScript:
```js
var obj = { name: "John", age: 30, city: "New York" }
```
Use a função JSON.stringify() para converte-la em uma string.
```js
var myJSON = JSON.stringify(obj)
```
O resultado será uma string que segue a notação JSON. "myJSON" é agora uma string pronta para ser enviada ao servidor.

O mesmo pode ser feito com vetores.

### Exceções:
Em JSON, objetos de data e funções não são permitidos. A função "JSON.stringify()" converterá qualquer dados em strings.

**Atenção: Você pode converter uma string novamente em um objeto de data ao recebedor.**

#### Stringify Funções

Em JSON, funções não são permitidas como valores de objetos. 

A função "JSON.stringify()" removerá qualquer função de um objeto JavaScript, ambos as chaves e o valor:
```js
var obj = { name: "John", age: function () {return 30;}, city: "New York"}
var myJSON = JSON.stringify(obj)
document.getElementById("demo").innerHTML = myJSON
// Retorna "{"name":"John","city":"New York"}"
```
Isso pode ser omitido se você converter funções em strings antes de executar a função "JSON.stringify()":
```js
var obj = { name: "John", age: function () {return 30;}, city: "New York" };
obj.age = obj.age.toString()
var myJSON = JSON.stringify(obj)
document.getElementById("demo").innerHTML = myJSON
// {"name":"John","age":"function () {return 30;}","city":"New York"}
```
**Atenção: Se você enviar funções usando JSON, as funções perderão seus escopos, e o recebedor terá que usar "eval()" para converter novamente em funções.**

## Objetos JSON

Você pode acessar valores de objetos em objetos JSON através de pontos (.) ou colchetes ([ ]). 
```js
x = myObj.name
y = myObj["name"]
```

### Iterando um Objeto:

Você pode iterar através de propriedades de objetos usando o loop "for-in":
```js
myObj = { "name":"John", "age":30, "car":null }
for (x in myObj) {
  document.getElementById("demo").innerHTML += x + "<br>"
}
// name 
// age
// car
```
Em um loop "for-in"
```js
myObj = { "name":"John", "age":30, "car":null };
for (x in myObj) {
  document.getElementById("demo").innerHTML += myObj[x] + "<br>"
// John
// 30
// null
```

### Objetos Aninhados em JSON:

Valores em um objeto JSON pode estar em um outro objeto JSON:
```js
myObj = {
  "name":"John",
  "age":30,
  "cars": {
    "car1":"Ford",
    "car2":"BMW",
    "car3":"Fiat"
  }
}
```
Você pode acessar objetos aninhados JSON através do uso de notação de ponto ou notação de colchetes:
```js
x = myObj.cars.car2

x = myObj.cars["car2"]
```

Da mesma forma você usar para modificar valores:
```js
myObj.cars.car2 = "Mercedes"

myObj.cars["car2"] = "Mercedes"
```

Assim como você pode usar para deletar propriedades com a keyword "delete":
```js
delete mybj.cars.cars2
```

## Vetores em JSON:

Você acessar valores de vetores dentro de objetos usando números de indexação:
```js
x = myObj.cars[0]
```

### Iterando através de um Vetor:

Você pode acessar valores de um vetor usando o loop "for-in":
```js
for (i in myObj.cars) {
  x += myObj.cars[i] + "<br>"
}
```
Ou você pode usar um loop "for":
```js
for (i = 0; i < myObj.cars.length; i++) {
  x += myObj.cars[i] + "<br>"
}
```

### Vetores Aninhados em Objetos JSON:
Valores em um vetor podem também estar em um outro vetor, ou mesmo em um outro objeto JSON:
```js
myObj = {
  "name":"John",
  "age":30,
  "cars": [
      { "name":"Ford", "models":["Fiesta", "Focus", "Mustang"]},
      { "name":"BMW", "models":[ "320", "X3", "X5" ] },
      { "name":"Fiat", "models":[ "500", "Panda" ] }
  ]
}
```

Para acessar vetores dentro de vetores, use o loop "for-in" para cada vetor: 
```js
var x = ""
for (i in myObj.cars) {
    x += "<h2>" + myObj.cars[i].name + "</h2>"
    for (j in myObj.cars[i].models) {
        x += myObj.cars[i].models[j] + "<br>"
    }
}
document.getElementById("demo").innerHTML = x
```

## JSON PHP:

### O Arquivo PHP:

PHP tem alguma funções embutidas para lidar com JSON.

Objetos em PHP pode ser convertidos em JSON através do uso da função PHP "json_encode()":
```php
<?php
$myObj->name = "John";
$myObj->age = 30;
$myObj->city = "New York";

$myJSON = json_encode($myObj)

echo $myJSON
?>
// {"name":"John","age":30,"city":"New York"}
```

### O Cliente JavaScript:

Aqui está um código JS no cliente, usando uma chamada AJAX para solicitar o arquivo PHP do exemplo acima.
Use JSON.parse() para converter o resultado em um objeto JS:
```js
var xmlhttp = new XMLHttpRequest()
xmlhttp.onreadystatechange = function()
    if (this.readyState == 4 && this.status == 200) {
        var myObj = JSON.parse(this.responseText)
        document.getElementById("demo").innerHTML = myObj.name
    }
}
xmlhttp.open("GET", "demo_file.php", true)
xmlhttp.send()
// "John"
```

### Vetor em PHP:
Vetores em PHP também serão convertidos em JSON ao usar a função "json_encode()":
```php
<?php
$myArr = array("John", "Mary", "Peter", "Sally")

$myJSON = json_encode($myArr)

echo $myJSON
?>
// ["John","Mary","Peter","Sally"]
```

Usando o JSON.parse() para converter o resultado em um vetor JS:
```js
var xmlhttp = new XMLHttpRequest();
xmlhttp.onreadystatechange = function() {
    if (this.readyState == 4 && this.status == 200) {
        var myObj = JSON.parse(this.responseText);
        document.getElementById("demo").innerHTML = myObj[2]
    }
}
xmlhttp.open("GET", "demo_file_arry.php", true)
xmlhttp.send()
// "Peter"
```

### PHP Database:
PHP é uma linguagem de programação do lado servidor, e pode ser usada para acessar um database.

Imagine que você tem um database em seu servidor, e você quer enviar uma solicitação para ele a partir do cliente onde você pede as 10 primeiras colunas em uma tabela chamada "customers".

No lado cliente, faça um objeto JSON que descreve o número de colunas que você deseja retornar.

Antes de enviar a solicitação para o servidor, converta o objeto JSON em uma string e envie-a como um parâmetro para a url da página PHP:
```js
var obj, dbParam, xmlhttp
obj = { "limit":10 }
dbParam = JSON.stringify(obj)
xmlhttp = new XMLHttpRequest()
xmlhttp.onreadystatechange = function()
    if (this.readyState == 4 && this.status == 200) {
        document.getElementById("demo").innerHTML = this.responseText
    }
}
xmlhttp.open("GET", "json_demo_db.php?x=" + dbParam, true)
xmlhttp.send()
```

Explicação do exemplo:
1. Defina um objeto contendo uma propriedade "limite" e o valor.
2. Converta o objeto em uma stirng JSON.
3. Envie uma solicitação do arquivo PHP com a string JSON como um parâmetro.
4. Espere até a requisição retornar com o resultado (como JSON)
5. Exiba o resultado recebido do arquivo PHP.

### O arquivo PHP:
```php
<?php
header("Content-Type: application/json; charset=UTF-8");
$obj = json_decode($_GET["x"], false);

$conn = new mysqli("myServer", "myUser", "myPassword", "Northwind");
$stmt = $conn->prepare("SELECT name FROM customers LIMIT ?");
$stmt->bind_param("s", $obj->limit);
$stmt->execute();
$result = $stmt->get_result();
$outp = $result->fetch_all(MYSQLI_ASSOC);

echo json_encode($outp);
?>
```

Explicação do Arquivo PHP:
1. Converta a solicitação em um objeto usando a função PHP "json_decode()"
2. Acessa o database e prencha o vetor com os dados requeridos.
3. Adicione o vetor para um objeto e retorne o objeto como JSON usando a função "json_encode().

### Itere Através do Resultado:
Converta o resultado recebido de um arquivo PHP em um objeto JS, ou nesse caso, um vetor JS:
```html
<script>
var obj, dbParam, xmlhttp, myObj, x, txt = ""
obj = { "limit":5 }
dbParam = JSON.stringify(obj)
xmlhttp = new XMLHttpRequest()
xmlhttp.onreadystatechange = function() {
    if (this.readyState == 4 && this.status == 200) {
        myObj = JSON.parse(this.responseText)
        for (x in myObj) {
            txt += myObj[x].name + "<br>"
        }
        document.getElementById("demo").innerHTML = txt
    }
}
xmlhttp.open("GET", "json_demo_db.php?x=" + dbParam, true)
xmlhttp.send()
</script>
<!--  Alfreds Futterkiste, Ana Trujillo Emparedados y helados, Antonio Moreno Taqueria, Around the Horn, Berglunds snabbkop -->
```
### Método PHP = POST

Quando enviamos dados a um servidor, é frequemente melhor usarmos o método HTTP "POST". 

Para enviar requisições AJAX usando o método POST, especifique o método e o cabeçalho correto. O dado enviado para o servidor deve agora ser um argumento para o método "send()":
```js
obj = { "limit":10 }
dbParam = JSON.stringify(obj)
xmlhttp = new XMLHttpRequest()
xmlhttp.onreadystatechange = function() {
    if (this.readyState == 4 && this.status == 200) {
        myObj = JSON.parse(this.responseText)
        for (x in myObj) {
            txt += myObj[x].name + "<br>"
        }
        document.getElementById("demo").innerHTML = txt
    }
}
xmlhttp.open("POST", "json_demo_db.php", true)
xmlhttp.setRequestHeader("Content-type", "application/x-www-form-urlencoded")
xmlhttp.send("x=" + dbParam)
```

A única diferença no arquivo PHP é o método para receber o dado transferido:
```php
<?php
header("Content-Type: application/json; charset=UTF-8");
$obj = json_decode($_POST["x"], false);

$conn = new mysqli("myServer", "myUser", "myPassword", "Northwind");
$stmt = $conn->prepare("SELECT name FROM customers LIMIT ?");
$stmt->bind_param("s", $obj->limit);
$stmt->execute();
$result = $stmt->get_result();
$outp = $result->fetch_all(MYSQLI_ASSOC);

echo json_encode($outp);
?>
```

## JSON HTML

JSON pode ser muito facilmente traduzido em JavaScript.
JavaScript pode ser usado para produzir HTML em suas páginas web.

### Tabela HTML:
Faça uma tabela HTML com os dados recebidos como JSON:
```js
obj = { table: "customers", limit: 20 }
dbParam = JSON.stringify(obj)
xmlhttp = new XMLHttpRequest()
xmlhttp.onreadystatechange = function() {
    if (this.readyState == 4 && this.state == 200) {
        myObj = JSON.parse(this.responseText)
        txt += "<table border='1'>"
        for (x in myObj) {
            txt += "<tr><td>" + myObj[x].name + "</td></tr>"
        }
        txt += "</table>"
        document.getElementById("demo").innerHTML = txt
    }
}
xmlhttp.open("POST", "json_demo_db_post.php", true)
xmlhttp.setRequestHeader("Content-type", "application/x-www-form-urlencoded")
xmlhttp.send("x=" + dbParam)
// Retorna uma tabela de nomes com 20 itens.
```

### Tabela Dinâmica HTML:
Faça uma tabela HTML baseado no valor de um menu "drop down":
```html
<select id="myselect" onchange="change_myselect(this.value)">
    <option value="">Escolha uma opção:</option>
    <option value="customers">Customers</option>
    <option value="products">Products</option>
    <option value="suppliers">Suppliers</option>
</select>

<script>
function change_myselect(sel) {
    var obj, dbParam, xmlhttp, myObj, txt = ""
    obj = { table: sel, limit: 20 }
    dbParam = JSON.stringify(obj)
    xmlhttp = new XMLHttpRequest()
    xmlhttp.onreadystatechange = function() {
        if (this.readyState == 4 && this.state == 200) {
            myObj = JSON.parse(this.responseText)
            txt += "<table border='1'>"
            for (x in myObj) {
                txt += "<tr><td>" + myObj[x].name + "</td></tr>"
            }
            txt += "</table>"
            document.getElementById("demo").innerHTML = txt
        }
    }
    xmlhttp.open("POST", "json_demo_html_table.php", true)
    xmlhttp.setRequestHeader("Content-type", "application/x-www-form-urlencoded")
    xmlhttp.send("x=" + dbParam)
}
</script>         
<!-- Retornará uma lista em formato tabela segundo o valor escolhido no menu. -->
```
### Lista HTML Drop Down:

Fazendo uma lista HTML Drop Down com os dados recebidos como JSON:
```html
<p id="demo"></p>

<script>
var obj, dbParam, xmlhttp, myObj, x, txt = ""
obj = { table: "customers", limit: 20 }
dbParam = JSON.stringify(obj)
xmlhttp = new XMLHttpRequest()
xmlhttp.onreadystatechange = function() {
    if (this.readyState == 4 && this.status == 200) {
        myObj = JSON.parse(this.responseText)
        txt += "<select>"
        for (x in myObj) {
            txt += "<option>" + myObj[x].name
        }
        txt += "</select>
        document.getElementById("demo").innerHTML = txt
    }
}
xmlhttp.open("POST", "json_demo_html_table.php", true)
xmlhttp.setRequestHeader("Content-type", "application/x-www-form-urlencoded")
xmlhttp.send("x=" + dbParam
</script>   
```

## JSONP

JSONP é um método para envio de dados JSON sem se preocupar com questões entre domínios.

JSONP não usa o objeto "XMLHttpRequest"

Ao invés disso, JSONP usa a tag ```<script>```			

### Introdução ao JSONP
JSONP significa JSON com Preenchimento (padding). 

Solicitando um arquivo de um outro domínio pode causar problemas, devido à política de domínio-cruzado.

Solicitando um script externo de um outro domínio não conduz a esse problema.

JSONP usa essa vantagem, e solicita arquivos usando a tag "script" ao invés do objeto XMLHttpRequest:
```html
<script src="demo_json.php">
```
### O Arquivo Servidor:
O arquivo no servidor envelopa o resultado dentro de uma chamada de função:
```php
<?php
$myJSON = '{ "name":"John", "age":30, "city":"New York" }';

echo "myFunc(".$myJSON.");";
?>
```
O resultado retorna um chamado para uma função chamada "myFunc" com os dados JSON como um parâmetro

Tenha certeza que a função existe no lado cliente.

### A Função JavaScript:
A função chamada "myFunc" está localizada no lado cliente, e pronta para lidar com os dados JSON:
```js
function myFunc(myObj)
  document.getElementById("demo").innerHTML = myObj.name
}
// John
```
### Criando uma Tag Script Dinâmica:
O exemplo acima executará a função "myFunc" quando a página está carregando, baseado sobre onde você coloca a tag script, no qual não é muito satisfatório.
A tag script deveria apenas ser criada quando necessária:
```js
function clickButton() {
  var s = document.createElement("script")
  s.src = "demo_jsonp.php"
  document.body.appendChild(s)
}
function myFunc(myObj) {
  document.getElementById("demo").innerHTML = myObj.name
}
```

### Reultado JSONP Dinâmico:

Os exemplos anteriores são ainda bastante estáticos.
Faça o exemplo dinâmico pelo envio de JSON para o arquivo php, e faça o arquivo php retornar um objeto JSON com base nas informações que obtém.
```php
<?php
header("Content-Type: application/json; charset=UTF-8");
$obj = json_decode($_GET["x"], false);

$conn = new mysqli("MyServer", "myUser", "myPassword", "Northwind");
$result = $conn->query("SELECT name FROM ".$obj->table." LIMIT ".$obj->$limit);
$outp = array();
$outp = $result->fetch_all(MYSQLI_ASSOC);

echo "myFunc(".json_encode($outp).")";
?>
```

Arquivo PHP explicado:
1. Converte a requisição em um objeto, usando a função PHP "json_decode()".
2. Acessa a database, e preenche um vetor com os dados solicitados.
3. Adiciona o vetor a um objeto.
4. Converte o vetor em JSON usando a função "json_encode()".
5. Envelopa "myFunc()" ao redor do objeto de retorno.

Exemplo JavaScript, no qual a função "myFunc" será chamada do arquivo php:
```js
function clickButton() {
  var obj, s
  obj = { table: "products", limit: 10 }
  s = document.createElement("script")
  s.src = "json_demo_db.php?x=" + JSON.stringify(obj)
  document.body.appendChild(s)
}
function myFunc(myObj) {
  var x, txt = ""
  for (x in myObj) {
    txt += myObj[x].name + "<br>"
  }
  document.getElementById("demo").innerHTML = txt
}
```

### Função Callback:
Quando você não possui controle sobre o arquivo do servidor, como obter o arquivo do servidor para chamar a função correta?
Às vezes o servidor oferece uma função callback como um parâmetro:
```js
function clickButton() {
  var s = document.createElement("script")
  s.src = "jsonp_demo_db.php?callback=myDisplayFunction"
  document.body.appendChild(s)
}

function myDisplayFunction(myObj) {
  document.getElementById("demo").innerHTML = myObj.name
}
// John
```

## Introdução a Web API:

Uma Web API é um sonho para programadores:
1. Ela pode extender a funcionalidade do navegador;
2. Ela pode simplificar bastante funções complexas;
3. Ela pode prover uma sintaxe fácil para códigos complexos.

### O Que É Uma Web API?
API significa Application Programming Interface. Uma Web API é uma interface de programação de aplicativo para a Web.

Uma API  de Navegador pode extender suas funcionalidades, enquanto que uma API de Servidor extende as funcionalidades de servidores web.

### APIs de Navegador:
Tods os navegadores possuem um conjunto de APIs embutidas para suportar operações complexas, e ajudar ao acesso de dados.

Por exemplo, a API de Geolocalização pode retornar as coordenadas de onde o navegador está localizado:
```js
var x = document.getElementById("demo")

function getLocation() {
    if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition(showPosition)
    } else {
        x.innerHTML = "Geolocation is not supported by this browser."
    }
}

function showPosition(position) {
    x.innerHTML = "Latitude: " + position.coords.latitude + 
    "<br>Longitude: " + position.coords.longitude
}
```

### APIs de Terceiros:
APIs de Terceiros não são construídos em seu navegador.

Para usar essas APIs você terá que baixar o código da Web.

Exemplos:
1. Youtube API - Permite exibir vídeos na página web.
2. Twitter API - Permite exibir Tweets na página web.
3. Facebook API  - permite exibir informações de Facebook na página. etc.

## API de Histórico da Web: 

A API de Histórico Web provê métodos fáceis para acessar o obejto "windows.history".

O objeto window.history contém as URLs visitadas pelo usuário.

### Método de Histórico "back()":
O método "back()" carrega a URL anterior na lista window.history. É o mesmo que clica na "seta de retorno" em seu navegador.
```html
<button onclick="myFunction()">Go Back</button>

<script>
function myFunction() {
  window.history.back()
}
</script>
```

### Método de Histórico "go()":
O método "go()" carrega uma URL específica da lista do histórico:
```html
<button onclick="myFunction()">Go Back 2 Pages</button>

<script>
function myFunction() {
  window.history.go(-2)
}
</script>
```

### Propriedades de Objetos de Histórico:

* length =>	Retorna o número de URLs na lista de histórico.

### Métodos de Objeto de Histórico:

| | |
|---|---|
back()	|	Carrega a URL anterior na lista de histórico;
forward()	|	Carrega a URL posterior na lista de histórico;
go()	|	Carrega uma URL específica da lista de histórico.

## API de Armazenamento Web:

A API de Armazenamento Web é uma sintaxe simples para armazenar e recuperar dados no navegador. É bastante fácil de usar:
```js
localStorage.setItem("name", "John Doe")
document.getElementById("demo").innerHTML = 
localStorage.getIttem("name")
// "John Doe"
```

### Objeto "localStorage":	
O objeto "localStorage" provê acesso ao armazenamento local para uma página web em particular. Ele permite você armazenar, ler, adicionar, modificar, e deletar itens de dados para aquele domínio.


Os dados são armazenados sem data de expiração, e não serão deletados quando o navegador é fechado.

Os dados ficarão disponíveis por dias, semanas e anos.

### O Método "setItem()":
O método "localStorage.setItem()" armazena um item de dado em um armazenamento.

Ele recebe um nome e um valor como parâmetros:
```js
localStorage.setItem("name", "John Doe")
```

### O Método "getItem()"
O método "localStorage.getItem()" recupera um item de dado a partir do armazenamento. Ele recebe um nome como parâmetro:
```js
localStorage.getItem("name")
```

### O Objeto "sessionStorage"
O objeto "sessionStorage" é idêntico ao objeto localStorage. A diferença é que o objeto "sessionStorage" armazena dados por uma sessão.

Os dados é deletado quando o navegador é fechado. 
```js
sessionStorage.setItem("name","John Doe")
document.getElementById("demo").innerHTML =
sessionStorage.getItem("name")
// "John Doe"
```
**Atenção: O objeto "sessionStorage" também utiliza da mesma forma os métodos getItem() e setItem().**

### Métodos e Propriedades do Objeto de Armazenamento:

| | |
|---|---|
key(n)		|	Retorna o nome do nth chave no armazenamento.
length		|	Retorna o número de itens de dados armazenados.
getItem(nome)	|	Retorna o valor do nome da chave específica.
setItem(nome, valor)	|	Adiciona aquela chave ao armazenamento, ou atualiza aquele valor de chave se ele já existe.
removeItem(nome)	|	Remove aquela chave do armazenamento.
clear()		|	Esvazia todas as chaves do armazenamento.

## WEB WORKERS API

Um web worker é um script de JS executando no fundo, sem afetar a performance da página.

### O Que É Um Web Worker?
Quando executando scripts em uma página HTML, a página não responde até que o script seja finalizado.

Um web worker é um JavaScript que executa nos fundos, independentemente de outros scripts, sem afetar a performance da página. Você pode continuar a fazer o que desejar: clicar, selecionar coisas, etc., enquanto o web worker executa.

### Exemplo de Web Worker:
O exemplo abaixo cria um web worker simples que conta números ao fundo:
```html
<p>Count numbers: <output id="result"></output></p>
<button onclick="startWorker()">Start Worker</button>
<button onclick="stopWorker()">Stop Worker</button>

<script>
var w

function startWorker() {
    if (typeof(Worker) !== "undefined") {
        if (typeof(w) == "undefined") {
            w = new Worker("demo_worker.js")
        }
        w.onmessage = function(event) {
            document.getElementById("result").innerHTML = event.data
        }
    } else {
        document.getElementById("result").innerHTML = "Sorry, your browser does not support Web Workers..."
    }
}

function stopWorker() {
    w.terminate()
    w = undefined
}	
```

**Atenção: Note que primeiro foi preciso verificar se o navegador possui a API de Web Worker. Navegadores como IE9 ou versões anteriores não possuem. Para verificar faça:**
```js
if (typeof(Worker) !== "undefined") {
    / Sim! Há suporte para Web Worker
    / Bloco de código
} else {
    / Desculpe! Não há suporte para Web Worker
}
```

### Criando um Arquivo Web Worker:
Agora criaremos nosso web worker em um JavaScript externo. Aqui criaremos um script que conta. O script é armazenado no arquivo "demo_workers.js":
```js
var i = 0

function timedCount() {
    i++
    postMessage(i)
    setTimeout("timedCount()",500)
}

timedCount()
```
A importante importante do código acima é o método "postMessage()" - no qual é suado para postar uma mensagem de volta à página HTML.

**Atenção: Normalmente web workers não são usados para tais scripts simples, mas por mais tarefas que exigem mais CPU.**

### Criando um Objeto Web Worker:
Agora que nós temos o arquivo web worker, precisamos chama-lo de uma página HTML.

As linhas a seguir verificam se o worker já existe. Se não, ele cria um novo objeto web worker e executa 
```js
if (type(w) == "undefined") {
    w = new Worker("demo_workers.js")
}
```
Então podemos enviar e receber messagens do web worker. Adicione um evento listener "onmessage" para o web worker:
```js
w.onmessage = function(event){
    document.getElementById("result").innerHTML = event.data
}
```
Quando o web worker posta uma messagem, o código dentro do evento listener é executado. Os dados do web worker são armazenados em event.data.

**Atenção: "event.data" é um método de eventos vinculado ao JQuery. É uma propriedade que contém os dados opcionais passados para um método de evento quando o manipulador atual em execução é vinculado.**

### Evento onmessage:
O evento "onmessage" ocorre quando uma messagem é recebida através de uma fonte de evento.
```js
var source = new EventSource("demo_sse.php")
source.onmessage = function(event) {
    document.getElementById("myDIV").innerHTML += event.data + "<br>"
}
```

O objeto de evento para o evento "onmessage" suporta as seguintes propriedades:
* data - Contém a messagem atual
* origin - A URL do documento que invocou o evento
* lastEventId - o identificador da última messagem vista no fluxo de evento.

### Encerre um Web Worker:
Quando um objeto web worker é criado, ele continuará a "ouvir" as mensagens (mesmo depois que o script externo seja finalizado) até que ele seja encerrado.
Para encerrar um web worker, e liberar os recursos do navegador/computador, use o método "terminate()":
```js
w.terminate()
```

### Reutilize o Web Worker:
Se você define a variável worker como "undefined" logo após ela tenha sido encerrada, você poderá reutilizar o código:
```js
w = undefined
```

### Web Worker e o DOM:

Estando os Web Workers em arquivos externos, eles não terão acesso aos seguintes objetos JavaScript:
* O objeto window
* O objeto document
* O objeto parent.

Portanto, direcione com códigos na página HTML para que o evento ocorra utilizando como evento o script externo.

## FETCH API em JAVASCRIPT:

A interface Fetch API permite ao navegador web realizar requisições HTTP aos servidores web.

Se você usa o objeto XMLHttpRequest, Fetch API pode fazer o mesmo em uma maneira mais simples.

### Um Exemplo de Fetch API:
O exemplo abaixo busca um arquivo e exibe o conteúdo:
```js
let file = "fetch_info.txt"

fetch(file)
.then(x => x.test())
.then(y => document.getElementById("demo").innerHTML = y)
```
Já que o Fetch API é baseado em async e await, o exemplo acima pode ser melhor entendido dessa forma:
```js
getText("fetch_info.txt")
async function getText(file) {
  let x = await fetch(file)
  let y = await x.text()
  document.getElementById("demo").innerHTML = y
}
```
**Atenção: "text()" não aceita qualquer argumento e pode ser usado para documentos XML e HTML. Resulta em uma string contendo o texto combinado de todos os elementos correspondentes.**

Ou ainda melhor: Use nomes inteligíveis ao invés de x e y:
```js
getText("fetch_info.txt")
async function getText(file) {
  let myObject = await fetch(file)
  let myText = await myObject.text()
  document.getElementById("demo").innerHTML = myText
}
```

## API de Geolocalização Web:

A HTML Geolocation API é usado para receber a posição geográfica de um usuário.

Porém, já que isso compromete a privacidade, a posição não está disponível a menos que o usuário aprove.

**Atenção: Geolocalização é mais acurada para dispositivos com GPS, como smartphones.**

**Atenção: A partir do Chrome 50, o API apenas funcionará sob contextos seguros, como HTTPS. Se seu site é hospedado em uma origem insegura (tais como HTTP), a requisição para receber a localização do usuário não funcionará.**

### Usando o Geolocation API:
O método "getCurrentPosition()" é usado para retornar a posição do usuário. 

O exemplo abaixo retorna a latitude e longitude da posição do usuário:
```js
var x = document.getElementById("demo")
function getLocation() {
    if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition(showPosition) 
    } else {
        x.innerHTML = "Geolocation is not supported by this browser."
    }
}

function showPosition(position) {
    x.innerHTML = "Latitude: " + position.coords.latitude +
    "<br>Longitude: " + position.coords.longitude
}
```

Exemplo explicado:
1. Verifique se Geolocalização é suportada;
2. Se sim, execute o método "getCurrentPosition()". Se não, exibe uma mensagem ao usuário.
3. Se o método "getCurrentPosition()" obtém sucesso, ele retorna um objeto de coordenada para a função especificada no parâmetro (showPosition)
4. A função showPosition() retorna a Latitude e Longitude.

O exemplo acima é um script de geolocalização bastante básico, sem manejamento de erros.

### Lidando com Erros e Rejeições:
O segundo parâmetro do método "getCurrentPosition()" é usado para lidar com erros. Ele especifica uma função para executar se há falhas em receber a localização do usuário:
```js
function showError(error) {
    switch(error.code) {
        case error.PERMISSION_DENIED:
            x.innerHTML = "User denied the request for Geolocation."
            break
        case error.POSITION_UNAVAILABLE:
            x.innerHTML = "Location information is unavailable."
            break
        case error.TIMEOUT:
            x.innerHTML = "The request to get user location timed out."
            break
        case error.UNKNOWN_ERROR:
            x.innerHTML = "An unknown error occurred."
            break
    }
}
```

### Exibindo o Resultado em um Mapa:
Para exibir o resultado em um mapa, você precisa acessar um serviço de mapas, como o Google Maps.

No exemplo abaixo, a latitude e longitude retornadas são usadas para mostrar a localização no Google Maps (usando uma imagem estática).
```js
function showPosition(position) {
    var latlon = position.coords.latitude + "," + position.coords.longitude
    
    var img_url = "https://maps.googleapis.com/maps/api/staticmap?center="+latlon+"&zoom=14&size=400x300&sensor=false&key=YOUR_KEY"

    document.getElementById("mapholder").innerHTML = "<img src=' " 
    +img_url+"'>"
}
```

### Informação de uma Localização Específica:

Essa página tem demonstrado como mostrar uma posição de usuário em um mapa.

Geolocalização é também bastante útil para informações de localização específica, como:
- Informações locais atualizadas.
- Mostrando Pontos de Interesse próximos ao usuário.
- Navegação passo-a-passo (GPS)

### O Método getCurrentPosition() - Retorno de dado:
O método "getCurrentPosition()" retorna um objeto se houver sucesso. As propriedades "latitude", "longitude" e "accuracy" sempre serão retornadas. As outras propriedades são retornadas se disponíveis:

| | |
|---|---|
coords.latitude	|	Latitude em número decimal
coords.longitude	|	Longitude em número decimal
coords.accuracy	|	A precisão da posição.
coords.altitude	|	A altura em metros acima do nível médio do mar.
coords.altitudeAccuracy	|	A precisão da altura.
coords.heading	|	Valor em graus no sentido horário a partir do Norte.
coords.speed	|	A velocidade em metros por segundo
timestamp		|	A data/tempo da resposta.

### Objeto Geolocation - Outros Métodos Interessantes:

O objeto Geolocation também tem outros métodos interessantes:

* watchPosition() - Retorna a posição atual do usuário e continua a retornar a posição atualizada enquanto o usuário se move (como o GPS em um carro)
* clearWatch() - Para o método "watchPosition()".

O exemplo abaixo mostra o método "watchPosition()". Você precisa de um dispositivo GPS preciso para testar isso (como smartphones):
```js
<script>
var x = document.getElementById("demo")
function getLocation() {
    if (navigator.geolocation) {
        navigator.geolocation.watchPosition(showPosition) 
    } else {
        x.innerHTML = "Geolocation is not supported by this browser."
    }
}
function showPosition(position) {
    x.innerHTML = "Latitude: " + position.coords.latitude +
    "<br>Longitude: " + position.coords.longitude
}
</script>
```

## JAVASCRIPT / JQUERY DOM SELECTORS:

jQuery foi criado em 2006 por John Resig. Ele foi desenhado para lidar com Imcompatibilidades de Navegadores e para simplificar a Manipulação de HTML DOM, Event Handiling, Animações e Ajax.

Por mais de 10 anos, jQuery tem sido a biblioteca JavaScript mais popular no mundo.

No entanto, após a Versão 5 do JavaScript (2009), a maioria das utilidades jQuery podem ser resolvidas com poucas linhas de JavaScript padrão:

### Encontrando Elementos HTML pelo Id:

jQuery:
```js
var myElement = $("#id01")
```
JavaScript:
```js
var myElement = document.getElementById("id01")
```

### Encontrando Elementos HTML pelo Nome da Tag:
Retorna todos os elementos ```<p>```:

jQuery:
```js
var myElements = $("p")
```

JavaScript:
```js
var myElements = document.getElementsByTagName("p")
```

### Encontrando Elementos HTML pelo Nome da Classe:
Retorna todos os elemenos com class="intro"

jQuery:
```js
var myElements = $(".intro")
```
JavaScript:
```js
var myElements = document.getElementsByClassName("intro")
```

### Encontrando Elementos HTML por Seletores CSS:
Retorna uma lista de todos elementos ```<p>``` com class="intro"

jQuery:
```js
var myElements = $("p.intro")
```
JavaScript:
```js
var myElements = document.querySelectorAll("p.intro")
```

## JAVASCRIPT / JQUERY ELEMENTOS HTML:

### Definindo um Conteúdo de Texto:
Defina um texto interno de um elemento HTML:

jQuery:
```js
myElement.text("Hello World!")
```
JavaScript:
```js
myElement.textContent = "Hello World!"
```
### Obtendo um Conteúdo de Texto:
Obtenha o texto interno de um elemento HTML:

jQuery:
```js
var myText = myElement.text()
```
JavaScript:
```js
var myText = myElement.textContent || myElement.innerText
```
### Defina um Conteúdo HTML:

jQuery:
```js
var myElement.html("<p>Hello World</p>")
```
JavaScript:
```js
var myElement.innerHTML = "<p>Hello World</p>"
```
### Obtenha Conteúdo HTML:

jQuery:
```js
var content = myElement.html()
```
JavaScript:
```js
var content = myElement.innerHTML
```

## JQUERY CSS:

### Escondendo Elementos HTML:

jQuery:
```js
myElement.hide()
```
JavaScript:
```js 
myElement.style.display = "none"
```
### Mostrando Elementos HTML:

jQuery:
```js
myElement.show()
```
JavaScript:
```js
myElement.style.display = ""
```
**Atenção: Esse método permite que o elemento selecionado seja mostrando enquanto que o resto seja escondido.**

### Estilizando Elementos HTML:

jQuery:
```js
myElement.css("font-size","35px")
```
JavaScript:
```js
myElement.style.fontSize = "35px"
```

## JQUERY DOM HTML:

### Removendo Elementos:

jQuery:
```js
$("#id").remove()
```
JavaScript:
```js
element.parentNode.removeChild(element)
```
### Receba Elementos Pais:

jQuery:
```js
var myParent = myElement.parent()
```
JavaScript:
```js
var myParent = myElement,parentNode
```