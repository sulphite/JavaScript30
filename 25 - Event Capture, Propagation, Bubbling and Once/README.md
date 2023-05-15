# Exercise 25: Event Propagation

This isn't really a project at all, rather a more in depth explanation of the order in which events trigger.

Fire up the starting code and you will see 3 divs nested inside each other with classes "one", "two" and "three". Add click event listeners
to these, with a callback function that logs the value of the classlist to the console. What will happen if you click on the middle div?

## Explanation

Say you have a page with some nested divs, and click event listeners on them. When you click on a nested div (or any other element), you trigger a click event on that div, but also on **every parent element of that div**, all the way up to the html element! This is what we mean by “bubbling”.

How this actually works is that javascript goes from the top of the document down and “captures” all of these click events in the capturing phase (basically storing which elements you clicked on - body, div one, div two, …), then it starts the bubbling phase from the bottom up - it starts firing the actual click events, in the reverse order to how they were captured.

As an aside, this gives you the difference between an event’s `target` and `currentTarget` properties - target always refers to the original target of the event, whereas currentTarget refers to the element that is currently handling the event.

- [More info on event flow from W3C here](https://www.w3.org/TR/DOM-Level-3-Events/#event-flow)
- [Discussion of the history behind capturing and bubbling here](https://www.quirksmode.org/js/events_order.html#link4)

`addEventListener` can take an options object as the third argument where you can alter the default behaviours:

- `capture: true` means we will trigger events as they are captured, rather than when bubbling back up.
- `once: true` means that after the event has triggered once, the script will stop listening for any further events until a page reload.

Additionally you can add `event.stopPropagation()` in your callback function to stop events bubbling up at all.
