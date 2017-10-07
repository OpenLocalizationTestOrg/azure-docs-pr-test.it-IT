---
title: aaaBack le credenziali di backup tooa distribuito classica macchine virtuali di Azure | Documenti Microsoft
description: Individuare, registrare ed eseguire il backup delle macchine virtuali usando queste procedure per il backup di macchine virtuali di Azure.
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: backup della macchina virtuale; eseguire il backup della macchina virtuale; backup e ripristino di emergenza; backup di vm
ms.assetid: c0ab5469-65fd-4af5-ae9b-f5d183f82ce8
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: 048e32d9b2bd5bdd7a125225a71a6d805bb4fbd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-virtual-machines-classic-portal"></a>Eseguire il backup di macchine virtuali di Azure (portale classico)
> [!div class="op_single_selector"]
> * [Eseguire il backup dell'insieme di credenziali di macchine virtuali tooRecovery servizi](backup-azure-arm-vms.md)
> * [Eseguire il backup dell'insieme di credenziali tooBackup macchine virtuali](backup-azure-vms.md)
>
>

In questo articolo vengono descritte le procedure hello per il backup di un insieme di credenziali Backup tooa distribuito classica macchina virtuale di Azure (VM). Esistono alcune attività, che è necessario tootake care di poter eseguire il backup di una macchina virtuale di Azure. Se non è già in questo caso, tutte le hello [prerequisiti](backup-azure-vms-prepare.md) tooprepare l'ambiente per il backup delle macchine virtuali.

Per ulteriori informazioni, vedere gli articoli di hello in [pianificazione dell'infrastruttura di backup di VM in Azure](backup-azure-vms-introduction.md) e [macchine virtuali di Azure](https://azure.microsoft.com/documentation/services/virtual-machines/).

> [!NOTE]
> Azure offre due modelli di distribuzione per creare e usare le risorse: [Resource Manager e distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md). Un insieme di credenziali per il backup consente di proteggere solo macchine virtuali distribuite con il modello di distribuzione classica. Non è possibile proteggere le macchine virtuali distribuite con il modello di distribuzione Resource Manager usando un insieme di credenziali per il backup. Vedere [eseguire il backup dell'insieme di credenziali di macchine virtuali tooRecovery servizi](backup-azure-arm-vms.md) per informazioni dettagliate sull'utilizzo dei servizi di ripristino di insiemi di credenziali.
>
>

L'esecuzione del backup di macchine virtuali di Azure prevede tre passaggi principali:

![Tooback tre passaggi di una macchina virtuale IaaS di Azure](./media/backup-azure-vms/3-steps-for-backup.png)

> [!NOTE]
> Il backup di macchine virtuali è un processo locale. È possibile eseguire il backup di macchine virtuali in una regione tooa insieme di credenziali backup in un'altra area. È quindi necessario creare un insieme di credenziali per il backup in ogni area di Azure dove sono presenti VM di cui sarà seguito il backup.
>
> [!IMPORTANT]
> A partire da marzo 2017, è possibile utilizzare non è più insiemi di credenziali Backup hello toocreate portale classico.
> È ora possibile aggiornare i servizi archivi di Backup gli insiemi di credenziali tooRecovery. Per informazioni dettagliate, vedere l'articolo hello [aggiornare un tooa insieme di credenziali di Backup dell'insieme di credenziali di servizi di ripristino](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft incoraggia gli utenti tooupgrade insiemi di credenziali di servizi tooRecovery insiemi di credenziali di Backup.<br/> Dopo 15 ottobre 2017, è possibile utilizzare gli insiemi di credenziali di PowerShell toocreate Backup. **Entro il 1° novembre 2017**:
>- Tutti gli archivi di Backup rimanenti verrà automaticamente aggiornato tooRecovery servizi insiemi di credenziali.
>- Si sarà in grado di tooaccess ai dati di backup nel portale classico hello. Utilizzare invece hello Azure tooaccess portale i dati di backup in insiemi di servizi di ripristino.
>

## <a name="step-1---discover-azure-virtual-machines"></a>Passaggio 1: Individuare le macchine virtuali di Azure
tooensure ogni nuova sottoscrizione toohello aggiunta di macchine virtuali (VM) vengono identificati prima di registrare, eseguire il processo di individuazione di hello. le query di processo di Hello Azure per elenco hello delle macchine virtuali nella sottoscrizione di hello, insieme a informazioni aggiuntive come nome del servizio cloud hello e area hello.

1. Accedi toohello [portale classico](http://manage.windowsazure.com/)
2. Nell'elenco di hello dei servizi Azure, fare clic su **servizi di ripristino** elenco hello tooopen degli insiemi di credenziali di Backup e ripristino del sito.
    ![Elenco dell'insieme di credenziali](./media/backup-azure-vms/choose-vault-list.png)
3. Nell'elenco di hello degli insiemi di credenziali di Backup, selezionare hello insieme di credenziali tooback una macchina virtuale.

    Se si tratta di un nuovo portale hello insieme di credenziali apre toohello **avvio rapido** pagina.

    ![Menu Elementi registrati aperto](./media/backup-azure-vms/vault-quick-start.png)

    Se in precedenza è stato configurato l'insieme di credenziali hello, viene visualizzato il portale di hello menu toohello utilizzato più di recente.
4. Dal menu di insieme di credenziali hello (in alto hello hello pagina), fare clic su **elementi registrati**.

    ![Menu Elementi registrati aperto](./media/backup-azure-vms/vault-menu.png)
5. Da hello **tipo** dal menu **macchina virtuale di Azure**.

    ![Selezionare il carico di lavoro](./media/backup-azure-vms/discovery-select-workload.png)
6. Fare clic su **DISCOVER** nella parte inferiore di hello della pagina hello.
    ![Pulsante Individua](./media/backup-azure-vms/discover-button-only.png)

    il processo di individuazione Hello potrebbe richiedere alcuni minuti hello le macchine virtuali sono in elencati in formato tabulare. Vi è una notifica nella parte inferiore di hello della schermata Ciao che informa che il processo di hello sia in esecuzione.

    ![Individuare le VM](./media/backup-azure-vms/discovering-vms.png)

    notifica Hello cambia quando il processo di hello. Se il processo di individuazione hello non ha trovato hello le macchine virtuali, verificare che le macchine virtuali hello esistono. Se le macchine virtuali hello esistono, verificare hello macchine virtuali sono in hello stessa area dell'insieme di credenziali di backup hello. Se le macchine virtuali hello esistano e siano in hello stessa area, verificare che le macchine virtuali hello non sono già registrati tooa credenziali di backup. Se una macchina virtuale è tooa assegnate credenziali di backup non è disponibile toobe assegnato tooother insiemi di credenziali backup.

    ![Individuazione completata](./media/backup-azure-vms/discovery-complete.png)

    Dopo aver individuato i nuovi elementi di hello, andare tooStep 2 e registrare le macchine virtuali.

## <a name="step-2---register-azure-virtual-machines"></a>Passaggio 2: Registrare le macchine virtuali di Azure
Si registra un tooassociate macchina virtuale di Azure con hello servizio Azure Backup. Questa attività viene in genere eseguita una sola volta.

1. Passare l'insieme di credenziali backup toohello in **servizi di ripristino** in hello portale di Azure e quindi fare clic su **elementi registrati**.
2. Selezionare **macchina virtuale di Azure** dal menu a discesa hello.

    ![Selezionare il carico di lavoro](./media/backup-azure-vms/discovery-select-workload.png)
3. Fare clic su **registrare** nella parte inferiore di hello della pagina hello.
    ![Pulsante Registra](./media/backup-azure-vms/register-button-only.png)
4. In hello **registrare elementi** menu di scelta rapida, hello selezionare le macchine virtuali che si desidera tooregister. Se sono presenti due o più macchine virtuali con hello stesso nome, utilizzare toodistinguish servizio cloud di hello tra di essi.

   > [!TIP]
   > È possibile registrare più macchine virtuali contemporaneamente.
   >
   >

    Viene creato un processo per ogni macchina virtuale selezionata.
5. Fare clic su **Visualizza processo** in hello notifica toogo toohello **processi** pagina.

    ![Registrare il processo](./media/backup-azure-vms/register-create-job.png)

    macchina virtuale Hello viene visualizzato anche nell'elenco di hello degli elementi registrati, insieme allo stato di hello dell'operazione di registrazione hello.

    ![Registering status 1](./media/backup-azure-vms/register-status01.png)

    Al termine dell'operazione di hello, lo stato di hello cambia hello tooreflect *registrato* stato.

    ![Registration status 2](./media/backup-azure-vms/register-status02.png)

## <a name="step-3---protect-azure-virtual-machines"></a>Passaggio 3: Proteggere le macchine virtuali di Azure
Ora è possibile impostare un criterio di backup e memorizzazione per la macchina virtuale hello. È possibile proteggere più macchine virtuali usando una singola operazione.

Azure insiemi di credenziali di Backup creati dopo maggio 2015 forniti con un criterio predefinito creato nell'insieme di credenziali hello. Questi criteri predefiniti prevedono un periodo di conservazione predefinito di 30 giorni e una pianificazione per il backup una volta al giorno.

1. Passare l'insieme di credenziali backup toohello in **servizi di ripristino** in hello portale di Azure e quindi fare clic su **elementi registrati**.
2. Selezionare **macchina virtuale di Azure** dal menu a discesa hello.

    ![Select workload in portal](./media/backup-azure-vms/select-workload.png)
3. Fare clic su **PROTEGGI** nella parte inferiore di hello della pagina hello.

    Hello **guidata proteggere elementi** viene visualizzato. procedura guidata di Hello Elenca solo le macchine virtuali che vengono registrate e non protetti. Selezionare le macchine virtuali hello che si desidera tooprotect.

    Se sono presenti due o più macchine virtuali con hello stesso nome, utilizzare hello cloud servizio toodistinguish tra le macchine virtuali hello.

   > [!TIP]
   > È possibile proteggere più macchine virtuali contemporaneamente.
   >
   >

    ![Configurare la protezione su vasta scala](./media/backup-azure-vms/protect-at-scale.png)

4. Scegliere un **pianificazione del backup** tooback backup di macchine virtuali hello selezionato. È possibile scegliere da un set di criteri esistenti o definirne di nuovi.

    Ai singoli criteri di backup possono essere associate più macchine virtuali. Tuttavia, hello macchina virtuale può solo essere associato a un criterio in qualsiasi punto nel tempo.

    ![Proteggere con nuovi criteri](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > Un criterio di backup include uno schema di memorizzazione per i backup pianificato hello. Se si seleziona un criterio di backup, è possibile modificare le opzioni di memorizzazione hello nel passaggio successivo hello.
   >
   >

5. Scegliere un **mantenimento** tooassociate con backup hello.

    ![Proteggere con criteri di conservazione flessibili](./media/backup-azure-vms/policy-retention.png)

    Criteri di conservazione specificano durata hello per archiviare un backup. È possibile specificare i criteri di conservazione diversi in base a quando viene eseguito il backup di hello. Ad esempio, un punto di backup eseguito quotidianamente, che funge da punto di ripristino operativo, può essere conservato per 90 giorni. In confronto, un punto di backup eseguito alla fine hello ogni trimestre (per motivi di controllo) potrebbe essere necessario toobe mantenuti per numero di mesi o anni.

    ![Virtual machine is backed up with recovery point](./media/backup-azure-vms/long-term-retention.png)

    In questa immagine di esempio:

   * **Criteri di conservazione giornaliera**: i backup eseguiti ogni giorno vengono archiviati per 30 giorni.
   * **Criteri di conservazione settimanale**: i backup eseguiti ogni domenica vengono conservati per 104 settimane.
   * **Criteri di conservazione mensile**: i backup eseguiti su hello ultima domenica di ogni mese vengono conservati per 120 mesi.
   * **Criteri di conservazione annuale**: i backup eseguiti su hello prima domenica di ogni mese di gennaio vengono mantenuti per 99 anni.

     Un processo viene creato criteri di protezione tooconfigure hello e associare criteri di toothat hello macchine virtuali per ogni macchina virtuale selezionata.
6. elenco di hello tooview di **configurazione della protezione** processi, nel menu hello gli insiemi di credenziali, fare clic su **processi** e selezionare **configurazione della protezione** da hello **operazione ** filtro.

    ![Configure protection job](./media/backup-azure-vms/protect-configureprotection.png)

## <a name="initial-backup"></a>Backup iniziale
Una volta macchina virtuale hello è protetto con un criterio, viene visualizzata in hello **elementi protetti** scheda con stato hello *Protected - (in sospeso il backup iniziale)*. Per impostazione predefinita, backup pianificato prima hello è hello *backup iniziale*.

backup iniziale hello di tootrigger immediatamente dopo la configurazione di protezione:

1. Nella parte inferiore di hello di hello **elementi protetti** pagina, fare clic su **Esegui Backup**.

    Hello servizio Backup di Azure crea un processo di backup per l'operazione di backup iniziale hello.
2. Fare clic su hello **processi** elenco della scheda tooview hello dei processi.

    ![Backup in progress](./media/backup-azure-vms/protect-inprogress.png)

> [!NOTE]
> Durante l'operazione di backup hello, hello servizio Backup di Azure esegue un'estensione di backup toohello comando in ogni macchina virtuale di tooflush tutti i processi di scrittura e uno snapshot coerente.
>
>

Al termine di backup iniziale hello, lo stato di hello della macchina virtuale hello in hello **elementi protetti** scheda *Protected*.

![Virtual machine is backed up with recovery point](./media/backup-azure-vms/protect-backedupvm.png)

## <a name="viewing-backup-status-and-details"></a>Visualizzazione dello stato di backup e dei relativi dettagli
Una volta protetto, aumenta anche il numero di macchine virtuali hello hello **Dashboard** pagina riepilogo. Hello **Dashboard** pagina mostra anche il numero di hello di processi da hello ultime 24 ore che sono stati *ha esito positivo*, hanno *Impossibile*e sono *in corso*. In hello **processi** pagina, utilizzare hello **stato**, **operazione**, o **da** e **a** toofilter menu processi di Hello.

![Status of backup in Dashboard page](./media/backup-azure-vms/dashboard-protectedvms.png)

I valori nel dashboard di hello vengono aggiornati una volta ogni 24 ore.

## <a name="troubleshooting-errors"></a>Risoluzione dei problemi
Se si verificano problemi durante il backup la macchina virtuale, esaminare hello [articolo sulla risoluzione dei problemi di VM](backup-azure-vms-troubleshoot.md) per assistenza.

## <a name="next-steps"></a>Passaggi successivi
* [Gestire e monitorare il backup delle macchine virtuali di Azure](backup-azure-manage-vms.md)
* [Ripristino di macchine virtuali](backup-azure-restore-vms.md)
