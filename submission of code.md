# 編碼101
## 第一堂base64編碼 - 20 pts
請問底下字串的base64編碼為何?
```
BreakallCTF{happyhackinghighhaaha}
```

solution
```
import base64
print(base64.b64encode(b"BreakallCTF{happyhackinghighhaaha}"))
```

output
```
b'QnJlYWthbGxDVEZ7aGFwcHloYWNraW5naGlnaGhhYWhhfQ=='
```

其中
```
QnJlYWthbGxDVEZ7aGFwcHloYWNraW5naGlnaGhhYWhhfQ==
```
即為解

## Base64 - 20 pts
編碼與解碼是資訊領域日常都在使用的技術，如Ascii、Base64、Base32各有其適用處，請問你對Base64編碼與解碼的技術了解嗎?

你知道如何解碼下列資料嗎:
```
QnJlYWtBTExDVEZ7NTN1c1pRM2hXVzI1ZGNoWjdkWGV9
```

solution
```
import base64
print(base64.b64decode("QnJlYWtBTExDVEZ7NTN1c1pRM2hXVzI1ZGNoWjdkWGV9"))
```

output
```
b'BreakALLCTF{53usZQ3hWW25dchZ7dXe}'
```

其中
```
BreakALLCTF{53usZQ3hWW25dchZ7dXe}
```
即為解


## Base32 - 20 pts
編碼與解碼是資訊領域日常都在使用的技術，Base32是由使用26個字母A-Z和數字0-9的編碼。

請問你對Base32編碼與解碼的技術了解嗎?

你知道如何解碼下列資料嗎:

```
66 114 101 97 107 65 76 76 67 84 70 123 65 109 118 48 117 68 121 101 114 118 80 116 109 86 114 57 83 83 83 75 125
```

solution
```
import base64
print(base64.b32decode("IJZGKYLLIFGEYQ2UIZ5TS6BUHA2VMUZXO5UWS5CCLJMFKVLIJVSX2==="))
```

output
```
b'BreakALLCTF{9x485VS7wiitBZXUUhMe}'
```

其中
```
BreakALLCTF{9x485VS7wiitBZXUUhMe}
```
即為解

# PPC_Ez
## hello world - 50 pts
你連的到伺服器嗎?
```
nc 120.114.62.214 2405
```
solution
```
from pwn import *

ip = "120.114.62.214"
port = 2405

r = remote(ip, port)

res = r.recv()
print(res)

r.interactive()

```

flag
```
CTF{Hel10WorLD123}
```
