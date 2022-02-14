# Tutorial rápido de Python para Matemáticos

© Ricardo Miranda Martins, 2022 - http://www.ime.unicamp.br/~rmiranda/

## Índice

1. [Introdução](1-intro.html) 
2. [Python é uma boa calculadora!](2-calculadora.html) [(código fonte)](2-calculadora.ipynb)
3. [Resolvendo equações](3-resolvendo-eqs.html)  [(código fonte)](3-resolvendo-eqs.ipynb)
4. [Gráficos](4-graficos.html)  [(código fonte)](4-graficos.ipynb)
5. [Sistemas lineares e matrizes](5-lineares-e-matrizes.html)  [(código fonte)](5-lineares-e-matrizes.ipynb)
6. [Limites, derivadas e integrais](6-limites-derivadas-integrais.html)  [(código fonte)](6-limites-derivadas-integrais.ipynb)
7. [Equações direrenciais](7-equacoes-diferenciais.html)  [(código fonte)](7-equacoes-diferenciais.ipynb)

# O que tem aqui?

Aqui está um caminho rápido para aprender a usar Python para fazer cálculos matemáticos. Se você não sabe programar, esse site é para você. Aqui, seremos duas pessoas que não sabem programar tentando aprender alguma coisa.

Você vai aprender a resolver equações, inverter matrizes, fazer gráficos, resolver equações diferenciais.. o foco não é em detalhes das sintaxes dos comandos. Afinal, é para isso que você paga internet, certo? Ok - vou ser bonzinho e mesmo assim colocar alguns exemplos de coisas simples, usando ```if```, ```for```, etc.

O objetivo aqui é ser um guia estilo mão-na-massa ou copie-cole-e-altere.

Se você está meio perdido: para usar o Python, eu recomendo que você use o Jupyter. Vá em https://jupyter.org/try e inicie um JupyterLab. Quando aparecer a tela de seleção, escolha Python na aba "Notebook". Melhor mesmo é você instalá-lo em seu computador, usando o [Anaconda](https://www.anaconda.com/).

## Referências bibliográficas

Alguns sites muito bons para aprender a usar *Python* com objetivo de fazer coisas de matemática:

1. [Mathematical Python](https://personal.math.ubc.ca/~pwalls/math-python/), por Patrick Walls.
2. [Dynamical systems with applications using Python](http://www.doc.mmu.ac.uk/STAFF/S.Lynch/DSAP_Jupyter_Notebook.html): site base do livro do [Stephen Lynch](http://www.doc.mmu.ac.uk/STAFF/S.Lynch/) de onde tirei/adaptei vários códigos que estão aqui.
3. [SciPython](https://scipython.com/) 
4. [Problem Solving with Python](https://problemsolvingwithpython.com/)
5. [SciPy Lecture Notes](https://scipy-lectures.org/index.html)
6. [PythonForUndergradEngineers](https://pythonforundergradengineers.com/)
7. [SciPy 2017 tutorial "Automatic Code Generation with SymPy"](https://www.sympy.org/scipy-2017-codegen-tutorial/notebooks/20-ordinary-differential-equations.html)

Parte dos códigos disponibilizados não foram originalmente feitos por mim, mas adaptados de códigos encontrados no StackOverFlow, StackExchange, etc. Sempre que ainda tiver o link pro código original, vou indicar. Então chega de blá-blá-blá e vamos lá.

## Mensagem legal e copyright

Estas notas de aula estão regidas pela [Licença Pública Creative Commons Atribuição 4.0 Internacional](https://creativecommons.org/licenses/by/4.0/legalcode.pt). Veja um resumo do que você pode ou não fazer [clicando aqui](https://creativecommons.org/licenses/by/4.0/deed.pt_BR).

