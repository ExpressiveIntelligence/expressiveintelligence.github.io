# eis-static

A preliminary attempt at a [Jekyll](https://jekyllrb.com/) version of the new EIS website.

## Some Interesting Files

* `_config.yml`: The Jekyll configuration file. Ours is pretty straightforward at the moment, since we're not trying to do anything especially fancy, but you could modify this to do things like add new article types other than the default `page`.
* `_data/publications.json`: An incomplete list of all our publications, stored as an array of JSON objects. This is used to build the table of publications on the site's `/publications` page, and could also be used as a data source for other pages. (For instance, we could pull out all the publications with a given tag and render them on the page for a particular project.)
* `_layouts/page.html`: The base layout for the `page` article type (currently used by every page on the site.) This is where you can go to change things like the site-wide header or the global CSS styles.

## FAQ

### Why do all the page files start with three dashes, a `title: Some page title` line, and three more dashes?

The information between `---` lines at the top of the file is [Jekyll front matter](https://jekyllrb.com/docs/front-matter/). The presence of front matter indicates to Jekyll that it should somehow transform this file when the site is built, for instance by wrapping its content in the `page` template to add stuff like the site-wide header. Files that don't have front matter will be ignored by Jekyll and served as normal static files, without any transformation.

### What's with all these weird curly braces and percent signs in the page files?

Jekyll uses the [Liquid template language](https://shopify.github.io/liquid/) to handle things like iterating over lists and substituting the values of variables into page content. Double curly braces (e.g. `{{some_variable}}`) mean "evaluate whatever's wrapped inside as a Liquid expression, then substitute the resulting value into the page content." Single curly braces with percent signs (e.g. `{% some gibberish %}`) are used for more "magical" constructs like if/else conditionals, variable assignment, iteration over lists, and so on.

### Why are all the pages stored as `{{actual-page-name}}/index.html` instead of `{{actual-page-name}}.html`?

It's a matter of personal preference! I think URLs look cleaner without unnecessary filetype suffixes, and this is a way to achieve the cleaner URLs I crave.
