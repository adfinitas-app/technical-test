# Test technique backend

## Objectif :
L'objectif de ce test est d'évaluer vos compétences en développement backend, en particulier dans la création de deux serveurs utilisant Express.js et Redis pour le traitement de calculs reçus via des requêtes POST.

## Instructions :
Développez deux serveurs un en Express.js pour recevoir les requêtes POST contenant des calculs à effectuer et un autre qui utilise les Pub/Sub de Redis pour traiter les calculs en utilisant une file d'attente.
1. Un **collecteur** qui reçoit les requêtes POST contenant des calculs à effectuer (uniquement 2 opérandes) et les stocke dans une file d'attente pour être traitées ultérieurement
2. Un **processeur** qui traite les tâches en utilisant un système de file d'attente.
3. Créer un README-RUN.md pour expliquer comment exécuter le projet.

Bonus : 
1. Utilisez Docker pour exécuter les serveurs. 

## Spécifications techniques :
### Collecteur :
1. Le **collecteur** doit être développé en utilisant Express.js.
2. Il doit être capable de recevoir des requêtes POST à l'endpoint `/compute`.
3. Chaque requête POST doit contenir un objet JSON avec les données du calcul à effectuer. Par exemple :
    ```json
    {
        "operation": "addition", // ou "substract", "multiply", "divide"
        "operands": [5, 3] // Les deux opérandes
    }
    ```
4. Le **collecteur** doit inclure une route POST qui stocke les tâches dans une file d'attente pour traitement ultérieur. Par exemple :   
      ```typescript
   app.post('/compute', async (req, res) => {
       // Stocker la tâche dans une file d'attente
      return res.json({status: "ok"});
   })
   ```   
5. Le **collecteur** doit être en mesure de comprendre et de traiter différents types d'opérations mathématiques telles que l'addition, la soustraction, la multiplication et la division.
6. Utiliser les clés suivantes dans "operation" pour les différentes opérations :

   | Operation | Description                       |
   |-----------|-----------------------------------|
   | add       | Addition des deux opérandes       |
   | substract | Soustraction des deux opérandes   |
   | multiply  | Multiplication des deux opérandes |
   | divide    | Division des deux opérandes       |

7. Le **collecteur** doit stocker les tâches dans une file d'attente Redis pour traitement ultérieur.
8. Le **collecteur** doit renvoyer une réponse JSON avec un statut "ok" pour chaque requête POST reçue.
9. Le **collecteur** doit être capable de gérer les erreurs et de renvoyer une réponse JSON avec un statut "error" en cas d'erreur.
10. Le **collecteur** doit être capable de gérer les erreurs de validation des données et de renvoyer une réponse JSON avec un statut "error" en cas d'erreur de validation.



### Processeur
1. Le **processeur** doit être développé en utilisant le subscriber Redis pour traiter les tâches stockées dans une file d'attente
      ```typescript
   await subscriber.subscribe('task', async (message) => {
       // Traiter le message
   })
   ```
2. Il doit être capable de récupérer les tâches à traiter depuis une file d'attente.
3. Il doit valider les données reçues et effectuer les calculs demandés.
4. Une fois qu'une tâche est traitée, le **processeur** doit renvoyer le résultat calculé dans la réponse à la requête POST.
5. Si une erreur se produit lors du traitement d'une tâche, le processeur doit mettre à jour le statut de la tâche ainsi que stocker le message d'erreur dans le champ result.

### Interface des données :
Vous pouvez utiliser ces interfaces pour définir les types de données dans votre code.
```typescript
interface Operands {
    [key: string]: (operand1: number, operand2: number) => number;
}

interface Compute {
    operation: string;
    operand: number[];
}

interface Task {
    id: string;
    compute: Compute;
    result: number | string;
    status: "success" | "failed" | "pending";
}
```


---

## Fichiers du projet

1. **Collector (collector.ts)** : Ce fichier contient le code pour le collecteur qui reçoit les requêtes POST et les stocke dans Redis pour traitement ultérieur.
2. **Processor (processor.ts)** : Ce fichier contient le code pour le processeur qui traite les tâches en utilisant Redis comme système de file d'attente.
3. Bonus : **Dockerfile-proc** : Ce fichier contient les instructions pour créer une image Docker contenant le code du collecteur et du processeur.
3.  Bonus : **Dockerfile-collector** : Ce fichier contient les instructions pour créer une image Docker contenant le code du collecteur.
4. **docker-compose.yml** : Ce fichier contient les instructions pour exécuter les images Docker du collecteur et du processeur ainsi que les lignes déja préparées pour Redis. 
5. **.env** : Ce fichier contient les variables d'environnement nécessaires pour exécuter les images Docker.
6. **.gitignore** : Ce fichier contient les fichiers et dossiers à ignorer lors de la mise en ligne du projet.
7. **package.json** : Ce fichier contient les dépendances du projet.
8. **README-RUN.md** : Ce fichier contient les instructions pour exécuter le projet.

