

At [Bocoup](http://bocoup.com), we recently conducted an internal survey about working remotely and methods
for communicating with people who aren’t working from the Boston office. We used a Google Docs form to
gather responses, and when all of the answers were in, I had a spreadsheet with about 300 data points.

It probably surprises no one here that I exported the data as a CSV and then wrote a small program to tell me
what everyone had said. I used Ruby because there are still times when the asynchronicity of JavaScript makes
a solution perfectly absurd, but certainly I could have written it in JS, or Python, or Perl, or probably even
Java if I was a special kind of masochist. There wasn’t much to it: key concepts included iteration over
lists of things, turning strings into lists of things, and using hashes to accumulate the totals. If I
didn’t know about hashes I still could have made it work, though it would have been a wee bit less
flexible. It was about 40 lines of terrible but working code.

Where my partner works, there are grown-ups who make a very good living who can barely use Excel, even though
they work with data every day. Their processes are as inefficient as you might expect as a result. These
colleagues of hers aren’t fresh out of college, but they’re young enough that they have decades
ahead of them where they will need to make money. I know my partner could readily learn how to write little
programs like the one I wrote, but she is reluctant to invest the time because she knows that no one else at
her job could understand them, and she’s already an order of magnitude better at the technology side of
things than most of her colleagues.

I wonder often what will happen in fields like this. It is sobering to remember how far behind they are: still
crunching data by hand, still versioning documents using filenames, still emailing documents around and around
and around because it’s the most reliable solution that everyone involved can understand. On the one
hand, it makes me feel like my comfort with technology means I will probably always be employable; on the
other hand, I have to remind myself that I could probably never bear to work there.