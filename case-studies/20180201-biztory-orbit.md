---
layout: post
title: "New Homepage: MVP Design and Development"
meta: "Redesigning and redeveloping my own website to serve a new purpose"
permalink: /case-studies/koendecouck/
next-case-study-title: "000"
next-case-study-url: /case-studies/000/
hide-hire-me-link: true
---

My own website has a long history of ongoing webdevelopment, going back more than 15 years ever since the first simple HTML version. I've chipped at it on and off over the years, incorporating better technologies as they became available. The current version is ofcourse what you see before you. It's form and content has matured alongside my own professional development. It offers a unique longitudinal view in my processes and workflow, unbothered by external restraints. 

## History

My first self-made homepage dates back to my teenage years, back in the time of early HTML. It was an experiment in interactive web design.

Here are some of the earlier designs:
2003.jpg
2009.jpg
2011.jpg
2014.jpg
2017.jpg
2018.jpg

## The project

The last iteration of this site had been running for at least 4 years (2013-2017). It was Wordpress-based, with a heavily customized proprietary theme, and served as a professional portfolio.
The design had received a lot of praise, both from past employers and clients. As non-developers, they liked the high amount of visual imagery that illustrated my work. Never mind that all that content made the site bloated to servers, and working with Wordpress presented constant worries over versioning, security and limitations. When the site actually went down under an intense Chinese DDoS attack, I decided it was time for a new approach.

<figure>
  <img src="/img/content/case-studies/koendecouck/old.png" alt="">
  <figcaption>Screenshot of this site in 2017 <a href="/img/content/case-studies/koendecouck/old-full.png">View full size/quality (179KB).</a></figcaption>
</figure>

Redesigning a site is never a quick task, particularly when it's your own. However I had a very clear idea of what 'good design' looked like, and had four years of client feedback on the previous iteration. Based on that vision I decided to develop a new, solid MVP after work. The requirements for that MVP were simple:

* Fast, clever design that still performs nicely on low-band data lines.
* Minimalist philosophy: only relevant, structured, high quality content.
* Universality: a clear format for web posts that
* Introduce a [Case Studies](/case-studies/) section to feature client work
  (given that the majority of my work is consultancy based, case studies make
  more sense than a portfolio does).
 * Scale back the use of images, especially high resolution images (but without compromising content accessibility to non-developers).
 * Put less (but not too little) focus on blog posts.
 * Resistant to trends: have as few dependencies as possible to external entities.


## The process

As I’m not too great a designer, I didn’t want to spend ages frustrating myself
making mockups in Sketch. I scribbled a rough wireframe onto a folded up piece
of printer paper, and set my mind toward thinking about how I might want
something to look and, more importantly, function. I installed a brand new
instance of [Jekyll](http://jekyllrb.com/), ported over my old content, and got
hacking away straight into code.

I set up [a Trello board](https://trello.com/b/9A5xvct0/koendecouckgithubio) to try
and keep things focussed, but ultimately I just bounced around ideas and
features as soon as I thought of them.

Having the content already there was a real boon, and meant that I didn’t have
that much work to do restructuring any of the IA. I’d spent weeks on end
constantly tweaking and refining the copy used throughout the site, so it was
something I didn’t really need to worry about during the redesign.

<figure>
  <img src="/img/content/case-studies/css-wizardry/new.jpg" alt="">
  <figcaption>Screenshot of the current CSS Wizardry home page. <a href="/img/content/case-studies/css-wizardry/new-full.png">View full size/quality (550KB).</a></figcaption>
</figure>

## The tech

Naturally, CSS Wizardry is built on top of [inuitcss](http://www.inuitcss.com/),
my open-source, Sass-based, OOCSS framework. inuitcss is currently (at the time
of writing) in a state of flux: its GitHub repos are a collection of pre-alpha
modules that, although stable, are still, as yet, unofficial. Despite that, I
know that I have complete faith in the new version of inuitcss—the [NHSx
site](/case-studies/nhs-nhsx-elearning-platform/) was built on the pre-alpha
modules with great success.

Using inuitcss (installed via its [Bower](http://bower.io/) packages) meant that
I had the UI’s framework and architecture set up in less than half-an-hour. This
helped me work very quickly.

As well as using inuitcss, I built the CSS onto [ITCSS](http://itcss.io/), an
as-yet unpublished, proprietary CSS architecture of mine which lends itself well
to scalability and manageable code on long-running products, which CSS Wizardry
certainly aims to be.

As mentioned, the site is built on Jekyll, which can be hosted on [GitHub
Pages](https://pages.github.com/), and its source code is hosted [on
GitHub](https://github.com/koendecouck/koendecouck.github.com).

The site is responsive—mobile-first flavour—and testing it (as well as demoing
it to friends and peers) was made incredibly easy by using
[Finch](https://meetfinch.com/), a new product which allows developers to
securely expose their local dev sites to any internet-connected device. This
meant I could check CSS Wizardry on mobiles, tablets, and larger screens without
having to host it on a staging server. Being able to save time like this
definitely helped me hit my self-imposed deadline.

Finally, due to no external requirements or constraints, this iteration of CSS
Wizardry practices everything I preach. Further, it will continue to do so, as
it is built on an architecture designed to accommodate change.

## Summary

I gave myself a very tight deadline to get together an MVP for a better
positioned, more business focussed CSS Wizardry. Working with open-source tools,
and in a very pragmatic and agile manner, I was able to get the MVP live over
the course of a long weekend.

I am now in a position where I can move CSS Wizardry forward as a product, and,
after a very intense initial sprint, spend fragments of time improving and
honing the site in coming weeks. It was very important to me that I get
something ‘good’ live in a few days, rather than spending months trying to
strive for ‘perfect’.

The current version is Jekyll-based and completely open source, very different from the last iteration that used a heavily customized, proprietary Wordpress theme. The design philosophy behind it is also quite different: it is actually LESS visually loaded than last iteration was.

---

{% include promo-next.html %}
