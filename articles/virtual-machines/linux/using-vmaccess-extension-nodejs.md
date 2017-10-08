---
title: accesso aaaReset sull'uso di macchine virtuali Linux di Azure hello estensione VMAccess | Documenti Microsoft
description: Reimpostare l'accesso in macchine virtuali Linux di Azure utilizzando hello estensione VMAccess.
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 261a9646-1f93-407e-951e-0be7226b3064
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/25/2016
ms.author: v-livech
ms.openlocfilehash: 2636655f3f7d14ba30e1dc62c319e4e278521ead
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-users-ssh-and-check-or-repair-disks-on-azure-linux-vms-using-hello-vmaccess-extension-with-hello-azure-cli-10"></a>Gestire utenti, SSH e controllo o i dischi di ripristino di macchine virtuali Linux di Azure utilizzando hello estensione VMAccess con hello Azure CLI 1.0
Questo articolo illustra come toouse hello Azure VMAcesss estensione toocheck o ripristinare un disco, reimpostare l'accesso utente, gestire gli account utente o reimpostare configurazione SSHD hello in Linux. articolo Hello richiede:

* Un account Azure. È possibile [ottenere una versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Hello [CLI di Azure](../../cli-install-nodejs.md) accesso `azure login`.
* Hello Azure CLI *deve essere* modalità Azure Resource Manager `azure config mode arm`.


## <a name="cli-versions-toocomplete-hello-task"></a>Attività hello toocomplete versioni CLI
È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:

- [Azure CLI 1.0](#quick-commands): l'interfaccia CLI per hello classic risorse Gestione modelli di distribuzione e (in questo articolo)
- [Azure CLI 2.0](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -la prossima generazione CLI per modello di distribuzione di gestione risorse hello


## <a name="quick-commands"></a>Comandi rapidi
Esistono due modi toouse VMAccess in macchine virtuali Linux:

* Utilizzo di hello Azure CLI 1.0 e hello parametri obbligatori.
* Usare file JSON non elaborati che VMAccess elabora e su cui basa le sue operazioni.

Per la sezione comando rapido hello, verrà toouse hello Azure CLI 1.0 `azure vm reset-access` metodo. In hello esempi di comando seguente, sostituire i valori di hello che contengono "esempio" con i valori hello dal proprio ambiente.

## <a name="create-a-resource-group-and-linux-vm"></a>Creare un gruppo di risorse e una VM Linux
```bash
azure group create myResourceGroup westus
```

## <a name="create-a-debian-vm"></a>Creare una VM Debian
```azurecli
azure vm quick-create \
  -M ~/.ssh/id_rsa.pub \
  -u myAdminUser \
  -g myResourceGroup \
  -l westus \
  -y Linux \
  -n myVM \
  -Q Debian
```

## <a name="reset-root-password"></a>Reimpostare la password radice
password di tooreset hello radice:

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u root \
  -p myNewPassword
```

## <a name="ssh-key-reset"></a>Reimpostazione della chiave SSH
chiave SSH di hello tooreset di un utente non radice:

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u myAdminUser \
  -M ~/.ssh/id_rsa.pub
```

## <a name="create-a-user"></a>Creare un utente
toocreate un utente:

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u myAdminUser \
  -p myAdminUserPassword
```

## <a name="remove-a-user"></a>Rimuovere un utente
```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -R myRemovedUser
```

## <a name="reset-sshd"></a>Reimpostare un disco SSHD
configurazione di SSHD tooreset hello:

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM
  -r
```


## <a name="detailed-walkthrough"></a>Procedura dettagliata
### <a name="vmaccess-defined"></a>Estensione VMAccess definita:
disco Hello nella VM Linux verrà visualizzati errori. È in qualche modo reimpostare la password radice hello per le VM Linux o eliminato la chiave privata SSH. In tal caso, in giorni hello del Data Center di hello, si sarebbe necessario toodrive non esiste e quindi aprire hello KVM tooget alla console di server hello. Hello estensione VMAccess Azure può essere paragonato a tale commutatore KVM consente tooaccess hello console tooreset accesso tooLinux o eseguire la manutenzione a livello di disco.

Per hello dettagliate procedura dettagliata, verrà esteso hello toouse di VMAccess, che utilizza il file JSON non elaborati.  Questi file JSON di VMAccess possono essere chiamati anche dai modelli di Azure.

### <a name="using-vmaccess-toocheck-or-repair-hello-disk-of-a-linux-vm"></a>Utilizzo di VMAccess toocheck o Ripristina hello disco di una VM Linux
Uso di VMAccess è possibile eseguire un sfck eseguire nel disco hello nella VM Linux.  È inoltre possibile eseguire una verifica del disco e ripristinarlo utilizzando un VMAccess.

toocheck quindi hello disco usare questo script VMAccess:

`disk_check_repair.json`

```json
{
  "check_disk": "true",
  "repair_disk": "true, user-disk-name"
}
```

Eseguire lo script di VMAccess hello con:

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path disk_check_repair.json
```

### <a name="using-vmaccess-tooreset-user-access-toolinux"></a>Utilizzo di VMAccess tooreset utente accesso tooLinux
Se si smarrisce accesso tooroot nella VM Linux, è possibile avviare una password di VMAccess script tooreset hello radice.

la password radice hello tooreset, utilizzare questo script VMAccess:

`reset_root_password.json`

```json
{
  "username":"root",
  "password":"myNewPassword"
}
```

Eseguire lo script di VMAccess hello con:

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_root_password.json
```

la chiave SSH hello tooreset di un utente non radice, utilizzare questo script VMAccess:

`reset_ssh_key.json`

```json
{
  "username":"myAdminUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myAdminUser@myVM" 
}
```

Eseguire lo script di VMAccess hello con:

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_ssh_key.json
```

### <a name="using-vmaccess-toomanage-user-accounts-on-linux"></a>Tramite gli account utente di VMAccess toomanage in Linux
VMAccess è uno script Python che può essere utenti toomanage utilizzati nella VM Linux senza accesso e l'utilizzo di sudo o hello account radice.

toocreate un utente, utilizzare questo script VMAccess:

`create_new_user.json`

```json
{
  "username":"myNewUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myNewUser@myVM",
  "password":"myNewUserPassword"
}
```

Eseguire lo script di VMAccess hello con:

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path create_new_user.json
```

toodelete un utente, utilizzare questo script VMAccess:

`remove_user.json`

```json
{
  "remove_user":"myDeletedUser"
}
```

Eseguire lo script di VMAccess hello con:

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path remove_user.json
```

### <a name="using-vmaccess-tooreset-hello-sshd-configuration"></a>Utilizzando la configurazione di VMAccess tooreset hello SSHD
Se si apportano configurazione SSHD macchine virtuali Linux toohello di modifiche e connessione SSH hello chiudere prima la verifica delle modifiche di hello, può essere impedito SSH'ing nuovamente.  VMAccess può essere utilizzato tooreset hello SSHD configurazione tooa indietro configurazione valida senza accedere su SSH.

configurazione di SSHD hello tooreset utilizzare questo script VMAccess:

`reset_sshd.json`

```json
{
  "reset_ssh": true
}
```

Eseguire lo script di VMAccess hello con:

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_sshd.json
```

## <a name="next-steps"></a>Passaggi successivi
L'aggiornamento di Linux, utilizzando le estensioni di VMAccess di Azure è un metodo toomake viene modificato in una VM Linux in esecuzione.  È anche possibile utilizzare strumenti come cloud init e modelli di Azure toomodify VM Linux all'avvio del sistema.

[Informazioni sulle estensioni e sulle funzionalità delle macchine virtuali](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Creazione di modelli di Azure Resource Manager con le estensioni di VM Linux](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Utilizzo di cloud init toocustomize una VM Linux durante la creazione](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

