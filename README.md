
# jxxcarlson/elm-markdown


The aim of this Markdown library is
to provide a pure Elm implementation of Markdown
which offers a small set of optional extensions:

- Standard: the usual thing
- Extended: strike-though text, tables, and Poetry and Verbatim blocks, 
better image handling
- ExtendedMath: like Extended, but math formulas written in
TeX/LaTeX, eg.,
```
This **is** a test: $a^2 + b^2 = c^2$.
```
are properly rendered.


## How to use it


For simple applications, use the `Madrkown.Elm` and `Markdown.Option` modules,
as in these examples:

```
Markdown.Elm.toHtml Extended "This **is** a test."

Markdown.Elm.toHtml ExtendedMath "Use $a^2 + b^2 = c^2$."
```

where in `Markdown.Option` one has

```
type Option
    = Standard
    | Extended
    | ExtendedMath
```

For the `ExtendedMath` option, take a look at `./app-demo/index.html` in the 
[source code](https://github.com/jxxcarlson/elm-markdown) to see what to do.
You will need some Javascript, incuding MathJax 3.

## Demo

There are two versions
of the demo, a basic one in  `./app-demo/`, 
another in `app-demo-fancy` which has more features and some optimizations
that are useful for documents with a lot of mathematics.

See [markdown.minilatex.app](https://markdown.minilatex.app)
for the latest version the fancy demo.

**NOTE:** This package is still evolving relatively rapidly.  I regret
publishing so many updates, but I am using it in several apps, and this
is the only way I know how to encapsulate the complexity, work
 with the CI build systems, and keep my sanity

## Installing the Demo

```bash
$ cd to ./app-demo-fancy

$ npm install

$ npm start
```

## Style

The style used by the library is entirely determined by the
definitions of the CSS classes that you refer to in your
`index.html`.  The ones used for the demo app are found
in `./app-demo/assets/style.css` and `./app-demo-fancy/assets/style.css`
You can easily reconfigure the CSS to satsify your
own esthetics.


## Markdown extensions

I am trying to be conservative about extensions to
Markdown.  However, there are two that I thought
important enough to add: tables, poetry blocks and verbatim text.
Poetry blocks are
are like quotation blocks, except that they begin
with ">>" instead of ">".  Line endings are respected
in poetry blocks.  Verbatim blocks are like code blocks,
except that they are set off by four backticks instead of
three.  No syntax coloring is applied to verbatim blocks.

### Images

The usual `![My favorite image](imageUrl)` does the usual thing, with the image 
scaled to 100% of the width. You can 
also say `![My favorite image::left](imageUrl)` or 
`![My favorite image::right](imageUrl)` to float the image left or right at 
40% width. The widths are defined in `style.css`.



## Advanced Usage: AST

If you 
wish to write your own renderer, or do other fancy things,
you will want to produce and manpulate the AST:

```
Markdown.Parse.toMDBlockTree : Version 
       -> Option -> Document -> Tree MDBlock
```

where `Version` is an integer and `Document` is a type alias for `String`.  
This is also useful if you wish to transform the abstract syntax tree before 
rendering it. The `Version` parameter may be set to zero if you do not
have to worry about updated thd ids of rendered elements in an interactive 
editing environment.



## Editor

The fancy demo app now uses [pure Elm text editor](https://package.elm-lang.org/packages/jxxcarlson/elm-text-editor/latest/).
It is very much a work in progress. 

## Bugs and whatnot

Please write me at jxxcarlson@gmail.com or post an
issue on the [Github repository](https://github.com/jxxcarlson/elm-markdown)
regarding bugs or anything else. I will steer
this library towards the Commonmark spec to the greatest
extent possible by the method of successive approximations


## Changes

See `CHANGELOG.md`


## Thanks

Thanks to Folkert de Vries and Luke Westby.  A shout-out
to Folkert for an optimiztaion of the pure text 
rendering (10 x speedup).

