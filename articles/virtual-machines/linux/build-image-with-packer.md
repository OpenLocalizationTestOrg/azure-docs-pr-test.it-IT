---
title: aaaHow toocreate immagini di macchina virtuale Linux Azure con chi | Documenti Microsoft
description: Informazioni su come le immagini di toocreate chi toouse delle macchine virtuali Linux in Azure
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/18/2017
ms.author: iainfou
ms.openlocfilehash: 5990598859e73efac477884bc8de5fd5138bf6e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-packer-toocreate-linux-virtual-machine-images-in-azure"></a>Come le immagini di macchina virtuale Linux di toouse chi toocreate in Azure
Ogni macchina virtuale (VM) in Azure viene creato da un'immagine che definisce hello di Linux e versione del sistema operativo. Le immagini possono includere applicazioni e configurazioni preinstallate. Hello Azure Marketplace fornisce molte immagini prima e di terze parti per le distribuzioni più comuni e di ambienti applicazione oppure è possibile creare le proprie esigenze tooyour immagini personalizzate personalizzate. In questo articolo illustra in dettaglio come hello toouse aprire lo strumento di origine [chi](https://www.packer.io/) toodefine e compilazione immagini personalizzate in Azure.


## <a name="create-azure-resource-group"></a>Creare un gruppo di risorse di Azure
Durante il processo di compilazione hello, chi crea risorse di Azure temporanee durante la compilazione di macchina virtuale di origine hello. toocapture che VM di origine per l'utilizzo come un'immagine, è necessario definire un gruppo di risorse. l'output dal processo di compilazione chi hello Hello viene archiviato in questo gruppo di risorse.

Come prima cosa creare un gruppo di risorse con [az group create](/cli/azure/group#create). esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *eastus* percorso:

```azurecli
az group create -n myResourceGroup -l eastus
```


## <a name="create-azure-credentials"></a>Creare credenziali di Azure
Per eseguire l'autenticazione con Azure, Packer usa un'entità servizio. Un'entità servizio di Azure è un'identità di sicurezza che è possibile usare con le app, con i servizi e con strumenti di automazione come Packer. È controllare e definire le autorizzazioni di hello come entità di servizio toowhat operazioni hello è possibile eseguire in Azure.

Creare un servizio principale con [az ad sp creare-per-rbac](/cli/azure/ad/sp#create-for-rbac) e le credenziali di hello output che chi deve:

```azurecli
az ad sp create-for-rbac --query [appId,password,tenant]
```

Un esempio di output di hello da hello precedenti comandi è la seguente:

```azurecli
"f5b6a5cf-fbdf-4a9f-b3b8-3c2cd00225a4",
"0e760437-bf34-4aad-9f8d-870be799c55d",
"72f988bf-86f1-41af-91ab-2d7cd011db47"
```

tooAzure tooauthenticate, è necessario anche con l'ID sottoscrizione Azure tooobtain [mostra account az](/cli/azure/account#show):

```azurecli
az account show --query [id] --output tsv
```

Utilizzare l'output di hello di questi due comandi nel passaggio successivo hello.


## <a name="define-packer-template"></a>Definire un modello di Packer
immagini toobuild, si crea un modello come un file JSON. Nel modello hello definisce generatori e provisioners per l'esecuzione di hello effettivo processo di compilazione. Chi ha un [strumento di provisioning per Azure](https://www.packer.io/docs/builders/azure.html) che consentono di toodefine Azure risorse, ad esempio credenziali dell'entità servizio hello create nel passaggio precedente hello.

Creare un file denominato *ubuntu.json* e Incolla hello seguendo il contenuto. Immettere i valori per i seguenti hello:

| .                           | Dove tooobtain |
|-------------------------------------|----------------------------------------------------|
| *client_id*                         | Prima riga di output da `az ad sp` create command - *appId* |
| *client_secret*                     | Seconda riga di output da `az ad sp` create command - *password* |
| *tenant_id*                         | Terza riga di output da `az ad sp` create command - *tenant* |
| *subscription_id*                   | Output del comando `az account show` |
| *managed_image_resource_group_name* | Nome del gruppo di risorse creato nel primo passaggio hello |
| *managed_image_name*                | Nome dell'immagine di disco gestito hello creato |


```json
{
  "builders": [{
    "type": "azure-arm",

    "client_id": "f5b6a5cf-fbdf-4a9f-b3b8-3c2cd00225a4",
    "client_secret": "0e760437-bf34-4aad-9f8d-870be799c55d",
    "tenant_id": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "subscription_id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx",

    "managed_image_resource_group_name": "myResourceGroup",
    "managed_image_name": "myPackerImage",

    "os_type": "Linux",
    "image_publisher": "Canonical",
    "image_offer": "UbuntuServer",
    "image_sku": "16.04-LTS",

    "azure_tags": {
        "dept": "Engineering",
        "task": "Image deployment"
    },

    "location": "East US",
    "vm_size": "Standard_DS2_v2"
  }],
  "provisioners": [{
    "execute_command": "chmod +x {{ .Path }}; {{ .Vars }} sudo -E sh '{{ .Path }}'",
    "inline": [
      "apt-get update",
      "apt-get upgrade -y",
      "apt-get -y install nginx",

      "/usr/sbin/waagent -force -deprovision+user && export HISTSIZE=0 && sync"
    ],
    "inline_shebang": "/bin/sh -x",
    "type": "shell"
  }]
}
```

Questo modello crea un'immagine Ubuntu 16.04 LTS, installa NGINX e annullamento del provisioning hello macchina virtuale.

> [!NOTE]
> Se si espande credenziali dell'utente tooprovision questo modello, modificare il comando di provisioning hello che l'annullamento del provisioning hello Azure agente tooread `-deprovision` anziché `deprovision+user`.
> Hello `+user` flag rimuove tutti gli account utente dalla macchina virtuale di origine hello.


## <a name="build-packer-image"></a>Compilare l'immagine in Packer
Se non si dispone già installati nel computer locale, chi [seguire le istruzioni di installazione di hello chi](https://www.packer.io/docs/install/index.html).

Creare immagini hello specificando il chi file modello nel modo seguente:

```bash
./packer build ubuntu.json
```

Un esempio di output di hello da hello precedenti comandi è la seguente:

```bash
azure-arm output will be in this color.

==> azure-arm: Running builder ...
    azure-arm: Creating Azure Resource Manager (ARM) client ...
==> azure-arm: Creating resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> Location          : ‘East US’
==> azure-arm:  -> Tags              :
==> azure-arm:  ->> dept : Engineering
==> azure-arm:  ->> task : Image deployment
==> azure-arm: Validating deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> DeploymentName    : ‘pkrdpswtxmqm7ly’
==> azure-arm: Deploying deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> DeploymentName    : ‘pkrdpswtxmqm7ly’
==> azure-arm: Getting hello VM’s IP address ...
==> azure-arm:  -> ResourceGroupName   : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> PublicIPAddressName : ‘packerPublicIP’
==> azure-arm:  -> NicName             : ‘packerNic’
==> azure-arm:  -> Network Connection  : ‘PublicEndpoint’
==> azure-arm:  -> IP Address          : ‘40.76.218.147’
==> azure-arm: Waiting for SSH toobecome available...
==> azure-arm: Connected tooSSH!
==> azure-arm: Provisioning with shell script: /var/folders/h1/ymh5bdx15wgdn5hvgj1wc0zh0000gn/T/packer-shell868574263
    azure-arm: WARNING! hello waagent service will be stopped.
    azure-arm: WARNING! Cached DHCP leases will be deleted.
    azure-arm: WARNING! root password will be disabled. You will not be able toologin as root.
    azure-arm: WARNING! /etc/resolvconf/resolv.conf.d/tail and /etc/resolvconf/resolv.conf.d/original will be deleted.
    azure-arm: WARNING! packer account and entire home directory will be deleted.
==> azure-arm: Querying hello machine’s properties ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> ComputeName       : ‘pkrvmswtxmqm7ly’
==> azure-arm:  -> Managed OS Disk   : ‘/subscriptions/guid/resourceGroups/packer-Resource-Group-swtxmqm7ly/providers/Microsoft.Compute/disks/osdisk’
==> azure-arm: Powering off machine ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> ComputeName       : ‘pkrvmswtxmqm7ly’
==> azure-arm: Capturing image ...
==> azure-arm:  -> Compute ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> Compute Name              : ‘pkrvmswtxmqm7ly’
==> azure-arm:  -> Compute Location          : ‘East US’
==> azure-arm:  -> Image ResourceGroupName   : ‘myResourceGroup’
==> azure-arm:  -> Image Name                : ‘myPackerImage’
==> azure-arm:  -> Image Location            : ‘eastus’
==> azure-arm: Deleting resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm: Deleting hello temporary OS disk ...
==> azure-arm:  -> OS Disk : skipping, managed disk was used...
Build ‘azure-arm’ finished.

==> Builds finished. hello artifacts of successful builds are:
--> azure-arm: Azure.ResourceManagement.VMImage:

ManagedImageResourceGroupName: myResourceGroup
ManagedImageName: myPackerImage
ManagedImageLocation: eastus
```


## <a name="create-vm-from-azure-image"></a>Creare una macchina virtuale da un'immagine di Azure
È ora possibile creare una macchina virtuale dall'immagine con [az vm create](/cli/azure/vm#create). Specificare l'immagine è stato creato con hello hello `--image` parametro. esempio Hello crea una macchina virtuale denominata *myVM* da *myPackerImage* e genera le chiavi SSH se non esiste già:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image myPackerImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

Sono necessari alcuni minuti toocreate hello macchina virtuale. Dopo aver creato hello VM, prendere nota di hello `publicIpAddress` visualizzato da hello CLI di Azure. Questo indirizzo è sito NGINX di hello tooaccess usato tramite un web browser.

tooallow web tooreach traffico la macchina virtuale, aprire la porta 80 da hello Internet con [az vm open-porta](/cli/azure/vm#open-port):

```azurecli
az vm open-port \
    --resource-group myResourceGroup \
    --name myVM \
    --port 80
```

## <a name="test-vm-and-nginx"></a>Testare la macchina virtuale e NGINX
È ora possibile aprire un web browser e immettere `http://publicIpAddress` nella barra degli indirizzi hello. Fornire la propria pubblico indirizzo IP da hello VM creare il processo. verrà visualizzata la pagina NGINX di Hello predefinito come hello di esempio seguente:

![Sito NGINX predefinito](./media/build-image-with-packer/nginx.png) 


## <a name="next-steps"></a>Passaggi successivi
In questo esempio, chi toocreate un'immagine di macchina virtuale è usato con NGINX già installato. È possibile utilizzare questa immagine di macchina virtuale insieme a distribuzione flussi di lavoro esistenti, ad esempio toodeploy tooVMs l'app creata da hello immagine con Ansible, Chef o Puppet.

Per altri modelli di Packer di esempio per distribuzioni di Linux di altro tipo, vedere [questo repository di GitHub](https://github.com/hashicorp/packer/tree/master/examples/azure).