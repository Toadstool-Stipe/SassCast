#OOCSS v OOSCSS
###SassCast show notes

* Differences between Semantic and Presentational classes
** Semantic: a taxonomy that carries meaning. A semantic class should make reference to the block it is associated to. Example: .user-registration, or 
** Presentational: purely visual. A presentational class will carry no meaning other 

* Basic principals of OOCSS
	*Heavy use of presentational classes
	*Dependent on application of presentational classes to the markup
	*Requires updates to the CSS and markup for design changes
	*Argument: lends itself to leaner CSS. Practical use cases creates thousands of lines of CSS that may never be used. Example: Twitter bootstrap

* Basic principals of OOSCSS
** Requires Sass
** Makes use of presentational objects
** Allows for semantic classes in the DOM, while leveraging presentational objects in your Sass  
