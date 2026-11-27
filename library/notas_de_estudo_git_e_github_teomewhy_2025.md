# TEOMEWHY - GIT & GITHUB 2025

> **Curso Base:** [TeoMeWhy - Introdução ao Git e Github](https://www.youtube.com/watch?v=Y_fFZjzw-D4&list=PLvlkVRRKOYFQyKmdrassLNxkzSMM6tcSL)  
> **Material de Apoio Geral:** [GitHub Git Cheat Sheet (PT-BR)](https://training.github.com/downloads/pt_BR/github-git-cheat-sheet/) | [Tutorial Introdutório HubSpot](https://product.hubspot.com/blog/git-and-github-tutorial-for-beginners)

---

## SUMMARY

1. [**Instalação e primeiros conceitos (commit tree)**](#1-instalação-e-primeiros-conceitos-commit-tree)
2. [**Primeiros comandos**](#2-primeiros-comandos)
3. [**Branches**](#3-branches)
4. [**Resolução de conflitos**](#4-resolução-de-conflitos)
5. [**Pull Request (PR)**](#5-pull-request-pr)
6. [**Fork e Fluxos de Trabalho**](#6-fork-e-fluxos-de-trabalho)
7. [**Integração com VS Code**](#7-integração-com-vs-code)
8. [**Git Flow e Conventional Commits**](#8-git-flow-e-conventional-commits)
9. [**GitIgnore e GitKeep**](#9-gitignore-e-gitkeep)

---

## 1. Instalação e primeiros conceitos (commit tree)

> **Referências:** [Pro Git Book - 1.1 Sobre Controle de Versão](https://git-scm.com/book/pt-br/v2/Come%C3%A7ando-Sobre-Controle-de-Vers%C3%A3o) | [Pro Git Book - 1.5 Instalando o Git](https://git-scm.com/book/pt-br/v2/Come%C3%A7ando-Instalando-o-Git)

### O que é o Git?

- Software open-source para gerenciamento e controle de versão de arquivos (criado por Linus Torvalds), multiplataforma.
- Precisa ser iniciado no diretório de interesse a ser versionado, chamado de **Working Directory** (diretório de trabalho).

### Instalação e Atualização

- **Windows (via Winget):**
  ```bash
  winget install --id Git.Git -e --source winget
  ```
- **Outros gestores de pacotes (Linux/macOS):**
  ```bash
  <manager> install git
  ```
- **Verificar versão e atualizar:**
  - `git -v`: Exibe a versão atual instalada no sistema operacional.
  - `git update`: Atualiza o pacote do Git.

### Configuração Inicial do Ambiente

- **Identidade do autor:**
  ```bash
  git config --global user.name "Seu Nome"
  git config --global user.email "seu.email@exemplo.com"
  ```
- **Branch padrão:**
  ```bash
  git config --global init.defaultBranch main
  ```
  _(Nota: Antigamente o padrão era `master`; a migração para `main` ocorreu por questões semânticas e de inclusão)._
- **Editor de texto padrão:**
  - Verificar editor atual: `git config --get core.editor` ou `git var GIT_EDITOR`
  - Configurar novo editor: `git config --global core.editor "<comando-do-editor>"`
    - **VS Code:** `git config --global core.editor "code --wait"`
    - **Nano:** `git config --global core.editor "nano"`
    - **Vim:** `git config --global core.editor "vim"`
    - **Sublime Text:** `git config --global core.editor "subl -n -w"`

### Conceitos Fundamentais: Commit, Staging e Árvore (Commit Tree)

- **Staging Environment (Index):** Área intermediária ("palco") onde as modificações são preparadas antes de serem salvas definitivamente no histórico.
- **Commit:** É o registro (checkpoint/imagem) do progresso atual das alterações que estavam no _stage_. Cada commit possui um identificador **hash** único.
- **Versionamento e Árvore de Commits:** Os commits formam uma linha do tempo (árvore de nós). Navegar pelos hashes permite retornar a estados anteriores, reutilizar códigos e manter a continuidade segura do projeto.

---

## 2. Primeiros comandos

> **Referências:** [Pro Git Book - 2.2 Gravando Alterações no Repositório](https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository) | [Pro Git Book - 2.3 Visualizando o Histórico de Commits](https://git-scm.com/book/pt-br/v2/Fundamentos-de-Git-Visualizando-o-Hist%C3%B3rico-de-Commits)

### Comandos Essenciais de Terminal (Shell / Bash)

- `ls`: Lista arquivos do diretório atual (`dir` no Windows CMD).
  - `ls -a`: Lista também arquivos ocultos (ex: `.git`, `.gitignore`).
  - `ls <dir>`: Lista o conteúdo de uma subpasta sem precisar entrar nela.
- `cd <diretorio>`: Navega entre diretórios (`cd ..` volta um nível).
- `pwd`: Exibe o caminho absoluto (_path_) do diretório atual.
- `clear` (ou `Ctrl + L`): Limpa a tela do terminal (`cls` no Windows).
- `mkdir <nome>`: Cria um novo diretório.
- `touch <arquivo>`: Cria um arquivo vazio para edição posterior.
- `echo '<mensagem>' >> <arquivo>`: Cria o arquivo (se não existir) e anexa (_append_) o texto ao final. _(Usar `>` único sobrescreve todo o conteúdo)._
- `mv "<arquivo>" <dir>`: Move ou renomeia arquivos/diretórios.
- `cat <arquivo>`: Exibe o conteúdo de um arquivo no terminal (`type` no Windows CMD).
- `rm -rf <dir>`: Exclui recursivamente e à força um diretório e todo o seu conteúdo (**cuidado: ação irreversível**).

### Comandos Iniciais e de Versionamento no Git

- **Inicialização:**
  - `git init .`: Transforma o diretório atual em um repositório Git, criando a pasta oculta `.git/`.
  - `git init <dir>`: Cria um repositório isolado dentro da subpasta especificada _(evite aninhar repositórios para não gerar conflitos de rastreio)_.
- **Inspeção de Status e Diferenças:**
  - `git status`: Mostra a branch atual, arquivos rastreados (_tracked_), não rastreados (_untracked_) e o que está no _stage_.
  - `git status -s`: Exibição resumida (`A` = no staging; `M` = modificado; `MM` = modificado no staging e no working directory; `??` = não rastreado).
  - `git diff`: Exibe as linhas exatas modificadas que ainda **não** foram para o _staging_.
  - `git diff --staged`: Exibe as modificações que já estão no _staging_ comparadas ao último commit.
- **Preparação (Staging Area) e Remoção:**
  - `git add <arquivo>`: Envia um arquivo específico para o _stage_.
  - `git add .`: Envia todos os arquivos modificados/novos do diretório atual para o _stage_.
  - `git add *.txt` (ou `file*`): Adiciona arquivos por padrão de extensão ou prefixo.
  - `git ls-files --stage`: Lista os arquivos indexados atualmente na área de _staging_ (`.git/index`).
  - `git reset <arquivo>`: Retira o arquivo do _stage_ (rollback do `git add`), mantendo as alterações no arquivo local.
  - `git rm <arquivo>`: Remove o arquivo do rastreamento do Git e do diretório (use `-f` para forçar caso já esteja no _stage_).
  - `git rm --cached <arquivo>`: Remove o arquivo do rastreamento do git
- **Registro e Histórico:**
  - `git commit -m "<mensagem>"`: Salva os arquivos do _stage_ no histórico do repositório com uma mensagem descritiva.
  - `git commit -v`: Abre o editor padrão exibindo o _diff_ completo das alterações para redigir a mensagem.
  - `git log`: Exibe o histórico de commits da branch atual (pressione `q` para sair).
  - `git log -1`: Mostra apenas o último commit realizado.
  - `git revert <hash>`: Cria um novo commit desfazendo as alterações introduzidas por um commit específico anterior.

---

## 3. Branches

> **Referências:** [Pro Git Book - 3.1 Branches em Poucas Palavras](https://git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell) | [Pro Git Book - 3.2 Branches e Merges Básicos](https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)

Branches são ramificações isoladas do repositório. Cada branch possui seu próprio histórico de commits e área de _staging_, permitindo desenvolver funcionalidades ou correções sem afetar a linha principal (`main`). O ponteiro **HEAD** indica em qual branch você está trabalhando no momento.

- **Boas práticas:** Antes de trocar de branch, certifique-se de commitar suas alterações atuais (deixar o _working directory_ limpo) para evitar conflitos ou perda de contexto.

### Comandos Principais

- `git branch`: Lista todas as branches locais e destaca a branch ativa.
- `git branch <nome>`: Cria uma nova branch sem mudar para ela.
- `git checkout -b <nome>`: Cria uma nova branch e muda automaticamente para ela.
- `git checkout <nome>` (ou `git switch <nome>`): Alterna para a branch selecionada.
- `git branch -m main`: Renomeia a branch atual para `main`.
- `git merge <branch>`: Traz e mescla as alterações da `<branch>` informada para dentro da branch onde você está posicionado no momento.
- `git branch -d <nome>`: Apaga uma branch local que já foi mesclada (use `-D` para forçar a exclusão caso não tenha sido mesclada).

---

## 4. Resolução de conflitos

> **Referência:** [GitHub Docs - Sobre conflitos de merge](https://docs.github.com/pt/pull-requests/collaborating-with-pull-requests/addressing-merge-conflicts/about-merge-conflicts)

### Quando ocorrem?

Conflitos acontecem durante um `git merge` (ou `git pull`) quando duas branches diferentes possuem **alterações divergentes nas mesmas linhas de um mesmo arquivo**, impedindo o Git de decidir automaticamente qual versão deve prevalecer.

### Como resolver?

1. **Identificação:** O Git pausará o merge e marcará os arquivos conflitantes no código com delimitadores (`<<<<<<< HEAD`, `=======`, `>>>>>>> branch-origem`).
2. **Edição:** Abra o arquivo afetado (manualmente ou via `git mergetool` / interface do VS Code) e escolha qual trecho de código manter, removendo os marcadores do Git.
3. **Consolidação:** Após salvar o arquivo corrigido, finalize o processo:
   ```bash
   git add <arquivo-resolvido>
   git commit -m "fix: resolve conflitos de merge"
   ```

### Boas Práticas de Integridade

- **Atualize sua branch antes do merge final:** Costuma-se fazer o merge da `main` para dentro da sua branch de trabalho (`feature`) antes de enviar para a `main`. Assim, os conflitos são resolvidos no ambiente isolado da sua branch, protegendo a integridade da `main` (que geralmente reflete o código em **Produção / PROD**).

---

## 5. Pull Request (PR)

> **Referências:** [Pro Git Book - 2.5 Trabalhando com Remotos](https://git-scm.com/book/en/v2/Git-Basics-Working-with-Remotes) | [GitHub Docs - Sobre Pull Requests](https://docs.github.com/pt/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests)

### Repositórios Remotos (`origin`)

Repositórios remotos são versões do projeto hospedadas em servidores na nuvem (GitHub, GitLab, Bitbucket) que sincronizam todo o histórico de commits com a máquina local.

- `git clone <url-repo> [pasta-destino]`: Baixa uma cópia completa de um repositório remoto (via HTTPS ou SSH) para a máquina local.
- `git remote add origin <url-repo>`: Vincula um repositório local existente a um repositório remoto chamado `origin`.
- `git remote -v`: Lista as URLs remotas configuradas.
- `git remote show <nome>`: Exibe detalhes sobre o repositório remoto (branches rastreadas, status, etc.).
- `git remote rename <antigo> <novo>`: Renomeia um apontamento remoto.
- `git remote remove <nome>`: Remove o vínculo com o repositório remoto.

### Sincronização (Push, Fetch e Pull)

- `git push -u origin main`: Envia os commits locais para o repositório remoto pela primeira vez, vinculando o rastreamento (_upstream_).
- `git push origin <branch>`: Envia as alterações da branch local para a branch correspondente no servidor remoto.
- `git fetch <remote>`: Baixa as atualizações e novas branches do repositório remoto para o banco de dados local **sem** mesclar automaticamente ao seu código atual.
- `git pull origin <branch>`: Baixa as atualizações remotas e faz o `merge` automático na sua branch local (`git fetch` + `git merge`).

### O que é um Pull Request (PR)?

- É um pedido formal de revisão e integração de código feito na interface do GitHub (ou plataforma similar) para mesclar alterações de uma branch secundária na `main`.
- Permite revisão de código (_Code Review_), execução de testes automatizados e discussão antes do merge definitivo. _(Agentes de IA integrados ao GitHub também podem automatizar a abertura e revisão de PRs quando autorizados)._

---

## 6. Fork e Fluxos de Trabalho

> **Referências:** [GitHub Docs - Fazer fork de um repositório](https://docs.github.com/pt/pull-requests/collaborating-with-pull-requests/working-with-forks/fork-a-repo) | [GitHub Docs - Sincronizar um fork](https://docs.github.com/pt/pull-requests/collaborating-with-pull-requests/working-with-forks/syncing-a-fork)

### Conceito de Fork vs. Hard Fork

- **Fork (Colaboração Open-Source):** Cria uma cópia independente de um repositório de terceiros na sua própria conta do GitHub. Você clona o _seu_ fork, cria uma nova branch, faz o `push` para o _seu_ repositório remoto e abre um **Pull Request** solicitando que o dono do projeto original aceite suas alterações na `main` dele.
  - **Sync Fork:** Botão na interface do GitHub (ou via `git fetch upstream` + `git merge upstream/main`) usado para manter a `main` do seu fork atualizada com as novidades do repositório original (`upstream`).
- **Hard Fork (Derivação Independente):** Prática de clonar/copiar um repositório para seguir um caminho próprio e independente de desenvolvimento ou estudo, mantendo o vínculo de histórico ou os devidos créditos de autoria conforme a licença do software (evitando plágio ou violação de direitos autorais).

---

### Resumo dos 3 Fluxos de Trabalho Práticos

#### A. Fluxo Local (Sem repositório remoto)

1. `git checkout -b <nova-branch>`
2. Criar ou editar arquivos
3. `git status` e `git add <arquivos>`
4. `git commit -m "mensagem descritiva"`
5. `git checkout main`
6. `git merge <nova-branch>`

#### B. Fluxo GitHub ↔ Local (Projeto Próprio ou Corporativo)

1. `git clone <url-do-projeto>`
2. `git checkout -b <nova-branch>`
3. Editar arquivos, rodar `git status`, `git add <arquivos>` e `git commit -m "mensagem"`
4. `git push origin <nova-branch>`
5. Abrir **Pull Request** no GitHub para a `main` e realizar o merge após aprovação
6. Excluir `<nova-branch>` remota no GitHub
7. No terminal local: `git checkout main` → `git pull origin main` → `git branch -d <nova-branch>`

#### C. Fluxo GitHub ↔ Local (Projetos Open-Source via Fork)

1. Fazer o **Fork** do projeto original para a sua conta no GitHub
2. `git clone <url-do-seu-fork>`
3. _(Opcional)_ Configurar repositório original: `git remote add upstream <url-repo-original>`
4. `git checkout -b <nova-branch>`
5. Editar arquivos, rodar `git add <arquivos>` e `git commit -m "mensagem"`
6. `git push origin <nova-branch>`
7. Abrir **Pull Request** no GitHub da branch do seu fork para a `main` do repositório original
8. Após aprovação, excluir `<nova-branch>` no seu fork remoto e sincronizar sua `main` (`Sync fork`)
9. No terminal local: `git checkout main` → `git pull origin main` → `git branch -d <nova-branch>`

### Git Tag (Marcadores de Versão e Releases)

> **Nota de Engenharia de Software:** `git tag` não é um escopo de ramificação do **Git Flow** (que organiza branches como `main`, `develop`, `feature/*`, `release/*` e `hotfix/*`), mas costuma acompanhar o ciclo de _release_ para marcar versões estáveis (ex.: `v1.0.0`) sobre commits específicos.

#### Comandos essenciais

- **Listar tags existentes:**
  ```bash
  git tag
  ```
- **Criar uma tag leve (aponta diretamente para o commit atual):**
  ```bash
  git tag v0.1.0
  ```
- **Criar uma tag anotada (recomendada para versões/releases, registra autor, data e mensagem):**
  ```bash
  git tag -a v1.0.0 -m "Versão inicial estável"
  ```
- **Criar uma tag apontando para um commit específico:**
  ```bash
  git tag -a v0.2.0 <hash-do-commit> -m "Marco anterior"
  ```
- **Inspecionar detalhes de uma tag anotada:**
  ```bash
  git show v1.0.0
  ```

#### Envio para o remoto

O `git push origin <branch>` não envia _tags_ por padrão; é necessário enviá-las explicitamente:

- **Enviar uma tag específica para o remoto:**
  ```bash
  git push origin v1.0.0
  ```
- **Enviar todas as tags locais para o remoto:**
  ```bash
  git push origin --tags
  ```

#### Remoção de tags

- **Apagar uma tag local:**
  ```bash
  git tag -d v1.0.0
  ```
- **Apagar uma tag no repositório remoto:**
  ```bash
  git push origin --delete v1.0.0
  ```

---

## 7. Integração com VS Code

> **Referência:** [VS Code Docs - Using Git source control in VS Code](https://code.visualstudio.com/docs/sourcecontrol/overview)

O Visual Studio Code possui integração nativa e visual com o Git através da aba **Source Control** (`Ctrl + Shift + G`):

- **Rastreamento automático:** Indica visualmente arquivos modificados (`M`), adicionados/untracked (`U`) e deletados (`D`) direto na árvore de arquivos.
- **Staging e Commits visuais:** Permite adicionar arquivos ao _stage_ (`+`), visualizar o _diff_ lado a lado com um clique e escrever mensagens de commit sem precisar usar o terminal.
- **Sincronização Remota:** Botões diretos para `Sync Changes` (Pull/Push), troca de branches no canto inferior esquerdo e visualização da linha do tempo de commits e branches.
- **Resolução de Conflitos:** Interface interativa com botões para aceitar alterações atuais (_Accept Current_), alterações recebidas (_Accept Incoming_) ou ambas (_Accept Both_).

---

## 8. Git Flow e Conventional Commits

> **Referências:** [Conventional Commits v1.0.0](https://www.conventionalcommits.org/pt-br/v1.0.0/) | [Atlassian - Gitflow Workflow](https://www.atlassian.com/br/git/tutorials/comparing-workflows/gitflow-workflow) | [Commitlint](https://github.com/conventional-changelog/commitlint) | []Commitizen](https://github.com/commitizen/cz-cli)

### Estrutura Completa de um Commit

A estrutura padrão para mensagens de commit segue o formato:

```text
<type>(<scope>): <subject>
<BLANK LINE>
<body>
<BLANK LINE>
<footer>
```

_(Onde `<BLANK LINE>` indica que deve haver uma linha em branco separando os blocos)._

- **Partes da mensagem:**
  1. **`type` (categoria):** Indica a natureza da mudança e costuma seguir os mesmos prefixos usados na nomeação de branches.
  2. **`scope` (escopo):** Define onde a alteração foi aplicada — geralmente o nome de um módulo, entidade ou funcionalidade (ex: `veículo`, `auth`, `checkout`).
  3. **`subject` (assunto):** Resumo curto e objetivo no imperativo (ex: _adiciona_, _altera_, _corrige_, _remove_).
  4. **`body` (corpo — opcional):** Espaço para detalhar o contexto, o _porquê_ e os impactos técnicos da mudança.
  5. **`footer` (rodapé — opcional):** Utilizado para referenciar códigos/IDs de tarefas no Kanban/Jira (ex: `PL-1234`) ou sinalizar _breaking changes_.

- **Exemplo de commit:**

  ```text
  refactor(veículo): altera inserção da placa para utilizar trim

  PL-1234
  ```

### Conventional Commits

Convenção semântica para padronizar mensagens de commit, facilitar a leitura do histórico e automatizar a geração de _changelogs_:

- **`feat:`** Nova funcionalidade adicionada ao projeto.
- **`fix:`** Correção de um bug ou falha.
- **`docs:`** Alterações exclusivamente em documentação (ex: `README.md`, notas de estudo).
- **`style:`** Ajustes de formatação que não alteram a lógica do código (espaços, indentação, ponto e vírgula).
- **`refactor:`** Refatoração de código que não corrige bug nem adiciona nova funcionalidade.
- **`perf:`** Alterações focadas em melhoria de performance.
- **`build:`** Atualizações de tarefas de build, configurações, scripts ou dependências.
- **`chore:`** Mudanças no projeto que não afetam o sistema ou arquivos de testes. Mudanças de desenvolvimento. (ex: atualização de .gitignore, adicionar prettier)
- **`test:`** Criação ou alteração de códigos de teste (ex: criação de testes unitários)
- **`revert:`** Indica a reversão de um commit anterior

### Organização de Branches (Modelo Git Flow)

- **Branches principais (permanentes):**
  - **`main`:** Reflete o código estável em **produção**. Recebe merges apenas de versões testadas e aprovadas (vindas de `release/*` ou `hotfix/*`), geralmente acompanhadas de uma `git tag` de versão.
  - **`develop`:** Branch principal de desenvolvimento e integração. Reúne as novas entregas já concluídas e validadas antes de serem preparadas para ir para produção.

- **Branches de suporte (temporárias):**
  - **`feature/`:** Criada a partir da `develop` para desenvolver uma nova funcionalidade ou melhoria isolada. Ao ser concluída, retorna via merge/PR para a `develop` e é excluída.
  - **`release/`:** Criada a partir da `develop` quando um conjunto de funcionalidades está pronto para ser publicado (ex.: `release/v1.2.0`). Serve para ajustes finais, correções leves de homologação e atualização de versão/changelog; ao finalizar, é mesclada tanto na `main` (gerando a _tag_ de lançamento) quanto de volta na `develop`.
  - **`hotfix/`:** Criada diretamente a partir da `main` para corrigir rapidamente um bug crítico encontrado em produção (ex.: `hotfix/corrige-login`). Após a correção, é mesclada tanto na `main` (gerando nova _tag_ de _patch_) quanto na `develop` para manter as branches sincronizadas.

- **Padrão detalhado em 3 partes (categoria + entrega + código da tarefa):**
  1. **Tipo/categoria da branch:** `docs`, `feat`, `fix`, `perf`, `refactor`.
  2. **O que a branch entrega:** Descrição curta da atividade ou funcionalidade.
  3. **Código da tarefa no Kanban/Jira:** Identificador da demanda (ex: `K-078`).
  - _Exemplos:_ `docs-notas-de-estudos-K-078` ou `docs-cheatsheets`.

- **Padrão enxuto por contexto (`/`):**
  Para manter a nomenclatura mais direta e limpa no dia a dia:
  - `feat/<nome-da-funcionalidade>` (ex: `feat/cheatsheets`)
  - `fix/<nome-da-correcao>`
  - `docs/<nome-da-documentacao>` (ex: `docs/notas-de-estudos`)

### Commitlint

Ferramenta para validação de mensagens de commits seguindo o padrão **Conventional Commits**.

#### Git Flow e CI/CD

- **Regras por projeto:** para projetos específicos, crie o arquivo de configuração dentro do diretório de trabalho do repositório para definir regras de commit próprias daquele fluxo/projeto, quando necessário.
- **Uso global no terminal:** a instalação no diretório base do usuário na máquina atende validações padronizadas via terminal fora de um projeto específico.

#### Instalação no working directory (com `npm` / Windows)

```bash
npm install -D @commitlint/cli @commitlint/config-conventional

# Usa o Node para evitar problemas de encoding no Windows
node -e "fs.writeFileSync('commitlint.config.js', process.argv[1])" "export default { extends: ['@commitlint/config-conventional'] };"

# Caso ocorra conflito/aviso de ES module no Node, altere o conteúdo de commitlint.config.js para:
# module.exports = { extends: ['@commitlint/config-conventional'] };
```

#### Exemplo de uso (sem configuração de hooks / Husky)

```bash
echo "mensagem do commit que se deseja validar" | npx commitlint
```

> **Nota sobre hooks:** Para ver como configurar hooks (como o Husky) e automatizar a validação no fluxo de commit, acesse a documentação oficial em [https://commitlint.js.org/guides/local-setup.html](https://commitlint.js.org/guides/local-setup.html).

### Commitizen

Ferramenta para construção de commits de forma iterativa, seguindo o Conventional Commits

#### Intatalação (npm)

```bash
npm install -g commitizen
```

Uso (O comando invoca o git commit após a finalização da interface):

```bash
git cz
```

---

## 9. GitIgnore e GitKeep

> **Referências:** [GitHub Docs - Ignorando arquivos (.gitignore)](https://docs.github.com/pt/get-started/getting-started-with-git/ignoring-files) | [Coleção de Templates .gitignore (GitHub)](https://github.com/github/gitignore)

### `.gitignore`

Arquivo de configuração na raiz do projeto que instrui o Git sobre quais arquivos ou pastas devem ser **ignorados** (não rastreados e nunca enviados ao repositório).

- **O que ignorar:**
  - **Dados brutos e arquivos pesados:** Bases de dados não devem ser versionadas no Git (ex: pastas `data/` com `.csv`, `.xlsx`, `.parquet`, `.db`).
  - **Segurança e Credenciais:** Arquivos com senhas, tokens e chaves de API (ex: `.env`, `credentials.json`).
  - **Arquivos de ambiente/sistema:** Pastas de dependências e caches (ex: `node_modules/`, `__pycache__/`, `.venv/`, `.DS_Store`).
- **Comandos úteis para criar/ler:**
  ```bash
  echo "*.csv" > .gitignore      # Cria o arquivo e adiciona a regra
  echo ".env" >> .gitignore      # Adiciona nova regra ao final sem apagar as anteriores
  cat .gitignore                 # Lê as regras configuradas
  ```

### `.gitkeep`

Como o Git rastreia arquivos e **não rastreia pastas vazias**, diretórios sem conteúdo são ignorados ao fazer commits ou clones.

- **Para que serve:** É um arquivo vazio criado dentro de um diretório (ex: `data/.gitkeep`) apenas para forçar o Git a manter a estrutura daquela pasta no repositório.
- **Uso comum com `.gitignore`:** Ao configurar o `.gitignore` para ignorar todos os arquivos dentro de `data/*` mas manter exceção para `!data/.gitkeep`, você garante que os dados pesados não subam para o GitHub, mas a pasta `data/` continuará existindo na hierarquia do projeto para quem clonar o repositório.
