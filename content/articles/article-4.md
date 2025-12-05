---
title: "Article Four"
description: ""
omit_header_text: true
summary: "Article on AI Use"
type: page
weight: 3
---

## AI Use Article

The use of AI was incredibly helpful in creating my project. It not only assisted me in troubleshooting mistakes I made, but played a large role in creating my enhancement. I first used AI to help me create my index.html file to ensure that my blog posts had their own index and were not rendering on my home page. 

Here is the link to my conversation: https://chatgpt.com/share/6932817c-ded8-8013-8809-4ac63430f18d

However, (for whatever reason) it would not load my complete conversation for trouble shooting the full Dark Mode Toggle button. I was able to copy and paste the chat, but it wouldn't load a link for my full conversation. I have the full conversation copy and pasted below after the conclusion of this article. 

AI also helped me to get my image to render correctly on my “About Me” page. Initially, I had linked the file of the image directly to the static folder (as seen in my initial-ellie-price). I told chatGPT that my image was not rendering and it asked to know the directions of my static folder. After explaining what my static folder looked like to chatGPT, it instructed me to instead create a “css” and “images” folder to house the image instead. Once I fixed that error, my photo presented correctly on my “About Me” page. 

Lastly, AI was mostly helpful in assistance in creating my enhancement. I chose to create a button that would turn my website from “Light Mode” to “Dark Mode”. I was aware of creating the button, but I had very little knowledge on how to ensure the function worked. Not only did AI instruct me on how to create the functional button, it also helped me to override my theme to ensure it worked. The original solution it gave me would work for a typical Hugo site, however my theme was restricting the button from working correctly. I expressed my concerns to chatGPT and it provided me with a similar solution utilizing “important!” to guarantee the function of the button would override the theme settings and work correctly. 

Here is a link to my conversation: https://chatgpt.com/share/69328842-1d44-8013-86e2-0fef6e927aad

In the same context, I used my AI chats to help me explain and understand my enhancement for my article. Since I was unfamiliar with the way the code worked, it helped me to grasp the main ideas and cultivate an essay explaining the steps of the enhancement. 

In essence, I found AI to be very helpful in this project. It helped me to create a fully working enhancement, explain my enhancement steps, and fix any minute errors I might have faced along the way of this project. However, the solutions and explanations were difficult for me to fully understand. Although it was confusing at times, it ultimately gave me the solutions I was looking for. 

## Full chatGPT conversation: 
✅ Step 1 — Add the Toggle Button (HTML)
Put this inside your theme header or navigation.
File:
 themes/beautifulhugo/layouts/partials/header.html
 (or wherever you want the button to show)
<button id="mode-toggle" style="cursor:pointer;">
  Toggle Dark Mode
</button>


✅ Step 2 — Add Dark Mode CSS
Add this to your main CSS file.
File:
 static/css/custom.css
 (If you don't have it, create it.)
.dark-mode {
  background-color: #111;
  color: white;
}

.dark-mode a {
  color: #90caf9;
}

Then include the CSS in head.html:
File:
 themes/beautifulhugo/layouts/partials/head.html
Add:
<link rel="stylesheet" href="/css/custom.css">


✅ Step 3 — Add the JavaScript
Place this at the bottom of baseof.html right before </body>.
File:
 themes/beautifulhugo/layouts/_default/baseof.html
Add:
<script>
  const toggle = document.getElementById("mode-toggle");

  toggle.addEventListener("click", function () {
    document.body.classList.toggle("dark-mode");
  });
</script>


🌙 That’s it — you now have a working Dark Mode toggle!
No Hugo Pipes, no minify, no errors.

If you want, I can:
✅ Make the button look better
 ✅ Make it save the mode in localStorage so it stays after reload
 ✅ Turn it into a little sun/moon icon
Just tell me!
You said:

its not working
ChatGPT said:
Thought for 5s
Nice screenshot — thanks, that made the problem obvious. Two things are wrong in your baseof.html right now that prevent the toggle from working:
Your <script> runs before the toggle button exists (you put the script before the navbar/header that contains the button). That makes document.getElementById("mode-toggle") return null, so nothing happens.


Your CSS link is placed after </html>, so your styles may not be loading.


Below I give a minimal, safe layout you can paste into themes/beautifulhugo/layouts/_default/baseof.html (or fix your file to match the structure). This ensures the CSS is in the <head>, the DOM elements exist when the script runs, and the script is robust (won’t throw errors if the button is missing).

1) Put CSS in the head
Edit themes/beautifulhugo/layouts/partials/head.html or inside <head> in baseof.html and include:
<link rel="stylesheet" href="/css/custom.css">

Make sure static/css/custom.css exists.

2) Header partial: include the button
In your header partial (e.g. themes/beautifulhugo/layouts/partials/header.html) add the button where you want it to appear (inside the nav):
<button id="mode-toggle" style="cursor:pointer;">Toggle Dark Mode</button>

Confirm the id is exactly mode-toggle.

3) Use this correct baseof.html skeleton
Replace the relevant parts of your baseof.html with something like this (keep your partial calls and blocks — this is just the structure):
<!DOCTYPE html>
<html lang="{{ .Lang }}">
  <head>
    {{ partial "head.html" . }}
    <link rel="stylesheet" href="/css/custom.css">  <!-- ensure this is in head -->
  </head>

  <body>
    {{ partial "nav.html" . }}
    {{ block "header" . }}{{ partial "header.html" . }}{{ end }}
    {{ block "main" . }}{{ end }}

    {{ partial "footer.html" . }}

    <!-- Put your script AFTER the elements it touches -->
    <script>
      // wait for DOM in case partials take time to render
      document.addEventListener("DOMContentLoaded", function () {
        const toggle = document.getElementById("mode-toggle");
        if (!toggle) return; // safe-guard: do nothing if button not present

        // optional: restore stored preference
        if (localStorage.getItem("theme") === "dark") {
          document.body.classList.add("dark-mode");
        }

        toggle.addEventListener("click", function () {
          document.body.classList.toggle("dark-mode");

          // optionally persist preference
          if (document.body.classList.contains("dark-mode")) {
            localStorage.setItem("theme", "dark");
          } else {
            localStorage.setItem("theme", "light");
          }
        });
      });
    </script>
  </body>
</html>

Important: There must be one <head> and one <body> block only; remove extra </body> / </html> duplicates you have in the screenshot.

4) custom.css (example)
Put this in static/css/custom.css:
/* light mode (default) */
body {
  background: white;
  color: black;
}

/* dark mode */
.dark-mode {
  background: #111;
  color: #f2f2f2;
}

.dark-mode a { color: #90caf9; }

/* button styling (optional) */
#mode-toggle {
  margin-left: 10px;
  padding: 6px 10px;
  border-radius: 6px;
  border: 1px solid #ccc;
  background: none;
  cursor: pointer;
}


5) How to check it’s working
Run hugo server -D.


Open http://localhost:1313/.


Open DevTools (F12) → Elements: find the button #mode-toggle.


If it’s missing, the partial isn’t included where you thought it was.


Click the button — the body element should gain/remove the dark-mode class.


Check Console for errors. If there’s Uncaught TypeError referencing getElementById, it means the script still ran before the DOM — the DOMContentLoaded wrapper above prevents that.



If you want, I can:
Check the exact contents of your baseof.html (paste it here) and patch it for you, or


Generate the exact header.html, head.html patch files to copy.


But with the three fixes above (CSS in head, button in header, script after body and wrapped in DOMContentLoaded + null-check) this will work reliably.
You said:
this is my base of html page: {{ if le hugo.Version "0.124.0" }} 	{{ errorf "Please use Hugo version 0.124.0 or higher!" }} {{ end }} <!DOCTYPE html> <html lang="{{ .Lang }}" itemscope itemtype="http://schema.org/WebPage"> <head> {{ partial "head.html" . }} </head> <script> const toggle = document.getElementById("mode-toggle"); toggle.addEventListener("click", function () { document.body.classList.toggle("dark-mode"); }); </script> </body> {{ partial "nav.html" . }} {{ block "header" . }}{{ partial "header.html" . }}{{ end }} {{ block "main" . }}{{ end }} {{ partial "footer.html" . }} {{ block "footer" . }}{{ end }} </body> </html> <link rel="stylesheet" href="/css/custom.css">
ChatGPT said:
Your baseof.html is broken in several important ways:
❌ The <script> is outside the <body>
 ❌ There are two <body> tags
 ❌ Your CSS <link> is after </html>
 ❌ The script runs before the toggle button exists, so it fails
 ❌ Your HTML structure is inverted — content is placed after the closing </body>
This will definitely break Hugo layouts and produce unpredictable results.
Below is a correct, fixed, clean version of your baseof.html you can paste in exactly as written.

✅ Corrected baseof.html (copy-paste this)
{{ if le hugo.Version "0.124.0" }}
  {{ errorf "Please use Hugo version 0.124.0 or higher!" }}
{{ end }}

<!DOCTYPE html>
<html lang="{{ .Lang }}" itemscope itemtype="http://schema.org/WebPage">
  <head>
    {{ partial "head.html" . }}
    <link rel="stylesheet" href="/css/custom.css">
  </head>

  <body>
    {{ partial "nav.html" . }}
    {{ block "header" . }}{{ partial "header.html" . }}{{ end }}
    {{ block "main" . }}{{ end }}
    {{ partial "footer.html" . }}
    {{ block "footer" . }}{{ end }}

    <!-- Correct placement: script goes at the bottom *inside* body -->
    <script>
      document.addEventListener("DOMContentLoaded", function () {
        const toggle = document.getElementById("mode-toggle");
        if (!toggle) return; // avoid errors if button missing

        toggle.addEventListener("click", function () {
          document.body.classList.toggle("dark-mode");
        });
      });
    </script>

  </body>
</html>


⚠️ IMPORTANT
You MUST have the button inside your nav or header file.
Put this in themes/beautifulhugo/layouts/partials/header.html:
<button id="mode-toggle">Toggle Dark Mode</button>

Or wherever you want the button to appear.

🎉 After this, the toggle WILL WORK
This fixes:
✔ Correct HTML structure
 ✔ Script loads after elements exist
 ✔ CSS loads in the correct location
 ✔ Removes duplicate <body>
 ✔ No more errors
If you paste your header partial here, I can verify the button placement too.
You said:
the button is showing up, but it does not chnage from light to dark
ChatGPT said:
Great — if the button shows up but nothing changes, then the problem is almost certainly one of these:
✅ 1. Your CSS is not loading
Your custom.css must be in:
static/css/custom.css

Not themes/.../static
 Not assets/css
 Not /content
Correct location:
 initial-ellie-price/static/css/custom.css
Inside custom.css, you must have:
.dark-mode {
  background-color: #111 !important;
  color: #f2f2f2 !important;
}

.dark-mode a {
  color: #90caf9 !important;
}

Add the !important to guarantee it overrides theme styles.
🔥 If CSS doesn’t load → dark mode will appear to do nothing.

✅ 2. Your script IS running, but the theme CSS is overriding it
BeautifulHugo has very strong built-in theme colors.
Your .dark-mode styles must override them.
 Check in DevTools:
Right-click → Inspect


Click the <body> tag.


Click the button.


See if the body gets this class:


<body class="dark-mode">

✔ If the class is added but colors don’t change → CSS is being overridden.
Just add this stronger CSS:
body.dark-mode,
html.dark-mode,
.dark-mode body {
    background: #111 !important;
    color: #eee !important;
}

.dark-mode .post-content,
.dark-mode .article,
.dark-mode .content {
    color: #eee !important;
}

.dark-mode a {
    color: #8ab4f8 !important;
}

Adding !important ensures it wins against theme defaults.

❌ 3. Your CSS link may still be in the wrong place
In your final working baseof.html, the CSS link must be INSIDE <head>:
✔ Correct:
<head>
  {{ partial "head.html" . }}
  <link rel="stylesheet" href="/css/custom.css">
</head>

❌ Wrong (this makes dark mode NOT work):
After </html>


Inside <body>


Inside partials that override each other



❌ 4. Button ID mismatch
Your JS looks for:
document.getElementById("mode-toggle")

Your button MUST be exactly:
<button id="mode-toggle">Toggle Dark Mode</button>

If the ID is different even slightly → click does nothing.

👍 The Quick Debug Test (do this!)
Open your site → Right click → Inspect → Console tab.
Paste this:
document.body.classList.add("dark-mode")

Press Enter.
If the page turns dark → CSS works.
If it stays light → CSS is not loading OR not strong enough.
Tell me which result you get and I’ll fix it in one step.
You said:
this is my baseof.html: {{ if le hugo.Version "0.124.0" }} {{ errorf "Please use Hugo version 0.124.0 or higher!" }} {{ end }} <!DOCTYPE html> <html lang="{{ .Lang }}" itemscope itemtype="http://schema.org/WebPage"> <head> {{ partial "head.html" . }} <link rel="stylesheet" href="/css/custom.css"> </head> <body> {{ partial "nav.html" . }} {{ block "header" . }}{{ partial "header.html" . }}{{ end }} {{ block "main" . }}{{ end }} {{ partial "footer.html" . }} {{ block "footer" . }}{{ end }} <!-- Correct placement: script goes at the bottom *inside* body --> <script> document.addEventListener("DOMContentLoaded", function () { const toggle = document.getElementById("mode-toggle"); if (!toggle) return; // avoid errors if button missing toggle.addEventListener("click", function () { document.body.classList.toggle("dark-mode"); }); }); </script> </body> </html>
ChatGPT said:
Great — your baseof.html is correct now.
 So the JS is working but the theme is overriding your CSS.
That means your .dark-mode class is being added… but BeautifulHugo’s styles are stronger, so nothing visibly changes.
Let’s fix that.

✅ Step 1 — Check if the class is being added
Open your site → Right-click → Inspect → Elements → click the button.
You should see:
<body class="dark-mode">

If you see that, your JS is working.
So now we fix the CSS.

✅ Step 2 — Replace your entire custom.css with this stronger version
Create or replace:
static/css/custom.css

With:
/* Base override */
body.dark-mode,
html.dark-mode {
    background-color: #121212 !important;
    color: #e0e0e0 !important;
}

/* General text */
.dark-mode p,
.dark-mode li,
.dark-mode span,
.dark-mode div {
    color: #e0e0e0 !important;
}

/* Links */
.dark-mode a {
    color: #80bfff !important;
}

/* Navbar */
.dark-mode .navbar,
.dark-mode header,
.dark-mode nav {
    background-color: #1e1e1e !important;
    color: #e0e0e0 !important;
}

/* Article content */
.dark-mode .post,
.dark-mode .post-content,
.dark-mode .article,
.dark-mode .content {
    background-color: #1a1a1a !important;
    color: #e0e0e0 !important;
}

/* Code blocks */
.dark-mode pre,
.dark-mode code {
    background-color: #333 !important;
    color: #eee !important;
}

/* Footers */
.dark-mode footer {
    background-color: #1e1e1e !important;
    color: #e0e0e0 !important;
}


✅ Step 3 — Restart your server
In terminal:
Ctrl + C
hugo server -D


⭐ This WILL work
BeautifulHugo has many nested containers with their own colors, so the dark-mode CSS MUST:
Use !important


Target nav, footer, posts, content blocks


Override theme background defaults


The CSS above covers all of that.

If you want, send me:
A screenshot of your site


Your header/nav partial


Your current custom.css


And I can fine-tune the dark mode so it looks perfect.
You said:
this is the message i recieved after dong the commands: cpric@CPrice MINGW64 ~/initial-ellie-price (main) $ Ctrl + C hugo server -D bash: Ctrl: command not found Watching for changes in C:\Users\cpric\initial-ellie-price\{archetypes,assets,content,data,i18n,layouts,static,themes} Watching for config changes in C:\Users\cpric\initial-ellie-price\hugo.toml Start building sites … hugo v0.151.2-a3574f6f70c9b272e3de53cf976018ee3ff16fd1+extended windows/amd64 BuildDate=2025-10-16T16:52:34Z VendorInfo=gohugoio WARN calling IsSet with unsupported type "ptr" (*page.siteWrapper) will always return false. WARN calling IsSet with unsupported type "invalid" (<nil>) will always return false. │ EN ──────────────────┼───── Pages │ 15 Paginator pages │ 0 Non-page files │ 0 Static files │ 194 Processed images │ 0 Aliases │ 2 Cleaned │ 0 Built in 8076 ms Environment: "development" Serving pages from disk Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender Web Server is available at http://localhost:1313/ (bind address 127.0.0.1) Press Ctrl+C to stop
ChatGPT said:
No worries — that message just means you typed:
Ctrl + C

literally into the terminal, and Bash tried to interpret it as a command.
✅ Correct way to stop Hugo:
Just press:
Hold Ctrl and tap C
Do NOT type the letters Ctrl + C.

But the important part:
Your server did restart successfully, and Hugo is running fine:
Web Server is available at http://localhost:1313/

So now we can check the dark mode.

✅ Next Step: Confirm whether dark mode is working
Open your site in the browser


Press your Toggle Dark Mode button


Open DevTools → Inspect → Elements


Look at the <body> tag


Does it change from:
<body>

to
<body class="dark-mode">

❗ Tell me which one you see.
If the class appears → JS is working → CSS is the only problem.
 If the class does NOT appear → the toggle button ID or JS path is wrong.

⭐ You are very close.
Just tell me what the <body> tag shows when you click the button, and I’ll fix the final piece.
You said:
i see: <body class="dark-mode">
ChatGPT said:
Perfect — that tells us:
✅ Your JavaScript is working
❌ Your CSS is not taking effect
Your Hugo theme is overriding your dark-mode styles.
So now we fix ONLY the CSS.

✅ 1. Confirm your CSS file is in the right location
This is the #1 reason dark mode still looks the same.
Your custom.css MUST be exactly here:
initial-ellie-price/static/css/custom.css

Not:
themes/beautifulhugo/static/


assets/


content/


layouts/


ONLY the project-level static folder works for /css/custom.css.
Double-check the folder path on your computer.

✅ 2. Confirm the browser is loading your CSS
Open your browser → right-click → Inspect → Network → reload.
Look for this file:
custom.css
Status: 200

If it is not loading → the path is wrong.
If it loads → the CSS needs to be stronger.

✅ 3. Replace your entire custom.css with this bulletproof version
Paste this into:
static/css/custom.css

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

This version is extremely aggressive — it overrides all theme styles using !important and wildcard selectors.

✅ 4. Restart the server
In the terminal:
Press Ctrl + C
 Then run:
hugo server -D


🎉 After this, your dark mode will visibly change the entire site
If anything is still not switching colors, send me:
👉 A screenshot of the page after clicking “Toggle Dark Mode”
 👉 A screenshot of your static/css folder
I’ll fix the rest in seconds.
You said:


ChatGPT said:
Great — your screenshots tell me exactly what's happening:
✅ Your button works — it does toggle the dark-mode class on <body>
 ❌ Your CSS is not applying, because your selectors are wrong.

✅ THE REAL ISSUE
Your CSS file uses selectors like:
body.dark-mode,
html.dark-mode {
  background-color: #111 !important;
  color: #f1f1f1 !important;
}

…but in your screenshot, the HTML shows:
<body class="dark-mode">

That means your CSS should work — but it doesn’t, which means one of these two things is happening:

❗ ISSUE #1 — Your custom.css file is in the wrong place
Your file is in:
static/images/css/custom.css

But in your HTML you load:
<link rel="stylesheet" href="/css/custom.css">

These do NOT match.
👉 Hugo will serve this file at:
/images/css/custom.css

But you are trying to load:
/css/custom.css

📌 So your dark mode CSS never loads.

✅ FIX
Move your file here:
static/css/custom.css

NOT inside static/images/.

❗ ISSUE #2 — Your theme CSS overrides everything
Even after moving the file, the theme might override your styles unless you use strong selectors.
To be safe, add this at the TOP of custom.css:
body.dark-mode * {
  color: #f1f1f1 !important;
  background-color: #111 !important;
}

This guarantees dark mode shows everywhere.

✔️ After you move the file:
Move the file:


static/images/css/custom.css  ❌ wrong
static/css/custom.css         ✅ correct

Save everything.


Stop Hugo server (Ctrl+C)


Restart:


hugo server -D
 