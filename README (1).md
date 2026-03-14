# 🔍 PageVault — Mini moteur de recherche communautaire

Un moteur de recherche où chaque utilisateur peut publier ses propres pages HTML,
et où tout le monde peut les retrouver via une barre de recherche fuzzy.

---

## 📁 Structure du projet

```
pagevault/
├── index.html          ← L'application complète
├── firebase-config.js  ← Tes clés Firebase (à remplir)
├── firestore.rules     ← Règles de sécurité Firestore
└── README.md
```

---

## 🚀 Mise en place étape par étape

### 1. Créer le projet Firebase

1. Va sur [console.firebase.google.com](https://console.firebase.google.com)
2. Clique **Ajouter un projet** → donne un nom → Continuer
3. Désactive Google Analytics si tu veux → **Créer le projet**

---

### 2. Activer Firestore (base de données)

1. Dans le menu gauche → **Firestore Database**
2. Clique **Créer une base de données**
3. Choisis **Mode production** → Suivant
4. Sélectionne une région (ex: `europe-west1`) → **Activer**

---

### 3. Activer l'authentification Email/Mot de passe

1. Menu gauche → **Authentication** → **Commencer**
2. Onglet **Sign-in method**
3. Clique sur **E-mail/Mot de passe** → Active → **Enregistrer**

---

### 4. Récupérer la config Firebase

1. Menu gauche → ⚙️ **Paramètres du projet**
2. Scroll vers **Tes applications** → Clique sur `</>` (Web)
3. Enregistre l'app (nom au choix), **sans** activer Firebase Hosting
4. Copie le bloc `firebaseConfig` affiché

5. Ouvre `firebase-config.js` et colle tes valeurs :

```js
export const firebaseConfig = {
  apiKey:            "AIzaSy...",
  authDomain:        "mon-projet.firebaseapp.com",
  projectId:         "mon-projet",
  storageBucket:     "mon-projet.appspot.com",
  messagingSenderId: "123456789",
  appId:             "1:123456789:web:abc..."
};
```

---

### 5. Déployer les règles Firestore

**Option A — Via la console Firebase (plus simple) :**
1. Firestore → onglet **Règles**
2. Efface le contenu actuel
3. Colle le contenu du fichier `firestore.rules`
4. Clique **Publier**

**Option B — Via Firebase CLI :**
```bash
npm install -g firebase-tools
firebase login
firebase init firestore   # sélectionne ton projet
firebase deploy --only firestore:rules
```

---

### 6. Mettre le site sur GitHub Pages

#### a) Crée un dépôt GitHub
1. Va sur [github.com](https://github.com) → **New repository**
2. Nomme-le `pagevault` (ou ce que tu veux)
3. **Public** → Create repository

#### b) Push les fichiers

```bash
git init
git add .
git commit -m "🚀 Initial commit — PageVault"
git branch -M main
git remote add origin https://github.com/TON_USERNAME/pagevault.git
git push -u origin main
```

#### c) Activer GitHub Pages
1. Dépôt → **Settings** → **Pages**
2. Source : **Deploy from a branch**
3. Branch : `main` / `/ (root)` → **Save**
4. Ton site sera dispo en quelques minutes sur :
   `https://TON_USERNAME.github.io/pagevault/`

---

### 7. Autoriser ton domaine dans Firebase Auth

1. Firebase Console → **Authentication** → **Settings**
2. Onglet **Domaines autorisés**
3. Clique **Ajouter un domaine**
4. Ajoute : `TON_USERNAME.github.io`

> ⚠️ Sans cette étape, la connexion échouera depuis GitHub Pages.

---

## 🎮 Utilisation

### Mode Recherche
- Tape le nom d'une page dans la barre de recherche
- Les résultats s'affichent par correspondance (fuzzy search)
- Clique sur une carte pour voir la page en plein écran

### Mode Créateur
1. Clique sur **✦ Créateur** dans la nav
2. Crée un compte ou connecte-toi
3. Colle ton HTML dans la zone de texte
4. Donne un nom à ta page → **Publier**
5. Ta page est visible dans la recherche pour tous !

---

## 🔒 Sécurité

- Toutes les pages sont publiquement **lisibles**
- Seuls les utilisateurs **connectés** peuvent publier
- Chaque page est liée à son auteur par son UID
- Seul l'auteur peut **modifier ou supprimer** sa propre page
- Le HTML des pages s'exécute dans un `<iframe sandbox>` pour isoler le contenu

---

## 🛠️ Dépannage

| Problème | Solution |
|---|---|
| "auth/unauthorized-domain" | Ajoute ton domaine dans Firebase Auth → Domaines autorisés |
| "permission-denied" | Vérifie que les règles Firestore sont bien publiées |
| La recherche ne trouve rien | Les pages se chargent au démarrage ; recharge la page |
| Le HTML ne s'affiche pas | Vérifie que ton HTML est valide et complet |

---

## 📄 Licence

Projet libre, fais-en ce que tu veux !
