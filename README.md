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

var upper = name.split(' ') // creates an array [shane, osbourne]
.map(x => x.charAt(0).toUpperCase() + x.slice(1)) // produces another array: [Shane, Osbourne]
.join(' '); //  creates a string: 'Shane Osbourne'

console.log(upper); // 'Shane Osbourne'

```
## *_indexOf()_* is used to search an Array for a particular value
### Practical Use Cases
_**#1. Search for particular Strings in an array**_
```javascript
// Array.prototype.indexOf()

var family = ['Shane', 'Sally', 'Isaac', 'Kittie'];
// check if a value in an Array already exists
var kittieExists = family.indexOf('Kittie') > -1;

console.log(family.indexOf('Kittie')); // 3 -> Kittie was found at index 3; when the value is NOT FOUND you get -1;
console.log(kittieExists); // true

if(!kittieExists){ // if kittie does nOT exist
  family.push('kittie'); // add it to the array
}
```
_**#2. Search for particular Object Values in an array**_
```javascript
// Array.prototype.indexOf()

// lets say we have 3 objects
var shane = {
  name: 'Shane'
}
var sally = {
  name: 'Sally'
}
var kittie = {
  name: 'Kittie'
}

var family = [shane, sally]; // array of objects containing shane and sally

// search for the kittie object in family
console.log(family.indexOf(kittie)); // -1 -> when the value is NOT FOUND you get -1;

```
_**#3. How to use indexOf() to create a filter**_
```javascript
var whitelist = ['.css', '.js'];

var events = [
  {
    file: 'css/core.css'
  },
  {
    file: 'js/app.js'
  },
  {
    file: 'index.html'
  }
];
// filter the events Array based on wether or not the extension of the files matches anything on the whitelist
var filtered = events.filter(event => {
  // use the path module to get the file extension
  var ext = require('path').extname(event.file);
  // check if this file ext is part of the whitelist and therefor should be allowed on the filtered results
  return whitelist.indexOf(ext) > -1;
});

console.log(filtered);// [{file: 'css/core.css'}, {file: 'js/app.js'}]
```
