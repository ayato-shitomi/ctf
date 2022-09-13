# rsa-pop-quiz（2022年9月12日）未解決

## 問題

> クラスの皆さん、席についてください！小テストの時間です... `nc shell1.production.cognitivectf.com 26616`

## アプローチ

とりあえず、これでqとpが出てきたので、そっから出てくるはず。

```
AyatoShitomi@picoCTF_production_shell_001:~$ nc shell1.production.cognitivectf.com 26616
#### NEW PROBLEM ####
q : 60413
p : 76753
##### PRODUCE THE FOLLOWING ####
n
IS THIS POSSIBLE and FEASIBLE? (Y/N):Y
#### TIME TO SHOW ME WHAT YOU GOT! ###
n: 
That's not an int! Exiting

AyatoShitomi@picoCTF_production_shell_001:~$ 
```

n = qp

途中でわからなかったので、放置
