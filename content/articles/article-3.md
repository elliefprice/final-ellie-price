---
title: "Article Three"
description: ""
omit_header_text: true
summary: "Article On Enhancemnet"
type: page
weight: 3
---

## Enhancement Article

For my enhancement I chose to create a toggle button that would change the background of the pages of my website from “Light Mode” to “Dark Mode”. This was a customization of the theming using CSS. 
I put a button in my navigation bar so it shows up on every page.
Code I used:

```js
<button id="mode-toggle">Toggle Dark Mode</button>
```
At this point, the button was visible but didn’t do anything yet. Next, I created the dark mode mechanism using CSS. I put the styles inside my custom.css file in my static folder.
```js
.dark-mode {
  background-color: black;
  color: white;
}

.dark-mode a {
  color: #88c0ff;
}
```
I then wrote CSS rules to change the background and text colors when Dark Mode is active.
Simple CSS wasn’t enough because my theme’s styles were stronger.
Because of this, chatGPT gave me a new CSS to override my theme to ensure the button would work correctly.

```js
/* Global dark mode override */
body.dark-mode, html.dark-mode {
    background-color: #111 !important;
    color: #f1f1f1 !important;
}

/* Force all text to lighten */
.dark-mode * {
    color: #e6e6e6 !important;
    border-color: #555 !important;
}

/* Override theme backgrounds */
.dark-mode,
.dark-mode .container,
.dark-mode .post,
.dark-mode .content,
.dark-mode .post-content,
.dark-mode .article,
.dark-mode .page,
.dark-mode .entry,
.dark-mode .wrapper,
.dark-mode .page-content,
.dark-mode #content {
    background-color: #111 !important;
}

/* Navbar */
.dark-mode nav,
.dark-mode .navbar,
.dark-mode header {
    background-color: #1a1a1a !important;
    color: #eee !important;
}

/* Links */
.dark-mode a {
    color: #80bfff !important;
}

/* Footer */
.dark-mode footer {
    background-color: #1a1a1a !important;
    color: #ddd !important;
}

/* Code blocks */
.dark-mode pre,
.dark-mode code {
    background-color: #333 !important;
    color: #fff !important;
}
```
I then needed to link custom.css inside the <head> of baseof.html:
```js
<link rel="stylesheet" href="/css/custom.css">
```

JavaScript makes the button actually switch modes.
 This script looks for the toggle button and adds or removes the .dark-mode class when the button is clicked.
I added the script at the bottom of the <body> section of baseof.html.

```js
document.addEventListener("DOMContentLoaded", function () {
  const toggle = document.getElementById("mode-toggle");
  if (!toggle) return;

  toggle.addEventListener("click", function () {
    document.body.classList.toggle("dark-mode");
  });
});
```
```js DOMContentLoaded ``` makes sure the page loads before the script runs.
```js getElementById()``` finds the toggle button in the navigation bar.
```js addEventListener("click")```  listens for button clicks.
```js lassList.toggle()``` turns dark mode on and off by adding or removing .dark-mode.


I originally placed the script in the wrong section of the page, which caused it not to work. Moving it to the bottom of the <body> fixed the problem because the button now exists when the script runs.

## Full ChatGPT Conversation (of explanation)

Enhancement Article: Adding a Dark Mode Toggle Button

For my website enhancement, I chose to create a Dark Mode toggle button. This button allows the user to switch the site from “Light Mode” (default) to “Dark Mode,” which makes the background darker and the text lighter. This enhancement involved HTML, CSS, and JavaScript working together.

1. Adding the Toggle Button (HTML)

The first step was putting a button into my navigation bar so that it appears on every page of my website. I added the following line inside my nav.html partial:

<button id="mode-toggle">Toggle Dark Mode</button>


This created the button, but at this point the button did not do anything yet.

2. Creating Dark Mode Styling (CSS)

Next, I created the CSS rules that control what the page looks like in dark mode. I added this to my custom.css file inside the static/css/ folder.

Initially I tried simple CSS:

.dark-mode {
  background-color: black;
  color: white;
}

.dark-mode a {
  color: #88c0ff;
}


However, because my Hugo theme applied its own styles, this basic CSS wasn’t strong enough. The dark mode only applied to a few areas and not the whole page. ChatGPT helped me generate CSS that overrides my theme using !important. This fixed the issue:

/* Global dark mode override */
body.dark-mode, html.dark-mode {
    background-color: #111 !important;
    color: #f1f1f1 !important;
}

/* Force all text to lighten */
.dark-mode * {
    color: #e6e6e6 !important;
    border-color: #555 !important;
}

/* Override theme backgrounds */
.dark-mode,
.dark-mode .container,
.dark-mode .post,
.dark-mode .content,
.dark-mode .post-content,
.dark-mode .article,
.dark-mode .page,
.dark-mode .entry,
.dark-mode .wrapper,
.dark-mode .page-content,
.dark-mode #content {
    background-color: #111 !important;
}

/* Navbar */
.dark-mode nav,
.dark-mode .navbar,
.dark-mode header {
    background-color: #1a1a1a !important;
    color: #eee !important;
}

/* Links */
.dark-mode a {
    color: #80bfff !important;
}

/* Footer */
.dark-mode footer {
    background-color: #1a1a1a !important;
    color: #ddd !important;
}

/* Code blocks */
.dark-mode pre,
.dark-mode code {
    background-color: #333 !important;
    color: #fff !important;
}


This CSS fully forces the theme into dark mode when .dark-mode is active.

3. Linking My Custom CSS File in the HTML

To make sure the styles load, I had to link custom.css inside the <head> section of baseof.html.

I added:

<link rel="stylesheet" href="/css/custom.css">


Without this link, the browser would never know that custom.css exists, so dark mode would not work.

4. Adding the JavaScript (JS)

The JavaScript is what actually activates dark mode when the button is clicked. I placed the script at the bottom of the <body> of baseof.html.

document.addEventListener("DOMContentLoaded", function () {
  const toggle = document.getElementById("mode-toggle");
  if (!toggle) return;

  toggle.addEventListener("click", function () {
    document.body.classList.toggle("dark-mode");
  });
});

What this script does (in simple terms):

DOMContentLoaded → waits until the page finishes loading

getElementById() → finds the toggle button by ID

addEventListener("click") → listens for button clicks

classList.toggle() → adds or removes .dark-mode on the <body>

When the class is added → Dark Mode turns on
When the class is removed → The site goes back to Light Mode

5. Fixing the JavaScript Placement Bug

My toggle didn’t work at first because I put the script in the wrong section of the page.

The problem was:

The JavaScript tried to find the button before the button was loaded.

The fix was to move the script to the bottom of the <body> so that the button exists when the script runs. After moving it, the toggle worked perfectly.

Final Summary

By combining HTML (the button), CSS (the dark-mode styles), and JavaScript (the toggle action), I successfully added a Dark Mode toggle to my website. The biggest challenge was overriding my theme’s default styling and placing the JavaScript in the correct location, but once those issues were fixed, the enhancement worked exactly as intended.
