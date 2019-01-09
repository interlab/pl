
#### Различия в регулярных выражениях между версиями языка Perl

#### Cсылки:
 - https://docs.perl6.org/language/5to6-nutshell#Regular_expressions_(_regex_/_regexp_)
 - https://docs.perl6.org/language/regexes
 - https://tpm-regex.perl6.party/
 - https://perldoc.pl/perlretut


Perl 5
```perl5
next if $line  =~ /static/  ;
```

Perl 6
```perl6
next if $line ~~ /static/  ;
```

---

Perl 5
```perl5
next if $line !~ /dynamic/ ;
```

Perl 6
```perl6
next if $line !~~ /dynamic/ ;
```

---

Perl 5
```perl5
$line =~ s/abc/123/;
```

Perl 6
```perl6
$line ~~ s/abc/123/;
```

---

Perl 5
```perl5
/(.+)/ and print $1;
```

Perl 6
```perl6
/(.+)/ and print $0;
```

---

Perl 5
```perl5
next if $line =~ /static/i;
```

Perl6
```perl6
next if $line ~~ m:i/static/;
```

---

Perl 5
```perl5
next if $line =~ m/
```

Perl 6
```perl6
next if $line ~~ m/
```

---

Perl 5
```perl5
next if $line =~ m/[^abc]/;
```

Perl 6
```perl6
next if $line ~~ m/<-[abc]>/;
```

---

Perl 5
```perl5
next if $line =~ m/[a-zA-Z]/;
```

Perl 6
```perl6
next if $line ~~ m/<[a..zA..Z]>/;
```

---

Perl 5
```perl5
say $1 if 'abc' =~ /(?:a|b)(c)/; # OUTPUT: c
```

Perl 6
```perl6
say ~$0 if 'abc' ~~ / [a||b] (c) /; # OUTPUT: c
```

---

Perl 5
```perl5
say 'abcdefg' =~ /\w{2,5}/;
```

Perl 6
```perl6
say 'abcdefg' ~~ /\w ** 2..5/;
```

---

Perl 5
```perl5
say 1 if 'foobar' =~ /(?<=foo)bar/;
```

Perl 6
```perl6
say 1 if 'foobar' ~~ / <after foo> bar /;
```

---

Perl 5
```perl5
say 0 unless 'foobar' =~ /(?<!foo)bar/;
```

Perl 6
```perl6
say 0 unless 'foobar' ~~ / <!after foo> bar /;
```

---

Perl 5
```perl5
say 1 if 'barbaz' =~ /bar(?=baz)/;
```

Perl 6
```perl6
say 1 if 'barbaz' ~~ / bar <before baz> /;
```

---

Perl 5
```perl5
say 0 unless 'barbaz' =~ /bar(?!baz)/;
```

Perl 6
```perl6
say 0 unless 'barbaz' ~~ / bar <!before baz> /;
```


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
