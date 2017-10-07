---
title: " Eliminare un insieme di credenziali dei servizi di ripristino in Azure | Microsoft Docs "
description: "Come toodelete un Backup di Azure e servizi di ripristino dell'insieme di credenziali. Un insieme di credenziali di backup può essere definito come un insieme di credenziali cloud o un insieme di credenziali di ripristino di Azure. Risoluzione dei problemi quando non è possibile eliminare un insieme di credenziali di backup nel portale classico hello o il portale di Azure."
services: service-name
documentationcenter: dev-center-name
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 5fa08157-2612-4020-bd90-f9e3c3bc1806
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: markgal;trinadhk
ms.openlocfilehash: 9047f50f4b2c991fbf2454ddcad08073ec7cd975
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="delete-a-recovery-services-vault"></a>Eliminare un insieme di credenziali dei servizi di ripristino
Hello servizio Backup di Azure è disponibili due tipi di insiemi di credenziali - hello credenziali Backup e l'insieme di credenziali di servizi di ripristino hello. insieme di credenziali Backup Hello ordine di priorità. Quindi hello insieme di credenziali di servizi di ripristino avvento di distribuzioni di gestione risorse di toosupport hello espanso. A causa di hello funzionalità estese e le dipendenze di hello informazioni che devono essere archiviate nell'insieme di credenziali hello, l'eliminazione di un insieme di credenziali di Backup o i servizi di ripristino possono generare confusione. Questo articolo spiega come hello toodelete insiemi di credenziali nel portale classico hello e hello portale di Azure.  

| **Tipo di distribuzione** | **Portale** | **Nome dell'insieme di credenziali** |
| --- | --- | --- |
| Classico |Classico |Insieme di credenziali per il backup |
| Gestione risorse |Azure |Insieme di credenziali dei servizi di ripristino |

> [!NOTE]
> Le credenziali per il backup non consentono di proteggere le soluzioni distribuite con Resource Manager. Tuttavia, è possibile utilizzare un insieme di credenziali di servizi di ripristino tooprotect tradizionalmente distribuito i server e le macchine virtuali.  
>

> [!IMPORTANT]
> È ora possibile aggiornare i servizi archivi di Backup gli insiemi di credenziali tooRecovery. Per informazioni dettagliate, vedere l'articolo hello [aggiornare un tooa insieme di credenziali di Backup dell'insieme di credenziali di servizi di ripristino](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft incoraggia gli utenti tooupgrade insiemi di credenziali di servizi tooRecovery insiemi di credenziali di Backup.<br/> **15 ottobre 2017**, non potrà più insiemi di credenziali Backup a toocreate toouse in grado di PowerShell. <br/> **A partire dal 1° novembre 2017**:
>- Gli insiemi di credenziali di Backup rimanenti verrà automaticamente aggiornato tooRecovery servizi insiemi di credenziali.
>- Si sarà in grado di tooaccess ai dati di backup nel portale classico hello. Utilizzare invece hello Azure tooaccess portale i dati di backup in insiemi di servizi di ripristino.
>

In questo articolo, utilizziamo termine hello, insieme di credenziali, toorefer toohello di modulo generico dell'insieme di credenziali Backup hello o insieme di credenziali di servizi di ripristino. Utilizziamo nome formale hello, insieme di credenziali di Backup o insieme di credenziali di servizi di ripristino, quando è necessario toodistinguish tra insiemi di credenziali hello.

## <a name="deleting-a-recovery-services-vault"></a>Eliminazione di un insieme di credenziali dei servizi di ripristino
L'eliminazione di un insieme di credenziali di servizi di ripristino è un processo in un solo passaggio - *fornito insieme di credenziali hello non contiene risorse*. Prima di poter eliminare un insieme di credenziali di servizi di ripristino, è necessario rimuovere o eliminare tutte le risorse nell'insieme di credenziali hello. Se si tenta di toodelete un insieme di credenziali che contiene le risorse, viene visualizzato un errore di hello seguente immagine:

![Errore di eliminazione dell'insieme di credenziali](./media/backup-azure-delete-vault/vault-deletion-error.png) <br/>

Fino a quando non è stata deselezionata risorse hello dall'insieme di credenziali hello, fare clic su **ripetere** produce hello lo stesso errore. Se è bloccato su questo messaggio di errore, fare clic su **Annulla** e utilizzare hello seguenti passaggi viene risorse hello toodelete nell'insieme di credenziali hello.

### <a name="removing-hello-items-from-a-vault-protecting-a-vm"></a>Rimozione di elementi hello da un insieme di credenziali di protezione di una macchina virtuale
Se si dispone già di servizi di ripristino hello aprire insieme di credenziali, ignorare toohello secondo passaggio.

1. Aprire il portale di Azure hello e aprire insieme di credenziali hello desiderato toodelete hello Dashboard.

   Se non si dispone dell'insieme di credenziali di servizi di ripristino hello bloccato toohello Dashboard, nel menu Hub hello, fare clic su **più servizi** e nell'elenco di hello delle risorse, digitare **servizi di ripristino**. Si inizia a digitare, hello filtri di elenco in base all'input. Fare clic su **Insiemi di credenziali dei servizi di ripristino**.

   ![Creare un insieme di credenziali dei servizi di ripristino - Passaggio 1](./media/backup-azure-delete-vault/open-recovery-services-vault.png) <br/>

   viene visualizzato l'elenco di Hello degli insiemi di credenziali di servizi di ripristino. Dall'elenco di hello, selezionare l'insieme di credenziali di hello desiderato toodelete.

   ![scegliere un insieme di credenziali dall'elenco](./media/backup-azure-work-with-vaults/choose-vault-to-delete.png)
2. In hello credenziali vista, cercare in hello **Essentials** riquadro. toodelete un insieme di credenziali non possono essere presenti tutti gli elementi protetti. Se viene visualizzato un numero diverso da zero, in presenza di **elementi Backup** o **server di gestione di Backup**, è necessario rimuovere gli elementi prima di poter eliminare l'insieme di credenziali hello.

    ![Cercare gli elementi protetti nel riquadro Informazioni di base](./media/backup-azure-delete-vault/contoso-bkpvault-settings.png)

    Macchine virtuali e i file e cartelle sono considerate elementi di Backup e sono elencate in hello **elementi Backup** area del riquadro Essentials hello. Un server DPM è elencato in hello **il Server di gestione di Backup** area del riquadro Essentials hello. **Gli elementi replicati** riguardano toohello servizio Azure Site Recovery.
3. rimozione di hello toobegin gli elementi protetti dall'insieme di credenziali hello, trovare gli elementi di hello nell'insieme di credenziali hello. Nel dashboard dell'insieme di credenziali hello fare clic su **impostazioni**, quindi fare clic su **Backup elementi** tooopen tale pannello.

    ![scegliere un insieme di credenziali dall'elenco](./media/backup-azure-delete-vault/open-settings-and-backup-items.png)

    Hello **elementi Backup** blade dispone di elenchi separati, in base a tipo di elemento di hello: macchine virtuali di Azure o cartelle di File (vedere l'immagine). elenco di tipo di elemento predefinito Hello mostrato è macchine virtuali di Azure. elenco di hello tooview degli elementi di cartelle di File nell'insieme di credenziali hello, selezionare **File-cartelle** dal menu a discesa hello.
4. Prima di poter eliminare un elemento dall'insieme di credenziali hello protegge una macchina virtuale, è necessario arrestare il processo di backup dell'elemento hello ed eliminare dati punto di ripristino hello. Per ogni elemento nell'insieme di credenziali hello, seguire questi passaggi:

    a. In hello **gli elementi di Backup** pannello rapida hello elemento e il menu di scelta rapida hello selezionare **Interrompi backup**.

    ![arrestare il processo di backup hello](./media/backup-azure-delete-vault/stop-the-backup-process.png)

    verrà visualizzata la finestra di blade Interrompi Backup Hello.

    b. In hello **Interrompi Backup** pannello da hello **scegliere un'opzione** dal menu **Elimina dati di Backup** > nome hello del tipo di elemento di hello > e fare clic su **arrestare backup**.

    Nome hello del tipo di elemento di hello, si desidera toodelete tooverify è. Hello **Interrompi Backup** pulsante attiva dopo aver verificato elemento hello. Se non è possibile visualizzare hello casella tootype hello nome della finestra di backup dell'elemento hello, si è scelto di hello **mantenere i dati di Backup** opzione.

    ![Elimina dati di backup](./media/backup-azure-delete-vault/stop-backup-blade-delete-backup-data.png)

    Facoltativamente, è possibile fornire un motivo perché si desidera eliminare i dati di hello e aggiungere un commento. Dopo aver fatto clic **Interrompi Backup**, consentire hello eliminazione processo toocomplete prima di tentare l'insieme di credenziali toodelete hello. tooverify che hello processo è stata completata, controllare i messaggi hello Azure ![Elimina dati di backup](./media/backup-azure-delete-vault/messages.png). <br/>
    Una volta completato il processo di hello, viene visualizzato un messaggio hello processo di backup è stato arrestato e dati di backup hello, per tale elemento, è stati eliminati.

    c. Dopo l'eliminazione di un elemento nell'elenco hello in hello **elementi Backup** menu, fare clic su **aggiornamento** hello toosee elementi nell'insieme di credenziali hello.

      ![Elimina dati di backup](./media/backup-azure-delete-vault/empty-items-list.png)

      Quando non esistono elementi nell'elenco di hello, scorrere toohello **Essentials** riquadro nel pannello dell'insieme di credenziali di Backup hello. Nell'elenco non dovrebbero essere presenti **Elementi di backup**, **Server di gestione di backup** o **Elementi replicati**. Se gli elementi vengono ancora visualizzati nell'insieme di credenziali hello, restituire toostep tre e scegliere un elenco di tipo di elemento diverso.  
5. Quando non sono disponibili altri elementi sulla barra degli strumenti di hello insieme di credenziali, fare clic su **eliminare**.

    ![Elimina dati di backup](./media/backup-azure-delete-vault/delete-vault.png)
6. Fare clic su tooverify che si desidera l'insieme di credenziali hello toodelete **Sì**.

    insieme di credenziali Hello viene eliminato e portale hello restituisce toohello **New** menu del servizio.

## <a name="what-if-i-stopped-hello-backup-process-but-retained-hello-data"></a>Cosa accade se si ha interrotto il processo backup di hello ma mantenuti dati hello?
Se è stato interrotto il processo backup di hello ma accidentalmente *mantenuti* dati hello, è necessario eliminare i dati di backup hello prima di poter eliminare l'insieme di credenziali hello. dati di backup hello toodelete:

1. In hello **gli elementi di Backup** pannello rapida hello elemento e nel menu di scelta rapida hello fare clic su **Elimina dati di backup**.

    ![Elimina dati di backup](./media/backup-azure-delete-vault/delete-backup-data-menu.png)

    Hello **Elimina dati di Backup** apre blade.
2. In hello **Elimina dati di Backup** blade, nome hello del tipo di elemento di hello e fare clic su **eliminare**.

    ![Elimina dati di backup](./media/backup-azure-delete-vault/delete-retained-vault.png)

    Dopo avere eliminato dati hello, restituire toostep 4c e continuare il processo di hello.

## <a name="delete-a-vault-used-tooprotect-a-dpm-server"></a>Eliminare tooprotect un insieme di credenziali utilizzato un server DPM
Prima di poter eliminare tooprotect un insieme di credenziali utilizzato un server DPM, è necessario cancellare i punti di ripristino che sono stati creati e quindi annullare la registrazione di server hello dall'insieme di credenziali hello.

dati hello toodelete associati a un gruppo protezione dati:

1. Nella Console amministrazione DPM hello, fare clic su **protezione** > selezionare un gruppo protezione dati > selezionare hello membro del gruppo protezione > nella barra multifunzione dello strumento di hello, fare clic su **rimuovere**.

  Hello tooactivate di membro del gruppo protezione dati selezionare hello **rimuovere** pulsante nella barra multifunzione dello strumento hello. Nell'esempio hello è membro di hello **dummyvm9**. tooselect più membri nel gruppo protezione dati hello, tenendo premuto Ctrl hello facendo clic su membri hello.

    ![Elimina dati di backup](./media/backup-azure-delete-vault/az-portal-delete-protection-group.png)

    Hello **Arresta protezione dati** verrà visualizzata la finestra di dialogo.
2. In hello **Arresta protezione dati** finestra di dialogo Seleziona **Elimina dati protetti**, fare clic su **Arresta protezione dati**.

    ![Elimina dati di backup](./media/backup-azure-delete-vault/delete-dpm-protection-group.png)

    toodelete un insieme di credenziali, è necessario cancellare o eliminare, insieme di credenziali hello i dati protetti. In base al numero di hello di punti di ripristino e i dati nel gruppo protezione dati hello, potrebbero essere necessari dai dati di alcuni secondi tooseveral minuti toodelete hello. Hello **Arresta protezione dati** finestra di dialogo Mostra lo stato di hello quando hello è stato completato.

    ![Elimina dati di backup](./media/backup-azure-delete-vault/success-deleting-protection-group.png)
3. Continuare questo processo per tutti i membri di tutti i gruppi di protezione.

    Rimuovere tutti i dati protetti e tutti i gruppi di protezione dati.
4. Dopo aver eliminato tutti i membri dal gruppo protezione dati hello, passare toohello portale di Azure. Aprire il dashboard dell'insieme di credenziali hello e assicurarsi che vi siano non **elementi Backup**, **server di gestione di Backup**, o **gli elementi replicati**. Sulla barra degli strumenti dell'insieme di credenziali hello, fare clic su **eliminare**.

    ![Elimina dati di backup](./media/backup-azure-delete-vault/delete-vault.png)

    Se sono presenti credenziali toohello di Backup gestione i server registrati, è possibile eliminare l'insieme di credenziali hello anche se non sono presenti dati nell'insieme di credenziali hello. Se i server di gestione Backup hello associati all'insieme di credenziali hello è stata eliminata, ma sono presenti i server elencati in hello **Essentials** riquadro, vedere [trova hello Backup Gestione server toohello registrato dell'insieme di credenziali](backup-azure-delete-vault.md#find-the-backup-management-servers-registered-to-the-vault) .
5. Fare clic su tooverify che si desidera l'insieme di credenziali hello toodelete **Sì**.

    insieme di credenziali Hello viene eliminato e portale hello restituisce toohello **New** menu del servizio.

## <a name="delete-a-vault-used-tooprotect-a-production-server"></a>Eliminare tooprotect un insieme di credenziali utilizzato un server di produzione
Prima di poter eliminare tooprotect un insieme di credenziali utilizzato un server di produzione, è necessario eliminare o annullare la registrazione hello server dall'insieme di credenziali hello.

server di produzione hello toodelete associato all'insieme di credenziali hello:

1. Nel portale di Azure hello, aprire il dashboard dell'insieme di credenziali hello e fare clic su **impostazioni** > **Backup infrastruttura** > **server di produzione**.

    ![aprire il pannello Server di produzione](./media/backup-azure-delete-vault/delete-production-server.png)

    Hello **server di produzione** pannello apre ed elenca tutti i server di produzione nell'insieme di credenziali hello.

    ![elenco di server di produzione](./media/backup-azure-delete-vault/list-of-production-servers.png)
2. In hello **server di produzione** pannello destro del mouse sul server hello e fare clic su **eliminare**.

    ![eliminare il server di produzione ](./media/backup-azure-delete-vault/delete-server-on-production-server-blade.png)

    Hello **eliminare** apre blade.

    ![eliminare il server di produzione ](./media/backup-azure-delete-vault/delete-blade.png)
3. In hello **eliminare** pannello, confermare il nome di server hello e fare clic su **eliminare**. Correttamente è necessario assegnare un nome server hello, hello tooactivate **eliminare** pulsante.

    Una volta che l'insieme di credenziali hello viene eliminato, viene visualizzato un messaggio che informa dell'insieme di credenziali di hello è stato eliminato. Dopo l'eliminazione di tutti i server nell'insieme di credenziali hello, scorrere il riquadro Essentials toohello indietro nel dashboard dell'insieme di credenziali hello.
4. Nel dashboard dell'insieme di credenziali hello, assicurarsi che vi siano non **elementi Backup**, **server di gestione di Backup**, o **gli elementi replicati**. Sulla barra degli strumenti dell'insieme di credenziali hello, fare clic su **eliminare**.
5. Fare clic su tooverify che si desidera l'insieme di credenziali hello toodelete **Sì**.

    insieme di credenziali Hello viene eliminato e portale hello restituisce toohello **New** menu del servizio.

## <a name="delete-a-backup-vault-in-classic-portal"></a>Eliminare un insieme di credenziali di backup nel portale classico
Hello istruzioni che seguono sono per l'eliminazione di un insieme di credenziali di Backup nel portale classico hello. Prima di poter eliminare l'insieme di credenziali Backup hello, è necessario eliminare i punti di ripristino hello, o eseguito il backup degli elementi e rimuovere server hello registrato. Hello Server registrati sono hello Windows Server, workstation o macchine virtuali che sono stati registrati toohello insieme di credenziali.

1. Aprire hello [portale classico](https://manage.windowsazure.com).

2. Elenco di hello di insiemi di credenziali di backup, selezionare l'insieme di credenziali di hello desiderato toodelete.

    ![Elimina dati di backup](./media/backup-azure-delete-vault/classic-portal-delete-vault-open-vault.png)

    Apre il dashboard dell'insieme di credenziali di Hello. Esaminare il numero di hello delle macchine virtuali Windows Server e/o Azure associato all'insieme di credenziali hello. Inoltre, esaminare hello spazio di archiviazione totale utilizzato in Azure. Arrestare tutti i processi di backup ed eliminare tutti i dati prima di eliminare l'insieme di credenziali hello.

3. Fare clic su hello **elementi protetti** scheda e quindi fare clic su **Arresta protezione dati**

    ![Elimina dati di backup](./media/backup-azure-delete-vault/classic-portal-delete-vault-stop-protect.png)

    Hello **arrestare la protezione di 'l'insieme di credenziali'** viene visualizzata la finestra.
4. In hello **arrestare la protezione di 'l'insieme di credenziali'** finestra di dialogo, controllo **Elimina dati di backup associati** e fare clic su ![segno di spunta](./media/backup-azure-delete-vault/checkmark.png). <br/>
    È facoltativamente possibile scegliere un motivo per l'arresto della protezione e aggiungere un commento.

    ![Elimina dati di backup](./media/backup-azure-delete-vault/classic-portal-delete-vault-verify-stop-protect.png)

    Dopo l'eliminazione di elementi di hello nell'insieme di credenziali hello, insieme di credenziali hello sarà vuoto.

    ![Elimina dati di backup](./media/backup-azure-delete-vault/classic-portal-delete-vault-post-delete-data.png)
5. Nell'elenco di hello delle schede, fare clic su **elementi registrati**. Hello **tipo** dal menu a discesa, consente di digitare toochoose hello dell'insieme di credenziali toohello server registrato. tipo di Hello può essere Windows Server o macchina virtuale di Azure. Nell'esempio seguente di hello, selezionare l'insieme di credenziali registrati toohello hello macchina virtuale e fare clic su **Unregister**.

    ![Elimina dati di backup](./media/backup-azure-delete-vault/classic-portal-unregister.png)

  Se si desidera registrazione hello toodelete per Windows Server, da hello **tipo** menu a discesa, seleziona **Windows Server**, fare clic su ![segno di spunta](./media/backup-azure-delete-vault/checkmark.png) schermata Ciao toorefresh, e quindi fare clic su **eliminare**. <br/>

  ![selezionare Windows Server](./media/backup-azure-delete-vault/select-windows-server.png)

6. Nell'elenco di hello delle schede, fare clic su **Dashboard** tooopen che scheda. Verificare che non sono presenti server registrati o macchine virtuali di Azure protette nel cloud hello. Verificare anche che la risorsa di archiviazione non includa dati. Fare clic su **eliminare** insieme di credenziali toodelete hello.

    ![Elimina dati di backup](./media/backup-azure-delete-vault/classic-portal-list-of-tabs-dashboard.png)

    verrà visualizzata la schermata di conferma di Hello Backup Elimina insieme di credenziali. Selezionare un'opzione perché si vuole eliminare l'insieme di credenziali hello e fare clic su ![segno di spunta](./media/backup-azure-delete-vault/checkmark.png). <br/>

    ![Elimina dati di backup](./media/backup-azure-delete-vault/classic-portal-delete-vault-confirmation-1.png)

    insieme di credenziali Hello viene eliminato, e si restituisce toohello dashboard del portale classico.

### <a name="find-hello-backup-management-servers-registered-toohello-vault"></a>Trovare l'insieme di credenziali di hello Gestione Backup server registrati toohello
Se si dispone di più server registrati tooa archivio, può essere difficile tooremember li. Server hello toosee registrato insieme di credenziali toohello ed eliminarli:

1. Dashboard dell'insieme di credenziali hello aperto.
2. In hello **Essentials** riquadro, fare clic su **impostazioni** tooopen tale pannello.

    ![aprire il pannello Impostazioni](./media/backup-azure-delete-vault/backup-vault-click-settings.png)
3. In hello **pannello impostazioni**, fare clic su **infrastruttura Backup**.
4. In hello **Backup infrastruttura** pannello, fare clic su **il server di gestione di Backup**. verrà visualizzata la finestra di blade di Hello Server di gestione di Backup.

    ![elenco di server di gestione di backup](./media/backup-azure-delete-vault/list-of-backup-management-servers.png)
5. toodelete un server dall'elenco di hello, fare doppio clic su nome hello del server di hello e quindi fare clic su **eliminare**.
    Hello **eliminare** apre blade.
6. In hello **eliminare** pannello, specificare il nome di hello del server di hello. Se è un nome lungo, è possibile copiare e incollare, dall'elenco di hello del server di gestione di Backup. Fare quindi clic su **Elimina**.  
