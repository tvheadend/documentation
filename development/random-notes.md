---
description: >-
  Snippets of stuff that developers have learned that may be useful to other
  developers but is not yet sufficiently complete or structured for a dedicated
  page.
---

# Random Notes

## WebUI

The WebUI is built on a 'single page application' framework called [Ext JS](https://www.sencha.com/products/extjs/).  The version used appears to be 3.4.1.1 which, is considerably outdated (released circa 2009-2011).

A link to the Ext JS documentation can be found here: [https://cdn.sencha.com/ext/gpl/3.4.1.1/docs/](https://cdn.sencha.com/ext/gpl/3.4.1.1/docs/)

The WebUI appears to be heavily dependent upon the internal `idnode` structures that not only supply the data to the WebUI via JSON, but also data type and formatting information.  See the [JSON Documentation](json-api/) for more details.

Each page or group of pages in the WebUI has its own JavaScript file, however, these normally contain just some setup and housekeeping functions specific to that area, all of the heaving lifting is done in `idnode.js` and  `tvheadend.js` based on the idnode(s) in question.

## Red Black Trees

Internally, TVH stores many objects in Red-Black tree structures rather than arrays.  There are a number of preprocessor macros to support this.  All of these macros are named `RB_fn`, for example, `RB_FOREACH`.\
\
[https://github.com/tvheadend/tvheadend/blob/master/src/redblack.h](https://github.com/tvheadend/tvheadend/blob/master/src/redblack.h)\
[https://en.wikipedia.org/wiki/Red%E2%80%93black\_tree](https://en.wikipedia.org/wiki/Red%E2%80%93black\_tree)
