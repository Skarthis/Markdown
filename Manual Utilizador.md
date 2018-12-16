---


---

<hr>
<hr>
<h1 id="inteligência-artificial---adji‒boto">Inteligência Artificial - Adji‒boto*</h1>
<h2 id="manual-de-utilizador">Manual de Utilizador</h2>
<h3 id="acrónimos-e-convenções-usadas">Acrónimos e convenções usadas</h3>
<p><strong>Lista:</strong>  Conjunto de valores envolvidos por parêntesis. Ex.: ( a b c )<br>
<strong>Nó:</strong> Estrutura de dados que guarda informação do jogo actual, nomeadamente o estado do tabuleiro actual, valores heurísticos e o seu no antecessor.<br>
<strong>Heurística:</strong> Cálculo para atribuir um valor concreto a um nó.<br>
Ex.: h = número de peças existentes no tabuleiro</p>
De notar, em LISP as funções são chamadas da seguinte forma:<br>
<code>(&lt;funtion&gt; &lt;arg1&gt; &lt;arg2&gt;)</code>
<h3 id="introdução">Introdução</h3>
<p>
Este manual tem como objectivo guiar o utilizador para que consiga fazer uso do programa Adji‒boto* com sucesso. O Adji‒boto* consiste numa variante simplificada do Adji‒boto e Oware, desenvolvido através da linguagem LISP no âmbito da cadeira de Inteligência Artificial - Licenciatura em Engenharia Informática do politécnico de Setúbal 2018/19.<br>
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
<p>
</p><p>É necessário que na directoria C:\IA, sejam colocados os ficheiros do programa, nomeadamente:</p>
<ul>
<li>procura.lisp</li>
<li>puzzle.lisp</li>
<li>projeto.lisp</li>
<li>problemas.dat</li>
</ul>
<p>Para iniciar o programa deve compilar no IDE (ex.: lispWorks) o ficheiro <em>projeto.lisp</em>* e de seguida executar a função star, conforme a imagem:</p>
<p><img src="https://lh3.googleusercontent.com/P0n2GFRhErYECHN1pUmWm4StMZ9FiWzwO7GxhXcyGKkjKIXJxtrfkG0FSUmitBipZYkUPxow8-A" alt="enter image description here"></p>
<p>Para navegar nos menus basta inserir o número desejado e premir <em>*Enter</em>.</p>
<h3 id="input">Input
</h3><p>Além do início do programa através da função <em><em>start</em></em>, todo o input directo no programa é efectuado apenas com os algarismos correspondentes ás acções do menu actual.</p>
<p>
</p><p>É contudo, possível adicionar mais tabuleiros ao programa através do ficheiro <em>problemas.dat</em>, o ficheiro pode ser aberto como um <em>txt</em> com o seguinte aspecto:</p>
<p></p>
