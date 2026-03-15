# TP : Automatisation de Workflow avec n8n 🚀

## 🎯 Objectifs
- Comprendre les enjeux de l'automatisation.
- Déployer n8n via Docker.
- Créer un workflow capable de récupérer des données et d'envoyer une notification.

---

## 💎 1. Pourquoi automatiser ? (10 min)
Aujourd'hui, on utilise tous des dizaines d'outils : Gmail, Drive, Instagram, Discord, GitHub... Le souci, c'est que ces applications ne communiquent pas entre elles. Résultat : on passe un temps fou à faire du "copier-coller" manuel, à déplacer des fichiers ou à remplir des tableaux. C'est lent, c'est ennuyeux et c'est une perte de temps.
n8n est un outil qui permet de faire "communiquer" vos applications entre elles à travers des workflows.

L'automatisation permet de supprimer les tâches répétitives à faible valeur ajoutée (saisie de données, transferts d'emails, surveillance de prix). 

Il existe plusieurs outils d'automatisations, tels que Zapier ou Make, cependant, n8n se distingue par plusieurs critères :
- Le concept "Fair-Code" : n8n est auto-hébergeable (pas besoin de passer forcement par le cloud pour l'utiliser). Cela implique qu'il est possible de l'installer sur vos propres serveurs si vous en avez, ce qui peut réduire les coûts, et cela implique aussi qu'en se faisant, vous gardez un contrôle sur vos données.
- Le "Low-Code": Dans Zapier ou Make, on peut créer des workflows, mais on ne peut pas insérer des scripts, ce qui réduit le nombre de possibilités d'utilisation. Dans n8n, on peut injecter des scripts JavaScript ou Python pour plus de flexibilité.

# TODO : rédiger
Automatiser une tâche de 10 minutes par jour fait gagner 60 heures par an.
---

## 🛠 2. Installation de n8n en self-host avec Docker (20 min)

### Prérequis
Avoir docker sur sa machine

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

