Efficient way to re-use a front-end library in your project
-----------------------------------------------------------

by Renoir Boulanger <http://twitter.com/renoirb>

Extending or re-using one (or many) front-end libraries is a very common practice.

For example. Imagine you want to create a new project, and you already have a few modules available such as a few widgets (e.g. (Flash/alert/notification messagge)[http://patternry.com/p=feedback-messages/]) previously created.

This tutorial is not about how to version or use an external but explain how I recommend using an external source and import it from project to project, while isolating your own project-specific code but heavily use it's concepts.


Common mistake
==============

Unfortunately, a common mistake is that people simply copy-paste code from project to project without real version scheme or version control mechanisms at all (e.g. Git, Subversion). From a set of personnal, mixed with some other project's source. 

Carrying practices and dead-wood code alone every project, without follow up from the author or the source.


A better way?
=============

A way I figured out would be to use the same concepts of programming practices. Import, extend your specialized version, separate concerns, re-use. proffit.


Compiled CSS
============

Why?

Because it permits you many things, ideal for project reuse.

If you ever had:

- Commented your CSS file with notes similar to `background-color:#000000 /* THEME: color #595958 plus 100% darker */`
- Have sparated blocks and search replace all instances of a color to replace
- Wanted to separate alignment, font-size, and bordering without changing everywhere
- Wished something like `color: darken($themeColor, 10%);` existed
- Wanted to use CSS's native @import to separate, but without the need to explode http requests

This is some of my own personnal reasons I prefer using compiled CSS.

Personally, I like LESS. It runs in the browser, can run on the server side (within NodeJS), compile from the command line, and be automated. My killer argument is that it can only as simple as.

    ```
    <link rel="stylesheet/less" type="text/css" href="styles.less" />
    <script src="less.js" type="text/javascript"></script>
    ```

(See usage for more details)[http://lesscss.org/#usage]

And copy paste from `localStorage` from Firefox/Chrome the compiled css and commit the css to the project's as minified CSS.


How to do?
==========

Create a folder within your project that will handle external libraries.

    ```
    (rest of your project)
    web/
      assets/
        lib/
          bootstrap/
          misc/
        js/
        main.less
    ```      

In the `web/assets/lib/bootstrap/` either download, svn external or submodule from a specific version and keep it as it is. untouched.

While in this example I use Twitter Bootstrap, I often use some specific sup-parts from the also Excellent (Zurb Foundation)[http://foundation.zurb.com/], (their font-icons, for example)[http://www.zurb.com/playground/foundation-icons] library.

Then. In `main.less` I copy-paste the conteent from `web/assets/lib/bootstrap/less/bootstrap.less` content, into `web/assets/main.less`, adjust  paths accordingly.

(Not finished)