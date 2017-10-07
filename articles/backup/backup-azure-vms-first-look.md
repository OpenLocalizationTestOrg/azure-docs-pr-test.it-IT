---
title: 'Primo approccio: Eseguire il backup di VM di Azure con un insieme di credenziali di backup | Microsoft Docs'
description: Utilizzare hello tooback portale classico di insieme di credenziali Backup tooa macchine virtuali di Azure. In questa esercitazione illustra tutte le fasi, tra cui la creazione di credenziali di Backup hello, la registrazione delle macchine virtuali di hello, creazione di criteri di backup e in esecuzione il processo di backup iniziale di hello.
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 722820dc-b65f-425c-a9e5-c1946e896a87
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/2/2017
ms.author: markgal;
ms.openlocfilehash: 77700e69eab9faccbc7ef923e1eb4e1f97be75d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="first-look-backing-up-azure-virtual-machines"></a>Primo approccio: Backup di macchine virtuali di Azure
> [!div class="op_single_selector"]
> * [Proteggere le VM con un insieme di credenziali dei servizi di ripristino](backup-azure-vms-first-look-arm.md)
> * [Proteggere le VM di Azure con un insieme di credenziali per il backup](backup-azure-vms-first-look.md)
>
>

In questa esercitazione illustra i passaggi di hello per il backup di un archivio di backup tooa macchina virtuale di Azure (VM) in Azure. Questo articolo descrive il modello classico di hello o modello di distribuzione di Service Manager, per il backup di macchine virtuali. Hello passaggi seguenti si applicano solo tooBackup gli insiemi di credenziali creati nel portale classico hello. Si consiglia di utilizzare il modello di gestione risorse hello per le nuove distribuzioni.

Se si desidera eseguire il backup di un archivio di servizi di ripristino tooa VM appartenente tooa gruppo di risorse, vedere [innanzitutto: proteggere macchine virtuali con un insieme di credenziali di servizi di ripristino](backup-azure-vms-first-look-arm.md).

toosuccessfully completare seguente hello esercitazione devono essere presente questi prerequisiti:

* È stata creata una VM nella sottoscrizione di Azure.
* Hello macchina virtuale dispone di connettività tooAzure indirizzi IP. Per altre informazioni, vedere [Connettività di rete](backup-azure-vms-prepare.md#network-connectivity).


> [!NOTE]
> Azure offre due modelli di distribuzione per creare e usare le risorse: [Resource Manager e distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md). In questa esercitazione viene utilizzato con le macchine virtuali create nel portale classico hello.
>
>

## <a name="create-a-backup-vault"></a>Creare un insieme di credenziali per il backup
Un insieme di credenziali di backup è un'entità contenente tutti i backup di hello e i punti di ripristino che sono stati creati nel corso del tempo. insieme di credenziali backup Hello contiene anche i criteri di backup hello che vengono applicati toohello le macchine virtuali viene eseguito il backup.

> [!IMPORTANT]
> A partire da marzo 2017, è possibile utilizzare non è più insiemi di credenziali Backup hello toocreate portale classico.
> È possibile aggiornare i servizi archivi di Backup gli insiemi di credenziali tooRecovery. Per informazioni dettagliate, vedere l'articolo hello [aggiornare un tooa insieme di credenziali di Backup dell'insieme di credenziali di servizi di ripristino](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft incoraggia gli utenti tooupgrade insiemi di credenziali di servizi tooRecovery insiemi di credenziali di Backup.<br/> Dopo 15 ottobre 2017, è possibile utilizzare gli insiemi di credenziali di PowerShell toocreate Backup. **Entro il 1° novembre 2017**:
>- Tutti gli archivi di Backup rimanenti verrà automaticamente aggiornato tooRecovery servizi insiemi di credenziali.
>- Si sarà in grado di tooaccess ai dati di backup nel portale classico hello. Utilizzare invece hello Azure tooaccess portale i dati di backup in insiemi di servizi di ripristino.
>

## <a name="discover-and-register-azure-virtual-machines"></a>Individuare e registrare le macchine virtuali di Azure
Prima di registrare hello macchina virtuale con un insieme di credenziali, eseguire tooidentify processo di individuazione hello nuove macchine virtuali. Viene restituito un elenco di macchine virtuali nella sottoscrizione di hello, insieme a informazioni aggiuntive come nome del servizio cloud hello e area hello.

1. Accedi toohello [portale di Azure classico](http://manage.windowsazure.com/)
2. Nel portale di Azure classico hello, fare clic su **servizi di ripristino** elenco hello tooopen degli insiemi di credenziali di servizi di ripristino.
    ![Selezionare il carico di lavoro](./media/backup-azure-vms-first-look/recovery-services-icon.png)
3. Hello l'elenco degli insiemi di credenziali, selezionare hello insieme di credenziali tooback una macchina virtuale.

    Quando si seleziona l'insieme di credenziali, aprirla in hello **avvio rapido** pagina
4. Dal menu di hello insieme di credenziali, fare clic su **elementi registrati**.

    ![Selezionare il carico di lavoro](./media/backup-azure-vms-first-look/configure-registered-items.png)
5. Da hello **tipo** dal menu **macchina virtuale di Azure**.

    ![Selezionare il carico di lavoro](./media/backup-azure-vms/discovery-select-workload.png)
6. Fare clic su **DISCOVER** nella parte inferiore di hello della pagina hello.
    ![Pulsante Individua](./media/backup-azure-vms/discover-button-only.png)

    il processo di individuazione Hello potrebbe richiedere alcuni minuti hello le macchine virtuali sono in elencati in formato tabulare. Vi è una notifica nella parte inferiore di hello della schermata Ciao che informa che il processo di hello sia in esecuzione.

    ![Individuare le VM](./media/backup-azure-vms/discovering-vms.png)

    notifica Hello cambia quando il processo di hello.

    ![Individuazione completata](./media/backup-azure-vms-first-look/discovery-complete.png)
7. Fare clic su **registrare** nella parte inferiore di hello della pagina hello.
    ![Pulsante Registra](./media/backup-azure-vms-first-look/register-icon.png)
8. In hello **registrare elementi** menu di scelta rapida, hello selezionare le macchine virtuali che si desidera tooregister.

   > [!TIP]
   > È possibile registrare più macchine virtuali contemporaneamente.
   >
   >

    Viene creato un processo per ogni macchina virtuale selezionata.
9. Fare clic su **Visualizza processo** in hello notifica toogo toohello **processi** pagina.

    ![Registrare il processo](./media/backup-azure-vms/register-create-job.png)

    macchina virtuale Hello viene visualizzato anche nell'elenco di hello degli elementi registrati, insieme allo stato di hello dell'operazione di registrazione hello.

    ![Registering status 1](./media/backup-azure-vms/register-status01.png)

    Al termine dell'operazione di hello, lo stato di hello cambia hello tooreflect *registrato* stato.

    ![Registration status 2](./media/backup-azure-vms/register-status02.png)

## <a name="install-hello-vm-agent-on-hello-virtual-machine"></a>Installare hello agente della macchina virtuale nella macchina virtuale hello
Hello agente VM di Azure deve essere installato nella macchina virtuale di Azure per hello Backup estensione toowork hello. Se la macchina virtuale è stata creata da una raccolta di Azure hello, hello agente VM è già presente nella macchina virtuale; hello è possibile ignorare troppo[protegge le macchine virtuali](backup-azure-vms-first-look.md#create-the-backup-policy).

Se la macchina virtuale eseguita la migrazione da un data center locale, hello VM probabilmente non dispone di hello che agente VM installato. È necessario installare hello agente della macchina virtuale nella macchina virtuale hello hello tooprotect procedere macchina virtuale. Per i passaggi dettagliati per l'installazione di hello agente VM, vedere hello [sezione agente di macchine Virtuali dell'articolo di macchine virtuali Backup hello](backup-azure-vms-prepare.md#vm-agent).

## <a name="create-hello-backup-policy"></a>Creare criteri di backup hello
Prima attivare il processo di backup iniziale di hello, pianificare hello quando vengono eseguiti gli snapshot di backup. Hello pianificare gli snapshot di backup vengono eseguiti e hello di questi snapshot del periodo di tempo vengono mantenute, è criteri di backup hello. informazioni di memorizzazione Hello si basano sullo schema di rotazione dei backup nonno-padre-figlio.

1. Passare l'insieme di credenziali backup toohello in **servizi di ripristino** in hello portale di Azure classico, quindi fare clic su **elementi registrati**.
2. Selezionare **macchina virtuale di Azure** dal menu a discesa hello.

    ![Select workload in portal](./media/backup-azure-vms/select-workload.png)
3. Fare clic su **PROTEGGI** nella parte inferiore di hello della pagina hello.
    ![Fare clic su Protezione](./media/backup-azure-vms-first-look/protect-icon.png)

    Hello **guidata proteggere elementi** sono elencati *solo* macchine virtuali che vengono registrate e non protetti.

    ![Configurare la protezione su vasta scala](./media/backup-azure-vms/protect-at-scale.png)
4. Selezionare le macchine virtuali hello che si desidera tooprotect.

    Se sono presenti due o più macchine virtuali con hello stesso nome, utilizzare hello servizio Cloud toodistinguish tra le macchine virtuali hello.
5. In hello **configurare la protezione** menu selezionare un criterio esistente o creare un nuovo tooprotect criteri macchine virtuali hello identificato.

    Nuovi archivi di Backup dispone di un criterio predefinito associato all'insieme di credenziali hello. Questo criterio ha quotidianamente snapshot ogni sera e snapshot giornaliero hello vengono mantenuti per 30 giorni. Ai singoli criteri di backup possono essere associate più macchine virtuali. Tuttavia, hello macchina virtuale può essere solo associata a un criterio alla volta.

    ![Proteggere con nuovi criteri](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > Un criterio di backup include uno schema di memorizzazione per i backup pianificato hello. Se si seleziona un criterio di backup, le opzioni di memorizzazione hello toomodify Impossibile sarà nel passaggio successivo hello.
   >
   >
6. In **mantenimento** definire hello giornaliera, settimanale, mensile e annuo ambito per i punti di backup specifico hello.

    ![Virtual machine is backed up with recovery point](./media/backup-azure-vms/long-term-retention.png)

    Criteri di conservazione specificano durata hello per archiviare un backup. È possibile specificare i criteri di conservazione diversi in base a quando viene eseguito il backup di hello.
7. Fare clic su **processi** tooview hello elenco **configurazione della protezione** processi.

    ![Configure protection job](./media/backup-azure-vms/protect-configureprotection.png)

    Ora che è stato stabilito criteri hello, passare passaggio successivo toohello ed eseguire il backup iniziale hello.

## <a name="initial-backup"></a>Backup iniziale
Una volta che una macchina virtuale è stata protetta con un criterio, è possibile visualizzare tale relazione nella hello **elementi protetti** scheda. Fino a quando non hello iniziale backup viene eseguito, hello **lo stato di protezione** viene illustrato come **Protected - (in sospeso il backup iniziale)**. Per impostazione predefinita, backup pianificato prima hello è hello *backup iniziale*.

![Backup in sospeso](./media/backup-azure-vms-first-look/protection-pending-border.png)

toostart hello backup iniziale ora:

1. In hello **elementi protetti** pagina, fare clic su **Esegui Backup** nella parte inferiore di hello della pagina hello.
    ![Icona Esegui backup ora](./media/backup-azure-vms-first-look/backup-now-icon.png)

    Hello servizio Backup di Azure crea un processo di backup per l'operazione di backup iniziale hello.
2. Fare clic su hello **processi** elenco della scheda tooview hello dei processi.

    ![Backup in progress](./media/backup-azure-vms-first-look/protect-inprogress.png)

    Quando il backup iniziale è stato completato, lo stato di hello della macchina virtuale hello in hello **elementi protetti** scheda *Protected*.

    ![Virtual machine is backed up with recovery point](./media/backup-azure-vms/protect-backedupvm.png)

   > [!NOTE]
   > Il backup di macchine virtuali è un processo locale. È possibile eseguire il backup di macchine virtuali da una regione tooa insieme di credenziali backup in un'altra area. In tal caso, per ogni area di Azure con macchine virtuali che devono toobe eseguito il backup, è necessario creare almeno un insieme di credenziali di backup in tale area.
   >
   >

## <a name="next-steps"></a>Passaggi successivi
Ora che è stato eseguito il backup di una macchina virtuale, sono disponibili diversi passaggi successivi interessanti. passaggio più logica Hello è toofamiliarize manualmente con il ripristino di dati tooa macchina virtuale. Tuttavia, vi sono attività di gestione che consentono di comprendere come tookeep dati sicuri e ridurre al minimo i costi.

* [Gestire e monitorare il backup delle macchine virtuali di Azure](backup-azure-manage-vms.md)
* [Ripristino di macchine virtuali](backup-azure-restore-vms.md)
* [Guida alla risoluzione dei problemi](backup-azure-vms-troubleshoot.md)

## <a name="questions"></a>Domande?
Se si hanno domande o se è presente una funzionalità che si desidera toosee incluso, [inviare commenti e suggerimenti](http://aka.ms/azurebackup_feedback).
