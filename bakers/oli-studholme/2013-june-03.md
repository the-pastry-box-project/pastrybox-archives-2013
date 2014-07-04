

# CSS: reset or normalize?

Building for the web can be like building on quicksand. Browsers have tended to do mostly the same thing, but
have occasional, maddeningly unpredictable differences. For example, browsers all come with “user agent
stylesheets” — a default set of CSS styles, so that a heading looks like a heading etc., even before you
style the page[1](#fn1). Of course, every browser engine uses a slightly different set of defaults.

One example of this was [default list
styles](https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Consistent_list_indentation), where Internet
Explorer and Opera initially[2](#fn2) indented lists with `margin-left: 30pt;` in their default browser
stylesheets, while Firefox and KHTML went with `padding-left: 40px;`. If you wanted to change the default
indent, specifying `ul {padding-left: 0;}` would lead to very different results across browsers.

## CSS resets[3](#fn3)

To get a little stability, some developers reset all margins and padding using the universal
selector:

	* {margin: 0; padding: 0;}

With this at the start of your stylesheet, when you specified a list indent you got what you expected.
However, using `*` meant the default margin and padding were nuked for *all* elements, which became painful as
soon as you added a `<form>` element.

[Tantek Çelik](http://tantek.com/log/2004/09.html#d06t2354) and [Eric
Meyer](http://meyerweb.com/eric/thoughts/2004/09/15/emreallyem-undoing-htmlcss/) started discussing a more
targeted way to address user agent style differences in 2004, with the [YUI CSS
Reset](http://nate.koechley.com/blog/2006/05/09/second-yui-release/) appearing in 2006, and the [Meyer
Reset](http://meyerweb.com/eric/thoughts/2007/04/12/reset-styles/) in 2007.

> The point
> of a reset is to zero out as much as possible … [and] to serve as a starting point for your own baseline
> styles — [Eric
> Meyer](http://meyerweb.com/eric/thoughts/2011/01/26/reset-v2-0/#comment-542624)

Here’s the first rule of [Eric’s current (v2.0) CSS
Reset](http://meyerweb.com/eric/tools/css/reset/):

	html, body, div, span, applet, object, iframe,
	h1, h2, h3, h4, h5, h6, p, blockquote, pre, a, abbr, acronym, address, big, cite, code, del, dfn, em, img,
	ins, kbd, q, s, samp, small, strike, strong, sub, sup, tt, var, b, u, i, center, dl, dt, dd, ol, ul, li,
	fieldset, form, label, legend, table, caption, tbody, tfoot, thead, tr, th, td, article, aside, canvas,
	details, embed,  figure, figcaption, footer, header, hgroup,  menu, nav, output, ruby, section, summary, time,
	mark, audio, video {  margin: 0;  padding: 0;  border: 0;  font-size: 100%;  font: inherit;  vertical-align:
	baseline; } …

This resets several properties on many (but not all) elements back to the equivalent of plain text. Because
only appropriate elements are reset, this avoids some of the problems of `* {margin: 0; padding: 0;}`. We can
then define styles for these reset “unstyled” properties, safe in the knowledge we’re building on a
stable, cross-browser base. This “unstyled” styling also acts as a reminder to consciously set appropriate
styles for these elements.

## Problems with CSS resets

CSS resets have been a lifesaver, but especially with the rise of frameworks they are now often used as-is.
For example, Eric assumed people would build on the reset styles he proposed, overriding them as appropriate,
and version 1 of the Meyer Reset included this rule for a time:

	/* remember to define focus
	styles! */ :focus {  outline: 0; }

Sadly, not everyone did define focus styles, and Eric has removed this from v2.

Using a reset can also start to feel a little perverse. Resetting browser default styles does force us to
deliberate on how each element should appear, helping ensure we use elements for their semantics and not their
default styling. But for elements like `i` and `em` that’s almost always the browser default style. Other
default browser styles, like the text sizes for headings which used to be ridiculously large, have changed to
become passable defaults. There’s also the problem of someone wanting to use a reset HTML element after
handoff, still with only the “unstyled” reset styles specified.

For me the main issue with resets is inheritance, leading to spam in your browser dev tools. When you’re
trying to track down a CSS problem on a deeply nested element in someone else’s code, this does not
help:![img](http://the-pastry-box-project.net/wp-content/uploads/2013/06/inspector-spam.png)CSS reset
rules repeating due to inheritance

## Normalize.css

Nicolas Gallagher and Jonathan Neal have taken a different approach with
[Normalize.css](http://necolas.github.io/normalize.css/), “a small CSS file that provides better
cross-browser consistency in the default styling of HTML elements”. As with CSS resets it gives us a
reliable cross-browser starting point — the main reason for using a reset in the first place — but the two
approaches are philosophically different.

CSS resets override user agent styles to return many elements back to an “unstyled” state, a level
foundation we can safely build upon. However, we then need to define styles for most elements before we can
build with them. Normalize.css instead addresses only the inconsistencies between user agent default styles,
choosing the most appropriate default where there are differences. We get a safe cross-browser foundation here
too, but one that includes normalized user agent styles as basic building materials ready for use. It’s
basically a kind of an idealized, cross-browser version of CSS 2.1’s [Default style
sheet](http://www.w3.org/TR/CSS2/sample.html). For both ways we then need to add our own overriding styles to
build the view, but because the browser defaults remain with Normalize.css, in general fewer styles need to be
added.

Because the changes in Normalize.css are a lot more targeted, there isn’t an inheritance cascade of
overwritten rules in your browser’s developer tools. Here’s a simple `<ul>`: “unstyled”, with
the Meyer Reset, and with Normalize.css versions 1 and
2:![img](http://the-pastry-box-project.net/wp-content/uploads/2013/06/unstyled.png)An “unstyled”
unordered list
element![img](http://the-pastry-box-project.net/wp-content/uploads/2013/06/meyer-reset.png)Applying the Meyer
Reset![img](http://the-pastry-box-project.net/wp-content/uploads/2013/06/normalize-v1.png)Applying
Normalize.css v1![img](http://the-pastry-box-project.net/wp-content/uploads/2013/06/normalize-v2.png)Applying
Normalize.css v2

You can clearly see the difference in philosophy, with the Meyer Reset example appearing as two lines of plain
text with no margins, padding or bullets, while the Normalize.css examples are similar to the default styling.
The difference in the styles applied to this `<ul>` are also easy to see. 

However, these are not all the styles being applied to the `<ul>`. For comparison, here’s the same
“unstyled” screenshot, but with the user agent styles visible, in Firefox 21 and Opera Next 15:
![img](http://the-pastry-box-project.net/wp-content/uploads/2013/06/user-agent-styles-moz.png)Mozilla user
agent
styles![img](http://the-pastry-box-project.net/wp-content/uploads/2013/06/user-agent-styles-opera.png)Opera
user agent styles

*This* is the CSS that we’re resetting or normalizing. 

Normalize.css version 2 supports modern browsers plus IE 8, whereas version 1 also contains additional support
for legacy browsers like IE 6 and 7. These older browsers need more normalization, and this can have minor
disadvantages, for example the added vertical margins for the nested list in the Normalize.css v1 screenshot
above. This split into two versions is useful if you no longer need to provide old browsers with Grade A
support, and also if you want to learn about old browser quirks.

Normalize.css also helps correct some browser bugs, including “display settings for HTML5 elements,
correcting `font-size` for preformatted text, SVG overflow in IE9, and many form-related bugs across browsers
and operating systems”. For example, the following CSS fixes WebKit issues with HTML5’s new `<input
type="search">` element:

	/** * 1. Address `appearance` set to `searchfield` in
	Safari 5 and Chrome. * 2. Address `box-sizing` set to `border-box` in Safari 5 and Chrome *    (include `-moz`
	to future-proof). */ input[type="search"] { -webkit-appearance: textfield; /* 1 */ -moz-box-sizing:
	content-box; -webkit-box-sizing: content-box; /* 2 */ box-sizing: content-box; }

Without it, WebKit’s default use of `-webkit-appearance: searchfield;` for `type="search"`
prevents the styling of font, padding, border, and background properties on OS X and iOS, and gives buggy
behavior for the border property on Windows.

An added bonus is Normalize.css is heavily commented and
[well-documented](https://github.com/necolas/normalize.css/wiki/), helping you learn why each rule is there.
This does make it noticeably longer than CSS resets, but when minified and Gzipped even the larger
Normalize.css v1 is only 1KB.

## Conclusion

While philosophically different to CSS resets like the Meyer Reset, Normalize.css is very much carrying on the
same tradition, continuing in the footsteps of Tantek and Eric. You might even already be using it — it’s
a core part of [HTML5 Boilerplate](http://html5boilerplate.com/),
[Bootstrap](http://twitter.github.io/bootstrap/), and YUI’s new [Pure](http://purecss.io/base/). 

User agent stylesheets are converging, and hopefully one day we won’t need to reset or normalize. There’s
even [a valid argument](http://snook.ca/archives/html_and_css/no_css_reset/) for not worrying about small
differences between browsers (although being a Snook-level genius helps with that). But for now if you’re
using a CSS reset, or nothing at all, [give Normalize.css a try](http://necolas.github.io/normalize.css/) on
your next project.

## Addenda

 *   [[1]](#r1) You can see the user agent style sheets for
[Mozilla](http://mxr.mozilla.org/mozilla-release/source/layout/style/html.css),
[WebKit](http://trac.webkit.org/browser/trunk/Source/WebCore/css/html.css), and [IE](http://www.iecss.com/).
[CSS2.1 User Agent Style Sheet Defaults](http://css-class.com/test/css/defaults/UA-style-sheet-defaults.htm)
highlights the differences across (older) browsers. These styles also include things like `style {display:
none;}` — try adding `style {display: block;}` to your CSS and see what happens.

 *  [[2]](#r2) Since then, all browsers have migrated to setting list indenting via `padding-left` or
`padding-start`, with IE7 being the last IE browser to use `margin-left` for this.

 *   [[3]](#r3) For detailed background on the history of CSS resets, read [The History of CSS
Resets](http://sixrevisions.com/css/the-history-of-css-resets/), by Michael Tuck.

*My thanks to Eric Meyer and Nicolas Gallagher for their feedback on this article, and for these wonderful
tools.*

*Postscript:* While nuking margins and padding on all elements with `* {margin: 0; padding: 0;}` is gonna be a
bad time, there is one universal selector-based reset you should still consider: `* {box-sizing:
border-box;}`. This changes padding and border to being part of an element’s width, rather than additional
to it. For more information, check out Paul Irish’s article “[box-sizing: border-box
FTW](http://www.paulirish.com/2012/box-sizing-border-box-ftw/)”. 