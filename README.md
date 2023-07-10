# Desafio - NoxTec

Implementação de um sistema de agendamento telefônico, com as tecnologias Spring Boot (Java), Angular e PostgreSQL.

## Requisitos funcionais:
- Uma tela para cadastrar contatos
- Validar se o contato já foi cadastrado através do número do celular
- Uma tela para consultar contatos
- Conseguir atualizar e inativar o contato
- Deverá ter a possibilidade de colocar um contato como favorito
- A comunicação do back deve ser realizada por API

### Criação banco de dados
Tipo Banco: PostgreSQL
```
create schema desafio;
create table desafio.contato(
    contato_id serial primary key,
    contato_nome varchar(100),
    contato_email varchar(255),
    contato_celular varchar(11),
    contato_telefone varchar(10),
    contato_sn_favorito character(1),
    contato_sn_ativo character(1),
    contato_dh_cad timestamp without time zone);

```

## Ferramentas e linguagens para desenvolvimento
- Java 17 (open JDK)
- Angular 14
- IntelliJ comunity

*Back deve ser em Java 8+ com Spring Boot*.

*Front deve ser em Angular, se possível.*

## Uso de Docker 

Para facilitar o desenvolvimento, se fez necessário o uso de docker para subir imagens *on demand*, evitando a configuração de variáveis de ambientes locais e evitando o retrabalho. A aplicação pode ser iniciada através do comando 
```
  $ docker-compose up -d 
```
no terminal. Para parar a aplicação, basta executar o comando 
``` 
  $ docker-compose down
```
que a aplicação irá encerrar.

### Instalação do Docker

Instruções de instalação do **Docker** no [Ubuntu](https://docs.docker.com/install/linux/docker-ce/ubuntu/) e [Windows](https://docs.docker.com/docker-for-windows/install/).

**Docker Compose** já está incluíddo nos pacotes *Windows*, no *Ubuntu* deve-se seguir [essas instruções](https://docs.docker.com/compose/install/).

## contato-postgres (Database)

A base de dados PostgreSQL contém apenas um schema (desafio) com uma tabela (contato).

Depois de executar esses comandos, a base de dados pode ser acessada por esses acessos:

- Host: *localhost*
- Database: *desafio*
- User: *postgres*
- Password: *postgres*


As configurações do ambiente da base de dados podem ser alteradas no arquivo *docker-compose.yml*
*docker-compose.yml* file.

```yml
kanban-postgres:
    image: "postgres:9.6-alpine"
    container_name: kanban-postgres
    volumes:
      - kanban-data:/var/lib/postgresql/data
    ports:
      - 5555:5555
    environment:
      - POSTGRES_DB:desafio
      - POSTGRES_USER:postgres
      - POSTGRES_PASSWORD:postgres
```

## contato-app (REST API)

Essa é uma aplicação que utiliza Spring Boot, que processa as informações da base de dados e 
permite a que a aplicação possa ser consumida pelo frontend por meio de endpoints.
Os métodos HTTP suportados são  GET, POST, PUT e DELETE para os recursos do contato.

A lista contendo todos os endpoints pode ser acessada por meio do Swagger UI,
sendo executado através do link [http://localhost:8080/api/swagger-ui.html](http://localhost:8080/api/swagger-ui.html).

A aplicação também está em um container Docker, que pode ser modificado no arquivo **desafio-app/Dockerfile**.

## contato-ui (Frontend)

Essa é a parte visual da aplicação, onde o usuário poderá interagir com o sistema.
O Frontend consome a API REST fornecida pelo 
*contato-app*.

Pode ser acessado pelo link [http://localhost:4200/](http://localhost:4200/)
