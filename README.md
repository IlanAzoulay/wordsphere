# wordsphere
NPM package: a 3D rolling sphere of words following your mouse movements.

Compatible with Vue JS.


## PREVIEW

<div align="center">
	<img src="https://github.com/IlanAzoulay/wordsphere/blob/master/preview/wordsphere_preview.gif" alt="Preview GIF">
</div>

## FEATURES
Words of your chosing are spread around a fully customizable sphere.\
The sphere is activated when the user's mouse enters its bounding square, and will rotate towards the direction given by the mouse.\
When the mouse leaves the component's bounding square, movement will gradually slow down.\
You can also make the sphere move on its own with just a few tweaks (detailled below)


## INSTALLATION

```bash
npm i wordsphere
```

(TODO: instructions for Nuxt JS)

## HOW TO USE

### BASICS

Add this code to the *<script>* part of your Vue file

```js
import WordSphere from 'wordsphere';

export default {
  components: {
    WordSphere
  }
}
```

<br />

And, in the HTML part, add it almost like any other Vue component, just with a few twists:

```html
<WordSphere :items_list="['Your', 'words', 'here', 'make', 'that', 'list', 'long', 'if', 'you', 'want']"/>
```

We will discuss the input props of the component in more details below, but *items\_list* is non-optional.

<br />

### CUSTOMIZE WITH INPUT PROPERTIES / PROPS

Here is the full list of props you can customize:

#### 1. items\_list

Type: `Array`\
Array of strings, the list of words you want to include in the sphere

#### 2. radius

Type: `Number`\
Unit: `REM`\
Radius of the sphere

#### 3. text\_color

Type: `String`\
Color of the words in the sphere

#### 4. font\_size\_max

Type: `Number`\
Unit: `REM`\
Font size when a word is at the closest point to the user.\
*NOTE: the font size of words furthest behind will be half of that* 

#### 5. blur\_max

Type: `Number`\
Unit: `REM`\
Blur when a word is at the furthest point from user

#### 6. update\_interval

Type: `Number`\
Unit: `milliseconds`\
IMPORTANT: change THIS prop to modify movement speed. The lower the interval, the faster

#### 7. extra\_padding

Type: `Number`\
Unit: `REM`\
Padding around the sphere, in which mouse movement is still listened to

<br />

Overall, if you want to specify all props, this would be the result when calling the component:

```html
<WordSphere 
	:items_list="['Your', 'words', 'here', 'make', 'that', 'list', 'long', 'if', 'you', 'want']"
	:radius="12
	:text_color="'#00FFEA'"
	:font_size_max="2"
	:blur_max="0.1"
	:update_interval="15"
	:extra_padding="2"
	/>
```
<br />

### AUTONOMOUS MOVEMENT

You wish the sphere could move on its own when becoming visible?\
Well my friend, wish no more! Here's how to do it:

#### STEP 1: Add an id and ref to the component

```html
<WordSphere id="id_sphere_object" ref="ref_sphere_object"
      :items_list="['1', '2', '3', '4', '5', '6', '7', '8']"
      :radius="10"
      :text_color="'black'"
      :font_size_max="2"/>
```

#### STEP 2: Add this piece of script

Inside of *export default* within *<script>*

```js
mounted(){
	window.addEventListener("scroll", this.onScroll);
},
methods: {
	onScroll(e) {
		// if the sphere becomes visible
		if (document.getElementById("id_sphere_object").getBoundingClientRect().top <= window.innerHeight){
			this.$refs.ref_sphere_object.start_autonomous_move();
			window.removeEventListener("scroll", this.onScroll);
		}
	},
}
```

My code is based on scroll, but you can of course do your own tweaks to activate autonomous move based on another type of event!

<br />

## LICENSE

Copyright 2022 Ilan Azoulay

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), 
to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, 
and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, 
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, 
WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
