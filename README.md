# Cooking with Goblins website

This repository is the cooperative's website.

It's based on [Jekyll](https://jekyllrb.com/), using [GitHub pages](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll).

## Install

To get started working with the website locally, you'll need a Ruby environment installed. As part of that, you'll need to have installed bundler and gem, and then jekyll. See [Installing Ruby on the team Notion](https://www.notion.so/Installing-Ruby-for-Jekyll-development-2770d05b6bad80b79d00e6cca44977f0).

Pull the project, navigate to the project folder and run `bundle install` to install project dependencies.

To have the project running a live reload while working with it, run `bundle exec jekyll serve --livereload`. By default it runs on port 4000, so navigating in your browser to `localhost:4000` should show you the running site. As you make changes in the project folder, the site will rebuild and refresh.

> **N.B.** Some changes, like changing the contents of image files, may require a forced refresh, because browsers keep them in cache, even for local sites. On Firefox, that's shift-click on reload. I'm not sure on shortcuts or other borwsers.

## Project info

### Style architecture

The styles are achitected to sit somewhere between keeping things small and simple, and a more familiar [7-1 architecture](https://archisacademy.com/en/blogs/sass-7-1-pattern) ([example project](https://github.com/KhomsiAdam/SASS-Architecture)). 7-1 lite, if you will. Most of the 7 categories have a single stylesheet, internally organised into the traditional sections. As the project grows in complexity, these can be replaced with a more complex internal structure with little impact on consuming stylesheets.

> Because of the way Jekyll works, there is a higher level "main" file in /assets, to hook into Jekyll processing (it has blank YAML frontmatter), which imports the actual SASS styles from _sass/goblin-theme.sass, which would be the top-level main file of the project in "typical" architecture.

- theme/
  - goblin-theme.sass (main sass file)
  - _abstracts.sass
    - variables
    - mixins
  - _base.sass
    - reset
  - _layout.sass
    - site header
    - footer
    - page content
    - posts
    - showcase
  - _themes.sass
    - third-party
    - theme
    - syntax highlighting

### Code style
Code is in line with the included .editorconfig.

> Yes, generally we prefer tabs for code. They have a lot of upsides. Unfortunatley, YAML must use spaces and that means the because Jekyll embeds YAML in Markdown, that the .editorconfig is set up for spaces in markdown files, as it can't currently handle indent rules per-language, just file type.

Anything that can't be encoded in .editorconfig is below, though it should eventually be codified in a linter rules config.

#### SASS
Sass files can be in either syntax, though I prefer sass.

##### Rule spacing
Unless it's the first rule of a section, there should be 2 blank lines between the final line of a rule and the start of the selectors for the next rule. If using SCSS syntax, the line featuring a brace can be counted as blank.

There does not need to be spacing lines between rules which are nested, though it can be useful to differentiate different aspects of a rule, such as responsiveness:

```sass
.showcase
	display: flex
	// ...
	img
		+rounded-rect
		align-self: stretch
	.block-emphasis
		padding:.3rem .5rem

	+media-query-progressive($tablet-up)
		> *
			min-width: unset
```

Sections have 30-width headers as below. There should be 3 blank lines between a rule and a section heading, with the same exception for `}` in SCSS syntax as above.

```sass
// ==========================
// --       Variables      --
// ==========================
```
