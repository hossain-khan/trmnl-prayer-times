# Getting Started with Islamic Prayer Times Plugin

This guide explains how to set up and configure the Islamic Prayer Times plugin for your TRMNL device.

## Step 1: Install the Plugin

1. Open the [TRMNL App](https://app.trmnl.com)
2. Search for **"Islamic Prayer Times"**
3. Click **"Add Plugin"**

## Step 2: Configure Your Location

Once installed, open the plugin settings:

1. **Location** *(required)*: Enter your city, address, or neighborhood
   - Examples: `"Toronto, Ontario, CA"`, `"London, UK"`, `"Paris, France"`
   - Include city and country for best results
2. **Calculation Method** *(required)*: Choose the method used by your local mosque
   - Default: **Muslim World League (MWL)** – widely used globally
   - See the [Aladhan calculation methods](https://aladhan.com/calculation-methods) for the full list
3. **Time Format**: Choose `24-hour` (default) or `12-hour` format
4. **Show Islamic Calendar Date** *(optional)*: Display the Hijri date alongside prayer times
5. **Custom Plugin Title** *(optional)*: Override the default "Prayer Times" title

## Step 3: Pick a Layout

| Layout | Description |
|---|---|
| **Full** | All 5 prayers with date and sunrise — best for a dedicated display |
| **Half Horizontal** | All 5 prayers in compact cards — side-by-side display |
| **Half Vertical** | All 5 prayers in compact cards — stacked display |
| **Quadrant** | All 5 prayers — compact corner display |

## Step 4: Done!

Prayer times update daily (every 24 hours) automatically from [Aladhan API](https://aladhan.com).

---

## For Developers

### Repository Structure

```
trmnl-prayer-times/
├── templates/
│   ├── full.liquid              ← Full-screen layout with date and prayers
│   ├── half_horizontal.liquid  ← Half-size horizontal layout
│   ├── half_vertical.liquid    ← Half-size vertical layout
│   ├── quadrant.liquid         ← Compact corner layout
│   ├── shared.liquid           ← Reusable components (prayer_row, title_bar, etc.)
│   └── shared-icons.liquid     ← Base64-encoded icon assets
├── assets/
│   ├── demo/                   ← Preview screenshots
│   └── sample-response/        ← Sample Aladhan API response JSON
├── custom-fields.yml           ← User-facing form fields
├── settings.yml                ← Plugin configuration (polling URL, refresh rate)
└── README.md                   ← Full documentation
```

### Testing Templates

1. Go to [TRMNL Markup Editor](https://editor.trmnl.com)
2. Copy a template (e.g., `full.liquid`) into the editor
3. Use the sample data from `assets/sample-response/toronto.json` as test JSON
4. Preview on different device sizes (sm, md, lg)

### Sample API Response

The plugin polls the [Aladhan API](https://aladhan.com/prayer-times-api) daily:

```
GET https://api.aladhan.com/v1/timingsByAddress/now?address={address}&method={method}
```

See `assets/sample-response/toronto.json` for the full response structure.

Key fields used in templates:

```
data.timings.Fajr       ← Fajr prayer time (HH:mm)
data.timings.Dhuhr      ← Dhuhr prayer time (HH:mm)
data.timings.Asr        ← Asr prayer time (HH:mm)
data.timings.Maghrib    ← Maghrib prayer time (HH:mm)
data.timings.Isha       ← Isha prayer time (HH:mm)
data.timings.Sunrise    ← Sunrise time (HH:mm)
data.date.gregorian     ← Gregorian date (day, month, weekday, year)
data.date.hijri         ← Hijri/Islamic date (day, month, year)
```

### Troubleshooting

**Prayer times not showing?**
- Verify the location field is filled in and recognizable by Aladhan (include city + country)
- Check that the plugin has refreshed since configuration

**Wrong prayer times?**
- Try a different calculation method in settings that matches your mosque
- Verify your location is spelled correctly

**12-hour format not working?**
- Ensure the "Time Format" setting is set to "12-hour"

---

For more information, see [README.md](README.md) and [DATA_SOURCE.md](DATA_SOURCE.md).

