Flatdoc
=======

Flatdoc is a small JavaScript file that fetches Markdown files (from Github or
    any URL) and renders them as full pages. Essentially, it's the easiest way
to make open source documentation from *Readme* files.

 * No server-side components
 * No build process needed
 * Deployable via GitHub Pages
 * Just create an HTML file and deploy!

*Current version: 0.8.0*

Getting started
---------------

Create a file based on the template, which has a bare DOM, link to the
scripts, and a link to a theme. It will look something like this (not exact).
For GitHub projects, simply place this file in your [GitHub pages] branch and
you're all good to go.

*In short: just download this file and upload it somewhere.*

[Download template >][template]

``` html
<html>
  <head>
    <!-- Doclet -->
    <script src='http://rstacruz.github.io/flatdoc/v/0.8.0/legacy.js'></script>
    <script src='http://rstacruz.github.io/flatdoc/v/0.8.0/flatdoc.js'></script>

    <!-- Doclet theme (optional) -->
    <link  href='http://rstacruz.github.io/flatdoc/v/0.8.0/theme.white/style.css' rel='stylesheet'>
    <script src='http://rstacruz.github.io/flatdoc/v/0.8.0/theme.white/script.js'></script>

    <!-- Initializer -->
    <script>
      Doclet.run({
        fetcher: Doclet.github('USER/REPO')
      });
    </script>
  </head>

  <body role='flatdoc'>
    <div role='flatdoc-menu'></div>
    <div role='flatdoc-content'></div>
  </body>
</html>
```

### Via GitHub

To fetch a Github Repository's readme file, use the `Doclet.github` fetcher.
This will fetch the Readme file of the repository's default branch.

``` javascript
Doclet.run({
  fetcher: Doclet.github('USER/REPO')
});
```

You may also fetch another file other than the Readme file, just specify it as
the 2nd parameter.

``` javascript
Doclet.run({
  fetcher: Doclet.github('USER/REPO', 'Changelog.md')
});
```

After you've done this, you probably want to deploy it via [GitHub Pages].

[GitHub Pages guide >][GitHub Pages]

### Via a file

You may also fetch a file. In this example, this fetches the file `Readme.md` in
the same folder as the HTML file.

``` javascript
Doclet.run({
  fetcher: Doclet.file('Readme.md')
});
```

You may actually supply any URL here. It will be fetched via AJAX. This is
useful for local testing.

``` javascript
Doclet.run({
  fetcher: Doclet.file('http://yoursite.com/Readme.md')
});
```

How it works
------------

Flatdoc is a hosted `.js` file (along with a theme and its assets) that you can
add into any page hosted anywhere.

#### All client-side

There are no build scripts or 3rd-party services involved. Everything is done in
the browser. Worried about performance? Oh, It's pretty fast.

Flatdoc utilizes the [GitHub API] to fetch your project's Readme files. You may
also configure it to fetch any arbitrary URL via AJAX.

#### Lightning-fast parsing

Next, it uses [marked], an extremely fast Markdown parser that has support for
GitHub flavored Markdown.

Flatdoc then simply renders *menu* and *content* DOM elements to your HTML
document. Flatdoc also comes with a default theme to style your page for you, or
you may opt to create your own styles.

Making documentation
--------------------

Simply create a Markdown document.

Markdown extras
---------------

Flatdoc offers a few harmless, unobtrusive extras that come in handy in building
documentation sites.

#### Blockquotes

Blockquotes show up as side figures. This is useful for providing side
information or non-code examples.

> Blockquotes are blocks that begin with `>`.

#### Smart quotes

Single quotes, double quotes, and double-hyphens are automatically replaced to
their typographically-accurate equivalent. This, of course, does not apply to
`<code>` and `<pre>` blocks to leave code alone.

> "From a certain point onward there is no longer any turning back. That is the
> point that must be reached."  
> --Franz Kafka

#### Buttons

If your link text has a `>` at the end (for instance: `Continue >`), they show
up as buttons.

> [View in GitHub >][project]

Customizing
-----------

### Theme options

For the default theme (*theme-white*), You can set theme options by adding
clasess to the `<body>` element. The available options are:


#### big-h3
Makes 3rd-level headings bigger.

``` html
<body class='big-h3'>
```

#### no-literate
Disables "literate" mode, where code appears on the right and content text
appear on the left.

``` html
<body class='no-literate'>
```

### Adding more markup

You have full control over the HTML file, just add markup wherever you see fit.
As long as you leave `role='flatdoc-content'` and `role='flatdoc-menu'` empty as
they are, you'll be fine.

Here are some ideas to get you started.

 * Add a CSS file to make your own CSS adjustments.
 * Add a 'Tweet' button on top.
 * Add Google Analytics.
 * Use CSS to style the IDs in menus (`#acknowledgements + p`).

### JavaScript hooks

Flatdoc emits the events `flatdoc:loading` and `flatdoc:ready` to help you make
custom behavior when the document loads.

``` js
$(document).on('flatdoc:ready', function() {
  // I don't like this section to appear
  $("#acknowledgements").remove();
});
```

Full customization
------------------

You don't have to be restricted to the given theme. Flatdoc is just really one
`.js` file that expects 2 HTML elements (for *menu* and *content*). Start with
the blank template and customize as you see fit.

[Get blank template >][template]

``` html
<html>
  <head>
    <script src='jquery.js'></script>
    <script src='http://rstacruz.github.io/flatdoc/v/0.8.0/flatdoc.js'></script>
    <!-- Initializer -->
    <script>
      Doclet.run({
        fetcher: Doclet.github('USER/REPO')
      });
    </script>
  </head>

  <body role='flatdoc'>
    <div role='flatdoc-menu'></div>
    <div role='flatdoc-content'></div>
  </body>
</html>
```
Misc
====

Inspirations
------------

The following projects have inspired Flatdoc.

 * [Backbone.js] - Jeremy's projects have always adopted this "one page
 documentation" approach which I really love.

 * [Docco] - Jeremy's Docco introduced me to the world of literate programming,
 and side-by-side documentation in general.

 * [Stripe] - Flatdoc took inspiration on the look of their API documentation.

Changelog
---------

#### v0.8.0 - May 26, 2013

First version.

Acknowledgements
----------------

© 2013, Rico Sta. Cruz. Released under the [MIT 
License](http://www.opensource.org/licenses/mit-license.php).

**Flatdoc** is authored and maintained by [Rico Sta. Cruz][rsc] with help from its 
[contributors][c]. It is sponsored by my startup, [Nadarei, Inc][nd].

 * [My website](http://ricostacruz.com) (ricostacruz.com)
 * [Nadarei, Inc.](http://nadarei.co) (nadarei.co)
 * [Github](http://github.com/rstacruz) (@rstacruz)
 * [Twitter](http://twitter.com/rstacruz) (@rstacruz)

[rsc]: http://ricostacruz.com
[c]:   http://github.com/rstacruz/flatdoc/contributors
[nd]:  http://nadarei.co

[GitHub pages]: https://pages.github.com
[project]: https://github.com/rstacruz/flatdoc
[template]: https://github.com/rstacruz/flatdoc/raw/gh-pages/template.html
[GitHub API]: http://github.com/api
[marked]: https://github.com/chjj/marked
[Backbone.js]: http://backbonejs.org
[dox]: https://github.com/visionmedia/dox
[Stripe]: https://stripe.com/docs/api
[Docco]: http://jashkenas.github.com/docco
[blank]: https://github.com/rstacruz/flatdoc/raw/gh-pages/blank.html
