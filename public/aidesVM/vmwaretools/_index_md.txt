+++
title = "Activer le glisser déposer entre votre VM et votre SSD ?"
weight = 161
+++

Ces étapes vous permettront de , texte et images entre votre machine hôte et la VM en utilisant le glisser déposer. Notez que certaines restrictions peuvent s'appliquer selon la configuration de votre environnement VMware.

Pour pouvoir transférer des fichiers, dossiers entre votre machine hôte et une machine virtuelle sous VMware, suivez ces étapes :

1. **Installer VMware Tools** :
   - Assurez-vous que VMware Tools est installé sur la VM. Cette suite d'utilitaires améliore les performances et offre des fonctionnalités comme le glisser déposer.
   - Pour l'installer :
     - Ouvrez VMware Workstation.
     - Sélectionnez votre VM et cliquez sur `Lecteur` > `Gérer` > `Installer VMware Tools`.
     - Suivez les instructions à l'écran pour finaliser l'installation, puis redémarrez la VM.

2. **Activer le glisser déposer** :
   - Après avoir installé VMware Tools :
     - Allez dans `Lecteur` > `Gérer` > `Paramètres de la machine virtuelle`.
     - Dans l'onglet `Options`, sélectionnez `Isolation des invités`.
     - Cochez les cases `Activer le glisser déposer` et `Activer le copier-coller`.
     - Cliquez sur `OK` pour enregistrer les modifications.

3. **Redémarrer la VM** :
   - Pour que les modifications prennent effet, redémarrez la machine virtuelle.

---
## Références

1. [IT Connect](https://www.it-connect.fr/vmware-workstation-repertoire-partage-avec-une-vm-windows/)
2. [informatiweb](https://www.informatiweb-pro.net/virtualisation/vmware/vmware-workstation-15-transferer-fichiers-entre-pc-hote-et-vm.html)
3. [thewindowsclub.blog](https://thewindowsclub.blog/fr/how-to-enable-copy-and-paste-for-a-vmware-virtual-machine/?utm_source=chatgpt.com)
4. [techsyncer](https://www.techsyncer.com/fr/3-simple-ways-to-transfer-files-from-a-vm-to-a-host.html)

