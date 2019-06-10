---


---

<h1 id="scss">SCSS</h1>
<p>SCSS/SASS is a CSS extension language, that makes styling easier by introducing features such are <em>variables</em>, <em>nesting properties</em>, etc.</p>
<p>However, browsers do not support .scss format, they only support .css format. In order to convert .scss files to .css we actually need a compiler.<br>
SASS and SCSS are pretty much the same except for minor syntax variations.</p>
<h2 id="variables">Variables</h2>
<p>SCSS makes it easier by enabling us to use variables, just like any other language. we can use variables to store certain values and use them wherever we want.</p>
<p>.scss :</p>
<pre><code>$varName : green;

h1{
	color : $varName;
}
h2{
	color : $varName;
}
</code></pre>
<p>The above SCSS code gets translated into css as,</p>
<p>.css :</p>
<pre><code>h1{
	color: green;
}
h2{
	color: green;
}
</code></pre>
<p>The point to be noted here is, when we want to change a value we used in so many places, it would be much easier if we had used variables. Changing <code>$varName</code> to <code>red</code> would ultimately replace the all the locations that used it in <code>.css</code>	file.</p>
<h2 id="nesting-properties">Nesting properties</h2>
<p>In SCSS we can nest properties, though is not supported by CSS it gets translated into respective CSS style when compiled.<br>
Here’s an example,</p>
<p>.scss:</p>
<pre><code>$background-color : blue;
$hover-color : aqua;
nav{
	ul{
		background : $background-color;
		a{
			padding: 10px 16px; // short hand for top and bottom and left and right.
		}
		a:hover{
			backgound : $hover-color;
		}
	}
}
</code></pre>
<p>The above SCSS gets translated to,</p>
<p>.css</p>
<pre><code>nav ul{
	background: blue;
}
nav a{
	padding: 10px 16px;
}
nav a:hover{
	background : aqua;
}
</code></pre>
<h2 id="partials">Partials</h2>
<p>SCSS enables us to define part of the styling in a separate file and include it in the main stylesheet to improve readability.</p>
<blockquote>
<p>Create SCSS file with name starting with <code>_</code> (an underscore) and ends with usual .scss extension.</p>
</blockquote>
<p>The underscore is an indication that this is not a main stylesheet and it is going to be imported into a main stylesheet.</p>
<blockquote>
<p>In the main stylesheet import the partial stylesheet we created by adding the following line to the main sheet.<br>
<code>@import "partialStylesheetNameWithoutUnderscore"</code></p>
</blockquote>
<h4 id="example">Example:</h4>
<p><strong>_partial.scss</strong>:</p>
<pre><code>$div-background : blue;
div{
	background : $div-background;
}
</code></pre>
<p><strong>main.scss</strong>:</p>
<pre><code>@import "partial"; 
$font-color : green;
</code></pre>
<p>It is basically equivalent of copying the style and pasting it in the main style sheet, which happens by itself when we compile the main style sheet.</p>
<h2 id="extension--inheritance">Extension / Inheritance</h2>
<p>When there are occurrences where two css classes share almost the same styles but with some minimal variations, to ease job in repeating the code extension helps us in extending an existing class and change the required properties in the extended class.<br>
<strong>.scss</strong>:</p>
<pre><code>.text{
	font-color: blue;
	font-stle : italic;
}
.heading-text{
	@extend .text;
	font-size : 10px;
}
.body-text{
	@extend .text;
	font-size : 12px;
}
</code></pre>
<p>In case the property that is edited already exists in the class which is being extended, then it gets updated in the extending class.</p>
<pre><code>.text{
	font-color: blue;
	font-stle : italic;
	font-size : 5px;
}
.heading-text{
	@extend .text;
	font-size : 10px; 
}
</code></pre>
<p>The <code>font-size</code> property in the heading-text gets updated to <code>10px</code>.<br>
The tags that use <code>.text</code> class will have font size of <code>5px</code> and the ones that use <code>heading-text</code> will have size <code>10px</code>.</p>
<h2 id="mixin">Mixin</h2>
<p>Mixins are pretty much like functions, cases where in two classes have the same style properties but with different values, we can’t use <code>extend</code>, thus <code>mixin</code>.</p>
<pre><code>@mixin  buttonDesign($radius,$color){
	border-radius: $radius;
	color: $color;
}
.button1{
	@include  buttonDesign(5px,blue );
	margin: 5px;
	padding: 5px;
}
.button2{
	@include  buttonDesign(3px, green );
	margin: 2px;
	padding: 5px;
}
</code></pre>
<p>Now, <code>button1</code> and <code>button2</code> classes have the same properties defines in <code>buttonDesign</code> with different values included  in them, we don’t need to repeat the code to achieve that, Mixin does that for us.<br>
<code>@mixin</code> is used to define set of properties with variable values as parameters and <code>@include mixinName(parameters)</code> will include them in the class where it is called.</p>
<h2 id="operations">Operations</h2>
<p>SCSS supports a arithmetic operations.</p>
<h4 id="example-1">Example:</h4>
<pre><code>$button-color : #00ff00;
$button-padding : 5px;
.button{
	color : $button-color + 5;
	padding : $button-padding*2;
}
</code></pre>
<p>Here multiplying <code>$button-color</code> by <code>2</code> will brighten the color and adding <code>$button-padding</code> by <code>5</code> will increase the the padding size by <code>5px</code>.</p>
<h4 id="note">Note:</h4>
<p>We don’t need to specify <code>px</code> after the  number we add or multiply, SCSS compiler will take care of that.<br>
i.e <code>$button-color + 5px</code> is equivalent of <code>$button-color + 5</code>.</p>

