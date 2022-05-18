1.What is a potential pitfall with using typeof `bar === "object"` to determine if bar is an object? How can this pitfall be avoided?

---->
  `typeof bar === "object"` is a used to check if bar is an object, but in JavaScript null is also considered an object!

Therefore, if we check null value it will gives true(not false) to the console:

	var bar = null;
	console.log(typeof bar === "object");  // logs true!
As long as one is aware of this, the problem can easily be avoided by also checking if bar is null:

	console.log((bar !== null) && (typeof bar === "object"));  // logs false

<hr>
2.What will the code below output to the console and why?

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

<hr>
5.What is the significance, and what are the benefits, of including `use strict` at the beginning of a JavaScript source file?

---->
to voluntarily enforce stricter parsing and error handling on your JavaScript code at runtime. Some of keys benefit using `use strict` are-

-Makes debugging easier.

-Disallows duplicate parameter values.

-Throws error on invalid usage of delete.

-Eliminates this coercion.

-Prevents accidental globals.

<hr>
6.Consider the two functions below. Will they both return the same thing? Why or why not?

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

	console.log(0.1 + 0.2);
	console.log(0.1 + 0.2 == 0.3);
	
----> It will returns-

	0.30000000000000004
	false
	
It might print out 0.3 and true, or it might not. Numbers in JavaScript are all treated with floating point precision, and as such, may not always yield the expected results.”

<hr>

8.In what order will the numbers 1-4 be logged to the console when the code below is executed? Why?

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

---->
The following simple function will return true if str is a palindrome; otherwise, it returns false.

	function isPalindrome(str) {
	  str = str.replace(/\W/g, '').toLowerCase();
	  return (str == str.split('').reverse().join(''));
	}
