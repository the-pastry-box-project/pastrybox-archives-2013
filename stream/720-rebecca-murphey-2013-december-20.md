

Over the last few weeks, the team I work on has been observing a holiday code freeze — no new features, and
lots of time spent fixing bugs and paying down technical debt. Morale is through the roof — even our
designated curmudgeon seems to be enjoying himself — but my favorite thing has been seeing the snowball
effect that occurs when we start fixing little things. We took the time to add some logging to a fickle
process, and discovered that a little caching could go a long way. We created a Chrome extension to help us
work on and debug our app; suddenly, bugs are easier to investigate, and we have a place we can add new
utilities as they occur to us. We buckled down and rewrote and documented a swath of code whose original
developer left the company over the summer, and now we have new insight into how we can use it to solve
problems in the future. We made more than 40 improvements to our application’s accessibility, and baked an
appreciation of its importance into our team’s DNA in the process. We finally addressed a longstanding `//
TODO` by adding a handful of lines to our codebase, and cut several kilobytes from our production app in the
process. We instrumented our code to give us real-world performance numbers from actual users, and created a
page where we can see those numbers in real time so we know if something is going wrong.

At our team retrospective the other day, the happiness and enthusiasm was palpable, and the list of answers to
“what went well?” was long. Whenever I give a talk about refactoring a codebase, someone in the audience
always asks, “How do I convince my company that this is as important as the next big feature or deadline?”
My answer is simple: for the sake of the health of your team and your project, you can’t afford to *not* pay
attention to these things. If the powers that be don’t believe you, well, we’re hiring. :)