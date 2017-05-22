3 JavaScript questions to watch out for during coding interviews

JavaScript is the official language of all modern web browsers. As such, JavaScript questions come up in all sorts of developer interviews.
This article isn’t about the newest JavaScript libraries, common development practices, or any of the new ES6 functions. Rather, it’s about 3 things that usually come up in interviews when discussing JavaScript. I myself have been asked these questions, and my friends have told me they’ve been asked them, too.
Of course these aren’t the only 3 things you should study before a JavaScript interview — there are a multitude of ways you can better prepare for an upcoming interview — but below are 3 questions an interviewer may ask to judge how well you know and understand the JavaScript language and the DOM.
So let’s get started! Note that we’re going to use vanilla JavaScript in the examples below, since your interviewer will usually want to see how well you understand JavaScript and the DOM without the help of libraries like jQuery.
Question #1: Event delegation
When building an application, sometimes you’ll need to attach event listeners to buttons, text, or images on the page in order to perform some action when the user interacts with the element.
If we take a simple todo list as an example, the interviewer may tell you that they want an action to occur when a user clicks one of the list items. And they want you to implement this functionality in JavaScript assuming the following HTML code:

You may want to do something like the following to attach event listeners to the elements:

While this does technically work, the problem is that you’re attaching an event listener to every single item individually. This is fine for 4 elements, but what if someone adds 10,000 items (they may have a lot of things to do) to their todo list? Then your function will create 10,000 separate event listeners and attach each of them to the DOM. This isn’t very efficient.
In an interview it would be best to first ask the interviewer what the maximum number of elements the user can enter is. If it can never be more than 10, for example, then the above code would work fine. But if there’s no limit to the number of items the user can enter, then you’d want to use a more efficient solution.
If your application could end up with hundreds of event listeners, the more efficient solution would be to actually attach one event listener to the whole container, and then be able to access each item when it’s actually clicked. This is called event delegation, and it’s much more efficient than attaching separate event handlers.
Here’s the code for event delegation:

Question #2: Using a closure within a loop
Closures are sometimes brought up in an interview so that the interviewer can gauge how familiar you are with the language, and whether you know when to implement a closure.
A closure is basically when an inner function has access to variables outside of its scope. Closures can be used for things like implementing privacy and creating function factories. A common interview question regarding the use of closures is something like this:
Write a function that will loop through a list of integers and print the index of each element after a 3 second delay.
A common (incorrect) implementation I’ve seen for this problem looks something like this:

If you run this you’ll see that you actually get the 4 printed out every time instead of the expected 0, 1, 2, 3 after a 3 second delay.
To correctly identify why this is happening it would be useful to have an understanding of why this happens in JavaScript, which is exactly what the interviewer is trying to test.
The reason for this is because the setTimeout function creates a function (the closure) that has access to its outer scope, which is the loop that contains the index i. After 3 seconds go by, the function is executed and it prints out the value of i, which at the end of the loop is at 4 because it cycles through 0, 1, 2, 3, 4 and the loop finally stops at 4.
There are actually a few ways of correctly writing the function for this problem. Here are two of them:


Question #3: Debouncing
There are some browser events that can fire many times within a short timespan very quickly, such as resizing a window or scrolling down a page. If you attach an event listener to the window scroll event for example, and the user continuously scrolls down the page very quickly, your event may fire thousands of times within the span of 3 seconds. This can cause some serious performance issues.
If you’re discussing building an application in an interview, and events like scrolling, window resizing, or key pressing come up, make sure to mention debouncing and/or throttling as a way to improve page speed and performance. A real example taken from this guest post on css-tricks:
In 2011, an issue popped up on the Twitter website: when you were scrolling down your Twitter feed, it became slow and unresponsive. John Resig published a blog post about the problem where it was explained how bad of an idea it is to directly attach expensive functions to the scroll event.
Debouncing is one way to solve this issue by limiting the time that needs to pass by until a function is called again. A correct implementation of debouncing would therefore group several function calls into one and execute it only once after some time has elapsed. Here’s an implementation in plain JavaScript that makes use of topics such as scope, closures, this, and timing events:

This function — when wrapped around an event — will execute only after a certain amount of time has elapsed.
You would use this function like so:

Throttling is another technique that’s is similar to debouncing, except that instead of waiting for some time to pass by before calling a function, throttling just spreads the function calls across a longer time interval. So if an event occurs 10 times within 100 milliseconds, throttling could spread out each of the function calls to be executed once every 2 seconds instead of all firing within 100 milliseconds.
For more information on debouncing and throttling, the following articles and tutorials may be helpful:
Throttling and Debouncing in JavaScript
The Difference Between Throttling and Debouncing
Examples of Throttling and Debouncing







##Responses:

**Bill:**
>Thanks for these good examples of JS interview questions. I like how you emphasized understanding JS fundamentals.
>Regarding Question #2 (looping), just using let and const would make the code more readable and safe.
>Regarding Question #3 (debouncing), while it’s a useful exercise to make a debouncer and it’s only a few lines of code, I’d recommend just using a micro-library for it, to reduce testing surface area and save time.


**Jessica:**
>Hey :-) thanks for sharing!

>I actually wasn’t asked one of the questions in my last interview, but instead we went on to discuss prototypes which was also fun!
>Btw. the delayed print of i should also work with .bind(). Haven’t tested it, but if i’m not mistaken setTimeout(console.log.bind(undefined, ‘Print i: ’ + i), 3000);
>should also do the trick.

**John:**
>Such a good read.



**Dylan:**
>Doesn’t expecting the unexpected make the unexpected expected?



**Soros:**
>Man is the only living being who cuts trees, makes paper, and writes “SAVE TREES” on it.


**Bill:**
>Whoever said that nothing was impossible obviously never tried slamming a revolving door.



**Shon:**
>For Sale: Parachute. Only used once, never opened, small stain.
