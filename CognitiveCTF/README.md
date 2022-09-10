# CognitiveCTF

CognitiveCTFを解いたときの記録を徒然していこうかなと思いました。

## 2Warm（2022年9月11日）

問題の概要
> 121(10進法)を2進数に変換する

### 考え方１

コマンドラインで進数変換できたはず。

調べたら`bc`コマンドが出てきた。

> ```
> echo "obase=to_base; ibase=from_base; number_str" | bc
> ```
> obase,ibaseで指定できる値は、2以上の整数ならなんでもOK。
https://qiita.com/macoril/items/77ba050cad17f03ed46a

ということは、`echo "obase=2; ibase=10; 121" | bc`でいける。

```bash
AyatoShitomi@picoCTF_production_shell_001:~$ echo "obase=2; ibase=10; 121" | bc
1111001
AyatoShitomi@picoCTF_production_shell_001:~$ 
```

よって`1111001`がフラグの中身

### 考え方２

進数変換は上から順に変換する数で割っていけばいい。

> 121/2 = 60 ... 1
60/2 = 30 ... 0
30/2 = 15 ... 0
15/2 = 7 ... 1
7/2 = 3 ... 1
3/2 = 1 ... 1
1/2 = 0 ... 1

よって`1111001`がフラグの中身

