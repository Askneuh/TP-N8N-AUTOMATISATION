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


## 🔍 3. Découverte de l'interface (15 min)

Une fois que vous arrivez sur l'interface, vous tombez sur la page qui répertorie tout vos workflows, si vous êtes vraiment nouveaux sur n8n, vous n'aurez encore aucun workflow.
Créez en un nouveau. Pour cela cliquez soit sur le bouton create workflow en haut a droite, soit sur le + en haut a gauche, puis workflow.
Vous accédez alors à l'espace de travail, appelé canva.
L'architecture d'un workflow se compose toujours d'un noeud de trigger (trigger node), qui active le flux, de noeuds d'actions, qui définissent ce que le workflow fait à chaque étape, et de flux de données qui circulent au fil des étapes.
Pour créer la trigger node, cliquez sur le + au milieu de votre écran, un onglet s'ouvrira à droite de votre écran et vous aurez le choix entre différentes nodes. Pour le premier exemple, sélectionner la node Trigger Manually, de sorte que vous puissiez lancer le workflow quand bon vous semble.
Pour ajouter une node d'action, cliquez sur le plus a droite de la trigger node. Dans le menu à droite, vous aurez le choix à une multitude d'actions différentes, passez quelques minutes pour explorer ce qu'il est possible de faire, nous n'aurons pas le temps de tout aborder.
Pour ce premier exemple, sélectionner le noeud Edit Field (vous pouvez le taper dans la barre de recherche). Comme le noeud est le premier du workflow et que le trigger ne fait passer aucune donnée, nous allons créer une variable a faire passer dans notre workflow. Ajoutez un champ de type String, et rentrez comme valeur quelque chose comme "Salut", n'oubliez pas de mettre un nom. Sortez de l'interface en appuyant sur échappe par exemple, et éxecuter le workflow. Vous ne devriez pas avoir d'erreur mais pour l'instant, rien de particulier ne se produit. Vous avez simplement créé un champ textuel et l'avez fait passé en output de votre node. Cliquez a nouveau sur le bouton + a droite de la node edit fields, et ajoutez a nouveau une node Edit Fields. Cette fois, dans l'onglet Input à gauche, vous devriez voir la variable que vous avez définie précédemment. Créez un champ textuel, et glissez la variable dans la valeur, puis ajoutez votre nom par exemple. Exécutez le workflow complet, vous pourrez voir s'afficher l'output final du workflow. Ceci était un exemple vraiment minimaliste de ce que l'on peut faire avec n8n, pour vous introduire les concepts essentiels. Il existe plein de nodes qui permettent d'interagir avec des applications comme google sheets, discord, telegram etc... et même avec des Agents IA. Un exercice permettant la création d'un workflow un peu plus complet vous est proposé par la suite.

---

## Mise en pratique

L'objectif de cet exercice est de créer un workflow qui récupère votre CV ainsi qu'une offre de stage/d'emploi, et qui vous rédige une lettre de motivation personnalisée. Les instructions seront moins précises que pour l'exemple de découverte, mais n'hésitez pas à nous appeler si vous avez la moindre question. Le code du workflow complet est aussi disponible sur github, sous format json, vous pouvez le télécharger et l'importer dans n8n si besoin.

La première étape consiste à récupérer votre CV et votre offre d'emploi. Cela peut se faire dans la trigger node. Ajoutez la trigger node n8n form à votre canva, et ajoutez deux form elements, un de type text, et un de type file. Ces éléments serviront pour récupérer respectivement l'offre d'emploi sous forme de texte, et le CV en pdf # ATTENTION JE CROIS QUE SI ON MET PAS EN PDF C BIZARRE. Pour l'élément CV, rajoutez l'attribut Accepted file, et rentrez .pdf, et nommez le label significativement. Vous pouvez aussi ajouter l'attribut required field.

Ensuite, nous voulons extraire les informations de votre CV, en effet, l'agent IA que nous utiliserons par la suite ne peut pas directement lire le pdf. Pour cela ajoutez la node Extract from File. Sélectionnez Extract From PDF, dans le champ input, glissez l'input du PDF. Ce noeud convertira le contenu du pdf en texte pour que l'agent puisse l'utiliser.
