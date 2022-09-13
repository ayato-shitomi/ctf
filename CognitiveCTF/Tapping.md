
# Tapping（2022年9月12日）

## 問題

> 信号線から入ってくる何かを盗聴しました。何と言っていますか？ `nc shell1.production.cognitivectf.com 48474`

## アプローチ

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
