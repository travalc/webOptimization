## Website Performance Optimization portfolio project
This project demonstrates learned website optimizations to improve performance and user experience.


### Getting started
  1. Insure that Google PageSpeed Insights Chrome extension is installed to view pagespeed scores.
####Part 1: Optimize PageSpeed Insights score for index.html
  1. Open index.html to view sample page to be tested.
  2. After page has loaded, click the PageSpeed Insights extension on the upper right hand corner of the window to open PageSpeed Insights.
  3. Once PageSpeed Insights has been opened, wait for the analysis to complete and view score for both desktop and mobile.
  4. Please insure that the scores for desktop and mobile are both over 90 for sufficient optimization.
####Part 2: Optimize Frames per Second in pizza.html
  1. Open views/pizza.html to navigate to pizza website that will be tested for frames per second optimization.
  2. Open Chrome DevTools (or your preferred browser's dev tools) and navigate to the "Timeline" panel.
  3. Click the record button in the Timeline panel and scroll down the page. Click the stop button to retrieve results.
  4. In the timeline panel, once results have been retrieved, take a look at the frames per measurement and insure background animations are running at a consistent 60 frames per second to insure sufficient optimization.
  5. Navigate down the page to the resize pizzas bar. Open up the Javascript console in DevTools.
  6. Click on the bar to resize pizzas from small to medium to large.
  7. View Javascript console to see measurement of time to resize pizzas. Insure this time is under 5 ms (milliseconds) to insure sufficient optimization.

####Explanation of optimizations

In index.html, in order to achieve a PageSpeed Insights score of over 90, I made the following optimizations:
  1. Removed Google fonts link as it didn't really add much to the page.
  2. Although it is best practice to keep CSS in separate file, for purpose of this exercise CSS styles were inlined in index.html to maximize efficiency.
  3. All render blocking scripts were moved to end of the body of index.html and async attributes were added to certain scripts so that they run asynchronously while render tree is parsed.
  4. Pizzeria image was drastically minified to optimize page load.

In order to achieve a consistent 60 FPS in views/pizza.html, the following changes were made to views/js/main.js:
  1. In anonymous function attached to DOMContentLoaded event, number of background pizzas created in for loop on line 547 was reduced from 200 to 35 in order to drastically reduce number of operations being run by loop.
  2. Items array is declared in global scope and defined outside of scope of updatePositions in order to prevent this layout read from being repeatedly run. Also, "mover" class for these items is selected using getElementsByClassName instead of querySelectorAll to improve efficiency.
  3. In updatePositions function, variables were defined removing scroll distance from top measurements and items.length from for loops.
  4. The 5 phases of background images were pushed to constArray array and removed from for loop to prevent this operation from being repeatedly read by for loop.
  5. In for loop at line 527, items[i].style.left was changed to items[i].style.transform = 'translateX(..' as the .transform property doesn't trigger layout changes unlike the .left property, greatly reducing time to produce each frame.
