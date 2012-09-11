#OOCSS v OOSCSS
##SassCast show notes

###Differences between Semantic and Presentational classes
* Semantic: a taxonomy that carries meaning. A semantic class should make reference to the HTML block it is associated to. Example: .user-registration, or .billing-info
* Presentational: purely visual. A presentational class will carry no meaning other then to describe the visual being applied to the HTML block. 

##Basic principals of OOCSS
### The good
* Emphasis on reuse
* Keep selectors lean
* Extend classes
* 'Style' separate from content
* 'Content' separate from container

### The Bad
* Heavy use of presentational classes
* Requires application of presentational classes to the markup
* Coupling of CSS(skin) to markup(structure)
* Requires updates to the CSS and markup for design changes
* Argument: lends itself to leaner CSS. Practical use cases creates thousands of lines of CSS that may never be used. Example: Twitter bootstrap

###Basic principals of OOSCSS
* There is no CSS, only Sass
* Placeholder presentational objects
* Mixins for reusable logic to create repetitive CSS
* Semantic classes in the DOM, placeholder presentational objects in your Sass
* Build UI structures and frameworks otherwise impossible with CSS
* Extend classes in your Sass, not the DOM

One can argue that Sass lends itself to code bloat, and I applaud OOCSS for it's ability to put a spotlight on the egregious misuse of CSS in some of the most popular and well written sites. Fact of the matter is that every site I have ever worked on, and had the please of speaking with others with similar experiences, have started out projects with the best of intentions. But after the site goes live and maintenance falls into the hands of others, the code quality goes astray. 

Web sites and web applications of today are larger then ever. I remember writing CSS for sites that consisted of less then 100 lines of code. Hell, we hit that mark with a simple reset. As the CSS gets larger, the UI's get more complicated, the teams working together get larger and skill levels vary greatly, we need a better solution. 

Sure OOCSS' goal is to address some of these issues. After all if you have this library of simply names classes like `.category` `.ptn` `.pvn` `.pan` `.simpleExt` `.onlinestore` etc ... and a simple way to document all these options and their meaning, it is reactively easy for another developer to come along and apply these classes to the markup like so

```html
<div class="category pan simpleExt">
  ...
</div>
```

























