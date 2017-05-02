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
####  Practical Use Cases:
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
#### Practical Use Cases
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
## Create a shallow Copy of an Array with slice()
```javascript
// Array.prototype.slice()
  var items = [1,2,3,4,5];
  var copy = items.slice();

  // anything we do to the copy won't affect the original Array
  copy.push(6);
  copy[0] = 100;

  console.log(copy); // [100,2,3,4,5,6]
  console.log(items); // [1,2,3,4,5]
```
#### Practical Use Case
```javascript
var person  = {
    name: 'shane-osbourne'
};

var filters = {
    'deslugify': x => x.replace('-', ' '),
    'uppercase': x => x.toUpperCase()
};

var input    = 'name | deslugify | uppercase';

var sections = input.split('|').map(x => x.trim()); // ["name", "deslugify", "uppercase"]
console.log(sections);

var ref      = person[sections[0]]; // "shane-osbourne"
var output   = sections
    .slice(1) // ["deslugify", "uppercase"]

    .reduce((prev, next) => {
      // if filters exists that matches the name of deslugify or uppercase
        if (filters[next]) { // if filters[deslugify] exists
            return filters[next].call(null, prev);// return the result of calling filters with no context and prev value; prev is ref
        }
        return prev; // if filters[next] did not exist, give prev value
    }, ref); // start with the ref "shane-osbourne"

console.log(output); //"SHANE OSBOURNE"
```
## Sort an Array alphabetically or numerically
```javascript
// Array.prototype.sort()

// when using sort with numbers; the numbers are being converted to strings first and then compared using their position in unicode

var items = [10,30,20];
items.sort(); // [10,20,30]

// ISSUE (wrong result) when you have different ranges of numbers(bc of the unicode position)
var items = [10,30,2,20];
items.sort(); // WRONG result [10,2,20,30]

// SOLUTION (compare the current with next item  using the sorting algorthm)
// 1. sort in INCREASING order
items.sort((a, b) => a - b); // GOOD result [2,10,20,30]
// 1. sort in DECREASING order
items.sort((a, b) => b - a); // GOOD result [30, 20, 10, 2]

```
### How the sorting algorithm works
```javascript
items.sort((a, b) =>{
  console.log(a-b); // [2,10,20,30]
  if (a - b === 0){
    return 0;
  }
  if (a - b < 0){
    return -1;
  }
  if (a - b > 0){
    return 1;
  }
})
```
#### Practical use Cases
```javascript
var lessons = [
    {
        title: 'Javascript Array methods in depth - concat',
        views: 1000
    },
    {
        title: 'Javascript Array methods in depth - slice',
        views: 1050
    },
    {
        title: 'Javascript Array methods in depth - join',
        views: 1025
    }
];
// sort the lessons based on views number(biggest to smallest)
var list = lessons
    .sort((a, b) => b.views - a.views) // gives back a new sorted array

    // for each item in the array give an <li> tag with some padding; accessing the title and the views
    .map(x => `    <li>${x.title} (${x.views})</li>`)
    .join('\n'); // join all the <li> together with a new line character

// merge all our <li> tags into a <ul>
var output = `<ul>\n${list}\n</ul>`;
console.log(output);

// select the output div and put the ul in it
var container = document.querySelector('#output');
container.innerHTML = output;

// You get in console
<ul>
    <li>Javascript Array methods in depth - slice (1050)</li>
    <li>Javascript Array methods in depth - join (1025)</li>
    <li>Javascript Array methods in depth - concat (1000)</li>
</ul>
```
