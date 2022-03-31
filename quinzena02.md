Quickcheck é uma bilbioteca de testes baseada em testes de invariantes (os quais corretude capturam a corretude do algoritmo), complementar a testes unitários. 

Funções de alta ordem são funções que admitem outras funções como entradas ou devolvem outras funções. No Haskell, funções de alta ordem podem ser pensadas como tipos de dados, os quais podem servir como argumentos de entrada de outras funções ou como saída destas. Funções de alta ordem permitem realizar tarefas que seriam muito dificilmente executadas caso funções de alta ordem não existissem.
As duas funções de alta ordem mais icônicas em Haskell são:

Map – aplica uma mesma função a todas as entradas de uma lista;
	ex.: map (+3) [1, 5, 7, 9]  retorna [4, 8, 10, 12]
Filter – “filtra” de uma lista A uma outra lista B que contém apenas os elementos de A que respeitem uma certa condição.
	ex.: filter (<3) [1, 2, 5, 8, -1, 0] retorna [1, 2, -1, 0]

Outras funções de alta ordem importantes:
any – recebe um predicado p e uma lista; retorna True se existe algum elemento da lista para o qual o predicado p é verdadeiro; retorna False do contrário;
takeWhile -  recebe um predicado f e uma lista A; retira os elementos da lista A e colocando na lista B até quando encontra o primeiro elemento de A para o qual o predicado f não vale; retorna B;
dropWhile -  análogo a takeWhile, mas com a lógica da função “drop”.

Folding: técnica que permite aplicar, sequencialmente, uma função f a cada elemento da lista e a um resultado parcial, o qual é obtido de forma incremental.
foldr: começa a partir do fim da lista;
foldl: começa a partir do início da lista

Composição de funções em Haskell: utiliza-se o operador ‘.’ (ponto).


