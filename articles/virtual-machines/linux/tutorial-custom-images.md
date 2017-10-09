---
title: immagini di macchina virtuale con hello CLI di Azure personalizzate aaaCreate | Documenti Microsoft
description: 'Esercitazione: creare un''immagine di macchina virtuale personalizzata utilizzando hello CLI di Azure.'
services: virtual-machines-linux
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/21/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 217a993c0c1d48939b74108ac6c5f7a1a619416c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-hello-cli"></a>Creare un'immagine personalizzata di una macchina virtuale di Azure utilizzando hello CLI

Le immagini personalizzate sono come le immagini di marketplace, ma si possono creare autonomamente. Immagini personalizzate possono essere utilizzati toobootstrap configurazioni, ad esempio il precaricamento di applicazioni, configurazioni dell'applicazione e altre configurazioni del sistema operativo. In questa esercitazione viene creata un'immagine personalizzata di una macchina virtuale di Azure. Si apprenderà come:

> [!div class="checklist"]
> * Eseguire il deprovisioning e generalizzare le macchine virtuali
> * Creare un'immagine personalizzata
> * Creare una VM da un'immagine personalizzata
> * Elenco di tutte le immagini di hello nella sottoscrizione
> * Eliminare un'immagine


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se si sceglie tooinstall e utilizza hello CLI in locale, questa esercitazione, è necessario che sia in esecuzione hello Azure CLI versione 2.0.4 o versioni successive. Eseguire `az --version` versione hello toofind. Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="before-you-begin"></a>Prima di iniziare

passaggi di Hello riportati di seguito in dettaglio come tootake una macchina virtuale esistente e attivare i dati in un oggetto personalizzato riutilizzabile immagine che si possono usare toocreate nuove istanze di macchina virtuale.

esempio di hello toocomplete in questa esercitazione, è necessario disporre di una macchina virtuale esistente. Se necessario, questo [script di esempio](../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md) può crearne una appositamente. Quando il lavoro esercitazione hello, sostituire il gruppo di risorse di hello e VM nomi dove necessario.

## <a name="create-a-custom-image"></a>Creare un'immagine personalizzata

toocreate un'immagine di una macchina virtuale, è necessario tooprepare hello VM deprovisioning, la deallocazione e quindi contrassegnando origine hello VM come generalizzato. Una volta hello che macchina virtuale è stata preparata, è possibile creare un'immagine.

### <a name="deprovision-hello-vm"></a>Eseguire il deprovisioning hello VM 

Deprovisioning generalizza hello VM rimuovendo le informazioni specifiche del computer. La generalizzazione rende possibili toodeploy più macchine virtuali da una singola immagine. Durante il deprovisioning, nome host hello viene reimpostato troppo*localhost.localdomain*. Vengono eliminati anche i lease DHCP memorizzati nella cache, le chiavi host SSH, le configurazioni nameserver e le password radicele.

hello toodeprovision macchina virtuale, utilizzare l'agente VM di Azure hello (waagent). agente VM di Azure Hello viene installato nella macchina virtuale hello e gestisce il provisioning e l'interazione con il Controller di infrastruttura di Azure hello. Per ulteriori informazioni, vedere hello [Guida dell'utente dell'agente Linux di Azure](agent-user-guide.md).

Tooyour macchina virtuale di connettersi tramite SSH e hello esecuzione comando toodeprovision Ciao macchina virtuale. Con hello `+user` argomento, l'ultimo account di provisioning utente hello ed eventuali dati associati vengono eliminati anche. Sostituire l'indirizzo IP di esempio hello con indirizzo IP pubblico hello della macchina virtuale.

SSH toohello macchina virtuale.
```bash
ssh azureuser@52.174.34.95
```
Eseguire il deprovisioning hello macchina virtuale.

```bash
sudo waagent -deprovision+user -force
```
Chiudere una sessione SSH hello.

```bash
exit
```

### <a name="deallocate-and-mark-hello-vm-as-generalized"></a>Rilasciare e contrassegnare hello VM come generalizzato

toocreate un'immagine, hello VM deve toobe deallocato. Deallocare hello VM utilizzando [az vm deallocare](/cli//azure/vm#deallocate). 
   
```azurecli-interactive 
az vm deallocate --resource-group myResourceGroup --name myVM
```

Infine, impostare lo stato di hello di hello VM come generalizzata con [generalizzare la macchina virtuale az](/cli//azure/vm#generalize) affinché hello piattaforma Azure sappia hello VM sia stato generalizzato. È possibile creare solo un'immagine da una VM generalizzata.
   
```azurecli-interactive 
az vm generalize --resource-group myResourceGroup --name myVM
```

### <a name="create-hello-image"></a>Creare l'immagine di hello

Ora è possibile creare un'immagine di macchina virtuale hello utilizzando [immagine az creare](/cli//azure/image#create). esempio Hello crea un'immagine denominata *myImage* da una macchina virtuale denominata *myVM*.
   
```azurecli-interactive 
az image create \
    --resource-group myResourceGroup \
    --name myImage \
    --source myVM
```
 
## <a name="create-vms-from-hello-image"></a>Creare macchine virtuali da immagini hello

Dopo aver creato un'immagine, è possibile creare nuove macchine virtuali da hello immagine utilizzando [creare vm az](/cli/azure/vm#create). esempio Hello crea una macchina virtuale denominata *myVMfromImage* dall'immagine hello denominato *myImage*.

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVMfromImage \
    --image myImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

## <a name="image-management"></a>Gestione delle immagini 

Di seguito sono riportati alcuni esempi di attività comuni di gestione di immagini e come toocomplete loro utilizzando hello CLI di Azure.

Elencare tutte le immagini per nome in formato tabella.

```azurecli-interactive 
az image list \
  --resource-group myResourceGroup
```

Eliminare un'immagine. In questo esempio elimina hello immagine denominata *myOldImage* da hello *myResourceGroup*.

```azurecli-interactive 
az image delete \
    --name myOldImage \
    --resource-group myResourceGroup
```

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione è stata creata un'immagine di macchina virtuale personalizzata. Si è appreso come:

> [!div class="checklist"]
> * Eseguire il deprovisioning e generalizzare le macchine virtuali
> * Creare un'immagine personalizzata
> * Creare una VM da un'immagine personalizzata
> * Elenco di tutte le immagini di hello nella sottoscrizione
> * Eliminare un'immagine

Spostare toohello Avanti toolearn esercitazione sulle macchine virtuali a disponibilità elevata.

> [!div class="nextstepaction"]
> [Creare macchine virtuali a disponibilità elevata](tutorial-availability-sets.md).

