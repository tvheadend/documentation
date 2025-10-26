# Integration Guide for Main Repository

This guide explains how the main Tvheadend repository can reference and include files from this documentation repository.

## Overview

The WebUI in-app help documentation has been moved to this repository to centralize documentation management. The main Tvheadend repository can reference these files using includes or direct links.

## File Structure Reference

The documentation is organized as follows:

```
webui/
├── class/              # Class documentation (37 files)
├── property/           # Property help (45 files)  
├── wizard/             # Wizard steps (8 files)
├── markdown/           # General docs (19 files)
├── static/img/         # Images and icons (135 files)
└── README.md           # This structure overview

.gitbook/includes/      # Reusable content blocks (22 files)
```

## Using Include Directives

The files use GitBook's include directive to pull in reusable content. For example:

```markdown
{% include "../../.gitbook/includes/users_contents.md" %}
```

These reusable content blocks are stored in the `.gitbook/includes/` directory and can be referenced from any documentation file using relative paths.

### Option 1: Git Submodule
Add this repository as a git submodule in the main repository:

```bash
cd /path/to/tvheadend
git submodule add https://github.com/tvheadend/documentation.git docs-external
```

Then update the include paths to reference `docs-external/webui/`.

### Option 2: Direct URLs
Configure the help system to fetch documentation from the live repository:

```
https://raw.githubusercontent.com/tvheadend/documentation/master/webui/class/access_entry.md
```

### Option 3: Build-time Copy
During the build process, fetch the latest documentation:

```bash
# In build script
wget -r -np -nH --cut-dirs=2 \
  https://github.com/tvheadend/documentation/tree/master/webui/
```

## File Mapping

The original `docs/` folder structure has been preserved under `webui/`:

| Original Path | New Path in Documentation Repo |
|---------------|--------------------------------|
| `docs/class/*.md` | `webui/class/*.md` |
| `docs/property/*.md` | `webui/property/*.md` |
| `docs/wizard/*.md` | `webui/wizard/*.md` |
| `docs/markdown/*.md` | `webui/markdown/*.md` |
| `docs/markdown/inc/*.md` | `.gitbook/includes/*.md` (reusable content) |

## Examples

### Access Entry Documentation
- **Original**: `docs/class/access_entry.md`
- **New Location**: `webui/class/access_entry.md`
- **Full URL**: `https://github.com/tvheadend/documentation/blob/master/webui/class/access_entry.md`

### Include File for Users
- **Original**: `docs/markdown/inc/users_contents.md`
- **New Location**: `.gitbook/includes/users_contents.md`
- **Include**: `{% include "../../.gitbook/includes/users_contents.md" %}`

### Wizard Hello Page
- **Original**: `docs/wizard/hello.md`
- **New Location**: `webui/wizard/hello.md`

## Maintaining Compatibility

To maintain compatibility with the existing in-app help system:

1. **Keep the same file names** - All files retain their original names
2. **Use GitBook includes** - Reusable content uses `{% include %}` syntax
3. **Maintain structure** - The directory hierarchy remains the same (class/, property/, wizard/, markdown/)

## Next Steps for Main Repository

1. Decide on the integration approach (submodule, URL fetch, or build-time copy)
2. Update the help system to reference the new location
3. Configure the build process to pull in documentation as needed
4. Update any hard-coded paths in the application
5. Test the in-app help system with the new documentation location
6. (Optional) Remove the old docs/ folder once migration is confirmed working

## Benefits

- **Centralized documentation** - All documentation in one place
- **Easier contributions** - Users can contribute to docs without building the app
- **Version control** - Documentation can be versioned independently
- **Reduced repository size** - Main repo doesn't carry doc files
- **Better collaboration** - Documentation team can work independently

## Questions?

If you have questions about integrating this documentation, please open an issue in the documentation repository or contact the Tvheadend development team.
