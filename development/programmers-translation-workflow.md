---
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Programmers Translation Workflow

## Background

Translatable texts within TVH are divided into 3 areas:

Text used within the application to describe object properties and values, etc.\
Text used within the main web user interface (WebUI).\
Text used within the 'Help' system of the WebUI (Documentation).

All text is entered in English into the program/documentation source files. For successful translation, the English text also must be added to the master language translation files.

There are 3 master translation files.

`intl/tvheadend.pot`\
`intl/js/tvheadend.js.pot`\
`intl/docs/tvheadend.doc.pot`

These master translation `.pot` files are converted into various language-specific `po` files [as described here](translations.md).

After translation, the language-specific `.po` files are used to build TVH. For example (where XX represents the language code):

`intl/tvheadend.XX.po`\
`intl/js/tvheadend.js.XX.po`\
`intl/docs/tvheadend.doc.XX.po`

This system is very similar to [GNU tettext](https://www.gnu.org/software/gettext/) where a `msgid` tag contains the original English text and a `msgstr` tag contains the translated text.

`msgid "Yes"`\
`msgstr "Oui`

## Programmer Usage

Within program code written in the 'C' programming language, the `N_()` macro is used to identify English text that can be translated into another language. `_()` is used to return translated text at runtime based on the core application's language setting (from the OS).

Within the WebUI code written in the 'JavaScript' programming language, the `_()` function is used to indicate that translation is required.

All of the help system [documentation files](webui-help-content-workflow.md) are converted from markdown text files into C static arrays that also eventually use the `N_()` function before display.

If no translation is available, the original English text passed to `N_()` or `_()`will be returned.

## Building the .pot Files

The 3 `.pot` files are updated by running the `make intl` command which searches the source files for translatable strings and updates the 3 `.pot` files accordingly.

## Build Process

Although there is a single unified build process, translations for each programming language or area referred to above are described separately for clarity.

The list of languages to be processed is determined by the `LANGUAGES_ALL` variable set in `Makefile.common`.

### Build Process - Main Application (C code) and WebUI Help (Markdown)

Called from the main Makefile, the script `support/poc.py` processes the `intl/tvheadend.XX.po` (main application) and `intl/docs/tvheadend.doc.XX.po` (documentation) files and produces a consolidated `tvh_locale_inc.c` file containing all of the text as static C char arrays plus an index array.  This file will be compiled into the final application binary.

### Build Process - WebUI (JavaScript)

Called from Makefile.webui, the script, `support/pojs.py` converts all of the individual `intl/js/tvheadend.js.XX.po` files into individual `webui/static/intl/tvh.XX.js.gz` files. These files are loaded dynamically at runtime by the WebUI based on the user's linguistic preferences.
