# **Instalacão do terminal Zsh, configuração do Oh My Zsh e configuração do Alias**

Sempre que utilizo o linux eu uso esse terminal ao invés do bash, acho ele muito mais prático, limpo e fácil de usar. Com zsh ao dar o comando ``cd`` pra procurar um direitório, ao invés de digitar o nome do diretório só precisamos usar a tecla tab e navegar entre os diretórios de boa.

Primeiramente certifique que o ``git`` esteja instalado, pois vamos precisar dele mais na frente, caso nao esteja instalado é só digitar o seguinte comando:

````
sudo apt install git
````

Feito isso, agora vamos instalar o ZSH:

````
sudo apt install zsh
````
Ótimo, agora vamos precisar clonar um repositório do Oh My Zsh:

```
git clone https://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh
```
Clonado o repositório, agora será preciso criar o arquivo ``.zshrc`` que é um arquivo onde estará todas as configurações do zsh, nesse arquivo você pode mudar o tema, adicionar alias e outros. No meu caso eu só uso para adicionar os meus Alias, que são atalhos para que eu nao precise digitar comandos enormes que utilizo sempre. Logo mais vou ensinar como fazer os alias. 

Bom, agora crie o arquivo com esse comando:

````
cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc
````

Agora mude o padrão do seu terminal para o Zsh, já que ele ja vem como bash:

```
chsh -s $(which zsh)
```
Feito isso, será preciso reiniciar seu Linux, se tiver usando WSL é só fechar o terminal e abrir novamente.

Se você quiser mudar o tema do seu zsh, [aqui vai um link](https://github.com/ohmyzsh/ohmyzsh/wiki/themes) com vários temas. No meu caso eu sempre utilizo o que ja vem de padrão pra mim é o suficiente.

---
## **Utilizando Alias**


Para facilitar nosso trabalho ao utilizar o terminal. Localize o arquivo ``.zshrc`` , geralmente ele está na pasta raiz do seu sistema, depois de localizá-lo abra ele com seu editor. Bem no final você verá algo assim:
````
# Example aliases
# alias zshconfig="mate ~/.zshrc"
# alias ohmyzsh="mate ~/.oh-my-zsh"
````

Para explicar melhor, vamos entender: 
primeiro colocamos ``alias``, depois colocamos o nome do atalho ``zshconfig`` e depois o comando que será acionado ``"mate ~/.zshrc"``

No meu caso eu utilizo alguns padrões, como eu trabalho muito com o docker, ao invés de eu digitar ``docker-compose run --rm`` toda vez que for precisar de um comando, eu só coloco ``d-run``, veja abaixo:

````
alias d-run="docker-compose run --rm"
````
Aqui são alguns dos atalhos que utilizo no meu dia-a-dia nos meus trabalhos. 

```
alias d-up="docker-compose up -d"
alias d-down="docker-compose down"
alias d-run="docker-compose run --rm"
alias ..="cd .."
alias d-build="docker-compose up -d --build"
alias update-upgrade="sudo apt update && sudo apt upgrade -y"
alias update="sudo apt update"
alias gtadd="git add ."
alias gtm="git commit -m"
alias gtpm="git push origin master"
alias gtp="git push"
```

>**Lembre-se:** Depois de adicionar todos os alias, salve o arquivo e reinicie o terminal, depois é só usar de a vontade.

O Zsh tem vários plugins e temas, então existe uma possibilidade enorme de personalização, basta fazer uma pesquisa rápida que você vai encontrar, eu particularmente já deixo assim do jeito que vem mesmo.