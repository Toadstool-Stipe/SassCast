#OOCSS v OOSCSS
##SassCast show notes

Hey everyone and welcome to another installemnt of SassCast. 

In this episode I am going to talk about what I see as the main differences between vanilla CSS w/OOCSS and using Sass. To begin, I want to make sure that we are all clear on the definitions betwee Semantic and Presentations classes.    

###Semantic and Presentational classes
* Presentational: purely visual. A presentational class will carry no meaning other then to describe the visual being applied to the HTML block.
* Semantic: a taxonomy that carries meaning. A semantic class should make reference to the HTML block it is associated to. Example: `.user-registration`, or `.billing-info`

Ok, now that we have that out of the way, let's get into the principals of OOCSS. The good and the bad. 

##Basic principals of OOCSS
### The good
* Emphasis on reuse
* Keep selectors lean
* Extend classes
* Emphasis on 'Style' separate from content
* Emphasis on 'Content' separate from container

### The Bad
* Heavy use of presentational classes
* Requires application of presentational classes to the markup
* Coupling of CSS(skin) to markup(structure)
* Requires updates to the CSS and markup for design changes
* Argument: creates thousands of lines of CSS that may never be used. Example: Twitter bootstrap

###Basic principals of OOSCSS
* There is no CSS, only Sass
* Placeholder presentational objects
* Mixins for reusable logic to create repetitive CSS
* Semantic classes in the DOM, placeholder presentational objects in your Sass
* Build UI structures and frameworks otherwise impossible with CSS
* Extend classes in your Sass, not the DOM


Sure OOCSS' goal is to address some of these issues. After all if you have this library of simply names classes like `.ptn` `.pvn` `.pan` etc ... and a simple way to document all these options and their meaning, it is reactively easy for another developer to come along and apply these classes to the markup like so.

```html
<div class="pan">
  ...
</div>
```

*Troll warning: The following example is simply an illustration.* 

For this example we are going to style the form `label`. Now this label will be made up of a few simple styles like `font-family` `font-size` `color` and `margin`. For starters we may start with something like ...

```css
.billing-info label {
  font-family: arial;
  font-size: 14px;
  color: #313131;
  margin-bottom: 10px;
}
```

If you are following a design spec and weren't really following any OOCSS guidelines, this would make sense, but nothing is really reusable. All these 'parts' need to be copied and pasted into other classes. So, how can we make this better? OOCSS says like this ...

```css
.label-font-family {
  font-family: arial;
}

.larger-font-size {
  font-size: 150%;
}

.text-color {
  color: #313131;
}

.mbm, .mvm, .mam {
  margin-bottom:10px !important
}
```

Then in our markup we would do this:

```html
<fieldset>
  <label for="field" class="arial-font-family larger-font-size text-color mbm">Form Label</label>
</fieldset>
```

Wow, that is a mouthful. What, you don't believe me? Have you seen the [Twitter Bootstrap Button Generator](http://www.plugolabs.com/twitter-bootstrap-button-generator/)?

```html
<a href="#" class="btn btn-success btn-large">
  <i class="icon-white icon-heart"></i> Bootstrap Button Generator
</a>
```

##Lets talk about OO'S'CSS now
*Scaleable, Modulare Object Oriented Sassy Cascading Style Sheets*

Taking that same example we can get back to the semantic naming of these markup blocks and use Sass to create the reusable CSS objects. 

```html
<fieldset class="billing-info">
  <label for="text-field">
    ...
  </label>
</fieldset>
```

```scss
%arial-font-family {
  font-family: arial;
}

%larger-font-size {
  font-size: 150%;
}

%text-color {
  color: #313131;
}

%mbm {
  margin-bottom:10px !important
}

.billing-info {
  label {
    @extend %arial-font-family;
    @extend %larger-font-size;
    @extend %text-color;
    @extend %mbm;
  }
}
```

In this example I am using a new feature of Sass, silent placeholders. This allows developers to make OOCSS type presentational class and they sit there silent until they are extended within another class that will be used by the site. `.billing-info label` in this example. 

Using this technique, the silent classes when extended into the `.billing-info` selector process to the following CSS.

```css
.billing-info label {
  font-family: arial; }

.billing-info label {
  font-size: 150%; }

.billing-info label {
  color: #313131; }

.billing-info label {
  margin-bottom: 10px !important; }
```

Let's expand on this idea and say that we have labels for the Shipping Address that we want to have the same look.

```scss
.shiping-info {
  label {
    @extend %arial-font-family;
    @extend %larger-font-size;
    @extend %text-color;
    @extend %mbm;
  }
}
```

Here's the CSS

```css
.billing-info label {
  font-family: arial; }

.billing-info label, .shiping-info label {
  font-size: 150%; }

.billing-info label, .shiping-info label {
  color: #313131; }

.billing-info label, .shiping-info label {
  margin-bottom: 10px !important; }
```

So what happens when we want to use these OOSCSS placeholder classes in other parts of the site, like so?

```scss
div {
  &:first-line {
    @extend %larger-font-size;
  }
}

input {
  &[type=text] {
    @extend %mbm;
  }
}
```

In the end we get this ...

```css
.billing-info label {
  font-family: arial; }

.billing-info label, .shiping-info label, div:first-line {
  font-size: 150%; }

.billing-info label, .shiping-info label {
  color: #313131; }

.billing-info label, .shiping-info label, input[type=text] {
  margin-bottom: 10px !important; }
```

Extending classes in the CSS has long been the defacto way for writing tight CSS. While OOCSS does not directly advocate for this technique, I say that OO'S'CSS does. 

Draw your own conclusions, make your own decisions. But from my experience in writing CSS for the past 12 years, Sass is hands down the best way to write scaleable and manageable CSS libraries. 