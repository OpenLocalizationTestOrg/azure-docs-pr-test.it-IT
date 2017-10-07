---
title: aaaReplicate tooAzure di macchine virtuali Hyper-V nel portale classico hello | Documenti Microsoft
description: In questo articolo viene descritto come tooreplicate virtuale Hyper-V macchine tooAzure quando macchine non sono gestite nei cloud VMM.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 3f4c4483-e3dd-495a-bd02-c16e9e28c88d
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 02/21/2017
ms.author: raynew
ms.openlocfilehash: 12d08d950a79e956436cb03ffc87ab40e86c589e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-between-on-premises-hyper-v-virtual-machines-and-azure-without-vmm-with-azure-site-recovery"></a>Replica tra macchine virtuali Hyper-V locali e Azure (senza VMM) con Azure Site Recovery
> [!div class="op_single_selector"]
> * [Portale di Azure](site-recovery-hyper-v-site-to-azure.md)
> * [PowerShell - Gestione risorse](site-recovery-deploy-with-powershell-resource-manager.md)
> * [Portale classico](site-recovery-hyper-v-site-to-azure-classic.md)
>
>

In questo articolo viene descritto come tooreplicate locale tooAzure di macchine virtuali Hyper-V, utilizzando hello [Azure Site Recovery](site-recovery-overview.md) servizio nel portale di Azure hello. In questo scenario, i server Hyper-V non sono gestiti in cloud VMM.

Dopo aver letto questo articolo, inviare eventuali commenti nella parte inferiore di hello o porre domande tecniche su hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="site-recovery-in-hello-azure-portal"></a>Ripristino del sito in hello portale di Azure

Azure offre due [modelli di distribuzione](../resource-manager-deployment-model.md) diversi per creare e usare le risorse: Azure Resource Manager e distribuzione classica. Azure offre inoltre due portali: hello portale di Azure classico e hello portale di Azure.

Questo articolo viene descritto come toodeploy nel portale classico hello. portale classico Hello può essere utilizzato toomaintain insiemi di credenziali esistenti. È possibile creare nuovi insiemi di credenziali usando portale classico hello.

## <a name="site-recovery-in-your-business"></a>Site Recovery in azienda

Le organizzazioni devono una strategia di BCDR che determina come le applicazioni e i dati rimangono in esecuzione e disponibili durante i tempi di inattività pianificati ed e ripristino le condizioni di lavoro toonormal appena possibile. Ecco quali vantaggi offre Site Recovery:

* Protezione esterna per le app aziendali in esecuzione su VM Hyper-V.
* Tooset un'unica posizione, gestire e monitorare la replica, il failover e ripristino.
* TooAzure semplice failover e failback (ripristino) dal server host di Azure tooHyper-V nel sito locale.
* Piani di ripristino con più VM per fare in modo che il failover dei carichi di lavoro delle applicazioni a più livelli venga eseguito contemporaneamente.

## <a name="azure-prerequisites"></a>Prerequisiti di Azure
* È necessario un account [Microsoft Azure](https://azure.microsoft.com/) . È possibile iniziare con una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).
* È necessario un toostore replicati dati dell'account di archiviazione di Azure. account di Hello deve replica geografica abilitata. Dovrebbe essere nella stessa area dell'insieme di credenziali di Azure Site Recovery hello hello e associato hello stessa sottoscrizione. [Altre informazioni sull'Archiviazione di Azure](../storage/common/storage-introduction.md). Si noti che non è supportato lo spostamento di account di archiviazione creati utilizzando hello [nuovo portale di Azure](../storage/common/storage-create-storage-account.md) tra gruppi di risorse.
* È necessario una rete virtuale di Azure in modo che le macchine virtuali di Azure connessa tooa rete quando si esegue il failover dal sito primario.

## <a name="hyper-v-prerequisites"></a>Prerequisiti di Hyper-V
* Sarà necessario uno o più server in esecuzione nel sito locale di origine hello **Windows Server 2012 R2** con installato il ruolo Hyper-V hello o **Microsoft Hyper-V Server 2012 R2**. Questo server deve:
* Contenere una o più macchine virtuali.
* Essere connesso toohello Internet, direttamente o tramite un proxy.
* Eseguire correzioni hello descritte nell'articolo [2961977](https://support.microsoft.com/en-us/kb/2961977 "KB2961977").

## <a name="virtual-machine-prerequisites"></a>Prerequisiti delle macchine virtuali
Macchine virtuali da tooprotect devono essere conformi ai [requisiti macchina virtuale di Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

## <a name="provider-and-agent-prerequisites"></a>Prerequisiti di provider e agente
Come parte della distribuzione di Azure Site Recovery consentiranno di installare il Provider di Azure Site Recovery hello di hello Azure Recovery Services Agent in ogni server Hyper-V. Si noti che:

* È consigliabile eseguire sempre l'agente e versioni più recenti di hello di hello Provider. Sono disponibili nel portale di Site Recovery hello.
* Tutti i server Hyper-V in un insieme di credenziali deve avere hello stesse versioni di hello Provider e agente.
* Provider in esecuzione nel server di hello Hello connette tooSite ripristino su hello internet. È possibile farlo senza un proxy, le impostazioni proxy hello attualmente configurate nel server Hyper-V hello o con impostazioni proxy personalizzate configurate durante l'installazione del Provider. È necessario che abbia accesso al server proxy hello desiderato toouse questi URL hello per la connessione tooAzure toomake:

  * *.accesscontrol.windows.net
  * *.backup.windowsazure.com
  * *.hypervrecoverymanager.windowsazure.com
  * *. store.core.windows.net      
  * *.blob.core.windows.net
  - https://www.msftncsi.com/ncsi.txt
  - time.windows.com
  - time.nist.gov
* Consentono inoltre di indirizzi IP hello descritti in [intervalli IP dei Data Center Azure](https://www.microsoft.com/download/details.aspx?id=41653) e il protocollo HTTPS (443). Si dispone di intervalli IP hello tooallow di hello regione di Azure che si prevede di toouse e quello di Stati Uniti occidentali.

Questo grafico mostra i canali di comunicazione diversi hello e le porte utilizzate da Site Recovery per la replica e orchestrazione

![Topologia B2A](./media/site-recovery-hyper-v-site-to-azure-classic/b2a-topology.png)

## <a name="step-1-create-a-vault"></a>Passaggio 1: Creare un insieme di credenziali
1. Accedi toohello [portale di gestione](https://portal.azure.com).
2. Espandere **Servizi dati** > **Servizi di ripristino** e fare clic su **Insieme di credenziali di Site Recovery**.
3. Fare clic su **Creare nuovo** > **Creazione rapida**.
4. In **nome**, immettere un insieme di credenziali di nome descrittivo tooidentify hello.
5. In **area**, selezionare hello area geografica per l'insieme di credenziali hello. aree toocheck supportato vedere aree geografiche disponibili in [dettagli prezzi di Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
6. Fare clic su **Create vault**.

    ![Nuovo insieme di credenziali](./media/site-recovery-hyper-v-site-to-azure-classic/vault.png)

Controllare tooconfirm barra di stato hello che hello insieme di credenziali è stato creato correttamente. insieme di credenziali Hello verrà elencato come **Active** nella pagina principale di servizi di ripristino hello.

## <a name="step-2-create-a-hyper-v-site"></a>Passaggio 2: Creare un sito Hyper-V
1. Nella pagina Servizi di ripristino hello, fare clic sulla pagina avvio rapido di hello insieme di credenziali tooopen hello. Guida introduttiva può anche essere aperto in qualsiasi momento facendo clic sull'icona hello.

    ![Avvio rapido](./media/site-recovery-hyper-v-site-to-azure-classic/quick-start-icon.png)
2. Nell'elenco a discesa hello, selezionare **tra un sito Hyper-V locale e Azure**.

    ![Scenario del sito di Hyper-V](./media/site-recovery-hyper-v-site-to-azure-classic/select-scenario.png)
3. In **Crea un sito Hyper-V** fare clic su **Crea sito Hyper-V**. Specificare un nome per il sito e salvare.

    ![Sito di Hyper-V](./media/site-recovery-hyper-v-site-to-azure-classic/create-site.png)

## <a name="step-3-install-hello-provider-and-agent"></a>Passaggio 3: Installare hello Provider e agente
Installare Provider hello e l'agente in ogni server Hyper-V con macchine virtuali che si desidera tooprotect.

Se si sta installando in un cluster Hyper-V, esegue i passaggi da 5 a 11 su ogni nodo nel cluster di failover hello. Dopo che tutti i nodi vengono registrati e protezione è abilitata, le macchine virtuali saranno protetti anche se essi eseguire la migrazione tra nodi cluster hello.

1. In **Prepara server Hyper-V** fare clic sul file **Scaricare una chiave di registrazione**.
2. In hello **Scarica chiave di registrazione** pagina, fare clic su **scaricare** sito toohello successivo. Scaricare hello tooa chiave posizione sicura facilmente accessibile dal server hello Hyper-V. chiave Hello è valido per 5 giorni dopo la sua creazione.

    ![Chiave di registrazione](./media/site-recovery-hyper-v-site-to-azure-classic/download-key.png)
3. Fare clic su **Download hello Provider** tooobtain versione più recente di hello.
4. Eseguire il file hello in ogni server Hyper-V da tooregister nell'insieme di credenziali hello. file Hello installa due componenti:
   * **Provider di Azure Site Recovery**: gestisce le comunicazioni e l'orchestrazione tra il server di hello Hyper-V e il portale di Azure Site Recovery hello.
   * **Agente di servizi di ripristino Azure**: gestisce il trasferimento dei dati tra le macchine virtuali in esecuzione su server Hyper-V di origine hello e archiviazione di Azure.
5. In **Microsoft Update** è possibile fornire il consenso esplicito agli aggiornamenti. Con questa impostazione è abilitata, Provider e l'agente aggiornamenti verranno installati in base a criteri di Microsoft Update tooyour.

    ![Microsoft Updates](./media/site-recovery-hyper-v-site-to-azure-classic/provider1.png)
6. In **installazione** specificare dove si desidera tooinstall hello Provider e agente nel server Hyper-V di hello.

    ![Percorso di installazione](./media/site-recovery-hyper-v-site-to-azure-classic/provider2.png)
7. Al termine dell'installazione continuare l'impostazione del server di hello tooregister nell'insieme di credenziali hello.
8. In hello **impostazioni insieme di credenziali** pagina, fare clic su **Sfoglia** tooselect file di chiave hello. Specificare una sottoscrizione di Azure Site Recovery hello, nome di archivio, hello e hello Hyper-V del sito toowhich hello Hyper-V server appartiene.

    ![Server registration](./media/site-recovery-hyper-v-site-to-azure-classic/provider8.PNG)
9. In hello **connessione Internet** pagina è possibile specificare la modalità di connessione tooAzure Site Recovery Provider hello. Selezionare **utilizza impostazioni proxy del sistema predefinito** toouse hello Internet impostazioni di connessione predefinite configurate nel server di hello. Se non si specifica un valore predefinito di hello verranno usate le impostazioni.

   ![Internet Settings](./media/site-recovery-hyper-v-site-to-azure-classic/provider7.PNG)
10. Registrazione Avvia server hello tooregister nell'insieme di credenziali hello.

    ![Server registration](./media/site-recovery-hyper-v-site-to-azure-classic/provider15.PNG)
11. Dopo il completamento di registrazione dei metadati da hello Hyper-V server verrà recuperato da Azure Site Recovery e hello server viene visualizzato nella hello **siti Hyper-V** scheda hello **server** pagina nell'insieme di credenziali hello.

### <a name="install-hello-provider-from-hello-command-line"></a>Installare Provider hello dalla riga di comando hello
In alternativa è possibile installare Provider di Azure Site Recovery hello dalla riga di comando hello. Utilizzare questo metodo se si desidera tooinstall hello Provider in un computer che esegue Windows Server Core 2012 R2. Eseguire dalla riga di comando hello come segue:

1. Scaricare hello Provider e registrazione tooa chiave cartella di installazione. ad esempio C:\ASR.
2. Eseguire il prompt dei comandi come amministratore e digitare:

        C:\Windows\System32> CD C:\ASR
        C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
3. Installare quindi hello Provider eseguendo:

        C:\ASR> setupdr.exe /i
4. Eseguire dopo la registrazione toocomplete hello:

        CD C:\Program Files\Microsoft Azure Site Recovery Provider
        C:\Program Files\Microsoft Azure Site Recovery Provider\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file> /EncryptionEnabled <full file name toosave hello encryption certificate>         

I parametri includono:

* **/ Credenziali**: specificare il percorso di hello hello chiave di registrazione è stato scaricato.
* **/ FriendlyName**: specificare un server host Hyper-V hello tooidentify. Questo nome verrà visualizzato nel portale di hello
* **/EncryptionEnabled**: facoltativo. Specificare se si desidera tooencrypt macchine virtuali di replica in Azure (alla crittografia rest).
* **/proxyAddress**; **/proxyport**; **/proxyUsername**; **/proxyPassword**: facoltativo. Se si desidera toouse un proxy personalizzato, o il proxy esistente richiede l'autenticazione, specificare i parametri del proxy.

## <a name="step-4-create-an-azure-storage-account"></a>Passaggio 4: Creare un account di archiviazione di Azure
* In **preparare le risorse** selezionare **crea Account di archiviazione** toocreate un account di archiviazione di Azure se non si dispone di uno. account di Hello deve disporre di replica geografica abilitata. Dovrebbe essere nella stessa area dell'insieme di credenziali di Azure Site Recovery hello hello e associato hello stessa sottoscrizione.

    ![Crea account di archiviazione](./media/site-recovery-hyper-v-site-to-azure-classic/create-resources.png)

> [!NOTE]
> 1. Non è supportata spostamento hello di account di archiviazione creati utilizzando hello [nuovo portale di Azure](../storage/common/storage-create-storage-account.md) tra gruppi di risorse.
> 2. [Migrazione di account di archiviazione](../azure-resource-manager/resource-group-move-resources.md) tra risorse gruppi all'interno hello stessa sottoscrizione o per le sottoscrizioni non è supportata per gli account di archiviazione utilizzati per la distribuzione di Site Recovery.
>

## <a name="step-5-create-and-configure-protection-groups"></a>Passaggio 5: Creare e configurare gruppi di protezione 
Gruppi di protezione sono raggruppamenti logici di macchine virtuali che si desidera utilizzare tooprotect hello stesse impostazioni di protezione. Si applica a gruppo protezione dati tooa le impostazioni di protezione e tali impostazioni sono applicati tooall le macchine virtuali che si aggiunge il gruppo di toohello.

1. In **Crea e configura gruppi di protezione** fare clic su **Crea gruppo di protezione dati**. Se non risultano soddisfatti tutti i requisiti, viene visualizzato un messaggio in cui è disponibile l'opzione **Visualizza dettagli** che consente di ottenere maggiori informazioni.
2. In hello **gruppi protezione dati** scheda, aggiungere un gruppo protezione dati. Specificare un nome, un sito Hyper-V di origine hello e una destinazione di hello **Azure**, il nome della sottoscrizione Azure Site Recovery e hello account di archiviazione di Azure.

    ![Gruppo protezione dati](./media/site-recovery-hyper-v-site-to-azure-classic/protection-group.png)
3. In **le impostazioni di replica** set hello **frequenza di copia** toospecify la frequenza di sincronizzazione delta dati hello tra hello origine e di destinazione. È possibile impostare too30 secondi, 5 minuti o 15 minuti.
4. In **Mantieni punti di ripristino** specificare il numero di ore della cronologia di ripristino da archiviare.
5. In **frequenza degli snapshot coerenti con l'applicazione** è possibile specificare se gli snapshot tootake che utilizzano tooensure del servizio Copia Shadow del Volume (VSS) che le applicazioni sono in uno stato coerente durante hello snapshot. Per impostazione predefinita questi snapshot non vengono eseguiti. Assicurarsi che questo valore è impostato tooless numero hello di punti di ripristino aggiuntivi configurati. Questa è supportata solo se macchina virtuale hello è in esecuzione un sistema operativo Windows.
6. In **ora inizio replica iniziale** specificare quando la replica iniziale delle macchine virtuali nel gruppo protezione dati hello deve essere inviata tooAzure.

    ![Gruppo protezione dati](./media/site-recovery-hyper-v-site-to-azure-classic/protection-group2.png)

## <a name="step-6-enable-virtual-machine-protection"></a>Passaggio 6: Abilitare la protezione delle macchine virtuali
Aggiungere le macchine virtuali tooa protezione gruppo tooenable dati per loro.

> [!NOTE]
> La protezione di macchine virtuali che eseguono Linux con un indirizzo IP statico non è supportata.
>
>

1. In hello **macchine** scheda per gruppo protezione dati hello, fare clic su * * tooprotection di macchine virtuali Aggiungi gruppi di protezione tooenable * *.
2. In hello **abilitare la protezione della macchina virtuale** pagina hello selezionare le macchine virtuali da tooprotect.

    ![Abilitare la protezione delle macchine virtuali](./media/site-recovery-hyper-v-site-to-azure-classic/add-vm.png)

    Avvia i processi di protezione consentono di Hello. È possibile monitorare lo stato di avanzamento in hello **processi** scheda. Macchina virtuale di hello viene eseguito il processo di finalizzazione della protezione hello è pronto per il failover.
3. Dopo la configurazione della protezione è possibile:

   * Visualizzare le macchine virtuali in **elementi protetti** > **gruppi protezione dati** > *protectiongroup_name*  >  **Macchine virtuali** è possibile visualizzare dettagli toomachine hello **proprietà** scheda...
   * Configurare le proprietà di failover hello per le macchine virtuali in **elementi protetti** > **gruppi protezione dati** > *protectiongroup_name*  >  **Macchine virtuali** *Nome_macchina_virtuale* > **configura**. È possibile configurare:

     * **Nome**: nome hello della macchina virtuale hello in Azure.
     * **Dimensioni**: hello dimensioni di destinazione della macchina virtuale hello che viene eseguito il failover.

       ![Configurare le proprietà della macchina virtuale](./media/site-recovery-hyper-v-site-to-azure-classic/vm-properties.png)
   * Configurare altre impostazioni della macchina virtuale in *Elementi protetti** > **Gruppi di protezione** > *nome_gruppodiprotezione* > **Macchine virtuali***nome_macchina_virtuale* > **Configura**, tra cui:

     * **Le schede di rete**: hello numero di schede di rete dipende dalle dimensioni hello specificate per la macchina virtuale di destinazione hello. Controllare [specifiche di dimensione di macchina virtuale](../virtual-machines/linux/sizes.md) per il numero di schede di rete supportato dalle dimensioni di macchina virtuale hello hello.

       Quando si modifica la dimensione hello per una macchina virtuale e salvare le impostazioni di hello, numero hello di scheda di rete viene modificato quando si apre **configura** hello pagina successiva. numero di Hello di schede di rete delle macchine virtuali di destinazione è minimo del numero di hello di schede di rete nella macchina virtuale di origine e il numero massimo di schede di rete supportato dalle dimensioni hello della macchina virtuale hello scelto. Questo concetto è illustrato di seguito:

       * Se il numero di hello di schede di rete nel computer di origine hello è minore o uguale toohello numero di schede consentite per le dimensioni del computer di destinazione hello, quindi sarà necessario destinazione hello hello origine hello stesso numero di schede.
       * Se il numero di hello di schede per la macchina virtuale di origine hello supera il numero di hello consentito per la dimensione di destinazione hello quindi massimo di dimensioni di destinazione hello verrà utilizzato.
       * Se, ad esempio un computer di origine ha due schede di rete e le dimensioni del computer di destinazione hello supporta quattro, il computer di destinazione hello avrà due schede. Se il computer di origine hello dispone di due schede ma hello dimensioni di destinazione supportata supportano solo una macchina di destinazione hello avrà una sola scheda di.

     * **Rete di Azure**: specificare la macchina virtuale hello rete toowhich hello deve eseguire il failover. Se macchina virtuale hello dispone di tutte le schede di più schede di rete deve toohello connesso stessa rete di Azure.
     * **Subnet** per ogni scheda di rete nella macchina virtuale hello subnet selezionare hello nella macchina di hello Azure rete toowhich hello devono connettersi dopo il failover.
     * **Indirizzo IP di destinazione**: se la scheda di rete hello della macchina virtuale di origine è configurata toouse statico un indirizzo IP è possibile specificare l'indirizzo IP hello per tooensure di macchina virtuale di destinazione hello che hello macchina ha hello stesso indirizzo IP dopo il failover .  Se non si specifica un indirizzo IP verrà assegnato un indirizzo disponibile in fase di hello di failover. Se si specifica un indirizzo che si sta usando, il failover avrà esito negativo.

     > [!NOTE]
     > [Migrazione delle reti](../azure-resource-manager/resource-group-move-resources.md) tra risorse gruppi all'interno hello stessa sottoscrizione o per le sottoscrizioni non è supportata per le reti utilizzate per la distribuzione di Site Recovery.
     >

     ![Configurare le proprietà della macchina virtuale](./media/site-recovery-hyper-v-site-to-azure-classic/multiple-nic.png)




## <a name="step-7-create-a-recovery-plan"></a>Passaggio 7: Creare un piano di ripristino
Nella distribuzione di ordine tootest hello è possibile eseguire un failover di test per una singola macchina virtuale o un piano di ripristino che contiene uno o più macchine virtuali. [Altre informazioni](site-recovery-create-recovery-plans.md) sulla creazione di un piano di ripristino.

## <a name="step-8-test-hello-deployment"></a>Passaggio 8: Testare la distribuzione di hello
Esistono due modi toorun un tooAzure di failover di test.

* **Failover di test senza una rete di Azure**: questo tipo di failover di test controlla che la macchina virtuale hello viene visualizzato correttamente in Azure. macchina virtuale Hello non saranno connesse tooany rete di Azure dopo il failover.
* **Failover di test con una rete di Azure**: questo tipo di failover verifica che hello intero ambiente di replica venga rilevato come previsto e che è stato eseguito il failover le macchine virtuali hello connette toohello di rete di Azure di destinazione specificato. Si noti che per il test failover subnet hello della macchina virtuale di test hello verrà rilevata in base alla subnet hello della macchina virtuale di replica hello. Questa è la replica di diversi tooregular quando subnet hello di una macchina virtuale di replica si basa su subnet hello della macchina virtuale di origine hello.

Se si desidera toorun un failover di test senza specificare una rete di Azure non è necessario tooprepare nulla.

toorun un failover di test con una destinazione di rete di Azure, occorre toocreate una nuova rete di Azure isolata dalla rete di Azure di produzione (comportamento predefinito quando si crea una nuova rete in Azure). Per altre informazioni dettagliate, vedere [Eseguire un failover di test](site-recovery-failover.md) .

toofully testare la distribuzione di replica e la rete è necessario tooset backup infrastruttura hello in modo che hello replicati toowork macchina virtuale come previsto. Un modo per eseguire questa tootooset rapidamente una macchina virtuale come controller di dominio con DNS e replicare tooAzure utilizzando toocreate il ripristino del sito di rete eseguendo un failover di test in test hello.  [Altre informazioni](site-recovery-active-directory.md#test-failover-considerations) e considerazioni sul failover di test per Active Directory.

Eseguire il failover di test hello come segue:

> [!NOTE]
> tooget hello migliori prestazioni quando si esegue l'operazione tooAzure un failover, assicurarsi di aver installato nel computer protetto hello hello agente di Azure. Questo consente un avvio più veloce e facilita anche la diagnosi nel caso di problemi. L'agente Linux è disponibile [qui](https://github.com/Azure/WALinuxAgent), mentre l'agente Windows è disponibile [qui](http://go.microsoft.com/fwlink/?LinkID=394789)
>
>

1. In hello **piani di ripristino** , selezionare il piano di hello e fare clic su **Failover di Test**.
2. In hello **conferma Failover di Test** pagina selezionare **Nessuno** o una rete di Azure specifica.  Si noti che se si seleziona **Nessuno** hello test failover verifica che la macchina virtuale hello replicato correttamente tooAzure ma non controllare la configurazione di rete di replica.

    ![Failover di test](./media/site-recovery-hyper-v-site-to-azure-classic/test-nonetwork.png)
3. In hello **processi** scheda è possibile monitorare lo stato di avanzamento di failover. È anche necessario replica test della macchina virtuale in grado di toosee hello in hello portale di Azure. Se si sta imposta backup di macchine virtuali tooaccess dalla rete locale è possibile avviare una macchina virtuale di toohello connessione Desktop remoto.
4. Quando il failover hello raggiunge hello **test completo** fase, fare clic su **completa Test** toofinish hello failover di test. È possibile eseguire il drill-down toohello **processo** scheda tootrack failover corso, lo stato e tooperform eventuali azioni necessarie.
5. Dopo il failover sarà in grado di toosee replica di test hello macchina virtuale nel portale di Azure hello. Se si sta imposta backup di macchine virtuali tooaccess dalla rete locale è possibile avviare una macchina virtuale di toohello connessione Desktop remoto.

   1. Verificare che le macchine virtuali hello è stata avviata correttamente.
   2. Se si desidera tooconnect toohello macchina virtuale di Azure tramite Desktop remoto dopo il failover hello, abilitare connessione Desktop remoto sulla macchina virtuale hello prima di eseguire il failover di test hello. È necessario anche un endpoint RDP sulla macchina virtuale hello tooadd. È possibile sfruttare un [runbook di automazione di Azure](site-recovery-runbook-automation.md) toodo che.
   3. Dopo il failover se si utilizza una macchina di virtuale toohello pubblica del tooconnect indirizzo IP in Azure tramite Desktop remoto, verificare che non si dispone di tutti i criteri che impediscono la connessione macchina virtuale tooa utilizzando un indirizzo pubblico dominio.
6. Al termine hello test hello seguenti:

   * Fare clic su **hello failover di test è stato completato**. Pulizia hello power tooautomatically ambiente di test disattivare ed eliminare hello macchine virtuali di test.
   * Fare clic su **note** toorecord e salvare eventuali commenti associati hello test failover.
7. Quando il failover hello raggiunge hello **test completo** fase fine verifica hello come indicato di seguito:
   1. Consente di visualizzare nel portale di Azure hello hello macchina virtuale di replica. Verificare che la macchina virtuale hello viene avviato correttamente.
   2. Se si sta imposta backup di macchine virtuali tooaccess dalla rete locale è possibile avviare una macchina virtuale di toohello connessione Desktop remoto.
   3. Fare clic su **test completo hello** toofinish è.
   4. Fare clic su **note** toorecord e salvare eventuali commenti associati hello test failover.
   5. Fare clic su **hello failover di test è stato completato**. Pulizia hello power tooautomatically ambiente di test disattivare ed eliminare hello macchina virtuale di test.

## <a name="next-steps"></a>Passaggi successivi
Dopo aver configurato correttamente la distribuzione, leggere [altre informazioni](site-recovery-failover.md) sul failover.
