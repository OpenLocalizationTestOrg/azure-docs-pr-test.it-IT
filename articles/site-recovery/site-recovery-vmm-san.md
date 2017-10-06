---
title: aaaReplicate macchine virtuali Hyper-V in VMM con SAN usando Azure Site Recovery | Documenti Microsoft
description: Questo articolo viene descritto come macchine virtuali Hyper-V tooreplicate tra due siti con Azure Site Recovery con replica SAN.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: eb480459-04d0-4c57-96c6-9b0829e96d65
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: cee4ff519a8e9e7f29e17e923a9533fb339634b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-vms-in-vmm-clouds-tooa-secondary-site-with-azure-site-recovery-by-using-san"></a>Replicare macchine virtuali Hyper-V nel sito secondario tooa cloud VMM con Azure Site Recovery con SAN


Usare questo articolo, se si desidera toodeploy [Azure Site Recovery](site-recovery-overview.md) toomanage replica di macchine virtuali Hyper-V (gestite nei cloud di System Center Virtual Machine Manager) tooa VMM sito secondario, usando Azure Site Recovery nel portale classico hello. Questo scenario non è disponibile nel nuovo portale di Azure hello.



Inviare eventuali commenti alla fine di hello di questo articolo. Ottenere le risposte alle domande tootechnical in hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="why-replicate-with-san-and-site-recovery"></a>Vantaggi della replica con SAN e Site Recovery

* SAN fornisce una soluzione di replica a livello aziendale, scalabile, in modo che un sito primario contenente Hyper-V con SAN possono essere replicati LUN tooa del sito secondario con SAN. L'archiviazione viene gestita da VMM e la replica e il failover vengono orchestrati con Site Recovery.
* Il ripristino del sito ha collaborato con molti [partner di archiviazione SAN](http://social.technet.microsoft.com/wiki/contents/articles/28317.deploying-azure-site-recovery-with-vmm-and-san-supported-storage-arrays.aspx) replica tooprovide tra archiviazione Fibre Channel e iSCSI.  
* Usare le app esistenti di SAN infrastruttura tooprotect cruciali distribuite nei cluster Hyper-V. Le macchine virtuali possono essere replicate come gruppo, in modo da consentire il failover coerente delle app di livello N.
* La replica SAN garantisce la replica coerente tra i diversi livelli di un'applicazione grazie a una replica sincronizzata con valori RTO e RPO bassi e una replica non sincronizzata per elevata flessibilità, in base alle caratteristiche dell'array di archiviazione.  
* È possibile gestire l'archiviazione SAN in hello infrastruttura VMM e utilizzare SMI-S nel servizio di archiviazione esistente toodiscover VMM.  

Si noti che:
- La replica da sito a sito con SAN non è disponibile nel portale di Azure hello. È disponibile solo nel portale classico hello. Impossibile creare nuovi insiemi di credenziali nel portale classico hello. Gli insiemi di credenziali esistenti possono essere mantenuti.
- Non è supportata la replica da tooAzure SAN.
- Non è possibile replicare Vhdx condivisi, o unità logica (LUN) che sono direttamente connessi tooVMs tramite iSCSI o Fibre Channel. I cluster guest possono essere replicati.


## <a name="architecture"></a>Architettura

![Architettura SAN](./media/site-recovery-vmm-san/architecture.png)

- **Azure**: configurare un insieme di credenziali di Site Recovery nel portale di Azure hello.
- **Archiviazione SAN**: hello infrastruttura VMM la gestione archiviazione SAN. Aggiungere il provider di archiviazione di hello, creare classificazioni di archiviazione e impostare i pool di archiviazione.
- **VMM e Hyper-V**: è consigliabile un server VMM in ogni sito. Configurare cloud privati VMM e inserire cluster Hyper-V in tali cloud. Durante la distribuzione, hello Provider di Azure Site Recovery è installato in ogni server VMM e server hello è registrato nell'insieme di credenziali hello. Hello Provider comunica con la replica di toomanage hello il ripristino del sito del servizio, il failover e failback.
- **Replica**: dopo aver impostare l'archiviazione in VMM e configurare la replica in Site Recovery, la replica viene eseguita tra hello primario e secondario sistema di archiviazione SAN. TooSite ripristino viene inviato alcun dato di replica.
- **Failover**: abilitare il failover nel portale di Site Recovery hello. Non si verifica alcuna perdita di dati durante il failover perché la replica è sincrona.
- **Il failback**: toofail back, attivare le modifiche delta dei tootransfer replica inversa da hello secondario toohello sito primario. Una volta completata la replica inversa, si esegue un failover pianificato dal tooprimary secondario. Il failover pianificato arresta replica hello macchine virtuali nel sito secondario hello e li Avvia nel sito primario di hello.


## <a name="before-you-start"></a>Prima di iniziare


**Prerequisiti** | **Dettagli**
--- | ---
**Azzurro** |È necessario un account [Microsoft Azure](https://azure.microsoft.com/) . È possibile iniziare con una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/). [Altre informazioni](https://azure.microsoft.com/pricing/details/site-recovery/) sui prezzi di Site Recovery. Creare un tooconfigure insieme di credenziali di Azure Site Recovery e gestire la replica e failover.
**VMM** | È possibile utilizzare un singolo server VMM e la replica tra aree diverse, ma è consigliabile uno VMM nel sito primario di hello e uno nel sito secondario hello. Un server VMM può essere distribuito come server autonomo fisico o virtuale oppure come cluster. <br/><br/>server VMM Hello deve essere in esecuzione System Center 2012 R2 o versioni successive con aggiornamenti cumulativi più recenti di hello.<br/><br/> È necessario almeno un cloud configurato nel server VMM primario hello desiderato tooprotect e un cloud configurato nel server VMM secondario hello toouse si desidera per il failover.<br/><br/> cloud di origine Hello deve contenere uno o più gruppi host VMM.<br/><br/> Tutti i cloud VMM è necessario impostare il profilo di capacità Hyper-V hello.<br/><br/> Per altre informazioni sulla configurazione di cloud VMM, vedere [Distribuire un cloud privato in VMM](https://technet.microsoft.com/en-us/system-center-docs/vmm/scenario/cloud-overview).
**Hyper-V** | Sono necessari uno o più cluster Hyper-V nei cloud VMM primario e secondario.<br/><br/> cluster Hyper-V di origine Hello deve contenere uno o più macchine virtuali.<br/><br/> gruppi di host VMM Hello in siti primari e secondari hello devono contenere almeno un cluster Hyper-V hello.<br/><br/>server di Hyper-V Hello host e di destinazione deve essere in esecuzione Windows Server 2012 o versione successiva con gli aggiornamenti più recenti di ruolo e hello hello Hyper-V installato.<br/><br/> Se si esegue Hyper-V in un cluster e si usa un cluster basato su indirizzi IP statici, il broker del cluster non viene creato automaticamente, ma è necessario configurarlo manualmente. Per altre informazioni, vedere [Preparing host clusters for Hyper-V replica](https://www.petri.com/use-hyper-v-replica-broker-prepare-host-clusters) (Preparazione di cluster host per la replica Hyper-V).
**Archiviazione SAN** | È possibile replicare macchine virtuali in cluster guest con l'archiviazione iSCSI o Fibre Channel o usando dischi rigidi virtuali condivisi (vhdx).<br/><br/> È necessario due array SAN: uno nel sito primario di hello e il sito secondario hello in uno.<br/><br/> Un'infrastruttura di rete deve essere configurata tra matrici di hello. Devono essere configurati processi di peering e di replica. Le licenze di replica devono essere configurate in base alle esigenze di array di archiviazione hello.<br/><br/>Configurazione di rete tra i server host Hyper-V hello e array di archiviazione hello in modo che gli host possano comunicare con i LUN di archiviazione tramite iSCSI o Fibre Channel.<br/><br/> Vedere il post di blog sugli [array di archiviazione supportati](http://social.technet.microsoft.com/wiki/contents/articles/28317.deploying-azure-site-recovery-with-vmm-and-san-supported-storage-arrays.aspx).<br/><br/> Deve essere installato il provider SMI-S produttori di array di archiviazione e array SAN hello devono essere gestite dal provider di hello. Impostare il secondo toomanufacturer istruzioni di hello Provider.<br/><br/>Assicurarsi che i provider SMI-S della matrice hello è in un server che hello VMM può accedere tramite rete hello con un indirizzo IP o nome di dominio completo.<br/><br/> Ogni array SAN deve avere uno o più pool di archiviazione disponibili.<br/><br/> server VMM primario Hello deve gestire l'array primario hello e server VMM secondario hello deve gestire l'array secondario hello.
**Mapping di rete** | Impostare il mapping di rete in modo che le macchine virtuali replicate vengono posizionate in server host di Hyper-V secondario dopo il failover e in modo che siano le reti VM tooappropriate connesso. Se non si configura il mapping di rete, le macchine virtuali di replica sarà connessa tooany rete dopo il failover.<br/><br/> È necessario verificare che le reti VMM siano configurate correttamente, in modo che sia possibile configurare il mapping di rete durante la distribuzione di Site Recovery. In VMM, hello macchine virtuali nell'host Hyper-V di origine hello deve essere connesso tooa rete VM di VMM. La rete deve essere collegato tooa la rete logica associata al cloud hello.<br/><br/> cloud di destinazione Hello deve avere una rete VM corrispondente e deve essere a sua volta collegato tooa rete logica corrispondente associata al cloud di destinazione hello.<br/><br/>.

## <a name="step-1-prepare-hello-vmm-infrastructure"></a>Passaggio 1: Preparare l'infrastruttura VMM hello
tooprepare l'infrastruttura VMM, è necessario:

1. Verificare i cloud VMM.
2. Integrare e classificare l'archiviazione SAN in VMM.
3. Creare unità logiche e allocare spazio di archiviazione.
4. Creare gruppi di replica.
5. Configurare reti VM.

### <a name="verify-vmm-clouds"></a>Verificare i cloud VMM

Assicurarsi che i cloud VMM siano configurati correttamente prima di iniziare la distribuzione di Site Recovery.

### <a name="integrate-and-classify-san-storage-in-hello-vmm-fabric"></a>Integrare e classificare l'archiviazione SAN in hello infrastruttura VMM

1. Nella console VMM, hello andare troppo**infrastruttura** > **archiviazione** > **Aggiungi risorse** > **idispositividiarchiviazione**.
2. In hello **aggiungere dispositivi di archiviazione** procedura guidata, selezionare **selezionare un tipo di provider di archiviazione** e selezionare **dispositivi SAN e NAS individuati e gestiti da un provider SMI-S**.

    ![Tipo di provider](./media/site-recovery-vmm-san/provider-type.png)

3. In hello **specifica il protocollo e l'indirizzo del Provider di archiviazione SMI-S hello** selezionare **SMI-S CIMXML** e specificare le impostazioni di hello per connessione toohello provider.
4. In **FQDN o indirizzo IP del Provider** e **porta TCP/IP**, specificare le impostazioni di hello per connessione toohello provider. È possibile usare una connessione SSL solo per SMI-S CIMXML.

    ![Connessione provider](./media/site-recovery-vmm-san/connect-settings.png)
5. In **account RunAs**, specificare un account RunAs VMM che può accedere a provider hello o creare un account.
6. In hello **raccogliere informazioni** pagina, VMM tenta automaticamente di importazione e toodiscover hello archiviazione informazioni sul dispositivo. individuazione tooretry, fare clic su **Provider di analisi**. Se il processo di individuazione hello ha esito positivo, hello individuati gli array di archiviazione, pool di archiviazione, produttore, modello e capacità sono elencati nella pagina di hello.

    ![Individua l'archiviazione](./media/site-recovery-vmm-san/discover.png)
7. In **selezionare tooplace di pool di archiviazione sotto la gestione e assegnare una classificazione**, selezionare i pool di archiviazione hello che VMM verrà gestire e assegnare loro una classificazione. Informazioni di LUN vengono importate dai pool di archiviazione hello. Creare i LUN in base alle applicazioni di hello è necessario tooprotect, dai requisiti di capacità e i requisiti per le operazioni necessarie tooreplicate insieme.

    ![Classifica l’archiviazione](./media/site-recovery-vmm-san/classify.png)

### <a name="create-luns-and-allocate-storage"></a>Creare unità logiche e allocare spazio di archiviazione.

Creare i LUN in base alle applicazioni di hello è necessario tooprotect, i requisiti di capacità e i requisiti per le operazioni necessarie tooreplicate insieme.

1. Dopo l'archiviazione hello viene visualizzato in hello infrastruttura di VMM, è possibile [il provisioning dei LUN](https://technet.microsoft.com/en-us/system-center-docs/vmm/manage/manage-storage-host-groups#create-a-lun-in-vmm).

     > [!NOTE]
     > Non aggiungere dischi rigidi virtuali per macchina virtuale che sono abilitati per la replica tooLUNs hello. Se le unità logiche non si trovano in un gruppo di replica di Site Recovery, non vengono rilevate da quest'ultimo componente.
     >

2. Allocare il cluster host Hyper-V di archiviazione capacità toohello in modo che VMM possa distribuire archiviazione toohello il provisioning dei dati della macchina virtuale:

   * Prima di allocare cluster toohello di archiviazione, è necessario tooallocate il gruppo di host VMM toohello in cui hello risiede cluster. Per ulteriori informazioni, vedere [come tooa unità logiche di archiviazione tooallocate host in VMM gruppo](https://technet.microsoft.com/library/gg610686.aspx) e [come tooa gruppo di host in VMM crea pool di archiviazione tooallocate](https://technet.microsoft.com/library/gg610635.aspx).
   * Allocare cluster toohello capacità di archiviazione, come descritto in [come cluster di archiviazione tooconfigure in un host Hyper-V in VMM](https://technet.microsoft.com/library/gg610692.aspx).

    ![Tipo di provider](./media/site-recovery-vmm-san/provider-type.png)
3. In **specifica il protocollo e l'indirizzo del Provider di archiviazione SMI-S hello**selezionare **SMI-S CIMXML**. Specificare le impostazioni di hello per la connessione toohello provider. È possibile usare una connessione SSL solo per SMI-S CIMXML.

    ![Connessione provider](./media/site-recovery-vmm-san/connect-settings.png)
4. In **account RunAs**, specificare un account RunAs VMM che può accedere a provider hello o creare un account.
5. In **raccogliere informazioni**, VMM tenta automaticamente di importazione e toodiscover hello archiviazione informazioni sul dispositivo. Se è necessario tooretry, fare clic su **Provider di analisi**. Quando il processo di individuazione hello ha esito positivo, gli array di archiviazione, hello capacità, produttore, modello e i pool di archiviazione sono elencati nella pagina hello.

    ![Individua l'archiviazione](./media/site-recovery-vmm-san/discover.png)
7. In **selezionare tooplace di pool di archiviazione sotto la gestione e assegnare una classificazione**, selezionare i pool di archiviazione hello che VMM verrà gestire e assegnare loro una classificazione. Informazioni di LUN vengono importate dai pool di archiviazione hello.

    ![Classifica l’archiviazione](./media/site-recovery-vmm-san/classify.png)


### <a name="create-replication-groups"></a>Creare gruppi di replica

Creare un gruppo di replica che include tutti i LUN di hello che dovranno essere tooreplicate insieme.

1. Nella console VMM, hello aprire hello **gruppi di replica** scheda delle proprietà di matrice di archiviazione hello e quindi fare clic su **New**.
2. Creare il gruppo di replica hello.

    ![Gruppo di replica SAN](./media/site-recovery-vmm-san/rep-group.png)

### <a name="set-up-networks"></a>Configurare le reti

Se si desidera tooconfigure il mapping di rete, hello seguenti:

1. Vedere il mapping della rete di Site Recovery.
2. Preparare le reti VM in VMM:

   * [Configurare le reti logiche](https://technet.microsoft.com/en-us/system-center-docs/vmm/manage/manage-network-logical-networks).
   * [Configurare le reti VM](https://technet.microsoft.com/en-us/system-center-docs/vmm/manage/manage-network-vm-networks).


## <a name="step-2-create-a-vault"></a>Passaggio 2: creare un insieme di credenziali

1. Accedi toohello [portale di Azure](https://portal.azure.com) dal server VMM hello desiderato tooregister nell'insieme di credenziali hello.
2. Espandere **Servizi dati** > **Servizi di ripristino** e quindi **Insieme di credenziali di Site Recovery**.
3. Fare clic su **Creare nuovo** > **Creazione rapida**.
4. In **nome**, immettere un insieme di credenziali di nome descrittivo tooidentify hello.
5. In **area**, selezionare hello area geografica per l'insieme di credenziali hello. aree toocheck supportati, vedere [dettagli prezzi di Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
6. Fare clic su **Create vault**.

    ![New Vault](./media/site-recovery-vmm-san/create-vault.png)

Controllare tooconfirm barra di stato hello che hello insieme di credenziali è stato creato correttamente. insieme di credenziali Hello verrà elencato come **Active** su hello principale **servizi di ripristino** pagina.

### <a name="register-hello-vmm-servers"></a>Registrare i server VMM hello

1. Aprire hello **avvio rapido** pagina hello **servizi di ripristino** pagina. Avvio rapido possibile neanche possibile aprire in qualsiasi momento facendo clic sull'icona di hello.

    ![Quick Start Icon](./media/site-recovery-vmm-san/quick-start-icon.png)
2. Nella casella di riepilogo a discesa hello selezionare **tra Hyper-V locale del sito tramite replica basata su array**.

    ![Chiave di registrazione](./media/site-recovery-vmm-san/select-san.png)
3. In **server VMM preparare**, scaricare hello la versione più recente del file di installazione di Provider di Azure Site Recovery hello.
4. Eseguire questo file nel server VMM di origine hello. Se VMM è distribuito in un cluster e si sta installando hello Provider hello per la prima volta, installare hello Provider in un nodo attivo e di fine server VMM nell'insieme di credenziali hello hello installazione tooregister hello. Installare quindi hello Provider in hello altri nodi. Se si esegue l'aggiornamento di hello Provider, è necessario tooupgrade in tutti i nodi in modo che essi hanno hello stessa versione del Provider.
5. Hello programma consente di verificare i requisiti e le richieste autorizzazioni toostop hello l'installazione del Provider toobegin servizio VMM. servizio Hello verrà riavviato automaticamente al completamento dell'installazione. In un cluster VMM, sarà un ruolo del Cluster hello toostop richiesta.
6. In **Microsoft Update**, è possibile acconsentire esplicitamente agli aggiornamenti e aggiornamenti del Provider verranno installati in base a criteri di Microsoft Update tooyour.

    ![Microsoft Updates](./media/site-recovery-vmm-san/ms-update.png)

7. Per impostazione predefinita, il percorso di installazione hello per hello Provider è <SystemDrive>\Programmi\Microsoft System Center 2012 R2\Virtual Machine Manager\bin. Fare clic su **installare** toobegin.

    ![Percorso di installazione](./media/site-recovery-vmm-san/install-location.png)

8. Dopo aver installato hello Provider, fare clic su **registrare** server VMM di hello tooregister nell'insieme di credenziali hello.

    ![Installazione completata](./media/site-recovery-vmm-san/install-complete.png)

9. In **connessione Internet**, specificare la modalità di connessione Internet toohello hello Provider. Selezionare **utilizza impostazioni proxy del sistema predefinito** se si desidera toouse hello predefinito impostazioni della connessione Internet sul server hello.

    ![Internet Settings](./media/site-recovery-vmm-san/proxy-details.png)

   * Se si desidera toouse un proxy personalizzato, configurarlo prima di installare hello Provider. Quando si configurano le impostazioni del proxy personalizzato, un test viene eseguito connessione proxy di toocheck hello.
   * Se si utilizza un proxy personalizzato, o se il proxy predefinito richiede l'autenticazione, è necessario immettere i dettagli del proxy hello, tra cui la porta e indirizzo hello.
   * Hello necessario il che URL deve essere accessibile dal server VMM hello.
   * Se si utilizza un proxy personalizzato, un account RunAs VMM (DRAProxyAccount) viene creato automaticamente tramite hello specificato le credenziali del proxy. Configurare il server proxy hello in modo che questo account può autenticare. È possibile modificare impostazioni hello Run As account nella console VMM hello (**impostazioni** > **sicurezza** > **account RunAs**  >  **DRAProxyAccount**). È necessario riavviare il servizio VMM hello per effetto di tootake modifica hello.
10. In **chiave di registrazione**selezionare chiave hello scaricati dal server VMM di hello toohello portale e copiato.
11. In **nome insieme di credenziali**, verificare il nome di hello dell'insieme di credenziali hello in cui hello server verrà registrato.

    ![Server registration](./media/site-recovery-vmm-san/vault-creds.png)
12. impostazione di crittografia Hello viene utilizzata solo per la replica tooAzure VMM. È possibile ignorarla.

    ![Server registration](./media/site-recovery-vmm-san/encrypt.png)
13. In **nome Server**, specificare un server di nome descrittivo tooidentify hello VMM nell'insieme di credenziali hello. In una configurazione cluster, specificare il nome del ruolo cluster VMM hello.
14. In **sincronizzazione metadati cloud iniziali**, selezionare se si desidera toosynchronize metadati per tutti i cloud nel server VMM hello. Questa azione deve solo toohappen una volta in ogni server. Se non si desidera toosynchronize tutti i cloud, è possibile lasciare deselezionata questa opzione e sincronizzare ogni cloud singolarmente nelle proprietà del cloud nella console VMM hello hello.

    ![Server registration](./media/site-recovery-vmm-san/friendly-name.png)

15. Fare clic su **Avanti** processo hello toocomplete. Dopo la registrazione, i metadati dal server VMM hello vengono recuperati da Azure Site Recovery. server Hello viene visualizzato nel **server** > **server VMM** nell'insieme di credenziali hello.

### <a name="command-line-installation"></a>Installazione dalla riga di comando

Provider di Azure Site Recovery Hello può anche essere installato utilizzando hello seguente riga di comando. Questo metodo può essere provider hello tooinstall utilizzato in Server Core per Windows Server 2012 R2.

1. Scaricare hello Provider e registrazione tooa chiave cartella di installazione. ad esempio C:\ASR.
2. Arrestare il servizio VMM hello.
3. Estrarre il programma di installazione del Provider hello. Eseguire questi comandi come amministratore:

        C:\Windows\System32> CD C:\ASR
        C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
4. Installare hello Provider:

        C:\ASR> setupdr.exe /i
5. Registrare hello Provider:

        CD C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin
        C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file> /EncryptionEnabled <full file name toosave hello encryption certificate>         

Parametri

* **/ Credenziali**: parametro obbligatorio per il percorso di hello in cui hello Trova file di chiave di registrazione.  
* **/ FriendlyName**: parametro obbligatorio per il nome del server host Hyper-V hello visualizzata nel portale di Azure Site Recovery hello hello.
* **/ EncryptionEnabled**: parametro facoltativo utilizzato solo quando la replica da VMM tooAzure.
* **/ProxyAddress**: parametro facoltativo che specifica l'indirizzo di hello del server proxy hello.
* **/ProxyPort**: parametro facoltativo che specifica la porta del server proxy hello hello.
* **/proxyUsername**: parametro facoltativo che specifica il nome utente di hello proxy (se il proxy di hello richiede l'autenticazione).
* **/proxyPassword**: parametro facoltativo che specifica la password di hello per l'autenticazione con il server proxy hello (se il proxy di hello richiede l'autenticazione).

## <a name="step-3-map-storage-arrays-and-pools"></a>Passaggio 3: Eseguire il mapping di array e pool di archiviazione

Eseguire il mapping di array primario e secondario toospecify quale pool di archiviazione secondario riceve i dati di replica dal pool primario hello. Eseguire il mapping di archiviazione prima di configurare la replica, perché le informazioni di mapping hello viene utilizzate quando si abilita la protezione per i gruppi di replica.

Prima di iniziare, verificare che i cloud VMM siano visualizzati nell'insieme di credenziali hello. Cloud vengono rilevati durante la sincronizzazione di tutti i cloud durante l'installazione del Provider o durante la sincronizzazione di un cloud specifico nella console VMM hello.

1. Fare clic su **Risorse** > **Archiviazione server** > **Mappa array di origine e di destinazione**.
    ![Registrazione del server](./media/site-recovery-vmm-san/storage-map.png)

2. Selezionare gli array di archiviazione hello nel sito primario di hello ed eseguirne il mapping matrici toostorage nel sito secondario hello. In **pool di archiviazione**, selezionare un'origine e destinazione toomap pool di archiviazione.

    ![Server registration](./media/site-recovery-vmm-san/storage-map-pool.png)

## <a name="step-4-configure-replication-settings"></a>Passaggio 4: Configurare le impostazioni di replica

Dopo la registrazione dei server VMM, configurare le impostazioni di protezione del cloud.

1. In hello **avvio rapido** pagina, fare clic su **impostare la protezione per i cloud VMM**.
2. In hello **elementi protetti** selezionare cloud hello **configurazione**.
3. In **Destinazione** selezionare **VMM**.
4. In **percorso di destinazione**, selezionare i server VMM hello che gestisce il cloud hello da toouse per il ripristino.
5. In **cloud di destinazione**, selezionare il cloud di destinazione hello da toouse per failover della macchina virtuale.
   * Si consiglia di selezionare un cloud di destinazione che soddisfa i requisiti di ripristino per proteggere le macchine virtuali hello.
   * Un cloud può appartenere solo coppia singolo cloud tooa - come un database primario o un cloud di destinazione.
6. Site Recovery verifica che i cloud abbiano accesso tooSAN archiviazione e che l'archiviazione hello vengono eseguito il mapping di matrici.
7. Se la verifica ha esito positivo, in **Tipo di replica** selezionare **SAN**.

Dopo aver salvato le impostazioni di hello, viene creato un processo che può essere monitorato nella hello **processi** scheda. Impostazioni possono essere modificate in hello **configura** scheda. Se si desidera percorso di destinazione hello toomodify o cloud di destinazione, è necessario rimuovere la configurazione cloud hello e successivamente, riconfigurare il cloud hello.

## <a name="step-5-enable-network-mapping"></a>Passaggio 5: Abilitare il mapping di rete

1. In hello **avvio rapido** pagina, fare clic su **mapping delle reti**.
2. Selezionare i server VMM di origine hello, quindi hello destinazione VMM toowhich messaggi hello del server verranno eseguito il mapping di reti. viene visualizzato l'elenco di Hello di reti di origine e le relative reti di destinazione associate. Per le reti non mappate viene visualizzato un valore vuoto. Fare clic su hello informazioni icona Avanti toohello origine e destinazione nomi tooview hello subnet della rete per ogni rete.
3. Selezionare una rete in **Rete nell'origine** e quindi fare clic su **Esegui mapping**. servizio di Hello rileva le reti VM hello nel server di destinazione hello e li visualizza.

    ![Architettura SAN](./media/site-recovery-vmm-san/network-map1.png)
4. Selezionare una delle reti VM hello dal server VMM di destinazione hello.

    ![Architettura SAN](./media/site-recovery-vmm-san/network-map2.png)

5. Quando si seleziona una rete di destinazione, hello cloud protetti che usano la rete di origine hello vengono visualizzati. Vengono visualizzate anche le reti di destinazione disponibili. Si consiglia di selezionare una rete di destinazione è disponibile tooall hello aree che si utilizza per la replica.
6. Fare clic su processo di mapping hello toocomplete hello segno di spunta. Viene avviato un processo che tiene traccia dell'avanzamento. È possibile visualizzarlo in hello **processi** scheda.

## <a name="step-6-enable-replication-for-replication-groups"></a>Passaggio 6: Abilitare la replica per i gruppi di replica

Prima di abilitare la protezione per le macchine virtuali, è necessario replica tooenable per gruppi di replica di archiviazione.

1. In hello **proprietà** pagina del cloud primario di hello nel portale di Site Recovery hello, aprire hello **macchine virtuali** scheda e fare clic su **Aggiungi gruppo di replica**.
2. Selezionare uno o più VMM gruppi di replica associati a cloud hello, verificare le matrici di origine e destinazione hello e specificare la frequenza di replica hello.

Il ripristino del sito, VMM e i provider SMI-S hello il provisioning dell'archiviazione del sito di destinazione hello LUN e abilitare la replica di archiviazione. Se il gruppo di replica hello è già stato replicato, il ripristino del sito riutilizza la relazione di replica esistente hello e aggiornamenti hello informazioni.

## <a name="step-7-enable-protection-for-virtual-machines"></a>Passaggio 7: Abilitare la protezione per le macchine virtuali


La replica di un gruppo di archiviazione, abilitare la protezione per le macchine virtuali nella console VMM hello con uno dei seguenti metodi hello:

* **Nuova macchina virtuale**: quando si crea una macchina virtuale, abilitare la replica e associare il gruppo di replica hello hello macchina virtuale.
  Con questa opzione, VMM utilizza l'archiviazione VM hello di posizionamento intelligente toooptimally sul posto su LUN hello hello del gruppo di replica. Site Recovery Orchestra la creazione di hello dell'ombreggiatura VM nel sito secondario hello e alloca capacità in modo che le macchine virtuali di replica possono essere avviate dopo il failover.
* **Macchina virtuale esistente**: se una macchina virtuale è già stata distribuita in VMM, è possibile abilitare la replica e di eseguire un gruppo di replica tooa di migrazione di archiviazione. Dopo il completamento, VMM e il ripristino del sito di rilevamento hello nuova macchina virtuale e iniziano a gestirla in Site Recovery. Un'ombreggiatura in macchina virtuale viene creato nel sito secondario hello e capacità viene allocata in modo che la replica hello VM può essere avviata dopo il failover.

![Abilitare la protezione](./media/site-recovery-vmm-san/enable-protect.png)

Dopo che le macchine virtuali sono abilitate per la replica, vengono visualizzati nella console di Site Recovery hello. È possibile ora visualizzare le proprietà delle macchine virtuali e monitorare lo stato e i gruppi di replica di failover che contengono più macchine virtuali. Nella replica SAN tutte le macchine virtuali associate a un gruppo di replica devono essere sottoposte a failover insieme. In questo modo si verifica il failover a livello di archiviazione hello prima. È importante toogroup la replica di gruppi in modo corretto e collocare insieme solo macchine virtuali associate.

> [!NOTE]
> Dopo avere abilitato la replica per una macchina virtuale, non aggiungere tooLUNs relativi dischi rigidi virtuali, a meno che non si trovano in un gruppo di replica di Site Recovery. I dischi rigidi virtuali vengono rilevati da Site Recovery sono se si trovano in un gruppo di replica relativo.
>
>

È possibile monitorare lo stato di avanzamento, tra cui la replica iniziale hello, su hello **processi** scheda. Quando si esegue il processo di finalizzazione della protezione hello, macchina virtuale hello è pronto per il failover.

![Processo di protezione delle macchine virtuali](./media/site-recovery-vmm-san/job-props.png)

## <a name="step-8-test-hello-deployment"></a>Passaggio 8: Testare la distribuzione di hello

Testare la distribuzione toomake assicurarsi che le macchine virtuali eseguire il failover come previsto. toodo, creare un piano di ripristino ed eseguire un failover di test.

1. In hello **piani di ripristino** scheda, fare clic su **crea piano di ripristino**.
2. Specificare un nome per il piano di ripristino hello e selezionare i server VMM di origine e di destinazione. server di origine Hello deve disporre di macchine virtuali che sono abilitate per il failover e ripristino. Selezionare **SAN** tooview solo cloud configurati per la replica SAN.

    ![Crea piano di ripristino](./media/site-recovery-vmm-san/r-plan.png)

3. In **Seleziona macchine virtuali** selezionare i gruppi di replica. Tutte le macchine virtuali associate al gruppo hello vengono aggiunti toohello piano di ripristino. Queste macchine virtuali vengono aggiunti il gruppo toohello ripristino piano predefinito (gruppo 1). Se necessario, è possibile aggiungere più gruppi. Dopo la replica, le macchine virtuali sono numerate in base a ordine toohello dei gruppi del piano di ripristino hello.

    ![Selezionare le macchine virtuali](./media/site-recovery-vmm-san/r-plan-vm.png)
4. Dopo aver creato il piano di ripristino di hello, viene visualizzato nell'elenco hello hello **piani di ripristino** scheda. Selezionare il piano di hello e scegliere **Failover di Test**.
5. In hello **conferma Failover di Test** selezionare **Nessuno**. Con questa opzione è abilitata, hello eseguito il failover delle macchine virtuali di replica non verrà connesso tooany rete. Ciò consente di verificare che hello macchine virtuali di failover come previsto, ma non il test di ambiente di rete hello. Per altre informazioni su altre opzioni di rete, vedere [Failover in Site Recovery](site-recovery-failover.md).

    ![Seleziona rete di test](./media/site-recovery-vmm-san/test-fail1.png)

6. macchina virtuale di test Hello viene creato in hello stesso host come host hello in quale replica hello esiste macchina virtuale. Non viene aggiunta toohello cloud in cui hello replica macchina virtuale si trova.
2. Dopo la replica, la replica hello macchina virtuale avrà un indirizzo IP diverso da quello di macchina virtuale primaria hello. Se gli indirizzi vengono emessi da un protocollo DHCP, l'aggiornamento viene eseguito automaticamente. Se non si utilizza DHCP e si desidera hello stessi indirizzi, è necessario toorun un paio di script.
3. Eseguire questo indirizzo IP di script tooretrieve hello:

       $vm = Get-SCVirtualMachine -Name <VM_NAME>
       $na = $vm[0].VirtualNetworkAdapters>
       $ip = Get-SCIPAddress -GrantToObjectID $na[0].id
       $ip.address  

4. Eseguire questo tooupdate di script di esempio DNS. Specificare l'indirizzo IP hello recuperato.

       [string]$Zone,
       [string]$name,
       [string]$IP
       )
       $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
       $newrecord = $record.clone()
       $newrecord.RecordData[0].IPv4Address  =  $IP
       Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord


## <a name="next-steps"></a>Passaggi successivi

Dopo aver eseguito un toocheck di failover di test che l'ambiente funzioni come previsto, vedere [failover di Site Recovery](site-recovery-failover.md) toolearn sui diversi tipi di failover.
