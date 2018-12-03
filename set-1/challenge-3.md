# Single-byte XOR cipher

## The challenge

The hex encoded string:

```
1b37373331363f78151b7f2b783431333d78397828372d363c78373e783a393b3736
```

... has been XOR'd against a single character. Find the key, decrypt the message.

You can do this by hand. But don't: write code to do it for you.

How? Devise some method for "scoring" a piece of English plaintext. Character frequency is a good metric. Evaluate each output and choose the one with the best score.

## The solution

NodeJS:

```javascript
const encodedString = "1b37373331363f78151b7f2b783431333d78397828372d363c78373e783a393b3736"
const rankText = text => {
  const letterFrequenciesEnglish={a: 0.08167,b: 0.01492,c: 0.02782,d: 0.04253,e: 0.12702,f: 0.02228,g: 0.02015,h: 0.06094,i: 0.06966,j: 0.00153,k: 0.00772,l: 0.04025,m: 0.02406,n: 0.06749,o: 0.07507,p: 0.01929,q: 0.00095,r: 0.05987,s: 0.06327,t: 0.09056,u: 0.02758,v: 0.00978,w: 0.02360,x: 0.00150,y: 0.01974,z: 0.00074}
  const letterOccurrencesText = text
    .split("")
    .map(char => char.toLowerCase())
    .reduce((acc, curr) => {
      acc[curr] ? acc[curr]++ : acc[curr] = 1;
      return acc;
    }, {});

  let score = 0;
  for (let letter in letterFrequenciesEnglish) {
    score += letterFrequenciesEnglish[letter] - (letterOccurrencesText[letter]/text.length || 1)
  }
  return score
}

const generateDecodedText = (input, key) => Buffer.from(input, "hex").map(e => e^key).toString()

let results = []
for (let i = 0; i < 255; i++) {
  let decodedText = generateDecodedText(encodedString, i.toString(16))
  results.push([decodedText,rankText(decodedText)])
}
console.log(results.sort((a,b) => b[1] - a[1])[0][0])
```
