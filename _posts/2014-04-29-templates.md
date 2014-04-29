---
layout: post
title: Traits and Templates
---

This [article](http://www.boost.org/doc/libs/1_55_0/libs/geometry/doc/html/geometry/design.html) describes how to write a C++ library with templates and traits and it made some buzz. 

At first, I really thought it was a joke. The code is getting more and more complex and the author seems to enjoy it. Yes, the final code is general and can compute distances in arbitrary dimensions, but at the expense of traits that need to be implemented and readability for the regular programmer.

Glad I'm not coding in C++.

Oops, actually I am, and have been for the last 6 months.

# Then what?

There is unfortunately no perfect language out there. All we can hope is that the new ones learn from the mistakes of the old ones. Like Java avoided most of the object oriented mistakes of C++, which had the C compatibility burden.

The current trend is closures, introduced very recently in Java 8 and C++ 11. If these languages (and others) do not dare to break some backward compatibility, we can guess they will be outdated in a few years when we realize they modeled something wrong.