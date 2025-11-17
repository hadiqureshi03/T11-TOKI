# UX Patterns - TOKI Website

Denne dokumentation beskriver de fire primære UX patterns der er implementeret på TOKI's website for at skabe en optimal brugeroplevelse.

## 1. Sticky Navbar

### Beskrivelse
Navigationsbjælken forbliver synlig øverst på skærmen, selv når brugeren scroller ned på siden. Dette sikrer konstant adgang til hovednavigationen.

### Implementering
Implementeret i [navbar.astro](src/components/navbar.astro)

**CSS Kode:**
```css
.navbar {
  position: sticky;
  top: 0;
  background-color: #FAF2E7;
  padding: 2rem 2rem;
  z-index: 1000;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  border-bottom: 2px solid #000;
}
```

### Hvorfor dette pattern?
- **Forbedret navigation:** Brugeren kan altid nemt finde tilbage til hovedsektioner uden at skulle scrolle helt til toppen
- **Bedre UX:** Reducerer antallet af klik og scrolling for at navigere rundt på sitet
- **Professionelt udtryk:** Moderne websites bruger sticky navigation som standard
- **Konsistent branding:** Logoet er altid synligt, hvilket styrker brand awareness

### Tekniske detaljer
- `position: sticky` gør elementet "klæber" til toppen når brugeren scroller forbi det
- `z-index: 1000` sikrer at navigationen ligger over alt andet indhold
- `box-shadow` tilføjer subtil dybde der adskiller navigation fra indhold
- Responsive breakpoints tilpasser padding og logo-størrelse på mindre skærme

---

## 2. Smooth Scrolling

### Beskrivelse
Når brugeren klikker på navigation links (f.eks. "WORK" eller "CONTACT"), scroller siden blidt ned til den relevante sektion i stedet for at "hoppe" direkte.

### Implementering
Implementeret gennem HTML anchor links og CSS scroll behavior

**HTML Eksempel:**
```html
<a href="#work">WORK</a>
<a href="#contact">CONTACT</a>
```

**CSS Global Style:**
```css
html {
  scroll-behavior: smooth;
}
```

### Hvorfor dette pattern?
- **Bedre brugeroplevelse:** Den bløde overgang gør det lettere for brugeren at orientere sig og følge med i hvor de befinder sig på siden
- **Reducerer desorientering:** Pludselige spring kan være forvirrende - smooth scrolling giver kontekst
- **Moderne standard:** Forventet funktionalitet på professionelle websites
- **Tilgængelighed:** Hjælper brugere med at forstå sidens struktur bedre

### Tekniske detaljer
- `scroll-behavior: smooth` aktiverer native browser smooth scrolling
- Fungerer automatisk med alle anchor links (#work, #contact, etc.)
- Browseren håndterer animationen, hvilket giver god performance
- Respekterer brugerens "prefers-reduced-motion" indstillinger for tilgængelighed

---

## 3. Hover Effect Overlay Pattern

### Beskrivelse
I Work Index sektionen vises et mørkt overlay med tekst når brugeren hover over et projekt. Overlayed "slider" op fra bunden af billedet.

### Implementering
Implementeret i [workindex.astro](src/components/workindex.astro)

**CSS Kode:**
```css
.work-item {
  position: relative;
  overflow: hidden;
  transition: transform 0.3s ease;
}

.work-item:hover {
  transform: scale(1.02);
}

.work-overlay {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  background: rgba(0, 0, 0, 0.7);
  padding: 1.5rem;
  transform: translateY(100%);
  transition: transform 0.3s ease;
}

.work-item:hover .work-overlay {
  transform: translateY(0);
}
```

### Hvorfor dette pattern?
- **Visuelt engagement:** Tiltræker opmærksomhed og inviterer til interaktion
- **Informationshierarki:** Holder billedet som primært fokus, men giver kontekst ved hover
- **Interaktiv feedback:** Bekræfter for brugeren at elementet er klikbart
- **Professionelt design:** Almindeligt brugt i portfolio og galleri-interfaces
- **Pladsbesparende:** Viser information kun når det er relevant (on-demand)

### Tekniske detaljer
- `transform: translateY(100%)` skjuler overlay under billedet initialt
- `transform: translateY(0)` slider overlayed op ved hover
- `transition: transform 0.3s ease` skaber den bløde animation
- `transform: scale(1.02)` giver en subtil zoom-effekt på hele kortet
- `position: absolute` og `overflow: hidden` sikrer at overlay ikke går uden for billedet

### Animation Timing
- **0.3 sekunder** er valgt som optimal hastighed:
  - Hurtigt nok til at føles responsivt
  - Langsomt nok til at være synligt og behageligt

---

## 4. Responsive Design

### Beskrivelse
Website'et tilpasser sig automatisk til forskellige skærmstørrelser - fra store desktop skærme til små mobile enheder. Layout, font-størrelser og spacing justeres dynamisk.

### Implementering
Implementeret gennem mobile-first CSS media queries i alle komponenter

**Breakpoints:**
```css
/* Desktop: Standard styling (ingen media query) */

/* Tablet og mindre */
@media (max-width: 1024px) {
  .work-grid {
    grid-template-columns: 1fr;
    gap: 2rem;
  }
}

/* Mobil */
@media (max-width: 768px) {
  .work-grid {
    grid-template-columns: repeat(2, 1fr);
    gap: 1rem;
  }
}

/* Lille mobil */
@media (max-width: 480px) {
  .work-grid {
    grid-template-columns: 1fr;
    gap: 1rem;
  }
}

/* Meget lille mobil */
@media (max-width: 360px) {
  .nav-container {
    flex-direction: column;
  }
}
```

### Hvorfor dette pattern?
- **Universal tilgængelighed:** Mere end 60% af web-trafik kommer fra mobile enheder
- **Bedre brugeroplevelse:** Optimeret layout for hver enhed type
- **SEO fordele:** Google prioriterer mobile-friendly websites
- **Professionel standard:** Forventet funktionalitet i moderne web design
- **Fremtidssikring:** Virker på nye enheder med forskellige skærmstørrelser

### Responsive Elementer

#### Navbar
- **Desktop:** Logo centreret, links på hver side
- **Tablet (768px):** Mindre padding, reduceret font-størrelse
- **Mobil (480px):** Kompakt layout, mindre logo
- **Meget lille (360px):** Stacked layout med logo øverst

#### Work Grid
- **Desktop:** 3 kolonner grid
- **Tablet (768px):** 2 kolonner grid
- **Mobil (480px):** 1 kolonne (fuld bredde)

#### Singleview Page
- **Desktop:** 2-kolonne layout (billeder til venstre, tekst til højre)
- **Tablet (1024px):** Stacked layout (billeder først, derefter tekst)
- **Mobil:** Optimerede font-størrelser og spacing

### Tekniske detaljer

**Fluid Typography:**
```css
font-size: clamp(2rem, 4vw, 3rem);
```
- Minimum: 2rem
- Foretrukken: 4% af viewport bredde
- Maximum: 3rem

**Flexible Images:**
```css
.work-image {
  width: 100%;
  height: auto;
  object-fit: cover;
}
```

**Container Constraints:**
```css
.container {
  max-width: 1400px;
  margin: 0 auto;
  padding: 0 2rem;
  width: 100%;
}
```

### Testede Devices
- Desktop (1920px+)
- Laptop (1366px - 1920px)
- Tablet (768px - 1024px)
- Mobil Landscape (480px - 768px)
- Mobil Portrait (320px - 480px)

---

## Samlet UX Strategi

Disse fire patterns arbejder sammen for at skabe en sammenhængende brugeroplevelse:

1. **Sticky Navbar** = Konstant navigation tilgængelighed
2. **Smooth Scrolling** = Behagelig navigation mellem sektioner
3. **Hover Overlays** = Interaktiv feedback og information on-demand
4. **Responsive Design** = Optimal oplevelse på alle enheder

### Performance Overvejelser
- CSS transitions bruger GPU-acceleration (`transform` frem for `top`/`left`)
- Minimale JavaScript dependencies (kun native browser features)
- Optimerede billeder med `object-fit` for hurtig load
- Mobile-first approach reducerer unødvendig CSS

### Tilgængelighed
- Respekterer `prefers-reduced-motion` for brugere der ikke ønsker animationer
- Tastatur navigation fungerer med alle interaktive elementer
- Kontrastforhold overholder WCAG 2.1 standarder
- Semantisk HTML for screen readers

### Browser Support
- Chrome/Edge (moderne versioner)
- Firefox (moderne versioner)
- Safari (moderne versioner)
- Mobile browsers (iOS Safari, Chrome Mobile)

---

**Dokumentation oprettet:** 2025
**Version:** 1.0
**Projekt:** TOKI - Sustainable Packaging Solutions
