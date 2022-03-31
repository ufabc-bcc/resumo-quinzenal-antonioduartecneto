### Monoids

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

### Foldable

A classe dos Foldables pode ser definido como a seguir:

```haskell

class Foldable t where
   fold    :: Monoid a => t a -> a
   foldMap :: Monoid b => (a -> b) -> t a -> b
   foldr   :: (a -> b -> b) -> b -> t a -> b
   foldl   :: (a -> b -> a) -> a -> t b -> a


```


### Functores

Functors são funções que fazem com que as funções de um certo tipo sejam aplicáveis a um tipo paramétrico contendo esse tipo.

No Haskell um Functor é definido como uma classe de tipos:

```haskell

class Functor f where
   fmap :: (a -> b) -> f a -> f b


```

### Funtores Aplicativos

Applicative têm sua classe de tipo definida como:

```haskell

class Functor f => Applicative f where
  pure  :: a -> f a
  (<*>) :: f (a -> b) -> f a -> f b


```

### Traversable

Traversables são tipos que podem ser mapeados. A sua classe pode ser definida como:

```haskell

class (Functor t, Foldable t) => Traversable t where
  traverse :: Applicative f =>
			    (a -> f b) -> t a -> f (t b)

instance Traversable [] where
  traverse g []     = pure []
  traverse g (x:xs) = pure (:) <*> g x <*> traverse g xs


```


