# FlowRange — Prérequis participants

> À lire et installer **avant la formation**. Comptez 15-20 minutes.
> Si vous rencontrez un problème, contactez l'équipe avant le jour J.

---

## Ce dont vous avez besoin

| Outil | Version minimale | Vérification |
|---|---|---|
| Visual Studio Code | 1.95+ | `code --version` |
| Extension GitHub Copilot | Dernière version | Voir ci-dessous |
| .NET SDK | 9.0+ | `dotnet --version` |
| Node.js | 20 LTS+ | `node --version` |
| npm | 10+ | `npm --version` |
| Git | 2.40+ | `git --version` |

---

## Étape 1 — Visual Studio Code

Téléchargez et installez VS Code depuis [https://code.visualstudio.com](https://code.visualstudio.com).

**Vérification :** Ouvrez un terminal et tapez :
```bash
code --version
```
Vous devez voir un numéro de version (ex: `1.98.0`).

---

## Étape 2 — Extension GitHub Copilot

1. Ouvrez VS Code
2. Allez dans l'onglet Extensions (`Ctrl+Shift+X`)
3. Cherchez **"GitHub Copilot"**
4. Installez l'extension **GitHub Copilot** (éditeur : GitHub) — elle installe aussi GitHub Copilot Chat automatiquement

**Connexion :** Au premier lancement, VS Code vous demandera de vous connecter avec votre compte GitHub. Assurez-vous d'avoir une licence Copilot active (compte personnel ou licence entreprise fournie par Expertime/Orange).

**Vérification :** L'icône Copilot doit apparaître dans la barre de statut en bas de VS Code (icône GitHub).

---

## Étape 3 — .NET SDK 9

Téléchargez depuis [https://dotnet.microsoft.com/download](https://dotnet.microsoft.com/download) — choisissez **.NET 9 SDK**.

**Vérification :**
```bash
dotnet --version
# Attendu : 9.0.x
```

---

## Étape 4 — Node.js 20 LTS

Téléchargez depuis [https://nodejs.org](https://nodejs.org) — choisissez la version **LTS (20.x)**.

**Vérification :**
```bash
node --version
# Attendu : v20.x.x ou supérieur

npm --version
# Attendu : 10.x.x ou supérieur
```

---

## Étape 5 — Git

Téléchargez depuis [https://git-scm.com](https://git-scm.com).

**Vérification :**
```bash
git --version
# Attendu : git version 2.4x.x
```

---

## Étape 6 — Vérification complète

Copiez et exécutez ce bloc dans un terminal pour tout vérifier d'un coup :

```bash
echo "=== Vérification prérequis FlowRange ===" && \
echo "VS Code : $(code --version | head -1)" && \
echo ".NET SDK : $(dotnet --version)" && \
echo "Node.js : $(node --version)" && \
echo "npm : $(npm --version)" && \
echo "Git : $(git --version)" && \
echo "=== Tout est prêt ! ==="
```

---

## Extensions VS Code recommandées

Installez ces extensions pour être dans les meilleures conditions :

```
GitHub Copilot               (obligatoire)
GitHub Copilot Chat          (obligatoire — installée avec Copilot)
C# Dev Kit                   (ms-dotnettools.csdevkit)
Vue - Official               (Vue.volar)
Tailwind CSS IntelliSense    (bradlc.vscode-tailwindcss)
```

Pour les installer en une commande :
```bash
code --install-extension ms-dotnettools.csdevkit
code --install-extension Vue.volar
code --install-extension bradlc.vscode-tailwindcss
```

---

## En cas de problème

- **GitHub Copilot ne s'active pas** : vérifiez que votre compte GitHub a une licence Copilot active sur [https://github.com/settings/copilot](https://github.com/settings/copilot)
- **.NET SDK non reconnu** : redémarrez votre terminal après l'installation
- **Node.js non reconnu** : redémarrez votre terminal, ou vérifiez que le PATH a été mis à jour par l'installateur

Contactez l'équipe de formation si un problème persiste avant la session.
