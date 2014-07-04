

Within the standards world every now and then modularization comes up. “Standards should be modular!” One
could imagine Jeff Jaffe (W3C’s CEO) going on stage at one of W3C’s conferences and yelling “modularity!
modularity! modularity!” and one would not be too far from the truth. The standards created however are
often not modular, but rather bolt-on solutions on top of the existing stack (often bolt-on solutions
themselves). So rather than modules that evolve over time, we have an ever increasing set of standards that
patch each other, often in non-obvious ways.

One way this is evident is that the software that uses these standards often uses a different architecture. In
software [CSP](http://www.w3.org/TR/CSP/) is not a single module, but rather would be part of e.g. HTTP
(header processing), fetching (protocol for retrieving bits out of URL used by HTML’s `img` element and
every other piece of content that can be used to initiate a request), and some mediation part that enforces
the policy. In part it makes sense to design new features separately initially. This helps implementors to
grasp the work that needs be done and developers how they can make use of this new feature. But long-term it
harms the understanding of the platform. Say we introduce a new feature that performs a fetching operation.
What will its effect be on CSP? What will its effect be on other specifications bolted on top of fetching? You
do not just need to use the fetching protocol in the right way, you also need to patch CSP and potentially
other places. In other words, the modularity has left the building.

The standards process needs to become more flexible so the documents that describe the web platform can evolve
over time and change shape to meet new demands and constraints. The WHATWG has been pioneering this model for
close to a decade now and given the superior class of documents that have been developed it seems about time
to take note.