# Exercice 1

1. **Addition de douveau disque dure de 5Go**
![image](https://user-images.githubusercontent.com/97104312/194231304-741b6053-82e7-4100-8b0c-4c75a94f8f5e.png)

2. On vérifie que le nouveau disque dure est bien détectée avec la commande `lsblk`  
 ![image](https://user-images.githubusercontent.com/97104312/194232212-786da282-f466-40d3-9a66-eb12db97656c.png)


3. Partitionnez ce disque en utilisant fdisk : créez une première partition de 2 Go de type Linux (n°83), et une seconde partition de 3 Go en NTFS (n°7)

`sudo fdisk /dev/sdb`  

![image](https://user-images.githubusercontent.com/97104312/194274782-86b56651-0cc2-43ba-a59f-6693fcb8d34b.png)


4. Il faut lancer ces 2 commandes: `sudo mkfs -t ext4 /dev/sdb1` `sudo mkfs -t ntfs /dev/sdb2`

5. `df -T` N'affiche que les disques **"montées"**.

6. 
`sudo mkdir /data`  
`sudo mkdir /win`  
`sudo nano /etc/fstab`  
On rajoute de lignes suivantes:
```
/dev/sdb1 /data ext4 defaults 0 2
/dev/sdb2 /win ntfs defaults 0 2
``` 

7. Utilisez la commande mount puis redémarrez votre VM pour valider la configuration

```bash
$ sudo mount -a
```

8. Il faut utiliser **VMware RC**.

9.

## Exercice 2. Partitionnement LVM

1. 
`sudo umount /data`  
`sudo umount /win`  
`sudo nano /etc/fstab`   

2.On utilise la même méthose et on lui donne le type 8.  

3.On utilise la commande `sudo pvcreate /dev/sdb1 ` `sudo pvdisplay`  

4.On utilise la commande `vgcreate ` et `vgdisplay`  

5.Il faut utiliser la commande: `sudo lvcreate -n lvData -l 100%FREE vg1`

8.Utilisez la commande vgextend <nom_vg> <nom_pv> pour ajouter le nouveau disque au groupe de volumes.  

9.Utilisez la commande `lvresize`pour agrandir le volume logique. Enfin, on redimentionne avec: `resize2fs`.
