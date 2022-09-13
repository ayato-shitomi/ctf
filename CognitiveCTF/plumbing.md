
# plumbing（2022年9月12日）

## 問題

> ファイルの外で処理データを扱わなければならないときもあります。プログラムの出力を保持したまま、フラグを検索する方法を見つけてください。`shell1.production.cognitivectf.com 48438`に接続してください。

## アプローチ

ヒントを読んだ。

> フラグのフォーマットはCognitiveCTF{XXXX}であることを覚えておいてください。
パイプとは何ですか？そのようなパイプではありません...この種類の

ncで接続する。

```shell
AyatoShitomi@picoCTF_production_shell_001:~$ nc shell1.production.cognitivectf.com 48438 | grep CTF
CognitiveCTF{digital_plumb3r_a0a0c498}
```
出てきたので確認したらOK。
