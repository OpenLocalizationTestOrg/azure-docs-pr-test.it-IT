---
title: aaaReset accesso tooan VM Linux di Azure | Documenti Microsoft
description: Come gli utenti toomanage e Reimposta accesso sull'uso di macchine virtuali Linux hello estensione VMAccess e hello Azure CLI 2.0
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 261a9646-1f93-407e-951e-0be7226b3064
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 08/04/2017
ms.author: danlep
ms.openlocfilehash: 2f8db01b9fac20bf547d8b1926e5c0b3c5d18280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-users-ssh-and-check-or-repair-disks-on-linux-vms-using-hello-vmaccess-extension-with-hello-azure-cli-20"></a>Gestire utenti, SSH e controllo o i dischi di ripristino sull'uso di macchine virtuali Linux hello estensione VMAccess con hello Azure CLI 2.0
disco Hello nella VM Linux verrà visualizzati errori. È in qualche modo reimpostare la password radice hello per le VM Linux o eliminato la chiave privata SSH. In tal caso, in giorni hello del Data Center di hello, si sarebbe necessario toodrive non esiste e quindi aprire hello KVM tooget alla console di server hello. Hello estensione VMAccess Azure può essere paragonato a tale commutatore KVM consente tooaccess hello console tooreset accesso tooLinux o eseguire la manutenzione a livello di disco.

Questo articolo illustra come toouse hello toocheck estensione VMAccess Azure o ripristinare un disco, reimpostare l'accesso utente, gestire gli account utente o Reimposta configurazione SSH hello in Linux. È anche possibile eseguire questi passaggi con hello [CLI di Azure 1.0](using-vmaccess-extension-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).


## <a name="ways-toouse-hello-vmaccess-extension"></a>Modi toouse hello estensione VMAccess
Esistono due modi, che è possibile utilizzare l'estensione VMAccess hello in macchine virtuali Linux:

* Utilizzare hello Azure CLI 2.0 e i parametri di hello necessario.
* [JSON non elaborata di utilizzare i file che il processo di estensione VMAccess hello](#use-json-files-and-the-vmaccess-extension) e quindi agire su.

Dopo l'utilizzo di esempi di Hello [utente vm az](/cli/azure/vm/user) comandi. tooperform questi passaggi, è necessario hello più recente [CLI di Azure 2.0](/cli/azure/install-az-cli2) installato e registrato con un account Azure tooan [accesso az](/cli/azure/#login).

## <a name="reset-ssh-key"></a>Ripristinare la chiave SSH
esempio Hello Reimposta chiave SSH hello per utente hello `azureuser` nella macchina virtuale denominata hello `myVM`:

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="reset-password"></a>Reimpostazione delle password
esempio Hello Reimposta password hello hello utente `azureuser` nella macchina virtuale denominata hello `myVM`:

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --password myNewPassword
```

## <a name="restart-ssh"></a>Riavviare SSH
esempio Hello riavvia il daemon SSH hello e reimposta hello i valori di toodefault configurazione SSH in una macchina virtuale denominata `myVM`:

```azurecli
az vm user reset-ssh \
  --resource-group myResourceGroup \
  --name myVM
```

## <a name="create-a-user"></a>Creare un utente
esempio Hello crea un utente denominato `myNewUser` usando una chiave SSH per l'autenticazione nella macchina virtuale denominata hello `myVM`:

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="delete-a-user"></a>Eliminare un utente
esempio Hello Elimina un utente denominato `myNewUser` nella macchina virtuale denominata hello `myVM`:

```azurecli
az vm user delete \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser
```


## <a name="use-json-files-and-hello-vmaccess-extension"></a>Utilizzare i file JSON e hello estensione VMAccess
seguono esempi Hello utilizza file JSON non elaborati. Utilizzare [az vm estensione set](/cli/azure/vm/extension#set) toothen chiamare i file JSON. Questi file JSON possono essere chiamati anche dai modelli di Azure. 

### <a name="reset-user-access"></a>Ripristinare l'accesso utente
Se si smarrisce accesso tooroot nella VM Linux, è possibile avviare un tooreset script VMAccess chiave SSH o la password dell'utente.

chiave pubblica SSH hello di tooreset di un utente, creare un file denominato `reset_ssh_key.json` e aggiungere le impostazioni nel seguente formato hello. Sostituire i valori per hello `username` e `ssh_key` parametri:

```json
{
  "username":"azureuser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNGxxxxxx2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7xxxxxxwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5wxxtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== azureuser@myVM"
}
```

Eseguire lo script di VMAccess hello con:

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_ssh_key.json
```

tooreset una password utente, creare un file denominato `reset_user_password.json` e aggiungere le impostazioni nel seguente formato hello. Sostituire i valori per hello `username` e `password` parametri:

```json
{
  "username":"azureuser",
  "password":"myNewPassword" 
}
```

Eseguire lo script di VMAccess hello con:

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_user_password.json
```

### <a name="restart-ssh"></a>Riavviare SSH
toorestart hello daemon SSH e reimpostare i valori hello SSH configurazione toodefault, creare un file denominato `reset_sshd.json`. Aggiungere hello seguente contenuto:

```json
{
  "reset_ssh": true
}
```

Eseguire lo script di VMAccess hello con:

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_sshd.json
```

### <a name="manage-users"></a>Gestire gli utenti

toocreate un utente che usa una chiave SSH per l'autenticazione, creare un file denominato `create_new_user.json` e aggiungere le impostazioni nel seguente formato hello. Sostituire i valori per hello `username` e `ssh_key` parametri:

```json
{
  "username":"myNewUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myNewUser@myVM",
  "password":"myNewUserPassword"
}
```

Eseguire lo script di VMAccess hello con:

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings create_new_user.json
```

toodelete un utente, creare un file denominato `delete_user.json` e aggiungere hello dopo contenuto. Sostituire il valore per hello `remove_user` parametro:

```json
{
  "remove_user":"myNewUser"
}
```

Eseguire lo script di VMAccess hello con:

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings delete_user.json
```

### <a name="check-or-repair-hello-disk"></a>Verificare o riparare hello disco
Uso di VMAccess è anche possibile controllare e ripristinare un disco di cui sono stati aggiunti toohello VM Linux.

toocheck quindi hello disco, creare un file denominato `disk_check_repair.json` e aggiungere le impostazioni nel seguente formato hello. Sostituire il valore per nome hello `repair_disk`:

```json
{
  "check_disk": "true",
  "repair_disk": "true, mydiskname"
}
```

Eseguire lo script di VMAccess hello con:

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings disk_check_repair.json
```

## <a name="next-steps"></a>Passaggi successivi
L'aggiornamento di Linux mediante hello estensione VMAccess Azure è un metodo toomake viene modificato in una VM Linux in esecuzione. È anche possibile usare strumenti come cloud-inizializzazione e Gestione risorse di Azure modelli toomodify VM Linux all'avvio del sistema.

[Estensioni e funzionalità delle macchine virtuali per Linux](extensions-features.md)

[Creazione di modelli di Azure Resource Manager con le estensioni di VM Linux](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Utilizzo di cloud init toocustomize una VM Linux durante la creazione](using-cloud-init.md)

