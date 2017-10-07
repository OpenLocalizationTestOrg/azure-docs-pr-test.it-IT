---
title: in un pool da immagini personalizzate aaaProvision Azure Batch | Documenti Microsoft
description: "È possibile creare un pool da un'immagine personalizzata di tooprovision calcolo nodi che contengono software hello e i dati necessari per l'applicazione di Batch. Immagini personalizzate sono un modo efficiente tooconfigure i carichi di lavoro Batch toorun nodi di calcolo."
services: batch
author: tamram
manager: timlt
ms.service: batch
ms.topic: article
ms.date: 08/07/2017
ms.author: tamram
ms.openlocfilehash: 5cb698ee90f7d3ec9ffe69fa4dc602132c3f7569
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-a-custom-image-toocreate-a-pool-of-virtual-machines"></a>Utilizzare toocreate un'immagine personalizzata un pool di macchine virtuali

Quando si crea un pool di macchine virtuali in Azure Batch, specificare un'immagine di macchina virtuale (VM) che fornisce hello del sistema operativo per ogni nodo di calcolo nel pool di hello. È possibile creare un pool di macchine virtuali usando un'immagine di Azure Marketplace oppure fornendo un'immagine di disco rigido virtuale personalizzata preparata. Quando si specifica un'immagine personalizzata, è possibile controllo sulla configurazione del sistema operativo hello in fase di hello che viene eseguito il provisioning di ogni nodo di calcolo. L'immagine personalizzata è incluse anche le applicazioni e dati di riferimento che sono disponibili in hello nodo di calcolo non appena è disponibile.

Utilizza un'immagine personalizzata può risparmiare tempo durante il recupero di nodi di calcolo del pool pronto toorun il carico di lavoro di Batch. Benché sia sempre possibile usare un'immagine di Azure Marketplace e installare il software in ogni nodo di calcolo dopo averne effettuato il provisioning, questo approccio può rivelarsi meno efficiente rispetto all'uso di un'immagine personalizzata. 

Un'immagine personalizzata che è configurata per lo scenario di toouse alcuni motivi includono la necessità di:

- **Configurare il sistema operativo hello (sistema operativo)** alcuna configurazione particolare del sistema operativo hello può essere eseguite su immagine personalizzata hello. 
- **Installare applicazioni di grandi dimensioni.** L'installazione di applicazioni in un'immagine personalizzata è più efficiente che installarle in ogni nodo di calcolo dopo averne effettuato il provisioning.
- **Copiare quantità significative di dati.** Se i dati di hello immagine personalizzata toohello copiato, deve solo toobe copiati una volta, anziché del nodo di calcolo tooeach, risparmiando tempo e la larghezza di banda.
- **Riavviare il computer hello VM durante il processo di installazione di hello.** Riavvio hello VM può essere un processo richiede molto tempo, soprattutto se si dispone di un numero di nodi di calcolo.

## <a name="prerequisites"></a>Prerequisiti

- **Un account Batch è stato creato con la modalità di allocazione del pool di hello sottoscrizione utente.** toouse un pool di macchine virtuali tooprovision immagine personalizzata, creare un account Batch con hello sottoscrizione utente [modalità di allocazione del pool](batch-api-basics.md#pool-allocation-mode). In questa modalità, il pool di Batch viene allocato nella sottoscrizione hello in cui risiede l'account di hello. Vedere hello [Account](batch-api-basics.md#account) sezione [paralleli su larga scala di sviluppare soluzioni con Batch di calcolo](batch-api-basics.md) per informazioni sull'impostazione di modalità di allocazione del pool di hello quando si crea un account Batch.

- Un **account di archiviazione di Azure**. toocreate un pool di macchine virtuali mediante un'immagine personalizzata, è necessario un account di archiviazione di Azure standard, di uso generale in hello stessa sottoscrizione e area. Se si crea un'immagine personalizzata da una macchina virtuale di Azure, si copierà hello immagine toohello account di archiviazione in cui si trova su disco del sistema operativo della macchina virtuale di hello e non sarà necessario toocreate un account di archiviazione separata. 
    
## <a name="prepare-a-custom-image"></a>Preparare un'immagine personalizzata

tooprepare un'immagine personalizzata per l'utilizzo con Batch, è necessario generalizzare un'installazione esistente di Linux o Windows. La generalizzazione di un'installazione del sistema operativo comporta la rimozione delle informazioni specifiche del computer. il risultato di Hello è un'immagine che può essere installata su altri computer o macchine virtuali.  

> [!IMPORTANT]
> Batch non supporta attualmente l'utilizzo di Azure gestiti immagini tooprovision un pool. immagine personalizzata Hello è utilizzare tooprovision che un pool deve essere archiviato in archiviazione di Azure. 
>
> Quando si prepara un'immagine personalizzata, tenere hello presente seguenti punti:
> - Garantire che un'immagine del sistema operativo base hello è utilizzare tooprovision i pool di Batch non sia una pre-installato le estensioni di Azure, ad esempio estensione Custom Script hello. Se l'immagine di hello contiene un'estensione di pre-installata, Azure potrebbe verificarsi problemi di distribuzione hello macchina virtuale.
> - Garantire che un'immagine del sistema operativo base hello che fornire utilizza hello unità temporanea predefinita, come hello agente nodo Batch attualmente prevista unità temporanea predefinita di hello.
>
>

È possibile usare qualsiasi immagine Windows o Linux preparata esistente come immagine personalizzata. Ad esempio, se si desidera toouse un'immagine locale e quindi caricare l'account di archiviazione di Azure con i tooan immagine hello in hello stessa sottoscrizione e area geografica dell'account Batch usando [AzCopy](../storage/storage-use-azcopy.md) o un altro strumento di caricamento.

È anche possibile preparare un'immagine personalizzata da una VM di Azure nuova o esistente. Se si sta creando una nuova macchina virtuale, è possibile utilizzare un'immagine di Azure Marketplace come immagine di base hello per l'immagine personalizzata e quindi personalizzarlo. immagine di base hello toocustomize, creare una macchina virtuale di Azure e aggiungere le applicazioni o dati tooit. Quindi generalizzare hello VM tooserve come immagine personalizzata e salvarlo tooAzure archiviazione. 

tooprepare un'immagine personalizzata da una macchina virtuale di Azure, seguire questi passaggi:

1. Creare una VM di Azure **non gestita** da un'immagine di Azure Marketplace. Azure Marketplace include immagini sia per [Windows](../virtual-machines/windows/quick-create-portal.md) che per [Linux](../virtual-machines/linux/quick-create-portal.md).
    
    Nel passaggio 3 di hello processo di creazione della macchina virtuale, assicurarsi di selezionare **n** per **archiviazione: utilizzare dischi gestiti** opzione. Prendere nota del nome di account di archiviazione di hello per disco del sistema operativo della macchina virtuale di hello, come l'account di archiviazione è anche in Azure verrà salvato l'immagine personalizzata:

    ![Creare una macchina virtuale non gestita e nome di account di archiviazione hello nota](media/batch-custom-images/vm-create-storage.png)
 
2. Completare il processo di hello di creazione di una macchina virtuale e attendere che toobe allocato da Azure. Di seguito è riportata un'immagine che mostra una macchina virtuale nel portale di Azure in stato di esecuzione hello hello:

    ![Creare una macchina virtuale da un'immagine del marketplace](media/batch-custom-images/vm-status-running.png)

3. Una volta hello macchina virtuale è in esecuzione, connettersi tooit tramite RDP (per Windows) o SSH (per Linux). Installare il software necessario o copiare i dati desiderati e quindi generalizzare hello macchina virtuale. Seguire i passaggi di hello descritti in [Generalize hello VM](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sa-copy-generalized.md#generalize-the-vm). 
   
4. Seguire i passaggi di hello troppo[Accedi tooAzure PowerShell](../virtual-machines/windows/sa-copy-generalized.md#log-in-to-azure-powershell). tooinstall Azure PowerShell, vedere [Panoramica di Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.2.0). 

5. Seguire i passaggi di hello troppo[Deallocate hello VM e set hello stato toogeneralized](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sa-copy-generalized#deallocate-the-vm-and-set-the-state-to-generalized). 

    Nel portale di Azure hello, si noti che hello deallocata:

    ![Verificare che hello deallocata](media/batch-custom-images/vm-status-deallocated.png)

6.  Creare e salvare hello VM immagine tooAzure archiviazione utilizzando hello [Salva AzureRmVMImage](https://docs.microsoft.com/powershell/module/azurerm.compute/save-azurermvmimage) cmdlet di PowerShell. Seguire le istruzioni di hello descritte [Crea immagine hello](../virtual-machines/windows/sa-copy-generalized.md#create-the-image).
    
    immagine di macchina virtuale Hello viene salvato l'account di archiviazione Azure toohello creato quando hello VM è stato creato, come illustrato nel passaggio 1 di questa procedura. cmdlet Save-AzureRmVMImage Hello Salva hello immagine toohello **sistema** contenitore nell'account di archiviazione. Hello `-DestinationContainername` una directory virtuale all'interno di hello di nomi di parametro **sistema** contenitore. Hello `-VHDNamePrefix` parametro specifica un prefisso per il nome di blob hello. Questo prefisso è il nome di blob toohello preceduta da un trattino. 

    Si supponga, ad esempio, che è necessario chiamare Save AzureRmVMImage con hello seguenti parametri:  

        Save-AzureRmVMImage -ResourceGroupName sample-resource-group -Name vm-custom-image -DestinationContainerName batchimages -VHDNamePrefix custom -Path C:\Temp\Images\vm-custom-image.json

    l'immagine risultante Hello viene salvato toohello percorso e nome del blob illustrato di seguito:

    ![Percorso del disco rigido virtuale salvato nel contenitore system](media/batch-custom-images/vhd-in-vm-storage-account.png)

    > [!NOTE]
    > Una VM non gestita di Azure crea più account di archiviazione per scopi diversi. Se non è stato annotato nome hello hello del contenitore dell'archiviazione per il disco del sistema operativo hello quando hello macchina virtuale è stata creata, quindi trovare account di archiviazione di hello associata che contiene hello **sistema** contenitore. Spostarsi tra hello **sistema** toofind hello personalizzato immagine contenitore con i valori hello specificati per hello **Salva AzureRmVMImage** comando.

## <a name="create-a-pool-from-a-custom-image-in-hello-portal"></a>Creare un pool da un'immagine personalizzata nel portale di hello

Dopo avere salvato l'immagine personalizzata e conoscendone il percorso, è possibile creare un pool di Batch da tale immagine. Seguire questi toocreate passaggi un pool da hello portale di Azure:

1. Passare l'account Batch tooyour in hello portale di Azure. Questo account deve essere hello stessa sottoscrizione e area come archiviazione hello account immagine personalizzata di hello che lo contiene. 
2. In hello **impostazioni** finestra hello a sinistra, seleziona hello **pool** voce di menu.
3. In hello **pool** finestra, seleziona hello **Aggiungi** comando.
4. In hello **Aggiungi Pool** selezionare **immagine personalizzata (Linux/Windows)** da hello **tipo di immagine** elenco a discesa. portale Hello Visualizza hello **immagine personalizzata** selezione. Passare toohello account di archiviazione in cui si trova l'immagine personalizzata e selezionare hello VHD desiderato dal contenitore hello. 
5. Seleziona hello corretto **offerta/server di pubblicazione/Sku** per il disco rigido virtuale personalizzato.
6. Specificare hello rimanenti impostazioni, tra cui hello **dimensioni nodo**, **dedicato i nodi di destinazione**, e **nodi per priorità bassa**, nonché qualsiasi desiderato impostazioni facoltative.

    Ad esempio, per un'immagine personalizzata di Microsoft Windows Server Datacenter 2016, hello **Aggiungi Pool** verrà visualizzata la finestra, come illustrato di seguito:

    ![Aggiungere un pool da un'immagine di Windows personalizzata](media/batch-custom-images/add-pool-custom-image.png)
  
toocheck se un pool esistente è basato su un'immagine personalizzata, vedere hello **del sistema operativo** proprietà nella sezione di riepilogo risorse hello di hello **Pool** finestra. Se il pool di hello è stato creato da un'immagine personalizzata, è impostato troppo**immagine di macchina virtuale personalizzata**.

Vengono visualizzati tutti i dischi rigidi virtuali personalizzati associati a un pool nel pool di hello **proprietà** finestra.
 
## <a name="next-steps"></a>Passaggi successivi

- Per una panoramica dettagliata di Batch, vedere [Sviluppare soluzioni di calcolo parallele su larga scala con Batch](batch-api-basics.md).
- Per informazioni sulla creazione di un account Batch, vedere [creare un account Batch con il portale di Azure hello](batch-account-create-portal.md).
