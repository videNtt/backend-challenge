# Desafio Técnico — Distribuição de contratos

## Bem-vindo ao Grupo Aval (Toledo Piza Advogados Associados) 🏢

O **Grupo Aval / Toledo Piza Advogados Associados** é uma empresa brasileira com mais de 45 anos de experiência especializada em serviços de recuperação de crédito e soluções financeiras.

Este desafio é a porta de entrada para fazer parte desse time. Ele foi desenhado para refletir problemas reais do nosso dia a dia: sistemas distribuídos, tempo real, experiência de usuário e arquitetura bem pensada.

Não esperamos perfeição — esperamos raciocínio claro, código limpo e decisões justificadas. Mostre como você pensa e como você constrói.

---

## 1. Visão geral

Construa uma solução web para gerenciamento de devedores, contratos, parcelas e telefones, incluindo uma funcionalidade de distribuição de registros baseada em critérios de negócio e a exportação de parcelas em aberto.

A solução deverá ser desenvolvida utilizando boas práticas de programação, organização de código, modelagem de banco de dados, validações, segurança e preocupação com desempenho.

Este teste técnico tem como objetivo avaliar conhecimentos práticos de desenvolvimento de aplicações web utilizando **.NET, C#, SQL Server, HTML, CSS, JavaScript e AJAX**, além da capacidade de análise e implementação de regras de negócio.

Importante: o objetivo não é avaliar apenas se o candidato consegue implementar telas de CRUD. A análise da modelagem, arquitetura, SQL, Stored Procedures, regras de negócio e decisões técnicas faz parte da avaliação.

---

## 2. Stack

### Obrigatória
A solução deverá utilizar:

- C#;
- .NET Framework ou .NET Core;
- Visual Studio;
- SQL Server;
- HTML5;
- CSS;
- JavaScript;
- AJAX.

### Opcional

O candidato poderá utilizar bibliotecas e frameworks adicionais, desde que informe no README quais foram utilizados e o motivo da escolha.

Exemplos:

- ASP.NET MVC;
- ASP.NET Core MVC;
- ASP.NET Web API;
- Razor Pages;
- Entity Framework;
- Dapper;
- JQuery;
- Bootstrap;
- outras bibliotecas de apoio.

```
A utilização dessas tecnologias adicionais não é obrigatória.
```
---

## 3. Objetivo da aplicação

A aplicação deverá permitir o gerenciamento das seguintes entidades:

Devedor
   ├── Contratos
   │      └── Parcelas
   │
   └── Telefones

Além dos cadastros, deverá existir uma tela de distribuição de devedores/contratos/parcelas/telefones.

```
A lógica principal da distribuição deverá ser implementada em Stored Procedure no SQL Server.
```` 

---

## 4. Cadastros

### Devedores

Implementar um CRUD completo de devedores.

|Campo					|Tipo	|Obrigatório|
|CPF					|Texto	|Sim		|
|Nome					|Texto	|Sim		|
|Data de nascimento		|Data	|Sim		|
|Sexo					|M/F	|Sim		|

Funcionalidades
A tela deverá permitir:

- Cadastrar devedor;
- Alterar devedor;
- Consultar devedor;
- Excluir devedor;
- Pesquisar por CPF;
- Pesquisar por nome;
- Validar CPF;
- Impedir CPF duplicado;
- Validar campos obrigatórios.
- O CPF deverá ser armazenado no banco somente com os números.

```
A máscara poderá ser aplicada na apresentação.
```
### Contratos

Cada devedor poderá possuir um ou mais contratos.

|Campo					|Tipo		|Obrigatório|
|Devedor				|FK			|Sim		|
|Número do contrato		|Texto		|Sim		|
|Produto				|Texto		|Sim		|
|Plano					|Inteiro	|Sim		|

Funcionalidades
Implementar:

- Cadastrar contrato;
- Alterar contrato;
- Consultar contrato;
- Excluir contrato;
- Pesquisa por número do contrato;
- Pesquisa por CPF;
- Pesquisa por nome;
- Filtro por produto;
- Filtro por plano.

```
O número do contrato deverá ser único.
```

### Parcelas

Cada contrato deverá possuir uma ou mais parcelas.

|Campo					|Tipo		|Obrigatório|
|Contrato				|FK			|Sim		|
|Número da parcela		|Inteiro	|Sim		|
|Data de vencimento		|Data		|Sim		|
|Valor da parcela		|Decimal	|Sim		|
|Situação da parcela	|Texto/Enum	|Sim		|
|Data de devolução		|Data		|Não		|

Situações
A aplicação deverá contemplar, no mínimo:

- "A" = Aberta;
- "P" = Paga;
- "D" = Devolvida;
- "C" = Cancelada.

```
O candidato poderá utilizar outras situações, desde que documente a decisão.
```

Regras:
1. Uma parcela pertence a um contrato.
2. O número da parcela não poderá se repetir dentro do mesmo contrato.
3. O valor deverá ser maior que zero.
4. A data de devolução poderá ser nula.
```
Somente parcelas consideradas em aberto deverão participar da distribuição/exportação.
````

### Telefones

Cada devedor poderá possuir um ou mais telefones.

|Campo		|Tipo		|Obrigatório|
|Devedor	|FK			|Sim		|
|DDD		|Inteiro	|Sim		|
|Número		|Inteiro	|Sim		|
|WhatsApp	|Texto/Enum	|Sim		|
|Prioridade	|Inteiro	|Sim		|

Funcionalidades
Implementar:

- Cadastrar telefone;
- Alterar telefone;
- Consultar telefone;
- Excluir telefone;
- Pesquisa por número;

````
Quanto menor o número da prioridade, maior a prioridade do telefone.
```

---

## 5. Tela de Distribuição

A aplicação deverá possuir uma tela onde o usuário consiga informar critérios para realizar a distribuição de registros.

A distribuição deverá considerar:

- Contrato;
- Produto;
- Plano;
- Parcela;
- Faixa de atraso;
- Vencimento;
- Telefone;
- Prioridade.

Regra importante:

```
A lógica de distribuição deverá ser implementada em uma Stored Procedure no SQL Server.
A aplicação não deverá concentrar a regra principal de distribuição em C#.
A aplicação deverá apenas receber os parâmetros informados pelo usuário, chamar a Stored Procedure e apresentar o resultado.
```
---

## 6. Critérios da distribuição

### 6.1. Contrato
A tela deverá permitir filtrar por:

Produto;
Plano.
Exemplo:

Produto: Consignado
Plano: Plano A

### 6.2. Parcela
A distribuição deverá permitir trabalhar com:

faixa de atraso;
data de vencimento.
Exemplo:

Faixa de atraso:
0 a 30 dias

Data de vencimento:
01/08/2026 até 31/08/2026

Os dias de atraso poderão ser calculados considerando a data atual:

Dias de atraso = Data atual - Data de vencimento

Somente parcelas em aberto deverão ser consideradas.

### 6.3. Telefone
A distribuição deverá considerar a prioridade dos telefones.

Exemplo:

Telefone A → Prioridade 1
Telefone B → Prioridade 2
Telefone C → Prioridade 3

O telefone de maior prioridade deverá ser considerado antes dos demais.

---

## 7. Análise da regra de distribuição

O candidato deverá analisar os requisitos apresentados e definir uma estratégia de distribuição.

Não é necessário que este README forneça toda a regra pronta.

Faz parte do teste avaliar a capacidade do candidato de:

- Interpretar requisitos;
- Identificar ambiguidades;
- Tomar decisões técnicas;
- Documentar premissas;
- Implementar a solução;
- Justificar as decisões tomadas.

O candidato deverá documentar no próprio README:

1. Como determinou quais parcelas são elegíveis;
2. Como tratou as faixas de atraso;
3. Como aplicou os filtros de produto/plano;
4. Como selecionou os telefones;
5. Como tratou diferentes prioridades;
6. Como evitou registros duplicados;
7. Como tratou execuções simultâneas da distribuição.

---

## 8. Concorrência

Considere o seguinte cenário:

Operador A → executa distribuição
Operador B → executa distribuição simultaneamente

A solução deverá considerar como evitar que a mesma informação seja distribuída indevidamente para os dois operadores.

O candidato deverá explicar no README sua estratégia para tratar:

- Concorrência;
- Transações;
- Consistência;
- Duplicidade;
- Rollback em caso de erro.
```
Não é obrigatório implementar uma solução complexa, mas a decisão técnica deverá ser documentada.
````

---

## 9. Stored Procedure

A lógica de distribuição deverá ser executada através de uma Stored Procedure.

A aplicação deverá passar os parâmetros necessários para a procedure.

Exemplo conceitual:

EXEC dbo.sp_Distribuir
     @Produto = 'Consignado',
     @Plano = 'Plano A',
     @DiasAtrasoInicial = 0,
     @DiasAtrasoFinal = 30,
     @DataVencimentoInicial = '2026-08-01',
     @DataVencimentoFinal = '2026-08-31';

O nome, parâmetros e implementação ficam a critério do candidato.

A procedure deverá ser entregue junto com o projeto.

```A Stored Procedure deve ser nomeada no seguinte padrão: ``` `dbo.sp_DistribuirYYYYMMDDINICIAIS`

Onde `YYYYMMDD` siginifica o ano, mês e dia e `INICIAIS` significa as iniciais do seu nome completo.

Exemplo:

Data da criação: 11/09/2026
Candidato: Fulano da Silva Junior
Stored Procedure: `dbo.Distribuir20260911FSJ``

---

## 10. Resultado da distribuição

Após executar a distribuição, a aplicação deverá apresentar os registros encontrados.

O resultado deverá conter, no mínimo:

- CPF
- Nome
- DataNascimento
- Sexo
- NumeroContrato
- Produto
- Plano
- NumeroParcela
- DataVencimento
- DDD
- Numero
- WhatsApp
- Prioridade

---

## 11. AJAX
As operações de consulta e distribuição deverão utilizar AJAX sempre que tecnicamente adequado.

Exemplo de fluxo esperado:

Browser
   ↓
JavaScript
   ↓
AJAX
   ↓
Controller / API
   ↓
Service
   ↓
Repository
   ↓
Stored Procedure
   ↓
SQL Server

Poderão ser utilizados:

Fetch API;
XMLHttpRequest;
jQuery AJAX.
A escolha deverá ser documentada.

---

## 12. Exportação

A aplicação deverá permitir exportar as parcelas em aberto para:

TXT; ou
CSV.
O arquivo deverá utilizar o seguinte layout:

CPF;Nome;Contrato;Produto;Plano;Parcela;Vencimento;DDD;Telefone;WhatsApp;Prioridade

Exemplo:

11111111111;João da Silva;123456;Consignado;24;3;10/08/2026;11;999999999;Sim;1
22222222222;Maria Souza;654321;Consignado;60;5;15/08/2026;11;988888888;Sim;1
22222222222;Maria Souza;654321;Consignado;60;5;15/08/2026;11;977777777;Não;2

Regras
1. Separador: ;
2. Uma linha por registro;
3. Não utilizar separador de milhar;
4. Datas deverão possuir formato consistente;
5. O encoding deverá ser informado no README;
6. Não deverão ser exportadas parcelas que não estejam em aberto.

O cabeçalho deverá respeitar exatamente:
```
CPF;Nome;Contrato;Produto;Plano;Parcela;Vencimento;DDD;Telefone;WhatsApp;Prioridade
````

---

## 13. Banco de dados

O candidato deverá entregar scripts SQL para criação do banco.

A modelagem deverá contemplar, no mínimo, as seguintes entidades:

Devedores
Contratos
Parcelas
Telefones

Uma estrutura conceitual esperada é:

Devedores
---------
Id
CPF
Nome
DataNascimento
Sexo

Contratos
---------
Id
DevedorId
NumeroContrato
Produto
Plano

Parcelas
--------
Id
ContratoId
NumeroParcela
DataVencimento
ValorParcela
Situacao
DataDevolucao

Telefones
---------
Id
DevedorId
DDD
Numero
WhatsApp
Prioridade

A implementação da modelagem fica a critério do candidato.

### 13.1 Banco de dados — requisitos

A solução deverá considerar:

- Primary Keys;
- Foreign Keys;
- Índices;
- Constraints;
- Integridade referencial;
- Tipos de dados adequados;
- Regras de unicidade;
- Relacionamentos;
- Performance das consultas.

O candidato deverá justificar os principais índices criados.

### 13.2 Massa de testes

O projeto deverá conter um script para criação de massa de testes.

A massa deverá ser suficiente para demonstrar o funcionamento da aplicação.

Como referência, recomendamos:

- Pelo menos 20 devedores;
- Alguns devedores com múltiplos contratos;
- Alguns contratos com múltiplas parcelas;
- Alguns devedores com múltiplos telefones;
- Diferentes prioridades de telefone;
- Diferentes produtos;
- Diferentes planos;
- Parcelas abertas;
- Parcelas pagas;
- Parcelas devolvidas;
- Parcelas canceladas;
- Parcelas em diferentes faixas de atraso.

```
A massa de testes deverá permitir validar adequadamente a regra de distribuição.
```

---

## 14. Validações

A aplicação deverá possuir validações no frontend e backend.

Exemplos:

- CPF obrigatório;
- CPF válido;
- CPF não duplicado;
- Nome obrigatório;
- Data de nascimento válida;
- Sexo válido;
- Contrato obrigatório;
- Contrato único;
- Produto obrigatório;
- Plano obrigatório;
- Número da parcela obrigatório;
- Parcela única dentro do contrato;
- Valor maior que zero;
- DDD válido;
- Telefone válido;
- Prioridade válida.

```
Validações implementadas apenas em JavaScript não são suficientes. 
As regras importantes deverão ser protegidas também no backend e/ou banco de dados.
```

---

## 15. Performance

Considere que, em um cenário real, a tabela de parcelas poderá possuir milhões de registros.

A solução deverá evitar consultas desnecessariamente pesadas.

O candidato deverá considerar:

- Índices;
- Filtros;
- Joins;
- Paginação;
- Consultas parametrizadas;
- Seleção somente das colunas necessárias;
- Evitar SELECT *;
- Evitar N+1 queries;
- Utilização adequada do SQL Server;
- Stored Procedures quando apropriado.

No README, responda:
```
Se a tabela de parcelas possuísse 10 milhões de registros, quais índices você criaria para melhorar a consulta da distribuição e por quê?
```

---

## 16. Arquitetura

Não será exigida uma arquitetura específica.

Entretanto, será avaliada a organização da solução.

Por exemplo:

Web
 ├── Controllers
 ├── Views
 ├── Models
 └── wwwroot

Application
 ├── Services
 ├── DTOs
 └── Interfaces

Infrastructure
 ├── Repositories
 └── Database

O candidato poderá utilizar outra estrutura, desde que seja coerente e justifique suas decisões.

---

## 17. Entregáveis

Entregáveis
O repositório deverá conter:

- Código-fonte completo;
- Solution do Visual Studio;
- Scripts SQL;
- Stored Procedures;
- Massa de testes;
- README atualizado;
- Instruções de instalação;
- Instruções de configuração;
- Arquivo TXT/CSV de exemplo.

Sugestão de estrutura:

/
├── README.md
├── src/
│   └── ...
│
├── database/
│   ├── 001-create-database.sql
│   ├── 002-create-tables.sql
│   ├── 003-create-indexes.sql
│   ├── 004-create-procedures.sql
│   └── 005-seed.sql
│
├── docs/
│   └── ...
│
└── samples/
    └── parcelas-abertas.csv

A estrutura acima é apenas uma sugestão.

---

## 18. README do candidato

Além deste documento, o candidato deverá complementar o README do projeto com:

Tecnologias utilizadas
Descrever:

- versão do .NET;
- versão do SQL Server;
- bibliotecas utilizadas;
- frameworks utilizados.
- Arquitetura
Explicar a arquitetura escolhida e o motivo.

Banco de dados
Explicar:

- principais tabelas;
- relacionamentos;
- índices;
- constraints.
- Distribuição

Explicar detalhadamente:

- critérios utilizados;
- Regras implementadas;
- Stored Procedure;
- Tratamento de concorrência;
- Decisões tomadas.

Exportação
Explicar:

- Formato escolhido;
- Encoding;
- Formato das datas;
- Estratégia de geração do arquivo;
- Decisões técnicas;
- Descrever as principais decisões e eventuais limitações.

---

## 19. README do candidato

Os itens abaixo não são obrigatórios, mas poderão ser considerados diferenciais:

- Testes unitários;
- Testes de integração;
- Docker;
- Docker Compose;
- Entity Framework;
- Dapper;
- Swagger/OpenAPI;
- Dependency Injection;
- Async/await;
- Logging;
- Tratamento global de exceções;
- Paginação server-side;
- Filtros dinâmicos;
- Responsividade;
- Autenticação;
- Autorização;
- Auditoria;
- Processamento assíncrono para grandes exportações.

---

## 20. O que será observado
Além dos requisitos funcionais, serão observados:

- Qualidade do código;
- Legibilidade;
- Organização;
- Nomenclatura;
- Modelagem;
- Conhecimento de SQL Server;
- Qualidade das queries;
- Qualidade das Stored Procedures;
- Tratamento de erros;
- Validações;
- Segurança;
- Performance;
- Experiência do usuário;
- Capacidade de análise;
- Clareza das decisões técnicas;
- Capacidade de explicar a própria solução.

```
Não é necessário utilizar a tecnologia mais sofisticada disponível.
Uma solução simples, consistente, bem estruturada e bem justificada poderá ser melhor avaliada do que uma solução excessivamente complexa.
````

---

## 21. Critério de transparência
Não será avaliado apenas o resultado final.

Durante a avaliação poderão ser considerados:

- Histórico de commits;
- Organização dos commits;
- Mensagens de commit;
- Documentação;
- Decisões técnicas;
- Capacidade de explicar o código desenvolvido.

```
Recomenda-se utilizar commits pequenos e descritivos durante o desenvolvimento.
```

Exemplo:

feat: cria estrutura inicial do projeto
feat: implementa cadastro de devedores
feat: implementa cadastro de contratos
feat: implementa cadastro de parcelas
feat: implementa cadastro de telefones
fix: corrige bug no cadastro de contratos
feat: adiciona procedure de distribuição
feat: adiciona tela de distribuição
fix: corrige erro na tela de distribuição
feat: adiciona exportação de parcelas
docs: adiciona instruções de instalação

---

## 22. Entrega
O candidato deverá disponibilizar o projeto em um repositório Git.

O repositório deverá permitir que outra pessoa consiga:

- Clonar o projeto;
- Criar o banco;
- Executar os scripts;
- Configurar a aplicação;
- Executar o projeto;
- Utilizar a massa de testes;
- Testar a distribuição;
- Gerar o arquivo TXT/CSV.

```
As instruções deverão estar suficientemente detalhadas para que o projeto possa ser executado sem a necessidade de intervenção do candidato.
```

---

## 23. Critérios de avaliação

A avaliação será realizada considerando a qualidade geral da solução.

|Critério							|Pontos|
|Modelagem SQL						|15    |
|CRUD de Devedores					|10    |
|CRUD de Contratos e Parcelas		|10    |
|CRUD de Telefones					|5     |
|Stored Procedure / Distribuição	|20    |
|Backend / C# / .NET				|10    |
|HTML / CSS / JavaScript / AJAX		|10    |
|Exportação TXT/CSV					|5     |
|Validações							|5     |
|Arquitetura / Organização			|5     |
|Segurança / Performance			|5     |
|Total								|100   |

|Pontuação	|Avaliação			|
|90–100		|Excelente          |
|75–89		|Muito bom          |
|60–74		|Bom                |
|50–59		|Abaixo do esperado |
|0–49		|Não recomendado    |
            
A classificação é apenas uma referência. 
A avaliação poderá considerar também a experiência esperada para a posição.
