---
layout: default
title: Prática 4 -- Acionamento de um motor CC com um transistor NPN
---


### {{ page.title }}
{:.no_toc}


O objetivo das próximas duas práticas é fazer o acionamento de um motor de
corrente contínua com o Arduino. Nesta prática, o motor será acionado em
somente um sentido, utilizando um transistor NPN. Na próxima, será acionado
nos dois sentidos utilizando a ponte H do circuito integrado [L293D].
Essas aplicações são representativas do acionamento de cargas de potência
com dispositivos eletrônicos. Variações desses circuitos são utilizados, por
exemplo, para acionamento de placas de Peltier para aquecimento ou resfriamento,
solenóides, motores de passo, e motores de corrente alternada sem escovas
(_brushless_) ou de indução.

**Tópicos:**
* Procedimento x
* Procedimento y
{:toc}


Circuito de acionamento com um transistor NPN
---------------------------------------------

Abaixo temos o diagrama de um circuito para acionamento de um motor de corrente
contínua com um Arduino usando um transistor NPN. Os terminais do transistor
(coletor, emissor e base) estão indicados. Em antiparalelo com o motor temos
um diodo de roda livre para proteger a chave, pois o motor é uma carga indutiva.
O acionamento da base do transistor é feito pelo pino digital 9 do Arduino.
Quando a saída está em nível lógico alto (5V) o transistor está saturado,
operando como chave fechada. Quando a saída está em nível lógico baixo (0V) o
transistor está em corte, operando como chave aberta.

{%
   include figure.html
   file="motor-npn.svg"
   caption="Circuito para acionamento do motor com um transistor NPN."
%}

Se utilizarmos o modelo de chave para o transistor, o circuito acima é 
equivalente a este mostrado abaixo. Observe que com este circuito, só é
possível acionar o motor em um sentido. Isso porque o torque, em um motor
de corrente contínua de ímã permanente, é proporcional à corrente. Para se
inverter o sentido do torque, é necessário inverter o sentido da corrente,
o que não é possível com este circuito.

{%
   include figure.html
   file="motor-chave.svg"
   caption="Circuito equivalente ao de acionamento do motor, 
            com o transistor modelado como uma chave."
%}

Monte esse circuito em um protoboard no ambiente de simulação. Vale lembrar que
ambos os terminais do motor tem a mesma função, se forem trocados a única coisa
que se alter é o sentido da rotação mecânica que, nesta prática, não importa.
Com esse circuito, faça as atividades abaixo.

> ## Montagem: Teste do acionamento
>
> A função da primeira montagem é testar as conexões do circuito. Consiste
> simplesmente em testar a funcionalidade básica do sistema: abrir e fechar
> a chave. Faça então um código para o Arduino que liga o motor, aguarda 1s, 
> desliga o motor, aguarda 1s e repete o processo do início. Esse é o programa
> mais simples que testa se tudo está ligado corretamente.
>
> **Dica:** Lembre de configurar o pino 9 como saída com a função `pinMode`.


> ## Montagem: Aceleração e desaceleração gradual
>
> Utilizando modulação por largura de pulso, como na prática anterior, é 
> possível fornecer uma tensão média no motor entre 0V e 5V. Para o segundo 
> teste, faça um programa que, periodicamente, varie a tensão média no motor
> gradualmente de 0V a 5V e depois de 5V a 0V.
> 
> **Dica:** Utilize a função [analogWrite], como feito com o LED na prática
> anterior.


> ## Atividade para entrega: Comando pelo potenciômetro
>
> Faça agora uma atividade para a entrega que combina elementos testados 
> nas duas montagens anteriores. Adicione um potenciômetro ao circuito, leia
> a tensão com uma entrada analógica e utilize esse valor para comandar a 
> tensão média no motor, através da modulação por largura de pulso. A tensão 
> média no motor deverá ser igual à tensão medida no potenciômetro.
> Salve o circuito no Tinkercad com o nome "Prática 4: NPN". 
> 
> **Dica:** Utilize as funções [analogRead] e [analogWrite] como feito na 
> prática 2.

> ## Atividade para entrega: Quedas de tensão no transistor
>
> Nesta atividade para entrega, meça com um voltímetro as quedas de tensão
> entre a base e o emissor $$v_{be}$$, e entre o coletor e o emissor $$v_{ce}$$
> quando a saída do Arduino estiver em nível lógico alto. Com base nas medidas,
> em que modo o transistor está operando? Avalie se é razoável aproximar o 
> transistor por uma  chave fechada, como na Figura&#8239;2, nesta aplicação. 
> Inclua essas considerações no relatório.

> ## Atividade para entrega: Corrente de base
>
> Como calcular a corrente de base do trasistor? Utilizando as características
> típicas de um transistor de silício (veja as equações do resumo do 
> Capítulo&nbsp;3 do livro do Boylestad e Nashelsky), estime a corrente de 
> base para o circuito da figura abaixo. Meça a corrente de base com um
> amperímetro e compare.

{%
  include figure.html
  file="motor-npn-5v.svg"
  caption="Circuito para medição da corrente de base."
%}




[L293D]: https://www.ti.com/lit/ds/symlink/l293.pdf

[analogWrite]: https://www.arduino.cc/en/Reference/AnalogWrite
[analogRead]: https://www.arduino.cc/en/Reference/AnalogRead
[map]: https://www.arduino.cc/en/Reference/map
