---
title: macchine virtuali aaaReplicate Hyper-V in VMM cloud tooAzure | Documenti Microsoft
description: In questo articolo viene descritto come macchine virtuali di Hyper-V tooreplicate negli host Hyper-V situato in tooAzure cloud di System Center VMM.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 9d526a1f-0d8e-46ec-83eb-7ea762271db5
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/23/2017
ms.author: raynew
ms.openlocfilehash: 136f68585534c17b615ecc4e82c0133bf813503f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure"></a>Replica delle macchine virtuali Hyper-V in VMM cloud tooAzure
> [!div class="op_single_selector"]
> * [Portale di Azure](site-recovery-vmm-to-azure.md)
> * [PowerShell - Gestione risorse](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [Portale classico](site-recovery-vmm-to-azure-classic.md)
> * [PowerShell - Classico](site-recovery-deploy-with-powershell.md)
>
>

servizio Azure Site Recovery Hello contribuisce tooyour continuità aziendale e strategia di ripristino di emergenza per la replica di orchestrazione, failover e il ripristino delle macchine virtuali e server fisici. Macchine possono essere replicati tooAzure o tooa locale secondario data center. Per una rapida panoramica, leggere [Che cos'è Azure Site Recovery?](site-recovery-overview.md)

## <a name="overview"></a>Panoramica
In questo articolo viene descritto come toodeploy Site Recovery tooreplicate Hyper-V le macchine virtuali in Hyper-V host server che si trovano in tooAzure di cloud privati VMM.

articolo Hello include i prerequisiti per scenario hello e Mostra come tooset di un insieme di credenziali di Site Recovery, ottenere hello Provider di Azure Site Recovery installato nel server VMM di origine hello, registrare hello server nell'insieme di credenziali hello, aggiungere un account di archiviazione di Azure, installare hello Agente di servizi di ripristino di Azure nei server host Hyper-V, configurare le impostazioni di protezione per i cloud VMM che verranno applicati tooall protetto le macchine virtuali e quindi abilitare la protezione per le macchine virtuali. Completare test toomake failover hello che tutto funzioni come previsto.

Inviare eventuali commenti o domande nella parte inferiore di hello di questo articolo, o di hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="architecture"></a>Architettura
![Architettura](./media/site-recovery-vmm-to-azure-classic/topology.png)

* Hello Provider di Azure Site Recovery è installato nel hello VMM durante la distribuzione di Site Recovery e il server VMM hello è registrato nell'insieme di credenziali Site Recovery hello. Hello Provider comunica con l'orchestrazione di replica toohandle Site Recovery.
* agente di servizi di ripristino di Azure Hello viene installato nei server host Hyper-V durante la distribuzione di Site Recovery. Gestisce l'archiviazione tooAzure replica dei dati.

## <a name="azure-prerequisites"></a>Prerequisiti di Azure
Ecco gli elementi richiesti in Azure.

| **Prerequisito** | **Dettagli** |
| --- | --- |
| **Account di Azure** |È necessario un account [Microsoft Azure](https://azure.microsoft.com/) . È possibile iniziare con una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/). [Altre informazioni](https://azure.microsoft.com/pricing/details/site-recovery/) sui prezzi di Site Recovery. |
| **Archiviazione di Azure** |È necessario un toostore replicati dati dell'account di archiviazione di Azure. I dati replicati vengono memorizzati nell'archiviazione di Azure e le macchine virtuali di Azure vengono attivate quando si verifica il failover. <br/><br/>È necessario un [account di archiviazione con ridondanza geografica Standard](../storage/common/storage-redundancy.md#geo-redundant-storage). Hello account deve essere in hello stessa area geografica del servizio Site Recovery hello e associato hello stessa sottoscrizione. Si noti che gli account di archiviazione toopremium di replica non è attualmente supportato e non devono essere usate.<br/><br/>[Altre informazioni](../storage/common/storage-introduction.md) sul servizio di archiviazione di Azure. |
| **Rete di Azure** |È necessario che una rete virtuale di Azure che si connetteranno macchine virtuali di Azure viene eseguito il failover toowhen. Hello rete virtuale di Azure deve essere in hello stessa area dell'insieme di credenziali di Site Recovery hello. |

## <a name="on-premises-prerequisites"></a>Prerequisiti locali
Ecco gli elementi richiesti in locale.

| **Prerequisito** | **Dettagli** |
| --- | --- |
| **VMM** |È necessario almeno un server VMM distribuito come server fisico o virtuale autonomo o come cluster virtuale. <br/><br/>server VMM Hello deve essere in esecuzione System Center 2012 R2 con aggiornamenti cumulativi più recenti di hello.<br/><br/>È necessario almeno un cloud configurato nel server VMM hello.<br/><br/>cloud di origine Hello che si desidera tooprotect deve contenere uno o più gruppi host VMM.<br/><br/>Per altre informazioni sulla configurazione dei cloud VMM, vedere la [procedura dettagliata per la creazione di cloud privati con System Center 2012 SP1 VMM](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx) nel blog di Keith Mayer. |
| **Hyper-V** |È necessario uno o più server host Hyper-V o cluster in hello cloud VMM. server host Hello deve disporre di uno o più macchine virtuali e. <br/><br/>Hello Hyper-V server deve essere in esecuzione in almeno **Windows Server 2012 R2** con il ruolo Hyper-V hello o **Microsoft Hyper-V Server 2012 R2** e avere hello installati aggiornamenti più recenti.<br/><br/>Qualsiasi server Hyper-V contenente le macchine virtuali desiderate tooprotect deve trovarsi in un cloud VMM.<br/><br/>Se si esegue Hyper-V in un cluster, si noti che il gestore del cluster non viene creato automaticamente se viene usato un cluster basato su indirizzi IP statici. È necessario un gestore cluster hello tooconfigure manualmente. [Altre informazioni](https://www.petri.com/use-hyper-v-replica-broker-prepare-host-clusters) nel post di blog di Aidan Finn. |
| **Computer protetti** | Macchine virtuali che si desidera tooprotect devono essere conformi a [requisiti Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements). |

## <a name="network-mapping-prerequisites"></a>Prerequisiti di mapping di rete
Quando si proteggono macchine virtuali nella rete di Azure viene eseguito il mapping tra le reti VM nel server VMM di origine hello e seguente hello tooenable di reti di Azure di destinazione:

* Tutti i computer che il failover su hello stesso può connettersi tooeach altri, indipendentemente dal piano di ripristino si trovano in rete.
* Se nella rete Azure di destinazione hello è stato configurato un gateway di rete, le macchine virtuali possono connettersi le macchine virtuali locali tooother.
* Se non si configura rete mapping solo le macchine virtuali che il failover hello stesso piano di ripristino saranno in grado di tooconnect tooeach altri dopo tooAzure di failover.

Se si desidera che il mapping di rete toodeploy, occorre seguente hello:

* Hello le macchine virtuali da tooprotect nel server VMM di origine hello deve essere una rete VM tooa connesso. La rete deve essere collegato tooa la rete logica associata al cloud hello.
* Le macchine virtuali toowhich replicata una rete di Azure possono connettersi dopo il failover. Selezionare la rete in fase di hello di failover. rete Hello devono trovarsi in hello stessa area la sottoscrizione di Azure Site Recovery.


Preparare le reti in VMM:

   * [Configurare le reti logiche](https://technet.microsoft.com/library/jj721568.aspx).
   * [Configurare le reti VM](https://technet.microsoft.com/library/jj721575.aspx).


## <a name="step-1-create-a-site-recovery-vault"></a>Passaggio 1: creare un insieme di credenziali di Ripristino sito
1. Accedi toohello [portale di gestione](https://portal.azure.com) dal server VMM hello desiderato tooregister.
2. Espandere **Servizi dati**  > **Servizi di ripristino**  > **Insieme di credenziali di Site Recovery**.
3. Fare clic su **Creare nuovo** > **Creazione rapida**.
4. In **nome**, immettere un insieme di credenziali di nome descrittivo tooidentify hello.
5. In **area**, selezionare hello area geografica per l'insieme di credenziali hello. aree toocheck supportato vedere aree geografiche disponibili in [dettagli prezzi di Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
6. Fare clic su **Create vault**.

    ![New Vault](./media/site-recovery-vmm-to-azure-classic/create-vault.png)

Controllare tooconfirm barra di stato hello che hello insieme di credenziali è stato creato correttamente. insieme di credenziali Hello verrà elencato come **Active** nella pagina principale di servizi di ripristino hello.

## <a name="step-2-generate-a-vault-registration-key"></a>Passaggio 2: generare una chiave di registrazione dell'insieme di credenziali
Generare una chiave di registrazione nell'insieme di credenziali hello. Dopo aver scaricato hello Provider di Azure Site Recovery e installarlo nel server VMM hello, si utilizzerà il server VMM di hello tooregister chiave nell'insieme di credenziali hello.

1. In hello **servizi di ripristino** pagina, fare clic su pagina di avvio rapido di hello insieme di credenziali tooopen hello. Guida introduttiva può anche essere aperto in qualsiasi momento facendo clic sull'icona hello.

    ![Quick Start Icon](./media/site-recovery-vmm-to-azure-classic/qs-icon.png)
2. Nell'elenco a discesa hello, selezionare **tra un sito VMM locale e Microsoft Azure**.
3. In **Preparare i server VMM** fare clic sul file **Generate registration key**. file di chiave Hello viene generato automaticamente ed è valido per 5 giorni dopo la sua creazione. Se si accede non di hello portale di Azure da un server VMM hello, occorre toocopy toohello file server.

    ![Chiave di registrazione](./media/site-recovery-vmm-to-azure-classic/register-key.png)

## <a name="step-3-install-hello-azure-site-recovery-provider"></a>Passaggio 3: Installare il Provider di Azure Site Recovery hello
1. In **avvio rapido** > **server VMM preparare**, fare clic su **Scarica Provider Microsoft Azure Site Recovery per l'installazione nei server VMM** tooobtain hello versione più recente del file di installazione di Provider hello.
2. Eseguire questo file nel server VMM di origine hello.

   > [!NOTE]
   > Se VMM è distribuito in un cluster e si sta installando hello Provider per hello prima installarlo in un nodo attivo e di fine server VMM nell'insieme di credenziali hello hello installazione tooregister hello. Installare quindi hello Provider in hello altri nodi. Si noti che se si esegue l'aggiornamento di hello Provider tooupgrade in tutti i nodi è necessario perché tutti dovrebbero essere in esecuzione hello stessa versione del Provider.
   >
   >
3. Hello programma di installazione esegue un controllo prerequisiti e le richieste di autorizzazione toostop hello VMM servizio toobegin l'installazione del Provider. Hello servizio VMM verrà riavviato automaticamente al completamento dell'installazione. Se si sta installando in un cluster VMM, che sarà richiesto il ruolo Cluster toostop hello.
4. In **Microsoft Update** è possibile fornire il consenso esplicito agli aggiornamenti. Con questa impostazione abilitata Provider aggiornamenti verranno installati in base a criteri di Microsoft Update tooyour.

    ![Microsoft Updates](./media/site-recovery-vmm-to-azure-classic/updates.png)
5. percorso di installazione dei Provider è stato impostato troppo hello Hello**<SystemDrive>\Programmi\Microsoft System Center 2012 R2\Virtual Machine Manager\bin**. Fare clic su **Installa**.

   ![InstallLocation](./media/site-recovery-vmm-to-azure-classic/install-location.png)
6. Dopo aver hello Provider è installato, fare clic su **registrare** server hello tooregister nell'insieme di credenziali hello.

    ![InstallComplete](./media/site-recovery-vmm-to-azure-classic/install-complete.png)
7. In **nome insieme di credenziali**, verificare il nome di hello dell'insieme di credenziali hello in cui hello server verrà registrato. Fare clic su *Avanti*.

    ![Server registration](./media/site-recovery-vmm-to-azure-classic/vaultcred.PNG)
8. In **connessione Internet** specificare hello come Provider in esecuzione in VMM hello toohello Internet si connette a server. Selezionare **Connetti con impostazioni proxy esistenti** toouse hello Internet impostazioni di connessione predefinite configurate nel server di hello.

    ![Internet Settings](./media/site-recovery-vmm-to-azure-classic/proxydetails.PNG)

   * Se si desidera toouse un proxy personalizzato è necessario configurarlo prima di installare hello Provider. Quando si configurano impostazioni proxy personalizzate connessione proxy di hello toocheck verrà eseguito un test.
   * Se si utilizza un proxy personalizzato, o il proxy predefinito richiede l'autenticazione, occorre tooenter hello proxy dettagli, inclusi la porta e indirizzo proxy hello.
   * URL seguenti devono essere accessibili da hello Server VMM e host Hyper-v hello
     * *.hypervrecoverymanager.windowsazure.com
     * *.accesscontrol.windows.net
     * *.backup.windowsazure.com
     * *.blob.core.windows.net
     * *.store.core.windows.net
   * Consenti indirizzi IP hello descritti in [intervalli IP dei Data Center Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653) e il protocollo HTTPS (443). È necessario che gli intervalli IP toowhite-elenco di hello regione di Azure che si prevede di toouse e quello di Stati Uniti occidentali.
   * Se si utilizza un proxy personalizzato un account RunAs VMM (DRAProxyAccount) verrà creato automaticamente tramite hello specificato le credenziali del proxy. Configurare il server proxy hello in modo che questo account può autenticare correttamente. le impostazioni dell'account RunAs VMM Hello possono essere modificate nella console VMM hello. toodo, aprire hello **impostazioni** area di lavoro, espandere **sicurezza**, fare clic su **account RunAs**e quindi modificare la password di hello di DRAProxyAccount. Servizio VMM toorestart hello è necessario in modo che questa impostazione ha effetto.
9. In **chiave di registrazione**selezionare chiave hello quello scaricato da Azure Site Recovery e copiato toohello server VMM.
10. impostazione di crittografia Hello viene utilizzato solo quando si esegue la replica di macchine virtuali Hyper-V in VMM cloud tooAzure. Se si esegue la replica del sito secondario tooa non utilizzato.
11. In **nome Server**, specificare un server di nome descrittivo tooidentify hello VMM nell'insieme di credenziali hello. In una configurazione cluster specificare il nome del ruolo cluster VMM hello.
12. In **Sincronizza metadati cloud** selezionare se si desidera toosynchronize metadati per tutti i cloud nel server VMM hello con insieme di credenziali hello. Questa azione deve solo toohappen una volta in ogni server. Se non si desidera toosynchronize tutti i cloud, è possibile lasciare deselezionata questa opzione e sincronizzare ogni cloud singolarmente nelle proprietà del cloud nella console VMM hello hello.
13. Fare clic su **Avanti** processo hello toocomplete. Dopo la registrazione, i metadati dal server VMM hello vengono recuperati da Azure Site Recovery. server Hello viene visualizzato nella hello **server VMM** scheda hello **server** pagina nell'insieme di credenziali hello.

    ![Ultima pagina](./media/site-recovery-vmm-to-azure-classic/provider13.PNG)

Dopo la registrazione, i metadati dal server VMM hello vengono recuperati da Azure Site Recovery. server Hello viene visualizzato nella hello **server VMM** scheda, hello **server** pagina nell'insieme di credenziali hello.

### <a name="command-line-installation"></a>Installazione dalla riga di comando
Provider di Azure Site Recovery Hello può anche essere installato utilizzando hello seguente riga di comando. Questo metodo può essere provider hello tooinstall utilizzati in un Server Core per Windows Server 2012 R2.

1. Scaricare hello Provider e registrazione tooa chiave cartella di installazione. ad esempio C:\ASR.
2. Arrestare il servizio System Center Virtual Machine Manager hello
3. Da un prompt dei comandi con privilegi elevati, estrarre il programma di installazione di hello Provider con questi comandi:

        C:\Windows\System32> CD C:\ASR
        C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
4. Installare il provider di hello come indicato di seguito:

        C:\ASR> setupdr.exe /i
5. Registrare Provider hello come segue:

        CD C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin
        C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file> /EncryptionEnabled <full file name toosave hello encryption certificate>       

I parametri sono i seguenti:

* **/ Credenziali** : parametro obbligatorio che specifica il percorso di hello in cui hello Trova file di chiave di registrazione  
* **/ FriendlyName** : parametro obbligatorio per il nome del server host Hyper-V hello visualizzata nel portale di Azure Site Recovery hello hello.
* **/ EncryptionEnabled** : parametro facoltativo toospecify se si desidera tooencryption le macchine virtuali in Azure (alla crittografia rest). nome del file Hello deve avere un **PFX** estensione.
* **/ProxyAddress** : parametro facoltativo che specifica l'indirizzo di hello del server proxy hello.
* **/ProxyPort** : parametro facoltativo che specifica la porta del server proxy hello hello.
* **/proxyUsername** : parametro facoltativo che specifica il nome utente proxy di hello.
* **/proxyPassword** : parametro facoltativo che specifica la password proxy hello.  

## <a name="step-4-create-an-azure-storage-account"></a>Passaggio 4: Creare un account di archiviazione di Azure
1. Se non hai un account di archiviazione di Azure fare clic su **aggiungere un Account di archiviazione di Azure** toocreate un account.
2. Creare un account con la replica geografica abilitata. È necessario in hello stessa area hello servizio Azure Site Recovery e associato hello stessa sottoscrizione.

    ![Account di archiviazione](./media/site-recovery-vmm-to-azure-classic/storage.png)

> [!NOTE]
> [Migrazione di account di archiviazione](../azure-resource-manager/resource-group-move-resources.md) tra risorse gruppi all'interno hello stessa sottoscrizione o per le sottoscrizioni non è supportata per gli account di archiviazione utilizzati per la distribuzione di Site Recovery.
>
>

## <a name="step-5-install-hello-azure-recovery-services-agent"></a>Passaggio 5: Installare hello Azure Recovery Services Agent
Installare l'agente di servizi di ripristino di Azure hello in ogni server host Hyper-V in hello cloud VMM.

1. Fare clic su **avvio rapido** > **scaricare ripristino agente servizi di Azure e installa negli host** tooobtain hello più recente del file di installazione dell'agente di hello.

    ![Installare l'agente di Servizi di ripristino](./media/site-recovery-vmm-to-azure-classic/install-agent.png)
2. Eseguire il file di installazione hello in ogni server host Hyper-V.
3. In hello **controllo dei prerequisiti** pagina fare clic su **Avanti**. Gli eventuali prerequisiti mancanti verranno installati automaticamente.

    ![Prerequisiti per l'agente di Servizi di ripristino di Azure](./media/site-recovery-vmm-to-azure-classic/agent-prereqs.png)
4. In hello **le impostazioni di installazione** pagina, specificare dove si desidera agente hello tooinstall e percorso della cache di hello select in cui verranno installati i metadati di backup. Fare clic su **Installa**.
5. Dopo il completamento dell'installazione fare clic su **Chiudi** guidata hello toocomplete.

    ![Registrare l'Agente di Servizi di ripristino di Microsoft Azure](./media/site-recovery-vmm-to-azure-classic/agent-register.png)

### <a name="command-line-installation"></a>Installazione dalla riga di comando
Inoltre, è possibile installare agente servizi di ripristino di Microsoft Azure hello dalla riga di comando di hello tramite questo comando:

    marsagentinstaller.exe /q /nu

## <a name="step-6-configure-cloud-protection-settings"></a>Passaggio 6: configurare le impostazioni di protezione del cloud
Dopo aver registrato il server VMM hello, è possibile configurare le impostazioni di protezione cloud. È abilitata l'opzione hello **Sincronizza i dati cloud con insieme di credenziali hello** durante l'installazione di Provider hello conseguenza verranno visualizzati tutti i cloud nel server VMM hello in hello <b>elementi protetti</b> scheda nell'insieme di credenziali hello.

![Cloud pubblicato](./media/site-recovery-vmm-to-azure-classic/clouds-list.png)

1. Nella pagina introduttiva hello, fare clic su **impostare la protezione per i cloud VMM**.
2. In hello **elementi protetti** scheda, fare clic sul cloud hello si desidera tooconfigure e analizzare toohello **configurazione** scheda.
3. In **Rete Azure di destinazione** select **Azure**.
4. In **Account di archiviazione** selezionare account di archiviazione di Azure hello usato per la replica.
5. Impostare **crittografare i dati archiviati** troppo**Off**. Questa impostazione specifica che i dati devono essere crittografati durante la replica tra hello nel sito locale e Azure.
6. In **frequenza di copia** lasciare l'impostazione predefinita hello. Questo valore consente di specificare la frequenza della sincronizzazione dei dati tra il percorso di origine e di destinazione.
7. In **Mantieni punti di ripristino per**, lasciare l'impostazione predefinita hello. Con un valore predefinito pari a zero, viene archiviata solo hello ultimo punto di ripristino per una macchina virtuale primaria in un server host di replica.
8. In **frequenza degli snapshot coerenti con l'applicazione**, lasciare l'impostazione predefinita hello. Questo valore specifica la frequenza con cui toocreate snapshot. Le istantanee utilizzano tooensure del servizio Copia Shadow del Volume (VSS) che le applicazioni sono in uno stato coerente durante hello snapshot.  Se si imposta un valore, assicurarsi che è minore del numero di hello di punti di ripristino aggiuntivi configurati.
9. In **ora inizio replica**, specificare quando avviare la replica iniziale dei dati tooAzure. verrà utilizzato il fuso orario Hello nel server host Hyper-V di hello. È consigliabile pianificare la replica iniziale di hello durante le fasce orarie.

    ![Impostazioni della replica cloud](./media/site-recovery-vmm-to-azure-classic/cloud-settings.png)

Dopo aver salvato le impostazioni di hello un processo verrà creato e può essere monitorato nella hello **processi** scheda. Tutti i server host Hyper-V in cloud di origine VMM hello verranno configurati per la replica.

Dopo il salvataggio delle impostazioni di cloud possono essere modificate per hello **configura** scheda toomodify hello destinazione percorso o destinazione account di archiviazione sarà necessaria la configurazione cloud di tooremove hello e successivamente, riconfigurare il cloud hello. Si noti che se si modifica hello storage account hello modifica viene applicata solo per le macchine virtuali che sono abilitate per la protezione dopo che l'account di archiviazione hello è stato modificato. Macchine virtuali esistenti non vengono migrate toohello nuovo account di archiviazione.

## <a name="step-7-configure-network-mapping"></a>Passaggio 7: Configurare il mapping di rete
Prima di iniziare il mapping di rete verificare che le macchine virtuali nel server VMM di origine hello rete VM tooa connesso. Inoltre, creare una o più rete virtuali di Azure. Si noti che più reti VM possono essere mappate tooa singola rete di Azure.

1. Nella pagina introduttiva hello, fare clic su **mapping delle reti**.
2. In hello **reti** scheda **percorso di origine**, selezionare server VMM di origine hello. In **Percorso di destinazione** selezionare Azure.
3. In **origine** vengono visualizzate le reti di un elenco di reti VM associato con il server VMM hello. In **destinazione** reti hello Azure reti associate hello sottoscrizione vengono visualizzate.
4. Selezionare una rete VM di origine hello e fare clic su **mappa**.
5. In hello **selezionare una rete di destinazione** pagina destinazione selezionare hello Azure rete toouse.
6. Fare clic su processo di mapping hello toocomplete hello segno di spunta.

    ![Impostazioni della replica cloud](./media/site-recovery-vmm-to-azure-classic/map-networks.png)

Dopo aver salvato le impostazioni di hello avanzamento del mapping hello tootrack viene avviato un processo e può essere monitorato nella scheda processi hello. Le macchine virtuali di replica esistente che corrispondono toohello rete VM di origine sarà connessa toohello reti Azure di destinazione. Nuove macchine virtuali che sono connessi toohello rete VM di origine sarà toohello connesso rete di Azure connessa dopo la replica. Se si modifica un mapping esistente con una nuova rete, macchine virtuali di replica verranno connesse usando le nuove impostazioni hello.

Si noti che se la rete di destinazione hello dispone di più subnet e una di queste subnet è hello stesso nome di subnet nella macchina virtuale di origine che hello si trova, quindi hello macchina virtuale di replica sarà connessa toothat subnet di destinazione dopo il failover. Se non è presente alcuna subnet di destinazione con un nome corrispondente, macchina virtuale hello sarà toohello connessi prima subnet nella rete hello.

> [!NOTE]
> [Migrazione delle reti](../azure-resource-manager/resource-group-move-resources.md) tra risorse gruppi all'interno hello stessa sottoscrizione o per le sottoscrizioni non è supportata per le reti utilizzate per la distribuzione di Site Recovery.
>
>

## <a name="step-8-enable-protection-for-virtual-machines"></a>Passaggio 8: Abilitare la protezione per le macchine virtuali
Dopo aver configurate correttamente i server, cloud e reti, è possibile abilitare la protezione per le macchine virtuali nel cloud hello. Si noti hello segue:

* Le macchine virtuali devono essere conformi ai [requisiti di Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
* per la macchina virtuale hello, è necessario impostare del sistema operativo di tooenable protezione hello e proprietà del disco del sistema operativo. Quando si crea una macchina virtuale in VMM utilizzando un modello di macchina virtuale è possibile impostare proprietà hello. È inoltre possibile impostare queste proprietà per le macchine virtuali esistenti in hello **generale** e **configurazione Hardware** schede delle proprietà di hello macchina virtuale. Se le proprietà non impostate in VMM sarà in grado di tooconfigure nel portale di Azure Site Recovery hello.

    ![Crea macchina virtuale](./media/site-recovery-vmm-to-azure-classic/enable-new.png)

    ![Modificare le proprietà della macchina virtuale](./media/site-recovery-vmm-to-azure-classic/enable-existing.png)

1. protezione tooenable hello **macchine virtuali** scheda cloud hello in cui hello si trova la macchina virtuale, fare clic su **abilitare la protezione** > **aggiungere macchine virtuali**.
2. Selezionare hello uno desiderato tooprotect hello elenco di macchine virtuali nel cloud hello.

    ![Abilitare la protezione delle macchine virtuali](./media/site-recovery-vmm-to-azure-classic/select-vm.png)

    Avanzamento di hello **Abilita protezione** azione in hello **processi** scheda, inclusa la replica iniziale di hello. Dopo aver hello **finalizzazione della protezione** processo viene eseguito macchina virtuale di hello è pronta per il failover. Dopo aver abilitato la protezione e le macchine virtuali vengono replicate, sarà in grado di tooview usarle in Azure.

    ![Processo di protezione delle macchine virtuali](./media/site-recovery-vmm-to-azure-classic/vm-jobs.png)

1. Verificare la proprietà della macchina virtuale hello e modificarla in base alle esigenze.

    ![Verifica macchine virtuali](./media/site-recovery-vmm-to-azure-classic/vm-properties.png)
2. In hello **configura** scheda delle proprietà di macchina virtuale hello seguenti proprietà di rete può essere modificata.

* **Numero di schede di rete nella macchina virtuale di destinazione hello** -numero hello di schede di rete dipende dalla dimensione hello specificata per la macchina virtuale di destinazione hello. Controllare [specifiche di dimensione di macchina virtuale](../virtual-machines/linux/sizes.md) per il numero di schede supportato dalle dimensioni di macchina virtuale hello hello. Quando si modifica la dimensione hello per una macchina virtuale e salvare le impostazioni di hello, alla successiva apertura hello hello verrà modificato da hello numero di schede di rete **configura** pagina. numero di Hello di schede di rete di macchine virtuali di destinazione è il numero minimo di hello di schede di rete origine macchina virtuale e hello il numero massimo di schede di rete supportato dalle dimensioni hello della macchina virtuale hello scelto, come indicato di seguito:

  * Se il numero di hello di schede di rete nel computer di origine hello è minore o uguale toohello numero di schede consentite per le dimensioni del computer di destinazione hello, quindi sarà necessario destinazione hello hello origine hello stesso numero di schede.
  * Se il numero di hello di schede per la macchina virtuale di origine hello supera il numero di hello consentito per la dimensione di destinazione hello quindi massimo di dimensioni di destinazione hello verrà utilizzato.
  * Ad esempio, se un computer di origine dispone di due schede di rete e le dimensioni del computer di destinazione hello supporta quattro, nel computer di destinazione hello avrà due schede. Se il computer di origine hello dispone di due schede ma hello dimensioni di destinazione supportata supportano solo una macchina di destinazione hello avrà una sola scheda di.     
* **Rete della macchina virtuale di destinazione hello** -macchina virtuale di hello rete toowhich hello si connette toois determinato dal mapping di rete della rete hello della macchina virtuale di origine. Se hello macchina virtuale di origine ha più reti adapter e l'origine di rete sono reti di toodifferent mappata nella destinazione, quindi sarà necessario toochoose tra una delle reti di destinazione hello.
* **Subnet di ogni scheda di rete** : per ogni scheda di rete, è possibile selezionare hello toowhich di subnet hello failover macchina virtuale si connetterà a.
* **Indirizzo IP di destinazione** - se la scheda di rete hello della macchina virtuale di origine è toouse configurato un indirizzo IP statico di indirizzi, quindi è possibile fornire l'indirizzo IP hello per hello macchina virtuale di destinazione. Utilizzare questa funzionalità conserva l'indirizzo IP hello di una macchina virtuale di origine dopo un failover. Se non viene specificato alcun indirizzo IP qualsiasi indirizzo IP disponibile è dato toohello scheda di rete in fase di hello di failover. Se è già utilizzato da un'altra macchina virtuale in esecuzione in Azure ma viene specificato l'indirizzo IP di destinazione hello failover avrà esito negativo.  

    ![Modificare le proprietà di rete](./media/site-recovery-vmm-to-azure-classic/multi-nic.png)

> [!NOTE]
> Le macchine virtuali Linux con indirizzo IP statico non sono supportate.
>
>

## <a name="test-hello-deployment"></a>Distribuzione di prova hello
pianificare la distribuzione, è possibile eseguire un failover di test per una singola macchina virtuale o creare un piano di ripristino costituita da più macchine virtuali ed eseguire un failover di test per hello tootest.  

Il failover di test consente di simulare il meccanismo di failover e di ripristino in una rete isolata. Si noti che:

* Se si desidera tooconnect toohello macchina virtuale di Azure tramite Desktop remoto dopo il failover hello, abilitare connessione Desktop remoto sulla macchina virtuale hello prima di eseguire il failover di test hello.
* Dopo il failover, utilizzare un toohello macchina virtuale di Azure tramite Desktop remoto tooconnect indirizzo pubblico di IP. Se si desidera toodo, assicurarsi che tutti i criteri che impediscono la connessione tooa virtual machine tramite un indirizzo pubblico dominio non è.

> [!NOTE]
> tooget hello migliori prestazioni quando si esegue il failover tooAzure, assicurarsi di aver installato hello agente su hello VM di Azure. Questo consente di avere tempi di avvio più rapidi e contribuisce alla risoluzione dei problemi. Scaricare hello [agente Linux](https://github.com/Azure/WALinuxAgent), o hello [dell'agente di Windows](http://go.microsoft.com/fwlink/?LinkID=394789).
>
>

### <a name="create-a-recovery-plan"></a>Creare un piano di ripristino
1. In hello **piani di ripristino** scheda, aggiungere un nuovo piano. Specificare un nome di **VMM** in **tipo di origine**e il server VMM di origine hello in **origine**. destinazione Hello sarà Azure.

    ![Crea piano di ripristino](./media/site-recovery-vmm-to-azure-classic/recovery-plan1.png)
2. In hello **Seleziona macchine virtuali** pagina, piano di ripristino toohello tooadd selezionare le macchine virtuali. Queste macchine virtuali vengono aggiunte gruppo predefinito piano di ripristino toohello: gruppo 1. In un singolo piano di ripristino è stato testato un massimo di 100 macchine virtuali.

* Proprietà della macchina virtuale hello tooverify prima di aggiungerli toohello piano, fare clic su macchina virtuale hello nella pagina delle proprietà hello del cloud hello in cui si trova. È anche possibile configurare proprietà della macchina virtuale hello nella console VMM hello.
* Tutte le macchine virtuali hello che vengono visualizzate sono state abilitate per la protezione. elenco di Hello include entrambe le macchine virtuali che sono abilitate per protezione dati e la replica iniziale è stata completata e quelle che sono abilitati per la protezione con la replica in sospeso iniziale. Solo le macchine virtuali con la replica iniziale completa possono eseguire il failover come parte di un piano di ripristino.

    ![Crea piano di ripristino](./media/site-recovery-vmm-to-azure-classic/select-rp.png)

Dopo aver creato un piano di ripristino, viene visualizzato in hello **piani di ripristino** scheda. È inoltre possibile aggiungere [i runbook di automazione di Azure](site-recovery-runbook-automation.md) toohello azioni tooautomate piano di ripristino durante il failover.

### <a name="run-a-test-failover"></a>Eseguire un failover di test
Esistono due modi toorun un tooAzure di failover di test.

* **Failover di test senza una rete di Azure**: questo tipo di failover di test controlla che la macchina virtuale hello viene visualizzato correttamente in Azure. macchina virtuale Hello non saranno connesse tooany rete di Azure dopo il failover.
* **Failover di test con una rete di Azure**: questo tipo di failover verifica che hello intero ambiente di replica venga rilevato come previsto e che è stato eseguito il failover le macchine virtuali hello sarà connessa toohello di rete di Azure di destinazione specificato. Per la gestione della subnet, per il test failover subnet hello della macchina virtuale di test hello verrà rilevata in base alla subnet hello della macchina virtuale di replica hello. Questa è la replica di diversi tooregular quando subnet hello di una macchina virtuale di replica si basa su subnet hello della macchina virtuale di origine hello.

Se si desidera toorun un failover di test per una macchina virtuale abilitata per la protezione tooAzure senza specificare una rete Azure di destinazione non è necessario tooprepare nulla. toorun un failover di test con una destinazione di rete di Azure, occorre toocreate una nuova rete di Azure isolata dalla rete di Azure di produzione (comportamento predefinito quando si crea una nuova rete in Azure). Osservare come troppo[eseguire un failover di test](site-recovery-failover.md) per altri dettagli.

È anche necessario tooset backup infrastruttura hello per toowork macchina virtuale replicata hello come previsto. Ad esempio, una macchina virtuale con DNS e Controller di dominio può essere replicata tooAzure usando Azure Site Recovery e può essere creata in una rete di test hello utilizzando Test del Failover. Per altri dettagli, vedere la sezione [Considerazioni sul failover di test per Active Directory](site-recovery-active-directory.md#test-failover-considerations) .

hello toorun un failover di test seguente:

1. In hello **piani di ripristino** , selezionare il piano di hello e fare clic su **Failover di Test**.
2. In hello **conferma Failover di Test** pagina selezionare **Nessuno** o una rete di Azure specifica.  Si noti che se si specifica nessuno hello failover di test verrà verificare che hello macchina virtuale replicato correttamente tooAzure, ma non contatta la configurazione di rete di replica.

    ![Nessuna rete](./media/site-recovery-vmm-to-azure-classic/test-no-network.png)
3. Se la crittografia dei dati è abilitato per il cloud di hello, in **chiave di crittografia** certificato selezionare hello emesso durante l'installazione di hello Provider nel server VMM, hello quando è stata attivata la crittografia dei dati tooenable opzione hello per un cloud .
4. In hello **processi** scheda è possibile monitorare lo stato di avanzamento di failover. È anche necessario replica test della macchina virtuale in grado di toosee hello in hello portale di Azure. Se si sta imposta backup di macchine virtuali tooaccess dalla rete locale è possibile avviare una macchina virtuale di toohello connessione Desktop remoto.
5. Quando il failover hello raggiunge hello **test completo** fase, fare clic su **completamento del Test** toofinish è. È possibile eseguire il drill-down toohello **processo** scheda tootrack failover corso, lo stato e tooperform eventuali azioni necessarie.
6. Dopo il failover, è possibile visualizzare una replica di test hello macchina virtuale nel portale di Azure hello. Se si sta imposta backup di macchine virtuali tooaccess dalla rete locale è possibile avviare una macchina virtuale di toohello connessione Desktop remoto. Hello seguenti:

   1. Verificare che le macchine virtuali hello è stata avviata correttamente.
   2. Se si desidera tooconnect toohello macchina virtuale di Azure tramite Desktop remoto dopo il failover hello, abilitare connessione Desktop remoto sulla macchina virtuale hello prima di eseguire il failover di test hello. È inoltre necessario un endpoint RDP sulla macchina virtuale hello tooadd. È possibile sfruttare un [runbook di automazione di Azure](site-recovery-runbook-automation.md) toodo che.
   3. Dopo il failover, se si usa una macchina di virtuale toohello pubblica del tooconnect indirizzo IP in Azure tramite Desktop remoto, verificare che tutti i criteri che impediscono la connessione macchina virtuale tooa utilizzando un indirizzo pubblico dominio non è.
7. Al termine hello test hello seguenti:

   * Fare clic su **hello failover di test è stato completato**. Pulizia hello power tooautomatically ambiente di test disattivare ed eliminare hello macchine virtuali di test.
   * Fare clic su **note** toorecord e salvare eventuali commenti associati hello test failover.


## <a name="next-steps"></a>Passaggi successivi
Altre informazioni sulla [configurazione dei piani di ripristino](site-recovery-create-recovery-plans.md) e sul [failover](site-recovery-failover.md).
