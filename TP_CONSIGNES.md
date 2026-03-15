# TP : Automatisation de Workflow avec n8n 🚀

## 🎯 Objectifs
- Comprendre les enjeux de l'automatisation.
- Déployer n8n via Docker.
- Créer un workflow capable de récupérer des données et d'envoyer une notification.

---

## 💎 1. Pourquoi automatiser ? (10 min)
*Note : Discussion rapide ou lecture.*
L'automatisation permet de supprimer les tâches répétitives à faible valeur ajoutée (saisie de données, transferts d'emails, surveillance de prix). 
**n8n** se distingue par :
- Son approche **Self-hosted** (protection des données).
- Sa flexibilité **Low-code** (nœuds visuels + JavaScript).

---

## 🛠 2. Installation avec Docker (20 min)

### Prérequis
Assurez-vous que Docker Desktop est lancé sur votre machine.

### Lancement de l'instance
Ouvrez un terminal et collez la commande suivante :
\`\`\`bash
docker run -it --rm \
  --name n8n \
  -p 5678:5678 \
  -v ~/.n8n:/home/node/.n8n \
  docker.n8n.io/n8nio/n8n
\`\`\`

Une fois le conteneur démarré, accédez à l'interface sur : `http://localhost:5678`

---

## 🔍 3. Découverte de l'interface (15 min)
* **Trigger nodes :** Comment le workflow démarre (ex: Heure fixe, Webhook, Email reçu).
* **Action nodes :** Ce que le workflow fait (ex: Envoyer un message, Créer un fichier).
* **Data flow :** Observez comment le JSON passe d'un nœud à l'autre.

---

## 🚀 4. Exercice : Créer une veille Bitcoin -> Discord (40 min)

### Étape 1 : Le déclencheur
Ajoutez un nœud **Schedule Trigger**...

### Étape 2 : L'appel API
Ajoutez un nœud **HTTP Request**. 
- **URL :** `https://api.coindesk.com/v1/bpi/currentprice.json`
- **Méthode :** GET

### Étape 3 : La condition
Ajoutez un nœud **IF**. Comparez le prix actuel à un seuil de $60,000.

### Étape 4 : La notification
Utilisez le nœud **Discord** (via Webhook) pour envoyer le message en cas de succès.

---

## 🆘 5. Dépannage (Troubleshooting)
- **Erreur de port :** Si le port 5678 est déjà pris, changez `-p 5678:5678` en `-p 8080:5678`.
- **Docker Permission :** Sur Linux, n'oubliez pas le `sudo`.
- **JSON non défini :** Vérifiez que vous avez bien exécuté le nœud précédent pour avoir des données de test.

---

## ✅ Validation
Pour valider le TP, exportez votre workflow au format JSON et soumettez-le.
