# 🕌 Islamic Prayer Times for TRMNL

Display accurate Islamic prayer times on your TRMNL e-ink device or BYOD display, powered by the reliable [Aladhan API](https://aladhan.com/). Shows all 5 daily prayers (Fajr, Dhuhr, Asr, Maghrib, Isha) with optional Islamic (Hijri) calendar dates in beautiful, responsive layouts.

## ✨ Features

- **Accurate Prayer Times**: Uses Aladhan API with 20+ calculation methods
- **4 Responsive Layouts**: Full-screen, half horizontal/vertical, and compact quadrant
- **Smart Display**: Works on all TRMNL devices and BYOD displays
- **User Customizable**:
  - Location by address (e.g., "London, UK", "New York, USA")
  - Calculation method (Muslim World League, ISNA, and more)
  - Time format (24-hour or 12-hour with AM/PM)
  - Optional Hijri (Islamic calendar) date
  - Custom plugin title
- **E-ink Optimized**: Perfect readability on grayscale and monochrome displays

## 🚀 Quick Start

### Installation

1. Open [TRMNL App](https://app.trmnl.com)
2. Search for **"Islamic Prayer Times"** plugin
3. Click **"Add Plugin"**

### Configuration

1. **Set Your Location**:
   - Enter your city, address, or neighborhood
   - Examples: "Trafalgar Square, London, UK", "Paris, France", "New York, USA"
   - The plugin automatically geocodes your location

2. **Choose Calculation Method**:
   - Muslim World League (MWL) - Recommended as default
   - Islamic Society of North America (ISNA)
   - Or select from 20+ other Islamic scholarly methods

3. **Select Time Format**:
   - 24-hour format: "14:30"
   - 12-hour format: "2:30 PM"

4. **Optional Settings**:
   - Show Islamic (Hijri) calendar date
   - Customize the plugin title

5. **Choose Layout**:
   - **Full**: All 5 prayers with dates (recommended for dedicated space)
   - **Half Horizontal**: Side-by-side layout for mixed displays
   - **Half Vertical**: Vertical list format for narrow spaces
   - **Quadrant**: Compact corner display for dashboards

### That's It!

Prayer times auto-update daily and are accurate for your location based on the calculation method you choose.

## 📁 Project Structure

```
trmnl-prayer-times/
├── .github/
│   └── copilot-instructions.md     # Development guidelines
├── assets/
│   ├── icon/                       # Decorative icons (mosque, praying figure)
│   ├── demo/                       # Demo screenshots
│   └── sample-response/            # Sample API responses for testing
├── templates/
│   ├── shared.liquid               # Reusable prayer components
│   ├── full.liquid                 # Full-screen layout (all 5 prayers + dates)
│   ├── half_horizontal.liquid      # Side-by-side layout
│   ├── half_vertical.liquid        # Vertical list layout
│   └── quadrant.liquid             # Compact corner layout
├── settings.yml                    # API endpoint & refresh configuration
├── custom-fields.yml               # User-facing form fields
├── README.md                       # This file
├── LICENSE                         # MIT License
└── GETTING_STARTED.md              # Extended setup guide
```

## 🎨 Layout Templates

### Full Layout (`full.liquid`)
- All 5 prayers in grid format
- Gregorian date + optional Hijri date
- Best for dedicated prayer times display
- Shows prayer times for the entire day

### Half Horizontal (`half_horizontal.liquid`)
- Side-by-side prayer columns
- Responsive: switches to vertical on portrait
- Good for shared dashboard spaces
- Compact yet readable

### Half Vertical (`half_vertical.liquid`)
- Vertical list of all 5 prayers
- Name and time side-by-side
- Dividers between each prayer
- Minimal height usage

### Quadrant (`quadrant.liquid`)
- Single corner compact display
- Minimal padding and spacing
- Perfect for dashboard integration
- Shows essential prayer info only

### Layout Previews

| Full Layout | Half Horizontal |
|---|---|
| ![Full Layout](assets/demo/preview-full.png) | ![Half Horizontal](assets/demo/preview-half-horizontal.png) |
| All 5 prayers + dates | Side-by-side columns |

| Half Vertical | Quadrant |
|---|---|
| ![Half Vertical](assets/demo/preview-half-vertical.png) | ![Quadrant](assets/demo/preview-quadrant.png) |
| Vertical list | Compact corner |

## ⚙️ How It Works

### Data Flow

```
1. User enters location (e.g., "London, UK")
2. User selects calculation method (e.g., Muslim World League)
3. TRMNL device gets configured
4. Every 24 hours, TRMNL requests: https://api.aladhan.com/v1/timingsByAddress/now
   - Parameters: address, method
5. Aladhan API returns 5 prayer times for that day
6. TRMNL renders prayer times in chosen layout
7. User sees accurate prayer times for their location
```

### Configuration Files

**`settings.yml`**:
```yaml
strategy: "polling"                              # Daily polling
polling_url: "https://api.aladhan.com/v1/timingsByAddress/now?address={{address}}&method={{method}}"
refresh_frequency: 1440                          # Once per 24 hours
layouts: [full, half_horizontal, half_vertical, quadrant]
```

**`custom-fields.yml`**:
- `address` (required): Your location as text
- `method` (required): Calculation method (9 options)
- `time_format` (optional): 24h or 12h display
- `show_hijri_date` (optional): Display Islamic calendar
- `custom_title` (optional): Rename the plugin

### Calculation Methods (Aladhan API)

All methods follow Islamic scholarship standards:

- **Muslim World League (MWL)** - Used globally ⭐ Recommended
- **Islamic Society of North America (ISNA)**
- **University of Islamic Sciences, Karachi**
- **Umm Al-Qura University, Makkah**
- **Egyptian General Authority**
- Plus 8+ additional regional and scholarly methods

[View all methods →](https://aladhan.com/calculation-methods)

## 🧪 Testing & Verification

### Test with Sample Data

Use sample responses in `assets/sample-response/`:
1. Go to [editor.trmnl.com](https://editor.trmnl.com)
2. Copy template code from `templates/full.liquid`
3. Paste sample JSON from `assets/sample-response/toronto.json`
4. Preview and test all layouts

### Verification Checklist

- [ ] All 5 prayers display correctly
- [ ] Time format toggles work (24h/12h)
- [ ] Hijri date shows when enabled
- [ ] Custom title overrides work
- [ ] Responsive across all device sizes
- [ ] Error state displays when unconfigured
- [ ] Test different calculation methods

## 📚 Resources

**Prayer Times & Islamic Calendar**:
- [Aladhan API Docs](https://aladhan.com/prayer-times-api)
- [Calculation Methods Explained](https://aladhan.com/calculation-methods)

**TRMNL Development**:
- [TRMNL Framework](https://trmnl.com/framework) - Design system
- [Device Models API](https://trmnl.com/api/models) - Device specs
- [Plugin Guides](https://help.trmnl.com/en/collections/7820559-plugin-guides)

## ❓ FAQ

**Q: Do I need an API key?**  
A: No! Aladhan API is free to use. No registration needed.

**Q: Which calculation method should I use?**  
A: Muslim World League (MWL) is widely used globally. However, choose the method that matches your local Islamic authority or personal preference.

**Q: Can I change the location after setup?**  
A: Yes! Edit the plugin settings in TRMNL and enter a new location.

**Q: Does it work for prayer times during Ramadan?**  
A: Yes, prayer times adjust automatically based on the actual astronomical calculations for each day.

**Q: What if my prayer times don't match my mosque?**  
A: Mosques often use their own adjustments. Try different calculation methods to find one that matches your mosque's times.

## 📄 License

MIT License - see [LICENSE](LICENSE) for details

---

**Made with 🙏 for the Muslim community**

Last Updated: February 2026

## � Common Issues & Solutions

**Q: "Configure Location" error appears**  
A: Make sure you've entered a valid location (e.g., "London, UK" or "New York, USA"). The location must be a city, address, or neighborhood that Aladhan can geocode.

**Q: Prayer times don't match my mosque**  
A: Different Islamic authorities use different calculation methods. Try switching to a different method in the plugin settings that matches your local mosque or Islamic center.

**Q: Show Hijri Date isn't working**  
A: Enable "Show Islamic Calendar Date" in the plugin settings, save, and refresh your TRMNL device. The Hijri date will appear in the full and half layouts.

**Q: Time format (12h/24h) isn't changing**  
A: Change the setting in TRMNL app, save, and wait for the device to refresh (up to 24 hours, or manually refresh if your device supports it).

**Q: Prayer times are way off**  
A: Verify your location is correct. Use examples like "London, UK" or "Paris, France" - including city and country helps the API geocode accurately.

**Q: Custom title doesn't work**  
A: Enter your custom title in the "Custom Plugin Title" field and save. It will override the default "Islamic Prayer Times" name.

## 📞 Getting Help

- **Prayer Times Questions**: Contact your local Islamic center or [visit Aladhan](https://aladhan.com/)
- **Plugin Issues**: Check this README or open an issue on GitHub
- **TRMNL Support**: [help.trmnl.com](https://help.trmnl.com)

## 🤝 Contributing

Contributions welcome! Whether it's bug fixes, new features, or improvements:
- Found an issue? Submit it!
- Have a layout idea? Create a PR!
- Want to add more calculation methods? Help us improve!

## 📄 License

MIT License - see [LICENSE](LICENSE) for details

---

**Made with 🙏 for the Muslim community**

Last Updated: February 2026
