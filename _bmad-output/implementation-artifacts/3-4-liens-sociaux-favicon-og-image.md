# Story 3.4: Liens sociaux, favicon et og-image

Status: ready-for-dev

## Story

En tant que visiteur ou personne qui recoit le lien du site,
je veux voir une identite propre dans l'onglet, le footer et les apercus sociaux,
afin que le portfolio paraisse finalise et partageable.

## Acceptance Criteria

1. Le favicon est visible dans l'onglet et coherent avec l'identite Ghilas.
2. Les meta Open Graph et Twitter sont completes et coherentes avec le contenu reel.
3. Une image `og-image` 1200x630 est referencee par une URL publique valide.
4. Les liens GitHub et LinkedIn reels sont visibles dans le footer.
5. Les liens sociaux s'ouvrent dans un nouvel onglet avec `rel="noopener noreferrer"`.
6. Le footer reste propre sur desktop et mobile.
7. Aucun placeholder `[username]`, `example.com`, ou domaine non choisi ne reste dans le code.

## Inputs requis avant implementation

- URL GitHub reelle.
- URL LinkedIn reelle.
- Domaine final ou URL Vercel finale.
- Titre et description sociaux definitifs.
- Fichier `og-image.jpg` final ou consigne explicite pour le generer.

## Tasks / Subtasks

- [ ] Verifier le favicon existant et l'ajuster uniquement si le nom/monogramme final change. (AC: 1)
- [ ] Completer/aligner les meta `og:title`, `og:description`, `og:url`, `og:image`, `twitter:*`. (AC: 2, 3)
- [ ] Ajouter ou verifier `og-image.jpg` a la racine du projet quand l'image est disponible. (AC: 3)
- [ ] Ajouter `.footer-social` entre `.footer-logo` et `.footer-email`. (AC: 4)
- [ ] Ajouter les liens GitHub/LinkedIn reels avec labels accessibles. (AC: 4, 5)
- [ ] Verifier que le CSS `.footer-social` et `.footer-social-link` existe et reste coherent mobile. (AC: 6)
- [ ] Rechercher les placeholders restants dans `index.html`. (AC: 7)

## Dev Notes

### Etat actuel

- Le favicon SVG inline existe deja dans le `<head>`: [index.html](</home/etud/Bureau/site vitrine/index.html:8>).
- Les meta OG/Twitter existent partiellement, mais `og:image` manque: [index.html](</home/etud/Bureau/site vitrine/index.html:10>).
- Le CSS des liens sociaux existe deja: [index.html](</home/etud/Bureau/site vitrine/index.html:323>).
- Le footer n'affiche pas encore les liens sociaux malgre le CSS: [index.html](</home/etud/Bureau/site vitrine/index.html:991>).

### Implementation cible

Head:

Mettre les valeurs finales dans les balises existantes:

- `og:title` et `twitter:title`: titre social definitif.
- `og:description` et `twitter:description`: description sociale definitive.
- `og:url`: URL publique finale du site.
- `og:image` et `twitter:image`: URL absolue de l'image sociale finale, par exemple l'URL publique du fichier `/og-image.jpg`.
- `og:type`: `website`.
- `twitter:card`: `summary_large_image`.

Footer:

Ajouter un bloc `.footer-social` avec les URL reelles fournies dans les inputs.
Chaque lien doit avoir:

- `target="_blank"`
- `rel="noopener noreferrer"`
- `aria-label="GitHub de Ghilas"` ou `aria-label="LinkedIn de Ghilas"`
- `class="footer-social-link"`

Remplacer les SVG inline par ceux deja proposes dans [stories-dev-ready.md](</home/etud/Bureau/site vitrine/_bmad-output/implementation-artifacts/stories-dev-ready.md:209>) ou utiliser des icones SVG simples en `currentColor`. Ne pas importer de librairie d'icones dans ce fichier unique.

### Guardrails implementation

- Ne pas pointer `og:image` vers un fichier absent en production.
- Ne pas utiliser d'URL locale ou relative si le partage social doit fonctionner hors site; preferer URL absolue du domaine final.
- Ne pas modifier le style global du footer sauf necessaire pour l'espacement.
- Ne pas changer les couleurs du favicon hors palette.
- Ne pas utiliser de blanc pur dans les SVG sociaux; `currentColor` doit heriter de `--color-muted`/`--color-gold`.

## Testing Requirements

- Ouvrir le site: favicon visible.
- Verifier `index.html`: aucun `[username]`, `[url]`, `domaine-final`, `example.com`.
- Tester les deux liens sociaux: nouvel onglet, URL correcte.
- Tester mobile 375px: footer sans chevauchement.
- Tester apercu social apres deploiement avec LinkedIn Post Inspector ou equivalent.

## References

- Epic 3.4 source: [stories-dev-ready.md](</home/etud/Bureau/site vitrine/_bmad-output/implementation-artifacts/stories-dev-ready.md:188>)
- Epic 3 planning: [epics-and-stories.md](</home/etud/Bureau/site vitrine/_bmad-output/planning-artifacts/epics-and-stories.md:39>)
- UX implementation guidelines meta: [ux-design-specification.md](</home/etud/Bureau/site vitrine/_bmad-output/planning-artifacts/ux-design-specification.md:733>)
- Design system: [DESIGN.md](</home/etud/Bureau/site vitrine/DESIGN.md:1>)

## Dev Agent Record

### Agent Model Used

TBD by dev agent.

### Debug Log References

### Completion Notes List

### File List
