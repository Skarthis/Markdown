
# Inteligência Artificial - Adji‒boto*
## Manual de Utilizador 



### Acrónimos e convenções usadas

__Lista:__  Conjunto de valores envolvidos por parêntesis. Ex.: ( a b c )
__Nó:__ Estrutura de dados que guarda informação do jogo actual, nomeadamente o estado do tabuleiro actual, valores heurísticos e o seu no antecessor.Heurística: Cálculo para atribuir um valor concreto a um nó.
Ex.: h = número de peças existentes no tabuleiro

De notar, em LISP as funções são chamadas da seguinte forma: 
`(<funtion> <arg1> <arg2>)`

### Introdução
Este manual tem como objectivo guiar o utilizador para que consiga fazer uso do programa Adji‒boto* com sucesso. O Adji‒boto* consiste numa variante simplificada do Adji‒boto e Oware, desenvolvido através da linguagem LISP no âmbito da cadeira de Inteligência Artificial - Licenciatura em Engenharia Informática do politécnico de Setúbal 2018/19.
Esta versão simplificada do Adji‒boto consiste num tabuleiro com dois lados cada um com seis posições, o tabuleiro inicial pode ter várias variantes em relação ao número de peças existentes e a sua distribuição. Enquanto que no jogo normal são necessários dois jogadores esta versão é jogada apenas por um e pode efectuar jogadas de ambos os lados do tabuleiro.
O presente programa inicia com um tabuleiro escolhido pelo utilizador e aplica um dos algoritmos de procura também escolhido pelo utilizador e devolve visualmente todas as jogadas efectuadas que levaram à solução, ou seja, ao tabuleiro que não possui peças.A navegação no programa é feita através de menus simples em ASCII, que permite:Visualizar todos os tabuleiros possíveisEfectuar um jogo com um tabuleiro e um algoritmo de procura escolhidos pelo utilizadorQue o utilizador escolha qual a função heurística que pretende usar, caso escolha um algoritmo que faz uso de heurísticasAnalisar os resultados de um jogo, após o jogo alcançar uma solução

### Instalação e utilização</p><p>

É necessário que na directoria C:\IA, sejam colocados os ficheiros do programa, nomeadamente:procura.lisppuzzle.lispprojeto.lispproblemas.datPara iniciar o programa deve compilar no IDE (ex.: lispWorks) o ficheiro projeto.lisp* e de seguida executar a função start, conforme a imagem:

![enter image description here](https://lh3.googleusercontent.com/P0n2GFRhErYECHN1pUmWm4StMZ9FiWzwO7GxhXcyGKkjKIXJxtrfkG0FSUmitBipZYkUPxow8-APara navegar nos menus basta inserir o número desejado e premir *Enter</h3><p>*.

### Input

Além do início do programa através da função </em>*start*, todo o input directo no programa é efectuado apenas com os algarismos correspondentes ás acções do menu actual.</p><p>

É contudo, possível adicionar mais tabuleiros ao programa através do ficheiro 3.googleusercontent.com/7qpoLOle51l0yrRLIpBgpmIWxGQXgiZC-9SBmEV36WQZF7SYAMFDnNJbbGqBKlzm61sag0agjBA)

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTMwMTE3NzY1XX0=
-->