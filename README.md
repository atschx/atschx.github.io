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
- Positioning line: **在我这里都是未知**
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

- **Framework**: Jekyll + GitHub Pages, serving one static `index.html`
- **Typography** (embedded in `index.html`, no font CDN at runtime):
  - Bodoni Moda variable, latin only, optical size 6–96 and weight 500–600, for the brand name and English entry titles
  - IBM Plex Sans 400, latin only, for UI text
  - IBM Plex Mono 400, latin only, for labels and metadata
  - Chinese uses the system stack after IBM Plex Sans: PingFang SC, Hiragino Sans GB, Noto Sans CJK SC, Microsoft YaHei, sans-serif
- **Licenses**: SIL Open Font License 1.1
  - `assets/fonts/OFL-BodoniModa.txt`
  - `assets/fonts/OFL-IBMPlexSans.txt`
  - `assets/fonts/OFL-IBMPlexMono.txt`
- **Browser Support**: Modern browsers with CSS3 and WOFF2 support
- **Files**:
  - `index.html` - Homepage: markup, inlined CSS, and subset WOFF2 data URIs
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
