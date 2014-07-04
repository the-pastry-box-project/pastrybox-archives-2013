

The web platform consists of many layers. And many of those layers lack in detail. These subsystems are
generally understood (in the sense of X goes in, Y comes out), but the exact rules of each varies across the
board and it takes time and a lot of effort to plug the holes. I like plugging holes. Finding the bits that
are not defined or incorrectly defined and fixing them is one of the pleasures I take in my job. CSS 2.1 is
generally seen as the first real attempt at doing that within the web platform community. A more recent
example is the HTML parser. Parsing HTML has been an unpopular reverse engineering project for over a decade,
but nowadays you can simply write some code that matches requirements written in plain English.

At the [WHATWG](http://www.whatwg.org/) I am leading a couple of such efforts, trying to standardize the
[DOM](http://dom.spec.whatwg.org/), [Encoding](http://encoding.spec.whatwg.org/),
[Fetch](http://fetch.spec.whatwg.org/), and [URL](http://url.spec.whatwg.org/) subsystems in great detail.
These web platform layers have existed for well over a decade now and converging their implementations is a
costly and painful process. Long term however, having the same behavior across clients will greatly benefit
web developers and the long term health of the web.