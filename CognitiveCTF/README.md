# CognitiveCTF

CognitiveCTFを解いたときの記録を徒然していこうかなと思いました。

## 13（2022年9月11日）

### 問題
> 暗号は時として簡単に解けることもあります。ROT13をご存知ですか？`PbtavgvirPGS{abg_gbb_onq_bs_n_ceboyrz_7qsn03oq}`

### 考え方

`rot13`について調べたらシーザー暗号の一つで文字を13個後ろに入れ替えてるだけ。
変換サイトがあるので、これに入れればいい

https://rot13.com/

フラグは`CognitiveCTF{not_too_bad_of_a_problem_7dfa03bd}`だった。

## handy-shellcode（2022年9月11日）未解決

Binary Rxploitationと呼ばれる分野らしい。

### 問題の概要

> このプログラムは与えた任意のシェルコードを実行します。<br>
> シェルを起動し、それを使ってflag.txtを読み出してください。<br>
> このプログラムはshell1.production.cognitivectf.comの以下ディレクトリに置かれています。<br>
> `/problems/handy-shellcode_3_eefb645e8107c9aa00c62fb91b755de8`<br>
> なおプログラムのソースコードはここからダウンロードできます。<br>

### アプローチ

「このプログラム」をダウンロードする。

```shell
AyatoShitomi@picoCTF_production_shell_001:~$ curl -OL https://shell1.production.cognitivectf.com/static/a2ca0dccd07a850a295dc299b763230a/vuln
```

先ほど同様「ソースコードはここからダウンロード」をCURLでダウンロードする。

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <sys/types.h>

#define BUFSIZE 148
#define FLAGSIZE 128

void vuln(char *buf){
  gets(buf);
  puts(buf);
}

int main(int argc, char **argv){

  setvbuf(stdout, NULL, _IONBF, 0);

  // Set the gid to the effective gid
  // this prevents /bin/sh from dropping the privileges
  gid_t gid = getegid();
  setresgid(gid, gid, gid);

  char buf[BUFSIZE];

  puts("Enter your shellcode:");
  vuln(buf);

  puts("Thanks! Executing now...");

  ((void (*)())buf)();


  puts("Finishing Executing Shellcode. Exiting now...");

  return 0;
}
```

わからなかったから放置

## 2Warm（2022年9月11日）

### 問題の概要
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

