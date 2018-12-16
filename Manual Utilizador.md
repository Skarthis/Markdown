
# Inteligência Artificial - Adji‒boto*
## Manual de Utilizador 


### Acrónimos e convenções usadas

__Lista:__  Conjunto de valores envolvidos por parêntesis. Ex.: ( a b c )
__Nó:__ Estrutura de dados que guarda informação do jogo actual, nomeadamente o estado do tabuleiro actual, valores heurísticos e o seu no antecessor.
__Heurística:__ Cálculo para atribuir um valor concreto a um nó. 
Ex.: h = número de peças existentes no tabuleiro

De notar, em LISP as funções são chamadas da seguinte forma: 
`(<funtion> <arg1> <arg2>)`

### Introdução
Este manual tem como objectivo guiar o utilizador para que consiga fazer uso do programa Adji‒boto* com sucesso. O Adji‒boto* consiste numa variante simplificada do Adji‒boto e Oware, desenvolvido através da linguagem LISP no âmbito da cadeira de Inteligência Artificial - Licenciatura em Engenharia Informática do politécnico de Setúbal 2018/19.
Esta versão simplificada do Adji‒boto consiste num tabuleiro com dois lados cada um com seis posições, o tabuleiro inicial pode ter várias variantes em relação ao número de peças existentes e a sua distribuição. Enquanto que no jogo normal são necessários dois jogadores esta versão é jogada apenas por um e pode efectuar jogadas de ambos os lados do tabuleiro.
O presente programa inicia com um tabuleiro escolhido pelo utilizador e aplica um dos algoritmos de procura também escolhido pelo utilizador e devolve visualmente todas as jogadas efectuadas que levaram à solução, ou seja, ao tabuleiro que não possui peças.

A navegação no programa é feita através de menus simples em ASCII, que permite:

 - Visualizar todos os tabuleiros possíveis 
 - Efectuar um jogo com um tabuleiro e um algoritmo de procura escolhidos pelo utilizador
 - Que o utilizador escolha qual a função heurística que pretende usar, caso escolha um algoritmo que faz uso de heurísticas
 - Analisar os resultados de um jogo, após o jogo alcançar uma solução

### Instalação e utilização

É necessário que na directoria C:\IA, sejam colocados os ficheiros do programa, nomeadamente:

 - procura.lisp
 - puzzle.lisp
 - projeto.lisp
 - problemas.dat

Para iniciar o programa deve compilar no IDE (ex.: lispWorks) o ficheiro *projeto.lisp* e de seguida executar a função start, conforme a imagem:

![enter image description here](https://lh3.googleusercontent.com/P0n2GFRhErYECHN1pUmWm4StMZ9FiWzwO7GxhXcyGKkjKIXJxtrfkG0FSUmitBipZYkUPxow8-A)

Para navegar nos menus basta inserir o número desejado e premir *Enter*.

### Input

Além do início do programa através da função *start*, todo o input directo no programa é efectuado apenas com os algarismos correspondentes ás acções do menu actual.

É contudo, possível adicionar mais tabuleiros ao programa através do ficheiro *problemas.dat*, o ficheiro pode ser aberto como um *txt* com o seguinte aspecto:

![enter image description here](https://lh3.googleusercontent.com/s8VOgA6M3vYk2ipFC9tZjOGINploonOypQVEYUlFm0j-AeERk_2i1l5frLRwkWqXTNyw5UhNOZg)

Para adicionar um tabuleiro basta inserir como exemplificado na imagem o novo tabuleiro, no formato `( <tabuleiro> )` onde o tabuleiro é as duas listas correspondentes a cada lado do tabuleiro de jogo.
__Notas:__ Deixar uma linha vazia entre cada tabuleiro; Introduzir os lados do tabuleiro em linhas diferentes.

### Outputs

Depois de um jogo ter sido efectuado, será apresentado visualmente todos as jogadas efectuadas até à solução, e de seguida o menu inicial.

![enter image description here](https://lh3.googleusercontent.com/gJEk1yEfui_Gxo30DMFnpHMe1fv3uAIbVTSUl0B3SdwJFqNfuekHxKWCmgas30qEKJEx_XcAs6o)

Para além disso serão gravadas as estatísticas e medidas de desempenho num ficheiro à parte, *resultados.dat* na mesma directoria que o programa. Usando a seguinte estrutura:

![enter image description here](https://lh3.googleusercontent.com/KN8YFzFG4n9Wh-EiNsyYnfXg7SNvkaRCPfyfanq6e6zEuXXlO1yCxAh-xAWmOkiVFU-HvdNWckg)

__Notas:__
 - Número de nós gerados - número total de possíveis jogadas geradas
 - Número de nós expandidos - número de tabuleiros onde se exploraram as jogadas possíveis
 - Penetrância - quociente entre o comprimento da solução e o número total de nós gerados
 - Comprimento da solução - número de níveis da árvore do problema desde a raiz até à solução
 - Factor de ramificação média - o número médio de ramos gerados por cada nó

### Algoritmos de procura
![enter image description here](https://kevhuang.com/content/images/2015/06/tree-traversal.gif)

#### Breadth-first Search
Algoritmo de procura em __largura__, completa a exploração de todos os nós existentes num nível antes de passar para os seus filhos (nível seguinte).

#### Depth-first Search
Algoritmo de procura em __profundidade__, explora sempre o nó aberto mais à esquerda e só depois de esgotar o caminho mais à esquerda volta os níveis necessários atrás até encontrar o nó mais à esquerda que não seja o que já foi esgotado.

#### A* - informed search
O algoritmo A* é um algoritmo de procura __informada__, que faz uso de uma dada função heurística para atribuir um valor a cada nó que é gerado e opta por explorar sempre o nó de menor valor.

### Exemplo do programa

![enter image description here](https://lh3.googleusercontent.com/WA8dXJ2VbAbgNj-E5bW2VmkCqXfuD2kzmXGgm4TGBFbJcadXxj929xg01ORo_We3byldsrgxpbw)
![enter image description here](https://lh3.googleusercontent.com/7qpoLOle51l0yrRLIpBgpmIWxGQXgiZC-9SBmEV36WQZF7SYAMFDnNJbbGqBKlzm61sag0agjBA)

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwMTkwMzgzMzQsMTE3NDc1Mjk1Nl19
-->