# SECCON BEGINNERS 2022 SAPPORO

## MEMO

11月に予選があるらしい。

## 講義

CTFって色んな分野がある。

> - web
> - crypto
> - reversing
> - pwnable
> - misc

CTFの問題を特前に知識をつけることが大切。

**CTFTimeというサイトでCTFの開催を知ることができる。**

## web講義

[web用スライド](./src/web.pdf)

問題の解き方

> - 調査（脆弱性診断、コードをみる）
> - 仮説
> - 検証（実際に攻撃をしてみる）

Web問題は最初にHTMLを見るべき。
変数名や関数名がわかりやすく作られる。

### 演習問題

4つのフラグを見つける。

#### `ctf4b{flag_1n_a_re5pon5e_he4der}`

レスポンスヘッダーの中にあった。F12で確認すればよき。

#### `flag="ctf4b{f14g_1n_a_C00k1e}"`

Cookieの中に入っていた。

#### `ctf4b{th15_1s_a_fl4g!}`

htmlのコメント欄にあった。
`curl URL > xxx.html && cat xxx.html | grep "ctf"`

#### `ctf4b{c4n_y0u_see_me?}`

flagのあるページがリダイレクトされているからcurlで見ればいい。
`curl URL/flag > xxxx.html && cat xxxx.html | grep "ctf"`

### XXS

被害者の環境でスクリプトを実行する という認識。

- ユーザーの入力がアプリケーションに取り込まれる場所を探す。
- 文字列をスクリプトとして解釈させるか

動的に生成される場所にスクリプトを注入する。

```html
<h1></h1>
```

ここにスクリプトを入れるのは簡単だね。

```html
<h1><script>...</script></h1>
```

ここに挿入するには、`"><script>...</script><"`を入れてやる。

```html
<a herf=""></a>
```

以下。

```html
<a href=""><script>...</script></a>
```

### SQLi

SQLとは横がレコード、縦がカラム、セルがフィールドのようなイメージ。

**Payloads All The Things**というのがいろいろなペイロードを配布している。

**Port SwiggerのAll Learning Materials**というサイトで手を動かしながら学べる。

#### 演習問題

> `SELECT name FROM users WHERE name='入力' AND pass='入力';`このような叩き方をするアプリがあります。
どのような入力ををすれば`id`が`1`の`admin`にログインできますか。

解答：`hogehogehack' OR id=1;`

以下のようなSQL文が実行される。
`SELECT name FROM users WHERE name='hogehogehack' OR id=1; --AND pass='入力';`

## Reversing講義

[講義資料はこちら](./src/Reversing講義資料-Sapporo2022.pdf)

GCCでコンパイルされるファイルを`ELFファイル`というんだって。

ファイル解析は3つの方法がある。

- 表層解析　`strings`などでファイル中の文字列から解析をする
- 静的解析　Ghidraなどでアセンブリを読む
- 動的解析　BDGなどで動かしながら学ぶ

CTFを解くとき、`file`コマンドと`strings`コマンドを実行するといい。

### 静的解析演習

`rev/seiteki_kaiseki`を利用する。

```shell
> cd rev
> chmod 777 seiteki_kaiseki

> strings seiteki_kaiseki
/lib64/ld-linux-x86-64.so.2
^:0^
mgUa
libc.so.6
puts
__stack_chk_fail
stdin
fgets
strlen
__cxa_finalize
strcmp
__libc_start_main
GLIBC_2.4
GLIBC_2.2.5
_ITM_deregisterTMCloneTable
__gmon_start__
_ITM_registerTMCloneTable
u+UH
<1u4H
<2u%H
[]A\A]A^A_
ctf4b{we1cme_4o_rev4r3ing_2o22}
Please input password:
Please input PIN:
Correct!!!
Incorrect Bye...
:*3$"
GCC: (Ubuntu 9.4.0-1ubuntu1~20.04.1) 9.4.0
crtstuff.c
deregister_tm_clones
__do_global_dtors_aux
completed.8061
__do_global_dtors_aux_fini_array_entry
frame_dummy
__frame_dummy_init_array_entry
src.c
__FRAME_END__
__init_array_end
_DYNAaMIC
__init_array_start
__GNU_EH_FRAME_HDR
_GLOBAL_OFFSET_TABLE_
__libc_csu_fini
_ITM_deregisterTMCloneTable
puts@@GLIBC_2.2.5
stdin@@GLIBC_2.2.5
_edata
strlen@@GLIBC_2.2.5
__stack_chk_fail@@GLIBC_2.4
__libc_start_main@@GLIBC_2.2.5
fgets@@GLIBC_2.2.5
__data_start
strcmp@@GLIBC_2.2.5
__gmon_start__
__dso_handle
_IO_stdin_used
__libc_csu_init
__bss_start
main
check_pin
__TMC_END__
_ITM_registerTMCloneTable
__cxa_finalize@@GLIBC_2.2.5
PASSWORD
.symtab
.strtab
.shstrtab
.interp
.note.gnu.property
.note.gnu.build-id
.note.ABI-tag
.gnu.hash
.dynsym
.dynstr
.gnu.version
.gnu.version_r
.rela.dyn
.rela.plt
.init
.plt.got
.plt.sec
.text
.fini
.rodata
.eh_frame_hdr
.eh_frame
.init_array
.fini_array
.dynamic
.data
.bss
.comment
```

passwordを`ctf4b{we1cme_4o_rev4r3ing_2o22}`で検証するとあってた！

### Ghidra

オペランド＝引数

あとはPINがわかる必要がある。

main関数から、`check_pin`のような関数に飛んだら`1230`かどうかをチェックして戻り値をセットするものがあったから、PINにはそれを入れればいいね。

アセンブリを見るときには、`CALL`の直前にどのようなオペランドを呼び出しているかを見るべきですね。

### 動的解析演習

`rev/douteki_kaiseki`

関数の戻り値を変えてやると幸せ。

`start`でmain関数まで動く。
その際関数の戻り値`cmp eax,0x2022`をする。
この前に一旦関数を止める。
`set eax 0`等で2020とeaxの比較した際にDIFFが出るようにしてやれば、クリアできるね！
