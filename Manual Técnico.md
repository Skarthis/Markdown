# Inteligência Artificial - Adji-Boto*

## Manual Técnico

### Introdução

O manual técnico contem a documentação sobre a implementação do programa *Adji-Boto** escrito em *LISP* , uma versão simplificada do jogo Oware.
o programa está dividido em 4 ficheiros:

 - puzzle.lisp - implementação da resolução do problema e operadores  
 - procura.lisp - implementação dos algoritmos de procura e auxiliares necessários
 - projecto.lisp - interacção com o utilizador
 - problemas.dat - ficheiro onde se encontram os problemas

O objectivo do programa é efectuar e mostrar ao utilizador a sequência de jogadas para remover todas as pecas do tabuleiro.

### Puzzle
Neste  ficheiro encontram-se as funções especificas ao jogo, tais como a distribuição das pecas durante uma jogada, a contagem de pecas num tabuleiro e a verificação de solução.

##### Distribute
``` javascript
 (defun distribute (n l c)
  (cond
   ((= n 0)nil)
   (t(cons (next-position l c)(distribute (1- n)
   (first(next-position l c))(second(next-position l c)))))))
```
Função que recebe uma posição no tabuleiro, linha coluna *l c* e um *n* que corresponde ao numero de peças a jogar, e retorna uma lista com todos as posições *(l c)* que devem ser incrementadas.

##### Increment
```javascript
(defun increment-all (lst board)
  (cond
   ((null lst)board)
   (t(increment-all (rest lst)(increment-position 
   (first(car lst))(second(car lst)) board)))))

(defun increment-position (lin col lst)
  (replace-a col lin lst (1+ (cell lin col lst))))
  ```

Funcão que recebe o tabuleiro *board* e a lista retornada peda função *distribute*
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2NjI4NDc4MDAsMTIwNjY1NjIxMCwzMD
Q5NjY4OTgsMTYzMDE4NTIzN119
-->