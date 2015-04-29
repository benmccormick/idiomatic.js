# Windsor Circle JavaScript Style Guide

### This document is based on [Idiomatic.js](https://github.com/rwaldron/idiomatic.js).  You can find the original source on Github, including a list of contributors and many additional resources.

## Principles

- All code in any code-base should look like a single person typed it, no matter how many people contributed.
- If there is a disagreement over style, it should be argued at the level of changing this guide, not through writing incompatible code
- Generally, decisions that do not effect readability or encourage mistakes should default to the current state
- Code is read many more times than written.  Following conventions encourages readability

## Practices

- Code Style should be enforced through tools.  We use jsHint to test our ES5 code and ESLint to test our ES6 code.  You should use an editor plugin to see tool feedback as you type, and all code reviewed code should pass style checking without warnings before being approved.  We use EditorConfig to enforce consistent whitespace.
- Part of writing good code is testing. All new code written should include unit tests that meaningfully test the codes behavior.  Note that the goal of Unit Testing is to ensure certain behaviors, and testing should be strucuture agnostic as much as is feasible.


## Table of Contents

 * [Whitespace](#whitespace)
 * [Beautiful Syntax](#spacing)
 * [Type Checking (Courtesy jQuery Core Style Guidelines)](#type)
 * [Conditional Evaluation](#cond)
 * [Naming](#naming)
 * [Comments](#comments)
 * [Backbone & Other Libraries](#backbone)
 * [ES6](#es6)
 * [ES5](#es5)
 * [Miscellaneous Style](#misc)


------------------------------------------------

## Windsor Circle JavaScript Style Guidelines


1. <a name="whitespace">Whitespace</a>
  - Always indent using 4 spaces (not tabs)
  - If your editor supports it, always work with the "show invisibles" setting turned on. The benefits of this practice are:
      - Enforced consistency
      - Eliminating end of line whitespace
      - Eliminating blank line whitespace
      - Commits and diffs that are easier to read
  - Use [Editorconfig](http://editorconfig.org/).  It supports most IDEs and handles most whitespace settings.


2. <a name="spacing">Beautiful Syntax</a>

    A. Parens, Braces, Linebreaks

    ```javascript

    // if/else/for/while/try always have spaces, braces and span multiple lines
    // this encourages readability

    // 2.A.1.1
    // Examples of really cramped syntax

    if(condition) doSomething();

    while(condition) iterating++;

    for(var i=0;i<100;i++) someIterativeFn();


    // 2.A.1.1
    // Always use brackets for block statements and include a space 
    // after the condition before the first bracket

    if (condition) {
      // statements
    }

    while (condition) {
      // statements
    }

    for (var i = 0; i < 100; i++) {
      // statements
    }

    ```


    B. Assignments, Declarations, Functions ( Named, Expression, Constructor )

    ```javascript

    // 2.B.1.1
    // Variables
    var foo = "bar",
      num = 1,
      undef;

    // Literal notations:
    var array = [],
      object = {};


    // 2.B.1.2
    // Using only one `var` per scope (function) promotes readability
    // and keeps your declaration list free of clutter (also saves a few keystrokes)

    // Bad
    var foo = "";
    var bar = "";
    var qux;

    // Good
    var foo = "",
      bar = "",
      qux;

    // or..
    var // Comment on these
    foo = "",
    bar = "",
    quux;

    // 2.B.1.3
    // var statements should always be in the beginning of their respective scope (function).


    // Bad
    function foo() {

      // some statements here

      var bar = "",
        qux;
    }

    // Good
    function foo() {
      var bar = "",
        qux;

      // all statements after the variables declarations.
    }

    // 2.B.1.4
    // const and let, from ECMAScript 6, should likewise be at the top of their scope (block).

    // Bad
    function foo() {
      let foo,
        bar;
      if(condition) {
        bar = "";
        // statements
      }
    }
    // Good
    function foo() {
      let foo;
      if(condition) {
        let bar = "";
        // statements
      }
    }
    ```

    ```javascript

    // 2.B.2.1
    // Named Function Declaration
    function foo(arg1, argN) {

    }

    // Usage
    foo(arg1, argN);


    // 2.B.2.2
    // Named Function Declaration
    function square(number) {
      return number * number;
    }

    // Usage
    square( 10 );

    // Really contrived continuation passing style
    function square(number, callback) {
      callback(number * number);
    }

    square(10, function(square) {
      // callback statements
    });


    // 2.B.2.3
    // Function Expression
    var square = function(number) {
      // Return something valuable and relevant
      return number * number;
    };

    // Function Expression with Identifier
    // This preferred form has the added value of being
    // able to call itself and have an identity in stack traces:
    var factorial = function factorial(number) {
      if(number < 2) {
        return 1;
      }

      return number * factorial( number - 1 );
    };


    // 2.B.2.4
    // Constructor Declaration
    function FooBar( options ) {

      this.options = options;
    }

    // Usage
    var fooBar = new FooBar({ a: "alpha" });

    fooBar.options;
    // { a: "alpha" }

    ```

    E. Quotes

    Use single quotes.  For multiline strings or when concatenating variables, you can also use the ES6 backticks string syntax.

    F. End of Lines and Empty Lines

    Whitespace can ruin diffs and make changesets impossible to read. Set your editor to remove trailing whitespace and newline whitespace
    automatically.

3. <a name="type">Type Checking (Courtesy jQuery Core Style Guidelines)</a>

    A. Actual Types

    String:

        _.isString(variable)

    Number:

        _.isNumber(variable) //includes Infinity, -Infinity and NaN or
        _.isFinite(variable)

    Boolean:

        _.isBoolean(variable)

    Object:

        _.isObject(variable)

    Array:

        _.isArray(variable)

    null:

        variable === null

    null or undefined:

        variable == null

    undefined:

      Global Variables:

        typeof variable === "undefined"

      Local Variables:

        variable === undefined

      Properties:

        object.prop === undefined
        object.hasOwnProperty( prop )
        "prop" in object

    B. Coerced Types


    ```javascript

    // 3.B.1.1

    var number = 1,
      string = "1",
      bool = true;

    //to convert from a string to a number

    number === +string  //true

    //to convert from a number to a string

    string === "" + number //true

    //to convert from a string or a number to a boolean

    bool === !!number //true
    bool === !!string //true
    ```


    ```javascript
    // 3.B.1.2

    //to convert to an integer

    var num = 2.5;

    parseInt(num, 10); // 2
    ```



4. <a name="cond">Conditional Evaluation</a>

    ```javascript

    // 4.1.1
    // When only evaluating that an array has length,
    // instead of this:
    if (array.length > 0) ...

    // ...evaluate truthiness, like this:
    if (array.length) ...


    // 4.1.2
    // When only evaluating that an array is empty,
    // instead of this:
    if (array.length === 0) ...

    // ...evaluate truthiness, like this:
    if (!array.length) ...


    // 4.1.3
    // When only evaluating that a string is not empty,
    // instead of this:
    if (string !== "") ...

    // ...evaluate truthiness, like this:
    if (string) ...


    // 4.1.4
    // When only evaluating that a string _is_ empty,
    // instead of this:
    if (string === "") ...

    // ...evaluate falsy-ness, like this:
    if (!string) ...


    // 4.1.5
    // When only evaluating that a reference is true,
    // instead of this:
    if (foo === true) ...

    // take advantage of built in capabilities:
    if (foo) ...


    // 4.1.6
    // When evaluating that a reference is false,
    // instead of this:
    if (foo === false) ...

    // ...use negation to coerce a true evaluation
    if (!foo) ...

    // ...Be careful, this will also match: 0, "", null, undefined, NaN
    // If you _MUST_ test for a boolean false, then use
    if (foo === false) ...
    ```
    ALWAYS evaluate for the best, most accurate result - the above is a guideline, not a dogma.

    ```javascript

    // 4.2.1
    // Type coercion and evaluation notes

    // Use `===` and not `==` 

    // === does not coerce type, which means that:

    "1" === 1;
    // false

    // == does coerce type, which means that:

    "1" == 1;
    // true

    // Switching between == and === can be confusing and leads to subtle bugs
    // Always use ===


    // 4.2.2
    // Booleans, Truthies & Falsies

    // Booleans:
    true, false

    // Truthy:
    "foo", 1

    // Falsy:
    "", 0, null, undefined, NaN, void 0

    ```


5. <a name="naming">Naming</a>



    A. You are not a human code compiler/compressor, so don't try to be one.

    The following code is an example of egregious naming:

    ```javascript

    // 6.A.1.1
    // Example of code with poor names

    function q(s) {
      return document.querySelectorAll(s);
    }
    var i,a=[],els=q("#foo");
    for(i=0;i<els.length;i++){a.push(els[i]);}
    ```

    Don't do that :)

    Here's the same piece of logic, but with kinder, more thoughtful naming (and a readable structure):

    ```javascript

    // 6.A.2.1
    // Example of code with improved names

    function query( selector ) {
      return document.querySelectorAll( selector );
    }

    var idx = 0,
      elements = [],
      matches = query("#foo"),
      length = matches.length;

    for ( ; idx < length; idx++ ) {
      elements.push( matches[ idx ] );
    }

    ```

    A few additional naming pointers:

    ```javascript

    // 6.A.3.1
    // Naming strings

    `dog` is a string


    // 6.A.3.2
    // Naming arrays

    `dogs` is an array of `dog` strings


    // 6.A.3.3
    // Naming functions, objects, instances, etc

    camelCase; function and var declarations


    // 6.A.3.4
    // Naming constructors, prototypes, etc.

    PascalCase; constructor function

    // 6.A.3.5
    // From the Google Closure Library Style Guide

    functionNamesLikeThis;
    variableNamesLikeThis;
    ConstructorNamesLikeThis;
    EnumNamesLikeThis;
    methodNamesLikeThis;
    SYMBOLIC_CONSTANTS_LIKE_THIS;
    ```

    B. Faces of `this`

    Beyond the generally well known use cases of `call` and `apply`, always prefer `.bind(this)` or a functional equivalent, for creating `BoundFunction` definitions for later invocation. Only resort to aliasing when no preferable option is available. When using ES6 code, use `()=>{}` functions when possible instead of bind(this).  Those functions should only be used when you specifically want to capture the outer context.

    ```javascript

    // 6.B.1
    function Device( opts ) {

      this.value = null;

      // open an async stream,
      // this will be called continuously
      stream.read( opts.path, function( data ) {

        // Update this instance's current value
        // with the most recent value from the
        // data stream
        this.value = data;

      }.bind(this) );

      // Throttle the frequency of events emitted from
      // this Device instance
      setInterval(function() {

        // Emit a throttled event
        this.emit("event");

      }.bind(this), opts.freq || 100 );
    }

    // Just pretend we've inherited EventEmitter ;)

    ```



    ```javascript
    // 6.B.2

    //In ES6 use () => {} rather than bind(this) when creating an anonymous function
    setInterval(() => {
        // Emit a throttled event
        this.emit("event");
    }, opts.freq || 100 );

    //Don't use () => just to abbreviate.  It should have a connotation that you're changing the scope

    //Bad:
    setInterval( () => {
        foo();
        bar();
    }, 300);
    ```

    As a last resort, create an alias to `this` using `self` as an Identifier. This is extremely bug prone and should be avoided whenever possible.

    ```javascript

    // 6.B.3

    function Device( opts ) {
      var self = this;

      this.value = null;

      stream.read( opts.path, function( data ) {

        self.value = data;

      });

      setInterval(function() {

        self.emit("event");

      }, opts.freq || 100 );
    }

    ```


    C. Use `thisArg`

    Several prototype methods of ES 5.1 built-ins come with a special `thisArg` signature, which should be used whenever possible

    ```javascript

    // 6.C.1

    var obj;

    obj = { f: "foo", b: "bar", q: "qux" };

    Object.keys( obj ).forEach(function( key ) {

      // |this| now refers to `obj`

      console.log( this[ key ] );

    }, obj ); // <-- the last arg is `thisArg`

    // Prints...

    // "foo"
    // "bar"
    // "qux"

    ```

    `thisArg` can be used with `Array.prototype.every`, `Array.prototype.forEach`, `Array.prototype.some`, `Array.prototype.map`, `Array.prototype.filter`
    Many LoDash and Backbone functions also allow specifying a `thisArg`



7. <a name="comments">Comments</a>

    A. Style

    - Single line above the code that is subject
    -  Multiline is good too
    - Avoid end of line comments

    B. Content

    - Focus on explaining why the code exists, not what it is doing
    - Comments should be code reviewed too!


8. <a name="backbone">Backbone Style</a>

    A. Base Classes

    - Always use Marionette Base Classes For Views
    - Don't Use multiple levels of inheritance.  Views should inherit from Marionette Classes (Views, Behaviors, Applications), or Backbone Classes (Models, Collections, Routers).  Shared code should use behaviors (Views), composition (multiple small Views/Web Components) or a mixin library (Models/Collections)
    
    B. jQuery and View Scope

    - Views should never modify DOM elements outside the scope of their root element
    - Views should never modify DOM elements inside child Views, they may sometimes need to read these elements directly
    - Global jQuery should never be used within a View, instead view.$ or view.$el should be used
    - As Much as possible view content should be rendered within the render function, rather than through direct DOM manipulation or jQuery plugins
    - jQuery plugins should be encapsualated within a custom element if possible

    C. Separation of Concerns
    
    - View code should never be directly concerned with loading data.  That should be delegated to a model.  There are bad examples of this in our code that should not be copied
    - Model code should not be directly concerned with formatting.  Single case formatting should be handled by a View (template helpers) General case formatting should be pulled into a utility class, or a custom element

    D. View Communication
    
    - Views should never be directly aware of any other views, except for their own child views
    - Communication between views can occur in 3 ways:
        1. Listening to changes on a shared Data object
        2. Listening to events on a child View
        3. Listing to events/commands/requests on a Backbone.Radio channel

    E. View Rendering
    
    - For every `Marionette.Application` there should be a single rootView, attached to the applciation as the rootView property
    - That View should never be rendered, but instead declare regions on existing DOM elements and show childViews on initialization
    - Below that root level, every View should be rendered using showChildView (ideally in the onBeforeShow callback of a parents view), or as part of a collectionView
    
    F. Property Ordering
    
    - For Backbone Views and Behaviors properties and methods should go in the following order: declarative properties (template, className, events, etc), template related functions (serializeData, templateHelpers), lifecycle methods in order of occurrence (initialize, onBeforeRender/Attach/Show, onRender/Attach/Show, onBeforeDestroy, onDestroy), any helper methods
    - For Models, Applications, Routers, etc follow a similar convention of putting declarative datas and rules on top, Library method overrides next, and custom helper functions at the bottom

    G. Services

    - For common resources or utilities, consider defining a Service object that can be interacted with via radio requests
    - Services should be single purpose and focused on abstracting common system operations (logging, data retrieval, displaying toaster messages)

    H. Misc Library rules

    - When possible, use LoDash for common operations rather than rolling your own helpers
    - For working with dates always use Moment rather than built in JavaScript dates


9. <a name="es6">ES6 Style</a>

    A. Modules
    
    - All ES6 code should use the ES6 module style
    - stick to a single export from each file

    B. Classes

    - Don't use Classes with Mn/Backbone objects until there's a better story for handling data properties

    C. let/const

    - Always prefer let to var when using ES6 code.  Const is encouraged for variables that should not change

    D. ()=>

    - As previously stated, use fat arrow functions only when they carry functional purpose, don't use them just to abbreviate
    - They are encouraged over function(){}.bind(this) when useful in that way though

10. <a name="es5">ES5 Style </a>

    A. Modules

    - All ES5 code should use AMD modules
    - if an AMD module holds 3 or more dependencies, they should be listed on separate lines
    - the first line of every module should be ``'use strict';` You can learn more about [strict mode here](http://www.nczonline.net/blog/2012/03/13/its-time-to-start-using-javascript-strict-mode/).  ES6 modules are in strict mode by default
    
    B. Deprecated

    - All new code should be written in the ES6 style
    - If you're making significant changes to an ES5 style, consider taking the time to convert it to an ES6 file.  Note that this will require adding tests and passing automated style checking

11. <a name="misc">Miscellaneous Style</a>

    A. Length preferences
    
    - Prefer short lines, short functions, short modules and short files
    - Keep lines under 100 characters as a hard limit, prefer shorter as possible
    - Avoid deep nested indentation by moving inner behavior into helper functions
    - We don't currently enforce a hard limit on files, but once a file is larger than 200 lines, its probably time to start considering opportunities to split it or refactor
    - Similarly we don't enforce a hard limit on functions but if a function does not easily fit within your editor screen, consider splitting it
    
    B. Code Flow
    
    - When code captures a complex workflow (a function that performs more than one step), consider breaking it up into multiple functions
    - When breaking a workflow into multiple functions, the top level control function should sit at the top of the module (or higher than its related functions), and the related functions should fall beneath that
    - When using this style it's very important to give functions meaningful names that describe their function.  If this is hard it's possibly a sign that the functions can be split up further.
    
----------


<a rel="license" href="http://creativecommons.org/licenses/by/3.0/deed.en_US"><img alt="Creative Commons License" style="border-width:0" src="http://i.creativecommons.org/l/by/3.0/80x15.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">Principles of Writing Consistent, Idiomatic JavaScript</span> by <a xmlns:cc="http://creativecommons.org/ns#" href="https://github.com/rwldrn/idiomatic.js" property="cc:attributionName" rel="cc:attributionURL">Rick Waldron and Contributors</a> is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by/3.0/deed.en_US">Creative Commons Attribution 3.0 Unported License</a>.<br />Based on a work at <a xmlns:dct="http://purl.org/dc/terms/" href="https://github.com/rwldrn/idiomatic.js" rel="dct:source">github.com/rwldrn/idiomatic.js</a>.
