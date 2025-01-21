# Tópicos Avançados de Engenharia de Software

## Archive_1

### Pergunta 1

Um sistema de ar condicionado liga-se sempre que a temperatura baixa dos 18°C e sempre que a temperatura sobe acima dos 25°C. O sistema mantém-se desligado para as restantes temperaturas possíveis. Como valores possíveis consideremos apenas valores inteiros sem qualquer outra restrição numérica. Considerando que está a utilizar a técnica de testes de software "Boundary Value Analysis" qual das seguintes respostas prevê a cobertura mínima dos valores a testar?

Select one:

- [ ] a. -1, 0, 17, 18, 19, 24, 25, 26, 100, 101
- [ ] b. 17, 18, 19, 24, 25, 26
- [ ] c. 18, 19, 24, 25
- [ ] d. 17, 18, 25, 26

### Pergunta 2

Das técnicas apresentadas, qual delas é uma técnica de testes de software do tipo Black Box.

Select one:

- [ ] a. Partition Equivalence
- [ ] b. Boundary Value Analysis
- [ ] c. Nenhuma
- [ ] d. Ambas

### Pergunta 3

Segundo Pettichord deverá haver um foco em 5 categorias ao recorrer a técnicas de teste. Quais são essas 5 categorias?

Select one:

- [ ] a. Testers, Coverage, Potential Problems, Activities e Evaluation
- [ ] b. Black Box, White Box, Testers, Tests e Regression
- [ ] c. Unit Tests, Integration Tests, System Tests, Acceptance Tests e Real Users
- [ ] d. Testers, Tests, Potencial Outcomes, Tasks e Results

### Pergunta 4

Um sistema de ar condicionado liga-se sempre que a temperatura baixa dos 18°C e sempre que a temperatura sobe acima dos 25°C. O sistema mantém-se desligado para as restantes temperaturas possíveis. Como valores possíveis consideremos apenas valores inteiros sem qualquer outra restrição numérica. Considerando que está a utilizar a técnica de testes de software "Equivalence Partitions" qual das seguintes respostas prevê a cobertura de todas as partições?

Select one:

- [ ] a. 12, 16, 22
- [ ] b. 24, 27, 17
- [ ] c. 22, 23, 24
- [ ] d. 14, 15, 19

### Pergunta 5

Quais das seguintes técnicas são técnicas de "Black Box Testing"?

Select one or more:

- [ ] a. Equivalence Partitioning
- [ ] b. Boundary Value Analysis
- [ ] c. Decision Testing
- [ ] d. Statement Testing

### Pergunta 6

No "Manifesto for Agile Software Development" os seus 17 signatários assumiram que valorizavam mais alguns aspetos em relação a outros. Quais são os mais valorizados?

Select one or more:

- [ ] a. Individuals and interactions
- [ ] b. Comprehensive documentation
- [ ] c. Customer collaboration
- [ ] d. Processes and tools
- [ ] e. Contract negotiation
- [ ] f. Working software
- [ ] g. Following a plan
- [ ] h. Responding to change

### Pergunta 7

Uma das práticas mais conhecidas que foi introduzida pelo Extreme Programming é o "Test-First Programming". Indique qual das seguintes afirmações descreve com maior exatidão esta conhecida prática.

- [ ] a. Escrever um teste automatizado antes de escrever código.
- [ ] b. Endereçar problemas de âmbito, permitindo apresentar apenas os testes automatizados aos clientes.
- [ ] c. Reduzir o número de testes de software necessários.
- [ ] d. Promover alternativas aos testes de aceitação.

### Pergunta 8

Uma das práticas mais conhecidas que foi introduzida pelo Extreme Programming é o "Pair Programming". Indique qual das seguintes afirmações não é uma vantagem associada a esta prática.

- [ ] a. Todo o código é escrito por 2 pessoas que se sentam numa única máquina.
- [ ] b. O diálogo entre os 2 programadores permite, para além, de programar, analisar, desenhar e testar o código.
- [ ] c. Ao ter uma equipa de 2 pessoas é possível dividir melhor o trabalho permitindo que 1 pessoa se foque mais numa determinada funcionalidade e a outra pessoa noutra funcionalidade.
- [ ] d. É a prática que permite clarificar ideias e garantir que ambos os programadores se apoiam mutuamente.

### Pergunta 9

Em Extreme Programming (XP) estão previstos espaços temporais que são considerados os ciclos e/ou iterações de desenvolvimento. Indique a opção que apresenta os previstos por Kent Beck.

- [ ] a. Horário, Diário e Semanal.
- [ ] b. Diário, Semanal e Mensal.
- [ ] c. Diário, Semanal e Trimestral.
- [ ] d. Semanal, Mensal e Anual.

### Pergunta 10

Quais são os artefactos do "Scrum"?

Select one:

- [ ] a. Sprint Planning, Sprint, Daily Scrum, Sprint Review e Sprint Retrospective
- [ ] b. Product Backlog, Sprint Backlog e Product Increment
- [ ] c. Product Backlog, Sprint Backlog, Daily Chart, Demo e Feedback
- [ ] d. Product Backlog Event, Sprint Backlog Event, Monitoring Charts Update e Product Increment Demo

### Pergunta 11

Que responsabilidades (accountabilities) existem numa Scrum Team?

Select one:

- [ ] a. Scrum Master, Product Master e Developers
- [ ] b. Scrum Owner, Product Owner e Developers
- [ ] c. Scrum Master, Product Owner e Developers
- [ ] d. Sprint Owner, Sprint Product e Developers

### Pergunta 12

Depois de inicializar um novo repositório de Git e criar um ficheiro chamado taes-2020.html, qual dos seguintes comandos não funcionará?

- [ ] a. git add taes-2020.html
- [ ] b. git status
- [ ] c. git add.
- [ ] d. git commit -m "taes 2020 web file added"

### Pergunta 13

Qual o comando Git para criar num repositório do zero (novo e vazio)

- [ ] a. git init
- [ ] b. git start
- [ ] c. git create --empty
- [ ] d. git clone null

### Pergunta 14

Qual das seguintes keywords permite que o mesmo cenário possa ser executado para vários conjuntos de dados?

- [ ] a. Scenario outline
- [ ] b. Scenario
- [ ] c. Given
- [ ] d. Feature

### Pergunta 15

Dado o seguinte extrato de pseudo-código indique os casos de teste necessários para atingir 100% de statement coverage?

```text
SE idade < 25 E sexo = masculino E NOT (casado) ENTAO
  premium = premium + 1500
SENAO
  SE casado OU sexo = feminino ENTAO
    premium premium - 200
  SE idade > 45 E idade < 65 ENTAO
    premium = premium - 100
FIM
```

### Pergunta 16

*"The most efficient and effective method of conveying information to and within a development team is face-to-face conversation."* é um dos princípios que suportam o Agile Manifesto.

Explique em que medida é que o Scrum dá reposta a este princípio.

### Pergunta 17

O Extreme Programming (XP) é considerado uma metodologia ágil.
O Kanban é considerado uma metodologia ágil.
São metodologias nitidamente distintas e cada uma emprega, entre outros aspetos, um conjunto de práticas muito bem definido.
Enumere os aspetos que têm em comum e que permitem que possam ser ambas consideradas metodologias ágeis.
