# TEOMEWHY - GIT/GITHUB
1. Instalação e primeiros conceitos
2. Primeiros comandos
3. Branches
4. Resolução de conflitos
5. Pull Request (PR)
6. Fork
7. Integração com VS Code
8. Git flow
9. GitKeep / GitIgnore

## 1. Instalação e primeiros conceitos (commit)
- Software para gerenciamento de versão de arquivos de texto;
- Git é um software instalavel em qualquer plataforma -> open source (criado por Linux Tovards);
- instalação via gestor de pacotes do Windows
    **winget install --id Git.Git -e --source winget**
- instalação por outros gestores de pacotes:
    **<manager> install git**
- **git -v** ## versão do pacote atual no SO;
- **git update** ## comando para atualizar
- qual meu editor default do ambiente git?
    1. **git config --get core_editor** -> **git var GIT_EDITOR**
    2. **git config --global core.editor "<comando-do-editor>"** ## para configurar novos editores de texto;
        1. VS Code: git config --global core.editor "code --wait"
        2. Nano: git config --global core.editor "nano"
        3. Vim: git config --global core.editor "vim"
        4. Sublime Text: git config --global core.editor "subl -n -w"
- branch defaut: main -> antigamente usava master (mudança de cunho social-semantico)
- O conceito de 'commit' -> envio de status atual / progresso de alterações do arquivo para o stage local do git, como checkpoint, imagem atual do arquivo -> conjunto de alterações salvas no git para uso posterior;
- commit x versionamento -> podemos salvar diversos checkpoits de alterações em momentos diferentes, tendo versões do arquivo para uso/reuso/continuidade/retorno;
- versionamento x arvore de commits: precisamos de atenção para salvar alterações na arvore de nós com uso de versoes do commit para andar pelos nós/versões;

## 2. Primeiros comandos
### linha de comando - shell/bash/terminal
- **ls**: lista arquivos dentro do diretorio de trablho -> **dir** no windows;
    - **ls -a**: lista arquivos ocultos do direotiro
    - **ls <dir> <param etc>**: lista o conteudo do diretorio nivel abaixo, sem precisar acessar 
- **cd <diretorio>**: move entre diretorios
- **pwd**: retorna o caminho absoluto (path) do diretorio de trabalho
- **clear** ou **ctrl+L**: limpa as informações do terminal -> **cls** no windows
- **mkdir** : cria novo diretorio no diretorio atual
- **mv <"arquivo"> <dir>**: move o arquivo do repo atua para o repo abaixo -> atenção que ele faz uma copia
- **cat <arquivo>** :mostra o que tem dentro do arquivo
- **rm -rf <dir>**: exclui um diretorio -> atenção se ha arquivos dentro dele

### git - comandos iniciais
- **git init .** : promove o diretorio de trabalho em um repositorio git, embrulha o direotrio dentro d euma pasta invisivel do git
    - **git init <dir>**: existe mas não se recomenda aninhar diretorios e repositorios devido a conflitos e rastreios

#### extra
- **git config --global init.defaultBranch main**
- **git branch -m main**: renomeia a branch atual, no caso 'master > main'

### git - comandos de versionamento !
- **git status**: nome de branch atual - commits - tracked/untracked files - sugestoes
- **git add <file or .>**: adiciona arquivos para a pasta .git/ do working diretory -> stage
    - git add <file>: arquivo focal;
    - git add . : todos os arquivos do working diretory atual
    - git add file* / git add *.txt : todos os arquivos que iniciam com 'file' ou finalizam com certo tipo de arquivo;
    - **git ls-files --stage**: dentro do diretorio .git/, podemos ver os arquivos indexados para o stage do git
- **git commit -M "<msn>"**
 
- **git log** : ver o log dos commits feitos na branch do repo
    - **git log -1** : ver log do ultimo commit
 
- **git config --global user.email <"email">**
- **git config --global user.name <"nome do user">**

## 2. Branches

- **git diff <file>**: mostra o que foi alterado em cada commit realizado no arquivo em questão;
- **git reset <file>** : rollback do stage dos arquivos adicionados por git add
- **git checkout -b <nome da branch>**
- **git branch** : lista das branches do projeto
- **git checkout <branch>**: muda para branch selecionada

---


# GIT: ferramenta de controle de versão
[Github cheat sheet](https://training.github.com/downloads/pt_BR/github-git-cheat-sheet/)

1. ref(2020, Hubspot): [An Intro to Git and GitHub for Beginners (Tutorial)](https://product.hubspot.com/blog/git-and-github-tutorial-for-beginners)
2. ref: [2.2 Git Basics - Recording Changes to the Repository](https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository)
3. ref: [3.1 Git Branching - Branches in a Nutshell](https://git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell)
4. ref: [3.2 Git Branching - Basic Branching and Merging](https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
5. ref: [2.5 Git Basics - Working with Remotes](https://git-scm.com/book/en/v2/Git-Basics-Working-with-Remotes)

A ferramenta GIT precisa ser iniciada, por terminal ou UI dedicada, no repositório de interesse a se controlar o versionamento das versões. Em suma, inicie git na pasta onde está seu conteúdo a ser versionado, o chamado **working directory**

- **git init**: inicia um ambiente git para aquele working repositório


Com a criação, adição e modificação de arquivos no repositório iniciado com git (working directory), necessita-se saber se o git identificou o arquivo 'novo' e se ele está sendo acompanhado pelo software (**tracked / untracked**). Costume verificar o status de acompanhamento das modificações realizadas dentro do repositório para saber o que será designado para o git

- **git status**
- git status -s
  - A: no staging,
  - M: modificado,
  - MM: modificado, staging, modicado - há mudanças no staging e outras não ainda,
  - ??: não está tracked ainda
- git diff: linhas exatas das modificações feitas nos arquivos que não foram pro stagging
  - git diff --staged : modificações no staggin comparadas ao ultimo commit

Um commit é um registro da alteração feita em um repositório, registrado juntamente com o arquivo alterado. Esses registros formam uma linha de tempo das modificações realizadas. Podemos fluir nas versões de arquivo por essa linha do tempo a partir dos commits.
Antes de realizar um commit, é necessário colocar a modificação feita no chamado '**staging environment**' (o palco do repositório git, ou index).

![image.png](attachment:ec716361-1b6e-4288-8d9e-e32a32e879ea.png)

- **git add** . ou <file>: adiciona files do working directory para o staging environment, com uso de um index

Git Ignore
- [git bash e linux]cat .gitigonre *<padrão para quais arquivos ignorar no repo>
  - [window]: type .gitignore : visualizar a lista de arquivos a serem ignorados
  - echo *<padrão> > .gitignore
  - echo *<outro padrão para adição> >> .gitignore

![image.png](attachment:71d0a103-cfdb-409f-91b9-651085b158f0.png)

Emfim, registrar as modificações feitas na versão do seu repositório, com uma mensagem clara do que foi feito até esse commit.

- **git commit -m '<mensagem>'**: adiciona fo index para diretorio virtual de versões
ou

- git commit -v : verborragico das alterações feitas (semelhante ao git diff), possibilitando escrever, também, uma mensagem sobre.

Todo commit possui um identificador hash, único para cada commit, por onde podemos navegar o estado da versão:

- git revert <hash code name do commit>: retornamos as modificações do estado do projeto para o estado do commit pedido

Para remover arquivos do versionamento e 'tracking' do GIT, não basta deleta-los (ou tira-los) do working directory (repositório), precisa remover do staging e então commitar a alteração posteriormente.

- **git rm <arquivo ou padrão>**: remove o arquivo do staging, consolidando no proximo commit do repo
  - git rm <arquivo ou padrão> -f: se já houve git add das alterações feitas

Atráves da lógica de commits, o GIT consegue operacionalizar branches: estados separados do seu repositório (working directory), onde alterações são geridas para aquela branch, onde cada uma possui seu staging e lista de commits. No futuro, voce pode mergear o conteúdo da branch com a versão main/master de seu repo, em qualquer momento do fluxo de trabalho que faça sentido, e voltar para continuar de onde parou naquela branch.
Lembar que as branches e a master crescem em commits indepdnentemente, sendo necessário merges recorrentes para mante-las atualizadas em igualdade de alterações feitas pelo tempo.
A arovore GIT mantem ponteiro HEAD atualizado na branch ativa (após git checkout), e cada branch aponta para seu ultimo commit.
Antes de mudar de branches, certifique de manter as alterações em commits (staging are limpa e alterações comitadas). Ajuda no andamento do versionamento e conflitos de branch

- **git checkout -b <nome_da_branche>**: cria uma branch para o working directory e aponta para ela, para iniciar os trabalhos
- git branch: visualiza qual a branch atual e quais são as existentes para aquele repositório
  - git btanch <nome>: cria uma branch, mas não muda para ela
- git checkout <nome da branch>: muda para branch

Após commitar as alterações feitas em uma branch, ao mudar para outra, voce pode atualizar a atual com as alterações do ultimo commit da outra branch.
A qualquer momento voce pode trazer os dados de uma branch para outra com o git merge, a depender das etapas e interações do seu trabalho (user story, hotfix, production version, etc).
A depender do andamento do ponteiro de commit das branches, um merge pode significar a criação de um commit merge para unificar branches, ou pode ser necessário a resolução de conflitos, com escolha de mudanças, git add (staging area) e então git commit com as mudanças finais.

- **git merge <nome da branch à trazer as alterações>**: mergea na branch onde se chamou o comando, as alterações da branch chamada, logo, o ponteiro das 2 branchs apontam para o mesmo ultimo commit
- git branch -d <branch>: apaga a branch, geralmente utilizado após merge com a master/main/primary.
- git mergetool : ferramenta visual para resolução de conflitos de merge

Trabalhar com ferramentas online remotas de git, como github, traz beneficios como gerenciamento e agregação de repositórios na nuvem. 
Crie uma conta em um website, como github, e crie seu repositório e siga as instruções ou conecte com seu repositório working directory local, tambem.
Esse repositório remoto será a `origin` (origem) para onde commits de suas branches serão enviadas para sincronia remota com o comando `git push`. Lembrando que o repositório remoto pode contar com n branches daquela pasta de trabalho.

- **git remote add origin <URL_repositrio>**: cria um vinculo com repositorio que vc gerencia ou compartilha setando ele como origem atual do seu working directory; pode ser necessario vincular acesso de login e senha ou SSH key
- git remote show <nome do repo remoto>: mostra infos sobre o repo, pode ser o `origin`
- git remote add <shortname> <url>: cria um atalho para a URL do repositorio remoto de interesse
- git remote rename <nome do remote><novo nome>
- git remote remove <nome do remoto>: remover caso nao use mais ou houve mudança de servidor, etc

- **git push <remote> <branch>**: envia alterações da branch para o repo remoto.
- git push -u origin <branch da origem do push>: geralmente eh a master quando criamos o repo, mas pode variar e ser enviado as branch quando quiser
- **git push origin <nome da brunch>**: envia as alterações a serem atualizadas no repo na cloud

- **git clone <repo URL>**: chamar esse comando no nível de hierarquia de pasta desejado no gerenciador de pastas do S.O
- **git remote add upstream** <URL do repo original da conta de git do dono original>: fazer isso no repo clone
- **git fetch <remote repo>**: traz os arquivos que vem não tinha desde a ultima vez que voce clonou o repo, sendo necessario fazer um commit de merge manualmente (git merge). Voce pode usar o **git pull** no seu repo clone, que fara o merge com as atualizações da branch que voce nao tem
  - git fetch upstream
  - git merge upstream/main
 

O `pull request`são pedidos de revisão para commits/branches que alterarão os arquivos de um repositorio, para que os donos do mesmo revisem o que foi enviado pelo git push de determinado colaborador.

- Após o aceite de um PR, recomenda-se deletar a branch para evitar muitas branches em um projeto.

- **git pull** <remote> <branch>: traz o estado atual da branch apos aceites de PR, por exemplo, com a ação de merge com o que esta em seu repo local
  - git pull origin master
 
- **git log**: ver todos os commits feitos naquele repositório após a ultima sincronização, com indiação da branch
