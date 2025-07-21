# Cooking with Goblins website

This repository is the cooperative's website.

It's based on [Jekyll](https://jekyllrb.com/), using [GitHub pages](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll).

How-tos coming soon.

## Project info

### Style architecture

The styles are achitected to sit somewhere between keeping things small and simple, and a more familiar 7-1 architectuire. 7-1 lite, if you will. Most of the 7 categories have a single stylesheet, internally organised into the traditional sections. As the project grows in complexity, these can be replaced with a more complex internal structure with little impact on consuming stylesheets.

> Because of the way Jekyll works, there is a higher level "main" file in /assets, to hook into Jekyll processing (it has blank YAML frontmatter), which imports the actual SASS styles from _sass/goblin-theme.sass, which would be the top-level main file of the project in "typical" architecture/

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
Sass can be in either syntax, though I prefer sass.

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
