# Qu’est-ce qu’on a ? — stock de la coloc

Site hébergé gratuitement sur **GitHub Pages**, données dans **Firebase Firestore** (offre gratuite Spark, sans carte bancaire), connexion avec Google.

Compte environ 20 minutes la première fois.

## Contenu du dossier

| Fichier | Rôle |
|---|---|
| `index.html` | L’appli entière (stock, recettes, courses) |
| `firebase-config.js` | Les identifiants de ton projet Firebase, à compléter |
| `firestore.rules` | Qui a le droit de lire et modifier les données |

## 1. Créer le projet Firebase

1. Va sur https://console.firebase.google.com et clique sur **Créer un projet**. Google Analytics n’est pas utile, tu peux le désactiver.
2. Dans le menu **Build › Firestore Database**, clique sur **Créer une base de données**. Choisis une région en Europe (par exemple `eur3` ou `europe-west1`), puis le **mode production**.
3. Dans **Build › Authentication**, clique sur **Commencer**, puis active le fournisseur **Google**.
4. Dans **⚙️ Paramètres du projet › Général**, descends jusqu’à **Vos applications**, clique sur l’icône **</>** (Web), donne un nom à l’appli. Pas besoin de Firebase Hosting.
5. Firebase affiche un objet `firebaseConfig`. Copie ses valeurs dans `firebase-config.js`.

## 2. Protéger les données

1. Ouvre `firestore.rules` et remplace les adresses d’exemple par les adresses Gmail de toute la coloc, en minuscules.
2. Dans la console, va dans **Firestore Database › Règles**, colle tout le contenu du fichier à la place de l’existant, puis clique sur **Publier**.

Sans cette étape, personne ne peut accéder aux données (le mode production bloque tout). Pour ajouter un coloc plus tard, ajoute son adresse dans la liste et republie les règles.

## 3. Mettre le site en ligne sur GitHub Pages

1. Crée un compte sur https://github.com si tu n’en as pas.
2. Clique sur **New repository**, nomme-le par exemple `stock-coloc`, laisse-le **Public** (GitHub Pages est gratuit pour les dépôts publics) et crée-le.
3. Clique sur **uploading an existing file** et glisse `index.html`, `firebase-config.js` et `firestore.rules`. Valide avec **Commit changes**.
4. Dans **Settings › Pages**, sous **Branch**, choisis `main` et le dossier `/ (root)`, puis **Save**.
5. Après une minute, ton site est disponible à l’adresse `https://TON-PSEUDO.github.io/stock-coloc/`.

Le dépôt est public, mais ça ne pose pas de problème : la configuration Firebase n’est pas un secret, et les données restent protégées par les règles de l’étape 2.

## 4. Autoriser l’adresse du site dans Firebase

Dans **Authentication › Settings › Authorized domains**, clique sur **Add domain** et ajoute `TON-PSEUDO.github.io`.

Sans ça, la connexion Google affiche une erreur `auth/unauthorized-domain`.

## 5. Sur les téléphones

Ouvre l’adresse du site, connecte-toi avec Google, puis ajoute la page à l’écran d’accueil :

- **iPhone** : bouton Partager de Safari › **Sur l’écran d’accueil**.
- **Android** : menu ⋮ de Chrome › **Ajouter à l’écran d’accueil**.

L’appli garde une copie du stock sur le téléphone : si le réseau est mauvais au supermarché, tu vois quand même la dernière version, et les modifications sont envoyées au retour du réseau.

## Modifier l’appli plus tard

Sur GitHub, ouvre `index.html`, clique sur le crayon ✏️, modifie, puis **Commit changes**. Le site se met à jour en une minute environ.

## Dépannage

- **« Le compte … n’est pas sur la liste de la coloc »** : l’adresse n’est pas dans `firestore.rules`, ou les règles n’ont pas été publiées.
- **La fenêtre Google ne s’ouvre pas depuis l’icône de l’écran d’accueil sur iPhone** : connecte-toi une fois depuis Safari, puis réessaie depuis l’icône. Si ça bloque toujours, utilise un favori Safari plutôt que l’icône.
- **Page blanche** : vérifie que `firebase-config.js` est bien dans le même dossier que `index.html` sur GitHub et que tu as remplacé toutes les valeurs `A_REMPLACER`.

## Limites de l’offre gratuite (à vérifier sur firebase.google.com/pricing)

Firestore Spark : 1 Gio de stockage, 50 000 lectures, 20 000 écritures et 20 000 suppressions par jour. Pour une coloc, vous resterez très loin de ces limites. Si un quota est dépassé, l’appli s’arrête jusqu’au lendemain ; rien n’est facturé tant que tu restes sur Spark.
