# I was wrong about unit tests

- what I thought they were
- how I get value out of them
- one of the best times to write unit tests: when you know there's a bug.  Write the failing test first, then fix the code so that the test passes.

For years, I wrote widely-used business software without knowing what a unit test was.  All I knew was that they were magical tools that guaranteed that your software didn't have any mistakes in it.

This sounded pretty awesome, since the software I worked on often produced errors.  I had no idea how testing would work, since our user interface code had a ton business logic baked in - testing our software meant opening the app and clicking on things.

I think I googled "C++ tests" once, which taught me that unit tests require big test frameworks that bring a ton of environment with them.  This knowledge put tests clearly in the "never going to be worth the investment" category.  Better to focus on making the code simple than to dive into the deep pool of tests.

Thankfully, I was wrong.

It turns out you don't need a test framework at all, all you need is an "assert" function that throws an error if you make a false assertion.

You don't need to think about testing your application, or a whole screen - just write tests a function at a time.

To get started, make a new file with a "main" function, import the file with the class or function you want to test, create some dummy data to pass to the function, and then write a single "assert" call that asserts that the function returned the value that you expected.

If you run that file and it finishes successfully, your test passed.  If it throws an error, the test failed.

That's it, that's a real test!  Everything else is just fanciness.

It's important to remember that no matter how advanced your testing setup is, good unit tests will still follow this same pattern - you set up your initial data, you call the function or method that you're testing, and you assert that the output is reasonable.  Define inputs, assert expected outputs.  That's it.

Now, taking the time to write that test file will almost certainly feel less easy than launching your app and tracing through it to debug it, but it has two huge advantages that make it pay off.

First if you write a couple of these tests, you can test multiple complicated flows at once by re-running your tests, which means you can iterate toward the fix quicker than if you were launching your whole app every few minutes and running through two or three different flows.

Second, if you save these tests to your codebase, they can help you guarantee that nobody will accidentally introduce the same bug again.

Of course, that's only likely to happen if people actually run the tests in the future.  The only way to enforce that practically is if you can run all of the tests at once with a single command.

This is one of those bits of fanciness that people use test frameworks for, but even here, you can use a simple homemade version and get most of the value.

If a 20-line shell script that compiles and executes all filenames in your directory structure that end in "test" turns out to be less intimidating to your team than pulling in your community's favorite test framework, that's totally fine.

Once you've gotten that far, the next step is to run the tests automatically at important times, like right before doing a production build, or in pre-commit hooks, or whenever you push to the master repository.

This is what I wish I would have been told ten years ago.  Tests don't need a big framework or days of re-architecting the build.

Even if you don't add any automation at all when getting started, sometimes when you're tracking down a nasty bug in the accounting code, a couple test functions with assert calls is just what you need.
