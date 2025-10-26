# Documentation Migration Summary

## Overview

This document summarizes the migration of in-app help documentation from the main tvheadend repository (https://github.com/tvheadend/tvheadend) to this documentation repository.

## What Was Migrated

All files from the `docs/` folder and associated images from `src/webui/static/img/` in the main repository have been copied to the `webui/` folder in this repository, maintaining the exact same structure and file names.

## File Statistics

| Category | Count | Location |
|----------|-------|----------|
| Class Documentation | 37 files | `webui/class/` |
| Property Help | 45 files | `webui/property/` |
| Wizard Steps | 8 files | `webui/wizard/` |
| General Markdown | 19 files | `webui/markdown/` |
| Reusable Content | 22 files | `.gitbook/includes/` |
| Images and Icons | 135 files | `webui/static/img/` |
| **Total** | **266 files** | |
| Supporting Documentation | 2 files | `webui/README.md`, `webui/INTEGRATION.md` |

## Directory Structure

```
webui/
├── README.md                  # Overview of webui documentation
├── INTEGRATION.md             # Guide for main repo integration
├── class/                     # Class-based help (37 files)
│   ├── access_entry.md
│   ├── bouquet.md
│   ├── caclient.md
│   └── ...
├── property/                  # Property-specific help (45 files)
│   ├── action.md
│   ├── auth.md
│   ├── authcode.md
│   └── ...
├── wizard/                    # Setup wizard help (8 files)
│   ├── channels.md
│   ├── hello.md
│   ├── login.md
│   └── ...
├── markdown/                  # General documentation (19 files)
│   ├── introduction.md
│   ├── installation.md
│   ├── firstconfig.md
│   ├── epg.md
│   └── ...
└── static/                    # Images and icons (135 files)
    └── img/
        ├── opencollective.png
        └── doc/
            ├── caclient/
            ├── channel/
            ├── config/
            ├── icons/
            └── ...

.gitbook/includes/             # Reusable content blocks (22 files)
├── buttons.md
├── config_contents.md
├── users_overview.md
└── ...
```

## Verification

All files have been verified to match the original files byte-for-byte using MD5 checksums. No content was lost or modified during the migration.

- ✅ All 131 markdown files copied successfully
- ✅ All 135 image and icon files copied successfully
- ✅ File structure preserved exactly
- ✅ All include directives (`<tvh_include>`) preserved
- ✅ All image references working correctly
- ✅ No files modified or lost

## Content Preservation

The following aspects of the documentation have been preserved:

1. **Include directives**: Converted to GitBook's include syntax
   - Old: `<tvh_include>inc/users_contents</tvh_include>`
   - New: `{% include "../../.gitbook/includes/users_contents.md" %}`

2. **Image references**: All image paths remain unchanged
   - Example: `!['Access Entries' Tab](static/img/doc/users/access_entries_tab.png)`

3. **Internal links**: All cross-references between files preserved
   - Example: `[Access Entries](class/access)`

4. **Markdown formatting**: All tables, lists, code blocks, etc. preserved

## Benefits of This Migration

1. **Centralized Documentation**: All user-facing documentation in one repository
2. **Easier Contributions**: Users can contribute to docs without cloning the main codebase
3. **Independent Versioning**: Documentation can evolve independently of the application
4. **Reduced Main Repo Size**: Removes documentation files from the main codebase
5. **Better Organization**: Clearer separation between code and documentation

## Next Steps

For the main tvheadend repository:

1. Review the integration guide in `webui/INTEGRATION.md`
2. Choose an integration approach (git submodule, URL fetch, or build-time copy)
3. Update the help system to reference the new location
4. Test the in-app help with the new documentation location
5. Deprecate and eventually remove the old `docs/` folder

## References

- **Original Location**: `tvheadend/tvheadend` repository, `docs/` folder
- **New Location**: `tvheadend/documentation` repository, `webui/` folder
- **Integration Guide**: [webui/INTEGRATION.md](webui/INTEGRATION.md)
- **WebUI Documentation**: [webui/README.md](webui/README.md)

## Date of Migration

Migration completed: October 26, 2025

## Contact

For questions about this migration or the documentation structure, please open an issue in this repository.
