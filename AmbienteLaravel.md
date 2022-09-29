
# **Instalação do PHP, PostgreSQL, pgAdmin, Composer e Laravel**

Tutorial de instalacão do meu ambiente de desenvolvimento WEB com PHP e PostgreSQL, geralmente uso essas instruções para preparar meu ambiente de desenvolvimento no Windows utilizando o WSL2 (Windows Subsystem Linux 2).

## **1 - Instalação WSL2 no Windows 10 ou 11**

Agora você pode instalar tudo o que precisa para executar o WSL (Subsistema do Windows para Linux) inserindo este comando no PowerShell administrador ou no Prompt de Comando do Windows e reiniciando o computador quando finalizar a instalação.

```
wsl --install
```  
Ao digitar esse comando, ele ja instala automaticamente o Ubuntu, caso queria instalar outra distro linux no WSL2, verifique as instruções [nesse link.](https://docs.microsoft.com/pt-br/windows/wsl/install)

## **2 - Instalando e Configurando o PostrgeSQL**

Primeiramente gosto de preparar meu banco de dados e por isso instalo logo o PostgreSQL. 

---
### **2.1 - Instalação do PostgreSQL**

```
sudo apt update

sudo apt install postgresql postgresql-contrib libpq-dev
```


> **Importante:** Por alguma razão sempre que for abrir a sua distro no WSL o postgres vem desativado, pra isso é preciso sempre ativá-lo, os comandos abaixo serão muito comuns, recomendo criar um alias pra cada um desses. Nesse outro [tutorial](/InstalacaoZSH.md) eu ensino como fazer isso.

#### Verifica o status:
```
sudo service postgresql status
```

#### Ativar:
```
sudo service postgresql start
```

#### Desativar:
```
sudo service postgresql stop
```

---
### **2.3 - Configurando a sua própria senha e usuario para o Postgres**

Abra o terminal e digite o seguinte comando:

```
sudo -u postgres createuser "username"
```
>Obs: coloque o nome de usuário sem as aspas

Essa senha é para entrar no server do postgres

```
sudo passwd postgres
```

Digite a senha e depois reinicie o seu terminal.

Depois de reiniciado, agora digite o seguinte comando:

```
 sudo -u postgres psql
```

esse comando vai abrir o shell do postgres, nele voce vai alterar a Role para uma senha nova

```
ALTER USER "username" PASSWORD 'password';
```
>Importante: Em username é pra colocar sem aspas. Em password é necessário deixar as aspas simples!

--- 

## **3 - Instalando e Configurando o PgAdmin**

Baixe e instale o PgAdmin no Windows, baixe a última versão atualizada. [Aqui](https://www.pgadmin.org/download/pgadmin-4-windows/)

Abra a sua distro e verifique se o posgtres está ativado.

#### Verificar status:
```
sudo service postgresql status
```

#### Ativar:
```
sudo service postgresql start
```

Abra o PgAdmin e provavelmente irá pedir uma senha, nesse caso coloque a mesma configurada anteriormente para o Postgres, agora com o botão direito do mouse vá em: 

**Servers -> Create -> Server**

Abrirá um janela e na aba **General** escolha um nome para o seu server, eu geralmente coloco **localhost**.

Na aba **Connection**:

Host name/address coloque: ```127.0.0.1```

Maintenance database: ````postgres````

Username: ````postgres````

Password: ````postgres````

> **Impotante:** Essas configurações acima são as padrões e prefiro deixar assim por pura comodidade mesmo, porém se você quiser pode mudar o Username e Password, [aqui tem um tutorial de como fazer isso](https://harshityadav95.medium.com/postgresql-in-windows-subsystem-for-linux-wsl-6dc751ac1ff3). 

Depois clique em save e seu server estará conectado e funcionando.

### **3.1 - Criando banco de dados**

Com o mouse direito clique em **Database -> Create -> Database**
Escolha o nome do seu banco de dados e abaixo o **Owner**

Pronto, banco de dados configurado e funcionando perfeitamente. 
> **Observação:** Não se esqueça de fazer o a reversão do WSL1 para o WSL2, acima está as instruções é só fazer o inverso.

---

## **4 - Instalando Laravel, PHP e Composer**

Primeiramente antes de instalar o Laravel, precisamos instalar o PHP e o Composer que é o gerenciador de pacotes do PHP.

### **4.1 - Instalação do PHP**

Primeiro atualize as dependências e depois instale o PHP:
```
sudo apt update

sudo apt install php php-cli php-fpm php-json php-common php-mysql php-pgsql php-zip php-gd php-mbstring php-curl php-xml php-pear php-bcmath

```

### **4.2 - Instalação do Composer**

**1 - Instalando as dependências**
```
sudo apt update

sudo apt install curl php-cli php-mbstring git unzip
```
**2 - Baixando e Instalando o Composer**

````
cd ~

curl -sS https://getcomposer.org/installer -o composer-setup.php
````
Obtendo o HASH mais recente do instalador baixado.

```
HASH=`curl -sS https://composer.github.io/installer.sig`
```

Se você quiser verificar o valor obtido, execute:

```
echo $HASH
```

Agora execute o código PHP para verificar se o script de instalação está pronto para ser executado:

```
php -r "if (hash_file('SHA384', 'composer-setup.php') === '$HASH') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"

```

Você verá o seguinte resultado:

```
Installer verified
```

> Se a saída diz ````Installer corrupt````, você precisará baixar o script de instalação novamente e verificar se você está usando o hash correto. Em seguida, repita o processo de verificação. Quando você tiver um instalador verificado, você pode continuar.

Para instalar o composer globalmente, use o seguinte comando que baixará e instalará o Composer como um comando disponível em todo o sistema chamado composer, sob ``/usr/local/bin`` :

```
sudo php composer-setup.php --install-dir=/usr/local/bin --filename=composer
```

Você verá um resultado parecido com este:
```
All settings correct for using Composer
Downloading...

Composer (version 1.10.5) successfully installed to: /usr/local/bin/composer
Use it: php /usr/local/bin/composer
```

Para verificar a instalação execute:

```
composer
```
Você verá algo mais ou menos assim:

```
   ______
  / ____/___  ____ ___  ____  ____  ________  _____
 / /   / __ \/ __ `__ \/ __ \/ __ \/ ___/ _ \/ ___/
/ /___/ /_/ / / / / / / /_/ / /_/ (__  )  __/ /
\____/\____/_/ /_/ /_/ .___/\____/____/\___/_/
                    /_/
Composer version XX

Usage:
  command [options] [arguments]

Options:
  -h, --help                     Display this help message
  -q, --quiet                    Do not output any message
  -V, --version                  Display this application version
      --ansi                     Force ANSI output
      --no-ansi                  Disable ANSI output
  -n, --no-interaction           Do not ask any interactive question
      --profile                  Display timing and memory usage information
      --no-plugins               Whether to disable plugins.
  -d, --working-dir=WORKING-DIR  If specified, use the given directory as working directory.
      --no-cache                 Prevent use of the cache
  -v|vv|vvv, --verbose           Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug
...
```
---

### **4.3 - Instalação e Configuração do Laravel**

Com o PHP, Composer e PostgreSQL instalados e funcionando, é hora de instalar e configurar o Laravel, essa é a parte mais fácil de todo o processo, veja a seguir:

```
composer create-project --prefer-dist laravel/laravel "Seu-Projeto"
```
> **Observação: coloque o nome do seu projeto sem as aspas!**

Configurando o seu arquivo ``.env`` e conexão com o banco de dados:

Abra seu editor ou IDE para configurá-lo. De acordo com as configurações feitas no pgAdmin agora vamos passar aquelas configurações para o ``.env`` e essa parte deve se parecer com isso aqui:
```
DB_CONNECTION=pgsql
DB_HOST=127.0.0.1
DB_PORT=5432
DB_DATABASE=seubanco
DB_USERNAME=postgres
DB_PASSWORD=postgres
```
Feito a conexão com o banco de dados agora vamos gerar uma chave para a sua aplicação através da linha de comando ``artisan``:

```
php artisan key:generate
```

Agora vamos rodar as migrations:

```
php artisan migrate
```

Por padrão o Laravel já vem com um servidor interno, então não precisamos utilizar o apache ou nginx por exemplo, basta apenas executar o seguinte comando:

```
php artisan serve
```

Será exibido algo assim:

```
Starting Laravel development server: http://127.0.0.1:8000
[Tue Mar  2 00:43:56 2021] PHP 7.4.3 Development Server (http://127.0.0.1:8000) started
```
No seu navegador é só colar o endereço do server que será algo assim: ``http://127.0.0.1:8000``

---

Tudo certo, agora é só praticar. Meu objetivo com isso é mostrar meu ambiente de desenvolvimento que sempre utilizo no meu dia-a-dia e possivelmente ajudar alguém que esteja procurando por algum tutorial fácil. 

Se tiver algum erro ou sugestões manda uma DM no meu [**Twitter**](https://twitter.com/hercilioln)