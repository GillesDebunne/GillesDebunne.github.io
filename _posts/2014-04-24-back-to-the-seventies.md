---
layout: post
title: Bash, back to the seventies
---

Yesterday I decided I [needed some tests]({% post_url 2014-04-23-you-shall-test %}). Overnight, simple curl in a bash script seemed appropriate to test a REST API.

I created a new `test` configuration in grunt-preprocess. It generates some duplicated code, that I was unable not remove.
I added [grunt-shell](https://www.npmjs.org/package/grunt-shell) to be able to launch scripts from grunt.

I had it all working in half an hour. Grunt is ok, but the ecosystem looks a bit young, with a lot of extensions providing the same service (grunt-exec, grunt-shell, grunt-run...), some allegedly no longer maintained.

Anyway, now on to my script.

# Bash bashing

The shell script first calls `mysql` to create and populate a test database.
I used `mysql_config_editor` to persist a MySql login configuration and avoid the "Using a password on the command line interface can be insecure" warnings when setting the password from the command line.

I created an `assert` bash function to check the JSON returned by a query, and an `assertError` to check the http return code of invalid requests (hint: `curl -s -o /dev/null -w "%{http_code}"`). A nice DSL with one-liner tests:

```
assert "POST" "user" "$USER" '{"id":"1","role":"user","token":".."}'
assertError "POST" "user" "$INVALID_USER" 403
```

But bash was not helping me. One line sums it up:

```
if [ "$RESULT" != "$EXPECTED" ]; then
```

where you learn that `[` is not just a funny parenthesis, but an alias to the `test` *command*, which expects `]` as it last argument. This explains why you need this `;` at the end to separate the `then`. And do not try to remove any of the space characters here, they are *all* required. Same thing for the *quotes*, which prevent new spaces from appearing.

Bash is a dinosaur, coming from the seventies, when you were so proud you could format your 720k floppy using the command line. I knew it, but my script was short, and all I needed was to get these two `assert` methods running.

# And then a test fails

In this test, I give a new type of header parameter to curl, but it manages to mess with the parameters and their quotes. When I `echo` the command and then run it in a shell, I get the correct result. But when bash runs it, I can see on the server log that the header parameters are wrong, maybe because it added some quotes this time.

I've spent more than half a day on these tests, and all the bugs I've found so far were in the tests.
