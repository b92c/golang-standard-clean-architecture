# Layout de Projeto em Go usando Clean Architecture

## Visão Geral

Este documento descreve um layout de projeto para aplicações em Go que seguem os princípios da Clean Architecture. Este layout organiza o código de maneira que respeite a regra de dependência e promova a separação de preocupações, tornando o projeto mais fácil de manter e escalar.

## Estrutura de Diretórios

```plaintext
/project-root
│
├── /cmd
│   └── /api
│       └── main.go
├── /internal
│   ├── /domain
│   │   ├── /entities
│   │   │   └── user.go
│   │   └── /repositories
│   │       └── user_repository.go
│   ├── /usecases
│   │   └── user_usecase.go
│   └── /adapters
│       ├── /controllers
│       │   └── user_controller.go
│       ├── /presenters
│       │   └── user_presenter.go
│       └── /gateways
│           └── user_repository_db.go
├── /pkg
│   ├── /configs
│   │   └── config.yaml
│   ├── /framework
│   │   ├── /http
│   │   │   ├── /middlewares
│   │   │   └── router.go
│   │   └── /database
│   │       └── db.go
│   └── /utils
│       └── strings.go
├── /scripts
│   └── setup.sh
├── /test
│   └──  /integration
│       └── user_integration_test.go
├── .gitignore
├── go.mod
└── README.md
```

### Descrição dos Diretórios e Subdiretórios

#### `/cmd`

Este diretório contém os pontos de entrada da aplicação. Cada subdiretório representa uma aplicação executável distinta.

- **/cmd/api**: Contém o arquivo `main.go`, que é o ponto de entrada da aplicação principal. A função `main` neste arquivo geralmente importa e invoca código de outros diretórios como `/internal` e `/pkg`.

#### `/internal`

Este diretório contém o código da aplicação que não deve ser exposto a outros projetos. O código aqui é específico para este projeto e não é reutilizável externamente.

- **/internal/domain**: Contém as entidades e interfaces do domínio da aplicação.
  - **/entities**: Contém as entidades de domínio, que são os modelos de negócio (por exemplo, `user.go`).
  - **/repositories**: Contém as interfaces para os repositórios (por exemplo, `user_repository.go`).

- **/internal/usecases**: Contém os casos de uso (interactors) que implementam a lógica de aplicação específica (por exemplo, `user_usecase.go`).

- **/internal/adapters**: Contém os adaptadores que fazem a ponte entre as interfaces externas e a aplicação.
  - **/controllers**: Contém os controladores que lidam com a interação entre a camada de apresentação e os casos de uso (por exemplo, `user_controller.go`).
  - **/presenters**: Contém os apresentadores que formatam as respostas (por exemplo, `user_presenter.go`).
  - **/gateways**: Contém as implementações dos repositórios, como acesso a banco de dados ou serviços externos (por exemplo, `user_repository_db.go`).

#### `/pkg`

Este diretório contém pacotes reutilizáveis que podem ser usados por outros projetos. O código aqui é genérico e pode ser compartilhado.

- **/configs**: Contém arquivos de configuração (por exemplo, `config.yaml`).
- **/framework**: Contém implementações de detalhes específicos de frameworks.
  - **/http**: Contém configurações e middleware para frameworks web (por exemplo, `router.go`).
  - **/database**: Contém configurações e inicializações de banco de dados (por exemplo, `db.go`).
- **/utils**: Contém funções utilitárias que são independentes do domínio da aplicação (por exemplo, `strings.go`).

#### `/scripts`

Este diretório contém scripts para tarefas de construção, deploy, etc. Esses scripts mantêm o Makefile de nível raiz pequeno e simples (por exemplo, `setup.sh`).

#### `/test`

Este diretório contém testes automatizados organizados por tipo.

- **/integration**: Contém testes de integração que verificam a interação entre diferentes partes do sistema (por exemplo, `user_integration_test.go`).
- **/unit**: Contém testes unitários que verificam funcionalidades isoladas (por exemplo, `user_usecase_test.go`).

#### Outros Arquivos

- **.gitignore**: Arquivo que especifica quais arquivos e diretórios devem ser ignorados pelo Git.
- **go.mod**: Arquivo que define o módulo Go e suas dependências.
- **README.md**: Documentação do projeto.

## Considerações Finais

Este layout de projeto segue os princípios da Clean Architecture, garantindo que o código esteja bem organizado e separado em diferentes camadas de responsabilidade. Isso facilita a manutenção, testes e escalabilidade do projeto. Sinta-se à vontade para adaptar este layout conforme necessário para atender às necessidades específicas do seu projeto.