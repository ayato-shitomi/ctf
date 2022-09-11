# CognitiveCTF

CognitiveCTFを解いたときの記録を徒然していこうかなと思いました。
フラグ形式`CognitiveCTF{}`で、大文字小文字区別なし。


## vault-door-1（2022年9月12日）

### 問題

> この金庫は複雑な配列を使っている！君が解明してくれることを願っているよ、特別捜査官。
金庫のソースコードはここだ: `VaultDoor1.java`

### アプローチ

Curlでとってくる。

```java
import java.util.*;

class VaultDoor1 {
    public static void main(String args[]) {
        VaultDoor1 vaultDoor = new VaultDoor1();
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter vault password: ");
        String userInput = scanner.next();
        String input = userInput.substring("CognitiveCTF{".length(),userInput.length()-1);
        if (vaultDoor.checkPassword(input)) {
            System.out.println("Access granted.");
        } else {
            System.out.println("Access denied!");
        }
    }

    // I came up with a more secure way to check the password without putting
    // the password itself in the source code. I think this is going to be
    // UNHACKABLE!! I hope Dr. Evil agrees...
    //
    // -Minion #8728
    public boolean checkPassword(String password) {
        return password.length() == 32 &&
               password.charAt(10) == '_' &&
               password.charAt(11) == 't' &&
               password.charAt(18) == 'r' &&
               password.charAt(31) == '9' &&
               password.charAt(14) == '_' &&
               password.charAt(3)  == 'c' &&
               password.charAt(24) == '5' &&
               password.charAt(2)  == '5' &&
               password.charAt(27) == '3' &&
               password.charAt(7)  == 'b' &&
               password.charAt(25) == '_' &&
               password.charAt(17) == '4' &&
               password.charAt(29) == 'c' &&
               password.charAt(0)  == 'd' &&
               password.charAt(1)  == '3' &&
               password.charAt(22) == '3' &&
               password.charAt(9)  == '3' &&
               password.charAt(20) == 'c' &&
               password.charAt(5)  == '4' &&
               password.charAt(15) == 'c' &&
               password.charAt(30) == '8' &&
               password.charAt(26) == 'c' &&
               password.charAt(13) == '3' &&
               password.charAt(4)  == 'r' &&
               password.charAt(28) == 'c' &&
               password.charAt(6)  == 'm' &&
               password.charAt(8)  == 'l' &&
               password.charAt(23) == 'r' &&
               password.charAt(12) == 'H' &&
               password.charAt(16) == 'H' &&
               password.charAt(21) == 'T' &&
               password.charAt(19) == '4';
    }
}
```

並べ替えればフラグになると思われる。
`t`というファイルを作った。
```
               password.charAt(10) == '_' &&
               password.charAt(11) == 't' &&
               password.charAt(18) == 'r' &&
               password.charAt(31) == '9' &&
               password.charAt(14) == '_' &&
               password.charAt(3)  == 'c' &&
               password.charAt(24) == '5' &&
               password.charAt(2)  == '5' &&
               password.charAt(27) == '3' &&
               password.charAt(7)  == 'b' &&
               password.charAt(25) == '_' &&
               password.charAt(17) == '4' &&
               password.charAt(29) == 'c' &&
               password.charAt(0)  == 'd' &&
               password.charAt(1)  == '3' &&
               password.charAt(22) == '3' &&
               password.charAt(9)  == '3' &&
               password.charAt(20) == 'c' &&
               password.charAt(5)  == '4' &&
               password.charAt(15) == 'c' &&
               password.charAt(30) == '8' &&
               password.charAt(26) == 'c' &&
               password.charAt(13) == '3' &&
               password.charAt(4)  == 'r' &&
               password.charAt(28) == 'c' &&
               password.charAt(6)  == 'm' &&
               password.charAt(8)  == 'l' &&
               password.charAt(23) == 'r' &&
               password.charAt(12) == 'H' &&
               password.charAt(16) == 'H' &&
               password.charAt(21) == 'T' &&
               password.charAt(19) == '4';
```

Pythonでどんどん置換していってこのような感じで出てきた。

```
10'_'
11't'
18'r'
31'9'
14'_'
3'c'
24'5'
2'5'
27'3'
7'b'
25'_'
17'4'
29'c'
0'd'
1'3'
22'3'
9'3'
20'c'
5'4'
15'c'
30'8'
26'c'
13'3'
4'r'
28'c'
6'm'
8'l'
23'r'
12'H'
16'H'
21'T'
19'4'
```


こんな文字列が出てきた。`d35cr4mbl3_tH3_cH4r4cT3r5_c3cc89`

`CognitiveCTF{d35cr4mbl3_tH3_cH4r4cT3r5_c3cc89}`これを確認する。

## rsa-pop-quiz（2022年9月12日）未解決

### 問題

> クラスの皆さん、席についてください！小テストの時間です... `nc shell1.production.cognitivectf.com 26616`

### アプローチ

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


## Tapping（2022年9月12日）

### 問題

> 信号線から入ってくる何かを盗聴しました。何と言っていますか？ `nc shell1.production.cognitivectf.com 48474`

### アプローチ

そのまま実行したら、出てきた。

```
AyatoShitomi@picoCTF_production_shell_001:~$ nc shell1.production.cognitivectf.com 48474
-.-. --- --. -. .. - .. ...- . -.-. - ..-. { -- ----- .-. ... ...-- -.-. ----- -.. ...-- .---- ... ..-. ..- -. ...-- ---.. .---- ..-. -.-. ..-. .---- ----- }
^C
```

フラグのフォーマットだとわかった。モールス信号だとわかった。

```bash
AyatoShitomi@picoCTF_production_shell_001:~$ nc shell1.production.cognitivectf.com 48474 > morusu
^C
AyatoShitomi@picoCTF_production_shell_001:~$ cat morusu 
-.-. --- --. -. .. - .. ...- . -.-. - ..-. { -- ----- .-. ... ...-- -.-. ----- -.. ...-- .---- ... ..-. ..- -. ...-- ---.. .---- ..-. -.-. ..-. .---- ----- }
```

https://morsedecoder.com/ ここで変換できる。

`COGNITIVECTF#M0RS3C0D31SFUN381FCF10#`が出てきたので、`COGNITIVECTF{M0RS3C0D31SFUN381FCF10}`でOK

## plumbing（2022年9月12日）

### 問題

> ファイルの外で処理データを扱わなければならないときもあります。プログラムの出力を保持したまま、フラグを検索する方法を見つけてください。`shell1.production.cognitivectf.com 48438`に接続してください。

### アプローチ

ヒントを読んだ。

> フラグのフォーマットはCognitiveCTF{XXXX}であることを覚えておいてください。
パイプとは何ですか？そのようなパイプではありません...この種類の

ncで接続する。

```shell
AyatoShitomi@picoCTF_production_shell_001:~$ nc shell1.production.cognitivectf.com 48438 | grep CTF
CognitiveCTF{digital_plumb3r_a0a0c498}
```
出てきたので確認したらOK。

## dont-use-client-side（2022年9月12日）

### 問題

> この超セキュアなポータルに侵入できますか？
https://shell1.production.cognitivectf.com/problem/30590/ (link) or http://shell1.production.cognitivectf.com:30590

### アプローチ

ソースを見たらこんなんだった。

```js
  function verify() {
    checkpass = document.getElementById("pass").value;
    split = 4;
    if (checkpass.substring(0, split) == 'Cogn') {
      if (checkpass.substring(split*6, split*7) == 'plz_') {
        if (checkpass.substring(split*1, split*2) == 'itiv') {
          if (checkpass.substring(split*4, split*5) == 'clie') {
            if (checkpass.substring(split*8, split*9) == 'c9b}') {
              if (checkpass.substring(split*3, split*4) == '{no_') {
                if (checkpass.substring(split*5, split*6) == 'nts_') {
                  if (checkpass.substring(split*2, split*3) == 'eCTF') {
                    if (checkpass.substring(split*7, split*8) == '9b5b') {
                      alert("Password Verified");
                    }
                  }
                }
              }
            }
          }
        }
      }
    }
    else {
      alert("Incorrect password");
    }
    
  }
```

|Num|Pass|
|---|---|
|0, 4|'Cogn'|
|24, 28|'plz_'|
|4, 8|'itiv'|
|16, 20|'clie'|
|32, 36|'c9b}'|
|12, 16|'{no_'|
|20, 24|'nts_'|
|8, 12|'eCTF'|
|28 32|'9b5b'|

これを並べ替えると`CognitiveCTF{no_clients_plz_9b5bc9b}`となる。

パスワードの欄に入れるとOKだった。検証してOK！

## logon（2022年9月11日）

### 問題

> 工場は、工場の利用者全員に隠し事をしています。
管理者(admin)としてログインし、何を隠しているのか見つけ出してください。
https://shell1.production.cognitivectf.com/problem/48492/ (link) or http://shell1.production.cognitivectf.com:48492

### アプローチ

ディレクトリトラバーサルをやってもダメ
ソースファイルを見てもそれらしきフラグはなかった。

Adminとしてログインってなってたから、Cookieを見てみたら、`admin`という鍵が`False`だったので、`True`にしてリロードしたら出た。

`CognitiveCTF{th3_c0nsp1r4cy_l1v3s_d7232a74}`


## whats-the-difference（2022年9月11日）未解決

### 問題

> 2つの画像の違いを見つけられますか？。
このファイルはshell1.production.cognitivectf.comの以下ディレクトリに置かれています。
`/problems/whats-the-difference_0_5101ecff12a8735483234efc43ebe1f2`

### アプローチ

わからなかったから放置


## So Meta（2022年9月11日）

### 問題

> この画像からフラグを探し出してください。
このファイルはshell1.production.cognitivectf.comの以下ディレクトリにも置かれています。
/problems/so-meta_2_1fdd96839249b508f04d47ff5b4d0e6b

### アプローチ

問題名からMetaタグの中にフラグがあると思う。

```shell
AyatoShitomi@picoCTF_production_shell_001:/problems/so-meta_2_1fdd96839249b508f04d47ff5b4d0e6b$ ls
pico_img.png
AyatoShitomi@picoCTF_production_shell_001:/problems/so-meta_2_1fdd96839249b508f04d47ff5b4d0e6b$ strings pico_img.png  | grep CTF
CognitiveCTF{s0_m3ta_846c1cfa}
```

`CognitiveCTF{s0_m3ta_846c1cfa}`を検証する


## Bases（2022年9月11日）

### 問題

> `bDNhcm5fdGgzX3IwcDM1X2U5YjlkMTgw`は何を意味しますか？これには基数(base)が関係していそうです。

### アプローチ

大体Base64でデコードしたら何とかなりそうと思った。

`base64`コマンドと言うものがある。

```shell
AyatoShitomi@picoCTF_production_shell_001:~$ echo "bDNhcm5fdGgzX3IwcDM1X2U5YjlkMTgw" > t && base64 -d t && echo
l3arn_th3_r0p35_e9b9d180
AyatoShitomi@picoCTF_production_shell_001:~$ 
```

`CignitiveCTF{l3arn_th3_r0p35_e9b9d180}`でOK

## what's a net cat?（2022年9月11日）

### 問題

> netcat (nc) を使うことはかなり重要になってきます。
shell1.production.cognitivectf.comのポート番号15580に接続してフラグを獲得できますか？

### アプローチ

ncコマンドについて調べる

```shell
AyatoShitomi@picoCTF_production_shell_001:~$ nc
usage: nc [-46CDdFhklNnrStUuvZz] [-I length] [-i interval] [-M ttl]
          [-m minttl] [-O length] [-P proxy_username] [-p source_port]
          [-q seconds] [-s source] [-T keyword] [-V rtable] [-W recvlimit] [-w timeout]
          [-X proxy_protocol] [-x proxy_address[:port]]           [destination] [port]
AyatoShitomi@picoCTF_production_shell_001:~$ 
```

`nc shell1.production.cognitivectf.com:15580`でいけるのかな。と思ったら違った。

```shell
AyatoShitomi@picoCTF_production_shell_001:~$ nc shell1.production.cognitivectf.com 15580
You're on your way to becoming the net cat master
CognitiveCTF{nEtCat_Mast3ry_09ed53fe}
```

`CognitiveCTF{nEtCat_Mast3ry_09ed53fe}`を検証してOK

## strings it（2022年9月11日）

### 問題
> 実行せずにこのファイルにあるフラグを見つけることができますか？
このファイルはshell1.production.cognitivectf.comの以下ディレクトリにも置かれています。
/problems/strings-it_0_6574bcb359a79eaef28d07f8b6af2877

### アプローチ
ディレクトリ移動

```
AyatoShitomi@picoCTF_production_shell_001:~$ cd /problems/strings-it_0_6574bcb359a79eaef28d07f8b6af2877
AyatoShitomi@picoCTF_production_shell_001:/problems/strings-it_0_6574bcb359a79eaef28d07f8b6af2877$ ls
strings
```
Stringsコマンドでみたら、長すぎたのでさらにGrepする。

```
AyatoShitomi@picoCTF_production_shell_001:/problems/strings-it_0_6574bcb359a79eaef28d07f8b6af2877$ strings strings  | grep "{"
CognitiveCTF{5tRIng5_1T_e22f4874}
```

検証してOK。

## First Grep（2022年9月11日）

### 問題
> ファイルの中にあるフラグを見つけられますか？手動で調べるのは本当に面倒ですが、どうやらもっと良い方法があるみたいです。このファイルはシェルサーバーの /problems/first-grep_3_76db5c9e677a5a741754b6b4c9b0526a にもあります

### アプローチ

問題名からしてGrepを使えば早い。

```
AyatoShitomi@picoCTF_production_shell_001:/problems/first-grep_3_76db5c9e677a5a741754b6b4c9b0526a$ grep "{" file 
CognitiveCTF{grep_is_good_to_find_things_83b1c474}
```
検証してみる。OKだった。

## Insp3ct0r（2022年9月11日）

### 問題

> Kishor Balanは、次のコードは検証が必要になるかもしれないとこっそり教えてくれました。: https://shell1.production.cognitivectf.com/problem/15589/ (link) or http://shell1.production.cognitivectf.com:15589

### アプローチ

サイト開く。
Devツールのコンソールには何も表示されてなかった。

`index.html`の中にこれがあった。

```html
</p>
	<!-- Html is neat. Anyways have 1/3 of the flag: CognitiveCTF{tru3 -->
      </div>
```

Howのところにこのように書いてあった。これがヒントだったと気が付く。

> I used these to make this site:
HTML
CSS
JS (JavaScript)

同じく`myjs.js`を見てみたら、またフラグがあった。

```js
/* Javascript sure is neat. Anyways part 3/3 of the flag: t_lucky?b009d771} */
```

最後に`myscc.css`を見た。

```css
/* You need CSS to make pretty pages. Here's part 2/3 of the flag: _d3t3ct1ve_0r_ju5 */
```

これで3つ集まった。

`CognitiveCTF{tru3_d3t3ct1ve_0r_ju5t_lucky?b009d771}`でフラグを検証する。

## Glory of the Garden（2022年9月11日）

### 問題

> この庭園には見た目以上のものが含まれています。
このファイルはshell1.production.cognitivectf.comの以下ディレクトリにも置かれています。
/problems/glory-of-the-garden_0_a0f972e9b4d12e22fba5d6d1fedeb045

### アプローチ

```shell
AyatoShitomi@picoCTF_production_shell_001:~$ cd /problems/glory-of-the-garden_0_a0f972e9b4d12e22fba5d6d1fedeb045
AyatoShitomi@picoCTF_production_shell_001:/problems/glory-of-the-garden_0_a0f972e9b4d12e22fba5d6d1fedeb045$ ls
garden.jpg
AyatoShitomi@picoCTF_production_shell_001:/problems/glory-of-the-garden_0_a0f972e9b4d12e22fba5d6d1fedeb045$ 
```

JPEGの写真があった。
なんだろうと思って、ファイルをダウンロードする。
普通の写真だったから、ファイルの中に何か入っていると思った。

```
AyatoShitomi@picoCTF_production_shell_001:/problems/glory-of-the-garden_0_a0f972e9b4d12e22fba5d6d1fedeb045$ strings garden.jpg

...

mjx/
s\]|."Ue
\qZf
Here is a flag "CognitiveCTF{more_than_m33ts_the_3y3_392ff9d1}"
```

Stringsコマンドでフラグでてきた。
回答したら正解だった。

## The Numbers（2022年9月11日）

### 問題
> 数字は...何の意味があるの？

### アプローチ

数字のリンクをクリックするとPNGファイルがダウンロードされた。

内容は`3 15 7 14 9 20 9 22 5 3 20 6 {20 8 5 14 21 13 2 5 18 19 13 1 19 15 14 3 15 4}`だった。

`{}`があるからフラグだとすぐわかる。
またこの問題のフラグ形式が`CognitiveCTG{FLAG}`なので、`3 ... 3 ... {...}`のCで一致している。

`3 15 7 14 9 20 9 22 5 3 20 6 {20 8 5 14 21 13 2 5 18 19 13 1 19 15 14 3 15 4}`

`3`が`C`ならば、`1`が`A`である。

簡単なプログラムを作る。

```python
import sys

av = sys.argv[1]
print(av)
obj = av.split(" ")
tmp = []

for i in obj:
    n = int(i.replace("{","").replace("}",""))
    n += 64
    print(n, chr(n))
    tmp.append(chr(n))

for w in tmp:
    print(w, end="")
print()
```

これの出力が`COGNITIVECTFTHENUMBERSMASONCOD`になった。`{}`を補って比較するとこんな感じ。
> `COGNITIVECTF{THENUMBERSMASONCOD}`<br>
> `CognitiveCTG{FLAG}`<br>

ちょっとフォーマット違うけど、入力したらあってた。

## practice-run-1（2022年9月11日）

### 問題
> ここから先へ進むには、プログラムをどうやって動かすかを知っておく必要があります。フラグを得るには、Shellサーバー上で/problems/practice-run-1_0_e898984dec5059fd94fd863587109ed6へ移動し、このプログラムを実行してください。

### アプローチ

まずは「このプログラム」をダウンロードする。
`run_this`というファイル名だとわかって、ディレクトリを移動して同じファイル名を発見したので実行。

```shell
AyatoShitomi@picoCTF_production_shell_001:~$ curl -OL https://shell1.production.cognitivectf.com/static/0d6d958d91c106e52d5bbe2f0e835b06/run_this
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  646k  100  646k    0     0  3893k      0 --:--:-- --:--:-- --:--:-- 3893k
AyatoShitomi@picoCTF_production_shell_001:~$ ls
run_this
AyatoShitomi@picoCTF_production_shell_001:~$ cd /problems/practice-run-1_0_e898984dec5059fd94fd863587109ed6
AyatoShitomi@picoCTF_production_shell_001:/problems/practice-run-1_0_e898984dec5059fd94fd863587109ed6$ ls
run_this
AyatoShitomi@picoCTF_production_shell_001:/problems/practice-run-1_0_e898984dec5059fd94fd863587109ed6$ ./run_this 
CognitiveCTF{g3t_r3adY_2_r3v3r53!!!!}
AyatoShitomi@picoCTF_production_shell_001:/problems/practice-run-1_0_e898984dec5059fd94fd863587109ed6$ 
```

`ognitiveCTF{g3t_r3adY_2_r3v3r53!!!!}`であってたのでOK

## 13（2022年9月11日）

### 問題
> 暗号は時として簡単に解けることもあります。ROT13をご存知ですか？`PbtavgvirPGS{abg_gbb_onq_bs_n_ceboyrz_7qsn03oq}`

### アプローチ

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

分かった。

```shell
AyatoShitomi@picoCTF_production_shell_001:~$ cd /problems/handy-shellcode_3_eefb645e8107c9aa00c62fb91b755de8
AyatoShitomi@picoCTF_production_shell_001:/problems/handy-shellcode_3_eefb645e8107c9aa00c62fb91b755de8$ ls
flag.txt  vuln  vuln.c
```

ここに格納されていた。この`flag.txt`を読めばいい。

ここでまた手が詰まった。


## 2Warm（2022年9月11日）

### 問題の概要
> 121(10進法)を2進数に変換する

### アプローチ１

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

### アプローチ２

進数変換は上から順に変換する数で割っていけばいい。

> 121/2 = 60 ... 1
60/2 = 30 ... 0
30/2 = 15 ... 0
15/2 = 7 ... 1
7/2 = 3 ... 1
3/2 = 1 ... 1
1/2 = 0 ... 1

よって`1111001`がフラグの中身

