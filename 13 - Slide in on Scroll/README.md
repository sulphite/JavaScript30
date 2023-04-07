# Exercise 13: Slide In On Scroll

Written with assistance from [this excellent text guide by Nitish Dayal](https://github.com/nitishdayal/JavaScript30/tree/master/exercises/13%20-%20Slide%20in%20on%20Scroll)

Given an HTML document with multiple paragraphs and images, write the necessary
JavaScript code to slide the images into view when the user scrolls to a point
where it would be logical to display the image.

## Guide

If you inspect the images in browser you can see that much of the work is
already done: they are offset from their final positions using
`transform: translateX` and opacity is set to zero. All we need to do is apply
the `.active` class (already defined in css) when the images are in view, to
revert these rules.

**How might we do this?**

The idea here is to have a function we call every time the user scrolls, which
will check where every image is relative to the window and apply or remove the
`.active` class as required.

1. First thing we want to do is select all the images with the .slide-in class,
  and save them for later in a variable.
2. Now we want a "scroll" event listener on the entire window object. Name the
  callback function something relevant (remember what we are trying to do: check
  if images are in view and then slide them), we will create it next.
3. Let's write that function (above the eventlistener). Now, we have a bit of a
  problem here. If you try console logging the scroll events, you can see there
  are A Lot of them. Running our function 50 times a second could be bad for
  performance. Fortunately, the debounce function we are given helps us with this. We can pass it a function
  and a "wait" argument (in milliseconds) and it will enforce an interval of at
  least that much time in between function calls, blocking all the other times you
  might be triggering the event.
4. So make sure to wrap your function call in the event listener inside `debounce()`.
5. Inside the function let's iterate over all the images and for each one,
