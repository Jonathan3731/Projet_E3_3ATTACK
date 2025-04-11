# Projet_E3_3ATTACK
Rendu du TP Final du groupe composé de Tomy, Romain, Soulaymane et Jonathan.
## VM Metasploitable3 (sous Windows sur Virtual Box)
### Installation de la VM
Installation de Vagrant pour déployer la VM :

![image](https://github.com/user-attachments/assets/1b323162-9b5d-42b3-ab24-f88e6bd80db6)

Pour déployer la VM sur Virtual Box il faut utiliser quelques commandes venant de Vagrant :

![image](https://github.com/user-attachments/assets/6fc8edbc-2eb8-4eb7-a6ff-2d9f74da6312)

Une fois que les commandes ont finis de s'exécuter, des fichiers apparaîssent dans le dossier cible :

![image](https://github.com/user-attachments/assets/4ec0e216-fc7d-4be3-b8d0-6751ffb47f98)

La VM Metasploitable3 remonte bien sur Virtual Box :

![image](https://github.com/user-attachments/assets/efb103d0-ba2b-4809-a7db-3f732dccc49e)

### Pentest
Nous commençons par découvrir le réseau pour connaître l'ip de la VM cible :

![image](https://github.com/user-attachments/assets/49f153b6-342e-4941-b700-d0fa5130e22b)
![image](https://github.com/user-attachments/assets/5bca1328-a415-441a-803b-e34b59bae7eb)

Maintenant que l'ip est connu, nous pouvons faire un NMAP pour savoir quels sont les ports ouverts de la cible :

![image](https://github.com/user-attachments/assets/770acac0-b93f-4440-ba82-41596f540a3b)

#### Port 21 : FTP
Tout d'abord il faut trouver une faille par rapport à la version de FTP utilisée. Pour cela nous utilisons la commande "search" :
![image](https://github.com/user-attachments/assets/4c290393-74ad-4686-8812-dd9ad1e8c713)

Utilisation de l'exploit :

![image](https://github.com/user-attachments/assets/e902cbf9-a136-4f53-b66a-a3ed31c48d43)

Nous regardons les paramètres à renseigner :

![image](https://github.com/user-attachments/assets/81d22f40-ee8d-42ea-b95d-fe6084d2fc53)

Nous mettons l'adresse ip de la cible et de l'attaquant :

![image](https://github.com/user-attachments/assets/de0d6ebd-001d-4aa6-a677-9ee28e4ddc8f)

Nous lançons l'exploit mais une erreur est survenue en raison du manque de la précision d'un chemin :

![image](https://github.com/user-attachments/assets/07821cf5-b7d4-441d-873c-7f6f4ac41793)

Après avoir indiqué le chemin, nous retentons l'exploit et cela fonctionne :

![image](https://github.com/user-attachments/assets/6d84c44f-91af-4716-a842-8c95cd6a8e2a)

Nous stabilisons le shell et nous mettons en background la session pour faire un reverse shell :

![image](https://github.com/user-attachments/assets/cc0d4394-8ada-4e74-8506-7ab96e99053a)

Mise en place du reverse shell meterpreter vers la session de l'exploit FTP :

![image](https://github.com/user-attachments/assets/47a812ba-6708-45d2-9a25-6589a087b180)

Enfin, à l'aide de meterpreter nous téléchargeons les données du serveur FTP :

![image](https://github.com/user-attachments/assets/5d43c0c3-3763-4b41-badd-1c8063c42542)





## VM Icecream
