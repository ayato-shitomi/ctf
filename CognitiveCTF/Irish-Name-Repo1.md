# Irish-Name-Repo 1（2022年9月24日）

## 問題

> 次のウェブサイトが稼働しています。
https://shell1.production.cognitivectf.com/problem/30596/ (link) or http://shell1.production.cognitivectf.com:30596
ログインできると思いますか？ログインできるか試してみてください！

## アプローチ

自分のログインパスでログインしたけど無理だった。

適当にやったら、PHPが走ってたのでSQLインジェクションと推測

`admin';--`を入れて完了！
