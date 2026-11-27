# Curso TMW Git & GitHub - Notas de Estudo

[![Commitizen friendly](https://img.shields.io/badge/commitizen-friendly-brightgreen.svg)](http://commitizen.github.io/cz-cli/)

Repositório dedicado aos estudos de controle de versionamento com **Git** (`git version 2.56.0.windows.3`) e hospedagem colaborativa no **GitHub**.

O material acompanha a trilha principal do curso [**TeoMeWhy — Introdução ao Git e GitHub**](https://www.youtube.com/watch?v=Y_fFZjzw-D4&list=PLvlkVRRKOYFQyKmdrassLNxkzSMM6tcSL), complementada por documentação oficial e ferramentas práticas de padronização de fluxo e mensagens de commit (`Git Flow`, `Conventional Commits`, `Commitlint` e `Commitizen`) que vão além do escopo base das aulas.

---

## Sumário

1. [Sobre o Repositório e Escopo de Estudos](#sobre-o-repositório-e-escopo-de-estudos)
2. [Conteúdo Abordado nas Notas](#conteúdo-abordado-nas-notas)
3. [Ferramentas de Padronização de Commits (Commitizen e Commitlint)](#ferramentas-de-padronização-de-commits-commitizen-e-commitlint)
4. [Referências Utilizadas nas Notas](#referências-utilizadas-nas-notas)

---

## Sobre o Repositório e Escopo de Estudos

- **Base do curso:** A estrutura central segue as aulas do canal **TeoMeWhy**, cobrindo desde comandos essenciais de terminal e Git até colaboração remota com Pull Requests e Forks.
- **Aprofundamentos complementares:** Ao longo das anotações, foram incorporadas referências externas (como o _Pro Git Book_, _GitHub Docs_ e _Atlassian_) e ferramentas de automação de qualidade de histórico (`Commitizen`, `Commitlint` e `Husky`) mantidas localmente para manter o repositório remoto limpo.

---

## Conteúdo Abordado nas Notas

As anotações completas estão organizadas em `library/notas_de_estudo_git_e_github_teomewhy_2025.md` e cobrem:

1. **Instalação e primeiros conceitos (`commit tree`):** configuração inicial (`user.name`, `user.email`, `init.defaultBranch`, `core.editor`), área de _staging_ e árvore de commits.
2. **Primeiros comandos:** navegação no terminal (Shell/Bash), inicialização, inspeção (`status`, `diff`, `log`) e ciclo de vida de alterações (`add`, `reset`, `rm`, `commit`, `revert`).
3. **Branches:** criação, navegação (`switch` / `checkout`), mesclagem (`merge`) e limpeza de ramificações.
4. **Resolução de conflitos:** identificação de marcadores de conflito e boas práticas antes do merge na `main`.
5. **Pull Request (PR):** repositórios remotos (`origin`), sincronização (`push`, `fetch`, `pull`) e fluxo de revisão.
6. **Fork e Fluxos de Trabalho:** diferença entre _Fork_ e _Hard Fork_ e resumo prático dos fluxos local, corporativo/próprio e open-source (`upstream`), como também uso do Git Tag.
7. **Integração com VS Code:** uso da aba _Source Control_, visualização de _diffs_ e resolução interativa de conflitos.
8. **Git Flow e Conventional Commits:** anatomia da mensagem de commit, tipos semânticos, convenção de branches e automação com `Commitlint` e `Commitizen`.
9. **`.gitignore` e `.gitkeep`:** regras de exclusão de arquivos locais/sensíveis e preservação de diretórios vazios.

---

## Ferramentas de Padronização de Commits (Commitizen e Commitlint)

Para aplicar o padrão **Conventional Commits** na prática durante os estudos, o ambiente local utiliza duas ferramentas complementares (mantidas fora do rastreamento remoto via `.gitignore`):

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

> **Nota:** Apenas clonar o repositório não instala nem ativa a validação automaticamente; é necessário ter o **Node.js/npm** instalado na máquina.

```bash
# Instalação das dependências de validação
npm install -D @commitlint/cli @commitlint/config-conventional

# Teste rápido via linha de comando
echo "feat: adiciona nova funcionalidade" | npx commitlint
echo "mensagem fora do padrao" | npx commitlint
```

_(Para automatizar a execução via Git Hooks com Husky, consulte a [documentação oficial de setup local do Commitlint](https://commitlint.js.org/guides/local-setup.html))._

---

## Referências Utilizadas nas Notas

### Curso Base e Materiais Introdutórios

- [TeoMeWhy — Introdução ao Git e GitHub (YouTube)](https://www.youtube.com/watch?v=Y_fFZjzw-D4&list=PLvlkVRRKOYFQyKmdrassLNxkzSMM6tcSL)
- [GitHub Git Cheat Sheet (PT-BR)](https://training.github.com/downloads/pt_BR/github-git-cheat-sheet/)
- [Tutorial Introdutório de Git e GitHub — HubSpot](https://product.hubspot.com/blog/git-and-github-tutorial-for-beginners)

### Documentação Oficial Git & GitHub

- [Pro Git Book — 1.1 Sobre Controle de Versão](https://git-scm.com/book/pt-br/v2/Come%C3%A7ando-Sobre-Controle-de-Vers%C3%A3o)
- [Pro Git Book — 1.5 Instalando o Git](https://git-scm.com/book/pt-br/v2/Come%C3%A7ando-Instalando-o-Git)
- [Pro Git Book — 2.2 Gravando Alterações no Repositório](https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository)
- [Pro Git Book — 2.3 Visualizando o Histórico de Commits](https://git-scm.com/book/pt-br/v2/Fundamentos-de-Git-Visualizando-o-Hist%C3%B3rico-de-Commits)
- [Pro Git Book — 2.5 Trabalhando com Remotos](https://git-scm.com/book/en/v2/Git-Basics-Working-with-Remotes)
- [Pro Git Book — 3.1 Branches em Poucas Palavras](https://git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell)
- [Pro Git Book — 3.2 Branches e Merges Básicos](https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
- [GitHub Docs — Sobre conflitos de merge](https://docs.github.com/pt/pull-requests/collaborating-with-pull-requests/addressing-merge-conflicts/about-merge-conflicts)
- [GitHub Docs — Sobre Pull Requests](https://docs.github.com/pt/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests)
- [GitHub Docs — Fazer fork de um repositório](https://docs.github.com/pt/pull-requests/collaborating-with-pull-requests/working-with-forks/fork-a-repo)
- [GitHub Docs — Sincronizar um fork](https://docs.github.com/pt/pull-requests/collaborating-with-pull-requests/working-with-forks/syncing-a-fork)
- [GitHub Docs — Ignorando arquivos (`.gitignore`)](https://docs.github.com/pt/get-started/getting-started-with-git/ignoring-files)
- [Coleção Oficial de Templates `.gitignore` — GitHub](https://github.com/github/gitignore)
- [VS Code Docs — Using Git source control in VS Code](https://code.visualstudio.com/docs/sourcecontrol/overview)

### Fluxos de Trabalho e Padronização de Commits

- [Conventional Commits v1.0.0 (PT-BR)](https://www.conventionalcommits.org/pt-br/v1.0.0/)
- [Atlassian — Gitflow Workflow](https://www.atlassian.com/br/git/tutorials/comparing-workflows/gitflow-workflow)
- [Commitlint — Documentação e Repositório Oficial](https://github.com/conventional-changelog/commitlint)
- [Commitlint — Local Setup (Hooks & Husky)](https://commitlint.js.org/guides/local-setup.html)
- [Commitizen (`cz-cli`) — Repositório Oficial](https://github.com/commitizen/cz-cli)
