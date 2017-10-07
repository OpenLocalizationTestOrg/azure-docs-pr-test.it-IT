---
title: eliminazione di account di archiviazione di Azure, contenitori o i dischi rigidi virtuali in una distribuzione classica aaaTroubleshoot | Documenti Microsoft
description: Risolvere i problemi eliminando account di archiviazione di Azure, contenitori o dischi rigidi virtuali in una distribuzione classica
services: storage
documentationcenter: 
author: genlin
manager: felixwu
editor: tysonn
tags: storage
ms.assetid: 0f7a8243-d8dc-432a-9d37-1272a0cb3a5c
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.openlocfilehash: 6bbfa032e1968718c623227bb426d553e2951075
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deleting-azure-storage-accounts-containers-or-vhds-in-a-classic-deployment"></a>Risolvere i problemi eliminando account di archiviazione di Azure, contenitori o dischi rigidi virtuali in una distribuzione classica
[!INCLUDE [storage-selector-cannot-delete-storage-account-container-vhd](../../includes/storage-selector-cannot-delete-storage-account-container-vhd.md)]

È possibile ricevere errori quando si tenta di account di archiviazione di Azure hello toodelete, contenitore o disco rigido virtuale in hello [portale di Azure](https://portal.azure.com/) o hello [portale di Azure classico](https://manage.windowsazure.com/). problemi di Hello possono essere causati da hello seguenti circostanze:

* Quando si elimina una macchina virtuale, disco hello e disco rigido virtuale non vengono automaticamente eliminati. Che potrebbe essere motivo hello per errore di eliminazione dell'account di archiviazione. È non eliminare il disco di hello in modo che è possibile utilizzare hello disco toomount un'altra macchina virtuale.
* È ancora presente un lease su un blob del disco o hello associata disco hello.
* È ancora presente un'immagine di VM che usa un BLOB, un contenitore o un account di archiviazione.

Se il problema di Azure non viene risolto in questo articolo, visitare hello forum di Azure in [MSDN e hello Overflow dello Stack](https://azure.microsoft.com/support/forums/). È possibile registrare il problema in questi forum o too@AzureSupport su Twitter. Inoltre, è possibile inviare una richiesta di supporto tecnico di Azure selezionando **ottenere supporto** su hello [supporto tecnico di Azure](https://azure.microsoft.com/support/options/) sito.

## <a name="symptoms"></a>Sintomi
Hello seguente sezione vengono elencati gli errori comuni che potrebbero essere visualizzati quando si tenta di account di archiviazione di Azure hello toodelete, contenitori o i dischi rigidi virtuali.

### <a name="scenario-1-unable-toodelete-a-storage-account"></a>Scenario 1: Impossibile toodelete un account di archiviazione
Quando ci si sposta account di archiviazione classico toohello in hello [portale di Azure](https://portal.azure.com/) e selezionare **eliminare**, è possibile che visualizzata con un elenco di oggetti che impediscono l'eliminazione dell'account di archiviazione hello:

  ![Immagine di errore quando eliminare account di archiviazione hello](./media/storage-cannot-delete-storage-account-container-vhd/newerror.png)

Quando ci si sposta toohello account di archiviazione in hello [portale di Azure classico](https://manage.windowsazure.com/) e selezionare **eliminare**, si potrebbe manifestarsi uno dei seguenti errori hello:

- *L'account di archiviazione StorageAccountName contiene immagini di VM. Assicurarsi di rimuovere queste immagini prima di eliminare questo account di archiviazione.*

- *Account di archiviazione toodelete < vm-storage-account-name > non è riuscito. Account di archiviazione non è possibile toodelete < vm-storage-account-name >: ' account di archiviazione < vm-storage-account-name > include alcune immagini attive e/o dischi. Assicurarsi di rimuovere tali immagini e/o dischi prima di eliminare l'account di archiviazione.*

- *L'account di archiviazione<nome-account-archiviazione-vm> presenta alcune immagini e/o dischi attivi, ad esempio xxxxxxxxx- xxxxxxxxx-O-209490240936090599. Assicurarsi di rimuovere tali immagini e/o dischi prima di eliminare l'account di archiviazione.*

- *L'account di archiviazione &lt;nome-account-archiviazione-vm&gt; presenta 1 contenitore con un'immagine attiva e/o elementi di disco. Verificare che tali elementi vengono rimossi dal repository immagini hello prima di eliminare questo account di archiviazione*.

- *Invio non riuscito L'account di archiviazione &lt;nome-account-archiviazione-vm&gt; presenta 1 contenitore con un'immagine attiva e/o elementi di disco. Verificare che tali elementi vengono rimossi dal repository immagini hello prima di eliminare questo account di archiviazione. Quando si tenta di toodelete un account di archiviazione e che siano ancora attivi dischi associati, si verrà visualizzato un messaggio per indicare che esistono i dischi attivi che richiedono toobe eliminato*.

### <a name="scenario-2-unable-toodelete-a-container"></a>Scenario 2: Impossibile toodelete un contenitore
Quando si tenta di contenitore di archiviazione toodelete hello, potresti vedere hello errore seguente:

*Contenitore di archiviazione non riuscite toodelete <container name>. Errore: ' non è presente un lease sul contenitore hello ed è stato specificato alcun ID lease nella richiesta di hello*.

Or

*Hello dischi della macchina virtuale seguenti utilizza BLOB in questo contenitore, pertanto hello contenitore non può essere eliminato: VirtualMachineDiskName1, VirtualMachineDiskName2,...*

### <a name="scenario-3-unable-toodelete-a-vhd"></a>Scenario 3: Impossibile toodelete un disco rigido virtuale
Dopo che si elimina una macchina virtuale e quindi provare a toodelete hello BLOB per hello associata dischi rigidi virtuali, è possibile ricevere hello seguente messaggio:

*Blob toodelete non riuscita ' percorso/XXXXXX-XXXXXX-os-1447379084699.vhd'. Errore: ' non è presente un lease sul blob hello ed è stato specificato alcun ID lease nella richiesta di hello.*

Or

*BLOB 'BlobName.vhd' è in uso come disco di macchina virtuale 'VirtualMachineDiskName', pertanto hello non può essere eliminato.*

## <a name="solution"></a>Soluzione
problemi più comuni di hello tooresolve, provare a hello seguente metodo:

### <a name="step-1-delete-any-disks-that-are-preventing-deletion-of-hello-storage-account-container-or-vhd"></a>Passaggio 1: Eliminare i dischi che impediscono l'eliminazione di account di archiviazione hello, contenitore o disco rigido virtuale
1. Passare toohello [portale di Azure classico](https://manage.windowsazure.com/).
2. Selezionare **MACCHINA VIRTUALE** > **DISCHI**.

    ![Immagine di dischi all'interno di macchine virtuali nel Portale di Azure classico.](./media/storage-cannot-delete-storage-account-container-vhd/VMUI.png)
3. Individuare i dischi che sono associati account di archiviazione hello, contenitore o disco rigido virtuale che si desidera toodelete hello. Quando si seleziona il percorso di hello del disco di hello, si noterà hello associati account di archiviazione, contenitore o disco rigido virtuale.

    ![Immagine che mostra le informazioni sulla posizione per i dischi nel Portale di Azure classico](./media/storage-cannot-delete-storage-account-container-vhd/DiskLocation.png)
4. Eliminare i dischi hello utilizzando uno dei seguenti metodi hello:

  - Se è presente alcuna macchina virtuale è elencato nella hello **collegato a** campo disco hello, è possibile eliminare il disco hello direttamente.

  - Se il disco di hello è un disco dati, seguire questi passaggi:

    1. Controllare nome hello della macchina virtuale che hello disco è collegato a hello.
    2. Andare troppo**macchine virtuali** > **istanze**, quindi individuare hello macchina virtuale.
    3. Assicurarsi che non sta utilizzando attivamente disco hello.
    4. Selezionare **Scollega disco** nella parte inferiore di hello del disco di hello toodetach portale hello.
    5. Andare troppo**macchine virtuali** > **dischi**e attendere hello **collegato a** tooturn campo vuoto. Ciò indica disco hello è disconnesso da hello VM.
    6. Selezionare **eliminare** in fondo hello **macchine virtuali** > **dischi** disco hello toodelete.

  - Se il disco di hello è un disco del sistema operativo (hello **OS contiene** campo ha un valore come Windows) e collegato tooa macchina virtuale, seguire questi passaggi hello toodelete macchina virtuale. disco del sistema operativo Hello non è possibile scollegare, quindi è necessario il lease hello toorelease di toodelete hello macchina virtuale.

    1. Controllare nome hello di hello di hello macchina virtuale che è collegato il disco dati.  
    2. Andare troppo**macchine virtuali** > **istanze**, e quindi seleziona hello macchina virtuale che hello disco è collegato.
    3. Assicurarsi che non sta utilizzando attivamente hello di macchina virtuale e che è non è più necessario hello macchina virtuale.
    4. Selezionare hello VM hello disco è collegato a, quindi selezionare **eliminare** > **hello Elimina dischi collegati**.
    5. Andare troppo**macchine virtuali** > **dischi**e attendere toodisappear disco hello.  Potrebbe richiedere alcuni minuti prima che questo toooccur e potrebbe essere necessario pagina hello toorefresh.
    6. Se il disco di hello non scomparsa, attendere hello **collegato a** tooturn campo vuoto. Ciò indica disco hello è completamente scollegato dalla macchina virtuale hello.  Quindi, selezionare il disco hello e selezionare **eliminare** nella parte inferiore di hello di hello pagine toodelete hello disco.


   > [!NOTE]
   > Se un disco collegato tooa VM, non sarà in grado di toodelete è. I dischi vengono scollegati da una VM eliminata in modo asincrono. Potrebbe richiedere alcuni minuti dopo l'eliminazione di hello VM per questa tooclear campo backup.
   >
   >


### <a name="step-2-delete-any-vm-images-that-are-preventing-deletion-of-hello-storage-account-or-container"></a>Passaggio 2: Eliminare tutte le immagini di macchina virtuale che impediscono l'eliminazione dell'account di archiviazione hello o del contenitore
1. Passare toohello [portale di Azure classico](https://manage.windowsazure.com/).
2. Selezionare **macchina virtuale** > **immagini**, quindi eliminare immagini hello relative agli account di archiviazione hello, contenitore o disco rigido virtuale.

    Successivamente, riprovare account di archiviazione hello toodelete, contenitore o disco rigido virtuale.

> [!WARNING]
> Essere tooback che backup di tutti i desideri toosave prima di eliminare account hello. Quando si elimina un disco rigido virtuale, un BLOB, una tabella, una coda o un file, l'elemento viene eliminato definitivamente. Verificare che la risorsa hello non è in uso.
>
>

## <a name="about-hello-stopped-deallocated-status"></a>Su hello stato arrestato (deallocato)
Macchine virtuali che sono state create nel modello di distribuzione classica hello e che sono state mantenute avrà hello **arrestato (deallocato)** stato di entrambi hello [portale di Azure](https://portal.azure.com/) o [portale di Azure classico ](https://manage.windowsazure.com/).

**Portale di Azure classico**:

![Stato Arrestato (deallocato) per VM nel Portale di Azure.](./media/storage-cannot-delete-storage-account-container-vhd/moreinfo2.png)

**Portale di Azure**:

![Stato Arrestato (deallocato) per VM nel Portale di Azure classico.](./media/storage-cannot-delete-storage-account-container-vhd/moreinfo1.png)

Uno stato "Arrestato (deallocato)" Rilascia le risorse di computer di hello, ad esempio hello CPU, memoria e rete. i dischi di Hello, tuttavia, vengono mantenuti comunque in modo che è possibile rapidamente ricreare hello VM se necessario. Questi dischi vengono creati all'interno di VHD, che sono supportati da Archiviazione di Azure. account di archiviazione Hello dispone di questi dischi rigidi virtuali e dischi hello con lease i dischi rigidi virtuali.

## <a name="next-steps"></a>Passaggi successivi
* [Eliminare un account di archiviazione](storage-create-storage-account.md#delete-a-storage-account)
