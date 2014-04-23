---
layout: post
title: You shall test
---

But it's a pain. I don't like testing.

> Booooooo !

I hear you, agile craftsmen. But since I never make bugs...

> Booooooo ! Booooooo !

Got it. Still, I'm not a big fan of tests, I feel like I'm wasting my time. Except for very specific / complex / sensitive parts of the code, I hardly test my code. The fact that my work is usually very UI-centric does not help either. Toggle a button, rotate the camera using the mouse and check that the wireframe is correctly displayed. Good luck.

More testing is definitively something I want to try in this post series. Maybe I wouldn't have tried if it wasn't for this blog actually.

And sometimes, your system explodes, as is the case now with my angularJS side project. Each defect leads to a new one. My architecture is probably really bad, since this is my first project using this technological stack. The first isolated part I'll try to test is the REST API.

# Testing a REST API

It's a single PHP page, using the [Slim framework](http://www.slimframework.com/) and accessing a mySql database. Around 10 different actions, with various error return codes.

phpUnit, DbUnit, sure, but I don't care about the PHP side, only about the REST API.

Frustrated after these long minutes looking for tools, I decided to do it by hand: Create a test grunt configuration, binding to a test database, maybe using SqlLite, and then I'll do simple curl requests and check the results. And yes, some requests will have side effects and their order will matter.

> Booooooo !

That's exactly the kind of mistakes 'bad' programers do, for lack of knowledge of the appropriate tooling. They end up re-inventing the wheel and wasting even more time. So let's sleep over it.
