---
title: 'Backup di Azure: Ripristinare le macchine virtuali utilizzando hello portale di Azure | Documenti Microsoft'
description: Ripristinare una macchina virtuale di Azure da un punto di ripristino con il portale di Azure
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "ripristinare i backup. modalità toorestore; punto di ripristino."
ms.assetid: 372b87c6-3544-4dc5-bbc9-c742ca502159
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/15/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: f4f75d1da73c7760d2952afe80ff94918a08351c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-portal-toorestore-virtual-machines"></a>Utilizzare le macchine virtuali di Azure toorestore portale
> [!div class="op_single_selector"]
> * [Ripristinare VM nel portale classico](backup-azure-restore-vms.md)
> * [Ripristinare VM nel portale di Azure](backup-azure-arm-restore-vms.md)
>
>

È possibile proteggere i dati mediante la creazione di snapshot dei dati a intervalli definiti. Questi snapshot sono noti come punti di ripristino e vengono archiviati negli insiemi di credenziali dei servizi di ripristino. Se o quando è necessario toorepair o ricompilazione di una macchina virtuale, è possibile ripristinare hello macchina virtuale da uno qualsiasi dei punti di ripristino salvata hello. Quando si ripristina un punto di ripristino, è possibile creare una nuova macchina virtuale è una rappresentazione punto-in-time della macchina virtuale, il backup o ripristino di dischi e utilizzare modello hello in dotazione con il toocustomize hello ripristinato macchina virtuale o eseguire un ripristino di singoli file. Questo articolo viene illustrato come toorestore tooa una macchina virtuale nuova macchina virtuale o i dischi di ripristino di tutti i backup. Per il ripristino di singoli file, fare riferimento troppo[ripristinare i file di backup di macchina virtuale di Azure](backup-azure-restore-files-from-vm.md)

![3-ways-restore-from-vm-backup](./media/backup-azure-arm-restore-vms/azure-vm-backup-restore.png)

> [!NOTE]
> Azure offre due modelli di distribuzione per creare e usare le risorse: [Resource Manager e distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md). Questo articolo fornisce informazioni di hello e le procedure per il ripristino di macchine virtuali distribuite tramite il modello di gestione risorse hello.
>
>

Il ripristino di una macchina virtuale o di tutti i dischi dal backup della macchina virtuale prevede due passaggi:

1. Selezionare un punto di ripristino
2. Selezione hello ripristinare tipo - creare una nuova macchina virtuale o ripristinare i dischi e specificare i parametri obbligatori. 

## <a name="select-restore-point-for-restore"></a>Selezionare un punto di ripristino
1. Accedi toohello [portale di Azure](http://portal.azure.com/)
2. Hello Azure menu, scegliere **Sfoglia** e nell'elenco di hello dei servizi, digitare **servizi di ripristino**. elenco di Hello servizi regola toowhat digitato. Quando viene visualizzato **Insiemi di credenziali dei servizi di ripristino**, selezionare questa opzione.

    ![Aprire l'insieme di credenziali dei Servizi di ripristino](./media/backup-azure-arm-restore-vms/open-recovery-services-vault.png)

    viene visualizzato l'elenco di Hello degli insiemi di credenziali nella sottoscrizione hello.

    ![Elenco di insiemi di credenziali dei Servizi di ripristino](./media/backup-azure-arm-restore-vms/list-of-rs-vaults.png)
3. Dall'elenco di hello, insieme di credenziali selezionare hello associata a macchina virtuale che si desidera toorestore hello. Quando si sceglie l'insieme di credenziali hello, verrà visualizzato il relativo dashboard.

    ![Elenco di insiemi di credenziali dei Servizi di ripristino](./media/backup-azure-arm-restore-vms/select-vault-open-vault-blade.png)
4. Ora che si sta nel dashboard dell'insieme di credenziali hello. In hello **elementi Backup** riquadro, fare clic su **macchine virtuali di Azure** toodisplay hello macchine virtuali associato all'insieme di credenziali hello.

    ![Dashboard dell'insieme di credenziali](./media/backup-azure-arm-restore-vms/vault-dashboard.png)

    Hello **elementi Backup** blade si apre e visualizza l'elenco di hello macchine virtuali di Azure.

    ![Elenco di VM nell'insieme di credenziali](./media/backup-azure-arm-restore-vms/list-of-vms-in-vault.png)
5. Dall'elenco di hello, selezionare un dashboard hello tooopen della macchina virtuale. Apre il dashboard di VM Hello toohello area monitoraggio, che contiene sezione punti di ripristino hello.

    ![Elenco di VM nell'insieme di credenziali](./media/backup-azure-arm-restore-vms/vm-blade.png)
6. Scegliere dal menu del dashboard VM hello **ripristino**

    ![Elenco di VM nell'insieme di credenziali](./media/backup-azure-arm-restore-vms/vm-blade-menu-restore.png)

    verrà visualizzata la finestra di pannello Ripristina Hello.

    ![Pannello Ripristina](./media/backup-azure-arm-restore-vms/restore-blade.png)
7. In hello **ripristinare** pannello, fare clic su **punto di ripristino** tooopen hello **punto di ripristino selezionare** blade.

    ![Pannello Ripristina](./media/backup-azure-arm-restore-vms/recovery-point-selector.png)

    Per impostazione predefinita, finestra di dialogo hello Visualizza tutti i punti di ripristino dal hello ultimi 30 giorni. Hello utilizzare **filtro** visualizzati di punti di ripristino di intervallo di tempo tooalter hello di hello. Per impostazione predefinita, vengono visualizzati i punti di ripristino di ogni coerenza. Modificare **ripristinare tutti i punti** filtrare tooselect una verifica di coerenza specifico punti di ripristino. Per ulteriori informazioni su ogni tipo di punto di ripristino, vedere la spiegazione di hello di [la coerenza dei dati](backup-azure-vms-introduction.md#data-consistency).  

   * **Coerenza dei punti di ripristino** scegliere:
     * Punti di ripristino coerenti con l'arresto anomalo del sistema
     * Punti di ripristino coerenti con l'applicazione
     * Punti di ripristino coerenti con il file system
     * Tutti i punti di ripristino  
8. Scegliere un punto di ripristino e fare clic su **OK**.

    ![Scegliere il punto di ripristino ](./media/backup-azure-arm-restore-vms/select-recovery-point.png)

    Hello **ripristinare** pannello Mostra hello punto di ripristino è impostato.

    ![Punto di ripristino impostato](./media/backup-azure-arm-restore-vms/recovery-point-set.png)
9. In hello **ripristinare** pannello **ripristino configurazione** viene aperto automaticamente dopo aver impostato il punto di ripristino.

## <a name="choosing-a-vm-restore-configuration"></a>Scelta di una configurazione di ripristino per la macchina virtuale
Dopo aver selezionato il punto di ripristino di hello, scegliere una configurazione per il ripristino macchina virtuale. Le scelte effettuate per la configurazione di hello ripristino VM sono toouse: portale di Azure o PowerShell.

1. Se non si fosse già esiste, andare toohello **ripristinare** blade. Verificare un [punto di ripristino è stata selezionata](#select-restore-point-for-restore), fare clic su **ripristino configurazione** tooopen hello **configurazione recupero** blade.

    ![Configurazione guidata del ripristino configurata](./media/backup-azure-arm-restore-vms/recovery-configuration-wizard-recovery-type.png)
2. In hello **ripristino configurazione** pannello sono disponibili due opzioni:
   * Ripristinare la macchina virtuale completa
   * Ripristinare i dischi di cui è stato eseguito il backup

Il portale offre un'opzione di creazione rapida per la macchina virtuale ripristinata. Se si desidera una configurazione della macchina virtuale hello toocustomize o nomi di risorse hello create come parte di creare una nuova opzione di macchina virtuale, utilizzare PowerShell o toorestore portale backup dischi e utilizzare tooattach comandi PowerShell li toochoice del modello di configurazione o l'utilizzo VM che viene fornito con il ripristino hello toocustomize dischi ripristinati macchina virtuale. Vedere [il ripristino di una macchina virtuale con le configurazioni di rete speciali](#restoring-vms-with-special-network-configurations) per informazioni dettagliate su come toorestore macchina virtuale che dispone di più schede di rete o con bilanciamento del carico. Se la macchina virtuale di Windows utilizza [HUB licenze](../virtual-machines/windows/hybrid-use-benefit-licensing.md), è necessario toorestore dischi e utilizzare PowerShell o il modello come specificato di seguito toocreate hello VM e assicurarsi di specificare LicenseType come "Windows_Server" durante la creazione di VM tooavail HUB vantaggi nella macchina virtuale ripristinata. 
 
## <a name="create-a-new-vm-from-restore-point"></a>Creare una nuova macchina virtuale dal punto di ripristino
Se non si è già presente, [selezionare un punto di ripristino](#restoring-vms-with-special-network-configurations) prima di procedere toocreating una nuova macchina virtuale di ripristino scegliere. Dopo aver selezionato il punto di ripristino, in hello **ripristino configurazione** pannello, immettere o selezionare i valori per ognuno dei seguenti campi hello:

* **Restore Type** (Tipo ripristino): creare la macchina virtuale.
* **Nome della macchina virtuale** -specificare un nome per hello macchina virtuale. nome di Hello deve essere il gruppo di risorse univoco toohello (per una macchina virtuale distribuita di gestione delle risorse) o il servizio cloud (per una macchina virtuale classico). Se esiste già nella sottoscrizione hello non è possibile sostituire macchina virtuale hello.
* **Gruppo di risorse** : usare un gruppo di risorse esistente oppure crearne uno nuovo. Se si desidera ripristinare una macchina virtuale classica, è possibile usare questo nome di hello toospecify di campo di un nuovo servizio cloud. Se si sta creando un nuovo servizio cloud a gruppo/risorsa, nome hello deve essere globalmente univoco. In genere, nome del servizio cloud hello è associata a un URL pubblico - ad esempio: [cloudservice]. cloudapp.net. Se si tenta di toouse un nome per hello cloud risorsa gruppo/servizio cloud che è già stato usato, Azure assegna hello risorsa gruppo/servizio cloud hello stesso nome come hello macchina virtuale. Azure visualizza i gruppi di risorse/servizi cloud e le VM non associate ai gruppi di affinità. Per ulteriori informazioni, vedere [come toomigrate da gruppi di affinità tooa internazionali rete virtuale (VNet)](../virtual-network/virtual-networks-migrate-to-regional-vnet.md).
* **Rete virtuale** : selezionare la rete virtuale (VNET) durante la creazione di hello hello macchina virtuale. campo di Hello fornisce tutte le reti virtuali associate alla sottoscrizione hello. Gruppo di risorse di hello VM viene visualizzato tra parentesi.
* **Subnet** -se hello rete virtuale dispone di subnet, prima subnet hello è selezionata per impostazione predefinita. Se sono presenti altre subnet, selezionare la subnet hello desiderato.
* **Account di archiviazione** -questo menu elenca gli account di archiviazione hello in hello stesso percorso hello insieme di credenziali di servizi di ripristino. Gli account di archiviazione con ridondanza della zona non sono supportati. Se non sono disponibili account di archiviazione con servizi di ripristino hello stesso percorso hello credenziali, è necessario crearne uno prima di avviare l'operazione di ripristino hello. tipo di replica dell'account di archiviazione Hello viene riportato tra parentesi.

![Configurazione guidata del ripristino configurata](./media/backup-azure-arm-restore-vms/recovery-configuration-wizard.png)

> [!NOTE]
> 1. Se si vuole ripristinare una macchina virtuale distribuita con il modello di distribuzione Resource Manager, è necessario identificare una rete virtuale. Una rete virtuale è facoltativa per una macchina virtuale distribuita con il modello di distribuzione classica.
> 2. Se si desidera ripristinare le macchine virtuali con dischi gestiti, assicurarsi che l'account di archiviazione selezionato non sia stato abilitato per la crittografia del servizio di archiviazione (Storage Service Encryption - SSE) nel corso del suo ciclo di vita.
> 3. Basato sul tipo di archiviazione hello dell'account di archiviazione selezionato (standard o premium), tutti i dischi ripristinati sarà premium o dischi standard. Attualmente non sono supportati dischi in modalità mista durante il ripristino.  
>
>

In hello **ripristino configurazione** pannello, fare clic su **OK** ripristino configurazione di toofinalize hello. In hello **ripristinare** pannello, fare clic su **ripristinare** tootrigger operazione di ripristino hello.

## <a name="restore-backed-up-disks"></a>Ripristinare i dischi di cui è stato eseguito il backup
Se si desidera una macchina virtuale di hello toocustomize quale si desidera toocreate dal backup dischi rispetto a quello presente nel Pannello di configurazione Ripristina, seleziona **ripristinare dischi** come valore per **tipo ripristinare**. Questa opzione richiede un account di archiviazione in cui vengono copiati i dischi dal backup. Quando si sceglie un account di archiviazione, selezionare un account che condivisioni hello nello stesso percorso come insieme di credenziali di servizi di ripristino hello. Gli account di archiviazione con ridondanza della zona non sono supportati. Se non sono disponibili account di archiviazione con servizi di ripristino hello stesso percorso hello credenziali, è necessario crearne uno prima di avviare l'operazione di ripristino hello. tipo di replica dell'account di archiviazione Hello viene riportato tra parentesi.

Al termine dell'operazione di ripristino, è possibile:
* [VM di ripristino hello toocustomize modello di utilizzo](#use-templates-to-customize-restore-vm)
* [Hello utilizzare ripristinato macchina virtuale esistente di dischi tooattach tooan](../virtual-machines/windows/attach-managed-disk-portal.md)
* [Creare una nuova macchina virtuale tramite PowerShell dai dischi ripristinati.](./backup-azure-vms-automation.md#restore-an-azure-vm)

In hello **ripristino configurazione** pannello, fare clic su **OK** ripristino configurazione di toofinalize hello. In hello **ripristinare** pannello, fare clic su **ripristinare** tootrigger operazione di ripristino hello.

![Configurazione di ripristino completata](./media/backup-azure-arm-restore-vms/trigger-restore-operation.png)

## <a name="track-hello-restore-operation"></a>Operazione di ripristino hello traccia
Quando si attiva l'operazione di ripristino hello, hello servizio di Backup crea un processo per l'operazione di ripristino hello di rilevamento. Hello servizio di Backup anche crea e visualizza temporaneamente notifica hello nell'area di notifica del portale. Se non viene visualizzata la notifica hello, è sempre possibile scegliere hello notifiche icona tooview le notifiche.

![Ripristino attivato](./media/backup-azure-arm-restore-vms/restore-notification.png)

operazione di hello tooview durante l'elaborazione o tooview quando è stata completata, aprire l'elenco dei processi di Backup hello.

1. Hello Azure menu, scegliere **Sfoglia** e nell'elenco di hello dei servizi, digitare **servizi di ripristino**. elenco di Hello servizi regola toowhat digitato. Quando viene visualizzato **Insiemi di credenziali dei servizi di ripristino**, selezionare questa opzione.

    ![Aprire l'insieme di credenziali dei Servizi di ripristino](./media/backup-azure-arm-restore-vms/open-recovery-services-vault.png)

    viene visualizzato l'elenco di Hello degli insiemi di credenziali nella sottoscrizione hello.

    ![Elenco di insiemi di credenziali dei Servizi di ripristino](./media/backup-azure-arm-restore-vms/list-of-rs-vaults.png)
2. Dall'elenco di hello, insieme di credenziali selezionare hello associato hello VM è stato ripristinato. Quando si sceglie l'insieme di credenziali hello, verrà visualizzato il relativo dashboard.
3. Nel dashboard dell'insieme di credenziali hello in hello **i processi di Backup** riquadro, fare clic su **macchine virtuali di Azure** processi hello toodisplay associati all'insieme di credenziali hello.

    ![Dashboard dell'insieme di credenziali](./media/backup-azure-arm-restore-vms/vault-dashboard-jobs.png)

    Hello **i processi di Backup** blade si apre e visualizza l'elenco hello dei processi.

    ![Elenco di VM nell'insieme di credenziali](./media/backup-azure-arm-restore-vms/restore-job-in-progress.png)
    
## <a name="use-templates-toocustomize-restore-vm"></a>Utilizzare modelli toocustomize ripristino vm
Una volta [viene completata l'operazione di ripristino dischi](#Track-the-restore-operation), è possibile utilizzare il modello hello che viene generato come parte dell'operazione di ripristino toocreate una nuova macchina virtuale con una configurazione diversa dai nomi di configurazione o toocustomize backup delle risorse creato come creare una nuova macchina virtuale dal punto di ripristino. 

> [!NOTE]
> Verranno aggiunti i modelli come parte dell'operazione di ripristino dei dischi per i punti di ripristino creati dopo il 1° marzo 2017. Sono applicabili alle macchine virtuali del disco non crittografato e non gestito. Il supporto per le macchine virtuali crittografate e le macchine virtuali del disco gestito verrà fornito nelle versioni future. 
>
>

modello di hello tooget generato come parte dell'opzione di dischi, ripristino

1. Passare i dettagli dei processi toorestore toohello processo corrispondente. 
2. Nella schermata dei dettagli processo hello ripristino, fare clic su *distribuire modello* pulsante tooinitiate distribuzione del modello. 

     ![drill-down del processo di ripristino](./media/backup-azure-arm-restore-vms/restore-job-drill-down.png)
   
Nel Pannello di modello hello Distribuisci per la distribuzione personalizzata, utilizzare la distribuzione dei modelli troppo[modificare e distribuire il modello di hello](../azure-resource-manager/resource-group-template-deploy-portal.md#deploy-resources-from-custom-template) o aggiungere ulteriori personalizzazioni da [creando un modello](../azure-resource-manager/resource-group-authoring-templates.md) prima di distribuire. 

   ![caricamento della distribuzione del modello](./media/backup-azure-arm-restore-vms/loading-template.png)
   
Dopo aver immesso i valori hello richiesto, accettare hello *termini e condizioni* e fare clic su **acquisto**.

   ![invio della distribuzione del modello](./media/backup-azure-arm-restore-vms/submitting-template.png)

## <a name="post-restore-steps"></a>Operazioni successive al ripristino
* Se si usa una distribuzione Linux basata su cloud-init, ad esempio Ubuntu, per motivi di sicurezza la password viene bloccata dopo il ripristino. Per utilizzare estensione VMAccess su hello ripristinato VM troppo[hello di reimpostazione password](../virtual-machines/linux/classic/reset-access.md). È consigliabile utilizzare le chiavi SSH su tooavoid queste distribuzioni reimpostazione password post ripristino.
* Estensioni presenti durante la configurazione di backup hello verranno installate, ma che non sarà attivati. In caso di problemi, reinstallare le estensioni. 
* Se backup hello macchina virtuale è l'indirizzo IP statico, il ripristino di post, macchina virtuale ripristinata conterrà un conflitto di tooavoid IP dinamico durante la creazione di VM di ripristino. Altre informazioni su come è possibile [aggiungere un toorestored IP statico VM](../virtual-network/virtual-networks-reserved-private-ip.md#how-to-add-a-static-internal-ip-to-an-existing-vm)
* La macchina virtuale ripristinata non avrà set di disponibilità. È consigliabile usare l'opzione di ripristino dei dischi e [aggiungere il set di disponibilità](../virtual-machines/windows/tutorial-availability-sets.md) durante la creazione di una macchina virtuale da PowerShell o dei modelli tramite i dischi ripristinati. 


## <a name="backup-for-restored-vms"></a>Backup per le macchine virtuali ripristinate
Se è stato ripristinato VM toosame gruppo di risorse con stesso nome originariamente il backup VM hello, backup continua su hello ripristino post macchina virtuale. Se si è ripristinato gruppo di risorse diverso tooa VM o specificare un nome diverso per la macchina virtuale ripristinata, questo viene considerato come una nuova macchina virtuale e toosetup backup necessario per la macchina virtuale ripristinata.

## <a name="restoring-a-vm-during-azure-datacenter-disaster"></a>Ripristino di una macchina virtuale durante un'emergenza nel data center di Azure
Backup di Azure consente di ripristino di backup associati data center di macchine virtuali toohello nel caso in cui le macchine virtuali eseguono esperienze di emergenza e sono configurati toobe insieme di credenziali di Backup con ridondanza geografica di hello primario data center. Durante tali scenari, è necessario un account di archiviazione, è presente nel centro dati associato tooselect e resto del processo di ripristino hello rimane stesso. Backup di Azure Usa il servizio di calcolo dalla macchina virtuale di area geografica associata toocreate hello ripristinato. Altre informazioni sulla [resilienza dei centri dati di Azure](../resiliency/resiliency-technical-guidance-recovery-loss-azure-region.md)

## <a name="restoring-domain-controller-vms"></a>Ripristino delle macchine virtuali del controller di dominio
L'esecuzione del backup delle macchine virtuali del controller di dominio (DC) è uno scenario supportato da Backup di Azure. Tuttavia, prestare attenzione durante il processo di ripristino hello. il processo di ripristino corrette Hello dipende dalla struttura di hello del dominio hello. Nel caso più semplice hello è un singolo controller di dominio in un singolo dominio. Più comunemente per i carichi di produzione, saranno presenti più controller di dominio per ogni dominio, ad esempio alcuni controller locali. Infine, è possibile avere una foresta con più domini. 

Da un hello prospettiva di Active Directory macchina virtuale di Azure è come qualsiasi altra macchina virtuale in un hypervisor supportato moderna. Hello differenza principale con gli hypervisor locale è che non è disponibile in Azure console macchina virtuale. La console è obbligatoria per alcuni scenari, ad esempio per il ripristino tramite un backup di tipo di ripristino bare metal (BMR). Ripristino macchina virtuale dall'insieme di credenziali backup hello è tuttavia una sostituzione completa per il ripristino bare metal. È anche disponibile Active Directory Restore Mode (DSRM), in modo che tutti gli scenari di ripristino di Active Directory siano attuabili. Per altre informazioni di base, vedere [Backup and Restore considerations for virtualized Domain Controllers](https://technet.microsoft.com/en-us/library/virtual_active_directory_domain_controller_virtualization_hyperv(v=ws.10).aspx#backup_and_restore_considerations_for_virtualized_domain_controllers) (Considerazioni sul backup e sul ripristino per i controller di dominio virtualizzati) e [Planning for Active Directory Forest Recovery](https://technet.microsoft.com/en-us/library/planning-active-directory-forest-recovery(v=ws.10).aspx) (Pianificazione del ripristino delle foreste di Active Directory).

### <a name="single-dc-in-a-single-domain"></a>Controller di dominio unico in un singolo dominio
Hello VM possono essere ripristinati (ad esempio, tutte le altre VM) da hello Azure portal o utilizzo di PowerShell.

### <a name="multiple-dcs-in-a-single-domain"></a>Controller di dominio multipli in un singolo dominio
Quando altri controller di dominio di hello nello stesso dominio può essere raggiunto attraverso hello rete, hello controller di dominio può essere ripristinato come qualsiasi macchina virtuale. Se è hello ultimo restanti controller di dominio nel dominio hello o viene eseguito un ripristino in una rete isolata, deve essere seguita una procedura di ripristino della foresta.

### <a name="multiple-domains-in-one-forest"></a>Domini multipli in una foresta
Quando altri controller di dominio di hello nello stesso dominio può essere raggiunto attraverso hello rete, hello controller di dominio può essere ripristinato come qualsiasi macchina virtuale. Tuttavia, in tutti gli altri casi è consigliabile il ripristino della foresta.

## <a name="restoring-vms-with-special-network-configurations"></a>Ripristino delle macchine virtuali con configurazioni di rete speciali
È possibile tooback backup e ripristino di macchine virtuali con hello seguenti configurazioni di rete speciali. Tuttavia, queste configurazioni richiedono alcune considerazioni speciali durante passare attraverso il processo di ripristino hello.

* Macchine virtuali nel servizio di bilanciamento del carico (interno ed esterno)
* Macchine virtuali con più indirizzi IP riservati
* Macchine virtuali con più NIC

> [!IMPORTANT]
> Quando si crea la configurazione di rete speciale hello per le macchine virtuali, è necessario utilizzare le macchine virtuali toocreate PowerShell dai dischi hello ripristinati.
>
>

macchine virtuali di toofully ricreare hello dopo il ripristino toodisk, seguire questi passaggi:

1. Ripristinare i dischi hello da un insieme di credenziali per servizi di ripristino tramite [PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm)
2. Configurazione della macchina virtuale hello necessarie per Bilanciamento carico di creare / più NIC/più riservato IP utilizzando hello i cmdlet di PowerShell e usarlo hello toocreate macchina virtuale della configurazione desiderata.

   * Creare una macchina virtuale nel servizio cloud con [bilanciamento del carico interno ](https://azure.microsoft.com/documentation/articles/load-balancer-internal-getstarted/)
   * Creare VM tooconnect troppo[bilanciamento del carico per Internet](https://azure.microsoft.com/en-us/documentation/articles/load-balancer-internet-getstarted/)
   * Creare una macchina virtuale con [più NIC](https://azure.microsoft.com/documentation/articles/virtual-networks-multiple-nics/)
   * Creare una macchina virtuale con [più indirizzi IP riservati](https://azure.microsoft.com/documentation/articles/virtual-networks-reserved-public-ip/)

## <a name="next-steps"></a>Passaggi successivi
Ora che è possibile ripristinare le macchine virtuali, vedere Risoluzione dei problemi per ulteriori informazioni sugli errori comuni con le macchine virtuali hello. Inoltre, si consiglia di estrarre articolo hello sulla gestione delle attività con le macchine virtuali.

* [Risoluzione dei problemi](backup-azure-vms-troubleshoot.md#restore)
* [Gestire le macchine virtuali](backup-azure-manage-vms.md)
