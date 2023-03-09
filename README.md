# eleventy-base-blog v8 - MODIFIED TO USE sass as a template language

This repo is based on the [eleventy-base-blog](https://github.com/11ty/eleventy-base-blog)

It was modified as follows to illustrate an issue:

- removed all uses of the css bundling feature
- moved all css files to a css folder under the input folder, content
- renamed main .css files with an .scss extension
- created a main.scss with a series of @use statements to include the other scss files
- added code to eleventy config to support sass as a template language

ISSUE:

Non-existent items are added to collections.all resulting in sitemap entries that reference the css files that seem to be intermediate results of processing done in the plugin.

For example, this repo includes the following files in a css directory under the eleventy input directory (which is named content):

```
/content
  /css
    _index.scss
    _message-box.scss
    _prism-diff.scss
    _prism-okaidia.css
    main.scss
```

main.scss has 4 @use statements, referencing each of the other files.

The sitemap.xml that results from processing sitemap.njk includes the following entries:

```
<url>
  <loc>https://example.com/css/_index.css</loc>
  <lastmod>2023-03-02</lastmod>
</url>

<url>
  <loc>https://example.com/css/_message-box.css</loc>
  <lastmod>2023-03-02</lastmod>
</url>

<url>
  <loc>https://example.com/css/_prism-diff.css</loc>
  <lastmod>2023-03-02</lastmod>
</url>

<url>
  <loc>https://example.com/css/main.css</loc>
  <lastmod>2023-03-08</lastmod>
</url>
```
