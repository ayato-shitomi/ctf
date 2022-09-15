# where are the robots

## 問題

> ロボット達を見つけられますか？https://shell1.production.cognitivectf.com/problem/30562/ (link) or http://shell1.production.cognitivectf.com:30562

## アプローチ

ソースファイルにそれらしきものはなかった。

ロボットだからクローラーかなと思った

`/sitemap.xml`は何もなかったが、`/robots.txt`には何か出てきた。
このような表示になったので、アクセスしてみる。
> User-agent: * Disallow: /72f2710a.html

以下のようなフラグがでてきた。

`CognitiveCTF{ca1cu1at1ng_Mach1n3s_2f6633aa}`

検証してOK
