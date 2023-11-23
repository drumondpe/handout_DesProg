Algoritmo de Karatsuba
======
Quanto tempo é necessário para multiplicar dois números naturais?
---------

Depende. Algumas multiplicações podem ser feitas de cabeça, por exemplo, **2x2**. Mas e **13166566948 x 561584877879**?
Se esses dois números têm `md a` e `md b` dígitos respectivamente, o algoritmo usual consome tempo proporcional a `md a × b`.

O algoritmo que aprendemos na escola resolve o problema em tempo proporcional a n². Existe algum algoritmo mais rápido? SIM, o **Algoritmo de Karatsuba**.

O algoritmo
---------

O Algoritmo de Karatsuba divide os números em partes menores e aplica a multiplicação recursivamente, mas com uma estratégia inteligente de combinação dos resultados intermediários. 

A redução nas multiplicações ocorre na etapa de combinação, onde são realizadas multiplicações menores em vez de multiplicar todos os dígitos individualmente. Dificilmente deve ter ficado claro, por isso vamos deduzir uma fórmula para ficar mais claro.

Suponha que desejamos multiplicar os números `md 1234` e `md 5678`. O Algoritmo de Karatsuba divide cada número em duas partes aproximadamente iguais: 

* Número 1: `md 12` e `md 34` 
* Número 2: `md 56` e `md 78` 

??? Atividade 1: Equilibrando os números

Quando dividimos o número ao meio, a parte mais significativa está "perdendo" suas casas decimais (a casa de milhar e das centenas), se fizermos a soma `md 12 + 34` não vamos chegar no número `md 1234` então é necessário que desloquemos os números mais significativos para suas devidas casas.

Faça isso para os números `md 1234` e `md 5678` que já foram separados

::: Gabarito
* X: `md (12 x 10^(4/2)) + 34 ` 
* Y: `md (56 x 10^(4/2)) + 78 ` 

Assim, somando os números, voltaríamos a ter `md 1234` e `md 5678`
  
:::
???

??? Atividade 2: Dando nome aos números 

Da multiplicação anterior, temos que:

* `md a = 12`
* `md b = 34`
* `md c = 56`
* `md d = 78`
* `md n = 4` 
n representa o número de dígitos do número

Como ficam `md X` e `md Y` quando substituímos seus números pelas respectivas letras?

::: Gabarito
* `md X = ((a x 10^(n/2)) + b`  
* `md Y = ((c x 10^(n/2)) + d`  

:::
???

??? Atividade 3: Multiplicação dos dois números 

Faça faça a multiplicação `md X x Y`, aplicando a distributiva

::: Gabarito

* `md XY = ((a x 10^(n/2)) + b) x ((c x 10^(n/2)) + d`
* `md XY = ac x 10^n + ((a x d) + (b x c)) x 10^(n/2) + bd`

:::
???

Com essa fórmula em mãos, podemos aplicar uma identidade algébrica para possuirmos apenas 3 multiplicações diferentes, ao invés de 4.

XY = ac x 10^n + ((a x d) + (b x c)) x 10^(n/2) + bd

a identidade algébrica que podemos utilizar aqui é: 
a + bc + d = (a+b)×(c+d) − bd − ac

mas 

??? Exercício 1: Utilizando a fórmula da multiplicação recursiva

`md XY = (a x c) x 10^n + ((a x d) + (b x c)) x 10^(n/2) + b x d`

Então, para substituir na fórmula, temos:
`md a = 12; b = 34; c = 56; d = 78; n = 4`


!!! Dica
A fórmula do algoritmo de Karatsuba pode ser uma combinação de 5 passos para facilitar os cálculos:

`md I`: a x c

`md II`: b x d

`md III`: (a+b) x (c+d)

`md IV `: `md III - II - I` 

`md V`: `md I`x10^n + `md IV`x10^n/2 + `md II`
n


(a x c)x10^n + ((a+b) x (c+d) - b x d - a x c)x10^n/2 + b x d

!!!

::: Gabarito
* Passo I: `md ac = 12 x 56 = 672` 

* Passo II: `md bd = 34 x 78 = 2652`

* Passo III : `md (a+b)(c+d) = (12 + 34) x (56 + 78) = 6164`

* Passo IV: `md 6164 - 2652 - 672 = 2840`

* Passo V: `md 6720000 + 2652 + 284000 = 7006652`
:::
???

Agora vamos fazer outro exercício para fixar o conteúdo

??? Exercício

Faça a multiplicação dos números `md 234567` x `md 345678`. Lembre de usar a dica fornecida.

::: Gabarito
Temos que `md a = 234`, `md b = 567`, `md c = 345`, `md d = 678`, `md n = 6` 

* Passo I: `md ac = 234 x 345 = 80.730`

* Passo II: `md bd = 567 x 678 = 384.426`

* Passo III: `md (a+b)(c+d) = (234 + 567) x (345 + 678) = 819.423`

* Passo IV: `md 819.423 - 384.426 - 80.730 = 354.267`

* Passo V: `md 80.730 x 10^6 + 354.267 x 10^3 + 384.426` = `md 81.084.651.426`
:::
???

O código
---------
Como sabemos, o Algoritmo de Karatsuba é recursivo, e ele receberá os números que queremos multiplicar (a e b) e a quantidade de dígitos do maior algarismo (n). Com isso, podemos começar a "carcaça" do nosso código. 

``` c
void karatsuba(a, b, n) {

    karatsuba(c, d, n);

}
```
Feito isso, o primeiro passo do Algoritmo de Karatsuba é separar no meio os dois algarismos que iremos multiplicar.

??? Exercício
Faça uma função em C que realize esse processo e devolva os dois novos algarismo resultante da separação. 

`md Dica 1:` Lembre-se que o divisor será 10 elevado a metade da quantidade de dígitos do maior número.

`md Dica 2:` A biblioteca *<math.h>* possui uma função chamada pow() que realiza essa exponencial.

::: Gabarito
``` c
#include <math.h>

void separador(int num, int m, int* high, int* low) {
    int divisor = pow(10, m);
    *high = num / divisor;
    *low = num % divisor;
}
```
:::
???

Agora, podemos separar os algarismos no nosso código o obter 4 números dessa separação.

``` c
void karatsuba(a, b, n) {

    int m = n / 2;

    int high1, low1, high2, low2;
    separador(a, m, &high1, &low1);
    separador(b, m, &high2, &low2);

    karatsuba(c, d, n);
}
```
O próximo passo é relizar as recursivas dos seguintes subproblemas: 
* Multiplicação entre as partes inferiores dos dois números (low1 e low2)
* Multiplicação entre a soma das partes inferiores e superiores de ambos os números
* Multiplicação entre as partes superiores dos dois números

??? Exercício
Passe essas recursivas para o nosso código e defina um limite para as recursões!

`md Dica:` Para o limite, pense: "Quando que as multiplicações ficam pequenas o suficiente para serem feitas do jeito convencional?"

::: Gabarito
``` c
void karatsuba(a, b, n) {

    if (a < 10 || b < 10)
        return a * b;

    int m = n / 2;

    int high1, low1, high2, low2;
    separador(a, m, &high1, &low1);
    separador(b, m, &high2, &low2);

    r0 = karatsuba(low1, low2)
    r1 = karatsuba(low1 + high1, low2 + high2)
    r2 = karatsuba(high1, high2)
}
```
:::
???

Por último, basta aplicar a fórmula que aprendemos anteriormente.

``` c
int karatsuba(a, b, n) {

    if (a < 10 || b < 10)
        return a * b;

    int m = n / 2;

    int high1, low1, high2, low2;
    separador(a, m, &high1, &low1);
    separador(b, m, &high2, &low2);

    r0 = karatsuba(low1, low2)
    r1 = karatsuba(low1 + high1, low2 + high2)
    r2 = karatsuba(high1, high2)

    return (z2 * pow(10, m2 * 2)) + ((z1 - z2 - z0) * pow(10, m2)) + z0;
}
```
E assim temos o código do Algoritmo de Karatsuba.

Complexidade do algoritmo
---------
Denotamos por T(n) o consumo de tempo do algoritmo. Nosso código realiza divisões, três chamadas recursivas, combinação por soma e subtração, além de multiplicações adicionais e potências de 10.
Com isso, o tempo total de execução ficaria: 

$$ T(n) = 3T(n/2) + O(n) $$

A solução dessa relação de recorrência é *O(n^log2(3))*, que é aproximadamente *O(n^1.58)*. Em comparação, o algoritmo de multiplicação tradicional tem uma complexidade de *O(n^2)*.

Portanto, para números muito grandes, o algoritmo de Karatsuba é mais eficiente em termos de complexidade do que a multiplicação tradicional.