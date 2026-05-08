# DESIGN.md — Site Vitrine Montre (Ghilas)

## Agent Prompt Guide

Tu crées un site portfolio one-page pour Ghilas, développeur/designer web.
Le concept central est une montre fictive de luxe qui s'assemble composant
par composant au scroll. Style : dark luxueux inspiré de Rolex. Chaque
pixel doit inspirer confiance et excellence. Ne jamais utiliser de lorem ipsum.
Ne jamais inventer de couleurs hors palette. Respecter le layout 2 colonnes.

---

## Color Palette

| Token | Hex | Usage |
|-------|-----|-------|
| `--color-bg` | `#0a0a0a` | Fond principal |
| `--color-bg-subtle` | `#111111` | Variations de fond |
| `--color-bg-card` | `#141414` | Surfaces |
| `--color-gold` | `#c9a040` | Accent principal |
| `--color-gold-light` | `#e8c97a` | Reflets, halos |
| `--color-gold-dark` | `#8a6a20` | Or sombre |
| `--color-cream` | `#f5f0e8` | Texte principal |
| `--color-muted` | `#6b6b6b` | Texte secondaire |
| `--color-border` | `#1e1e1e` | Séparateurs |

**Règle** : fond noir, texte crème, accent or uniquement. Jamais de blanc pur, jamais de couleur saturée.

---

## Typography

**Display** : Cormorant Garamond (Google Fonts) — font-weight 300, letter-spacing 0.1–0.3em
**Body / UI** : Inter (Google Fonts) — font-weight 300–400

### Type Scale

| Rôle | Font | Size | Weight | Tracking |
|------|------|------|--------|---------|
| Hero | Cormorant | clamp(4rem, 8vw, 8rem) | 300 | 0.05em |
| Section title | Cormorant | clamp(2rem, 4vw, 3.5rem) | 300 | 0.1em |
| Step label | Inter | 0.7rem | 300 | 0.3em uppercase |
| Step title | Cormorant | clamp(1.5rem, 3vw, 2.5rem) | 300 | 0.08em |
| Body | Inter | 0.85rem | 300 | 0 |
| Nav | Inter | 0.7rem | 400 | 0.15em uppercase |
| CTA | Inter | 0.85rem | 400 | 0.1em uppercase |

---

## Layout

- **Max-width** : 1400px, centré
- **Grid** : 2 colonnes `1fr 1fr` sur desktop, 1 colonne sur mobile
- **Section height** : `min-height: 100vh` par étape d'assemblage
- **Colonne gauche** : sticky, texte narratif + numéro d'étape
- **Colonne droite** : montre SVG + halo animé, centré
- **Padding horizontal** : 64px desktop, 24px mobile

### Spacing System (base 8px)

```
--space-1: 8px
--space-2: 16px
--space-4: 32px
--space-8: 64px
--space-16: 128px
```

---

## Components

### NavBar
- Position fixed, top 0, full width
- Transparent sur hero → backdrop-filter blur(12px) après 80px de scroll
- Contenu : logo (Cormorant, crème) | liens (Inter, muted) | CTA (border or)

### WatchAssembly
- SVG inline, 6 layers superposés avec `data-watch-part="1"` à `"6"`
- Taille : 440px desktop, clamp(240px, 70vw, 380px) mobile
- Halo doré derrière : radial-gradient animé, pulse 3s infinite

### StepText
- `.step-number` : Cormorant 8rem, `--color-border` (discret, décoratif)
- `.step-label` : Inter 0.7rem uppercase, `--color-gold`
- `.step-title` : Cormorant, grand, `--color-cream`
- `.step-desc` : Inter 0.85rem, `--color-muted`, max 2 lignes

### ProgressBar
- 6 segments flex, hauteur 1px
- Couleur : `--color-border` → `--color-gold` au fur et à mesure

### CTAButton
- Border 1px `--color-gold`, fond transparent → or subtil au hover
- Padding 14px 40px, Inter uppercase, letter-spacing 0.15em
- Transition all 400ms ease

---

## Animation

```css
--ease-luxury: cubic-bezier(0.25, 0.1, 0.25, 1);
--duration-slow: 800ms;
--duration-medium: 400ms;
```

- Entrée composant : `opacity 0→1` + `translateY(20px→0)`, 700ms ease-luxury
- Halo pulse : scale 0.95→1.05, opacity 0.5→0.9, 3s infinite
- Reveal burst au nouveau composant : scale 1.2 éclat, 400ms
- Texte : fade-out 200ms avant fade-in du suivant

### Reduced Motion

```css
@media (prefers-reduced-motion: reduce) {
  * { animation: none !important; transition: opacity 300ms ease !important; }
}
```

---

## Responsive Behavior

| Breakpoint | Layout | Montre |
|------------|--------|--------|
| < 768px | 1 colonne, montre en haut | clamp(240px, 70vw, 300px) |
| 768px–1023px | 2 colonnes resserrées | 360px |
| ≥ 1024px | 2 colonnes `1fr 1fr` | 440px |
| ≥ 1440px | max-width 1400px centré | 480px |

---

## Depth & Elevation

Minimal. Pas de box-shadow génériques. Profondeur créée par :
- Contraste noir/or
- Le halo derrière la montre (radial-gradient)
- Bordures subtiles `--color-border` (1px)

---

## Scrollbar

```css
::-webkit-scrollbar { width: 2px; }
::-webkit-scrollbar-thumb { background: var(--color-gold); }
::-webkit-scrollbar-track { background: var(--color-bg); }
```
