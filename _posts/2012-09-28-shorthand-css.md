Efficient shorthand css techniques
----------------------------------
by [pankajparashar](https://github.com/pankajparashar)

Use shorthand CSS techniques, when saving those extra bytes is crucial for you!

But beware of the cascade. If you set a specific effect, make sure there is not 
already defined. Being precise becomes more and more important as the code stacks up.

## 1. Padding

### Case 1.1 - Padding for all four sections is uniform

    /* longhand */
    padding-top:5px;
    padding-right:5px;
    padding-bottom:5px;
    padding-left:5px;

    /* shorthand */
    padding:5px;


### Case 1.2 - Padding for (top & bottom) and (right & left) is the same


    /* longhand */
    padding-top:1px;
    padding-right:2px;
    padding-bottom:1px;
    padding-left:2px;

    /* shorthand */
    padding:1px 2px;


### Case 1.3 - Padding for right & left is the same


    /* longhand */
    padding-top:1px;
    padding-right:2px;
    padding-bottom:3px;
    padding-left:2px;

    /* shorthand */
    padding:1px 2px 3px;


### Case 1.4 - Padding for all four sections is different


    /* longhand */
    padding-top:1px;
    padding-right:2px;
    padding-bottom:3px;
    padding-left:4px;

    /* shorthand */
    padding:1px 2px 3px 4px;


## 2. Margin

### Case 2.1 - Margin for all four sections is uniform


    /* longhand */
    margin-top:5px;
    margin-right:5px;
    margin-bottom:5px;
    margin-left:5px;

    /* shorthand */
    margin:5px;


### Case 2.2 - Margin for (top & bottom) and (right & left) is the same

    /* longhand */
    margin-top:1px;
    margin-right:2px;
    margin-bottom:1px;
    margin-left:2px;

    /* shorthand */
    margin:1px 2px;


### Case 2.3 - Margin for right & left is the same

    /* longhand */
    margin-top:1px;
    margin-right:2px;
    margin-bottom:3px;
    margin-left:2px;

    /* shorthand */
    margin:1px 2px 3px;


### Case 2.4 - Margin for all four sections is different

    /* longhand */
    margin-top:1px;
    margin-right:2px;
    margin-bottom:1px;
    margin-left:2px;

    /* shorthand */
    margin:1px 2px;


## 3. Border

### Case 3.1 - Border width, style & color is specified

    /* longhand */
    border-width:1px;
    border-style:solid;
    border-color:#000;

    /* shorthand */
    border:1px solid #000;


### Case 3.2 - Border width for all four sides is specified

    /* longhand */
    border-top-width:1px;
    border-right-width:2px;
    border-bottom-width:3px;
    border-left-width:4px;

    /* shorthand */
    border-width:1px 2px 3px 4px;


## 4. Font

A common caveat about fonts is that, like colors, their effect bubbles up until it is redefined in a stronger selector.

Beware of the original definition then, when needed, use the most precise longhand to do your effect. 

Sometimes it is even better to create a specific sub class (e.g. `bolded`) than being over 
specific (e.g. `header > nav strong.title {}`, albeit specific, is considered as a VERY BAD practices)

### Case 4.1 - Font style, variant, weight, size, height, family is specified

    /* longhand */
    font-style:italic;
    font-variant:small-caps;
    font-weight:bold;
    font-size:1em;
    line-height:140%;
    font-family:"Lucida Grande",sans-serif;

    /* shorthand */
    font:italic small-caps bold 1em/140% "Lucida Grande",sans-serif;


##5. Background

### Case 5.1 - Background color, image, repeat, attachment, position is specified


    /* longhand */
    background-color:#f00;
    background-image:url(background.gif);
    background-repeat:no-repeat;
    background-attachment:fixed;
    background-position:0 0;

    /* shorthand */
    background:#f00 url(background.gif) no-repeat fixed 0 0;


## 6. Colors

### Case 6.1 - When a color consists of three pairs of hexadecimal digits, you can omit one digit from each pair


    /* longhand */
    color:#000000;
    color:#336699;
    color:#0099CC;

    /* shorthand */
    color:#000;
    color:#369;
    color:#09C;


## 7. List Style

### Case 7.1 - When list type, position and image is specified


    /* longhand */
    list-style-type:square;
    list-style-position:inside;
    list-style-image:url(image.gif);

    /* shorthand */
    list-style:square inside url(image.gif);


## 8. Outline

### Case 8.1 - When outline color, style and width is specified


    /* longhand */
    outline-color:#f00;
    outline-style:solid;
    outline-width:2px;

    /* shorthand */
    outline:#f00 solid 2px;

