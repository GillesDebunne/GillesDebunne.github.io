---
layout: post
title: Less is more
---

Today, I tried to switch to [less](http://lesscss.org/) instead of plain old `css` for a project. Turned out not to be so easy.

Using `sass` or `less` is now an obvious choice to overcome `css`' limitations. Sass is supposedly a bit more powerful, but I'm planning to tweak a bootstrap theme, and its native language is less. And using any of these is still way better than css.

# Grunt process

I installed `grunt-recess` which *seemed* the right plugin for less processing.

Tweaking from readings here and there, it took me two hours to get grunt to compile the less files and live reload my site on change. Turns out it was probably correctly configured from the beginning, except for a typo in a path name (I would have *sooo* loved at least a little warning).

# Less version

But then, I got an error when building the vanilla bootstrap. Turns out `grunt-recess` is using less v1.3, while bootstrap uses the v1.4 `extend` feature, and less' latest version is v1.7.

Switching to [`grunt-contrib-less`](https://github.com/gruntjs/grunt-contrib-less) instead, which seems more official and actually runs less v1.7. I guess I'll first look at the [gruntjs](http://gruntjs.com/) web site next time I need a new grunt plugin. It's a bit the jungle out there (why not try [assemble-less](https://github.com/assemble/assemble-less) whie at it?). A new build system, [gulp](http://gulpjs.com/) is emerging and may replace `grunt`, but we'll see this later.

Here is the final `Gruntfile` configuration:

```
less: {
  dev: {
    files: {
      '.tmp/styles/bootstrap.css': '<%= yeoman.app %>/styles/bootstrap.less'
    }
  },
  prod: {
    options: {
      cleancss: true,
      compress: true
    },
    files: {
      '.tmp/styles/bootstrap.css': '<%= yeoman.app %>/styles/bootstrap.less'
    }
  }
},
```

Again, not so happy about this `files` duplication for the `dev` and `prod` environments.

Also added this in the `watch` section for live reload:

```
less: {
  files: ['<%= yeoman.app %>/styles/{,*/}*.less'],
  tasks: ['less:dev']
},
```

# Bootswatch customisation

Once bootstrap was successfully compiled from less to css, with live reload I could finally start customising.
I started from a [bootswatch](http://bootswatch.com/) theme. I was worried I would have to modify files directly: I do not want to touch the original bootstrap files, which will evolve and are version controlled using `bower`.

Turns out to be easy, 
-  just copy `bootstrap.less` and edit it to `import` the original bootstrap files, located in `bower_components/bootstrap/less`.
-  use a local and customised `variables.less` file instead of the original one to define the main variables.
-  finally import `bootswatch.less` and `myCustomStyle.less` before `utilities.less` to add custom style.

Now converting my css tweaks into less, the web page structure appears in the less file, which is cleaner and simpler.
