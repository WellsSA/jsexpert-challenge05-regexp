<!-- challenge information -->

[challengeguide]: https://wellssa.github.io/jsexpert-challenge-guide/

<!-- description links -->

[dadosabertosgov]: https://dados.gov.br/pagina/dados-abertos
[alesp]: https://www.al.sp.gov.br/
[dadosabertosalesp]: https://www.al.sp.gov.br/bases/
[okfn]: http://okfn.org
[projetoscsv]: http://www.al.sp.gov.br/bases/projetos/projeto-de-lei.csv
[csvdesafio]: https://github.com/WellsSA/jsexpert-challenge05-regexp/blob/master/docs/projeto-de-lei.csv

<!-- hints -->

[uber]: https://www.uber.com/
[airbnb]: https://www.airbnb.com/
[regex101]: https://regex101.com/
[todohighlight]: https://marketplace.visualstudio.com/items?itemName=wayou.vscode-todo-highlight

# Story: Mineração de Dados Legislativos

> Nota do Wells: Esse desafio faz parte de uma série de desafios e quaisquer informações adicionais e/ou ajuda que você precise, é só conferir aqui no [Guia oficial dos Desafios JS Expert][challengeguide]! Bons estudos e ótimo desafio! :rocket:

## Motivação

Com o objetivo de trazer cenários reais aplicando os conteúdos vistos no `módulo 06 - Expressões Regulares - RegExp`, a idéia é levar vocês a fazer um "CSV parser" customizado usando `Expressões Regulares` para obter as informações de dentro de um arquivo CSV, mas não só isso como também aplicar essas `Expressões Regulares` nas informações retornadas para extrair ainda mais informação de valor, formatação e padronização ao nosso código final, tudo isso enquanto usamos `TDD` na prática usando padrões de projeto como `Fluent API` e `Facade`, e também entendemos mais sobre a `validação de segurança de Expressões Regulares`!

## Idéia geral

A [Assembléia Legislativa de São Paulo (ALESP)][alesp], onde se organiza o poder legislativo estadual do Estado de São Paulo - que é onde se propõem e discutem as leis a entrarem ou não em vigor no estado -, seguindo os preceitos da [política de dados abertos][dadosabertosgov] do governo federal, disponibiliza os dados sobre a Legislação do Estado de São Paulo (como Proposições, Processos e demais informações que vocês podem ver no [Portal de dados abertos da ALESP][dadosabertosalesp]) para o público geral.

Resumindo essa questão dos Dados Abertos:

> "Qualquer pessoa pode livremente usá-los, reutilizá-los e redistribuí-los, estando sujeito a, no máximo, a exigência de creditar a sua autoria e compartilhar pela mesma licença." - Definição de Dados Abertos pela [Open Knowledge Foundation][okfn], mencionada em ambos os portais de Dados Abertos citados anteriormente.

Esses dados podem ser amplamente utilizados em diversos segmentos empresariais, especialmente os que oferecem Monitoramento Legislativo sobre o andamento de **Projetos de lei** e propostas do gênero que visem mudar a estrutura legal do Estado - que é o tipo de coisa que toda e qualquer empresa que lide com a Estrutura Urbana, Organização Social, Mobilidade e afins, como [Uber][uber], [AirBnB][airbnb], Yellow, e afins; precisa se preocupar constantemente -.

## O projeto

Pensando na importância dos dados mencionados a pouco, dentre esta vastidão de dados disponibilizados no [Portal de dados abertos da ALESP][dadosabertosalesp], usaremos como base o [CSV de Projetos de Lei][projetoscsv] para fazer uma aplicação que lê os projetos de lei presentes no CSV e extrai informações úteis sobre eles, facilitando a busca e exibição desses dados em outros portais no futuro.

### Etapa 1 - leitura do CSV

Usando `Expressões Regulares` e o `Projeto base feito em aula durante o módulo 06`, faça uma aplicação usando os padrões de projeto `Fluent API` e `Facade` que leia e extraia as informações presentes no [CSV de Projetos de Lei fornecido no desafio][csvdesafio] e as deixe prontas para o uso da aplicação.

<img width="967" alt="image" src="https://user-images.githubusercontent.com/41883467/162134824-f219a9a7-ae59-4bbb-93e8-88cbb3c141a6.png">

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

![image](https://user-images.githubusercontent.com/41883467/162134881-b8f3cbf1-455a-404f-86d3-a3b237391918.png)

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

## Requisitos do desafio

- [ ] Uso de TDD do início ao fim do projeto
- [ ] Testes Unitários e 100% de Code Coverage
- [ ] Uso de Expressões Regulares
- [ ] Validação de segurança de Expressões Regulares
- [ ] Uso do padrão `Fluent API` e também o padrão `Facade`

> Dica do Wells: parece difícil, mas é só se basear no **Projeto base feito em aula durante o módulo 06** que fica tranquilo, confia! :)

### Dicas

- Lembre-se que para trabalhar com `Expressões Regulares`, é possível testar elas em tempo real usando o site [Regex101][regex101], e lembre-se sempre que além das aulas e das anotações, o Google é sempre uma boa ferramenta.

  > Dica Wells do dia: Fazer o passo a passo usando TDD muito provavelmente vai deixar as coisas bem mais fáceis :)

- Para melhorar sua experiência de desenvolvimento, você pode usar a extensão [TODO Highlight][todohighlight] no VSCode, recebendo o auxilio visual para encontrar os `//TODO: comments`, assim:
  ![image](https://user-images.githubusercontent.com/41883467/153465555-f2daa3e0-5770-4139-8344-dd2b792e159e.png)

### Extras

- Dessa vez não tem desafio opcional, já que ele ficaria muito complexo, maaas, como sempre, para quem busca os "próximos passos" e um desafio ainda maior que o proposto, lá no arquivo `test/mock/valid.js` tem uma sessão de "Nota extra + Dica do Wells" que pode servir de base para um "desafio extra" - mas eu fortemente recomendo que você faça o desafio normal primeiro :)

### Arquitetura e onde trabalhar

```
project
│   README.md
│   package.json
│
└───docs
│   │  projeto-de-lei.csv
│
└───src
│   │  index.js
│   │  project.js
│   │  textProcessorFacade.js
│   │  textProcessorFluentAPI.js
│   │  util.js
│
└───test
│   │  project.test.js
│   │  textProcessorFluentAPI.test.js
│   │  util.test.js
│   │
│   └───mock
│   │   │   valid.js
│   │
│
```

### Sugestão de implementação

> Dica do Wells: Vale lembrar que nesse desafio você é livre pra criar a estrutura que quiser, a sugestão aqui é só um "quick start" pro caso de você querer conferir se a ordem que você pensou em resolver o desafio faz sentido

1. Faça o desafio do módulo 06 junto com o Erick, já que a estrutura do desafio vai ser praticamente a mesma

2. Para fazer a leitura do arquivo no `index.js`, a estrutura do desafio e a dica devem bastar

3. Talvez a maior dificuldade, que é a parte mais diferente, seja pensar nos métodos que ficarão no textProcessorFluentAPI, já que estamos trabalhando com um arquivo completamente diferente do visto em aula

- Pra essa parte do desafio, sinta-se livre pra ir descobrindo como dividir o CSV e pegar a informação
- Caso queira uma ajuda, aqui está o passo a passo de como foi feita a solução do desafio:
  - extractHeaders =>
    - entrada: mock (texto em `/mock/valid.js`)
    - saída:
    ```js
    {
      headers: 'título;link;autor;etapa;ementa;indexadoresnorma;',
      content: mock,
    };
    ```
  - extractContent =>
    - entrada: saída do extractHeaders
    - saída:
    ```js
    {
      headers: 'título;link;autor;etapa;ementa;indexadoresnorma;',
      content: [
        'Projeto de lei 584/2016;http://www.al.sp.gov.br/propositura?id=1322563;Jorge Wilson Xerife do Consumidor;PAUTA;Dispõe sobre a inclusão de cláusula nos contratos de adesão aos serviços de telefonia fixa, de telefonia móvel e de banda larga móvel, e dá outras providências.;CONTRATO, OBRIGATORIEDADE, CLÁUSULA, SERVIÇO, TELEFONIA MÓVEL, TELEFONIA FIXA, PRAZO, INCLUSÃO, RESCISÃO CONTRATUAL, LIBERAÇÃO;',
        'Projeto de lei 580/2016;http://www.al.sp.gov.br/propositura?id=1323286;Marcia Lia;PAUTA;Estabelece normas gerais para a realização de Concurso Público pela Administração Pública Direta e Indireta do Estado.;NORMAS, REALIZAÇÃO, CONCURSO PÚBLICO ESTADUAL, ESTADO DE SÃO PAULO, ADMINISTRAÇÃO PÚBLICA DIRETA E INDIRETA;',
        'Projeto de lei 545/2016;http://www.al.sp.gov.br/propositura?id=1322832;Roberto Morais, Itamar Borges;PAUTA;Altera a Lei nº 13.550, de 2009, que dispõe sobre a utilização e proteção da vegetação nativa do Bioma Cerrado no Estado de São Paulo.;',
      ],
    };
    ```
  - splitValues =>
    - entrada: saída do extractContent
    - saída:
    ```js
    {
      headers: [
        'título',
        'link',
        'autor',
        'etapa',
        'ementa',
        'indexadoresnorma',
      ],
      content: [
        [
          'Projeto de lei 584/2016',
          'http://www.al.sp.gov.br/propositura?id=1322563',
          'Jorge Wilson Xerife do Consumidor',
          'PAUTA',
          'Dispõe sobre a inclusão de cláusula nos contratos de adesão aos serviços de telefonia fixa, de telefonia móvel e de banda larga móvel, e dá outras providências.',
          'CONTRATO, OBRIGATORIEDADE, CLÁUSULA, SERVIÇO, TELEFONIA MÓVEL, TELEFONIA FIXA, PRAZO, INCLUSÃO, RESCISÃO CONTRATUAL, LIBERAÇÃO',
        ],
        [
          'Projeto de lei 580/2016',
          'http://www.al.sp.gov.br/propositura?id=1323286',
          'Marcia Lia',
          'PAUTA',
          'Estabelece normas gerais para a realização de Concurso Público pela Administração Pública Direta e Indireta do Estado.',
          'NORMAS, REALIZAÇÃO, CONCURSO PÚBLICO ESTADUAL, ESTADO DE SÃO PAULO, ADMINISTRAÇÃO PÚBLICA DIRETA E INDIRETA',
        ],
        [
          'Projeto de lei 545/2016',
          'http://www.al.sp.gov.br/propositura?id=1322832',
          'Roberto Morais, Itamar Borges',
          'PAUTA',
          'Altera a Lei nº 13.550, de 2009, que dispõe sobre a utilização e proteção da vegetação nativa do Bioma Cerrado no Estado de São Paulo.',
        ],
      ],
    };
    ```
  - mapRawObjects =>
    - entrada: saída do splitValues
    - saída:
    ```js
    [
      {
        título: 'Projeto de lei 584/2016',
        link: 'http://www.al.sp.gov.br/propositura?id=1322563',
        autor: 'Jorge Wilson Xerife do Consumidor',
        etapa: 'PAUTA',
        ementa:
          'Dispõe sobre a inclusão de cláusula nos contratos de adesão aos serviços de telefonia fixa, de telefonia móvel e de banda larga móvel, e dá outras providências.',
        indexadoresnorma:
          'CONTRATO, OBRIGATORIEDADE, CLÁUSULA, SERVIÇO, TELEFONIA MÓVEL, TELEFONIA FIXA, PRAZO, INCLUSÃO, RESCISÃO CONTRATUAL, LIBERAÇÃO',
      },
      {
        título: 'Projeto de lei 580/2016',
        link: 'http://www.al.sp.gov.br/propositura?id=1323286',
        autor: 'Marcia Lia',
        etapa: 'PAUTA',
        ementa:
          'Estabelece normas gerais para a realização de Concurso Público pela Administração Pública Direta e Indireta do Estado.',
        indexadoresnorma:
          'NORMAS, REALIZAÇÃO, CONCURSO PÚBLICO ESTADUAL, ESTADO DE SÃO PAULO, ADMINISTRAÇÃO PÚBLICA DIRETA E INDIRETA',
      },
      {
        título: 'Projeto de lei 545/2016',
        link: 'http://www.al.sp.gov.br/propositura?id=1322832',
        autor: 'Roberto Morais, Itamar Borges',
        etapa: 'PAUTA',
        ementa:
          'Altera a Lei nº 13.550, de 2009, que dispõe sobre a utilização e proteção da vegetação nativa do Bioma Cerrado no Estado de São Paulo.',
      },
    ];
    ```
  - mapProjects =>
    - entrada: saída do mapRawObjects
    - saída:
    ```js
    [
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
      {
        id: '1323286',
        numero: '580',
        ano: '2016',
        autores: [
          {
            nome: 'Marcia Lia',
          },
        ],
        url: 'http://www.al.sp.gov.br/propositura?id=1323286',
        indexadores: [
          'NORMAS',
          'REALIZAÇÃO',
          'CONCURSO PÚBLICO ESTADUAL',
          'ESTADO DE SÃO PAULO',
          'ADMINISTRAÇÃO PÚBLICA DIRETA E INDIRETA',
        ],
      },
      {
        id: '1322832',
        numero: '545',
        ano: '2016',
        autores: [{ nome: 'Roberto Morais' }, { nome: 'Itamar Borges' }],
        url: 'http://www.al.sp.gov.br/propositura?id=1322832',
        indexadores: [],
      },
    ];
    ```

## Submissão

1. Crie um fork deste repositório e modifique o README.md inserindo o seu nome no início do arquivo.

2. Instale as dependências usando `npm i`.

3. Implemente cada um dos arquivos esperados (com um `//@TODO: comment` no início)

4. Envie o link no canal `#desafios-jsexpert` da nossa comunidade no discord.

## Até quando?

Se você está pegando esse desafio na estréia, corre lá e envia pra gente até _Quarta-feira, 09 de março de 2022 (28/04/2022)_!

> Dica extra do Wells: Data de entrega curiosamente no dia do aniversário de 22 anos desse que vos fala, então se terminar o desafio no último dia, só vai ser aceito se mandar um parabéns no chat, hein? 😄 Bons estudos e ótimo desafio!
