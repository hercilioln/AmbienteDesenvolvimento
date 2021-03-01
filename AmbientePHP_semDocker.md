
# Instalação Ambiente Laravel PHP + PostgreSQL sem Docker no WSL2

Tutorial de instalacão do meu ambiente de desenvolvimento WEB com PHP e PostgreSQL sem docker, geralmente uso essas instruções para preparar meu ambiente de desenvolvimento no Windows utilizando o WSL2 (Windows Subsystem Linux 2).

## 1 - Instalação WSL2 no Windows 10
---
Há duas maneiras de instalar o WSL2 e nesse [**site**](https://docs.microsoft.com/pt-br/windows/wsl/install-win10) da própria Microsoft tem todas as etapas de instalação.
## 2 Instalando e Configurando o PostrgeSQL
---
Primeiramente gosto de preparar meu banco de dados e por isso instalo logo o PostgreSQL. Há um detalhe importante: o PostgreSQL depois de instalado não se conecta ao banco porque aparece um erro de servidor, nunca entendi o porquê, porém a soluçao é instalar ele como WSL1 e depois reverter para o WSL2 que vai funcionar perfeitamente. 
### 2.1 - Reverter WSL2 para WSL1
Primeiramente verifique qual versão sua distro está instalada, no PowerShell vai esse comando.  


```wsl --list --verbose```  

Aparecerá uma linha com a a distro e a versão do WSL e se caso estiver no WSL2 será necessário reverter a versão para que o Postrgers funcione 

```wsl --set-version <nome da distro> <versão do WSL>```

