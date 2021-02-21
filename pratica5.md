---
layout: default
title: Prática 5 -- Acionamento de um motor CC com ponte H
---

### {{ page.title }}
{:.no_toc}


O objetivo desta prática e da anterior é fazer o acionamento de um motor de
corrente contínua com o Arduino. Na prática anterior, o motor foi acionado em
somente um sentido, utilizando um único transistor NPN. Nesta, o motor será
acionado nos dois sentidos utilizando a ponte H do circuito integrado [L293D].
Essas aplicações são representativas do acionamento de cargas de potência
com dispositivos eletrônicos. Variações desses circuitos são utilizados, por
exemplo, para acionamento de placas de Peltier para aquecimento ou resfriamento,
solenóides, motores de passo, e motores de corrente alternada sem escovas
(_brushless_).

**Tópicos:**
* Procedimento x
* Procedimento y
{:toc}

Circuito de acionamento com a ponte H
-------------------------------------

Para operar o motor nos dois sentidos, é necessário um circuito que possibilite
aplicar a tensão da fonte no motor nos dois sentidos, isto é, invertendo os
terminais do motor. A ponte H é um dispositivo com 4 chaves que permite isso,
como mostrado no circuito abaixo. 
Suas saídas são os nós 1Y e 2Y, que estão conectados aos terminais do motor.
Cada metade da ponte é composta de duas chaves e uma saída, indicados na figura
pelos números 1 ou 2.
Quando a chave alta (H) está fechada, o nó de saída é conectado ao terminal 
de alimentação $$V_{\operatorname{CC}}$$.
Quando a chave baixa (L) está fechada, o nó de saída é conectado ao terminal 
ao terra.
Note que as chaves superior e inferior de uma mesma meia ponte não podem ser
fechadas ao mesmo tempo, senão teríamos um curto-circuito.

{%
   include figure.html
   file="ponte-h-chave.svg"
   caption="Ponte H para acionamento de um motor, representada com chaves."
%}

Desta forma, quando as chaves $$S_{1H}$$ e $$S_{2L}$$ estão fechadas,
é aplicada tensão no motor em um sentido. Já quando as chaves $$S_{1L}$$ 
e $$S_{2H}$$ são fechadas, é aplicada tensão no motor no outro sentido. 
Com isso, é possível fazer com que o motor gire em ambos sentidos de
rotação.


É possível construir uma ponte H com pelo menos 4 transistores bipolares,
mas iremos, para esta prática, utilizar o circuito integrado [L293D] que
possui 4 meia-ponte já implementadas, o que simplifica nossa montagem.
Com um L293D é possível fazer 2 ponte H, o que pode ser utilizado para acionar
2 motores CC ou um motor de passo bipolar de duas fases, por exemplo. 
O circuito com 
transistores da saída de cada meia ponte é mostrado na Figura 5 da folha de 
dados. Observe que o dispositivo já tem os diodos de roda livre para proteção
contra cargas indutivas como motores. A folha de dados também mostra vários
exemplos de aplicação.

Esse circuito possui duas entradas de alimentação, VCC1 e VCC2. A alimentação
VCC1 supre a lógica interna do dispositivo e deve ter uma tensão de 5V; a
entrada VCC2 alimenta a carga, aceitando uma tensão de 4,5V a 36V. As duas
fontes de alimentação devem ter uma referência comum, que é o pino terra.
Há vários terra no CI para melhorar a dissipação de calor.
Não é necessário conectar todos, pois eles são conectados internamente, mas 
isso é boa prática em montagens mais permanentes. 

Cada meia ponte do L293D possui 2 entradas (EN e A) e uma saída (Y). A entrada
EN (enable) serve para habilitar ou desabilitar a meia ponte. Quando ela está
em nível lógico baixo a saída Y está aberta. Quando a ponte está habilitada 
(entrada EN em nível lógico alto), a tensão na saída Y é VCC2 quando A está em
nível lógico alto e 0V quando A está em nível lógico baixo. Observe também
que temos só duas entradas de enable, uma para cada par de meia ponte.

A montagem desta parte da prática está mostrada na figura abaixo.
Utilizaremos a mesma fonte para alimentar o CI e o motor,
por isso VCC1 e VCC2 devem estar ligados na fonte de 5V do Arduino.
Conecte também os pinos terra do CI no terra do Arduino. Como manteremos a ponte
habilitada o tempo todo, conecte também a entrada 1,2EN no 5V. 
Um detalhe é que, novamente, a tradução automática dos nomes dos
pinos no Tinkercad ficou esquisita, _terra_ foi traduzido como _solo_.
Para comandar a
ponte, conecte as entradas 1A e 2A da ponte às saídas digitais 9 e 10 do
Arduino, respectivamente. Por fim, conecte as saídas da ponte 1Y e 2Y aos 
terminais do motor. Os demais pinos não precisam ser conectados.

{%
   include figure.html
   file="l293-montagem.svg"
   caption="Montagem para acionamento do motor com a ponte H integrada L293D."
%}

> ## Montagem: Teste do acionamento
>
> O primeiro teste consiste em ligar o motor em um sentido, aguardar 1s, 
> desligar o motor, aguardar 1s, ligar o motor no outro sentido, aguardar 1s,
> desligar o motor, aguardar 1s e repetir. Esse programa serve para ver se a
> montagem foi feita corretamente e se é possível acionar o motor nos dois 
> sentidos.
>
> Para ligar o motor em um sentido, deve-se colocar a saída 10 em nível lógico
> alto e a 9 em baixo. Para inverter o sentido, basta inverter as saídas: 10 em
> nível baixo e 9 em alto. O motor é parado quando ambas as saídas estão no 
> mesmo nível lógico, alto ou baixo.


> ## Montagem: Aceleração e desaceleração gradual
>
> O segundo teste consiste em acionar o motor com uma tensão gradual de -5V a
> 5V, utilizando modulação por largura de pulso, depois acionar com tensão
> de 5V a -5V e repetir o ciclo. O motor deverá parar suavemente e trocar de
> sentido de rotação.
> 
> Para fazer modulação por largura de pulso com a ponte H, eu sugiro manter
> um dos seus lados em nível lógico zero enquanto o outro é acionado com 
> uma onda em PWM. Para inverter o sentido, faça a mesma coisa trocando os
> lados da ponte, o que estava em PWM fica em zero enquanto o que estava em
> zero envia uma onda com modulação por largura de pulso.


> ## Atividade: Comando pelo potenciômetro
>
> Utilize um potenciômetro e uma entrada analógica do Arduino para comandar a
> tensão no motor. Quando o potenciômetro estiver na posição central o motor
> deverá estar parado, quando estiver em um extremo o motor deverá ser acionado
> com 5V e quando estiver no outro extremo o motor deverá ser acionado com 
> tensão -5V. Nas posições intermediárias a tensão no motor deverá ser
> proporcional à posição do potenciômetro.
>
> Observe que o ponteciômetro deverá somente servir como interface para o
> comando do usuário, sua conexão com a ponte H é feita exclusivamente por 
> software. Salve no Tinkercad com o nome de "Prática 5".
>
> Utilizando um voltímetro, meça a tensão no motor quando o comando do 
> potenciômetro estiver em cada um dos extremos. Qual é a queda de tensão
> nos transistores da ponte?


[L293D]: L293D.pdf

[analogWrite]: https://www.arduino.cc/en/Reference/AnalogWrite
[analogRead]: https://www.arduino.cc/en/Reference/AnalogRead
[map]: https://www.arduino.cc/en/Reference/map
