# NaviCare Now Website

This is the Hugo-based website for NaviCare Now.

## Brand Identity

The website follows a specific brand color palette designed to represent the core values of NaviCare Now:

| Color | Hex | Component | Meaning |
| :--- | :--- | :--- | :--- |
| **Primary** | `#E86A5C` | **CARE** | Menschlichkeit, Wärme, Dringlichkeit. Pflegerische Beziehung, Fürsorge. (Now-Schrift, Logo-Punkt) |
| **Secondary** | `#7B5EA7` | **EMPOWERMENT** | Stärke, Würde, Kompetenz. Professionelle Stärke, Selbstwirksamkeit. (Pfeil rechts) |
| **Third** | `#16477E` | **TECH** | Innovation, Digital, Zukunft. Technologie, smarte Lösungen. (NaviCare-Schrift) |
| **Quaternary** | `#2DCDC8` | **PROCESS** | Fluss, Verlässlichkeit, Klarheit. Qualität, Struktur und Verlässlichkeit. (Pfeil links) |

## Development

### Configuration
Colors and fonts are managed in `config/_default/params.toml` under the `[variables]` section.

### Styles
Custom styles and brand utilities are located in `themes/wallet-hugo/assets/scss/custom.scss`. These styles use the SCSS variables defined by the Hugo theme to ensure consistency.

### Build
To build the site, run:
```bash
hugo --minify
```
