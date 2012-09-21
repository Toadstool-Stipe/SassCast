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

One can argue that Sass lends itself to code bloat, and I applaud OOCSS for it's ability to put a spotlight on the egregious misuse of CSS in some of the most popular and well written sites. Fact of the matter is that every site I have ever worked on, and had the pleasure of speaking with others with similar experiences, have started out projects with the best of intentions. But after the site goes live and maintenance falls into the hands of others, the code quality goes astray. 

Web sites and web applications of today are larger then ever. I remember writing CSS for sites that consisted of less then 100 lines of code. Hell, we hit that mark with a simple reset. As the CSS gets larger, the UI's get more complicated, the teams working together get larger and skill levels vary greatly, we need a better solution. 

Sure OOCSS' goal is to address some of these issues. After all if you have this library of simply names classes like `.category` `.ptn` `.pvn` `.pan` `.simpleExt` `.onlinestore` etc ... and a simple way to document all these options and their meaning, it is reactively easy for another developer to come along and apply these classes to the markup like so

```html
<div class="pan simpleExt">
  ...
</div>
```

But where I begin to have issue is that this is not easy to read. Someone coming into the code and not understanding the OOCSS framework has to really dig into the code to figure out what this means. Why does this combination of classes work? If changes are to be made, a developer needs to get into the markup as well as the CSS. In some cases, this may be a real issue depending on how other features are wired to the markup and classes. We all 'know' that we should create special selectors for JS, but do all developers do the right thing? 

I don't 100% understand the naming convention of OOCSS either. I like to use names that have meaning that everyone can understand. I want my cake and eat it too. After all, we are developers and we are masters of our domain, right? 

Gettng back to semantic HTML and CSS. In the markup we are writing, it would make the most sense to use a class name that has meaning related to the content within. Lets use that `.billing-info` class again. This seems like a name that belongs to a form, so lets append this to a semantically correct tag like `fieldset`.

```html
<fieldset class="billing-info">
  ...
</fieldset>
```

*Troll warning: The following example is simply an illustration. I am not advocating that CSS should be written this way. Put the Twitter down and don't send me emails.* 

For this example we are going to style the form `label`. Now this label will be made up of a few simple styles like `font-family` `font-size` `color` and `margin`. For starters we may start with something like ...

```css
.billing-info label {
  font-family: arial;
  font-size: 14px;
  color: #313131;
  margin-bottom: 10px;
}
```

Looking at this, if you were following a design spec and weren't really following any OOCSS guidelines, this would make sense, but nothing is really reusable. All these 'parts' need to be copied and pasted into other classes. So, how can we make this better? OOCSS says like this ...

```css
.arial-font-family {
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
<fieldset class="billing-info">
  <label for="field" class="arial-font-family larger-font-size text-color mbm">Form Label</label>
</fieldset>
```

Wow, that is a mouthful. What, you don't believe me? Have you seen the [Twitter Bootstrap Button Generator](http://www.plugolabs.com/twitter-bootstrap-button-generator/)?

```html
<a href="#" class="btn btn-success btn-large">
  <i class="icon-white icon-heart"></i> Bootstrap Button Generator
</a>
```

C'mon, really? I am supposed to do that with each button in the site? Really? 

But using these techniques I can see where the CSS will be so slim that it is max performance, but at what cost? The process of detailing the markup like this is a maintenance nightmare. And sure when you first start a project there are fewer lines of these OOCSS classes, but as the project grows the number of these classes will grow too. Then at what point does this become to hard to parse through? 

Now OOCSS does have a solution for making all these rules easy to manage. There is a `core.css` file, but it is loaded with css `@import` rules. Really? OOCSS is supposed to be the demarkation of CSS performance and they are using one of the oldest, and [proven more then once],(http://goo.gl/ZkP2w) worst performance killer on the planet? 

##Lets talk about OO'S'CSS now.
### Or what I have been calling it, SMOOSCSS (pronounced 'smokes')
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

So what happens when we want to use these OOSCSS silent classes in other parts of the site, like so?

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
  font-family: arial;
}

.billing-info label, div:first-line {
  font-size: 150%;
}

.billing-info label {
  color: #313131;
}

.billing-info label, input[type=text] {
  margin-bottom: 10px !important;
}
```

Extending classes in the CSS has long been the defacto way for writing tight CSS. While OOCSS does not directly advocate for this technique, I say that OO'S'CSS does. 

Draw your own conclusions, make your own decisions. But from my experience in writing CSS for the past 12 years, Sass is hands down the best way to write scaleable and manageable CSS libraries. 