# Test technique

## 📚 Sommaire
- [Backend](#backend)
- [Frontend](#frontend)
- [SQL](#sql)

## 🔙 Backend
-  [Dossier](backend)
-  [Readme](backend/README.md)

L'idée ici est de créer deux serveurs, un collecteur et un processeur, qui communiquent entre eux via Redis.
Le collecteur reçoit des requêtes POST contenant des calculs à effectuer et les stocke dans une file d'attente pour être traitées ultérieurement.
Le processeur récupère les tâches à traiter depuis la file d'attente, effectue les calculs demandés et renvoie le résultat calculé sur Redis.

## 🖥️ Frontend
-  [Dossier](front)
-  [Readme](front/README.md)

Il faut créer une calculatrice simple qui prend deux opérandes et un opérateur.
La calculatrice doit afficher les résultats en se servant des serveurs créés dans le backend et des résulats stockés dans Redis.

## 💾 SQL
-  [Dossier](sql)
-  [Readme](sql/README.md)

---
**Note :**
Pour ce test, je vous demande de forker ce repository sur votre compte GitHub personnel et de me donner un accès en privé. Veuillez utiliser la convention de commits [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/). 
Utilisez des branches au maximum pour que je puisse évaluer votre utilisation de Git.


Si vous avez des questions, n'hésitez pas à [m'envoyer un mail](mailto:hbuval@adfinitas.fr) 📧
