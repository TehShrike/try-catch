# Confession: doing inaccurate arithmetic on currency values in a point-of-sale system

My first job was working on point-of-sale software, which is the software that cashiers use to ring up the stuff that you buy in a store.

In point-of-sale software, it's very important that your arithmetic always be correct: that you always add totals up to the same amount, and always calculate tax accurately.

When I started working on the software, fresh-faced and full of optimism, all of the arithmetic done by the software was done using floating point numbers.  Floating point numbers are a super-efficient way for processors to do calculations on fractional numbers with potentially many many numbers after the decimal point, but without any guarantees for precision.

I didn't see any problems with this when I started.

One day, I got a support call from a client with a weird issue: an old invoice would show up as having an unpaid balance of one cent on one of their computers, but on every other computer, it showed as being paid in full.  When I tested on my computer, I got the same total as had originally been calculated for that invoice, but on one of the client's computers, the tax rate would calculate to be one cent different.

There wasn't any bug in our code, except for the fact that we were using floating point arithmetic, and that one computer's processor came up with a number that was off by a fraction of a millionth of a penny different, which would cause it to round to a different cent.  That was disconcerting.

A while after that, I ran into a case that I could reproduce reliably on my machine.  It wasn't even a very strange edge case - with a fractional quantity of something, the tax rate would come out to a dollar fifty-five.  But our software didn't show a dollar fifty-five, it showed a dollar fifty-six.

Internally, after doing the multiplication using floating point arithmetic, the tax rate was being calculated to come out to one point five five zero zero zero zero zero zero zero zero zero zero zero one dollars, which we would then round to a dollar fifty six.

I started scheming up a series of multiplying and dividing steps that would solve the issue, but it turns out there's no way you can precisely correct for imprecise arithmetic.  Eventually I realized this important fact: you should never, ever use floating point numbers to represent money values.  Not even double precision floating point numbers.

There are number data types that will do arithmetic without any loss in precision.  Some programming languages provide them out of the box.  They're usually called "big number" or "big integer" or "arbitrary precision" libraries.  As long as you store your numbers in the database with a fixed-point type, like MySQL's "decimal" type, and you only ever represent the numbers in your code with one of those arbitrary precision number libraries, then you're good - you won't lose pennies because of floating point arithmetic.

This is a very easy mistake to make if you don't know about it, because in almost every programming language, if you type a number with a decimal point into your editor, it will be represented in code as a floating point value.  It's natural to assume that that must be the best way to represent fractional dollars.

BUT IT'S NOT!
