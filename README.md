# Project 5 Website Performance Optimization Portfolio Project
##### by Scott Jensen, April 5, 2016

In this project we are supposed to optimize an online portfolio for speed! In particular, optimize the 
critical rendering path and make this page render as quickly as possible by applying the techniques 
learned in the Critical Rendering Path lesson of the Website Performance Optimization Udacity course. 
index.html should achieve a PageSpeed score of at least 90 for Mobile and Desktop. Optimizations are made 
to views/js/main.js make views/pizza.html render with a consistent frame-rate at 60fps when scrolling. 
Time to resize pizzas is less than 5 ms using the pizza size slider on the views/pizza.html page. Resize 
time is shown in the browser developer tools. A READMEOriginal.md file is included detailing all steps that
were required to successfully run the application and outlines the optimizations that the student was making 
in views/js/main.js for pizza.html. Comments in views/js/main.js for pizza.html are present and effectively 
explain longer code procedures.

To get started, check out the repository, and inspect the code.

### Files, Dependencies, and Use

This project depends on the following files and needs a browser to display the index.html page.

* `css/print.css`
* `css/style.css`
* `images/2048.png`
* `images/cam_be_like.png`
* `images/mobilewebdev.png`
* `images/profilepic.png`
* `images/pizza.png`
* `images/pizzeria.png`
* `js/perfmatters.js`
* `views/js/main.js`
* `views/css/bootstrap-grid.css`
* `views/css/style.css`
* `views/images/pizza.png`
* `views/images/pizzeria.png`
* `views/pizza.html`
* `index.html`
* `project-2048.html`
* `project-mobile.html`
* `project-webperf.html`
* `README.md`
* `READMEOriginal.md`

#### TODO: add instructions about how all steps necessary to download, configure and implement
#### the task runner on the reviewer's desktop should be included in the README.md file.

#### Part 1: Optimize PageSpeed Insights score for index.html

Some useful tips to help you get started:

1. Open NetBeans IDE and make a new project with the existing source found in the repository.
2. Make a new file called package.json and add dependencies for ngrok, pagespeed, and grunt.
3. Run this command in a terminal: npm install.
4. Make a new file called Gruntfile.js and fill the contents with what was found [here]
   (http://www.jamescryer.com/2014/06/12/grunt-pagespeed-and-ngrok-locally-testing/).
5. Push run button in NetBeans IDE which launches chromium on localhost:8383.
6. Download and install [ngrok](https://ngrok.com/) to make your local server accessible remotely.

  ``` bash
  $> cd /path/to/your-project-folder
  $> ngrok http 8383
  ```

7. Copy the public URL ngrok gives you and try running it through PageSpeed Insights! Optional: 
[More on integrating ngrok, Grunt and PageSpeed.]
(http://www.jamescryer.com/2014/06/12/grunt-pagespeed-and-ngrok-locally-testing/)
^^This script that was recommended by Udacity did not work.

##### Profile, optimize, measure...

I used the website optimization, worked on the PageSpeed Insights, using the tunnel through ngrok:
https://developers.google.com/speed/pagespeed/insights/?url=http%3A%2F%2F08331848.ngrok.io%2Ffrontend%2FP5%2Findex.html&tab=mobile
I installed Grunt and used it to minimize my style.css and put in inline with index.html. Then I added the async keyword to my JavaScript 
tags and optimized with the WebPagetest website. We shrank the images down to 100 pixels wide. We moved some of the pictures from the 
remote server to my own server. I found the instructions on Google fonts to load them asynchronously. I reduced the size of a picture 
and changed the other picture to link them in the image file. I moved the script tags down to the HTML page at the bottom of the footer 
tag. Now I got 93% on the mobile app.

#### Part 2: Optimize Frames per Second in pizza.html

To measure Jank, I use the timeline on Chromium development tools, because I develop on
Ubuntu and that's what works on my PC:

1. Open up Chromium and run the website on my local server:
   http://localhost:8383/P5/views/pizza.html.
2. Open up the developer tools, click the Timeline link, click the record timeline button, 
   reload the page, and when the page is done reloading, stop the record timeline button.
3. Zoom inside the main thread until I find function calls and I look at which code line
   number where they were at to get me a clue about what I need to fix.

To optimize views/pizza.html, I modified views/js/main.js until the frames per second 
rate is 60 fps or higher. I have found instructive comments in main.js, and added my own
when and where I change things. 

I found Lesson 4 in the Browser Rendering Optimization class. It was very helpful for 
finding the answer to fixing the code, especially the requestAnimationFrame.

I resized pizzas in less than 5 ms and used the slider of pizza size on the views/pizza.html.
Changed this function as recommended by Cameron Pittman in Lesson 5 - Stop FSL Solution. I
changed the insane changePizzaSizes code by moving the document.querySelectorAll outside the
loop. Then I removed the useless determineDx function and changed the pixels to percentages 
for the pizza width.

You might find the FPS Counter/HUD Display useful in Chrome developer tools described here: 
[Chrome Dev Tools tips-and-tricks](https://developer.chrome.com/devtools/docs/tips-and-tricks).

### Optimization Tips and Tricks
* [Optimizing Performance](https://developers.google.com/web/fundamentals/performance/ "web performance")
* [Analyzing the Critical Rendering Path](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/analyzing-crp.html "analyzing crp")
* [Optimizing the Critical Rendering Path](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/optimizing-critical-rendering-path.html "optimize the crp!")
* [Avoiding Rendering Blocking CSS](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/render-blocking-css.html "render blocking css")
* [Optimizing JavaScript](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/adding-interactivity-with-javascript.html "javascript")
* [Measuring with Navigation Timing](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/measure-crp.html "nav timing api"). We didn't cover the Navigation Timing API in the first two lessons but it's an incredibly useful tool for automated page profiling. I highly recommend reading.
* <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/eliminate-downloads.html">The fewer the downloads, the better</a>
* <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/optimize-encoding-and-transfer.html">Reduce the size of text</a>
* <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/image-optimization.html">Optimize images</a>
* <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/http-caching.html">HTTP caching</a>

### Customization with Bootstrap
The portfolio was built on Twitter's <a href="http://getbootstrap.com/">Bootstrap</a> framework. All 
custom styles are in `dist/css/portfolio.css` in the portfolio repo.

* <a href="http://getbootstrap.com/css/">Bootstrap's CSS Classes</a>
* <a href="http://getbootstrap.com/components/">Bootstrap's Components</a>
