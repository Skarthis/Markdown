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
Função que retorna uma lista de posições onde é possível efectuar uma jogada.

##### Count-pieces
```javascript
(defun count-pieces (node)
  (+ (count-pieces-aux(first(get-node-state node)))
     (count-pieces-aux(second(get-node-state node)))))

(defun count-pieces-aux (lst &optional (n 0))
  (cond
   ((= 6 n)0)
   (t (+ (nth n lst)(count-pieces-aux lst (1+ n))))))
   ```
Função que conta todas as peças existentes no tabuleiro actual.
##### Get-solution-states
```javascript
(defun get-solution-states (node)
  (cond 
   ((null (get-node-parent node))(list (car node)))
   (t (append (get-solution-states (get-node-parent node))
    (list (car node))))))
```
Função que retorna todos os tabuleiros desde o nó *node* até ao nó de origem.


### Procura

Ficheiro que contem as funções relativas aos algoritmos de procura e todas as funções que os suportam, como a construção e a geração de nós, heurísticas.
Um nó tem a seguinte estrutura:
`<nó>::= ( <
estado_do_tabuleiro > < nó-pai > g h )
`
onde *g* corresponde à profundidade, e *h* ao valor heurístico do nó.

##### Heuristic-a
```javascript
(defun heuristic-a (node)
  (- (count-pieces node)
   (-(count-pieces(get-origin-node node))(count-pieces node))))
  ```
  Função que define a heurística: 
  h(x) = o(x) − c(x) em que: 
 
 - o(x) é o número de peças a capturar no tabuleiro x
 - c(x) é o número de peças já capturadas no tabuleiro x

##### Expand-node
```javascript
(defun expand-node (node)
  (expand-node-aux node (possible-plays(get-node-state node))))
  
(defun expand-node-aux (node lst)
  (cond
   ((null lst)nil)
   (t (cons (construct-node(play (first(car lst))
(second(car lst)) (get-node-state node)) node (1+ 
(get-node-g node)))
(expand-node-aux node (rest lst))))))

(defun expand-node* (chosen-node heuristic)
  (mapcar #'(lambda (node) (change-value-h node 
  (funcall heuristic node))) (expand-node chosen-node)))
  ```
  
  Funções que geram os nós sucessores para os diferentes algoritmos de procura.

##### Breadth-first search

```javascript
(defun bfs(expandFunction open &optional (closed '()))
  (let ((open-size (length open)))
   (cond
    ((= open-size 0) nil)
    (t
     (let* ((chosen-node (car open))
            (expanded-list (funcall expandFunction chosen-node)))
      (if (solutionp chosen-node)
       (list (get-solution-states chosen-node) (length open) (length closed))
        (bfs expandFunction (concatenate 'list (cdr open) (remove-nil (remove-duplicated expanded-list open closed)))
			(concatenate 'list closed (list chosen-node)))))))))
```
Algoritmo de procura em largura. Recebe o nome da função geradora *expandFunction* e uma lista com o nó inicial *(list node)*. O algoritmo começa por atribuir o nó corrente à lista de abertos e gera uma lista de sucessores, o critério de paragem do algoritmo é dado pela função *solutionp* que verifica se um nó é solução. Caso não seja verificado o critério de paragem, o algoritmo é chamado recursivamente colocando o nó corrente na lista de fechados e concatenando à lista de abertos a lista de sucessores.

##### Depth-first search

```javascript
(defun dfs(expandFunction max-depth open &optional (closed '()))
  (cond
   ((= (length open) 0) nil)
   ((> (calculate-node-depth (car open)) max-depth) (dfs expandFunction max-depth (cdr open) (concatenate 'list closed (car open))))
   (t
     (let* ((chosen-node (car open))
            (expanded-list (funcall expandFunction chosen-node)))
      (if (solutionp chosen-node)
        (list (get-solution-states chosen-node) (calculate-node-depth chosen-node) (length open) (length closed))
       (dfs expandFunction max-depth (concatenate 'list expanded-list(cdr open))
		(concatenate 'list closed chosen-node)))))))
```
Algoritmo de procura em profundidade. Recebe o nome da função geradora _expandFunction_ , a profundidade máxima e uma lista com o nó inicial _(list node)_. O algoritmo começa por atribuir o nó corrente à lista de abertos e gera uma lista de sucessores, o critério de paragem do algoritmo é dado pela função _solutionp_ que verifica se um nó é solução. Caso não seja verificado o critério de paragem, o algoritmo é chamado recursivamente colocando o nó corrente na lista de fechados e concatenando à lista de abertos a lista de sucessores, mas ordenando os sucessores em primeiro lugar. Para além disso não serão gerados quaisquer nós com profundidade que ultrapasse a profundidade máxima dada.

##### A* 
```javascript
(defun A*(expandFunction heuristic open &optional (closed '()) (expanded-nodes 0))
  (cond
   ((= (length open) 0) nil)
   (t
     (let* ((chosen-node (get-lowest-value open))
            (expanded-list (funcall expandFunction chosen-node heuristic))
            (updated-closed (update-closed expanded-list closed chosen-node))
            (updated-open (update-open expanded-list (cdr open) chosen-node))
            (new-open (remove-nil (append updated-open (remove-duplicated-aux expanded-list updated-open) updated-closed))))
      (if (solutionp chosen-node)
       (list (get-solution-states chosen-node) (length open) (length closed) expanded-nodes)
        ;;chama a*, colocando os sucessores em open e poe o primeiro elemento de open em closed
       (A* expandFunction heuristic new-open (remove-duplicated-aux (concatenate 'list closed (list chosen-node)) 
												updated-closed) (1+ expanded-nodes)))))))	
```
O algoritmo A* tem uma estrutura similar aos anteriores. Sendo a diferença entre o A*, que é um algoritmo de procura informada, e os anteriores que o A* associa um valor heurístico a cada nó e opta por expandir em primeiro lugar o nó de menor custo.

```javascript
(defun get-lowest-value (open)
  (cond
   ((= (length open)1)(car open))
   (t (let ((lowest-node (get-lowest-value (rest open))))
        (if (< (get-node-value (car open))(get-node-value lowest-node))(car open)
          lowest-node)))))
```
Função usada pelo A* para escolher o nó de menor custo numa dada lista de abertos.

### Projecto
Este ficheiro constitui a interacção com o utilizador, e a criação de estatísticas gravadas em *resultados.dat*. Assim como ler os problemas presentes no ficheiro *problemas.dat*.


##### Get-problems-path
```javascript
(defun get-problems-path()
"path (C:\lisp\problemas.dat)"
    (make-pathname :host "c" :directory '(:absolute "ia") :name "problemas" :type "dat"))
```
Função que define o __path__ para o ficheiro *problemas.dat*.

##### Read-boards
```javascript
(defun read-boards ()
   (with-open-file (file (get-problems-path) :if-does-not-exist nil)
     (do ((result nil (cons next result))
        	(next (read file nil 'eof) (read file nil 'eof)))
                ((equal next 'eof) (reverse result)))))
```
Função que lê os tabuleiros do ficheiro *problemas.dat*

##### Read-board
```javascript
(defun read-board(backMenu)
    (progn (boards)
      (let ((opt (read)))
           (cond ((eq opt '0) (funcall backMenu))
                 ((not (numberp opt)) (progn (format t "Insira uma opção válida") (read-board backMenu))) 
                 (t
                  (let ((boards-list (read-boards)))
                  (if (or (< opt 0) (> opt (length boards-list))) (progn (format t "Insira uma opção válida") (read-board backMenu))
                                 (list opt (nth(1- opt) boards-list))
                  )))))))
```
Função que escolhe o tabuleiro que o utilizador escolheu através da interface para ser usado num jogo.

##### Exec-search
```javascript 
(defun exec-search()
;;Executa um algoritmo, dependendo da opcao escolhida"
    (progn (read-algorithm-message)
      (let ((opt (read)))
           (cond ((not (numberp opt)) (progn (format t "Insira uma opção válida") (exec-search)))
                 ((or (> opt 4) (< opt 0) ) (progn (format t "Insira uma opção válida") (exec-search)))
                 ((eq opt 0) (start))         
                 (T (let* ((board-node (read-board 'exec-search))
                           (board (second board-node))
                           (nboard (first board-node))
                           (node (list (construct-node board nil))))
                        (ecase opt
                          (1 
                             (let ((solution (list (current-time) (bfs 'expand-node node) (current-time) nboard 'BFS)))
                               (progn (write-statistics-file solution) solution)))

                          (2 (let* ((depth (read-depth))
                                    (solution (list (current-time) (dfs 'expand-node depth node) (current-time) nboard 'DFS depth)))
                               (progn (write-statistics-file solution) solution)))
     
                          (3  (let* ((heuristic (read-heuristic))
                                    (solution (list (current-time) (A* 'expand-node* heuristic node) (current-time) nboard 'A*)))
                              (progn (write-statistics-file solution) solution)))
							  )))))))
```

Função que executa um jogo, depois de o utilizador ter feito as selecções necessárias na interface.


##### Conjunto de funções que geram as estatísticas no ficheiro resultados
```javascript
(defun write-statistics-file (solution)
  (let* ((start-time (first solution))
         (solution-path (second solution))
         (end-time (third solution))
         (nboard (fourth solution))
         (search (fifth solution)))
            (with-open-file (file (get-results-path) :direction :output :if-exists :append :if-does-not-exist :create)
                (ecase search
                      ('BFS (write-bfsdfs-statistics file solution-path start-time end-time nboard 'BFS ))         
                          ('DFS (let ((depth (sixth solution))) (write-bfsdfs-statistics file solution-path start-time end-time nboard 'DFS depth)))
                      ('A* (write-a*-statistics file solution-path start-time end-time nboard 'A* ))
                ))))


(defun write-bfsdfs-statistics (stream solution-path start-time end-time nboard search &optional depth)
  (progn 
    (format stream "~%* Resolução do Tabuleiro ~a *" nboard)
    (format stream "~%~t> Algoritmo: ~a " search)
    (format stream "~%~t> Início: ~a:~a:~a" (first start-time) (second start-time) (third start-time))
    (format stream "~%~t> Fim: ~a:~a:~a" (first end-time) (second end-time) (third end-time))
    (format stream "~%~t> Número de nós gerados: ~a" (number-generated-nodes solution-path))
    (format stream "~%~t> Número de nós expandidos: ~a" (number-expanded-nodes-bfsdfs solution-path))
    (format stream "~%~t> Penetrância: ~F" (penetrance solution-path))
    (format stream "~%~t> Fator de ramificação média ~F" (branching-factor solution-path))
    (if (eq search 'DFS)
        (format stream "~%~t> Profundidade máxima: ~a" depth))
    (format stream "~%~t> Comprimento da solução ~a" (solution-length solution-path))
    (format stream "~%~t> Estado Inicial")
    (print-board (first (first solution-path)) stream)
    (format stream "~%~t> Estado Final")
    (print-board (solution-node solution-path) stream)
  ))

  
(defun write-a*-statistics (stream solution-path start-time end-time nboard search)
  (progn 
    (format stream "~%* Resolução do Tabuleiro ~a *" nboard)
    (format stream "~%~t> Algoritmo: ~a " search)
    (format stream "~%~t> Início: ~a:~a:~a" (first start-time) (second start-time) (third start-time))
    (format stream "~%~t> Fim: ~a:~a:~a" (first end-time) (second end-time) (third end-time))
    (format stream "~%~t> Número de nós gerados: ~a" (number-generated-nodes solution-path))
    (format stream "~%~t> Número de nós expandidos: ~a" (number-expanded-nodes-a* solution-path))
    (format stream "~%~t> Penetrância: ~F" (penetrance solution-path))
    (format stream "~%~t> Fator de ramificação média: ~F" (branching-factor solution-path))
    (format stream "~%~t> Comprimento da solução ~a" (solution-length solution-path))
    (format stream "~%~t> Estado Inicial")
    (print-board (first (first solution-path)) stream)
    (format stream "~%~t> Estado Final")
    (print-board (solution-node solution-path) stream)
  ))
```
### Resultados
Estatísticas obtidas da execução dos algoritmos de procura com os vários problemas, a heurística usada foi a fornecida no enunciado.

| Tabuleiro | Algoritmo | Nós Gerados | Nós Expandidos | Penetrância | Fator Ramificação | Inicio | Fim |
|:-----|:------|:-----|:-----|:-----|:-----|:-----|:-----|
| 1 | BFS | 24| 15 | 0.20833333 |1.5968559 | 0:55:0 | 0:55:0 |
| 1 | DFS | 13 | 6 | 0.61538464 | 1.0852652 | 0:55:11 | 0:55:11 |
| 1 |  A*| 10 | 6 | 0.7 | 1.0852652 | 1:5:16 | 1:5:16 |
|2|BFS|- |- |- |- |- |- |
|2|DFS|78 |60 | 0.24358975| 1.1421085| 0:55:14|0:55:14 |
|2|A*|40 |35 |0.425 | 1.0852652| 1:7:33 |  1:7:33|
|3 |BFS| 3983|1154 |0.0017574693 |3.0747845 |0:55:3 |0:55:4 |
|3 |DFS| 28|18 |0.39285713 |1.1421085 |0:55:28 |0:55:28 |
|3 |A*|15 | 6|0.46666667 | 1.198952| 1:8:0|1:8:0 |
|4 |BFS|- |- |- |- |- |- |
|4 |DFS|213|169 |0.2112676 |1.0852652 |0:55:39 |0:55:39 |
|4 |A*|147 |60 |0.27891156 | 1.0284217|  1:8:14|  1:8:14|
|5 |BFS|- |- |- |- | -|- |
|5 |DFS|539 |435| 0.19480519|1.0284217 |0:56:21 |0:56:21 |
|5 |A*|198 |194 | 0.32323232 | 1.0284217| 1:8:30|1:8:30 |
|6 |BFS|- |- |- | -|- |- |
|6 |DFS|364 |291 | 0.2032967|1.0284217 |0:56:48 |0:56:48 |
|6 |A*|193 | 168 | 0.29015544 |1.0284217 |1:8:43 |1:8:43 |
|7 |BFS|- | -| -|- |- |- |
|7 |DFS|618 |503 |0.18770227 |1.0284217 |  0:56:59| 0:56:59 |
|7 |A*|217 |213 |0.31797236 | 1.0284217|1:8:54 |1:8:54 |


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTExODg2NTQzMjksLTY3NTAzNDg2OCwyMD
I5MTI2MjksLTk1MDk0Mzc4MywtNjk3MjAwMTA0LDEyMDY2NTYy
MTAsMzA0OTY2ODk4LDE2MzAxODUyMzddfQ==
-->