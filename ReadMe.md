1.What is a potential pitfall with using typeof `bar === "object"` to determine if bar is an object? How can this pitfall be avoided?
--
---->
  `typeof bar === "object"` is a used to check if bar is an object, but in JavaScript null is also considered an object!

Therefore, if we check null value it will gives true(not false) to the console:

	var bar = null;
	console.log(typeof bar === "object");  // logs true!
As long as one is aware of this, the problem can easily be avoided by also checking if bar is null:

	console.log((bar !== null) && (typeof bar === "object"));  // logs false

<hr>
2.What will the code below output to the console and why?
--
	(function(){
	  var a = b = 3;
	})();
	
	console.log("a defined? " + (typeof a !== 'undefined'));
	console.log("b defined? " + (typeof b !== 'undefined'));
	
----> It means:

		b = 3;
		var a = b;
as result output will be-

	  	a defined? false
	  	b defined? true
	  	
	  	
<hr>
3.What will the code below output to the console and why?
--
		var myObject = {
		    foo: "bar",
		    func: function() {
		        var self = this;
		        console.log("outer func:  this.foo = " + this.foo);
		        console.log("outer func:  self.foo = " + self.foo);
		        (function() {
		            console.log("inner func:  this.foo = " + this.foo);
		            console.log("inner func:  self.foo = " + self.foo);
		        }());
		    }
		};
		myObject.func();

----> console it will run following--

		outer func:  this.foo = bar
		outer func:  self.foo = bar
		inner func:  this.foo = undefined
		inner func:  self.foo = bar
		
In outer function, both `this` and `self` refer to `myObject` so both access `foo`.

In inner function, this no longer refers to `myObject`. As a result, `this.foo` is `undefined` in the inner function, whereas the reference to the local variable `self` remains in scope and is accessible there.

<hr>

4.What is the significance of, and reason for, wrapping the entire content of a JavaScript source file in a function block?
--
<hr>
5.What is the significance, and what are the benefits, of including `use strict` at the beginning of a JavaScript source file?
--
---->
to voluntarily enforce stricter parsing and error handling on your JavaScript code at runtime. Some of keys benefit using `use strict` are-

-Makes debugging easier.

-Disallows duplicate parameter values.

-Throws error on invalid usage of delete.

-Eliminates this coercion.

-Prevents accidental globals.

<hr>
6.Consider the two functions below. Will they both return the same thing? Why or why not?
--

	function foo1()
	{
	  return {
	      bar: "hello"
	  };
	}
	
	function foo2()
	{
	  return
	  {
	      bar: "hello"
	  };
	}

---->

	foo1() 
	{bar: 'hello'}bar: "hello"
	foo2() 
	undefined

The reason for this has to do with the fact that semicolons are technically optional in JavaScript. As a result, when the line containing the return statement is encountered in foo2(), a semicolon is automatically inserted immediately after the return statement.

No error is thrown since the remainder of the code is perfectly valid, even though it doesn’t ever get invoked or do anything.

<hr>

7.What will the code below output? Explain your answer.
--

	console.log(0.1 + 0.2);
	console.log(0.1 + 0.2 == 0.3);
	
----> It will returns-

	0.30000000000000004
	false
	
It might print out 0.3 and true, or it might not. Numbers in JavaScript are all treated with floating point precision, and as such, may not always yield the expected results.”

<hr>

8.In what order will the numbers 1-4 be logged to the console when the code below is executed? Why?
--

	(function() {
	    console.log(1); 
	    setTimeout(function(){console.log(2)}, 1000); 
	    setTimeout(function(){console.log(3)}, 0); 
	    console.log(4);
	})();
	
---->
The values will be logged in the following order:

	1
	4
	3
	2
	
1 and 4 are displayed first since they are logged by simple calls to console.log() without any delay.

2 is displayed after 3 because 2 is being logged after a delay of 1 second whereas 3 is being logged after a delay of 0 msecs.

4 is displayed before 3 even 3 has 0 msecs deley timeout its because 3 has a `setTimeout()` function which checks the event queue and processes pending events. since the call to console.log(3) is invoked via setTimeout, so it is slightly delayed.

<hr>

9.Write a simple function (less than 160 characters) that returns a boolean indicating whether or not a string is a palindrome.
--
---->
The following simple function will return true if str is a palindrome; otherwise, it returns false.

	function isPalindrome(str) {
	  str = str.replace(/\W/g, '').toLowerCase();
	  return (str == str.split('').reverse().join(''));
	}
	
<hr>

10.Write a sum method which will work properly when invoked using either syntax below.
--

	console.log(sum(2,3));   // Outputs 5
	console.log(sum(2)(3));  // Outputs 5
	
----> 
we can do with following ways;

		function sum(x, y) {
		  if (y !== undefined) {
		    return x + y;
		  } else {
		    return function(y) { 
		    return x + y; 
		    };
		  }
		}
	
<hr>	
11.Consider the following code snippet:
--

	for (var i = 0; i < 5; i++) {
	  var btn = document.createElement('button');
	  btn.appendChild(document.createTextNode('Button ' + i));
	  btn.addEventListener('click', function(){ console.log(i); });
	  document.body.appendChild(btn);
	}
	
What gets logged to the console when the user clicks on “Button 4” and why?
---->
it prints `<button>Button 4 </button>` in console.
No matter what button the user clicks the number 5 will always be logged to the console. This is because, at the point that the onclick method is invoked (for any of the buttons), the for loop has already completed and the variable i already has a value of 5.

<hr>

12.Assuming d is an “empty” object in scope, say:
--

	var d = {};
…what is accomplished using the following code?

	[ 'zebra', 'horse' ].forEach(function(k) {
	d[k] = undefined;
	});
	
---->

	d 
	{zebra: undefined, horse: undefined}
	
here d is an object where 'zebra' and 'horse' will be keys and with undefined values.

<hr>

13.What will the code below output to the console and why?
--

	var arr1 = "john".split('');
	var arr2 = arr1.reverse();
	var arr3 = "jones".split('');
	arr2.push(arr3);
	console.log("array 1: length=" + arr1.length + " last=" + arr1.slice(-1));
	console.log("array 2: length=" + arr2.length + " last=" + arr2.slice(-1));
	
---->
The output will be-
	"array 1: length=5 last=j,o,n,e,s"
	"array 2: length=5 last=j,o,n,e,s"
	
Calling an array object’s `reverse()` method doesn’t only return the array in reverse order, it also reverses the order of the array itself (i.e., in this case, arr1).

The `reverse()` method returns a reference to the array itself (i.e., in this case, arr1). As a result, `arr2` is simply a reference to (rather than a copy of) `arr1`. Therefore, when anything is done to `arr2` (i.e., when we invoke arr2.push(arr3);), `arr1` will be affected as well since `arr1` and `arr2` are simply references to the same object.

<hr>
14.What will the code below output to the console?
--
	console.log(1 +  "2" + "2");
	console.log(1 +  +"2" + "2");
	console.log(1 +  -"1" + "2");
	console.log(+"1" +  "1" + "2");
	console.log( "A" - "B" + "2");
	console.log( "A" - "B" + 2);
---->

The above code will output the following to the console:

	"122"
	"32"
	"02"
	"112"
	"NaN2"
	NaN
	
<hr>

15.The following recursive code will cause a stack overflow if the array list is too large. How can you fix this and still retain the recursive pattern?
--

	var list = readHugeList();
	
	var nextListItem = function() {
	    var item = list.pop();
	
	    if (item) {
	        // process the list item...
	        nextListItem();
	    }
	};

---->
The potential stack overflow can be avoided by modifying the nextListItem function as follows:

	var list = readHugeList();
	
	var nextListItem = function() {
	    var item = list.pop();
	
	    if (item) {
	        // process the list item...
	        setTimeout( nextListItem, 0);
	    }
	};

When `nextListItem` runs, if item is not `null`, the timeout function (`nextListItem`) is pushed to the event queue and the function exits, thereby leaving the call stack clear.

--
16.What is a “closure” in JavaScript? Provide an example.
--
	
	var globalVar = "xyz";

	(function outerFunc(outerArg) {
    var outerVar = 'a';
    
    (function innerFunc(innerArg) {
    var innerVar = 'b';
    
    console.log(
        "outerArg = " + outerArg + "\n" +
        "innerArg = " + innerArg + "\n" +
        "outerVar = " + outerVar + "\n" +
        "innerVar = " + innerVar + "\n" +
        "globalVar = " + globalVar);
    
    })(456);
	})(123);
	
---->
In the above example, variables from innerFunc, outerFunc, and the global namespace are all in scope in the innerFunc. The above code will therefore produce the following output:

	outerArg = 123
	innerArg = 456
	outerVar = a
	innerVar = b
	globalVar = xyz
	
<hr>

17.What would the following lines of code output to the console?
--
	console.log("0 || 1 = "+(0 || 1));
	console.log("1 || 2 = "+(1 || 2));
	console.log("0 && 1 = "+(0 && 1));
	console.log("1 && 2 = "+(1 && 2));
---->
The code will output the following four lines:

	0 || 1 = 1
	1 || 2 = 1
	0 && 1 = 0
	1 && 2 = 2
	
In JavaScript, both || and && are logical operators that return the first fully-determined “logical value” when evaluated from left to right.
<hr>

18.What will be the output when the following code is executed? Explain.
--
	console.log(false == '0')
	console.log(false === '0')
	console.log(5=='5')

---->
The code will output:

	true
	false
	true
here == is doesn't check type it just check the value.

<hr>
19.What is the output out of the following code? Explain your answer.
--

	var a={},
	    b={key:'b'},
	    c={key:'c'};
	
	a[b]=123;
	a[c]=456;
	
	console.log(a[b]);
	
---->
The output of this code will be 456 (not 123).

The reason for this is as follows: When setting an object property, JavaScript will implicitly stringify the parameter value. In this case, since b and c are both objects, they will both be converted to "[object Object]". As a result, a[b] anda[c] are both equivalent to a["[object Object]"] and can be used interchangeably. Therefore, setting or referencing a[c] is precisely the same as setting or referencing a[b].

<hr>

20.What will the following code output to the console:
--

	console.log((function f(n){return ((n > 1) ? n * f(n-1) : n)})(10));
	
---->

The code will output the value of 10 factorial (i.e., 10!, or 3,628,800).


The named function f() calls itself recursively, until it gets down to calling f(1) which simply returns 1. Here, therefore, is what this does:

	f(1): returns n, which is 1
	f(2): returns 2 * f(1), which is 2
	f(3): returns 3 * f(2), which is 6
	f(4): returns 4 * f(3), which is 24
	f(5): returns 5 * f(4), which is 120
	f(6): returns 6 * f(5), which is 720
	f(7): returns 7 * f(6), which is 5040
	f(8): returns 8 * f(7), which is 40320
	f(9): returns 9 * f(8), which is 362880
	f(10): returns 10 * f(9), which is 3628800
	
<hr>

21.Consider the code snippet below. What will the console output be and why?
--

	(function(x) {
	    return (function(y) {
	        console.log(x);
	    })(2)
	})(1);
---->
The output will be 1. x is not defined in the inner function, the scope of the outer function is searched for a defined variable x, which is found to have a value of 1.
<hr>

22.What will the following code output to the console and why? What is the issue with this code and how can it be fixed.
--

	var hero = {
	    _name: 'John Doe',
	    getSecretIdentity: function (){
	        return this._name;
	    }
	};
	
	var stoleSecretIdentity = hero.getSecretIdentity;
	
	console.log(stoleSecretIdentity());
	console.log(hero.getSecretIdentity());

The code will output:

	undefined
	John Doe
	
The first console.log prints undefined because we are extracting the method from the hero object, so stoleSecretIdentity() is being invoked in the global context (i.e., the window object) where the _name property does not exist.

One way to fix the stoleSecretIdentity() function is as follows:

	var stoleSecretIdentity = hero.getSecretIdentity.bind(hero);
<hr>

23.Create a function that, given a DOM Element on the page, will visit the element itself and all of its descendents (not just its immediate children). For each element visited, the function should pass that element to a provided callback function.

The arguments to the function should be:

a DOM element
a callback function (that takes a DOM element as its argument)
--
Visiting all elements in a tree (DOM) is a classic Depth-First-Search algorithm application. Here’s an example solution:

	function Traverse(p_element,p_callback) {
	   p_callback(p_element);
	   var list = p_element.children;
	   for (var i = 0; i < list.length; i++) {
	       Traverse(list[i],p_callback);  // recursive call
	   }
	}
	
24.Testing your this knowledge in JavaScript: What is the output of the following code?
--

	var length = 10;
	function fn() {
		console.log(this.length);
	}
	
	var obj = {
	  length: 5,
	  method: function(fn) {
	    fn();
	    arguments[0]();
	  }
	};
	
	obj.method(fn, 1);
	
---->

	Output:
	
	10
	2
<hr>

25.Consider the following code. What will the output be, and why?
--

	(function () {
	    try {
	        throw new Error();
	    } catch (x) {
	        var x = 1, y = 2;
	        console.log(x);
	    }
	    console.log(x);
	    console.log(y);
	})();
---->

	1
	undefined
	2
<hr>
26.What will be the output of this code?
--

	var x = 21;
	var girl = function () {
	    console.log(x);
	    var x = 20;
	};
	girl ();
	
---->
Neither 21, nor 20, the result is undefined
<hr>
27.

	for (let i = 0; i < 5; i++) {
  	setTimeout(function() { console.log(i); }, i * 1000 );
	}
	
What will this code print?
--
---->
It will print 0 1 2 3 4, because we use let instead of var here. The variable i is only seen in the for loop’s block scope.
<hr>

28.What do the following lines output, and why?

	console.log(1 < 2 < 3);
	console.log(3 > 2 > 1);
	
---->

	true
	false
	
The first statement returns true which is as expected.

The second returns false because of how the engine works regarding operator associativity for < and >. It compares left to right, so 3 > 2 > 1 JavaScript translates to true > 1. true has value 1, so it then compares 1 > 1, which is false.

<hr>
29.How do you add an element at the begining of an array? How do you add one at the end?

	var myArray = ['a', 'b', 'c', 'd'];
	myArray.push('end');
	myArray.unshift('start');
	console.log(myArray); // ["start", "a", "b", "c", "d", "end"]

---->

	myArray = ['start', ...myArray, 'end'];
	
<hr>
<b>
30.Imagine you have this code:

`var a = [1, 2, 3];`

a) Will this result in a crash?

`a[10] = 99;`

b) What will this output?

`console.log(a[6]);`

</b>
---->

a) It will not crash. The JavaScript engine will make array slots 3 through 9 be “empty slots.”

b) Here, a[6] will output undefined, but the slot still remains empty rather than filled with undefined. This may be an important nuance in some cases. For example, when using map(), empty slots will remain empty in map()’s output, but undefined slots will be remapped using the function passed to it:

	var b = [undefined];
	b[2] = 1;
	console.log(b);             // (3) [undefined, empty × 1, 1]
	console.log(b.map(e => 7)); // (3) [7,         empty × 1, 7]
	
<hr>
32.What is the value of `typeof undefined == typeof NULL`?
---->
The expression will be evaluated to true, since NULL will be treated as any other undefined variable.

Note: JavaScript is case-sensitive and here we are using NULL instead of null.

<hr>
33.What would following code return?
--
`console.log(typeof typeof 1);`

---->
`string`

`typeof 1` will return `"number"` and typeof `"number"` will return `string`.
<hr>

34.What will be the output of the following code:
--

	for (var i = 0; i < 5; i++) {
		setTimeout(function() { console.log(i); }, i * 1000 );
	}
--->

The code sample shown will not display the values 0, 1, 2, 3, and 4 as might be expected; rather, it will display 5, 5, 5, 5, and 5.

<hr>

35.What is NaN? What is its type? How can you reliably test if a value is equal to NaN?
--
---->
The NaN property represents a value that is “not a number”. 
For one thing, although NaN means “not a number”, its type is, believe it or not, Number:

	console.log(typeof NaN === "number");  // logs "true"
Additionally, NaN compared to anything – even itself! – is false:

	console.log(NaN === NaN);  // logs "false"
	
<hr>

36.What will the following code output and why?

	var b = 1;
	function outer(){
	   	var b = 2
	    function inner(){
	        b++;
	        var b = 3;
	        console.log(b)
	    }
	    inner();
	}
	outer();
---->
Output to the console will be “3”.

There are three closures in the example, each with it’s own `var b ` declaration. When a variable is invoked closures will be checked in order from local to global until an instance is found. Since the inner closure has a `b` variable of its own, that is what will be output.

eg. for clear view;

	function inner () {
	    var b; // b is undefined
	    b++; // b is NaN
	    b = 3; // b is 3
	    console.log(b); // output "3"
	}
	
<hr>

37.Discuss possible ways to write a function isInteger(x) that determines if x is an integer.
--
---->

`function isInteger(x) { return (x ^ 0) === x; }`

	
`function isInteger(x) { return (typeof x === 'number') && (x % 1 === 0); }`

`function isInteger(x) { return Math.round(x) === x; }`

`function isInteger(x) { return parseInt(x, 10) === x; }`
<hr>

38.How do you clone an object?
--
---->

	var obj = {a: 1 ,b: 2}
	var objclone = Object.assign({},obj);

Now the value of objclone is {a: 1 ,b: 2} but points to a different object than obj.

Object.assign() will just do a shallow copy, not a deep copy. This means that nested objects aren’t copied. They still refer to the same nested objects as the original:

	let obj = {
	    a: 1,
	    b: 2,
	    c: {
	        age: 30
	    }
	};

	var objclone = Object.assign({},obj);
	console.log('objclone: ', objclone);

	obj.c.age = 45;
	console.log('After Change - obj: ', obj);           // 45 - This also changes
	console.log('After Change - objclone: ', objclone); // 45