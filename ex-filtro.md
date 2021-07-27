---
layout: default
title: Exercício -- Resposta em frequência de um circuito ativo
---

### {{ page.title }}
{:.no_toc}

Considere o filtro ativo representado no circuito abaixo. Assumindo que o
amplificador operacional é ideal, responda às questões abaixo.

{%
   include figure.html
   file="filtro.svg"
   caption="Filtro ativo."
%}


1. Qual a função de transferência entre a tensão de entrada $$V_e(\omega)$$ e
   a tensão de saída $$V_s(\omega)$$?
2. Para os parâmetros de $$R_1=10\,\mathrm{k}\Omega$$, 
   $$R_2=15\,\mathrm{k}\Omega$$ e $$C=100\,\mathrm{nF}$$, plote com o auxílio do
   computador os gráficos do ganho e fase da resposta em frequência, para a
   frequência $$f$$ variando de 0&#x202f;Hz a 5&#x202f;kHz.
   Os gráficos devem ser plotados com escala linear nos eixos das abscissas e
   ordenadas. Qualquer ambiente computacional pode ser utilizado para gerar
   os gráficos.
3. Com base na resposta das questões anteriores, esse filtro é, 
   qualitativamente, passa-altas ou passa-baixas? Qual é a frequência de corte
   do filtro?
