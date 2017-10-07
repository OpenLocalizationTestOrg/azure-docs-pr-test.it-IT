---
title: aaaReplicate macchine virtuali Hyper-V tooAzure | Documenti Microsoft
description: Viene descritto come replica tooorchestrate, failover e il ripristino di locale Hyper-V VM tooAzure
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 1777e0eb-accb-42b5-a747-11272e131a52
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 04/05/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: hyper-v-site-walkthrough-overview
ms.openlocfilehash: 6fba41e43823fc57511d51ea2e09691159693982
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-without-vmm-tooazure-using-azure-site-recovery-with-hello-azure-portal"></a>La replica Hyper-V le macchine virtuali (senza VMM) tooAzure con Azure Site Recovery hello portale di Azure

> [!div class="op_single_selector"]
> * [Portale di Azure](site-recovery-hyper-v-site-to-azure.md)
> * [Azure classico](site-recovery-hyper-v-site-to-azure-classic.md)
> * [PowerShell - Gestione risorse](site-recovery-deploy-with-powershell-resource-manager.md)
>
>

In questo articolo viene descritto come tooreplicate locale tooAzure di macchine virtuali Hyper-V, utilizzando [Azure Site Recovery](site-recovery-overview.md) in hello portale di Azure. In questa distribuzione le macchine virtuali Hyper-V non vengono gestite tramite la soluzione Virtual Machine Manager (VMM) di System Center.

Dopo aver letto questo articolo, inviare eventuali commenti nella parte inferiore di hello o porre domande tecniche su hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

Se si desidera toomigrate macchine tooAzure (senza il failback), per ulteriori [questo articolo](site-recovery-migrate-to-azure.md).



## <a name="deployment-steps"></a>Passaggi di distribuzione

Seguire questi passaggi per la distribuzione di hello articolo toocomplete:

1. [Altre informazioni](site-recovery-components.md#hyper-v-to-azure) sull'architettura di hello per questa distribuzione. Ottenere inoltre [altre informazioni](site-recovery-hyper-v-azure-architecture.md) sul funzionamento della replica Hyper-V in Site Recovery.
2. Verificare i prerequisiti e le limitazioni.
3. Configurare la rete e gli account di archiviazione di Azure.
4. Preparare gli host Hyper-V.
5. Creare un insieme di credenziali dei servizi di ripristino. insieme di credenziali Hello contiene impostazioni di configurazione e Orchestra la replica.
6. Specificare le impostazioni di origine. Creare un sito Hyper-V che contiene gli host Hyper-V hello e registrare sito hello nell'insieme di credenziali hello. Installare Provider di Azure Site Recovery hello e agente di servizi di ripristino di Microsoft hello, negli host Hyper-V hello.
7. Specificare le impostazioni di replica e di destinazione.
8. Abilitare la replica per hello macchine virtuali.
9. Eseguire un toomake di failover di test che tutto funzioni come previsto.



## <a name="prerequisites"></a>Prerequisiti


**Requisito** | **Dettagli** |
--- | --- |
**Azure** | Vedere i [requisiti di Azure](site-recovery-prereq.md#azure-requirements).
**Server locali** | [Altre informazioni](site-recovery-prereq.md#disaster-recovery-of-hyper-v-virtual-machines-to-azure-no-virtual-machine-manager) sui requisiti per gli host Hyper-V locale di hello.
**VM Hyper-V locali** | Macchine virtuali che si desidera tooreplicate deve essere in esecuzione un [sistema operativo supportato](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)e devono essere conformi con [Azure prerequisiti](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
**URL di Azure** | Host Hyper-V è necessario accedere toothese URL:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> Se si dispone di regole del firewall basato su indirizzi IP, assicurarsi che consentano la comunicazione tooAzure.<br/></br> Consenti hello [intervalli IP dei Data Center Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)e hello porta HTTPS (443).<br/></br> Consenti gli intervalli di indirizzi IP per hello area della sottoscrizione di Azure e per Stati Uniti occidentali (utilizzato per il controllo di accesso e gestione delle identità).



## <a name="prepare-for-deployment"></a>Preparare la distribuzione

tooprepare per la distribuzione che è necessario:

1. [Configurare una rete di Azure](#set-up-an-azure-network) in cui verranno collocate le VM di Azure al momento della creazione, dopo il failover.
2. [Configurare un account di archiviazione di Azure](#set-up-an-azure-storage-account) per i dati replicati.
3. [Preparare gli host Hyper-V hello](#prepare-the-hyper-v-hosts) tooensure possano accedere hello necessari URL.

### <a name="set-up-an-azure-network"></a>Configurare una rete di Azure

Configurare una rete di Azure. È necessario in modo che le macchine virtuali di Azure hello create dopo il failover rete tooa connesso.

* rete Hello devono trovarsi in hello stessa area hello insieme di credenziali di servizi di ripristino.
* A seconda del modello di risorsa hello desiderate toouse per eseguire il failover le macchine virtuali di Azure, impostate hello rete di Azure in [modalità di gestione risorse](../virtual-network/virtual-networks-create-vnet-arm-pportal.md), o [modalità classica](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).
* È consigliabile configurare una rete prima di iniziare. In caso contrario, è necessario toodo durante la distribuzione di Site Recovery.
- Gli account di archiviazione utilizzati da Site Recovery non possono essere [spostato](../azure-resource-manager/resource-group-move-resources.md) all'interno di hello stesso, o in sottoscrizioni diverse,.


### <a name="set-up-an-azure-storage-account"></a>Configurare un account di archiviazione di Azure

- È necessario un account di archiviazione Azure toohold dati replicati tooAzure standard o premium. [Archiviazione premium](../storage/storage-premium-storage.md) viene in genere utilizzato per le macchine virtuali che richiedono un costantemente elevato delle prestazioni dei / o e carichi di lavoro con utilizzo intensivo a bassa latenza toohost IO.
- Se si desidera toouse un toostore account premium dati replicati, è inoltre necessario disporre di un log del replica toostore account di archiviazione standard che in corso di acquisizione Cambia dati tooon locali.
- A seconda del modello di risorsa hello desiderate toouse per eseguire il failover le macchine virtuali di Azure, è configurato un account in [modalità di gestione risorse](../storage/storage-create-storage-account.md), o [modalità classica](../storage/storage-create-storage-account-classic-portal.md).
- È consigliabile configurare un account di archiviazione prima di iniziare. In caso contrario, è necessario toodo durante la distribuzione di Site Recovery. Hello devono trovarsi nello hello stessa area hello insieme di credenziali di servizi di ripristino.
- Non è possibile spostare gli account di archiviazione utilizzato da Site Recovery nei gruppi di risorse all'interno di hello stessa sottoscrizione, o in diverse sottoscrizioni.


### <a name="prepare-hello-hyper-v-hosts"></a>Preparare l'host Hyper-V hello

* Verificare che gli host Hyper-V hello soddisfino hello [prerequisiti](site-recovery-prereq.md#disaster-recovery-of-hyper-v-virtual-machines-to-azure-no-virtual-machine-manager).
- Assicurarsi che gli host hello possono accedere agli URL di hello necessario.


## <a name="create-a-recovery-services-vault"></a>Creare un insieme di credenziali di Servizi di ripristino
1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Fare clic su **Nuovo** > **Monitoraggio e gestione** > **Backup e Site Recovery (OMS)**.  

    ![Nuovo insieme di credenziali](./media/site-recovery-hyper-v-site-to-azure/new-vault.png)

3. In **nome**, specificare un insieme di credenziali di nome descrittivo tooidentify hello. Se è disponibile più di una sottoscrizione, selezionarne una.

4. [Creare un nuovo gruppo di risorse](../azure-resource-manager/resource-group-template-deploy-portal.md) o selezionarne uno esistente e specificare un'area di Azure. Macchine saranno replicate toothis area. aree toocheck supportati, vedere disponibilità a livello geografico in [dettagli prezzi di Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).

5. Insieme di credenziali di tooquickly accesso hello da hello Dashboard, fare clic su **Pin toodashboard**, quindi fare clic su **crea**.

    ![Nuovo insieme di credenziali](./media/site-recovery-hyper-v-site-to-azure/new-vault-settings.png)

verrà visualizzata di nuovo insieme di credenziali Hello in hello **Dashboard** > **tutte le risorse** elenco e su hello principale **insiemi di credenziali di servizi di ripristino** blade.



## <a name="select-hello-protection-goal"></a>Selezionare l'obiettivo di protezione hello

Selezionare gli elementi da tooreplicate, e in cui si desidera tooreplicate per.

1. In hello **insiemi di credenziali di servizi di ripristino**selezionare insieme di credenziali hello.
2. In **Introduzione** fare clic su **Site Recovery** > **Preparare l'infrastruttura** > **Obiettivo di protezione**.

    ![Scegliere gli obiettivi](./media/site-recovery-hyper-v-site-to-azure/choose-goals.png)
3. In **obiettivi della protezione dati**selezionare **tooAzure**e selezionare **Sì, con Hyper-V**. Selezionare **n** tooconfirm VMM non è in uso. Fare quindi clic su **OK**.

    ![Scegliere gli obiettivi](./media/site-recovery-hyper-v-site-to-azure/choose-goals2.png)

## <a name="set-up-hello-source-environment"></a>Configurare un ambiente di origine hello

Impostare il sito di hello Hyper-V, installare hello Provider di Azure Site Recovery e l'agente di servizi di ripristino di Azure di hello negli host Hyper-V e registrare sito hello nell'insieme di credenziali hello.

1. In **Preparare l'infrastruttura** fare clic su **Origine**. Fare clic su un nuovo sito Hyper-V come contenitore per l'host Hyper-V o cluster, tooadd **+ sito Hyper-V**.

    ![Impostare l'origine](./media/site-recovery-hyper-v-site-to-azure/set-source1.png)
2. In **sito Hyper-V creare**, specificare un nome per il sito hello. Fare quindi clic su **OK**. Ora, selezionare il sito di hello creata, quindi fare clic su **+ Server Hyper-V** tooadd un sito di toohello server.

    ![Impostare l'origine](./media/site-recovery-hyper-v-site-to-azure/set-source2.png)

3. In **Aggiungi server** > **Tipo di server** verificare che sia visualizzato **Server Hyper-V**.

    - Verificare che tale server hello Hyper-V da tooadd è conforme con hello [prerequisiti](#on-premises-prerequisites), ed è in grado di tooaccess hello URL specificati.
    - Scaricare i file di installazione di Provider di Azure Site Recovery hello. Eseguire questo hello tooinstall file Provider e hello agente servizi di ripristino in ogni host Hyper-V.

    ![Impostare l'origine](./media/site-recovery-hyper-v-site-to-azure/set-source3.png)


## <a name="install-hello-provider-and-agent"></a>Installare hello Provider e agente

1. Eseguire i file di installazione di Provider di hello in ogni host aggiunti al sito toohello Hyper-V. Se l'installazione viene eseguita in un cluster Hyper-V, eseguire il file di installazione in ogni nodo del cluster. L'installazione e la registrazione di ogni nodo del cluster Hyper-V garantisce che le macchine virtuali siano protette anche se ne viene eseguita la migrazione tra i nodi.
2. In **Microsoft Update** è possibile acconsentire esplicitamente agli aggiornamenti in modo che gli aggiornamenti del provider vengano installati in base ai criteri di Microsoft Update.
3. In **installazione**, accettare o modificare percorso di installazione di Provider predefinito hello e fare clic su **installare**.
4. In **impostazioni insieme di credenziali**, fare clic su **Sfoglia** tooselect hello insieme di credenziali chiave file scaricato. Specificare una sottoscrizione di Azure Site Recovery hello, nome di archivio, hello e hello Hyper-V del sito toowhich hello Hyper-V server appartiene.

    ![Server registration](./media/site-recovery-hyper-v-site-to-azure/provider3.png)

5. In **le impostazioni del Proxy**, specificare la modalità Provider in esecuzione in host Hyper-V si connette tooAzure Site Recovery tramite hello hello internet.

    * Se si desidera selezionare direttamente hello Provider tooconnect **connettersi direttamente tooAzure il ripristino del sito senza un proxy**.
    * Se il proxy esistente richiede l'autenticazione, o si desidera toouse un proxy personalizzato per la connessione al Provider di hello, selezionare **connettersi tooAzure ripristino del sito utilizzando un server proxy**.
    * Se si usa un proxy:
        - Specificare le credenziali, porta e indirizzo hello
        - Rendono che URL hello descritto in hello [prerequisiti](#prerequisites) siano consentiti attraverso il proxy di hello.

    ![Internet](./media/site-recovery-hyper-v-site-to-azure/provider7.PNG)

6. Al termine dell'installazione, fare clic su **registrare** server hello tooregister nell'insieme di credenziali hello.

    ![Percorso di installazione](./media/site-recovery-hyper-v-site-to-azure/provider2.png)

7. Al termine della registrazione, i metadati dal server hello Hyper-V vengono recuperati da Azure Site Recovery e hello server viene visualizzato nel **infrastruttura di Site Recovery** > **host Hyper-V**.


## <a name="set-up-hello-target-environment"></a>Configurare un ambiente di destinazione hello

Specificare l'account di archiviazione di Azure hello per la replica e si connetterà hello Azure rete toowhich macchine virtuali di Azure dopo il failover.

1. Fare clic su **Preparare l'infrastruttura** > **Destinazione**.
2. Selezionare la sottoscrizione hello e gruppo di risorse hello in cui si desidera toocreate hello macchine virtuali di Azure dopo il failover. Scegliere hello distribuzione modello che si vuole toouse in Azure (classica o risorsa di gestione) per le macchine virtuali hello.

3. Site Recovery verifica la disponibilità di uno o più account di archiviazione di Azure e reti compatibili.

    - Se non si dispone di un account di archiviazione, fare clic su **+ archiviazione** toocreate inline un account basato su Gestione risorse. Leggere i [requisiti per l'archiviazione](site-recovery-prereq.md#azure-requirements).
    - Se non si dispone di una rete di Azure, fare clic su **+ rete** toocreate un inline basate su Gestione risorse di rete.

    ![Archiviazione](./media/site-recovery-vmware-to-azure/enable-rep3.png)




## <a name="configure-replication-settings"></a>Configurare le impostazioni di replica

1. toocreate nuovi criteri di replica, fare clic su **Prepare infrastruttura** > **le impostazioni di replica** > **+ crea e associa**.

    ![Rete](./media/site-recovery-hyper-v-site-to-azure/gs-replication.png)
2. In **Criteri di creazione e associazione**specificare il nome dei criteri.
3. In **frequenza di copia**, specificare la frequenza con cui si desidera dati delta tooreplicate dopo la replica iniziale hello (ogni 30 secondi, 5 o 15 minuti).

    > [!NOTE]
    > Quando la replica di archiviazione toopremium, non è supportata una frequenza secondo 30. limitazione di Hello è determinato dal numero di hello di snapshot per ogni blob (100) supportato da archiviazione premium. [Altre informazioni](../storage/storage-premium-storage.md#snapshots-and-copy-blob)

4. In **conservazione del punto di ripristino**, specificare in ore il tempo è un intervallo di conservazione hello per ogni punto di ripristino. Macchine virtuali possono essere ripristinati tooany punto all'interno di una finestra.
5. In **Frequenza snapshot coerenti con l'app** specificare la frequenza, da 1 a 12 ore, per la creazione di punti di ripristino contenenti snapshot coerenti con l'applicazione.

    - Hyper-V usa due tipi di snapshot, uno snapshot standard che fornisce uno snapshot incrementale dell'intera macchina virtuale di hello e uno snapshot coerente dell'applicazione che accetta uno snapshot del punto nel tempo dei dati dell'applicazione hello macchina virtuale hello.
    - Snapshot coerenti dell'applicazione usare tooensure del servizio Copia Shadow del Volume (VSS) che le applicazioni sono in uno stato coerente durante hello snapshot.
    - Se si abilita snapshot coerenti dell'applicazione, influisce negativamente sulle prestazioni di hello delle applicazioni in esecuzione in macchine virtuali di origine. Verificare che il valore di hello impostato è minore hello numero di punti di ripristino aggiuntivi configurati.

6. In **ora inizio replica iniziale**, specificare quando toostart hello la replica iniziale. la replica di Hello viene eseguita tramite la larghezza di banda internet pertanto è opportuno tooschedule è di fuori dell'orario di disponibilità. Fare quindi clic su **OK**.

    ![Criteri di replica](./media/site-recovery-hyper-v-site-to-azure/gs-replication2.png)

Quando si crea un nuovo criterio, è associata automaticamente a sito Hyper-V hello. È possibile associare un sito Hyper-V (e hello macchine virtuali in esso) a più criteri di replica in **replica** > criteri-name > **associare sito Hyper-V**.

## <a name="capacity-planning"></a>Pianificazione della capacità

Dopo aver configurato l'infrastruttura di base è possibile passare alla pianificazione della capacità e valutare se sono necessarie altre risorse.

Il ripristino del sito fornisce un toohelp di pianificazione della capacità è allocare risorse hello di calcolo, rete e archiviazione. È possibile eseguire la pianificazione hello in modalità rapida per le stime in base a un numero medio di macchine virtuali, dischi e archiviazione, o in modalità dettagliata con numeri personalizzati a livello di carico di lavoro hello. Prima di iniziare è necessario:

* Raccogliere informazioni sull'ambiente di replica, incluse le macchine virtuali, i dischi per ogni macchina virtuale e le risorse di archiviazione per ogni disco.
* Stima hello modifica (varianza) tariffa giornaliera per i dati replicati. È possibile utilizzare hello [Capacity Planner for Hyper-V Replica](https://www.microsoft.com/download/details.aspx?id=39057) toohelp si esegue questa operazione.

1. Fare clic su **scaricare** toodownload hello strumento e quindi eseguirlo. [Leggere l'articolo hello](site-recovery-capacity-planner.md) che accompagna strumento hello.
2. Al termine, selezionare **Sì** in **è stato eseguito hello Capacity Planner**?

   ![Pianificazione della capacità](./media/site-recovery-hyper-v-site-to-azure/gs-capacity-planning.png)

Ulteriori informazioni sul [controllo della larghezza di banda di rete](#network-bandwidth-considerations)



## <a name="enable-replication"></a>Abilitare la replica

Prima di iniziare, assicurarsi che l'account utente di Azure è necessario hello [autorizzazioni](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replica di un nuovo tooAzure macchina virtuale.

Abilitare la replica per le macchine virtuali nel modo seguente:          

1. Fare clic su **Eseguire la replica dell'applicazione** > **Origine**. Dopo aver configurato la replica per hello prima volta, è possibile fare clic su **+ replicare** replica tooenable per computer aggiuntivi.

    ![Abilitare la replica](./media/site-recovery-hyper-v-site-to-azure/enable-replication.png)
2. In **origine**, selezionare il sito hello Hyper-V. Fare quindi clic su **OK**.
3. In **destinazione**, selezionare una sottoscrizione di insieme di credenziali hello e hello failover modello toouse in Azure (classica o risorsa management) dopo il failover.
4. Selezionare l'account di archiviazione hello da toouse. Se non si dispone di un account a cui si vuole toouse, è possibile [crearlo](#set-up-an-azure-storage-account). Fare quindi clic su **OK**.
5. Quando si crea il failover, si connetterà hello seleziona Azure toowhich rete e subnet macchine virtuali di Azure.

    - tooapply hello rete impostazioni tooall macchine si abilita per la replica, selezionare **Configura ora per macchine virtuali selezionate**.
    - Selezionare **configurare successivamente** tooselect hello Azure rete al computer.
    - Se non si dispone di una rete a cui si desidera toouse, è possibile [crearlo](#set-up-an-azure-network). Selezionare una subnet, se applicabile. Fare quindi clic su **OK**.

   ![Abilitare la replica](./media/site-recovery-hyper-v-site-to-azure/enable-replication11.png)

6. In **macchine virtuali** > **selezionare le macchine virtuali**fare clic e selezionare ogni computer in cui si desidera tooreplicate. È possibile selezionare solo i computer per cui è possibile abilitare la replica. Fare quindi clic su **OK**.

    ![Abilitare la replica](./media/site-recovery-hyper-v-site-to-azure/enable-replication5-for-exclude-disk.png)

7. In **proprietà** > **configurare proprietà**selezionare hello del sistema operativo per le macchine virtuali selezionata hello e hello disco del sistema operativo.
8. Verificare il nome di macchina virtuale di Azure hello (nome di destinazione) sia conforme ai [requisiti macchina virtuale di Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
9. Per impostazione predefinita sono selezionati tutti i dischi di hello di hello VM per la replica, ma è possibile cancellare i dischi tooexclude li.
    - Si consiglia di larghezza di banda replica tooreduce tooexclude dischi. Ad esempio, non è possibile tooreplicate dischi con dati temporanei o dati che sono stato aggiornato un computer o App ogni volta che viene riavviato (ad esempio pagefile.sys o tempdb di Microsoft SQL Server). È possibile escludere il disco di hello dalla replica dal disco hello deselezionando la casella.
    - Solo i dischi di base possono essere esclusi dalla replica. Non è possibile escludere dischi del sistema operativo
    - e non è consigliabile escludere dischi dinamici. Site Recovery non può determinare se un disco rigido virtuale all'interno della macchina virtuale guest è di base o dinamico. Se non sono esclusi tutti i dischi dei volumi dinamici dipendenti, disco dinamico protetto hello verrà visualizzata come un disco guasto quando hello VM viene eseguito il failover e hello dati presenti sul disco non saranno accessibili.
        - Dopo aver abilitato la replica, non è più possibile aggiungere o rimuovere dischi da replicare. Se si desidera tooadd o esclude un disco, necessitano di protezione toodisable per hello macchina virtuale e riabilitarla.
        - Per i dischi creati manualmente in Azure non viene eseguito il failback. Ad esempio, se si esito negativo su tre dischi e creare due direttamente nella macchina virtuale di Azure, solo hello tre dischi che sono stati eseguiti il failover non verranno eseguiti nuovamente da Azure tooHyper-V. È possibile includere i dischi creati manualmente il failback oppure la replica inversa da tooAzure Hyper-V.
        - Se si esclude un disco è sufficiente per toooperate un'applicazione, dopo il failover tooAzure occorre toocreate manualmente in Azure, in modo che hello replicati applicazione può essere eseguito. In alternativa, è possibile integrare automazione di Azure in un piano di ripristino disco hello toocreate durante il failover della macchina hello.

10. Fare clic su **OK** toosave modifiche. È possibile impostare proprietà aggiuntive in un secondo momento.

    ![Abilitare la replica](./media/site-recovery-hyper-v-site-to-azure/enable-replication6-with-exclude-disk.png)

11. In **le impostazioni di replica** > **configurare le impostazioni di replica**, selezionare i criteri di replica hello da tooapply per hello protetto le macchine virtuali. Fare quindi clic su **OK**. È possibile modificare il criterio di replica hello in **criteri di replica** > criteri-name > **Modifica impostazioni**. Le modifiche applicate verranno usate per i computer di cui è già in corso la replica e per i nuovi computer.


   ![Abilitare la replica](./media/site-recovery-hyper-v-site-to-azure/enable-replication7.png)

È possibile monitorare lo stato di avanzamento di hello **Abilita protezione** processo **processi** > **i processi di ripristino del sito**. Dopo aver hello **finalizzazione della protezione** processo viene eseguito hello macchina è pronta per il failover.

### <a name="view-and-manage-vm-properties"></a>Visualizzare e gestire le proprietà della macchina virtuale

È consigliabile verificare le proprietà di hello hello computer di origine.

1. In **elementi protetti**, fare clic su **elementi replicati**e selezionare hello macchina.

    ![Abilitare la replica](./media/site-recovery-hyper-v-site-to-azure/test-failover1.png)
2. In **proprietà**, è possibile visualizzare la replica e le informazioni di failover per hello macchina virtuale.

    ![Abilitare la replica](./media/site-recovery-hyper-v-site-to-azure/test-failover2.png)
3. In **di calcolo e rete** > **calcolo proprietà**, è possibile specificare dimensioni delle macchine Virtuali di Azure hello nome e di destinazione. Se si desidera, modificare toocomply nome hello ai requisiti di Azure. È inoltre possibile visualizzare e modificare le informazioni relative alla rete di destinazione hello, subnet e indirizzi IP che verranno assegnato toohello macchina virtuale di Azure. Si noti hello segue:

   * È possibile impostare l'indirizzo IP di destinazione hello. Se non si fornisce un indirizzo, hello failover macchina utilizzerà DHCP. Se si imposta un indirizzo che non è disponibile in caso di failover, hello failover avrà esito negativo. Hello stesso indirizzo IP di destinazione è utilizzabile per il test failover se è disponibile in rete di failover di test hello hello indirizzo.
   * numero di Hello di schede di rete dipende dalla dimensione hello specificata per la macchina virtuale di destinazione hello, come indicato di seguito:

     * Se il numero di hello di schede di rete nel computer di origine hello è minore o uguale toohello numero di schede consentite per le dimensioni del computer di destinazione hello, quindi sarà necessario destinazione hello hello origine hello stesso numero di schede.
     * Se il numero di hello di schede per la macchina virtuale di origine hello supera il numero di hello consentito per la dimensione di destinazione hello quindi massimo di dimensioni di destinazione hello verrà utilizzato.
     * Se, ad esempio un computer di origine ha due schede di rete e le dimensioni del computer di destinazione hello supporta quattro, il computer di destinazione hello avrà due schede. Se il computer di origine hello dispone di due schede ma hello dimensioni di destinazione supportata supportano solo una macchina di destinazione hello avrà una sola scheda di.     
     * Se hello macchina virtuale dispone di più schede di rete verranno tutti connettono toohello stessa rete.
     * Se macchina virtuale hello ha più schede di rete hello prima uno nell'elenco di hello diventa hello *predefinito* scheda di rete nella macchina virtuale di Azure hello.

     ![Abilitare la replica](./media/site-recovery-hyper-v-site-to-azure/test-failover4.png)

4. In **dischi**, è possibile vedere hello del sistema operativo e dischi dati in hello VM che verranno replicati.

#### <a name="managed-disks"></a>Dischi gestiti

In **di calcolo e rete** > **calcolo proprietà**, è possibile impostare "Utilizzo dischi gestiti" impostazione troppo "Sì" per hello VM se si desidera tooattach dischi gestiti tooyour macchina in tooAzure di migrazione. Dischi gestiti semplifica la gestione disco per le macchine virtuali IaaS di Azure per la gestione degli account di archiviazione hello associati hello dischi di macchina virtuale. [Altre informazioni su Managed Disks](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview).

   - I dischi gestiti sono macchina virtuale creata e associata toohello solo su tooAzure un failover. Per abilitare la protezione, i dati da computer locali continueranno tooreplicate toostorage account.
   Dischi gestiti possono essere creati solo per macchine virtuali distribuite mediante il modello di distribuzione Gestione risorse di hello.

  > [!NOTE]
  > Il failback da un ambiente Hyper-V locale tooon Azure non è attualmente supportato per i computer con dischi gestiti. Impostare "Utilizzo dischi gestiti" troppo 'Yes' solo se si intende toomigrate tooAzure questo computer.

   - Quando si imposta "Utilizzo dischi gestiti" troppo "Yes", solo set di disponibilità nel gruppo di risorse hello con set di "Utilizzo dischi gestiti" troppo "Yes" saranno disponibili per la selezione. In questo modo le macchine virtuali con dischi gestiti può essere solo parte del set di disponibilità con il set di proprietà "Utilizzare gestito dischi" troppo "Yes". Assicurarsi di creare set di disponibilità con il set di proprietà "Dischi utilizzare gestito" in base a dischi toouse preventivo gestiti in caso di failover. Analogamente, quando si imposta "Utilizzo dischi gestiti" troppo "No", solo i set di disponibilità nel gruppo di risorse hello con proprietà "Utilizzo dischi gestiti" impostare troppo "No" saranno disponibili per la selezione. [Altre informazioni sui dischi gestiti e i set di disponibilità](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set).

  > [!NOTE]
  > Se l'account di archiviazione hello usato per la replica è stata crittografata con la crittografia del servizio di archiviazione in qualsiasi punto nel tempo, creazione di dischi gestiti durante il failover avrà esito negativo. È possibile impostare "Utilizzo dischi gestiti" troppo "No" e quindi ripetere il failover o disabilitare la protezione per la macchina virtuale hello e proteggerlo tooa account di archiviazione che non è abilitata in qualsiasi punto nel tempo la crittografia del servizio di archiviazione.
  > [Altre informazioni su Crittografia del servizio di archiviazione e dischi gestiti](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).


## <a name="test-hello-deployment"></a>Distribuzione di prova hello

distribuzione di hello tootest è possibile eseguire un failover di test per una singola macchina virtuale o un piano di ripristino che contiene uno o più macchine virtuali.

### <a name="before-you-start"></a>Prima di iniziare

 - Se si desidera tooconnect tooAzure macchine virtuali tramite RDP dopo il failover, vedere [preparazione tooconnect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover).
 - test toofully toocopy di Active Directory e DNS è necessario nell'ambiente di test. [Altre informazioni](site-recovery-active-directory.md#test-failover-considerations)

### <a name="run-a-test-failover"></a>Eseguire un failover di test

1. toofail su un singolo computer, in **elementi replicati**, fare clic su hello VM > **+ Test Failover** icona.
2. toofail sul ripristino di un piano, in **piani di ripristino**, piano hello rapida > **Failover di Test**. un piano di ripristino, toocreate [seguire queste istruzioni](site-recovery-create-recovery-plans.md).
3. In **Failover di Test**selezionare hello Azure rete toowhich macchine virtuali di Azure saranno connesse dopo il failover viene eseguito.
4. Fare clic su **OK** toobegin hello failover. È possibile monitorare i progressi facendo clic su hello VM tooopen le relative proprietà o in hello **Failover di Test** processo nel nome dell'insieme di credenziali > **processi** > **i processi di ripristino del sito**.
5. Al termine del processo di failover di hello, inoltre deve essere in grado di replica hello toosee macchina di Azure vengono visualizzati nel portale di Azure hello > **macchine virtuali**. È necessario verificare che tale hello VM sia dimensioni appropriate hello, che si è connesso toohello di rete appropriata e che sia in esecuzione.
6. Se sono preparati per le connessioni dopo il failover, dovrebbe essere in grado di tooconnect toohello macchina virtuale di Azure.
7. Al termine, fare clic su **il failover di test di pulizia** nel piano di ripristino hello. In **note** registrare e salvare eventuali commenti associati hello test failover. Questa operazione eliminerà hello le macchine virtuali che sono state create durante il failover di test.

Per altre informazioni, leggere hello [Test failover tooAzure](site-recovery-test-failover-to-azure.md) articolo.



## <a name="monitor-hello-deployment"></a>Monitoraggio hello distribuzione

Le impostazioni di configurazione di monitoraggio hello, stato e l'integrità per la distribuzione di Site Recovery:

1. Fare clic su hello tooaccess nome insieme di credenziali di hello **Essentials** dashboard. In questo dashboard è possibile rilevare i processi di Site Recovery, lo stato della replica, i piani di ripristino, l'integrità del server e gli eventi.  

    ![Informazioni di base](./media/site-recovery-hyper-v-site-to-azure/essentials.png)
2. In hello **integrità** riquadro è possibile monitorare i server del sito che segnalano problemi e hello gli eventi generati da Site Recovery hello ultime 24 ore. È possibile personalizzare i riquadri di Essentials tooshow hello e layout di tooyou più utili, incluso lo stato di hello altri il ripristino del sito e gli insiemi di credenziali di Backup.
3. È possibile gestire e monitorare la replica in hello **elementi replicati**, **piani di ripristino**, e **i processi di ripristino del sito** riquadri. È possibile eseguire il drill-down dei processi altri dettagli in **Processi** > **Site Recovery Jobs** (Processi di Site Recovery).

## <a name="command-line-provider-and-agent-installation"></a>Installazione del provider e dell'agente dalla riga di comando

Hello Provider di Azure Site Recovery e l'agente possono essere installati anche usando hello seguente riga di comando. Questo metodo può essere provider hello tooinstall utilizzati in un Server Core per Windows Server 2012 R2.

1. Scaricare hello Provider e registrazione tooa chiave cartella di installazione. ad esempio C:\ASR.
2. Da un prompt dei comandi con privilegi elevati, eseguire il programma di installazione del Provider questi comandi tooextract hello:

            C:\Windows\System32> CD C:\ASR
            C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
3. Eseguire questo comando tooinstall componenti hello:

            C:\ASR> setupdr.exe /i
4. Eseguire quindi questi server di hello tooregister comandi nell'insieme di credenziali hello:

            CD C:\Program Files\Microsoft Azure Site Recovery Provider\
            C:\Program Files\Microsoft Azure Site Recovery Provider\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file>

<br/>
Dove:

* **/ Credenziali**: parametro obbligatorio che specifica il percorso di hello in cui hello Trova file di chiave di registrazione  
* **/ FriendlyName**: parametro obbligatorio per il nome del server host Hyper-V hello visualizzata nel portale di Azure Site Recovery hello hello.
* **/ProxyAddress**: parametro facoltativo che specifica l'indirizzo di hello del server proxy hello.
* **/ProxyPort** : parametro facoltativo che specifica la porta del server proxy hello hello.
* **/proxyUsername**: parametro facoltativo che specifica il nome utente di hello Proxy (se proxy richiede l'autenticazione).
* **/proxyPassword**: parametro facoltativo che specifica hello Password per l'autenticazione con il server proxy hello (se proxy richiede l'autenticazione).


## <a name="network-bandwidth-considerations"></a>Considerazioni sulla larghezza di banda di rete
È possibile utilizzare hello [dello strumento di pianificazione della capacità di Hyper-V](site-recovery-capacity-planner.md) della larghezza di banda di toocalculate hello è necessario per la replica (la replica iniziale e quindi delta). quantità di hello toocontrol di utilizzo della larghezza di banda per la replica sono disponibili alcune opzioni:

* **Limitazione della larghezza di banda**: Hyper-V che vengono replicati tooAzure del traffico tramite uno specifico host Hyper-V. È possibile limitare la larghezza di banda nel server host hello.
* **Modificare la larghezza di banda**: È possibile influenzare la larghezza di banda hello utilizzata per la replica con un paio di chiavi del Registro di sistema.

### <a name="throttle-bandwidth"></a>Limitare la larghezza di banda
1. Aprire hello MMC di Backup di Microsoft Azure snap-nel server host Hyper-V di hello. Per impostazione predefinita, un collegamento per il Backup di Microsoft Azure è disponibile sul desktop hello o in C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.
2. Nello snap-in hello fare clic su **Modifica proprietà**.
3. In hello **limitazione** scheda selezionare **abilitare la limitazione per le operazioni di backup all'utilizzo della larghezza di banda di internet**e impostare i limiti di hello per lavoro e non lavorative ore. Valori validi sono compresi 512 Mbps di too102 Kbps al secondo.

    ![Limitare la larghezza di banda](./media/site-recovery-hyper-v-site-to-azure/throttle2.png)

È inoltre possibile utilizzare hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) tooset limitazione delle richieste di cmdlet. Di seguito è riportato un esempio:

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

**Set-OBMachineSetting -NoThrottle** indica che non è necessaria alcuna limitazione.

### <a name="influence-network-bandwidth"></a>Influire sulla larghezza di banda di rete
1. Nel Registro di sistema hello passare troppo**Backup\Replication Azure HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows**.
   * il traffico di larghezza di banda hello tooinfluence su un disco di replica, modificare hello valore hello **UploadThreadsPerVM**, o creare la chiave di hello se non esiste.
   * larghezza di banda hello tooinfluence per il traffico di failback da Azure, modificare il valore di hello **DownloadThreadsPerVM**.
2. valore predefinito di Hello è 4. In una rete di "provisioning eccessivo", queste chiavi del Registro di sistema devono essere modificate dai valori predefiniti di hello. Hello massimo è 32. Monitorare il traffico toooptimize hello valore.

## <a name="next-steps"></a>Passaggi successivi

Dopo il completamento della replica iniziale e il test di distribuzione di hello, è possibile richiamare i failover come hello necessità. [Altre informazioni](site-recovery-failover.md) sui diversi tipi di failover e modalità toorun li.
