--- 
layout: post
title: CSS3 Color Animations
postNumber: 1
truncateCharacter: 350
---

CSS3 animations allow you to alter the values of CSS properties over time.  They're now supported in Firefox 5+, Chrome, Safari 4+, iOS, Android 4+, and the upcoming IE10, therefore, using them in real production websites is possible.  One of the cool things you can do with them is change the color of an element using exclusively CSS.  Previously a technique like this was only possible using <a href="https://developer.mozilla.org/en/window.setInterval">JavaScript's setInterval function</a> to gradually change the appropriate property of the element. See <a href="http://jqueryui.com/demos/animate/">jQuery UI's animate demos</a> for a good example.

### Getting Started

Let's start with a basic example (note - Whether or not you see the animation depends on whether your browser supports CSS3 animations.  You can check at <a href="http://caniuse.com/css-animation">caniuse.com</a>).

<iframe style="width: 100%; height: 120px;" src="http://jsfiddle.net/RfYMA/1/embedded/result,html,css/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

### Syntax

Let's break this down one section at a time.
<pre class="prettyprint lang-css linenums">
div {
	-webkit-animation: color_change 1s infinite alternate;
    -moz-animation: color_change 1s infinite alternate;  
	-ms-animation: color_change 1s infinite alternate;  
	-o-animation: color_change 1s infinite alternate;
	animation: color_change 1s infinite alternate;   
}
</pre>

The <code>animation</code> property is how you define a <a href="https://developer.mozilla.org/en/CSS/CSS_animations">CSS3 animation</a>.  The <a href="https://developer.mozilla.org/en-US/">MDN</a> (Mozilla Developer Network) docs have extensive documentation on all the various sub properties available to configure the animation <a href="https://developer.mozilla.org/en/CSS/CSS_animations#Configuring_the_animation">here</a>.  In this example I'm setting…
<ul>
	<li>
		<code><a href="https://developer.mozilla.org/en/CSS/animation-name">animation_name</a></code>:
		<code>color_change</code> - This refers to a named @keyframes rule, which we'll get into in a minute.
	</li>
	<li>
		<code><a href="https://developer.mozilla.org/en/CSS/animation-duration">animation_duration</a></code>:
		<code>1s</code> - The animation should last 1 second.
	</li>
	<li>
		<code><a href="https://developer.mozilla.org/en/CSS/animation-iteration-count">animation_iteration_count</a></code>:
	 	<code>infinite</code> - The animation will cycle forever.
	</li>
	<li>
		<code><a href="https://developer.mozilla.org/en/CSS/animation-direction">animation_direction</a></code>:
		<code>alternate</code> - This will tell the animation to alternate, from start to end, then end to start, then start to end, and so on.  In this example it keeps the box from being jerky by quickly switching from red to blue.
	</li>
</ul>

For readability you can also list the properties out individually.

<pre class="prettyprint linenums lang-css">
/* Note: Prefixes omitted, see below */
div {
	animation-name: color_change;
	animation-duration: 1s;
	animation-iteration-count: infinite;
	animation-direction: alternate;
}
</pre>

### Prefixes

The vendor prefixes are necessary because CSS3 animations are still considered an experimental feature (the <a href="http://www.w3.org/TR/css3-animations/">spec</a> is still in working draft status.  However, the syntax is consistent across modern browsers, so you only have to copy and paste the code to add all the necessary prefixes.  Always include the un-prefixed property last to make your code future friendly to browsers that add un-prefixed support.  For an up to date list of what browsers support CSS3 animations and which prefixes to use check out the <a href="http://caniuse.com/css-animation">CSS animation page at caniuse.com</a>.

If you get sick of typing out all the vendor prefixes you're not alone.  <a href="http://leaverou.github.com/prefixfree/">-prefix-free</a> is a tool by <a href="http://lea.verou.me/">Lea Verou</a> that lets you write your CSS unprefixed.  A JavaScript file detects whether a browser prefix is necessary, which one to use, and applies it automatically.

Another option is <a href="http://prefixr.com/">Prefixr</a> by Jeffrey Way of <a href="http://net.tutsplus.com/">nettuts</a>.  It lets you copy and paste your code in, run it, and have the appropriate prefixes added automatically.

Browser prefixes have been been a hot topic lately after it was announced that IE, Firefox, and Opera are <a href="http://lists.w3.org/Archives/Public/www-style/2012Feb/0313.html">considering adopting support for -webkit prefixes</a>.  If you're curious a <a href="http://remysharp.com/2012/02/09/vendor-prefixes-about-to-go-south/">number</a> <a href="http://christianheilmann.com/2012/02/09/now-vendor-prefixes-have-become-a-problem-want-to-help-fix-it/">of</a> <a href="http://www.brucelawson.co.uk/2012/on-the-vendor-prefixes-problem/">others</a> have <a href="http://infrequently.org/2012/02/misdirection/">written</a> about this.

### Keyframes

<pre class="prettyprint lang-css linenums">
@-webkit-keyframes color_change {
	from { background-color: blue; }
	to { background-color: red; }
}
@-moz-keyframes color_change {
	from { background-color: blue; }
	to { background-color: red; }
}
@-ms-keyframes color_change {
	from { background-color: blue; }
	to { background-color: red; }
}
@-o-keyframes color_change {
	from { background-color: blue; }
	to { background-color: red; }
}
@keyframes color_change {
	from { background-color: blue; }
	to { background-color: red; }
}
</pre>

<a href="https://developer.mozilla.org/en/CSS/@keyframes">Keyframes</a> are a way of specifying a set of properties and their values at different states of an animation.  <code>@keyframes color_change</code> gives the @keyframes a name of <code>color_change</code>.  This provides the connection used on the animation property above.

<pre class="prettyprint lang-css">
from { background-color: blue; }
to { background-color: red; }
</pre>

This animation only has 2 steps, a start and an end.  Since such animations are quite common, the <a href="http://www.w3.org/TR/css3-animations/#keyframes-">spec</a> provides the keywords <code>from</code> and <code>to</code> for defining the state of properties at the beginning and end of the animation.  This could also have been written using percentages for the steps.

<pre class="prettyprint lang-css">
0% { background-color: blue; }
100% { background-color: red; }
</pre>

If the animation has more than 2 steps, they can be listed using multiple steps as such.

<pre class="prettyprint lang-css">
0% { background-color: blue; }
25% { background-color: orange; }
50% { background-color: yellow; }
75% { background-color: black; }
100% { background-color: red; }
</pre>

### Real World Example

Since the first demo was rather contrived, I thought I'd provide an example of how you could use this technique in the real world.  On buttons, a common UI pattern is to provide the user with visual feedback that they're on the button by applying a subtle color change.  This is usually done by applying a different <code>background-color</code> on the hover pseudoclass of the button as such:

<pre class="prettyprint lang-css linenums">
button {
	background-color: pink;
}
button:hover {
	background-color: hotpink;
}
</pre>

To improve upon this, we can add a CSS 3 color animation to gradually make the color transition.  The following example shows each side by side:

<iframe style="width: 100%; height: 250px" src="http://jsfiddle.net/PTfZD/3/embedded/result,html,css/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

### Falling Back Gracefully

Since CSS3 animations are only present in modern browsers, there's a good chance a number of your users won't have them available.  Luckily, CSS3 animations fallback gracefully to browsers that don't support them.  If the browser doesn't know how to handle a CSS animation, it just ignores the CSS rules.  Therefore, make sure not to use CSS animations to perform functionality that is vital to your site or application, it should simply enhance the user experience.

In the button example above if the browser can't perform the animation, the animated button will simply fallback on the hover button's behavior.

<pre class="prettyprint lang-css linenums">
button {
	background-color: pink;
}
button:hover {
	/* IE <= 6 get no hover effect */
	/* All browsers IE 7+ know how to handle this */
	background-color: hotpink;
	
	/* Browsers that support CSS animations get the animation, */
	/* those that don't ignore this and move on. */
	/* Note: I've omitted the vendor prefixes for simplicity. */
	animation: color_change 1s;
}
</pre>

### Detect Support and Polyfill

If you have a CSS color animation that you absolutely must have work on all browsers back to IE6, you can do so by detecting support via <a href="modernizr.com">Modernizr</a>, and falling back to <a href="http://jqueryui.com/demos/animate/">jQuery UI's animation</a>.

<pre class="prettyprint lang-js linenums">
if (!Modernizr.cssanimation) {
	$('button').on('mouseover', function() {
		//jQuery UI doesn't support the hotpink keyword :(
		$(this).animate({ backgroundColor: '#FF69B4' }, 1000);
	}).on('mouseout', function() {
		$(this).stop(true, true);
		$(this).css('backgroundColor', 'pink');
	});            
}
</pre>

Live example (this should work across all browsers):

<iframe style="width: 100%; height: 160px" src="http://jsfiddle.net/tj_vantoll/2Yrpe/3/embedded/result,js,css,html" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

If the jQuery UI approach already works cross browser why would you bother doing this with CSS?
<ul>
	<li>Certain desktop and mobile browsers can use hardware acceleration with CSS3 animations.  This usually results in the animation rendering smoother.</li>
	<li>Users with JavaScript disabled will still see the animation.</li>
	<li>If you're only using jQuery & jQuery UI for this animation you can save yourself two HTTP requests by using <a href="http://www.modernizr.com/docs/#load">Modernizr's load function</a>.  This will first test whether the browser supports CSS animations, if it does nothing needs to be done, if it doesn't all scripts listed in the <code>nope</code> parameter will be loaded.
</ul>

<pre class="prettyprint lang-js linenums">
Modernizr.load({
	test: Modernizr.cssanimation,
	nope: ['jquery.js', 'jquery-ui']
});
</pre>

### Summary

CSS 3 color animations can be used in modern browsers today.  For most use cases no animations in unsupported browsers isn't a problem, and, if it is, <a href="http://jqueryui.com">jQuery UI</a> can be used to polyfill the functionality.