# Git & GitHub Training Lab: Engenharia de Versionamento, CI/CD e Notas de Estudos

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Commitizen friendly](https://img.shields.io/badge/commitizen-friendly-brightgreen.svg)](http://commitizen.github.io/cz-cli/)

Laboratório prático e repositório de estudos dedicado a controle de versão com **Git** (`git version 2.56.0.windows.3`), colaboração no **GitHub**, padronização de histórico e automação de releases.

A base conceitual acompanha a trilha do curso **TeoMeWhy — Introdução ao Git e GitHub**, expandida para um ambiente de prática (_Training Lab_) com **Git Flow**, **Conventional Commits**, **Commitlint**, **Commitizen**, **Git Tag**, **Semantic Versioning (SemVer)**, **semantic-release** e **CI/CD com GitHub Actions**.

---

## Sumário

1. [Sobre o Training Lab](#sobre-o-training-lab)
2. [Estrutura do Repositório](#estrutura-do-repositório)
3. [Trilha de Estudos e Notas](#trilha-de-estudos-e-notas)
4. [Fluxo Prático: Padronização, Versionamento e CI/CD](#fluxo-prático-padronização-versionamento-e-cicd)
5. [Referências](#referências)
6. [Licença](#licença)

---

## Sobre o Training Lab

- **Do estudo à prática de engenharia:** Vai além de anotações passivas ao servir como espaço de experimentação para comandos, _branches_, resolução de conflitos, _Pull Requests_, _forks_ e automação de entregas.
- **Base teórica estruturada:** As anotações completas ficam em `library/notas_de_estudo_git_e_github_teomewhy_2025.md`, funcionando como caderno de consulta e referência rápida do laboratório.
- **Higiene do repositório e automação:** Arquivos locais ou dependências auxiliares podem ficar fora do rastreamento remoto via `.gitignore` para preservar o repositório limpo, enquanto configurações de _workflow_ em CI/CD (como GitHub Actions) organizam a automação na `main`.

---

## Estrutura do Repositório

A organização abaixo reflete a estrutura do repositório e os arquivos locais auxiliares mantidos fora do rastreamento via `.gitignore`:

```text
git_training/
├── .github/
│   └── workflows/
│       └── release.yml                                # Pipeline de CI/CD para versionamento e releases na main
├── library/
│   ├── presentation/
│   │   └── .gitkeep                                   # Preserva o diretório vazio no Git (PDFs locais ignorados via .gitignore)
│   ├── git_commands.txt                               # Consulta rápida de comandos Git
│   ├── Command Line shortcuts.txt                     # Atalhos e comandos essenciais de terminal
│   └── notas_de_estudo_git_e_github_teomewhy_2025.md  # Caderno completo de estudos e referências
├── .gitignore                                         # Regras de exclusão de arquivos locais, PDFs e dependências
├── .releaserc.json                                    # (Local / ignorado) Configuração do semantic-release para simulações
└── README.md                                          # Visão geral do Training Lab e guia de uso
```

---

## Trilha de Estudos e Notas

O material completo em `library/notas_de_estudo_git_e_github_teomewhy_2025.md` está organizado em nove módulos:

1. **Instalação e primeiros conceitos (`commit tree`):** configuração inicial (`user.name`, `user.email`, `init.defaultBranch`, `core.editor`), área de _staging_ e árvore de commits.
2. **Primeiros comandos:** navegação no terminal (Shell/Bash), inicialização, inspeção (`status`, `diff`, `log`) e ciclo de vida de alterações (`add`, `reset`, `rm`, `commit`, `revert`).
3. **Branches:** criação, navegação (`switch` / `checkout`), mesclagem (`merge`) e limpeza de ramificações.
4. **Resolução de conflitos:** leitura de marcadores de conflito e boas práticas antes do _merge_ na `main`.
5. **Pull Request (PR):** repositórios remotos (`origin`), sincronização (`push`, `fetch`, `pull`) e fluxo de revisão de código.
6. **Fork, Fluxos de Trabalho, Git Tag e Semantic Release:** diferença entre _Fork_ e _Hard Fork_, fluxos local/próprio/open-source (`upstream`), _tags_ leves e anotadas (`git tag`), versionamento semântico (`SemVer`), simulação/publicação com `semantic-release` e `.releaserc.json`, e automação de CI/CD via GitHub Actions (YAML).
7. **Integração com VS Code:** uso da aba _Source Control_, inspeção de _diffs_ e resolução interativa de conflitos.
8. **Git Flow e Conventional Commits:** estrutura da mensagem de commit, tipos semânticos, convenção de _branches_ (_main_, _develop_, _feature/_, _release/_, _hotfix/_) e apoio de `Commitlint` e `Commitizen`.
9. **`.gitignore` e `.gitkeep`:** exclusão de arquivos locais/sensíveis e manutenção de diretórios vazios no histórico.

---

## Fluxo Prático: Padronização, Versionamento e CI/CD

Para exercitar a esteira de versionamento no laboratório (requer **Node.js/npm** onde aplicável):

### 1. Construção guiada de commits com Commitizen

Ajuda a montar mensagens no padrão **Conventional Commits** de forma interativa no terminal:

```bash
# Instalação global do CLI e do adaptador convencional
npm install -g commitizen cz-conventional-changelog

# Execução após preparar os arquivos com git add
git cz
```

### 2. Validação de mensagens com Commitlint

Verifica se a mensagem de commit atende às convenções antes de consolidar o registro:

```bash
# Instalação das dependências de validação
npm install -D @commitlint/cli @commitlint/config-conventional

# Teste rápido via linha de comando
echo "feat: adiciona nova funcionalidade" | npx commitlint
echo "mensagem fora do padrao" | npx commitlint
```

### 3. Simulação e release semântico com `semantic-release`

Avalia commits na `main` segundo o **SemVer** (`MAJOR.MINOR.PATCH`) usando `.releaserc.json` (sem `@semantic-release/npm` para releases focadas no GitHub), podendo ser automatizado em `.github/workflows/release.yml` via GitHub Actions:

```bash
# Simulação local sem criar tags nem alterar o remoto
npx semantic-release --dry-run
```

---

## Referências

- ATLASSIAN. **Gitflow Workflow**. Atlassian Git Tutorials, [s. d.]. Disponível em: <https://www.atlassian.com/br/git/tutorials/comparing-workflows/gitflow-workflow>. Acesso em: 26 nov. 2026.
- CHACON, Scott; STRAUB, Ben. **Pro Git**. 2. ed. [S. l.]: Apress, 2014–2026. Seção 1.1: Sobre Controle de Versão. Disponível em: <https://git-scm.com/book/pt-br/v2/Come%C3%A7ando-Sobre-Controle-de-Vers%C3%A3o>. Acesso em: 26 nov. 2026.
- CHACON, Scott; STRAUB, Ben. **Pro Git**. 2. ed. [S. l.]: Apress, 2014–2026. Seção 1.5: Instalando o Git. Disponível em: <https://git-scm.com/book/pt-br/v2/Come%C3%A7ando-Instalando-o-Git>. Acesso em: 26 nov. 2026.
- CHACON, Scott; STRAUB, Ben. **Pro Git**. 2. ed. [S. l.]: Apress, 2014–2026. Section 2.2: Recording Changes to the Repository. Disponível em: <https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository>. Acesso em: 26 nov. 2026.
- CHACON, Scott; STRAUB, Ben. **Pro Git**. 2. ed. [S. l.]: Apress, 2014–2026. Seção 2.3: Visualizando o Histórico de Commits. Disponível em: <https://git-scm.com/book/pt-br/v2/Fundamentos-de-Git-Visualizando-o-Hist%C3%B3rico-de-Commits>. Acesso em: 26 nov. 2026.
- CHACON, Scott; STRAUB, Ben. **Pro Git**. 2. ed. [S. l.]: Apress, 2014–2026. Section 2.5: Working with Remotes. Disponível em: <https://git-scm.com/book/en/v2/Git-Basics-Working-with-Remotes>. Acesso em: 26 nov. 2026.
- CHACON, Scott; STRAUB, Ben. **Pro Git**. 2. ed. [S. l.]: Apress, 2014–2026. Section 3.1: Branches in a Nutshell. Disponível em: <https://git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell>. Acesso em: 26 nov. 2026.
- CHACON, Scott; STRAUB, Ben. **Pro Git**. 2. ed. [S. l.]: Apress, 2014–2026. Section 3.2: Basic Branching and Merging. Disponível em: <https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging>. Acesso em: 26 nov. 2026.
- COMMITIZEN. **cz-cli**: The commitizen command line utility. [S. l.]: GitHub, [s. d.]. Disponível em: <https://github.com/commitizen/cz-cli>. Acesso em: 26 nov. 2026.
- COMMITLINT. **Commitlint**: Lint commit messages. [S. l.]: GitHub, [s. d.]. Disponível em: <https://github.com/conventional-changelog/commitlint>. Acesso em: 26 nov. 2026.
- COMMITLINT. **Local setup**. Commitlint Documentation, [s. d.]. Disponível em: <https://commitlint.js.org/guides/local-setup.html>. Acesso em: 26 nov. 2026.
- CONVENTIONAL COMMITS. **Conventional Commits 1.0.0**. [S. l.], [s. d.]. Disponível em: <https://www.conventionalcommits.org/pt-br/v1.0.0/>. Acesso em: 26 nov. 2026.
- GITHUB. **Git Cheat Sheet**. [S. l.]: GitHub Training, [s. d.]. Disponível em: <https://training.github.com/downloads/pt_BR/github-git-cheat-sheet/>. Acesso em: 26 nov. 2026.
- GITHUB. **gitignore**: A collection of useful `.gitignore` templates. [S. l.]: GitHub, [s. d.]. Disponível em: <https://github.com/github/gitignore>. Acesso em: 26 nov. 2026.
- GITHUB DOCS. **Fazer fork de um repositório**. [S. l.]: GitHub, [s. d.]. Disponível em: <https://docs.github.com/pt/pull-requests/collaborating-with-pull-requests/working-with-forks/fork-a-repo>. Acesso em: 26 nov. 2026.
- GITHUB DOCS. **Ignorando arquivos**. [S. l.]: GitHub, [s. d.]. Disponível em: <https://docs.github.com/pt/get-started/getting-started-with-git/ignoring-files>. Acesso em: 26 nov. 2026.
- GITHUB DOCS. **Sincronizar um fork**. [S. l.]: GitHub, [s. d.]. Disponível em: <https://docs.github.com/pt/pull-requests/collaborating-with-pull-requests/working-with-forks/syncing-a-fork>. Acesso em: 26 nov. 2026.
- GITHUB DOCS. **Sobre conflitos de merge**. [S. l.]: GitHub, [s. d.]. Disponível em: <https://docs.github.com/pt/pull-requests/collaborating-with-pull-requests/addressing-merge-conflicts/about-merge-conflicts>. Acesso em: 26 nov. 2026.
- GITHUB DOCS. **Sobre pull requests**. [S. l.]: GitHub, [s. d.]. Disponível em: <https://docs.github.com/pt/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests>. Acesso em: 26 nov. 2026.
- HUBSPOT. **Git and GitHub Tutorial for Beginners**. HubSpot Blog, [s. d.]. Disponível em: <https://product.hubspot.com/blog/git-and-github-tutorial-for-beginners>. Acesso em: 26 nov. 2026.
- MICROSOFT / VISUAL STUDIO CODE. **Using Git source control in VS Code**. Visual Studio Code Documentation, [s. d.]. Disponível em: <https://code.visualstudio.com/docs/sourcecontrol/overview>. Acesso em: 26 nov. 2026.
- PRESTON-WERNER, Tom. **Semantic Versioning 2.0.0**. [S. l.], [s. d.]. Disponível em: <https://semver.org/>. Acesso em: 26 nov. 2026.
- TEOMEWHY. **Introdução ao Git e GitHub**. YouTube, [s. d.]. Playlist. Disponível em: <https://www.youtube.com/watch?v=Y_fFZjzw-D4&list=PLvlkVRRKOYFQyKmdrassLNxkzSMM6tcSL>. Acesso em: 26 nov. 2026.

## Licença

Este projeto está licenciado sob a **Licença MIT** — consulte o arquivo [LICENSE](./LICENSE) para mais detalhes.
