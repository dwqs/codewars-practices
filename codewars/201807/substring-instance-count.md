
## Description

Complete the solution so that it returns the number of times the search_text is found within the full_text.

```js
searchSubstr( fullText, searchText, allowOverlap = true )
```

so that overlapping solutions are (not) counted. If the searchText is empty, it should return 0.

### Examples
```js
searchSubstr('aa_bb_cc_dd_bb_e', 'bb') # should return 2 since bb shows up twice
searchSubstr('aaabbbcccc', 'bbb') # should return 1
searchSubstr( 'aaa', 'aa' ) # should return 2
searchSubstr( 'aaa', '' ) # should return 0
searchSubstr( 'aaa', 'aa', false ) # should return 1
```

**Kata's link**: [Return substring instance count](https://www.codewars.com/kata/return-substring-instance-count-2)

## Best Practices

**First:**
```js
function searchSubstr(fullText, searchText, allowOverlap) {
  if(searchText == '') return 0;
  var re = new RegExp(searchText, 'g');
  if(allowOverlap) {
    var count = 0;
    while(re.exec(fullText)) {count++; re.lastIndex -= searchText.length - 1;}
    return count;
  } else return (fullText.match(re) || []).length || 0;
}
```

**Second:**
```js
function searchSubstr( fullText, searchText, allowOverlap ){
  if(fullText == "" || searchText == "") return 0;
  
  var re = new RegExp(searchText, "g"), count = 0, match;
  while (match = re.exec(fullText)) {
    count++;
    if(allowOverlap) re.lastIndex = match.index+1;
  }
  return count;
}
```

## My solutions
```js
function countOverlap (reg, matched, fullText, searchText) {
    let count = matched.length;
    for (let i = 0, l = matched.length; i < l; i++) {
        const start = fullText.indexOf(matched[0]) + 1;
        const end = start + searchText.length;
        const sub = fullText.slice(start, end + 1);
        
        if (reg.test(sub)) {
            count += 1;
        }

        fullText = fullText.slice(start + searchText.length);
    }
    return count;
}

function searchSubstr( fullText, searchText, allowOverlap = true ){
    if (!searchText) {
        return 0;
    }

    const reg = new RegExp(searchText, 'g');
    const matched = fullText.match(reg);

    return allowOverlap ? (matched ? countOverlap(reg, matched, fullText, searchText) : 0) : (matched ? matched.length : 0);
}
```
