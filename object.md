# Object

## 1. _Create Object_

> There are many ways to create an Object in javascript.

``` js
  const personA = {};

  const personB = Object.create({});

  const personC = new Object();
```

> The Object.create() method creates a new object, using an existing object as the prototype of the newly created object.

<br />

## 2. _Object.defineProperties()_

``` js
  Object.defineProperties(personA, {
    firstname: {
      value: 'John',
      writable: false, // can't be modified if set to false
      enumerable: false, // isn't accessible if set to false
      configurable: false // can't be deleted if set to false
    },
    lastname: {
      value: 'Doe',
      writable: true,
      enumerable: true,
      configurable: true
    }
  });
```

<br />

## 3. _Object.defineProperty()_

``` js
  Object.defineProperty(personA, 'image', {
    value: 'https://placeholder.com/images/user/1',
    writable: false, // can't be modified if set to false
    enumerable: true, // isn't accessible if set to false
    configurable: false // can't be deleted if set to false
  });
```

<br />

## 4. _Object.getOwnPropertyDescriptor()_

``` js
  const descriptor1 = Object.getOwnPropertyDescriptor(personA, 'firstname');

  console.log(
    descriptor1.value, 
    descriptor1.configurable, 
    descriptor1.enumerable, 
    descriptor1.writable
  );
```

<br />

## 5. _Object.getOwnPropertyDescriptors()_

``` js
  const descriptors1 = Object.getOwnPropertyDescriptors(personA);

  console.log(
    descriptors1.lastname.value, 
    descriptors1.lastname.writable, 
    descriptors1.lastname.configurable, 
    descriptors1.lastname.enumerable
  );
```

<br />

## 6. _Object.getOwnPropertyNames()_

> The Object.getOwnPropertyNames() method returns an array of all properties (including non-enumerable properties except for those which use Symbol) found directly in a given object.

``` js
  console.log(Object.getOwnPropertyNames(personA));
```

<br />

## 7. _Object.freeze()_

> There are many ways to create an Object in javascript.

``` js
  personB.lastname = 'Doe';
  const forzenPersonB = Object.freeze(personB);

  personB.firstname = 'Jane'; // New properties cannot be added
  personB.lastname = 'Wayne'; // Existing properties cannot be modified
  delete personB.lastname; // Existing properties cannot be deleted

  console.log('isFrozen? ', Object.isFrozen(personB));
  console.log('Person B ', personB);

  console.log(forzenPersonB === personB); // freeze() returns the same object that was passed in.
```
<br />

## 8. _Object.isExtensible()_

``` js
  console.log('personC isExtensible?', Object.isExtensible(personC));
  Object.preventExtensions(personC);
  console.log('personC isExtensible?', Object.isExtensible(personC));

  console.log('personB isExtensible?', Object.isExtensible(personB)); // Not extensible because the object is frozen.
  console.log('personA isExtensible?', Object.isExtensible(personA)); // Extensible

  try {
    Object.defineProperty(personC, 'emailId', {
      value: 'somerandom@email.address'
    });
  } catch (e) {
    console.log(e); // expected output: TypeError: Cannot define property property1, object is not extensible
  }
```

<br />

## 9. _Object.seal()_

> The Object.seal() method seals an object, preventing new properties from being added to it and marking all existing properties as non-configurable. Values of present properties can still be changed as long as they are writable.

``` js
  console.log('personA isSealed?', Object.isSealed(personA));
  Object.seal(personA);
  console.log('personA isSealed?', Object.isSealed(personA));

  try {
    Object.defineProperty(personA, 'contactNumber', {
      value: '801020304050',
      enumerable: true
    });
  } catch (e) {
    // Cannot add property as object is sealed.
    console.log(e); // expected output: TypeError: Cannot define property property1, object is not extensible
  }

  console.log(personA);
  // The lastname property's configurable descriptor is set to false. 
  console.log(Object.getOwnPropertyDescriptors(personA)); // [Marks all existing properties as non-configurable]

  personA.firstname = 'Noman'; // Non writable properties cannot be modified
  personA.lastname = 'Landrover'; // While writable properties can be modified
  console.log(Object.getOwnPropertyDescriptors(personA));
```

<br />

## 10. _Object.getPrototypeOf()_

``` js
  console.log('getPrototypeOf', Object.getPrototypeOf(personA));
```

<br />

## 11. _Object.is()_

> The Object.is() method determines whether two values are the same value.

### Conditions :-

1. both undefined
2. both null
3. both true or both false
4. both strings of the same length with the same characters in the same order
5. both the same object (meaning both values reference the same object in memory)

``` js
  Object.is(25, 25);                // true
  Object.is('foo', 'foo');          // true
  Object.is('foo', 'bar');          // false
  Object.is(null, null);            // true
  Object.is(undefined, undefined);  // true
  // Object.is(window, window);        // true
  Object.is([], []);                // false
  var foo = { a: 1 };
  var bar = { a: 1 };
  Object.is(foo, foo);              // true
  Object.is(foo, bar);              // false
```

<br />

## 12. _Object.keys()_

> Returns an array of a given object's own enumerable property names.

``` js
  console.log('Object.keys()', Object.keys(personA)); 
```

<br />

## 13. _Object.values()_

> The Object.values() method returns an array of a given object's own enumerable property values

``` js
  console.log('Object.values()', Object.values(personA)); 
```

<br />

## 14. _Object.entries()_

> Returns an array of a given object's own enumerable string-keyed property [key, value] pairs.

``` js
  const entries = Object.entries(personA);

  console.log('Object.entries()', entries);
```

<br />

## 15. _Object.fromEntries()_

> The Object.fromEntries() method transforms a list of key-value pairs into an object.

``` js
  console.log('Object.fromEntries()', Object.fromEntries(entries));
```

<br />

## 16. _Object.assign()_

> The Object.assign() method copies all enumerable own properties from one or more source objects to a target object. It returns the modified target object.

``` js
  const tempPersonA = Object.assign({}, personA);

  console.log('Object.assign', tempPersonA); // Property firstname is not copied as it is not enumerable.
```

``` js
  console.log('personB', personB);
  const tempPersonB = Object.assign({}, personB);
  console.log('Object.assign', tempPersonB);
```

<br />

## 17. _Object.prototype.propertyIsEnumerable()_

> The propertyIsEnumerable() method returns a Boolean indicating whether the specified property is enumerable and is the object's own property.

``` js
  console.log(personA.propertyIsEnumerable('firstname'));
  console.log(personA.propertyIsEnumerable('lastname'));
```

``` js
  const array = [
    'This is first string',
    'This is second string'
  ];
  console.log(Object.getOwnPropertyDescriptors(array));
  console.log(array.propertyIsEnumerable(0));
  console.log(array.propertyIsEnumerable('length'));
```

<br />

## 18. _Object.setPrototypeOf()_

> The Object.setPrototypeOf() method sets the prototype (i.e., the internal [[Prototype]] property) of a specified object to another object or null.

> Object.setPrototypeOf() is in the ECMAScript 2015 specification. It is generally considered the proper way to set the prototype of an object, vs. the more controversial Object.prototype.**proto** property.

``` js
  const personD = {};
  console.log(Object.setPrototypeOf(personD, {value: 10}));
  console.log(Object.getPrototypeOf(personD));
```

<br />
