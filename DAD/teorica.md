# Desenvolvimento de Aplicações Distribuídas

## Teórica

### 21/01/2021

**Em relação ao Node.js qual das seguintes afirmações é verdadeira?**

- [x] O Node.js é um servidor "single-threaded"
- [ ] O Node.js está otimizado para operações que envolvem muitos cálculos (CPU intensive operations)
- [ ] O Node.js suporta transações
- [ ] O Node.js utiliza um modelo de programação orientado a objetos

**A biblioteca "Vue Router" inclui o "router-link". O que é o "router-link"?**

- [ ] É o objecto que permite ligar o componente Vue Router à aplicação que utiliza a framework Vue.js
- [ ] É o componente incluido no Vue Router que é responsável por desenhar os componentes associados às rotas internas da aplicação
- [ ] É a propriedade do componente Vue Router que permite configurar as rotas internas da aplicação
- [x] É o componente incluido no Vue Router que é responsável por gerar uma hiperligação que irá referenciar uma rota interna da aplicação

**Em relação à secção `props` das opções de configuração de um componente Vue.js, qual das seguintes afirmações é verdadeira?**

- [ ] As propriedades da secção "props" são diretamente x acessíveis aos componentes "filhos" (componentes utilizados no template do "pai")
- [ ] O valor das propriedades da secção "props" são mantidas automaticamente no gestor de estado global (Vuex ou similar)
- [ ] As propriedades definidas na secção "props" despoletam eventos automaticamente para que possam ser acedidas pelos componentes "filhos" (componentes utilizados no template do "pai")
- [x] As propriedades da secção "props" são acessíveis no template que utiliza o componente (template do componente pai)

**Qual das seguintes secções de código de um template da Framework Vue.js, permite criar um conjunto de parágrafos?**

- [ ] `<v-for="a in arrayDados" ><p>{{ a }}</p></v-for>`
- [ ] `<p v-for.create(10)="a">{{ a }}</p>`
- [x] `<p v-for="(a, b) in arrayDados">{{ a }} {{ b }}</p>`
- [ ] `<p v-for.create="a in arrayDados">{{ a }}</p>`

**Qual das seguintes secções de código de um template da Framework Vue.js é válida?**

- [ ] `<input v-model.required="age">`
- [x] `<input v-model.lazy="age">`
- [ ] `<input v-model={{ age }}>`
- [ ] `<input v-model(required)="age">`

**Em relação aos WebSockets, qual das seguintes afirmações é verdadeira?**

- [ ] Os WebSockets estabelecem um canal de comunicação seguro e encriptado entre o cliente e o servidor
- [ ] Um servidor de WebSockets é mais escalável (consegue suportar mais clientes) que um servidor HTTP
- [ ] Os WebSockets modificam o protocolo HTTP, reduzindo a latência da mesmo
- [x] Para iniciar a comunicação com Websockets, o cliente começa por enviar um "handshake" ao servidor através de um pedido HTTP

**Qual dos seguintes itens *não* é uma diretiva da Framework Vue.js?**

- [x] v-set
- [ ] v-on
- [ ] v-for
- [ ] v-model

**Se um componente Vue.js desenha uma linha de uma tabela (elemento `<tr>`) e é representado pelo elemento `<linha>`, como é que deverá ser utilizado num template?**

- [ ] `<table><tr><linha></linha></tr><tr><<linha></linha></tr></table>`
- [x] `<table><tr is=linha></tr><tr is=linha></tr></table>`
- [ ] `<table><linha></linha><linha></linha></table>`
- [ ] `<table><linha is:table:row></linha><linha is:table:row></linha></table>`

**Considerando a utilização da biblioteca "Socket.io" no servidor, e que a variável "io" refere-se ao servidor de WebSockets e a variável "socket" refere-se ao socket que liga o servidor ao cliente C1, indique qual o código para enviar a mensagem "msg" com o objeto (obj) para o cliente C1.**

- [ ] `io.sockets.to('C1').emit('msg', obj)`
- [ ] `socket.emit('C1', 'msg', obj)`
- [x] `socket.emit('msg', obj)`
- [ ] `io.emit('C1', 'msg', obj)`

**Qual das seguintes secções de código permite registar um componente Vue.js com o nome "Component" e associá-lo à tag "abc"?**

- [ ] `Vue.Component(Register('abc'))`
- [ ] `Component.Register('abc')`
- [ ] `new Vue(abc, Component)`
- [x] `new Vue({ el: '#app', component: { 'abc': Component} })`

**Para que serve a diretiva `v-on` da Framework Vue.js?**

- [ ] Para mostrar ou esconder elementos HTML consoante a ocorrência de eventos
- [ ] Para declarar quais os elementos HTML que ficam ligados ao modelo de dados
- [x] Para definir qual o código que responde a um evento
- [ ] Para ativar ou desativar elementos HTML no template

**Qual dos seguintes itens *não* é uma diretiva da Framework Vue.js?**

- [ ] v-show
- [x] v-repeat
- [ ] v-for
- [ ] v-bind

**Na arquitetura REST, o método DELETE deverá ser utilizado:**

- [ ] Para atualizar dados
- [ ] Para consultar dados
- [ ] Para inserir dados
- [x] Para remover dados

**A Framework Vue.js suporta "two-way data-binding". O que é o "two-way data-binding"?**

- [ ] É um mecanismo que permite ao Vue.js conectar-se, de forma transparente, a qualquer tipo de base de dados, usando 2 formas de acesso distinto: acesso síncrono ou acesso assíncrono
- [x] É uma técnica que permite sincronizar as fontes de dados do código com a sua representação no desenho, de forma a que as alterações nas fontes de dados refletem- se no desenho, e vice-versa
- [ ] É um mecanismo que permite ao Vue.js conectar-se, de forma transparente, a bases de dados relacionais e não- relacionais
- [ ] É uma técnica que permite sincronizar as fontes de dados do código com a sua representação no desenho, usando 2 formas de acesso distinto: acesso síncrono ou acesso assíncrono

**A biblioteca "Vuex" permite fazer a gestão de estado nas aplicações Vue.js. Qual a forma mais correta para alterar o estado de uma Vuex "store"?**

- [x] Fazendo o commit de uma mutação ("mutation")
- [ ] Invocando um dos métodos da Vuex Store: "create", "update" ou "delete"
- [ ] Fazendo o commit de um "setter"
- [ ] Invocando o método setState() relativo ao estado que se pretende alterar. Por exemplo, se o nome do estado é "user", deverá ser invocado o método setUser()

**Qual dos seguintes itens é uma restrição arquitetural (architectural constraint) do estilo arquitetural REST?**

- [ ] Transporte de dados em JSON (JSON data transportation)
- [ ] Sistema em Camadas (Layered System)
- [ ] Serviços Transacionais (Transactionals Services)
- [ ] Comunicações Bidirecionais (Bidirectional Communications)

### 21/10/2021

**Considerando o seguinte código JavaScript:**

```js
var x = function (p1, p2, p3) {
  return "x=" + p1 + p2 + p3
}(2, 3)
```

**Qual o valor da variável x ?**

- [ ] 5
- [ ] "x=23undefined"
- [ ] undefined
- [ ] x é uma função

**Qual dos seguintes items é um objeto, biblioteca ou framework que permite estabelecer comunicação HTTP com o servidor.**

- [ ] XMLHttpRequest
- [ ] CSS
- [ ] PHPHttp
- [ ] JSON

**Quem é o responsável pela execução de código Javascript?**

- [ ] O JVM (Java Virtual Machine)
- [ ] O servidor Web
- [ ] O Javascript Engine
- [ ] O cliente Web (Browser)

**Depois de executada a seguinte secção de código ECMAScript 6, qual o valor da variável `x`?**

```js
let a = [1, 2, 3, 4]
let x = 0
a.forEach(v => { x += v })
```

- [ ] Nenhumas das outras opções corresponde ao valor de x
- [ ] [1, 3, 6, 10]
- [ ] x é uma função
- [ ] 10

**No contexto do desenvolvimento de aplicações Web, para além do Document Object Model (DOM) existem 2 novos conceitos, o Virtual DOM e o Shadow DOM. Quais das seguintes afirmações sobre Virtual DOM e/ou Shadow DOM é verdadeira?**

- [ ] Ambas melhoram o desempenho das páginas, mas utilizam diferentes abordagens para o fazer. O Virtual DOM utiliza a virtualização do DOM e o Shadow DOM utiliza memória Shadow.
- [ ] A Shadow DOM permite criar efeitos de transparências e sombras. A Virtual DOM utiliza uma máquina virtual para melhorar o encapsulamento e isolamento das páginas
- [ ] Shadow DOM é uma API que está incluída nos browsers mais recentes e o Virtual DOM é uma técnica utilizada por algumas frameworks Javascript
- [ ] O Virtual DOM faz parte do motor de execução virtual do browser (Virtual Browser Engine) e o Shadow DOM é uma técnica utilizada pelas frameworks Javascript que replica o Virtual DOM em browsers que não suportam o Virtual Browser Engine

**Qual dos seguintes itens *não* é uma função do Document Object Model (DOM)?**

- [ ] getElementByld
- [ ] getElementsByTagName
- [ ] getElementByQuerySelector
- [ ] getElementsByName

**Considerando que existe uma API REST com o endpoint `http://api.com/dados/x` que devolve a string `X` e demora *3 segundos*, e o endpoint `http://api.com/dados/y` que devolve a string `Y` e demora *1 segundo*, e considerando o seguinte código JavaScript (que usa a biblioteca Axios):**

```js
let endpointX = 'http://api.com/dados/x'
let endpointY = 'http://api.com/dados/y'
axios.get(endpointX)
  .then(r => {
    console.log(r.data)
    axios.get(endpointY)
  })
  .then(r => {
    console.log(r.data)
  })
console.log("END")
```

**Quanto tempo demora a execução e o que é escrito na consola?**

- [ ] Demora 4 segundos e escreve na consola:\
END\
X\
Y
- [ ] É instantâneo e escreve na consola:\
END
- [ ] Demora 3 segundos e escreve na consola:\
END\
X\
... Mensagem de erro ...
- [ ] Demora 3 segundos e escreve na consola:\
END\
X\
Y

**Considerando o seguinte código JavaScript:**

```js
var a = ""
if (a + "")
  console.log("A")
else
  console.log("B")
```

**O que é escrito na consola?**

- [ ] Não escreve nada na consola
- [ ] B
- [ ] A
- [ ] Escreve uma mensagem de erro na consola

**Supondo que a variável "a" tem o valor de 18. Qual das seguintes secções de código (ECMAScript6) atribui à variável "str" o valor de: "Nota do aluno é 18"?**

- [ ] let str = 'Nota do aluno é $a'
- [ ] let str = "Nota do aluno é $a"
- [ ] let str = \`Nota do aluno é ${a}\`
- [ ] let str = 'Nota do aluno é ' . a

**O ECMA Script 6 introduz 2 novas estruturas de dados, o `Set` e o `Map`. Qual das seguintes afirmações sobre estas estruturas é verdadeira:**

- [ ] Ambas permitem manter conjuntos de dados de vários tipos (exemplo: string, números, objetos, etc...)
- [ ] O Map permite manter um conjunto de pares chave+valor
- [ ] O Set permite manter um conjunto de dados únicos
- [ ] Todas as restantes afirmações são verdadeiras

**Qual o resultado da expressão JavaScript:**

`1 == "1" ? false : true`

- [ ] true
- [ ] A expressão é inválida
- [ ] undefined
- [ ] false

### 14/01/2022

**Tendo em conta o seguinte código (ECMAScript 6):**

```js
let a = "8"
console.log(`a= ${a * 2}` + a + a * 2 + "${a+a}")
```

**O que é escrito na consola?**

- [x] `a= 16816${a+a}`
- [ ] Não escreve nada na consola porque o código é inválido
- [ ] `a= 16244016`
- [ ] `a= 1681688`

**Qual dos seguintes items *não* é um dos princípios orientadores para garantir uma interface uniforme no estilo arquitetural REST?**

- [ ] Mensagens auto-descritivas (self-descriptive messages)
- [ ] Manipulação dos recursos através das suas representações (manipulation of resources through representations)
- [x] Autenticação baseada em JWT Tokens (JWT token based authentication)
- [ ] Identificação de recursos (Identification of resources)

**Utilizando a framework Vue.js, qual o método mais correto para um componente "filho" passar dados para um componente "pai"? Nota: O componente "pai" utiliza no seu template o componente "filho".**

- [x] O filho deverá despoletar (emitir) um evento
- [ ] Através de uma propriedade definida na secção "props" do filho
- [ ] O pai deverá despoletar (emitir) um evento
- [ ] Através de uma propriedade definida na secção "props" do pai

**Considerando a utilização da biblioteca "Socket.io" no servidor, e que a variável `io` refere-se ao servidor de WebSockets e a variável `socket` refere-se ao socket que liga o servidor ao cliente C1, indique qual o código do servidor para enviar a mensagem "msg" com o objeto (obj) para todos os clientes que estão no canal (room/channel) com o nome "canal".**

- [x] `io.to('canal').emit('msg', obj)`
- [ ] `socket.emit('canal', 'msg', obj)`
- [ ] `socket.to('canal').emit ('msg', obj)`
- [ ] `io.emit('canal', 'msg', obj)`

**Os componentes Vue.js podem incluir propriedades nas secções `data` e `props`. Qual a diferença entre as duas abordagens?**

- [ ] Ao contrário das propriedades da secção "data", as propriedades da secção "props" não são acessíveis no template que utiliza o componente (template do componente pai)
- [ ] Ao contrário das propriedades da secção "props", as propriedades da secção "data" não são acessíveis no template do próprio componente
- [ ] Ao contrário das propriedades da secção "data", as propriedades da secção "props" não são acessíveis no template do próprio componente
- [x] Ao contrário das propriedades da secção "props", as propriedades da secção "data" não são acessíveis no template que utiliza o componente (template do componente pai)

**Qual das seguintes secções de código de um template da Framework Vue.js é válida?**

- [x] `<input v-model.trim="msg">`
- [ ] `<input v-model.required="msg">`
- [ ] `<input v-model:required="msg">`
- [ ] `<input v-model={{ msg }}>`

**Considerando o seguinte código JavaScript:**

```js
(function (p1) {
  console.log(p1 * 2)
})
p1(3)
```

**O que é escrito na consola?**

- [ ] 3*2
- [x] É escrita uma mensagem de erro na consola
- [ ] p1*2
- [ ] 6

**Aplicando os princípios de uma arquitetura REST, qual das seguintes secções de código no cliente é a mais correcta para, utilizando uma API REST, criar um novo registo da entidade livro?**

- [x] `axios.post('http://minha.api.com/livros', { novoLivro })`
- [ ] `axios.get('http://minha.api.com/livro/create', { novoLivro })`
- [ ] `axios.post('http://minha.api.com/livros/create', { novoLivro })`
- [ ] `axios.put('http://minha.api.com/livro', { novoLivro })`

**Considerando que existe uma API REST com o endpoint `http://api.com/dados/x` que devolve o número 3 e o endpoint `http://api.com/dados/y` que devolve o número 5, e considerando o seguinte código JavaScript (que usa a biblioteca Axios):**

```js
let endpointX = 'http://api.com/dados/x'
let endpointY = 'http://api.com/dados/y'
var f1 = async function () {
  var res1 = axios.get(endpointX)
  console.log(res1.data)
  var res2 = await axios.get(endpointY)
  console.log(res2.data)
  return res1.data + res2.data
}
console.log("A")
f1()
console.log("END")
```

**O que é escrito na consola?**

- [ ] A\
undefined\
END\
5
- [ ] A\
3\
5\
END
- [ ] A\
END\
3\
5
- [ ] Escreve uma mensagem de erro na consola

**Qual dos seguintes itens representa dados JSON válidos?**

- [ ] `[2, "a", 3, {"b": 12: "c": 1: "d": 4}]`
- [ ] `{"a": 12, "b": true, "c": [2, "e", 3, {"f", 4}]}`
- [ ] `{"a": [2, "b", 3, ["c": [1, 2, 4]], ["d"]]}`
- [x] `["a", [2, "b", 3, {"c": [1, 2, 4, {"d": "d"}]}, ["d"]]]`

**Qual das seguintes secções de código é a mais correta para aceder (ler) ao estado, ou parte do estado, de uma Vuex store?**

- [ ] `let x = this.$store.x`
- [x] `let x = this.$store.state.x`
- [ ] `let x = this.$vuex.store.x`
- [ ] `let x = this.$state.x`

### 24/10/2022

**Qual dos seguintes items é um objeto, biblioteca ou framework que permite estabelecer comunicação HTTP com o servidor.**

- [ ] HTML API
- [ ] JSON
- [ ] DOM AJAX
- [x] Axios

**Em relação às funções "callback" do JavaScript, qual das seguintes afirmações é verdadeira:**

- [ ] As funções "callback" permitem aumentar a funcionalidade dos tipos primitivos
- [ ] As funções "callback" são funções que podem ser invocadas pelos protótipos dos objetos
- [ ] As funções "callback" são funções privadas dos objetos
- [x] As funções "callback" são passadas por parâmetro para outras funções, que as podem invocar

**Tendo em conta o seguinte código (ECMAScript 6):**

```js
let a = 6
console.log(`a= ${a * 2 + a} + ${a}` + `${a}` + a * 2 + '${a}')
```

**O que é escrito na consola?**

- [ ] `a= ${6 * 2 + 6} + ${6} 612${6}`
- [ ] Não escreve nada na consola porque o código é inválido
- [ ] `a= 24 186`
- [x] `a= 18 + 6 612${a}`

**O Cross-Origin Resource Sharing (CORS) permite:**

- [x] Ignorar a política de segurança "same-origin policy" dos browsers
- [ ] Distribuir recursos (ex: base de dados; ficheiros) por vários domínios
- [ ] Partilhar recursos (ex: ficheiros) entre vários browsers
- [ ] Encriptar o protocolo HTTP para melhorar a segurança da comunicação

**Qual dos seguintes itens é uma função do Document Object Model (DOM)?**

- [ ] getElementByClass
- [ ] getElementsByType
- [x] getElementsByClassName
- [ ] getElementByIndex

**Alguns browsers incluem a API Shadow DOM. Para que serve esta API?**

- [x] Facilita o desenvolvimento de componentes melhorando o encapsulamento e isolamento dos mesmos
- [ ] Permite ao servidor fazer o rendering das páginas e enviar o resultado para a Shadow DOM no cliente (browser), melhorando desta forma o desempenho das páginas e a integração entre o cliente e o servidor
- [ ] Permite melhorar o desempenho do processo de rendering de toda a página em simultâneo
- [ ] Permite melhorar o desempenho do processo de rendering dos componentes

**Depois de executada a seguinte secção de código ECMAScript 6, qual o valor da variável *x*?**

```js
let a = 3
let x = (a => a ✶ 2) ((a => a * 2) (2, 3))
```

- [ ] 8
- [ ] x é inválido porque o código tem um ou mais erros
- [ ] x é uma função
- [ ] 6

**Depois de executada a seguinte secção de código ECMAScript 6, qual o valor da variável *x*?**

```js
let a = 3
let x = (b => (a => a * 2) (a, b))
```

- [ ] x é inválido porque o código tem um ou mais erros
- [ ] undefined
- [x] x é uma função
- [ ] 6

**Depois de executada a seguinte secção de código ECMAScript 6, qual o valor da variável *x*?**

```js
let a = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
let x = a.filter(v => v % 3 == 0)
```

- [ ] x é inválido porque o código tem um ou mais erros
- [ ] [1, 2, 4, 5, 7, 8, 10]
- [ ] x é uma função
- [x] [3, 6, 9]

**Depois de executada a seguinte secção de código ECMAScript 6, qual o valor da variável *x*?**

```js
let a = 3
let x = a => 2 * a(2)
```

- [ ] x é inválido porque o código tem um ou mais erros
- [ ] 6
- [ ] x é uma função
- [ ] 12

**Considerando que existe uma API REST com o endpoint `http://api.com/dados/x` que devolve a string `X` e demora *3 segundos*, e o endpoint `http://api.com/dados/y` que devolve a string `Y` e demora *1 segundo*, e considerando o seguinte código JavaScript (que usa a biblioteca Axios):**

```js
let endpointX = 'http://api.com/dados/x'
let endpointY = 'http://api.com/dados/y'
axios.get(endpointX)
  .then(r => {
    console.log(r.data)
  })
axios.get(endpointY)
  .then(r => {
    console.log(r.data)
  })
console.log("END")
```

**Quanto tempo demora a execução e o que é escrito na consola?**

- [ ] Demora 4 segundos e escreve na consola:\
END\
Y\
X
- [ ] Demora 4 segundos e escreve na consola:\
END\
X\
Y
- [x] Demora 3 segundos e escreve na consola:\
END\
Y\
X
- [ ] Demora 3 segundos e escreve na consola:\
END\
X\
Y

**Qual das seguintes opções não é um tipo de dados nativo do JavaScript?**

- [ ] String
- [ ] Number
- [x] Char
- [ ] Undefined

**Considerando o seguinte código JavaScript:**

```js
var a = 9
if ("a" % 2)
  console.log("A")
else
  console.log("B")
```

**O que é escrito na consola?**

- [x] B
- [ ] Escreve uma mensagem de erro na consola
- [ ] Não escreve nada na consola
- [ ] A

**Considerando o seguinte código JavaScript:**

```js
var x = function (p1, p2, p3) {
  return p1 + p2 + p3
}("2", 3)
```

**Qual o valor da variável x ?**

- [ ] x não tem valor porque a expressão é inválida
- [x] "23undefined"
- [ ] undefined
- [ ] 5

**Qual o resultado da expressão JavaScript:**

`"a" + 2`

- [ ] A expressão é inválida
- [ ] "a"
- [ ] 2
- [x] "a2"

**Qual dos seguintes itens representa dados JSON válidos?**

- [ ] `["a", [2, "b", 3, {"c": [1, 2, 4, true, "d"]}, [false]]]`
- [ ] `[2, "a", 3, {"b": 12, "c": true}]`
- [x] Todos os outros itens representam dados JSON válidos
- [ ] `{"a": 12, "b": true, "c": [2, "e", 3, {"f": 4}]}`

**Que tipo de relacionamento existe entre os clientes web (browsers) e os servidores web?**

- [ ] Relação N:M
- [ ] Relação 1:1
- [ ] Relação 1:N
- [ ] Relação N:1

**Qual dos seguintes itens não é uma vantagem das aplicações Web tradicionais (modelo multi-página) quando comparadas com as aplicações com modelo SPA (Single Page Application)?**

- [x] As aplicações são mais seguras
- [ ] É um modelo mais adequado à utilização de ferramentas de análise (analytics tools)
- [ ] O carregamento inicial das páginas é mais rápido
- [ ] É um modelo mais adequado à utilização de técnicas de otimização de motores de pesquisa (SEO - Search Engine Optimization)

### 06/11/2023

**A biblioteca "Vue Router" pode ser configurada para utilizar o "modo historia" ("History Mode"). O que é que este modo permite?**

- [x] Permite que o URL das rotas internas da aplicação tenham um formato similar às rotas do servidor (exemplo: `http://site.com/users/123`)
- [ ] Permite que a aplicação Vue.js mantenha um log com o histórico de todas as rotas internas utilizadas
- [ ] Permite enviar para o servidor informação sobre o histórico de utilização da aplicação
- [ ] Permite que a aplicação Vue.js mantenha um log com o histórico de todas os componentes utilizados

**Qual das seguintes secções de código de um template da Framework Vue.js, permite criar um conjunto de parágrafos?**

- [ ] `<p v-for="a in arrayDados">{{ a }}</p>`
- [ ] `<p v-create="newParagraph">{{ newParagraph }}</p>`
- [ ] `<v-for="a in arrayDados"><p>{{ a }}</p></v-for>`
- [ ] `<p v-repeat="i in arrayDados">{{ arrayDados[i] }}</p>`

**Qual das seguintes secções de código de um template da Framework Vue.js é válida?**

- [ ] `<input v-model.required="age">`
- [x] `<input v-model.lazy="age">`
- [ ] `<input v-model={{ age }}>`
- [ ] `<input v-model (required)="age">`

**Em relação aos WebSockets, qual das seguintes afirmações é verdadeira?**

- [ ] Os WebSockets estabelecem um canal de comunicação seguro e encriptado entre o cliente e o servidor
- [ ] Um servidor de WebSockets é mais escalável (consegue suportar mais clientes) que um servidor HTTP
- [ ] Os WebSockets modificam o protocolo HTTP, reduzindo a latência da mesmo
- [x] Para iniciar a comunicação com Websockets, o cliente começa por enviar um "handshake" ao servidor através de um pedido HTTP

**Qual das seguintes secções de código permite registar um componente Vue.js com o nome "Component" e associá-lo à tag "abc"?**

- [ ] `Vue.Component (Register('abc'))`
- [ ] `Component.Register('abc')`
- [ ] `new Vue (abc, Component)`
- [x] `new Vue({ el: '#app', component: { 'abc': Component} })`

**Em relação às funções "callback" do JavaScript, qual das seguintes afirmações é verdadeira:**

- [ ] As funções "callback" permitem manter o estado das variáveis locais da função que a contém, enquanto a própria função "closure" persistir
- [x] As funções "callback" são passadas por parâmetro para outras funções, que as podem invocar
- [ ] As funções "callback" são funções que permitem a uma página voltar atrás, ou seja, repetem a execução do código anterior
- [ ] As funções "callback" são as funções que estão incluídas dentro de outras funções

### 08/11/2023

**Na Framework Vue.js, o desenho ("rendering") das páginas Web ...**

- [x] ... é definido através de templates declarativos
- [ ] ... é definido pela API "Virtual DOM Engine" dos browsers
- [ ] ... é feito pelo motor de vistas (view engine) "Blade"
- [ ] ... é feito pelo motor de vistas "Vue Engine"

### 09/11/2023

**Qual o resultado da expressão JavaScript:**

`"false" == false`

- [ ] true
- [ ] undefined
- [ ] A expressão é inválida
- [x] false

**Supondo que um componente Vue.js inclui a propriedade "a" definida da seguinte forma:**

```js
<script setup>
  // ...
  const x = defineProps(['a'])
  // ...
</script>
```

**Qual o código, dentro da secção `<script setup>`, que irá escrever na consola o valor da propriedade "a"?**

- [ ] console.log(a.value)
- [ ] console.log(a)
- [ ] console.log(getProperty('a'))
- [x] console.log(x.a)

**Os componentes Vue.js podem usar funções ou "computed properties" para calcular valores que serão usados no componente, tal como se pode observar no seguinte exemplo de código:**

```js
<script setup>
. . .
const x1 = () => {
  return 10 ✶ some.value
}
const x2 = computed(() => {
  return 10 * some.value
})
</script>
```

**Qual das seguintes afirmações que compara funções (exemplo = x1) com "computed properties" (exemplo = x2) é verdadeira?**

- [x] Todas as afirmações são verdadeiras
- [ ] Quando uma computed property é usada num template, a sintaxe é similar a uma variável reativa - exemplo: {{ x2 }}. Quando uma função é usada num template, a sintaxe é a mesma que usada por qualquer função - é necessário invocar a função através de paréntesis - exemplo: {{ x1() }}
- [ ] As computed properties não podem ter argumentos (parâmetros). As funções podem ter argumentos (parâmetros).
- [ ] O valor devolvido pelas computed properties fica em cache, o que significa que a função associada a uma computed property que está a ser usada num template só é invocada quando alguma das variáveis reactivas incluídas no corpo dessa função é alterada (no exemplo, se a computed property "x2" for usada no template, a função associada à mesma só será executada se o valor de "some.value" for alterado). Já as funções que são usadas no template, são invocadas sempre que uma variável reativa usada no template é alterada, mesmo que não esteja diretamente relacionada com a função (no exemplo, se a função "x1" for usada num template, esta será executada sempre que o valor de qualquer variável reativa do template for alterado)

**Tendo em conta o seguinte código (ECMAScript 6):**

```js
let a = 4
console.log(`a= ${a * 2} + ${a} + {a} ` + a + a * 2 + '${a}')
```

**O que é escrito na consola?**

- [ ] `a= 124 484`
- [ ] Não escreve nada na consola porque o código é inválido
- [x] `a= 8 + 4 + {a} 48${a}`
- [ ] `a= 12{a} 12{a}`

**Considerando o seguinte código JavaScript:**

```js
var a = "-11"
if (a + 11)
  console.log("A")
else
  console.log("B")
```

**O que é escrito na consola?**

- [ ] Escreve uma mensagem de erro na consola
- [x] A
- [ ] Não escreve nada na consola
- [ ] B

**Considerando o seguinte código JavaScript:**

```js
(p1 => {
  console.log(p1*2)
})(7)
```

**O que é escrito na consola?**

- [ ] Não escreve nada na consola
- [ ] Escreve uma mensagem de erro na consola
- [x] 14
- [ ] 7*2

**O JavaScript é uma linguagem de programação...**

- [ ] Orientada a eventos
- [ ] Funcional
- [ ] Orientada a Objetos
- [x] Multiparadigma

**A framework Vue.js 3 suporta 2 APIs: a "Options API" e a "Composition API". Qual das seguintes afirmações relativas às 2 APIs é verdadeira?**

- [ ] Ao contrário do que acontece com a "Composition API", os componentes definidos com a "Option API" podem incluir propriedades "computed"
- [ ] Todas as restantes afirmações são verdadeiras
- [ ] Ao contrário do que acontece com a "Option API", os componentes definidos com a "Composition API" podem incluir dados (variáveis) reactivos
- [x] Ao contrário do que acontece com a "Composition API", os componentes especificados com a "Option API" têm acesso à variável "this", que se refere à instância do componente e é preenchida em runtime pela framework Vue.js

**Em relação às diretivas *v-show* e *v-if* da Framework Vue.js, qual das afirmações é verdadeira?**

- [ ] A diretiva v-show necessita da diretiva v-show-end para fechar o bloco que se pretende mostrar ou esconder
- [ ] A diretiva v-show só funciona em conjunto com a diretiva v-if
- [ ] Para mostrar ou esconder elementos HTML, a diretiva v-if aplica ou remove estilos a esses elementos
- [x] Ambas as diretivas permitem mostrar ou esconder elementos HTML, mas só a diretiva v-if é que constrói e destrói elementos para os mostrar e esconder

**Qual dos seguintes itens é uma vantagem das aplicações com modelo híbrido quando comparadas com aplicações com modelo SPA (Single Page Application)?**

- [ ] O carregamento inicial dos conteúdos é mais rápido
- [x] É um modelo mais adequado à utilização de técnicas de otimização de motores de pesquisa (SEO - Search Engine Optimization)
- [ ] O Permite o funcionamento offline das aplicações já carregadas
- [ ] A navegação entre conteúdos é mais fluída

**No contexto do desenvolvimento de aplicações Web, para além do Document Object Model (DOM) existem 2 novos conceitos, o Virtual DOM e o Shadow DOM. Quais as semelhanças e/ou diferenças entre os 2?**

- [ ] Ambos aumentam as capacidades do DOM, mas utilizam diferentes abordagens para o fazer. O Virtual DOM utiliza a virtualização do DOM e o Shadow DOM utiliza memória Shadow.
- [x] O Shadow DOM tem a ver com o encapsulamento e isolamento dos componentes e o Virtual DOM tem a ver com o desempenho do processo de rendering do conteúdo das páginas
- [ ] O Virtual DOM faz parte do motor de execução virtual do browser (Virtual Browser Engine) e o Shadow DOM é utilizado pelas frameworks Javascript para optimizar o desempenho das mesmas
- [ ] Ambos aumentam as capacidades do DOM por forma a suportar novos tipos de conteúdos em HTML

**Qual das seguintes secções de código de um template da Framework Vue.js, permite criar um conjunto de parágrafos?**

- [ ] `<v-for="a in arrayDados"><p>{{ a }}</p></v-for>`
- [ ] `<p v-repeat="i in arrayDados">{{ arrayDados[i] }}</p>`
- [ ] `<p><v-for="i in arrayDados">{{ arrayDados[i] }}</v-for></p>`
- [x] `<p v-for="(a, b) in arrayDados">{{ a }}</p>`

**O que é necessário para que um componente Vue.js suporte a diretiva *v-model*?**

- [x] Incluir a propriedade (props) com o nome "modelValue" e emitir o evento com o nome "update:modelValue"
- [ ] Acrescentar uma propriedade com o nome "props" e valor = ['model']
- [ ] Incluir a função "v-model" no código do componente
- [ ] Nenhuma das outras opções permite que um componente suporte a diretiva v-model

**Qual das seguintes secções de código permite a um componente Vue.js emitir evento/s corretamente?**

- [ ]

  ```js
  <script setup>
  import { ref } from 'vue'
  const emit = defineEvent('x')
  const m = () => {
    emit(x)
  }
  </script>
  ```

- [ ]

  ```js
  <script setup>
  import { ref } from 'vue'
  const emit = defineEmits('x')
  const m = () => {
    emit('x')
  }
  </script>
  ```

- [x]

  ```js
  <script setup>
  import { ref } from 'vue'
  const a = defineEmits (['x'])
  const m = () => {
    a('x')
  }
  </script>
  ```

- [ ]

  ```js
  <script setup>
  import { ref } from 'vue'
  const emit = defineEmits(['a', 'b', 'c'])
  const m = () => {
    emit('a', 'b', 'c')
    emit(a, b, c)
    emit(a, 'b', 'c')
  }
  </script>
  ```

**Em relação ao sistema de reatividade da framework Vue.js, qual das seguintes afirmações é verdadeira?**

- [ ] Todas as restantes afirmações são verdadeiras
- [ ] Os dados reativos que suportam one-way binding são definidos pela função reactive() e os dados reativos que suportam two-way binding são definidos pela função ref()
- [ ] Os dados reativos só podem ser representados no template através da diretiva v-model
- [x] Os dados reativos definidos pela função ref() são acedidos pela propriedade value.\
  Exemplo de código:

  ```js
  const a = ref(0)
  a.value++
  ```

**A framework "Vue.js" pode utilizar a ferramenta "Vite.js". Qual das seguintes afirmações sobre o "Vite.js" é verdadeira?**

- [ ] Durante o desenvolvimento de uma aplicação Vue.js, o Vite.js compila os módulos JavaScript em código binário para correr num servidor web local
- [x] Durante o desenvolvimento de uma aplicação Vue.js, o Vite.js utiliza a funcionalidade de Hot Module Replacement (HMR) para garantir que a aplicação é atualizada automaticamente e o mais rapidamente possível, sempre que o programador alterar código nos ficheiros JavaScript.
- [ ] Durante o desenvolvimento de uma aplicação Vue.js, o Vite.js cria um servidor web local para acesso aos endpoints das APIs.
- [ ] No processo de publicação da aplicação Vue.js, o Vite.js compila os módulos JavaScript em código binário para correr num servidor web

**Depois de executada a seguinte secção de código ECMAScript 6, qual o valor da variável *x*?**

```js
let a = 3
let x = (a => (a => a ✶ 2)(a))(2, 3)
```

- [ ] x é uma função
- [ ] x é inválido porque o código tem um ou mais erros
- [x] 4
- [ ] 6

### 10/11/2023

**Tendo em conta o seguinte código (ECMAScript 6):**

```js
let a = 6
console.log(`a= ${a * 2 + a} + ${a} ` + `${a}` + a * 2 + '${a}')
```

**O que é escrito na consola?**

- [ ] `a= ${6 * 2 + 6} + ${6} 612${6}`
- [ ] Não escreve nada na consola porque o código é inválido
- [ ] `a= 24 186`
- [ ] `a= 18 + 6 612${a}`

**Depois de executada a seguinte secção de código ECMAScript 6, qual o valor da variável *x*?**

```js
let a = 3
let x = ((b) => (a => a * 2)) (2, 3)
```

- [ ] 4
- [x] x é uma função
- [ ] x é inválido porque o código tem um ou mais erros
- [ ] 6

**Qual das seguintes secções de código permite a um componente Vue.js emitir evento/s corretamente?**

- [x] Todas as secções de código emitem eventos corretamente.
- [ ]

  ```js
  <script setup>
  import { ref } from 'vue'
  const emit = defineEmits(['a', 'b', 'c'])
  const m = () => {
    emit('a', 'b', 'c')
    emit('b', 'a', 'c')
    emit('c', 'b', 'a')
  }
  </script>
  ```

- [ ]

  ```js
  <script setup>
  import { ref } from 'vue'
  const a = defineEmits(['x'])
  const m = () => {
    a('x')
  }
  </script>
  ```

- [ ]

  ```js
  <script setup>
  import { ref } from 'vue'
  const emit = defineEmits(['x'])
  const m = () => {
    emit('x')
  }
  </script>
  ```

**Considerando o seguinte código JavaScript:**

```js
var a = "2"
if (a - 2)
  console.log("A")
else
  console.log("B")
```

**O que é escrito na consola?**

- [ ] Escreve uma mensagem de erro na consola
- [x] B
- [ ] A
- [ ] Não escreve nada na consola

**Supondo que a variável "a" tem o valor de 8. Qual das seguintes secções de código (ECMAScript 6) escreve na consola:**

`Idade = 32`

- [ ] console.log(`Idade = {a * 2}` + 2 * a)
- [x] console.log(`Idade = ${a * 2 + a * 2}`)
- [ ] console.log("Idade = ${a * 4}")
- [ ] console.log('Idade = {a + 2 + a * 2}')

**Os componentes Vue.js podem usar funções ou "computed properties" para calcular valores que serão usados no componente, tal como se pode observar no seguinte exemplo de código:**

```js
<script setup>
. . .
const x1 = () => {
  return 10 ✶ some.value
}
const x2 = computed(() => {
  return 10 ✶ some.value
})
</script>
```

**Qual das seguintes afirmações que compara funções (exemplo = x1) com "computed properties" (exemplo = x2) é verdadeira?**

- [ ] As funções tem um desempenho ligeiramente superior às computed properties, porque estas últimas utilizam funções callback.
- [x] As computed properties não podem ter argumentos (parâmetros). As funções podem ter argumentos (parâmetros).
- [ ] As funções e as computed properties têm um comportamento e utilização similar. As computed properties são "alias" das funções para simplificar a utilização das mesmas nos templates.
- [ ] As computed properties tem um desempenho ligeiramente superior às funções, porque as computed properties são compiladas e as funções são interpretadas

**Qual dos seguintes itens é uma limitação das aplicações com modelo SPA (Single Page Application) quando comparadas com aplicações tradicionais (modelo multi-página)?**

- [ ] As aplicações SPA são mais inseguras
- [ ] Navegação entre diferentes conteúdos é mais lenta
- [ ] Não permite o funcionamento offline das aplicações já carregadas
- [x] O carregamento inicial dos conteúdos é mais lento

**Depois de executada a seguinte secção de código ECMAScript 6, qual o valor da variável *x*?**

```js
let a = 3
let x = ((b) => (a => a ✶ 2)(4))(2, 3)
```

- [ ] 6
- [x] 8
- [ ] x é uma função
- [ ] x é inválido porque o código tem um ou mais erros

**A framework Vue.js 3 suporta 2 APIs: a "Options API" e a "Composition API". Qual das seguintes afirmações relativas às 2 APIs é verdadeira?**

- [ ] Todas as restantes afirmações são verdadeiras
- [ ] Ao contrário do que acontece com a "Option API", os componentes definidos com a "Composition API" podem incluir dados (variáveis) reactivos
- [x] A "Composition API" permite especificar componentes através de um objecto com a função setup()
- [ ] A "Option API" permite especificar componentes através da secção de código `<script option>`

**Qual o resultado da expressão JavaScript:**

`"5" - 2`

- [ ] A expressão é inválida
- [ ] "5-2"
- [x] 3
- [ ] "52"

**Em relação ao sistema de reatividade da framework Vue.js, qual das seguintes afirmações é verdadeira?**

- [x] Nenhuma das restantes afirmações é verdadeira
- [ ] Os dados reativos que suportam one-way binding são definidos pela função reactive() e os dados reativos que suportam two-way binding são definidos pela função ref()
- [ ] Os dados reativos que suportam one-way binding são definidos pela função ref() e os dados reativos que suportam two-way binding são definidos pela função reactive()
- [ ] Enquanto os dados reativos definidos pela função reactive() podem ser de qualquer tipo, os dados reativos definidos pela função ref() só podem ser do tipo Object

**Em relação às diretivas *v-show* e *v-if* da Framework Vue.js, qual das afirmações é *falsa*?**

- [x] A diretiva v-show constrói ou destrói elementos HTML conforme necessário
- [ ] A diretiva v-show irá mostrar ou esconder elementos HTML conforme o valor de uma expressão booleana
- [ ] A diretiva v-if pode-se associar à diretiva v-else
- [ ] A diretiva v-if pode ser aplicada a elementos correspondentes a componentes Vue (exemplo: `<my-component>`)

**O JavaScript é uma linguagem de programação...**

- [ ] derivada do Java, mas apenas com as funcionalidades de "scripting"
- [ ] que permite converter aplicações Java em scripts para executar nos Browsers
- [x] Nenhuma das outras opções é válida
- [ ] derivada do Java, mas sem as suas características de programação orientada a objetos

**A framework "Vue.js" pode utilizar a ferramenta "Vite.js". Qual das seguintes afirmações sobre o "Vite.js" é verdadeira?**

- [x] Durante o desenvolvimento de uma aplicação Vue.js, o Vite.js cria um servidor web local que utiliza os módulos dos browsers para correr a aplicação.
- [ ] Durante o desenvolvimento de uma aplicação Vue.js, o Vite.js compila os módulos JavaScript em código binário para correr num servidor web local
- [ ] Durante o desenvolvimento de uma aplicação Vue.js, o Vite.js cria um servidor web local para acesso aos endpoints das APIs.
- [ ] No processo de publicação da aplicação Vue.js, o Vite.js compila os módulos JavaScript em código binário para correr num servidor web

**Considerando o seguinte código JavaScript:**

```js
((p1) => {
  console.log(p1 * 2)
})
p1(7)
```

**O que é escrito na consola?**

- [ ] 14
- [ ] undefined
- [ ] Não escreve nada na consola
- [x] É escrita uma mensagem de erro na consola

### 07/01/2024

**Na arquitetura REST, o método DELETE deverá ser utilizado:**

- [ ] Para atualizar dados
- [ ] Para consultar dados
- [ ] Para inserir dados
- [x] Para remover dados

**Considerando que existe uma API REST com o endpoint `http://api.com/dados` e que este devolve a string "A", e considerando o seguinte código JavaScript (que usa a biblioteca Axios):**

```js
axios.get('http://api.com/dados').then(function (response) {
  console.log(response.data)
})
console.log("B")
axios.get('http://api.com/dados').then(function (response) {
  console.log(response.data)
})
console.log("C")
```

**O que é escrito na consola?**

- [ ] undefined\
B\
undefined\
C
- [ ] B\
C\
A\
A
- [ ] B\
C
- [ ] Escreve uma mensagem de erro na consola

**Considerando que existe uma API REST com o endpoint `http://api.com/dados` e que este devolve a string "X", e considerando o seguinte código JavaScript (que usa a biblioteca Axios):**

```js
let endpoint = 'http://api.com/dados'
console.log("A")
axios.get(endpoint).then(function (response) {
  console.log(response.data)
  axios.get(endpoint).then(function (response) {
    console.log(response.data)
  })
  console.log("B")
})
console.log("C")
```

**O que é escrito na consola?**

- [ ] A\
C\
X\
B\
X
- [ ] A\
undefined\
undefined\
B
с
- [ ] A\
. . . Mensagem de erro . . .\
C
- [ ] A\
C\
B\
X\
X

**Qual dos seguintes itens *não* representa dados JSON válidos?**

- [ ] ["a", [2, "b", {"c": [1, {"d": "d", "e": "e"}]}, [{"f": ["f"]}]]]
- [ ] [2, "a", 3, {"b": 12, "c": 1, "d": 4}, false]
- [ ] ["a", [2, "b", 3, {"c": [1, 2, 4, {"d": "e": 3}]}, ["d": 2]]]
- [ ] ["a", [2, "b", 3, {"c": [1, 2, 4, {"d": "e"}]}, ["d", 2]]]

### 08/01/2024

**O que é o Cross-Origin Resource Sharing (CORS)?**

- [ ] É uma especificação W3C que permite comunicação entre domínios cruzados ("cross-domain")
- [ ] É um formato de dados alternativo ao JSON com melhorias na segurança
- [ ] É um formato de dados que permite partilhar recursos entre vários domínios
- [ ] É uma extensão ao protocolo HTTP que permite mais segurança na comunicação

**Qual das seguintes secções de código permite a um componente Vue.js emitir evento/s corretamente?**

- [ ]

  ```js
  <script setup>
  import { ref } from 'vue'
  const emit = defineEvent(['x'])
  const m = () => {
    emit('x')
  }
  </script>
  ```

- [x] Nenhuma das secções de código emite evento/s corretamente.
- [ ]

  ```js
  <script setup>
  import { ref } from 'vue'
  const emit = defineEmits(['a', 'b', 'c'])
  const m = () => {
    emit(['a', 'b', 'c'])
    emit(['a', 'b'])
    emit('a', 'b', 'c')
  }
  </script>
  ```

- [ ] Todas as secções de código emitem eventos corretamente.

**Na arquitetura REST, para criar um recurso no servidor deve ser utilizado o método HTTP:**

- [x] POST
- [ ] CREATE
- [ ] STORE
- [ ] PATCH

**Qual dos seguintes itens representa dados JSON válidos?**

- [x] ["a", [2, "b", {"c": [1, {"d": "d"}]}, [{"e": ["f", "g"]}]]]
- [ ] ["a", [2, "b", 3, {"c": [1, 2, 4, {"d": "e": 3}]}, ["d": 2]]]
- [ ] {"a", [2, "b", 3, true]}
- [ ] [2, "a", 3, {"b": 12: "c": 1: "d": 4}]

**Em relação aos WebSockets, qual das seguintes afirmações é *falsa*?**

- [ ] Os WebSockets incluem um protocolo de comunicação que poderá ser utilizado por diversas linguagens (Javascript, Java, C, etc)
- [ ] Para iniciar a comunicação com Websockets, o cliente começa por enviar um "handshake" ao servidor através de um pedido HTTP
- [ ] A API dos WebSockets é um standard W3C
- [x] Os WebSockets estabelecem um canal de comunicação seguro e encriptado entre o cliente e o servidor

**Considerando que o componente Vue "ContaBancaria" inclui a propriedade (prop) "saldo", qual a secção de código do template desse componente que apresenta o valor do saldo a vermelho, quando este é negativo? Nota: Considere que a classe CSS "negativo" define uma formatação com o texto a vermelho.**

- [ ] Saldo = `<span v-if=(saldo<0) {class='negativo'}>{{saldo}}</span>`
- [ ] Nenhuma das outras secções de código apresentam o valor do saldo a vermelho, quando o mesmo é negativo
- [x] Saldo = `<span :class="{negativo: saldo < 0}">{{saldo}}</span>`
- [ ] Saldo = `<span class="{{ saldo < 0 ? 'negativo' : '' }}">{{saldo}}</span>`

**Considerando que existe uma API REST com o endpoint `http://api.com/dados/x` que devolve o número 3 e demora 3 segundos, e o endpoint `http://api.com/dados/y` que devolve o número 5 e demora 1 segundo, e considerando o seguinte código JavaScript (que usa a biblioteca Axios):**

```js
let endpointX = 'http://api.com/dados/x'
let endpointY = 'http://api.com/dados/y'
let f1 = async function () {
  let a = axios.get(endpointX)
  let b = axios.get(endpointY)
  return (await a).data + (await b).data
}
var f2 = async function () {
  console.log("A")
  console.log(await f1())
}
console.log(f2())
console.log("END")
```

**Quanto tempo demora a execução do código e o que é escrito na consola?**

- [ ] Demora 3 segundos e escreve na consola:\
A\
Promise ...\
END\
8
- [ ] Escreve uma mensagem de erro na consola
- [ ] Demora 4 segundos e escreve na consola:\
END\
A
Promise ...\
8
- [ ] Demora 4 segundos e escreve na consola:\
Promise ...\
A\
END\
8

**Considerando o seguinte código JavaScript:**

```js
var f = function () {
  var i = 1
  return function () {
    console.log(i)
    i += 2
  }
}
f()
f()
f()
```

**O que é escrito na consola?**

- [x] Não escreve nada na consola
- [ ] 1\
1\
1
- [ ] A definição/código de uma função (repetida 3 vezes)
- [ ] 1\
3\
5

**Considerando a utilização da biblioteca "Socket.io" no servidor, e que a variável `io` refere-se ao servidor de WebSockets e a variável `socket` refere-se ao socket que liga o servidor ao cliente C1. Considerando que estão ligados 3 utilizadores ao servidor (C1, C2 e C3), indique qual o código para enviar a mensagem "msg" com o objeto (obj) para o cliente C3.**

- [ ] `socket('C3').emit('msg', obj)`
- [ ] `socket.emit('C3', 'msg', obj)`
- [x] Nenhuma das outras opções tem o código necessário para enviar uma mensagem para o cliente C3
- [ ] `io.socket_id('C3').emit('msg', obj)`

**Em relação às "promises" do JavaScript, qual das seguintes afirmações é verdadeira:**

- [ ] As "promises" são funções que prometem um conjunto de resultados, ou seja, que permitem especificar quais os resultados esperados na sua execução
- [x] As "promises" permitem encadear operações assíncronas
- [ ] As "promises" são funções que não têm nome
- [ ] As "promises" são o equivalente do Javascript às interfaces de programação orientada a objetos

**Qual das seguintes funções converte dados nativos do JavaScript numa string com dados JSON?**

- [ ] Object.convertToJSON
- [ ] JSON.encode()
- [x] JSON.stringify()
- [ ] JSON.parse()

**Supondo que uma aplicação desenvolvida em Vue.js utiliza a biblioteca "Vue Router" para implementação de um sistema de rotas, e que inclui entre outras, uma rota com o nome "admin" e uma rota com o nome "login" (esta ultima irá apresentar o formulário de autenticação). Supondo também que inclui a biblioteca "authorization.js" com a função isAdmin() que devolve true ou false conforme o utilizador atual seja ou não administrador. Qual dos seguintes itens tem o código correto para garantir que apenas os utilizadores que são administradores poderão aceder à rota "admin".**

- [ ]

  ```js
  <script setup>
  . . .
  import {isAdmin} from "./libs/authorization.js"
  . . .
  const router = createRouter({
    . . .
    routes: [
    {
      name: 'admin',
    },
    . . .
  })

  router.guard((to, from, next) => {
    if ((to.name == 'admin') && (!isAdmin())) {
      abort()
    }
  })
  </script>
  ```

- [ ]

  ```js
  <script setup>
  . . .
  import {isAdmin} from "./libs/authorization.js"
  . . .
  const router = createRouter({
    . . .
    routes: [
      {
        name: 'admin',
        authorization: () => isAdmin()
        . . .
      },
      . . .
    ]
  })
  </script>
  ```

- [ ]

  ```js
  <script setup>
  . . .
  import {isAdmin} from "./libs/authorization.js"
  . . .
  const router = createRouter({
    . . .
    routes: [
      {
        name: 'admin',
        . . .
      },
      . . .
    ]
  })

  router.beforeEnter ((to, from, next) => {
    if ((to.name == 'admin') && (!isAdmin())) {
      unauthorize()
    }
  })
  </script>
  ```

- [x]

  ```js
  <script setup>
  . . .
  import {isAdmin} from "./libs/authorization.js"
  . . .
  const router = createRouter({
    . . .
    routes: [
      {
      name: 'admin',
      . . .
      },
      . . .
    ]
  })

  router.beforeEach((to, from, next) => {
    if ((to.name == 'admin') && (!isAdmin())) {
      next({ name: 'login' })
    } else {
      next()
    }
  })
  </script>
  ```

**Qual dos seguintes itens *não* é uma diretiva da Framework Vue.js?**

- [x] v-attr
- [ ] v-else
- [ ] v-show
- [ ] v-on

**Supondo que um componente Vue.js inclui o seguinte código JavaScript:**

```js
<script setup>
. . .
const someObject = createSomeObject(...)
provide('x', someObject)
. . .
</script>
```

**Para que serve o método `provide` no código anterior?**

- [x] Permite que todos os componentes descendentes deste (quer sejam descendentes diretos ou indiretos) tenham acesso ao objeto "someObject" através da função "inject"
- [ ] Permite fornecer o objeto "someObject" à propriedade (prop) "x", através da função "inject" do object "someObject"
- [ ] Permite criar um provider com o nome "x", para acesso ao object "someObject". Este provider permite injectar eventos, propriedades e métodos ao objeto "someObject" sem aceder ao código do referido objeto
- [ ] Permite injetar a propriedade "x" ao objeto "someObject"

**Considerando a utilização da biblioteca "Socket.io" no servidor, e que a variável `io` refere-se ao servidor de WebSockets e a variável `socket` refere-se ao socket que liga o servidor ao cliente C1, indique qual o código para enviar a mensagem "msg" com o objeto (obj) para todos os clientes ligados ao servidor.**

- [ ] `socket.emit('msg', obj)`
- [ ] `io.to('*').emit('msg', obj)`
- [x] `io.emit('msg', obj)`
- [ ] `socket.emit('*', 'msg', obj)`

**Considerando o seguinte código JavaScript:**

```js
var f = function () {
var i = 1
  return function () {
    console.log(i)
    i += 2
  }
}()
f()
f()
f()
```

**O que é escrito na consola?**

- [x] 1\
3\
5
- [ ] A definição/código de uma função (repetida 3 vezes)
- [ ] Não escreve nada na consola
- [ ] 1\
1\
1

**A biblioteca "Pinia" permite fazer a gestão de estado nas aplicações Vue.js, em que cada aplicação Vue.js pode conter vários "Pinia stores". Qual dos seguintes itens corresponde a elementos que os "Pinia stores" poderão ter?**

- [ ] State
- [x] Todos os outros itens correspondem a elementos que os "Pinia stores" poderão ter
- [ ] Actions
- [ ] Getters

**Considerando que existe uma API REST com o endpoint `http://api.com/dados/x` que devolve o número *3* e demora *3 segundos*, e o endpoint `http://api.com/dados/y`" que devolve o número *5* e demora *1 segundo*, e considerando o seguinte código JavaScript (que usa a biblioteca Axios):**

```js
let endpointX = 'http://api.com/dados/x'
let endpointY = 'http://api.com/dados/y'
var f1 = async function () {
  var res1 = await axios.get(endpointX)
  var res2 = await axios.get(endpointY)
  console.log(res1.data)
  console.log(res2.data)
  return res1.data + res2.data
}
var f2 = async function () {
  console.log("A")
  console.log(await f1())
}
console.log(f2())
console.log("END")
```

**Quanto tempo demora a execução do código e o que é escrito na consola?**

- [ ] Escreve uma mensagem de erro na consola
- [ ] Demora 4 segundos e escreve na consola:\
A\
3\
5\
8\
END
- [ ] Demora 3 segundos e escreve na consola:\
Promise . . .\
END\
A\
3\
5\
8
- [x] Demora 4 segundos e escreve na consola:\
A\
Promise . . .\
END\
3\
5\
8

**Considerando que existe uma API REST com o endpoint `http://api.com/dados/x` que devolve o número 3 e demora 3 segundos, e o endpoint `http://api.com/dados/y` que devolve o número 5 e demora 1 segundo, e considerando o seguinte código JavaScript (que usa a biblioteca Axios):**

```js
let endpointX = 'http://api.com/dados/x'
let endpointY 'http://api.com/dados/y'
let f1 = async function () {
  let a = axios.get(endpointX)
  let b = axios.get(endpointY)
  let r1 = (await a).data
  let r2 = (await b).data
  console.log(a)
  console.log(r1)
  return r1 + r2
}
var f2 = async function () {
  console.log("A")
  console.log(await f1())
}
f2()
console.log("END")
```

**Quanto tempo demora a execução do código e o que é escrito na consola?**

- [ ] Escreve uma mensagem de erro na consola
- [ ] Demora 4 segundos e escreve na consola:\
END\
Promise ...\
Promise ...\
3
- [x] Demora 3 segundos e escreve na consola:
A
END
Promise ...
3
8
- [ ] Demora 4 segundos e escreve na consola:
END
A
Promise ...
3
8

**Aplicando os princípios de uma arquitetura REST, qual das seguintes secções de código no cliente é a mais correcta para, utilizando uma API REST, alterar o título de uma entidade livro?**

**Nota1: Considere que cada entidade livro tem um ID, um título, uma descrição e um preço.**

**Nota2: Considere que a variável livro está previamente definida com este valor:**

```js
let livro= {
  ID: 3,
  titulo: 'Um livro qualquer',
  descricao: 'Descrição do livro',
  preco: 15.0
}
```

- [ ] `axios.patch('http://minha.api.com/livros/' + livro.id + '/patch', { livro })`
- [x] `axios.patch('http://minha.api.com/livros/' + livro.id, { 'titulo': livro.titulo })`
- [ ] `axios.put(http://minha.api.com/livro/' + livro.id, { livro })`
- [ ] `axios.post('http://minha.api.com/livros/update', { livro })`

### 09/01/2024

**Supondo que uma aplicação desenvolvida em Vue.js utiliza a biblioteca "Vue Router" para implementação de um sistema de rotas, e que inclui uma rota com o nome "Project" e que aceita o parâmetro "id". Um determinado componente dessa aplicação inclui a função f1() que tem como objectivo saltar para a rota referida, com o id = 12 (irá mostrar o projeto cujo id = 12).**

**Qual dos seguintes itens tem o código correto para o pretendido:**

- [x]

  ```js
  <script setup>
  . . .
  import { useRouter } from 'vue-router'
  const router = useRouter()
  . . .
  const f1() => {
    router.push({ name: 'Project', params: (id:12)})
  }
  . . .
  </script>
  ```

- [ ]

  ```js
  <script setup>
  . . .
  import { useRouter } from 'vue-router'
  const router = useRouter()
  . . .
  const f1 = () => {
    router.push('Project/12')
  }
  . . .
  </script>
  ```

- [ ]

  ```js
  <script setup>
  . . .
  import { useRouter } from 'vue-router'
  const router = useRouter()
  . . .
  const f1 = () => {
    router.goto('Project/12')
  }
  . . .
  </script>
  ```

- [ ]

  ```js
  <script setup>
  . . .
  import { useRouter } from 'vue-router'
  const router = useRouter()
  . . .
  const f1 = () => {
    router.navigate('Project', 12)
  }
  </script>
  ```

**Considerando que o componente Vue "ContaBancaria" inclui a propriedade (prop) "saldo", qual a secção de código do template desse componente que apresenta o valor do saldo a vermelho, quando este é negativo, e a verde caso contrário (saldo >=0)?**

**Nota: Considere que a classe CSS "negativo" define uma formatação com o texto a vermelho e a classe CSS "positivo" define uma formatação com o texto a verde.**

- [ ] Saldo - `<span v-if=(saldo<0) {class='negativo'} v-else {class='positive'}>{{saldo}}</span>`
- [x] Saldo - `<span :class="{negativo: saldo < 0, positivo: saldo >= 0}">{{saldo}}</span>`
- [ ] Todas as outras secções de código apresentam o valor do saldo a vermelho, quando o mesmo é negativo, e a verde quando o saldo é maior ou igual a zero
- [ ] Saldo - `<span class="{{ saldo < 0 ? 'negativo' : 'positivo' }}">{{saldo}}</span>`

**Qual dos seguintes itens não é uma diretiva da Framework Vue.js?**

- [ ] v-show
- [ ] v-model
- [ ] v-bind
- [x] v-emit

**A biblioteca "Pinia" permite fazer a gestão de estado nas aplicações Vue.js, em que cada aplicação Vue.js pode conter vários "Pinia stores". Qual dos seguintes itens corresponde a elementos que os "Pinia stores" poderão ter?**

- [x] Getters
- [ ] Synchronous Data
- [ ] Assynchronous Data
- [ ] Tables

**O ficheiro principal de uma aplicação feita em Vue.js inclui o seguinte código JavaScript:**

```js
. . .
const someObject = createSomeObject(...)
const app = createApp(App)
app.provide('x', someObject)
. . .
```

**Para que serve o método `provide` no código anterior?**

- [ ] Permite injetar a propriedade "x" ao objeto "someObject" através da função "inject" a colocar no objeto "someObject"
- [ ] Permite fornecer o objeto "someObject" ao componente "x", através da função "inject" do componente "x"
- [x] Permite que todos os componentes da aplicação tenham acesso ao objeto "someObject" através da função "inject".
- [ ] Permite criar um provider com o nome "x", para acesso ao object "someObject". Este provider permite injectar eventos, propriedades e métodos ao objeto "someObject" sem aceder ao código do referido objeto

**A biblioteca "Vue Router" pode ser configurada para utilizar o modo ("History Mode") "HTML5 mode". O que é que o modo "HTML5 mode" permite?**

- [x] Permite que o URL das rotas internas da aplicação tenham um formato similar às rotas do servidor (exemplo: `http://meusite.com/users/123`)
- [ ] Permite que a aplicação Vue.js mantenha um log com o histórico de todas os componentes utilizados
- [ ] Permite enviar para o servidor informação sobre o histórico de utilização do HTML na aplicação
- [ ] Permite que a aplicação Vue.js mantenha um log com o histórico de todas as rotas internas utilizadas

**Em relação aos WebSockets, qual das seguintes afirmações é verdadeira?**

- [x] Os WebSockets incluem um protocolo de comunicação que poderá ser utilizado por diversas linguagens (Javascript, Java, C#, etc.)
- [ ] Os WebSockets modificam o protocolo HTTP, optimizando o desempenho do mesmo
- [ ] Os WebSockets permitem a comunicação direta entre 2 ou mais clientes (browsers)
- [ ] Os WebSockets estabelecem um canal de comunicação seguro e encriptado entre o cliente e o servidor

**Qual das seguintes funções converte dados nativos do JavaScript numa string com dados JSON?**

- [ ] JSON.parse()
- [ ] JSON.decode()
- [x] JSON.stringify()
- [ ] JSON.encode()

**Na arquitetura REST, para obter um recurso do servidor deve ser utilizado o método HTTP:**

- [ ] INDEX
- [x] GET
- [ ] POST
- [ ] LOAD

**No contexto da Framework Vue.js, qual das seguintes secções de código não corresponde a um "Text Interpolation" válido?**

- [x] `<a href="{{ x }}">Some Url</a>`
- [ ] `<a href=http://www.a.com">{{ x+y }}</a>`
- [ ] `<a href=http://www.a.com">{{ functionA(x) }}</a>`
- [ ] `<a href=http://www.a.com">{{ x }}</a>`

**Considerando que existe uma API REST com o endpoint `http://api.com/dados` e que este devolve a string `X`, e considerando o seguinte código JavaScript (que usa a biblioteca Axios):**

```js
let endpoint = 'http://api.com/dados'
axios.get(endpoint).then(function (response) {
  console.log(response.data)
  console.log("A")
})
console.log("B")
```

**O que é escrito na consola?**

- [ ] A\
B\
X
- [x] B\
X\
A
- [ ] X\
A\
B
- [ ] undefined\
A\
B

**Considerando que o componente Vue "ContaBancaria" inclui a propriedade (prop) "saldo", qual a secção de código do template desse componente que apresenta o valor do saldo a vermelho, quando este é negativo?**

**Nota: Considere que a classe CSS "negativo" define uma formatação com o texto a vermelho.**

- [x] Saldo = `<span :class="{negativo: saldo < 0}">{{saldo}}</span>`
- [ ] Saldo = `<span class="{{ saldo < 0 ? 'negativo' : '' }}">{{saldo}}</span>`
- [ ] Saldo = `<span v-if="saldo<0" class='negativo' v-else="">{{saldo}}</span>`
- [ ] Todas as outras secções de código apresentam o valor do saldo a vermelho, quando o mesmo é negativo

**Considerando que existe uma API REST com o endpoint `http://api.com/dados/x` que devolve o número 3 e o endpoint `http://api.com/dados/y` que devolve o número 5, e considerando o seguinte código JavaScript (que usa a biblioteca Axios):**

```js
let endpointX = 'http://api.com/dados/x'
let endpointY = 'http://api.com/dados/y'
var f1 = async function () {
  var res1 = await axios.get(endpointX)
  console.log(res1.data)
  var res2 = await axios.get(endpointY)
  console.log(res2.data)
  return res1.data + res2.data
}
console.log("A")
f1()
console.log("END")
```

**O que é escrito na consola?**

- [ ] A\
3\
5\
8\
END
- [ ] Escreve uma mensagem de erro na consola
- [ ] A\
END\
3\
5
- [ ] A\
3\
5\
END

**A biblioteca "Vue Router" inclui o "router-view". O que é o "router-view"?**

- [ ] É o componente incluido no Vue Router que é responsável por gerar uma hiperligação que irá referenciar uma rota interna da aplicação
- [ ] É o objeto incluido no Vue Router que injecta dados da aplicação nas vistas internas do Vue.js
- [x] É o componente incluido no Vue Router que é responsável por desenhar os componentes associados às rotas internas da aplicação
- [ ] É a propriedade do componente Vue Router que permite configurar as rotas internas da aplicação

**Supondo que uma aplicação desenvolvida em Vue.js utiliza a biblioteca "Vue Router" para implementação de um sistema de rotas, e que inclui uma rota com o nome "Project" e que aceita o parâmetro "id". Um determinado componente dessa aplicação inclui a função f1() que tem como objectivo saltar para a rota referida, com o id = 12 (irá mostrar o projeto cujo id = 12).**

**Qual dos seguintes itens tem o código correto para o pretendido:**

- [x]

  ```js
  <script setup>
  . . .
  import { useRouter } from 'vue-router'
  const router = useRouter()
  . . .
  const f1 = () => {
    router.push({ name: 'Project', params: {id:12}})
  }
  . . .
  </script>
  ```

- [ ]

  ```js
  <script setup>
  . . .
  import { useRouter, route } from 'vue-router'
  const router = useRouter()
  . . .
  const f1 = () => {
    router.navigate(new route({ name: 'Project', params: {id:12}}))
  }
  . . .
  </script>
  ```

- [ ]

  ```js
  <script setup>
  . . .
  import { useRouter, route } from 'vue-router'
  const router = useRouter()
  . . .
  const f1 = () => {
    router.push(new route('Project', {id:12}))
  }
  . . .
  </script>
  ```

- [ ]

  ```js
  <script setup>
  . . .
  import { useRouter } from 'vue-router'
  const router = useRouter()
  . . .
  const f1 = () => {
    router.navigate({ name: 'Project', params: {id:12}})
  }
  </script>
  ```

**Supondo que um componente Vue.js inclui o seguinte código JavaScript:**

```js
<script setup>
. . .
const someObject = createSomeObject(...)
provide('x', someObject)
. . .
</script>
```

**Para que serve o método `provide` no código anterior?**

- [x] Permite que todos os componentes descendentes deste (quer sejam descendentes diretos ou indiretos) tenham acesso ao objeto "someObject" através da função "inject"
- [ ] Permite associar o provider "someObject" à propriedade "x", sendo que o provider permite acesso a APIs, WebSockets ou outros recursos externos
- [ ] Permite criar um provider com o nome "x", para acesso ao object "someObject". Este provider permite injectar eventos, propriedades e métodos ao objeto "someObject" sem aceder ao código do referido objeto
- [ ] Permite injetar a propriedade "x" ao objeto "someObject" através da função "inject" a colocar no objeto "someObject"

**Na arquitetura REST, qual dos seguintes métodos HTTP pode ser utilizado para alterar ou atualizar um recurso do servidor?**

- [ ] POST
- [x] PUT
- [ ] UPDATE
- [ ] DIFF

**Em relação aos WebSockets, qual das seguintes afirmações é verdadeira?**

- [ ] Os WebSockets permitem a comunicação direta entre 2 ou mais clientes (browsers)
- [ ] Os WebSockets têm como objetivo tornar os serviços Web RESTful mais rápidos
- [ ] Os WebSockets modificam o protocolo HTTP, optimizando o desempenho do mesmo
- [x] Os WebSockets estabelecem um canal de comunicação entre o cliente e o servidor, através de uma ligação TCP

**Considerando o seguinte código JavaScript:**

```js
var f = function () {
  var i = 1
  return function (x) {
    i += x
    console.log(i)
  }
}()
f(1)
f(2)
```

**O que é escrito na consola?**

- [ ] 2\
3
- [ ] Não escreve nada na consola
- [ ] A definição/código de uma função (repetida 2 vezes)
- [x] 2\
4

**Considerando que existe uma API REST com o endpoint `http://api.com/dados/x` que devolve o número 3 e o endpoint `http://api.com/dados/y` que devolve o número 5, e considerando o seguinte código JavaScript (que usa a biblioteca Axios):**

```js
let endpointX = 'http://api.com/dados/x'
let endpointY = 'http://api.com/dados/y'
var f1 = async function () {
  var res1 = await axios.get(endpointX)
  var res2 = await axios.get(endpointY)
  console.log(res1.data + res2.data)
}
console.log("A")
f1()
console.log("END")
```

**O que é escrito na consola?**

- [ ] A\
END
- [ ] Escreve uma mensagem de erro na consola
- [ ] A\
8\
END
- [x] A\
END\
8

**Considerando que existe uma API REST com o endpoint `http://api.com/dados` e que este devolve a string `A`, e considerando o seguinte código JavaScript (que usa a biblioteca Axios):**

```js
axios.get('http://api.com/dados').then(function (response) {
  console.log(response.data)
})
console.log("B")
```

**O que é escrito na consola?**

- [ ] A\
B
- [ ] B
- [ ] undefined\
B
- [x] B\
A

**A biblioteca "Vue Router" pode ser configurada para utilizar diferentes modos ("History Modes"). Qual dos seguintes itens é um "History Mode" suportado pela biblioteca "Vue Router"?**

- [x] Todos os outros itens são history modes suportados pelo Vue Router
- [ ] Hash mode
- [ ] HTML 5 mode
- [ ] Memory mode

**Considerando o seguinte código JavaScript:**

```js
var f = function () {
  var i = 3
  console.log(i)
  return function () {
    console.log(i)
    i *= 2
  }
}()
f()
f()
f()
```

**O que é escrito na consola?**

- [ ] A definição/código de uma função (repetida 3 vezes)
- [ ] 3\
3\
3
- [x] 3\
3\
6\
12
- [ ] 3\
6\
12

**Considerando que o componente Vue "ContaBancaria" inclui a propriedade (prop) "saldo", qual a secção de código do template desse componente que apresenta o valor do saldo a vermelho, quando este é negativo?**

**Nota: Considere que a classe CSS "negativo" define uma formatação com o texto a vermelho.**

- [x] Nenhuma das outras secções de código apresentam o valor do saldo a vermelho, quando o mesmo é negativo
- [ ] Saldo = `<span {{ saldo < 0 ? 'class=negativo' : '' }}">{{saldo}}</span>`
- [ ] Saldo = `<span v-if=(saldo<0) {class='negativo'}>{{saldo}}</span>`
- [ ] Saldo = `<span class="{{ saldo < 0 ? 'negativo' : '' }}">{{saldo}}</span>`

**Considerando que existe uma API REST com o endpoint `http://api.com/dados` e que este devolve a string `X`, e considerando o seguinte código JavaScript (que usa a biblioteca Axios):**

```js
let endpoint = 'http://api.com/dados'
axios.get(endpoint).then(function (response) {
  console.log(response.data)
  console.log("A")
  axios.get(endpoint).then(function (response) {
    console.log(response.data)
    console.log("B")
  })
})
console.log("D")
```

**O que é escrito na consola?**

- [x] D\
X\
A\
X\
B
- [ ] undefined
A\
undefined\
B\
D
- [ ] A
B\
D\
X\
X
- [ ] D
A\
B\
X\
X

**Considerando a utilização da biblioteca "Socket.io" no servidor, e que a variável `io` refere-se ao servidor de WebSockets e a variável `socket` refere-se ao socket que liga o servidor ao cliente C1, indique qual o código do servidor para enviar a mensagem "msg" com o objeto (obj) para todos os clientes que estão no canal (room/channel) com o nome "canal".**

- [ ] `io.emit('canal', 'msg', obj)`
- [ ] `socket.emit('canal', 'msg', obj)`
- [ ] `socket.to('canal').emit ('msg', obj)`
- [x] `io.in('canal').emit('msg', obj)`

**Qual das seguintes funções converte uma string com dados JSON em dados nativos do JavaScript?**

- [ ] `String.ConvertFromJSON`
- [ ] `JSON.toNative()`
- [x] `JSON.parse()`
- [ ] `JSON.decode()`

**Qual dos seguintes itens representa dados JSON válidos?**

- [ ] `[2, "a", 3, {"b": 12: 20}]`
- [ ] `{"a", [2, "b", 3, true]}`
- [x] `["a", [2, "b", 3, {"c": [1, 2, 4]}, ["d"]]]`
- [ ] `{"a": 12, "b": true, "c": [2, "e", 3, {"f", 4}]}`

**Aplicando os princípios de uma arquitetura REST, qual das seguintes secções de código no cliente é a mais correcta para, utilizando uma API REST, apagar um registo da entidade livro?**

- [ ] `axios.post('http://minha.api.com/livros/delete', { livroToDelete })`
- [x] `axios.delete('http://minha.api.com/livros/' + livroToDelete.id )`
- [ ] `axios.destroy('http://minha.api.com/livros/ + livroToDelete.id + '/delete')`
- [ ] `axios.delete('http://minha.api.com/livros/delete', { livroToDelete })`

**A biblioteca "Vue Router" inclui uma funcionalidade que se chama "Navigation Guards". O que são os "Navigation Guards"?**

- [ ] É um mecanismo que aumenta a segurança do navegador web, restringindo o acesso da aplicação Vue.js aos recursos internos do navegador web
- [ ] É um mecanismo que aumenta a segurança da aplicação Vue.js, restringindo o acesso do navegador web aos recursos internos da aplicação
- [x] São funções que são executadas sempre que o Vue Router altera a rota interna da aplicação
- [ ] São componentes que permitem mostrar ou esconder menus de navegação

**Na arquitetura REST, qual dos seguintes métodos HTTP pode ser utilizado para alterar ou atualizar um recurso do servidor?**

- [ ] POST
- [x] PATCH
- [ ] DIFF
- [ ] UPDATE

**A biblioteca "Pinia" permite fazer a gestão de estado nas aplicações Vue.js, em que cada aplicação Vue.js pode conter vários "Pinia stores". Qual dos seguintes itens corresponde a elementos que os "Pinia stores" poderão ter?**

- [x] Actions
- [ ] Tables
- [ ] Nenhum dos outros itens correspondem a elementos que os "Pinia stores" poderão ter
- [ ] References

**Em relação às "promises" do JavaScript, qual das seguintes afirmações é verdadeira:**

- [ ] As "promises" são funções que prometem um conjunto de resultados, ou seja, que permitem especificar quais os resultados esperados na sua execução
- [ ] As "promises" são funções anónimas que incluem "closures", propriedades e dados JSON
- [ ] As "promises" são as funções internas das funções de "closure"
- [x] As "promises" têm 3 estados: "pending": "fulfilled" e "rejected"

**No contexto da Framework Vue.js, qual das seguintes secções de código não corresponde a um "Text Interpolation" válido?**

- [ ] `<a href="http://www.a.com">{{ x }}</a>`
- [ ] `<a href="http://www.a.com">{{ functionA(x) }}</a>`
- [ ] Todas as outras opções têm código com "Text Interpolation" válido
- [x] `<a href="{{ x }}">Some Url</a>`

**Qual dos seguintes itens *não* é uma diretiva da Framework Vue.js?**

- [ ] v-on
- [ ] v-show
- [ ] v-model
- [x] v-click

**Supondo que um componente Vue.js inclui a variável reativa "r" definida da seguinte forma:**

```js
<script setup>
  const r = ref(3)
</script>
```

**Qual o código, dentro da secção `<script setup>`, que garante que sempre que o valor da variável reativa `r` seja alterado, irá escrever na consola o valor antigo e o novo valor.**

- [ ]

  ```js
  defineWatch('r', (a, b) => {
    console.log(`value of r has changed from ${a} to ${b}`)
  })
  ```

- [ ]

  ```js
  onChange((r) => {
    console.log(`value of r has changed from ${r.oldValue} to ${r.newValue}`)
  })
  ```

- [ ]

  ```js
  const ev = whenEmit('r', (newValue, oldValue) => {
    console.log(`value of r has changed from ${oldValue} to ${newValue}`)
  })
  ```

- [x]

  ```js
  watch(r, (a, b) => {
    console.log(`value of r has changed from ${b} to ${a}`)
  })
  ```

**Em relação aos WebSockets, qual das seguintes afirmações é *falsa*?**

- [x] Os WebSockets têm como objetivo tornar os serviços Web RESTful mais rápidos
- [ ] Os WebSockets permitem a comunicação bidirecional entre o cliente e o servidor
- [ ] Para iniciar a comunicação com WebSockets, o cliente começa por enviar um "handshake" ao servidor através de um pedido HTTP
- [ ] A API dos WebSockets é um standard W3C

### 10/01/2024

**Aplicando os princípios de uma arquitetura REST, qual das seguintes secções de código no cliente é a mais correcta para, utilizando uma API REST, alterar um registo da entidade livro?**

- [ ] `axios.patch('http://minha.api.com/livros/' + livro.id + '/patch', { livro })`
- [x] `axios.put('http://minha.api.com/livros/' + livro.id, { livro })`
- [ ] `axios.post('http://minha.api.com/livros/update', { livro })`
- [ ] `axios.put('http://minha.api.com/livro', { livro })`

**Qual dos seguintes items é relativo a um objeto, biblioteca ou framework incluído no browser e que permite estabelecer comunicação HTTP com o servidor.**

- [x] Fetch API
- [ ] Http API
- [ ] DOM
- [ ] Axios

### 11/01/2024

**Qual dos seguintes itens representa dados JSON válidos?**

- [ ] `["a", [2, "b", 3, {"c": [1, 2, 4, {"d": "e": 3}]}, ["d": 2]]]`
- [ ] Nenhum dos outros itens representa dados JSON válidos
- [x] `["a", [2, "b", {"c": [1, {"d": "d"}]}, [{"e": ["f", "g"]}]]]`
- [ ] `[2, "a", 3, {"b": 12: "c": 1: "d": 4}]`

**Na arquitetura REST, o método PATCH deverá ser utilizado:**

- [ ] Para consultar dados
- [ ] Para inserir dados
- [ ] Para remover dados
- [x] Para atualizar dados

**Em relação aos WebSockets, qual das seguintes afirmações é *falsa*?**

- [x] Os WebSockets modificam o protocolo HTTP, reduzindo a latência do mesmo
- [ ] Os WebSockets incluem um protocolo de comunicação que poderá ser utilizado por diversas linguagens (Javascript, Java, C#, etc)
- [ ] Os WebSockets permitem a comunicação bidirecional entre o cliente e o servidor
- [ ] Para iniciar a comunicação com WebSockets, o cliente começa por enviar um "handshake" ao servidor através de um pedido HTTP

**Qual das seguintes secções de código de um template da Framework Vue.js, permite definir uma hiperligação?**

- [ ] `<v-link href="getUrl()"> ... </a>`
- [ ] `<a href={{ getUrl() }}> ... </a>`
- [ ] `<a v-link="getUrl()"> ... </a>`
- [ ] `<a v-bind:href="getUrl()"> ... </a>`

**Um componente Vue.js inclui o seguinte código JavaScript:**

```js
<script setup>
  . . .
  const x = inject('a')
  . . .
</script>
```

**Para que serve a função `inject` no código anterior?**

- [ ] Permite injetar no objecto 'x' os eventos associados à propriedade 'a'
- [x] Permite injetar neste componente um objeto (ou outro tipo de dados) que foi criado noutro componente (ascendente) e fornecido a este através da função "provide".
- [ ] Permite injetar uma biblioteca externa neste componente, para acesso a APIs, WebSockets ou outros recursos externos
- [ ] O Permite injetar um provider de serviços externos à aplicação.

**Qual dos seguintes itens não é uma diretiva da Framework Vue.js?**

- [ ] v-show
- [ ] v-bind
- [x] v-while
- [ ] v-model

**Qual dos seguintes itens representa dados JSON válidos?**

- [x] Todos os outros itens representam dados JSON válidos
- [ ] `[false]`
- [ ] `[2, "a", 3, {"b": 12, "c": true}]`
- [ ] `["a", [2, "b", {"c": [1, {"d": "d"}]}, [{"e": ["f", "g"]}]],[false]]`

**A biblioteca "Vue Router" pode ser configurada para utilizar diferentes modos ("History Modes"). Qual dos seguintes itens é um "History Mode" suportado pela biblioteca "Vue Router"?**

- [ ] Encrypt mode
- [x] HTML 5 mode
- [ ] Browser mode
- [ ] Nenhum dos outros itens é um history mode suportado pelo Vue Router

**Qual dos seguintes itens representa dados JSON válidos?**

- [ ] `{"a": 12, "b": true, "c": [2, "e", 3, {"f", 4}]}`
- [ ] `[2, "a", 3, {"b": 12: "c": 1: "d": 4}]`
- [x] `["a", [2, "b", 3, {"c": [1, 2, 4, {"d": "d"}]}, ["d"]]]`
- [ ] Nenhum dos outros itens representa dados JSON válidos

**Qual das seguintes secções de código de um template da Framework Vue.js, permite definir uma imagem?**

- [x] `<img v-bind:src="imageUrl()">`
- [ ] `<img v-attr(src)="{{ imageUrl() }}">`
- [ ] `<v-img src="imageUrl()">`
- [ ] `<img @src="imageUrl()">`

**Considerando o seguinte código JavaScript:**

```js
var f = function () {
  var i = 1
  return function () {
    console.log(i)
    i += 2
  }()
}()
f()
f()
f()
```

**O que é escrito na consola?**

- [ ] 1\
1\
1
- [ ] A definição/código de uma função (repetida 3 vezes)
- [x] Escreve "1" e de seguida escreve um erro
- [ ] 1\
3\
5

**Em relação às funções anónimas do JavaScript, qual das seguintes afirmações é verdadeira:**

- [ ] As funções anónimas são funções que podem ser invocadas por utilizadores anónimos (utilizadores que não estão autenticados)
- [ ] As funções anónimas são funções que só podem ser atribuídas a variáveis
- [x] As funções anónimas são funções que não têm nome
- [ ] As funções anónimas não têm nome e são funções privadas dos ficheiros onde estão definidas

**Em relação às funções "closure" do JavaScript, qual das seguintes afirmações é verdadeira:**

- [ ] As funções "closure" são funções construtoras de classes
- [ ] As funções "closure" permitem redefinir os protótipos dos objetos
- [x] As funções "closure" permitem manter o estado das variáveis locais da função que a contém, enquanto a própria função "closure" persistir
- [ ] As funções "closure" permitem aumentar a funcionalidade dos tipos primitivos

**Considerando que o componente Vue "ContaBancaria" inclui a propriedade (prop) "saldo", qual a secção de código do template desse componente que apresenta o valor do saldo a vermelho, quando este é negativo, e a verde caso contrário (saldo >=0)?**

**Nota: Considere que a classe CSS "negativo" define uma formatação com o texto a vermelho e a classe CSS "positivo" define uma formatação com o texto a verde.**

- [ ] Nenhuma das outras secções de código apresentam o valor do saldo a vermelho, quando o mesmo é negativo, e a verde quando o saldo é maior ou igual a zero
- [ ] Saldo = `<span class="{{ saldo < 0 ? 'negativo' : 'positivo' }}">{{saldo}}</span>`
- [ ] Saldo = `<span v-if=(saldo<0) {class='negativo'} v-else {class='positivo'}>{{saldo}}</span>`
- [x] Saldo = `<span class="{negativo: saldo < 0, positivo: saldo >= 0}">{{saldo}}</span>`

**Algumas frameworks Javascript utilizam uma técnica ou mecanismo designado de Virtual DOM. Para que serve o Virtual DOM?**

- [ ] Permite virtualizar o DOM de forma a que o comportamento do mesmo seja sempre igual, independentemente do browser onde a aplicação é executada
- [ ] Permite ao servidor fazer o rendering das páginas e enviar o resultado para a Virtual DOM no cliente (browser), melhorando desta forma o desempenho das páginas e a integração entre o cliente e o servidor
- [x] Permite melhorar o desempenho e eficiência do rendering das páginas
- [ ] Permite melhorar o encapsulamento e isolamento dos componentes DOM

**Depois de executada a seguinte secção de código ECMAScript 6, qual o valor da variável `x`?**

```js
let a = 3
let x = a => a * 2
```

- [x] x é uma função
- [ ] x é inválido porque o código tem um ou mais erros
- [ ] 6
- [ ] 3

**Supondo que a variável "a" tem o valor de 9. Qual das seguintes secções de código (ECMAScript6) atribui à variável "str" o valor de:**

`"Nota do aluno é 18"`

- [ ] `let str = "Nota do aluno é ${2*a}"`
- [ ] `let str = 'Nota do aluno é $a+$a'`
- [x] `` let str = `Nota do aluno é ${a*2}` ``
- [ ] `let str = 'Nota do aluno é ' . (a * 2)`

**Considerando que existe uma API REST com o endpoint `http://api.com/dados/x` que devolve a string `X` e demora *3 segundos*, e o endpoint `http://api.com/dados/y` que devolve a string `Y` e demora *1 segundo*, e considerando o seguinte código JavaScript (que usa a biblioteca Axios):**

```js
let endpointX = 'http://api.com/dados/x'
let endpointY = 'http://api.com/dados/y'
axios.get(endpointX)
  .then(r => {
    console.log(r.data)
    return axios.get(endpointY)
  })
  .then(r => {
    console.log(r.data)
    return r.data
  })
console.log("END")
```

**Quanto tempo demora a execução e o que é escrito na consola?**

- [ ] Demora 4 segundos e escreve na consola:\
END\
Y\
X
- [x] Demora 4 segundos e escreve na consola:\
END\
X\
Y
- [ ] É instantâneo e escreve uma mensagem de erro na consola
- [ ] Demora 3 segundos e escreve na consola:\
END\
X

**Qual das seguintes secções de código permite a um componente Vue.js emitir evento/s corretamente?**

- [x] Todas as secções de código emitem eventos corretamente.
- [ ]

  ```js
  <script setup>
  import { ref } from 'vue'
  const emit = defineEmits(['a', 'b', 'c'])
  const m = () => {
    emit('a', ['a', 'b', 'c'])
    emit('b', { a: 1, b: 2, c: 3 })
    emit('c', 'emit')
  }
  </script>
  ```

- [ ]

  ```js
  <script setup>
  import { ref } from 'vue'
  const emit = defineEmits(['a', 'b', 'c'])
  const m = () => {
    emit('a', 'b', 'c')
    emit('b', 'b', 'b', 'b')
    emit('c')
  }
  </script>
  ```

- [ ] Nenhuma das secções de código emite evento/s corretamente.

**Considerando que existe uma API REST com o endpoint `http://api.com/dados/x` que devolve o número *3* e o endpoint `http://api.com/dados/y` que devolve o número *5*, e considerando o seguinte código JavaScript (que usa a biblioteca Axios):**

```js
let endpointX = 'http://api.com/dados/x'
let endpointY = 'http://api.com/dados/y'
var f1 = async function () {
  var res1 = axios.get(endpointX)
  var res2 = await axios.get(endpointY)
  console.log(res1.data)
  console.log(res2.data)
}
console.log("A")
f1()
console.log("END")
```

**O que é escrito na consola?**

- [ ] A\
END\
3\
5
- [ ] A\
3\
5\
END
- [x] A\
END\
undefined\
5
- [ ] Escreve uma mensagem de erro na consola

**Na arquitetura REST, para obter um recurso do servidor deve ser utilizado o método HTTP:**

- [ ] PUT
- [x] GET
- [ ] OBTAIN
- [ ] LOAD

**Qual das seguintes opções é uma característica da linguagem JavaScript?**

- [ ] É uma linguagem compilada
- [ ] É utilizada exclusivamente nos clientes Web (browsers)
- [x] Suporta o paradigma de programação funcional
- [ ] Foi desenvolvida em integração com a linguagem PHP

**Qual das seguintes opções é um tipo de dados nativo do JavaScript?**

- [ ] Real
- [ ] Todas as outras opções são tipos de dados nativos do Javascript
- [ ] Integer
- [x] Number

**Qual das seguintes expressões é um objeto válido em JavaScript?**

- [ ] Nenhuma das outras expressões é um objeto válido
- [x] `{ z: ["a", 3, {}], x: [undefined, function () { return null }] }`
- [ ] `{ z: [], x: ["a": 3], undefined }`
- [ ] `{ z: ["a", 3, {a, "3"}, { a: 1, b: 2 }] }`

**Considerando o seguinte código JavaScript:**

```js
let a = 1
let b = 3
console.log((a, b) => {
  console.log(b)
  return a + b
})
```

**O que é escrito na consola?**

- [ ] Não escreve nada na consola
- [x] A definição/código de uma função
- [ ] O
- [ ] 3\
4

**Um componente Vue.js inclui o seguinte código JavaScript:**

```js
<script setup>
  . . .
  const x = inject('a')
  . . .
</script>
```

**Para que serve a função `inject` no código anterior?**

- [x] Permite injetar neste componente um objeto (ou outro tipo de dados) que foi criado noutro componente (ascendente) e fornecido a este através da função "provide".
- [ ] Permite injetar uma biblioteca externa neste componente
- [ ] Permite injetar o provider com o nome "a", para acesso a APIs, WebSockets ou outros recursos externos. A configuração do provider é feita na aplicação através da função de configuração "provide"
- [ ] Permite injetar no objecto 'x' os eventos associados à propriedade 'a'

**A framework Vue.js 3 suporta 2 APIs: a "Options API" e a "Composition API". Qual das seguintes afirmações relativas às 2 APIs é verdadeira?**

- [ ] Todas as restantes afirmações são verdadeiras
- [ ] Ao contrário do que acontece com a "Option API", a definição de componentes com a "Composition API" é feita através da composição de vários ficheiros
- [ ] Ao contrário do que acontece com a "Composition API", a "Option API" permite acrescentar propriedades (props) de opção aos componentes
- [x] Ao contrário do que acontece com a "Composition API", os componentes especificados com a "Option API" têm acesso à variável "this", que se refere à instância do componente e é preenchida em runtime pela framework Vue.js

**Supondo que se pretende definir a propriedade (prop) com o nome `a` num determinado componente. Qual o código que o permite fazer?**

- [ ]  

  ```js
  <script setup>
  . . .
  const a = defineProps({ name: 'a' })
  . . .
  </script>
  ```

- [ ]  

  ```js
  <script setup>
  . . .
  const props = { 'a' : 3 }
  . . .
  </script>
  ```

- [ ]  

  ```js
  <script setup>
  . . .
  const props = defineProps('a')
  . . .
  </script>
  ```

- [x]  

  ```js
  <script setup>
  . . .
  const x = defineProps(['a'])
  . . .
  </script>
  ```

**O que é necessário para que um componente Vue.js suporte a diretiva `v-model`?**

- [ ] A diretiva v-model só pode ser definida pela própria framework Vue.js
- [ ] Incluir uma propriedade de leitura e escrita com o nome "v-model"
- [x] Incluir a propriedade (props) com o nome "modelValue" e emitir o evento com o nome "update:modelValue"
- [ ] Incluir a função "v-model" que devolve o valor do modelo

**Em relação às diretivas `v-show` e `v-if` da Framework Vue.js, qual das afirmações é verdadeira?**

- [ ] Para mostrar ou esconder elementos HTML, a diretiva v-if aplica ou remove estilos a esses elementos
- [ ] A diretiva v-show só funciona em conjunto com a diretiva v-if
- [ ] A diretiva v-show constrói ou destrói elementos HTML conforme necessário
- [x] Para mostrar ou esconder elementos HTML, a diretiva v-show aplica ou remove estilos a esses elementos

**Em relação ao sistema de reatividade da framework Vue.js, qual das seguintes afirmações é verdadeira?**

- [ ] Os dados reativos definidos pela função reactive() podem ser de qualquer tipo (String, Number, Boolean, Object, Array, etc.)
- [ ] Todas as restantes afirmações são verdadeiras
- [x] Os dados reativos definidos pela função reactive() são acedidos diretamente pela referência devolvida pela função.

  Exemplo de código:

  ```js
  const a = reactive({c:0})
  a.c++
  ```

- [ ] Os dados reativos que suportam one-way binding são definidos pela função ref() e os dados reativos que suportam two-way binding são definidos pela função reactive()

**Qual das seguintes secções de código de um template da Framework Vue.js, permite definir uma imagem?**

- [ ] `<img src="{{ imageUrl() }}">`
- [x] `<img :src="imageUrl()">`
- [ ] `<v-image src="imageUrl()">`
- [ ] `<img v-src="imageUrl()">`

**No contexto das aplicações Web, qual das seguintes afirmações relativas ao modelo aplicacional híbrido é correta?**

- [x] Os conteúdos das aplicações híbridas são apresentados no cliente através de várias páginas web distintas, mas cada página tem a capacidade de alterar o seu conteúdo sem a necessidade de refrescar a mesma por completo
- [ ] As aplicações híbridas são aplicações que suportam o protocolo HTTP e o protocolo HTTPS em simultâneo
- [ ] As aplicações híbridas são aplicações que suportam execução síncrona e assincrona
- [ ] As aplicações híbridas são aplicações que permitem a execução de Javascript no cliente e no servidor

### 12/01/2024

**Qual dos seguintes items não é um Javascript Engine?**

- [ ] Google Chrome
- [ ] V8
- [ ] Todas as outras opções são Javascript Engines
- [ ] SpiderMonkey

### 30/01/2024

**Depois de executada a seguinte secção de código ECMAScript 6, qual o valor da variável `x`?**

```js
let a = [1, 2, 3, 4]
let x = 0
a.forEach(v => { x += v })
```

- [ ] x é uma função
- [ ] x é inválido porque o código tem um ou mais erros
- [ ] [1, 3, 6, 10]
- [ ] 10

### 02/02/2024

**Qual das seguintes linguagens é interpretada e executada pelo Javascript Engine?**

- [ ] Javascript e PHP
- [ ] Javascript e Java
- [ ] Javascript, CoffeeScript e TypeScript
- [x] Apenas Javascript

### 04/02/2024

**A Framework Vue.js suporta "data-binding". O que é o "data-binding"?**

- [ ] É um mecanismo que permite ao Vue.js conectar-se, de forma transparente, automática e sem código, a bases de dados relacionais
- [ ] É um mecanismo que permite ao Vue.js conectar-se, de forma transparente, automática e sem código, a qualquer tipo de base de dados
- [ ] É um mecanismo que permite associar campos de datas (ex: data de nascimento) a inputs com calendários
- [x] É uma técnica que permite sincronizar as fontes de dados do código com a sua representação no desenho, de forma a que as alterações nas fontes de dados refletem-se no desenho

**Em relação às funções anónimas do JavaScript, qual das seguintes afirmações é verdadeira:**

- [ ] As funções anónimas não têm nome e são funções privadas dos ficheiros onde estão definidas
- [ ] As funções anónimas são funções que podem ser invocadas por utilizadores anónimos (utilizadores que não estão autenticados)
- [ ] As funções anónimas não têm nome e são funções privadas dos objetos
- [x] Nenhuma das outras afirmações é verdadeira

**Considerando o seguinte código JavaScript:**

```js
var f = function () {
  var i = 3
  console.log(i)
  return function () {
    console.log(i)
    i *= 2
  }()
}
f()
f()
f()
```

**O que é escrito na consola?**

- [ ] 3\
3\
6\
12
- [x] 3\
3\
3\
3\
3\
3
- [ ] A definição/código de uma função (repetida 3 vezes)
- [ ] 3\
3\
3

### 05/02/2024

**Um componente Vue.js inclui o seguinte código JavaScript:**

```js
<script setup>
  ...
  const x = inject('a')
  ...
</script>
```

**Para que serve a função inject no código anterior?**

- [ ] Permite injetar uma biblioteca externa neste componente
- [ ] Permite injetar o provider com o nome "a", para acesso a APIs, WebSockets ou outros recursos externos. A configuração do provider é feita na aplicação através da função de configuração "provide"
- [x] Permite injetar neste componente um objeto (ou outro tipo de dados) que foi criado noutro componente (ascendente) e fornecido a este através da função "provide".
- [ ] Permite injetar no objecto 'x' os eventos associados à propriedade 'a'

**O Javascript Engine:**

- [x] Executa JavaScript em vários contextos (Browser, Node.js, etc.)
- [ ] Compila JavaScript para Java e executa o código resultante
- [ ] Executa JavaScript exclusivamente no cliente (Browser)
- [ ] É um motor gráfico que permite melhorar o desempenho do JavaScript

**Supondo que um componente Vue.js inclui a propriedade "a" definida da seguinte forma:**

```js
<script setup>
  // ...
  const x = defineProps(['a'])
  // ...
</script>
```

**Qual o código, dentro da secção `<script setup>`, que irá escrever na consola o valor da propriedade "a"?**

- [ ] console.log(a.prop)
- [ ] console.log(a.prop.value)
- [x] console.log(x.a)
- [ ] console.log(a.value)

### 06/02/2024

**Qual o resultado da expressão JavaScript:**

`"1" == 1`

- [ ] A expressão é inválida
- [ ] undefined
- [ ] false
- [x] true

### 07/02/2024

**Qual das seguintes opções é um tipo de dados nativo do JavaScript?**

- [ ] Float
- [ ] Integer
- [ ] Function
- [ ] Char
