Bucket Sort
======

A ideia
---------

Imagine que você vai jogar Presidente. Na distribuição de cartas, a regra é que todos os jogadores recebam cartas até que o baralho acabe. Como Presidente depende da hierarquia das cartas (por exemplo, 2 é a maior e 3 a pior), é normal que cada jogador coloque as suas cartas em ordem crescente antes que o jogo comece, para entender melhor como está sua mão. O comportamento de um participante é separar entre cartas ruins, medianas e boas. 

O que define cada categoria é um intervalo das piores até as maiores. Para o Presidente, da carta 3 à 7 o jogador colocaria num monte de cartas ruins, 8 à Q seriam cartas medianas e J ao 2, cartas boas. Após separar em cada grupo, o jogador coloca as cartas de cada grupo em ordem entre elas e, depois, junta os grupos. Se ele colocar primeiros as piores cartas, depois as medianas e, por fim, as melhores, é garantido que a mão dele estará ordenada da pior para a melhor.

A ideia do Bucket Sort é parecida com o comportamento do jogador de Presidente: recebe uma amostra desordenada, divide ela em vários "grupos" com intervalos específicos, ordena cada grupo e junta todos os grupos, do intervalo com os menores valores ao intervalo com os maiores.


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

![](bucketresult.png)

Exemplo
---------
:buckets

Implementação
-------------
Para construir a lógica da ordenação do Bucket Sort, é preciso estabelecer simplificações. A mais importante é que o número de buckets será predefinido, fixo para cada implementação. 
??? Checkpoint

Com base no que foi dito, qual é a assinatura da função?

::: Gabarito
`py def bucket_sort_errado(array, k)`, sendo que k é o número de Buckets.
:::

???

Para definir os limites de valores que cada Bucket terá, existem várias estratégias. Uma delas é, a partir do valores mínimos e máximos, calcular o Range a partir do número de buckets. A lógica do Range é parecida com o cálculo de Resolução de conversores analógicos-digitais.

$$r = \frac{Vmax-Vmin}{k}$$

Complexidade
-------------
Pior caso:

Como foi dito anteriormente, o *Bucket Sort* é especialmente útil quando temos um vetor a ser ordenado distribúido de maneira uniforme.
Portanto, o caso de pior performance de algortimo seria quando temos todos os elementos em apenas um *bucket*. Nesse cenário, a complexidade será determinada pelo algoritmo de ordenação interno ao *bucket sort*. Circunstâncias nas quais temos grande disprepância entre a quantidade de elementos dentro de cada bucket também não são ideais. Qaunto maior essa diferença, os benefícios e qualidades deo *bucket sort* se esmaecem, enquanto as deficiências do algoritmo interna são exarcebadas.

Caso médio:

Como o *bucket sort* deve principalmente ser usado com distribuições uniformes, consideraremos uma array distribuído de tal maneira para determinar a complexidade de seu caso médio.  

Primeiramente, o algortimo deve varrer o array completaente, para determinar o maior valor em seu interior. Portanto, o tempo de processamento será diretamente proporcional ao tamanho desse array, sendo a complexidade $O(n)$.

Partindo do pressuposto que utilizaremos o *insertion sort* como algortimo interno do *bucket sort*, temos que o caso médio do *insertion* terá complexidade $O(n^2)$. Denominando *k* a quantidade de *buckets* utilizada no algoritmo, temos que a quantidade de elementos a serem ordenados pelo insertion em cada bucket será $O(\frac{n}{k})^2$. Como temos *k* buckets para rodar o *insertion sort*, a complexidade será de $O(\frac{n^2}{k^2})*k$, que será igual a $O(\frac{n^2}{k})$. Com cada bucket ordenado, resta apenas concatená-los na ordem correto. Isso ocorrerá em tempo proporcional ao número de *buckets*, tendo complexidade $O(k)$.

Assim, teremos que a complexidade final do algoritmo será $O(n + \frac{n^2}{k} + k)$. 

Melhor caso: 

Pode-se deduzir a complexidade do melhor caso a partir da complexidade do caso médio. O melhor caso pode ser percebido quando temos um algoritmo mais flexível e avançado, no qual o número de *buckets* é proporcional ao número de elementos do vetor. Nesse cenário, temos que 



Você também pode criar

1. listas;

2. ordenadas,

assim como

* listas;

* não-ordenadas

e imagens. Lembre que todas as imagens devem estar em uma subpasta *img*.

![](buckets.png)

Para tabelas, usa-se a [notação do
MultiMarkdown](https://fletcher.github.io/MultiMarkdown-6/syntax/tables.html),
que é muito flexível. Vale a pena abrir esse link para saber todas as
possibilidades.

| coluna a | coluna b |
|----------|----------|
| 1        | 2        |

Ao longo de um texto, você pode usar *itálico*, **negrito**, {red}(vermelho) e
[[tecla]]. Também pode usar uma equação LaTeX: $f(n) \leq g(n)$. Se for muito
grande, você pode isolá-la em um parágrafo.

$$\lim_{n \rightarrow \infty} \frac{f(n)}{g(n)} \leq 1$$

Para inserir uma animação, use `md :` seguido do nome de uma pasta onde as
imagens estão. Essa pasta também deve estar em *img*.

:bubble

Você também pode inserir código, inclusive especificando a linguagem.

``` py
def f():
    print('hello world')
```

``` c
void f() {
    printf("hello world\n");
}
```

Se não especificar nenhuma, o código fica com colorização de terminal.

```
hello world
```


!!! Aviso
Este é um exemplo de aviso, entre `md !!!`.
!!!


??? Exercício

Este é um exemplo de exercício, entre `md ???`.

::: Gabarito
Este é um exemplo de gabarito, entre `md :::`.
:::

???
