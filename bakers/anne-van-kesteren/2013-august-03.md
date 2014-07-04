

There is a lesson we learned doing CSS, HTML, JavaScript, et al on the web. Mode switching hurts. Quirks mode
has not been worth the cost. Absorbing the few differences and providing ways to opt into the desired behavior
would have been better. Similarly, `"use strict"`, introduced as consensus compromise by TC39 while
developing version 5 of ECMAScript, still causes trouble. Deciding how new features in JavaScript have to work
often begs the question as to whether that needs to be different in `"use strict"` code or how it
would interact with such code. Networking seems to somehow get away with it more easily, although we still
have support HTTP/0.9. I suspect this might be because there are less moving pieces and deploying a server
stack is generally more involved than writing some HTML. I’d be interested in seeing research in this
area.