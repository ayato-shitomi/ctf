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


