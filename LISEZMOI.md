# Cartes mentales de séance : installation

Application web (GitHub Pages) avec connexion par email et mot de passe (Google Firebase, gratuit).
Seuls les comptes que vous validez peuvent l'utiliser.

## Contenu du dossier

| Fichier | Rôle |
|---|---|
| `index.html` | L'application |
| `firebase-config.js` | Les clés de votre projet Firebase (à remplir) |
| `firestore.rules` | Les règles de sécurité (à coller dans Firebase) |

Tant que `firebase-config.js` n'est pas rempli, l'application tourne en **mode démo** (sans connexion).

---

## Étape 1 : créer le projet Firebase (une seule fois)

1. Allez sur https://console.firebase.google.com et connectez-vous avec votre compte Google.
2. Cliquez sur **Créer un projet**, nommez-le par exemple `cartes-mentales`. Google Analytics n'est pas nécessaire.
3. Sur la page d'accueil du projet, cliquez sur l'icône **Web `</>`**, donnez un nom (ex. `site`), puis cliquez sur **Enregistrer l'application**.
   Ne cochez pas « Firebase Hosting ».
4. Firebase affiche un bloc `const firebaseConfig = { apiKey: "...", ... }`.
   Copiez ces 6 valeurs dans `firebase-config.js` à la place des `A_REMPLACER`.

## Étape 2 : activer la connexion par email

1. Menu de gauche : **Créer > Authentication**, puis **Commencer**.
2. Onglet **Méthode de connexion**, choisissez **Adresse e-mail/Mot de passe**, activez le premier interrupteur et enregistrez.
3. Onglet **Paramètres > Domaines autorisés**, cliquez sur **Ajouter un domaine** : `votre-nom.github.io`.

## Étape 3 : créer la base de données et coller les règles

1. Menu : **Créer > Firestore Database**, puis **Créer une base de données**.
   Choisissez un emplacement (ex. `europe-west`) et le **mode production**.
2. Onglet **Règles** : effacez tout, collez le contenu de `firestore.rules` et cliquez sur **Publier**.

## Étape 4 : créer VOTRE compte administrateur

1. **Authentication > Utilisateurs > Ajouter un utilisateur** : votre email et votre mot de passe.
2. **Firestore Database > Données > Commencer une collection**.
   - ID de la collection : `autorises`
   - ID du document : votre email **en minuscules** (ex. `prenom.nom@exemple.ma`)
   - Champs (type *string*) : `role` = `admin`, `nom` = votre nom, `ecole` = votre école
   - Cliquez sur **Enregistrer**.

## Étape 5 : mettre en ligne sur GitHub Pages

1. Sur GitHub, créez un dépôt public (ex. `cartes-mentales`).
2. **Add file > Upload files** : déposez `index.html`, `firebase-config.js` (rempli) et `firestore.rules`, puis **Commit changes**.
3. **Settings > Pages > Branch : `main` / `(root)` > Save**.
4. Après environ une minute, l'adresse est `https://votre-nom.github.io/cartes-mentales/`.

> Les clés de `firebase-config.js` peuvent être publiques : c'est prévu par Firebase.
> La sécurité vient des règles Firestore et de la liste des comptes validés.

---

## Utilisation au quotidien (administrateur)

Connectez-vous et ouvrez l'onglet **Utilisateurs** :

- **Valider un enseignant** : saisissez son email, un mot de passe (bouton « Générer »), son nom et son école, puis cliquez sur **Créer et valider le compte**.
  Utilisez ensuite **Copier les identifiants** pour les lui envoyer.
- **Retirer l'accès** : le compte est bloqué tout de suite, même si la personne connaît son mot de passe.
- **Lien mot de passe** : la personne reçoit un email pour choisir un nouveau mot de passe.
- Vous pouvez aussi désactiver ou supprimer un compte dans **Authentication > Utilisateurs**.

Le nom et l'école de l'enseignant sont remplis automatiquement sur ses nouvelles cartes.
Chaque enseignant ne voit que ses propres séances. Elles sont enregistrées en ligne et accessibles depuis n'importe quel appareil.

## Coût

Avec le plan gratuit Spark, Firebase couvre largement quelques centaines d'enseignants.
Aucune carte bancaire n'est demandée.
