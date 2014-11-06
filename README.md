HackThisSiteExploration
=======================

Exploration of the challenges on https://www.hackthissite.org

This website has a multitude of hacking challenges, the purpose of this exploration is to go through some of them and document my solutions.

(I also learned the difference between ' and `)
Javascript Problems
=======================

Listed at https://www.hackthissite.org/missions/javascript/

Idiot Test
----------------------
As noted, this problem was easy, simply by inspecting the javascript we can see that the authentication is done client-side which is obviously a bad idea.

```javascript
function check(x)
{
    if (x == "cookies")
    {
        alert("win!");
        window.location += "?lvl_password="+x;
    } else {
        alert("Fail D:");
    }
}
```

Disable Javascript
---------------------

Still easy, as noted in the problem redirecting through javascript is hardly secure as javascript can always be disabled client-side. I used a firefox addon called QuickJS 1.3 that allows quick disabling and renabling of javascript

Math Time
---------------------

This time, an obscure client-side calculation is done which is used to check the length of a password. Since moo can be easily calculated as 14, the password can be anything 14 characters long such as 12345678901234

```javascript
var foo = 5 + 6 * 7  //This evaluates to 47
var bar = foo % 8 //This evaluates to 7
var moo = bar * 2 //This evaluates to 14
var rar = moo / 3
function check(x)
{
        if (x.length == moo)
        {
                        alert("win!");
                        window.location += "?lvl_password="+x;
        } else {
                        alert("fail D:");
	 }
}
```

Var?
-------------------

This is the first problem that made me facepalm, at first you don't see an obvious solution by inspecting the code.

```javascript
function check(x)
{
        "+RawrRawr+" == "hack_this_site"
	if (x == ""+RawrRawr+"")
        {
		alert("Rawr! win!");
                window.location = "../../../missions/javascript/4/?lvl_password="+x;
        } else {
		alert("Rawr, nope, try again!");
	}
}
```

Until you realize that there is a scroll bar, scroll to the right and you get

```javascript
RawrRawr = moo;
```

