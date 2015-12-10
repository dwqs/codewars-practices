#Description

**Write this function**

![](http://i.imgur.com/mlbRlEm.png)

`for i from 1 to n`, do `i % m` and return the `sum`.

```
f(n=10, m=5) // returns 20 (1+2+3+4+0 + 1+2+3+4+0)
```

You'll need to get a little clever with performance, since n can be a very large number

**Kata's link:** [Sum of many ints](http://www.codewars.com/kata/sum-of-many-ints/)

#Best Practices

**First:**
```
f = function(n, m) {
  sum1toN = function(x) {
    return x * (x + 1) / 2;
  };
  
  return (sum1toN(m - 1)) * (Math.floor(n / m)) + sum1toN(n % m);
};
```

**Second:**
```
function f(n, m) {
  return Math.floor(n / m) * m * (m - 1) / 2 + (n % m) * (n % m + 1) / 2
}
```

**Third:**
```
function f(n, m) {
  return gauss(m - 1) * (n / m | 0) + gauss(n % m)
}

function gauss(n) {
  return n * (n + 1) / 2
}
```

**Fourth:**
```
function f(n, m) {
  return Math.floor(n/m) * (m-1)*m/2 + (n%m)*(n%m+1)/2;
}
```

**Fifth:**
```
function f(n, m) {
  return ~~(n/m)*m*(m-1)/2 + n%m * (n%m + 1)/2;
}
```