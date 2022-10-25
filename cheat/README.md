# 無操作でセッションが落ちないようにする。

```
while :
do
        sleep 60
        date
done
```

ワンライナーだとこんな感じ。

`while : ;do sleep 1 | date ; done`


# XSS

`script`という文字列が消される場合は`javascrscriptipt`のような文字列を送ればよい。
結果的に`javascript`とかが生成される。

