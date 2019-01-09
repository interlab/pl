
#### Различия в регулярных выражениях между версиями языка Perl

#### Cсылки:
 - https://docs.perl6.org/language/5to6-nutshell#Regular_expressions_(_regex_/_regexp_)
 - https://docs.perl6.org/language/regexes
 - https://tpm-regex.perl6.party/
 - https://perldoc.pl/perlretut

| Perl 5 | Perl 6
| ------ | ------ |
| `next if $line  =~ /static/  ;`    | `next if $line ~~ /static/  ;`  |
| `next if $line !~ /dynamic/ ;`     | `next if $line !~~ /dynamic/ ;` |
| | |
| `$line =~ s/abc/123/;` | `$line ~~ s/abc/123/;` |
| `/(.+)/ and print $1;` | `/(.+)/ and print $0;` |
| `next if $line =~ /static/i;` | `next if $line ~~ m:i/static/;` |
| `next if $line =~ m/` | `next if $line ~~ m/` |
| `next if $line =~ m/[^abc]/;` | `next if $line ~~ m/<-[abc]>/;` |
| `next if $line =~ m/[a-zA-Z]/;` | `next if $line ~~ m/<[a..zA..Z]>/;` |
| `say $1 if 'abc' =~ /(?:a|b)(c)/; # OUTPUT: c` | `say ~$0 if 'abc' ~~ / [a||b] (c) /; # OUTPUT: c` |
| `say 'abcdefg' =~ /\w{2,5}/;` | `say 'abcdefg' ~~ /\w ** 2..5/;` |
|||
| `say 1 if 'foobar' =~ /(?<=foo)bar/;` | `say 1 if 'foobar' ~~ / <after foo> bar /;` |
| `say 0 unless 'foobar' =~ /(?<!foo)bar/;` | `say 0 unless 'foobar' ~~ / <!after foo> bar /;` |
| `say 1 if 'barbaz' =~ /bar(?=baz)/;` | `say 1 if 'barbaz' ~~ / bar <before baz> /;` |
| `say 0 unless 'barbaz' =~ /bar(?!baz)/;` | `say 0 unless 'barbaz' ~~ / bar <!before baz> /;` |


#### Perl 6
#### Жадное совпадение: .*

```perl
'abababa' ~~ /a .* a/ && say ~$/;   # abababa
```

#### Скромное совпадение .*?
```perl6
'abababa' ~~ /a .*? a/ && say ~$/;   # aba
```

#### Жадные и скромные совпадения для "общих квантификаторов" ** min..max
```perl6
say '/foo/o/bar/' ~~ /\/. ** 1..10 \//; # /foo/o/bar/
say '/foo/o/bar/' ~~ /\/.**!{1..10}\//; # /foo/o/bar/
say '/foo/o/bar/' ~~ /\/.**?{1..10}\//; # /foo/
```
