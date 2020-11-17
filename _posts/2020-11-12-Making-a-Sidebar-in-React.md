---
layout: post
title: Making a SideBar in React with Bootstrap
date:  2020-11-12 11:51:00 -0500
categories: jekyll update
---
# Making a SideBar in React with Bootstrap

How to make a basic collapsable side bar

Styling in React is made a lot easier with the ‘react-bootstrap’ library of components and styles that are easily available. Doing something like making a nav bar at the top of your app takes only a few lines of code…but for some truly unfortunate reason, moving that nav bar to the* side* of the app( a SIDEBAR?) isn’t quite as easy. In this brief code along, we’ll make a sidebar that looks like this:

![](https://cdn-images-1.medium.com/max/2000/1*q3TuH9bdyzcPVL4oB03D8A.gif)

*To keep things concise, I’m going to gloss over installing and importing [Bootstrap](https://react-bootstrap.github.io/getting-started/introduction) and all the [routing components](https://reactrouter.com/web/guides/quick-start) for React. I’m also going to assume that you’re already familiar with how to use both, so check out those links if something isn’t clear along the way (their documentation is amazing).*

We’ll start with a basic collapsable nav bar that covers the top of the page. It will navigate between the Home component and the About Component, both of which display some text. You can copy and paste the [boilerplate code](https://react-bootstrap.github.io/components/navbar/) from the React Bootstrap documentation, or code along with the image (recommended).

![](https://cdn-images-1.medium.com/max/2438/1*3erO6wQkWB-4BFqjs0E3eQ.png)

The are several important things to note here:

First is that the Navbar component is nested inside a column, a row, then container. The React Bootstrap documentation alludes to the idea that you can put the Navbar component in a container to center it, but makes no mention of how else you could use this. Here, we put it in a row and column in a container so that we can move it horizontally.

The second interesting bit is what gives us the collapsable functionality. Navbar.Toggle will, on click, hide or show whatever is in the Navbar.Collapse block. It’s enabled in the opening Navbar tag, where we set the prop ‘expand’ to ‘s’. This is a bit of responsive design that says “As long as the viewport is at least ‘small’ (576px), the Navbar is allowed to collapse”. On viewports below that *breakpoint,* the entire Navbar will display.

Add the following to your App.css file:

![](https://cdn-images-1.medium.com/max/2000/1*_xtZs370wXyjZiJxIB3LGQ.png)

And add the following class names to your Home and About components:

![](https://cdn-images-1.medium.com/max/2000/1*R9ZWaK7F20WuFeqF_3UowA.png)

The above code combined displays the following:

![](https://cdn-images-1.medium.com/max/5760/1*gkeGxOooIVKtKqSvYEz5-w.png)

You may notice that the Navbar stretches across the top of the page, but stops just short of meeting the edge. Those edges are a result of Bootstrap components’ default settings — they render with 15px of padding or margin (depending on if they’re nested inside something else) in order to keep components aligned relative to one another. For our purposes, we want to eliminate that padding and margin, condense the Navbar, and move it to the side of the screen.

Add the following code to App.js and App.css:

![](https://cdn-images-1.medium.com/max/2000/1*zJ7ebTx7ijb5zSAMBIQbNg.png)

![](https://cdn-images-1.medium.com/max/2000/1*DtmsHxf4-h0pvndUBeJa3w.png)

*We set the class names of the Container, Row, and Column to styles that we set in App.css.*

*We also give Column the prop ‘xs={2}. This says that the column will only use 2 units of the 12 in the row anytime the viewport is bigger than extra small — one unit for the Home link, and one for the toggle.*

*And here, we set the padding left and right to zero for the container and column. We also set the background color to match.*

*We don’t need to change the color for the row, since it’s rendered under the column.*

The above code will display the following:

![](https://cdn-images-1.medium.com/max/5760/1*V6GIdmwSTAzbkaSeFEREzA.png)

Much better. Now let’s style the links so they don’t look like something from the 90’s — use [this awesome website](https://css-tricks.com/examples/ButtonMaker/#) to make a custom button and apply the CSS to your links through the ‘home-button’ and ‘about-button’ classes in App.css. You should end up with something like this:

![](https://cdn-images-1.medium.com/max/5760/1*nGtnmR-cvGpGgY2xGFiPLA.png)

Thanks so much for reading. While this problem isn’t the best implementation, it’s certainly a start and should fit your basic needs. If you have any input on how to improve it, feel free to leave a comment.

**If you have any questions or would just like to chat, v*isit my [LinkedIn](http://www.linkedin.com/in/benjamin-looper-a6a088158).***

**Check out my [Github](https://github.com/BenLooper) if you’d like to see more of my work.**
