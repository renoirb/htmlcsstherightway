How to change colors and parameters in a CSS framework such as Bootstrap
--------------------------------------------------------------------------------

I thought to re-visit the previous post because somebody asked on the
Bootstrap Mailing list if they can change some elements colors
using plain css.

I was assuming that the person do not know the existence of css pre-processors
so I shared the following blueprint on how to do.

1. Download [bootstrap distribution](http://getbootstrap.com) and the less.js file.

It is a bad practice to modify external library but better extending it. Here's how

2. Create a copy of bootstrap.less outside of bootstrap distribution folder.

3. Adjust path on the bootstrap.less @include directives.

4. Create your own variables.less

5. Call that one in your own new bootstrap.less file

6. The new variables.less file should have only variables you want to rewrite. And it should have an include at its top to the original (aka overloading) variables.less file

Follow [LESS css pre-processor](http://lesscss.org/) howto to use less and yoi can change colours!

Best regards
