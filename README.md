## Front-end Nanodegree Website Optimization Project

The challenge for this project was to optimize this an portfolio for speed. Using [Google's PageSpeed](https://developers.google.com/speed/pagespeed/insights/) service, the optimized index.html page and associated dependencies must attain a score of 90 or better for both the mobile and desktop views. At last measure, the optimizations detailed below resulted in a [score of 99 for mobile](https://developers.google.com/speed/pagespeed/insights/?url=https%3A%2F%2Fgeoffhumphrey.github.io%2Ffrontend-nanodegree-mobile-portfolio%2F) and [91 for desktop](https://developers.google.com/speed/pagespeed/insights/?url=https%3A%2F%2Fgeoffhumphrey.github.io%2Ffrontend-nanodegree-mobile-portfolio%2F&tab=desktop).

### Optimizations

Optimizations for the project focused on these main sources: /index.html (and associated files), images contained in the /img and /views/imgages directories, and /views/js/main.js.

### index.html

_Note that the following changes were also applied to the /project-2048.html, /project-mobile.html, and /project-webperf.html files as well as /index.html._

A quick change that was very easy to make, but had a great impact on performance, was to load the Google Analytics script asynchronously:
```<script async src="http://www.google-analytics.com/analytics.js"></script>```

The same can be applied to the /js/perfmatters.js file:
```<script async src="js/perfmatters.js"></script>```

Analytics script loads were also moved to the end of the page.

A media="print" attribute was added to the print.css tag to lower the priority of its load.

Finally, referenced a smaller and more compressed version of pizzeria.jpg instead of requiring the browser to resize the behemoth original image (see image optimizations below)

### Image Optimizations

All images were compressed utilizing Photoshop, reducing their sizes to optimal levels for their respective uses. I realize that there are image optimizers available via Grunt. In the interest of time, I fell back to a more familiar way using Photoshop. A goal of mine is to get fully versed in Grunt to make image optimization and minifying far less "manual" processes.

In particular, the /views/images/pizzeria.jpg file, prior to optimization, was a burly 2.25 megabytes! Utilizing a combination of optimization and the [srcset](https://developers.google.com/web/fundamentals/design-and-ux/responsive/images) attribute for [responsive images](https://developer.mozilla.org/en-US/docs/Learn/HTML/Multimedia_and_embedding/Responsive_images) so that the proper image scale (and thus, filesize) is presented to the user depending upon their device.


