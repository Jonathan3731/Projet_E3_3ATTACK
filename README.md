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


#### Port 80 : HTTP Apache 2.4.7

En renseignant l'adresse ip de la cible suivi du port 80 nous arrivons sur le site WEB et nous pouvons voir plusieurs dossiers qui sont des différentes fonctionnalités du site :

![image](https://github.com/user-attachments/assets/00f75f29-7c9b-4f61-9a94-e8ab2eac4865)

Nous pouvons donc chercher des failles selon les fonctionnalités, nous commençons par "drupal" :

![image](https://github.com/user-attachments/assets/6caf3d49-c445-499c-9740-83956098adbd)

Nous décidons d'utiliser l'exploit 16 pour réaliser une injection SQL et nous arrivons à accéder à meterpreter sur la cible :

![image](https://github.com/user-attachments/assets/e03d42b3-2f7b-413d-aecc-92337d327407)


#### Port 22 : SSH

Nous analysons la version de SSH utilisé :

![image](https://github.com/user-attachments/assets/36f77fa6-f9ed-42b2-8683-0e8dd29ae30b)

Nous recherchons une faille à l'aide de la commande "search" selon la version de SSH :

![image](https://github.com/user-attachments/assets/991df993-2d04-4eb6-bcaf-3b1503c99c3a)
![image](https://github.com/user-attachments/assets/91cd13f4-bdf2-44c5-b5a1-52fb118c4293)

Nous utilisons l'exploit 61 et renseignons les paramètres nécessaires : 

![image](https://github.com/user-attachments/assets/4ea95dec-760a-4086-8048-db8e472b10af)
![image](https://github.com/user-attachments/assets/5d98c907-8bb5-4f01-ab71-625400a0d582)

L'exploit a bien fonctionné car nous voyons les login de SSH :
![image](https://github.com/user-attachments/assets/7b92b238-7f65-4389-86a9-83a4a2a62e4d)


#### Port 6697 : IRCD

Dans le NMAP fait auparavant, il y avait le port IRCD, nous recherchons donc des failles avec la commande "search" :

![image](https://github.com/user-attachments/assets/9aab33ac-25ac-4594-96c1-af9b17f39e93)

Nous utilisons donc la seule faille trouvée et indiquons les paramètres nécessaires : 

![image](https://github.com/user-attachments/assets/6e720da6-089c-4d71-9f00-1fa8c2a6fb65)
![image](https://github.com/user-attachments/assets/9140ee51-5afb-462f-97e7-4a87bd729464)

L'exploit a bien fonctionné :
![image](https://github.com/user-attachments/assets/2ae39de2-04f5-4e3a-b42d-aab339c19146)


#### Port 8080 : HTTP Jetty 8.1.7

Lors d'un nmap plus précis vers les ports 80 etc, nous voyons qu'il y a aussi le port 8080 qui est ouvert.

![image](https://github.com/user-attachments/assets/8d6c0796-2585-443c-8991-db32a7873cee)

Lorsque nous tentons d'accéder à au serveur WEB en indiquant l'adresse ip et le port 8080 nous arrivons sur cette page :

![image](https://github.com/user-attachments/assets/cea97fd1-4336-419d-a25e-bae2e88094aa)

En cliquant sur le lien, nous arrivons sur cette page : 

![image](https://github.com/user-attachments/assets/93707124-1c54-4803-a0df-4e1404a431d9)

Nous avons donc chercher des failles avec le nom affiché à l'écran :

![image](https://github.com/user-attachments/assets/928c03e8-9605-4825-b67f-79920126a72a)

Nous utilisons la seule faille disponible en indiquant les paramètres nécessaires à son fonctionnement :

![image](https://github.com/user-attachments/assets/6e4e60ec-1d30-4a22-b1d6-7be596e09b29)

L'exploit a bien fonctionné :

![image](https://github.com/user-attachments/assets/9eb1c005-067b-453e-9fb6-af7affe671ed)


