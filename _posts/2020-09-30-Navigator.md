---
layout: post
title: Navigator
date:  2020-09-30 11:51:00 -0500
categories: jekyll update
---

# Navigator

- A simple way to build complex narratives.

### *Part I — Modeling the concept*

*Thanks so much for reading. I’ll be updating this project regularly, follow this [GitHub link](https://github.com/BenLooper/Navigator) if you’d like to have a look or make any contributions.*

Like many people, when I first started programming I wanted to make a text game. This is no easy task for a beginner — not only must they write a program to play a story, but they must also *write *said story*. *I’ve read and written my entire life, but bringing it together with programming proved challenging to say the least. Ultimately I never finished it, and it’s something that’s bothered me ever since.

I’ve come a long way as a programmer and a developer since then, and have decided to finally come back and finish what I started. I intend for this to be a guide not only in making my tool, but also more generally in how to write a choice driven story (also called a Pick a Path story).

**What is a Pick a Path adventure?**

If you’ve ever read any of the old Goosebumps books that prompted you to “turn to page 56 to see something happen!”, then you’re already on the level. A pick a path adventure (or PaP), was a writing fad that popped up in the late 90’s. If you’ve ever played *any* game in which the choices you make affect the outcome of the story, you’ve played/read a PaP adventure.

**Why do we need a tool to write one?**

You don’t! Or at least, R.L. Stine probably didn’t use one. But I’m not as good at writing stories as him (or many other people for that matter), so I’m making a tool to help me. Also, take a look at this flowchart:

![2 choices turns into 16 endings before long…](https://cdn-images-1.medium.com/max/4780/1*9vBLf5qQYk26bpv4YzEtng.png)*2 choices turns into 16 endings before long…*

Say you only give the user two choices to work with. After doing this just four times, you now have up to sixteen endings to write (some choice strings may end earlier). It’s called exponential growth, and it’s scary in most contexts (see viruses). For reference, most Goosebumps novels gave the reader four choices, and modern PaP books can have many, many more.

That is an insane amount of writing, but that’s not even the hardest part. You also have to keep your stories straight and organize them into a non-contradictory, cohesive experience.

How do you even physically do that? I tried it with a variety of platforms, and my frustration ultimately led me to make my own tool to do it.

![My roommate and I tried to write one manually…](https://cdn-images-1.medium.com/max/2000/1*5751ToxLEKqaMbnIOZSE4A.jpeg)*My roommate and I tried to write one manually…*

**What is Navigator?**

Navigator is my solution to the conundrum seen above. Don’t let the fancy name fool you — that took me two seconds to think of. The domain however took quite a bit more thought. It breaks a story into three easy models that link into one another sequentially:

Prompt

    - belongs_to :project
    - belongs_to :text
    - has_many :choices

Choice

    - belongs_to :project
    - belongs_to :prompt
    - has_one :text

Text

    - belongs_to: project 
    - belongs_to :choice
    - has_one :prompt

In essence, all Navigator will do is ask the user to fill out each of these models one after the other, then aggregate them into a Project model. The flow of the program will look like this:

Navigator will prompt you to start with some background text.

    ex: You're riding the subway home on a stormy day. You work the night shift, so you're alone most of the way. 
    When you get off, the old public phone on the wall begins to ring. You hesitate for a moment, then pick it up. 
    A raspy voice tells you that you have 2 hours to live! :(

When you’re done, it will then ask you for a prompt. This is written manually, to increase flexibility when writing.

    ex: What do you do?

Next, Navigator will ask you to fill out the choices for this prompt. You can make as many as you want (be warned: more choices = more writing)

    ex: Choice 1: Hang up the phone and walk away.
        
        Choice 2: Demand who's calling.

It will redirect you to the overview of your project so far, where you can choose what threads to fill out next.

Finally, when you want a thread to end, simply check the “ending” box in the text input. This will close the thread from having another prompt.

That’s generally what it will look like. The next step will be to make the skeleton of the app and try to achieve the core functionality shown above. Keep an eye on the GitHub repo for changes before the next post comes.

A huge help to me in learning more about PaP stories was this post from AWORDLOVER in HobbyLark. If you’re interested in learning the specifics of writing a PaP story, read their article here:
[**How to Write a Pick-a-Path Story**
*My articles are written from the perspective of being a successful author on HubPages, blogger, website owner and…*hobbylark.com](https://hobbylark.com/writing/How-To-Write-A-Pick-A-Path-Story)

*Find me on [LinkedIn](http://www.linkedin.com/in/benjamin-looper-a6a088158) and [Github](https://github.com/benlooper)*
