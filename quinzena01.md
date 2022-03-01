# SEMANA 1

**Paradigma**: estilo de programação.

- **Paradigma Imperativo**: um programa é uma sequência de comandos que alteram o estado do sistema; segue-se um “passo a passo” até chegar no resultado final desejado. O fluxo de controle é explícito e completo. Desvios incondicionais dificultam reprodução dos passos de execução

- **Paradigma Estruturado**: programas contém estrutura de fluxo de controle condicional. Estrutura-se o código em blocos lógicos (procedimentos e funções), os quais possuem no seu escopo instruções imperativas.

- **Paradigma de Orientação a Objetos** : utilizam-se classes e objetos. Objetos contêm dados, estados próprios e métodos que alteram ou recuperam os dados/estados (classes podem ter métodos de classe, compartilhados por todos objetos). Objetos comunicam entre si para compor a lógica do programa. As classes encapsulam códigos imperativos para segurança e reuso.

- **Paradigma Declarativo**: especifica-se o que se deseja realizar, mas sem detalhar os passos de execução. Utiliza DSLs e, por isto, atinge um nível mais alto de abstração que outros paradigmas.

- **Paradigma Lógico**: especifica-se um conjunto de fatos e regras; o interpretador infere respostas para perguntas sobre o programa. O retorno do programa é dado em forma de pergunta corretamente especificada.

## Paradigma Funcional
```
Programas são avaliações/composições de funções que não alteram estados; dados são imutáveis. Isso reduz a quantidade de bugs.
```
- Baseia-se no cálculo λ;
- Programas são declarativos, mas sem limitações do paradigma declarativo;
- Faz-se uso de um garbage collector para resolver as limitações que a imutabilidade de dados impõe;
- Usa funções puras: funções que não apresentam efeito colateral; para uma mesma entrada, sempre retornam o mesmos valor;
- Os laços iterativos são implementados via recursão;
- Linguagens funcionais podem usar avaliação preguiçosa. Se este for o caso, quando uma expressão é gerada, também é gerada uma promessa de execução. Quando necessário, a promessa é avaliada.

# SEMANA 2

## Cálculo λ
- Haskell é uma linguagem funcional cujo funcionamento se baseia no cálculo λ.

- O cálculo λ é uma alternativa teórica às máquinas de Turing como fundamento teórico para os computadores modernos.
Com funções λ é possível construir todos os tipos básicos, estruturas de dados e operadores que as linguagens de programação não funcionais costumam ter.

## GHC 

- O compilador GHC suporta nativamente vários tipos básicos de dados. Alguns deles são: Bool (booleanos); Char (caracteres); String (cadeias de caracteres); Int (inteiros de -2^63 até 2^63 -1 ); Integer (inteiros de precisão arbitrária);Float (valores em ponto-flutuante com precisão simples; Double (valores em ponto-flutuante com precisão dupla).

## Listas 
Haskell também tem suporte a listas, sendo “:” é o operador cons, de concatenação. 

        data [] a = [] | a : [a]


- Uma lista ou é a lista vazia, ou é uma concatenação de um elemento do tipo a com uma lista do tipo a.

- Listas podem ser “infinitas” - não infinitas de fato, mas seus elementos são avaliados apenas quando necessário (lazy evaluation).

- Algumas das funções básicas para manipulação de listas são:

        '!!' recupera o i-ésimo elemento da lista

        'head' retorna o primeiro elemento da lista

        'tail' retorna a lista sem o primeiro elemento

        'take' retorna os n primeiros elementos da lista

        'drop' retorna a lista sem os n primeiros elementos

        'sum' e 'product' retornam a somatória e produtória de uma lista

- É possível concatenar listas, realizar “pattern matching” com as mesmas e mesclar listas.
