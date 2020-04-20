# Part 0
Clone branch part0 for the initial set up.


# Part 1

## Mocking Up a Tagline
1. Pretend you have this mockup from a designer
![tagline mockup](./images/tagline.png)
1. Mock it up in the browser.
```html
<h1>Get your own flying car today! <a href="">Read More &raquo;</a></h1>
```

```css
body {
    background: #DCDBD9;
    color: #2d2d2d;
    font: normal 100% Cambria, Georgia, serif;
}

h1 {
    font-size: 24px;
    font-style: italic;
}

h1 a {
    color: #747477;
    font: bold 11px Calibri, Optima, Arial, sans-serif;
    letter-spacing: 0.15em; /* 25px / 16px */
    text-transform: uppercase;
    text-decoration: none;
}
```
1. Pixels are fine... but they aren't flexible, so let's change this to something a little more
proportional...like `em`. Remember, the em unit is relative to the font-size of the element (ex. 2em is 2 times the font size of the current font).
1. How to get these from pixels to ems? `target / context = result` where target is the pixel font size in our comp, context is the font-size of the current containing element, and this will give us our result, which is the value we set using our em unit.
1. Assuming that setting the 100% font-size on our body elements makes everything 16px... we can just plug our values into our formula: 24 / 16 = 1.5. 24px is one and a half times bigger than 16px, so our new font-size is 1.5em.

```css
h1 {
    font-size: 1.5em;
    font-style: italic;
}
```
1. The font size should appear the same, but now it's relative and scaleable!
1. Time to move onto our anchor tag! Use the same formula. 11 / 24 = 0.4583333333
1. That's an awful number... but don't round it! Why would you? It's proportionally accurate. It's more proportional than if you had rounded it off to .46em. So let's add it to our CSS.
1. Why is this cool? Change font-size on body from 100% to 150%...everything scales!

## Okay...where's the grid though
- Check out branch `step2-completed-basic-styling`.
- Read `step4-fluid-grid-completed` readme on github.

We've gotten this far and still haven't touched on the subject of grids, which is supposed to be what this section is about. BUT doing this with something simple like fonts will allow us to understand it and apply it to layouts and grids.

Let's pretend the graphic designer at your company has sent you a mockup that you are tasked with coding. For time's sake, we'll pretend that the basic colors, typography, and other details not related to layout are already completed.

The mockup:
![the mockup of the new blog page](./images/blogpost.png)

Show the PhotoShop version with the grids.

1. Now, we need to get this information into some proper columns.
1. We can get some information about the layout from looking at the mockup with a grid enabled.
1. The grid is 12 columns across. Each column is 69pixels across, separated by 12px gutters. This adds up to 960px. 
1. The blog itself is 900px, and centered horizontally in the grid.
1. The left-hand column is 566px wide, and the aside here is 331 pixels across.
1. So, let's get those set up!

```css
* { box-sizing: border-box; }

.page {
    margin: 36px auto;
    width: 960px;
}

.blog {
    overflow: auto;
    background: white;
    box-shadow: 0 0 5px 5px rgba(0,0,0,.1);
    margin: 0 auto 24px;
    width: 900px;
}

header {
    background: var(--PrimaryColor);
    padding: 24px;
}

main {
    padding: 24px 0;
    float: left;
    width: 566px;
    padding: 24px;
}

aside {
    padding: 24px 0;
    float: right;
    width: 331px;
}

```

1. Resize screen and demo.
1. Now, let's get them into pixels!!!
1. Now we want to rid the blog of that 900px value and set it to something proportional to the page. We can use our target/context formula.
1. We know our target: it's 900px. We want to change that something in relative terms - a % of it's containing element, which is the page. The container's target is 960px.
1. 900px / 960px = .9375 - change this into a %

```css
.page {
    width: 80%;
}

.blog {
    width: 93.75%; /* 900 / 960 */
    margin: 0 auto;
}
```
1. Now - content columns. Left is 566px and right is 331px. Let's replace those with percentages.
1. Before we use our formula, remember that our context has changed. The width of the container is
900px, not 960 anymore.
1. For the main, it's 566 / 900 = .628888889.
1. For the aside, it's 331 / 900 = .367777778

```css
main {
    width: 62.8888889%;
}

aside {
    width: 36.7777778%;
}
```

1. Just like that, we have a flexible, grid-based layout!
1. Now, let's do some detail work.
1. We have some hard-coded margins and paddings on some of our elements. Let's get rid of those.
1. Show mockup. Say we've been treating the space like 24px. Let's change these to match our proportions using our handy formula.

target / context = result
24px / 900px = 0.026666666

```css
main, aside, header {
    padding: 1em 2.6666666%; /* 24px / 900px */
}

.page {
    margin: 1em auto;
}
```