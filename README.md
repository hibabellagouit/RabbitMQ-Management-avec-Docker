# Guide d'Installation et d'Utilisation de RabbitMQ avec Docker

## Objectif
Mettre en place RabbitMQ via Docker (gestion d'images), puis manipuler l'interface web pour créer un exchange, une queue, effectuer un binding, publier un message et lire les messages depuis la queue.

## Prérequis
- Docker installé (Docker Desktop sous Windows, ou Docker Engine sous Linux)
- Accès à Internet (pour télécharger l'image)
- Navigateur web

## 🚀 Installation et Configuration

### Étape 1 : Télécharger l'image Docker
```bash
docker pull rabbitmq:3.12.9-management
```

### Étape 2 : Lancer le conteneur
```bash
docker run -d \
  --hostname rabbit \
  --name rabbit-server \
  -p 15672:15672 \
  -p 5672:5672 \
  rabbitmq:3.12.9-management
```

**Explication des paramètres :**
- `-d` : exécution en arrière-plan (mode détaché)
- `--hostname rabbit` : nom d'hôte interne du serveur RabbitMQ
- `--name rabbit-server` : nom du conteneur
- `-p 15672:15672` : port pour l'interface web
- `-p 5672:5672` : port pour les connexions AMQP

### Étape 3 : Vérification
1. Ouvrir Docker Desktop
2. Vérifier que `rabbit-server` est en état "Running"
3. Vérifier que les ports 15672 et 5672 sont bien exposés

## 🌐 Accès à l'Interface Web
1. Ouvrir votre navigateur
2. Aller à : http://localhost:15672
3. S'authentifier avec :
   - **Username** : `guest`
   - **Password** : `guest`

## 🛠 Configuration de RabbitMQ

### Créer un Exchange
1. Aller dans l'onglet "Exchanges"
2. Cliquer sur "Add a new exchange"
3. Renseigner :
   - **Name** : `2iteExchange`
   - **Type** : `direct`
   - **Durability** : `Durable`
4. Cliquer sur "Add exchange"

### Créer une Queue
1. Aller dans "Queues"
2. Cliquer sur "Add a new queue"
3. Renseigner :
   - **Type** : `Classic`
   - **Name** : `2iteQueue`
   - **Durability** : `Durable`
4. Cliquer sur "Add queue"

### Effectuer un Binding
1. Retourner dans "Exchanges"
2. Cliquer sur "2iteExchange"
3. Aller à la section "Bindings"
4. Dans "Add binding from this exchange" :
   - **To queue** : sélectionner `2iteQueue`
   - **Routing key** : laisser vide ou définir une clé
5. Cliquer sur "Bind"

## 📨 Publier un Message
1. Toujours dans l'onglet de l'exchange "2iteExchange"
2. Aller à la section "Publish message"
3. Si vous avez utilisé une Routing key lors du binding, la spécifier ici
4. Entrer votre message dans le champ "Payload"
5. Cliquer sur "Publish message"

## 📥 Lire les Messages
1. Aller dans l'onglet "Queues"
2. Cliquer sur "2iteQueue"
3. Dans la section "Get messages", cliquer sur "Get Message(s)" pour voir les messages en attente

## ⚠️ Remarque Importante
- Si vous avez laissé le champ "Routing key" vide lors du binding, assurez-vous de la laisser vide lors de la publication
- Si vous avez défini une clé de routage (par exemple `rk.2ite`), utilisez la même clé lors de la publication

## 🔄 Commandes Utiles

### Arrêter le conteneur
```bash
docker stop rabbit-server
```

### Redémarrer le conteneur
```bash
docker start rabbit-server
```

### Supprimer le conteneur
```bash
docker rm rabbit-server
```

### Voir les logs du conteneur
```bash
docker logs rabbit-server
```
<img width="1162" height="982" alt="Design sans titre (1)" src="https://github.com/user-attachments/assets/7e81703e-b6a2-47cd-862c-02bd8d4cb392" />
<img width="1920" height="1080" alt="Design sans titre (2)" src="https://github.com/user-attachments/assets/4e46fb02-9714-4de7-a9da-ce667484092d" />
<img width="1920" height="1080" alt="Design sans titre (3)" src="https://github.com/user-attachments/assets/8cfade95-ae79-42f0-84aa-4eb9848af915" />

