# STARK VARG — Documentation App

Application web sécurisée hébergée sur GitHub Pages.

---

## 📁 Structure des fichiers

```
stark-docs-app/
├── index.html    ← Page de connexion (login)
├── app.html      ← Application principale (docs)
├── users.json    ← Liste des utilisateurs (à gérer toi-même)
└── README.md
```

---

## 🚀 Déploiement sur GitHub Pages (1 fois)

1. Crée un compte sur **github.com** si tu n'en as pas
2. Clique sur **"New repository"**
3. Nom du repo : `stark-docs` (ou ce que tu veux)
4. Coche **"Public"** (requis pour GitHub Pages gratuit)
5. Clique **"Create repository"**
6. Upload les 3 fichiers : `index.html`, `app.html`, `users.json`
   - Bouton **"Add file" → "Upload files"**
7. Dans **Settings → Pages** :
   - Source : **"Deploy from a branch"**
   - Branch : **main** / dossier **/ (root)**
   - Clique **Save**
8. Ton URL sera : `https://TON-PSEUDO.github.io/stark-docs/`

> ⏱ Attends 1-2 minutes après le déploiement initial.

---

## 📲 Raccourci sur téléphone

### iPhone (Safari)
1. Ouvre `https://TON-PSEUDO.github.io/stark-docs/` dans **Safari**
2. Icône **Partager** (carré + flèche) → **"Sur l'écran d'accueil"**
3. Nom : **STARK DOCS** → Ajouter

### Android (Chrome)
1. Ouvre l'URL dans **Chrome**
2. Menu ⋮ → **"Ajouter à l'écran d'accueil"**

---

## 👤 Identifiants par défaut

| Utilisateur | ID       | Mot de passe |
|-------------|----------|-------------|
| Franck      | franck   | Varg2025!   |
| User 2      | user2    | Stark002!   |
| User 3      | user3    | Stark003!   |

**⚠️ Change les mots de passe après le premier accès !**

---

## ✏️ Modifier / Ajouter un utilisateur

Les mots de passe sont hashés en **SHA-256** avec le sel `stark_salt_2025`.

### Générer un nouveau hash (dans ton navigateur)

Ouvre la console DevTools (F12) et colle :

```javascript
async function hash(pwd) {
  const buf = await crypto.subtle.digest('SHA-256', new TextEncoder().encode(pwd + 'stark_salt_2025'));
  return Array.from(new Uint8Array(buf)).map(b => b.toString(16).padStart(2,'0')).join('');
}
hash('MonNouveauMotDePasse!').then(console.log);
```

Copie le hash généré et modifie `users.json` sur GitHub (bouton ✏️ crayon).

### Exemple users.json

```json
[
  {
    "id": "franck",
    "password": "HASH_ICI",
    "name": "Franck",
    "role": "admin"
  },
  {
    "id": "marie",
    "password": "HASH_ICI",
    "name": "Marie",
    "role": "user"
  }
]
```

### Champs disponibles
- `id` : identifiant de connexion (minuscules, sans espace)
- `password` : hash SHA-256 du mot de passe + sel
- `name` : prénom affiché dans l'app
- `role` : `admin` ou `user` (pour évolution future)

---

## 🔒 Sécurité

- Les mots de passe ne sont **jamais stockés en clair**
- La session expire à la **fermeture du navigateur** (sessionStorage)
- Le `users.json` est public sur GitHub Pages → ne pas y mettre de données sensibles
- Pour plus de sécurité : rendre le repo **privé** + activer GitHub Pages sur repo privé (nécessite GitHub Pro)

---

*Stark Future — starkfuture.com*
