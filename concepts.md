# Box Model

Internet explorer displayed an element's **padding** and **border** as part of element's overall **width** and **height**. Example if we set an element with a width of 200 px and a padding of 20 px, instead of adding to original width, padding would cut into original width. Result would be IE would display content area width as 160 px (200 - 20 on right - 20 on left).

The **content-box** property would use default browser behavior i.e padding and border values will be added to specified width.

```css
article{
    box-sizing: content-box;
    width: 200px;
    padding: 20px;
    border: 1px solid #000;
}
```

Here article width would be 242px.

The **border-box**  property will calculate width including content, padding and border but not margin. 

```css
article{
    box-sizing: border-box;
    width: 200px;
    padding: 20px;
    border: 1px solid #000;
}
```

Here article width would be 158px;

If we set a height of 500 px on element, and text inside of box stretches beyond box boundaries, we need to use overflow property:

```css
article{
    overflow: visible; //Default Setting and allows content to flow over
    overflow: hidden;  //Hide any content that flows outside the box
    overflow: scroll;  //Give the box its own scrollbar
    overflow: auto;	   //detects size of content and creates a scrollbar if necessary
}
```



# Layout Types

4 types of layout:

* Fixed
* Elastic
* Fluid
* Min/Max



Same Examples are valid for height also;

```html
<div class="fixed-size">
    Fixed (px)
</div>

<div class="Elastix-size">
    Elastic (em)
</div>

<div class="fluid-size">
    Fluid (%)
</div>

<div class="threshold-size">
    Threshold (min and max)
</div>
```

```css
body{
    font-size: 200%;
}

div{
    background: aqua;
    padding: 20px;
    margin: 10px;
    font-size: 1em;
}

.fixed-size{
    width: 200px;
}

.elastic-size{
    width: 12.5em;   /*200px/16px*/
    /*Width varies with font size*/
}

.fluid-size{
    width: 70%;
}

.threshold-size{
    min-width: 500px;
    max-width: 900px;
}
```



# Display

Certain elements by default cover block area and others are side by side.

```css
div{
    display: inline; /*appears side by side. Doesnt let width or top and bottom margins*/
    display: block; /* displays one above the other */
    display: inline-block; /*Displays side by side. Allows top and bottom margins and width to be specified*/
}
```

Also for block level elements, top and bottom margins doesn't combine.

For inline elements, left and right margins combine.



# Float

Allows pulling elements left or right. Doesn't impact elements to be floated but elements that come after it. For that we need to use clear property and set it to either left, right or both.

Strategy is to make elements block and float them left or right. 

```html
<p>
    Contrary to popular belief, Lorem Ipsum is not simply random text. It has roots in a piece of classical Latin literature from 45 BC, making it over 2000 years old. Richard McClintock, a Latin professor at Hampden-Sydney College in Virginia, looked up one of the more obscure Latin words, consectetur, from a Lorem Ipsum passage, and going through the cites of the word in classical literature, discovered the undoubtable source. Lorem Ipsum comes from sections 1.10.32 and 1.10.33 of "de Finibus Bonorum et Malorum" (The Extremes of Good and Evil) by Cicero, written in 45 BC. This book is a treatise on the theory of ethics, very popular during the Renaissance. The first line of Lorem Ipsum.
</p>

<img src="http://placekitten.com/200/230">

<p>
    Contrary to popular belief, Lorem Ipsum is not simply random text. It has roots in a piece of classical Latin literature from 45 BC, making it over 2000 years old. Richard McClintock, a Latin professor at Hampden-Sydney College in Virginia, looked up one of the more obscure Latin words, consectetur, from a Lorem Ipsum passage, and going through the cites of the word in classical literature, discovered the undoubtable source. Lorem Ipsum comes from sections 1.10.32 and 1.10.33 of "de Finibus Bonorum et Malorum" (The Extremes of Good and Evil) by Cicero, written in 45 BC. This book is a treatise on the theory of ethics, very popular during the Renaissance. The first line of Lorem Ipsum, "Lore
</p>

<p class="fall-below">
    Contrary to popular belief, Lorem Ipsum is not simply random text. It has roots in a piece of classical Latin literature from 45 BC, making it over 2000 years old. Richard McClintock, a Latin professor at Hampden-Sydney College in Virginia, looked up one of the more obscure Latin words, consectetur, from a Lorem Ipsum passage, and going through the cites of the word in classical literature, discovered the undoubtable source. Lorem Ipsum comes from sections 1.10.32 and 1.10.33 of "de Finibus Bonorum et Malorum" (The Extremes of Good and Evil) by Cicero, written in 45 BC. This book is a treatise on the theory of ethics, very popular during the Renaissance. The first line of Lorem Ipsum, "Lore
</p>
```

```css
img{
    display: block; /* inline elements can't have margin from top or bottom*/
    float: left;
    margin: 0 20px 10px 0;
}

.fall-below{
    clear: both;
}
```



# Clearfix (Bug of parent of floated element)

```html
<section id="jazz" class="clearfix">
	<article>Miles D</article>
    <article>BB King</article>
</section>

<section id="rock" class="clearfix">
	<article>AC/DC</article>
    <article>Black Sabbath</article>
</section>
```

```css
article{
	width: 100px;
    height: 100px;
    padding: 20px;
    margin: 10px;
}

#jazz article{
    float: left;
    background: aqua;
}

#rock article{
    float: right;
    background: lime;
}

.clearfix:after{
    content: ".";
    display: block;
    clear: both;
    visibility: hidden;
    height: 0;
    line-height: 0;
}
```



# Centering

A simple website using above concepts:

```html
<div class="wrapper">
    <header>
    	<h1>Music Store</h1>
    </header>
    <section id="new">
    	<h2>New Items</h2>
    </section>
    <section id="music">
    	<h2>Music</h2>
    </section>
    <section id="clothing">
    	<h2>Clothing</h2>
    </section>
    <footer>
    	&copy; 2020 Music Store
    </footer>
</div>
```

```css
.wrapper{
    margin: 0 auto; /* Centering */
    width: 600px;
    background: #ccc;
}

header, footer{
    padding: 10px;
    background: #000;
    color: #fff;
}

section{
    padding: 20px;
}

#new{
    float: left;
    background: red;
    width: 33.3333; 
}

#music{
    float: left;
    background: yellow;
    width: 33.3333;
}

#clothing{
    float: left;
    background: green;
    width: 33.3333;/*Adds to 99.99% which suits only when no padding is specified for any element. If we specify padding for section, it adds to 6% more and this coloum falls. Solution is below. It will fail if we specify margin also suppose say to section as below code doesn't cover for margin. Then solution is subtract from each of width value, the equivalent margin value. */
}

*{
    -webkit-box-sizing: border-box;
    -moz-box-sizing: border-box;
    box-sizing: border-box; /*IE box model*/
}
```

