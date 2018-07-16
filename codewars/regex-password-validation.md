## Description

You need to write regex that will validate a password to make sure it meets the following criteria:

* At least six characters long
* contains a lowercase letter
* contains an uppercase letter
* contains a number

Valid passwords will only be alphanumeric characters.

**Kata's link**: [Regex Password Validation](https://www.codewars.com/kata/regex-password-validation/)

## Best Practices

**First:**
```js
function validate(password) {
  return /^(?=.*\d)(?=.*[a-z])(?=.*[A-Z])[a-zA-Z0-9]{6,}$/.test(password);
}
```

**Second:**
```js
function validate(password) {
  return  /^[A-Za-z0-9]{6,}$/.test(password) &&
          /[A-Z]+/           .test(password) &&
          /[a-z]+/           .test(password) &&
          /[0-9]+/           .test(password) ;
}
```

## My solutions
I didn't resolve it.
