---
title: un'immagine di una VM Linux in Azure utilizzando CLI 2.0 aaaCapture | Documenti Microsoft
description: Acquisire un'immagine di toouse una macchina virtuale di Azure per distribuzioni di massa tramite hello CLI di Azure 2.0.
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e608116f-f478-41be-b787-c2ad91b5a802
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 07/10/2017
ms.author: cynthn
ms.openlocfilehash: 9558332a86186b282775097428df462709373012
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-image-of-a-virtual-machine-or-vhd"></a>Come toocreate un'immagine di una macchina virtuale o un disco rigido virtuale

<!-- generalize, image - extended version of hello tutorial-->

toocreate più copie di una macchina virtuale (VM) toouse in Azure, acquisire un'immagine di macchina virtuale hello o hello disco rigido virtuale del sistema operativo. toocreate un'immagine, è necessario rimuovere le informazioni personali che rende più sicura toodeploy più volte. In hello alla procedura seguente si deprovisioning di una macchina virtuale esistente, rilasciare e creare un'immagine. È possibile utilizzare questa immagine toocreate macchine virtuali, in qualsiasi gruppo di risorse nella sottoscrizione.

Se si desidera toocreate una copia della VM Linux esistente per il backup o il debug o si carica un VHD Linux specializzato da una macchina virtuale locale, vedere [caricare e creare una VM Linux dall'immagine del disco personalizzato](upload-vhd.md).  

È inoltre possibile utilizzare **chi** toocreate configurazione personalizzata. Per ulteriori informazioni sull'utilizzo di chi, vedere [come le immagini di macchina virtuale Linux di toouse chi toocreate in Azure](build-image-with-packer.md).


## <a name="before-you-begin"></a>Prima di iniziare
Verificare che siano soddisfatti hello seguenti prerequisiti:

* È necessario una macchina virtuale di Azure creata nel modello di distribuzione di gestione risorse hello utilizzando dischi gestiti. Se è stata creata una VM Linux, è possibile utilizzare hello [portale](quick-create-portal.md), hello [CLI di Azure](quick-create-cli.md), o [modelli di gestione risorse](create-ssh-secured-vm-from-template.md). Configurare hello macchina virtuale in base alle esigenze. Ad esempio, [aggiungere dischi dati](add-disk.md), applicare aggiornamenti e installare applicazioni. 

* È inoltre necessario hello toohave più recente [CLI di Azure 2.0](/cli/azure/install-az-cli2) installato e registrato con un account Azure tooan [accesso az](/cli/azure/#login).

## <a name="quick-commands"></a>Comandi rapidi

Per una versione semplificata di questo argomento, per il test, la valutazione o di formazione su macchine virtuali in Azure, vedere [creare un'immagine personalizzata di una macchina virtuale di Azure utilizzando hello CLI](tutorial-custom-images.md).


## <a name="step-1-deprovision-hello-vm"></a>Passaggio 1: Eseguire il deprovisioning hello VM
Eseguire il deprovisioning hello macchina virtuale con l'agente VM di Azure hello, toodelete file specifici di computer e i dati. Hello utilizzare `waagent` con hello *-deprovisioning + user* parametro nell'origine VM Linux. Per ulteriori informazioni, vedere hello [Guida dell'utente dell'agente Linux di Azure](../windows/agent-user-guide.md).

1. Connettersi tooyour VM Linux utilizzando un client SSH.
2. Nella finestra di hello SSH, digitare hello comando seguente:
   
    ```bash
    sudo waagent -deprovision+user
    ```
<br>
   > [!NOTE]
   > Solo il seguente comando in una macchina virtuale che si desidera toocapture come immagine. Non garantisce che l'immagine hello viene cancellato di tutte le informazioni riservate o adatto per la ridistribuzione. Hello *+ user* parametro anche rimuove l'ultimo account di provisioning utente hello. Se si desidera tookeep le credenziali dell'account in hello macchina virtuale, usare semplicemente *-deprovisioning* tooleave hello account utente sul posto.
 
3. Tipo **y** toocontinue. È possibile aggiungere hello **-force** tooavoid parametro questo passaggio di conferma.
4. Al termine del comando di hello, digitare **uscire**. Questo passaggio consente di chiudere client SSH hello.

## <a name="step-2-create-vm-image"></a>Passaggio 2: Creare l'immagine della macchina virtuale
Utilizzare hello toomark hello Azure CLI 2.0 VM come generalizzato e acquisire l'immagine hello. In hello negli esempi seguenti, sostituire i nomi dei parametri di esempio con i valori desiderati. I nomi dei parametri di esempio includono *myResourceGroup*, *myVnet* e *myVM*.

1. Deallocare una macchina virtuale che deprovisioning con hello [az vm deallocare](/cli//azure/vm#deallocate). esempio Hello dealloca hello macchina virtuale denominata *myVM* nel gruppo di risorse hello denominato *myResourceGroup*:
   
    ```azurecli
    az vm deallocate \
      --resource-group myResourceGroup \
      --name myVM
    ```

2. Hello contrassegno VM come generalizzata con [generalizzare la macchina virtuale az](/cli//azure/vm#generalize). Hello in seguito esempio contrassegni hello hello macchina virtuale denominata *myVM* nel gruppo di risorse hello denominato *myResourceGroup* come generalizzato:
   
    ```azurecli
    az vm generalize \
      --resource-group myResourceGroup \
      --name myVM
    ```

3. Creare un'immagine di risorsa di macchina virtuale hello con [immagine az creare](/cli//azure/image#create). esempio Hello crea un'immagine denominata *myImage* nel gruppo di risorse hello denominato *myResourceGroup* utilizzando hello risorsa di macchina virtuale denominata *myVM*:
   
    ```azurecli
    az image create \
      --resource-group myResourceGroup \
      --name myImage --source myVM
    ```
   
   > [!NOTE]
   > Hello immagine è creata in hello stesso gruppo di risorse come la macchina virtuale di origine. Con questa immagine è possibile creare macchine virtuali in qualsiasi gruppo di risorse all'interno della sottoscrizione. Da una prospettiva di gestione, è preferibile toocreate un gruppo di risorse specifiche per le risorse macchina virtuale e le immagini.

## <a name="step-3-create-a-vm-from-hello-captured-image"></a>Passaggio 3: Creare una macchina virtuale dall'immagine acquisita hello
Creare una macchina virtuale utilizzando l'immagine di hello è stato creato con [creare vm az](/cli/azure/vm#create). esempio Hello crea una macchina virtuale denominata *myVMDeployed* dall'immagine hello denominato *myImage*:

```azurecli
az vm create \
   --resource-group myResourceGroup \
   --name myVMDeployed \
   --image myImage\
   --admin-username azureuser \
   --ssh-key-value ~/.ssh/id_rsa.pub
```

### <a name="creating-hello-vm-in-another-resource-group"></a>Creazione di hello macchina virtuale in un altro gruppo di risorse 

È possibile creare macchine virtuali da un'immagine in qualsiasi gruppo di risorse all'interno della sottoscrizione. toocreate una macchina virtuale in un gruppo di risorse diverso da quello immagine hello, specificare l'immagine di tooyour ID completo della risorsa hello. Utilizzare [elenco immagini az](/cli/azure/image#list) tooview un elenco di immagini. Hello l'output è simile toohello seguente esempio:

```json
"id": "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage",
   "location": "westus",
   "name": "myImage",
```

Hello seguente utilizza [creare vm az](/cli/azure/vm#create) toocreate una macchina virtuale in un gruppo di risorse diverso da quello immagine di origine hello specificando l'ID di risorsa immagine hello:

```azurecli
az vm create \
   --resource-group myOtherResourceGroup \
   --name myOtherVMDeployed \
   --image "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage" \
   --admin-username azureuser \
   --ssh-key-value ~/.ssh/id_rsa.pub
```


## <a name="step-4-verify-hello-deployment"></a>Passaggio 4: Verificare la distribuzione di hello

Ora SSH toohello macchina virtuale è stato creato distribuzione hello tooverify e iniziare a usare hello nuova macchina virtuale. tooconnect tramite SSH, trovare hello o indirizzo IP della macchina virtuale con [Mostra vm az](/cli/azure/vm#show):

```azurecli
az vm show \
   --resource-group myResourceGroup \
   --name myVMDeployed \
   --show-details
```

## <a name="next-steps"></a>Passaggi successivi
È possibile creare più macchine virtuali da un'immagine di macchina virtuale di origine. Se è necessario l'immagine di tooyour toomake modifiche: 

- Creare una macchina virtuale da un'immagine dell'utente.
- Apportare aggiornamenti o modifiche alla configurazione.
- Seguire hello passaggi nuovamente toodeprovision, rilasciare, generalizzare e creare un'immagine.
- Usare la nuova immagine per le distribuzioni future. Se necessario, eliminare l'immagine originale hello.

Per ulteriori informazioni sulla gestione delle macchine virtuali con hello CLI, vedere [CLI di Azure 2.0](/cli/azure/overview).
