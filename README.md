#deck.ext.js

Deck.ext.js provides a set of extensions, themes and use cases for the deck.js framework.
Deck.js is a JavaScript library for building modern HTML presentations which is flexible enough to let advanced CSS and JavaScript authors craft highly customized decks, but also provides templates and themes for the HTML novice to build a standard slideshow.

Currently Deck.ext.js provides the following extensions:

- deck.toc.js, provides a support for TOC,
- deck.asvg.js, provides a support for including and animating SVG images,
- deck.clone.js, provides a support for cloning a deck presentation to another window,
- deck.notes.js, provides a support for adding and viewing speaker notes.
- deck.animator.js, provides a support for animating HTML elements.

Currently Deck.ext.js provides the following themes:

- beamer, aims to provides a team similar to the Latex beamer

I'll soon provide an illustration on how to use deck.toc.js together with the beamer themes. 

##deck.toc.js extension

This extension provides the support for TOC within the deck.js framework.

### General Idea

The `deck.toc.js` extension uses the H* tags to build the TOC.

- H1 represents the title of the presentation
- H2 corresponds to a section
- H3 corresponds to a subsection
- H4 corresponds to a subsubsection

The TOC is automatically constructed when `deck.init` is called, and pressing
on `t` will toggle the TOC panel.

Elements in the TOC panel are clickable and thus it provides another way
to navigate easily in the slides.

### Example

The following:

        <section class="slide" id="title-slide">
            <h1>The Presentation Title</h1>
        </section>

        <section class="slide">
            <h2>Section 1</h2>
            <p>If you want to learn about making your own themes, extending deck.js, and more, check out the&nbsp;<a href="../docs/">documentation</a>.</p>
        </section>

        <section class="slide">
            <h3>Section 1.1</h3>
            <p>If you want to learn about making your own themes, extending deck.js, and more, check out the&nbsp;<a href="../docs/">documentation</a>.</p>
        </section>

        <section class="slide">
            <h3>Section 1.2</h3>
            <p>If you want to learn about making your own themes, extending deck.js, and more, check out the&nbsp;<a href="../docs/">documentation</a>.</p>
        </section>

        <section class="slide">
            <h2>Section 2</h2>
            <p>If you want to learn about making your own themes, extending deck.js, and more, check out the&nbsp;<a href="../docs/">documentation</a>.</p>
        </section>

        <section class="slide">
            <h2>Section 3</h2>
            <p>If you want to learn about making your own themes, extending deck.js, and more, check out the&nbsp;<a href="../docs/">documentation</a>.</p>
        </section>

will build the following TOC:

- The Presentation Title
    - Section 1
        - Section 1.1
        - Section 1.2
    - Section 2
    - Section 3

##deck.asvg.js extension

The `deck.asvg.js` extension (for Animated SVG) allows users to add animated schema into their presentation.

TO DETAIL THIS SECTION

##deck.clone.js extension

**ONLY TESTED WITH CHROMIUM and CHROME browser**

The `deck.clone.js` extension allows users to clone a deck presentation so that a clone of this presentation appears in a separate popup window.
The `deck.change` events of the master presentation are propagated to the cloned windows, so that when you navigate between the slides in the master window the navigation will operate nicely in the all the cloned windows. 
The advantage of cloning a deck presentation is that, on the master window you have the slides displayed while in the cloned window you have the speaker notes displayed.
The speaker notes can be displayed by using the `deck.notes.js` extension.

To clone a deck presentation just press `c`.

##deck.notes.js extension

The `deck.notes.js` extensions allows users to toggle speaker notes display by pressing the `n` key.
To add a note to a slide just add a simple div with a .notes class like below:


### Example

        <section class="slide" id="title-slide">
            <h1>The Presentation Title</h1>
        </section>

        <section class="slide">
            <h2>Section 1</h2>
            <p>If you want to learn about making your own themes, extending deck.js, and more, check out the&nbsp;<a href="../docs/">documentation</a>.</p>
            <div class="notes">
            This slide has speaker notes.
            </div>
        </section>

        <section class="slide">
            <h3>Section 1.1</h3>
            <p>If you want to learn about making your own themes, extending deck.js, and more, check out the&nbsp;<a href="../docs/">documentation</a>.</p>
        </section>

        <section class="slide">
            <h3>Section 1.2</h3>
            <p>If you want to learn about making your own themes, extending deck.js, and more, check out the&nbsp;<a href="../docs/">documentation</a>.</p>
            <div class="notes">
            This slide has speaker notes too.
            </div>
        </section>

This extension is better used together with the `deck.clone.js` extension.

##deck.animator.js extension

The `deck.animator.js` extension allows users animate HTML elements in their slides.
There is at most an animator for each slide.

The slide is linked to its animator thanks to the value of its custom attribute `data-dahu-animator`.
The JSON description of an animation follows the following format: 

        {
          "target": A CSS selector for the slides in which the animation occurs,
          "actions": [
            {
              "id": A chain to identify the action,
              "type": either "move", "appear" or "disappear",
              "target": The id of the HTML element to which the action applies,
              "duration": The duration of the action in ms,
              "trX": ("move" type only) the value in pixels of the abs translation,
              "trY": ("move" type only) the value in pixels of the ord translation
            },
            ...
          ]
        }

The following example makes the text disappear, then move and reappear as it moves:


### Example

        <section class="slide" id="containing_slide" data-dahu-animator="animDescription">
            <div id="moving_text">
                This text is animated
            </div>
            <script type="text/javascript">
                var animDescription = {
                    "target": "#containing_slide",
                    "actions": [
                        {
                            "id": "action1",
                            "type": "disappear",
                            "target": "#moving_text",
                            "trigger": "onChange",
                            "duration": 1000
                        },
                        {  
                            "id": "action2,
                            "type": "move",
                            "target": "#moving_text",
                            "trigger": "afterPrevious",
                            "trX": 150,
                            "trY": 100,
                            "duration": 2000
                        },
                        {
                            "id": "action3",
                            "type": "appear",
                            "target": "#moving_text",
                            "trigger": "withPrevious",
                            "duration": 1000
                        }
                    ]
                };
            </script>
        </section>