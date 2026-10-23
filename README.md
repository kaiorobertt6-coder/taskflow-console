TaskFlow (Gerenciador de Tarefas via Console)
Aplicação console desenvolvida em .NET 10 para gerenciamento de tarefas pessoais (To-Do List), priorizando boas práticas de arquitetura de software, qualidade de código com testes unitários em xUnit e rastreabilidade com Conventional Commits (Git Semantic Flow).

# 📋 Sumário
Visão Geral

Requisitos do Ambiente

Estrutura da Solução

Como Executar

1. Restauração e Compilação

2. Executar a Aplicação Console

3. Executar a Suíte de Testes

Garantia de Qualidade (xUnit)

Padrão de Versionamento (Conventional Commits)

🚀 Visão Geral
O TaskFlow oferece uma interface interativa em linha de comando (CLI) para criação, listagem e conclusão de tarefas com identificadores únicos (Guid). O projeto foi construído seguindo um ciclo evolutivo de desenvolvimento: estruturação, implementação de domínio, testes automatizados, tratamento e correção de bugs (graceful degradation), refatoração e documentação.

💻 Requisitos do Ambiente
.NET 10 SDK (ou versão instalada compatível, como .NET 8 ou 9).

Git para controle de versão.

Terminal de linha de comando ou IDE de sua preferência (VS Code, Visual Studio, Rider).

📂 Estrutura da Solução
Plaintext
taskflow-console/
│
├── TaskFlow.sln
│
├── TaskFlow.Console/             # Projeto Console (.NET 10)
│   ├── TaskItem.cs               # Entidade de domínio com lógica de conclusão e validação
│   ├── TaskManager.cs            # Gerenciador de tarefas em memória (CRUD básico)
│   ├── Program.cs                # Interface CLI com menu interativo em loop
│   └── TaskFlow.Console.csproj
│
└── TaskFlow.Tests/               # Projeto de Testes Unitários (xUnit)
    ├── TaskManagerTests.cs       # Suíte de testes para validação de regras de negócio
    └── TaskFlow.Tests.csproj
🛠️ Como Executar
Execute os comandos a partir da raiz da solução:

1. Restauração e Compilação
Para restaurar pacotes e compilar todos os projetos:

Bash
# Restaurar dependências
dotnet restore

# Compilar a solução
dotnet build
2. Executar a Aplicação Console
Para iniciar o menu interativo no terminal:

Bash
dotnet run --project TaskFlow.Console/TaskFlow.Console.csproj
Funcionalidades disponíveis no menu:

1. Adicionar Tarefa: cadastra uma nova tarefa validando títulos nulos ou em branco.

2. Listar Tarefas: exibe todas as tarefas cadastradas, indicando status ([ ] pendente / [X] concluída) e ID.

3. Concluir Tarefa: marca uma tarefa como concluída a partir do seu Guid.

0. Sair: finaliza o programa com segurança.

3. Executar a Suíte de Testes
Para rodar todos os testes automatizados e verificar a integridade da aplicação:

Bash
dotnet test
🧪 Garantia de Qualidade (xUnit)
A suíte de testes unitários em TaskFlow.Tests valida as principais regras de domínio e tratamento de exceções:

AddTask_Should_Add_Task_When_Title_Is_Valid: assegura que tarefas válidas são inseridas com status inicial pendente (IsCompleted == false) e ID gerado.

AddTask_Should_Throw_Exception_When_Title_Is_Empty: valida o lançamento de ArgumentException caso o título seja vazio ou formado apenas por espaços em branco.

GetById_Should_Return_Null_When_Task_Does_Not_Exist: garante que a busca por um identificador inexistente retorne null graciosamente, sem lançar exceções não tratadas.

🌳 Padrão de Versionamento (Conventional Commits)
O repositório adota a convenção semântica tipo(escopo): descrição, refletindo com clareza o histórico evolutivo da solução:

chore(core): initialize .NET 10 solution and console project structure

chore(test): add xUnit test project and reference to console Project

feat(domain): implement TaskItem entity with completion logic

feat(services): implement TaskManager logic for in-memory task management

test(unit): add xUnit test suite for TaskManager validation rules

fix(manager): handle missing task gracefully in search method

refactor(console): implement interactive menu loop in Program.cs

docs(readme): add build, run and test instructions

Para inspecionar o grafo linear de commits:

Bash
git log --oneline --graph
fiz tudo na develop, vou fazer um pull request para a main, qual descrição e titulo coloco?

Aqui estão opções de título e um modelo completo de descrição para o Pull Request de develop para main no repositório taskflow-console:

Opções de Título
Padrão Conventional Commits (Recomendado):

feat: implementar gerenciador de tarefas console com testes xunit e git semantic flow

Padrão Descritivo / Entrega Acadêmica:

Implementação do TaskFlow CLI: Domínio, Testes xUnit e Git Semantic Flow

Padrão Release:

Release v1.0.0: Entrega completa da aplicação TaskFlow

Modelo de Descrição para o Pull Request
Copie e cole este conteúdo no corpo do PR:

Markdown
## 📌 Descrição
Este Pull Request consolida o desenvolvimento completo da aplicação **TaskFlow (Gerenciador de Tarefas via Console)**, integrando a entidade de domínio, gerenciador em memória, interface interativa CLI, testes unitários automatizados com xUnit e documentação técnica.

Todo o ciclo de desenvolvimento seguiu estritamente o padrão **Git Semantic Flow (Conventional Commits)**.

---

## 🚀 Histórico Evolutivo e Entregas

* `chore(core)`: criação da solution `TaskFlow.sln` e do projeto console `TaskFlow.Console`.
* `chore(test)`: adição do projeto de testes `TaskFlow.Tests` com referência ao projeto principal.
* `feat(domain)`: implementação da entidade `TaskItem` com validação de título e lógica de conclusão.
* `feat(services)`: criação do serviço `TaskManager` para gerenciamento em memória (adicionar, buscar e concluir tarefas).
* `test(unit)`: suíte de testes unitários xUnit cobrindo inserção válida, lançamento de `ArgumentException` e busca de IDs inexistentes.
* `fix(manager)`: tratamento gracioso de tarefas não encontradas no método `GetById`, retornando `null` em vez de exceção não tratada.
* `refactor(console)`: refatoração da `Program.cs` com loop de menu interativo para o usuário.
* `docs(readme)`: documentação completa com arquitetura, guia de comandos CLI e explicação dos testes.

---

## 🧪 Validação e Critérios de Aceite

- [x] **Compilação limpa:** `dotnet build` sem erros ou warnings.
- [x] **Testes automatizados:** `dotnet test` executado com 100% dos testes aprovados.
- [x] **Grafo de commits semântico:** histórico linear e padronizado verificado via `git log --oneline --graph`.
- [x] **Execução CLI:** fluxo de navegação e CRUD em memória validado via `dotnet run`.

---

## 🛠️ Como testar localmente

```bash
git checkout main
git pull origin develop
dotnet test
dotnet run --project TaskFlow.Console/TaskFlow.Console.csproj
