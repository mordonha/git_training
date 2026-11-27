# Curso TMW Git & GitHub - Notas de Estudo

[![Commitizen friendly](https://img.shields.io/badge/commitizen-friendly-brightgreen.svg)](http://commitizen.github.io/cz-cli/)

Repositório dedicado aos estudos de controle de versionamento com **Git** (`git version 2.56.0.windows.3`) e hospedagem colaborativa no **GitHub**.

O material acompanha a trilha principal do curso **TeoMeWhy — Introdução ao Git e GitHub**, complementada por documentação oficial e práticas de engenharia de software voltadas à padronização de histórico, _branches_ e versionamento (`Git Flow`, `Conventional Commits`, `Commitlint`, `Commitizen`, `Git Tag` e `semantic-release`).

---

## Sumário

1. [Sobre o Repositório e Escopo de Estudos](#sobre-o-repositório-e-escopo-de-estudos)
2. [Conteúdo Abordado nas Notas](#conteúdo-abordado-nas-notas)
3. [Ferramentas de Padronização e Versionamento](#ferramentas-de-padronização-e-versionamento)
4. [Referências](#referências)

---

## Sobre o Repositório e Escopo de Estudos

- **Base do curso:** A estrutura central segue as aulas do canal **TeoMeWhy**, cobrindo desde comandos essenciais de terminal e Git até colaboração remota com _Pull Requests_ e _Forks_.
- **Aprofundamentos complementares:** Ao longo das anotações, foram incorporadas referências externas (como o _Pro Git Book_, _GitHub Docs_, _Atlassian_ e _SemVer_) e práticas de padronização e automação (`Commitizen`, `Commitlint`, `Husky`, `Git Tag` e `semantic-release`).
- **Organização local e remota:** Arquivos e dependências auxiliares de ambiente/automação podem ser mantidos fora do rastreamento remoto via `.gitignore` para preservar o repositório limpo, enquanto configurações de _workflow_ em CI/CD (como GitHub Actions) podem ser versionadas conforme a necessidade.

---

## Conteúdo Abordado nas Notas

As anotações completas estão organizadas em `library/notas_de_estudo_git_e_github_teomewhy_2025.md` e cobrem:

1. **Instalação e primeiros conceitos (`commit tree`):** configuração inicial (`user.name`, `user.email`, `init.defaultBranch`, `core.editor`), área de _staging_ e árvore de commits.
2. **Primeiros comandos:** navegação no terminal (Shell/Bash), inicialização, inspeção (`status`, `diff`, `log`) e ciclo de vida de alterações (`add`, `reset`, `rm`, `commit`, `revert`).
3. **Branches:** criação, navegação (`switch` / `checkout`), mesclagem (`merge`) e limpeza de ramificações.
4. **Resolução de conflitos:** identificação de marcadores de conflito e boas práticas antes do _merge_ na `main`.
5. **Pull Request (PR):** repositórios remotos (`origin`), sincronização (`push`, `fetch`, `pull`) e fluxo de revisão.
6. **Fork, Fluxos de Trabalho, Git Tag e Semantic Release:** diferença entre _Fork_ e _Hard Fork_, fluxos local/próprio/open-source (`upstream`), _tags_ leves e anotadas (`git tag`), versionamento semântico (`SemVer`), execução do `semantic-release` com `.releaserc.json` (`--dry-run` e publicação na `main`) e automação em CI/CD com GitHub Actions e YAML.
7. **Integração com VS Code:** uso da aba _Source Control_, visualização de _diffs_ e resolução interativa de conflitos.
8. **Git Flow e Conventional Commits:** anatomia da mensagem de commit, tipos semânticos, convenção de _branches_ (_main_, _develop_, _feature/_, _release/_, _hotfix/_) e validação/criação de commits com `Commitlint` e `Commitizen`.
9. **`.gitignore` e `.gitkeep`:** regras de exclusão de arquivos locais/sensíveis e preservação de diretórios vazios.

---

## Ferramentas de Padronização e Versionamento

Para aplicar **Conventional Commits** e versionamento semântico na prática durante os estudos, o ambiente pode utilizar as ferramentas abaixo (com **Node.js/npm** instalado quando aplicável):

### 1. Commitizen (Construção interativa de commits)

Auxilia na montagem passo a passo das mensagens de commit no terminal sem precisar decorar todos os prefixos.

```bash
# Instalação global do CLI e do adaptador convencional
npm install -g commitizen cz-conventional-changelog

# Uso após preparar os arquivos com git add
git cz
```

### 2. Commitlint (Validação de mensagens)

Verifica se a mensagem de commit segue as regras do **Conventional Commits** antes de consolidar o registro.

```bash
# Instalação das dependências de validação
npm install -D @commitlint/cli @commitlint/config-conventional

# Teste rápido via linha de comando
echo "feat: adiciona nova funcionalidade" | npx commitlint
echo "mensagem fora do padrao" | npx commitlint
```

### 3. Semantic Release (Simulação e versão semântica)

Calcula versões no padrão `MAJOR.MINOR.PATCH` a partir dos commits na `main` usando um `.releaserc.json` (por exemplo, sem `@semantic-release/npm` para releases apenas no GitHub):

```bash
# Simulação sem criar tags ou alterar o remoto
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
