# 🚀 Les Défis Bonus (Pour aller plus loin)

Bravo, vous avez terminé le workflow principal ! Vous avez désormais une automatisation qui lit votre CV et génère une lettre de motivation pertinente grâce à l'IA.

Si vous avez encore un peu de temps (ou si vous voulez simplement découvrir d'autres facettes de n8n), voici **deux défis Bonus**. Choisissez celui qui vous inspire le plus !

---

## 🏆 Bonus 1 : La notification Discord (Très visuel)
**Objectif :** Faire communiquer n8n avec Discord. Dès que votre lettre de motivation est créée dans Google Docs, un message récapitulatif est publié automatiquement sur un serveur Discord.

**Les étapes :**
1. Sur Discord (dans un serveur où vous avez les droits d'administration), créez un **Webhook** (Paramètres du serveur > Intégrations > Voir les Webhooks > Nouveau Webhook). Copiez l'**URL du Webhook**.
2. De retour sur n8n, ajoutez une nouvelle node **HTTP Request** à la toute fin de votre workflow.
3. Configurez cette node avec les paramètres suivants :
   - **Method** : `POST`
   - **URL** : *(Collez l'URL complète de votre Webhook Discord)*
   - Activez l'option **Send Body**
   - Ajoutez une valeur au **Body** contenant la clé `content` et le message de votre choix (Exemple: `"🎉 Ma lettre de motivation vient d'être générée !"`).
   > *Astuce : Vous pouvez utiliser les expressions dynamiques (ex: `{{ $json.output.objet }}`) dans le message pour le personnaliser comme vous l'avez fait pour le prompt AI !*
4. Cliquez sur **Test Workflow** et vérifiez que le bot s'est bien activé sur Discord.

---

## 🌐 Bonus 2 : Le générateur Multi-Langues (Avancé)
**Objectif :** Pousser l'agent IA à faire du traitement complexe. Pourquoi se contenter du Français ? Modifiez votre workflow pour que l'IA rédige la lettre de motivation et l'insère en **Français, Anglais et Espagnol** à la suite dans le même fichier Google Docs.

**Les étapes :**
1. Modifiez le **Prompt** de l'Agent IA qui gère le formatage. Demandez-lui explicitement de traduire la lettre originelle et séparez clairement la demande pour qu'il comprenne qu'il doit vous fournir 3 versions.
2. Modifiez la node **Structured Output Parser** pour qu'elle puisse réceptionner ce nouveau format. Son schéma devra attendre 3 blocs distincts (`fr`, `en`, `es`). Par exemple :
   ```json
   {
     "fr": { "objet": "String", "contenu": "String" },
     "en": { "objet": "String", "contenu": "String" },
     "es": { "objet": "String", "contenu": "String" }
   }
   ```
3. Dans la node **Update a document (Google Docs)**, ajoutez des actions **Insert** successives pour ajouter l'objet `fr` et le contenu `fr`, suivi de l'objet `en` et contenu `en`, etc. Pensez à rajouter des sauts de lignes pour que tout reste lisible !
4. Exécutez le workflow ! La magie de l'IA combinée à n8n devrait remplir instantanément le Google Doc avec vos 3 traductions.

> 💡 **En cas de blocage** : Pas de panique, les fichiers de correction `DISCORD_NOTIFICATION_WF.json` et `MULTI_LANG_WF.json` sont disponibles !