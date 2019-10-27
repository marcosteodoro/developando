+++ 
draft = true
date = 2019-10-27T11:32:17-03:00
title = "Montando seu ambiente de desenvolvimento Laravel utilizando Docker"
description = "Como utilizar o Docker para montar um ambiente de desenvolvimento Laravel completo utilizando todo o poder do framework"
slug = "" 
tags = ["docker", "laravel", "container", "devops", "php", "composer"]
categories = []
externalLink = ""
series = []
+++

## Montando seu ambiente de desenvolvimento Laravel utilizando Docker

Em breve teremos algumas postagens tratando alguns assuntos interessantes utilizando Laravel, e para aproveitar melhor esse tipo de conteúdo, nada melhor que um ambiente de desenvolvimento padronizado em nossas máquinas certo?!

Neste post iremos aprender como montar um ambiente de desenvolvimento completo para trabalhar principalmente com Laravel, porém, seguindo a mesma ideia é possível trabalhar com a maioria dos frameworks atuais de PHP.

Tendo essa padronização, é possível que rodemos exatamente os mesmos comandos em qualquer máquina, independente do sistema operacional, que o ambiente de desenvolvimento que rodará o projeto será o mesmo!  Dessa forma, nunca mais temos aquele clássico problema de "no meu computador funciona".

Para começar trabalhar com este ambiente devemos ter o *docker* e o *docker-compose* instalados em nossas máquinas (seja ela Windows, MAC ou Linux).

Os passos para a instalação em uma máquina com sistema operacional *Debian* ou com alguma distro baseada no mesmo podem ser encontrados neste [post](https://marcosteodoro.github.io/posts/dockerizando-seu-ambiente-de-desenvolvimento-php/).

Sem mais, vamos partir para a criação deste ambiente!

### *docker-compose.yaml*

Em uma pasta de sua preferência (onde os arquivos do seu projeto irão ficar posteriormente), crie um arquivo chamado *docker-compose.yaml* com o seguinte conteúdo: 

<script src="https://gist.github.com/marcosteodoro/06396ae7a243064903702cc547512ed8.js"></script>

O arquivo acima irá indicar todos os containeres que devem ser utilizados para a criação do ambiente que necessitamos para começar a desenvolver com o Laravel.

Esse ambiente conta com PHP 7.3, banco de dados Postgres SQL e Redis. Os containeres de PHP são do projeto Ambientum, e facilitam bastante nossa vida na criação dessa estrutura. Para saber mais em relação ao Ambientum e o que mais é possível fazer com ele dê uma conferida no docker hub neste [link](https://hub.docker.com/r/ambientum/php) ou no repositório do projeto no [github](https://github.com/ambientum/ambientum).

Ainda no mesmo diretório, rode o seguinte comando para fazer o download das imagens e colocar todo o ambiente para rodar:

``
docker-compose up -d
``

A primeira vez que rodar esse comando, é normal que demore um pouco pois o comando realiza o download de todas as imagens necessárias para subir os containeres que o ambiente necessita.

Após tudo executado, você terá o ambiente pronto para iniciar o trabalho com Laravel. Acessando o [localhost](http://localhost:8080) de sua máquina na porta 8080, terá o retorno de *404 not found*, e é sinal que seu ambiente foi configurado e está funcionando de acordo, porém ainda não colocamos nenhum arquivo no *directory root* da aplicação para ser exibido. (Caso ocorra algum erro por conta de portas já utilizadas em sua máquina, basta mudar o bind de portas no arquivo *docker-compose.yaml*).

Agora, mesmo sem ter o composer ou sequer o PHP em sua máquina, é possível que iniciemos um projeto Laravel, ou de qualquer outro projeto PHP, pois temos todas essas ferramentas configuradas no container!

Vamos iniciar um novo projeto digitando o seguinte comando no terminal:

``
docker-compose exec app composer create-project laravel/laravel my-awesome-project
``

O comando acima executa o comando *composer create-project laravel/laravel my-awesome-project* dentro do container, e como o mesmo está com o mapeamento de volumes com nossa máquina, teremos acesso à todos os arquivos do projeto no diretório da aplicação, onde se encontra o arquivo *docker-compose.yaml*.

Como resultado teremos o seguinte esquema de arquivos/diretórios em nossa aplicação:

<div class="align-center">
    <img src="/images/project-structure-after-composer-create-project.png" alt="Estrutura diretórios">
</div>

Aparentemente tudo functionando de acordo, porém, acessando o [localhost](http://localhost:8080) da aplicação, ainda temos aquele retorno de *404*...

Isso ocorre, por conta do *directory root* da aplicação estar esperando uma pasta public, na raiz do projeto. Portanto devemos mover nosso projeto para a raiz, e é possível fazer isso com o seguinte comando: 

``
mv my-awesome-project/* ./ && mv my-awesome-project/.* ./
``

Agora sim, temos um projeto Laravel fresquinho para iniciarmos o desenvolvimento!

E a pasta my-awesome-project da aplicação não tem mais motivo para existir, portanto podemos remove-lá com o seguinte comando:

``
rm -rf my-awesome-project 
``

Com este mesmo arquivo *docker-compose.yaml* é possível rodarmos projetos já existentes também, e o proceso fica bem facilitado nesse caso. Basta adicionar o mesmo na raiz do projeto e rodar o comando:

``
docker-compose up -d
``

Desta forma já teremos todo o ambiente necessário para rodar o projeto!

Lembrando que, para realizar o acesso do banco de dados de dentro do container, é necessário usar o host **postgres**, assim como os outros serviços definidos e mapeados em nosso *docker-compose.yaml*.

Em nossa máquina, graças aos binds, tudo pode ser acessado como *localhost*, como se fosse uma instalação realizada diretamente em nossa máquina.

Fico por aqui e espero ter ajudado!

-\-

Marcos Teodoro
