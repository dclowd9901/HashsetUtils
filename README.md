HashsetUtils
============

_.intersect() for complex objects


When to use
===========
You should use this library any time you want to 
- Quickly compare lots of complex objects
- Do those comparisons between multiple collections

How to use
==========
First, load the library:
```
// require.js
var HashsetUtils = require('HashsetUtils');

// amd
define([
  'HashsetUtils'
], function (HashsetUtils) {

});
```

Then use:
```
HashsetUtils.intersection(hashFunction, obj1, obj2, obj3...);
var myHashSet = new HashsetUtils.HashSet();
```

What's a hash function?
=======================
When this library creates a hashset, it's using a function on each value of your arrays 
that is tied to its uniqueness, like any other hashing function you've ever used (MD5, for instance).

Why do we have you give one? Because:
- Javascript doesn't have a native one.
- Some common hashing algorithms might provide collisionary values.
- You know what you want to compare, so your algorithm is going to be the best one for your case. You have complete control
over the comparison of your objects.

Let's say we have two arrays of objects:
```
var arr1 = [{
  foo: '1',
  bar: '2',
  baz: '3'
},
{
  foo: '4',
  bar: '5', 
  baz: '6'
}];

var arr2 = [{
  foo: '33',
  bar: '25',
  baz: '66'
},
{
  foo: '1',
  bar: '2', 
  baz: '3'
}];
```
You want to find the intersection of objects in arr1 with objects in arr2. And intersect() method seems ideal, but LoDash
and Underscore's are inadequate, as they only do a === comparison, which won't work for two objects with differing references.

So when we run the intersect method, we also provide it a way to create a comparable hash for intersecting objects:
```
HashsetUtils.intersect(function(object){
  return '' + object.foo + object.bar + object.baz;
}, arr1, arr2);
```
The hash function is provided a singular argument, which is one object from the arrays you're comparing. So, 
with the above hashing function, the resulting hashset for arr1 would look like this:
```
{
  '123': arr1[0], // for brevity, we're just denoting the reference
  '456': arr1[1]
}
```
So, you see, the resulting hashset should be a result of the property values we are most eager to compare, and because
we have that freedom, hashing objects for comparison can be blazing fast. 

Just for further illustrate, arr2's hashset would look like this:
```
{
  '332566': arr2[0],
  '123': arr2[1]
}
```

Contributing
============
If you care to contribute, fork and pull request, and I'll be happy to add it if it's contributive functionality.

