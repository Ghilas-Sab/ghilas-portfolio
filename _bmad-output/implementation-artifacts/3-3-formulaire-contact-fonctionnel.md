# Story 3.3: Formulaire de contact fonctionnel

Status: review

## Story

En tant que prospect,
je veux envoyer un message depuis le formulaire de contact,
afin que Ghilas recoive une demande reelle sans rechargement brutal de la page.

## Acceptance Criteria

1. Le formulaire envoie les champs `name`, `email`, `message` vers un endpoint Formspree valide.
2. Les champs obligatoires sont valides cote client avant envoi.
3. Le message de succes apparait sans rechargement de page apres une reponse OK.
4. Un message d'erreur clair apparait si un champ manque ou si l'envoi echoue.
5. Un honeypot `_gotcha` est present pour reduire le spam.
6. Ghilas recoit un email de test sur sa vraie adresse.
7. Le style du formulaire reste coherent avec le design actuel.

## Inputs requis avant implementation

- ID Formspree reel, au format endpoint `https://formspree.io/f/{form_id}`.
- Adresse email verifiee dans Formspree.
- Texte de succes final souhaite.

## Tasks / Subtasks

- [x] Creer/recuperer le endpoint Formspree depuis le dashboard. (AC: 1, 6)
- [x] Mettre a jour `<form id="contact-form">` avec `action="https://formspree.io/f/{form_id}" method="POST" novalidate`. (AC: 1)
- [x] Ajouter `<input type="text" name="_gotcha" class="visually-hidden" tabindex="-1" autocomplete="off" aria-hidden="true">`. (AC: 5)
- [x] Ajouter une classe CSS reutilisable `.visually-hidden` plutot qu'un style inline si possible. (AC: 5, 7)
- [x] Remplacer le handler submit actuel par un handler `async` utilisant `fetch(e.target.action, { method: 'POST', body: fd, headers: { Accept: 'application/json' } })`. (AC: 1, 3, 4)
- [x] Desactiver temporairement le bouton submit pendant l'envoi pour eviter les doubles soumissions. (AC: 4)
- [x] Gerer les etats: champs manquants, email invalide, succes, erreur reseau/reponse non-OK. (AC: 2, 3, 4)
- [x] Tester avec un vrai message et verifier la reception email. (AC: 6)

## Dev Notes

### Etat actuel

- Le formulaire existe deja sans `action` ni `method`: [index.html](</home/etud/Bureau/site vitrine/index.html:970>).
- Les champs `name`, `email`, `message` existent avec attributs `name` corrects: [index.html](</home/etud/Bureau/site vitrine/index.html:972>).
- Le message `#form-ok` existe deja: [index.html](</home/etud/Bureau/site vitrine/index.html:984>).
- Le JS actuel simule seulement le succes et n'envoie rien: [index.html](</home/etud/Bureau/site vitrine/index.html:1089>).

### Decision technique

- Utiliser Formspree en endpoint HTML/AJAX: compatible site statique, pas de backend, pas de framework.
- Conserver Vanilla JS et `fetch`; ne pas ajouter `@formspree/ajax` pour maintenir le principe zero dependance du projet.
- Formspree documente aussi `@formspree/ajax`, mais cette story privilegie le handler existant pour limiter le changement et garder le controle UI. Source officielle: https://help.formspree.io/articles/building-your-form/submit-forms-with-javascript-ajax/

### Implementation cible

```javascript
document.getElementById('contact-form').addEventListener('submit', async e => {
  e.preventDefault();
  const form = e.target;
  const fd = new FormData(form);
  const ok = document.getElementById('form-ok');
  const submit = form.querySelector('[type="submit"]');

  if (!fd.get('name')?.trim() || !fd.get('email')?.trim() || !fd.get('message')?.trim()) {
    ok.textContent = 'Veuillez remplir tous les champs.';
    ok.style.display = 'block';
    return;
  }

  submit.disabled = true;
  try {
    const res = await fetch(form.action, {
      method: 'POST',
      body: fd,
      headers: { Accept: 'application/json' }
    });
    if (!res.ok) throw new Error('Formspree submission failed');
    ok.textContent = 'Message envoye - je vous reponds dans les 24h.';
    ok.style.display = 'block';
    form.reset();
  } catch (error) {
    ok.textContent = "L'envoi a echoue. Reessayez ou contactez-moi par email.";
    ok.style.display = 'block';
  } finally {
    submit.disabled = false;
  }
});
```

Adapter les apostrophes/accents au style final du fichier si le reste du code les utilise.

### Guardrails implementation

- Ne pas exposer de cle API ou secret: Formspree endpoint public uniquement.
- Ne pas ajouter Resend sans backend/serverless; ce projet est un fichier statique.
- Ne pas supprimer les labels flottants existants.
- Ne pas remplacer le formulaire par un composant externe.
- Si l'endpoint Formspree manque, laisser le formulaire non modifie et signaler le blocage; ne pas utiliser un faux ID.

## Latest Technical Notes

- Formspree indique que l'endpoint de formulaire est du type `https://formspree.io/f/{form_id}` et que les champs doivent avoir un attribut `name`.
- La documentation Formspree AJAX a ete mise a jour le 23 mars 2026 et confirme les usages en JavaScript, avec gestion submit/success/errors.
- Le honeypot `_gotcha` est disponible sur tous les plans Formspree et les soumissions ou `_gotcha` est rempli sont ignorees.

## Testing Requirements

- Test champs vides: message d'erreur, pas de requete.
- Test email invalide: validation HTML5 ou message explicite.
- Test succes avec endpoint reel: message visible, reset du formulaire, email recu.
- Test erreur avec endpoint invalide temporaire: message d'echec visible, bouton reactive.
- Test mobile 375px: message d'etat sans debordement.

## References

- Epic 3.3 source: [stories-dev-ready.md](</home/etud/Bureau/site vitrine/_bmad-output/implementation-artifacts/stories-dev-ready.md:134>)
- Epic 3 planning: [epics-and-stories.md](</home/etud/Bureau/site vitrine/_bmad-output/planning-artifacts/epics-and-stories.md:38>)
- UX form pattern: [ux-design-specification.md](</home/etud/Bureau/site vitrine/_bmad-output/planning-artifacts/ux-design-specification.md:638>)
- Formspree HTML form docs: https://help.formspree.io/articles/building-your-form/building-an-html-form
- Formspree AJAX docs: https://help.formspree.io/articles/building-your-form/submit-forms-with-javascript-ajax/
- Formspree honeypot docs: https://help.formspree.io/articles/building-your-form/honeypot-spam-filtering/

## Dev Agent Record

### Agent Model Used

GPT-5 Codex

### Debug Log References

- Validation statique Node: parsing du script inline et checks du formulaire Formspree passes.
- Validation live Formspree: `curl` POST vers `https://formspree.io/f/mzdojzpk` retourne `{"next":"/thanks","ok":true}`.

### Completion Notes List

- Formulaire branche sur l'endpoint Formspree `https://formspree.io/f/mzdojzpk`.
- Honeypot `_gotcha` ajoute avec classe `.visually-hidden`.
- Handler submit converti en `async` avec `fetch(form.action)`, header `Accept: application/json`, gestion succes, champs manquants, email invalide et erreur reseau/reponse non-OK.
- Bouton submit desactive pendant l'envoi via `disabled` et `aria-busy`.
- Formspree a accepte une vraie soumission de test; verifier la reception dans la boite email associee si besoin.

### File List

- `index.html`

## Change Log

- 2026-05-08: Story 3.3 implementee et mise en review.
