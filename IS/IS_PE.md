# Systems Integration

## Pergunta 1

**Como funciona a integração de aplicações ao nível da aplicação por API (Application Program Interface)?**

- [ ] Os dados são obtidos através de hooks (ganchos) ancorados em objetos dos formulários;
- [x] Nenhuma das outras opções.
- [ ] Os dados são extraídos da base de dados e adicionados a uma nova base de dados;
- [ ] Os dados são extraídos de uma base de dados e inseridos noutra base de dados já existente;

## Pergunta 2

**Analise o XML e o esquema XML (XSD) a seguir e determine a resposta correta.**

**Xml Schema File**:

```xml
<xs:schema attributeFormDefault="unqualified" elementFormDefault="qualified" xmlns:xs="http://www.w3.org/2001/XMLSchema">
  <xs:element name="contacto">
    <xs:complexType>
      <xs:sequence>
        <xs:element name="nome" type="xs:string" />
        <xs:element maxOccurs="unbounded" name="telefone" type="phoneDetails">
        </xs:element>
      </xs:sequence>
    </xs:complexType>
  </xs:element>
  <xs:complexType name="phoneDetails">
    <xs:simpleContent>
      <xs:extension base="xs:int">
        <xs:attribute name="location" type="xs:string" use="required" />
      </xs:extension>
    </xs:simpleContent>
  </xs:complexType>
</xs:schema>
```

**XML File**:

```xml
<contacto>
  <nome>Filipe Gomes</nome>
  <telefone location="casa">932003093</telefone>
  <telefone location="trabalho">244800300</telefone>
  <telefone>244123123</telefone>
</contacto>
```

- [x] Apenas bem formado ("well-formed").
- [ ] Bem formado ("well-formed") e válido.
- [ ] Apenas válido.
- [ ] Nenhuma das outras opções.

## Pergunta 3

**Considere o tipo de integração ao nível dos dados (data level integration). Qual das seguintes afirmações está associada a este tipo de integração?**

- [ ] Os dados são obtidos invocando um método ou função local.
- [x] Nenhuma das outras opções.
- [ ] Os dados são obtidos invocando um método ou função remoto.
- [ ] Os dados são obtidos invocando métodos e funções locais e remotos.

## Pergunta 4

**No paradigma de comunicação Publish/Subscribe (publica/subscreve), que papel está atribuído à entidade que produz informação?**

- [ ] Subscriber ("subscritor").
- [x] Publisher ("publicador").
- [ ] Nenhuma das outras opções.
- [ ] Broker de mensagens.

## Pergunta 5

**Qual das seguintes afirmações está correta, no contexto dos Web Services?**

- [ ] Um Web Service é uma coleção de protocolos abertos e standards utilizados para a troca de dados entre aplicações ou sistemas.
- [ ] Aplicações de software implementadas em várias linguagens de programação e executadas em diferentes plataformas podem usar serviços web para trocar dados através da internet.
- [x] Ambas as opções anteriores.
- [ ] Nenhuma das opções.

## Pergunta 6

**Considere a integração ponto-a-ponto e a integração por middleware com vista à interligação entre 6 aplicações. Para cada abordagem apresentada, quantas ligações terão de ser mantidas/geridas?**

- [x] Ponto-a-Ponto: 15 ligações; Middleware: 6 ligações.
- [ ] Ponto-a-Ponto: 3 ligações; Middleware: 6 ligações.
- [ ] Ponto-a-Ponto: 6 ligações; Middleware: 3 ligações.
- [ ] Nenhuma das outras opções.

## Pergunta 7

**Na perspetiva do cliente, qual das rotas apresentadas permite retornar um determinado recurso do tipo *Spot*?**

**Exemplo 1**:

```c#
[Route("spots/{spotId}/parks/{parkId}")]
public IHttpActionResult GetSpotByPark(string spotId, string parkId)
{ ... }
```

**Exemplo 2**:

```c#
[Route("spots/{spotId}/{parkId}")]
public IHttpActionResult GetSpotByPark(string spotId, string parkName)
{ ... }
```

- [ ] Rota apresentada no código do exemplo 1.
- [ ] Rota apresentada no código do exemplo 2.
- [ ] Ambas as opções anteriores.
- [x] Nenhuma das opções.

## Pergunta 8

**Num documento XML bem formado, o nome do mesmo elemento pode ser escrito com letras maiúsculas e/ou minúsculas.**

**Selecione uma opção:**

- [ ] Verdadeiro
- [x] Falso

## Pergunta 9

**Considere a implementação de um RESTful Web Service usando a ASP.NET Web API, no qual está definido um controller para cada recurso a disponibilizar pelo serviço.**

**Qual é o objetivo do(s) controller(s) na ASP.NET Web API framework?**

- [ ] Servem para apresentar e representar os dados ao utilizador final, normalmente no ecrã.
- [ ] Ajudam a representar os dados trocados entre o serviço e o cliente, e vice-versa.
- [ ] Nenhuma das outras opções.
- [x] Servem para receber os pedidos HTTP vindos do cliente.

## Pergunta 10

**Qual a expressão XPath que permite obter o primeiro elemento *purchase* que possua o atributo *discount* superior a 5%?**

- [ ] `purchase [discount>5][1]`
- [x] Nenhuma das outras opções.
- [ ] `purchase[1][discount>5]`
- [ ] `purchase/count(1)/discount>5`

## Pergunta 11

**Para que serve o standard WSDL associado aos serviços Web SOAP?**

- [x] Serve para definir a interface de serviços Web SOAP.
- [ ] Serve para publicitar serviços Web SOAP.
- [ ] Nenhuma das outras opções.
- [ ] Serve para publicar serviços Web SOAP.

## Pergunta 12

**No contexto das arquiteturas orientadas a serviços (SOA), assinale a opção correta:**

- [ ] Nenhuma das outras opções.
- [x] Precisa de ser estabelecido um protocolo de comunicação para que haja comunicação entre diferentes sistemas com diferentes linguagens de programação.
- [ ] Do ponto de vista do SOA, um serviço é uma função de um sistema computacional que não pode ser consumido por um cliente, sendo usado apenas pelo próprio sistema.
- [ ] SOAP Web Services são um exemplo de sistema para os quais a arquitetura orientada a serviços não é aconselhada.

## Pergunta 13

**Qual das seguintes opções poderá representar a operação de atualização de uma fatura numa API REST?**

- [ ] PUT <http://www.exemplo.com/api/v1/faturas/alterar>.
- [x] Nenhuma das outras opções.
- [ ] PUT <http://www.exemplo.com/api/v1/faturas/modificar>.
- [ ] PUT <http://www.exemplo.com/api/v1/faturas>.

## Pergunta 14

**De que forma o broker Mosquitto poderá garantir a entrega não duplicada de mensagens aos(s) destino(s)?**

- [ ] Nenhuma das outras opções.
- [ ] Esta funcionalidade não está, ainda, disponível no broker Mosquitto.
- [ ] Através de configuração no ficheiro de configuração do broker Mosquitto.
- [x] Através da escolha da qualidade de serviço correta na configuração/uso do canal/tópico em causa.

## Pergunta 15

**Sobre a arquitetura orientada a serviços (SOA) pode-se dizer que parte dos seus princípios são o desacoplamento, abstração e autonomia.**

**Selecione uma opção:**

- [x] Verdadeiro
- [ ] Falso

## Pergunta 17

**Considere um serviço RESTful através do qual é possível gerir o recurso "restaurante" (com as ações GET, PUT, POST, DELETE) usando o formato JSON, disponibilizado pela instituição onde trabalha.**
**Suponha que pretende atualizar o registo de um restaurante através desse serviço.**

**Qual a ação HTTP que escolheria?**

- [ ] GET
- [ ] POST
- [x] PUT
- [ ] DELETE

**Proponha a URI indicada para o efeito:**

- [ ] <http://localhost:port/food>
- [ ] <http://localhost:port/food/{id}>
- [ ] <http://onlinefood.com/restaurante>
- [ ] <http://onlinefood.com/restaurante/{id}>
- [x] <http://onlinefood.com/restaurantes/{id}>

**Seria necessário enviar alguma informação/recurso no body do pedido?**

- [x] Sim
- [ ] Não

## Pergunta 18

**Na perspetiva do cliente REST, qual a diferença entre declarar a implementação da resposta ao GET como:**

```c#
public Customer[] GetAllCustomers()
{
  return arrCustomers;
}
public Customer[] GetCustomers()
{
  return arrCustomers;
}
```

**usando a convenção de nomes?**

- [ ] Apenas a versão GetAllCustomers faz sentido
- [ ] Ambas estão erradas já que não seguem a convenção de nomes.
- [x] Não há qualquer diferença.
- [ ] Apenas a versão GetCustomers faz sentido.

## Pergunta 19

**Que standard RPC (Remote Procedure Call) é utilizado pelos SOAP Web Services?**

- [ ] TCP (Transmission Control Protocol).
- [ ] WSDL (Web Service Description Language).
- [x] SOAP (Simple Object Access Protocol).
- [ ] Nenhuma das outras opções.

## Pergunta 20

**O que é um canal criado dentro de um sistema de mensagens?**

- [ ] Nenhuma das outras opções.
- [ ] Não é mais do que um ficheiro para partilha de informação entre aplicações.
- [ ] Não é mais do que uma diretoria para partilha de informação entre aplicações.
- [x] É um tópico de "conversação" para troca de informação entre aplicações.
