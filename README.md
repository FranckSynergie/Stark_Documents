# STARK VARG — Documentation App

Application web sécurisée hébergée sur GitHub Pages.

---

## 📁 Structure des fichiers

```
stark-docs-app/
├── index.html    ← Page de connexion (login)
├── app.html      ← Application principale (docs + sélecteur modèle)
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
6. Upload les 4 fichiers : `index.html`, `app.html`, `users.json`, `README.md`
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

## 🏍️ Sélection du modèle

À chaque connexion, l'utilisateur choisit sa version de moto :

| Bouton | Modèle | Type |
|--------|--------|------|
| **MX 1.0** | VARG MX version originale | Motocross |
| **MX 1.2** | VARG MX Gen 2 (2025) | Motocross |
| **EX** | VARG EX | Enduro |
| **SIM** | VARG SM / Supermoto | Supermoto |

Les documents affichés et les raccourcis s'adaptent automatiquement au modèle sélectionné. Le modèle est mémorisé pour la session. Pour changer de modèle, cliquer sur le badge rouge dans l'en-tête.

---

## 🔍 Mots-clés de recherche disponibles

| Catégorie | Mots-clés |
|-----------|-----------|
| **Suspension** | suspension, sag, fourche, amortisseur, réglage, fork, shock, ressort, spring, détente, compression, clicker |
| **Roues** | roue, roues, wheel, pneu, tyre, rayon, jante, rim, montage, démontage |
| **Freins** | frein, freins, brake, plaquette, disque, purge, liquide de frein, bleeding |
| **Plastiques** | plastique, carrosserie, garde-boue, fender, collant, sticker, décalque, kit graphique |
| **Chaîne** | chaîne, chain, pignon, couronne, sprocket, transmission, 520 |
| **Huile** | huile, oil, liquide, refroidissement, cooling, coolant, graisse, lubrifiant, vidange |
| **Batterie / Pile** | batterie, battery, chargeur, charger, pile, piles, autonomie, wh, cycle |
| **Réglages** | réglage, réglages, settings, app, bluetooth, mapping, puissance |
| **Remplacement** | remplacement, replace, montage, démontage, pièces, spare |
| **Dépannage** | dépannage, troubleshoot, panne, erreur, led, problème, reset |
| **Entretien** | entretien, maintenance, nettoyage, révision, lavage |

---

## 👤 Identifiants par défaut (10 comptes)

| # | Utilisateur | ID | Mot de passe |
|---|-------------|-----|-------------|
| 1 | Franck (admin) | `franck` | `Varg2025!` |
| 2 | Utilisateur 2 | `user2` | `Stark002!` |
| 3 | Utilisateur 3 | `user3` | `Stark003!` |
| 4 | Utilisateur 4 | `user4` | `Stark004!` |
| 5 | Utilisateur 5 | `user5` | `Stark005!` |
| 6 | Utilisateur 6 | `user6` | `Stark006!` |
| 7 | Utilisateur 7 | `user7` | `Stark007!` |
| 8 | Utilisateur 8 | `user8` | `Stark008!` |
| 9 | Utilisateur 9 | `user9` | `Stark009!` |
| 10 | Utilisateur 10 | `user10` | `Stark010!` |

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
- `role` : `admin` ou `user`

---

## 🔒 Sécurité

- Les mots de passe ne sont **jamais stockés en clair**
- La session expire à la **fermeture du navigateur** (sessionStorage)
- Le `users.json` est public sur GitHub Pages → ne pas y mettre de données sensibles
- Pour plus de sécurité : rendre le repo **privé** + activer GitHub Pages sur repo privé (nécessite GitHub Pro)

---

*Stark Future — starkfuture.com*
