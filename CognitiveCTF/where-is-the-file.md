# where-is-the-file

## 問題

> このファイルを隠すためにスーパーシークレットなマインド・トリックを使いました。おそらく何かが /problems/where-is-the-file_3_d073fc79221459357fe83fd369cf61ce にあるでしょう。

## アプローチ


```bash
AyatoShitomi@picoCTF_production_shell_001:/problems/where-is-the-file_3_d073fc79221459357fe83fd369cf61ce$ ls -la
total 36
drwxr-xr-x   2 root       root        4096 Jul 29  2021 .
drwxr-x--x 277 root       root       24576 Dec 14  2021 ..
-rw-rw-r--   1 hacksports hacksports    44 Jul 29  2021 .cant_see_me
AyatoShitomi@picoCTF_production_shell_001:/problems/where-is-the-file_3_d073fc79221459357fe83fd369cf61ce$ cat .cant_see_me 
CognitiveCTF{w3ll_that_d1dnt_w0RK_3dd9505d}
AyatoShitomi@picoCTF_production_shell_001:/problems/where-is-the-file_3_d073fc79221459357fe83fd369cf61ce$ 
```

隠しファイルになっていた。

検証してOK
