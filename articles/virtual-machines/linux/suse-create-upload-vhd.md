---
title: Création et téléchargement d'un disque dur virtuel SUSE Linux dans Azure
description: Apprenez à créer et à télécharger un disque dur virtuel (VHD) Azure contenant un système d'exploitation SUSE Linux.
author: gbowerman
ms.service: virtual-machines-linux
ms.subservice: imaging
ms.workload: infrastructure-services
ms.topic: how-to
ms.date: 03/12/2018
ms.author: guybo
ms.openlocfilehash: 73e07c612486d5f48b1ad3eca8044a561549092b
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2020
ms.locfileid: "87292115"
---
# <a name="prepare-a-sles-or-opensuse-virtual-machine-for-azure"></a>Préparation d'une machine virtuelle SLES ou openSUSE pour Azure


Cet article suppose que vous avez déjà installé un système d'exploitation SUSE ou openSUSE Linux dans un disque dur virtuel. Il existe de multiples outils dédiés à la création de fichiers .vhd, comme la solution de virtualisation Hyper-V. Pour obtenir des instructions, consultez la page [Installation du rôle Hyper-V et configuration d'une machine virtuelle](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh846766(v=ws.11)).

## <a name="sles--opensuse-installation-notes"></a>Notes d'installation SLES/openSUSE
* Consultez également les [Notes générales d’installation sous Linux](create-upload-generic.md#general-linux-installation-notes) pour obtenir d’autres conseils sur la préparation de Linux pour Azure.
* Azure ne prend pas en charge le format VHDX, seulement le **VHD fixe**.  Vous pouvez convertir le disque au format VHD à l'aide de Hyper-V Manager ou de l’applet de commande convert-vhd.
* Lors de l’installation du système Linux, il est recommandé d’utiliser les partitions standard plutôt que LVM (qui est souvent le choix par défaut pour de nombreuses installations). Ceci permettra d'éviter les conflits de noms avec des machines virtuelles clonées, notamment si un disque de système d'exploitation doit être relié à une autre machine virtuelle pour la dépanner. La technique [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) peut être utilisée sur les disques de données, le cas échéant.
* Ne configurez pas une partition d'échange sur le disque du système d'exploitation. L'agent Linux est configurable pour créer un fichier d'échange sur le disque de ressources temporaire.  Les étapes ci-dessous fournissent plus d’informations à ce sujet.
* Tous les VDH sur Azure doivent avoir une taille virtuelle alignée à 1 Mo. Lors de la conversion d’un disque brut vers VDH, vous devez vous assurer que la taille du disque brut est un multiple de 1 Mo avant la conversion. Pour plus d’informations, consultez [Notes d’installation sur Linux](create-upload-generic.md#general-linux-installation-notes).

## <a name="use-suse-studio"></a>Utilisation de SUSE Studio
[SUSE Studio](https://studioexpress.opensuse.org/) peut facilement créer et gérer vos images SLES et openSUSE pour Azure et Hyper-V. Cette approche est recommandée pour personnaliser vos propres images SLES et openSUSE.

Comme alternative à la création de votre propre disque dur virtuel, SUSE publie également des images BYOS (« Bring Your Own Subscription ») pour SLES sur [VMDepot](https://www.microsoft.com/en-us/research/wp-content/uploads/2016/04/using-and-contributing-vms-to-vm-depot.pdf).

## <a name="prepare-suse-linux-enterprise-server-11-sp4"></a>Préparation de SUSE Linux Enterprise Server 11 SP4
1. Dans le panneau central de Hyper-V Manager, sélectionnez la machine virtuelle.
2. Cliquez sur **Connect** pour ouvrir la fenêtre de la machine virtuelle.
3. Enregistrez votre système SUSE Linux Enterprise pour lui permettre de télécharger les mises à jour et d’installer des packages.
4. Mettez à jour le système avec les derniers correctifs :

    ```console
    # sudo zypper update
    ```

1. Installez l’agent Linux Azure à partir du référentiel SLES (SLE11-Public-Cloud-Module) :

    ```console
    # sudo zypper install python-azure-agent
    ```

1. Vérifiez que waagent est réglé sur « on » dans chkconfig et, dans le cas contraire, configurez son démarrage automatique :

    ```console
    # sudo chkconfig waagent on
    ```

7. Vérifiez que le service waagent est en cours d’exécution et, dans le cas contraire, démarrez-le : 

    ```console
    # sudo service waagent start
    ```

8. Modifiez la ligne de démarrage du noyau dans votre configuration grub pour y inclure les paramètres de noyau supplémentaires pour Azure. Pour cela, ouvrez le fichier « /boot/grub/menu.lst » dans un éditeur de texte et vérifiez que le noyau par défaut comprend les paramètres suivants :

    ```config-grub
    console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    ```

    Ceci permet d'assurer que tous les messages de la console sont envoyés vers le premier port série, ce qui peut simplifier les problèmes de débogage pour l'assistance d'Azure.
9. Vérifiez que /boot/grub/menu.lst et /etc/fstab référencent le disque à l’aide de son UUID (by-uuid) au lieu de son ID (by-id). 
   
    Obtention de l’UUID du disque

    ```console
    # ls /dev/disk/by-uuid/
    ```

    Si /dev/disk/by-id est utilisé, mettez à jour /boot/grub/menu.lst et /etc/fstab avec la valeur appropriée de by-uuid.
   
    Avant la modification
   
    `root=/dev/disk/by-id/SCSI-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxxx-part1`
   
    Après la modification
   
    `root=/dev/disk/by-uuid/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`

10. Modifiez les règles udev pour éviter la génération de règles statiques pour les interfaces Ethernet. Ces règles peuvent causer des problèmes lors du clonage d’une machine virtuelle dans Microsoft Azure ou Hyper-V :

    ```console
    # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
    # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules
    ```

11. Il est recommandé de modifier le fichier « /etc/sysconfig/network/dhcp » et le paramètre `DHCLIENT_SET_HOSTNAME` comme suit :

    ```config
    DHCLIENT_SET_HOSTNAME="no"
    ```

12. Sous « /etc/sudoers », commentez ou supprimez les lignes suivantes (si elles sont présentes) :

    ```text
    Defaults targetpw   # ask for the password of the target user i.e. root
    ALL    ALL=(ALL) ALL   # WARNING! Only use this together with 'Defaults targetpw'!
    ```

13. Vérifiez que le serveur SSH est installé et configuré pour démarrer au moment prévu.  C'est généralement le cas par défaut.
14. Ne créez pas d'espace swap sur le disque du système d'exploitation.
    
    L'agent Linux Azure peut configurer automatiquement un espace swap à l'aide du disque local de ressources connecté à la machine virtuelle après déploiement sur Azure. Notez que le disque de ressources local est un disque *temporaire* et qu'il peut être vidé lors de l'annulation de l'approvisionnement de la machine virtuelle. Après avoir installé l'agent Linux Azure (voir l'étape précédente), modifiez les paramètres suivants dans le fichier /etc/waagent.conf :

    ```config-conf
    ResourceDisk.Format=y
    ResourceDisk.Filesystem=ext4
    ResourceDisk.MountPoint=/mnt/resource
    ResourceDisk.EnableSwap=y
    ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.
    ```

15. Exécutez les commandes suivantes pour annuler le déploiement de la machine virtuelle et préparer son déploiement sur Azure :

    ```console
    # sudo waagent -force -deprovision
    # export HISTSIZE=0
    # logout
    ```
16. Cliquez sur **Action -> Arrêter** dans le Gestionnaire Hyper-V. Votre disque dur virtuel Linux est alors prêt pour le téléchargement dans Azure.

---
## <a name="prepare-opensuse-131"></a>Préparation de openSUSE 13.1+
1. Dans le panneau central de Hyper-V Manager, sélectionnez la machine virtuelle.
2. Cliquez sur **Connect** pour ouvrir la fenêtre de la machine virtuelle.
3. Sur l’interpréteur de commandes, exécutez la commande`zypper lr`. Si cette commande renvoie un résultat semblable à ce qui suit, alors les référentiels sont configurés comme prévu, aucune modification n'est nécessaire (notez que les numéros de version peuvent varier) :

   | # | Alias                 | Nom                  | activé | Actualiser
   | - | :-------------------- | :-------------------- | :------ | :------
   | 1 | Cloud:Tools_13.1      | Cloud:Tools_13.1      | Oui     | Oui
   | 2 | openSUSE_13.1_OSS     | openSUSE_13.1_OSS     | Oui     | Oui
   | 3 | openSUSE_13.1_Updates | openSUSE_13.1_Updates | Oui     | Oui

    Si la commande renvoie « Aucun référentiel défini... », utilisez les commandes suivantes pour ajouter ces référentiels :

    ```console
    # sudo zypper ar -f http://download.opensuse.org/repositories/Cloud:Tools/openSUSE_13.1 Cloud:Tools_13.1
    # sudo zypper ar -f https://download.opensuse.org/distribution/13.1/repo/oss openSUSE_13.1_OSS
    # sudo zypper ar -f http://download.opensuse.org/update/13.1 openSUSE_13.1_Updates
    ```

    Vous pouvez alors réexécuter la commande `zypper lr` pour vérifier que ces référentiels ont été ajoutés. Si un des référentiels de mise à jour concernés n'est pas activé, exécutez la commande suivante :

    ```console
    # sudo zypper mr -e [NUMBER OF REPOSITORY]
    ```

4. Mettez à jour le noyau vers la dernière version disponible :

    ```console
    # sudo zypper up kernel-default
    ```

    Ou, pour mettre à jour le système avec les derniers correctifs :

    ```console
    # sudo zypper update
    ```

5. Installez l'agent Linux Azure.

    ```console
    # sudo zypper install WALinuxAgent
    ```

6. Modifiez la ligne de démarrage du noyau dans votre configuration grub pour y inclure les paramètres de noyau supplémentaires pour Azure. Pour cela, ouvrez le fichier « /boot/grub/menu.lst » dans un éditeur de texte et vérifiez que le noyau par défaut comprend les paramètres suivants :

    ```config-grub
     console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    ```

   Ceci permet d'assurer que tous les messages de la console sont envoyés vers le premier port série, ce qui peut simplifier les problèmes de débogage pour l'assistance d'Azure. Supprimez également les paramètres suivants de la ligne de démarrage du noyau (s'ils sont présents) :

    ```config-grub
     libata.atapi_enabled=0 reserve=0x1f0,0x8
    ```

7. Il est recommandé de modifier le fichier « /etc/sysconfig/network/dhcp » et le paramètre `DHCLIENT_SET_HOSTNAME` comme suit :

    ```config
     DHCLIENT_SET_HOSTNAME="no"
    ```

8. **Important :** Sous « /etc/sudoers », commentez ou supprimez les lignes suivantes (si elles sont présentes) :

    ```text
    Defaults targetpw   # ask for the password of the target user i.e. root
    ALL    ALL=(ALL) ALL   # WARNING! Only use this together with 'Defaults targetpw'!
    ```

9. Vérifiez que le serveur SSH est installé et configuré pour démarrer au moment prévu.  C'est généralement le cas par défaut.
10. Ne créez pas d'espace swap sur le disque du système d'exploitation.

    L'agent Linux Azure peut configurer automatiquement un espace swap à l'aide du disque local de ressources connecté à la machine virtuelle après déploiement sur Azure. Notez que le disque de ressources local est un disque *temporaire* et qu'il peut être vidé lors de l'annulation de l'approvisionnement de la machine virtuelle. Après avoir installé l'agent Linux Azure (voir l'étape précédente), modifiez les paramètres suivants dans le fichier /etc/waagent.conf :

    ```config-conf
    ResourceDisk.Format=y
    ResourceDisk.Filesystem=ext4
    ResourceDisk.MountPoint=/mnt/resource
    ResourceDisk.EnableSwap=y
    ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.
    ```

11. Exécutez les commandes suivantes pour annuler le déploiement de la machine virtuelle et préparer son déploiement sur Azure :

    ```console
    # sudo waagent -force -deprovision
    # export HISTSIZE=0
    # logout
    ```

12. Vérifiez que l'agent Linux Azure est exécuté au démarrage :

    ```console
    # sudo systemctl enable waagent.service
    ```

13. Cliquez sur **Action -> Arrêter** dans le Gestionnaire Hyper-V. Votre disque dur virtuel Linux est alors prêt pour le téléchargement dans Azure.

## <a name="next-steps"></a>Étapes suivantes
Vous êtes maintenant prêt à utiliser votre disque dur virtuel SUSE Linux pour créer des machines virtuelles dans Azure. S’il s’agit de votre premier chargement du fichier .vhd sur Azure, consultez [Créer une machine virtuelle Linux à partir d’un disque personnalisé](upload-vhd.md#option-1-upload-a-vhd).
