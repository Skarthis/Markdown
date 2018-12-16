---


---

<h1 id="inteligência-artificial---adji‒boto">Inteligência Artificial - Adji‒boto*</h1>
<h2 id="manual-de-utilizador">Manual de Utilizador</h2>
<h3 id="acrónimos-e-convenções-usadas">Acrónimos e convenções usadas</h3>
<p><strong>Lista:</strong>  Conjunto de valores envolvidos por parêntesis. Ex.: ( a b c )<br>
<strong>Nó:</strong> Estrutura de dados que guarda informação do jogo actual, nomeadamente o estado do tabuleiro actual, valores heurísticos e o seu no antecessor.<br>
<strong>Heurística:</strong> Cálculo para atribuir um valor concreto a um nó.<br>
Ex.: h = número de peças existentes no tabuleiro</p>
<p>De notar, em LISP as funções são chamadas da seguinte forma:<br>
<code>(&lt;funtion&gt; &lt;arg1&gt; &lt;arg2&gt;)</code></p>
<h3 id="introdução">Introdução</h3>
<p>Este manual tem como objectivo guiar o utilizador para que consiga fazer uso do programa Adji‒boto* com sucesso. O Adji‒boto* consiste numa variante simplificada do Adji‒boto e Oware, desenvolvido através da linguagem LISP no âmbito da cadeira de Inteligência Artificial - Licenciatura em Engenharia Informática do politécnico de Setúbal 2018/19.<br>
Esta versão simplificada do Adji‒boto consiste num tabuleiro com dois lados cada um com seis posições, o tabuleiro inicial pode ter várias variantes em relação ao número de peças existentes e a sua distribuição. Enquanto que no jogo normal são necessários dois jogadores esta versão é jogada apenas por um e pode efectuar jogadas de ambos os lados do tabuleiro.<br>
O presente programa inicia com um tabuleiro escolhido pelo utilizador e aplica um dos algoritmos de procura também escolhido pelo utilizador e devolve visualmente todas as jogadas efectuadas que levaram à solução, ou seja, ao tabuleiro que não possui peças.</p>
<p>A navegação no programa é feita através de menus simples em ASCII, que permite:</p>
<ul>
<li>Visualizar todos os tabuleiros possíveis</li>
<li>Efectuar um jogo com um tabuleiro e um algoritmo de procura escolhidos pelo utilizador</li>
<li>Que o utilizador escolha qual a função heurística que pretende usar, caso escolha um algoritmo que faz uso de heurísticas</li>
<li>Analisar os resultados de um jogo, após o jogo alcançar uma solução</li>
</ul>
<h3 id="instalação-e-utilização">Instalação e utilização</h3>
<p>É necessário que na directoria C:\IA, sejam colocados os ficheiros do programa, nomeadamente:</p>
<ul>
<li>procura.lisp</li>
<li>puzzle.lisp</li>
<li>projeto.lisp</li>
<li>problemas.dat</li>
</ul>
<p>Para iniciar o programa deve compilar no IDE (ex.: lispWorks) o ficheiro <em>projeto.lisp</em> e de seguida executar a função start, conforme a imagem:</p>
<p><img src="https://lh3.googleusercontent.com/P0n2GFRhErYECHN1pUmWm4StMZ9FiWzwO7GxhXcyGKkjKIXJxtrfkG0FSUmitBipZYkUPxow8-A" alt="enter image description here"></p>
<p>Para navegar nos menus basta inserir o número desejado e premir <em>Enter</em>.</p>
<h3 id="input">Input</h3>
<p>Além do início do programa através da função <em>start</em>, todo o input directo no programa é efectuado apenas com os algarismos correspondentes ás acções do menu actual.</p>
<p>É contudo, possível adicionar mais tabuleiros ao programa através do ficheiro <em>problemas.dat</em>, o ficheiro pode ser aberto como um <em>txt</em> com o seguinte aspecto:</p>
<p><img src="https://lh3.googleusercontent.com/s8VOgA6M3vYk2ipFC9tZjOGINploonOypQVEYUlFm0j-AeERk_2i1l5frLRwkWqXTNyw5UhNOZg" alt="enter image description here"></p>
<p>Para adicionar um tabuleiro basta inserir como exemplificado na imagem o novo tabuleiro, no formato <code>( &lt;tabuleiro&gt; )</code> onde o tabuleiro é as duas listas correspondentes a cada lado do tabuleiro de jogo.<br>
<strong>Notas:</strong> Deixar uma linha vazia entre cada tabuleiro; Introduzir os lados do tabuleiro em linhas diferentes.</p>
<h3 id="outputs">Outputs</h3>
<p>Depois de um jogo ter sido efectuado, será apresentado visualmente todos as jogadas efectuadas até à solução, e de seguida o menu inicial.</p>
<p><img src="https://lh3.googleusercontent.com/gJEk1yEfui_Gxo30DMFnpHMe1fv3uAIbVTSUl0B3SdwJFqNfuekHxKWCmgas30qEKJEx_XcAs6o" alt="enter image description here"></p>
<p>Para além disso serão gravadas as estatísticas e medidas de desempenho num ficheiro à parte, <em>resultados.dat</em> na mesma directoria que o programa. Usando a seguinte estrutura:</p>
<p><img src="https://lh3.googleusercontent.com/KN8YFzFG4n9Wh-EiNsyYnfXg7SNvkaRCPfyfanq6e6zEuXXlO1yCxAh-xAWmOkiVFU-HvdNWckg" alt="enter image description here"></p>
<p><strong>Notas:</strong></p>
<ul>
<li>Número de nós gerados - número total de possíveis jogadas geradas</li>
<li>Número de nós expandidos - número de tabuleiros onde se exploraram as jogadas possíveis</li>
<li>Penetrância - quociente entre o comprimento da solução e o número total de nós gerados</li>
<li>Comprimento da solução - número de níveis da árvore do problema desde a raiz até à solução</li>
<li>Factor de ramificação média - o número médio de ramos gerados por cada nó</li>
</ul>
<h3 id="algoritmos-de-procura">Algoritmos de procura</h3>
<p><img src="https://kevhuang.com/content/images/2015/06/tree-traversal.gif" alt="enter image description here"></p>
<h4 id="breadth-first-search">Breadth-first Search</h4>
<p>Algoritmo de procura em <strong>largura</strong>, completa a exploração de todos os nós existentes num nível antes de passar para os seus filhos (nível seguinte).</p>
<h4 id="depth-first-search">Depth-first Search</h4>
<p>Algoritmo de procura em <strong>profundidade</strong>, explora sempre o nó aberto mais à esquerda e só depois de esgotar o caminho mais à esquerda volta os níveis necessários atrás até encontrar o nó mais à esquerda que não seja o que já foi esgotado.</p>
<h4 id="a---informed-search">A* - informed search</h4>
<p>O algoritmo A* é um algoritmo de procura <strong>informada</strong>, que faz uso de uma dada função heurística para atribuir um valor a cada nó que é gerado e opta por explorar sempre o nó de menor valor.</p>
<h3 id="exemplo-do-programa">Exemplo do programa</h3>
<p><img src="https://lh3.googleusercontent.com/WA8dXJ2VbAbgNj-E5bW2VmkCqXfuD2kzmXGgm4TGBFbJcadXxj929xg01ORo_We3byldsrgxpbw" alt="enter image description here"><br>
<img src="https://lh3.googleusercontent.com/7qpoLOle51l0yrRLIpBgpmIWxGQXgiZC-9SBmEV36WQZF7SYAMFDnNJbbGqBKlzm61sag0agjBA" alt="enter image description here"></p>

