# Night Sky Calendar 🌟

Automated calendar generator for astronomical events. Creates personalized stargazing schedules based on your location and equipment.

## Overview

Night Sky Calendar helps amateur astronomers plan their observing sessions by generating customized calendars of astronomical events. Whether you're using binoculars, a small telescope, or just your naked eyes, this tool filters events based on your equipment and location to show you what's worth observing.

## Features

- **Location-aware calculations** - Uses your coordinates for accurate rise/set times and visibility
- **Equipment filtering** - Customizes recommendations based on your telescope/binoculars specifications
- **Multiple output formats** - Generate ICS calendar files, PDF schedules, or web views
- **Weather integration** - Optional cloud cover probability for better planning
- **Magnitude filtering** - Hide objects too faint for your equipment or light pollution
- **Custom event types** - Planets, meteor showers, ISS passes, lunar phases, and more

## Installation

### Requirements
- Python 3.8+
- pip

### Setup
```bash
git clone https://github.com/i-eyesack/night-sky-calendar.git
cd night-sky-calendar
pip install -r requirements.txt
```

### Dependencies
- `ephem` - Astronomical calculations
- `icalendar` - ICS file generation
- `requests` - Weather API calls
- `matplotlib` - Sky charts (optional)
- `reportlab` - PDF generation

## Quick Start

### Basic Usage
```bash
python night_sky.py --lat 40.7128 --lon -74.0060 --days 30
```

### With Equipment Specifications
```bash
python night_sky.py --lat 40.7128 --lon -74.0060 --telescope-aperture 6 --limiting-magnitude 12.5 --days 30
```

### Generate Calendar File
```bash
python night_sky.py --lat 40.7128 --lon -74.0060 --output calendar.ics --format ics
```

## Configuration

Create a `config.yml` file for your default settings:

```yaml
location:
  latitude: 40.7128
  longitude: -74.0060
  timezone: "America/New_York"
  elevation: 10  # meters above sea level

equipment:
  telescope_aperture: 6  # inches
  limiting_magnitude: 12.5
  minimum_altitude: 30  # degrees above horizon

preferences:
  include_planets: true
  include_deep_sky: true
  include_meteor_showers: true
  include_iss_passes: true
  include_lunar_phases: true
  minimum_magnitude: 6.0  # naked eye limit in city

weather:
  enabled: false
  api_key: ""  # OpenWeatherMap API key
```

## Event Types

### Planetary Events
- Conjunctions and oppositions
- Greatest elongations (Mercury, Venus)
- Best viewing periods for each planet

### Deep Sky Objects
- Best viewing months for galaxies, nebulae, clusters
- Filtered by your equipment capabilities
- Rise/set times and optimal viewing windows

### Meteor Showers
- Peak dates and hourly rates
- Moon phase interference calculations
- Radiant position and best viewing times

### International Space Station
- Visible passes for your location
- Magnitude and duration information
- Pass predictions up to 10 days ahead

### Lunar Events
- New moon dates (best for deep sky)
- Full moon times
- Lunar eclipses and special librations

## Output Formats

### ICS Calendar
Import directly into Google Calendar, Outlook, or Apple Calendar:
```bash
python night_sky.py --format ics --output astronomy_2024.ics
```

### PDF Schedule
Printable monthly schedules:
```bash
python night_sky.py --format pdf --output march_2024.pdf
```

### Web View
Generate HTML page with interactive elements:
```bash
python night_sky.py --format html --output index.html
```

## Examples

### Urban Observer (City, Small Telescope)
```bash
python night_sky.py --lat 40.7128 --lon -74.0060 \
  --telescope-aperture 4 --limiting-magnitude 10 \
  --minimum-altitude 40 --exclude-faint-deep-sky
```

### Dark Sky Site (Rural, Large Telescope)
```bash
python night_sky.py --lat 43.0642 --lon -87.9073 \
  --telescope-aperture 12 --limiting-magnitude 16 \
  --minimum-altitude 20 --include-all-messier
```

### Naked Eye Only
```bash
python night_sky.py --lat 34.0522 --lon -118.2437 \
  --naked-eye-only --limiting-magnitude 5.5
```

## API Usage

The module can also be used as a Python library:

```python
from night_sky_calendar import SkyCalendar

# Initialize with location
calendar = SkyCalendar(latitude=40.7128, longitude=-74.0060)

# Set equipment parameters
calendar.set_equipment(aperture=6, limiting_magnitude=12.5)

# Generate events for next 30 days
events = calendar.generate_events(days=30)

# Export to various formats
calendar.export_ics("astronomy.ics")
calendar.export_pdf("schedule.pdf")
```

## Contributing

Contributions welcome! Areas where help is particularly appreciated:

- Additional astronomical event types
- Better light pollution modeling
- Mobile app development
- Translation to other languages

Please read `CONTRIBUTING.md` for guidelines.

## Astronomy Club Integration

This tool was originally developed for the Metro City Astronomy Club. Special features for clubs:

- Bulk calendar generation for multiple members
- Club event integration
- Equipment sharing schedules
- Group observing session planning

## Data Sources

- Planetary positions: PyEphem library
- Meteor shower data: International Meteor Organization
- ISS orbit data: NASA/SpaceX APIs
- Deep sky object catalog: Messier, NGC, IC catalogs
- Weather data: OpenWeatherMap API (optional)

## Known Limitations

- ISS predictions limited to 10 days (orbital mechanics)
- Weather integration requires API key
- Some deep sky objects may not account for light pollution accurately
- Doesn't include satellite flares (too unpredictable)

## License

MIT License - see LICENSE file for details.

## Author

Isaac Eyesack - [@sei-renae](https://github.com/sei-renae)

*"The sky is not the limit, it's just the beginning."*

## Changelog

### v2.1.0 (Current)
- Added weather integration
- Improved PDF formatting
- Better equipment filtering
- Bug fixes for southern hemisphere calculations

### v2.0.0
- Complete rewrite in Python 3.8+
- Added web output format
- Equipment-based filtering
- Configuration file support

### v1.x
- Initial release
- Basic ICS calendar generation
- Simple command-line interface
