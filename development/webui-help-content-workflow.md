# WebUI Help Content Workflow

## Front End

When a user clicks on a `Help` icon, the browser requests the following 2 URLs.

`http://[TVH_IP]:9981/markdown/class/[TVH_CLASS]?_dc=[??TIMESTAMP??]`

`http://[TVH_IP]:9981/markdown/toc?_dc=[??TIMESTAMP??]`

Both of these URLs return markdown content. The first URL consists of the `md` file that matches the URL’s class as well as all of the contents of all of the `<tvh_include>` files present in the main file followed by an `Items` section containing a description of the properties of the URL’s class.

The second URL contains the static table-of-contents in `md` format from `/docs/markdown/toc.md`.

The markdown data is converted into HTML using the third party `marked` library. This is called from the `tvheadend.mdhelp()` method in `src/webui/static/app/tvheadend.js`.

## Build Process

The script `support/doc/md_to_c.py` is called from the `Makefile` to create the C file `src/docs_inc.c`. This script is called multiple times for multiple `md` file locations with all being centralised into a single `src/docs_inc.c` file.

Each `md` file (including the `toc`) is converted to a C `const char` array. Each element of the array is a line from the source `md` files and is wrapped in an i18n translation function. The file names from the `<tvh_include>` lines are extracted and prefixed with the string `\xff\x04` via a the `MDINCLUDE` compiler preprocessor instruction and added to the array.

At the end of `src/docs_inc.c`, all of the above arrays are then indexed in a structure called `tvh_doc_page`.

In `src/webui/webui.c’` the `/markdown` URL path is configured to be handled by `page_markdown()` in `src/webui/doc_md.c`. There are various functions that are called within this module, however, the `\xff\x04` sequence is interpreted by the function `md_render()` where the `<tvh_include>` text is inserted into the content to be returned.

Once the text from the `md` files has been assembled, the `md_props()` function in `src/webui/doc_md.c` appends the `Items` markdown to the content to be returned.

A typical finally assembled result may look like this:

`[Content from first include file]`\
`Some text or seperator.`\
`[Content from second include file]`\
`Main body of the md file`\
`[Content from third include file]`\
`[Content from the internal object class definition]`

All text returned to the browser is passed through the C i18n process (JS has its own i18n process) and is capable of being rendered line-by-line into any language supported by TVH provided that a translation for that text exists.
