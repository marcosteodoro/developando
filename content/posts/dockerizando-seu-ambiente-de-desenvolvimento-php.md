+++ 
draft = true
date = 2019-09-27T15:42:02-03:00
title = "Dockerizando seu ambiente de desenvolvimento PHP"
description = "Nesse post monstar um ambiente pronto para o desenvolvimento de aplicações PHP com Docker"
slug = "dockerizando-seu-ambiente-de-desenvolvimento-php" 
tags = ['docker', 'php', 'containerezed', 'lamp']
categories = ['devops', 'docker', 'php']
+++

## Dockerizando seu ambiente de desenvolvimento PHP (Debian e derivados)

Seguiremos agora com um passo a passo para montar seu ambiente de desenvolvimento PHP utilizando Docker e Docker Compose.

Primeiramente, vamos realizar a instalação do Docker.

### Instalando o Docker

O primeiro passo é realizar a remoção de instalações anteriores de Docker, e para isso digite o seguinte comando em seu terminal: 

``
sudo apt-get remove docker docker-engine docker.io containerd runc
``

Agora iremos atualizar os dados de seu repositório apt com o seguinte comando: 

``
sudo apt-get update
``

Instale os pacotes necessários para o processo: 

`` 
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg2 \
    software-properties-common
``


Adicione a chave GPG oficial do repositório do Docker:

``
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -
``

Inclua o repositório do Docker em sua source list: 

``
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/debian \
   $(lsb_release -cs) \
   stable"
``

Com o procedimento anterior realizado já podemos partir efetivamente para a instalação do Docker.

Vamos primeiro atualizar o repositório para sincronizar o novo repositório adicionado: 

``
sudo apt-get update
``

E agora sim instalaremos os pacotes para realizar a instalação da ferramenta: 

``
sudo apt-get install docker-ce docker-ce-cli containerd.io
``

Com tudo isso realizado  temos uma instalação de Docker realizada. Para validar se tudo está funcionando de acordo, podemos rodar o seguinte comando: 

``
sudo docker run hello-world
``

Caso tudo tenha sido instalado com sucesso, o comando a seguir deve realizar o download de uma imagem Docker e deve colocar a mesma para rodar. Caso ocorra algum erro reinicie os passos.

Com tudo isso instalado e funcionando de acordo é interessante facilitarmos um pouco as coisas, e rodar os comandos do Docker sem a necessidade de rodar o comando *sudo* nos ajuda muito nessa parte. Para isso é necessário rodar o comando a seguir para adicionar seu usuário atual ao grupo do Docker da máquina: 

``
sudo usermod -aG docker $USER
``

### Instalando o *docker-compose*

À partir deste ponto já temos o Docker instalado. Agora podemos seguir adicionando o *docker-compose* à nossa máquina pois o mesmo irá facilitar nossa vida com ambientes que devemos subir para iniciar a programação.

Inicialmente iremos realizar o download do script para rodar a ferramenta: 

``
sudo curl -L "https://github.com/docker/compose/releases/download/1.24.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
``

Após baixado o script, necessitamos das permissões necessárias para execução, e as mesmas são concedidas com o comando: 

``
sudo chmod +x /usr/local/bin/docker-compose
``

Para comodidade, podemos adicionar o link a seguir: 

``
sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
``

O mesmo nos possibilita executar o comando *docker-compose* de qualquer lugar de nossa máquina.

Apoś isso, podemos rodar o comando a seguir e ver se o retorno condiz com a versão atual do *docker-compose*: 

``
docker-compose --version
``

### E agora, finalmente  partiremos para nosso ambiente de programação PHP

Iremos utilizar um ambiente que criei. 

O mesmo conta com o PHP versão 7.2, rodando sob o Apache 2 e se conectando com um link com o banco de dados MariaDB em sua versão 10.3.

Realize o clone do repositório em sua máquina com o seguinte comando: 

``
git clone https://github.com/marcosteodoro/docker-apache-php72-mariadb103.git
``

Entre no repositório com o comando:

``
cd docker-apache-php72-mariadb103
``

E após isso podemos dar um:

``
docker-compose up
`` 

O comando irá realizar o download das imagens necessárias para o funcionamento do ambiente e já irá subir o mesmo. Com tudo rodando de acordo teremos um retorno de *phpinfo()* em nosso localhost.

Espero ter ajudado em algo, e qualquer problemma é só entrar em contato.

#### Menções honrosas

O post anterior foi escrito ouvindo [Cássia Eller](https://open.spotify.com/artist/10naVTwNjE50daQVrN0bXh?si=r1CTAJGMQDivpA9CNEBr5A), então qualquer problema pode ir reclamar diretamente com ela.

-\-

Marcos Teodoro

