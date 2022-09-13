
# logon（2022年9月11日）

## 問題

> 工場は、工場の利用者全員に隠し事をしています。
管理者(admin)としてログインし、何を隠しているのか見つけ出してください。
https://shell1.production.cognitivectf.com/problem/48492/ (link) or http://shell1.production.cognitivectf.com:48492

## アプローチ

ディレクトリトラバーサルをやってもダメ
ソースファイルを見てもそれらしきフラグはなかった。

Adminとしてログインってなってたから、Cookieを見てみたら、`admin`という鍵が`False`だったので、`True`にしてリロードしたら出た。

`CognitiveCTF{th3_c0nsp1r4cy_l1v3s_d7232a74}`

