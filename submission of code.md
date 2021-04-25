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

## Ascii - 20 pts
編碼與解碼是資訊領域日常都在使用的技術，如Ascii、Base64、Base32各有其適用處。
ASCII(American Standard Code for Information Interchange)美國資訊交換標準代碼是基於拉丁字母的一套電腦編碼系統，它是現今最通用的單字元編碼系統。

請問你對Ascii編碼與解碼的技術了解嗎?
你知道如何解碼下列資料嗎:
```
66 114 101 97 107 65 76 76 67 84 70 123 65 109 118 48 117 68 121 101 114 118 80 116 109 86 114 57 83 83 83 75 125
```
看看維基百科的說明,來自我學習一下:
https://zh.wikipedia.org/wiki/ASCII

善用網路線上資源
試著用Google查察 ascii decoder

solution
```
number = '66 114 101 97 107 65 76 76 67 84 70 123 65 109 118 48 117 68 121 101 114 118 80 116 109 86 114 57 83 83 83 75 125 '
numbers = list(map(int, number.split()))
for i in numbers:
	print(chr(i), end='')
print("")
```
output
```
BreakALLCTF{Amv0uDyervPtmVr9SSSK}
```

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

## 3rd - 50 pts
可以幫我找出第三大的數字嗎?
```
nc 120.114.62.214 2400
```
solution by bubble sort
```
from pwn import *

ip = "120.114.62.214"
port = 2400

r = remote(ip, port)

r.recvuntil("Now You Turn")
r.recvuntil(" : ")
res = r.recvline()[:-1]  #recvline includes '\n'. Thus, by using [:-1] than '\n' will be excluded
#print(res)

#res="2 654 5 656 544"
numbers = list(map(int, res.split()))
print (numbers)
length = len(numbers)
sort = [int(numbers[0]), int(numbers[1]), int(numbers[2]), int(numbers[3])]
#sort = [0, 1, 2, 3]
for i in range(3, length):
	if sort[3] > int(numbers[i]):
		continue
	sort[3] = int(numbers[i])
	for x in range(0, 4):
		for y in range(0, 4-x-1):
			if sort[y] < sort[y+1]:
				sort[y], sort[y+1] = sort[y+1], sort[y]
				#print("sort[%d] is %d and sort[%d] is %d" % (y, sort[y], y+1, sort[y+1]))
#By bubble sort, the sequence has been sort form the biggest to the smallest
print(sort[2])

r.interactive()
```
flag
```
CTF{yoUaReInth33RdpL4c3}
```
solution by res.sort()
```
from pwn import *

ip = "120.114.62.214"
port = 2400

r = remote(ip, port)

r.recvuntil("Now You Turn")
r.recvuntil(" : ")
res = r.recvline()[:-1] # The input includes '\n', thus we use [:-1] to exclude the last char, i.e. '\n'

#get data
res = list(map(int, res.split()))

res.sort() # sort sequence from smallest to biggest

#return value to server
r.recvuntil("answer :")
r.sendline(str(res[-3]))

#print(res[-3])

r.interactive()
```
flag (same as the former solution)
```
CTF{yoUaReInth33RdpL4c3}
```

## count - 50 pts
你會數⼀到一百嗎?
```
nc 120.114.62.214 2403
```
solution
```
from pwn import*

ip= "120.114.62.214"
port = 2403

r = remote(ip, port)

for i in range(1, 101):
	r.recvuntil("wave")
	r.recvuntil("?")
	r.sendline(str(i))

r.interactive()
```
flag
```
CTF{gOOD4tMatHYOUarE}
```
