---
layout: post
title: Using Timers in React Apps
date:  2020-10-29 11:51:00 -0500
categories: jekyll update
---
# Using Timers in React Apps

Do yourself a favor — let this never be a problem again

Have you ever wanted a message to only show up for a few quick seconds, rather than stick around and ruin the aesthetic of your app with its bright red font? Or only give a user a certain amount of time to complete some action? Luckily for you, vanilla JavaScript has you covered with the built-in setTimeout and setInterval functions. UN-luckily for you, implementing them in React can be a challenge initially. Your first go round, you’re almost certain to either break the timer or break your app via an infinite rendering loop. Before we get into React though, let’s briefly review how these two functions work.

They both take two arguments — a function to do and a length of time (in milliseconds).

The first, setTimeout, will perform the function **once **after* *the time you specified has passed.

![Note — use a callback function to prevent changeColor from running right away](https://cdn-images-1.medium.com/max/2000/1*J-gNQPy-y4v_kj9muJqX9w.png)*Note — use a callback function to prevent changeColor from running right away*

If you want to prevent the execution of the function, calling clearTimeout( ) and passing it the variable assigned to the setTimeout function will cut it off if the function hasn’t already been run.

![](https://cdn-images-1.medium.com/max/2000/1*xeP5joqCewa1FDsmObEhyg.png)

The second function, setInterval, performs the function after the time you specified has passed **until you tell it to stop.**

![](https://cdn-images-1.medium.com/max/2000/1*1Y9wuqlpaeUM-BC75GPN7w.png)

To stop the cycle, you must call clearInterval( ), passing in the variable you assigned to the setInterval function.

![Suggestion — run clearInterval once some condition is met](https://cdn-images-1.medium.com/max/2000/1*-XGHpt0dW31Sff49JclL6A.png)*Suggestion — run clearInterval once some condition is met*

In a normal vanilla JS program, you should be able to use these functions without much difficulty once you understand how they work….

But in React, things can get tricky rather quickly. Here’s a simple timer component in React:

![](https://cdn-images-1.medium.com/max/2000/1*9QCUe6iLyVftajkAKndkaA.png)

The counter is set to 10 when the component is mounted. Once it’s rendered and after one second, setTimeout runs the callback function that first checks if the counter is greater than zero and, if it is, decreases the counter by one using setState. Then it returns a div with the time remaining in the counter. This works as a timer because *setState causes the component to re-render*, which causes setTimeout to be run again, until the counter reaches zero.

This approach works, but there’s a glaring problem — if there is *any *functionality in the timer’s parent component that causes the timer to re-render…well let’s just say that problems quickly arise.

![](https://cdn-images-1.medium.com/max/2000/1*pv1J7a0jAk0Xar-SdinSJA.png)

In this snippet, if a user clicks the button on line 28, it will run the function on line 12. That function uses setState, which would cause Game’s render block to re-run, which in turn would cause the Timer’s render block to re-run. The result will be a timer that slows down when you click the inflate button, as the timer is reset every time you do so.

But that’s just the **beginning **of your timer woes. Let’s say you want something to actually happen when your counter hits zero — we’d need to add some action in the else block in our Timer component. We’ll pass it a simple function from the Game component called finishGame, which will setState to adjust how the child components are rendered.

![finishGame sets the state to adjust how it’s children are rendered](https://cdn-images-1.medium.com/max/2000/1*onk9hFpBTOwXX6QvCvSYDg.png)*finishGame sets the state to adjust how it’s children are rendered*

![x.props.finishGame(timer) will run when the counter is 0](https://cdn-images-1.medium.com/max/2000/1*Oe9Nd-iyMzkLysQxe3GPfw.png)*x.props.finishGame(timer) will run when the counter is 0*

Makes sense, right? What could possibly go wrong?

If you guessed “an infinite loop that makes your computer’s fan go nuts”, you’d be correct. The counter is stored in state, and it was never updated to not equal zero. Timer gets rendered, which runs finishGame because the counter is at zero, which re-renders it, which runs finishGame, which re-renders it…..until you call uncle and ctrl-C.

The major complication that React brings to running timers is that if they’re re-rendered improperly, they just don’t work. I believe that the simple and safest solution is to actually *separate *them from the other moving parts of your app. This might sound terribly obvious, but for people with less experience using React it’s not. In vanilla Javascript, it was just a function that you ran. In React, it should be treated as its own concern entirely if you want it to work %100 of the time.

![](https://cdn-images-1.medium.com/max/2000/1*BlRxiQZLpLUQgggPmaWqUA.png)

Here you can see that I’ve rendered the Timer and the Game components separately. On the Timer side…

![](https://cdn-images-1.medium.com/max/2000/1*fO-ngzOB1UqUriEtQQTZUw.png)

After finishing the game, I reset the counter. I’ve also added some simple logic to determine whether or not to even start the timer again.

There’s likely a better solution than this, and I’m sure I’ll learn about it as soon as I’ve published this. Nonetheless, the core takeaways remain:

* *Simplify your timer — have it run a counter, then send a message back when it hits zero*

* *Separate your timer as it’s own concern, inside it’s own component*

* *Render your timer as little as possible*

* *Have tight control over the situations where it** is **rendered*

Thanks so much for reading, I hope I was able to save you a bit of time and stress.

**If you have any questions or would just like to chat, v*isit my [LinkedIn](http://www.linkedin.com/in/benjamin-looper-a6a088158).***

**Check out my [Github](https://github.com/BenLooper) if you’d like to see my work.**
