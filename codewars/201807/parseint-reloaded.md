
## Description

In this kata we want to convert a string into an integer. The strings simply represent the numbers in words.

Additional Notes:

* The minimum number is "zero" (inclusively)
* The maximum number, which must be supported is 1 million (inclusively)
* The "and" in e.g. "one hundred and twenty-four" is optional, in some cases it's present and in others it's not
* All tested numbers are valid, you don't need to validate them

### Examples
```js
"one" => 1
"twenty" => 20
"two hundred forty-six" => 246
"seven hundred eighty-three thousand nine hundred and nineteen" => 783919
```

**Kata's link**: [parseInt reloaded](https://www.codewars.com/kata/parseint-reloaded)

## Best Practices

**First:**
```js
function parseInt(string) {
  var map = {"zero":0,"one":1,"two":2,"three":3,"four":4,"five":5,"six":6,"seven":7,"eight":8,"nine":9,"ten":10,"eleven":11,"twelve":12,"thirteen":13,"fourteen":14,"fifteen":15,"sixteen":16,"seventeen":17,"eigthteen":18,"nineteen":19,
    "twenty":20, "thirty":30, "forty":40, "fifty":50, "sixty":60, "seventy":70, "eighty":80, "ninety":90,};
  var multiMap = {"hundred":100, "thousand":1000, "million":1000000};
  var result = 0, result2 = 0, multiply = 0;
  
  function getNumber(string) {
    var nArr = string.split("-");
    if (nArr.length > 1) {
      return map[nArr[0]] + map[nArr[1]];
    }
    return map[string];
  }
  
  string.split(" ").map(function(number) {
    if (multiMap[number]) {
      result *= multiMap[number];
      if (result >= 1000) {
        result2 = result;
        result = 0;
      }
    }
    else if (number != "and") {
      result += getNumber(number);
    }
  });
  return result + result2;
}
```

**Second:**
```js
var words = {
  "zero":0, "one":1, "two":2, "three":3, "four":4, "five":5, "six":6, "seven":7, "eight":8, "nine":9, 
  "ten":10, "eleven":11, "twelve":12, "thirteen":13, "fourteen":14, "fifteen":15, "sixteen":16, 
  "seventeen":17, "eighteen":18, "nineteen":19, "twenty":20, "thirty":30, "forty":40, "fifty":50, 
  "sixty":60, "seventy":70, "eighty":80, "ninety":90
};
var mult = { "hundred":100, "thousand":1000, "million": 1000000 };
function parseInt(str) {
  return str.split(/ |-/).reduce(function(value, word) {
    if (words[word]) value += words[word];
    if (mult[word]) value += mult[word] * (value % mult[word]) - (value % mult[word]);
    return value;
  },0);
}
```

## My solutions
```js
const numbersMap = {
    'zero': 0,
    'one': 1,
    'two': 2,
    'three': 3,
    'four': 4,
    'five': 5,
    'six': 6,
    'seven': 7,
    'eight': 8,
    'nine': 9,
    'ten': 10,
    'eleven': 11,
    'twelve': 12,
    'thirteen': 13,
    'fourteen': 14,
    'fifteen': 15,
    'sixteen': 16,
    'seventeen': 17,
    'eighteen': 18,
    'nineteen': 19,
    'twenty': 20,
    'thirty': 30,
    'forty': 40,
    'fifty': 50,
    'sixty': 60,
    'seventy': 70,
    'eighty': 80,
    'ninety': 90,
    'hundred': 100,
    'thousand': 1000,
    'million': 1000000
}

function getSimpleNumber (number) {
    return numbersMap[number] 
            ? numbersMap[number] 
            : number.split('-').map(v => numbersMap[v]).reduce((prev, next) => prev + next, 0);
}

function getComplexNumber (numbers) {
    let res = 0;
    numbers = numbers.filter(v => v !== 'and');

    for(let i = 0, l = numbers.length; i < l;) {
        if (numbers[i + 1] && ['hundred', 'thousand', 'million'].includes(numbers[i + 1])) {
            const v = numbers[i + 1];
            if (v === 'hundred') {
                res += numbersMap[numbers[i]] * numbersMap[numbers[i + 1]];
            } else {
                res += getSimpleNumber(numbers[i]);
                res = res * numbersMap[numbers[i + 1]];
            }
            i += 2;
            continue;
        } else if (numbers[i] === 'thousand') {
            res = res * numbersMap['thousand'];
        } else {
            res += getSimpleNumber(numbers[i]);
        }
        i += 1;
    }

    return res;
}

function parseInt (string) {
    // TODO: it's your task now
    const numbers = string.split(' ');
    return numbers.length === 1 ? getSimpleNumber(numbers[0]) : getComplexNumber(numbers);
}
```
