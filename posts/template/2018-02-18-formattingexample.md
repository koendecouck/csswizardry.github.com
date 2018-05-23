---
layout: post
title: "MD Formatting Example"
date: 2018-02-18 12:19:58
categories: Web Development
meta: "Reference for writing MD blogs"
---

This blog article uses the 'md' format, which is a very convenient format to use when you're writing blog posts that look like code. It should make visual formatting a lot easier to manage. None the less, there is always this page with a few formatting examples to remind myself and other people. Lots of really nifty things are possible with MD. We'll start with the basics: this paragraph consists mainly out of normal text, but you can also include hyperlinks like this: [hyperlink anchor](https://koendecouck.github.io).

New lines are obeyed in the final formatting, which makes it easier to edit. 

You can emphasize terms and put them in italics by using underscores _Like this_. Don't mistake these for <q>an expression in parantheses, which DOES NOT appear as italic</q>. Colored words can be made with `backtics` (conveniently Sublime marks these color words in a different color as well, so you can more easily tell). Beware: Use the power of color sparingly, for example only to denote branch names!
**Bold text is displayed with double asterisks, just like in ordered lists.**

Unordered lists of bullet points are made using asterisk characters:

* itemA
* itemB
* itemC

It is also very easy to make numbered as you can see here:

1. **Bold item 1**. Some text that talks about item1. You can even place footnotes on certain words, like this[^1]
2. **Refactoring can be scary.** All the different text formatting can be used, including _italics_ or <q>italics</q>. Do not confuse these with backtick `color words`. Do not use bold text, since it interferes with readibility. The item title is already bold after all.



Images can be inserted using 'figure' tags:

<figure>
<img src="/apple-touch-icon.png" alt="" />
</figure>

You can also separate sub-content of posts (like anekdotes, mini-stories) with a horizontal line. Use three dashes, which will be turned in a continuous horizonal line across the page after formatting.

- - -

Terminal command formatting is made like this:

    $ git reset --hard origin/master

Which displays the text in something resembling the terminal window. The dollar sign is displayed along with the following code.

Code blocks are fenced by backticks

```javascript
var s = "JavaScript syntax highlighting";
alert(s);
```

- - -

And then there's this:

> It involves quite some risk because we have quite a lot of users (200,000),
> **but it’s worth taking the risk to achieve big goals**.
>
> We are extremely excited about this opportunity to really make something
> stellar, **without having to deal with a lot of legacy**.

Or if you'd rather have a block quote:

<blockquote class="pull-quote  pull-quote--context-alt">
  <p>This is a block quote</p>
  <b class="pull-quote__source">
    <a href="https://twitter.com/koendecouck">Some guy</a>
  </b>
</blockquote>



## Section Title

In general you should use all these special features sparingly. Normal white paragraph text like this should dominate your article. You can however use an occational figure or list to break up content, and keep your audience's attention.

1. **It makes content visually more attractive.**
   Avoid writing walls of text. For ordered lists you can newline your list item's text like you see here (or not), in the final format it will appear next to the bold item title regardless.
2. **It makes easier to cognitively process.**
   The human brain can only understand things in sets of 3, 5 and 7.
3. **It allows diagonal reading.** 
   This is a good thing since most people don't have time to sit down and read a whole article of multiple pages.

Again, most of your article's content should be plane text, however don't forget to [insert hyperlinks where appropriate](https://koendecouck.github.io) to allow visitors to quickly navigate to supporting content.

Finally if you used footnotes (which I'd generally only recommend to cite academic papers, not for added thoughts) then please end the page with a horizontal line. This will keep the source material nicely separated from the main content on the page. It's a lot cleaner.

- - -

[^1]: This is an example of footnote text. It appears in small font at the bottom of the page.
