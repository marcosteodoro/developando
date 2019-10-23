+++ 
draft = true
date = 2019-10-22T18:58:17-03:00
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

Os passos para a instalação em uma máquina com sistema operacional *Debian* ou com alguma distro baseada no mesmo pode ser encontrada neste [post](https://marcosteodoro.github.io/posts/dockerizando-seu-ambiente-de-desenvolvimento-php/).

Sem mais, vamos partir para a criação deste ambiente!

### *docker-compose.yaml*

Em uma pasta de sua preferência (onde os arquivos do seu projeto irão ficar posteriormente), crie um arquivo chamado *docker-compose.yaml* com o seguinte conteúdo: 

<script src="https://gist.github.com/marcosteodoro/06396ae7a243064903702cc547512ed8.js"></script>

Dentro da pasta onde foi criado o arquivo *docker-compose.yaml* crie um novo diretório e dê o nome de htdocs a ele.

``
mkdir htdocs 
``
