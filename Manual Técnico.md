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

####
``` javascript
 (defun distribute (n l c)
  (cond
   ((= n 0)nil)
   (t(cons (next-position l c)(distribute (1- n)
   (first(next-position l c))(second(next-position l c)))))))
```

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTE5MzA2Njc2OSwxMjA2NjU2MjEwLDMwND
k2Njg5OCwxNjMwMTg1MjM3XX0=
-->