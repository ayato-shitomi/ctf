# Lv1

## [Forensics] River



## [Web] HTML Page

```shell
ayato@ubuntuVM ~/D/CTF ❯
 🐟 $ curl http://q9.ctf.cpaw.site/ > page.html && cat page.html | grep ctf
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  7344  100  7344    0     0  76271      0 --:--:-- --:--:-- --:--:-- 76500
    <meta name="keyword" content="ctf,flag">
          <p>実際にCTFに出場して、様々な問題に触れることが大事である。CTFは、ほぼ毎週世界中のどこかで行われている。<a href="https://ctftime.org/">ctftime</a>というサイトに行くと、世界で行われているCTFの日程を知ることが出来る。日本では他には常に動いているものだと<a href="http://ksnctf.sweetduet.info/">ksnctf</a>や<a href="http://ctf.katsudon.org/">akictf</a>などがあり、一定期間中に行われるものだと、日本で最も大規模な<a href="http://2015.seccon.jp/">SECCON CTF</a>、運営が学生主体の<a href="http://lepus-ctf.org/">LepusCTF</a>や<a href="http://score.mmactf.link/?locale=ja">MMA CTF</a>などがある。</p>
```

`meta`タグの中にコンテントのFlagがあったので、それを見るとある。

## [Misc] Can you open this file ? 

```shell
ayato@ubuntuVM ~/D/CTF ❯
 🐟 $ file  open_me
open_me: Composite Document File V2 Document, Little Endian, Os: Windows, Version 10.0, Code page: 932, Author: �v��, Template: Normal.dotm, Last Saved By: �v��, Revision Number: 1, Name of Creating Application: Microsoft Office Word, Total Editing Time: 28:00, Create Time/Date: Mon Oct 12 04:27:00 2015, Last Saved Time/Date: Mon Oct 12 04:55:00 2015, Number of Pages: 1, Number of Words: 3, Number of Characters: 23, Security: 0
```

`.doc`に変換すれば開ける。

（Wordがないため）Web上でPDFに変換した。

`cpaw{Th1s_f1le_c0uld_be_0p3n3d}`

## [Reversing] Can you execute ?

```shell
yato@ubuntuVM ~/Downloads ❯
 🐟 $ file exec_me 
exec_me: ELF 64-bit LSB executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, for GNU/Linux 2.6.24, BuildID[sha1]=663a3e0e5a079fddd0de92474688cd6812d3b550, not stripped
ayato@ubuntuVM ~/Downloads ❯
 🐟 $ chmod 777 exec_me 
ayato@ubuntuVM ~/Downloads ❯
 🐟 $ ./exec_me 
cpaw{Do_you_know_ELF_file?}
```

## [Crypto] Classical Cipher	

https://dencode.com/ja/cipher/caesar

## [Misc] Test Problem

そのまま入力
