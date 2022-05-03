Bucket Sort
======

A ideia
---------

Imagine que você vai jogar Presidente. Na distribuição de cartas, a regra é que todos os jogadores recebam cartas até que o baralho acabe. Como Presidente depende da hierarquia das cartas (por exemplo, 2 é a maior e 3 a pior), é normal que cada jogador coloque as suas cartas em ordem crescente antes que o jogo comece, para entender melhor como está sua mão. O comportamento de um participante é separar entre cartas ruins, medianas e boas. 

O que define cada categoria é um intervalo das piores até as maiores. Para o Presidente, da carta 3 à 7 o jogador colocaria num monte de carta ruim, 8 à Q seriam cartas medianas e J ao 2, cartas boas. Após separar em cada grupo, o jogador coloca as cartas de cada grupo em ordem entre elas e, depois, junta os grupos. Se ele colocar primeiros as piores cartas, depois as medianas e, por fim, as melhores, é garantido que a mão dele estará ordenada da pior para a melhor.

A ideia do Bucket Sort é parecida com o comportamento do jogador de Presidente: recebe uma amostra desordenada, divide ela em vários "grupos" com intervalos específicos, ordena cada grupo e junta todos os grupos, do intervalo com os menores valores ao intervalo com os maiores.


Pra simplificar a descrição da ideia, vamos "fingir" que podemos usar lista como em Python:

``` py
BUCKETS = n listas inicialmente vazias

CARTAS = Uma lista com todos os elementos do vetor

ORDENADO = Uma lista vazia

Para um indice i de valor de 0 Cartas

```

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
