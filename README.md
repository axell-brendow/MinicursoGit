# CONTROLE DE VERSÕES POR GIT

Instalação e alguns usos

## Primeiros passos

1. Instalar git

    1. Linux
        - Abrir um terminal e acionar o comando

            ```sudo apt-get install git git-core```
  
    2. Windows

        - [Download git for Windows](https://git-for-windows.github.io/)

        - Seguir as instruções para instalação do BitBucket ou GitHub:

            - BitBucket:
            
                https://www.atlassian.com/br/git/tutorials/install-git#windows

            - GitHub:
            
                https://help.github.com/pt/github/getting-started-with-github/set-up-git#setting-up-git

        - Selecionar as seguintes opções:

            ![Installation Components](https://i.imgur.com/kLhE0bS.jpg)

            ![Installation Editor](https://i.imgur.com/s47bFlW.png)

            Esta opção irá adicionar alguns comandos do Linux no ambiente do Windows
            ![Installation PATH](https://i.imgur.com/Y0r8CA1.jpg)

            ![Installation Line Endings](https://i.imgur.com/vH2qgpQ.jpg)


2. Após instalar o git

    1. Criar uma conta no GitHub ou Bitbucket.

    2. Criar um repositório. Um exemplo para o [GitHub](https://github.com/new):

        ![Exemplo criando repositório GitHub](https://i.imgur.com/xm7WJCt.jpg)

        Após criar, clique no botão para copiar o link
        ![Exemplo copiando o link do repositório](https://i.imgur.com/snz2V1V.jpg)

    2. Abrir o **terminal** (no Linux) ou 
      **PowerShell** (no Windows). Caso esteja no prompt do Windows, basta rodar o comando powershell.

    3. Configurar o seu nome de usuário do GitHub ou Bitbucket para identificar futuras interações.

        ```git config --global user.name <seu_nome_de_usuário>```

    4. Configurar o seu email de usuário do GitHub ou Bitbucket para identificar futuras interações.

        ```git config --global user.email <seu_email>```

    5. Para verificar as configurações realizadas:

        ```git config --global user.name```
        ```git config --global user.email```
    

## Criando o seu primeiro repositório git

3. Para criar o seu próprio repositório git:

    1. Criar uma pasta (por exemplo, project).

        ```mkdir project```
  
    2. Mudar para a pasta criada.

        ```pushd project```
  
    3. Criar um repositório git dentro dela.

        ```git init```

    4. Verificar a exist?ncia da pasta .git criada. Tudo sobre o repositório git está nela.

        ```ls -la``` (Linux)

        ```ls -fo``` (Windows/PowerShell)

    5. Criar um arquivo do tipo LEIA-ME, por enquanto não monitorado pelo git (untracked).

        ```echo "Commit inicial" > README.md```

    6. Abrir o arquivo criado em um editor de texto e acrescentar uma descrição do projeto.
  
        OBS.:
        É possível configurar um editor padrão:

        ```git config --global core.editor <nome_do_executavel_do_editor>``` ex.: notepad++

        OBS.:
        É possível configurar um comparador padrão (Útil para quando tivermos mais de uma versão dos arquivos):

        ```git config --global merge.tool <nome_do_executavel_do_comparador>``` ex.: diff

        OBS.:
        Para conferir as configurações:

        ```git config --list```

        OBS.:
        Para obter informações sobre os comandos, a qualquer momento:

        ```git help <comando>```

        ```git <comando> --help```

        ```man git-<comando>```

        Por exemplo:

        ```git help config```

    7. Verificar o estado do repositório após a criação desse arquivo:

        ```git status```

        ![Exemplo git status inicial](https://i.imgur.com/9nH0B4y.jpg)

        Observe que o arquivo README estará na lista de *Untracked Files*. Isso significa que o git não está monitorando as mudanças que ocorrem nele, ou seja, ele é só um arquivo normal no seu PC.

    8. Adicionar o arquivo no stage (palco). O stage é onde ficam os arquivos que estão sendo monitorados pelo git. Além disso, o git só salva o estado de arquivos que estejam no stage.

        ```git add README.md```

        Obs.: O arquivo foi apenas adicionado no stage. O estado dele ainda não foi salvo.

        Se desejar desfazer o ```git add```:

        ```git reset README.md```

    9. Verificar o novo estado do repositório:

        ```git status```

        Observe que agora o README está na lista de *Changes to be commited* (Mudanças a serem confirmadas).
      
    10. Confirmar a mudança do arquivo.

        ```git commit -m "Adiciona o README"```

        ![Exemplo git commit inicial](https://i.imgur.com/SaiTNF8.jpg)

        Com isso você acabou de salvar um estado (uma versão) dos arquivos que estavam no stage. No caso, apenas o README.md.

        OBS.:
        Até esse ponto a interação é local. Nada terá sido transferido para o repositório remoto.

        Se desejar mudar a mensagem do último commit feito:

        ```git commit --amend```

        Se desejar mudar o autor do último commit feito, primeiro faça o ```git config user.name``` e o ```git config user.email``` e, então, rode:

        ```git commit --amend --reset-author```

    Transição dos arquivos para os comandos git add, commit e checkout:

    ![Transição dos arquivos ao executar git add, commit e checkout](https://hackernoon.com/hn-images/1*zw0bLFWkaAP2QPfhxkoDEA.png)
      

## Trabalhando com repositórios remotos


4. Para trabalhar com um repositório remoto:

    1. Para linkar o seu repositório local com um repositório remoto:

        ```git remote add origin "https://github.com/USUARIO/REPOSITORIO"```

        O comando ```git remote add <apelido_repo> <url>``` serve para adicionar vias de conexão entre o seu repositório local e um repositório remoto.
        
        Neste caso, estamos dando o apelido *origin* para o link https://github.com/username/repository.
        
        Esse apelido (*origin*) é apenas uma convenção que usamos para representar o repositório remoto mais comum que você se conecta a partir deste repositório local.
    
        Para saber todas as vias de conexão remota do seu repositório local:

        ```git remote -v```

    2. Para enviar o estado do seu repositório local para o remoto:
    
        ```git push origin master```

        O comando ```git push <apelido_repo> <ramo ou branch>``` serve para enviar o estado local da branch especificada para a branch equivalente no repositório remoto com o apelido especificado.

        É importante ressaltar que ao rodar o comando ```git init```, a branch master (ramo mestre/principal) sempre é criada por padrão.

    3. Para verificar as últimas atualizações:

        ```git status```

    4. Se fizer alterações nos arquivos (por exemplo, README.md), adicioná-los ao stage (palco) para que o git possa salvar o novo estado deles.

        ```git add README.md```
    
        OBS.:
        Se você quiser adicionar todos os arquivos monitorados e não monitorados no stage:

        ```git add .```

        ou

        ```git add *```
    
    5. Identificar a modificação feita no repositório local:

        ```git commit -m "Incrementa o README"```

        Obs.: Se você tiver modificado apenas arquivos que já estão sendo monitorados (git add feito), não é necessário fazer o add novamente. Basta rodar o comando ```git commit -am "mensagem"``` que a opção -a se encarregará de adicionar todos os arquivos monitorados.
    
    6. Submeter as alterações para o repositório remoto.
    
        ```git push --set-upstream origin master```

        A opção ```--set-upstream <apelido_repositorio> <ramo ou branch>``` cria um vínculo entre a branch local e a branch remota equivalente (geralmente com o mesmo nome). Com isso, ao fazer git push origin, o git já saberá por exemplo que a master local se conecta com a master remota e não com outra branch remota.

        Para futuras submissões ao mesmo repositório basta usar:
        
        ```git push```

    ![Exemplo com todos os comandos](https://i.imgur.com/LXB9v17.jpg)
        

5. Para baixar/clonar um repositório remoto para o seu PC:

    ```git clone <url>```

## Operações comuns num repositório

6. Para remover arquivo(s) do repositório:

    ```git rm <arquivo>```

    ```git rm *.tmp```

7. Para renomear um arquivo:

    ```git mv <nome_antigo> <nome_novo>```

8. Para substituir um arquivo pela última versão dele:

    ```git checkout -- <arquivo>```

9. Para trazer o estado do repositório remoto para o seu repositório local:

    ```git pull origin master```

    Esse comando irá baixar o estado da branch master remota e irá tentar mesclar isso com o estado da sua branch master local.

    OBS.:
    Para verificar as configurações de envio e download entre o repositório local e o remoto:

    ```git remote show origin```

10. Para remover uma referência remota:

    ```git remote rm <apelido_repo>```

11. Para renomear uma referência remota

    ```git remote rename <apelido_antigo> <apelido_novo>```
    

## Branchs (ramos)

![Visualização de 3 branchs em paralelo](https://backlog.com/app/themes/backlog-child/assets/img/guides/git/collaboration/using_branches_001.png)

Essa imagem traz um exemplo do porquê de criar diferentes ramos em seu repositório. Enquanto o ramo principal (commits A, B e C) está operando em produção, você pode ter outros ramos para desenvolvimento de novas features ou conserto de bugs.

12. Trabalhando com ramos (branchs):

    1. Listar ramos existentes:

        ```git branch```

    2. Verificar ramos ocultos:

        ```git branch -a```

    3. Criar um ramo e já mudar para ele:

        ```git checkout -b NOME_DO_NOVO_RAMO```

    4. Mudar de ramo: 

        ```git checkout NOVO_RAMO```

    5. Retornar ao ramo principal:  

        ```git checkout master```



## Referências

CHACON, Scott; STRAUB, Ben. Pro Git Book. Apress, Disponível em: 
<https://git-scm.com/book/en/v2>. 
Acesso em: 28 de nov. de 2019.

Set up git. Disponível em: 
<https://help.github.com/en/github/getting-started-with-github/set-up-git>.
Acesso em: 28 de nov. de 2019.

Learn Git with Bitbucket Cloud. Disponível em: 
<https://www.atlassian.com/git/tutorials/learn-git-with-bitbucket-cloud>.
Acesso em: 28 de nov. de 2019.

README MinicursoGit. Disponível em: 
<https://github.com/axell-brendow/MinicursoGit>.
Acesso em: 01 de dez. de 2019.
