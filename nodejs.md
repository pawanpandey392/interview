# **Node JS Interview Questionare**
<br />

<h2><b><i>Question :- package.json Vs package-lock.json?</i></b></h2>
<h3><b><i>Answer - </i></b></h3>

<p>Package.json is used to install different open source and other available packages (that is, pre-packaged code modules) in a Node.js project.</p>

+ ### _1. Why is package-lock.json created?_

    <p>When you install any package in your project by executing the below command</p>

    ``` css
    npm i <package-name> — save
    ```
    <p>It will install the exact latest version of that package in your project and save the dependency in package.json with a carat (^) sign. Like, if the current version of a package is 5.2.3 then the installed version will be 5.2.3 and the saved dependency will be ^5.2.3. Carat (^) means it will support any higher version with major version 5 like 5.3.1 and so on. Here, package-lock.json is created for locking the dependency with the installed version.</p>

+ ### _2. What is the purpose or use of package-lock.json?_

    <p>To avoid differences in installed dependencies on different environments and to generate the same results on every environment we should use the package-lock.json file to install dependencies.</p>

    <p>Ideally, this file should be on your source control with the package.json file so when you or any other user will clone the project and run the command “npm i”, it will install the exact same version saved in package-lock.json file and you will able to generate the same results as you developed with that particular package.</p>

+ ### _3. Why should we commit package-lock.json with our project source code??_

    <p>During deployment, when you again run “npm i” with the same package.json file without the package-lock.json, the installed package might have a higher version now from what you had intended.</p>

    <p>Now, what if you wanted to have that particular version for your dependency during deployment which you used at the time of development. This is the need of creating a package-lock.json file and keeping it with the source code. This file is created with the details of the specific version installed in your project.</p>

    <p></p>

<br />

<h2><b><i>Question :- Explain Closures in Javascript?</i></b></h2>
<h3><b><i>Answer - </i></b></h3>

<p>A closure is the combination of a function bundled together (enclosed) with references to its surrounding state (the lexical environment). In other words, a closure gives you access to an outer function’s scope from an inner function. In JavaScript, closures are created every time a function is created, at function creation time.</p>

``` js
function init() {
    var name = 'Mozilla'; // name is a local variable created by init
    function displayName() { // displayName() is the inner function, a closure
        alert(name); // use variable declared in the parent function
    }
    displayName();
}
init();
```

<p>The amazing thing is, even if the outer function returns the inner function then also inner function will have access to outer function variables, in other programming languages if a function returns then it becomes ready for garbage collection or is completely removed from the heap, but in Javascript if there is closure then the parent function variables remain in the heap.</p>

<p>So the following code is also correct.</p>

``` js
function outer1() {
    var a = 123;
    return function() { // this function act as closure
        console.log(a);
    }
}

var func  = outer1();
func() // this will also print '123'
```

+ ### ***Advantages of closures:***
    - Callbacks implementation in javascript is heavily dependent on how closures work
    - Mostly used in Encapsulation of the code
    - Also used in creating API calling wrapper methods

+ ### ***Disadvantages of closures:***
    - Variables used by closure will not be garbage collected
    - Memory snapshot of the application will be increased if closures are not used properly

> <strong>Let try to solve the problem that comes along while making an async operation inside a loop</strong>

+ Use IIFE (Immediately Invoked Function Expression)
+ Replacing var with let keyword

<br />

<h2><b><i>Question :- Flattening a Javascript object?</i></b></h2>
<h3><b><i>Answer - </i></b></h3>

<p>Flattening deeply nested object can be easily achieved by using recursive technique.</p>

``` js
// input
var user = {
    name: "Vishal",
    address: {
        primary: {
            house: "109",
            street: {             
                main: "21",
                cross: "32"
            }
        }
    }
};

//output
{
    user_name: "Vishal",
    user_address_primary_house: "109",
    user_address_primary_street_main: "21",
    user_address_primary_street_cross: "32",
}
```

> <strong>Algorithm - </strong>

+ Iterate over keys of the object
+ Append child key name into the parent key name
+ If the child key's value is an object again call the same function
+ Else assign key to the new value

> <strong>Code Solution - </strong>

``` js 
var flattendObj = {};
const flattenObject = (obj, keyName) => {
    Object.keys(obj).forEach(key => {
        var newKey = `${keyName}_${key}` 
        if (typeof obj[key] === "object") {
            // calling the function again
            flattenObject(obj[key], newKey);
        } else {
            flattendObj[newKey] = obj[key];
        }
    });
};
console.log(flattendObj);
```

<br />

<h2><b><i>Question :- Debouncing in Javascript?</i></b></h2>
<h3><b><i>Answer - </i></b></h3>

<p>Debouncing is a very good to have feature, when user is expected to do a particular action very very quickly, such as typing a product name for searching in an e-commerce site.</p>

<p>Imagine on each key press the client code makes and API call for fetching the suggestions to be shown in the search result, these are so many api calls, to avoid this situation of making so many api call we can implement debouncing.</p>

> <strong>Debounce Algorithm - </strong>

+ Call a function on user action after a delay time
+ Clear the previous delay time on the next action if the action is performed before that delay time
+ Make use of setTimeout

> <strong>Code Solution - </strong>

``` html
<input id="debounce-input" />
```

``` js
// debounce logic
var timer = null;
const debounce = (actionHandler, delay) => {
    if (timer) {
        // clearing timer
        clearInterval(timer);
    }
    timer = setTimeout(actionHandler, delay);
};

// some costly function
const fetchDataFromAPI = () => {
    //here you can put your fetch logic
    console.log("fetchData");
};

// event binding to input
const elem = document.getElementById("debounce-input");

elem.addEventListener("input", e => {
    debounce(fetchDataFromAPI, 1000);
});
```

<br />

<h2><b><i>Question :- Javascript?</i></b></h2>
<h3><b><i>Answer - </i></b></h3>

<br />

<h2><b><i>Question :- Javascript?</i></b></h2>
<h3><b><i>Answer - </i></b></h3>

<br />

<h2><b><i>Question :- Javascript?</i></b></h2>
<h3><b><i>Answer - </i></b></h3>

<br />

<h2><b><i>Question :- Javascript?</i></b></h2>
<h3><b><i>Answer - </i></b></h3>





