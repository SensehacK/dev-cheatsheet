# CSS iFrame

Using Embed.ly stack widget but felt too much text and sponsorship to that widget which defeats my minimalistic approach to the design.

```html

<div class="embedly-card">
	<h4>
		<a
			href="https://medium.com/@kautilyasave/save-your-eyes-in-digital-life-d1269f50c06e"
			target="_blank"
			>Save your Eyes in Digital Life! - Kautilya Save - Medium</a
		>
	</h4>
	<p>
		An article comparing Mac OS Dark Mode Implementation Vs Windows
		10 Dark Mode & how sleep tracking apps & dark mode could improve
		your inconsistent sleep cycles & eyes.
	</p>
	<script
		async
		src="//cdn.embedly.com/widgets/platform.js"
		charset="UTF-8"
	></script>
</div>
```


Javascript for removing “Powered by Embed Ly” or “Via Embed.ly”

```javascript
// Calling Rescue Time Data
document.addEventListener("DOMContentLoaded", function () {
	// ...
	// setTimeout(embedLin, 5000);
	setTimeout(removeAllEmbed, 5000);
});

function embedLin() {
	console.log("Hello Kautilya");
	var cssLink = document.createElement("link");
	cssLink.href = "../css/embed.css";
	cssLink.rel = "stylesheet";
	console.log(cssLink.href.toString());
	cssLink.type = "text/css";
	// console.log(frames["emb_5480cf"].document.body);
	window.frames["embedly-card"].document.body.appendChild(cssLink);

	// frames["c"].document.body.appendChild(cssLink);
}

function removeAllEmbed() {
	console.log("Hello Sensehack");
	removeEmbedLayer("emb_sm4o04");
	removeAuthorViaEmbed("emb_sm4o04");
	removeEmbedLayer("emb_0is1oe");
	removeAuthorViaEmbed("emb_0is1oe");
	removeEmbedLayer("emb_5480cf");
	removeAuthorViaEmbed("emb_5480cf");
}

function oldEmbedRemove() {
	var iframe = document.getElementById("emb_sm4o04");
	var style = document.createElement("style");
	style.textContent =
		".card .brd {" +
		" text-align: right; padding: 7px 0 5px; display: none !important;" +
		"}";
		sty
	iframe.contentDocument.head.appendChild(style);
}

function removeEmbedLayer(idName) {
	var iframe1 = document.getElementById(idName);
	var style = document.createElement("style");
	style.textContent = ".card .brd {" + "display: none !important;" + "}";
	iframe1.contentDocument.head.appendChild(style);
}

function removeAuthorViaEmbed(idName) {
	var iframe1 = document.getElementById(idName);
	var style = document.createElement("style");
	style.textContent = ".card .hdr .via {" + "display: none !important;" + "}";
	iframe1.contentDocument.head.appendChild(style);
}
```

[SO](https://stackoverflow.com/questions/217776/how-to-apply-css-to-iframe?noredirect=1&lq=1)


## End Result

Image Before vs After differences

![alt text][article]

[article]: https://raw.githubusercontent.com/SensehacK/dev-cheatsheet/master/assets/clean_article_embedly.png
“Before After Article Stack

