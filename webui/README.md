# WebUI In-App Help Documentation

This directory contains the in-app help documentation for the Tvheadend web user interface. These files are used by the main Tvheadend application to provide contextual help to users.

## Directory Structure

- **class/** - Class-based documentation for various configuration screens and objects (37 files)
  - Access entries, bouquets, CA clients, channels, DVR configurations, EPG grabbers, filters, etc.
  
- **property/** - Property-specific help documentation (45 files)
  - Individual field help for authentication, cron, duplicate handling, DVR settings, streaming profiles, etc.
  
- **wizard/** - Setup wizard documentation (8 files)
  - Step-by-step help for the initial setup wizard including channels, login, muxes, network configuration
  
- **markdown/** - General documentation in markdown format (19 files)
  - Introduction, installation, first configuration, EPG, DVR, FAQs, command-line options, etc.

- **static/img/** - Images and icons referenced in the documentation (135 files)
  - Screenshots of various configuration screens and UI elements
  - Icons used in the documentation

Reusable content blocks are stored in the root-level `.gitbook/includes/` directory (22 files) and can be referenced from any documentation file using GitBook's include syntax.

## Usage in Main Repository

The main Tvheadend repository can reference these files using include directives like:

```markdown
{% include "../.gitbook/includes/users_contents.md" %}
```

This allows the in-app help system to pull content from this centralized documentation repository while keeping the help content separate from the application code.

## File Count

Total files: 266
- Markdown files: 131
- Images and icons: 135

This represents a complete mirror of the docs/ folder and associated images from the main tvheadend repository, maintaining the original structure to ensure compatibility with the in-app help system.
