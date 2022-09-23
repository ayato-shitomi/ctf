# asm1（2022年9月24日）

## 問題

> asm1(0xf81)は何を返しますか？16進数表記('0x'で始まる)でフラグを提出してください。
ソースコードはshell1.production.cognitivectf.comの以下ディレクトリに置かれています。
/problems/asm1_0_6b666dbe4c717f5c8eb15110c5d07010

## アプローチ

```shell
> file test.S 
test.S: ASCII text
```

ASCIIコードのただのファイルとわかったから、バイナリ形式を読めばよい。


```shell
> cat test.S 
asm1:
        <+0>:   push   ebp
        <+1>:   mov    ebp,esp
        <+3>:   cmp    DWORD PTR [ebp+0x8],0x557
        <+10>:  jg     0x512 <asm1+37>
        <+12>:  cmp    DWORD PTR [ebp+0x8],0x77a
        <+19>:  jne    0x50a <asm1+29>
        <+21>:  mov    eax,DWORD PTR [ebp+0x8]
        <+24>:  add    eax,0x18
        <+27>:  jmp    0x529 <asm1+60>
        <+29>:  mov    eax,DWORD PTR [ebp+0x8]
        <+32>:  sub    eax,0x18
        <+35>:  jmp    0x529 <asm1+60>
        <+37>:  cmp    DWORD PTR [ebp+0x8],0xcb0
        <+44>:  jne    0x523 <asm1+54>
        <+46>:  mov    eax,DWORD PTR [ebp+0x8]
        <+49>:  sub    eax,0x18
        <+52>:  jmp    0x529 <asm1+60>
        <+54>:  mov    eax,DWORD PTR [ebp+0x8]
        <+57>:  add    eax,0x18
        <+60>:  pop    ebp
        <+61>:  ret    
> 
```

どの条件にも入らずに、これだけが実行されてリターンされる。

```
        <+24>:  add    eax,0x18
```

eax + 0x18 = 0xf81 + 0x18 = 0xf99
