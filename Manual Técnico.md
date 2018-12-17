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

Função que recebe o tabuleiro *board* e a lista retornada pela função *distribute* e incrementa todas as posições na lista.

##### Next-position
```javascript
(defun next-position (l c)
  (cond
  ((and (= l 0)(= c 0))(list 1 0))
  ((and (= l 1)(= c 5))(list 0 5))
  ((and (= l 0)(and (> c 0)(<= c 5)))(list l (1- c)))
  ((and (= l 1)(and (>= c 0)(< c 5)))(list l (1+ c)))))
```
Função que recebe uma posição *l c* e retorna a posição seguinte de acordo com as regras do jogo, sentido de relógio inverso.

##### Play
```javascript
(defun play (l c board)
  (replace-a c l (play-aux (increment-all 
  (distribute(cell l c board) l c) board)
  (car(last (distribute(cell l c board) l c))))))
  
(defun play-aux (board pos)
   (let ((var (cell (first pos)(second pos) board)))
     (cond
      ((or (= 1 var)(= 3 var)(= 5 var))(replace-a 
      (second pos)(first pos) board))
      (t board))))
```
Função que efectua uma jogada no tabuleiro, remove as peças na posição *l c* e distribui pelas casas seguintes.

##### Possible-plays
```javascript
(defun possible-plays (board)
  (remove-nil(cons (car (possible-plays-aux board 0))
  (possible-plays-aux board 1))))

(defun possible-plays-aux(board l &optional (c 5))
  (cond
   ((< c 0)nil)
   ((= (cell l c board) 0)(possible-plays-aux board l (1- c)))
   (t (cons (list l c)(possible-plays-aux board l (1- c))))))
   ```
Função que retorna uma
<!--stackedit_data:
eyJoaXN0b3J5IjpbMzI5NzYzMDc2LDEyMDY2NTYyMTAsMzA0OT
Y2ODk4LDE2MzAxODUyMzddfQ==
-->