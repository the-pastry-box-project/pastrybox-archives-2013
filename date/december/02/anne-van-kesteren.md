

We have operating systems, browsers, app markets, and the web. I want to change the world so that the
operating system is the browser and its app market the web. I am using this last post to describe this system
in a little detail as it is exciting to think about, yet much is still unclear.

Foremost, everything on the system has a URL. You bookmark `https://mail.example.com/` to “install” your
Example Mail app on your home screen (`about:home`). Some of these URLs could be built-ins, e.g.
`about:settings` or`about:phone`, to deal with configuration and legacy applications the web does not really
have an interest in supporting natively. After all, with WebRTC we can make `https://phone.example.org/`
happen (and so much more).

Being able to navigate to these URLs is essential. This allows apps to be integrated with each other in the
same way sites are today, using `<a href="">`. On this system apps and sites will be within
the same continuum.

To get there offline will need to work. A flaky network should still give us access to our bookmarked URLs and
let us take photos with `http://betterphoto.example.com/nightly`. We need to get smarter about allocating
storage and not prompting the user for it. And since we will be putting the trust with the end-user rather
than a centralized app store, we have to get creative about APIs that are today deemed privileged. Can we do a
socket API that works for sites? Can we expose Bluetooth? Is exposing a Bluetooth API even sensible on a
platform that will likely outlive it?

That is what I’m working on so one day I can say “Native is dead, long live the native web.”