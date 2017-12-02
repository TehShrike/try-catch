# The programming language with the best ever elevator pitch

Elm has the best elevator pitch of any programming language: if you use Elm, you will have no run-time errors, ever.  If your code compiles, there will not be any exceptions thrown while the code is running.

If you're a person who writes code, this probably sounds crazy.  If it were possible to *not* throw errors, why wouldn't every language just do that?

Class-based type systems like in Java and C++ will catch certain sorts of errors when you compile - if you're trying to pass an invoice to a function that expects a customer, the compiler will poke you until you fix it.

But the compiler won't save you if you call some third-party library that decides to return a null invoice, or if you try to access an array element that doesn't exist.  All the major programming languages have ways to make unchecked exceptions occur while your program is running.

This makes Elm's claim sound unrealistically fantastic, but it gets more believable if you stare at it a while.

Elm is designed to be statically analyzed.  This means that you can parse the code and know quite a bit about what it does without having to actually run it.

Elm is also very particular about its types - if you have a function that can return a string or a number, you have to declare a new "String or Integer" type for your function to return.  And, importantly, the Elm compiler won't give your program the thumbs up unless you have code that handles both the String and Integer cases in every place where you call that function.

If it is possible for a function to have an error, like getting a HTTP error when you try to talk to your server, then that function returns a "result" type that can be either an error or a value.  The compiler won't let you interact with the result's value without also handling the possible error state somewhere.

I still haven't used Elm in a project yet, though I hope to some day.  I think it's worth taking a look at even if you don't use it, just to raise our expectations of what compilers should be doing for us.
