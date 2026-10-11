# ⚔️ Bot FFG – Gestion des rôles & Guerres

Bot Discord simple et extensible pour gérer les vérifications de membres et les annonces de guerre.

---

## 🎯 Fonctionnalités

### Commande `/verif @utilisateur`
Réservée aux **Officiers**. Le bot propose ensuite des menus :

1. **Choix du type**
   - **FFG** → Tag `[FFG]` + rôle `recrue` ou `soldat`
   - **Personnalisé** → Tag libre `[XXX]` + rôle `allié` ou `mercenaire`

2. Dans tous les cas, le rôle **vérifié** est aussi donné.

### Bouton rouge « Vérification des soldats »
- Retire les rôles : `vérifié`, `recrue`, `soldat`, `allié`, `mercenaire`
- Retire le tag `[...]` du pseudo
- Les anciennes **recrues** et **soldats** reçoivent automatiquement le rôle **réserviste**
- Envoie un message bilingue (FR + EN) dans le **salon de notification** en mentionnant les personnes concernées pour leur demander de se re-vérifier
- Les **Officiers** ne sont jamais touchés

### Bouton vert « Nouvelle guerre »
- Demande le numéro X
- Envoie `-- War X --` dans les salons configurés

### Configuration des salons
- Bouton gris ou commande `/config-guerre`
- Menu multi-sélection des salons

---

## 📋 Rôles nécessaires sur le serveur

Crée ces rôles (noms exacts) :

| Rôle          | Utilisation                              |
|---------------|------------------------------------------|
| `Officier`    | Peut utiliser toutes les commandes/boutons |
| `vérifié`     | Donné à chaque vérification              |
| `recrue`      | Membres FFG débutants                    |
| `soldat`      | Membres FFG confirmés                    |
| `allié`       | Alliés                                   |
| `mercenaire`  | Mercenaires                               |
| `réserviste`  | Anciennes recrues après reset            |

> **Important** : le rôle du bot doit être **au-dessus** de tous ces rôles dans la liste des rôles du serveur.

---

## 🚀 Installation

### 1. Créer le bot Discord
1. Va sur https://discord.com/developers/applications
2. **New Application** → nomme-le
3. Onglet **Bot** → Add Bot
4. **Reset Token** → copie le token
5. Active **Server Members Intent**
6. Onglet **OAuth2 → URL Generator**
   - Scopes : `bot` + `applications.commands`
   - Permissions : Manage Roles, Manage Nicknames, Send Messages, Embed Links, Read Message History, View Channels, Use Application Commands
7. Invite le bot avec le lien généré

### 2. Récupérer les IDs
- **Client ID** : OAuth2 → General
- **Guild ID** : Clic droit sur le serveur (Mode développeur activé) → Copier l’identifiant

### 3. Lancer le bot

```bash
cd ffg-bot
npm install
```

Crée un fichier `.env` :

```env
DISCORD_TOKEN=ton_token
CLIENT_ID=ton_client_id
GUILD_ID=id_de_ton_serveur
```

Puis :

```bash
npm run register   # Enregistre les commandes slash
npm start          # Lance le bot
```

### 4. Hébergement 24/7
La solution la plus simple : **Railway.app**  
(Crée un projet → ajoute les 3 variables d’environnement → Deploy)

---

## 🎮 Utilisation

1. Dans un salon staff : `/panel` → le panneau permanent apparaît
2. Configure les salons de guerre avec le bouton gris
3. Vérifie un membre avec `/verif @pseudo`
4. Utilise les boutons selon les besoins

---

## 🛠️ Extensibilité

Le code est pensé pour être facilement modifiable :
- Nouvelles commandes → `register-commands.js` + `index.js`
- Nouveaux boutons → ajouter dans le panneau + gérer le `customId`
- Nouveaux rôles → ajouter les constantes en haut de `index.js`

---

## ❓ Problèmes courants

| Problème | Solution |
|---------|----------|
| Le bot ne change pas les rôles/pseudos | Son rôle doit être plus haut que les rôles qu’il gère |
| Les commandes n’apparaissent pas | Relance `npm run register` |
| Erreur de permissions | Vérifie les permissions du bot dans le salon |

Besoin d’aide ? Envoie-moi le message d’erreur exact.
