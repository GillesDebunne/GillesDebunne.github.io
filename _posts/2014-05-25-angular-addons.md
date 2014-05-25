---
layout: post
title: AngularJS add ons
---

Tried to add two angular extensions to my project today.

[angular-tour](https://github.com/DaftMonk/angular-tour) was supposed to easily create a tour of the web site. But all I got was `undefined is not a function` error messages. I debugged a little with no luck and finally created an issue on the git project page. The bower also has a hard coded dependency on `jquery` version 2.0.3 which prevented an update to a more recent version for my project.

Next I tried to integrate [angular-slider](http://venturocket.github.io/angular-slider/), a replacement for [angular-slider](https://github.com/prajwalkman/angular-slider). I also looked at [angular-rangeslider](https://github.com/danielcrisp/angular-rangeslider) and [angular-jsslider](https://github.com/rzajac/angularjs-slider). So many options, all providing the same service, but with various limitations. The one I picked was basically invisible, as it does not provide a css, and had a flacky mouse tracking (clicking on a handle made it change the value).

## Large projects needed

Comparable to the problems I had with [grunt packages](% post_url 2014-05-08-less-is-more %), it really seems the JS ecosystem is a bit too young. Open source projects are nice and github has tons of them, but a few tens of users and a single maintainer are simply not enough to create production ready bricks.