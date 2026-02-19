# 🕌 Prayer Times for TRMNL

Display accurate Islamic prayer times on your TRMNL e-ink device, powered by the reliable [Aladhan API](https://aladhan.com/). Shows Fajr, Dhuhr, Asr, Maghrib, and Isha prayer times in multiple responsive layouts.

## 🚀 Quick Start

### Prerequisites

- A TRMNL device
- Your geographic coordinates (latitude/longitude)
- Understanding of [TRMNL Framework](https://trmnl.com/framework)

### Getting Started

1. **Add Prayer Times Plugin to TRMNL**:
   - Go to [TRMNL App](https://app.trmnl.com)
   - Search for "Prayer Times" plugin
   - Click "Add Plugin"

2. **Configure Your Location**:
   - Get your latitude and longitude (e.g., Google Maps or [GPS coordinates finder](https://www.gps-coordinates.net/))
   - Enter your coordinates in the plugin settings
   - Choose calculation method (Islamic Society of North America recommended)
   - Select time display format (24-hour or 12-hour)

3. **Choose Display Layout**:
   - **Full**: All prayers with Hijri date
   - **Half Horizontal**: Prayer times side-by-side
   - **Half Vertical**: Current/next prayer emphasized
   - **Quadrant**: Most important prayer only (compact)

4. **Save & Done**:
   - Prayer times auto-update daily with accurate times for your location
   - Displays all 5 religious prayer times: Fajr, Dhuhr, Asr, Maghrib, Isha

## 📁 Project Structure

```
your-plugin-name/
├── .github/
│   ├── copilot-instructions.md    # AI assistant context (customize this!)
│   └── TEMPLATE_USAGE.md           # Instructions for using the template
├── assets/
│   ├── icon/                       # Your plugin icon(s)
│   └── demo/                       # Demo screenshots
├── templates/
│   ├── shared.liquid               # Reusable components
│   ├── full.liquid                 # Full-screen layout
│   ├── half_horizontal.liquid      # Side-by-side layout
│   ├── half_vertical.liquid        # Stacked layout
│   └── quadrant.liquid             # Compact corner layout
├── settings.yml                    # Plugin configuration
├── custom-fields.yml               # Form field definitions
├── LICENSE                         # License (MIT by default)
└── README.md                       # This file
```

## 🎨 Template Files

### Core Templates

- **`shared.liquid`**: Reusable prayer times components
  - Error state for unconfigured plugin
  - Prayer card component
  - Prayer row component
  - Hijri date display
  - Title bar template

- **`full.liquid`**: Full-screen prayer times display
  - All 5 prayers in 2x3 grid layout
  - Gregorian & Hijri dates (conditional)
  - Tabular alignment for precise time display
  - Best for dedicated prayer time display

- **`half_horizontal.liquid`**: Side-by-side layout
  - Main prayers (Fajr, Dhuhr, Asr) on left
  - Evening prayers (Maghrib, Isha) on right
  - Responsive: switches to stacked on portrait
  - Good for shared TRMNL space

- **`half_vertical.liquid`**: Vertical list layout
  - All 5 prayers in list format
  - Name and time side-by-side
  - Dividers between each prayer
  - Compact height usage

- **`quadrant.liquid`**: Quarter-size compact display
  - Shows Fajr (first prayer) only
  - Minimal space (tight padding)
  - Perfect for dashboard integration

### Layout Previews

| Full Layout | Half Horizontal |
|---|---|
| ![Full Layout Preview](assets/demo/preview-full.png) | ![Half Horizontal Preview](assets/demo/preview-half-horizontal.png) |
| **Half Vertical** | **Quadrant** |
| ![Half Vertical Preview](assets/demo/preview-half-vertical.png) | ![Quadrant Preview](assets/demo/preview-quadrant.png) |

## ⚙️ Configuration Files

### `settings.yml`

Configure your plugin's behavior:

```yaml
strategy: "polling"                    # How to fetch data: polling, webhook, static
polling_url: "https://api.example.com" # Endpoint to fetch data from
refresh_frequency: 15                  # Update interval in minutes (1-1440)
layouts: [full, half_horizontal, ...]  # Available layout types
```

**Strategy Options**:
- **polling**: TRMNL fetches data at specified intervals (best for most plugins)
- **webhook**: You push data to TRMNL when it changes (lower latency)
- **static**: Hardcoded data (simple displays)

### `custom-fields.yml`

Define user-facing form fields:

```yaml
- key: "api_key"
  type: "text"
  label: "API Key"
  required: true

- key: "data_source"
  type: "select"
  options:
    - label: "Option A"
      value: "a"
```

**Field Types**: `text`, `long_text`, `select`, `checkbox`, `number`, `url`, `email`

Access in templates:
```liquid
{{ trmnl.plugin_settings.custom_fields_values.api_key }}
```

## 🎯 Key Features

### Accurate Prayer Times
- Uses the reliable **Aladhan API** (no key required)
- Muslim World League calculation method (recommended globally)
- Support for 20+ calculation methods
- Multiple time format options (24-hour / 12-hour)

### Responsive Design
- 4 layout options for different display configurations
- Supports all TRMNL devices and BYOD displays
- Breakpoints: `sm:` (600px), `md:` (800px), `lg:` (1024px+)
- Portrait mode responsive fallbacks

### Customizable
- User-configurable latitude/longitude
- Choice of calculation methods
- Optional Hijri (Islamic) date display
- Custom plugin title
- Multiple time format options

### E-ink Optimized
- Clean, high-contrast design
- Grayscale and monochrome compatible
- Smooth rendering on all bit-depths (1, 2, 4, 8-bit)
- Optimized typography for readability

## ⚙️ Configuration

### Settings (`settings.yml`)
The plugin uses the **Aladhan API** endpoint
```yaml
polling_url: "https://api.aladhan.com/v1/calendar?latitude={latitude}&longitude={longitude}&method={method}&month={month}&year={year}"
refresh_frequency: 1440    # Once daily (24 hours)
```

### Custom Fields (`custom-fields.yml`)
Users configure:
- **Latitude**: Geographic latitude (required)
- **Longitude**: Geographic longitude (required)
- **Calculation Method**: Islamic calculation method (required)
  - Muslim World League (MWL) - Recommended
  - Islamic Society of North America (ISNA)
  - And 18+ other methods
- **Time Format**: 24-hour or 12-hour display
- **Show Hijri Date**: Optional Islamic date display
- **Custom Title**: Optional custom plugin name

## 🔄 Data Flow

### Prayer Times from Aladhan API

```
1. User configures latitude/longitude in TRMNL plugin settings
2. TRMNL sends daily request to Aladhan API with user coordinates
3. Aladhan returns JSON with 5 prayer times:
   - Fajr (pre-dawn)
   - Dhuhr (noon)
   - Asr (afternoon)
   - Maghrib (sunset)
   - Isha (night)
4. TRMNL renders prayer times in chosen layout
5. Display refreshes daily at configured time
```

Example Aladhan API Response:
```json
{
  "data": [{
    "timings": {
      "Fajr": "05:45",
      "Dhuhr": "12:30",
      "Asr": "15:45",
      "Maghrib": "17:45",
      "Isha": "19:15"
    },
    "date": {
      "gregorian": {...},
      "hijri": {...}
    }
  }]
}
```

## 🧪 Testing

### Using TRMNL Markup Editor

1. Go to [editor.trmnl.com](https://editor.trmnl.com)
2. Copy your prayer times template code
3. Add sample JSON data from `assets/demo/sample-data.json`
4. Preview across all device sizes
5. Verify prayer times display correctly

### Prayer Times Test Data

The `assets/demo/sample-data.json` contains sample prayer times for New York (Feb 18, 2026):
- **Fajr**: 05:45 - Early morning
- **Dhuhr**: 12:30 - Noon
- **Asr**: 15:45 - Afternoon
- **Maghrib**: 17:45 - Sunset
- **Isha**: 19:15 - Evening

### Test Scenarios

✅ **Happy Path**
- Valid coordinates (latitude/longitude)
- All 5 prayer times display in correct layouts
- Responsive across sm, md, lg devices
- Time formatting works (24h/12h)

⚠️ **Edge Cases**
- Very high latitude (polar regions - prayer times may be unusual)
- Hijri date display enabled/disabled
- Different calculation methods
- Custom title override

❌ **Error States**
- No coordinates configured
- Invalid coordinates
- Missing custom fields

### Manual Checklist

- [ ] Test all 4 layouts (full, half_horizontal, half_vertical, quadrant)
- [ ] Verify on all device sizes (sm, md, lg)
- [ ] Test with sample data from assets/demo
- [ ] Try all calculation methods
- [ ] Test 24-hour and 12-hour formats
- [ ] Test with/without Hijri date
- [ ] Test custom title feature
- [ ] Verify error state displays
- [ ] Test portrait mode responsive
- [ ] Check tabular number alignment

## 📚 Development Resources

### TRMNL Documentation
- [TRMNL Framework](https://trmnl.com/framework) - Design system and utilities
- [Device Models API](https://trmnl.com/api/models) - Device specifications
- [Plugin Guides](https://help.trmnl.com/en/collections/7820559-plugin-guides) - How-to guides
- [Liquid 101](https://help.trmnl.com/en/articles/10671186-liquid-101) - Template language basics

### Prayer Times Resources
- [Aladhan API Docs](https://aladhan.com/developers) - Free prayer times API
- [Prayer Times Methods](https://aladhan.com/prayer-times-calculation) - Calculation method details
- [Islamic Calendar](https://en.wikipedia.org/wiki/Islamic_calendar) - Hijri calendar info

### Reference: Device Specifications

| Device | Width | Height | Display | Breakpoint |
|--------|-------|--------|---------|-----------|
| TRMNL X | 1040px | 780px | 4-bit (16 shades) | lg: |
| TRMNL OG V2 | 800px | 480px | 2-bit (4 shades) | md: |
| TRMNL OG | 800px | 480px | 1-bit (2 shades) | md: |
| Kindle 2024 | 800px | 480px | 8-bit (256 shades) | sm: |

### Framework Quick Reference

```liquid
<!-- Prayer Time Display -->
<div class="flex flex--col gap--small">
  <span class="label">Fajr</span>
  <span class="value value--large value--tnums">05:45</span>
</div>

<!-- Prayer Grid (2 columns) -->
<div class="grid grid--cols-2 gap--medium">
  <!-- Each prayer card -->
</div>

<!-- Responsive Divider -->
<div class="divider"></div>

<!-- Date Display -->
<div class="flex flex--col text--center">
  <span class="label">Tuesday</span>
  <span class="title">18 February</span>
</div>

<!-- Error State -->
<div class="flex flex--col flex--center-x flex--center-y h--full">
  <div class="value">🕌</div>
  <div class="title">Configure Location</div>
</div>
```

## 🐛 Common Issues & Solutions

### Prayer Times Not Displaying
- **Problem**: "Configure Location" error persists
- **Solution**: Verify latitude/longitude are valid numbers with decimals (e.g., 40.7128, -74.006)

### Wrong Prayer Times
- **Problem**: Times don't match local prayer times
- **Solution**: 
  1. Verify latitude/longitude are correct ([GPS Coordinates Finder](https://www.gps-coordinates.net/))
  2. Check calculation method selected (Muslim World League is recommended globally)
  3. Verify timezone settings in TRMNL

### Time Format Not Changing
- **Problem**: Still showing 24-hour format when set to 12-hour
- **Solution**: 
  1. Update settings.yml to use time format variable
  2. Re-upload templates to TRMNL
  3. Clear plugin cache/refresh device

### Hijri Date Not Showing
- **Problem**: Islamic date not displayed even when enabled
- **Solution**:
  1. Verify `show_hijri_date` is set to `true` in settings
  2. Check full.liquid template has hijri date rendering logic
  3. Ensure sample data includes hijri field from Aladhan

### Layout Issues on Specific Device
- **Problem**: Layout breaks on TRMNL OG but works on TRMNL X
- **Solution**:
  1. Test in TRMNL Markup Editor with correct device size
  2. Verify breakpoint usage (md:, lg: prefixes)
  3. Check portrait mode responsive fallbacks

## 📞 Getting Help

- **TRMNL Documentation**: [help.trmnl.com](https://help.trmnl.com)
- **Aladhan API**: [aladhan.com/developers](https://aladhan.com/developers)
- **TRMNL Framework**: [trmnl.com/framework](https://trmnl.com/framework)
- **GitHub Issues**: Open an issue in this repository

## 🤝 Contributing

Improvements, bug fixes, and feedback welcome!

- Found a display issue? Open an issue
- Have a better layout idea? Submit a PR
- Want to add calculation method examples? Contribute!
- Translations? Help expand to other languages!

## 📄 License

This plugin is provided under the MIT License - see [LICENSE](LICENSE) for details.

---

**Happy praying! 🙏**

Last Updated: February 18, 2026
