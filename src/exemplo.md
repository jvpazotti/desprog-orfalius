Bucket Sort
======

O problema
---------

Imagine que você vai jogar Presidente. Na distribuição de cartas, a regra é que todos os jogadores recebam cartas até que o baralho acabe. Assim como qualquer outro jogo de carta, Presidente possui um hierarquia de naipes, seguindo a ordem crescente de Ouros (losango vermelho),Espadas (parece uma seta gordinha) ,Copas (coração) e Paus (parece uma árvore), e é normal que cada jogador coloque as suas cartas em ordem crescente de **Forma Numérica**, no entanto, em jogos de carta o padrão é que os Naipes possuam um valor agregado maior do que os de números. O problema é que muitos jogadores acabam deixando os valores dos Naipes de lado no momento de organização das cartas antes do jogo começar.  

??? Checkpoint

Sabendo do que foi dito acima, qual voce acha que seria a forma ideal de um jogador ordenar suas cartas?

::: Gabarito
O jeito ideal de ordená-las seria primeiro ordenar de forma crescente os **Naipes** e depois ordernar as cartas pela **ordem numérica** do jogo em cada Naipe.
:::

???

Pode parecer não intuitivo pensar dessa forma, mas pense que as vezes ao jogar dessa forma faz 
com que os possíveis erros ao jogar diminuam de forma considerável.

A ideia do *Bucket* Sort é parecida com o comportamento do jogador de Presidente: recebe uma amostra desordenada, divide ela em vários "grupos" com intervalos específicos, ordena cada grupo e junta todos os grupos, do intervalo com os menores valores ao intervalo com os maiores.


Pra simplificar a descrição da ideia, vamos "fingir" que podemos usar lista como em Python:

``` py 

CARTAS = Uma lista com todos os elementos do vetor

BUCKETS = Uma lista vazia com tamanho n (n listas vazias)

VALOR MÁXIMO =  elemento do vetor CARTAS que tem o valor mais alto

Para i=1 até o tamanho da lista CARTAS:

    Colocar elemento i da lista CARTAS na lista BUCKETS na posição (n * lista CARTAS no elemento i / VALOR MÁXIMO) 

Para i até n:

    Ordernar a lista BUCKETS na posição i

retornar concatenação de BUCKETS[1],BUCKETS[2],BUCKETS[3],...BUCKETS[n]

```

Um exemplo do **resultado final do algoritmo** pode ser visto abaixo:

Exemplo
---------
:buckets

Implementação
-------------
Para construir a lógica da ordenação do *Bucket* Sort, é preciso estabelecer simplificações. A mais importante é que o número de buckets será predefinido, fixo para cada implementação. Outra simplificação é a de que o Array ordenado será de inteiros.
??? Checkpoint

Com base no que foi dito, qual é a assinatura da função?

::: Gabarito
`py def bucket_sort(array, k)`, sendo que k é o número de Buckets.
:::

???

Para definir os limites de valores que cada *Bucket* terá existem várias estratégias. Uma delas é, a partir do valores mínimos e máximos, calcular o Range com o número de buckets. A lógica do Range é parecida com o cálculo de Resolução de conversores analógicos-digitais.

$$r = \frac{Vmax-Vmin}{k}$$

Já que o Array será de inteiros, faz sentido ter apenas Ranges inteiros para os buckets, já que nunca haverá valores entre os inteiros que devem ser considerados ou não. Por isso, a divisão acima pode ser corrigida de dois jeitos: arrendondando o valor pra cima ou pra baixo. Se for arredondado pra cima, o Range será maior e, por isso, foi a escolha da implementação.

??? Checkpoint

Quanto será o Range de um *Bucket* se uma lista vai de 1 a 12 e o código tem 3 Buckets?

::: Gabarito
Com valor mínimo de 1 e máximo de 12, o Range é aproximadamente 3.67. Arredondando pra cima, cada *bucket* terá range de 4. Ou seja, primeiro *bucket* de 0 a 3, o segundo de 4 a 7 e o terceiro de 8 a 11. 
:::

???

Resumindo:
```py
Tendo o Array e k como argumentos
Calcule o Range a partir dos limites do Array
Crie k Buckets vazios
```
??? Checkpoint

Faça a implementação em python do pseudocódigo acima.

::: Gabarito
``` py     
minimum=min(array)
maximum=max(array)

r=ceil((maximum-minimum)/k)
buckets=[]

for i in range(k):
    buckets.append([])
```
:::

???

Agora, é preciso iterar nos Buckets e nos elementos, a fim de alocar cada elemento no *Bucket* certo. Para fazer a implementação da verificação do Range é preciso formular uma que é verdadeira para todos os buckets. Sabendo que existe um índice i que é um contador de buckets, imagine a situação a seguir:

```py
                                R=4
                            
    B0                          B1                          B2
i=0                         i=1                         i=2
Range = 0 a 3               Range = 4 a 7               Range = 8 a 11
```

??? Checkpoint

A partir de i e R, formule a condição que define o valor mínimo do *Bucket*.

::: Gabarito
Se `py e` é o elemento sendo verificado:
``` py     
e >= i*r
```
Para o B1, e >= 0*4

Para o B2, e >= 1*4 

Para o B3, e >= 2*4
:::

???

??? Checkpoint

A partir de i e R, formule a condição que define o valor máximo do *Bucket*.

::: Gabarito
Se `py e` é o elemento sendo verificado:
``` py     
e < (i+1)*r
```
Para o B1, e < 1*4

Para o B2, e < 2*4 

Para o B3, e < 3*4
:::

???

Sabendo disso, é possível implementar o código que aloca cada elemento no *bucket* certo.
```py
 for i,b in enumerate(buckets):
        for e in array:
            if e>=i*r and e<(i+1)*r:
                b.append(e)
                break
```

A lista `py buckets` agora possui k listas com os elementos da lista alocados. Basta iterar entre cada *bucket*, ordenar cada um e concatenar os buckets.

??? Checkpoint

Implemente o *Bucket Sort* em Python

::: Gabarito
``` py     
def bucket_sort(array, k):
    minimum=min(array)
    maximum=max(array)

    r=ceil((maximum-minimum)/k)
    buckets=[]

    for i in range(k):
        buckets.append([])

    for i,b in enumerate(buckets):
        for e in array:
            if e>=i*r and e<(i+1)*r:
                b.append(e)
                break

    s=[]
    for b in buckets:
        s.append(sorted(b))
    
    final_list=[]
    for b in s:
        final_list+=b

    return final_list
```
:::

???

No papel, parece estar funcionando corretamente. No entanto, imagine que o usuário está ordenando com 3 *buckets*, Vmax=13 e Vmin=1. Nesse caso, com a conta do Range dando 4, o último *bucket* irá cobrir de 8 a 11. É necessário um último *bucket* para cobrir o elemento 13, principalmente pela aproximação pra cima que foi feita na conta do Range.

O jeito mais fácil de fazer isso é fazer uma verificação se o elemento foi adicionado em algum *bucket* ou não, ou seja, se o elemento passou pelo `py if e>=i*r and e<(i+1)*r`. Se ele não passar nenhuma vez em todas as iterações de *Bucket*, será necessário criar um *Bucket* depois de todos os outros, para alocar essas exceções.

??? Checkpoint

Tente implementar essa correção descrita acima na iteração dos elementos.

::: Gabarito
``` py     
for e in array:
    adicionou=False
    for i,b in enumerate(buckets):
        if e>=i*r and e<(i+1)*r:
            adicionou=True
            b.append(e)
            break
    if not adicionou:
        buckets.append([e])
```
:::

???

Sendo assim, segue a implementação completa do *Bucket Sort*.
```py
def bucket_sort(array, k):
    minimum=min(array)
    maximum=max(array)

    r=ceil((maximum-minimum)/k)
    buckets=[]

    for i in range(k):
        buckets.append([])

    for e in array:
        adicionou=False
        for i,b in enumerate(buckets):
            if e>=i*r and e<(i+1)*r:
                adicionou=True
                b.append(e)
                break
        if not adicionou:
            buckets.append([e])

    s=[]
    for b in buckets:
        s.append(sorted(b))

    final_list=[]
    for b in s:
        final_list+=b

    return final_list
```

Complexidade
-------------

De forma sucinta, o algortimo do *bucket sort* em questão pode ser subdividido em 3 tarefas. Com um vetor de *n* elementos temos que:
    1. Subdividir o vetor original em *k* *buckets*, sendo a quantidade de elementos em cada bucket igual a $(\frac{n}{k})$
    2. Ordenar os valores no interior de cada *bucket* utilizando *insertion sort*.
    3. Concatenar os buckets já ordenados em um vetor.
A partir do custo, ou seja, da complexidade de cada uma dessas estapas, podemos determinar a complexidade total do *bucket sort*. Vamos começar analisando o caso médio, para então analisar-mos casos específicos.

* Pior caso:

Como foi dito anteriormente, o *Bucket Sort* é especialmente útil quando temos um vetor a ser ordenado distribuído de maneira uniforme.
Portanto, o caso de pior performance de algoritmo seria quando temos o todos os elementos em apenas um *bucket*. 

Nesse cenário, a complexidade será determinada pelo algoritmo de ordenação interno ao *bucket sort*, que será $O(n^2)$ considerando o uso do *insertion sort*. Além disso, circunstâncias nas quais temos grande discrepância entre a quantidade de elementos dentro de cada *bucket* também não são ideais. Quanto maior essa diferença, os benefícios e qualidades do *bucket sort* se esmaecem, enquanto as deficiências do algoritmo interno são exacerbadas, pois o segundo não é indicado para vetores grandes.

* Caso médio:

Como o *bucket sort* deve principalmente ser usado com distribuições uniformes, consideraremos uma array distribuído de tal maneira para determinar a complexidade de seu caso médio.  

Primeiramente, o algoritmo deve varrer o array completamente, para determinar o maior valor em seu interior e assim configurar o *range* dos *buckets*. Portanto, o tempo de processamento será diretamente proporcional ao tamanho desse array, sendo a complexidade $O(n)$.

Partindo do pressuposto que utilizaremos o *insertion sort* como algoritmo interno do *bucket sort*, temos que o caso médio do *insertion* tem complexidade $O(n^2)$. 

Denominando *k* a quantidade de *buckets* utilizada no algoritmo, temos que a quantidade de elementos a serem ordenados pelo *insertion* em cada *bucket* será $O(\frac{n}{k})^2$. Como temos *k* buckets para rodar o *insertion sort*, a complexidade será de $O(\frac{n^2}{k^2} \cdot k)$, que será igual a $O(\frac{n^2}{k})$. 

Com cada *bucket* ordenado, resta apenas concatená-los na ordem correta. Isso ocorrerá em tempo proporcional ao número de *buckets*, tendo complexidade $O(k)$. Assim, teremos que a complexidade final do algoritmo será:

$$O(n + \frac{n^2}{k} + k)$$ 

* Melhor caso:

Pode-se deduzir a complexidade do melhor caso a partir da complexidade do caso médio, considerando também uma entrada uniformemente distribuída. O melhor caso pode ser percebido quando temos um algoritmo mais flexível e avançado, no qual o número de *buckets* cresce proporcionalmente com um aumento no número de elementos do vetor. Se o número *k* de buckets for muito próximo a *n*, temos que a relação $\frac{n}{k}^2$ será $\frac{n^2}{n}$. Nessas circunstâncias, temos que a complexidade do algoritmo será $O(n)$, sendo este o caso de uso mais apropriado para o *bucket sort*.

Tabela de complexidade
-----------------------

|              |        Complexidade       |
|--------------|---------------------------|
| Pior caso    | $O(n^2)$                  |
|Caso médio    |$O(n + \frac{n^2}{k} + k)$ |
|Melhor caso   |  $O(n)$ para $k \approx n$|
| Memória      |        $O(n+k)$           |

Atividade Extra
-----------------------

??? Fake Quiz

Considere o vetor abaixo.
```py
array = [13,2,23,78,65,99,42,0,55]
```
Simule o comportamento da lista `py buckets` ao fim de cada iteração. Ou seja, cada elemento sendo atribuído ao *bucket* certo.
::: Gabarito
```     
[[13], [], [], []]
[[13, 2], [], [], []]
[[13, 2, 23], [], [], []]
[[13, 2, 23], [], [], [78]]
[[13, 2, 23], [], [65], [78]]
[[13, 2, 23], [], [65], [78, 99]]
[[13, 2, 23], [42], [65], [78, 99]]
[[13, 2, 23, 0], [42], [65], [78, 99]]
[[13, 2, 23, 0], [42], [65, 55], [78, 99]]
```
:::

???