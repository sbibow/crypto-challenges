# Detect single-character XOR

## The challenge

One of the 60-character strings in this file has been encrypted by single-character XOR.

Find it.

(Your code from #3 should help.)

## The solution

NodeJS:

```javascript
// from set-1-challenge-3
const rankText = text => {
  const letterFrequenciesEnglish={'a': 0.0651738,'b': 0.0124248,'c': 0.0217339,'d': 0.0349835,'e': 0.1041442,'f': 0.0197881,'g': 0.0158610,'h': 0.0492888,'i': 0.0558094,'j': 0.0009033,'k': 0.0050529,'l': 0.0331490,'m': 0.0202124,'n': 0.0564513,'o': 0.0596302,'p': 0.0137645,'q': 0.0008606,'r': 0.0497563,'s': 0.0515760,'t': 0.0729357,'u': 0.0225134,'v': 0.0082903,'w': 0.0171272,'x': 0.0013692,'y': 0.0145984,'z': 0.0007836,' ': 0.1918182}
  const chars = text
    .split("")
    .map(char => char.toLowerCase())

  let score = 0;
  for (let letter of chars) {
    score += letterFrequenciesEnglish[letter] || -1
  }
  return score
}

const generateDecodedText = (input, key) => Buffer.from(input, "hex").map(e => e^key).toString()

// this challenges code starts here
const fs = require('fs')
const data = fs.readFileSync('set-1-challenge-4-file.txt', 'utf8').split("\n")
let bestResults = []
for(let row of data) {
  let results = []
  for (let i = 0; i < 255; i++) {
    let decodedText = generateDecodedText(row, i.toString(16))
    results.push([decodedText,rankText(decodedText)])
  }
  bestResults.push(results.sort((a,b) => b[1] - a[1])[0])
}
console.log(bestResults.sort((a,b) => b[1] - a[1])[0])
```