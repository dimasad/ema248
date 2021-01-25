---
layout: default
title: Prática 3 -- Acionamento de um LED com transistor seguidor de emissor
---


### {{ page.title }}
{:.no_toc}

O objetivo desta prática é analisar uma aplicação de um transistor bipolar
no modo ativo, para amplificação de corrente. Primeiro um circuito será 
dimensionado com base em uma especificação de desempenho e as folhas de dados
dos dispositivos escolhidos. Em seguida, um circuito semelhante deverá ser 
montado no ambiente de simulação e alguns de seus parâmetros medidos.

**Tópicos:**
* Procedimento x
* Procedimento y
{:toc}

Circuito
--------

O circuito desta prática é um amplificador de corrente na topologia seguidor
de emissor, cujo diagrama está mostrado na figura abaixo. Esse circuito é
utilizado para acionamento de um LED com o Arduino, e sua função é diminuir
a corrente fornecida pelos pinos digitais do microcontrolador. Assim é possível,
por exemplo, comandar um LED de alta potência utilizando o Arduino e um 
circuito relativamente simples. 
{%
   include figure.html
   file="led-seg-emissor.svg"
   img_style=""
   caption="Diagrama de circuito para acionamento de um LED com o Arduino
            utilizando um transistor NPN na configuração de seguidor
            de emissor."
%}

Uma característica interessante desta topologia é que o transitor não satura,
pois a tensão do coletor é sempre maior ou igual que a da base. Isso significa
que o ganho de corrente do transistor é sempre alto, apesar da desvantagem
que a tensão coletor--emissor não é tão baixa. Por causa disso, esse circuito
é recomendado para cargas de potência baixa a média, como LEDs, por exemplo.
