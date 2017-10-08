---
title: aaaCapture un'immagine di una VM Linux | Documenti Microsoft
description: Informazioni su come toocapture creata un'immagine di una basata su Linux Azure macchina virtuale (VM) con il modello di distribuzione classica hello.
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 17d7ffee-a58e-4290-9de1-64c3cf1ddc05
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: iainfou
ms.openlocfilehash: 33c4059d5bb919a86bdc3492abca540750f365ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocapture-a-classic-linux-virtual-machine-as-an-image"></a>Come toocapture una macchina virtuale di Linux classica come un'immagine
> [!IMPORTANT]
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni. Informazioni su come troppo[eseguire questi passaggi tramite il modello di gestione risorse di hello](../capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

In questo articolo illustra come toocapture una classica macchina virtuale di Azure (VM) che eseguono Linux come un'immagine toocreate altre macchine virtuali. Questa immagine include disco del sistema operativo hello e dischi dati collegati toohello macchina virtuale. Configurazione di rete, non include pertanto è necessario tooconfigure che quando si crea hello altra macchina virtuale dall'immagine hello.

Archivi Azure hello immagine in **immagini**, insieme a tutte le immagini caricate dall'utente. Per altre informazioni sulle immagini, vedere [Informazioni sulle immagini di macchine virtuali in Azure][About Virtual Machine Images in Azure].

## <a name="before-you-begin"></a>Prima di iniziare
Questa procedura presuppone di aver già creato una macchina virtuale di Azure con modello di distribuzione classica hello e del sistema operativo configurato hello, incluso il collegamento a eventuali dischi dati. Se è necessario toocreate una macchina virtuale, leggere [come una macchina virtuale Linux tooCreate][How tooCreate a Linux Virtual Machine].

## <a name="capture-hello-virtual-machine"></a>Acquisire una macchina virtuale hello
1. [Connettersi toohello VM](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) utilizzando un client SSH di propria scelta.
2. Nella finestra hello SSH, digitare hello comando seguente. l'output di Hello `waagent` possono variare leggermente a seconda della versione di hello di questa utilità:

    ```bash
    sudo waagent -deprovision+user
    ```

    Hello precedente comando tenta di sistema hello tooclean e rendono adatto per la riconfigurazione. Questa operazione esegue hello seguenti attività:

   * Rimuove le chiavi SSH host (se Provisioning.RegenerateSshHostKeyPair 'y' nel file di configurazione hello)
   * Cancella la configurazione NameServer in /etc/resolv.conf
   * Rimuove hello `root` password utente di ecc/shadow (se Provisioning.DeleteRootPassword 'y' nel file di configurazione hello)
   * Rimuove i lease client DHCP memorizzati nella cache
   * Reimposta host toolocalhost.localdomain nome
   * Elimina account provisioning utente ultimo hello (ottenuto dal /var/lib/waagent) **e i dati associati**.

     > [!NOTE]
     > Deprovisioning Elimina i file e dati troppo "generalizzare" hello immagine. Solo il seguente comando in una macchina virtuale che si desidera toocapture come nuovo modello di immagine. Non garantisce che l'immagine hello viene cancellato di tutte le informazioni riservate o adatto per le parti toothird di ridistribuzione.

3. Tipo **y** toocontinue. È possibile aggiungere hello `-force` tooavoid parametro questo passaggio di conferma.
4. Tipo **uscita** client di tooclose hello SSH.

   > [!NOTE]
   > Hello rimanenti passaggi si presuppone che si dispone già di [installato hello Azure CLI](../../../cli-install-nodejs.md) nel computer client. Hello tutti i passaggi può essere eseguite anche in hello [portale di Azure](http://portal.azure.com).

5. Dal computer client, aprire Azure CLI e account di accesso tooyour sottoscrizione di Azure. Per informazioni dettagliate, leggere [connettersi tooan sottoscrizione di Azure da hello Azure CLI](../../../xplat-cli-connect.md).

   > [!NOTE]
   > Nel portale di Azure hello, accedi toohello portale.

6. Assicurarsi che sia attiva la modalità Gestione dei servizi:

    ```azurecli
    azure config mode asm
    ```

7. Arrestare hello macchina virtuale che è già sottoposta a deprovisioning. Hello seguente arresta macchina virtuale denominata hello `myVM`:

    ```azurecli
    azure vm shutdown myVM
    ```
   Se necessario, è possibile visualizzare un elenco di hello tutte le macchine virtuali creato nella sottoscrizione mediante`azure vm list`

   > [!NOTE]
   > Se si usa hello portale di Azure, selezionare hello macchina virtuale e fare clic su **arrestare** arrestare hello macchina virtuale.

8. Quando viene arrestato hello VM, acquisire l'immagine di hello. Hello dopo le acquisizioni di esempio hello macchina virtuale denominata `myVM` e crea un'immagine generalizzata denominata `myNewVM`:

    ```azurecli
    azure vm capture -t myVM myNewVM
    ```

    Hello `-t` sottocomando eliminazioni hello macchina virtuale originale.

    > [!NOTE]
    > Nel portale di Azure hello, è possibile acquisire un'immagine selezionando **immagine** dal menu di hub hello. È necessario hello toosupply le seguenti informazioni per l'immagine di hello: nome gruppo di risorse, posizione, tipo di sistema operativo e percorso di archiviazione blob.

9. Hello nuova immagine è ora disponibile nell'elenco di hello delle immagini che possono essere tooconfigure di utilizzare qualsiasi nuova macchina virtuale. È possibile visualizzarli con il comando hello:

   ```azurecli
   azure vm image list
   ```

   In hello [portale di Azure](http://portal.azure.com), hello nuova immagine viene visualizzata in hello **immagini di macchina virtuale (classico)** appartenente toohello **calcolo** servizi. È possibile accedere a **immagini di macchina virtuale (classico)** facendo _più servizi_ nella parte inferiore di hello di hello Azure service elenco e quindi cercare nella hello **calcolo** servizi.   

   ![Acquisizione dell'immagine eseguita correttamente](./media/capture-image/VMCapturedImageAvailable.png)

## <a name="next-steps"></a>Passaggi successivi
immagine di Hello è pronto toobe utilizzato toocreate macchine virtuali. È possibile utilizzare il comando di Azure CLI hello `azure vm create` e specificare il nome dell'immagine hello creato. Per ulteriori informazioni, vedere [Using hello CLI di Azure con il modello di distribuzione classica](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).

In alternativa, utilizzare hello [portale di Azure](http://portal.azure.com) toocreate una macchina virtuale personalizzata tramite hello **immagine** (metodo) e selezionando hello immagine creata. Per ulteriori informazioni, vedere [come una macchina virtuale personalizzata tooCreate][How tooCreate a Custom Virtual Machine].

**Vedere anche:** [Manuale dell'utente dell'agente Linux di Azure](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[About Virtual Machine Images in Azure]:../../virtual-machines-linux-classic-about-images.md
[How tooCreate a Custom Virtual Machine]:create-custom.md
[How tooAttach a Data Disk tooa Virtual Machine]:attach-disk.md
[How tooCreate a Linux Virtual Machine]:create-custom.md
