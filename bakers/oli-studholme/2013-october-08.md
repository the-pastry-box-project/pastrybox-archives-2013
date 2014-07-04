

# UTF-8

It’s 10 years since Joel Spolsky’s article “[The Absolute Minimum Every Software Developer Absolutely,
Positively Must Know About Unicode and Character Sets (No
Excuses!)](http://www.joelonsoftware.com/articles/Unicode.html)”. NotePad still saves in ASCII by default.
Many web developers still don’t know about character encoding. And I’m still getting mojibake
(garbled text) web pages, and errors like this:

	Running "compass:site_prod" (compass)
	taskEncoding::CompatibilityError on line ["28"] of
	/Users/oli/.rvm/gems/ruby-2.0.0-p247/gems/sass-3.2.9/lib/sass/tree/visitors/to_css.rb: incompatible character
	encodings: UTF-8 and ASCII-8BITRun with --trace to see the full backtrace

I’m not going to lie to you, encoding and other internationalization stuff can be hard work. But we’re not
in the business of easy. We’re in the business of *doing it right*. If you don’t know about unicode and
internationalization, it’s time to find out. Onward!

## Encoding

This is how computers map ones and zeroes to characters. Back in the day there was US-ASCII, which encoded 128
characters in 7-bit binary. Localized variants were introduced to accommodate foreign languages, leading to
8-bit ISO 8859-based encodings, and a whole mess of problems with incompatible encoding.

Unicode attempts to resolve this mess, and currently contains codepoints for more than 110,000 characters,
covering 100 scripts. While there are a ton of encodings you *could* use, for the web __use UTF-8__. You want
to use UTF-8 for your entire stack. So how do we get that?

## Browsers

First up, make sure your browsers auto-detect encoding, and set UTF-8 as the fallback. This should be the
default.

## Text editors

Your text editor should be set to always save documents as UTF-8. Luckily modern text editors already default
to this. In general, don’t save a Byte Order Mark (BOM) — it’s not needed for UTF-8, and historically
could cause problems.

## Declaring character encoding

According to HTML5, browsers determine an HTML page’s encoding using the following [encoding sniffing
steps](http://www.whatwg.org/specs/web-apps/current-work/multipage/parsing.html#determining-the-character-encoding):

 *  A user-set encoding, if there is one

 *  A Byte Order Mark

 *  An HTTP `charset` declaration in the web server’s response headers (`Content-Type:text/html;
charset=UTF-8`)

 *  A `<meta charset="">` declaration in the HTML page’s `<head>` (HTML5 style)

 *  A `<meta http-equiv="">` element declaring `charset` in the HTML page’s `<head>`
(old-skool HTML 4.1 etc. style)

 *  Heuristic analysis (= advanced guessing)

### Web server

You want your web server to be sending the right `charset` declaration header (`Content-Type:text/html;
charset=UTF-8`), or at least not sending a *wrong* one. You can check this in the Network tab of your
browser’s developer tools — select the html page and look for `Content-Type` in the headers. You can also
use tools such as the [W3C Internationalization Checker](http://validator.w3.org/i18n-checker/).

If you’re using an Apache server that’s sending a non-UTF-8 `charset` header and you can edit `.htaccess`,
you can set `charset` headers there:

	AddCharset utf-8 .html .htm .php .css .js

This could also be set as part of setting the MIME type (although MIME types should already be set in
Apache’s `mime.types` file):

	AddType 'text/html; charset=utf-8' .html .htm
	.phpAddType 'text/css; charset=utf-8' .cssAddType 'text/javascript; charset=utf-8'
	.js

Alternatively, if your URIs don’t use file type extensions via `mod_negotiation` ([and they
shouldn’t](http://www.w3.org/Provider/Style/URI.html)), Apache is pre-configured in `httpd-languages.conf`
to treat file names that contain `.utf8` as UTF-8. This means documents named like `index.utf8.html` get the
correct character set headers.

For those who can’t change incorrect server headers, the HTML5 spec recently reordered the encoding sniffing
steps to put the BOM above HTTP headers, so you have recourse. However, not all browsers support this, so it
would be better to ask your server admin to fix this (or get a better server).

For information on setting headers for other servers, and in server side scripting languages, see [Setting the
HTTP charset parameter](http://www.w3.org/International/O-HTTP-charset) by Martin Dürst and Richard
Ishida.

### In HTML and CSS

Even if you’ve set HTTP headers, it’s a good idea to also add `charset` declarations to your
documents.

Add `<meta charset="UTF-8" />` to your HTML5 document’s `<head>`, ideally immediately
after the opening `<head>` tag. It must appear in the first 1024 bytes of your document, so place it
before any ASCII art.

Browsers use a similar algorithm for CSS. For external stylesheets, the CSS equivalent of HTML’s `<meta
charset="utf-8">` is `@charset="utf-8";` at the top of your stylesheet — it must be
the first thing in the CSS file. Embedded stylesheets use the encoding of the HTML page.

JavaScript doesn’t have an equivalent character set declaration method, but this is normally not a problem.
However, you can declare encoding for a script with the `charset` attribute: `<script
charset="utf-8" src="[…]></script>`. Don’t add `charset` to an embedded
script — these take the encoding of the HTML page.

## HTML

We’ve covered declaring encoding, the most important step, above.

Next, if you’ve got any forms for user-submitted data, add the `accept-charset` attribute so the browser
sends UTF-8-encoded data:

`html<form action="[…]" accept-charset="UTF-8">…</form>`

If you’re using `<input type="email">` it’s nice to validate it client-side using
HTML5’s handy `pattern` attribute. You may be tempted to use something like
`[a-z0-9._%+-]+@[a-z0-9.-]+\.[a-z]{2,4}` — don’t! We have multi-byte URLs now, and you need to use a
pattern like `[^ @]@[^ @]` to support them.

Because we’re using UTF-8 we also no longer need to use escape codes such as `&#8220;` and `&#8221;`
for curly quotes (“”) and the like — we can just add these characters directly. While it won’t hurt if
you do escape things, the only characters you *need* to escape when using literally in UTF-8-encoded HTML5
are:

 *  `<` Less-than sign → `&lt;`

 *  `&` Ampersand → `&amp;`

You’ll also need to escape `"` Quotation mark (→ `&quot;`) or `'` Apostrophe (→
`&#39;`) if you use them in attribute text, such as an `alt` tag (or just use their “smart”
equivalents). Here’s a table on [how to type quotation characters
directly](http://html5doctor.com/blockquote-q-cite/#punctuation-characters).

Next, declare a page’s language by using the `lang` attribute. First, set the document’s main language in
the HTML tag. For example, a mainly Japanese document would use the language tag `ja`:

	<html
	lang="ja">

To find out a language’s tag, search for the language using Richard Ishida’s [Language Subtag
Lookup](http://rishida.net/utils/subtags/). You can add further information, such as a dialect (`en-US` for
American English) or script (`ja-latn` for Romanized Japanese), but only do so if it adds important
information. If you then want to include text in other languages on the page, add the appropriate
`lang="` attribute to an element wrapping the text.

HTML5 relaxes the restrictions on valid ID names, so you can now use [nearly anything as an ID
name](http://mathiasbynens.be/notes/html5-id-class), such as `id="☺"` or `id="大事"`,
the same as class names. Keep in mind you’ll need to [use character escapes in
CSS](http://mathiasbynens.be/notes/css-escapes) for some class and ID names.

## JavaScript

For the lowdown on character escapes in JavaScript, see [JavaScript character escape
sequences](http://mathiasbynens.be/notes/javascript-escapes) by Mathias Bynens. It also includes a handy
JavaScript string escaping tool. For more details, see [Unicode and
JavaScript](http://www.2ality.com/2013/09/javascript-unicode.html) by Dr. Axel Rauschmayer.

## MySQL

MySQL defaults to the character set of `latin1` and collation of `latin1_swedish_ci`, which turns your data
into a ticking time bomb. You can check what character set and collation you’re using via this MySQL
command:

	SHOW VARIABLES WHERE Variable_name LIKE 'character\_set\_%' OR Variable_name
	LIKE 'collation%';

While you can set MySQL up to use `DEFAULT CHARACTER SET utf8` and `DEFAULT COLLATE utf8_general_ci`, this
does *not* give full UTF-8 support. It only supports the Basic Multilingual Plane (BMP) of UTF-8, and will
lead to data loss if you insert glyphs from other planes, such as emoji. At the time of writing this is also
what many CMSes use by default ([WordPress](http://core.trac.wordpress.org/ticket/21212),
[Drupal](https://drupal.org/node/1314214)), so be wary of this.

However, MySQL 5.5.3 adds full UTF-8 support via the charset `utf8mb4`. To change to `utf8mb4` read Mathias
Bynens’ article [How to support full Unicode in MySQL
databases](http://mathiasbynens.be/notes/mysql-utf8mb4).

Encoding issues don’t muck around: the recently released WordPress 3.6.1 fixes a [PHP object injection
bug](http://vagosec.org/2013/09/wordpress-php-object-injection/) that can lead to remote code execution, due
to using `unserialize()` with MySQL’s `utf8` rather than `utf8mb4`.

## Programming

Some languages require you to specify encoding, and you’ll generally need to declare your database’s
character set and collation. Some also have encoding-related functions that e.g. default to Latin-1 (ahem,
PHP) to catch you out. Never assume that the data you’re dealing with is UTF-8 — ASCII appears identical
unless you view the hex to see if each character is taking one byte (ASCII) or three (UTF-8). Use a string
like `“Iñtërnâtiônàlizætiøn”` to check this.

Once you’ve read Joel’s post, read [What Every Programmer Absolutely, Positively Needs To Know About
Encodings And Character Sets To Work With Text](http://kunststube.net/encoding/), by David C. Zentgraf.

I hope that’s given you enough to get started. For more information, read the following links:

 *  [All About Unicode, UTF8 & Character
Sets](http://coding.smashingmagazine.com/2012/06/06/all-about-unicode-utf8-character-sets/) — Paul Tero

 *  [Love Hotels and Unicode](http://www.reigndesign.com/blog/love-hotels-and-unicode/) — Matt Mayer

 *  [Character encodings: Essential
concepts](http://www.w3.org/International/articles/definitions-characters/) — Richard Ishida, W3C

 *  [Handling character encodings in HTML and
CSS](http://www.w3.org/International/tutorials/tutorial-char-enc/) — Richard Ishida, W3C

 *  [Choosing a Language Tag](http://www.w3.org/International/questions/qa-choosing-language-tags) — Richard
Ishida, W3C

 *  [Migrating to Unicode](http://www.w3.org/International/articles/unicode-migration/) — Norbert
Lindenberg, Yahoo! (a little old, but wonderfully detailed)

 *  [HOWTO Use UTF-8 Throughout Your Web
Stack](http://rentzsch.tumblr.com/post/9133498042/howto-use-utf-8-throughout-your-web-stack) — Jonathan
‘Wolf’ Rentzsch

 *  [Encodings, Unabridged](http://yehudakatz.com/2010/05/17/encodings-unabridged/) — Yehuda Katz
(specifically on Ruby/Rails)

Happy internationalizing! ^_^b