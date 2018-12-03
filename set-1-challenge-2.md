# Fixed XOR

## The challenge

Write a function that takes two equal-length buffers and produces their XOR combination.

If your function works properly, then when you feed it the string:

```
1c0111001f010100061a024b53535009181c
```

... after hex decoding, and when XOR'd against:

```
686974207468652062756c6c277320657965
```

... should produce:

```
746865206b696420646f6e277420706c6179
```

## The solution

NodeJS:

```javascript
const aString = "1c0111001f010100061a024b53535009181c"
const bString = "686974207468652062756c6c277320657965"
const aBuffer = Buffer.from(aString, "hex")
const bBuffer = Buffer.from(bString, "hex")

const XORString = aBuffer.map((a,i) => a ^ bBuffer[i]).toString("hex")
console.log(XORString)
```

Browser:

```javascript
const parseHex = string => parseInt(string, 16)

const aString = "1c0111001f010100061a024b53535009181c"
const bString = "686974207468652062756c6c277320657965"
const aBuffer = aString.match(/.{2}/g).map(parseHex)
const bBuffer = bString.match(/.{2}/g).map(parseHex)

const XORString = aBuffer.map((a,i) => (a ^ bBuffer[i]).toString(16)).join("")
console.log(XORString)
```