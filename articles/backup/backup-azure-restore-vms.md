---
title: aaaRestore a macchine virtuali da un backup | Documenti Microsoft
description: Informazioni su come toorestore macchina virtuale di Azure da un ripristino punto
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
keywords: "ripristinare i backup. modalità toorestore; punto di ripristino."
ms.assetid: fed877b3-b496-49fb-99e4-653be7c23e3a
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: trinadhk; jimpark;
ms.openlocfilehash: 44c25f3248784accd1c2beaabb2c9a4dca3232d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="restore-virtual-machines-in-azure"></a>Ripristinare macchine virtuali in Azure
> [!div class="op_single_selector"]
> * [Ripristinare VM nel portale di Azure](backup-azure-arm-restore-vms.md)
> * [Ripristinare VM nel portale classico](backup-azure-restore-vms.md)
>
>

Ripristinare una macchina virtuale di tooa nuova macchina virtuale da backup di hello archiviati in un insieme di credenziali di Backup di Azure con hello seguendo i passaggi.

> [!IMPORTANT]
> È ora possibile aggiornare i servizi archivi di Backup gli insiemi di credenziali tooRecovery. Per informazioni dettagliate, vedere l'articolo hello [aggiornare un tooa insieme di credenziali di Backup dell'insieme di credenziali di servizi di ripristino](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft incoraggia gli utenti tooupgrade insiemi di credenziali di servizi tooRecovery insiemi di credenziali di Backup.<br/> **15 ottobre 2017**, non potrà più insiemi di credenziali Backup a toocreate toouse in grado di PowerShell. <br/> **A partire dal 1° novembre 2017**:
>- Gli insiemi di credenziali di Backup rimanenti verrà automaticamente aggiornato tooRecovery servizi insiemi di credenziali.
>- Si sarà in grado di tooaccess ai dati di backup nel portale classico hello. Utilizzare invece hello Azure tooaccess portale i dati di backup in insiemi di servizi di ripristino.
>

## <a name="restore-workflow"></a>Ripristinare un flusso di lavoro
### <a name="step-1-choose-an-item-toorestore"></a>Passaggio 1: Scegliere un elemento di toorestore
1. Passare toohello **elementi protetti** scheda e selezionare hello macchina virtuale da toorestore tooa nuova macchina virtuale.

    ![Elementi protetti](./media/backup-azure-restore-vms/protected-items.png)

    Hello **punto di ripristino** colonna hello **elementi protetti** pagina indicherà hello numero di punti di ripristino per una macchina virtuale. Hello **punto di ripristino più recente** colonna indica hello ora del backup più recente di hello da cui è possibile ripristinare una macchina virtuale.
2. Fare clic su **ripristinare** tooopen hello **ripristinare un elemento** procedura guidata.

    ![Ripristina elemento](./media/backup-azure-restore-vms/restore-item.png)

### <a name="step-2-pick-a-recovery-point"></a>Passaggio 2: Scegliere un punto di ripristino
1. In hello **selezionare un punto di ripristino** schermata, è possibile ripristinare dal punto di ripristino più recente di hello, o da un punto precedente nel tempo. Hello opzione predefinita selezionata quando si apre la procedura guidata è *punto di ripristino più recente*.

    ![selezione di un punto di ripristino](./media/backup-azure-restore-vms/select-recovery-point.png)
2. toopick un precedente punto nel tempo, scegliere hello **selezione data** opzione nell'elenco a discesa hello e selezionare una data nel controllo di calendario hello facendo clic su hello **sull'icona calendario**. Nel controllo hello, tutte le date che dispongono di punti di ripristino vengono riempite con una sfumatura di colore grigio chiara e siano dall'utente hello.

    ![Selezionare una data](./media/backup-azure-restore-vms/select-date.png)

    Dopo aver selezionato una data nel controllo di calendario hello, ripristino hello punti disponibili in che data verrà visualizzata nella tabella di punti di ripristino seguente. Hello **ora** colonna indica i tempi di hello in cui hello dello snapshot. Hello **tipo** colonna Visualizza hello [coerenza](https://azure.microsoft.com/documentation/articles/backup-azure-vms/#consistency-of-recovery-points) hello punto di ripristino. intestazione della tabella Hello Mostra il numero di hello di punti di ripristino disponibili in tale giorno tra parentesi.

    ![Punti di ripristino](./media/backup-azure-restore-vms/recovery-points.png)
3. Selezionare il punto di ripristino hello hello **punti di ripristino** tabella e fare clic su hello freccia toogo toohello avanti nella schermata successiva.

### <a name="step-3-specify-a-destination-location"></a>Passaggio 3: Specificare un percorso di destinazione
1. In hello **scegliere Ripristina istanza** schermata specificare i dettagli di in cui toorestore hello macchina virtuale.

   * Specificare il nome di macchina virtuale hello: In un determinato servizio cloud, il nome di macchina virtuale hello deve essere univoco. Non è supportata la sovrascrittura di macchine virtuali esistenti.
   * Selezionare un servizio cloud per hello VM: questo campo è obbligatorio per la creazione di una macchina virtuale. È possibile scegliere di utilizzare tooeither un servizio cloud esistente o creare un nuovo servizio cloud.

        Qualunque sia il nome del servizio cloud scelto, deve essere universalmente univoco. Nome del servizio cloud hello ottiene in genere, associata a un URL pubblico in formato hello [cloudservice]. cloudapp.net. Azure non consente un nuovo servizio cloud toocreate se è già stato utilizzato il nome di hello. Se si sceglie toocreate un nuovo servizio cloud, sarà specificato hello stesso nome come macchina virtuale hello: in quale case hello VM nome selezionato deve essere sufficientemente univoci toobe applicato toohello associata cloud service.

        Servizi cloud, viene visualizzato solo e reti virtuali che non sono associate a eventuali gruppi di affinità in hello ripristino dettagli dell'istanza. [Altre informazioni](../virtual-network/virtual-networks-migrate-to-regional-vnet.md).
2. Selezionare un account di archiviazione per VM hello: questo campo è obbligatorio per la creazione di hello macchina virtuale. È possibile selezionare gli account di archiviazione esistenti in hello stessa area dell'insieme di credenziali di Backup di Azure hello. Gli account di archiviazione con ridondanza della zona o con archiviazione di tipo Premium non sono supportati.

    Se non sono disponibili account di archiviazione con configurazione supportata, creare un account di archiviazione dell'operazione di ripristino precedenti toostarting configurazione supportata.

    ![Selezionare una rete virtuale](./media/backup-azure-restore-vms/restore-sa.png)
3. Selezionare una rete virtuale: rete virtuale hello (VNET) per macchina virtuale hello deve essere selezionato in fase di creazione di hello hello macchina virtuale. Hello ripristinare Mostra interfaccia utente tutte le reti virtuali hello all'interno di questa sottoscrizione che può essere utilizzato. Non è obbligatorio tooselect una rete virtuale per hello VM di ripristino: macchina virtuale di tooconnect in grado di ripristinare toohello sarà su hello internet anche se hello rete virtuale non è stato applicato.

    Se cloud hello servizio selezionato è associata a una rete virtuale, non è possibile modificare la rete virtuale hello.

    ![Selezionare una rete virtuale](./media/backup-azure-restore-vms/restore-cs-vnet.png)
4. Selezionare una subnet: nel caso in cui hello rete virtuale dispone di subnet, per impostazione predefinita è verrà selezionato prima subnet hello. Scegliere le opzioni di elenco a discesa hello subnet hello di propria scelta. Per informazioni dettagliate di subnet, vedere estensione tooNetworks hello [home page del portale](https://manage.windowsazure.com/), andare troppo**reti virtuali** e rete virtuale selezionare hello e drill-down dei dettagli di configurazione toosee subnet.

    ![Selezionare una subnet](./media/backup-azure-restore-vms/select-subnet.png)
5. Fare clic su hello **Invia** icona in hello guidata toosubmit hello dettagli e creare un processo di ripristino.

## <a name="track-hello-restore-operation"></a>Traccia l'operazione di ripristino hello
Dopo aver input tutte le informazioni nella procedura guidata Ripristino configurazione di hello hello e inviata Azure Backup tenterà toocreate un'operazione di ripristino hello tootrack processo.

![Creazione di un processo di ripristino](./media/backup-azure-restore-vms/create-restore-job.png)

Creazione del processo hello ha esito positivo, si noterà una notifica di tipo avviso popup indicante che il processo di hello viene creato. È possibile ottenere ulteriori dettagli, fare clic su hello **Visualizza processo** pulsante che ti condurrà troppo**processi** scheda.

![Processo di ripristino creato](./media/backup-azure-restore-vms/restore-job-created.png)

Al termine dell'operazione di ripristino hello, verrà contrassegnato come completato nel **processi** scheda.

![Processo di ripristino completato](./media/backup-azure-restore-vms/restore-job-complete.png)

Dopo il ripristino hello macchina virtuale potrebbe essere necessario estensioni hello toore installazione esistente in hello macchina virtuale originale e [modificare gli endpoint hello](../virtual-machines/windows/classic/setup-endpoints.md) per la macchina virtuale hello in hello portale di Azure.

## <a name="post-restore-steps"></a>Operazioni successive al ripristino
Se si usa una distribuzione Linux basata su cloud-init, ad esempio Ubuntu, per motivi di sicurezza, la password verrà bloccata dopo il ripristino. Per utilizzare estensione VMAccess su hello ripristinato VM troppo[hello di reimpostazione password](../virtual-machines/linux/classic/reset-access.md). È consigliabile utilizzare le chiavi SSH su tooavoid queste distribuzioni reimpostazione password post ripristino.

## <a name="backup-for-restored-vms"></a>Backup per le macchine virtuali ripristinate
Se è stato ripristinato servizio cloud VM toosame con stesso nome originariamente il backup VM hello, backup continuerà in hello ripristino post macchina virtuale. Se si è ripristinato VM tooa altro servizio cloud o specifica un nome diverso per la macchina virtuale ripristinata, questo verrà considerato come una nuova macchina virtuale e toosetup backup necessario per la macchina virtuale ripristinata.

## <a name="restoring-a-vm-during-azure-datacenter-disaster"></a>Ripristino di una macchina virtuale durante un'emergenza del data center di Azure
Backup di Azure consente di ripristino di backup associati data center di macchine virtuali toohello nel caso in cui le macchine virtuali eseguono esperienze di emergenza e sono configurati toobe insieme di credenziali di Backup con ridondanza geografica di hello primario data center. Durante tali scenari, è necessario un account di archiviazione che è presente nel centro dati associato tooselect e resto del processo di ripristino hello rimane stesso. Backup di Azure Usa il servizio di calcolo dalla macchina virtuale di area geografica associata toocreate hello ripristinato. Altre informazioni sulla [resilienza dei centri dati di Azure](../resiliency/resiliency-technical-guidance-recovery-loss-azure-region.md)

## <a name="restoring-domain-controller-vms"></a>Ripristino delle macchine virtuali del controller di dominio
L'esecuzione del backup delle macchine virtuali del controller di dominio (DC) è uno scenario supportato da Backup di Azure. Tuttavia, prestare attenzione durante il processo di ripristino hello. il processo di ripristino corrette Hello dipende dalla struttura di hello del dominio hello. Nel caso più semplice hello è un singolo controller di dominio in un singolo dominio. Più comunemente per i carichi di produzione, saranno presenti più controller di dominio per ogni dominio, ad esempio alcuni controller locali. Infine, è possibile avere una foresta con più domini.

Da un hello prospettiva di Active Directory macchina virtuale di Azure è come qualsiasi altra macchina virtuale in un hypervisor supportato moderna. Hello differenza principale con gli hypervisor locale è che non è disponibile in Azure console macchina virtuale. La console è obbligatoria per alcuni scenari, ad esempio per il ripristino tramite un backup di tipo di ripristino bare metal (BMR). Ripristino macchina virtuale dall'insieme di credenziali backup hello è tuttavia una sostituzione completa per il ripristino bare metal. È anche disponibile Active Directory Restore Mode (DSRM), in modo che tutti gli scenari di ripristino di Active Directory siano attuabili. Per altre informazioni di base, vedere [Backup and Restore considerations for virtualized Domain Controllers](https://technet.microsoft.com/en-us/library/virtual_active_directory_domain_controller_virtualization_hyperv(v=ws.10).aspx#backup_and_restore_considerations_for_virtualized_domain_controllers) (Considerazioni sul backup e sul ripristino per i controller di dominio virtualizzati) e [Planning for Active Directory Forest Recovery](https://technet.microsoft.com/en-us/library/planning-active-directory-forest-recovery(v=ws.10).aspx) (Pianificazione del ripristino delle foreste di Active Directory).

### <a name="single-dc-in-a-single-domain"></a>Controller di dominio unico in un singolo dominio
Hello VM possono essere ripristinati (ad esempio, tutte le altre VM) da hello Azure portal o utilizzo di PowerShell.

### <a name="multiple-dcs-in-a-single-domain"></a>Controller di dominio multipli in un singolo dominio
Quando altri controller di dominio di hello nello stesso dominio può essere raggiunto attraverso hello rete, hello controller di dominio può essere ripristinato come qualsiasi macchina virtuale. Se è hello ultimo restanti controller di dominio nel dominio hello o viene eseguito un ripristino in una rete isolata, deve essere seguita una procedura di ripristino della foresta.

### <a name="multiple-domains-in-one-forest"></a>Domini multipli in una foresta
Quando altri controller di dominio di hello nello stesso dominio può essere raggiunto attraverso hello rete, hello controller di dominio può essere ripristinato come qualsiasi macchina virtuale. Tuttavia, in tutti gli altri casi è consigliabile il ripristino della foresta.

<!--- WK: this following original supportability statement is incorrect, taking it out.
hello challenge arises because DSRM mode is not present in Azure. So toorestore such a VM, you cannot use hello Azure portal. hello only supported restore mechanism is disk-based restore using PowerShell.

> [!WARNING]
> For Domain Controller VMs in a multi-DC environment, do not use hello Azure portal for restore! Only PowerShell based restore is supported
>
>

Read more about hello [USN rollback problem](https://technet.microsoft.com/library/dd363553) and hello strategies suggested toofix it.
--->

## <a name="restoring-vms-with-special-network-configurations"></a>Ripristino delle macchine virtuali con configurazioni di rete speciali
Backup di Azure supporta il backup per le configurazioni di rete speciali seguenti delle macchine virtuali.

* Macchine virtuali nel servizio di bilanciamento del carico (interno ed esterno)
* Macchine virtuali con più indirizzi IP riservati
* Macchine virtuali con più NIC

Queste configurazioni rendono necessarie le considerazioni seguenti durante il ripristino.

> [!TIP]
> Utilizzare basate su PowerShell ripristino toorecreate hello rete speciale configurazione del flusso di ripristino di macchine virtuali post.
>
>

### <a name="restoring-from-hello-ui"></a>Ripristino da hello dell'interfaccia utente:
Durante il ripristino dall'interfaccia utente, **scegliere sempre un nuovo servizio cloud**. Si noti che poiché portale accetta solo obbligatorio parametri durante il flusso di ripristino, le macchine virtuali ripristinate con l'interfaccia utente perderà configurazione di rete speciali hello che dispongono. In altre parole, le macchine virtuali ripristinate saranno macchine virtuali normali senza la configurazione del bilanciamento del carico o di più NIC o di più indirizzi IP riservati.

### <a name="restoring-from-powershell"></a>Ripristino da PowerShell:
PowerShell ha hello possibilità toojust ripristinare i dischi di macchina virtuale hello da backup e non creare la macchina virtuale hello. Questa soluzione è utile durante il ripristino di macchine virtuali che richiedono le configurazioni di rete speciali descritte in precedenza.

In ordine toofully ricreare i post di macchina virtuale hello ripristino dei dischi, seguire questi passaggi:

1. Ripristinare i dischi hello dall'utilizzo di credenziali backup [il Backup di Azure PowerShell](backup-azure-vms-classic-automation.md#restore-an-azure-vm)
2. Creare la configurazione di macchina virtuale hello necessarie per bilanciamento del carico / più NIC/più riservato IP utilizzando hello i cmdlet di PowerShell e usarlo hello toocreate macchina virtuale della configurazione desiderata.

   * Creare una macchina virtuale nel servizio cloud con [bilanciamento del carico interno ](https://azure.microsoft.com/documentation/articles/load-balancer-internal-getstarted/)
   * Creare VM tooconnect troppo[bilanciamento del carico per Internet](https://azure.microsoft.com/en-us/documentation/articles/load-balancer-internet-getstarted/)
   * Creare una macchina virtuale con [più NIC](https://azure.microsoft.com/documentation/articles/virtual-networks-multiple-nics/)
   * Creare una macchina virtuale con [più indirizzi IP riservati](https://azure.microsoft.com/documentation/articles/virtual-networks-reserved-public-ip/)

## <a name="next-steps"></a>Passaggi successivi
* [Risoluzione dei problemi](backup-azure-vms-troubleshoot.md#restore)
* [Gestire le macchine virtuali](backup-azure-manage-vms.md)
