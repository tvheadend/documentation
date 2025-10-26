# WebUI In-App Help Documentation

This directory contains the in-app help documentation for the Tvheadend web user interface. These files are used by the main Tvheadend application to provide contextual help to users.

## Directory Structure

- **class/** - Class-based documentation for various configuration screens and objects (31 files)
  - Access entries, bouquets, CA clients, channels, DVR configurations, EPG grabbers, filters, etc.
  
- **property/** - Property-specific help documentation (44 files)
  - Individual field help for authentication, cron, duplicate handling, DVR settings, streaming profiles, etc.
  
- **wizard/** - Setup wizard documentation (8 files)
  - Step-by-step help for the initial setup wizard including channels, login, muxes, network configuration
  
- **markdown/** - General documentation in markdown format (19 files)
  - Introduction, installation, first configuration, EPG, DVR, FAQs, command-line options, etc.
  
- **markdown/inc/** - Reusable markdown includes (22 files)
  - Common button tables, content sections, overviews that are included in other documents

## Usage in Main Repository

The main Tvheadend repository can reference these files using include directives like:

```markdown
<tvh_include>inc/users_contents</tvh_include>
```

This allows the in-app help system to pull content from this centralized documentation repository while keeping the help content separate from the application code.

## File Count

Total files: 131

This represents a complete mirror of the docs/ folder from the main tvheadend repository, maintaining the original structure to ensure compatibility with the in-app help system.
