---
layout: post
title: Building a website in Haskell coming from Node.js
---

*This is an adapted transcript of a talk I gave at the [Functional Programming Montréal Meetup](http://www.meetup.com/Functional-Programming-Montreal/). In it, I share my experience learning Haskell to build a small website.*

A couple of months ago, I set myself the challenge to try and build a website in Haskell as a small side-project. It was an interesting journey, especially coming from a dynamic language background. I'll give examples from JavaScript and Node.js because that's what I work with the most currently, but really any dynamic language would apply (ex: Python, Ruby).

If you are a Haskell beginner or have been wondering about trying it out, hopefully by sharing my experience I can convince you to do so, and show you that it's not as scary as it seems (at least not always!). For more experienced Haskellers, maybe this can show you what kind of challenges beginners struggle with, and some of the things we can do as a community to make Haskell more approachable.

## Context

Let me start with a bit of background. I've been curious about Functional Programming concepts for a while now, and try to apply them when I write JavaScript for work (the language is versatile enough to support many different styles). I prefer functions over classes, keeping data immutable, etc. Outside of work, I've played around with Clojure, Elixir/Erlang, and more recently Haskell.

Another thing to keep in mind is that I explored Haskell from the point of view of a **web developer** that has mostly worked with **startups**. In that context, a web developer needs to:

- Have the necessary tools to **build web applications.** It's actually pretty simple: you need to fetch data by making **API** or **database** calls, transform that data and put it in some **HTML**, and respond to **HTTP** requests.
- Work on a **team**. You actually end up spending most of the time reading and modifying **other people's code**, versus writing new code.
- Constantly **adapt to change**. A startup is a fast-paced environment where being able to react quickly is crucial.

Of course, I wouldn't say Haskell solves every problem a startup web developer will face. But, notably thanks to its powerful type system, it does hold an interesting promise against these stakes, especially the last two.

So, how did my experience of building something in Haskell go?

- Was it **challenging**? I won't lie to you: yes, it was.
- Was it **possible**? Well, I built something and it works: so yes, it was.
- Would I **do it again**? Yes!

## The app

What is it that I built? Being a side-project, I wanted to keep it pretty simple. But hopefully it wasn't trivial, allowing me to explore Haskell solutions to problems related to web development.

I used the [Marvel Comics developer API](http://developer.marvel.com/) to have some data to work with. It's really convenient: it's free, you just sign up for a token and have access to data on characters and comics from the world of Marvel. I'd venture to say that a good portion of web sites consist of grabbing data from an HTTP API or a database (at least the ones I've worked on), so it will be interesting to see how this is done in Haskell.

A demo version of the project is hosted here: [example-marvel-haskell.herokuapp.com](http://example-marvel-haskell.herokuapp.com/).

Like I said, it is pretty simple. You have a landing page with feature Marvel characters and comics, which takes you to your traditional list view to browse the data. You'll notice that this means I had to implement pagination. The navbar at the top also shows you where you are on the site by highlighting the current section. Clicking on a character (or comic) takes you to a detail view. And since the data is relational, you can jump to the comics the character appeared in (and vice-versa).

[TODO: screenshots]

One thing to note is that this is something I had already built in JavaScript (to explore some libraries). Which means I was porting an existing app to Haskell, which is an approach I definitely recommend when learning a new language. Since you've already solved the "business problem", you know exactly what you want and you can focus on the new language or tech you are trying to learn.

Both versions of the app are of course open-source and available:

- JavaScript: [github.com/nicolashery/example-marvel-app](https://github.com/nicolashery/example-marvel-app)
- Haskell: [github.com/nicolashery/example-marvel-haskell](https://github.com/nicolashery/example-marvel-haskell)

## Jumping in

How does one go about **learning Haskell**? Well, everyone has a preferred way of learning but if someone asks me to point them in the right direction, here is what I would answer.

For a more hands-on approach to get excited by actually doing things, [Sean Hess](http://twitter.com/seanhess/) has a nice [Practical Haskell](http://seanhess.github.io/2015/08/04/practical-haskell-getting-started.html) "getting started" series. It will take you from setting up your local environment with [Stack](www.haskellstack.org) (setting up Haskell projects wasn't always that easy, Stack made it so much better!), to actually building a small JSON API, with no Haskell knowledge required!

Afterwards, to continue with a more studious approach, the [CIS 194: Introduction to Haskell](http://www.seas.upenn.edu/~cis194/spring13/) course was [recommended](https://github.com/bitemyapp/learnhaskell). I went through the first half and it is indeed of good quality. You read through the lectures and after each chapter you have a set of exercises to help things sink in (and it is easy to Google for the solutions if you get stuck).

In terms of books, the [Haskell Programming](http://haskellbook.com/) looks very well done. At the time of writing it is just being finished (although you can get an early access version). There is also [Learn You a Haskell for Great Good](http://learnyouahaskell.com/) which is free to read online.

When building something in a new language, the question "how do I do X?" often comes up. Good think there is a [curated set of libraries](www.haskelliseasy.com) available to get you started.

Finally, Haskell is a powerful language and there are often multiple ways to do something. It is also an old language, which means it carries some legacy baggage which you want to avoid. Thankfully, I found the [What I Wish I Knew When Learning Haskell](http://dev.stephendiehl.com/hask/) guide by [Stephen Diehl](https://twitter.com/smdiehl) which is a goldmine of best practices to help you find your way through the jungle.

Since my project was to build a web site, it came the time to pick a **web framework** to use. There are definitely more than 3 web frameworks in Haskell, but these are the ones that stood out for me.

[Yesod](http://www.yesodweb.com/) is very popular, and maybe one of the oldest ones so it is quite battle-tested. It makes me think of Rails in Ruby (or Django in Python) with a lot of things baked-in (notably best-practices, security, etc.). It is also very well documented, and it has a whole [book](http://www.yesodweb.com/book) available online. For my first project, it felt a little too much (I was afraid I'd be learning Yesod more than learning Haskell), so I didn't select it. But I would definitely want to try it out for the next one!

[Servant](http://haskell-servant.readthedocs.org/) is fairly new, but it is also the most intriguing and different. It really seams the most "Haskell specific" (i.e. there isn't a similar framework in another language), and it really leverages the type-system. It is very promising, and I'm eager to try it, but I thought it might be too different for a first project.

[Scotty](https://github.com/scotty-web/scotty/) is lightweight and familiar. It feels like Express in Node.js, Sinatra in Ruby, or Flask in Python. One drawback is it doesn't have a lot of docs, although you can find some examples in the repository. Since it looked like a framework that would be easy to start with and get out of my way, this is the one I ended up picking for my first project.
