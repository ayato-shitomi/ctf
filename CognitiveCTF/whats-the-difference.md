# whats-the-difference（2022年9月24日）

## 問題
> 2つの画像の違いを見つけられますか？。 このファイルはshell1.production.cognitivectf.comの以下ディレクトリに置かれています。 /problems/whats-the-difference_0_5101ecff12a8735483234efc43ebe1f2

## アプローチ

わからなかったから放置

バイナリとしての差分を表示するときは`cmp`コマンドを利用する。

`cmp -bl kitters.jpg cattos.jpg | less`

これで縦に並んだ文字列を見ていけばいい。
ＡＷＫとかで取り出せば良き。


```
> cmp -bl kitters.jpg cattos.jpg | awk '{print $5}' | tr -d "\n" && echo "\n"
CognitiveCTF{th3yr3_a5_d1ff3r3nt_4s_bu773r_4nd_j311y_79ab38c0be35a8654db1b3f1efc8c584}
```
