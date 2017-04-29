# Understanding JS Arrays with Practical Use Cases

## Use **_.concat_** to Add Values to an Array
```javascript
// with .concat you can Add values(of mixed types) to an Array
var items = [1,2];
var newItems = items.concat(3,4,'string', undefined);
console.log(newItems);  // [1, 2, 3, 4, 'string', undefined]

// .concat can also take in other arrays
var newArrayItems = items.concat([3,4], [5,6,7], 8,9);
console.log(newArrayItems);  // [1, 2, 3, 4, 5, 6, 7, 8, 9]

// USE CASE:
var people = [
  {
    name: 'Shane'
  },
  {
    name: 'Sally'
  }
];

var people2 = [
  {
    name: 'Simon'
  },
  {
    name: 'Ben'
  }
];

// Combine all the proprieties from the arrays above:

// BAD PRACTICE
people.forEach(function(person){
  console.log(person.name);
})
people1.forEach(function(person){
  console.log(person.name);
})

// GOOD PRACTICE
people.concat(people2).forEach(function(person){
  console.log(person.name);    /* "Shane"
                                  "Sally"
                                  "Simon"
                                  "Ben"   */
})
```
