# **Partie 1 : Gestion des utilisateurs**

**Q.2.1.1**

![Capture d'écran 2025-01-17 104946](https://github.com/user-attachments/assets/85f5506a-7dd9-49d3-85bb-7bf277ed4e1a)

**Q.2.1.2**

Pour un utilisateur standard et un usage personnel, il est recommandé de ne pas donner de privilèges root à ce compte et de bien gérer les permissions de restrictions vis a vis des fichiers systèmes.

---

# **Partie 2 : Configuration de SSH**

**Q.2.2.1**

![Capture d'écran 2025-01-17 105649](https://github.com/user-attachments/assets/a7b9ca94-342a-4567-9d72-249dcd3b0e69)

**Q.2.2.2**

![Capture d'écran 2025-01-17 105933](https://github.com/user-attachments/assets/0b9da904-9bf9-4ffc-8372-20fa4bda1e6d)


**Q.2.2.3**

![Capture d'écran 2025-01-17 110107](https://github.com/user-attachments/assets/b995e325-3c93-4071-80a0-59e61430dd95)

---

# **Partie 3 : Analyse du stockage**

**Q.2.3.1**

![Capture d'écran 2025-01-17 110515](https://github.com/user-attachments/assets/e08d396e-fead-459b-8ad2-82968cbf25c1)

On voit que les systèmes de fichiers actuellement montés sont:

- / sur cp3--vg-root;
- /boot sur md0p1.
  
**Q.2.3.2**

Sur la capture précédente on voit que les types de stockage utilisés sont:

- Du RAID1 sur md0;
- Du LVM sur le groupe cp3-vg.

**Q.2.3.3**

- Ajout du disque dans Virtualbox:
  
![Capture d'écran 2025-01-17 112348](https://github.com/user-attachments/assets/19f68c85-3264-4301-9e82-02fba0fd071d)

- On configure ensuite notre nouveau disque avec fdisk:

![Capture d'écran 2025-01-17 113820](https://github.com/user-attachments/assets/65c1eebe-acf8-4c28-8a7e-5e10ca9338c7)

- On prépare la partition:

![Capture d'écran 2025-01-17 113111](https://github.com/user-attachments/assets/f6c8a92e-dbc7-4f11-a38d-7ef808bc068c)

- On lui donne le type RAID:

![Capture d'écran 2025-01-17 113220](https://github.com/user-attachments/assets/dc8754bf-d098-475c-9b7c-7dbef853c1e3)

- Aprés l'écriture on Vérifie que notre partition est bien prête:

![Capture d'écran 2025-01-17 113307](https://github.com/user-attachments/assets/03de05b9-755b-4c40-863a-7ae3ba2997cf)

- On ajoute notre nouvelle partition au RAID existant:

![Capture d'écran 2025-01-17 113505](https://github.com/user-attachments/assets/7701c947-2079-4713-92c0-4b1b3e414ff5)

- On contrôle que tout est bon:

![Capture d'écran 2025-01-17 113505](https://github.com/user-attachments/assets/f37d74df-8270-4708-bfb0-975ad3715699)

- Et enfin On met à jour la configuration et on contrôle une dernière fois:

![Capture d'écran 2025-01-17 113616](https://github.com/user-attachments/assets/e64b1f5d-d00b-49e3-aa56-535aeaa33834)

**Q.2.3.4**

- On retrouve notre groupe Volume:

![Capture d'écran 2025-01-17 114558](https://github.com/user-attachments/assets/81493406-60e3-43be-ae8d-c3e9d7c6acfa)

- On va créer notre nouveau volume logique de 2go qui s'appel `lv_svg`:

![Capture d'écran 2025-01-17 114731](https://github.com/user-attachments/assets/6bf67992-c25e-4485-b078-a78e768beae6)

- On vérifie notre nouveau volume logique avec la commande `lvdisplay`: 

![Capture d'écran 2025-01-17 114956](https://github.com/user-attachments/assets/e1555c11-e48b-4df0-83c6-543954d25a2a)

- On formate notre volume en lui donnant le label sauvegarde:

![Capture d'écran 2025-01-17 115458](https://github.com/user-attachments/assets/1a6eecaa-31a7-48d3-a9eb-1519323c0a83)

- On monte notre disque au point de montage demandé:

![Capture d'écran 2025-01-17 115240](https://github.com/user-attachments/assets/b7d0690d-dcef-4ead-9aa2-9984bd935e44)

- On édite le fichier dans `/etc/fstab`:

![Capture d'écran 2025-01-17 115728](https://github.com/user-attachments/assets/5fe2d4eb-93a5-4a4c-9679-45adbdd0fe68)

- On vérifie que le montage est bon:

![Capture d'écran 2025-01-17 115750](https://github.com/user-attachments/assets/88317fed-7474-401e-9717-f14346402612)

**Q.2.3.5**

![Capture d'écran 2025-01-17 115851](https://github.com/user-attachments/assets/1a10ea9b-129d-44cc-b1ca-90e487ed3394)

Sur cette capture on voit qu'il nous reste - de 1.79G de stockage.

---

# **Partie 4 : Sauvegardes**

**Q.2.4.1**

- bareos-dir: c'est ce composant qui va permettre la configuration de toutes les tâches de Bareos tel que les jobs les calendriers de sauvegarde,... Le director contient la configuration principale de Bareos.

- bareos-sd: Il contient les configurations spécifiques au Storage Daemon et il est responsable du stockage des sauvegardes.

- bareos-fd: il contient configurations spécifiques au File Daemon, le composant installé sur les machines à sauvegarder. il communique avec le Director pour transmettre les données des fichiers à sauvegarder.

---

# **Partie 5 : Filtrage et analyse réseau**

**Q.2.5.1**

![Capture d'écran 2025-01-17 121351](https://github.com/user-attachments/assets/b36d7755-eeb9-4f4a-8659-e5d8a939eb87)

Avec cette capture, On voit qu'il y a les règles suivantes qui s'appliquent:

- pour le trafic entrant;
- sur les connexions déjà établit;
- le trafic local;
- sur la gestion de paquets invalides;
- pour le port 22;
- concernant le protocole ICMP v4 et v6

**Q.2.5.2**

Avec cette même capture, on en déduit ce qui est autorisé par Netfilter:

- les connexions établies sont autorisé;
- le trafic local est autorisé;
- les connexion SSH sur le port 22;
- les PINg v4 et V6;

**Q.2.5.3**

Avec cette même capture, on en déduit ce qui est interdit par Netfilter:

- les paquets invalides;
- tout les paquets qui ne sont pas explicitement autorisés

**Q.2.5.4**

![Capture d'écran 2025-01-17 122711](https://github.com/user-attachments/assets/48fefbec-c9e0-464f-b3f2-f7a5ff4567a7)

---

# **Partie 6 : Analyse de logs**

**Q.2.6.1**

![Capture d'écran 2025-01-17 123406](https://github.com/user-attachments/assets/c07dbc1b-3792-4cc6-b074-d0e9b9c50d27)










