# Stories — Prêtes pour le Développement
# Site Vitrine Ghilas

**Date** : 2026-05-08  
**Stack** : `index.html` unique — HTML + CSS + Vanilla JS  
**Principe** : On a déjà un prototype fonctionnel. On le met en ligne, on le remplit, on le soigne.

---

# EPIC 2 — Mise en ligne (~1h30)

---

## Story 2.1 — Git init + GitHub

**Tâches :**
```bash
cd "/home/etud/Bureau/site vitrine"
git init
git add index.html DESIGN.md CLAUDE.md .gitignore _bmad-output/
git commit -m "feat: portfolio prototype — watch assembly concept"
gh repo create ghilas-portfolio --public --source=. --push
```

**`.gitignore` à créer :**
```
.DS_Store
*.log
node_modules/
.env
```

**AC :**
- [ ] `git log` affiche le premier commit
- [ ] Le repo est visible sur github.com/[username]/ghilas-portfolio

**Estimation : 30 min**

---

## Story 2.2 — Branches + Vercel

**Tâches :**
```bash
# Créer branche develop
git checkout -b develop
git push -u origin develop
```

**Vercel (vercel.com) :**
```
1. "Add New Project" → Import ghilas-portfolio depuis GitHub
2. Framework Preset : Other
3. Build Command  : (vide)
4. Output Dir     : ./
5. Deploy → copier l'URL de preview
```

**Comment ça marche ensuite :**
- Travail sur `develop` → Vercel génère une URL de preview automatique
- `git merge develop main && git push` → Vercel déploie en production

**AC :**
- [ ] L'URL Vercel affiche le site avec toutes les animations
- [ ] Un push sur `develop` génère une URL de preview distincte

**Estimation : 30 min**

---

## Story 2.3 — Domaine personnalisé (optionnel)

**Tâches :**
```
1. Acheter ghilas.dev sur namecheap.com (~12€/an)
2. Vercel → Settings → Domains → Add "ghilas.dev"
3. Chez le registrar, configurer :
   A     @    76.76.21.21
   CNAME www  cname.vercel-dns.com
4. Attendre propagation DNS (15 min – 48h)
```

**AC :**
- [ ] https://ghilas.dev charge le site sans warning de sécurité
- [ ] http://ghilas.dev redirige automatiquement vers https://

**Estimation : 30 min (+ délai DNS)**

---

# EPIC 3 — Contenu réel (~5h30)

---

## Story 3.1 — Vrai contenu

**Éléments à collecter auprès de Ghilas, puis à remplacer dans `index.html` :**

| Element | Valeur actuelle (placeholder) | À remplacer par |
|---------|------------------------------|-----------------|
| `data-od-id="hero-eyebrow"` | "Portfolio · Design & Développement Web" | [à définir] |
| `data-od-id="hero-title"` | "l'artisan du web" | [à définir] |
| `data-od-id="s1-desc"` | "Chaque site repose sur..." | [vrai texte] |
| `data-od-id="s2-desc"` | "L'enveloppe reflète..." | [vrai texte] |
| `data-od-id="s3-desc"` | "Une interface claire..." | [vrai texte] |
| `data-od-id="s4-desc"` | "Le mouvement est invisible..." | [vrai texte] |
| `data-od-id="s5-desc"` | "Ce qui retient l'attention..." | [vrai texte] |
| `data-od-id="s6-desc"` | "Quand tout s'assemble..." | [vrai texte] |
| `data-od-id="reveal-sub"` | "Web Artisan · Depuis 2019" | [vraie année] |
| `data-od-id="foot-email"` | "contact@ghilas.dev" | [vrai email] |

**AC :**
- [ ] Zéro texte générique ou placeholder dans le site
- [ ] Les textes sur mobile ne débordent pas (tester à 375px)

**Estimation : 1h (+ temps de collecte contenu)**

---

## Story 3.2 — Section Projets

**Où l'insérer** : entre `#reveal` et `#contact` dans `index.html`

**HTML à ajouter :**
```html
<section id="projects" aria-labelledby="projects-heading">
  <p class="section-eyebrow" data-od-id="proj-eyebrow">Réalisations</p>
  <h2 class="section-title" id="projects-heading" data-od-id="proj-title">Projets récents</h2>
  <div class="projects-grid">
    <!-- Répéter pour chaque projet -->
    <article class="project-card" data-od-id="project-1">
      <div class="project-header">
        <h3 class="project-name" data-od-id="p1-name">[Nom du projet]</h3>
        <span class="project-year" data-od-id="p1-year">2024</span>
      </div>
      <p class="project-desc" data-od-id="p1-desc">[Description courte]</p>
      <ul class="project-stack" data-od-id="p1-stack">
        <li>React</li><li>Node.js</li>
      </ul>
      <a href="[url]" target="_blank" rel="noopener noreferrer"
         class="project-link" data-od-id="p1-link">Voir le projet →</a>
    </article>
  </div>
</section>
```

**CSS à ajouter dans `<style>` :**
```css
#projects { padding: 120px 64px; max-width: 1200px; margin: 0 auto; }
.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: var(--space-4);
  margin-top: var(--space-8);
}
.project-card {
  border: 1px solid var(--color-border);
  background: var(--color-bg-card);
  padding: var(--space-4);
  transition: border-color 400ms ease;
}
.project-card:hover { border-color: var(--color-gold-dark); }
.project-header { display: flex; justify-content: space-between; align-items: baseline; margin-bottom: 12px; }
.project-name { font-family: var(--font-display); font-size: 1.4rem; font-weight: 300; color: var(--color-cream); }
.project-year { font-size: 0.65rem; letter-spacing: 0.15em; color: var(--color-muted); }
.project-desc { color: var(--color-muted); font-size: 0.84rem; line-height: 1.7; margin-bottom: var(--space-2); }
.project-stack { display: flex; gap: 8px; flex-wrap: wrap; list-style: none; margin-bottom: var(--space-2); }
.project-stack li { font-size: 0.62rem; letter-spacing: 0.15em; text-transform: uppercase; color: var(--color-gold); border: 1px solid var(--color-gold-dark); padding: 3px 10px; }
.project-link { font-size: 0.72rem; letter-spacing: 0.1em; text-transform: uppercase; color: var(--color-gold); text-decoration: none; transition: color 300ms ease; }
.project-link:hover { color: var(--color-gold-light); }
@media (max-width: 1023px) { #projects { padding: 80px 32px; } }
@media (max-width: 599px)  { #projects { padding: 60px 20px; } }
```

**Nav — ajouter le lien Projets :**
```html
<li><a href="#projects" data-od-id="nav-projects">Projets</a></li>
```

**AC :**
- [ ] 3 à 6 projets affichés avec titre, description, stack, lien
- [ ] Grid responsive : 3 colonnes desktop, 2 tablette, 1 mobile
- [ ] Chaque lien s'ouvre dans un nouvel onglet

**Estimation : 2h**

---

## Story 3.3 — Formulaire de contact fonctionnel

**Option A — Formspree (le plus simple, 0 code backend) :**

```html
<!-- Remplacer <form id="contact-form"> par : -->
<form id="contact-form" action="https://formspree.io/f/[TON-ID]" method="POST" novalidate>
  <!-- Champs identiques, le JS reste le même pour l'UX -->
  <!-- Formspree gère l'envoi d'email -->
</form>
```

```javascript
// Remplacer le handler form dans le <script> par :
document.getElementById('contact-form').addEventListener('submit', async e => {
  e.preventDefault();
  const ok = document.getElementById('form-ok');
  const fd = new FormData(e.target);
  if (!fd.get('name')?.trim() || !fd.get('email')?.trim() || !fd.get('message')?.trim()) {
    ok.textContent = 'Veuillez remplir tous les champs.';
    ok.style.display = 'block';
    return;
  }
  const res = await fetch(e.target.action, {
    method: 'POST',
    body: fd,
    headers: { Accept: 'application/json' }
  });
  if (res.ok) {
    ok.textContent = 'Message reçu — je vous réponds dans les 24h.';
    ok.style.display = 'block';
    e.target.reset();
    setTimeout(() => { ok.style.display = 'none'; }, 6000);
  }
});
```

**Tâches :**
```
1. formspree.io → créer un compte gratuit
2. "New Form" → copier l'ID (ex: xpzgkrvw)
3. index.html → remplacer action du form
4. Tester : envoyer un vrai message, vérifier la réception email
```

**Anti-spam honeypot à ajouter dans le form :**
```html
<input type="text" name="_gotcha" style="display:none" tabindex="-1" aria-hidden="true">
```

**AC :**
- [ ] Ghilas reçoit l'email de test sur sa vraie adresse
- [ ] Le message de confirmation apparaît sans rechargement de page

**Estimation : 1h**

---

## Story 3.4 — Liens sociaux + favicon + og-image

**Favicon (dans `<head>`) :**
```html
<!-- Favicon SVG inline — lettre G or sur fond noir -->
<link rel="icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 32 32'><rect width='32' height='32' fill='%230a0a0a'/><text x='50%' y='50%' dominant-baseline='central' text-anchor='middle' font-family='serif' font-size='22' fill='%23c9a040'>G</text></svg>">
<meta name="theme-color" content="#c9a040">
```

**Open Graph (dans `<head>`, après `<title>`) :**
```html
<meta property="og:title" content="Ghilas — Web Artisan">
<meta property="og:description" content="Développeur & designer web. Chaque site est une œuvre de précision.">
<meta property="og:image" content="https://ghilas.dev/og-image.jpg">
<meta property="og:url" content="https://ghilas.dev">
<meta property="og:type" content="website">
<meta name="twitter:card" content="summary_large_image">
```

**Liens sociaux dans le footer :**
```html
<!-- Ajouter entre .footer-logo et .footer-email -->
<div class="footer-social">
  <a href="https://github.com/[username]" target="_blank" rel="noopener noreferrer"
     aria-label="GitHub de Ghilas" class="footer-social-link">
    <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor">
      <path d="M12 0C5.37 0 0 5.37 0 12c0 5.31 3.435 9.795 8.205 11.385.6.105.825-.255.825-.57 0-.285-.015-1.23-.015-2.235-3.015.555-3.795-.735-4.035-1.41-.135-.345-.72-1.41-1.23-1.695-.42-.225-1.02-.78-.015-.795.945-.015 1.62.87 1.845 1.23 1.08 1.815 2.805 1.305 3.495.99.105-.78.42-1.305.765-1.605-2.67-.3-5.46-1.335-5.46-5.925 0-1.305.465-2.385 1.23-3.225-.12-.3-.54-1.53.12-3.18 0 0 1.005-.315 3.3 1.23.96-.27 1.98-.405 3-.405s2.04.135 3 .405c2.295-1.56 3.3-1.23 3.3-1.23.66 1.65.24 2.88.12 3.18.765.84 1.23 1.905 1.23 3.225 0 4.605-2.805 5.625-5.475 5.925.435.375.81 1.095.81 2.22 0 1.605-.015 2.895-.015 3.3 0 .315.225.69.825.57A12.02 12.02 0 0 0 24 12c0-6.63-5.37-12-12-12z"/>
    </svg>
  </a>
  <a href="https://linkedin.com/in/[username]" target="_blank" rel="noopener noreferrer"
     aria-label="LinkedIn de Ghilas" class="footer-social-link">
    <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor">
      <path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433a2.062 2.062 0 0 1-2.063-2.065 2.064 2.064 0 1 1 2.063 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/>
    </svg>
  </a>
</div>
```

**CSS à ajouter :**
```css
.footer-social { display: flex; gap: 16px; align-items: center; }
.footer-social-link { color: var(--color-muted); transition: color 300ms ease; }
.footer-social-link:hover { color: var(--color-gold); }
```

**og-image.jpg :**
```
Créer une capture 1200×630px du hero avec la montre visible
Outil : navigateur en 1200px → screenshot → rogner → compresser < 200KB
```

**AC :**
- [ ] Favicon visible dans l'onglet
- [ ] Partage LinkedIn affiche l'og-image + titre + description
- [ ] Liens GitHub et LinkedIn fonctionnels

**Estimation : 1h**

---

# EPIC 4 — Polish & Lancement (~5h30)

---

## Story 4.1 — Navigation mobile (hamburger)

**HTML — modifier `<nav>` :**
```html
<nav id="navbar" aria-label="Navigation principale">
  <a href="#hero" class="nav-logo" data-od-id="nav-logo">Ghilas</a>
  <ul class="nav-links" id="nav-menu">
    <li><a href="#assembly" data-od-id="nav-approche">Approche</a></li>
    <li><a href="#projects" data-od-id="nav-projects">Projets</a></li>
    <li><a href="#contact" data-od-id="nav-contact">Contact</a></li>
  </ul>
  <a href="#contact" class="nav-cta" data-od-id="nav-cta">Parlons</a>
  <button class="nav-burger" aria-label="Menu" aria-expanded="false" aria-controls="nav-menu">
    <span></span><span></span><span></span>
  </button>
</nav>
```

**CSS à ajouter (dans le bloc `@media (max-width: 1023px)`) :**
```css
.nav-burger {
  display: flex; flex-direction: column; gap: 5px;
  background: none; border: none; cursor: pointer; padding: 8px;
}
.nav-burger span {
  width: 22px; height: 1px; background: var(--color-cream);
  transition: all 300ms var(--ease-luxury); display: block;
}
.nav-burger.open span:nth-child(1) { transform: rotate(45deg) translate(4px, 4px); }
.nav-burger.open span:nth-child(2) { opacity: 0; }
.nav-burger.open span:nth-child(3) { transform: rotate(-45deg) translate(4px, -4px); }
@media (max-width: 1023px) {
  .nav-burger { display: flex; }
  .nav-links {
    display: none; position: fixed;
    top: 0; right: 0; bottom: 0; width: 220px;
    background: var(--color-bg-subtle);
    flex-direction: column; justify-content: center;
    align-items: center; gap: 28px;
    border-left: 1px solid var(--color-border);
    z-index: 99;
  }
  .nav-links.open { display: flex; }
  .nav-links a { font-size: 0.85rem; }
}
```

**JS à ajouter dans `<script>` :**
```javascript
const burger = document.querySelector('.nav-burger');
const navMenu = document.getElementById('nav-menu');
burger?.addEventListener('click', () => {
  const open = burger.classList.toggle('open');
  navMenu.classList.toggle('open', open);
  burger.setAttribute('aria-expanded', open);
});
document.addEventListener('keydown', e => {
  if (e.key === 'Escape' && burger?.classList.contains('open')) {
    burger.classList.remove('open');
    navMenu.classList.remove('open');
    burger.setAttribute('aria-expanded', 'false');
  }
});
navMenu?.querySelectorAll('a').forEach(a => a.addEventListener('click', () => {
  burger.classList.remove('open');
  navMenu.classList.remove('open');
  burger.setAttribute('aria-expanded', 'false');
}));
```

**AC :**
- [ ] Sur mobile, le bouton hamburger apparaît et fonctionne
- [ ] Menu se ferme sur clic d'un lien ou touche Échap
- [ ] Sur desktop, le hamburger est invisible

**Estimation : 1h30**

---

## Story 4.2 — SEO de base

**Dans `<head>`, après `<title>` :**
```html
<meta name="description" content="Ghilas — Développeur & designer web. Portfolio de réalisations sur-mesure.">
<link rel="canonical" href="https://ghilas.dev">
```

**`robots.txt` — créer à la racine :**
```
User-agent: *
Allow: /
```

**AC :**
- [ ] Lighthouse SEO ≥ 90
- [ ] Meta description visible dans les résultats Google

**Estimation : 30 min**

---

## Story 4.3 — Tests cross-browser + cross-device

**Grille de test (remplir avant go-live) :**

| Test | Chrome | Firefox | Safari | Mobile Chrome |
|------|--------|---------|--------|---------------|
| Hero + animations entrée | ⬜ | ⬜ | ⬜ | ⬜ |
| Scroll assembly 6 étapes | ⬜ | ⬜ | ⬜ | ⬜ |
| Montre SVG + gradients | ⬜ | ⬜ | ⬜ | ⬜ |
| Aiguilles animées étape 6 | ⬜ | ⬜ | ⬜ | ⬜ |
| Nav hamburger mobile | — | — | — | ⬜ |
| Formulaire envoi | ⬜ | ⬜ | ⬜ | ⬜ |
| Layout 375px / 768px / 1440px | ⬜ | ⬜ | ⬜ | ⬜ |

**Outil** : Chrome DevTools → Device Toolbar (gratuit, suffisant)

**AC :**
- [ ] Toutes les cases cochées sans bug bloquant

**Estimation : 2h**

---

## Story 4.4 — Go-live + annonce

**Checklist finale :**
```
[ ] Vrai contenu partout (zéro placeholder)
[ ] Formulaire envoie un vrai email
[ ] Favicon visible
[ ] og-image visible sur partage LinkedIn
[ ] Tests cross-browser passés
[ ] HTTPS actif sur le domaine
[ ] Lighthouse Performance ≥ 85, SEO ≥ 90
```

**Annonce :**
```
[ ] Capture vidéo courte du scroll assembly (QuickTime, 15-20 sec)
[ ] Post LinkedIn avec l'URL + la vidéo + l'histoire du concept montre
[ ] Mettre à jour le bio GitHub avec l'URL
```

**Estimation : 1h30**

---

## Ordre d'exécution

```
Aujourd'hui  → Epic 2 : Git + GitHub + Vercel          (1h30)
Cette semaine → Epic 3 : Contenu + Projets + Formulaire (5h30)
Semaine pro  → Epic 4 : Hamburger + Tests + Go-live     (5h30)
```

**Total restant : ~12h**
