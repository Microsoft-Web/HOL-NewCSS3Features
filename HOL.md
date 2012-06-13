#New CSS3 Features#

## Overview ##

The Cascading Style Sheets Level 3 standard, commonly known as CSS3, is a vast improvement over the previous version of the standard. CSS3 defines new CSS properties and selectors, adds advanced layouts and visual effects, supports different types of devices and platforms, improves accessibility, and greatly extends the previously existing functionality. 
Internet Explorer 10 is more standards-compliant than ever and supports most of the CSS3 specifications. The sheer size of the CSS3 standard makes it difficult to demonstrate all the new features, so this lab will only present Internet Explorer 10’s support for a selection of these features. In particular, this lab focuses on fonts, column layout, and a few advanced selectors and visual effects.

<a name="Objectives" />
### Objectives ###

In this hands on lab, you will learn how to:

- Declare and use custom web fonts

- Lay out text in newspaper-style columns

- Use new CSS3 selectors

- Apply advanced visual effects to your elements

<a name="Prerequisites" />
### Prerequisites ###

- [Internet Explorer 10](http://windows.microsoft.com/en-US/internet-explorer/products/ie/home)

- An HTML editor of your choice

- Prior knowledge of CSS

<a name="Exercises" />
## Exercises ##

This hands on lab includes the following exercises:

1. [Exercise 1: Using Web Fonts](#Exercise1)

1. [Exercise 2: Using CSS3 Columns](#Exercise2)

1. [Exercise 3: Using CSS3 Selectors](#Exercise3)

1. [Exercise 4: Using New CSS3 Properties](#Exercise4)

1. [Exercise 5: Applying Visual Effects](#Exercise5)

 
Estimated time to complete this lab: **45-60 minutes**.

<a name="Exercise1" />
### Exercise 1: Using Web Fonts ###

The starting point for this exercise is the solution in the lab installation folder under the **Source\Begin** folder. As you progress through the exercise, you will gradually improve the design and layout of web pages in the application. 
Selecting the right fonts can greatly improve the design and usability of your application. The right fonts will contribute to the atmosphere conveyed by your application, make your site more accessible, and, most importantly, make it easier for your site’s visitors to read the content. The CSS standard has long provided support for using different font types and styles, but this support was limited to fonts that were built in to the browsers or already installed on the operating system. Because each operating system has a different set of installed fonts, the standard let designers specify multiple options, allowing browsers to choose the best font available. A designer could specify a number of preferred fonts, one for each operating system or browser as necessary. If the browser cannot find one of the fonts, it falls back on another font.
In addition, every modern browser supported five basic fonts, known as **generic font families**. These families (**serif**, **sans-serif**, **cursive**, **fantasy**, and **monospace**) do not map to actual fonts. Rather, they represent very broad categories that include most fonts. When a style sheet specifies only fonts that the browser does not recognize, the browser relies on the **generic font family** to describe a suitable alternative that preserves the basic characteristics of the preferred (missing) font. It is ultimately up to the browser to decide which font to use for each of the generic families.
Although very useful, these mechanisms are inherently imprecise. Designers have no control over the generic font families provided by the various browsers, and no control over the set of installed fonts on any given operating system or browser. There is no guarantee that the site will look the way it should on any given platform. Downloadable fonts solve this problem by letting developers and designers declare custom web fonts that modern browsers can download and display. With the advent of CSS3, designers can use almost any available web font (or even design their own), and be certain that visitors browsing with any modern browser will have the intended experience. The **@font-face** rule used to specify downloadable fonts also integrates seamlessly with the existing mechanism so browsers that do not support CSS3 or cannot download the font can still fall back on platform- or browser-specific fonts.
Internet Explorer has supported downloadable fonts since Internet Explorer 4, but its support was limited to Embedded Open Type (EOT) fonts. The EOT format is a proprietary format created by Microsoft that was not adopted by other browsers. CSS3 instead adds support for the Web Open Font Format (WOFF). Internet Explorer fully supports WOFF as well as other widely available downloadable font formats. Internet Explorer 10 also supports additional font features added in CSS3.

In this exercise, you will learn:

* How to declare a downloadable web font and use it in your application
* How to merge multiple web fonts

<a name="Ex1Task1" />
#### Task 1 - Declaring and Using a Web Font ####

This task shows how to create a **@font-face** rule to declare a web font and how to apply the web font to your application.

1. Copy the **Fonts** folder from the **Assets** folder and paste it in the **TheFacePlace** project folder (as a sibling of the **CSS** folder). The browser will use these fonts to render text.

	>**Note:** If you are using **Visual Studio**, you can copy the **Assets** folder and paste it onto the **TheFacePlace** project node in **Solution Explorer**. You can also use the mouse to drag the **Fonts** folder and drop it onto the **TheFacePlace** project node in **Solution Explorer**.

1. Open the **CSS\Base.css** file and create a new font face declaration at the top of the file. The **font-family** property is the new name assigned to the imported font. The **src** property is the location from which to download the custom font and the font’s format.
 	
	<!-- mark:1-5 -->
 	````CSS
	@font-face
	{
	    font-family: YanoneKaffeesatz;
	    src: url('../Fonts/YanoneKaffeesatz-Regular.woff') format('woff');
	}
	````

	>**Note:** This declaration is sufficient for Internet Explorer 10, but may not be supported by earlier versions of Internet Explorer or by other browsers.

1. Modify the font face declaration to support the legacy EOT format recognized by previous versions of Internet Explorer and to support formats recognized by other modern browsers:
 	
	<!-- mark:5-8 -->
 	````CSS
	@font-face
	{
	    font-family: YanoneKaffeesatz;
	    src: url('../Fonts/YanoneKaffeesatz-Regular.eot');
	    src: local("☺"),
	         url('../Fonts/YanoneKaffeesatz-Regular.woff') format('woff'),
	         url('../Fonts/YanoneKaffeesatz-Regular.ttf') format('truetype'),
	         url('../Fonts/YanoneKaffeesatz-Regular.svg') format('svg');	
	}
	````

	Internet Explorer 10 will use the WOFF font file, and earlier versions will use the EOT font file in the first **src** property. Other modern browsers will use the first specified format they recognize in the last (in this case, the second) **src** property.

1. Find the selector for the **body** tag and add a style declaration that references the custom **YanoneKaffeesatz** font face that was declared with the **@font-face** rule. Make sure to specify at least one fallback font, and always specify one of the generic font families, in case the browser is unable to download or display the YanoneKaffeesatz font.
 	
	<!-- mark:4 -->
 	````CSS
	body
	{
	    /* ... */
	    font-family: YanoneKaffeesatz, sans-serif;
	}
	````

<a name="Ex1Task2" />
#### Task 2 - Merging Multiple Web Fonts ####

The **@font-face** rule can be used to merge multiple font files into one font with multiple styles. For example, one file might contain just the regular style and another file might contain the bold style. When they are merged correctly, the browser will use the correct font file when either style is requested, without having to specify which one is being used in this instance. This task shows how to merge multiple web font files into one web font.

1. Add another **@font-face** rule to download the bold style font file for the same font. Add the **font-weight** property to instruct the browser to use this font file wherever text is supposed to be bold.
 	
	<!-- mark:1-10 -->
 	````CSS
	@font-face
	{
	    font-family: YanoneKaffeesatz;
	    font-weight: bold;
	    src: url('../Fonts/YanoneKaffeesatz-Bold.eot');
	    src: local("☺"),
	         url('../Fonts/YanoneKaffeesatz-Bold.woff') format('woff'),
	         url('../Fonts/YanoneKaffeesatz-Bold.ttf') format('truetype'),
	         url('../Fonts/YanoneKaffeesatz-Bold.svg') format('svg');
	}
	````

<a name="Exercise2" />
### Exercise 2: Using CSS3 Columns ###

Prior to CSS3, web developers and designers had to resort to all kinds of tricks to create the layouts they wanted for their sites. CSS3 provides a number of new layout mechanisms to support these requirements and make it easy to lay pages out in different ways. One of the most common layouts is CSS3 Columns, which lays text out in newspaper-style columns. Internet Explorer fully supports CSS3 Columns.

In this exercise, you will learn:

* How to apply column layout to your text

<a name="Ex2Task1" />
#### Task 1 - Applying Column Layout to Text ####

1.	In the **Base.css** file in the **CSS** folder, find the selector for **section** elements that are contained in **article** elements. The selector reads as **article section**. This selector applies to the main text content on the **Default.htm** page. Add the **column-count** property to the end of the block to specify that the text should be rendered using a columnar layout:

	<!-- mark:5-6 -->
	````CSS
	article section
	{
		/* ... */
		-moz-column-count: 3;
		-webkit-column-count: 3;
		column-count: 3;
	} 
	````

1.	Fine-tune the column layout by adding the **column-gap** property, which specifies the amount of horizontal space to put between the columns:
	
	<!-- mark:7-9 -->
	````CSS
	article section
	{
		/* ... */
		-moz-column-count: 3;
		-webkit-column-count: 3;
		column-count: 3;
		-moz-column-gap: 28px;
		-webkit-column-gap: 28px;
		column-gap: 28px;
	}

<a name="Exercise3" />
### Exercise 3: Using CSS3 Selectors ###

The primary purpose of CSS is to separate the style from the content. Selectors are crucial for this purpose because they allow us to apply styles to the HTML document without modifying the HTML itself. CSS3 adds a number of new selectors and broadens the reach of existing selectors to make it easier to select elements and element states that were either difficult or impossible to select with previous versions of CSS.

In this exercise, you will learn:

* How to use positional pseudo-class selectors
* How to use the :not pseudo-class selector

<a name="Ex3Task1" />
#### Task 1 - Using Positional Pseudo-Class Selectors ####

CSS3 adds many new pseudo-classes to match elements in ways that were not possible or easily accomplished in earlier versions. Many of these match elements based on their positions relative to their siblings. This task shows how to use just a couple of the positional pseudo-classes.

1.	Open the **NewGame.htm** file and find the **section** element with the **id** attribute **chooseImageSection**. Observe that the element contains four child elements: two **p** elements followed by two **input** elements. We would like to place some vertical space between the second **p** element and the first **input** element to better differentiate between the two options, without affecting the other siblings. In previous versions of CSS, there was no easy, explicit way to select the correct element. CSS3 provides a number of pseudo-classes that let you select the correct element precisely.
Open the **Base.css** file in the **CSS** folder and find the style block with the selector **#chooseImageSection**. Immediately after it, add a new style block that selects the last **p** element and adds a lower margin:
	
	<!-- mark:1-4 -->
	````CSS
	#chooseImageSection p:nth-of-type(2)
	{
		 margin-bottom: 15px;
	}
	````
Note the pseudo-class **:last-of-type**. From the descendants of the **chooseImageSection** element, every **p** element that is the last **p** element relative to its immediate siblings will be selected. In this case, only the second **p** element will be selected.

1.	Open the Default.htm file, find the **div** element with the id **InstructionsImages**. Observe that the element contains three child **img** elements. We would like to add some space to the left and right of the middle image. Open the **CSS\Base.css** file and find the block whose selector is **#InstructionsImages**. Add another selector immediately after it to add left and right margins only to the middle **img**:

	<!-- mark:1-5 -->
	````CSS
	#InstructionsImages > img:nth-child(2)
	{
		 margin-left: 35px;
		 margin-right: 35px;
	}
	````
The selector **#InstructionsImages > img:nth-child(2)** selects the second **img** element that is also a child of the element with the **InstructionsImages** id.

<a name="Ex3Task2" />
#### Task 2 - Using the :not Pseudo-Class Selector ####

CSS3 adds a number of additional pseudo-classes: the **:enabled** and **:disabled** pseudo-classes match enabled and disabled elements; the **:checked** pseudo-class matches elements (like the checkbox element) that are in a _checked_ state; and the **:empty** pseudo-class matches elements that have no content.
However, possibly the most interesting pseudo-class is the **:not()** pseudo-class. This pseudo-class can appear anywhere in the selector, and receives a parameter that is itself a simple selector such as an id, tag, or class selector. The pseudo-class will match any element that does not match the selector in the parenthesis. This task shows how to use the **:not** pseudo-class.

1.	The **OpenGame.htm** page shows thumbnails of stored images. When the mouse hovers over a thumbnail, that thumbnail is enlarged a bit to emphasize that image. However, we would like the remaining images to become a bit smaller and fade out. Earlier versions of CSS could not do this because they could only match elements in a specific state. It is possible and fairly simple to do this using JavaScript, but not very fast. More importantly, this is a presentational concern that should not require JavaScript.

	CSS3 therefore makes it possible to select these elements using the **:not()** pseudo-class. Open the **OpenView.css** file in the **CSS** folder and find the selector **.selection-mode .thumbnail.emphasis**. The **emphasis** class denotes the thumbnail that is currently under the mouse. To fade out the other thumbnails, insert the following style block just before the current block:

	<!-- mark:1-4 -->
	````CSS
	.selection-mode .thumbnail:not(.emphasis)
	{
		 opacity: 0.3;
	}
	````
	
	This selector matches elements with the **thumbnail** class that do _not_ have the **emphasis** class. The **opacity** property causes the thumbnails to appear faded out.

1.	Add another style block immediately after the previous one to make the unselected **img** elements (those that are descendants of the thumbnails) a bit smaller:

	<!-- mark:1-7 -->
	````CSS
	.selection-mode .thumbnail:not(.emphasis) img
	{
		 width: 74px;
		 height: 74px;
		 left: 13px;
		 top: 13px;
	}
	````

<a name="Exercise4" />
### Exercise 4: Using New CSS3 Properties ###

CSS3 adds many new styles intended to solve common problems that were very difficult or impossible to solve under previous versions of CSS. This exercise shows how to solve some of the most common problems using CSS3.

In this exercise, you will learn:

* How to add rounded corners to elements
* How to add shadows to elements

<a name="Ex4Task1" />
#### Task 1 - Adding Rounded Corners to Elements ####

HTML elements are rendered in boxes, with ordinary, pointed, 90-degree angles. However, these right angles are not usually very elegant or visually appealing. CSS3 features a set of properties to add support for rounded corners, one property for each corner: **border-top-left-radius**, **border-top-right-radius**, **border-bottom-right-radius**, **border-bottom-left-radius**. CSS3 also adds a shorthand property **border-radius** that can be used to set all four corners with one style declaration. This task shows how to use the **border-radius** property.

1.	Open the **OpenView.css** file in the **CSS** folder and find the **.game > .thumbnail** selector. Add the **border-radius** property to the selector block:

	<!-- mark:4 -->
	````CSS
	.game > .thumbnail
	{
		/* ... */
		border-radius: 5px;
	}
	````
	
	This property applies a five-pixel radius to each of the corners of the thumbnail elements on the Open Game page.

	> **Note:** Although this task applies the same radius to all the corners, the **border-radius** property can also be used to set a different radius for each corner.

<a name="Ex4Task2" />
#### Task 2 - Adding Box Shadows to Elements ####

Adding shadows to elements was a challenge prior to CSS3 and required a combination of CSS and images, and sometimes a bit of JavaScript as well, to pull off. CSS3 adds the new property **box-shadow** which lets designers and developers apply different kinds of shadows to elements. Shadows can be offset to any side or corner and can appear inside or outside the element. They can also be blurred to give smoother edges and multiple shadows can be combined. This task shows how to use the **box-shadow** property:

1.	Find the **.game > .thumbnail:active** selector block and add the **box-shadow** property to add a glow effect to the thumbnail when it is in the **active** state, which occurs while the user clicks the element but before the mouse button is released.

	<!-- mark:4 -->
	````CSS
	.game > .thumbnail:active
	{
		/* ... */
		box-shadow: 0px 0px 10px white;
	}
	````

	The first and second values determine the horizontal and vertical offsets, respectively. In this case, the shadow is not offset (the offset is zero pixels), so the shadow surrounds the element on all sides. The third value, the **blur**, specifies the width of the shadow. The blur is set to ten pixels, so the shadow extends ten pixels in every direction. The last value specifies the shadow’s color. A white color on a black background creates the glow effect.

1.	The selector **.game > .thumbnail.selected** should appear immediately after the **.game > .thumbnail:active** selector modified in the previous step. This selector applies after the thumbnail is clicked by the user. To show the user that the element is selected, a white glow with a green tinge is added using multiple **box-shadow** values stringed together, as follows:

	<!-- mark:4 -->
	````CSS
	.game > .thumbnail.selected
	{
		/* ... */
		box-shadow: 0px 0px 7px white, 0px 0px 10px green;
	}
	````

<a name="Exercise5" />
### Exercise 5: Applying Visual Effects ###

One of the greatest improvements in CSS3, fully supported by Internet Explorer 10, is in its support for advanced visual effects, including gradients, transforms, and animations. Internet Explorer 10 uses hardware acceleration to make the animations smoother.

In this exercise, you will learn:

* How to use linear gradients to create more appealing backgrounds
* How to apply 2D and 3D transformations to your elements
* How to create animated transitions
* How to create advanced animations

<a name="Ex5Task1" />
#### Task 1 - Using Linear Gradients to Create Appealing Backgrounds ####

Gradients are often used to make web sites more attractive, especially when used as backgrounds. However, prior to CSS3, the only way to add gradients was to make use of image files containing gradients. Such image files require additional bandwidth and cannot be easily resized without affecting their quality, making them difficult to use on adaptive sites. CSS3 therefore introduced support for gradients that do not suffer these disadvantages. This task shows how to use linear gradients.

1. In the **OpenView.css** file in the **CSS** folder, find the **#newGame > .thumbnail** selector. This selector matches the “**New Game**” thumbnail. Add the **background-image** property and set its value to a linear gradient.

	<!-- mark:5-8 -->
	````CSS
	#newGame > .thumbnail
	{
		 /* ... */
		 background-image: -ms-linear-gradient(bottom, #d7dd7e 1%, #dce638 99%);
		 background-image: -moz-linear-gradient(bottom, #d7dd7e 1%, #dce638 99%);
		 background-image: -webkit-linear-gradient(bottom, #d7dd7e 1%, #dce638 99%);
		 background-image: -o-linear-gradient(bottom, #d7dd7e 1%, #dce638 99%);
		 background-image: linear-gradient(bottom, #d7dd7e 1%, #dce638 99%);
	}
	````

	The first value, “**bottom,**” in the **linear-gradient()** function specifies that the gradient flows from the bottom of the element to its top. The remaining arguments are color stops, that indicate the colors that constitute the gradient and the positions at which they are located. The first color stop is close to the bottom (at the 1% mark) and uses the color **#d7dd7e**. The second color stop is close to the top (at the 99% mark) and uses the color **#dce638**. Any number of color stops can be specified at any number of points along the gradient.

	> **Note:** 	Gradients represent _replaced content_ just like images. Replaced content refers to elements that are rendered in special ways, such as images, video, and so forth. The browser creates the desired gradient images on the fly. Gradients can be used anywhere images can be specified in CSS3 and behave in the same way. For example, when a gradient is specified as a background image, it will also be affected by other properties affecting the background image. 
	CSS3 actually provides a slew of new ways to specify images in CSS, including the **image()** function that can be used to specify image fragments, solid color images, and image fallbacks. There are also multiple types of gradients, which can be specified with the **linear-gradient** function used in this task as well as the **radial-gradient**, **linear-repeating-gradient**, and **radial-repeating-gradient** functions.

<a name="Ex5Task2" />
#### Task 2 - Transforming Elements ####

Internet Explorer 10 fully supports two- and three-dimensional transformations, including rotation, scaling, translation, skewing, and more advanced matrix transformations. This task shows how to use the CSS3 Transforms module.

1. Open the **Base.css** file in the **CSS** folder and find the selector **.zoomInImg**. The **zoomInImg** class is applied to the asset images when the mouse hovers over them. To apply the zoom-in effect, add the **scale** transform to the **.zoomInImg** style block.
	
	<!-- mark:3-7 -->
	````CSS
	.zoomInImg
	{
		-ms-transform: scale(1.5, 1.5);
		-moz-transform: scale(1.5, 1.5);
		-webkit-transform: scale(1.5, 1.5);
		-o-transform: scale(1.5, 1.5);
		transform: scale(1.5, 1.5);
	}
	````
The **scale** function accepts two arguments that represent the scale multipliers for the x and y axes, respectively. The scale factor of 1.5 enlarges the image by 50%. 

1.	Find the selector for the **.rotateRight** class. Add the **rotateY** transform to the selector block.

	<!-- mark:3-7 -->
	````CSS
	.rotateRight
	{
		-ms-transform: rotateY(180deg);
		-moz-transform: rotateY(180deg);
		-webkit-transform: rotateY(180deg);
		-o-transform: rotateY(180deg);
		transform: rotateY(180deg);
	}
	````

	The **rotateY** transform rotates the element horizontally, around the y-axis. Rotating the element by 180 degrees creates the effect of flipping the element onto its back. This class is applied to the trash and magnifying glass icons on the **NewGame.htm** page when they are clicked.

1.	Find the selector for the **.iconsWrapper** class and add a **perspective** transform, a 3D transformation that changes the apparent distance from which the transform is viewed. This is particularly useful with animations, as it affects the apparent viewing angle of the animated transformation and improves the visual effect.

	<!-- mark:4-8 -->
	````CSS
	.iconsWrapper
	{
		/* ... */
		-ms-transform: perspective(50px);
		-moz-transform: perspective(50px);
		-webkit-transform: perspective(50px);
		-o-transform: perspective(50px);
		transform: perspective(50px);
	}
	````

<a name="Ex5Task3" />
#### Task 3- Creating Transitions ####

The ability to create animations is one the most intriguing features of the CSS3 specifications. Support for animation is provided by two separate CSS3 modules: CSS Transitions and CSS Animations. Each module provides a different approach. Transitions are simple and integrate very easily with existing CSS declarations. Animations are more advanced and support complex animations and finer-grained control.
Creating a transition takes two steps. First, the CSS **transition** property is used in a style block that matches the target elements in their initial state. The **transition** property specifies the CSS properties that will be animated. Then the final values of these properties, the values as they will appear at the end of the animation, are defined in CSS style blocks whose selectors match the modified states of the target elements. The selectors need only match the same elements for the transition to work: they can match a pseudo-class-specific state such as **:hover** or **:active**, or an unrelated class that is added to the element using JavaScript.
For example, if the background color of an element whose class is **animate-me** should be changed gradually (using animation) from blue to red when the mouse hovers over the element, two selector blocks are declared. The first defines the initial background color as being blue and specifies - using the **transition** property - that any changes to the **background-color** property should be animated automatically by the browser, as follows:
	
````CSS
.animate-me
{
	background-color: blue;
	transition: background-color 0.5s;
}
````

The transition property specifies that, any time the element’s background color changes (that is, any time it is overridden by another matching selector block), it should take half a second (0.5s) to perform the transition. To create the animation, simply add the following style declaration:

````CSS
.animate-me:hover
{
	background-color: red;
}
````

Every time the mouse hovers the **.animate-me** element, instead of immediately changing the background color to red, it will animate the change and gradually change the color over the course of the specified interval. Without the **transition** property, the background color would change immediately. Adding the **transition** property animates the property change. This task shows how to create CSS transitions.

1.	Open the file **Base.css** in the **CSS** folder and find the selector **nav ul#menuAssets li**. This selector matches the items on the top menu of the NewGame.htm page (i.e., the menu items that contain the text “EYES,” “NOSE,” and so forth). The style block defined by this selector sets the color to a shade of gray (**#2A2A2A**). The selector of the next style block matches the same elements when they are in the **:hover** state and sets the color to a shade of blue (**#00A2FF**). Currently, when the mouse hovers over the menu item, the browser changes the element’s color _immediately_ from gray to blue.

	To make the change more gradually, add the following style declarations to the **nav ul#menuAssets li**.
	
	<!-- mark:4-8 -->
	````CSS
	nav ul#menuAssets li
	{
		/* ... */
		-ms-transition: color 0.5s;
		-moz-transition: color 0.5s;
		-webkit-transition: color 0.5s;
		-o-transition: color 0.5s;
		transition: color 0.5s;
	}
	````

	This tells the browser that any change to the **color** property, such as the change that occurs when the element is in the **hover** state, should occur gradually and take 0.5s from beginning to end. When the state reverts (for example, when the mouse no longer hovers over the element), the color will change back gradually as well.

1. Transitions can also apply to classes that match the same element at different times. Find the selector for the **.page-container** class and note that the value of the **top** property is 0px. When the user clicks on the help icon (the question mark at the top right corner of the page), the contents of the instructions page are shown using JavaScript. In particular, the code appends the **instructions-page** class to the same element described by the **page-container** class. The selector **.instructions-page, .save-as-page** follows the **.page-container** selector and changes the **top** property value to **850px**. But the change is very abrupt. Add the following styles to make the transition smooth:

	<!-- mark:4-8 -->
	````CSS
	.page-container
	{
		/* ... */
		-ms-transition: top 1s;
		-moz-transition: top 1s;
		-webkit-transition: top 1s;
		-o-transition: top 1s;
		transition: top 1s;
	}
	````

	When the **top** is changed, the change is performed gradually over the course of a full second.

1.	If more than one property changes, the **all** keyword can be used to specify that every property change should be animated. A number of different changes are applied to the asset images, and we’d like to animate all of them. Find the **.assets img** selector and add a transition with the **all** keyword:

	<!-- mark:4-8 -->
	````CSS
	.assets img
	{
		/* ... */
		-ms-transition: all 0.5s;
		-moz-transition: all 0.5s;
		-webkit-transition: all 0.5s;
		-o-transition: all 0.5s;
		transition: all 0.5s;
	}
	````

	The following style blocks all apply to the same elements, so every change will be animated.

1. We can also select a set of properties to animate together, instead of animating all the changes. This can help improve performance and avoid animating properties that shouldn’t be animated. Open the **OpenView.css** file in the CSS folder and find the style block for **.game > .thumbnail > img**. When the mouse hovers over an image, the image is enlarged by changing only its **left**, **top**, **width** and **height** properties in a subsequent style block. Add the following styles to the style block:

	<!-- mark:4-8 -->
	````CSS
	.game > .thumbnail > img
	{
		/* ... */
		-ms-transition: width 0.3s linear 0.2s, height 0.3s linear 0.2s, left 0.3s linear 0.2s, top 0.3s linear 0.2s;
		-moz-transition: width 0.3s linear 0.2s, height 0.3s linear 0.2s, left 0.3s linear 0.2s, top 0.3s linear 0.2s;
		-webkit-transition: width 0.3s linear 0.2s, height 0.3s linear 0.2s, left 0.3s linear 0.2s, top 0.3s linear 0.2s;
		-o-transition: width 0.3s linear 0.2s, height 0.3s linear 0.2s, left 0.3s linear 0.2s, top 0.3s linear 0.2s;
		transition: width 0.3s linear 0.2s, height 0.3s linear 0.2s, left 0.3s linear 0.2s, top 0.3s linear 0.2s;
	}
	````

	The transition property accepts multiple values separated by commas (,). In addition to the property and the animation duration, these values also specify an easing function that determines how fast the animation proceeds at each stage, and a delay that determines how long to wait before starting the animation. For example, the first value specifies that the **width** property’s animation should last 0.3 seconds, that the animation should proceed at a constant (“linear”) rate, and that it should start 0.2 seconds from when the animation is triggered. The delay prevents the images from enlarging and contracting too quickly. The other values are identical, except for the selected properties.

1. Combining multiple transitions that have different values in one **transition** property can often create better animations. Find the **.game > .thumbnail** selector and add a transition for the **opacity** and **border-color** properties. Since the **opacity** property should be animated before the **border-color** is animated, they are given different delays.

	<!-- mark:4-8 -->
	````CSS
	.game > .thumbnail
	{
		/* ... */
		-ms-transition: opacity 0.3s linear 0.2s, border-color 0.5s linear;
		-moz-transition: opacity 0.3s linear 0.2s, border-color 0.5s linear;
		-webkit-transition: opacity 0.3s linear 0.2s, border-color 0.5s linear;
		-o-transition: opacity 0.3s linear 0.2s, border-color 0.5s linear;
		transition: opacity 0.3s linear 0.2s, border-color 0.5s linear;
	}
	````

<a name="Ex5Task4" />
#### Task 4 - Creating Animations ####

The second kind of animation provided by CSS3 and defined in the CSS Animations module provides keyframe-based animations. A keyframe specifies what should happen at a specific moment during the animation. 
Each module provides a different approach. Transitions are simple and integrate very easily with existing CSS declarations, while animations are more advanced and support complex animations and finer-grained control. This task shows how to create a CSS animation.

1. Open the file **Base.css** in the **CSS** folder and find the **img-container:hover** selector. This style block applies when the mouse hovers over the help icon that appears at the top right of the page. Instead of a simple transition that translates (or “slides”) the element upwards, we’ll create a slightly more complex animation that pushes it down a bit and then back up. First add the following styles to the style block:

	<!-- mark:4-18 -->
	````CSS
	.img-container:hover
	{
		/* ... */
		-ms-animation-name: emphasis;
		-ms-animation-duration: 3s;
		-ms-animation-iteration-count: 1;
		-moz-animation-name: emphasis;
		-moz-animation-duration: 3s;
		-moz-animation-iteration-count: 1;
		-webkit-animation-name: emphasis;
		-webkit-animation-duration: 3s;
		-webkit-animation-iteration-count: 1;
		-o-animation-name: emphasis;
		-o-animation-duration: 3s;
		-o-animation-iteration-count: 1;
		animation-name: emphasis;
		animation-duration: 3s;
		animation-iteration-count: 1;
	}
	````

	This code contains three CSS properties that affect the animation: **animation-name**, **animation-duration**, and **animation-iteration-count**. The value of the **animation-name** property is the name of the animation sequence that you will create in the next step. The **animation-duration** property determines the amount of time it takes for the animation to run from when it is triggered to when it ends. And the **animation-iteration-count** determines the number of times the iteration should run every time it is triggered. There are a number of other properties that can further control the way the animation runs, but these three are the most common.

1. An animation sequence is created using the **@keyframes** rule, whose content determines the stages, or keyframes, of the animation. To create the animation sequence, add the following code to the end of the **Base.css** file:

	<!-- mark:1-35 -->
	````CSS
	@-ms-keyframes emphasis
	{
		from
		{
			top: 0px;
			animation-timing-function: ease-out;
		}
		25%
		{
			top: 5px;
			animation-timing-function: ease-in;
		}
		to
		{
			top: -22px;
		}
	}

	@keyframes emphasis
	{
		from
		{
			top: 0px;
			animation-timing-function: ease-out;
		}
		25%
		{
			top: 5px;
			animation-timing-function: ease-in;
		}
		to
		{
			top: -22px;
		}
	}
	````

	The name of the animation sequence in this case is **emphasis**, and the sequence contains three keyframes. The **from** keyframe determines the initial state and the **to** keyframe determines the final state. In between these, any number of keyframes can be added by specifying their position in the animation. This animation contains one keyframe at the 25% mark. Each keyframe can affect different properties and use a different easing function. This animation is very simple, but the ability to create complex sequences using keyframes can help create very advanced animations.

<a name="Summary" />
## Summary ##

In this lab, you learned how to use a small selection of the new features added in CSS3 and implemented by Internet Explorer 10. The features you worked with include web fonts, column layouts, new selectors, rounded corners, box shadows, gradients, transitions, and animations. Internet Explorer 10 fully supports these and many other CSS3 features, so you can use them in any site or application that relies on Internet Explorer 10.
