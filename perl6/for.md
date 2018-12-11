

### Цикл for

#### Ссылки по теме:
- [Цикл for в Perl 6](https://perl6.ru/2018/01/07/%d1%80%d0%b0%d0%b7%d0%bd%d1%8b%d0%b5-%d0%b2%d0%b8%d0%b4%d1%8b-for-%d0%b2-perl-6/)
- https://docs.perl6.org/language/control#for
- https://perl6advent.wordpress.com/2009/12/07/day-7-looping-for-fun-and-profit/

#### Примеры:

#### Обход массива
```perl6
my @a = <alpha beta gamma delta>;
for @a {
  say $_;
}
```

то же самое:
```perl6
.say for @a;
```

то же самое:
```perl6
for @a -> $x {
  say $x;
}
```

Вывод сразу двух элементов на ряд:
```perl6
for @a -> $x, $y {
  say "$x $y";
}
```

#### Сохранить список значений в массив:
```perl6
my @a = do for 1, 2, 3 { $_ * 2 };
@a.say; # [2 4 6]
my @b = (for 1, 2, 3 { $_ * 2 });
@b.say; # [2 4 6]

```

#### Объединение двух массивов:
```perl6
for @array1 Z @array2 -> $it { say $it[0], ' ', $it[1]; }
```

Массивов может быть много:
```perl6
for @one Z @two Z @three Z @four -> $it {
  say $it.join(' - ');
}
```

#### Обход с индексом шага.
Вам нужна функция [enumerate](https://docs.python.org/3/library/functions.html#enumerate) из Python 3? Делайте так:
```perl6
my @array = <a b c d e f g h>;
for (^Inf Z @array).flat -> $index, $item { say $index, ' ', $item; }
```

То же самое, но компактней
```perl6
for ^Inf Z @array -> ($index, $item) { say $index, ' ', $item; }
```

Или добавляйте индекс вот так:
```perl6
for ^@array.elems Z @array -> ($index, $item) { say $index, ' ', $item; }
```

То же самое (элегантное решение): 
```perl6
for @array.kv -> $index, $item { say $index, ' ', $item; }
```

#### Обход хеша:
```perl6
my %h = alpha => 'a', beta => 'b', 
    gamma => 'c', delta => 'd';

for %h.kv -> $greek, $latin {
  say "$greek = $latin";
}
```

#### С проверкой типа:
```perl6
for 1..5 -> Int $i {
  say $i;
}
```

#### С "распаковкой аргумента"
```perl6
my @itemlist = (
    { book =>
        { author => 'Пушкин А. С.', title => 'Сказка о попе и ...' },
        count => 1,
        tags => <Поп Балда попадья черти>
    },
    {
        book =>
        { author => 'Гоголь Н. В.', title => 'Ночь перед ...' },
        count => 1,
        tags => <Вакула Солоха Дьяк Чёрт>
    },
);

for @itemlist -> % (:%book (Str:D :$title, Str:D :$author), Int :$count,
          :@tags ($first-tag, *@other-tags))
{
  say "$title, $author, $count, $first-tag, @other-tags[]";
}
```

#### Loop Phasers

see: [Loop Phasers](https://docs.perl6.org/language/phasers#Loop_Phasers)

Если у вас будет элемент с типом, отличимым от Int, то будет ошибка. FIRST сработает в начале, NEXT при каждом шаге цикла, LAST в конце.
```perl6
my @a2 = 1..Inf;
my $s = '-' x 10;
for @a2[^5] -> Int $i {
  FIRST { say "Поехали!\n{$s}"; }
  say $i;
  NEXT { say $s; }
  LAST { say 'Полёт завершён!'; }
}
```

#### next, redo, last
```perl6
for @q {
  say $_;
  # You can...
  next if $_ == 3; # Skip to the next iteration (`continue` in C-like languages).
  redo if $_ == 4; # Re-do the iteration, keeping the same topic variable (`$_`).
  last if $_ > 5; # Or break out of a loop (like `break` in C-like languages).
}
```

#### read-write
```perl6
my @foo = 1..3;
for @foo <-> $_ { $_++ }
say @foo; # [2, 3, 4]
```

#### default values
```perl6
my @list = 1, 2, 3, 4;
for @list -> $a, $b = 'N/A', $c = 'N/A' {
  say "$a $b $c";
}
# 1 2 3
# 4 N/A N/A
```
