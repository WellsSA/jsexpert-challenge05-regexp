[dadosabertosgov]: https://dados.gov.br/pagina/dados-abertos
[alesp]: https://www.al.sp.gov.br/
[dadosabertosalesp]: https://www.al.sp.gov.br/bases/
[okfn]: http://okfn.org
[projetoscsv]: http://www.al.sp.gov.br/bases/projetos/projeto-de-lei.csv
[uber]: https://www.uber.com/
[airbnb]: https://www.airbnb.com/
[csvdesafio]: https://github.com/WellsSA/jsexpert-challenge05-regexp/blob/master/docs/projeto-de-lei.csv

# Story: Mineração de dados legislativos

- Uso de Expressões Regulares
- Validação de segurança de Expressões Regulares
- Uso do padrão `Fluent API` e também o padrão `Facade`
- TDD na prática

Chegar mais próximo da vida real

- 100% de code coverage

## Antes de tudo

guia dos desafios

## Motivação

Com o objetivo de trazer cenários reais aplicando os conteúdos vistos no `módulo 06 - Expressões Regulares - RegExp`, a idéia é levar vocês a fazer um "CSV parser" customizado usando `Expressões Regulares` para obter as informações de dentro de um arquivo CSV, mas não só isso como também aplicar essas `Expressões Regulares` nas informações retornadas para extrair ainda mais informação de valor, formatação e padronização ao nosso código final, tudo isso enquanto usamos `TDD` na prática usando padrões de projeto como `Fluent API` e `Facade`, e também entendemos mais sobre a `validação de segurança de Expressões Regulares`!

## Idéia geral

A [Assembléia Legislativa de São Paulo (ALESP)][alesp], onde se organiza o poder legislativo estadual do Estado de São Paulo - resumidamente, onde se propõem e discutem as leis a entrarem ou não em vigor no estado -, seguindo os preceitos da [política de dados abertos][dadosabertosgov] do governo federal, disponibiliza os dados sobre a Legislação do Estado de São Paulo, bem como Proposições, Processos e demais informações que vocês podem ver no [Portal de dados abertos da ALESP][dadosabertosalesp] para o público geral.
Em outras palavras:

> "Qualquer pessoa pode livremente usá-los, reutilizá-los e redistribuí-los, estando sujeito a, no máximo, a exigência de creditar a sua autoria e compartilhar pela mesma licença." - Definição de Dados Abertos pela [Open Knowledge Foundation][okfn], mencionada em ambos os portais de Dados Abertos citados anteriormente.

Esses dados podem ser amplamente utilizados em diversos segmentos empresariais, especialmente os que oferecem Monitoramento Legislativo sobre o andamento de **Projetos de lei** e propostas do gênero que visem mudar a estrutura legal do Estado - que é o tipo de coisa que toda e qualquer empresa que lide com a Estrutura Urbana, Organização Social, Mobilidade e afins, como [Uber][uber], [AirBnB][airbnb], Yellow, e afins; precisa se preocupar constantemente -.

## O projeto

Pensando na importância dos dados mencionados a pouco, dentre esta vastidão de dados disponibilizados no [Portal de dados abertos da ALESP][dadosabertosalesp], usaremos como base o [CSV de Projetos de Lei][projetoscsv] para fazer uma aplicação que lê os projetos de lei presentes no CSV e extrai informações úteis sobre eles, facilitando a busca e exibição desses dados em outros portais no futuro.

### Etapa 1 - leitura do CSV

Usando `Expressões Regulares` e o `Projeto base feito em aula durante o módulo 06`, faça uma aplicação usando os padrões de projeto `Fluent API` e `Facade` que leia e extraia as informações presentes no [CSV de Projetos de Lei fornecido no desafio][csvdesafio] e as deixe prontas para o uso da aplicação.

## TODO: Inserir print aqui

#### Objetivo

Ler e deixar utilizáveis os campos `título`, `link`, `autor`, `etapa`, `ementa` e `indexadoresnorma`.
Objeto de exemplo:

```js
{
  título: 'Projeto de lei 584/2016',
  link: 'http://www.al.sp.gov.br/propositura?id=1322563',
  autor: 'Jorge Wilson Xerife do Consumidor',
  etapa: 'PAUTA',
  ementa:
    'Dispõe sobre a inclusão de cláusula nos contratos de adesão aos serviços de telefonia fixa, de telefonia móvel e de banda larga móvel, e dá outras providências.',
  indexadoresnorma:
    'CONTRATO, OBRIGATORIEDADE, CLÁUSULA, SERVIÇO, TELEFONIA MÓVEL, TELEFONIA FIXA, PRAZO, INCLUSÃO, RESCISÃO CONTRATUAL, LIBERAÇÃO',
}
```

#### Arquivos pertinentes:

- `index.js`: responsável por instanciar o `TextProcessorFacade`, ler o arquivo CSV e fornecer o texto contido no CSV à instância do `TextProcessorFacade`.
- `textProcessorFacade.js`: responsável por abstrair a execução do `TextProcessorFluentAPI` implementando um método `getProjectsFromCSV` que contém as chamadas ao Fluent API em ordem.
- `textProcessorFluentAPI.js`: responsável por implementar a Fluent API separando em etapas o processo de leitura e formatação do arquivo.

### Etapa 2 - extração de dados úteis

Usando `Expressões Regulares` e o `TextProcessorFluentAPI` feito na Etapa 1, crie uma classe que receba como valores os campos "raw" (`título`, `link`, `autor`, `etapa`, `ementa` e `indexadoresnorma`) e extraia informações úteis desses campos, retornando no construtor uma instância formatada com informações pertinentes.

## TODO: Inserir print aqui

#### Objetivo

Criar uma classe que receba no construtor os campos `título`, `link`, `autor`, `etapa`, `ementa` e `indexadoresnorma` e retorne uma instância com os campos `id`, `numero`, `ano`, `autores`, `url` e `indexadores`.

Objeto de exemplo:

```js
{
  id: '1322563',
  numero: '584',
  ano: '2016',
  autores: [
    {
      nome: 'Jorge Consumidor',
    },
  ],
  url: 'http://www.al.sp.gov.br/propositura?id=1322563',
  indexadores: [
    'CONTRATO',
    'OBRIGATORIEDADE',
    'CLÁUSULA',
    'SERVIÇO',
    'TELEFONIA MÓVEL',
    'TELEFONIA FIXA',
    'PRAZO',
    'INCLUSÃO',
    'RESCISÃO CONTRATUAL',
    'LIBERAÇÃO',
  ],
},
```

#### Arquivos pertinentes:

- `textProcessorFluentAPI.js`: responsável por implementar na Fluent API um método que chama a classe de mapeamento.
- `project.js`: responsável por implementar a classe `Project` conforme mencionado acima.

# FIXME: REMOVE TEMPLATE FROM PREVIOUS CHALLENGE BELOW

# Story: Mineração de dados legislativos

## Motivação

Como vocês sabem, o `módulo 05 - Advanced Javascript Data Types` apresenta estruturas tão sênior que os nossos casos de uso pra elas nas aulas são de dentro do próprio **código fonte do NodeJS**, e após conversar com alguns alunos sobre os últimos desafios, decidimos aplicar as estruturas vistas em aula em contextos onde elas podem brilhar!!

## Idéia geral

Este desafio consiste em um sistema de recomendação manual de criptomoedas, juntamente com um sistema de carteiras de recomendações personalizadas para cada usuário, onde é possível analisar informações sobre as criptos recomendadas e manter elas na carteira ou não - ou seja, é uma típica _Producer/Consumer Application_, como você pode ver na imagem a seguir:

![image](https://user-images.githubusercontent.com/41883467/153203842-8889bbd8-e9e4-496c-b8ae-d9c6c6ec57e3.png)

## Entendendo o ecossistema

### Provider

O Provider é o servidor que servirá como a API do sistema, e deverá ser executado antes de todos os outros serviços atráves do `npm run provider`. O comando mencionado sobe um servidor mock com `json-server`, trazendo dados na estrutura de uma uma API de criptomoedas real com informações atualizadas do dia 02/02/2021.

### Producer

> Dependências: Provider

O Producer será o nosso servidor Websocket principal da aplicação, e também será responsável por rodar a CLI onde é possível listar informações sobre as cryptos através do provider e enviar recomendações de cryptos aos Consumers conectados.

### Consumer

> Dependências: Producer

O Consumer será o nosso cliente Websocket que receberá as cryptos recomendadas pelo Producer, e irá rodar a CLI responsável pela visualização gráfica de histórico das cryptos recomendadas, bem como a gestão da carteira do Consumer em execução - note que podemos ter vários consumers rodando simultaneamente com carteiras locais diferentes.

## Funcionalidades

### Processo 01 (Lista de Crypto | Producer)

- Iniciar o servidor WS principal
- Listar as crypto moedas
- iniciar o mainLoop da CLI
  - Listar mais informações
  - Selecionar uma das currencies exibidas
    - quando selecionar, emitir evento para o _Processo 02_

### Processo 02 (Wallet | Consumer)

- Mostrar graficamente a crypto moeda selecionada atual
- Ouvir o evento de seleção de moeda para dicionar a moeda na Wallet
  dicionar a moeda na Wallet
- Selecionar uma das moedas na Wallet para ser a moeda representada no gr[áfico
- Excluir uma das moedas na Wallet

## Estruturas esperadas

- Generators, Iterators e Async Iterators
- Symbol
- Map e Set

### Requisitos do desafio

1. Suba o ambiente de desenvolvimento, executando os seguintes comandos em terminais diferentes: `npm run provider`, `npm run producer:dev`, `npm run consumer:dev`.

2. Usando o código fornecido do desafio, analise e implemente as partes que precisam de implementação usando o conteúdo visto em aula.

   > Nota: Os trechos que necessitam de modificação estão sinalizados com `//TODO: comments`. Veja a sessão de dicas abaixo para saber mais sobre.

3. Garanta que após a aplicação das estruturas, a aplicação execute conforme o vídeo abaixo:
   > Nota: Considere `npm start` como `npm run producer` e `npm run client` como `npm run consumer` :)

https://user-images.githubusercontent.com/41883467/153467415-9c8091d2-97dc-4fcc-9edf-55b36bd098a3.mp4

4. (Desafio opcional) Caso queira, valide se é possível a implementação com WeakSet e WeakMap, implemente e/ou deixe um comentário sobre no código.

5. (Desafio opcional) Caso queira, tente aplicar alguns testes no desafio e entender o funcionamento de cada trecho mais a fundo.

> Nota: Não se preocupe em alterar o código na CLI ou na implementação de websockets, já tivemos e/ou teremos desafios para vocês se aprofundarem nessa parte
> Nota da nota: Caso queira, alterações em quaisquer partes do fluxo são bem vindas, desde que sejam usadas as estruturas mencionadas na sessão de _"Estruturas esperadas"_.

### Dicas

- Lembre-se que esse módulo apresenta estruturas complexas, então tente entender as responsabilidades de cada uma para saber onde aplicar, e não se esqueça de procurar exemplos de implementação no próprio código do desafio ou em desafios anteriores, caso necessário. Fica por sua conta e criatividade montar o quebra cabeça e ir descobrindo por onde começar a implementar cada função.

  > Dica Wells do dia: Pode sair Mockando e implementando as funções para ver a CLI funcionando antes de ir implementando as estruturas de cara. Entender o fluxo da aplicação e o que deve ser retornado antes de de fato implementar as funções facilita muito a vida, confia :D

- Para melhorar sua experiência de desenvolvimento, você pode usar a extensão [TODO Highlight](https://marketplace.visualstudio.com/items?itemName=wayou.vscode-todo-highlight) no VSCode, recebendo o auxilio visual para encontrar os `//TODO: comments`, assim:
  ![image](https://user-images.githubusercontent.com/41883467/153465555-f2daa3e0-5770-4139-8344-dd2b792e159e.png)

### Extras

- [ ] Desafio opcional: Caso queira, valide se é possível a implementação com WeakSet e WeakMap, implemente e/ou deixe um comentário sobre no código.
- [ ] Desafio opcional: Caso queira, tente aplicar alguns testes no desafio e entender o funcionamento de cada trecho mais a fundo.

### Arquitetura e onde trabalhar

```
project
│   README.md
│   package.json
│
└───src
│   │  index.js
│   │  consumer-cli.js
│   │  producer-cli.js
│   │  producer-server.js
│   │  provider-server.json
│   │
│   └───config
│   │   │   language.js
│   │   │   terminal.js
│   │
│   └───entity
│   │   │   Crypto.js
│   │   │   User.js
│   │   │   Users.js
│   │
│   └───repository
│   │   │   CryptoRepository.js
│   │
│   └───service
│   │   │   IncomeService.js
│   │
│   └───util
│   │   │   Api.js
│   │   │   CustomTerminal.js
│
```

### Checklist features

- [ ] Deve implementar a estrutura esperada em `util/CustomTerminal.js`

- [ ] Deve implementar os métodos existentes em `service/CryptoService.js`

- [ ] Deve implementar a estrutura esperada no arquivo `entity/User.js`

- [ ] Deve implementar as estruturas esperadas no arquivo `entity/Users.js`

## Submissão

1. Crie um fork deste repositório e modifique o README.md inserindo o seu nome no início do arquivo.

2. Instale as dependências usando `npm i`.

3. Implemente cada uma das funções marcadas com um `//@TODO: comment`

4. Envie o link no canal `#desafios-jsexpert` da nossa comunidade no discord.

## Até quando?

Se você está pegando esse desafio na estréia, corre lá e envia pra gente até _Quarta-feira, 09 de março de 2022 (09/03/2022)_!
