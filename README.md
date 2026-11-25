# Curso TMW Git & Github 2025 by TeoMeWhy

Um curso para iniciarmos no aprendizado de controle de versionamento com a ferramenta GIT
(git version 2.56.0.windows.3) e a platafroma GitHub como repositório remoto.

1. Listagem de comandos para git bash e terminal;
2. Listagem de comandos para git
3. GitFlow
4. Integração com IDE Visual Studio Code

Para mais ifnormações e acesso ao curso:
Playlist do Curso no canal de Youtube [**TeoMeWhy - Introdução ao Git e Github**](https://www.youtube.com/watch?v=Y_fFZjzw-D4&list=PLvlkVRRKOYFQyKmdrassLNxkzSMM6tcSL)

## Validação de Commits (`commitlint`)

Apenas clonar o repositório com o arquivo `commitlint.config.js` **não executa a validação automaticamente** nem instala as dependências necessárias. O arquivo de configuração apenas define as regras do projeto — para validar mensagens de commit, é preciso ter o **Node.js/npm** e os pacotes do `commitlint` disponíveis no ambiente.

### Pré-requisitos e instalação

1. Tenha o **Node.js** e o **npm** instalados na máquina.
2. Instale o CLI do `commitlint` e a configuração convencional (localmente no projeto ou globalmente):

```bash
npm install --save-dev @commitlint/cli @commitlint/config-conventional
```

_(Caso queira testar sem instalar no projeto, o `npx` pode baixar/executar temporariamente se houver pacote/cache disponível no ambiente)._

### Como testar na linha de comando

```bash
echo "feat: adiciona nova funcionalidade" | npx commitlint
echo "mensagem fora do padrao" | npx commitlint
```
