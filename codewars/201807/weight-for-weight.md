
## Description

My friend John and I are members of the "Fat to Fit Club (FFC)". John is worried because each month a list with the weights of members is published and each month he is the last on the list which means he is the heaviest.

I am the one who establishes the list so I told him: "Don't worry any more, I will modify the order of the list". It was decided to attribute a "weight" to numbers. The weight of a number will be from now on the sum of its digits.

For example `99` will have "weight" `18`, `100` will have "weight" `1` so in the list `100` will come before `99`. Given a string with the weights of FFC members in normal order can you give this string ordered by "weights" of these numbers?

### Examples
`"56 65 74 100 99 68 86 180 90"` ordered by numbers weights becomes: `"100 180 90 56 65 74 68 86 99"`

When two numbers have the same "weight", let us class them as if they were strings and not numbers: `100` is before `180` because its "weight" (1) is less than the one of `180` (9) and `180` is before `90` since, having the same "weight" (9) it comes before as a string.

All numbers in the list are positive numbers and the list can be empty.

### Notes
* it may happen that the input string have leading, trailing whitespaces and more than a unique whitespace between two consecutive numbers
* Don't modify the input
* For C: The result is freed.

**Kata's link**: [Valid Parentheses](https://www.codewars.com/kata/weight-for-weight)

## Best Practices

**First:**
```js
function orderWeight(strng) {
  return strng
    .split(" ")
    .map(function(v) {  
      return {
        val: v,
        key: v.split("").reduce(function(prev, curr) {
          return parseInt(prev) + parseInt(curr);
        }, 0)
      };
    })
    .sort(function(a, b) {
      return a.key == b.key 
        ? a.val.localeCompare(b.val)
        : (a.key - b.key);
    })
    .map(function(v) {
      return v.val;
    })
    .join(" ");
}
```

**Second:**
```js
function orderWeight(strng) {
 const sum = (str)=>str.split('').reduce((sum,el)=>(sum+(+el)),0);
  function comp(a,b){
    let sumA = sum(a);
    let sumB = sum(b);
    return sumA === sumB ? a.localeCompare(b) : sumA - sumB;
   };
 return strng.split(' ').sort(comp).join(' ');
}
```

## My solutions
```js
function sumOfWeightDigits (weight) {
    return ('' + weight).split('').reduce((prev, next) => {
        return ~~prev + ~~next;
    }, 0);
}

function compare (a, b) {
    return a < b ? -1 : 1;
}

function orderWeight(strng) {
    // your code
    const weights = strng.trim().split(/\s{1,}/).map((v, i) => {
        return {
            key: '' + v,
            val: sumOfWeightDigits(v)
        }
    }).sort((a, b) => {
        const diff = a.val - b.val;
        return diff === 0 ? compare(a.key, b.key) : diff;
    });

    return weights.map(item => item.key).join(' ');
}
```
