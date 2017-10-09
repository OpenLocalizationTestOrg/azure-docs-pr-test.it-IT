---
title: aaaDifferent modi toocreate una VM Linux di Azure | Microsoft Azure
description: Informazioni su modi diversi di hello toocreate una macchina virtuale di Linux in Azure, inclusi i collegamenti tootools ed esercitazioni per ogni metodo.
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f38f8a44-6c88-4490-a84a-46388212d24c
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 250e92c063c87a8c1279097dc2264777d95478d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="different-ways-toocreate-a-linux-vm"></a>Modi diversi toocreate una VM Linux
È la flessibilità di hello in Azure toocreate una macchina virtuale Linux (VM) tooyou preferisci strumenti e i flussi di lavoro. In questo articolo riepiloga le differenze e gli esempi per creare le macchine virtuali Linux, tra cui hello CLI di Azure 2.0. È inoltre possibile visualizzare le opzioni di creazione inclusi hello [CLI di Azure 1.0](creation-choices-nodejs.md).

Hello [CLI di Azure 2.0](/cli/azure/install-az-cli2) è disponibile tra le piattaforme tramite un pacchetto npm, pacchetti di distribuzione fornito o contenitore Docker. Installare hello build più appropriato per l'ambiente e accedere con un account Azure tooan [accesso az](/cli/azure/#login)

* [Creare una VM Linux con hello Azure CLI 2.0](quick-create-cli.md)
  
  * Usare [az group create](/cli/azure/group#create) per creare un gruppo di risorse denominato *myResourceGroup*: 
   
    ```azurecli
    az group create --name myResourceGroup --location eastus
    ```
    
  * Creare una macchina virtuale con [creare vm az](/cli/azure/vm#create) denominato *myVM* utilizzando hello più recente *UbuntuLTS* immagine e generare le chiavi SSH se sono già presenti *~/.ssh*:

    ```azurecli
    az vm create \
        --resource-group myResourceGroup \
        --name myVM \
        --image UbuntuLTS \
        --generate-ssh-keys
    ```

* [Creare una VM Linux con un modello di Azure](create-ssh-secured-vm-from-template.md)
  
  * Hello seguente utilizza [distribuzione gruppo az creare](/cli/azure/group/deployment#create) toocreate una macchina virtuale da un modello archiviato in GitHub:
    
    ```azurecli
    az group deployment create --resource-group myResourceGroup \ 
      --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
      --parameters @myparameters.json
    ```
* [Creare una VM Linux e personalizzarla con cloud-init](tutorial-automate-vm-deployment.md)

* [Creare un'applicazione con carico bilanciato e disponibilità elevata in più VM Linux](tutorial-load-balancer.md)


## <a name="azure-portal"></a>Portale di Azure
Hello [portale di Azure](https://portal.azure.com) consente tooquickly creare una macchina virtuale poiché non c'è niente tooinstall nel sistema. Utilizzare hello toocreate portale Azure hello VM:

* [Creare una VM Linux di hello portale di Azure](quick-create-portal.md) 


## <a name="operating-system-and-image-choices"></a>Sistema operativo e opzioni dell'immagine
Quando si crea una macchina virtuale, si sceglie un'immagine in base a hello desiderato toorun sistema operativo. Azure e i relativi partner mettono a disposizione diverse immagini, alcune delle quali includono applicazioni e strumenti preinstallati. O, caricare una delle proprie immagini (vedere [hello seguente sezione](#use-your-own-image)).

### <a name="azure-images"></a>Immagini di Azure
Hello utilizzare [immagine di macchina virtuale az](/cli/azure/vm/image) comandi toosee disponibili dal server di pubblicazione, versione di distribuzione e le compilazioni.

Elenca gli editori disponibili:

```azurecli
az vm image list-publishers --location eastus
```

Elenca i prodotti disponibili (offerte) per un determinato editore:

```azurecli
az vm image list-offers --publisher Canonical --location eastus
```

Elenca gli SKU disponibili (versioni di distribuzione) di una determinata offerta:

```azurecli
az vm image list-skus --publisher Canonical --offer UbuntuServer --location eastus
```

Elenca tutte le immagini disponibili per una determinata versione:

```azurecli
az vm image list --publisher Canonical --offer UbuntuServer --sku 16.04.0-LTS --location eastus
```

Per ulteriori esempi sull'esplorazione e l'utilizzo di immagini disponibili, vedere [Naviga e selezionare le immagini di macchina virtuale di Azure con hello Azure CLI](cli-ps-findimage.md).

Hello [creare vm az](/cli/azure/vm#create) comando dispone di alias è possibile usare accesso tooquickly hello distribuzioni più comuni e le versioni più recenti. Utilizzo degli alias è spesso più veloce rispetto all'impostazione publisher hello, offerta, SKU e versione ogni volta che si crea una macchina virtuale:

| Alias | Autore | Offerta | SKU | Versione |
|:--- |:--- |:--- |:--- |:--- |
| CentOS |OpenLogic |Centos |7,2 |più recenti |
| CoreOS |CoreOS |CoreOS |Stabile |più recenti |
| Debian |credativ |Debian |8 |più recenti |
| openSUSE |SUSE |openSUSE |13.2 |più recenti |
| RHEL |Redhat |RHEL |7,2 |più recenti |
| SLES |SLES |SLES |12-SP1 |più recenti |
| UbuntuLTS |Canonical |UbuntuServer |14.04.4-LTS |più recenti |

### <a name="use-your-own-image"></a>Usare la propria immagine
Per personalizzazioni specifiche è possibile usare un'immagine basata su una VM di Azure esistente acquisendo tale VM. È anche possibile caricare un'immagine creata in locale. Per ulteriori informazioni sulle distribuzioni supportate e come toouse immagini personalizzate, vedere hello seguenti articoli:

* [Distribuzioni approvate per Azure](endorsed-distros.md)
* [Informazioni per distribuzioni non approvate](create-upload-generic.md)
* [Come un'immagine da una macchina virtuale di Azure esistente toocreate](tutorial-custom-images.md).
  
  * Guida introduttiva all'esempio comandi toocreate un'immagine da una macchina virtuale di Azure esistente:
    
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm generalize --resource-group myResourceGroup --name myVM
    az vm image create --resource-group myResourceGroup --source myVM --name myImage
    ```

## <a name="next-steps"></a>Passaggi successivi
* Creare una VM Linux con hello [CLI](quick-create-cli.md), da hello [portale](quick-create-portal.md), o tramite un [modello di Azure Resource Manager](../windows/cli-deploy-templates.md).
* Dopo aver creato una VM Linux, vedere le [informazioni sui dischi e l'archiviazione di Azure](tutorial-manage-disks.md).
* I passaggi troppo veloce[reimpostare una password o le chiavi SSH e gestire gli utenti](using-vmaccess-extension.md).
