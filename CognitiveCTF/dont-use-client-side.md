
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
