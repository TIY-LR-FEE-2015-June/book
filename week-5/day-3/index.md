
### JS Concat

* When to use concat
* Order matters
* Source Maps - I don't want to see an error on line 20000!
  
    var tree = concat(tree, {
      outputFile: '/output.js',
      inputFiles: ['loader.js', '**/*']
    });

### Underscore.js

Many array functions were added as part of the Javascript language in the last few years in a specification called ES5.
Because of this older mobile browsers and IE don't implement all things.

To fill in these gaps and give a lot of conveniences, a library called Underscore was created.
Unlike other libraries Underscore doesn't change the `Array.prototype` object.
Instead it wraps arrays (similar to how jQuery wraps around HTML elements) and then that result will have all of the standard functions we just covered: `forEach`, `filter`, `map`, `reduce`, `all`, and more!


## Side Effects, Mutability, and such

