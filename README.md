# eleventy-base-blog v8 - MODIFIED TO USE eleventy-plugin-sass-lightningcss

This repo is based on the [eleventy-base-blog](https://github.com/11ty/eleventy-base-blog)

ISSUE:

When using the [eleventy-plugin-sass-lightningcss](https://github.com/5t3ph/eleventy-plugin-sass-lightningcss) plugin as directed to process scss files, non-existent items are added to collections.all resulting in sitemap entries that reference the input scss files.

For example, this repo includes the following files in a css directory under the eleventy input directory (which is named content):

```
/content
  /css
    index.scss
    message-box.scss
    prism-diff.scss
    prism-okaidia.scss
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
		<loc>https://example.com/css/_prism-okaidia.css</loc>
		<lastmod>2023-03-08</lastmod>
	</url>

	<url>
		<loc>https://example.com/css/main.css</loc>
		<lastmod>2023-03-08</lastmod>
	</url>
```

The eleventy base blog was modified as follows to illustrate this issue:

- removed all uses of the css bundling feature
- moved all css files to a css folder under the input folder, content
- renamed all .css files with an .scss extension
- created a main.scss with a series of @use statements to include the other scss files
- installed the [eleventy-plugin-sass-lightningcss](https://github.com/5t3ph/eleventy-plugin-sass-lightningcss) plugin
- modified eleventy.config.js to add the lines necessary to add the plugin
