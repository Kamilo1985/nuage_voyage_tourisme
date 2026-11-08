# Nuage de destinations

Mini-activité FLE avec une question fixe et des séances indépendantes : chaque lancement crée un identifiant de séance, un nouveau QR code et un nuage vide. Les participants répondent sans créer de compte visible; l’application utilise l’authentification anonyme Firebase en arrière-plan.

**Question :** « Quelle est ta destination touristique préférée ? »

## Design

Inspiré du fichier de référence : fond gris clair `#f6f7f9`, texte `#333333`, en-tête dégradé corail `#ff5b63` → `#ff4a55`, accent `#ff5257`, cartes blanches arrondies, ombres douces et mise en page adaptée au téléphone.

## Mise en route

1. Créez un projet Firebase et une Realtime Database.
2. Dans Firebase Authentication, activez **Anonymous**.
3. Collez `database.rules.json` dans l’onglet **Realtime Database → Rules** et publiez les règles.
4. Enregistrez une application Web Firebase et copiez sa configuration dans `index.html`, dans `firebaseConfig`.
5. Dans GitHub, créez un dépôt vide, ajoutez `index.html` et `database.rules.json`, puis activez **Settings → Pages → Deploy from a branch → main / root**.
6. Ouvrez l’adresse GitHub Pages avec `?teacher=1`, puis cliquez sur **Nouvelle séance**. Les étudiants scannent le QR.

Exemple mode enseignant : `https://VOTRE-NOM.github.io/VOTRE-DEPOT/?teacher=1`

## Séparation des séances

Les réponses sont écrites sous `sessions/{id}/responses`. Le bouton **Nouvelle séance** génère une nouvelle clé aléatoire, donc les réponses antérieures ne sont pas chargées dans le nouveau nuage. **Terminer la séance** ferme l’accès d’écriture aux participants. Les réponses anciennes restent stockées dans Firebase; vous pouvez les supprimer manuellement dans la console si vous souhaitez les effacer.

## À savoir

- Firebase Anonymous Auth ne demande pas aux étudiants de créer un compte. Firebase crée un identifiant temporaire de usuario en arrière-plan.
- Le QR s’affiche à l’enseignant et est généré par un service QR externe à partir du lien de séance.
- Le projet est un prototype d’atelier. Quiconque détient le QR actif peut ajouter une réponse; utilisez-le seulement avec votre groupe.
- Les règles exigent une connexion anonyme et empêchent la lecture des sessions fermées. Protégez l’accès au compte Firebase de l’enseignant.
- La configuration client Firebase n’est pas un secret; la protection repose sur les règles de la base de données.
