### Bag

#### Links
 - [Sets, bags, and mixes](https://docs.perl6.org/language/setbagmix)
 - [Bag](https://docs.perl6.org/type/Bag)

#### (.) Baggy multiplication operator.
Возвращает суммарное умножение своих аргументов, т. е. сумку, содержащую каждый элемент аргументов с весами элемента по аргументам, умноженным вместе, чтобы получить новый вес.
```perl6
> <a b c> (.) <a b c d>
Bag(a, b, c)

> bag(<a a b c a d>) (.) bag(<a a b c c>)
Bag(a(6), b, c(2))

> <a a b c a d> (.) <a a b c c>
Bag(a(6), b, c(2))
```

#### (+) Baggy addition operator
Возвращает суммарное дополнение его аргументов, т. е. cумку, содержащую каждый элемент аргументов с весами элемента по аргументам, добавленным вместе для получения нового веса.
```perl6
> bag(<a a b c a d>) (+) bag(<a a b c c>)
Bag(a(5), b(2), c(3), d)
```
