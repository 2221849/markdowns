# Desenvolvimento de Aplicações Distribuídas

## Teórica - Recurso

**1. Considerando o seguinte código JavaScript:**

```js
var a = 8
if ("a" % 2)
    console.log("A")
else
    console.log("B")
```

O que é escrito na consola?

- [ ] Escreve uma mensagem de erro na consola?
- [ ] Não escreve nada na consola
- [x] B
- [ ] A

**2. Considerando que existe uma API REST com o endpoint `http://api.com/dados/x` que devolve o número 3 e demora 3 segundos, e o endpoint `http://api.com/dados/y` que devolve o número 5 e demora 1 segundo, e considerando o seguinte código JavaScript (que usa a biblioteca Axios):**

```js
let endpointX = 'http://api.com/dados/x'
let endpointY = 'http://api.com/dados/y'
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

- [ ] Demora 4 segundos e escreve na consola:\
END\
A\
Promise ...\
Promise ...\
3
- [ ] Escreve uma mensagem de erro na consola
- [ ] Demora 4 segundos e escreve na consola:\
END\
A\
Promise ...\
3\
8
- [x] Demora 3 segundos e escreve na consola:\
A\
END\
Promise ...\
3\
8

**3. Qual das seguintes opções é um tipo de dados nativo do JavaScript?**

- [ ] Char
- [x] Function
- [ ] Class
- [ ] Integer

**4. Em relação às funções "closure" do JavaScript, qual das seguintes afirmações é verdadeira?**

- [x] As funções "closure" permitem manter o estado das variáveis locais da função que a contém, enquanto a própria função "closure" persistir
- [ ] As funções "closure" são funções construtoras de classes
- [ ] As funções "closure" permitem redefinir os protótipos dos objetos
- [ ] As funções "closure" permitem aumentar a funcionalidade dos tipos primitivos

**5. Considerando que o componente Vue "ContaBancaria" inclui a propriedade (prop) "saldo", qual a secção de código do template desse componente que apresenta o valor do saldo a vermelho, quando este é negativo, e a verde caso contrário (saldo >=0)?
Nota: Considere que a classe CSS "negativo" define uma formatação com o texto a vermelho e a classe CSS "positivo" define uma formatação com o texto a verde.**

- [x] Saldo = `<span class="{negativo: saldo < 0, positivo: saldo >= 0}">{{saldo}}</span>`
- [ ] Todas as outras secções de código apresentam o valor do saldo a vermelho, quando o mesmo é negativo, e a verde, caso contrário
- [ ] Saldo = `<span v-if=(saldo<0) {class='negativo'} v-else {class='positivo'}>{{saldo}}</span>`
- [ ] Saldo = `<span class="{{ saldo < ? 'negativo' : 'positivo' }}">{{saldo}}</span>`

**6. Qual dos seguintes itens representa dados JSON válidos?**

- [x] `["a", [2, "b", {"c": [1, {"d": "d"}]}, [{"e": ["f", "g"]}]]]`
- [ ] `["a", [2, "b", 3, {"c": [1, 2, 4, {"d": "e": 3}]}, ["d": 2]]]`
- [ ] `[2, "a", 3, {"b": 12: "c": 1: "d": 4}]`
- [ ] Nenhum dos outros itens representa dados JSON válidos

**7. Considerando que existe uma API REST com o endpoint `http://api.com/dados` e que este devolve o número 3, e considerando o seguinte código JavaScript (que usa a biblioteca Axios):**

```js
let endpoint = 'http://api.com/dados'
console.log(function (m) {
  axios.get(endpoint)
    .then(function (r) {
      console.log(r.data)
      return r.data * m
    })
  console.log(m)
}(10))
console.log('END')
```

**O que é escrito na consola?**

- [ ] END X\
10\
3
- [ ] END\
undefined\
10\
3
- [x] 10\
undefined\
END\
3
- [ ] 10\
END\
15\
3

**8. Em relação ao sistema de reatividade da framework Vue.js, qual das seguintes afirmações é verdadeira?**

- [ ] Nenhuma das restantes afirmações é verdadeira
- [ ] Os dados reativos definidos pela função reactive() podem ser de qualquer tipo (String, Number, Boolean, Object, Array, etc.)
- [x] Os dados reativos definidos pela função reactive() são acedidos diretamente pela referência devolvida pela função.

  Exemplo de código:

  ```js
  const a = reactive({c:0})
  a.c++
  ```

- [ ] Os dados reativos que suportam one-way binding são definidos pela função ref() e os dados reativos que suportam two-way binding são definidos pela função reactive()

Aqui está a lista corrigida em Markdown:

**9. Supondo que se pretende definir a propriedade (prop) com o nome "a" num determinado componente. Qual o código que o permite fazer?**

- [ ] &#160;

  ```js
  <script setup>
  . . .
  const props = { 'a' : 'str value'}
  . . .
  </script>
  ```

- [x] &#160;

  ```js
  <script setup>
  . . .
  const x = defineProps(['a'])
  . . .
  </script>
  ```

- [ ] &#160;

  ```js
  <script setup>
  . . .
  const props = defineProps({
    prop: {
      name: 'a',
      type: String,
      default: 'x'
    }
  })
  . . .
  </script>
  ```

- [ ] &#160;

  ```js
  <script setup>
  . . .
  const props = defineProps('a')
  . . .
  </script>
  ```

**10. Em relação aos WebSockets, qual das seguintes afirmações é verdadeira?**

- [x] Para iniciar a comunicação com Websockets, o cliente começa por enviar um "handshake" ao servidor através de um pedido HTTP
- [ ] Os WebSockets modificam o protocolo HTTP, reduzindo a latência da mesmo
- [ ] Um servidor de WebSockets é mais escalável (consegue suportar mais clientes) que um servidor HTTP
- [ ] Os WebSockets estabelecem um canal de comunicação seguro e encriptado entre o cliente e o servidor

**11. Qual das seguintes secções de código permite a um componente Vue.js emitir evento/s corretamente?**

- [ ] &#160;

  ```js
  <script setup>
  import { ref } from 'vue'
  const emit = defineEmits(['x'])
  const m = () => {
    emit('x')
  }
  </script>
  ```

- [ ] &#160;

  ```js
  <script setup>
  import { ref } from 'vue'
  const emit = defineEmits(['a', 'b', 'c'])
  const m () => {
    emit('a', 'b', 'c')
    emit('b', 'a', 'c')
    emit('c', 'b', 'a')
  }
  </script>
  ```

- [x] Todas as secções de código emitem eventos corretamente.
- [ ] &#160;

  ```js
  <script setup>
  import { ref } from 'vue'
  const a = defineEmits(['x'])
  const m = () => {
    a('x')
  }
  </script>
  ```

**12. Considerando que existe uma API REST com o endpoint `http://api.com/dados/x` que devolve a string "X" e demora 3 segundos, e o endpoint `http://api.com/dados/y` que devolve a string "Y" e demora 1 segundo, e considerando o seguinte código JavaScript (que usa a biblioteca Axios):**

```js
let endpointX = 'http://api.com/dados/x'
let endpointy = 'http://api.com/dados/y'
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
- [ ] Demora 3 segundos e escreve na consola:\
END\
Y\
X
- [ ] Demora 3 segundos e escreve na consola:\
END\
X\
Y
- [x] Demora 4 segundos e escreve na consola:
END\
X\
Y

**13. Aplicando os princípios de uma arquitetura REST, qual das seguintes secções de código no cliente é a mais correcta para, utilizando uma API REST, criar um novo registo da entidade livro?**

- [ ] `axios.get('http://minha.api.com/livro/create', { novoLivro })`
- [x] `axios.post('http://minha.api.com/livros', { novoLivro })`
- [ ] `axios.put('http://minha.api.com/livro', { novoLivro })`
- [ ] `axios.post('http://minha.api.com/livros/create', { novoLivro })`

**14. Na arquitetura REST, para criar um recurso no servidor deve ser utilizado o método HTTP:**

- [ ] PATCH
- [ ] CREATE
- [ ] STORE
- [x] POST

**15. Tendo em conta o seguinte código (ECMAScript 6):**

```js
let a = 4
console.log(a= ${a × 2} + ${a} + {a} + a + a 2 + '${a}')
```

**O que é escrito na consola?**

- [ ] `a = 12{a} 12{a}`
- [x] `a = 8 + 4 + {a} 48${a}`
- [ ] Não escreve nada na consola porque o código é inválido
- [ ] `a = 124 484`

**16. No contexto das aplicações Web, qual das seguintes afirmações relativas ao modelo aplicacional híbrido é correta?**

- [x] Os conteúdos das aplicações híbridas são apresentados no cliente através de várias páginas web distintas, mas cada página tem a capacidade de alterar o seu conteúdo sem a necessidade de refrescar a mesma por completo
- [ ] As aplicações híbridas são aplicações que suportam execução síncrona e assíncrona
- [ ] As aplicações híbridas são aplicações que permitem a execução de Javascript no cliente e no servidor
- [ ] As aplicações híbridas são aplicações que suportam o protocolo HTTP e o protocolo HTTPS em simultâneo

**17. O padrão de desenho (design pattern) utilizado pela Framework "Vue.js" é:**

- [ ] Single-Page View-Model
- [x] Model-View ViewModel
- [ ] Model-View-Controller
- [ ] Singleton

**18. Supondo que um componente Vue.js inclui a variável reativa "r" definida da seguinte forma:**

```js
  <script setup>
  . . .
  const r = ref(3)
  . . .
  </script>
```

**Qual o código, dentro da secção `<script setup>`, que garante que sempre que o valor da variável reativa "r" seja alterado, irá escrever na consola o valor antigo e o novo valor.**

- [ ] &#160;

  ```js
  defineWatch('r', (a, b) => {
    console.log("value of r has changed from ${a} to ${b}`)
  })
  ```

- [ ] &#160;

  ```js
  onChange((r) => {
    console.log(`value of r has changed from ${r.oldValue} to ${r.newValue}`)
  })
  ```

- [x] &#160;

  ```js
  watch(r, (a, b) => {
    console.log(`value of r has changed from ${b} to ${a}`)
  })
  ```

- [ ] &#160;

  ```js
  const ev = whenEmit('r', (newValue, oldValue) => {
    console.log(`value of r has changed from ${oldValue} to ${newValue}`)
  })
  ```

**19. Considerando o seguinte código JavaScript:**

```js
((p1) => {
  console.log(p1 * 2)
})
p1(7)
```

**O que é escrito na consola?**

- [ ] 14
- [x] É escrita uma mensagem de erro na consola
- [ ] undefined
- [ ] Não escreve nada na consola

**20. Qual o resultado da expressão JavaScript:**

`"a" . 2`

- [ ] `"a"`
- [x] A expressão é inválida
- [ ] `"a2"`
- [ ] `2`

**21. O que é necessário para que um componente Vue.js suporte a diretiva v-model?**

- [x] Incluir a propriedade (props) com o nome "modelValue" e emitir o evento com o nome "update:modelValue"
- [ ] Incluir uma propriedade de leitura e escrita com o nome "v-model"
- [ ] Incluir a função "v-model" que devolve o valor do modelo
- [ ] A diretiva v-model só pode ser definida pela própria framework Vue.js

**22. Em relação às funções anónimas do JavaScript, qual das seguintes afirmações é verdadeira:**

- [ ] As funções anónimas não têm nome e são funções privadas dos ficheiros onde estão definidas
- [ ] As funções anónimas não têm nome e são funções privadas dos objetos
- [ ] As funções anónimas são funções que podem ser invocadas por utilizadores anónimos (utilizadores que não estão autenticados)
- [x] Nenhuma das outras afirmações é verdadeira

**23. A biblioteca "Vue Router" inclui o "router-link". O que é o "router-link"?**

- [ ] É o objecto que permite ligar o componente Vue Router à aplicação que utiliza a framework Vue.js
- [ ] É a propriedade do componente Vue Router que permite configurar as rotas internas da aplicação
- [ ] É o componente incluido no Vue Router que é responsável por desenhar os componentes associados às rotas internas da aplicação
- [x] É o componente incluido no Vue Router que é responsável por gerar uma hiperligação que irá referenciar uma rota interna da aplicação

**24. Considerando que existe uma API REST com o endpoint `http://api.com/dados/x` que devolve o número 3 e o endpoint `http://api.com/dados/y` que devolve o número 5, e considerando o seguinte código JavaScript (que usa a biblioteca Axios):**

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
END
- [x] A\
END\
3\
5
- [ ] Escreve uma mensagem de erro na consola
- [ ] A\
3\
5\
8\
END

**25. Os componentes Vue.js podem usar funções ou "computed properties" para calcular valores que serão apresentados no template, tal como se pode observar no seguinte exemplo de código:**

```js
<script setup>
. . .
const x1 = () => {
  return 10 * some.value
}
const x2 = computed(() => {
  return 10 * some.value
})
</script>

<template>
  . . .
  {{ x1() }} ... {{ x2 }}
  . . .
</template>
```

**Qual das seguintes afirmações que compara a função x1 com a "computed property" x2 é verdadeira?**

- [ ] A função "x1" e a computed property "x2" têm um comportamento e utilização similar. As computed properties são "alias" das funções para simplificar a utilização das mesmas nos templates.
- [x] A computed property "x2" só será executada se o valor de "some.value" for alterado. A função "x1" será executada sempre que o valor de qualquer propriedade reativa usada no template for alterada.
- [ ] Nenhuma das restantes afirmações é verdadeira
- [ ] A função "x1" tem um desempenho ligeiramente superior à computed property "x2", porque esta última utiliza uma função callback.

**26. No contexto da Framework Vue.js, qual das seguintes secções de código permite executar a função "f1" quando o utilizador clica num botão na página?**

- [ ] `<button on-click="f1()">botao</button>`
- [ ] `<button v-click="f1">botao</button>`
- [x] `<button @click="f1">botao</button>`
- [ ] `<v-click="f1()"><button>botao</button></v-click>`

**27. Em relação às diretivas v-show e v-if da Framework Vue.js, qual das afirmações é verdadeira?**

- [ ] A diretiva v-show pode-se associar à diretiva v-else
- [ ] Para mostrar ou esconder elementos HTML, a diretiva v-if aplica ou remove estilos a esses elementos
- [x] Nenhuma das outras afirmações é verdadeira
- [ ] A diretiva v-show constrói ou destrói elementos HTML conforme necessário

**28. Qual dos seguintes itens é uma diretiva da Framework Vue.js?**

- [ ] v-emit
- [ ] v-set
- [x] v-if
- [ ] v-while

**29. O JavaScript é uma linguagem de programação ...**

- [ ] interpretada, cujas aplicações são executadas no "Java Virtual Machine"
- [ ] compilada, cujas aplicações são executadas no "web browser"
- [ ] compilada, cujas aplicações são executadas no servidor Node.JS
- [x] interpretada, cujas aplicações são executadas no "JavaScript Engine"

**30. Considerando o seguinte código JavaScript:**

```js
let a = 1
let b = 3
console.log((a, b) => {
  console.log(b)
  return a + b
})
```

**O que é escrito na consola?**

- [ ] 3\
4
- [ ] 3
- [ ] Não escreve nada na consola
- [x] A definição/código de uma função

**31. A biblioteca "Pinia" permite fazer a gestão de estado nas aplicações Vue.js, em que cada aplicação Vue.js pode conter vários "Pinia stores". Qual dos seguintes itens corresponde a elementos que os "Pinia stores" poderão ter?**

- [ ] Getters
- [x] Todos os outros itens correspondem a elementos que os "Pinia stores" poderão ter ✔
- [ ] State
- [ ] Actions

**32. Qual das seguintes secções de código de um template da Framework Vue.js, permite criar um conjunto de parágrafos?**

- [ ] `<p v-for.create(10, idx)>{{ idx }}</p>`
- [x] `<p v-for="(a, b) in arrayDados">{{ a }}</p>`
- [ ] `<v-for="a in arrayDados"><p>{{ a }}</p></v-for>`
- [ ] `<p v-for.create="a in arrayDados">{{ a }}</p>`

**33. Depois de executada a seguinte secção de código ECMAScript 6, qual o valor da variável x?**

```js
let a = 3
let x = (a => a * 2) (4)
```

- [x] 8
- [ ] x é uma função
- [ ] 6
- [ ] false
Resposta correta:
8

**34. A framework Vue.js 3 suporta 2 APIs: a "Options API" e a "Composition API". Qual das seguintes afirmações relativas às 2 APIs é verdadeira?**

- [ ] Todas as restantes afirmações são verdadeiras
- [ ] Ao contrário do que acontece com a "Composition API", a "Option API" permite acrescentar propriedades (props) de opção aos componentes
- [x] Ao contrário do que acontece com a "Composition API", os componentes especificados com a "Option API" têm acesso à variável "this", que se refere à instância do componente e é preenchida em runtime pela framework Vue.js
- [ ] Ao contrário do que acontece com a "Option API", a definição de componentes com a "Composition API" é feita através da composição de vários ficheiros

**35. Considerando o seguinte código JavaScript:**

```js
var f = function () {
  var i = 1
  return function () {
    console.log(i)
    i + 2
  }
}
f()
f()
f()
```

**O que é escrito na consola?**

- [ ] 1\
1\
1
- [x] Não escreve nada na consola
- [ ] A definição/código de uma função (repetida 3 vezes)
- [ ] 1\
3\
5

**36. Supondo que um componente Vue.js inclui o seguinte código JavaScript:**

```js
<script setup>
  . . .
  const someObject = createSomeObject(...)
  provide('x', someObject)
  . . .
</script>
```

**Para que serve o método `provide` no código anterior?**

- [ ] Permite fornecer o objeto "someObject" à propriedade (prop) "x", através da função "inject" do object "someObject"
- [ ] Permite injetar a propriedade "x" ao objeto "someObject"
- [ ] Permite criar um provider com o nome "x", para acesso ao object "someObject". Este provider permite injectar eventos, propriedades e métodos ao objeto "someObject" sem aceder ao código do referido objeto
- [x] Permite que todos os componentes descendentes deste (quer sejam descendentes diretos ou indiretos) tenham acesso ao objeto "someObject" através da função "inject"

**37. Considerando que existe uma API REST com o endpoint `http://api.com/dados` e que este devolve a string "A", e considerando o seguinte código JavaScript (que usa a biblioteca Axios):**

```js
axios.get('http://api.com/dados').then(function (response) {
  console.log(response.data)
})
console.log("B")
```

**O que é escrito na consola?**

- [x] B
- [ ] B
- [ ] A\
B
- [ ] undefined\
B

**38. Supondo que uma aplicação desenvolvida em Vue.js utiliza a biblioteca "Vue Router" para implementação de um sistema de rotas, e que inclui uma rota com o nome "Project" e que aceita o parâmetro "id". Um determinado componente dessa aplicação inclui a função f10) que tem como objectivo saltar para a rota referida, com o id = 12 (irá mostrar o projeto cujo id = 12). Qual dos seguintes itens tem o código correto para o pretendido:**

- [x] &#160;

  ```js
  <script setup>
    . . .
    import { useRouter } from 'vue-router'
    const router = useRouter()
    . . .
    const f1 () => {
      router.push({ name: 'Project', params: {id:12}})
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
      router.goto({ name: 'Project', params: {id:12}})
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
    const f1 = () => {
      router.push('Project', {id: 12})
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
    router.navigate('Project/12')
  }
  . . .
  </script>
  ```

**39. Qual o resultado da expressão JavaScript:**

`1 == "1" ? false : true`

- [ ] true
- [ ] A expressão é inválida
- [ ] undefined
- [x] false

**Considerando a utilização da biblioteca "Socket.io" no servidor, e que a variável "io" refere-se ao servidor de WebSockets e a variável "socket" refere-se ao socket que liga o servidor ao cliente C1. Considerando que estão ligados 3 utilizadores ao servidor (C1, C2 e C3), indique qual o código para enviar a mensagem "msg" com o objeto (obj) para o cliente C3.**

- [ ] `socket.emit ('C3', 'msg', obj)`
- [x] `Nenhuma das outras opções tem o código necessário para enviar uma mensagem para o cliente C3`
- [ ] `io.socket_id('C3').emit('msg', obj)`
- [ ] `O socket('C3').omit('msg', obj)`
