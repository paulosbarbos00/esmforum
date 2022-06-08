# ESM Fórum

O **ESM Fórum** é um sistema de demonstração do livro [Engenharia de Software Moderna](https://engsoftmoderna.info). O objetivo é permitir que os alunos tenham um primeiro contato prático com os conceitos estudados no livro.

Do ponto de requisitos funcionais, o sistema é um fórum simples de perguntas e respostas, conforme ilustrado a seguir:

<p align="center">
    <img width="70%" src="https://user-images.githubusercontent.com/57276191/171216634-072dbf3c-4740-479f-a757-8d0ec28c68b7.png" />
</p>

Do ponto de vista tecnológico, o sistema é implementado em TypeScript, usando Node.js, React e SQLite.

Informações para instalação e execução podem ser encontradas [aqui](https://github.com/aserg-ufmg/esmforum/blob/main/install-info.md).

## Histórias de Usuário

#### Backlog do Produto

As histórias de usuário do nosso sistema -- que fazem parte do **backlog do produto** -- são as seguintes:

* Como usuário, eu gostaria de criar uma pergunta
* Como usuário, eu gostaria de responder uma pergunta
* Como usuário, eu gostaria de editar uma das minhas perguntas ou respostas
* Como usuário, eu gostaria de deletar uma das minhas perguntas ou respostas
* Como usuário, eu gostaria de favoritar uma pergunta ou resposta
* Como usuário, eu gostaria de me cadastrar no sistema
* Como usuário, eu gostaria de adicionar tags nas minhas perguntas
* Como usuário, eu gostaria de remover tags das minhas perguntas
* Como usuário, eu gostaria de pesquisar por perguntas ou respostas
* Como administrador, eu gostaria de editar ou remover perguntas ou respostas de qualquer usuário
* Como administrador, eu gostaria de adicionar ou remover tags de qualquer pergunta ou resposta

#### Backlog do Sprint

Neste momento, apenas o primeiro sprint foi concluído e implementado. As histórias implementadas neste primeiro sprint -- ou seja, as histórias que fizeram parte do **backlog do sprint** -- foram as seguintes:

* Como usuário, eu gostaria de criar uma pergunta
* Como usuário, eu gostaria de responder uma pergunta
* Como usuário, eu gostaria de editar uma das minhas perguntas ou respostas
* Como usuário, eu gostaria de deletar uma das minhas perguntas ou respostas

Veja que começamos o desenvolvimento por um conjunto de funcionalidades que julgamos mais importantes em um sistema como o ESM Fórum. Basicamente, neste primeiro sprint, o que implementamos foi um CRUD de perguntas e respostas. Para quem ainda não conhece, CRUD é uma sigla que significa Criar, Listar (Read), Atualizar (Update) e Deletar algum tipo de dado. 

Por outro lado, não nos preocupamos ainda com outras funcionalidades, como cadastro de usuários. Ou seja, nesse primeiro sprint, estamos assumindo que existe um único usuário no sistema, que já se encontra logado e habilitado a postar e responder perguntas. 

#### Tarefas

No backlog do sprint, para cada história também existe uma lista de tarefas, as quais são necessárias para implementar a história. Por exemplo, as tarefas associadas à história "Como usuário, eu gostaria de criar uma pergunta" são as seguintes:

* Projetar o leiaute básico da interface (frontend);
* Projetar e criar o banco de dados (backend)
* Implementar rotas no backend para inserir, remover e recuperar perguntas e respostas (backend)
* Implementar uma primeira versão da interface, apenas com criação de perguntas
* Implementar uma segunda versão da interface, com as demais operações sobre perguntas e respostas

## Arquitetura
```mermaid
    flowchart LR
        FRONTEND["FRONTEND \n (React)"] <--> BACKEND["BACKEND \n (TypeScript)"];
        BACKEND["BACKEND \n (TypeScript)"] <--> DATABASE["DATABASE \n (SQLite)"];
```
Frontend:

Interface em React para exibição de uma página inicial simplificada de um sistema de fórum. 
A estrutura contém: 
 - Forum: responsável pela organização geral e coleta de comentários da API.
 - Form: esquema para interação do usuário no fórum e chamada para alteração na base de dados.
 - ExhibitComment: esquema para exibição de árvore de comentários.

Backend:
```mermaid
    flowchart LR
        com --> cct;
        ind --> com;
        ind --> usr;
        usr --> uct;
        cct --> cmd;
        uct --> umd;
        cmd --> db;
        umd --> db;
        subgraph routes
        direction TB
        com["comment"];
        ind["index"];
        usr["user"];
        end
        subgraph controllers
        direction TB
        cct["commentControler"];
        uct["userControler"];
        end
        subgraph models
        direction TB
        cmd["comment"];
        umd["user"];
        end
        subgraph utils
        direction TB
        db["database"];
        end
```
Web REST API, para definir a interação entre os diferentes componentes de software, utilzando Node.js e Express para envio de requerimentos HTTP como POST, GET, PUT e DELETE.
A API conta com:
 - Models: modelos das tabelas comentário e usuário, definindo consultas para acesso e manipulação do banco de dados.
 - Controllers: manipula as solicitações e determina as ações sobre cada modelo.
 - Routes: estabelece as rotas para comunicação cliente-servidor.
 - Utils: define chamadas para conexão e execução de consultas ao banco de dados.

Banco de Dados:

Banco de dados simples compatível com SQLite com tabelas básicas para usuário e comentário estruturadas em um modelo relacional.


