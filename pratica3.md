---
layout: default
title: Prática 3 -- Acionamento de um LED com transistor seguidor de emissor
---


### {{ page.title }}
{:.no_toc}

O objetivo desta prática é analisar a aplicação de um transistor bipolar
no modo ativo para amplificação de corrente. Primeiro um circuito será 
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

Atividade para entrega: Dimensionamento
---------------------------------------

Considere agora o dimensionamento do resistor $$R$$ para acionamento de um LED
de potência modelo [VLWR9632], da [Vishay], cuja corrente nominal é de 
70&#x202F;mA,
bem acima do máximo que o Arduino pode suprir por seus pinos de saída digital.
Utilize as informações do transistor NPN de uso geral [BC549] para o 
dimensionamento e análise. 

Para esse circuito:

1. Escolha o valor de $$R$$ para acionar o LED com sua corrente nominal de
   70&#x202F;mA quando a saída do Arduino estiver em nível lógico alto, 
   5&#x202F;V. Para tal, utilize a tensão direta típica do LED da tabela de 
   características ópticas e elétricas, e a tensão base--emissor da 
   Figura&nbsp;2 das características de desempenho típico do transistor.
2. Estime a corrente de base $$i_B$$ quando o LED estiver aceso. Para tal, 
   utilize o ganho de corrente CC típico do modo ativo, mostrado na 
   Figura&nbsp;3.
3. Estime a potência dissipada no transistor. Esse valor está abaixo do máximo
   aceitável, de acordo com as informações da folha de dados?

Atividade para entrega: Simulação
---------------------------------

Simule agora esse circuito no tinkercad com $$R=120\,\Omega$$.
Acione o LED com a saída digital e meça as seguintes grandezas:

1. a corrente de base no transistor;
2. a corrente no LED;
3. a tensão base--emissor do transistor.

Lembre-se que o amperímetro deve ser ligado em série com o circuito de 
interesse. Já o voltímetro, por outro lado, deve ser ligado em paralelo.
Coloque os valores medidos no relatório. Observe que tanto o LED quanto o 
transistor NPN do Tinkercad são um pouco diferentes dos dispositivos analisados
na atividade anterior, mas seu comportamento qualitativo é muito parecido.

[BC549]: BC549_npn.pdf
[Vishay]: https://www.vishay.com/
[VLWR9632]: https://www.vishay.com/docs/81818/vlwr963.pdf
