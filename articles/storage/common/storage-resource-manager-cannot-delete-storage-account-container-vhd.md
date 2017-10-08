---
title: aaaTroubleshoot errori quando si elimina l'account di archiviazione di Azure, contenitori o i dischi rigidi virtuali | Documenti Microsoft
description: Risolvere gli errori quando si eliminano account di archiviazione, contenitori o dischi rigidi virtuali di Azure
services: storage
documentationcenter: 
author: genlin
manager: cshepard
editor: na
tags: storage
ms.assetid: 17403aa1-fe8d-45ec-bc33-2c0b61126286
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.openlocfilehash: 33261562a2dd2614b35bc1118924513f8c624d6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-errors-when-you-delete-azure-storage-accounts-containers-or-vhds"></a>Risolvere gli errori quando si eliminano account di archiviazione, contenitori o dischi rigidi virtuali di Azure

È possibile ricevere errori quando si tenta di toodelete un account di archiviazione di Azure, un contenitore o un disco rigido virtuale (VHD) in hello [portale di Azure](https://portal.azure.com). Questo articolo fornisce la risoluzione di problemi di indicazioni toohelp resolve hello in una distribuzione di gestione risorse di Azure.

Se in questo articolo non risolve il problema di Azure, visitare la pagina hello forum di Azure in [MSDN e l'Overflow dello Stack](https://azure.microsoft.com/support/forums/). È possibile registrare il problema in questi forum o too@AzureSupport su Twitter. Inoltre, è possibile inviare una richiesta di supporto tecnico di Azure selezionando **ottenere supporto** su hello [supporto tecnico di Azure](https://azure.microsoft.com/support/options/) sito.

## <a name="symptoms"></a>Sintomi
### <a name="scenario-1"></a>Scenario 1
Quando si tenta di toodelete un disco rigido virtuale in un account di archiviazione in una distribuzione di gestione delle risorse, viene visualizzato hello seguente messaggio di errore:

**Non è stato possibile blob toodelete 'vhds/BlobName.vhd'. Errore: Non è presente un lease sul blob hello ed è stato specificato alcun ID lease nella richiesta di hello.**

Questo problema può verificarsi perché la macchina virtuale (VM) è un lease sul disco rigido virtuale che si sta tentando di toodelete hello.

### <a name="scenario-2"></a>Scenario 2
Quando si tenta di toodelete un contenitore in un account di archiviazione in una distribuzione di gestione delle risorse, viene visualizzato hello seguente messaggio di errore:

**Non è stato possibile toodelete archiviazione contenitore 'VHD'. Errore: Non è presente un lease sul contenitore hello ed è stato specificato alcun ID lease nella richiesta di hello.**

Questo problema può verificarsi poiché hello contenitore dispone di un disco rigido virtuale che è stato bloccato nello stato di lease hello.

### <a name="scenario-3"></a>Scenario 3
Quando si tenta di toodelete un account di archiviazione in una distribuzione di gestione delle risorse, viene visualizzato hello seguente messaggio di errore:

**Account di archiviazione toodelete 'StorageAccountName' non è riuscito. Errore: Impossibile eliminare l'account di archiviazione hello a causa di elementi tooits in uso.**

Questo problema può verificarsi perché l'account di archiviazione hello contiene un disco rigido virtuale che si trova in stato di lease hello.

## <a name="solution"></a>Soluzione 
tooresolve questi problemi, è necessario identificare hello disco rigido virtuale che ha causato l'errore hello e hello associati macchina virtuale. Quindi, scollegare hello disco rigido virtuale da hello VM (per i dischi di dati) o eliminare hello VM che utilizza hello disco rigido virtuale (per i dischi del sistema operativo). Questo rimuove lease hello hello disco rigido virtuale e ne consente toobe eliminato. 

toodo questo, utilizzare uno dei seguenti metodi hello:

### <a name="method-1---use-azure-storage-explorer"></a>Metodo 1: usare Esplora archivi di Azure

### <a name="step-1-identify-hello-vhd-that-prevent-deletion-of-hello-storage-account"></a>Passaggio 1 identificare hello disco rigido virtuale che impediscono l'eliminazione dell'account di archiviazione hello

1. Quando si elimina l'account di archiviazione hello, si riceverà una finestra di messaggio come illustrato di seguito hello: 

    ![messaggio durante l'eliminazione di account di archiviazione hello](././media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. Controllare hello **disco URL** account di archiviazione tooidentify hello e hello disco rigido virtuale che non è possibile eliminare l'account di archiviazione di hello. Nell'esempio seguente di hello, hello stringa prima di ". n e t" nome account di archiviazione hello e "SCCM2012-2015-08-28.vhd" è il nome di file VHD hello.  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

### <a name="step-2-delete-hello-vhd-by-using-azure-storage-explorer"></a>Hello di eliminazione passaggio 2 VHD tramite Esplora archivi Azure

1. Download e installazione hello versione [Azure Storage Explorer](http://storageexplorer.com/). Questo strumento è un'applicazione autonoma di Microsoft che consente di utilizzare tooeasily dati di archiviazione di Azure in Windows, macOS e Linux.
2. Aprire Esplora archivi di Azure, selezionare ![icona account](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/account.png) Nella barra sinistra hello, selezionare l'ambiente di Azure e quindi eseguire l'accesso.

3. Selezionare tutte le sottoscrizioni o sottoscrizione hello che contiene l'account di archiviazione hello da toodelete.

    ![aggiungere sottoscrizione](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/addsub.png)

4. Passare l'account di archiviazione toohello che sono stati ottenuti da hello disco URL precedenti, seleziona hello **contenitori Blob** > **dischi rigidi virtuali** e cercare hello disco rigido virtuale che impedisce di account di archiviazione hello di eliminazione.
5. Se viene trovato hello disco rigido virtuale, controllare hello **nome della macchina virtuale** hello toofind colonna VM che utilizza questo disco rigido virtuale.

    ![Controllare la macchina virtuale](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/check-vm.png)

6. Rimuovere il lease hello hello VHD tramite il portale di Azure. Per ulteriori informazioni, vedere [lease hello rimuovere dal disco rigido virtuale hello](#remove-the-lease-from-the-vhd). 

7. Passare toohello Azure Storage Explorer, fare doppio clic su hello disco rigido virtuale e quindi selezionare Elimina.

8. Eliminare l'account di archiviazione hello.

### <a name="method-2---use-azure-portal"></a>Metodo 2: Usare il portale di Azure 

#### <a name="step-1-identify-hello-vhd-that-prevent-deletion-of-hello-storage-account"></a>Passaggio 1: Identificare hello disco rigido virtuale che impediscono l'eliminazione dell'account di archiviazione hello

1. Quando si elimina l'account di archiviazione hello, si riceverà una finestra di messaggio come illustrato di seguito hello: 

    ![messaggio durante l'eliminazione di account di archiviazione hello](././media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. Controllare hello **disco URL** account di archiviazione tooidentify hello e hello disco rigido virtuale che non è possibile eliminare l'account di archiviazione di hello. Nell'esempio seguente di hello, hello stringa prima di ". n e t" nome account di archiviazione hello e "SCCM2012-2015-08-28.vhd" è il nome di file VHD hello.  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

2. Accedi toohello [portale di Azure](https://portal.azure.com).
3. Nel menu Hub hello, selezionare **tutte le risorse**. Account di archiviazione toohello scegliere quindi **BLOB** > **dischi rigidi virtuali**.

    ![Schermata del portale di hello, con l'account di archiviazione hello e contenitore "VHD" hello evidenziato](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/opencontainer.png)

4. Individuare hello disco rigido virtuale che sono stati ottenuti dall'URL disco hello in precedenza. Quindi, determinare quale utilizza VM hello disco rigido virtuale. In genere, è possibile determinare la macchina virtuale contiene hello VHD controllando nome del disco rigido virtuale hello:

Macchina virtuale nel modello di sviluppo di Resource Manager

   * I dischi sistema operativo in genere seguono questa convenzione di denominazione: VMName-YYYY-MM-DD-HHMMSS.vhd
   * I dischi dati in genere seguono questa convenzione di denominazione: VMName-YYYY-MM-DD-HHMMSS.vhd

Macchina virtuale nel modello di sviluppo classico

   * I dischi sistema operativo in genere seguono questa convenzione di denominazione: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd
   * I dischi dati in genere seguono questa convenzione di denominazione: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd

#### <a name="step-2-remove-hello-lease-from-hello-vhd"></a>Passaggio 2: Rimuovere i lease hello da hello disco rigido virtuale

[Rimuovere il lease hello hello VHD](#remove-the-lease-from-the-vhd), quindi eliminare l'account di archiviazione hello.

## <a name="what-is-a-lease"></a>Che cos'è un lease?
Un lease non è un blocco che può essere utilizzato toocontrol accesso tooa blob (ad esempio, un disco rigido virtuale). Quando esiste un lease per un blob, solo i proprietari di hello del lease hello possono accedere blob hello. Un lease è importante per hello seguenti motivi:

* Impedisce il danneggiamento dei dati se più proprietari tenta toowrite toohello stessa parte di blob hello in hello contemporaneamente.
* Blob hello impedisce che venga eliminato se si sta utilizzando attivamente il (ad esempio, una macchina virtuale).
* Account di archiviazione hello impedisce che venga eliminato se si sta utilizzando attivamente il (ad esempio, una macchina virtuale).

### <a name="remove-hello-lease-from-hello-vhd"></a>Rimuovere il lease hello hello disco rigido virtuale
Se hello disco rigido virtuale è un disco del sistema operativo, è necessario eliminare lease hello tooremove di hello VM:

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. In hello **Hub** dal menu **macchine virtuali**.
3. Selezionare una macchina virtuale che contiene un lease sul disco rigido virtuale hello hello.
4. Assicurarsi che non sta utilizzando attivamente hello di macchina virtuale e che è non è più necessario hello macchina virtuale.
5. Nella parte superiore di hello di hello **dettagli VM** pannello seleziona **eliminare**, quindi fare clic su **Sì** tooconfirm.
6. Hello VM deve essere eliminato, ma può essere conservato hello disco rigido virtuale. Tuttavia, hello disco rigido virtuale non è più necessario disporre di un lease su di esso. Potrebbe richiedere alcuni minuti per hello lease toobe rilasciato. tooverify che hello lease viene rilasciato, andare troppo**tutte le risorse** > **nome Account di archiviazione** > **BLOB**  >  **dischi rigidi virtuali**. In hello **Blob proprietà** riquadro, hello **stato Lease** il valore deve essere **sbloccata**.

Se hello disco rigido virtuale è un disco dati, scollegare hello disco rigido virtuale da lease hello tooremove di hello VM:

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. In hello **Hub** dal menu **macchine virtuali**.
3. Selezionare una macchina virtuale che contiene un lease sul disco rigido virtuale hello hello.
4. Selezionare **dischi** su hello **dettagli VM** blade.
5. Selezionare i dischi dati hello che mantiene un lease su hello disco rigido virtuale. È possibile specificare quale disco rigido virtuale sia collegato in disco hello controllando URL hello di hello disco rigido virtuale.
6. Stabilire con certezza che non sta utilizzando attivamente disco dati hello.
7. Fare clic su **scollegamento** su hello **disco dettagli** blade.
8. disco Hello deve ora essere disconnesse dal hello VM e hello disco rigido virtuale non è più necessario un lease su di esso. Potrebbe richiedere alcuni minuti per hello lease toobe rilasciato. è stata rilasciata tooverify che hello lease, andare troppo**tutte le risorse** > **nome Account di archiviazione** > **BLOB**  >  **dischi rigidi virtuali**. In hello **Blob proprietà** riquadro, hello **stato Lease** il valore deve essere **sbloccata**.

## <a name="next-steps"></a>Passaggi successivi
* [Eliminare un account di archiviazione](storage-create-storage-account.md#delete-a-storage-account)
* [La modalità di blocco del lease dell'archiviazione blob toobreak hello in Microsoft Azure (PowerShell)](https://gallery.technet.microsoft.com/scriptcenter/How-to-break-the-locked-c2cd6492)
