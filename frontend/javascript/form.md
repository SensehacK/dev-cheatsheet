# Form



## Disable Input Paste


You can disable paste on input fields in javascript and web.
Disable paste in your input as follows:


```
html:
<input type="text" value="" id="myInput">

javascript:

window.onload = () => {
 const myInput = document.getElementById('myInput');
 myInput.onpaste = e => e.preventDefault();
}
```
[SO](https://stackoverflow.com/questions/12805803/disable-copy-paste-in-html-input-fields)


### Enable disable on browser settings or extension.

Firefox settings can be accessed by entering the following text in the address bar.

> about: config

Search for this key `dom.event.clipboardevents.enabled` &
set the boolean value to false

[How to geek](https://www.howtogeek.com/251807/how-to-enable-pasting-text-on-sites-that-block-it/)