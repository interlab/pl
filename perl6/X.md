
### Оператор X

#### Ссылки по теме:
 - [infix X](https://docs.perl6.org/language/operators#infix_X)

#### Синтаксис
```perl6
sub infix:<X>(**@lists --> List:D)
```

#### Examples
```perl6
1..3 X <a b c> X 9
# produces ((1 a 9) (1 b 9) (1 c 9)
#           (2 a 9) (2 b 9) (2 c 9)
#           (3 a 9) (3 b 9) (3 c 9))
```

```perl6
1..3 X~ <a b c> X~ 9
# produces (1a9 1b9 1c9 2a9 2b9 2c9 3a9 3b9 3c9) 
```

```perl6
for (-25..25) X (-25..25) -> ($y, $x) {
    print (16² < $x² + $y² < 20²) ?? 'o' !! '.';
    $x == 25 && say '';
}
```