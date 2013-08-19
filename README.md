Bootless
========
```
This is a work in progress, so please, hold your horses before you go and 
tear it apart ;)
```
The idea behind *Bootless* is to have the most of
[Twitter Bootstrap](http://getbootstrap.org/) v3 without using its markup in 
HTML. Since Bootstrap is written in [LESS](http://lesscss.org/) you could 
avoid using:
```html
<div id="example" class="col-xs-12 col-sm-8 col-md-6 col-lg-4">
    <a href="http://www.example.com/" class="btn btn-danger">Don't go to example.com!</a>
</div>
```
Instead you would just write:
```html
<div id="example">
    <a href="http://www.github.com/">Go to GitHub!</a>
</div>
```
And your LESS file would look like:
```less
#example {
    .col(12);
    > a {
        .button("success");
    }
}

// and somewhere later...
@media (min-width: @screen-tablet) and (max-width: @screen-tablet-max) {
    #example {
        .col(8);
    }
}
```
This way you would have more space to use for your `ng-controller`s and `ng-
model`s if you work with [Angular.js](http://angularjs.org/), and how much 
simpler this would look in [Jade](http://jade-lang.com/). **Less is more!**

To learn more why this approach is more desirable read this
[great article](http://ruby.bvision.com/blog/please-stop-embedding-bootstrap-classes-in-your-html).
To learn about `@screen-tablet` and other Bootstrap variables clone the
[Bootstrap's repository](https://github.com/twbs/bootstrap)
and lookup the `variables.less` file.

## "New mixins? Man, it really is bootless..."
Bootstrap already has `.make-row()` and `.make-*-column()` - why add new 
mixins for the same functionality?
You are always allowed to use Bootstrap's mixins if you like them. I believe 
however that if you use different .less files for different devices, it is 
less ambiguaous to use one `.col()` mixin in them than differently named
`.make-*-column()` which also add their own media query inside.

Bootstrap is not ready to use its classes as mixins in your LESS.
The fun starts if you try to use some classes, like `.jumbotron` or `.btn` 
as a mixin and then eg. turn off border radius. If you do not use some trick 
like:
```less
#element {
    .jumbotron;
    & {
        border-radius: 0;
    }
}
```
Bootstrap will most likely overwrite your style. And this code above just 
sucks; `&` was not meant for this.

To learn about `.make-*-column()` and other Bootstrap mixins clone the
[Bootstrap's repository](https://github.com/twbs/bootstrap) and lookup the
`mixins.less` file.

## Not only new mixins
There is this one variable in Bootstrap called `@grid-gutter-width`. The 
main thing it sets up is the padding on grid segments and the default value 
is 30px. It is not a very welcome solution as it gives you a grid with very 
thick frames. Since Bootstrap changed its policy to
`* { box-sizing: border-box; }` it would be much more welcome to work with a 
grid that makes it much easier to place elements exactly where you want them.
Using a second argument for `.make-*-column()` that changes the default
`@grid-gutter-width` for a specific column makes more mess than use. That is 
why *Bootless* changes some default values of Bootstrap variables, eg.:
`@grid-gutter-width` to `0` so you can use (or not) your own `padding`.

*To be continued...*
