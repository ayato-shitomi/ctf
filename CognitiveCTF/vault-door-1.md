# vault-door-1（2022年9月12日）

## 問題

> この金庫は複雑な配列を使っている！君が解明してくれることを願っているよ、特別捜査官。
金庫のソースコードはここだ: `VaultDoor1.java`

## アプローチ

Curlでとってくる。

```java
import java.util.*;

class VaultDoor1 {
    public static void main(String args[]) {
        VaultDoor1 vaultDoor = new VaultDoor1();
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter vault password: ");
        String userInput = scanner.next();
        String input = userInput.substring("CognitiveCTF{".length(),userInput.length()-1);
        if (vaultDoor.checkPassword(input)) {
            System.out.println("Access granted.");
        } else {
            System.out.println("Access denied!");
        }
    }

    // I came up with a more secure way to check the password without putting
    // the password itself in the source code. I think this is going to be
    // UNHACKABLE!! I hope Dr. Evil agrees...
    //
    // -Minion #8728
    public boolean checkPassword(String password) {
        return password.length() == 32 &&
               password.charAt(10) == '_' &&
               password.charAt(11) == 't' &&
               password.charAt(18) == 'r' &&
               password.charAt(31) == '9' &&
               password.charAt(14) == '_' &&
               password.charAt(3)  == 'c' &&
               password.charAt(24) == '5' &&
               password.charAt(2)  == '5' &&
               password.charAt(27) == '3' &&
               password.charAt(7)  == 'b' &&
               password.charAt(25) == '_' &&
               password.charAt(17) == '4' &&
               password.charAt(29) == 'c' &&
               password.charAt(0)  == 'd' &&
               password.charAt(1)  == '3' &&
               password.charAt(22) == '3' &&
               password.charAt(9)  == '3' &&
               password.charAt(20) == 'c' &&
               password.charAt(5)  == '4' &&
               password.charAt(15) == 'c' &&
               password.charAt(30) == '8' &&
               password.charAt(26) == 'c' &&
               password.charAt(13) == '3' &&
               password.charAt(4)  == 'r' &&
               password.charAt(28) == 'c' &&
               password.charAt(6)  == 'm' &&
               password.charAt(8)  == 'l' &&
               password.charAt(23) == 'r' &&
               password.charAt(12) == 'H' &&
               password.charAt(16) == 'H' &&
               password.charAt(21) == 'T' &&
               password.charAt(19) == '4';
    }
}
```

並べ替えればフラグになると思われる。
`t`というファイルを作った。
```
               password.charAt(10) == '_' &&
               password.charAt(11) == 't' &&
               password.charAt(18) == 'r' &&
               password.charAt(31) == '9' &&
               password.charAt(14) == '_' &&
               password.charAt(3)  == 'c' &&
               password.charAt(24) == '5' &&
               password.charAt(2)  == '5' &&
               password.charAt(27) == '3' &&
               password.charAt(7)  == 'b' &&
               password.charAt(25) == '_' &&
               password.charAt(17) == '4' &&
               password.charAt(29) == 'c' &&
               password.charAt(0)  == 'd' &&
               password.charAt(1)  == '3' &&
               password.charAt(22) == '3' &&
               password.charAt(9)  == '3' &&
               password.charAt(20) == 'c' &&
               password.charAt(5)  == '4' &&
               password.charAt(15) == 'c' &&
               password.charAt(30) == '8' &&
               password.charAt(26) == 'c' &&
               password.charAt(13) == '3' &&
               password.charAt(4)  == 'r' &&
               password.charAt(28) == 'c' &&
               password.charAt(6)  == 'm' &&
               password.charAt(8)  == 'l' &&
               password.charAt(23) == 'r' &&
               password.charAt(12) == 'H' &&
               password.charAt(16) == 'H' &&
               password.charAt(21) == 'T' &&
               password.charAt(19) == '4';
```

Pythonでどんどん置換していってこのような感じで出てきた。

```
10'_'
11't'
18'r'
31'9'
14'_'
3'c'
24'5'
2'5'
27'3'
7'b'
25'_'
17'4'
29'c'
0'd'
1'3'
22'3'
9'3'
20'c'
5'4'
15'c'
30'8'
26'c'
13'3'
4'r'
28'c'
6'm'
8'l'
23'r'
12'H'
16'H'
21'T'
19'4'
```


こんな文字列が出てきた。`d35cr4mbl3_tH3_cH4r4cT3r5_c3cc89`

`CognitiveCTF{d35cr4mbl3_tH3_cH4r4cT3r5_c3cc89}`これを確認する。
