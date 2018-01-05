# The worst SQL I've ever written

Hi, my name is Josh, and I've abused SQL.

When I was going to college, I had a computer science algorithms homework that gave me a database full of movies and required me to do a breadth-first search to find an actor's Kevin Bacon number, with a max depth of 7.  I solved the problem by writing a SELECT query with seven LEFT JOINs.  I did not get full marks on that homework.

Not too much later, still young and foolish, I wrote a time-tracking webapp for my employer.  This app would tell you when you clocked in and clocked out over the last week.

My client-side and server code was already complicated enough without a bunch of formatting code, so I made my database queries return the dates and times already formatted for the user to view.  I was comfortable with MySQL's date and time functions, so this seemed like a good idea at the time.

It was a very, very bad idea.

If you travelled to a customer's location, all of the dates and times would be off, because all of the dates were generated in the database server's time zone.

Eventually, we wanted to sell the software to another company, and they wanted dates formatted differently.  Because all the formatting was done at the database level, there was no easy way to change the display format based on a company setting, or a user setting, or anything else.

Over time, new views into the data were needed.  Every new query brought with it huge chunks of date formatting functions that were mostly the same, but with occasional small differences.

Eventually my regret turned into a small amount of wisdom.  Always fight to store data in its ideal format.  If I had stored all dates in a universal time zone instead of using the server time zone, I wouldn't have created the monsoon of technical debt I discovered as soon as time zones mattered.

When you have a datum in its ideal format, only transform it into a more specific format at the last possible minute.

If your API needs to return a date range as "number of minutes elapsed", call the function that does that math right before putting that value into the response object.

If your web site needs to display dates and times to the user, convert those dates from their ideal format into the user-friendly strings right where you're building up the HTML itself.

This gives you maximum freedom to compose whatever business logic and user settings are relevant without having to stick a "does the user care about seeing seconds?" function in your model code, or having to pass the user's current time zone from the browser all the way back.

You may have to suppress some "but it would be easier to just put that line here" urges, but it's worth it if you can avoid what I had to do, which is repeatedly tell my boss that what should have been a small change was going to take at least a week.
