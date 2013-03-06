# Creating and using jQuery events, the thing I wished I knew before

During web development, it often happens you want to attach events handler on 
something in your page. A common usage could be you want to flip a plus sign to a minus 
sign when you click on a button.

    <a href="/some/url/324" class="flip-icon" data-target="#generated-324"><i class="icon-plus"></i></a>

Later in a script you may be compelled to do something similar to the following (assuming you are using jQuery):

    $(document).ready(function(){
    // Rest of the document in document.ready
    // DO NOT USE AS-IS, SEE LAST EXAMPLE

        $('.flip-icon.).click(function(event){  
            event.preventDefault(); 
            var clicked = $(this);
            var flipElement = clicked.find('i');
            if (flipElement.hasClass('icon-plus')) {
                flipElement.removeClass('icon-plus').addClass('icon-minus');
            } else {
                flipElement.removeClass('icon-minus').addClass('icon-plus');
            }
        });
    });
    
But what happens if you want to add other events such as, for example, *activating an accordion*. You may end up with 
duplicating events and get some collisions.

*Did you know that the 'click' event is only a string and you can create any event name you may want?*

To describe what I am refering to, I have a add an other behavior that will also, in part, require the previous example.

Imagine we have an accordion managed already grabbing the element's `a[data-target]` click event handler.

    $(document).ready(function(){
    // Rest of the document in document.ready
    // DO NOT USE AS-IS, SEE LAST EXAMPLE

        $('a[data-target]').click(function(event){
            // do the accordion stuff
        });
    });

But, what if for some reason, our page has to reload some sections and our event handler managing the `a[data-target]` click gets lost

Instead, of creating a click specific event handler (what if we want to change) and be potentially lost with the element to attach event onto.

You can use [jQuery's `on` method](http://api.jquery.com/on/) and attach an event to the `<body>`, a safe element that every document has.

Things to note about the `on` method:

* First parameter is an event name, can be ANYTHING (yes, you read it), space separated
* Second element is on what to listen, can be null
* a `Function` object to handle the event

Also, there is nice thing about bubbling. 

When an event happens, the event crawls the DOM up to the body (called 'catch')
then gets back to the triggerer element (called 'bubbling') and firing in that order all event handlers.

Knowing all of this now, instead of attaching a single event type handler to a specific element, let's take 
advantage of our new knowledge.


    'use strict';
    $(document).ready(function(){
    // Rest of your document

        // Look at the 'flip-my-icon-event', we just made-up that one. See below.
        $('body').on('click flip-my-icon-event', '.flip-icon', function(){
    /* Look here     *************************                                       */
            // Let's put it also in a self-executing anonymous, to isolate scope
            (function(triggered){

                // Same as earlier.
                var clicked = $(this);
                var flipElement = clicked.find('i');
                if (flipElement.hasClass('icon-plus')) {
                    flipElement.removeClass('icon-plus').addClass('icon-minus');
                } else {
                    flipElement.removeClass('icon-minus').addClass('icon-plus');
                }
                // End same as earlier

            })($(this)); // this fires the self-executing.
        });

        $('body').on('click', 'a[data-target]', function(event){
            event.preventDefault();

            // do the accordion stuff
            var collapsible = $($(this).attr('data-target'));
            if (typeof collapsible.attr('data-collapsible') === 'undefined')  {
                collapsible
                    .collapse()
                    .attr('data-collapsible', 'applied')
                    .on('show', function(){
                        jQuery(this).parent().removeClass('is-hidden');
                    })
                    .on('hide', function(){
                        jQuery(this).parent().addClass('is-hidden');
                    });
            // End do the accordion stuff

            jQuery(this).trigger('click').trigger('flip-my-icon-event');
    /* Look here                         *******************************        */
            }
        });
    });

The following works, because of the following trigger html pattern, as from the begining:

    <a href="/some/url/324" class="flip-icon" data-target="#generated-324"><i class="icon-plus"></i></a>

And of the following:

* We have an icon for `.icon-plus` and `.icon-minus` class names
* The `a[data-target]` attribute has ALSO a `.flip-icon` class name
* The `a[data-target]` triggers our made-up `flip-my-icon-event` event to an element that also matches (see the two 'look here' comments)

*References*

* [**WPD** Events in Javascript (WebPlatform.org)](http://docs.webplatform.org/wiki/tutorials/events_in_javascript) 
* [jQuery `trigger` method](https://github.com/jquery/jquery/blob/master/src/event.js#L206) from the jQuery source
* [jQuery `on` method](https://github.com/jquery/jquery/blob/master/src/event.js#L715) from the jQuery source
* [jQuery documentation `on` method](http://api.jquery.com/on/)
* 
**Note** direct events handlers such as `live`, or `delegate` are considered deprecated (as of jQuery 1.7) [see delegate API](http://api.jquery.com/delegate/) and [live API](http://api.jquery.com/live/) notes.

