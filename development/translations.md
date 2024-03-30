# Translations

## Workflow

Tvheadend uses English (en\_GB) as the master langauge for the WebGUI and in-GUI help. Changes to source code that add new features and capabilities must also include updates to the master template `.pot`files under the `intl` directory if existing strings are reused or new strings added.

Merged changes to master template `.pot`files are automatically replicated to Transifex where we manage the translation process. Our project is here: [https://www.transifex.com/projects/p/tvheadend/](https://www.transifex.com/projects/p/tvheadend/)

If changes reuse existing strings local language files do not require translation. If they add new strings language contributors will be notified of the changes and can provide translations of the new strings in the language(s) they support. Once translated strings are saved, Transifex will automatically open a new pull-request against our GitHub repository with updates to the language `.po`files. Transifex will continue to push updates and will combine updates to multiple languages into the same pull-request as long as the pull-request remains open.

## Languages

Existing languages can be seen here: [https://app.transifex.com/tvheadend/tvheadend/languages/](https://app.transifex.com/tvheadend/tvheadend/languages/)

Languages can be added by submitting a language request on Transifex. Once the overall translation state exceeds 80% completed Transifex will submit a pull-request to add new language `.po`files to our GitHub repository. The final stage of addition (other than completing translations) is to edit the list of supported languages in `Makefile` resources.

> Do not submit requests for new languages on Transifex unless you are prepared to personally work on the translations. Translations require effort not magic!&#x20;
