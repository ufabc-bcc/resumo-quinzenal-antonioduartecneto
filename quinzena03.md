### Monoids [Monóide]

Um semigrupo é uma dupla composta por um conjunto de valores e um operador binário associativo sobre esses valores, denominado mappend (ou <>).

Um monoide é um tipo de semigrupo. É uma tripla composta por um conjunto de valores, um elemento identidade pertencente a esse conjunto de valores, denominado mempty, e um operador binário associativo sobre esses valores, denominada mappend.

Alguns exemplos
    Valores inteiros com o operador + e o elemento identidade 0
    Valores inteiros com o operador * e o elemento identidade 1
    Valores String com o operador ++ e o elemento identidade ""
  
Em Haskell, a classe Monoid é definida como:

```haskell

class Monoid a where 
   mempty  :: a
   mappend :: a -> a -> a

   mconcat :: [a] -> a
   mconcat = foldr mappend mempty 


```

A função "mconcat" serve para aplicar sucessivamente mappend em dois elementos de uma lista de valores do tipo a até que se tenha um só elemento.
Caso mappend não seja definido, é pressuposto o mesmo da definição de Semigroup.

Em Haskell, listas e o tipo Maybe, por exemplo, são as seguintes instâncias da class Monoid:


```haskell
instance Monoid [a] where
    mempty = []
    mappend = (++)

```

```haskell
instance Monoid a => Monoid (Maybe a) where -- 
    mempty = Nothing

    Nothing  `mappend`   my      = my
    mx       `mappend`   Nothing = mx
    Just x   `mappend`   Just y  = Just (x `mappend` y)
```

### Foldable [Dobrável]

A classe dos Foldables permite uma generalização dos tipos que podem ser "dobráveis" (não apenas listas). Pode ser definida como a seguir:

```haskell

class Foldable t where
   fold    :: Monoid a => t a -> a
   foldMap :: Monoid b => (a -> b) -> t a -> b
   foldr   :: (a -> b -> b) -> b -> t a -> b
   foldl   :: (a -> b -> a) -> a -> t b -> a


```

A função foldMap é a implementação de um modelo de programação conhecido como MapReduce:
- Map (mapeamento de cada elemento do tipo t em um monóide a) é feito em paralelo e de maneira distribuída;
- A parte do "fold" se encarrega da parte do Reduce


### Functors [Funtor]

Functors (no Haskell, endofunctors, na verdade) são funções que fazem com que as funções do tipo a->b, que tem como input um certo tipo a, sejam aplicáveis a um tipo paramétrico f que contém esse tipo a e retornem um valor do tipo f b
 
No Haskell um Functor é definido como uma classe de tipos:

```haskell

class Functor f where
   fmap :: (a -> b) -> f a -> f b


```

- fmap gozar de duas propriedades:
	- fmap id = id
	- fmap f . fmap g = fmap (f.g)

Exemplo de functors do tipo Maybe:

```haskell
instance Functor Maybe where
  fmap _ Nothing =  Nothing
  fmap g (Just x) = Just (g x)
```

Exemplo de functors do tipo lista:

```haskell
instance Functor [] where
  fmap = map
```

- <$> é a mesma coisa que fmap

### Applicative Functors [Funtores Aplicativos]

Applicative têm sua classe de tipo definida como:

```haskell

class Functor f => Applicative f where
  pure  :: a -> f a
  (<*>) :: f (a -> b) -> f a -> f b


```

"pure" indica que estamos transformando uma função pura em um determinado contexto computacional (de computação não determinística, de computação que pode falhar, etc.)

Exemplo para o tipo Maybe:

```haskell
instance Applicative Maybe where
  pure             = Just
  Nothing  <*> _   = Nothing
  (Just g) <*> mx  = fmap g mx
```

Exemplo para o tipo []:

```haskell

instance Applicative [] where
  pure x    = [x]
  gs <*> xs = [g x | g <- gs, x <- xs]

```

### Traversable ["Percorrível" ou "Atavessável"]

Traversables são tipos que podem ser mapeados. A sua classe pode ser definida como:

```haskell

class (Functor t, Foldable t) => Traversable t where
  traverse :: Applicative f =>
			    (a -> f b) -> t a -> f (t b)

instance Traversable [] where
  traverse g []     = pure []
  traverse g (x:xs) = pure (:) <*> g x <*> traverse g xs


```

Exemplo de uso:

- Temos uma função que mapeia um tipo a para Maybe b, por exemplo, e temos uma lista de a.
- Desejamos retornar um Maybe [b], e não [Maybe b]
- Utilizando Applicative para listas, podemos fazer isso do seguinte modo:

```haskell
class (Functor t, Foldable t) => Traversable t where
  traverse :: Applicative f =>
			    (a -> f b) -> t a -> f (t b)

instance Traversable [] where
  traverse g []     = pure []
  traverse g (x:xs) = pure (:) <*> g x <*> traverse g xs
```


