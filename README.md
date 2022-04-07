## Quick description

This is the official repository of the 4th EW.IT code challenge. Which is a Producer/Consumer Application where you can manually view and recommend cryptos on the Producer side & plot charts and manage your recommendation wallet on the Consumer side.

# FIXME: REMOVE TEMPLATE FROM PREVIOUS CHALLENGE BELOW

# Story: Sua própria carteira Crypto

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
