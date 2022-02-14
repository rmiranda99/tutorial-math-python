# Tutorial rápido de Python para Matemáticos

© Ricardo Miranda Martins, 2022 - http://www.ime.unicamp.br/~rmiranda/

## Índice

1. [Introdução](http://www.ime.unicamp.br/~rmiranda/python.html) 
2. [Python é uma boa calculadora!](2-calculadora.html) [(código fonte)](2-calculadora.ipynb)
3. [Resolvendo equações](3-resolvendo-eqs.html)  [(código fonte)](3-resolvendo-eqs.ipynb)
4. [Gráficos](4-graficos.html)  [(código fonte)](4-graficos.ipynb)
5. [Sistemas lineares e matrizes](5-lineares-e-matrizes.html)  [(código fonte)](5-lineares-e-matrizes.ipynb)
6. [Limites, derivadas e integrais](6-limites-derivadas-integrais.html)  [(código fonte)](6-limites-derivadas-integrais.ipynb)
7. [Equações direrenciais](7-equacoes-diferenciais.html)  [(código fonte)](7-equacoes-diferenciais.ipynb)


# Python é uma boa calculadora!

Vamos colocar o Python para fazer umas contas. Para isso, é só digitar o que você quer na linha aqui de baixo e depois apertar shift+enter. Tudo que você digitar na linha de código começando com # será interpretado como um comentário, e em geral é usado para explicar partes do código.


```python
# isto é um comentário. abaixo, fazemos a soma de 1 com 1
1+1
```




    2




```python
232323*8987
```




    2087886801



Para dividir dois números, é só usar o símbolo "/":


```python
11/4
```




    2.75



O resultado será um número decimal. Se você quiser fazer uma divisão inteira, aquela em que é produzido um quociente e um resto, terá que usar dois comandos. O ```//``` produz o quociente dessa divisão e o ```%``` o resto, como nos exemplos abaixo. Lembre-se que $11=4\cdot 2+3$.


```python
11//4
```




    2




```python
11 % 4
```




    3



O Python tem suas funções ampliadas com base em módulos/bibliotecas. Usaremos muitas delas em nossos exemplos. 

Uma das bibliotecas mais poderosas para matemática é a SymPy, para cálculos simbólicos. A SymPy é uma biblioteca enorme, então se importamos todas as funções dela para o ambiente de trabalho, além de começar a dar conflito com algumas outras funções, tudo pode ficar mais lento. Então o comando abaixo vai importar SymPy usando um atalho. Esse é um procedimento totalmente usual. No [site do SymPy](https://docs.sympy.org/latest/tutorial/index.html) você tem um tutorial bem legal que eu recomendo.

O comando ```import sympy as sp``` diz que estamos importando a biblioteca SymPy e o prefixo ```sp``` será usado para chamar as funções dessa biblioteca. A seguir, usamos o comando ```isprime```, que determina se um número é ou não primo.


```python
import sympy as sp
sp.isprime(11)
```




    True



## Sem preguiça, vamos programar um pouco!

Usar a função ```isprime``` do SymPy é ótimo, mas poderíamos ter programado um "crivo" para verificar primalidade, né? Vamos fazer isso. Vai ser uma primeira oportunidade de conhecer a sintaxe de alguns laços, que podem ser úteis mais pra frente.

Uma forma simples de verificar se um número é primo é a seguinte: tente dividí-lo por todos os inteiros maiores que 1 e menores que ele. Se nenhuma divisão for exata, o número é primo. Se em alguma divisão der resto zero, então o número não será primo. O código abaixo foi adaptado [daqui](https://stackoverflow.com/questions/4114167/checking-if-a-number-is-prime-in-python). 


```python
def checaprimo(n):
    if n == 2:
        return True
    if n % 2 == 0 or n <= 1:
        return False
    for divisor in range(3, n, 2):
        if n % divisor == 0:
            return False
    return True
checaprimo(101)
```




    True



Agora vamos pensar um pouco: estamos tentando dividir $n$ por todos os números entre $2$ e $n-1$. Será que precisamos de tudo isso? Ora, se $n$ for divisível por $k$, com $k<n$, então $n$ também será divisível por $n/k$. Das duas, uma: ou $k$ ou $n/k$ será menor que $\sqrt{n}$. A prova disso é fácil: se ambos forem maiores que $\sqrt{n}$, então o produto deles, que sabemos que resulta em $n$, seria $$n=k\cdot (n/k)>\sqrt{n}\cdot \sqrt{n}=n,$$ um absurdo portanto.

Logo, podemos alterar o ```range``` dentro do ```for``` para ir de $3$ até o inteiro maior ou igual a$\sqrt{n}$ (repare no uso da função ```int``` no código).

Como a função $\sqrt{x}$ não está implementada por padrão no Python, ao invés de implementá-la, vamos carregar a biblioteca ```math``` que vem com ela e outras funções simples no pacote. Veja detalhes sobre a ```math``` [aqui](https://docs.python.org/3/library/math.html).

Note que isso aumenta bastante a velocidade de execução do nosso algoritmo.


```python
import math
def checaprimo2(n):
    if n == 2:
        return True
    if n % 2 == 0 or n <= 1:
        return False
    for divisor in range(3, int(math.sqrt(n)), 2):
        if n % divisor == 0:
            return False
    return True
checaprimo2(101)
```




    True



## Bônus: programando nossa própria raiz quadrada

No código acima, para verificar a primalidade, usamos a função ```sqrt``` do pacote ```math``` do Python, mas isso é um exagero. Podemos facilmente programar uma função que calcula a raiz quadrada.

A função que vamos programar usa um argumento simples, que era usado pelos babilônios por volta do ano 60 d.C. para calcular a raiz quadrada: suponha que $x>0$ e queremos calcular $\sqrt{x}$. Seja $y$ com $y^2<x$. Então $\sqrt{x}$ está entre $y$ e $x/y$ ("perto do ponto médio desse intervalo"). Atualmente essa estratégia é conhecida como método de Heron, e sua demonstração é simples (tem até [aqui](https://en.wikipedia.org/wiki/Methods_of_computing_square_roots#Babylonian_method) na Wikipedia).

Em termos mais algoritmicos, a ideia é a seguinte. Queremos calcular $\sqrt{x}$. Escolha $y=1$ (ou qualquer outro número positivo). Então, a menos que $x=1$, a raiz quadrada de $x$ estará entre $y$ e $x/y$. Pegue então o ponto médio desse intervalo e chame de $y_1$. Novamente, a raiz quadrada de $x$ estará entre $y_1$ e $x/y_1$. Pegue novamente o ponto médio desse intervalo e continue sucessivamente. A sequência desses "pontos médios" vai convergir para a raiz quadrada.


```python
def minharaizquadrada(x):
    y=1
    # aqui é que definimos o numero de iterações, troque 10 pelo que quiser;
    # quando maior, melhor aproximação
    for k in range(1,10):
        y = (y + x/y)/2
    return y

# calculando sqrt(2)
minharaizquadrada(2)
```




    1.414213562373095



Pronto, agora temos nossa própria função para calcular raiz quadrada! Vamos rodar novamente aquele teste de primalidade, só que agora com nossa função raiz quadrada.


```python
def checaprimo3(n):
    if n == 2:
        return True
    if n % 2 == 0 or n <= 1:
        return False
    for divisor in range(3, int(minharaizquadrada(n)), 2):
        if n % divisor == 0:
            return False
    return True
checaprimo3(101)
```




    True



Bom, 101 continua sendo primo, então a função deve funcionar :)
