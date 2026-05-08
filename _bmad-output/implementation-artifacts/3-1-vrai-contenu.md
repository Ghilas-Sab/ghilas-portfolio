# Story 3.1: Vrai contenu

Status: ready-for-dev

## Story

En tant que visiteur professionnel,
je veux lire un contenu reel et specifique a Ghilas,
afin de comprendre rapidement son positionnement, ses services et pourquoi le contacter.

## Acceptance Criteria

1. Aucun texte generique ou placeholder ne reste visible dans le site.
2. Les textes remplacent les contenus actuels sans casser la narration de la montre en 6 etapes.
3. Les textes restent lisibles et sans debordement a 375px, 768px, 1024px et 1440px.
4. L'adresse email affichee dans le footer et les CTA/contact correspond a la vraie adresse de Ghilas.
5. La page conserve le style dark luxe: fond noir, texte creme, accent or, typographies existantes.

## Inputs requis avant implementation

- Hero eyebrow definitif.
- Hero title definitif, avec choix explicite de conserver ou non le saut de ligne et le `<em>`.
- Texte court pour chacune des 6 etapes d'assemblage.
- Baseline finale sous la signature: metier + vraie annee de debut.
- Email de contact reel.

## Tasks / Subtasks

- [ ] Inventorier les textes actuels dans [index.html](</home/etud/Bureau/site vitrine/index.html:407>). (AC: 1)
- [ ] Remplacer les textes relies a `data-od-id`: `hero-eyebrow`, `hero-title`, `s1-desc` a `s6-desc`, `reveal-sub`, `foot-email`. (AC: 1, 2, 4)
- [ ] Verifier que chaque description d'etape reste courte: idealement 1 phrase, max 2 lignes desktop. (AC: 2, 3)
- [ ] Conserver les labels et titres d'etapes si le nouveau contenu ne demande pas explicitement leur changement. (AC: 2)
- [ ] Mettre a jour l'attribut `href="mailto:..."` du footer en meme temps que le texte visible. (AC: 4)
- [ ] Tester les largeurs 375px, 768px, 1024px, 1440px; corriger uniquement les tailles/largeurs necessaires si un texte deborde. (AC: 3)

## Dev Notes

### Etat actuel

- Le site est un fichier unique: [index.html](</home/etud/Bureau/site vitrine/index.html:1>).
- Le contenu principal commence au hero: [index.html](</home/etud/Bureau/site vitrine/index.html:407>).
- Les 6 textes d'etapes sont dans `.step-desc`: [index.html](</home/etud/Bureau/site vitrine/index.html:888>).
- Le footer contient deja un email placeholder `contact@ghilas.dev`: [index.html](</home/etud/Bureau/site vitrine/index.html:993>).
- La navigation, l'animation de montre et le formulaire existent deja; cette story ne doit pas les refondre.

### Contraintes design

- Respecter strictement les tokens de [DESIGN.md](</home/etud/Bureau/site vitrine/DESIGN.md:9>): noir, creme, or, aucune couleur externe.
- Le projet doit rester en HTML/CSS/Vanilla JS, sans framework ni dependance de composant. Source: [ux-design-specification.md](</home/etud/Bureau/site vitrine/_bmad-output/planning-artifacts/ux-design-specification.md:262>).
- Le contenu doit soutenir la metaphore "artisan du web" et l'assemblage de la montre. Source: [ux-design-specification.md](</home/etud/Bureau/site vitrine/_bmad-output/planning-artifacts/ux-design-specification.md:45>).

### Guardrails implementation

- Ne pas ajouter de section, de carte, de modal ou de nouveau CTA dans cette story.
- Ne pas modifier le SVG de la montre.
- Ne pas changer les animations `IntersectionObserver` sauf si un test responsive prouve un debordement lie au texte.
- Ne jamais laisser `[a definir]`, lorem ipsum, ou formulation generique type "solutions digitales innovantes".
- Si une information manque, garder la story bloquee cote contenu plutot que d'inventer.

## Testing Requirements

- Verification manuelle dans le navigateur a 375px, 768px, 1024px, 1440px.
- Verification par recherche texte dans `index.html`: aucun `[`, `placeholder`, `a definir`, `Lorem`.
- Test du lien email: `mailto:` pointe vers la vraie adresse.
- Scroll complet: les 6 etapes restent visibles et la montre s'assemble jusqu'au reveal.

## References

- Epic 3.1 source: [stories-dev-ready.md](</home/etud/Bureau/site vitrine/_bmad-output/implementation-artifacts/stories-dev-ready.md:50>)
- Epic 3 planning: [epics-and-stories.md](</home/etud/Bureau/site vitrine/_bmad-output/planning-artifacts/epics-and-stories.md:36>)
- UX content principles: [ux-design-specification.md](</home/etud/Bureau/site vitrine/_bmad-output/planning-artifacts/ux-design-specification.md:37>)
- Design system: [DESIGN.md](</home/etud/Bureau/site vitrine/DESIGN.md:1>)

## Dev Agent Record

### Agent Model Used

TBD by dev agent.

### Debug Log References

### Completion Notes List

### File List

