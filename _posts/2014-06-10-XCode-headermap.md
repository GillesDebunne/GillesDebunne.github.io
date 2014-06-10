---
layout: post
title: XCode headermaps
---

When building with C/C++, the include paths are listed with a `-I` option, in search order. But XCode has an undocumented 'smart' feature called header map which supposedly accelerates the search process based on name.

However, when two files with the same name are provided by two different libraries (`JSON.h` in my case), the header maps do *not* preserve the include search paths order. The solution is to use the `+` icon in your project's build settings and add a `USE_HEADERMAP=NO` option. Hours lost.

## It just works

This problem, and XCode in general, is a good example of Apple doing it wrong. Whether the user base is too small, or the software is inherently more complex, it does not par with the quality and ease of use of other Apple products. An IDE should be a tool, not the whole ecosystem. I had to manually fix my XCode workspace files many times, when it got confused after renaming or deleting files. When dealing with code, the config files should be the reference and should be editable, instead of hiding configuration under the UI.