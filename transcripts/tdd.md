# Don't feel guilty about not using test-driven-development

People get all crazy about TDD because it works

TDD leaves very little room for bugs to sneak in

TDD gives you a bunch of tests that cover lots and lots of cases

Most devs want to get their idea into code

I often want to take big-jump refactors that I think are justified, and I don't want to enumerate every step

Many of the libraries I write tests for just don't deserve the extra time

TDD provides value, but not nearly as much value as just writing one or two tests.  So, don't let TDD scare you away from writing tests, or make you feel guilty for only having a couple tests.

Whatever you do: WRITE AT LEAST ONE TEST BEFORE YOU WRITE ANY CODE.

As long as you have one single test doing the most basic dumb thing, you're guaranteeing that your architecture is testable, and making it easy for you to write future tests.

When you need to write another test in a month to catch a bug, all you need to do is copy the first test and make some changes!

If a function with no tests is zero points, and a function written with test-driven development is a hundred points, a function with a single basic test is worth at least fifty points.

You can always write more tests for bugs, or before adding major functionality.  You don't need TDD, but you absolutely should write one single test before you start.
