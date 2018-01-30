## Front-end Nanodegree Website Optimization Project

The challenge for this project was to optimize this an portfolio for speed. Using [Google's PageSpeed](https://developers.google.com/speed/pagespeed/insights/) service, the optimized index.html page and associated dependencies must attain a score of 90 or better for both the mobile and desktop views. At last measure, the optimizations detailed below resulted in a [score of 99 for mobile](https://developers.google.com/speed/pagespeed/insights/?url=https%3A%2F%2Fgeoffhumphrey.github.io%2Ffrontend-nanodegree-mobile-portfolio%2F) and [96 for desktop](https://developers.google.com/speed/pagespeed/insights/?url=https%3A%2F%2Fgeoffhumphrey.github.io%2Ffrontend-nanodegree-mobile-portfolio%2F&tab=desktop).

### Optimizations

Optimizations for the project focused on these main sources: index.html (and associated files), images contained in the img and views/images directories, and views/js/main.js.

### index.html

_Note that the following changes were also applied to the project-2048.html, project-mobile.html, and project-webperf.html files as well as /index.html._

A quick change that was very easy to make, but had a great impact on performance, was to load the Google Analytics script asynchronously:

```<script async src="http://www.google-analytics.com/analytics.js"></script>```

The same can be applied to the /js/perfmatters.js file:

```<script async src="js/perfmatters.js"></script>```

The js/perfmatters.js code was then minified (using [javascript-minifier.com](https://javascript-minifier.com/)) and added to a new file called js/perfmatters.min.js. The reference in the index.html was updated to use this file.

Google Analytics script loads were also moved to the end of the page.

A media="print" attribute was added to the print.css tag to lower the priority of its load.

Since the styles defined in styles.css were not extensive, the entire script was first minified (using [cssminifier.com](https://cssminifier.com/)) and then added to /index.html inline in the `<head>`.

Finally, referenced a smaller and more compressed version of pizzeria.jpg instead of requiring the browser to first load and then resize the behemoth original image (see Image Optimizations below).

### views/pizza.html

Minified (using [cssminifier.com](https://cssminifier.com/)) and inlined the CSS styles from styles.css into the `<head>`.

Minified the views/css/bootstrap-grid.css code (using [cssminifier.com](https://cssminifier.com/)) and moved to a new file called views/css/bootstrap-grid.min.css. Referenced this file in pizza.html.

Compressed the views/images/pizza.png file (used in the page background).

### views/js/main.js

Most of the optimizations for the pizzeria portfolio item were made in this file:
- changePizzaSizes function
  - replaced the querySelectorAll methods with the more optimal getElementsByClassName.
  - determineDX function seemed to be a bit redundant and the only part of the function that was needed was the sizeSwitcher function.
  - moved the new width calculation out of the for loop as there was no need to calculate that more than once.
- updatePositions function.
  - replaced querySelectorAll in favor of getElementsByClassName.
  - moved the items variable outside the function, since we're referencing the same class name, no need to declare it each time the function runs
  - moved the scrollTop variable out of the loop since to reduce the number of lookups.
  - thanks to an idea presented by mcs in a [discussion forum post](https://discussions.udacity.com/t/project-4-how-do-i-optimize-the-background-pizzas-for-loop/36302?source_topic_id=248974), we can leverage caching by declaring an array and pushing only 6 values to it. Less expensive to generate only six than to recalculating each time when the phase variable is created in the loop.
- updated the loop that "draws" background pizzas upon scroll from the original 200 to one that is easily obtainable (window height divided by 50, window width devided by 50).

The views/js/main.js code was then minified (using [javascript-minifier.com](https://javascript-minifier.com/)) and added to a new file called view/js/main.min.js. The reference in the views/pizza.html was updated to use this file.

### Image Optimizations

All images utilized throughout the portfolio were compressed utilizing Photoshop, reducing their sizes to optimal levels for their respective uses. I realize that there are image optimizers available via Grunt. In the interest of time, I fell back to a more familiar way using Photoshop. A goal of mine is to get fully versed in Grunt to make image optimization and minifying far less "manual" processes.

In particular, the /views/images/pizzeria.jpg file, prior to optimization, was a burly 2.25 megabytes! Utilizing a combination of optimization and the [srcset](https://developers.google.com/web/fundamentals/design-and-ux/responsive/images) attribute for [responsive images](https://developer.mozilla.org/en-US/docs/Learn/HTML/Multimedia_and_embedding/Responsive_images) so that the proper image scale (and thus, filesize) is presented to the user depending upon their device.


