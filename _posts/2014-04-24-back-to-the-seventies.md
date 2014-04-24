---
layout: post
title: Back to the seventies
---

Yesterday I decided I [needed test]({% post_url 2014-04-23-you-shall-test %}). Overnight, simple curl in a bash script seemed ok to test a REST API.

I created a new `test` configuration in grunt-preprocess. It generates some duplicated code, that I could not remove.
I added [grunt shell](https://www.npmjs.org/package/grunt-shell) to my project to be able to launch scripts from grunt.

I had it all working in half an hour. Grunt is ok, the ecosystem is a bit young with a lot of extensions providing the same service (grunt-exec, grunt-shell, grunt-run...), some no longer maintained.

Anyway, now on to my script.

# Bash bashing

The shell script creates and populates a test database, used by the REST server when grunt runs the test configuration.
I used `mysql_config_editor` to persist a mySql login configuration and avoid the "Using a password on the command line interface can be insecure" warnings when setting the password from the command line.

I created an `assert` function to check the JSON returned by a query, and an `assertError` to check the http return code of invalid requests (hint: `curl -s -o /dev/null -w "%{http_code}"`). A nice DSL with one-liner tests:

```
assert "POST" "user" "$USER" '{"id":"1","role":"user","token":"..."}'
assertError "POST" "user" "$INVALID_USER" 403
```

But bash was not helping me. One line sums it up:
```
if [ "$RESULT" != "$EXPECTED" ]; then
```
where you learn that `[` is not just a funny parenthesis, but a *command*, which expects `]` as it last argument. This explains why you need this `;` at the end to separate the `then`. And do not try to remove any of the space characters here, they are *all* required. Same thing for the *quotes*, which prevent new spaces from appearing.

Bash is a dinosaur, inherited from the seventies, when you were so happy you could format your 720k floppy using the command line. I knew it, but my script is short, and all I need is to get these two assert methods running.

# And then a test fails

In this test, I give headers to curl, but it manages to mess with the parameters, the simple quotes, the double quotes. When I `echo` the command and run it, I get the correct result. But when bash runs it, I can see on the server log that the header parameters are wrong, maybe because it added some quotes this time.

I've spent hours on these tests, and all the bugs I found so far where in the tests. Bash shall die.
