
## Description

Move the first letter of each word to the end of it, then add "ay" to the end of the word. Leave punctuation marks untouched.

### Examples
```js
pigIt('Pig latin is cool'); // igPay atinlay siay oolcay
pigIt('Hello world !');     // elloHay orldWay !
```

**Kata's link**: [Simple Pig Latin](https://www.codewars.com/kata/simple-pig-latin)

## Best Practices

**First:**
```js
function pigIt(str){
  return str.replace(/(\w)(\w*)(\s|$)/g, "\$2\$1ay\$3")
}
```

**Second:**
```js
pigIt = s => s.split(' ').map(e => e.substr(1) + e[0] + 'ay').join(' ');
```

## My solutions
```js
function pigIt(str){
  //Code here
  str = str.trim().split(/\s{1,}/);
    return str.map(val => {
        if (/^[A-Za-z]+$/.test(val)) {
            return `${val.slice(1)}${val.slice(0, 1)}ay`;
        }
        return val;
    }).join(' ');
}
```
