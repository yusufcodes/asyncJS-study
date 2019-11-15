# Asynchronous JavaScript: Promises, Async/Await and AJAX
This repo contains the code and notes made as I followed along with Section 8: Asynchronous JavaScript: Promises, Async/Await and AJAX of [The Complete JavaScript Course](https://www.udemy.com/course/the-complete-javascript-course) on Udemy.


## Understanding Asynchronous JavaScript: The Event Loop

Synchronous JavaScript: Code is executed one by one, line by line, as it appears in the code. 

Asynchronous JavaScript: This type of JavaScript can help you avoid waiting for a single function to perform some tasks and finish, before performing some other actions in the program. The async function can be thought of as a **background process**, running whilst the rest of your code is executed.

The JavaScript Engine is made up of a number of parts:

1. Execution Stack
2. Message Queue
3. Event Loop
4. Web APIs

These elements work in conjunction with one another to allow for Asynchronous JavaScript to occur.

Suppose we have a simple synchronous function, regularFunction, and then a special asynchronous function, asyncFunction. 


```javascript
    const asyncFunction = () => {
        // Code
    }

    const regularFunction = () => {
        // Code
    }

    regularFunction();
```
Right now, both functions look identical except for the name of them. So let's add some code to make them *do stuff*. (That's always useful).

```javascript
    const asyncFunction = () => {
        // Code
    }

    const regularFunction = () => {
        console.log('Hello - I\'m a regular fuction!');
    }

    regularFunction();
```
All I've done here is add a console log statement to our regularFunction, which will display 'Hello - I'm a regular fuction!' in the console. This regularFunction is currently being called. However, nothing is happening with our asyncFunction.

We want to make this function into an **asynchronous function**. A handy Web API we can use is the **setTimeout method**. Web APIs are separate to the JavaScript Engine itself, but are made available as we run a JavaScript environment.

#### What is setTimeout, and how does it link to what we're learning about here?

The setTimeout method allows for you to specify a certain amount of time to wait before eventually executing a method. This is a good way to **emulate** the performance of an Asynchronous function.

*Example:* If you built a website which had multiple things to do to load the page, imagine having to wait for every single thing to load, one at a time, until the page is fully loaded? *That would be horrible*.

Instead, in the **waiting period** for each thing that we're trying to load, we can go off and do some **other things** whilst this one thing loads. We can them come back to the loaded thing and do what we want with it later.

Using setTimeout, I'd like to demonstrate how we can delay the execution of one method, whilst doing some other 'things' during this waiting period. Let's add the setTimeout method to our code.

```javascript
    const asyncFunction = () => {
        setTimeout( () => {
                console.log('...Hello, I\'m an async function, late to the party 😳');
            }, 3000);
    }

    const regularFunction = () => {
        console.log('Hello - I\'m a regular fuction!');
    }

    regularFunction();
```

In this example, I've passed in two parameters to the setTimeout method:

1. Function: The function that I want to run after the specified time.
   In my example, we print out the following statement:
   ...Hello, I'm an async function, late to the party 😳 (the 'late' (lame) joke will make sense later)
2. Time: The time in milliseconds that the timer should wait, before executing the function we defined.
   In my example, we wait 3000 milliseconds, which is 3 seconds, before executing the defined function.

Now that our Asynchronous Function is all set up, let's actually call this method. We'll do this in our regularFunction. We'll also add one more console log statement after we call the asynchronous function - this will make it easy to see the 'asynchronous' method in action.

```javascript
    const asyncFunction = () => {
        setTimeout( () => {
                console.log('...Hello, I\'m an async function, late to the party 😳');
            }, 3000);
    }

    const regularFunction = () => {
        console.log('Hello - I\'m a regular fuction!');
        asyncFunction();
        console.log('The end');
    }

    regularFunction();
```

When we run the above code, this will be the console output that we will retrieve:
![image](https://imgur.com/ljwgdj6.png "Display of the console when executing the described code");

Let's break down exactly what's happened here:

- We make our **first function call, regularFunction**, and add it to the **Execution Stack** (a 'stack' of data which our JS program uses to keep track of any function calls).
  - Within this function, we perform a console.log method - this also gets added to the Execution Stack and popped (removed) off the stack as it is ran instantly - (as log() is a method belonging to the console property).
- We then call the **asyncFunction** from the regularFunction. This will get added to the Execution Stack.
  - Within this function, we make a call to the **setTimeout** method. Similarly as above, this method call also gets added to the Execution Stack.
  - This method will setup our timer, with the specified delay time (3 seconds for us), and the function we want to run.
- Earlier I mentioned that setTimeout is a Web API which is external to the JavaScript Engine: we can leverage this external environment to **place our timer in, along with the callback function.**
  - In our example, the timer and associated function we defined to print a message is **sent to the Web API environment**.
  - Here, it waits for the period of time we define, before being moved to the **Message Queue** (a list of functions which need to be processed).
- While this timer is running in the Web API environment, we can now continue with the rest of our code:
  - The **setTimeout** method is **popped off the stack**, as well as the **asyncFunction**, as they've technically **finished executing** now.
  - We're back to our **regularFunction**, where we have **one final statement** to print: 'The end'
  - From the output shown above, we can see that 'The end' appears **before** the message from asyncFunction. This is because the timer and associated function waited three seconds in the Web API environment, before it was able to finally execute (once the function is moved to the Message Queue). In this time, we finished the rest of our regularFunction, which explains why 'The end' appeared before the message we defined in the callback function.

All of the above actions are kept in sync with **The Event Loop**: a part of the JavaScript engine which is always monitoring the Execution Stack and Message Queue, pushing any functions from the Message Queue ➡️ Execution Stack, much like our delayed function we created in the setTimeout method.

And that just about covers the concept of Asynchronous JavaScript (at a basic level)! 

## Asynchronous JavaScript with Callbacks

## TODO: Fill in sections about Callbacks, Promises and Async / Await. Currently have comments in my code (asynchronous.html) which I want to transfer here in a more readable format.

## AJAX and APIs

AJAX = Asynchronous JavaScript and XML

API = Application Programming Interface
Some kind of software to be used by other pieces of software, allowing for them to talk to each other.

## Making AJAX calls with Fetch and Promises
