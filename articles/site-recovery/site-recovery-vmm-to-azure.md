---
title: cloud di macchine virtuali Hyper-V in VMM aaaReplicate tooAzure | Documenti Microsoft
description: Gestire la replica, failover e il ripristino delle macchine virtuali Hyper-V gestiti in tooAzure cloud di System Center VMM
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: 84182fe4b63862ac7643208a22f236a7515a25a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure-using-site-recovery-in-hello-azure-portal"></a>Replicare le macchine virtuali Hyper-V in VMM cloud tooAzure usando Site Recovery nel portale di Azure hello
> [!div class="op_single_selector"]
> * [Portale di Azure](site-recovery-vmm-to-azure.md)
> * [Azure classico](site-recovery-vmm-to-azure-classic.md)
> * [PowerShell - Resource Manager](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [PowerShell - Classica](site-recovery-deploy-with-powershell.md)


In questo articolo viene descritto come tooreplicate locale macchine virtuali Hyper-V gestite in tooAzure cloud di System Center VMM, hello utilizzando [Azure Site Recovery](site-recovery-overview.md) di hello portale di Azure.

Dopo aver letto questo articolo, inviare eventuali commenti nella parte inferiore di hello o in hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

Se si desidera toomigrate macchine tooAzure (senza il failback), per ulteriori [questo articolo](site-recovery-migrate-to-azure.md).


## <a name="deployment-steps"></a>Passaggi di distribuzione

Seguire questi passaggi per la distribuzione di hello articolo toocomplete:


1. [Altre informazioni](site-recovery-components.md) sull'architettura di hello per questa distribuzione. Ottenere inoltre [altre informazioni](site-recovery-hyper-v-azure-architecture.md) sul funzionamento della replica Hyper-V in Site Recovery.
2. Verificare i prerequisiti e le limitazioni.
3. Configurare la rete e gli account di archiviazione di Azure.
4. Preparare i server VMM locale di hello e gli host Hyper-V.
5. Creare un insieme di credenziali dei servizi di ripristino. insieme di credenziali Hello contiene impostazioni di configurazione e Orchestra la replica.
6. Specificare le impostazioni di origine. Registrare il server VMM hello nell'insieme di credenziali hello. Installare Provider di Azure Site Recovery hello sull'agente di servizi di ripristino di Microsoft hello per la installazione server hello VMM negli host Hyper-V.
7. Specificare le impostazioni di replica e di destinazione.
8. Abilitare la replica per hello macchine virtuali.
9. Eseguire un toomake di failover di test che tutto funzioni come previsto.



## <a name="prerequisites"></a>Prerequisiti


**Requisiti di supporto** | **Dettagli**
--- | ---
**Azure** | Vedere i [requisiti di Azure](site-recovery-prereq.md#azure-requirements).
**Server locali** | [Altre informazioni](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-in-vmm-clouds-to-azure) sui requisiti per i server VMM locale di hello e gli host Hyper-V.
**VM Hyper-V locali** | Macchine virtuali che si desidera tooreplicate deve essere in esecuzione un [sistema operativo supportato](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)e devono essere conformi con [Azure prerequisiti](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
**URL di Azure** | server VMM Hello deve accedere toothese URL:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> Se si dispone di regole del firewall basato su indirizzi IP, assicurarsi che consentano la comunicazione tooAzure.<br/></br> Consenti hello [intervalli IP dei Data Center Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)e hello porta HTTPS (443).<br/></br> Consenti gli intervalli di indirizzi IP per hello area della sottoscrizione di Azure e per Stati Uniti occidentali (utilizzato per il controllo di accesso e gestione delle identità).


## <a name="prepare-for-deployment"></a>Preparare la distribuzione
tooprepare per la distribuzione, è necessario:

1. [Configurare una rete di Azure](#set-up-an-azure-network) in cui verranno collocate le VM di Azure dopo il failover.
2. [Configurare un account di archiviazione di Azure](#set-up-an-azure-storage-account) per i dati replicati.
3. [Preparare il server VMM hello](#prepare-the-vmm-server) per la distribuzione di Site Recovery.
4. Preparare il mapping di rete. Configurare le reti in modo che sia possibile configurare il mapping di rete durante la distribuzione di Site Recovery.

### <a name="set-up-an-azure-network"></a>Configurare una rete di Azure
È necessario un toowhich di rete di Azure creato dopo il failover si connetterà macchine virtuali di Azure.

* rete Hello devono trovarsi in hello stessa area hello insieme di credenziali di servizi di ripristino.
* A seconda del modello di risorsa hello desiderate toouse per eseguire il failover le macchine virtuali di Azure, impostate hello rete di Azure in [modalità di gestione risorse](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) o [modalità classica](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).
* È consigliabile configurare una rete prima di iniziare. In caso contrario, è necessario toodo durante la distribuzione di Site Recovery.
Le reti di Azure usate da Site Recovery non possono essere [spostato](../azure-resource-manager/resource-group-move-resources.md) all'interno di hello stesso, o in sottoscrizioni diverse,.

### <a name="set-up-an-azure-storage-account"></a>Configurare un account di archiviazione di Azure
* È necessario un account di archiviazione Azure toohold dati replicati tooAzure standard o premium. [Archiviazione premium](../storage/common/storage-premium-storage.md) viene utilizzato per le macchine virtuali che richiedono un costantemente elevato delle prestazioni dei / o e carichi di lavoro con utilizzo intensivo a bassa latenza toohost IO. Se si desidera toouse un toostore account premium dati replicati, è inoltre necessario disporre di un log del replica toostore account di archiviazione standard che in corso di acquisizione Cambia dati tooon locali. Hello account deve trovarsi in hello stessa area hello insieme di credenziali di servizi di ripristino.
* A seconda del modello di risorsa hello desiderate toouse per eseguire il failover le macchine virtuali di Azure, è configurato un account in [modalità di gestione risorse](../storage/common/storage-create-storage-account.md) o [modalità classica](../storage/common/storage-create-storage-account.md).
* È consigliabile configurare un account prima di iniziare. In caso contrario, è necessario toodo durante la distribuzione di Site Recovery.
- Si noti che l'account di archiviazione utilizzato da Site Recovery non può essere [spostato](../azure-resource-manager/resource-group-move-resources.md) all'interno di hello stesso, o in sottoscrizioni diverse,.

### <a name="prepare-hello-vmm-server"></a>Preparare il server VMM hello
* Verificare che il server VMM hello è conforme con hello [prerequisiti](#prerequisites).
* Durante la distribuzione di Site Recovery, è possibile specificare che tutti i cloud in un server VMM devono essere disponibili nel portale di Azure hello. Se si vuole solo tooappear specifica cloud nel portale di hello, è possibile abilitare questa impostazione nel cloud hello nella console di amministrazione VMM hello.

### <a name="prepare-for-network-mapping"></a>Preparare il mapping di rete
Durante la distribuzione di Site Recovery è necessario configurare il mapping di rete. Mapping di rete mappa tra le reti VM di VMM di origine e di destinazione le reti di Azure, hello tooenable seguenti:

* Computer che il failover su hello stessa rete possono connettersi tooeach altri, anche se non si failover hello stesso modo o in hello stesso piano di ripristino.
* Se un gateway di rete è configurato nella rete Azure di destinazione hello, macchine virtuali di Azure possono connettersi a macchine virtuali locali tooon.
* tooset mapping di rete, ecco cosa occorre:

  * Assicurarsi che le macchine virtuali di origine hello server host Hyper-V siano connesso tooa rete VM di VMM. La rete deve essere collegato tooa la rete logica associata al cloud hello.
  * Una rete di Azure come descritto [in precedenza](#set-up-an-azure-network)

## <a name="create-a-recovery-services-vault"></a>Creare un insieme di credenziali di Servizi di ripristino
1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Fare clic su **Nuovo** > **Monitoraggio e gestione** > **Backup e Site Recovery (OMS)**.

    ![Nuovo insieme di credenziali](./media/site-recovery-vmm-to-azure/new-vault3.png)
3. In **nome**, specificare un insieme di credenziali di nome descrittivo tooidentify hello. Se è disponibile più di una sottoscrizione, selezionarne una.
4. [Creare un gruppo di risorse](../azure-resource-manager/resource-group-template-deploy-portal.md)o selezionarne uno esistente. Specificare un'area di Azure. Macchine saranno replicate toothis area. aree toocheck supportato vedere aree geografiche disponibili in [dettagli prezzi di Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/)
5. Insieme di credenziali di tooquickly accesso hello da hello Dashboard, fare clic su **Pin toodashboard** > **Crea insieme di credenziali**.

    ![Nuovo insieme di credenziali](./media/site-recovery-vmm-to-azure/new-vault.png)

viene visualizzata di nuovo insieme di credenziali Hello in hello **Dashboard** > **tutte le risorse**e in hello principale **insiemi di credenziali di servizi di ripristino** blade.


## <a name="select-hello-protection-goal"></a>Selezionare l'obiettivo di protezione hello

Selezionare gli elementi da tooreplicate, e in cui si desidera tooreplicate per.

1. In **insiemi di credenziali di servizi di ripristino**selezionare insieme di credenziali hello.
2. In **Introduzione** fare clic su **Site Recovery** > **Preparare l'infrastruttura** > **Obiettivo di protezione**.

    ![Scegliere gli obiettivi](./media/site-recovery-vmm-to-azure/choose-goals.png)
3. In **obiettivi della protezione dati** selezionare **tooAzure**e selezionare **Sì, con Hyper-V**. Selezionare **Sì** tooconfirm gli host Hyper-V toomanage VMM e il sito di ripristino hello in uso. Fare quindi clic su **OK**.

## <a name="set-up-hello-source-environment"></a>Configurare un ambiente di origine hello

Installare hello Provider di Azure Site Recovery nel server VMM hello e registrare hello server nell'insieme di credenziali hello. Installare l'agente di servizi di ripristino di Azure hello in host Hyper-V.

1. Fare clic su **Preparare l'infrastruttura** > **Origine**.

    ![Impostare l'origine](./media/site-recovery-vmm-to-azure/set-source1.png)

2. In **origine Prepare**, fare clic su **+ VMM** tooadd un server VMM.

    ![Impostare l'origine](./media/site-recovery-vmm-to-azure/set-source2.png)

3. In **Aggiungi Server**, verificare che **server System Center VMM** viene visualizzato **tipo Server** e tale server VMM hello soddisfa hello [prerequisiti e l'URL requisiti](#prerequisites).
4. Scaricare i file di installazione di Provider di Azure Site Recovery hello.
5. Scaricare la chiave di registrazione hello. che sarà necessaria durante l'installazione. chiave di Hello è valida per cinque giorni dopo la generazione è.

    ![Impostare l'origine](./media/site-recovery-vmm-to-azure/set-source3.png)


## <a name="install-hello-provider-on-hello-vmm-server"></a>Installare hello Provider nel server VMM hello

1. Eseguire i file di installazione di Provider di hello nel server VMM hello.
2. In **Microsoft Update** è possibile acconsentire esplicitamente agli aggiornamenti in modo che gli aggiornamenti del provider vengano installati in base ai criteri di Microsoft Update.
3. In **installazione**, accettare o modificare percorso di installazione di Provider predefinito hello e fare clic su **installare**.

    ![Percorso di installazione](./media/site-recovery-vmm-to-azure/provider2.png)
4. Al termine dell'installazione, fare clic su **registrare** server VMM di hello tooregister nell'insieme di credenziali hello.
5. In hello **impostazioni insieme di credenziali** pagina, fare clic su **Sfoglia** tooselect file di chiave dell'insieme di credenziali hello. Specificare una sottoscrizione di Azure Site Recovery hello e il nome dell'insieme di credenziali hello.

    ![Server registration](./media/site-recovery-vmm-to-azure/provider10.PNG)
6. In **connessione Internet**, specificare la modalità Provider in esecuzione nel server VMM hello si connetterà tooSite ripristino su hello hello internet.

   * Se si desidera hello Provider tooconnect direttamente, selezionare **connettersi direttamente tooAzure il ripristino del sito senza un proxy**.
   * Se il proxy esistente richiede l'autenticazione, o si desidera toouse un proxy personalizzato, selezionare **connettersi tooAzure ripristino del sito utilizzando un server proxy**.
   * Se si utilizza un proxy personalizzato, specificare le credenziali, porta e indirizzo hello.
   * Se si utilizza un proxy, è necessario avere già hello URL consentiti descritto in [prerequisiti](#on-premises-prerequisites).
   * Se si utilizza un proxy personalizzato, un account RunAs VMM (DRAProxyAccount) verrà creato automaticamente tramite hello specificato le credenziali del proxy. Configurare il server proxy hello in modo che questo account può autenticare correttamente. le impostazioni dell'account RunAs VMM Hello possono essere modificate nella console VMM hello. In **impostazioni**, espandere **sicurezza** > **account RunAs**e quindi modificare la password di hello di DRAProxyAccount. Servizio VMM toorestart hello è necessario in modo che questa impostazione ha effetto.

     ![Internet](./media/site-recovery-vmm-to-azure/provider13.PNG)
7. Accettare o modificare il percorso di hello di un certificato SSL generato automaticamente per la crittografia dei dati. Questo certificato viene usato se si abilita la crittografia dei dati per un cloud protetto da Azure nel portale di Azure Site Recovery hello. Conservare il certificato in una posizione sicura, Quando si esegue un failover tooAzure necessario toodecrypt, se è abilitata la crittografia dei dati.

    > [!NOTE]
    > Si consiglia di funzionalità di crittografia hello toouse fornita da Azure per la crittografia dei dati inattivi, anziché utilizzare l'opzione di crittografia dati hello fornito da Azure Site Recovery. funzionalità di crittografia Hello fornita da Azure possono essere accesi per uno spazio di archiviazione > account e consente di ottenere prestazioni migliori, come la crittografia o decrittografia hello è gestita da archiviazione di Azure.
    > [Altre informazioni sulla crittografia del servizio di archiviazione in Azure](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption).
    
8. In **nome Server**, specificare un server di nome descrittivo tooidentify hello VMM nell'insieme di credenziali hello. In una configurazione cluster, specificare il nome del ruolo cluster VMM hello.
9. Abilitare **Sincronizza metadati cloud**, se si desidera toosynchronize metadati per tutti i cloud nel server VMM hello con insieme di credenziali hello. Questa azione deve solo toohappen una volta in ogni server. Se non si desidera toosynchronize tutti i cloud, è possibile lasciare deselezionata questa opzione e sincronizzare ogni cloud singolarmente nelle proprietà del cloud nella console VMM hello hello. Fare clic su **registrare** processo hello toocomplete.

    ![Server registration](./media/site-recovery-vmm-to-azure/provider16.PNG)
10. Verrà avviata la registrazione. Al termine della registrazione, il server di hello viene visualizzato nel **infrastruttura di Site Recovery** > **server VMM**.


## <a name="install-hello-azure-recovery-services-agent-on-hyper-v-hosts"></a>Installare l'agente di servizi di ripristino di Azure hello in host Hyper-V

1. Dopo aver configurato la hello Provider, file di installazione toodownload hello è necessario per l'agente di servizi di ripristino di Azure hello. Eseguire l'installazione in ogni server Hyper-V hello cloud VMM.

    ![Siti Hyper-V](./media/site-recovery-vmm-to-azure/hyperv-agent1.png)
2. In **Controllo dei prerequisiti** fare clic su **Avanti**. Gli eventuali prerequisiti mancanti verranno installati automaticamente.

    ![Prerequisiti per l'agente di Servizi di ripristino di Azure](./media/site-recovery-vmm-to-azure/hyperv-agent2.png)
3. In **le impostazioni di installazione**, accettare o modificare il percorso di installazione di hello e percorso della cache di hello. È possibile configurare cache di hello in un'unità con almeno 5 GB di spazio di archiviazione disponibile, ma è consigliabile un'unità di cache con più di 600 GB di spazio libero. Fare clic su **Installa**.
4. Al termine dell'installazione, fare clic su **Chiudi** toofinish.

    ![Registrare l'Agente di Servizi di ripristino di Microsoft Azure](./media/site-recovery-vmm-to-azure/hyperv-agent3.png)

### <a name="command-line-installation"></a>Installazione dalla riga di comando
È possibile installare agente servizi di ripristino di Microsoft Azure hello dalla riga di comando utilizzando hello comando seguente:

     marsagentinstaller.exe /q /nu

### <a name="set-up-internet-proxy-access-toosite-recovery-from-hyper-v-hosts"></a>Configurare internet proxy accesso tooSite ripristino dagli host Hyper-V

agente di servizi di ripristino Hello in esecuzione in host Hyper-V deve tooAzure accesso internet per la replica di macchina virtuale. Se si accede hello internet tramite un proxy, configurarlo come indicato di seguito:

1. Aprire hello Microsoft Azure Backup snap-in MMC in host Hyper-V hello. Per impostazione predefinita, un collegamento per il Backup di Microsoft Azure è disponibile sul desktop hello o in C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.
2. Hello nello snap-in, fare clic su **Modifica proprietà**.
3. In hello **configurazione Proxy** , specificare le informazioni sul server proxy.

    ![Registrare l'Agente di Servizi di ripristino di Microsoft Azure](./media/site-recovery-vmm-to-azure/mars-proxy.png)
4. Verificare che l'agente di hello possibile raggiungere l'URL di hello descritto in hello [prerequisiti](#on-premises-prerequisites).

## <a name="set-up-hello-target-environment"></a>Configurare un ambiente di destinazione hello
Specificare hello toobe di account di archiviazione di Azure utilizzata per la replica si connetterà hello Azure rete toowhich macchine virtuali di Azure dopo il failover.

1. Fare clic su **Prepare infrastruttura** > **destinazione**, selezionare la sottoscrizione hello e hello gruppo di risorse in cui si desidera hello toocreate eseguito il failover delle macchine virtuali. Scegliere modello di distribuzione hello che si desidera toouse in Azure (classica o risorsa di gestione) per il failover le macchine virtuali hello.

    ![Archiviazione](./media/site-recovery-vmm-to-azure/enablerep3.png)

2. Site Recovery verifica la disponibilità di uno o più account di archiviazione di Azure e reti compatibili.

    ![Archiviazione](./media/site-recovery-vmm-to-azure/compatible-storage.png)

3. Se ancora stato creato un account di archiviazione e si desidera toocreate uno usando Gestione risorse, fare clic su **+ account di archiviazione** toodo tale inline.  In hello **creare account di archiviazione** pannello specificare un nome dell'account, tipo, sottoscrizione e posizione. Hello account deve essere hello stesso percorso hello insieme di credenziali di servizi di ripristino.

   ![Archiviazione](./media/site-recovery-vmm-to-azure/gs-createstorage.png)


   * Se si desidera toocreate un account di archiviazione utilizzando il modello classico hello, eseguire questa operazione in hello portale di Azure. [Altre informazioni](../storage/common/storage-create-storage-account.md)
   * Se si utilizza un account di archiviazione premium per i dati replicati, impostare un account di archiviazione standard aggiuntiva, i log di replica toostore che acquisiscono dati locali tooon le modifiche in corso.
5. Se non è stata creata una rete di Azure e si desidera toocreate uno usando Gestione risorse, fare clic su **+ rete** toodo tale inline. In hello **crea rete virtuale** pannello specificare un nome di rete, intervallo di indirizzi, i dettagli di subnet, sottoscrizione e posizione. rete Hello devono trovarsi in hello stesso percorso hello insieme di credenziali di servizi di ripristino.

   ![Rete](./media/site-recovery-vmm-to-azure/gs-createnetwork.png)

   Se si desidera toocreate una rete usando il modello classico di hello, eseguire questa operazione in hello portale di Azure. [Altre informazioni](../virtual-network/virtual-networks-create-vnet-classic-pportal.md)

### <a name="configure-network-mapping"></a>Configurare il mapping di rete

* [Fare clic qui](#prepare-for-network-mapping) per una panoramica rapida del funzionamento del mapping di rete.
* Verificare che le macchine virtuali nel server VMM hello siano rete VM tooa connessi e di aver creato almeno una rete virtuale di Azure. Più reti VM possono essere mappate tooa singola rete di Azure.

Per configurare il mapping, procedere come segue:

1. In **infrastruttura di Site Recovery** > **mapping di rete** > **Mapping di rete**, fare clic su hello **+ Mapping di rete**  icona.

    ![Mapping di rete](./media/site-recovery-vmm-to-azure/network-mapping1.png)
2. In **aggiungere mapping di rete**, selezionare server VMM di origine hello e **Azure** come destinazione di hello.
3. Verificare la sottoscrizione hello e modello di distribuzione hello dopo il failover.
4. In **rete di origine**selezionare rete VM di hello origine locale si desidera toomap dall'elenco di hello associato al server VMM hello.
5. In **rete di destinazione**, selezionare hello in quale replica di macchine virtuali di Azure sarà disponibile quando si crea rete di Azure. Fare quindi clic su **OK**.

    ![Mapping di rete](./media/site-recovery-vmm-to-azure/network-mapping2.png)

Quando ha inizio il mapping di rete vengono eseguite le operazioni seguenti:

* Macchine virtuali esistenti in una rete VM origine hello sono connessi toohello rete di destinazione quando avviare il mapping. Rete VM di origine connesso toohello di nuove macchine virtuali connessi toohello eseguito il mapping di rete di Azure, quando viene eseguita la replica.
* Se si modifica un mapping di rete esistente, macchine virtuali di replica è possibile connettersi utilizzando le nuove impostazioni hello.
* Se la rete di destinazione hello dispone di più subnet e una di queste subnet è hello stesso nome di subnet nella macchina virtuale di origine che hello si trova, quindi hello macchina virtuale di replica si connette toothat subnet di destinazione dopo il failover.
* Se non è presente alcuna subnet di destinazione con un nome corrispondente, macchina virtuale hello si connette toohello prima subnet nella rete hello.

## <a name="configure-replication-settings"></a>Configurare le impostazioni di replica
1. toocreate nuovi criteri di replica, fare clic su **Prepare infrastruttura** > **le impostazioni di replica** > **+ crea e associa**.

    ![Rete](./media/site-recovery-vmm-to-azure/gs-replication.png)
2. In **Criteri di creazione e associazione**specificare il nome dei criteri.
3. In **frequenza di copia**, specificare la frequenza con cui si desidera dati delta tooreplicate dopo la replica iniziale hello (ogni 30 secondi, 5 o 15 minuti).

    > [!NOTE]
    >  Quando la replica di archiviazione toopremium, non è supportata una frequenza secondo 30. limitazione di Hello è determinato dal numero di hello di snapshot per ogni blob (100) supportato da archiviazione premium. [Altre informazioni](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob)

4. In **conservazione del punto di ripristino**, specificare in ore, per quanto tempo il periodo di memorizzazione hello verrà per ogni punto di ripristino. Macchine virtuali protette possono essere ripristinati tooany punto all'interno di una finestra.
5. In **Frequenza snapshot coerenti con l'app**specificare la frequenza, da 1 a 12 ore, per la creazione di punti di ripristino contenenti snapshot coerenti con l'applicazione. Hyper-V usa due tipi di snapshot, uno snapshot standard che fornisce uno snapshot incrementale dell'intera macchina virtuale di hello e uno snapshot coerente dell'applicazione che accetta uno snapshot del punto nel tempo dei dati dell'applicazione hello macchina virtuale hello. Snapshot coerenti dell'applicazione usare tooensure del servizio Copia Shadow del Volume (VSS) che le applicazioni sono in uno stato coerente durante hello snapshot. Si noti che se si abilita snapshot coerenti dell'applicazione, influisce negativamente sulle prestazioni di hello delle applicazioni in esecuzione in macchine virtuali di origine. Verificare che il valore di hello impostato è minore hello numero di punti di ripristino aggiuntivi configurati.
6. In **ora inizio replica iniziale**, indicare quando toostart hello la replica iniziale. la replica di Hello viene eseguita tramite la larghezza di banda internet pertanto è opportuno tooschedule è di fuori dell'orario di disponibilità.
7. In **crittografare i dati archiviati in Azure**, specificare se tooencrypt dati rest nell'archiviazione di Azure. Fare quindi clic su **OK**.

    ![Criteri di replica](./media/site-recovery-vmm-to-azure/gs-replication2.png)
8. Quando si crea un nuovo criterio automaticamente associato hello cloud VMM. Fare clic su **OK**. È possibile associare altri cloud VMM (e hello macchine virtuali in essi contenuti) con questo criterio di replica in **replica** > Nome criterio > **associare Cloud VMM**.

    ![Criteri di replica](./media/site-recovery-vmm-to-azure/policy-associate.png)

## <a name="capacity-planning"></a>Pianificazione della capacità

Dopo avere configurato l'infrastruttura di base, passare alla pianificazione della capacità e valutare se sono necessarie altre risorse.

Il ripristino del sito fornisce un toohelp di pianificazione della capacità allocare risorse hello per l'ambiente di origine, i componenti di Site Recovery, rete e archiviazione. È possibile eseguire la pianificazione hello in modalità rapida per le stime in base a un numero medio di macchine virtuali, dischi e archiviazione, o in modalità dettagliata in cui si input figure a livello di carico di lavoro hello. Prima di iniziare:

* Raccogliere informazioni sull'ambiente di replica, incluse le macchine virtuali, i dischi per ogni macchina virtuale e le risorse di archiviazione per ogni disco.
* Frequenza di modifica (varianza) di stima hello giornaliera è necessario per i dati replicati. È possibile utilizzare hello [Capacity planner for Hyper-V Replica](https://www.microsoft.com/download/details.aspx?id=39057) toohelp si esegue questa operazione.

1. Fare clic su **scaricare**, toodownload hello strumento e quindi eseguirlo. [Leggere l'articolo hello](site-recovery-capacity-planner.md) che accompagna strumento hello.
2. Al termine, selezionare **Sì** in **è stato eseguito hello Capacity Planner**?

   ![Pianificazione della capacità](./media/site-recovery-vmm-to-azure/gs-capacity-planning.png)

   Ulteriori informazioni sul [controllo della larghezza di banda di rete](#network-bandwidth-considerations)




## <a name="enable-replication"></a>Abilitare la replica

Prima di iniziare, assicurarsi che l'account utente di Azure è necessario hello [autorizzazioni](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replica di un nuovo tooAzure macchina virtuale.

Per abilitare la replica, procedere come descritto di seguito.

1. Fare clic su **Passaggio 2: Eseguire la replica dell'applicazione** > **Origine**. Dopo aver abilitato la replica per hello prima volta, fare clic su **+ replicare** nella replica di tooenable hello insieme di credenziali per le macchine aggiuntive.

    ![Abilitare la replica](./media/site-recovery-vmm-to-azure/enable-replication1.png)
2. In hello **origine** blade, server VMM selezionare hello e hello cloud in cui hello Hyper-V si trovano gli host. Fare quindi clic su **OK**.

    ![Abilitare la replica](./media/site-recovery-vmm-to-azure/enable-replication-source.png)
3. In **destinazione**, selezionare la sottoscrizione di hello, modello di distribuzione dopo il failover, e hello account di archiviazione in uso per i dati replicati.

    ![Abilitare la replica](./media/site-recovery-vmm-to-azure/enable-replication-target.png)
4. Selezionare l'account di archiviazione hello da toouse. Se si desidera toouse un account di archiviazione diverso rispetto a quelle si dispone, è possibile [crearlo](#set-up-an-azure-storage-account). Se si utilizza un account di archiviazione premium per i dati replicati, è necessario tooselect un ulteriore spazio di archiviazione standard account toostore i log di replica che consentono di acquisire le modifiche locali tooon data.toocreate un account di archiviazione utilizzando il modello di gestione risorse hello Fare clic su **Crea nuovo**. Se si desidera che un account di archiviazione utilizzando il modello classico hello toocreate, [nel portale di Azure hello](../storage/common/storage-create-storage-account.md). Fare quindi clic su **OK**.
5. Si connetterà hello seleziona Azure toowhich rete e subnet macchine virtuali di Azure, quando vengono creati dopo il failover. Selezionare **Configura ora per macchine virtuali selezionate**, tooapply hello rete impostazione tooall macchine selezionate per la protezione. Selezionare **configurare successivamente**, tooselect hello Azure rete al computer. Se si desidera toouse una rete diversa da quelle si dispone, è possibile [crearlo](#set-up-an-azure-network). Fare clic su modello di gestione risorse di hello toocreate una rete usando **Crea nuovo**. Se si desidera toocreate una rete usando il modello classico di hello, [nel portale di Azure hello](../virtual-network/virtual-networks-create-vnet-classic-pportal.md). Selezionare una subnet, se applicabile. Fare quindi clic su **OK**.
6. In **macchine virtuali** > **selezionare le macchine virtuali**fare clic e selezionare ogni computer in cui si desidera tooreplicate. È possibile selezionare solo i computer per cui è possibile abilitare la replica. Fare quindi clic su **OK**.

    ![Abilitare la replica](./media/site-recovery-vmm-to-azure/enable-replication5.png)

7. In **proprietà** > **configurare proprietà**selezionare hello del sistema operativo per le macchine virtuali selezionata hello e hello disco del sistema operativo.

    - Verificare il nome di macchina virtuale di Azure hello (nome di destinazione) sia conforme ai [requisiti macchina virtuale di Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).   
    - Per impostazione predefinita sono selezionati tutti i dischi di hello di hello VM per la replica, ma è possibile cancellare i dischi tooexclude li.

        - Si consiglia di larghezza di banda replica tooreduce tooexclude dischi. Ad esempio, non è possibile tooreplicate dischi con dati temporanei o dati che sono stato aggiornato un computer o App ogni volta che viene riavviato (ad esempio pagefile.sys o tempdb di Microsoft SQL Server). È possibile escludere il disco di hello dalla replica dal disco hello deselezionando la casella.
        - Solo i dischi di base possono essere esclusi dalla replica. Non è possibile escludere dischi del sistema operativo
        - e non è consigliabile escludere dischi dinamici. Site Recovery non può determinare se un disco rigido virtuale all'interno della macchina virtuale guest è di base o dinamico. Se non sono esclusi tutti i dischi dei volumi dinamici dipendenti, disco dinamico protetto hello verrà visualizzata come un disco guasto quando hello VM viene eseguito il failover e hello dati presenti sul disco non saranno accessibili.
        - Dopo aver abilitato la replica, non è più possibile aggiungere o rimuovere dischi da replicare. Se si desidera tooadd o esclude un disco, necessitano di protezione toodisable per hello macchina virtuale e riabilitarla.
        - Per i dischi creati manualmente in Azure non viene eseguito il failback. Ad esempio, se si esito negativo su tre dischi e creare due direttamente nella macchina virtuale di Azure, solo hello tre dischi che sono stati eseguiti il failover non verranno eseguiti nuovamente da Azure tooHyper-V. È possibile includere i dischi creati manualmente il failback oppure la replica inversa da tooAzure Hyper-V.
        - Se si esclude un disco è sufficiente per toooperate un'applicazione, dopo il failover tooAzure occorre toocreate manualmente in Azure, in modo che hello replicati applicazione può essere eseguito. In alternativa, è possibile integrare automazione di Azure in un piano di ripristino disco hello toocreate durante il failover della macchina hello.

    Fare clic su **OK** toosave modifiche. È possibile impostare proprietà aggiuntive in un secondo momento.

    ![Abilitare la replica](./media/site-recovery-vmm-to-azure/enable-replication6-with-exclude-disk.png)

8. In **le impostazioni di replica** > **configurare le impostazioni di replica**, selezionare i criteri di replica hello da tooapply per hello protetto le macchine virtuali. Fare quindi clic su **OK**. È possibile modificare il criterio di replica hello in **criteri di replica** > Nome criterio > **Modifica impostazioni**. Le modifiche applicate vengono usate per i computer di cui è già in corso la replica e per i nuovi computer.

   ![Abilitare la replica](./media/site-recovery-vmm-to-azure/enable-replication7.png)

È possibile monitorare lo stato di avanzamento di hello **Abilita protezione** processo **processi** > **i processi di ripristino del sito**. Dopo aver hello **finalizzazione della protezione** processo viene eseguito, hello macchina è pronta per il failover.

### <a name="view-and-manage-vm-properties"></a>Visualizzare e gestire le proprietà della macchina virtuale

È consigliabile verificare le proprietà di hello hello computer di origine. Tenere presente il nome della macchina virtuale di Azure hello deve essere conformi ai [requisiti macchina virtuale di Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

1. In **elementi protetti**, fare clic su **elementi replicati**, e selezionare hello toosee computer i dettagli.

    ![Abilitare la replica](./media/site-recovery-vmm-to-azure/vm-essentials.png)
2. In **proprietà**, è possibile visualizzare la replica e le informazioni di failover per hello macchina virtuale.

    ![Abilitare la replica](./media/site-recovery-vmm-to-azure/test-failover2.png)
3. In **di calcolo e rete** > **calcolo proprietà**, è possibile specificare dimensioni delle macchine Virtuali di Azure hello nome e di destinazione. Modificare hello Nome toocomply con [requisiti Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) se è necessario. È inoltre possibile visualizzare e modificare le informazioni relative alla rete di destinazione hello, subnet e indirizzi IP hello assegnato toohello macchina virtuale di Azure.
Si noti che:

   * È possibile impostare l'indirizzo IP di destinazione hello. Se non si fornisce un indirizzo, hello failover macchina utilizzerà DHCP. Se si imposta un indirizzo che non è disponibile in caso di failover, hello failover avrà esito negativo. Hello stesso indirizzo IP di destinazione è utilizzabile per il test failover se è disponibile in rete di failover di test hello hello indirizzo.
   * numero di Hello di schede di rete dipende dalla dimensione hello specificata per la macchina virtuale di destinazione hello, come indicato di seguito:

     * Se il numero di hello di schede di rete nel computer di origine hello è minore o uguale toohello numero di schede consentite per le dimensioni del computer di destinazione hello, quindi sarà necessario destinazione hello hello origine hello stesso numero di schede.
     * Se il numero di hello di schede per la macchina virtuale di origine hello supera hello numero consentito per le dimensioni di destinazione hello, quindi massimo di dimensioni di destinazione hello viene utilizzato.
     * Se, ad esempio un computer di origine ha due schede di rete e le dimensioni del computer di destinazione hello supporta quattro, il computer di destinazione hello avrà due schede. Se il computer di origine di hello ha due schede di ma hello dimensioni di destinazione supportata supportano solo uno, nel computer di destinazione hello avrà una sola scheda.     
     * Se hello macchina virtuale dispone di più schede di rete, verranno tutti connettono toohello stessa rete.

     ![Abilitare la replica](./media/site-recovery-vmm-to-azure/test-failover4.png)

4. In **dischi** su hello VM che verranno replicati, è possibile visualizzare hello del sistema operativo e i dischi dati.

#### <a name="managed-disks"></a>Dischi gestiti

In **di calcolo e rete** > **calcolo proprietà**, è possibile impostare "Utilizzo dischi gestiti" impostazione troppo "Sì" per hello VM se si desidera tooattach dischi gestiti tooyour macchina in tooAzure di migrazione. Dischi gestiti semplifica la gestione disco per le macchine virtuali IaaS di Azure per la gestione degli account di archiviazione hello associati hello dischi di macchina virtuale. [Altre informazioni su Managed Disks](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview).

   - I dischi gestiti sono macchina virtuale creata e associata toohello solo su tooAzure un failover. Per abilitare la protezione, i dati da computer locali continueranno tooreplicate toostorage account.
   Dischi gestiti possono essere creati solo per macchine virtuali distribuite mediante il modello di distribuzione Gestione risorse di hello.  

  > [!NOTE]
  > Il failback da un ambiente Hyper-V locale tooon Azure non è attualmente supportato per i computer con dischi gestiti. Impostare "Utilizzo dischi gestiti" troppo 'Yes' solo se si intende toomigrate questa macchina in Azure.

   - Quando si imposta "Utilizzo dischi gestiti" troppo "Yes", solo set di disponibilità nel gruppo di risorse hello con set di "Utilizzo dischi gestiti" troppo "Yes" saranno disponibili per la selezione. In questo modo le macchine virtuali con dischi gestiti può essere solo parte del set di disponibilità con il set di proprietà "Utilizzare gestito dischi" troppo "Yes". Assicurarsi di creare set di disponibilità con il set di proprietà "Dischi utilizzare gestito" in base a dischi toouse preventivo gestiti in caso di failover.  Analogamente, quando si imposta "Utilizzo dischi gestiti" troppo "No", solo i set di disponibilità nel gruppo di risorse hello con proprietà "Utilizzo dischi gestiti" impostare troppo "No" saranno disponibili per la selezione. [Altre informazioni sui dischi gestiti e i set di disponibilità](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set).

  > [!NOTE]
  > Se l'account di archiviazione hello usato per la replica è stata crittografata con la crittografia del servizio di archiviazione in qualsiasi punto nel tempo, creazione di dischi gestiti durante il failover avrà esito negativo. È possibile impostare "Utilizzo dischi gestiti" troppo "No" e quindi ripetere il failover o disabilitare la protezione per la macchina virtuale hello e proteggerlo tooa account di archiviazione che non è abilitata in qualsiasi punto nel tempo la crittografia del servizio di archiviazione.
  > [Altre informazioni su Crittografia del servizio di archiviazione e dischi gestiti](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).


## <a name="test-hello-deployment"></a>Distribuzione di prova hello

distribuzione di hello tootest è possibile eseguire un failover di test per una singola macchina virtuale o un piano di ripristino che contiene uno o più macchine virtuali.

### <a name="before-you-start"></a>Prima di iniziare

 - Se si desidera tooconnect tooAzure macchine virtuali tramite RDP dopo il failover, vedere [preparazione tooconnect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover).
 - test toofully toocopy di Active Directory e DNS è necessario nell'ambiente di test. [Altre informazioni](site-recovery-active-directory.md#test-failover-considerations)

### <a name="run-a-test-failover"></a>Eseguire un failover di test

1. toofail su una singola macchina virtuale, in **elementi replicati**, fare clic su hello VM > **+ Test Failover**.
2. toofail sul ripristino di un piano, in **piani di ripristino**, piano hello rapida > **Failover di Test**. un piano di ripristino, toocreate [seguire queste istruzioni](site-recovery-create-recovery-plans.md).
3. In **Failover di Test**selezionare hello Azure rete toowhich macchine virtuali di Azure connettersi dopo il failover si verifica.
4. Fare clic su **OK** toobegin hello failover. È possibile monitorare i progressi facendo clic su hello VM tooopen le relative proprietà o in hello **Failover di Test** processo **i processi di ripristino del sito**.
5. Al termine del processo di failover di hello, inoltre deve essere in grado di replica hello toosee macchina di Azure vengono visualizzati nel portale di Azure hello > **macchine virtuali**. È necessario verificare che tale hello VM sia dimensioni appropriate hello, che è connesso toohello di rete e sia in esecuzione.
6. Se sono preparati per le connessioni dopo il failover, dovrebbe essere in grado di tooconnect toohello macchina virtuale di Azure.
7. Al termine, fare clic su **il failover di test di pulizia** nel piano di ripristino hello. In **note** registrare e salvare eventuali commenti associati hello test failover. Questa operazione eliminerà hello le macchine virtuali che sono state create durante il failover di test.

Per altre informazioni, leggere hello [Test failover tooAzure](site-recovery-test-failover-to-azure.md) articolo.

## <a name="monitor-hello-deployment"></a>Monitoraggio hello distribuzione

Ecco come è possibile monitorare le impostazioni di configurazione, stato e stato di integrità per hello distribuzione di Site Recovery:

1. Fare clic su hello tooaccess nome insieme di credenziali di hello **Essentials** dashboard. In questo dashboard è possibile visualizzare i processi di Site Recovery, lo stato della replica, i piani di ripristino, l'integrità del server e gli eventi.  È possibile personalizzare **Essentials** tooshow hello riquadri e layout di tooyou più utili, incluso lo stato di hello degli altri insiemi di credenziali di Backup e ripristino del sito.

    ![Informazioni di base](./media/site-recovery-vmm-to-azure/essentials.png)
2. In **integrità**, è possibile monitorare i problemi nei server locali (server VMM o la configurazione) e hello gli eventi generati da Site Recovery hello ultime 24 ore.
3. In hello **elementi replicati**, **piani di ripristino**, e **i processi di ripristino del sito** riquadri, è possibile gestire e monitorare la replica. Per eseguire il drill-down dei processi, accedere a **Processi** > **Processi di Site Recovery**.

## <a name="command-line-installation-for-hello-azure-site-recovery-provider"></a>Installazione della riga di comando per hello Provider di Azure Site Recovery

Hello Provider di Azure Site Recovery può essere installato da hello della riga di comando. Questo metodo può essere utilizzato tooinstall hello Provider in Server Core per Windows Server 2012 R2.

1. Scaricare hello Provider e registrazione tooa chiave cartella di installazione. ad esempio C:\ASR.
2. Da un prompt dei comandi con privilegi elevati, eseguire il programma di installazione del Provider questi comandi tooextract hello:

            C:\Windows\System32> CD C:\ASR
            C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
3. Eseguire questo comando tooinstall componenti hello:

            C:\ASR> setupdr.exe /i
4. Quindi, eseguire questi comandi, il server hello tooregister nell'insieme di credenziali hello:

        CD C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin
        C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file> /EncryptionEnabled <full file name toosave hello encryption certificate>       

Dove:

* **/ Credenziali**: parametro obbligatorio che specifica in cui si trova file della chiave registrazione hello.  
* **/ FriendlyName**: parametro obbligatorio per il nome del server host Hyper-V hello visualizzata nel portale di Azure Site Recovery hello hello.
* * **/ EncryptionEnabled**: parametro facoltativo quando si esegue la replica di macchine virtuali Hyper-V in VMM cloud tooAzure. Specificare se si desidera tooencrypt le macchine virtuali in Azure (alla crittografia rest). Verificare che hello è il nome del file hello un **PFX** estensione. La crittografia è disabilitata per impostazione predefinita.

    > [!NOTE]
    > Si consiglia di funzionalità di crittografia hello toouse fornita da Azure per la crittografia dei dati inattivi, anziché utilizzare l'opzione di crittografia hello (opzione EncryptionEnabled), fornito da Azure Site Recovery. funzionalità di crittografia Hello fornita da Azure può essere attivata per un account di archiviazione e consente di ottenere prestazioni migliori, ad esempio la crittografia o decrittografia hello tramita Azure  
    > di Azure.
    > [Altre informazioni sulla crittografia del servizio di archiviazione in Azure](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption).
    
* **/ProxyAddress**: parametro facoltativo che specifica l'indirizzo di hello del server proxy hello.
* **/ProxyPort**: parametro facoltativo che specifica la porta del server proxy hello hello.
* **/proxyUsername**: parametro facoltativo che specifica il nome utente di hello proxy (se proxy richiede l'autenticazione).
* **/proxyPassword**: parametro facoltativo che specifica hello password tooauthenticate con il server proxy (se il proxy di hello richiede l'autenticazione).


### <a name="network-bandwidth-considerations"></a>Considerazioni sulla larghezza di banda di rete
È possibile utilizzare hello capacità planner strumento toocalculate hello della larghezza di banda che è necessario per la replica (la replica iniziale e quindi delta). quantità di hello toocontrol di utilizzo della larghezza di banda per la replica, si dispone di alcune opzioni:

* **Limitazione della larghezza di banda**: Hyper-V che esegue la replica del sito secondario tooa del traffico tramite uno specifico host Hyper-V. È possibile limitare la larghezza di banda nel server host hello.
* **Modificare la larghezza di banda**: È possibile influenzare la larghezza di banda hello utilizzata per la replica con un paio di chiavi del Registro di sistema.

#### <a name="throttle-bandwidth"></a>Limitare la larghezza di banda
1. Aprire hello MMC di Backup di Microsoft Azure snap-nel server host Hyper-V di hello. Per impostazione predefinita, un collegamento per il Backup di Microsoft Azure è disponibile sul desktop hello o in C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.
2. Hello nello snap-in, fare clic su **Modifica proprietà**.
3. In hello **limitazione** , selezionare **abilitare la limitazione per le operazioni di backup all'utilizzo della larghezza di banda di internet**e impostare i limiti di hello per lavoro e non lavorative ore. Valori validi sono compresi 512 Mbps di too102 Kbps al secondo.

    ![Limitare la larghezza di banda](./media/site-recovery-vmm-to-azure/throttle2.png)

È inoltre possibile utilizzare hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) tooset limitazione delle richieste di cmdlet. Di seguito è riportato un esempio:

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

**Set-OBMachineSetting -NoThrottle** indica che non è necessaria alcuna limitazione.

#### <a name="influence-network-bandwidth"></a>Influire sulla larghezza di banda di rete
Hello **UploadThreadsPerVM** i controlli di valore del Registro di sistema hello numero di thread utilizzati per il trasferimento di dati (la replica iniziale o delta) di un disco. Un valore maggiore aumenta hello larghezza di banda utilizzata per la replica. Hello **DownloadThreadsPerVM** il valore del Registro di sistema specifica il numero di hello di thread utilizzati per il trasferimento dei dati durante il failback.

1. Nel Registro di sistema hello passare troppo**Backup\Replication Azure HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows**.

   * Modificare il valore di hello **UploadThreadsPerVM** (o se non esiste, creare una chiave hello) toocontrol thread utilizzati per la replica su disco.
   * Modificare il valore di hello **DownloadThreadsPerVM** (o se non esiste, creare una chiave hello) toocontrol thread usato per il traffico di failback da Azure.
2. valore predefinito di Hello è 4. In una rete di "provisioning eccessivo", queste chiavi del Registro di sistema devono essere modificate dai valori predefiniti di hello. Hello massimo è 32. Monitorare il traffico toooptimize hello valore.

## <a name="next-steps"></a>Passaggi successivi

Dopo il completamento della replica iniziale e il test di distribuzione di hello, è possibile richiamare i failover come hello necessità. [Altre informazioni](site-recovery-failover.md) sui diversi tipi di failover e modalità toorun li.
