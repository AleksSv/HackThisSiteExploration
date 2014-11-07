HackThisSiteExploration
=======================

Exploration of the challenges on https://www.hackthissite.org

This website has a multitude of hacking challenges, the purpose of this exploration is to go through some of them and document my solutions. I primarily used Chrome Dev Tools for inspection.

(I also learned the difference between ' and ` for github markdown)
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

Escape!
-------------

This time the password is displayed as a hexadecimal, 696C6F76656D6F6F, I went to http://www.string-functions.com/hex-string.aspx to convert it and it resulted in ilovemoo

```javascript
moo = unescape('%69%6C%6F%76%65%6D%6F%6F');
      function check (x) {
        if (x == moo)
        {
          alert("Ahh.. so that's what she means");
          window.location = "../../../missions/javascript/5/?lvl_password="+x;
        }
        else {
          alert("Nope... try again!");
        }
}
```

go go away .js
-----------------

This is code was intended to be very messy and hard to read. However, ultimately the button can tell me which function was used to check the password, that function was inside the attached script src checkpass

```html
<button onclick="javascript:checkpass(document.getElementById('pass').value)">Check Password</button></p>
```

```javascript
<script type="text/javascript" src="/missions/javascript/6/checkpass"></script>
<script language="javascript">
RawrRawr = "moo";
function check(x)
{
"+RawrRawr+" == "hack_this_site"
if (x == ""+RawrRawr+"")
{
alert("Rawr! win!");
window.location = "about:blank";
} else {
alert("Rawr, nope, try again!");
}
}

function checkpassw(moo)
{
RawrRawr = moo;
checkpass(RawrRawr);
}
</script>
```

Contents of checkpass
```javascript
dairycow="moo";
moo = "pwns";
rawr = "moo";

function checkpass(pass)
{
if(pass == rawr+" "+moo)
{	
alert("How did you do that??? Good job!");
window.location = "../../../missions/javascript/6/?lvl_password="+pass;
} else {
alert("Nope, try again");
}
}
```

JS Obfuscation. FTW!
------------------

This was the first challenge rated as moderate, they weren't kidding about obfuscation. However, the solution was still obvious, j00w1n is the correct answer. I spent a while analyzing the Javascript, but it is simply writing the button HTML through the use of hexadecimals. And you can get the answer simply by looking at the HTML.

```html
<button onclick="javascript:if (document.getElementById("pass").value=="j00w1n"){alert("You WIN!");window.location += "?lvl_password="+document.getElementById("pass").value}else {alert("WRONG! Try again!")}">Check Password</button>
```

```javascript
<script language="javascript">
var _0x4e9d=["\x66\x72\x6F\x6D\x43\x68\x61\x72\x43\x6F\x64\x65","\x77\x72\x69\x74\x65"];document[_0x4e9d[0x1]](String[_0x4e9d[0x0]](0x3c,0x62,0x75,0x74,0x74,0x6f,0x6e,0x20,0x6f,0x6e,0x63,0x6c,0x69,0x63,0x6b,0x3d,0x27,0x6a,0x61,0x76,0x61,0x73,0x63,0x72,0x69,0x70,0x74,0x3a,0x69,0x66,0x20,0x28,0x64,0x6f,0x63,0x75,0x6d,0x65,0x6e,0x74,0x2e,0x67,0x65,0x74,0x45,0x6c,0x65,0x6d,0x65,0x6e,0x74,0x42,0x79,0x49,0x64,0x28,0x22,0x70,0x61,0x73,0x73,0x22,0x29,0x2e,0x76,0x61,0x6c,0x75,0x65,0x3d,0x3d,0x22,0x6a,0x30,0x30,0x77,0x31,0x6e,0x22,0x29,0x7b,0x61,0x6c,0x65,0x72,0x74,0x28,0x22,0x59,0x6f,0x75,0x20,0x57,0x49,0x4e,0x21,0x22,0x29,0x3b,0x77,0x69,0x6e,0x64,0x6f,0x77,0x2e,0x6c,0x6f,0x63,0x61,0x74,0x69,0x6f,0x6e,0x20,0x2b,0x3d,0x20,0x22,0x3f,0x6c,0x76,0x6c,0x5f,0x70,0x61,0x73,0x73,0x77,0x6f,0x72,0x64,0x3d,0x22,0x2b,0x64,0x6f,0x63,0x75,0x6d,0x65,0x6e,0x74,0x2e,0x67,0x65,0x74,0x45,0x6c,0x65,0x6d,0x65,0x6e,0x74,0x42,0x79,0x49,0x64,0x28,0x22,0x70,0x61,0x73,0x73,0x22,0x29,0x2e,0x76,0x61,0x6c,0x75,0x65,0x7d,0x65,0x6c,0x73,0x65,0x20,0x7b,0x61,0x6c,0x65,0x72,0x74,0x28,0x22,0x57,0x52,0x4f,0x4e,0x47,0x21,0x20,0x54,0x72,0x79,0x20,0x61,0x67,0x61,0x69,0x6e,0x21,0x22,0x29,0x7d,0x27,0x3e,0x43,0x68,0x65,0x63,0x6b,0x20,0x50,0x61,0x73,0x73,0x77,0x6f,0x72,0x64,0x3c,0x2f,0x62,0x75,0x74,0x74,0x6f,0x6e,0x3e));
</script>
```

I created my own HTML page, with simply this script inside it, and suprisingly this javascript actually creates that button noted above. I also did console.log(_0x4e9d) which resulted in

```
Array[2]
    0: "fromCharCode"
    1: "write"
    length: 2
```

From this pointed I know that each hexadecimal value was simply a character from the button HTML. 
