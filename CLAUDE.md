# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Shopify theme repository based on the **Tinker** theme (v2.1.6) by Shopify. The theme is structured according to Shopify's Online Store 2.0 architecture with sections, templates, blocks, and Liquid templating.

## Development Commands

### Theme Development
```bash
# Log in to Shopify (if not already authenticated)
shopify theme login

# Serve theme locally with hot reload
shopify theme dev

# Push theme to Shopify
shopify theme push

# Pull theme from Shopify
shopify theme pull

# Check theme for errors
shopify theme check
```

### JavaScript Development
The theme uses vanilla JavaScript with TypeScript checking via JSConfig. JavaScript files are located in `/assets/` directory and are loaded as ES modules. The main entry point is `critical.js`.

## Architecture

### Theme Structure
- **`/assets/`**: JavaScript, CSS files, and icons (SVG format)
- **`/blocks/`**: Reusable Liquid block components prefixed with `_`
- **`/config/`**: Theme settings (`settings_schema.json`) and data (`settings_data.json`)
- **`/layout/`**: Main layout files (`theme.liquid`, `password.liquid`)
- **`/locales/`**: Internationalization files in JSON format
- **`/sections/`**: Section files including header, footer, and page sections
- **`/snippets/`**: Reusable Liquid code snippets
- **`/templates/`**: JSON templates for different page types

### Key JavaScript Components
- **Web Components**: The theme uses custom elements pattern (see files like `cart-drawer.js`, `product-form.js`)
- **Event System**: Custom event system in `events.js` for component communication
- **Performance**: Lazy loading and section hydration via `section-hydration.js`
- **Utilities**: Common functions in `utilities.js`

### Liquid Templating Patterns
- Templates use JSON format with section references
- Sections can have blocks and settings
- Snippets are rendered with `{% render 'snippet-name' %}`
- Localization keys use `t:` prefix (e.g., `t:settings.label`)

### TypeScript Checking
JavaScript files are type-checked using JSConfig with:
- Base URL set to assets directory
- Strict null checks enabled
- No implicit any
- Custom type definitions in `global.d.ts`
- Path alias `@theme/*` for imports

## Important Patterns

### Adding New JavaScript
1. Create file in `/assets/` directory
2. Import as ES module in relevant section/template
3. Follow existing Web Component patterns when creating interactive elements
4. Use the event system for cross-component communication

### Section Development
1. Sections should be self-contained with their own settings
2. Use blocks for repeatable content within sections
3. Settings are defined in section schema at the bottom of the file

### Styling
- CSS files are in `/assets/` directory
- Main styles in `base.css`
- Component-specific styles can be inline or in separate files
- Color schemes are configurable via theme settings

## Notes
- This is a git repository with minimal commit history
- No package.json exists - dependencies are managed through Shopify's CDN
- The theme uses Shopify's native architecture without build tools
- All JavaScript runs client-side as ES modules