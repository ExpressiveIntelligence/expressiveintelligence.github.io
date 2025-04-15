# eis-static

Website for the [Expressive Intelligence Studio](https://eis.ucsc.edu) (EIS), a technical and cultural research group at UC Santa Cruz.

## Getting Started

If you have Windows, you first need to install Ruby+Devkit from [RubyInstaller](https://rubyinstaller.org/downloads/), then you can continue with the steps below. See the docs [here](https://jekyllrb.com/docs/installation/windows/) if you have trouble.

To start editing the site, install Jekyll:
```
gem install bundler jekyll
```

And then clone this directory and navigate into it:
```
git clone https://github.com/ExpressiveIntelligence/expressiveintelligence.github.io.git
cd expressiveintelligence.github.io
```

Then you can edit files, and see your changes by using Jekyll to build the static html and host it on a local server:
```
jekyll serve
```

Use a browser to navigate to the server address given by the command (e.g., http://127.0.0.1:4000/).

Stop the server with ctrl-c.

## Editing the Site
1. Before adding anything, use `git pull` to pull any changes made since you last touched the site
2. Make edits
3. Test your changes in the site with `jekyll serve` and navigating to the given address 
4. Before committing, run `jekyll build` to update the `_site/` directory
5. Confirm your changes locally and get them ready to push with `git add` and `git commit` (including any changes to the `_site/` directory)
6. Share your changes using `git push` (directly to the master branch) 
- Don’t make branches for now (we’ll use branches for making future iterations of the site)

## Updating the live site

Unitl recently, a cron job pulled updates from gihub to the live site (we should get this set up). For now, you need to follow these instructions instead.

1. Push your site edits locally using the above instructions.
2. Log on to the [UCSC VPN](https://its.ucsc.edu/vpn/campus-vpn.html). 
3. Run `ssh eis@eis.ucsc.edu` . You will need someone to share the password. Enter the password when prompted.
4. Pull the changes from GitHub: `cd /www/eis.ucsc.edu` followed by `sh pull.sh`

## Some Interesting Filescl

* `_config.yml`: The Jekyll configuration file. Ours is pretty straightforward at the moment, since we're not trying to do anything especially fancy, but you could modify this to do things like add new article types other than the default `page`.
* `_data/publications.json`: An incomplete list of all our publications, stored as an array of JSON objects. This is used to build the table of publications on the site's `/publications` page, and could also be used as a data source for other pages. (For instance, we could pull out all the publications with a given tag and render them on the page for a particular project.)
* `_layouts/page.html`: The base layout for the `page` article type (currently used by every page on the site.) This is where you can go to change things like the site-wide header or the global CSS styles.
* `_site/`: This directory contains the built version of the site. You shouldn't create, edit, or delete files in here directly; Jekyll will manage the contents of this directory for you. Run `jekyll build` (or `jekyll serve`) to regenerate the built version of the site.

## FAQ

### Why do all the page files start with three dashes, a `title: Some page title` line, and three more dashes?

The information between `---` lines at the top of the file is [Jekyll front matter](https://jekyllrb.com/docs/front-matter/). The presence of front matter indicates to Jekyll that it should somehow transform this file when the site is built, for instance by wrapping its content in the `page` template to add stuff like the site-wide header. Files that don't have front matter will be ignored by Jekyll and served as normal static files, without any transformation.

### What's with all these weird curly braces and percent signs in the page files?

Jekyll uses the [Liquid template language](https://shopify.github.io/liquid/) to handle things like iterating over lists and substituting the values of variables into page content. Double curly braces (e.g. `{{some_variable}}`) mean "evaluate whatever's wrapped inside as a Liquid expression, then substitute the resulting value into the page content." Single curly braces with percent signs (e.g. `{% some gibberish %}`) are used for more "magical" constructs like if/else conditionals, variable assignment, iteration over lists, and so on.

### Why are all the pages stored as `{{actual-page-name}}/index.html` instead of `{{actual-page-name}}.html`?

It's a matter of personal preference! I think URLs look cleaner without unnecessary filetype suffixes, and this is a way to achieve the cleaner URLs I crave.

### (Deprecated) How do the contents of this repository get mirrored to the BSOE server?

A cron job on the BSOE server regularly pulls down the contents of the `_site/` directory from this repository and makes them available at https://eis.ucsc.edu. As a result, only changes that are made to the `_site/` directory will be reflected on the official version of the site. This is why it's important to run `jekyll build` (and commit any resulting changes to the `_site/` directory) before you push an updated version of the site to this repo.

Including the `_site/` directory in the repository is unusual for a GitHub Pages site, but makes it possible for us to automatically mirror the site to the BSOE server without installing Jekyll there as well. We should probably find a better way to go about handling the deploy process in the future.
