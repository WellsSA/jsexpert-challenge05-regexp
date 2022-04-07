# Dicas extras: Mineração de Dados Legislativos

### Sugestão de implementação

> Dica do Wells: Vale lembrar que nesse desafio você é livre pra criar a estrutura que quiser, a sugestão aqui é só uma consulta pro caso de você querer conferir se a ordem que você pensou em resolver o desafio faz sentido

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

4. feito o FluentAPI já com os testes, é só implementar o `textProcessorFacade` e chamar o arquivo de verdade, seguindo a mesma estrutura do projeto do módulo 06.

5. Lá no `index.js`, só um `console.log` com os dados formatados por você (rodando o arquivo oficial do desafio) já é o suficiente. (exatamente como no projeto do módulo 06 também)
