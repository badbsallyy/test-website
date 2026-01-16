# Bot Detection Test Website

Eine lokale Test-Website, die sichtbar macht, wie eine normale Website einen "User" (für Playwright/Automation Tests) wahrnimmt.

## 🎯 Zweck

Diese Website zeigt:
- Welche Informationen der Browser/Test preisgibt
- Welche Bot-Flags gesetzt sind
- Wie „menschlich" oder „auffällig" der Browser wirkt
- Browser-Fingerprinting-Daten
- Automation-Detection-Flags (Playwright, Puppeteer, Selenium, etc.)

## 🚀 Verwendung

### Option 1: GitHub Pages (Online)
Die Website ist online über GitHub Pages verfügbar:
```
https://badbsallyy.github.io/test-website/
```

Die Website wird automatisch bei jedem Push auf den `main` Branch aktualisiert.

### Option 2: Direkt im Browser öffnen (file://)
```bash
# Öffne die index.html direkt im Browser
open index.html  # macOS
start index.html # Windows
xdg-open index.html # Linux
```

### Option 3: Mit lokalem HTTP-Server
```bash
# Python 3
python3 -m http.server 8000

# Python 2
python -m SimpleHTTPServer 8000

# Node.js (mit npx)
npx http-server -p 8000

# Dann Browser öffnen: http://localhost:8000
```

## 📊 Was wird erkannt?

### Bot-Detection Flags
- ✅ `navigator.webdriver` Flag
- ✅ Automation-Tools (Playwright, Puppeteer, Selenium, etc.)
- ✅ Headless-Browser-Indikatoren
- ✅ CDP (Chrome DevTools Protocol) Properties
- ✅ Browser-Inkonsistenzen

### Browser-Fingerprinting
- 🌐 Navigator Properties (UserAgent, Platform, Languages, etc.)
- 🎭 Browser Features (WebGL, WebRTC, ServiceWorker, etc.)
- 🖼️ WebGL-Renderer und -Vendor
- 🔌 Plugins und Extensions
- 📱 Device & Screen Informationen
- 🕰️ Performance & Timing Daten
- 🎨 Canvas Fingerprint

### Bot-Score
Die Website berechnet einen Bot-Score basierend auf erkannten Flags:
- **0 Flags**: 🟢 Menschlich
- **1-3 Flags**: 🟡 Verdächtig
- **4+ Flags**: 🔴 Bot erkannt

## 🧪 Testen mit Playwright

```javascript
// Beispiel Playwright Test
const { chromium } = require('playwright');

(async () => {
  const browser = await chromium.launch({ headless: false });
  const context = await browser.newContext();
  const page = await context.newPage();
  
  await page.goto('file:///path/to/index.html');
  // oder: await page.goto('http://localhost:8000');
  
  await page.waitForTimeout(6000); // Warten für alle Checks
  await page.screenshot({ path: 'bot-detection.png', fullPage: true });
  
  await browser.close();
})();
```

## 🔒 Sicherheit

Diese Website:
- ✅ Benötigt **kein Backend**
- ✅ Sendet **keine Daten** an externe Server
- ✅ Verwendet nur **HTML, CSS und Vanilla JavaScript**
- ✅ Funktioniert vollständig **offline**
- ✅ Speichert **keine Daten** (keine Cookies, kein LocalStorage für Tracking)

## 📝 Technische Details

- **Keine Dependencies**: Reines Vanilla JavaScript
- **Kein Build-Prozess**: Direkt ausführbar
- **Responsive Design**: Funktioniert auf Desktop und Mobile
- **Real-time Detection**: Analysen werden beim Laden durchgeführt

## 🛠️ Anpassungen

Die Datei `index.html` enthält alle HTML, CSS und JavaScript inline. Um Anpassungen vorzunehmen:
1. Öffne `index.html` in einem Editor
2. CSS befindet sich im `<style>` Tag
3. JavaScript befindet sich im `<script>` Tag am Ende
4. Speichern und Browser neu laden

## 📖 Weiterführende Informationen

### Erkannte Automation-Tools
- Playwright (`window.__playwright`)
- Puppeteer (`window.__puppeteer`)
- Selenium (`window.selenium`, `window._Selenium_IDE_Recorder`)
- PhantomJS (`window.callPhantom`, `window._phantom`)
- Nightmare (`window.__nightmare`)
- Chrome DevTools Protocol CDCs

### Headless-Indikatoren
- `HeadlessChrome` im User Agent
- Keine Browser-Plugins
- SwiftShader WebGL Renderer
- Inkonsistente Navigator-Properties

## 🤝 Beitragen

Dies ist eine Test-Website für Entwickler. Verbesserungen und zusätzliche Detections sind willkommen!
