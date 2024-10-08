# Exercice : 

## Synchronisation des Stocks avec une API Externe

**Contexte :**
Une entreprise fictive, **GlobalShop**, gère ses stocks dans Odoo mais souhaite synchroniser ses niveaux de stock avec
un système externe via une API REST. L'objectif est de créer un module Odoo personnalisé qui synchronise les quantités
de stock d'un produit entre Odoo et l'API externe.

**Objectifs :**
Votre tâche consiste à développer un module qui permet :

1. De récupérer les informations de stock depuis une API externe.
2. De mettre à jour automatiquement les quantités de stock dans Odoo en fonction des données de l'API.
3. D'afficher les informations de synchronisation dans l'interface d'Odoo.

### Détails de l'exercice :

1. **Création du Module :**
    - Créez un module Odoo personnalisé appelé `stock_sync_api`.
    - Le module doit permettre de synchroniser les quantités de stock pour chaque produit à partir d'une API externe.

2. **API Externe :**
    - Simulez une API REST qui retourne les informations de stock des produits sous le format JSON.
        - Exemple de réponse de l'API :
          ```json
          {
              "product_id": "123",
              "quantity": "50"
          }
          ```
    - Le candidat peut utiliser un service en ligne comme Postman pour simuler cette API ou un serveur local avec Flask
      par exemple.

3. **Modèle de Données :**
    - Ajoutez un champ dans le modèle `product.template` pour stocker l'ID externe du produit utilisé par l'API.
    - Ajoutez un champ pour suivre la dernière date de synchronisation.

4. **Intégration API :**
    - Créez une fonction dans le module qui appelle l'API externe pour récupérer les informations de stock d'un produit.
    - Comparez les quantités de stock récupérées avec celles d'Odoo.
    - Si les quantités diffèrent, mettez à jour les stocks dans Odoo.

5. **Vue Personnalisée :**
    - Modifiez la vue de produit pour inclure une section "API Synchronisation" avec :
        - L'ID externe du produit.
        - Le bouton pour "Lancer la synchronisation" manuellement.
        - La dernière date de synchronisation.

6. **Automatisation :**
    - Créez une tâche CRON (programmée) qui exécute la synchronisation de tous les produits de manière régulière (par
      exemple, toutes les heures).
    - Documentez comment le CRON peut être configuré et ajusté via Odoo.

7. **Gestion des Erreurs :**
    - Gérez les erreurs possibles lors de l'appel à l'API (erreur de connexion, réponse invalide, produit non trouvé).
    - Loggez les erreurs pour faciliter le débogage.

8. **Test et Documentation :**
    - Créez plusieurs cas de test pour valider :
        - Que la synchronisation fonctionne correctement (quantité mise à jour).
        - Que les erreurs sont bien gérées (ex. : appel à l'API échoue).
    - Documentez l'installation du module, l'utilisation du bouton de synchronisation manuelle et la configuration du
      CRON.

### Critères d'évaluation :

- Compétence dans l'intégration d'API externes avec Odoo.
- Capacité à créer et gérer des tâches CRON pour l'automatisation.
- Gestion des erreurs d'intégration.
- Structuration propre du module et organisation du code.
- Clarté de la documentation et capacité à tester les fonctionnalités développées.

### Ressources supplémentaires :

- Une instance Odoo avec le module de gestion de stock activé.
- Un environnement pour simuler ou accéder à une API REST.

---

# Local development

Build project

```shell
docker compose build
```

Start project

```shell
docker compose up
```

Destroy project

```shell
docker compose down -v
```


