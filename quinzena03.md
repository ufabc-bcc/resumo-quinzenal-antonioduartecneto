### Monoids; Foldable

Um Monoid é um conjunto de valores associados a um operador binário associativo e um elemento identidade:

    Valores inteiros com o operador + e o elemento 0
    Valores inteiros com o operador * e o elemento 1
    Valores String com o operador ++ e o elemento ""
A classe Monoid é definida como:

```haskell

class Monoid a where
   mempty  :: a
   mappend :: a -> a -> a

   mconcat :: [a] -> a
   mconcat = foldr mappend mempty


```


### Functores
### Funtores Aplicativos
### Traversable
