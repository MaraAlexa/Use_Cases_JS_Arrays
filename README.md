# Understanding JS Arrays with Practical Use Cases

## Use  *_.concat()_*  to Add Values to an Array
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
## Use *_.join()_* to Combine Values of an Array into a String
```javascript
// Array.prototype.join();

var name = ['Shane', 'Osbourne'];

// give all the values back as a string and I provide the separator in between
console.log(names.join(' '));  // Shane Osbourne with a space in between
console.log(names.join('-'));  // Shane-Osbourne
console.log(names.join(''));  // ShaneOsbourne
console.log(names.join());  // when not providing any arg at all, you get the values separated with a comma -> Shane,Osbourne

```
###  Practical Use Cases:
_**#1. Lets say you have a command line program and you want to provide a help screen to users**_
```javascript

// store each line of the help text in an array   
var help = [
  'Usage',
  '     foo-app <input>'
]
// check if the user has run the 'help' command by looking at the third argument available tools
if(process.argv[2] === 'help'){
  console.log(help.join('\n')); // takes every item in the help array, puts a new line in between each one and prints the result
}; // prints the values from the help array in the terminal (when users run help in the terminal):
 /*
 Usage
      foo-app <input>
*/
```
here is what the user would get if he runs help in command line
![alt text](/images/terminal.png "Logo Title Text 1")

_**#2. Lets say You want to Upper Case the first letter of each word in a String**_
```javascript
var name = 'shane osbourne';

var upper = name.split(' ') // [shane, osbourne]
.map(x => x.charAt(0).toUpperCase() + x.slice(1)) // produces another array: [Shane, Osbourne]
.join(' '); //  creates a string: 'Shane Osbourne'

console.log(upper); // 'Shane Osbourne'

```
