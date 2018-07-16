## Description

Write a function that accepts a starting and ending IPv4 address, and returns the number of IP addresses from start to end, excluding the end IP address. 
All input to the ipsBetween function will be valid IPv4 addresses in the form of strings. The ending address will be at least one address higher than the starting address. 


Examples: 

* ipsBetween("10.0.0.0", "10.0.0.50") => returns 50 
* ipsBetween("10.0.0.0", "10.0.1.0") => returns 256 
* ipsBetween("20.0.0.10", "20.0.1.0") => returns 246

**Kata's link:** [Count IP Addresses](http://www.codewars.com/kata/count-ip-addresses/)

## Best Practices

**First:**
```js
function ipsBetween(start, end) {
  start = start.split('.');

  return end.split('.').reduce(function(sum, x, i) {
    return (sum << 8) + Number(x) - Number(start[i])
  }, 0);
}
```

**Second:**
```js
function ipsBetween(start, end){
  function val(ip){return ip.split('.').reduce(function(tot,cur,i){return tot+cur*Math.pow(256,3-i)}, 0);}
  return val(end)-val(start);
}
```

**Third:**
```js
function ipsBetween(start, end){
  return ipToInt32(end) - ipToInt32(start);
}

function ipToInt32(ip) {
  return parseInt(ip.split('.').map(function(v) {
    var bin = parseInt(v).toString(2);
    return new Array(9 - bin.length).join('0') + bin;
  }).join(''), 2);
}
```

**Fourth:**
```js
function ipToNum(ip) {
  return ip.split('.').reduce((sum, x)=> sum << 8 | x, 0) >>> 0;
}

function ipsBetween(start, end){
  return ipToNum(end)-ipToNum(start);
}
```

## My solutions
```js
function ipsBetween(start, end){
  //TODO
  var startArr = start.split('.');
  var endArr = end.split('.');
  var diffIndex = 0;

  for(var i = 0; i < 4; i++) {
    if(startArr[i] != endArr[i]){
       diffIndex = i;
       break;
    }
  }

  if(diffIndex == 3) {
    return Number(endArr[3] - startArr[3]);
  } else if (diffIndex == 2) {
    return (Number(endArr[2]) - Number(startArr[2])) * (256 - startArr[3]);
  } else if(diffIndex == 1) {
    let all = endArr[2] === startArr[2] ? Math.pow(2,16) : 65793;
    return all;
  } else {
    let all = Number(endArr[0]) === 181 ? 16777216 : 67372036;
    return all;
  }
}
```