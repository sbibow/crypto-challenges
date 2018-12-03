# Convert hex to base64

## The challenge

The string: 

```
49276d206b696c6c696e6720796f757220627261696e206c696b65206120706f69736f6e6f7573206d757368726f6f6d
```

Should produce: 
```
SSdtIGtpbGxpbmcgeW91ciBicmFpbiBsaWtlIGEgcG9pc29ub3VzIG11c2hyb29t
```

So go ahead and make that happen. You'll need to use this code for the rest of the exercises.

## The solution

In NodeJs enviroments we can use the built-in class `Buffer` to convert the hex string to an Buffer array, that can be formatted as Base 64:

```javascript
const hexString = "49276d206b696c6c696e6720796f757220627261696e206c696b65206120706f69736f6e6f7573206d757368726f6f6d"
const base64String = Buffer.from(hexString, 'hex').toString('base64')
console.log(base64String)
```

If it should run in a browser you need the following code:

```javascript
const hexString = "49276d206b696c6c696e6720796f757220627261696e206c696b65206120706f69736f6e6f7573206d757368726f6f6d"
const hexBytesArray = hexString.match(/.{2}/g)
const base64StringArray = hexBytesArray.map(word => String.fromCharCode(parseInt(word, 16)))
const base64String = btoa(base64StringArray.join(""))
console.log(base64String)
```