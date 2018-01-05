# Bad math in cash register software

My first job was working on the point-of-sale software that cashiers use to ring up stuff that you buy in a store.

It's very important that cash registers do correct arithmetic: totals should always add up to the same amount.  Taxes should be calculated consistently.

When I started working on the project as a fresh-faced optimistic noobie, all the arithmetic was done using floating point numbers, which are an efficient way for processors to work with fractional numbers with lots of digits after the decimal point.

But there's a catch: floating point numbers don't guarantee precision.  They can cram any number into 4 or 8 bytes as a multiple of a couple other numbers, but sometimes the numbers are only really close to the desired value, instead of exactly the value you put in.  This comes up especially after doing a few arithmetic calculations.

I didn't see any problems with this when I started.

One day, I got a support call from a client having a weird issue: an old invoice would show up as having an unpaid balance of one cent on one of their computers, but on every other computer, it showed as being paid in full.

Every computer I tested on, including mine, would come up with the same invoice total for those lineitems, but that one computer would calculate the sales tax one cent off.

There wasn't any bug in our code, except for the fact that we were using floating point arithmetic.  Our best guess was that one computer's processor would come up with a different floating point representation of the tax amount that would get rounded differently when we trimmed the number to two digits after the decimal point.

That was disconcerting.

A while after that, I ran into another case that I could reproduce reliably on my machine.  It wasn't even a very strange edge case - with a fractional quantity of something, the tax rate would come out to a dollar fifty-five.  But our software didn't show a dollar fifty-five, it showed a dollar fifty-six.

Under the hood, after doing the multiplication using floating point arithmetic, the tax rate was being calculated to come out to one point five five zero zero zero zero zero zero zero zero zero zero zero one dollars, which we would then round to a dollar fifty six.

I started to scheme up a series of multiplying and dividing steps that would solve the issue, but it turns out there's no way you can precisely correct for imprecise arithmetic.  Eventually I realized an important fact: you should never, ever use floating point numbers to represent money values.  Not even double precision floating point numbers.

There are number data types that will do arithmetic without any loss in precision.  Some programming languages even provide them as a core library.  They're usually called "big number" or "big integer" or "arbitrary precision" libraries.  As long as you store your numbers in the database with a fixed-point type, like MySQL's "decimal" type, and you only ever represent the numbers in your code with one of these arbitrary precision number libraries, then you're good - you won't lose pennies because of floating point arithmetic.

It's easy to make this mistake if you don't know about it, because in almost every programming language, if you type a number with a decimal point into your editor, it will be represented in code as a floating point value.  It's natural to assume that this must be the best way to represent fractional dollars, even though it's not.

Storing money values as floating point numbers is actually a specific case of a really common mistake that people make all the time, which is to use data structures that aren't appropriate for what they're storing.

You'll see this often when people put items into an array and then iterate over the array to find items by a key, when they should be using some kind of hash map.  Or when people try to cram multiple values into a single column in a relational database.

People will sometimes do this because they don't know there's a better way to represent their data, but a lot of the time they'll just do it because it seems easier at the time.  But it will cause issues when you try to work with that data later, either by making it inefficient, or difficult to reason about, or by losing data when you do arithmetic that doesn't actually guarantee precision.

Use the correct data type and your life will be easier.  And don't ever store money values as floating point numbers.
