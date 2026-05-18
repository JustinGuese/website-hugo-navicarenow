# NaviCare Now Website

This is the Hugo-based website for NaviCare Now.

## Brand Identity

The website follows a specific brand color palette designed to represent the core values of NaviCare Now:

| Color          | Hex       | Component       | Meaning                                                                                           |
| :------------- | :-------- | :-------------- | :------------------------------------------------------------------------------------------------ |
| **Primary**    | `#E86A5C` | **CARE**        | Menschlichkeit, Wärme, Dringlichkeit. Pflegerische Beziehung, Fürsorge. (Now-Schrift, Logo-Punkt) |
| **Secondary**  | `#7B5EA7` | **EMPOWERMENT** | Stärke, Würde, Kompetenz. Professionelle Stärke, Selbstwirksamkeit. (Pfeil rechts)                |
| **Third**      | `#16477E` | **TECH**        | Innovation, Digital, Zukunft. Technologie, smarte Lösungen. (NaviCare-Schrift)                    |
| **Quaternary** | `#2DCDC8` | **PROCESS**     | Fluss, Verlässlichkeit, Klarheit. Qualität, Struktur und Verlässlichkeit. (Pfeil links)           |

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

#### cal.com

    <div class="col-lg-6 mt-5 mt-lg-0">
              <div class="contact-info">
                      <h4>{{ i18n `book_meeting` }}</h4>

              <!-- Cal inline embed code begins -->
              <div style="width:100%;height:100%;overflow:scroll" id="my-cal-inline-30min"></div>
              <script type="text/javascript">

(function (C, A, L) { let p = function (a, ar) { a.q.push(ar); }; let d = C.document; C.Cal = C.Cal || function () { let cal = C.Cal; let ar = arguments; if (!cal.loaded) { cal.ns = {}; cal.q = cal.q || []; d.head.appendChild(d.createElement("script")).src = A; cal.loaded = true; } if (ar[0] === L) { const api = function () { p(api, arguments); }; const namespace = ar[1]; api.q = api.q || []; if(typeof namespace === "string"){cal.ns[namespace] = cal.ns[namespace] || api;p(cal.ns[namespace], ar);p(cal, ["initNamespace", namespace]);} else p(cal, ar); return;} p(cal, ar); }; })(window, "https://app.cal.eu/embed/embed.js", "init");
Cal("init", "30min", {origin:"https://app.cal.eu"});

Cal.ns["30min"]("inline", {
elementOrSelector:"#my-cal-inline-30min",
config: {"layout":"month_view"},
calLink: "navicarenow/30min",
});

Cal.ns["30min"]("ui", {"hideEventTypeDetails":false,"layout":"month_view"});
</script>

  <!-- Cal inline embed code ends -->

              </div>
