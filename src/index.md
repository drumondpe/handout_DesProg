Algoritmo de Karatsuba
======

O algoritmo
---------
O Algoritmo de Karatsuba é uma técnica eficiente de multiplicação, encontra aplicação significativa na área de computação, especialmente em operações que envolvem números grandes. Essa abordagem é particularmente útil em algoritmos de multiplicação de números inteiros de grande magnitude, com impacto notável em campos como criptografia, processamento de sinais e processamento de grandes conjuntos de dados.

Considere, por exemplo, a aplicação do Algoritmo de Karatsuba em criptografia RSA, um sistema amplamente utilizado para segurança de comunicações online. Em RSA, a multiplicação de números primos extremamente grandes é uma operação fundamental. O uso do algoritmo de Karatsuba nesse contexto permite reduzir significativamente o número de operações de multiplicação, otimizando o desempenho do sistema.

Além disso, em ambientes de processamento de grandes volumes de dados, como em aplicações de aprendizado de máquina e análise de dados massivos, o Algoritmo de Karatsuba pode ser empregado para acelerar operações de multiplicação em aritmética de precisão arbitrária. Isso se traduz em ganhos de eficiência computacional, permitindo o processamento mais rápido e eficaz de tarefas intensivas em cálculos.

Suponha que precisamos multiplicar dois números grandes, como `md 12345678901234567890` e  `md 98765432109876543210`. O Algoritmo de Karatsuba divide esses números em partes menores, realiza multiplicações recursivas e, na etapa de combinação, emprega estratégias inteligentes para reduzir a quantidade de operações.

A multiplicação convencional desses números exigiria uma quantidade significativa de operações individuais. No entanto, o Algoritmo de Karatsuba quebra esse processo em etapas menores, reduzindo a carga computacional. Essa abordagem se torna ainda mais evidente à medida que lidamos com números cada vez mais extensos.


Para facilitar o seu entendimento, ilustraremos um exemplo com números menores para entender o mecanismo de maneira mais simples. Suponha que desejamos multiplicar os números `md 1234` e `md 5678`. O Algoritmo de Karatsuba divide cada número em duas partes aproximadamente iguais: 

* Número 1: `md 12` e `md 34` 
* Número 2: `md 56` e `md 78` 

??? Atividade 1: Equilibrando os números

Quando dividimos o número ao meio, a parte mais significativa está "perdendo" suas casas decimais (a casa de milhar e das centenas), se fizermos a soma `md 12 + 34` não vamos chegar no número `md 1234` então é necessário que desloquemos os números mais significativos para suas devidas casas.

Faça isso para os números `md 1234` e `md 5678` que já foram separados

::: Gabarito

* $X = (12 * 10^{4/2}) + 34$ 
* $Y = (56 * 10^{4/2} ) + 78$ 

Assim, somando os números, voltaríamos a ter `md 1234` e `md 5678`
  
:::
???

??? Atividade 2: Dando nome aos números 

Da separação anterior, temos que:

* `md a = 12`
* `md b = 34`
* `md c = 56`
* `md d = 78`
* `md n = 4` 
n representa o número de dígitos do número

Como ficam `md X` e `md Y` quando substituímos seus números pelas respectivas letras?

::: Gabarito
* $X = (a * 10^{n/2}) + b$  
* $Y = (c * 10^{n/2}) + d$  
:::
???

??? Atividade 3: Multiplicação dos dois números 

Faça a multiplicação $X * Y$, aplicando a distributiva

::: Gabarito
* $XY = ((a * 10^{n/2}) + b) * ((c * 10^{n/2}) + d)$
* $XY = ac * 10^n + ((ad) + (bc)) * 10^{n/2} + bd$
:::
???

??? Atividade 4: Fórmula da Multiplicação Recursiva
Com essa fórmula em mãos, podemos aplicar uma lógica para possuirmos apenas `md 3` multiplicações **diferentes**, ao invés de `md 4`.

Vamos chamar nossa equação de `md I`:

$I: XY = ac * 10^n + ((ad) + (bc)) * 10^{n/2} + bd$

E essa outra equação de `md II`:

$II: XY = ac * 10^n + ((a + b)(c + d) - bd - ac) * 10^{n/2} + bd$

Se expardirmos o produto $(a+b)(c+d)$ da segunda equação, teremos a seguinte expressão:

$(a+b)(c+d) = ac + ad + bc + bd$

De que forma podemos fazer com que a segunda equação se torne a primeira?

::: Gabarito
Subtraindo $ac$ e $bd$ da expressão:

$(a+b)(c+d) − ac − bd = ad + bc$

Agora, substituindo isso de volta na fórmula I, obtemos a fórmula II. A ideia é evitar calcular $ad$ e $bc$ separadamente, pois isso requer duas multiplicações adicionais. Em vez disso, podemos calcular $(a+b) × (c+d) − ac − bd$ em uma única multiplicação e reduzir a complexidade computacional do algoritmo de Karatsuba.

{red}(**$XY = ac * 10^n + ((a + b)(c + d) - bd - ac) * 10^{n/2} + bd$**)
:::
???

??? Exercício 1: Utilizando a fórmula da multiplicação recursiva
A partir da fórmula da multiplicação recursiva, resolva a multiplicação `md 1234` x `md 5678`

::: Gabarito
* Passo I: $ac = 12 * 56 = 672$ 

* Passo II: $bd = 34 * 78 = 2.652$

* Passo III : $(a+b)(c+d) = (12 + 34) * (56 + 78) = 6.164$

* Passo IV: $6.164 - 2.652 - 672 = 2.840$

* Passo V: $6.720.000 + 284.000 + 2.652 = 7.006.652$
:::
???

Agora vamos fazer outro exercício para fixar o conteúdo

??? Exercício 2

Faça a multiplicação dos números `md 234567` x `md 345678`. Lembre de usar a fórmula da multiplicação recursiva.

::: Gabarito
Temos que `md a = 234`, `md b = 567`, `md c = 345`, `md d = 678`, `md n = 6` 

* Passo I: $ac = 234 * 345 = 80.730$

* Passo II: $bd = 567 * 678 = 384.426$

* Passo III: $(a+b)(c+d) = (234 + 567) * (345 + 678) = 819.423$

* Passo IV: $819.423 - 384.426 - 80.730 = 354.267$

* Passo V: $80.730 * 10^6 + 354.267 * 10^3 + 384.426 = 81.084.651.426$
:::
???

Complexidade do algoritmo
---------
Vamos calcular juntos a complexidade do Algoritmo de Karatsuba! 

Como visto no tópico anterior, esse código realiza três chamadas recursivas, divisões, potências de 10 e combinações por soma e subtração.
Sendo assim, usaremos a receita para cálculo da complexidade de funções recursivas, vista na `md Aula 8`: 

1. Escreva a recorrência; 
2. Construa a árvore; 
3. Calcule um limitante para a altura; 
4. calcule a “soma de vermelhos” (parte não-recursiva das expansões) de cada andar.

??? Exercício 1
Escreva a recorrência do Algoritmo de Karatsuba. 

`md Dica 1:` A recursão é chamada três vezes com n/2.

`md Dica 2:` Podemos usar a multiplicação tradicional quando o maior algarismo tiver menos de 2 dígitos.

::: Gabarito
``` py
         /
        | 1             se n < 2;
f(n) = <
        | 3f(n/2)       se n >= 2.
         \
```
:::
???

Agora que temos a recorrência, podemos construir a árvore.

??? Exercício 2
Construa a árvore de complexidade do Algoritmo de Karatsuba.
:::
![](karatsuba.jpg)
:::
???

Feito isso, estimaremos a altura h da árvore.

??? Exercício 3
Calcule um limitante para a altura da árvore. 
::: Gabarito
``` py
Tamanho n divide por 2 a cada andar enquanto for maior que 2.
No antepenúltimo andar (h-2), ainda não chegamos na base.
n / 2^(h-2) > 2
n > 2 * 2^(h-2)
n / 2 > 2^(h-2)
log2(n / 2) > h - 2
h < log2(n/2)+2

h = O(log n), ou seja, h <= c log n
```
:::
???

Com a altura podemos calcular a soma de todas as "folhas", e assim chegar à complexidade do Algoritmo de Karatsuba. 

??? Exercício 4
Some a parte não recursiva de cada andar.  
::: Gabarito
``` py
Ao longo dos andares, temos
  (1 + 1 + 1 + ... + 1) + 1
= (h - 1) + 1
=  h

Como h <= c log n, pelas regras de simplificação
podemos concluir que a complexidade é O(log n).
```
:::
???

??? Complexidade de Tempo do Algoritmo de Karatsuba
Denotamos por T(n) o consumo de tempo do algoritmo. Nosso código realiza divisões, três chamadas recursivas, combinação por soma e subtração, além de multiplicações adicionais e potências de 10.
Com isso, o tempo total de execução ficaria: 

$$ T(n) = 3T(n/2) + O(n) $$

A solução dessa relação de recorrência é *O(n^log2(3))*, que é aproximadamente *O(n^1.58)*. Em comparação, o algoritmo de multiplicação tradicional tem uma complexidade de *O(n^2)*.
???


Portanto, para números muito grandes, o algoritmo de Karatsuba é mais eficiente em termos de complexidade do que a multiplicação tradicional.