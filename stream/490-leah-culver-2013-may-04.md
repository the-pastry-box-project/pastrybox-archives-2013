

When thinking about the future of OAuth it’s helpful to remember why OAuth was created.

I was lucky enough to be part of the original group of API providers who created OAuth so I know that OAuth
was (mostly) intended to solve two common problems with API authentication:

 *   SSL/TLS was expensive and complicated.

 *   Websites shouldn’t be storing passwords of other websites.

Of course #1 is past-tense for a reason. SSL is now commonplace for web applications. APIs can simply do all
their authentication over SSL, which is a really good thing. There’s no need to be swapping tokens around
over SSL!

Password storage, #2, is still an issue. Websites shouldn’t be storing plaintext passwords for other
websites. However… mobile! It’s kind of okay to store a user’s credentials on a mobile device.

There’s a third major purpose of OAuth which arose as an unintended consequence: one-click login.

One-click login has been OAuth’s greatest success. Users can log in to a new website using their Twitter or
Facebook credentials. It’s much faster than having to enter a bunch of signup information.

So what’s the future of OAuth? I really love the one-click login feature but the other two issues seem much
less relevant today.

For the future we need to consider the problems that plague API developers today.

What are best practices for mobile devices? How can we make OAuth as simple as possible for client developers
now that SSL is commonplace? Can we make one-click login even faster and more trustworthy?

These are all questions we need to be talking about for OAuth 3.0.