# Efficient way to re-use a front-end library in your project #

by [Renoir Boulanger](http://renoirboulanger.com)

Extending or re-using one (or many) front-end libraries is a very common practice. The holy-grail of efficiendy
in front-end development practices is to be able to import re-usable libraries and adapt to the project's requirements.

For example. Imagine you want to create a new project, and you already have a few modules available e.g. 
[alert or notification message](http://patternry.com/p=feedback-messages) that could be used in any other projects.

This tutorial is about isolating your own project-specific code, get the benefit of already made patterns that can then 
mixed-matched for every specific views you may need.


## A Common mistake ##

Unfortunately, a common mistake is that people simply copy-paste code from project to project without real 
version scheme or version control mechanisms at all (e.g. Git, Subversion). From a set of personnal, mixed 
with some other project's source.  

Carrying practices and "dead-wood" code alone every project, without follow up from the author or the source.

Although source-control is suggested, the essential to remember is to *not modify* external libraries. 
But merely extend and adapt; this is where CSS parsers comes in handy (more on this later).


## A better way? ##

A better would be to use the same concepts that programmers uses in the Object Oriented paradygm. In a few words:

    Import, extend your specialized version, separate concerns, re-use. proffit.

This is roughly what [OOCSS](http://oocss.org/) (Object Oriented CSS) stands for.

But why re-inventing when you can just use and reuse existing in an efficient way? 


## Compiled CSS ##

To be able to re-use, and separate concerns, we have no choice, we need something to process and replace things around.

You may follow my drift if you ever had wishes similar to those:

- Commented your CSS file with notes similar to `background-color:#000000 /* THEME: color #595958 plus 100% darker */`
- Have sparated blocks and search replace all instances of a color to replace
- Wanted to separate alignment, font-size, and bordering without changing everywhere
- Wished something like `color: darken($themeColor, 10%);` existed
- Wanted to use CSS's native @import to separate, but without the need to explode http requests

This is some of my own personnal reasons I prefer using compiled CSS.

After that, there is a lot of CSS parsers.

Personally, I like [LESS](http://lesscss.org/). Because: it can run in the browser, on the server side (within NodeJS),
compile from the command line, and be used in automated deployment tools. 

A killer argument is that it can only as simple as.

    <link rel="stylesheet/less" type="text/css" href="styles.less" />
    <script src="less.js" type="text/javascript"></script>

[See usage for more details](http://lesscss.org/#usage)

To use in production, get the compiled CSS in the `localStorage` from Firefox/Chrome (in the developer tools 
such as Firebug) the compiled css and commit the css to the project's as minified CSS.

Not to forget that you can also use as much as you need `@include` statements and separate your code, but end up 
with ONE css file.


## How to do? ##

Create a folder within your project that will handle external libraries.

    (rest of your project tree)
    web/
      assets/
        lib/
          bootstrap/
          misc/
        js/
        myproject/
          _variables.less
          _adaptations.less
          _modules.less
          _states.less
          _fonts.less
        main.less

In the `web/assets/lib/bootstrap/` either download, svn external or submodule from a specific version and keep it as 
it is. untouched.

While in this example I use Bootstrap, I often use some specific sup-parts from the also Excellent
[Zurb Foundation](http://foundation.zurb.com/), [their font-icons, library](http://www.zurb.com/playground/foundation-icons) for example.

Then. In `main.less` (or any name you choose as your "main"); copy-paste the conteent from the original
`web/assets/lib/bootstrap/less/bootstrap.less` into `web/assets/main.less`, and adjust paths accordingly.


## Customization ##

Now that you have this basic workspace, have a look at Bootstrap's `variables.less` file,
see `myproject/_variables.less` has my own version of the original.

Beware though. To avoid compilation errors; just make sure to include the original `variables.less` file, and only 
override what you need.

The rest comes by creating patterns and separate concerns. 

For example, Imagine you have the module `.form-actions` and you need to adjust for your needs.

We have the original:

    .navbar-fixed-top {
      position: fixed;
      top: 0;
      right: 0;
      left: 0;
      z-index: @zindexFixedNavbar;
    }
    .navbar-fixed-top .navbar-inner {
      padding-left:  0;
      padding-right: 0;
      .border-radius(0);
    }

Then, in your own project code (e.g. in `_adaptations.less`), you could adjust the original with specific styling:

    .myproject > .navbar-fixed-top .divider-vertical {
      background-color: lighten(@themeDarkestColor, 6%);
      border-right-color: darken(@themeDarkestColor, 15%);
      height: 62px;
    }

See also that I did not overspecify but precisely wanted to be the direct children (`>`) of `.myproject` that, in this 
case, is assigned to the `<body>` tag.


## In conclusion ##

The key for re-use is to separate the concerns and not edit your external libraries. By doing so, you will learn
how to be very specific with shorthand and selectors, without creating ridiculous selector trails.
