---
title: aaaUse cloud init toocustomize una VM Linux | Documenti Microsoft
description: Come toocustomize di cloud init toouse una VM Linux durante la creazione hello Azure CLI 2.0
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 195c22cd-4629-4582-9ee3-9749493f1d72
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: e7297e162fc73f0da42f195bec2fcbe23b310c1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-cloud-init-toocustomize-a-linux-vm-during-creation"></a>Usare cloud init toocustomize una VM Linux durante la creazione
Questo articolo illustra come toomake un tooset script cloud init hello nome host, aggiornare i pacchetti installati e gestire gli account utente con hello CLI di Azure 2.0. gli script di cloud init Hello vengono chiamati quando si crea una macchina virtuale (VM) da CLI di Azure. Per una panoramica più approfondita sull'installazione di applicazioni, la scrittura di file di configurazione e l'inserimento di chiavi da Key Vault, vedere [questa esercitazione](tutorial-automate-vm-deployment.md). È anche possibile eseguire questi passaggi con hello [CLI di Azure 1.0](using-cloud-init-nodejs.md).

## <a name="quick-commands"></a>Comandi rapidi
Creare uno script di cloud init.txt che imposta il nome host hello, Aggiorna tutti i pacchetti e aggiunge un tooLinux utente sudo.

```yaml
#cloud-config
hostname: myVMhostname
apt_upgrade: true
users:
  - name: myNewAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myVM
```

Creare un toolaunch gruppo di risorse di macchine virtuali in con [gruppo az creare](/cli/azure/group#create). esempio Hello Crea gruppo di risorse hello denominato *myResourceGroup*:

```azurecli
az group create --name myResourceGroup --location eastus
```

Creare una VM Linux con [creare vm az](/cli/azure/vm#create) tramite cloud init tooconfigure durante l'avvio con hello `--custom-data` parametro.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="detailed-walkthrough"></a>Procedura dettagliata
Quando si avvia una nuova VM Linux si ottiene un VM Linux standard senza alcuna personalizzazione né alcun adattamento. [Cloud init](https://cloudinit.readthedocs.org) è tooinject un metodo standard per le impostazioni di configurazione o script in tale VM Linux che è stato avviato per hello prima volta.

In Azure, esistono alcuni modi toomake modifiche in una VM Linux come viene distribuito o avviato.

* Inserire gli script che usano cloud-init.
* Inserire gli script utilizzando hello Azure [estensione VMAccess](using-vmaccess-extension.md).
* Un modello di Azure che usa cloud-init.
* Un modello di Azure che usa [CustomScriptExtention](extensions-customscript.md).

script tooinject in qualsiasi momento dopo l'avvio:

* Direttamente i comandi toorun SSH
* Inserire gli script utilizzando hello Azure [estensione VMAccess](using-vmaccess-extension.md), in modo imperativo o in un modello di Azure
* Strumenti per la gestione della configurazione come Ansible, Salt, Chef e Puppet.

> [!NOTE]
> Estensione VMAccess esegue uno script come radice in hello stesso tramite SSH possibile. Tuttavia, utilizzando l'estensione della macchina virtuale hello consente diverse funzionalità offerti da Azure che possono essere utili a seconda dello scenario.

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a>Disponibilità di cloud-init negli alias delle immagini a creazione rapida della VM di Azure:
| Alias | Autore | Offerta | SKU | Versione | Cloud-init |
|:--- |:--- |:--- |:--- |:--- |:--- |
| CentOS |OpenLogic |Centos |7,2 |più recenti |no |
| CoreOS |CoreOS |CoreOS |Stabile |più recenti |sì |
| Debian |credativ |Debian |8 |più recenti |no |
| openSUSE |SUSE |openSUSE |13.2 |più recenti |no |
| RHEL |Redhat |RHEL |7,2 |più recenti |no |
| UbuntuLTS |Canonical |UbuntuServer |14.04.4-LTS |più recenti |sì |

È in uso di nostri partner tooget cloud-init inclusi e l'utilizzo delle immagini hello che forniscono tooAzure.

## <a name="add-a-cloud-init-script-toohello-vm-creation-with-hello-azure-cli"></a>Aggiungere una creazione di VM cloud init script toohello con hello CLI di Azure
toolaunch uno script di inizializzazione di cloud durante la creazione di una macchina virtuale in Azure, specificare il file di cloud init hello mediante Azure CLI hello `--custom-data` passare.

Creare un toolaunch gruppo di risorse di macchine virtuali in con [gruppo az creare](/cli/azure/group#create). esempio Hello Crea gruppo di risorse hello denominato *myResourceGroup*:

```azurecli
az group create --name myResourceGroup --location eastus
```

Creare una VM Linux con [creare vm az](/cli/azure/vm#create) tramite cloud init tooconfigure durante l'avvio.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="create-a-cloud-init-script-tooset-hello-hostname-of-a-linux-vm"></a>Creare un nome di cloud init script tooset hello host di una VM Linux
Uno dei hello più semplice e più importanti impostazioni per tutte le VM Linux sarà hostname hello. È possibile definire facilmente tale impostazione tramite cloud-init con questo script.  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a>Script cloud-init di esempio denominato `cloud_config_hostname.txt`.
```yaml
#cloud-config
hostname: myservername
```

Durante l'avvio iniziale di hello di hello macchina virtuale, questo script cloud init imposta hello hostname troppo*nomeserver*. Creare una VM Linux con [creare vm az](/cli/azure/vm#create) tramite cloud init tooconfigure durante l'avvio.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

Account di accesso e verificare il nome host hello di hello nuova macchina virtuale.

```bash
ssh myVM
hostname
myservername
```

## <a name="create-a-cloud-init-script"></a>Creare uno script cloud-init
Per la sicurezza, si desidera il tooupdate Ubuntu VM al primo avvio hello. Con cloud init possiamo che con hello seguire script, a seconda della distribuzione di Linux hello in uso.

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-hello-debian-family"></a>Script di esempio cloud init `cloud_config_apt_upgrade.txt` per hello Debian famiglia
```yaml
#cloud-config
apt_upgrade: true
```

Dopo che è stato avviato Linux, tutti i pacchetti hello installato vengono aggiornati tramite **apt get**. Creare una VM Linux con [creare vm az](/cli/azure/vm#create) tramite cloud init tooconfigure durante l'avvio.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_apt_upgrade.txt
```

Accedere e verificare che tutti i pacchetti siano aggiornati.

```bash
ssh myUbuntuVM
sudo apt-get upgrade
Reading package lists... Done
Building dependency tree
Reading state information... Done
Calculating upgrade... Done
hello following packages have been kept back:
  linux-generic linux-headers-generic linux-image-generic
0 upgraded, 0 newly installed, 0 tooremove and 0 not upgraded.
```

## <a name="create-a-cloud-init-script-tooadd-a-user-toolinux"></a>Creare un tooadd script cloud init tooLinux un utente
Una delle attività di primo hello in qualsiasi nuova VM Linux è un utente per se stessi o tooavoid utilizzando tooadd *radice*. Le chiavi SSH sono consigliata per la sicurezza e ai fini dell'usabilità e vengono aggiunti toohello *~/.ssh/authorized_keys* file con questo script di inizializzazione di cloud.

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a>Script cloud-init `cloud_config_add_users.txt` di esempio per la famiglia Debian
```yaml
#cloud-config
users:
  - name: myCloudInitAddedAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myUbuntuVM
```

Dopo che è stato avviato Linux, tutti gli utenti di hello elencato sono il gruppo di sudo toohello creato e aggiunto. Creare una VM Linux con [creare vm az](/cli/azure/vm#create) tramite cloud init tooconfigure durante l'avvio.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_add_users.txt
```

Account di accesso e verificare utente hello appena creato.

```bash
ssh myVM
cat /etc/group
```

Output

```bash
root:x:0:
<snip />
sudo:x:27:myCloudInitAddedAdminUser
<snip />
myCloudInitAddedAdminUser:x:1000:
```

## <a name="next-steps"></a>Passaggi successivi
Cloud init sta diventando un modo standard toomodify VM Linux all'avvio del sistema. Azure offre inoltre estensioni VM, che consentono di toomodify il LinuxVM all'avvio del sistema o in fase di esecuzione. Ad esempio, è possibile utilizzare hello Azure VMAccessExtension tooreset SSH o informazioni utente durante l'esecuzione di hello macchina virtuale. Con cloud-init, occorre una password di hello tooreset riavvio.

[Informazioni sulle estensioni e sulle funzionalità delle macchine virtuali](extensions-features.md)

[Gestire utenti, SSH e controllo o i dischi di ripristino di macchine virtuali Linux di Azure utilizzando hello estensione VMAccess](using-vmaccess-extension.md)
