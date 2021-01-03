---
layout: default
title: Prática 1 -- Familiarização com o Laboratório
---

### {{ page.title }}
{:.no_toc}

Esta primeira prática tem como objetivo a familiarização com o ambiente de 
simulação e os principais elementos do laboratório de eletrônica. O [Tinkercad]
foi escolhido para simulação pois simula vários dos componentes que utilizamos
no laboratório, de uma maneira muito semelhante à que fazemos experimentalmente.
Nesta prática, iremos ver o uso do Arduino, do protoboard, e de LEDs.
Antes de começar, crie uma conta no Tinkercad e entre na sala de aula virtual,
conforme orientações na página de 
[Práticas no Ensino Remoto Emergencial][praticas-ere].

**Índice:**
* Procedimento x
* Procedimento y
{:toc}

Primeiros Passos com Arduino
----------------------------

Nesta seção da prática o Arduino será apresentado, junto com os primeiros 
passos para sua utilização. Serão mostrados alguns exemplos simples de
como simular um programa e usar a comunicação serial para monitorar seu
funcionamento.

### Sobre o Arduino

O Arduino é uma plataforma de hardware e software livre para prototipagem e 
desenvolvimento de projetos eletrônicos.
É desenvolvida em torno de um microcontrolador [ATmega328P], um processador
programável com interfaces para conectar a dispositivos, sensores e circuitos
dos mais diversos tipos.
O _firmware_ do microcontrolador é atualizado através da porta USB,
que também pode ser usada para alimentar o circuito.
O Arduino Uno, modelo utilizado nas práticas, pode ser visto na 
figura abaixo.

{%
   include figure.html
   file="arduino_uno.png"
   caption="Um Arduino Uno. 
            Fonte: [learn.sparkfun.com], licença Creative
            Commons Attribution Share-Alike."
%}

O Arduino é programado na linguagem C++, podendo também ser programado em C
ou diretamente em linguagem de máquina.
Para maiores informações sobre a linguagem e interface de programação do
Arduino, consulte a  [Documentação de Referência da Linguagem][arduino-ref].
Existe uma grande bibliografia complementar e literatura disponível na internet
sobre o Arduino. Um livro que eu gosto bastante é o [Arduino Cookbook],
mas para os objetivos desta disciplina basta a funcionalidade mais básica da
plataforma. Iremos utilizar o Arduino somente para explorar e aplicar os
conceitos estudados na teoria de eletrônica.

### Utilizando o Arduino no Tinkercad

Para utilizar o Arduino no Tinkercad, basta incluir o dispositivo 
"Arduino Uno R3" na montagem. Uma vez feito isso, é possível programá-lo
através da aba código, no canto superior direto da página. 
No Tinkercad, existe a possibilidade de programação utilizando uma
liguagem gráfica de blocos, mas não iremos usar essa funcionalidade na 
disciplina pois não corresponde ao que utilizamos no laboratório nem no
ambiente profissional. Por isso, selecione a modalidade "Texto" ao invés
de "Blocos" na caixa de seleção abaixo da aba de código. Todos esses
elementos são mostrados na figura abaixo.

{%
   include figure.html
   file="tinkercad_prog.svg"
   img_style="width: 100%"
   caption="Elementos principais da interface de programação do Arduino no
   Tinkercad."
%}

O programa default do Arduino no Tinkercad é o exemplo _[Blink]_, que faz
o LED da placa piscar na frequência de 0,5&nbsp;Hz.
O programa, reproduzido abaixo, mostra o esqueleto de um programa de Arduino.
O código que estiver no
corpo da função `setup` será executado uma vez, quando a placa for energizada, 
geralmente para configurar a placa e inicializar as variáveis do programa.
Já o código que estiver no corpo da função `loop` será executado repetidamente 
até a placa ser desligada; esse código contém a lógica de execução do programa.
Todo o texto que estiver depois dos caracteres `//` é um comentário.

```
void setup()
{
  pinMode(13, OUTPUT);
}

void loop()
{
  digitalWrite(13, HIGH);
  delay(1000); // Wait for 1000 millisecond(s)
  digitalWrite(13, LOW);
  delay(1000); // Wait for 1000 millisecond(s)
}
```

No programa acima, a função [pinMode] serve para configurar o modo de operação
dos pinos do Arduino. 
A chamada `pinMode(13, OUTPUT)` configura o pino 13, que está 
conectado internamente ao LED da placa, para que opere no modo de saída digital.
A função [digitalWrite], por sua vez, define o nível de tensão da saída como
alto (`HIGH`, correspondente a 5&nbsp;V) ou baixo 
(`LOW`, correspondente a 0&nbsp;V).
Por fim, a função [delay] pausa a execução do programa por um certo número de
milissegundos. Tudo isso junto faz com que o LED da placa pisque, permanecendo
1&nbsp;s ligado e em seguida 1&nbsp;s desligado.
Teste esse programa clicando em "Iniciar simulação" e observe seu funcionamento.

### Comunicação serial

A porta USB do Arduino pode ser utilizada também para transferência de dados
entre a placa e o computador, além de servir para carregar o programa. Ela está
conectada à porta serial do microcontrolador, uma interface básica de 
comunicação entre dispositivos digitais. Entre outras coisas, a porta serial
permite a impressão de texto do programa do Arduino, para monitoração e
_debug_ dos programas.

No código fonte, a porta serial é acessada através do objeto [Serial], que é
parte da biblioteca padrão do Arduino. O programa abaixo mostra um exemplo 
simples de comunicação serial. Antes de utilizar a porta, é necessário chamar
a função [Serial.begin] para inicializá-la e definir a taxa de transmissão de
dados (_baud rate_). Essa inicialização geralmente é feita na função `setup`.
Uma vez inicializada, a função [Serial.println] pode ser chamada para imprimir
um texto ou variável seguido por uma quebra de linha.

```
void setup() {
  Serial.begin(230400); // Inicializa a porta Serial
  Serial.println("Hello World!!!"); // Imprime um texto
}

void loop() {
  delay(1000); // Aguarda 1 segundo
  Serial.println("Oi de novo."); // Imprime outro texto novamente
}
```

Copie esse programa para o Tinkercad e inicie a simulação.
O resultado pode ser visto no Monitor serial, e consiste em uma mensagem
"Hello World!!!" seguida de "Oi de novo." impresso repetidamente. Um
exemplo do resultado da simulação pode ser visto na figura abaixo.

{%
   include figure.html
   file="tinkercad_hello.png"
   caption="Resultado esperado da simulação do programa _Hello World_."
%}


As funções [Serial.print] e [Serial.println] também podem ser utilizadas para
imprimir variáveis do programa. Abaixo temos um exemplo que mostra o valor de
uma [variável global][scope] do tipo `int` (número inteiro), declarada no 
início do programa. Após a função `setup` inicializar a porta serial, na
função loop o valor da variável é impresso, incrementado, e a execução do
pausada por 250&nbsp;ms até terminar e ser executada novamente.
Simule esse programa e observe sua saída com o Monitor serial.

```
int i = 0; // Define uma variável global

void setup() {
  Serial.begin(115200); // Inicializa a porta Serial
}

void loop() {
  Serial.print("O valor de i = ");  // Imprime um texto
  Serial.println(i); // Imprime o valor da variável
  i = i + 1; // Incrementa a variável

  delay(250); // Pausa a execução por 250ms
}
```


> ### Atividade para entrega
>
> Crie um programa para o Arduino que imprime na porta serial um número de 0 a
> 5 e depois de 4 a 1 novamente, repetindo as sequências indefinidamente.
> Coloque no relatório o código fonte do programa e salve no Tinkercad como
> "Prática 1---Serial". 
>
> **Dica:** existem duas principais maneiras de se fazer esse programa:
> 
> - utilizando dois laços [for] na função `loop`; ou
> - utilizando uma variável global para definir o valor do incremento do 
> contador, e alterando esse valor ao chegar nos extremos.
>
> Consulte a [API do Arduino][arduino-ref]. Para maiores informações a respeito
> da linguagem.

Acionamento de um LED
---------------------

Nesta parte da prática, será mostrado como fazer uma montagem no protoboard
para acionamento de um LED. 
Em um primeiro momento, o LED será ligado diretamente na fonte e, 
posteriormente, será acionado programaticamente por uma saída digital do
Arduino.

### Componentes utilizados

**Protoboards**, também denominados matrizes de contato, são placas para a
construção de protótipos de circuitos eletrônicos.
São compostos de uma placa com orifícios sobre faixas de condutores metálicos,
como mostrado na figura abaixo.
Dessa forma, os terminais sobre a mesma faixa de condutores estão todos 
conectados eletricamente, sem a necessidade de solda.
Além da conexão elétrica, os protoboards também tem a função de fixar 
mecanicamente os componentes.
As trilhas verticais nas bordas da placa, marcadas com linhas contínuas 
vermelhas e azuis, são geralmente utilizadas para os terminais da fonte de
alimentação. Para mais informações e fotos de protoboards por dentro,
veja [este guia](https://portal.vidadesilicio.com.br/protoboard/) bem
explicativo.

{%
   include figure.html
   file="protoboard.jpg"
   caption="Um protoboard e sua matriz interna de contatos.
            Fonte: [learn.sparkfun.com], licença Creative
            Commons Attribution Share-Alike."
%}

No Tinkercad, não é necessário utilizar protoboards para realizar a simulação,
mas eu gostaria que eles fossem utilizados para exercitar a montagem como é
feita no laboratório. O protoboard aparece como "placa de ensaio" na biblioteca
do Tinkercad. Ao se passar o mouse sobre um de seus pinos, os demais pontos da
mesma linha ou coluna, conectados internamente, são indicados em verde.

**LEDs.**
Os diodos emissores de luz (_light-emitting diode_, LED) são dispositivos
semicondutores que convertem energia elétrica em energia luminosa com alta
eficiência.
Por serem diodos, os LEDs possuem polaridade, caso seja conectado ao circuito
com seus terminais invertidos ele não acenderá.
Os terminais do LED podem ser identificados como mostrado na figura abaixo.
O pino do catodo é mais curto e marcado por um chanfro no encapsulamento
do componente, que pode ser identificado na vista superior do dispositivo.
Os terminais também podem ser identificados com a função de teste de diodo do
multímetro.

{%
   include figure.html
   file="led.svg"
   img_class="max-width-200px"
   caption="Como identificar os terminais de um LED.
            
            Fonte: [commons.wikimedia.org], imagem liberada em domínio público."
%}

No Tinkercad, o chanfro do LED é desenhado para identificação dos seus 
terminais. Apesar disso, a maneira mais fácil de identificar os terminais é
passando o mouse por cima deles, o que faz com que seu nome seja mostrado.
Nesse ponto, vale mencionar que o Tinkercad tem alguns erros de tradução,
e o catodo do LED é identificado incorretamente como "catódica".


**Resistores.**
Para acionar um LED também é essencial o uso de um resistor.
No laboratório, é comum os alunos esquecerem do resistor ao ligar o LED,
o que faz com que ele emita um brilho muito forte e bonito.
Acontece que esse também será também será o último brilho do LED, pois ocorre 
devido à queima do componente por sobrecorrente.

O valor da resistência de resistores de furo passante é indicado com o código
de cores mostrado na figura abaixo, no qual cada cor equivale a um dígito.
As duas primeiras faixas indicam os algarismos significativos da resistência,
a terceira faixa indica a um multiplicador e a quarta indica a faixa de
tolerância do valor. Observe que, ao alterar o valor da resistência no
Tinkercad, o código de cores do resistor é atualizado.

{%
   include figure.html
   file="codigo_de_cores_resistores.png"
   caption="Código de cores para identificação da resistência de resistores.
            Fonte: [digikey.com]."
%}

### Acionamento básico

A primeira montagem de teste do circuito consiste em acionar o LED diretamente
na fonte de 5&nbsp;V do Arduino. O diagrama do circuito e uma possível maneira
de montá-lo no protoboard estão representados na figura abaixo. 
Monte o circuito no Tinkercad, simule, e verifique se o LED acende.

{%
   include figure.html
   file="led-fonte-pratica1.svg"
   caption="Diagrama esquemático do circuito para acionamento do LED direto
            com a fonte e um exemplo de como montá-lo no protoboard."
%}

> ### Atividade para entrega
>
> A escolha do resistor utilizado no acionamento do LED é baseda na corrente
> que se deseja fornecê-lo que, por sua vez, é proporcional à luminosidade 
> emitida por ele.
> Utilizando o modelo simplificado do LED, apresentado na seção 1.9 do livro
> do Boylestad e Nashelsky, escolha o valor de resistores para que a corrente
> do LED seja de 5&nbsp;mA, 10&nbsp;mA e 20&nbsp;mA. Considere a queda de 
> tensão no LED, o parâmetro $$V_K$$ do modelo, igual a 2&nbsp;V.
> Simule o circuito com esses valores de resistência e meça a corrente
> através do LED com um multímetro. Mostre no relatório o valor de resistência
> escolhido e a corrente medida. Salve a montagens com um dos resistores no
> Tinkercad como "Prática 1---LED".
>
> **Obs.:** o modo de medição de corrente do multímetro do Tinkercad também
> foi incorretamente traduzido como "Amperagem". Lembre também que o amperímetro
> deve ficar em série com o circuito.

### Acionamento com uma saída digital

O comportamento dos pinos do Arduino pode ser definido e controlado por
software.
Quando um pino é configurado como saída digital, ele se torna uma fonte de
tensão que pode assumir dois valores: nívelo lógico baixo (0 V) ou 
alto (5 V).
Neste procedimento, vamos utilizar uma saída digital do Arduino para acionar
o LED. Esse exemplo é basicamente o pisca pisca do exemplo [Blink] com um
LED externo à placa.

**Funções para uso das saídas digitais.**
Para configurar o pino como saída, a função [pinMode] deve ser utilizada.
Geralmente essa configuração é feita na função `setup`, que é executada
toda vez que o dispositivo é ligado.
O nível de tensão do pino é então definido com a função [digitalWrite].
Abaixo temos um código que exemplifica o uso das saídas digitais.

**Montagem.**
Para testar esse código, monte o circuito representado na 
figura abaixo, que é acionado pela saída digital do Arduino.
Quando a saída estiver em nível lógico alto, o LED irá acender.
Quando estiver em nível lógico baixo, o LED irá apagar.

{%
   include figure.html
   file="led-porta-digital-pratica1.svg"
   caption="Montagem para acionamento do LED com uma saída digital do Arduino."
%}

Para comandar o Arduino, utilize o código abaixo. Ele faz o LED piscar ao
ligar e desligar a saída digital de número 10. Simule o circuito e veja
seu funcionamento.

```
void setup() {
  pinMode(10, OUTPUT); // Define o pino digital 10 como saída
}

void loop() {
  digitalWrite(10, HIGH); // Define a tensão do pino 10 em 5V
  delay(1000);  // Aguarda 1s

  digitalWrite(10, LOW); // Define a tensão do pino 10 em 0V
  delay(1000); // Aguarda 1s
}
```

[arduino-ref]: https://www.arduino.cc/reference/pt/
[Arduino Cookbook]: https://www.oreilly.com/library/view/arduino-cookbook/9781449399368/
[ATmega328P]: http://www.microchip.com/wwwproducts/en/ATmega328p
[Blink]: https://www.arduino.cc/en/Tutorial/BuiltInExamples/Blink
[commons.wikimedia.org]: http://commons.wikimedia.org
[delay]: https://www.arduino.cc/reference/pt/language/functions/time/delay/
[digikey.com]: http://www.digikey.com
[digitalWrite]: https://www.arduino.cc/reference/pt/language/functions/digital-io/digitalwrite/
[for]: https://www.arduino.cc/reference/pt/language/structure/control-structure/for/
[learn.sparkfun.com]: http://learn.sparkfun.com/
[pinMode]: https://www.arduino.cc/reference/pt/language/functions/digital-io/pinmode/
[praticas-ere]: /ema248/praticas-ere/
[scope]: https://www.arduino.cc/reference/pt/language/variables/variable-scope-qualifiers/scope/
[Serial]: https://www.arduino.cc/reference/pt/language/functions/communication/serial/
[Serial.begin]: https://www.arduino.cc/reference/pt/language/functions/communication/serial/begin/
[Serial.print]: https://www.arduino.cc/reference/pt/language/functions/communication/serial/print/
[Serial.println]: https://www.arduino.cc/reference/pt/language/functions/communication/serial/println/
[Tinkercad]: http://tinkercad.com/

[if]: http://arduino.cc/reference/en/language/structure/control-structure/if
[>]: http://arduino.cc/reference/en/language/structure/comparison-operators/greaterthan
[<]: http://arduino.cc/reference/en/language/structure/comparison-operators/lessthan
