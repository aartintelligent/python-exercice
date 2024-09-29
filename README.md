### Exercice : Développement d'une API avec gestion d'événements, base de données et RabbitMQ

**Contexte**  
Vous allez développer une application API qui reçoit des événements au format JSON via une requête HTTP, les stocke dans une base de données, génère un identifiant unique pour chaque événement, et publie ces événements dans une file d'attente RabbitMQ. Cette API doit également ajouter une date d'événement et un UID unique avant la publication.

### Objectif général
Développer une API RESTful capable de :
1. Recevoir des événements au format JSON.
2. Enregistrer ces événements dans une base de données.
3. Générer un UID unique pour chaque événement.
4. Publier ces événements dans une queue RabbitMQ avec l'UID et un horodatage.

### Détails de l'Exercice

1. **Route API** :
   - Vous devez créer une route `POST /api/event/{solution}/{model}/{action}`.
   - Cette route doit recevoir un body au format JSON avec les données de l'événement.
   - La route doit générer un **UID unique** pour chaque événement avant de le publier.
   - La route doit ajouter un champ `event_timestamp` contenant la date de l'événement en format UTC.

2. **Stockage dans la base de données** :
   - Enregistrer l'UID généré ainsi que les données de l'événement dans une base de données relationnelle (par exemple, PostgreSQL ou SQLite).
   - La base de données doit contenir au moins les champs suivants :
     - `event_uid` : UID unique généré pour l'événement.
     - `event_timestamp` : Horodatage de l'événement.
     - `event_data` : Les données JSON reçues.

3. **Gestion de RabbitMQ** :
   - Publier les messages dans une queue RabbitMQ définie par le chemin `{solution}/{model}/{action}`. Par exemple, si l'URL est `/api/event/ecommerce/order/create`, le message doit être publié dans une queue nommée `ecommerce/order/create`.
   - Le message publié doit suivre le format suivant :

   ```json
   {
     "event_uid": "xxxxxxxxxxxxxxxxxxxxxxxxx",
     "event_timestamp": "2024-09-25T12:34:56Z",
     "event_data": {
       "order_id": 12345,
       "customer": "John Doe",
       "total_amount": 250
     }
   }
   ```

4. **Validation des entrées** :
   - Vérifier que le body de la requête contient un JSON valide.
   - Valider la présence des champs clés requis dans le body et les paramètres URL (`solution`, `model`, `action`, etc.).

5. **Réponses HTTP** :
   - Retourner un statut HTTP 200 avec un message de succès si le message est publié avec succès.
   - Retourner un statut HTTP 400 en cas d'erreurs de validation (ex. : JSON invalide).
   - Retourner un statut HTTP 500 en cas d'échec de la publication dans RabbitMQ ou de l'enregistrement dans la base de données.

6. **Tests unitaires** :
   - Écrire des tests unitaires pour valider la fonctionnalité de l'API, incluant la validation des données, la génération de l'UID, et la gestion des erreurs.

### Exemples

**Requête :**

```
POST /api/event/ecommerce/order/create
Content-Type: application/json

{
    "order_id": 12345,
    "customer": "John Doe",
    "total_amount": 250
}
```

**Réponse attendue :**

```json
{
    "message": "Event published to queue ecommerce/order/create",
    "status": "success"
}
```

**Message publié dans RabbitMQ :**

```json
{
    "event_uid": "b7e23ec29af22b0b4e41da31e868d57226121c84",
    "event_timestamp": "2024-09-25T12:34:56Z",
    "event_data": {
      "order_id": 12345,
      "customer": "John Doe",
      "total_amount": 250
    }
}
```

### Contraintes techniques
- Utiliser **Flask** ou **FastAPI** pour développer l'API.
- Utiliser **pika** pour interagir avec RabbitMQ.
- Utiliser une base de données relationnelle (PostgreSQL, MySQL, ou SQLite).
- Documentez le code, incluant la configuration nécessaire pour RabbitMQ et la base de données.

### Bonus
- Vous pouvez configurer l'API et RabbitMQ via **docker-compose** afin de faciliter le déploiement.
- Implémenter une stratégie de retry en cas de défaillance lors de la publication dans RabbitMQ.

### Critères d'évaluation
- **Qualité du code** : Structure, lisibilité et organisation du projet.
- **Fonctionnalité** : L'API fonctionne correctement, les événements sont bien publiés dans RabbitMQ et enregistrés dans la base de données.
- **Robustesse** : Gestion correcte des erreurs et des cas limites.
- **Tests** : Qualité et couverture des tests unitaires.

Bonne chance et n’hésitez pas à poser des questions si nécessaire !
