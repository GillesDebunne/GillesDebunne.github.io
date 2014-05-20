---
layout: post
title: Bash is back
---

I had an [other]({% post_url 2014-04-24-back-to-the-seventies %}) painful experience with `bash` scripts today.

All I wanted to do was to create a cron task that updates some files in a folder, compresses and uploads these files on a web site using `ftp`.

As before, the `curl` part was problematic, when used in conjunction with variables.

But this time, I've found [this answer](http://thread.gmane.org/gmane.comp.web.curl.general/8716/focus=8723) in a thread.
Turns out that when you declare:

```
→ FOO='a b "c d"'
```

`echo $FOO` will work as expected, but `showargs $FOO` will list these parameters:

```
→ showargs $FOO
Program name: showargs
Parameter  1: a
Parameter  2: b
Parameter  3: "c
Parameter  4: d"
```

4 parameters instead of the expected 3, double quotes loosing their meaning and a text split by spaces.

## showargs

`showargs` is a simple C executable that lists the different parameters of a `bash` command. Here is its code:

```
#include <stdio.h>

int main (int argc, char *argv[]) {
        printf("Program name: %s\n", argv[0]);
        for (int i=1; i<argc; i++)
                printf("Parameter %2d: %s\n", i, argv[i]);

        return 0;
}
```

Use `gcc showargs.c -o showargs` to compile, and you'll get a pretty cool debugging tool. Simply preprend it in front of the failing command in your script to list its _actual_ parameters.

This allowed me to fix my curl syntax (by splitting a variable into two, bash black magic).

When I'm ready, I'll try to debug the bash REST test I abandoned few weeks ago.
