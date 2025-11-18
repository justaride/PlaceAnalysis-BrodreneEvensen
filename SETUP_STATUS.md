# Setup Status - Brødrene Evensen Portfolio

## ✅ Fullført

### Prosjektkopiering
- [x] Kopiert fra Maya Eiendom til place-analysis-brodreneevensen
- [x] Ekskludert node_modules, .next, .git, .vercel, .DS_Store

### Branding Oppdateringer
- [x] **package.json** - Navn og beskrivelse oppdatert til Brødrene Evensen
- [x] **README.md** - Tittel og lisens oppdatert
- [x] **layout.tsx** - Metadata (title, description, keywords, authors) oppdatert
- [x] **Header.tsx** - Midlertidig tekstlogo "Brødrene Evensen" (klar for logo-erstattning)

### Datarensing
- [x] Slettet Maya-eiendomsdata (4 JSON-filer fra src/data/eiendommer/)
- [x] Slettet Maya-aktørdata (4 JSON-filer fra src/data/aktorer/)
- [x] Slettet Maya-eiendomsbilder (public/images/)
- [x] Slettet Maya Plaace-bilder (public/images/plaace/)
- [x] Slettet Maya-logo (maya-logo.jpg)
- [x] Slettet Maya-spesifikk dokumentasjon (BRENNERIVEIEN_5_SETUP.md, etc.)
- [x] Slettet PDF-mappe med Maya-dokumenter

### Strukturell Integritet
- [x] Alle komponenter beholdt (ui, layout, eiendom, comparison)
- [x] Alle lib-funksjoner beholdt (eiendom-loader, validation, utils)
- [x] Alle typer beholdt (eiendom.ts, plaace.ts)
- [x] Scripts beholdt (validate-data.ts, process_aktor_csv.py)
- [x] Dokumentasjon beholdt (LEGG-TIL-EIENDOM.md, DATASTRUKTUR.md, DEPLOYMENT.md)
- [x] Natural State logo beholdt

---

## ⏳ Gjenstående Oppgaver

### 1. Logo (Høy prioritet)
- [ ] Skaff Brødrene Evensen logo (PNG eller JPG)
- [ ] Lagre som `/public/images/brodrene-evensen-logo.png`
- [ ] Oppdater Header.tsx:
  - Fjern tekst-placeholder
  - Uncomment logo-kode
  - Oppdater href til korrekt nettside (hvis ikke brodreneevensen.no)

### 2. Fargepalett (Medium prioritet)
- [ ] Bekreft om Brødrene Evensen har spesifikk fargepalett
- [ ] Evt. oppdater `tailwind.config.ts` under `lokka` farger:
  ```ts
  lokka: {
    primary: '#2C5F2D',    // Mørk grønn
    secondary: '#97BC62',   // Lys grønn
    accent: '#F4A259',      // Oransje
    neutral: '#2D3748',
    light: '#F7FAFC',
  }
  ```

### 3. Eiendomsdata (Kritisk)
For hver eiendom Brødrene Evensen ønsker å legge til:

#### a) Forberedelser
- [ ] Liste over adresser med gnr/bnr
- [ ] Plaace-rapporter (PDF eller screenshots)
- [ ] Hero-bilder (fasadebilder)
- [ ] Kartutsnitt
- [ ] Aktør-CSV fra Plaace
- [ ] Eiendomsprofiltekst (historikk, beskrivelse)

#### b) Per eiendom
- [ ] Opprett eiendom-ID (eks: `rodelokka-33`)
- [ ] Opprett JSON fra template:
  ```bash
  cp src/data/eiendommer/template.json src/data/eiendommer/[id].json
  ```
- [ ] Fyll inn all data i JSON-filen
- [ ] Opprett bildemappe:
  ```bash
  mkdir -p public/images/[id]
  mkdir -p public/images/plaace/[id]
  ```
- [ ] Last opp bilder (hero.jpg, map.png, plaace-screenshots)
- [ ] Prosesser aktør-CSV:
  ```bash
  python scripts/process_aktor_csv.py [csv-file] [id]
  ```
- [ ] Valider data:
  ```bash
  npm run validate:data
  ```
- [ ] Test lokalt:
  ```bash
  npm run dev
  # Naviger til http://localhost:3000/eiendommer/[id]
  ```

### 4. Git & Deployment
- [ ] Installer dependencies:
  ```bash
  cd /Users/gabrielboen/place-analysis-brodreneevensen
  npm install
  ```
- [ ] Initialiser Git:
  ```bash
  git init
  git add .
  git commit -m "Initial commit: Brødrene Evensen portfolio platform"
  ```
- [ ] Opprett GitHub repo:
  ```bash
  gh repo create place-analysis-brodreneevensen --private --source=.
  git push -u origin main
  ```
- [ ] Deploy til Vercel:
  ```bash
  vercel link
  vercel --prod
  ```

---

## 📋 Template for ny eiendom

Se `docs/LEGG-TIL-EIENDOM.md` for detaljert guide.

**Minimal JSON-struktur:**
```json
{
  "id": "eiendom-id",
  "adresse": "Gateadresse 123",
  "gnr": 123,
  "bnr": 456,
  "beskrivelse": "Kort beskrivelse...",
  "heroImage": "/images/[id]/hero.jpg",
  "mapImage": "/images/[id]/map.png",
  "coordinates": {
    "lat": 59.9139,
    "lng": 10.7522
  },
  "plaaceData": {
    "rapportDato": "2025-11-18T00:00:00Z",
    "screenshots": [...],
    "nokkeldata": {...}
  },
  "tilleggsinfo": {...},
  "metadata": {...}
}
```

---

## 🚀 Quick Start Commands

```bash
# Installer dependencies
npm install

# Start utviklingsserver
npm run dev

# Valider eiendomsdata
npm run validate:data

# Bygg for produksjon
npm run build

# Type-checking
npm run type-check

# Linting
npm run lint:fix

# Formatering
npm run format
```

---

## 📞 Support

For spørsmål om plattformen, kontakt Natural State eller se dokumentasjon i `/docs`.

---

**Dato opprettet:** 2025-11-18
**Status:** Klar for eiendomsdata og logo
