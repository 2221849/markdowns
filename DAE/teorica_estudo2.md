# Desenvolvimento de Aplicações Distribuídas

## Teórica

### 21/01/2021

**Em relação ao Node.js qual das seguintes afirmações é verdadeira?**

- [ ] O Node.js é um servidor "single-threaded"
- [ ] O Node.js está otimizado para operações que envolvem muitos cálculos (CPU intensive operations)
- [ ] O Node.js suporta transações
- [ ] O Node.js utiliza um modelo de programação orientado a objetos

**A biblioteca "Vue Router" inclui o "router-link". O que é o "router-link"?**

- [ ] É o objecto que permite ligar o componente Vue Router à aplicação que utiliza a framework Vue.js
- [ ] É o componente incluido no Vue Router que é responsável por desenhar os componentes associados às rotas internas da aplicação
- [ ] É a propriedade do componente Vue Router que permite configurar as rotas internas da aplicação
- [ ] É o componente incluido no Vue Router que é responsável por gerar uma hiperligação que irá referenciar uma rota interna da aplicação

**Em relação aos WebSockets, qual das seguintes afirmações é verdadeira?**

- [ ] Os WebSockets estabelecem um canal de comunicação seguro e encriptado entre o cliente e o servidor
- [ ] Um servidor de WebSockets é mais escalável (consegue suportar mais clientes) que um servidor HTTP
- [ ] Os WebSockets modificam o protocolo HTTP, reduzindo a latência da mesmo
- [ ] Para iniciar a comunicação com Websockets, o cliente começa por enviar um "handshake" ao servidor através de um pedido HTTP

**Se um componente Vue.js desenha uma linha de uma tabela (elemento `<tr>`) e é representado pelo elemento `<linha>`, como é que deverá ser utilizado num template?**

- [ ] `<table><tr><linha></linha></tr><tr><<linha></linha></tr></table>`
- [ ] `<table><tr is=linha></tr><tr is=linha></tr></table>`
- [ ] `<table><linha></linha><linha></linha></table>`
- [ ] `<table><linha is:table:row></linha><linha is:table:row></linha></table>`

**Considerando a utilização da biblioteca "Socket.io" no servidor, e que a variável "io" refere-se ao servidor de WebSockets e a variável "socket" refere-se ao socket que liga o servidor ao cliente C1, indique qual o código para enviar a mensagem "msg" com o objeto (obj) para o cliente C1.**

- [ ] `io.sockets.to('C1').emit('msg', obj)`
- [ ] `socket.emit('C1', 'msg', obj)`
- [ ] `socket.emit('msg', obj)`
- [ ] `io.emit('C1', 'msg', obj)`

**Qual das seguintes secções de código permite registar um componente Vue.js com o nome "Component" e associá-lo à tag "abc"?**

- [ ] `Vue.Component(Register('abc'))`
- [ ] `Component.Register('abc')`
- [ ] `new Vue(abc, Component)`
- [ ] `new Vue({ el: '#app', component: { 'abc': Component} })`

**A biblioteca "Vuex" permite fazer a gestão de estado nas aplicações Vue.js. Qual a forma mais correta para alterar o estado de uma Vuex "store"?**

- [ ] Fazendo o commit de uma mutação ("mutation")
- [ ] Invocando um dos métodos da Vuex Store: "create", "update" ou "delete"
- [ ] Fazendo o commit de um "setter"
- [ ] Invocando o método setState() relativo ao estado que se pretende alterar. Por exemplo, se o nome do estado é "user", deverá ser invocado o método setUser()

**Qual dos seguintes itens é uma restrição arquitetural (architectural constraint) do estilo arquitetural REST?**

- [ ] Transporte de dados em JSON (JSON data transportation)
- [ ] Sistema em Camadas (Layered System)
- [ ] Serviços Transacionais (Transactionals Services)
- [ ] Comunicações Bidirecionais (Bidirectional Communications)

### 21/10/2021


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

**O ECMA Script 6 introduz 2 novas estruturas de dados, o `Set` e o `Map`. Qual das seguintes afirmações sobre estas estruturas é verdadeira:**

- [ ] Ambas permitem manter conjuntos de dados de vários tipos (exemplo: string, números, objetos, etc...)
- [ ] O Map permite manter um conjunto de pares chave+valor
- [ ] O Set permite manter um conjunto de dados únicos
- [ ] Todas as restantes afirmações são verdadeiras

### 14/01/2022

**Qual dos seguintes items *não* é um dos princípios orientadores para garantir uma interface uniforme no estilo arquitetural REST?**

- [ ] Mensagens auto-descritivas (self-descriptive messages)
- [ ] Manipulação dos recursos através das suas representações (manipulation of resources through representations)
- [ ] Autenticação baseada em JWT Tokens (JWT token based authentication)
- [ ] Identificação de recursos (Identification of resources)

**Considerando a utilização da biblioteca "Socket.io" no servidor, e que a variável `io` refere-se ao servidor de WebSockets e a variável `socket` refere-se ao socket que liga o servidor ao cliente C1, indique qual o código do servidor para enviar a mensagem "msg" com o objeto (obj) para todos os clientes que estão no canal (room/channel) com o nome "canal".**

- [ ] `io.to('canal').emit('msg', obj)`
- [ ] `socket.emit('canal', 'msg', obj)`
- [ ] `socket.to('canal').emit ('msg', obj)`
- [ ] `io.emit('canal', 'msg', obj)`

**Aplicando os princípios de uma arquitetura REST, qual das seguintes secções de código no cliente é a mais correcta para, utilizando uma API REST, criar um novo registo da entidade livro?**

- [ ] `axios.post('http://minha.api.com/livros', { novoLivro })`
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
**Qual das seguintes secções de código é a mais correta para aceder (ler) ao estado, ou parte do estado, de uma Vuex store?**

- [ ] `let x = this.$store.x`
- [ ] `let x = this.$store.state.x`
- [ ] `let x = this.$vuex.store.x`
- [ ] `let x = this.$state.x`

### 24/10/2022

**Qual dos seguintes items é um objeto, biblioteca ou framework que permite estabelecer comunicação HTTP com o servidor.**

- [ ] HTML API
- [ ] JSON
- [ ] DOM AJAX
- [ ] Axios

**Tendo em conta o seguinte código (ECMAScript 6):**

```js
let a = 6
console.log(`a= ${a * 2 + a} + ${a}` + `${a}` + a * 2 + '${a}')
```

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
- [ ] Demora 3 segundos e escreve na consola:\
END\
Y\
X
- [ ] Demora 3 segundos e escreve na consola:\
END\
X\
Y

### 06/11/2023

**A biblioteca "Vue Router" pode ser configurada para utilizar o "modo historia" ("History Mode"). O que é que este modo permite?**

- [ ] Permite que o URL das rotas internas da aplicação tenham um formato similar às rotas do servidor (exemplo: `http://site.com/users/123`)
- [ ] Permite que a aplicação Vue.js mantenha um log com o histórico de todas as rotas internas utilizadas
- [ ] Permite enviar para o servidor informação sobre o histórico de utilização da aplicação
- [ ] Permite que a aplicação Vue.js mantenha um log com o histórico de todas os componentes utilizados

**Em relação aos WebSockets, qual das seguintes afirmações é verdadeira?**

- [ ] Os WebSockets estabelecem um canal de comunicação seguro e encriptado entre o cliente e o servidor
- [ ] Um servidor de WebSockets é mais escalável (consegue suportar mais clientes) que um servidor HTTP
- [ ] Os WebSockets modificam o protocolo HTTP, reduzindo a latência da mesmo
- [ ] Para iniciar a comunicação com Websockets, o cliente começa por enviar um "handshake" ao servidor através de um pedido HTTP

**Qual das seguintes secções de código permite registar um componente Vue.js com o nome "Component" e associá-lo à tag "abc"?**

- [ ] `Vue.Component (Register('abc'))`
- [ ] `Component.Register('abc')`
- [ ] `new Vue (abc, Component)`
- [ ] `new Vue({ el: '#app', component: { 'abc': Component} })`

### 08/11/2023

**Na Framework Vue.js, o desenho ("rendering") das páginas Web ...**

- [ ] ... é definido através de templates declarativos
- [ ] ... é definido pela API "Virtual DOM Engine" dos browsers
- [ ] ... é feito pelo motor de vistas (view engine) "Blade"
- [ ] ... é feito pelo motor de vistas "Vue Engine"

### 09/11/2023

**Em relação ao sistema de reatividade da framework Vue.js, qual das seguintes afirmações é verdadeira?**

- [ ] Todas as restantes afirmações são verdadeiras
- [ ] Os dados reativos que suportam one-way binding são definidos pela função reactive() e os dados reativos que suportam two-way binding são definidos pela função ref()
- [ ] Os dados reativos só podem ser representados no template através da diretiva v-model
- [ ] Os dados reativos definidos pela função ref() são acedidos pela propriedade value.\
  Exemplo de código:

  ```js
  const a = ref(0)
  a.value++
  ```

**A framework "Vue.js" pode utilizar a ferramenta "Vite.js". Qual das seguintes afirmações sobre o "Vite.js" é verdadeira?**

- [ ] Durante o desenvolvimento de uma aplicação Vue.js, o Vite.js compila os módulos JavaScript em código binário para correr num servidor web local
- [ ] Durante o desenvolvimento de uma aplicação Vue.js, o Vite.js utiliza a funcionalidade de Hot Module Replacement (HMR) para garantir que a aplicação é atualizada automaticamente e o mais rapidamente possível, sempre que o programador alterar código nos ficheiros JavaScript.
- [ ] Durante o desenvolvimento de uma aplicação Vue.js, o Vite.js cria um servidor web local para acesso aos endpoints das APIs.
- [ ] No processo de publicação da aplicação Vue.js, o Vite.js compila os módulos JavaScript em código binário para correr num servidor web

### 10/11/2023

**A framework "Vue.js" pode utilizar a ferramenta "Vite.js". Qual das seguintes afirmações sobre o "Vite.js" é verdadeira?**

- [ ] Durante o desenvolvimento de uma aplicação Vue.js, o Vite.js cria um servidor web local que utiliza os módulos dos browsers para correr a aplicação.
- [ ] Durante o desenvolvimento de uma aplicação Vue.js, o Vite.js compila os módulos JavaScript em código binário para correr num servidor web local
- [ ] Durante o desenvolvimento de uma aplicação Vue.js, o Vite.js cria um servidor web local para acesso aos endpoints das APIs.
- [ ] No processo de publicação da aplicação Vue.js, o Vite.js compila os módulos JavaScript em código binário para correr num servidor web

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

### 08/01/2024

**O que é o Cross-Origin Resource Sharing (CORS)?**

- [ ] É uma especificação W3C que permite comunicação entre domínios cruzados ("cross-domain")
- [ ] É um formato de dados alternativo ao JSON com melhorias na segurança
- [ ] É um formato de dados que permite partilhar recursos entre vários domínios
- [ ] É uma extensão ao protocolo HTTP que permite mais segurança na comunicação

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

**Considerando a utilização da biblioteca "Socket.io" no servidor, e que a variável `io` refere-se ao servidor de WebSockets e a variável `socket` refere-se ao socket que liga o servidor ao cliente C1. Considerando que estão ligados 3 utilizadores ao servidor (C1, C2 e C3), indique qual o código para enviar a mensagem "msg" com o objeto (obj) para o cliente C3.**

- [ ] `socket('C3').emit('msg', obj)`
- [ ] `socket.emit('C3', 'msg', obj)`
- [ ] Nenhuma das outras opções tem o código necessário para enviar uma mensagem para o cliente C3
- [ ] `io.socket_id('C3').emit('msg', obj)`

**Em relação às "promises" do JavaScript, qual das seguintes afirmações é verdadeira:**

- [ ] As "promises" são funções que prometem um conjunto de resultados, ou seja, que permitem especificar quais os resultados esperados na sua execução
- [ ] As "promises" permitem encadear operações assíncronas
- [ ] As "promises" são funções que não têm nome
- [ ] As "promises" são o equivalente do Javascript às interfaces de programação orientada a objetos

**Qual das seguintes funções converte dados nativos do JavaScript numa string com dados JSON?**

- [ ] Object.convertToJSON
- [ ] JSON.encode()
- [ ] JSON.stringify()
- [ ] JSON.parse()

**Supondo que uma aplicação desenvolvida em Vue.js utiliza a biblioteca "Vue Router" para implementação de um sistema de rotas, e que inclui entre outras, uma rota com o nome "admin" e uma rota com o nome "login" (esta ultima irá apresentar o formulário de autenticação). Supondo também que inclui a biblioteca "authorization.js" com a função isAdmin() que devolve true ou false conforme o utilizador atual seja ou não administrador. Qual dos seguintes itens tem o código correto para garantir que apenas os utilizadores que são administradores poderão aceder à rota "admin".**

- [ ] &#160;

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

- [ ] &#160;

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

- [ ] &#160;

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

- [ ] &#160;

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

- [ ] Permite que todos os componentes descendentes deste (quer sejam descendentes diretos ou indiretos) tenham acesso ao objeto "someObject" através da função "inject"
- [ ] Permite fornecer o objeto "someObject" à propriedade (prop) "x", através da função "inject" do object "someObject"
- [ ] Permite criar um provider com o nome "x", para acesso ao object "someObject". Este provider permite injectar eventos, propriedades e métodos ao objeto "someObject" sem aceder ao código do referido objeto
- [ ] Permite injetar a propriedade "x" ao objeto "someObject"

**Considerando a utilização da biblioteca "Socket.io" no servidor, e que a variável `io` refere-se ao servidor de WebSockets e a variável `socket` refere-se ao socket que liga o servidor ao cliente C1, indique qual o código para enviar a mensagem "msg" com o objeto (obj) para todos os clientes ligados ao servidor.**

- [ ] `socket.emit('msg', obj)`
- [ ] `io.to('*').emit('msg', obj)`
- [ ] `io.emit('msg', obj)`
- [ ] `socket.emit('*', 'msg', obj)`


**A biblioteca "Pinia" permite fazer a gestão de estado nas aplicações Vue.js, em que cada aplicação Vue.js pode conter vários "Pinia stores". Qual dos seguintes itens corresponde a elementos que os "Pinia stores" poderão ter?**

- [ ] State
- [ ] Todos os outros itens correspondem a elementos que os "Pinia stores" poderão ter
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
- [ ] Demora 4 segundos e escreve na consola:\
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
- [ ] Demora 3 segundos e escreve na consola:
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
- [ ] `axios.patch('http://minha.api.com/livros/' + livro.id, { 'titulo': livro.titulo })`
- [ ] `axios.put(http://minha.api.com/livro/' + livro.id, { livro })`
- [ ] `axios.post('http://minha.api.com/livros/update', { livro })`

### 09/01/2024

**Supondo que uma aplicação desenvolvida em Vue.js utiliza a biblioteca "Vue Router" para implementação de um sistema de rotas, e que inclui uma rota com o nome "Project" e que aceita o parâmetro "id". Um determinado componente dessa aplicação inclui a função f1() que tem como objectivo saltar para a rota referida, com o id = 12 (irá mostrar o projeto cujo id = 12).**

**Qual dos seguintes itens tem o código correto para o pretendido:**

- [ ] &#160;

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

- [ ] &#160;

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

- [ ] &#160;

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

- [ ] &#160;

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


**A biblioteca "Pinia" permite fazer a gestão de estado nas aplicações Vue.js, em que cada aplicação Vue.js pode conter vários "Pinia stores". Qual dos seguintes itens corresponde a elementos que os "Pinia stores" poderão ter?**

- [ ] Getters
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
- [ ] Permite que todos os componentes da aplicação tenham acesso ao objeto "someObject" através da função "inject".
- [ ] Permite criar um provider com o nome "x", para acesso ao object "someObject". Este provider permite injectar eventos, propriedades e métodos ao objeto "someObject" sem aceder ao código do referido objeto

**A biblioteca "Vue Router" pode ser configurada para utilizar o modo ("History Mode") "HTML5 mode". O que é que o modo "HTML5 mode" permite?**

- [ ] Permite que o URL das rotas internas da aplicação tenham um formato similar às rotas do servidor (exemplo: `http://meusite.com/users/123`)
- [ ] Permite que a aplicação Vue.js mantenha um log com o histórico de todas os componentes utilizados
- [ ] Permite enviar para o servidor informação sobre o histórico de utilização do HTML na aplicação
- [ ] Permite que a aplicação Vue.js mantenha um log com o histórico de todas as rotas internas utilizadas

**Em relação aos WebSockets, qual das seguintes afirmações é verdadeira?**

- [ ] Os WebSockets incluem um protocolo de comunicação que poderá ser utilizado por diversas linguagens (Javascript, Java, C#, etc.)
- [ ] Os WebSockets modificam o protocolo HTTP, optimizando o desempenho do mesmo
- [ ] Os WebSockets permitem a comunicação direta entre 2 ou mais clientes (browsers)
- [ ] Os WebSockets estabelecem um canal de comunicação seguro e encriptado entre o cliente e o servidor

**Qual das seguintes funções converte dados nativos do JavaScript numa string com dados JSON?**

- [ ] JSON.parse()
- [ ] JSON.decode()
- [ ] JSON.stringify()
- [ ] JSON.encode()



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
- [ ] B\
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

- [ ] Saldo = `<span :class="{negativo: saldo < 0}">{{saldo}}</span>`
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
- [ ] É o componente incluido no Vue Router que é responsável por desenhar os componentes associados às rotas internas da aplicação
- [ ] É a propriedade do componente Vue Router que permite configurar as rotas internas da aplicação

**Supondo que uma aplicação desenvolvida em Vue.js utiliza a biblioteca "Vue Router" para implementação de um sistema de rotas, e que inclui uma rota com o nome "Project" e que aceita o parâmetro "id". Um determinado componente dessa aplicação inclui a função f1() que tem como objectivo saltar para a rota referida, com o id = 12 (irá mostrar o projeto cujo id = 12).**

**Qual dos seguintes itens tem o código correto para o pretendido:**

- [ ] &#160;

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

- [ ] &#160;

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

- [ ] &#160;

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

- [ ] &#160;

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

- [ ] Permite que todos os componentes descendentes deste (quer sejam descendentes diretos ou indiretos) tenham acesso ao objeto "someObject" através da função "inject"
- [ ] Permite associar o provider "someObject" à propriedade "x", sendo que o provider permite acesso a APIs, WebSockets ou outros recursos externos
- [ ] Permite criar um provider com o nome "x", para acesso ao object "someObject". Este provider permite injectar eventos, propriedades e métodos ao objeto "someObject" sem aceder ao código do referido objeto
- [ ] Permite injetar a propriedade "x" ao objeto "someObject" através da função "inject" a colocar no objeto "someObject"


**Em relação aos WebSockets, qual das seguintes afirmações é verdadeira?**

- [ ] Os WebSockets permitem a comunicação direta entre 2 ou mais clientes (browsers)
- [ ] Os WebSockets têm como objetivo tornar os serviços Web RESTful mais rápidos
- [ ] Os WebSockets modificam o protocolo HTTP, optimizando o desempenho do mesmo
- [ ] Os WebSockets estabelecem um canal de comunicação entre o cliente e o servidor, através de uma ligação TCP


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
- [ ] A\
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
- [ ] B\
A

**A biblioteca "Vue Router" pode ser configurada para utilizar diferentes modos ("History Modes"). Qual dos seguintes itens é um "History Mode" suportado pela biblioteca "Vue Router"?**

- [ ] Todos os outros itens são history modes suportados pelo Vue Router
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

**Considerando que o componente Vue "ContaBancaria" inclui a propriedade (prop) "saldo", qual a secção de código do template desse componente que apresenta o valor do saldo a vermelho, quando este é negativo?**

**Nota: Considere que a classe CSS "negativo" define uma formatação com o texto a vermelho.**

- [ ] Nenhuma das outras secções de código apresentam o valor do saldo a vermelho, quando o mesmo é negativo
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

- [ ] D\
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
- [ ] `io.in('canal').emit('msg', obj)`

**Qual das seguintes funções converte uma string com dados JSON em dados nativos do JavaScript?**

- [ ] `String.ConvertFromJSON`
- [ ] `JSON.toNative()`
- [ ] `JSON.parse()`
- [ ] `JSON.decode()`

**Aplicando os princípios de uma arquitetura REST, qual das seguintes secções de código no cliente é a mais correcta para, utilizando uma API REST, apagar um registo da entidade livro?**

- [ ] `axios.post('http://minha.api.com/livros/delete', { livroToDelete })`
- [ ] `axios.delete('http://minha.api.com/livros/' + livroToDelete.id )`
- [ ] `axios.destroy('http://minha.api.com/livros/ + livroToDelete.id + '/delete')`
- [ ] `axios.delete('http://minha.api.com/livros/delete', { livroToDelete })`

**A biblioteca "Vue Router" inclui uma funcionalidade que se chama "Navigation Guards". O que são os "Navigation Guards"?**

- [ ] É um mecanismo que aumenta a segurança do navegador web, restringindo o acesso da aplicação Vue.js aos recursos internos do navegador web
- [ ] É um mecanismo que aumenta a segurança da aplicação Vue.js, restringindo o acesso do navegador web aos recursos internos da aplicação
- [ ] São funções que são executadas sempre que o Vue Router altera a rota interna da aplicação
- [ ] São componentes que permitem mostrar ou esconder menus de navegação

**A biblioteca "Pinia" permite fazer a gestão de estado nas aplicações Vue.js, em que cada aplicação Vue.js pode conter vários "Pinia stores". Qual dos seguintes itens corresponde a elementos que os "Pinia stores" poderão ter?**

- [ ] Actions
- [ ] Tables
- [ ] Nenhum dos outros itens correspondem a elementos que os "Pinia stores" poderão ter
- [ ] References

**Em relação às "promises" do JavaScript, qual das seguintes afirmações é verdadeira:**

- [ ] As "promises" são funções que prometem um conjunto de resultados, ou seja, que permitem especificar quais os resultados esperados na sua execução
- [ ] As "promises" são funções anónimas que incluem "closures", propriedades e dados JSON
- [ ] As "promises" são as funções internas das funções de "closure"
- [ ] As "promises" têm 3 estados: "pending": "fulfilled" e "rejected"

**Supondo que um componente Vue.js inclui a variável reativa "r" definida da seguinte forma:**

```js
<script setup>
  const r = ref(3)
</script>
```

**Em relação aos WebSockets, qual das seguintes afirmações é *falsa*?**

- [ ] Os WebSockets têm como objetivo tornar os serviços Web RESTful mais rápidos
- [ ] Os WebSockets permitem a comunicação bidirecional entre o cliente e o servidor
- [ ] Para iniciar a comunicação com WebSockets, o cliente começa por enviar um "handshake" ao servidor através de um pedido HTTP
- [ ] A API dos WebSockets é um standard W3C

### 10/01/2024

**Aplicando os princípios de uma arquitetura REST, qual das seguintes secções de código no cliente é a mais correcta para, utilizando uma API REST, alterar um registo da entidade livro?**

- [ ] `axios.patch('http://minha.api.com/livros/' + livro.id + '/patch', { livro })`
- [ ] `axios.put('http://minha.api.com/livros/' + livro.id, { livro })`
- [ ] `axios.post('http://minha.api.com/livros/update', { livro })`
- [ ] `axios.put('http://minha.api.com/livro', { livro })`

**Qual dos seguintes items é relativo a um objeto, biblioteca ou framework incluído no browser e que permite estabelecer comunicação HTTP com o servidor.**

- [ ] Fetch API
- [ ] Http API
- [ ] DOM
- [ ] Axios

### 11/01/2024

**Em relação aos WebSockets, qual das seguintes afirmações é *falsa*?**

- [ ] Os WebSockets modificam o protocolo HTTP, reduzindo a latência do mesmo
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
- [ ] Permite injetar neste componente um objeto (ou outro tipo de dados) que foi criado noutro componente (ascendente) e fornecido a este através da função "provide".
- [ ] Permite injetar uma biblioteca externa neste componente, para acesso a APIs, WebSockets ou outros recursos externos
- [ ] O Permite injetar um provider de serviços externos à aplicação.

**A biblioteca "Vue Router" pode ser configurada para utilizar diferentes modos ("History Modes"). Qual dos seguintes itens é um "History Mode" suportado pela biblioteca "Vue Router"?**

- [ ] Encrypt mode
- [ ] HTML 5 mode
- [ ] Browser mode
- [ ] Nenhum dos outros itens é um history mode suportado pelo Vue Router

**Qual das seguintes secções de código de um template da Framework Vue.js, permite definir uma imagem?**

- [ ] `<img v-bind:src="imageUrl()">`
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

**Em relação às funções "closure" do JavaScript, qual das seguintes afirmações é verdadeira:**

- [ ] As funções "closure" são funções construtoras de classes
- [ ] As funções "closure" permitem redefinir os protótipos dos objetos
- [ ] As funções "closure" permitem manter o estado das variáveis locais da função que a contém, enquanto a própria função "closure" persistir
- [ ] As funções "closure" permitem aumentar a funcionalidade dos tipos primitivos


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
- [ ] Demora 4 segundos e escreve na consola:\
END\
X\
Y
- [ ] É instantâneo e escreve uma mensagem de erro na consola
- [ ] Demora 3 segundos e escreve na consola:\
END\
X


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
- [ ] A\
END\
undefined\
5
- [ ] Escreve uma mensagem de erro na consola

**Considerando o seguinte código JavaScript:**

```js
let a = 1
let b = 3
console.log((a, b) => {
  console.log(b)
  return a + b
})
```

**Um componente Vue.js inclui o seguinte código JavaScript:**

```js
<script setup>
  . . .
  const x = inject('a')
  . . .
</script>
```

**Para que serve a função `inject` no código anterior?**

- [ ] Permite injetar neste componente um objeto (ou outro tipo de dados) que foi criado noutro componente (ascendente) e fornecido a este através da função "provide".
- [ ] Permite injetar uma biblioteca externa neste componente
- [ ] Permite injetar o provider com o nome "a", para acesso a APIs, WebSockets ou outros recursos externos. A configuração do provider é feita na aplicação através da função de configuração "provide"
- [ ] Permite injetar no objecto 'x' os eventos associados à propriedade 'a'

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
- [ ] Permite injetar neste componente um objeto (ou outro tipo de dados) que foi criado noutro componente (ascendente) e fornecido a este através da função "provide".
- [ ] Permite injetar no objecto 'x' os eventos associados à propriedade 'a'
