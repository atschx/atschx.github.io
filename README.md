# atschx.me - Direction E Homepage

Personal brand homepage for atschx.me, featuring a minimalist design with automatic light and dark mode support.

## Design Features

### Visual Style
- **Light Mode**: Cool gray-blue stone wall with soft daylight from upper right
- **Dark Mode**: Indigo interior with warm amber window light from upper right
- Automatic theme switching via `prefers-color-scheme` (no manual toggle)

### Color System
Based on OKLCH color roles with shared hues across modes:
- **Field** (Indigo ~270°): Cool stone (light) / Night interior (dark)
- **Window Light** (Amber ~68°): Warm illumination from upper right
- **Anchor** (Green ~150°): Current/selected path indicator

### Layout Structure
- Oversized "atschx" in Bodoni Moda typeface
- Positioning line: **都是为此**
- Three navigation entries:
  - **Blog** → https://blog.atschx.me (live, solid line)
  - **Photography** → Coming soon (dashed line, not clickable)
  - **About Me** → https://blog.atschx.me/about/ (live, solid line)
- GitHub corner link

### Responsive Design
- Full support for desktop, tablet, and mobile
- Optimized typography and spacing for each breakpoint
- Touch-friendly interaction targets

## Technical Implementation

- **Framework**: Jekyll + GitHub Pages
- **Typography**: 
  - Bodoni Moda (variable) for brand name and headings
  - IBM Plex Sans for body text
  - IBM Plex Mono for labels and metadata
  - Loaded via Google Fonts CDN
- **Browser Support**: Modern browsers with CSS3 support
- **Files**:
  - `index.html` - Homepage structure
  - `assets/css/main.css` - Direction E style system
  - `assets/css/fonts.css` - Font loading
  - `_config.yml` - Jekyll configuration

## Preserved from Previous Site
- `CNAME` - Domain configuration (atschx.me)
- `assets/images/` - Legacy image assets
- `assets/pdf/` - Legacy PDF documents
- `favicon.ico`

## Development

```bash
# Serve locally (requires Jekyll)
bundle exec jekyll serve

# Or use simple HTTP server
python3 -m http.server 8080
```

## Credits

Design: Direction E by atschx  
Implementation: 2026-11-27

---

**Note**: This design replaces the previous blog layout with owner authorization.
