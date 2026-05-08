# Story 3.2: Section Projets

Status: ready-for-dev

## Story

En tant que prospect,
je veux voir 3 a 6 realisations concretes de Ghilas,
afin d'evaluer rapidement son niveau, son style et la pertinence de le contacter.

## Acceptance Criteria

1. Une section `#projects` est ajoutee entre `#reveal` et `#contact`.
2. La section affiche 3 a 6 projets avec nom, annee, description courte, stack et lien.
3. La grille est responsive: 3 colonnes desktop si l'espace le permet, 2 tablette, 1 mobile.
4. Chaque lien projet s'ouvre dans un nouvel onglet avec `target="_blank"` et `rel="noopener noreferrer"`.
5. La navigation contient un lien `Projets` vers `#projects`.
6. L'ajout ne casse ni le reveal final, ni le CTA contact, ni le scroll smooth existant.

## Inputs requis avant implementation

Pour chaque projet:

- Nom du projet.
- Annee.
- Description en 1 a 2 phrases courtes.
- Stack technique.
- URL publique ou decision explicite d'afficher un projet sans lien.

## Tasks / Subtasks

- [ ] Inserer `<section id="projects" aria-labelledby="projects-heading">` entre `</section>` de `#reveal` et `#contact`. (AC: 1)
- [ ] Ajouter le heading, l'eyebrow et `.projects-grid` selon les conventions existantes. (AC: 1, 2)
- [ ] Creer 3 a 6 `<article class="project-card">`, chacun avec `h3`, annee, description, stack, lien. (AC: 2, 4)
- [ ] Ajouter le CSS `.projects-grid`, `.project-card`, `.project-*` dans le `<style>` existant. (AC: 3)
- [ ] Ajouter `Projets` dans `.nav-links` et garder `Contact` accessible. (AC: 5)
- [ ] Verifier que `document.querySelectorAll('a[href^="#"]')` continue de gerer le scroll smooth pour `#projects`. (AC: 6)
- [ ] Tester desktop/tablette/mobile et corriger les espacements sans changer la palette. (AC: 3, 6)

## Dev Notes

### Etat actuel

- `#reveal` se termine avant `#contact`: [index.html](</home/etud/Bureau/site vitrine/index.html:952>).
- `#contact` commence juste apres: [index.html](</home/etud/Bureau/site vitrine/index.html:965>).
- La nav actuelle contient `Approche`, `A propos`, `Contact`: [index.html](</home/etud/Bureau/site vitrine/index.html:384>).
- Le JS de smooth anchor cible deja tous les liens `href^="#"`: [index.html](</home/etud/Bureau/site vitrine/index.html:1117>).
- `.section-eyebrow`, `.section-title`, `.btn-primary` existent deja et doivent etre reutilises.

### Structure recommandee

```html
<section id="projects" aria-labelledby="projects-heading">
  <p class="section-eyebrow" data-od-id="proj-eyebrow">Realisations</p>
  <h2 class="section-title" id="projects-heading" data-od-id="proj-title">Projets recents</h2>
  <div class="projects-grid">
    <article class="project-card" data-od-id="project-1">
      <div class="project-header">
        <h3 class="project-name" data-od-id="p1-name">Nom du projet</h3>
        <span class="project-year" data-od-id="p1-year">2026</span>
      </div>
      <p class="project-desc" data-od-id="p1-desc">Description courte.</p>
      <ul class="project-stack" data-od-id="p1-stack">
        <li>HTML</li>
        <li>CSS</li>
        <li>JS</li>
      </ul>
      <a href="https://example.com" target="_blank" rel="noopener noreferrer" class="project-link" data-od-id="p1-link">Voir le projet</a>
    </article>
  </div>
</section>
```

### Contraintes design

- Garder la section sobre et dense; pas de layout marketing, pas de grande hero secondaire.
- Utiliser `--color-bg-card`, `--color-border`, `--color-gold`, `--color-muted`, `--color-cream`.
- Les cartes peuvent avoir une bordure 1px et un hover or discret; pas d'ombre generique.
- Ne pas mettre de cartes imbriquees.
- Garder les textes scannables: descriptions courtes, stack en tags fins.

### Guardrails implementation

- Ne pas importer de librairie de grille ou de framework CSS.
- Ne pas deplacer `#contact`; ajouter seulement `#projects` avant lui.
- Ne pas remplacer le lien nav `Contact`; ajouter `Projets` et ajuster l'ordre si besoin.
- Si un projet n'a pas encore d'URL, utiliser un texte non cliquable ou bloquer l'implementation; ne pas inventer une URL.

## Testing Requirements

- Test responsive a 375px, 768px, 1024px, 1440px.
- Test clic nav `Projets`: scroll vers la section.
- Test clic projets: ouverture nouvel onglet, pas d'erreur console.
- Verification clavier: Tab atteint les liens projets dans un ordre logique.

## References

- Epic 3.2 source: [stories-dev-ready.md](</home/etud/Bureau/site vitrine/_bmad-output/implementation-artifacts/stories-dev-ready.md:77>)
- Epic 3 planning: [epics-and-stories.md](</home/etud/Bureau/site vitrine/_bmad-output/planning-artifacts/epics-and-stories.md:37>)
- UX navigation patterns: [ux-design-specification.md](</home/etud/Bureau/site vitrine/_bmad-output/planning-artifacts/ux-design-specification.md:648>)
- Design system: [DESIGN.md](</home/etud/Bureau/site vitrine/DESIGN.md:1>)

## Dev Agent Record

### Agent Model Used

TBD by dev agent.

### Debug Log References

### Completion Notes List

### File List

