

# Testing the web

Earlier this month I took part in [Test the Web Forward
Tokyo](http://testthewebforward.org/events/tokyo-2013.html), a wonderful event organized by Adobe, Google,
HTML5J and friends on testing the web. Here’s a brief overview, then I’ll tell you why *you* should be
testing the web too.

Historically W3C specifications have been a little on the ambiguous side. This led to differing
implementations (like list indentation), and major pain for developers. In the last few years specs have
become a lot more explicit — for example, HTML error handling is finally specified in HTML5. However, they
can still contain small problems and ambiguities, things that are often not discovered until the spec is being
implemented and used. Also, with the breakneck pace of implementation there are still plenty of browser
bugs.

One way you can reduce programming bugs is to write tests, and user agent developers do this to check things
work as expected. However, as things become more complex it’s hard to cover all the possibilities, and there
are inevitably bugs that were never found during testing because they were never tested for. Each engine doing
this themselves also means a lot of duplication.

Recognizing this, the W3C has championed creating and collecting unit tests for their Test Suites. By making
one large collection of tests user agent developers can all use, they don’t need to create tests for every
facet of every spec themselves to check their work. Any tests they do make can be submitted for other UAs to
use. Making a test requires reading a specification in detail, which helps to discover any inconsistencies or
errors. This gives specification editors additional feedback, helping them fix mistakes and clarify things
before widespread implementation.

More explicit specifications and more testing have both contributed to a reduction in browser bugs, and a
corresponding increase in interoperability. Now we can finally begin to expect things written to the
specifications to work first time in modern browsers, a fantastic improvement.

So if tests help spec editors and user agents get it right first time, and give us better specs, fewer bugs,
and more interoperability, what’s the catch? Well, someone has to make them. Luckily this isn’t difficult
— *if you can write HTML or CSS, you can make a test*. It’s basically the same as making a bug reduction
— work out the feature you want to test, then make the simplest thing you can that tests that feature, and
*only* that feature. It should be obvious enough that your Grandma or Grandpa can tell if it passed or
failed.

If you want to give it a try, the steps are:

 *  Read through the resources on [Test the Web Forward](http://testthewebforward.org/index.html#resources),
especially [How to Write a
Reftest](http://adobe.github.io/web-platform/presentations/testtwf-how-to-write-a-reftest/#/).

 *  Get a GitHub account and fork the [HTML5](https://github.com/w3c/web-platform-tests) and/or
[CSS](https://github.com/w3c/csswg-test) testing repos, following [these GitHub
instructions](http://testthewebforward.org/resources/github_test_submission.html).

 *  Work out what feature of a specification you want to test for, and check there aren’t any tests for that
already. For CSS tests, search in [Shepherd, the CSS Test Suite Manager](http://test.csswg.org/shepherd/).
Make sure you’re using the most up-to-date version of the spec (usually the Editor’s Draft)!

 *  Duplicate a starter file
([examples](https://github.com/w3c/csswg-test/tree/master/contributors/ttwf_tokyo/starters)) or a similar
test, then edit it. Make sure you have a test file that tests the feature and describes the test, and a
reference file showing what the test should look like when it passes, both with the correct metadata.

 *  Check that your test passes when it’s meant to *and* fails when it should, and that a non-technical
person can understand the difference just by looking.

 *  Once your tests are ready to submit, follow those [GitHub
instructions](http://testthewebforward.org/resources/github_test_submission.html) again to set up a Pull
Request.

After you finish your first test, it’s really easy to modify it to test related things. Once you get into
it, making tests feels like a game, where you generally progress smoothly, then occasionally get a boss battle
with a browser bug or ambiguous bit of the spec. If this happens make sure to report the bug, or let the spec
editors know what’s confusing. If you find something *wrong* in the spec, you just hit the jackpot!

For an example of this in action, read Rodney Rehm’s article “[CSS3 Transitions: Thank God We Have A
Specification!](http://coding.smashingmagazine.com/2013/04/26/css3-transitions-thank-god-specification/)”.
Rodney turned over the stone of CSS Transitions and Animations, and found a mass of browser bugs and
inconsistencies. His article and tests have led to bug reports and proposed spec improvements. By doing so,
he’s made the web better for *all* of us. Respect! The best thing is there are plenty of features that still
lack tests, and most likely still have bugs and spec issues. We can *all* contribute.

The best way to make your first test is to join a [Test the Web Forward event](http://testthewebforward.org/).
If there’s not one coming up near you, consider [organizing your own testing
event](http://adobe-webplatform.github.io/testtwf-event-kit/) with some friends. It’s a fun way to learn
about one aspect of HTML or CSS in detail. More importantly, making tests helps interoperability, and
*interoperability helps us*. We can all help reduce browser bugs, and improve the specifications we use every
day.

So what are you waiting for? Show your ♡, and let’s [move the web
forward](http://www.movethewebforward.org/)!