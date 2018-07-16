
## Description

Write a function called that takes a string of parentheses, and determines if the order of the parentheses is valid. The function should return `true` if the string is valid, and `false` if it's invalid.

### Examples
```js
"()"              =>  true
")(()))"          =>  false
"("               =>  false
"(())((()())())"  =>  true
```

**Kata's link**: [Valid Parentheses](https://www.codewars.com/kata/valid-parentheses)

## Best Practices

**First:**
```js
// I had something that was smaller and looked cooler, but
// this is how you'd want to write an actual parser.
function validParentheses(string){
   var tokenizer = /[()]/g, // ignores characters in between; parentheses are
       count = 0,           // pretty useless if they're not grouping *something*
       token;
   while(token = tokenizer.exec(string), token !== null){
      if(token == "(") {
         count++;
      } else if(token == ")") {
         count--;
         if(count < 0) {
            return false;
         }
      }
   }
   return count == 0;
}
```

**Second:**
```js
function validParentheses(parens){
  var indent = 0;
  
  for (var i = 0 ; i < parens.length && indent >= 0; i++) {
    indent += (parens[i] == '(') ? 1 : -1;    
  }
  
  return (indent == 0);
}
```

**Third:**
```js
function validParentheses(parens){
  var n = 0;
  for (var i = 0; i < parens.length; i++) {
    if (parens[i] == '(') n++;
    if (parens[i] == ')') n--;
    if (n < 0) return false;
  }
  
  return n == 0;
}
```

## My solutions
```js
function validParentheses(parens){
  //TODO 
  const reg = /\(\)/g;
  while(reg.test(parens)) {
    parens = parens.replace(reg, '');
  }
    
  return parens === '';
}
```
