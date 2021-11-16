# Ecmascript Version 5

## 1. _Trailing Commas_

> Trailing commas are allowed in javascript after ecmascript 5.

```
  const person = {
    firstName: "John",
    lastName: " Doe",
    age: 46,
  }
```

<br />

## 2. _Property Access on Strings_

```
  let str = "HELLO WORLD";
  str.charAt(0);
  str[0];
```

<br />

## 3. _`String.trim()`_

```
  console.log(`String.trim() :- `);
  var str = "       Hello World!        ";
  // console.log(String.trim(str));
  console.log(str.trim());
```

<br />

## 4. _`Array.isArray()`_

```
  console.log(`Array.isArray() :- `);
  console.log(Array.isArray(null));
  console.log(Array.isArray({}));
  console.log(Array.isArray([]));
  console.log(Array.isArray('ssss'));
```

<br />

## 5. _`Array.forEach()`_

> The `forEach()` method executes a provided function once for each array element.

```
  let a = arr.forEach(x => console.log(x * 5));
  console.log(a);
```

<br />

## 6. _`Array.map()`_

> The `map()` method creates a new array populated with the results of calling a provided function on every element in the calling array.

```
  let b = arr.map(a => a);

  console.log('Given Array :- ', arr);
  console.log('Output :- ', b);
  console.log('Are both array equal? :- ', arr === b);
```

<br />

## 7. _`Array.filter()`_

> The `filter()` method creates a new array with all elements that pass the test implemented by the provided function.

```
  const words = ['spray', 'limit', 'elite', 'exuberant', 'destruction', 'present'];

  const result = words.filter(word => word.length > 6);
  console.log(result);
```

<br />

## 8. _`Array.reduce()`_

> The `reduce()` method executes a reducer function (that you provide) on each element of the array, resulting in single output value.

```
  const reducer = (accumulator, currentValue) => accumulator + currentValue;

  console.log(arr.reduce(reducer));
  console.log(arr.reduce(reducer, 15));
```

<br />

## 9. _`Array.reduceRight()`_

> The `reduceRight()` method applies a function against an accumulator and each value of the array (from right-to-left) to reduce it to a single value.

```
  let reducer1 = (accumulator, currentValue) => accumulator.concat(currentValue);

  const array1 = [[0, 1], [2, 3], [4, 5]].reduceRight(reducer1);
  console.log(array1);
```

<br />

## 10. _`Array.every()`_

> The `every()` method tests whether all elements in the array pass the test implemented by the provided function. It returns a Boolean value.

```
  const isBelowThreshold = (currentValue) => currentValue < 40;

  const array = [1, 30, 39, 29, 10, 13];
  console.log(array.every(isBelowThreshold));
```

<br />

## 11. _`Array.some()`_

> The `some()` method tests whether at least one element in the array passes the test implemented by the provided function. It returns a Boolean value.

```
  const even = (element) => element % 2 === 0;
  const lessThanTwenty = (element) => element < 20;
  const moreThanfifty = (element) => element > 50;

  console.log(array.some(even));
  console.log(array.some(lessThanTwenty));
  console.log(array.some(moreThanfifty));
```

<br />

## 12. _`Array.indexOf()`_

> The `indexOf()` method returns the first index at which a given element can be found in the array, or -1 if it is not present.

```
  const beasts = ['ant', 'bison', 'camel', 'duck', 'bison'];

  console.log(beasts.indexOf('bison'));
  console.log(beasts.indexOf('bison', 2)); // start from index 2
  console.log(beasts.indexOf('giraffe'));
```

<br />

## 13. _`Array.lastIndexOf()`_

> The `lastIndexOf()` method returns the last index at which a given element can be found in the array, or -1 if it is not present. The array is searched backwards, starting at fromIndex.

```
  const animals = ['Dodo', 'Tiger', 'Penguin', 'Dodo'];

  console.log(animals.lastIndexOf('Dodo'));
  console.log(animals.lastIndexOf('Tiger'));
```

<br />

## 14. _`JSON.parse()`_

> The `JSON.parse()` method parses a JSON string, constructing the JavaScript value or object described by the string. An optional reviver function can be provided to perform a transformation on the resulting object before it is returned.

```
  const json = '{"result":true, "count":42}';
  const obj = JSON.parse(json);

  console.log(obj.count);
  console.log(obj.result);
  // json.result is not parsed and is string.
  console.log(json.result);
```

<br />

## 15. _`JSON.stringify()`_

> The `JSON.stringify()` method converts a JavaScript object or value to a JSON string, optionally replacing values if a replacer function is specified or optionally including only the specified properties if a replacer array is specified.

```
  console.log(JSON.stringify({ x: 5, y: 6 }));
  console.log(JSON.stringify([new Number(3), new String('false'), new Boolean(false)]));
  console.log(JSON.stringify({ x: [10, undefined, function(){}, Symbol('')] }));
  console.log(JSON.stringify(new Date(2006, 0, 2, 15, 4, 5)));
```

<br />

## 16. _`Date.now()`_

> The static `Date.now()` method returns the number of milliseconds elapsed since January 1, 1970 00:00:00 UTC.

```
const start = Date.now();
console.log('It will take 2 seconds to run. Starting timer...');

setTimeout(() => {
  const millis = Date.now() - start;
  console.log(`Seconds elapsed = ${Math.floor(millis / 1000)}`);
}, 2000);
```

<br />

## 17. _Property Getters and Setters_

```
  let user = {
    name: "John",
    surname: "Smith",

    get fullName() {
      return `${this.name} ${this.surname}`;
    },

    set fullName(value) {
      [this.name, this.surname] = value.split(" ");
    }
  };
  console.log(`Set fullName is executed with the given value.`);
  user.fullName = "Alice Cooper";
  console.log(user.name);
  console.log(user.surname);
```

<br />

## 18. _New Object Property Methods_

> `Object.defineProperty()` is a new Object method in ES5.

```
  let person = {
    firstName: "John",
    lastName : "Doe",
    language : "NO",
  };
```

> Change a Property:

```
  Object.defineProperty(person, "language", {
    value: "EN",
    writable : true,
    enumerable : true,
    configurable : true
  });
```

<br />

## 19. _Change a Property_

> Adding or changing an object property

```
  Object.defineProperty(object, property, descriptor)
```

> Adding or changing many object properties

```
  Object.defineProperties(object, descriptors)
```

> Accessing Properties

```
  Object.getOwnPropertyDescriptor(object, property)
```

> Returns all properties as an array

```
  Object.getOwnPropertyNames(object)
```

> Returns enumerable properties as an array

```
  Object.keys(object)
```

> Accessing the prototype

```
  Object.getPrototypeOf(object)
```

> Prevents adding properties to an object

```
  Object.preventExtensions(object)

  <!-- Returns true if properties can be added to an object -->

  Object.isExtensible(object)
```

> Prevents changes of object properties (not values)

```
  Object.seal(object)

  <!-- Returns true if object is sealed -->

  Object.isSealed(object)
```

> Prevents any changes to an object

```
  Object.freeze(object)

  <!-- Returns true if object is frozen -->

  Object.isFrozen(object)
```

<br /><br />

# Ecmascript Version 6

## 1. _Default Parameters_

> Default values for parameter are accepted in javascript version above ecmascript 6.

```
  function calculateAge (defaultAge = 10) {
    console.log(`Your default age is ${defaultAge}`);
  }
  calculateAge();
  calculateAge(12);
```

<br />

## 2. _Template Literals_

```
  console.log('\n2. Template Literals :- ');
  let firstName = 'Caroline', lastName = 'Forbes';

  let name = `Your name is ${firstName} ${lastName}.`;
  console.log(name);
```

<br />

## 3. _Multi-line Strings_

```
  let poem = `Johny Johny Yes Papa,
              Eating sugar?  No, papa!
              Telling lies? No, papa!
              Open your mouth Ah, ah, ah!`;
  console.log(poem);
```

<br />

## 4. _Destructuring Assignment_

```
  let {age, a: status = false} = {age: 42, isAlive: true, livesIn: 'Nova Scotia'};
  let {livesIn, isAlive, ...newBe} = {age: 42, isAlive: true, livesIn: 'Nova Scotia', a: true};
  console.log(status);
  console.log(age);
  console.log(livesIn);
  console.log(isAlive);
  console.log(newBe);
```

<br />

## 5. _Enhanced Object Literals_

> Default values for parameter are accepted in javascript version above ecmascript 6.

```
  function getLaptop(make, model, year) {
    return {make, model, year}
  }
  getLaptop('Apple', 'MacBook', '2015');
```

<br />

## 6. _Arrow Functions_

```
  let arrowFunction = (params) => {
    console.log('Hey there, I am an Arrow function.');
    console.log(`I can even take params like ${params}`);
  };
  arrowFunction('Alienated Behaviour');
```

<br />

## 7. _Block-Scoped Constructs Let and Const_

```
function calculateAmount (boolVal) {
  let amount = 0;
  if (boolVal) {
    let amount = 1;
  }
  return amount;
}
console.log(calculateAmount(true));
```

<br />

## 8. _Classes_

```
  class Profile {
    constructor(firstName, lastName = '') {
      this.firstName = firstName;
      this.lastName = lastName;
    }

    getName() {
      console.log(`Name: ${this.firstName} ${this.lastName}`);
    }
  }
  let profileObj = new Profile('Damon', 'Salvatore');
  profileObj.getName();
```

<br />

## 9. _Modules_

```
  export var userID = 10;
  export function getName(name) {};

  import {userID, getName} from 'module';
  console.log(userID);
```

<br />

## 10. _Promises_

```
  let promise = new Promise((resolve, reject) => {
    console.log('I am inside a Promise.');
    resolve();
  }).then(() => {
    console.log('Then I got resolved.');
    reject();
  }).catch(() => {
    console.log('Then I got rejected.');
  }).finally(() => {
    console.log('Finally I am here.');
  });
```

<br /><br />

# Ecmascript Version 7

## 1. _`Array.prototype.includes`_

```
  let arr = ['a', 'b', 'c'];
  console.log(arr.includes('b'));
  console.log(arr.includes('d'));
  console.log(arr.includes('c', 2));
  console.log(arr.includes('c', 3));
  console.log(['a', 'b', NaN].includes(NaN));
  console.log('a123b'.includes('123'));
  console.log(arr.includes('c', '11eeee'));
```

<br />

## 2. _Exponentiation Operator (\*\*)_

```
console.log(2 ** 3)
console.log(2 ** 4)
```

<br /><br />

# Ecmascript Version 8

## 1. _`Object.values()` & `Object.entries()`_

```
  let arr = {
    'key': 'value',
    'key1': 'value',
    'key2': 'value'
  };
  console.log(Object.keys(arr));
  console.log(Object.values(arr));
  console.log(Object.values('arr'));
  console.log(Object.entries(arr));
```

<br />

## 2. _`String.prototype.padStart()` & `String.prototype.padEnd()`_

> padStart()

```
  console.log(JSON.stringify('Javascript'.padStart(10)));
  console.log(JSON.stringify('Javascript'.padStart(12)));
  console.log(JSON.stringify('Javascript'.padStart(15, 'x')));
  console.log(JSON.stringify('Javascript'.padStart(15, 'hey world')));
  console.log(JSON.stringify('Javascript'.padStart(1)));
```

> padEnd()

```
  console.log(JSON.stringify('Javascript'.padEnd(10)));
  console.log(JSON.stringify('Javascript'.padEnd(12)));
  console.log(JSON.stringify('Javascript'.padEnd(15, 'x')));
  console.log(JSON.stringify('Javascript'.padEnd(15, 'hey world')));
  console.log(JSON.stringify('Javascript'.padEnd(1)));
```

<br />

## 3. _`Object.getOwnPropertyDescriptors`_

```
  Object.freeze(arr);
  console.log(Object.getOwnPropertyDescriptors(arr));
```

<br />

## 4. _Trailing commas in function parameter lists_

```
  function trail (a, b, c,) {
    let obj = {key: 'value',};
    console.log('This is an example for trailing comma.');
    console.log(obj);
  }
  trail(2, 3, 5);
```

<br />

## 5. _Async Functions_

```
function delayMe () {
  return new Promise ((resolve, reject) => {
    setTimeout(() => {
      resolve('Hi, I will say hi after 5 seconds.');
    }, 5000);
  })
}
async function getContentFromMyWebsite () {
  let delay = await delayMe();
  console.log(delay);
}
getContentFromMyWebsite();
```

<br /><br />

# Ecmascript Version 9

## 1. _Rest/Spread Properties_

> Rest Properties

```
  const { first, second, ...others } = { first: 1, second: 2, third: 3, fourth: 4, fifth: 5 };
  console.log(first);
  console.log(second);
  console.log(others);
```

> Spread Properties

```
  const items = { first, second, ...others }
  console.log(items);
```

<br />

## 2. _Asynchronous iteration_

```
  for await (const line of readLines(filePath)) {
    console.log(line)
  }
```

<br />

## 3. _`Promise.prototype.finally()`_

```
  fetch('file.json')
    .then(data => data.json())
    .catch(error => console.error(error))
    .finally(() => console.log('finished'))
```

<br /><br />

# Ecmascript Version 10

## 1. _`Array.flat()`_

```
  let arr = [1, 2, 3, 4, 5, [6, 7, 8, 9, [10]]];
  console.log(arr.flat().flat());
```

<br />

## 2. _`Array.flatMap()`_

```
  let arr1 = [1, 2, 3, 4, 5];
  console.log(arr1.map(x => [x, x * 2]))
  console.log(arr1.flatMap(x => [x, x * 2]))
```

<br />

## 3. _`Object.fromEntries()`_

> Example One

```
  let arr2 = {
    name: 'Stefan Salvatore',
    age: '165 Years Old',
    species: 'Vampire'
  };
  let entries = Object.entries(arr2);
  let fromEntries = Object.fromEntries(entries);
  console.log(entries);
  console.log(fromEntries);
```

> Example Two

```
  let entries1 = new Map([
    [ 'name', 'Stefan Salvatore' ],
    [ 'age', '165 Years Old' ],
    [ 'species', 'Vampire' ]
  ]);
  let fromEntries1 = Object.fromEntries(entries1);
  console.log(fromEntries1);
```

<br />

## 4. _`String.trimStart()` & `String.trimEnd()`_

```
  let string = '      Hello World.      ';
  console.log(JSON.stringify(string.trimStart()));
  console.log(JSON.stringify(string.trimEnd()));
  console.log(JSON.stringify(string.trimStart().trimEnd()));
```

<br />

## 5. _Optional Catch Binding_

```
  try {
    throw new Error('This is Optional Catch Binding.');
  } catch {
    console.log('Optional Catch Binding with no params.');
  }
```

<br />

## 6. _`Function.toString()`_

```
  function sayHelloWorld () {
    let params = {name: 'Damon Salvatore'}
    console.log(`Hello ${params.name}`);
  }
  console.log(sayHelloWorld.toString());
```

<br />

## 7. _`Symbol.description`_

```
  let mySymbol = 'Hello Damon';
  let symObj = Symbol(mySymbol);
  console.log(symObj);
  console.log(String(symObj) === `Symbol(${mySymbol})`);
  console.log(symObj.description);
```

<br />

## 8. _Well Formed `JSON.Stringify()`_

```
  JSON.stringify('𝌆');
  JSON.stringify('\uD834\uDF06');
```

<br />

## 9. _`Array.Sort` Stability_

```
  let rating = [
    {name: 'Mike', age: 14},
    {name: 'Chad', age: 13},
    {name: 'Nick', age: 12},
    {name: 'Eminem', age: 12},
    {name: 'Rose', age: 12},
    {name: 'Diana', age: 13},
    {name: 'Megan', age: 12},
    {name: 'Hila', age: 14},
    {name: 'Ronan', age: 12},
    {name: 'Josh', age: 14},
    {name: 'Josey', age: 13},
  ]
  rating.sort((a, b) => a.age - b.age);
```

<br />

## 10. _JSON ⊂ ECMAScript (JSON Superset)_

```
  const LS = "";
  const PS = eval("'\u2029'");
  console.log(LS);
  console.log(PS);
```

<br /><br />

# Ecmascript Version 11

## 1. _BigInt_

> 2^53 – 1 is the maximum number you can represent in JavaScript. But with JavaScript ES11 update, BigInt will support the creation of numbers that are bigger than that. You can view the maximum number that can be represented in JavaScript for yourself by executing the below code.

```
  console.log(Number.MAX_SAFE_INTEGER); // output is: 9007199254740991

  // Case (i): When you add 1 to this number:
  const maxNum = Number.MAX_SAFE_INTEGER;
  console.log(maxNum +1); // output is: 9007199254740992

  // Case (ii): When you add 10 to this number:
  const maxNum = Number.MAX_SAFE_INTEGER;
  console.log(maxNum +10); // output is: 9007199254741000 which is wrong.
```

> Please Note: The right output is 9007199254741001.

> Hence, when you implement BigInt by adding the alphabet ‘n’ at the end of your number, you will get the correct output/result.

```
  const maxNum = 9007199254740991n;

  // Case (i): When you add 1 to this number:
  const maxNum = 9007199254740991n;
  console.log(maxNum +1n); // output is: 9007199254740992n

  // Case (ii): When you add 10 to this number:
  const maxNum = 9007199254740991n;
  console.log(maxNum +10n); // output  is: 9007199254741001n


  // Also, it is important to not mix BigInt with other types:

  const maxNum = 9007199254740991n;
  // output is: Cannot mix BigInt and other types, use explicit conversions
  console.log(maxNum +10);
```

<br />

## 2. _Dynamic Imports_

> While using webpack for module bundling, you may have used dynamic imports. With JavaScript ES11, you get native support for this feature.

```
  import('/dynamic-import-example.js')
    .then(Alert => {
        Alert.show();
    })
```

```
  export default {
    show() {
      console.log('Here are some good news from dynamic import.');
      return 'Here are some good news from dynamic import.';
    }
  }
```

<br />

## 3. _Global This_

> You can execute JavaScript codes in different environments, such as browsers or Node.js. In browsers, a global object is available under the window variable; whereas, in Node.js, it is an object called global. With globalThis, it is now easy to use a global object regardless of the environment in which the code is running.

```
  // In a browser
  window == globalThis // true

  // In node.js
  global == globalThis // true
```

<br />

## 4. _MatchAll_

> MatchAll method is useful when it comes to finding all the matches and their positions by applying the regular expression to a string. On the other hand, the match method returns only the items that were matched.

```
  const regex = /\b(iPhone)+\b/g;
  const smartphones = "S series, iPhone, note series, iPhone, A series, iPhone, moto phones";

  for (const match of smartphones.match(regex)) {
    console.log(match);
  }
```

> matchAll in contrast, returns additional information, such as the index of the string found.

```
  const regex = /\b(iPhone)+\b/g;
  const smartphones = "S series, iPhone, note series, iPhone, A series, iPhone, moto phones";
  for (const match of smartphones.matchAll(regex)) {
    console.log(match);
  }
```

<br />

## 5. _Nullish Coalescing_

```
  // Thruthy value without Nullish Coalescing
  let theNumber = 7
  let numb = theNumber || 5
  console.log(numb) // output is: 7

  // Falsy value with Nullish Coalescing
  let number = 0
  let num = number ?? 5
  console.log(num) // output is: 0

  // Null value with Nullish Coalescing
  let theNumber = null
  let number = theNumber ?? 5
  console.log(number) // output is: 5

  // More Example
  undefined ?? "string" // -> "string"
  null ?? "string" // -> "string"
  false ?? "string" // -> false
  NaN ?? "string" // -> NaN
```

<br />

## 6. _Optional Chaining_

> Accessing an Object Property

```
  const smartphones = {
      brands: {
          apple: true
      }
  }

  // output is: ‘true’
  console.log(smartphones.brands.apple);

  // output is: undefined, with no errors
  console.log(smartphones.companies?.motorola);

  // output is: TypeError: Cannot read property 'motorola' of undefined
  console.log(smartphones.companies.motorola);
```

> Accessing an Array

```
  let smartphone =  ['apple', 'samsung', 'motorola'];

  // output is: samsung
  console.log(smartphone[1]);

  // output is: TypeError: Cannot read property '1' of null
  smartphone = null
  console.log(smartphone[1]);

  // output is: undefined
  console.log(smartphone?.[1]);
```

> Calling a Function

```
  let phoneApple = () => {
    return '11 Pro Max'
  }

  // output is: 11 Pro Max
  console.log(phoneApple());

  // output is: TypeError: phoneApple is not a function
  phoneApple = null
  console.log(phoneApple());

  // undefined
  console.log(phoneApple?.());


  // More chaining
  const zipcode = person?.address?.zipcode;
```

<br />

## 7. _Private Identifier in Classes_

```
  class Smartphones {
    #phone_color = "silver";
    designer(name) {
      this.name = name;
    }

    get_color() {
      return this.#phone_color;
    }
  }
  const iPhone = new Smartphones("iPhone");

  // output is: silver
  console.log(iPhone.get_color());

  // output is: Private field '#phone_color' must be declared in an enclosing class
  console.log(iPhone.#phone_color)
```

<br />

## 8. _`Promise.allSettled`_

> When you want multiple Promises to complete, you can use Promise.all ([promise_1, promise_2]). In this process, if one of the promises fails, the JavaScript engine will throw an error. Luckily, there are cases in which the failure of one promise doesn’t matter, and the rest would resolve. To achieve that, the new JavaScript ES11 unpacks Promise.allSettled.

```
  promise_1 = Promise.resolve('hi');

  promise_2 = new Promise((resolve, reject) => setTimeout(reject, 100, 'world'));

  Promise.allSettled([promise_1, promise_2])
      .then(([promise_1_result, promise_2_result]) => {
        // output is: {status: 'fulfilled', value: 'hi'}
        console.log(promise_1_result);

        // output is: {status: 'rejected', reason: 'world'}
        console.log(promise_2_result);
      })

```

> Hence, only a resolved Promise returns an object with status and value; whereas, rejected Promise returns an object with status and reason.

<br />

## 9. _Static Identifier in Classes_

```
  class Smartphone {
    add_color() {
      console.log("Adding Colors");
    }
  }

  const apple = new Smartphone();

  // output is: Adding Colors
  apple.add_color();

  // TypeError: Smartphone.add_color is not a function
  Smartphone.add_color();
```

> When you try to access a method without instantiating the ‘Smartphone’ class, it will result in an error. With the help of static fields, you can now declare a class method using static keyword and call it from outside of a class.

```
  class Smartphone {
    designer(color) {
      this.color = color;
    }
    static create_smartphone(color) {
      return new Smartphone(color);
    }
  }

  // output is: undefined
  const silver = Smartphone.create_smartphone("silver");

```

<br />

## 10. _Top Level Await_

> To wait for a Promise to complete, a function with await operator should be defined within async function.

```
  const Smartphone = async () => {
      const color = await fetch(silver)
  };
```

> On the downside, if there is a need to wait for something in the global scope, it would not be possible, and generally needs an Immediately Invoked Function Expression.

```
  (async () => {
      const color = await fetch(silver)
  })();
```

> With the help of Top Level Await, you don’t have to wrap code in an async function. Instead, the below code will work:

```
  const color = await fetch(silver);
```

> It is very useful when it comes to using a fallback source when the initial one fails or resolving module dependencies.

```
  let Vue
  try {
      Vue = await import('silver_1_to_vue')
  } catch {
      Vue = await import('silver_2_to_vue')
  }
```

<br /><br />
