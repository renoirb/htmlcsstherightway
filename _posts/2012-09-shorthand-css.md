Efficient shorthand css techniques
----------------------------------
Use shorthand css techniques, when saving those extra bytes is crucial for you!

1. Padding
----------

`Case 1.1 - Padding for all four sections is uniform.`
```css
/* longhand */
padding-top:5px;
padding-right:5px;
padding-bottom:5px;
padding-left:5px;

/* shorthand */
padding:5px;
```

`Case 1.2 - Padding for (top & bottom) and (right & left) is the same.`
```css
/* longhand */
padding-top:1px;
padding-right:2px;
padding-bottom:1px;
padding-left:2px;

/* shorthand */
padding:1px 2px;
```

`Case 1.3 - Padding for right & left is the same.`
```css
/* longhand */
padding-top:1px;
padding-right:2px;
padding-bottom:3px;
padding-left:2px;

/* shorthand */
padding:1px 2px 3px;
```

`Case 1.4 - Padding for all four sections is different.`
```css
/* longhand */
padding-top:1px;
padding-right:2px;
padding-bottom:1px;
padding-left:2px;

/* shorthand */
padding:1px 2px;
```

2. Margin
----------

`Case 2.1 - Margin for all four sections is uniform.`
```css
/* longhand */
margin-top:5px;
margin-right:5px;
margin-bottom:5px;
margin-left:5px;

/* shorthand */
margin:5px;
```

`Case 2.2 - Margin for (top & bottom) and (right & left) is the same.`
```css
/* longhand */
margin-top:1px;
margin-right:2px;
margin-bottom:1px;
margin-left:2px;

/* shorthand */
margin:1px 2px;
```

`Case 2.3 - Margin for right & left is the same.`
```css
/* longhand */
margin-top:1px;
margin-right:2px;
margin-bottom:3px;
margin-left:2px;

/* shorthand */
margin:1px 2px 3px;
```

`Case 2.4 - Margin for all four sections is different.`
```css
/* longhand */
margin-top:1px;
margin-right:2px;
margin-bottom:1px;
margin-left:2px;

/* shorthand */
margin:1px 2px;
```

3. Border
---------

`Case 3.1 - Border width, style & color is specified.`
```css
/* longhand */
border-width:1px;
border-style:solid;
border-color:#000;

/* shorthand */
border:1px solid #000;
```

4. Font
-------

`Case 4.1 - Font style, variant, weight, size, height, family is specified.`
```css
/* longhand */
font-style:italic;
font-variant:small-caps;
font-weight:bold;
font-size:1em;
line-height:140%;
font-family:"Lucida Grande",sans-serif;

/* shorthand */
font:italic small-caps bold 1em/140% "Lucida Grande",sans-serif;
```

5. Background
-------------

`Case 5.1 - Background color, image, repeat, attachment, position is specified.`
```css
/* longhand */
background-color:#f00;
background-image:url(background.gif);
background-repeat:no-repeat;
background-attachment:fixed;
background-position:0 0;

/* shorthand */
background:#f00 url(background.gif) no-repeat fixed 0 0;
```