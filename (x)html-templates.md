Document Templates
==================

XML Declaration
--------------------------------------------------------------------------------

    <?xml version="1.0" [encoding="UTF-8"] [standalone="yes|no"]?>


* `[...]` denotes optional content and `|` denotes "or".
* The arguments are **not** attributes and must be given in this order.
* You probably want `encoding`, but you probably don't need `standalone`.
* You probably want only version `1.0` because it has the widest support.


HTML5
--------------------------------------------------------------------------------

    <!doctype html>
    <html lang="en-gb">
        <head>
            <meta charset="utf-8" /> 
            <title>...</title>

            <meta name="description" content="..." />

            <meta name="viewport" content="width=device-width, initial-scale=0.86, maximum-scale=3.0, minimum-scale=0.86" />
            
            <link rel="icon" href="/favicon.ico" />
            <link rel="canonical" href="..." />

            <script defer="defer" src="..."></script>

            <style>[inline some CSS to prioritise visible content]</style>
            <style>
                <!--// a11y //-->
                a.hidden-but-focusable
                {
                    position: absolute;
                    left:-999px; top: -999px;
                    width: 1px; height: 1px;
                    overflow: hidden;
                    z-index: -9999;
                }
                a.hidden-but-focusable:hover,
                a.hidden-but-focusable:focus,
                a.hidden-but-focusable:active
                {
                    font-size: 20px;
                    color: #00F; background-color: #FFF;
                    left: 0px; top: 0px;
                    padding: 15px; margin: 15px;
                    width: auto; height: auto;
                    overflow: display;
                    border: 4px dotted #00F;
                    z-index: 9999;
                }
                a.hidden-but-focusable > span
                {
                    display: block;
                    font-size: 16px;
                    color: #000;
                }
                span.webfont-one {
                    font-family: WebfontOne;
                }
            </style>

            <noscript id="deferred-styles">
                <!--// https://developers.google.com/speed/docs/insights/OptimizeCSSDelivery //-->
                <link rel="stylesheet" type="text/css" href="..." />
                <link rel="stylesheet" type="text/css" href="https://fonts.googleapis.com/css?family=FontOne:400,700|FontTwo:400,700" />
            </noscript>
        </head>
        <body>
            <a class="hidden-but-focusable" href="#main">Skip to main content<span>(click or press enter to skip; tab to continue to navigation)</span></a>

            <span class="hidden-but-focusable webfont-one"><b>F<i>o</i></b><i>n</i>t</span>
            <span class="hidden-but-focusable webfont-two"><b>F<i>o</i></b><i>n</i>t</span>

            <nav>
                [...]
            </nav>

            <main id="main">
                [...]
            </main>

            <script>
                var loadDeferredStyles = function()
                {
                    var addStylesNode = document.getElementById("deferred-styles");
                    var replacement = document.createElement("div");
                    replacement.innerHTML = addStylesNode.textContent;
                    document.body.appendChild(replacement)
                    addStylesNode.parentElement.removeChild(addStylesNode);
                };
                var raf = window.requestAnimationFrame || window.mozRequestAnimationFrame ||
                  window.webkitRequestAnimationFrame || window.msRequestAnimationFrame;
                if (raf) raf(function() { window.setTimeout(loadDeferredStyles, 0); });
                else window.addEventListener('load', loadDeferredStyles);
            </script>
        </body>
    </html>


* Notes on the "viewport" meta tag:
    + Setting `initial-scale` fixes weird zooming behaviour when rotating an iPhone
    + `width=device-width, initial-scale=0.86, maximum-scale=3.0, minimum-scale=0.86` fixes the weird initial zoom on most phones causing an annoying horizontal scrollbar
    + See [MDN: Using the viewport meta tag to control layout on mobile browsers](https://developer.mozilla.org/en-US/docs/Mozilla/Mobile/Viewport_meta_tag)
    + Useful reference: [common viewport sizes](http://viewportsizes.com/)

* Notes on webfonts and FOUT/FOIT (Flash of Unstyled Text / Flash of Invisible Text)
    + While a webfont downloads:
        - It used to just show a fallback font until it was ready (FOUT)
        - This was sensible!
        - Now most browsers make text invisible until the webfont is ready, for up to three seconds
        - That was a really fucking terrible idea. Like holy shit what the fuck.
            * I almost never swear in a professional context, but I'm angry
              because this is completely inaccessible and inequal behaviour
        - CSS `font-display` is a simple way to fix this
            * But as of 2019 this is Chrome-only
            * And you [can't use font-display with Google fonts yet](https://github.com/google/fonts/issues/358)
        - You have to fix this mess by forcing the font to load with content in each font-weight and -style.
    + TODO add fallback loader JS
        - See e.g. [Comprehensive Webfonts](https://www.zachleat.com/web/comprehensive-webfonts/) (skip to end)

* More notes on webfonts:
    + Raleway is beautiful

* Notes on font-weights:
    * Light: 100
    * Normal: 400
    * Medium: 500
    * Semi/Demi Bold: 600
    * Bold: 700
    * Extra/Ultra Bold: 800
    * Black/Heavy: 900
    * It's not given a keyword value, but 300 is nice.




