---
title: Replicare le macchine virtuali Hyper-V in Azure nel portale classico | Documentazione Microsoft
description: Questo articolo descrive come eseguire la replica di macchine virtuali Hyper-V in Azure quando le macchine non sono gestite in cloud VMM.
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
ms.openlocfilehash: 438f32ee3605e2dd0c46de7993a359cc269262fe
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="replicate-between-on-premises-hyper-v-virtual-machines-and-azure-without-vmm-with-azure-site-recovery"></a>Replica tra macchine virtuali Hyper-V locali e Azure (senza VMM) con Azure Site Recovery
> [!div class="op_single_selector"]
> * [Portale di Azure](site-recovery-hyper-v-site-to-azure.md)
> * [PowerShell - Gestione risorse](site-recovery-deploy-with-powershell-resource-manager.md)
> * [Portale classico](site-recovery-hyper-v-site-to-azure-classic.md)
>
>

Questo articolo illustra come replicare macchine virtuali Hyper-V locali in Azure usando il servizio [Azure Site Recovery](site-recovery-overview.md) nel portale di Azure. In questo scenario, i server Hyper-V non sono gestiti in cloud VMM.

Dopo la lettura di questo articolo, è possibile inserire commenti nella parte inferiore oppure porre domande tecniche nel [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="site-recovery-in-the-azure-portal"></a>Site Recovery nel portale di Azure

Azure offre due [modelli di distribuzione](../resource-manager-deployment-model.md) diversi per creare e usare le risorse: Azure Resource Manager e distribuzione classica. Sono disponibili due portali: il portale di Azure classico e il portale di Azure.

Questo articolo descrive come eseguire la distribuzione nel portale classico. Il portale classico può essere usato per gestire gli insiemi di credenziali esistenti. Non è possibile creare nuovi insieme di credenziali usando il portale classico.

## <a name="site-recovery-in-your-business"></a>Site Recovery in azienda

Le organizzazioni necessitano di una strategia di continuità aziendale e ripristino di emergenza per determinare come app e dati possano rimanere in esecuzione e disponibili durante i periodi di inattività, pianificati o meno, e come ripristinare le normali condizioni di lavoro il prima possibile. Ecco quali vantaggi offre Site Recovery:

* Protezione esterna per le app aziendali in esecuzione su VM Hyper-V.
* Un'unica posizione per l'impostazione, la gestione e il monitoraggio di replica, failover e ripristino.
* Semplicità delle operazioni di failover in Azure e di failback (ripristino) da Azure ai server host Hyper-V nel sito locale.
* Piani di ripristino con più VM per fare in modo che il failover dei carichi di lavoro delle applicazioni a più livelli venga eseguito contemporaneamente.

## <a name="azure-prerequisites"></a>Prerequisiti di Azure
* È necessario un account [Microsoft Azure](https://azure.microsoft.com/) . È possibile iniziare con una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Per archiviare i dati replicati è necessario un account di archiviazione di Azure. Nell'account deve essere abilitata la replica geografica. Dovrà trovarsi nella stessa area dell'insieme di credenziali di Azure Site Recovery ed essere associato alla stessa sottoscrizione. [Altre informazioni sull'Archiviazione di Azure](../storage/common/storage-introduction.md). Si noti che lo spostamento degli account di archiviazione creati con il [nuovo portale di Azure](../storage/common/storage-create-storage-account.md) tra gruppi di risorse non è supportato.
* È necessaria una rete virtuale di Azure in modo che le macchine virtuali di Azure siano connesse a una rete quando si esegue il failover dal sito primario.

## <a name="hyper-v-prerequisites"></a>Prerequisiti di Hyper-V
* Nel sito locale di origine sono necessari uno o più server che eseguono **Windows Server 2012 R2** e in cui sia installato il ruolo di Hyper-V o **Microsoft Hyper-V Server 2012 R2**. Questo server deve:
* Contenere una o più macchine virtuali.
* Essere connesso a Internet, in modo diretto o tramite proxy.
* Eseguire le correzioni descritte nell'articolo [2961977](https://support.microsoft.com/en-us/kb/2961977 "KB2961977").

## <a name="virtual-machine-prerequisites"></a>Prerequisiti delle macchine virtuali
Le macchine virtuali da proteggere devono essere conformi ai [Requisiti delle macchine virtuali di Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

## <a name="provider-and-agent-prerequisites"></a>Prerequisiti di provider e agente
Durante la distribuzione di Azure Site Recovery verranno installati il provider di Azure Site Recovery e l'agente Servizi di ripristino di Azure in ogni server Hyper-V. Si noti che:

* È consigliabile eseguire sempre le versioni più recenti del provider e dell'agente, disponibili nel portale di Site Recovery.
* Tutti i server Hyper-V di un insieme devono essere della stessa versione del provider e dell'agente.
* Il provider in esecuzione nel server si connette a Site Recovery via Internet. È possibile eseguire questa operazione senza un proxy, con le impostazioni proxy attualmente configurate nel server Hyper-V oppure con le impostazioni proxy personalizzate configurate durante l'installazione del provider. Assicurarsi che il server proxy da usare possa accedere a questi URL per la connessione ad Azure:

  * *.accesscontrol.windows.net
  * *.backup.windowsazure.com
  * *.hypervrecoverymanager.windowsazure.com
  * *. store.core.windows.net      
  * *.blob.core.windows.net
  - https://www.msftncsi.com/ncsi.txt
  - time.windows.com
  - time.nist.gov
* Consentire anche gli indirizzi IP descritti in [Azure Datacenter IP Ranges](https://www.microsoft.com/download/details.aspx?id=41653) e il protocollo HTTPS (443). È necessario consentire gli intervalli IP dell'area di Azure che si intende usare e quello degli Stati Uniti occidentali.

Questa immagine illustra i diversi canali e le porte di comunicazione usati da Site Recovery per la replica e l'orchestrazione

![Topologia B2A](./media/site-recovery-hyper-v-site-to-azure-classic/b2a-topology.png)

## <a name="step-1-create-a-vault"></a>Passaggio 1: Creare un insieme di credenziali
1. Accedere al [portale di gestione](https://portal.azure.com).
2. Espandere **Servizi dati** > **Servizi di ripristino** e fare clic su **Insieme di credenziali di Site Recovery**.
3. Fare clic su **Creare nuovo** > **Creazione rapida**.
4. In **Nome**immettere un nome descrittivo per identificare l'insieme di credenziali.
5. In **Region**selezionare l'area geografica per l'insieme di credenziali. Per verificare le aree geografiche supportate, vedere la sezione Disponibilità a livello geografico in [Prezzi di Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
6. Fare clic su **Create vault**.

    ![Nuovo insieme di credenziali](./media/site-recovery-hyper-v-site-to-azure-classic/vault.png)

Controllare la barra di stato per verificare che l'insieme di credenziali sia stato creato correttamente. L'insieme di credenziali verrà elencato come **Attivo** nella pagina principale di Servizi di ripristino.

## <a name="step-2-create-a-hyper-v-site"></a>Passaggio 2: Creare un sito Hyper-V
1. Nella pagina Servizi di ripristino fare clic sull'insieme di credenziali per aprire la pagina Avvio rapido. La pagina Avvio rapido può anche essere aperta in qualsiasi momento tramite l'icona.

    ![Avvio rapido](./media/site-recovery-hyper-v-site-to-azure-classic/quick-start-icon.png)
2. Dall'elenco a discesa selezionare **Tra un sito Hyper-V locale e Azure**.

    ![Scenario del sito di Hyper-V](./media/site-recovery-hyper-v-site-to-azure-classic/select-scenario.png)
3. In **Crea un sito Hyper-V** fare clic su **Crea sito Hyper-V**. Specificare un nome per il sito e salvare.

    ![Sito di Hyper-V](./media/site-recovery-hyper-v-site-to-azure-classic/create-site.png)

## <a name="step-3-install-the-provider-and-agent"></a>Passaggio 3: Installare Provider e agente
Installare il provider e l'agente in ogni server Hyper-V che include macchine virtuali da proteggere.

Se si desidera eseguire l’installazione in un cluster Hyper-V, eseguire i passaggi da 5 a 11 in ogni nodo del cluster di failover. Dopo aver registrato tutti i nodi e aver abilitato la protezione, le macchine virtuali saranno protette anche se migrano tra i nodi del cluster.

1. In **Prepara server Hyper-V** fare clic sul file **Scaricare una chiave di registrazione**.
2. Nella pagina **Scarica chiave di registrazione** fare clic su **Scarica** accanto al nome del sito. Scaricare il codice in un percorso sicuro a cui sia possibile accedere facilmente tramite il server Hyper-V. Il codice è valido per 5 giorni dal momento in cui viene generato.

    ![Registration key](./media/site-recovery-hyper-v-site-to-azure-classic/download-key.png)
3. Fare clic su **Scaricare il Provider** per ottenere la versione più recente.
4. Eseguire il file su ciascun server Hyper-V da registrare nell'insieme di credenziali. Il file installa due componenti:
   * **Provider di Azure Site Recovery**: gestisce le comunicazioni e l’orchestrazione tra il server Hyper-V e il portale di Azure Site Recovery.
   * **Agente di Servizi di ripristino di Azure**: gestisce il trasferimento dei dati tra le macchine virtuali in esecuzione sul server Hyper-V di origine e l'archiviazione di Azure.
5. In **Microsoft Update** è possibile fornire il consenso esplicito agli aggiornamenti. Se questa impostazione è abilitata, gli aggiornamenti del provider e dell'agente verranno installati in base ai criteri indicati in Microsoft Update.

    ![Microsoft Updates](./media/site-recovery-hyper-v-site-to-azure-classic/provider1.png)
6. In **Installazione** specificare la posizione di installazione di Provider e agente nel server Hyper-V.

    ![Posizione di installazione](./media/site-recovery-hyper-v-site-to-azure-classic/provider2.png)
7. Al termine dell'installazione, proseguire con la configurazione per registrare il server nell'insieme di credenziali.
8. Nella pagina **Impostazioni insieme di credenziali** fare clic su **Sfoglia** per selezionare il file di chiave. Specificare la sottoscrizione di Azure Site Recovery, il nome dell'insieme di credenziali e il sito Hyper-V a cui appartiene il server Hyper-V.

    ![Server registration](./media/site-recovery-hyper-v-site-to-azure-classic/provider8.PNG)
9. Nella pagina **Connessione Internet** specificare la modalità di connessione tra Provider e Azure Site Recovery. Selezionare **Usa impostazioni proxy del sistema predefinite** per usare le impostazioni di connessione a Internet predefinite configurate nel server. Se non si specifica un valore, verranno utilizzate le impostazioni predefinite.

   ![Internet Settings](./media/site-recovery-hyper-v-site-to-azure-classic/provider7.PNG)
10. La procedura di registrazione ha inizio e il server viene registrato nell'insieme di credenziali.

    ![Server registration](./media/site-recovery-hyper-v-site-to-azure-classic/provider15.PNG)
11. Al termine della registrazione, i metadati del server Hyper-V vengono recuperati da Azure Site Recovery e il server viene visualizzato nella scheda **Siti Hyper-V** della pagina **Server** all'interno dell'insieme di credenziali.

### <a name="install-the-provider-from-the-command-line"></a>Installare il provider dalla riga di comando
In alternativa è possibile installare il provider di Azure Site Recovery dalla riga di comando. Usare questo metodo per installare il provider in un computer che esegue Windows Server Core 2012 R2. Eseguire dalla riga di comando procedendo come indicato di seguito:

1. Scaricare il file di installazione del provider e il codice di registrazione in una cartella, ad esempio C:\ASR.
2. Eseguire il prompt dei comandi come amministratore e digitare:

        C:\Windows\System32> CD C:\ASR
        C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
3. Installare quindi il provider eseguendo:

        C:\ASR> setupdr.exe /i
4. Eseguire questo comando per completare la registrazione:

        CD C:\Program Files\Microsoft Azure Site Recovery Provider
        C:\Program Files\Microsoft Azure Site Recovery Provider\> DRConfigurator.exe /r  /Friendlyname <friendly name of the server> /Credentials <path of the credentials file> /EncryptionEnabled <full file name to save the encryption certificate>         

I parametri includono:

* **/Credentials**: specificare il percorso della chiave di registrazione scaricata.
* **/FriendlyName**: specificare un nome per identificare il server host Hyper-V. Questo nome verrà visualizzato nel portale.
* **/EncryptionEnabled**: facoltativo. Specificare se devono essere crittografate le macchine virtuali di replica in Azure (crittografia dei dati inattivi).
* **/proxyAddress**; **/proxyport**; **/proxyUsername**; **/proxyPassword**: facoltativo. Se si vuole usare un proxy personalizzato o se il proxy esistente richiede l'autenticazione, specificare i parametri del proxy.

## <a name="step-4-create-an-azure-storage-account"></a>Passaggio 4: Creare un account di archiviazione di Azure
* Nella pagina **Prepara risorse** selezionare **Crea account di archiviazione** per creare un account di archiviazione di Azure, se non ne è ancora stato creato uno. Nell'account deve essere abilitata la replica geografica. Dovrà trovarsi nella stessa area dell'insieme di credenziali di Azure Site Recovery ed essere associato alla stessa sottoscrizione.

    ![Crea account di archiviazione](./media/site-recovery-hyper-v-site-to-azure-classic/create-resources.png)

> [!NOTE]
> 1. Non è supportato lo spostamento degli account di archiviazione creati con il [nuovo portale di Azure](../storage/common/storage-create-storage-account.md) tra gruppi di risorse.
> 2. [La migrazione degli account di archiviazione](../azure-resource-manager/resource-group-move-resources.md) all'interno dei gruppi di risorse con la stessa sottoscrizione o all'interno delle sottoscrizioni non è supportata per gli account di archiviazione usati per la distribuzione di Site Recovery.
>

## <a name="step-5-create-and-configure-protection-groups"></a>Passaggio 5: Creare e configurare gruppi di protezione 
I gruppi di protezione dati sono raggruppamenti logici di macchine virtuali che si desidera proteggere utilizzando le stesse impostazioni di protezione. Se si applicano specifiche impostazioni di protezione a un gruppo, queste vengono automaticamente applicate a tutte le macchine virtuali aggiunte al gruppo.

1. In **Crea e configura gruppi di protezione** fare clic su **Crea gruppo di protezione dati**. Se non risultano soddisfatti tutti i requisiti, viene visualizzato un messaggio in cui è disponibile l'opzione **Visualizza dettagli** che consente di ottenere maggiori informazioni.
2. Nella scheda **Gruppo di protezione dati** , aggiungere un gruppo di protezione. Specificare un nome, il sito Hyper-V di origine, **Azure**di destinazione, il nome della sottoscrizione di Azure Site Recovery e l'account di archiviazione di Azure.

    ![Gruppo protezione dati](./media/site-recovery-hyper-v-site-to-azure-classic/protection-group.png)
3. In **Impostazioni di replica** impostare la **Frequenza di copia** per specificare la frequenza di sincronizzazione dei dati differenziali tra origine e destinazione. È possibile impostare su 30 secondi, 5 minuti o 15 minuti.
4. In **Mantieni punti di ripristino** specificare il numero di ore della cronologia di ripristino da archiviare.
5. In **Frequenza di snapshot coerenti con l’applicazione** è possibile specificare se eseguire snapshot che utilizzano il  servizio Copia Shadow del volume (VSS) per garantire che le applicazioni siano coerenti durante la creazione dello snapshot. Per impostazione predefinita questi snapshot non vengono eseguiti. Se si imposta un valore, questo deve essere inferiore al numero di punti di ripristino aggiuntivi configurati. Questa opzione è supportata solo se nella macchina virtuale è in esecuzione un sistema operativo Windows.
6. In **Ora di inizio replica iniziale** specificare quando la replica iniziale delle macchine virtuali nel gruppo di protezione deve essere inviata in Azure.

    ![Gruppo protezione dati](./media/site-recovery-hyper-v-site-to-azure-classic/protection-group2.png)

## <a name="step-6-enable-virtual-machine-protection"></a>Passaggio 6: Abilitare la protezione delle macchine virtuali
Aggiungere macchine virtuali a un gruppo di protezione per abilitare la protezione.

> [!NOTE]
> La protezione di macchine virtuali che eseguono Linux con un indirizzo IP statico non è supportata.
>
>

1. Nella scheda **Computer** del gruppo di protezione dati, fare clic su **Per proteggere le macchine virtuali, aggiungerle ai gruppi di protezione**.
2. Nella pagina **Abilita protezione macchine virtuali** selezionare le macchine virtuali da proteggere.

    ![Abilitare la protezione delle macchine virtuali](./media/site-recovery-hyper-v-site-to-azure-classic/add-vm.png)

    Vengono avviati i processi di abilitazione della protezione, Nella scheda **Processi** è possibile monitorare l'avanzamento. Dopo l'esecuzione del processo di finalizzazione della protezione la macchina virtuale è pronta per il failover.
3. Dopo la configurazione della protezione è possibile:

   * Visualizzare le macchine virtuali in **Elementi protetti** > **Gruppi protezione dati** > *nome_gruppoprotezione* > **Macchine virtuali** Nella scheda **Proprietà** è possibile eseguire il drill-down fino ai dettagli della macchina.
   * Configurare le proprietà di failover per una macchina virtuale in **Elementi protetti** > **Gruppi protezione dati** > *nome_gruppodiprotezione* > **Macchine virtuali** *nome_macchina_virtuale* > **Configura**. È possibile configurare:

     * **Nome**: il nome della macchina virtuale in Azure.
     * **Dimensioni**: le dimensioni della macchina virtuale di destinazione che esegue il failover.

       ![Configurare le proprietà della macchina virtuale](./media/site-recovery-hyper-v-site-to-azure-classic/vm-properties.png)
   * Configurare altre impostazioni della macchina virtuale in *Elementi protetti** > **Gruppi di protezione** > *nome_gruppodiprotezione* > **Macchine virtuali***nome_macchina_virtuale* > **Configura**, tra cui:

     * **Schede di rete**: il numero di schede di rete dipende dalle dimensioni specificate per la macchina virtuale di destinazione. Per il numero di schede di rete supportate dalle dimensioni della macchina virtuale, vedere le [specifiche sulle dimensioni delle macchine virtuali](../virtual-machines/linux/sizes.md) .

       Quando si modificano le dimensioni di una macchina virtuale e si salvano le impostazioni, il numero di schede di rete cambia alla successiva apertura della pagina **Configura** . Il numero di schede di rete delle macchine virtuali di destinazione corrisponde minimo al numero di schede di rete nella macchina virtuale di origine e al numero massimo di schede di rete supportate dalla dimensione della macchina virtuale selezionata. Questo concetto è illustrato di seguito:

       * Se il numero di schede di rete nella macchina di origine è minore o uguale al numero di schede consentite per la macchina di destinazione, la destinazione avrà lo stesso numero di schede dell’origine.
       * Se il numero di schede per la macchina virtuale di origine supera il numero consentito per le dimensioni di destinazione, verrà utilizzata la dimensione di destinazione massima.
       * Ad esempio, se una macchina di origine dispone di due schede di rete e le dimensioni della macchina di destinazione ne supportano quattro, la macchina di destinazione avrà due schede. Se la macchina di origine dispone di due schede ma le dimensioni di destinazione supportate ne consentono solo una, la macchina di destinazione avrà una sola scheda.

     * **Rete di Azure**: specificare la rete in cui la macchina virtuale deve eseguire il failover. Se la macchina virtuale ha più schede di rete, tutte le schede devono essere connesse alla stessa rete di Azure.
     * **Subnet** : per ogni scheda di rete nella macchina virtuale, selezionare la subnet nella rete di Azure a cui deve connettersi la macchina dopo il failover.
     * **Indirizzo IP di destinazione**: se la scheda di rete della macchina virtuale di origine è configurata per usare un indirizzo IP statico, è possibile specificare l'indirizzo IP per la macchina virtuale di destinazione per assicurarsi che la macchina abbia lo stesso indirizzo IP dopo il failover.  Se non si specifica un indirizzo IP, al momento del failover verrà assegnato un qualsiasi indirizzo disponibile. Se si specifica un indirizzo che si sta usando, il failover avrà esito negativo.

     > [!NOTE]
     > La [migrazione di reti](../azure-resource-manager/resource-group-move-resources.md) all'interno dei gruppi di risorse con la stessa sottoscrizione o all'interno delle sottoscrizioni non è supportata per le reti usate per la distribuzione di Site Recovery.
     >

     ![Configurare le proprietà della macchina virtuale](./media/site-recovery-hyper-v-site-to-azure-classic/multiple-nic.png)




## <a name="step-7-create-a-recovery-plan"></a>Passaggio 7: Creare un piano di ripristino
Per testare la distribuzione è possibile eseguire un failover di test per una singola macchina virtuale o un piano di ripristino che contenga una o più macchine virtuali. [Altre informazioni](site-recovery-create-recovery-plans.md) sulla creazione di un piano di ripristino.

## <a name="step-8-test-the-deployment"></a>Passaggio 8: Testare la distribuzione
È possibile eseguire un failover di test in Azure in due modi.

* **Failover di test senza una rete di Azure**: questo tipo di failover di test verifica che la macchina virtuale sia rilevata correttamente in Azure. La macchina virtuale non sarà connessa ad alcuna rete di Azure dopo il failover.
* **Failover di test con una rete di Azure**: questo tipo di failover verifica che l'intero ambiente di replica venga rilevato come previsto e che le macchine virtuali di cui viene eseguito il failover si connettano alla rete di Azure di destinazione specificata. Si noti che nel failover di test la subnet della macchina virtuale di test viene rilevata in base alla subnet della macchina virtuale di replica. Questo comportamento è diverso dalla replica normale quando la subnet della macchina virtuale di replica si basa sulla subnet della macchina virtuale di origine.

Per eseguire un failover di test senza specificare una rete di Azure non è necessario preparare l'ambiente.

Per eseguire un failover di test con una rete di Azure di destinazione, è necessario creare una nuova rete di Azure isolata dalla rete di Azure di produzione, ovvero il comportamento predefinito quando si crea una nuova rete in Azure. Per altre informazioni dettagliate, vedere [Eseguire un failover di test](site-recovery-failover.md) .

Per testare completamente la replica e la distribuzione di rete è necessario configurare l'infrastruttura in modo che la macchina virtuale replicata funzioni come previsto. Un modo di procedere consiste nel configurare una macchina virtuale come controller di dominio con DNS ed eseguirne la replica in Azure usando Site Recovery per crearla nella rete di test eseguendo un failover di test.  [Altre informazioni](site-recovery-active-directory.md#test-failover-considerations) e considerazioni sul failover di test per Active Directory.

Eseguire il failover di test come descritto di seguito:

> [!NOTE]
> Per ottenere prestazioni ottimali quando si esegue un failover in Azure, assicurarsi di aver installato l'agente di Azure nel computer protetto. Questo consente un avvio più veloce e facilita anche la diagnosi nel caso di problemi. L'agente Linux è disponibile [qui](https://github.com/Azure/WALinuxAgent), mentre l'agente Windows è disponibile [qui](http://go.microsoft.com/fwlink/?LinkID=394789)
>
>

1. Nella scheda **Piani di ripristino** selezionare il piano e fare clic su **Failover di test**.
2. Nella pagina **Conferma failover di test** selezionare **Nessuno** o una rete di Azure specifica.  Tenere presente che se si seleziona **Nessuno** , il failover di test verifica che la macchina virtuale venga replicata correttamente in Azure ma non controlla la configurazione della rete di replica.

    ![Failover di test](./media/site-recovery-hyper-v-site-to-azure-classic/test-nonetwork.png)
3. Nella scheda **Processi** è possibile tenere traccia dello stato di avanzamento del failover. Dovrebbe anche essere possibile vedere la replica di test della macchina virtuale nel portale di Azure. Se è stato impostato l'accesso alle macchine virtuali dalla rete locale, è possibile inizializzare una Connessione Desktop remoto alla macchina virtuale.
4. Quando il processo di failover raggiunge la **fase conclusiva**, fare clic su **Completa test** per completare il failover di test. È possibile eseguire il drill-down fino alla scheda **Processo** per tenere traccia dello stato e dell’avanzamento del failover ed eseguire eventuali azioni necessarie.
5. Al termine del processo di failover, nel portale di Azure sarà possibile visualizzare la replica del test eseguito sulla macchina virtuale. Se è stato impostato l'accesso alle macchine virtuali dalla rete locale, è possibile inizializzare una Connessione Desktop remoto alla macchina virtuale.

   1. Verificare che le macchine virtuali vengano avviate correttamente.
   2. Per eseguire la connessione alla macchina virtuale in Azure tramite Desktop remoto dopo il failover, abilitare Connessione Desktop remoto sulla macchina virtuale prima di eseguire il failover di test. È necessario anche aggiungere un endpoint RDP nella macchina virtuale. A tale scopo, è possibile usare un [runbook di automazione di Azure](site-recovery-runbook-automation.md) .
   3. Dopo il failover, se si utilizza un indirizzo IP pubblico per connettersi alla macchina virtuale in Azure tramite Desktop remoto, verificare che non siano definiti criteri di dominio che impediscono la connessione a una macchina virtuale utilizzando un indirizzo pubblico.
6. Al completamento del test, procedere come segue:

   * Fare clic su **Il failover di test è completo**. Pulire l'ambiente di test per spegnere automaticamente ed eliminare la macchine virtuali di test.
   * Fare clic su **Note** per registrare e salvare eventuali commenti associati al failover di test.
7. Quando il processo di failover raggiunge la **fase conclusiva** , completare la verifica come segue:
   1. Visualizzare la macchina virtuale di replica nel portale di Azure. Verificare che la macchina virtuale venga avviata correttamente.
   2. Se è stato impostato l'accesso alle macchine virtuali dalla rete locale, è possibile inizializzare una Connessione Desktop remoto alla macchina virtuale.
   3. Fare clic su **Completa il test** per portarlo a termine.
   4. Fare clic su **Note** per registrare e salvare eventuali commenti associati al failover di test.
   5. Fare clic su **Il failover di test è completo**. Pulire l'ambiente di test per spegnere automaticamente ed eliminare la macchina virtuale di test.

## <a name="next-steps"></a>Passaggi successivi
Dopo aver configurato correttamente la distribuzione, leggere [altre informazioni](site-recovery-failover.md) sul failover.
