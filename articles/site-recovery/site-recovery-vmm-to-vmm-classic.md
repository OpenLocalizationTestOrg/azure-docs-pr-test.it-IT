---
title: macchine virtuali Hyper-V nel sito secondario VMM tooa (classico di Azure) aaaReplicate | Documenti Microsoft
description: In questo articolo viene descritto come macchine virtuali Hyper-V in VMM tooreplicate cloud sito VMM secondario tooa con Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: a63acba3-8fb3-4926-aa29-b1e64a765681
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: raynew
ms.openlocfilehash: fe551e1f741579044f540ea0e50a6e36d48133ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site"></a>Replicare le macchine virtuali Hyper-V in VMM cloud tooa VMM del sito secondario
> [!div class="op_single_selector"]
> * [Portale di Azure](site-recovery-vmm-to-vmm.md)
> * [Portale classico](site-recovery-vmm-to-vmm-classic.md)
> * [PowerShell - Gestione risorse](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

servizio Azure Site Recovery Hello contribuisce tooyour continuità aziendale e strategia di ripristino di emergenza per la replica di orchestrazione, failover e il ripristino delle macchine virtuali e server fisici. Macchine possono essere replicati tooAzure o tooa locale secondario data center. Per una rapida panoramica, leggere [Che cos'è Azure Site Recovery?](site-recovery-overview.md)

## <a name="overview"></a>Panoramica
In questo articolo viene descritto come tooreplicate Hyper-V le macchine virtuali in Hyper-V host server gestiti nel sito VMM di VMM cloud toosecondary usando Azure Site Recovery.

articolo Hello sono inclusi i prerequisiti, Mostra è come tooset di un insieme di credenziali di Site Recovery, installa hello Provider di Azure Site Recovery nell'origine e il server VMM di destinazione, registrare i server hello nell'insieme di credenziali hello, configurare le impostazioni di protezione per i cloud VMM e quindi abilitare protezione per le macchine virtuali Hyper-V. Completare test toomake failover hello che tutto funzioni come previsto.

Inviare eventuali commenti o domande nella parte inferiore di hello di questo articolo, o di hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="architecture"></a>Architettura
immagine di Hello seguente vengono illustrati i canali di comunicazione diversi hello e le porte utilizzate da Azure Site Recovery per la replica e orchestrazione

![Topologia E2E](./media/site-recovery-vmm-to-vmm-classic/e2e-topology.png)

## <a name="before-you-start"></a>Prima di iniziare
Assicurarsi che siano rispettati i prerequisiti seguenti:

| **Prerequisiti** | **Dettagli** |
| --- | --- |
| **Azzurro** |È necessario un account [Microsoft Azure](https://azure.microsoft.com/) . È possibile iniziare con una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/). [Altre informazioni](https://azure.microsoft.com/pricing/details/site-recovery/) sui prezzi di Site Recovery. |
| **VMM** |È necessario almeno un server VMM.<br/><br/>server VMM Hello deve essere in esecuzione almeno System Center 2012 SP1 con aggiornamenti cumulativi più recenti di hello.<br/><br/>Se si desidera tooset la protezione con un singolo server VMM, è necessario almeno due cloud configurati nei server hello.<br/><br/>Se si desidera protezione toodeploy con due server VMM, ogni server deve essere almeno un cloud configurato nel server VMM primario hello desiderato tooprotect e un cloud configurato nel server VMM secondario hello desiderato toouse per la protezione e ripristino<br/><br/>Tutti i cloud VMM è necessario impostare profilo funzionalità di Hyper-V hello.<br/><br/>cloud di origine Hello che si desidera tooprotect deve contenere uno o più gruppi host VMM. |
| **Hyper-V** |È necessario uno o più server host Hyper-V in hello primari e secondari gruppi host VMM e uno o più macchine virtuali in ogni server host Hyper-V.<br/><br/>Hello server Hyper-V host e di destinazione deve essere in esecuzione almeno Windows Server 2012 con il ruolo Hyper-V hello e avere hello installati aggiornamenti più recenti.<br/><br/>Qualsiasi server Hyper-V contenente le macchine virtuali desiderate tooprotect deve trovarsi in un cloud VMM.<br/><br/>Se si esegue Hyper-V in un cluster, si noti che il broker del cluster non viene creato automaticamente se viene usato un cluster basato su indirizzi IP statici. È necessario un gestore cluster hello tooconfigure manualmente. [Altre informazioni](https://www.petri.com/use-hyper-v-replica-broker-prepare-host-clusters) nel post di blog di Aidan Finn. |
| **Mapping di rete** |È possibile configurare toomake mapping di rete assicurarsi che le macchine virtuali replicate vengono posizionate in server host di Hyper-V secondario dopo il failover, e che possano essere connesse a reti VM tooappropriate. Se non si configura il mapping di rete, le macchine virtuali di replica sarà connessa tooany rete dopo il failover.<br/><br/>tooset mapping di rete durante la distribuzione, assicurarsi che hello le macchine virtuali nel server host Hyper-V di origine di hello siano connesso tooa rete VM di VMM. La rete deve essere collegato tooa la rete logica associata al cloud hello. < br /<br/>cloud di destinazione Hello nel server VMM secondario hello utilizzati per il ripristino deve avere una rete VM corrispondente configurata e deve essere a sua volta collegato tooa rete logica associata al cloud di destinazione hello corrispondente. |
| **Mapping dell'archiviazione** |Per impostazione predefinita quando si replica una macchina virtuale in un origine Hyper-V host server tooa Hyper-V host server di destinazione, i dati replicati archiviati nel percorso predefinito di hello indicato per host Hyper-V di destinazione hello in Hyper-V Manager. Per un maggiore controllo sulla posizione di archiviazione dei dati replicati, configurare il mapping di archiviazione<br/><br/> archiviazione tooconfigure mapping, è necessario tooset classificazioni di archiviazione nell'origine hello e i server VMM di destinazione prima di iniziare la distribuzione. |

## <a name="step-1-create-a-site-recovery-vault"></a>Passaggio 1: creare un insieme di credenziali di Ripristino sito
1. Accedi toohello [portale di gestione](https://portal.azure.com) dal server VMM hello desiderato tooregister.
2. Espandere **Servizi dati** > **Servizi di ripristino** e fare clic su **Insieme di credenziali di Site Recovery**.
3. Fare clic su **Creare nuovo** > **Creazione rapida**.
4. In **nome**, immettere un insieme di credenziali di nome descrittivo tooidentify hello.
5. In **area** selezionare hello area geografica per l'insieme di credenziali hello. aree toocheck supportato vedere aree geografiche disponibili in [dettagli prezzi di Azure Site Recovery](http://go.microsoft.com/fwlink/?LinkId=389880).
6. Fare clic su **Create vault**.

    ![Create vault](./media/site-recovery-vmm-to-vmm-classic/create-vault.png)

Controllo stato hello barra tale insieme di credenziali hello è stato creato. insieme di credenziali Hello verrà elencato come **Active** nella pagina principale di servizi di ripristino hello.

## <a name="step-2-generate-a-vault-registration-key"></a>Passaggio 2: generare una chiave di registrazione dell'insieme di credenziali
Generare una chiave di registrazione nell'insieme di credenziali hello. Dopo aver scaricato hello Provider di Azure Site Recovery e installarlo nel server VMM hello, si utilizzerà il server VMM di hello tooregister chiave nell'insieme di credenziali hello.

1. In hello **servizi di ripristino** pagina, fare clic su pagina di avvio rapido di hello insieme di credenziali tooopen hello. Guida introduttiva può anche essere aperto in qualsiasi momento facendo clic sull'icona hello.

    ![Quick Start Icon](./media/site-recovery-vmm-to-vmm-classic/quick-start-icon.png)
2. Nell'elenco a discesa hello, selezionare **tra due siti VMM locali**.
3. In **Preparare i server VMM** fare clic sul file **Genera file della chiave di registrazione**. file di chiave Hello viene generato automaticamente ed è valido per 5 giorni dopo la sua creazione. Se si accede non di hello portale di Azure da un server VMM hello, è necessario toocopy questo toohello di file server.

    ![Chiave di registrazione](./media/site-recovery-vmm-to-vmm-classic/register-key.png)

## <a name="step-3-install-hello-azure-site-recovery-provider"></a>Passaggio 3: Installare il Provider di Azure Site Recovery hello
1. In hello **avvio rapido** pagina **server VMM preparare**, fare clic su **Scarica Provider Microsoft Azure Site Recovery per l'installazione nei server VMM** tooobtain hello più recente versione del file di installazione di Provider hello.
2. Eseguire questo file nel server VMM di origine hello.

   > [!NOTE]
   > Se VMM è distribuito in un cluster e si sta installando hello Provider per hello prima installarlo in un nodo attivo e di fine server VMM nell'insieme di credenziali hello hello installazione tooregister hello. Installare quindi hello Provider in hello altri nodi. Si noti che se si esegue l'aggiornamento di hello Provider, è necessario tooupgrade in tutti i nodi, in quanto tutti dovrebbero essere in esecuzione hello stessa versione del Provider.
   >
   >
3. programma di installazione Hello alcuni **verifica prerequisiti** e richieste hello toostop autorizzazione VMM toobegin l'installazione del Provider del servizio. Hello servizio VMM verrà riavviato automaticamente al completamento dell'installazione. Se si sta installando in un cluster VMM, che sarà richiesto il ruolo Cluster toostop hello.
4. In **Microsoft Update** è possibile fornire il consenso esplicito agli aggiornamenti. Con questa impostazione abilitata Provider aggiornamenti verranno installati in base a criteri di Microsoft Update tooyour.

    ![Microsoft Updates](./media/site-recovery-vmm-to-vmm-classic/ms-update.png)
5. il percorso di installazione di Hello è troppo**<SystemDrive>\Programmi\Microsoft System Center 2012 R2\Virtual Machine Manager\bin**. Fare clic su hello toostart pulsante Install installa hello Provider.

    ![InstallLocation](./media/site-recovery-vmm-to-vmm-classic/install-location.png)
6. Dopo aver hello Provider è installato, fare clic su **registrare** server hello tooregister nell'insieme di credenziali hello.

    ![InstallComplete](./media/site-recovery-vmm-to-vmm-classic/install-complete.png)
7. In **nome insieme di credenziali**, verificare il nome di hello dell'insieme di credenziali hello in cui hello server verrà registrato. Fare clic su *Avanti*.

    ![Server registration](./media/site-recovery-vmm-to-vmm-classic/vaultcred.PNG)
8. In **connessione Internet** specificare hello come Provider in esecuzione in VMM hello toohello Internet si connette a server. Selezionare **Connetti con impostazioni proxy esistenti** toouse hello Internet impostazioni di connessione predefinite configurate nel server di hello.

    ![Internet Settings](./media/site-recovery-vmm-to-vmm-classic/proxydetails.PNG)

   * Se si desidera toouse un proxy personalizzato è necessario configurarlo prima di installare hello Provider. Quando si configurano impostazioni proxy personalizzate connessione proxy di hello toocheck verrà eseguito un test.
   * Se si utilizza un proxy personalizzato, o il proxy predefinito richiede l'autenticazione è necessario tooenter hello proxy dettagli, inclusi la porta e indirizzo proxy hello.
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
13. Fare clic su **Avanti** processo hello toocomplete. Dopo la registrazione, i metadati dal server VMM hello vengono recuperati da Azure Site Recovery. server Hello viene visualizzato nel **server VMM** > **server** nell'insieme di credenziali hello.

    ![Server](./media/site-recovery-vmm-to-vmm-classic/provider13.PNG)

### <a name="command-line-installation"></a>Installazione dalla riga di comando
Provider di Azure Site Recovery Hello può anche essere installato dalla riga di comando hello. Questo metodo può essere provider hello tooinstall utilizzati in un Server CORE per Windows Server 2012 R2.

1. Scaricare hello Provider e registrazione tooa chiave cartella di installazione. ad esempio C:\ASR.
2. Arrestare hello servizio System Center Virtual Machine Manager
3. Estrarre il programma di installazione di hello Provider, eseguire questi comandi dal prompt dei comandi con **amministratore** privilegi:

        C:\Windows\System32> CD C:\ASR
        C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
4. Installare il provider di hello eseguendo:

        C:\ASR> setupdr.exe /i
5. Registrazione provider hello eseguendo:

        CD C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin
        C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file> /EncryptionEnabled <full file name toosave hello encryption certificate>     

Dove hello parametri sono:

* **/ Credenziali**: parametro obbligatorio che specifica il percorso di hello in cui hello Trova file di chiave di registrazione  
* **/ FriendlyName**: parametro obbligatorio per il nome del server host Hyper-V hello visualizzata nel portale di Azure Site Recovery hello hello.
* **/ EncryptionEnabled**: parametro facoltativo che è necessario toouse solo in hello VMM tooAzure Scenario se si richiede la crittografia delle macchine virtuali inattivi in Azure. Verificare che il nome di hello del file hello è fornire ha un **PFX** estensione.
* **/ProxyAddress**: parametro facoltativo che specifica l'indirizzo di hello del server proxy hello.
* **/ProxyPort**: parametro facoltativo che specifica la porta del server proxy hello hello.
* **/proxyUsername**: parametro facoltativo che specifica il nome utente di hello Proxy (se proxy richiede l'autenticazione).
* **/proxyPassword**: parametro facoltativo che specifica hello Password per l'autenticazione con il server proxy hello (se proxy richiede l'autenticazione).  

## <a name="step-4-configure-cloud-protection-settings"></a>Passaggio 4: configurare le impostazioni di protezione del cloud
Dopo la registrazione dei server VMM, sarà possibile configurare le impostazioni di protezione del cloud. Se è abilitata l'opzione di hello **Sincronizza i dati cloud con insieme di credenziali hello** durante l'installazione di Provider hello conseguenza verranno visualizzati tutti i cloud nel server VMM hello in hello **elementi protetti** scheda nell'insieme di credenziali hello. Se non è stato è possibile sincronizzare un cloud specifico con Azure Site Recovery in hello **generale** scheda della pagina delle proprietà di hello cloud nella console VMM hello.

![Cloud pubblicato](./media/site-recovery-vmm-to-vmm-classic/clouds-list.png)

1. Nella pagina introduttiva hello, fare clic su **impostare la protezione per i cloud VMM**.
2. In hello **cloud VMM** selezionare cloud hello tooconfigure desiderato e quindi passare toohello **configurazione** scheda.
3. In **Destinazione** selezionare **VMM**.
4. In **percorso di destinazione**, selezionare hello server VMM locale che gestisce il cloud hello da toouse per il ripristino.
5. In **cloud di destinazione**, selezionare il cloud di destinazione hello da toouse per il failover delle macchine virtuali nel cloud di origine hello. Si noti che:

   * Si consiglia di selezionare un cloud di destinazione che soddisfa i requisiti di ripristino per hello è possibile proteggere le macchine virtuali.
   * Un cloud può appartenere solo tooa coppia di cloud singolo, ad esempio un database primario o un cloud di destinazione.
6. In **Frequenza di copia**specificare la frequenza di sincronizzazione dei dati tra i percorsi di origine e di destinazione. Si noti che questa impostazione è rilevante solo quando l'host Hyper-V hello è in esecuzione Windows Server 2012 R2. Per gli altri server viene usata un'impostazione predefinita pari a cinque minuti.
7. In **punti di ripristino aggiuntivi**, specificare se si desidera toocreate altri punti. valore predefinito zero Hello indica che solo hello ultimo punto di ripristino per una macchina virtuale primaria viene archiviato in un server host di replica. Si noti che, per abilitare più punti di ripristino, è necessario ulteriore spazio di archiviazione per gli snapshot hello archiviati in corrispondenza di ogni punto di ripristino. Per impostazione predefinita, i punti di ripristino vengono creati ogni ora, in modo che in ogni punto siano contenuti dati per un periodo di tempo di un'ora. valore di punto di ripristino Hello assegnate per macchina virtuale hello nella console VMM hello non deve essere minore di hello valore assegnato nella console di Azure Site Recovery hello.
8. In **frequenza degli snapshot coerenti con l'applicazione**, specificare la frequenza snapshot coerenti dell'applicazione toocreate. Hyper-V usa due tipi di snapshot, uno snapshot standard che fornisce uno snapshot incrementale dell'intera macchina virtuale di hello e uno snapshot coerente dell'applicazione che accetta uno snapshot del punto nel tempo dei dati dell'applicazione hello macchina virtuale hello. Snapshot coerenti dell'applicazione usare tooensure del servizio Copia Shadow del Volume (VSS) che le applicazioni sono in uno stato coerente durante hello snapshot. Si noti che se si abilita snapshot coerenti dell'applicazione, influisce negativamente sulle prestazioni di hello delle applicazioni in esecuzione in macchine virtuali di origine. Verificare che il valore di hello impostato è minore hello numero di punti di ripristino aggiuntivi configurati.

    ![Configurare le impostazioni di protezione](./media/site-recovery-vmm-to-vmm-classic/cloud-settings.png)
9. In **Compressione trasferimento dati**specificare se i dati replicati che vengono trasferiti devono essere compressi.
10. In **autenticazione**, specificare come viene autenticato il traffico tra hello primario e i server host Hyper-V di ripristino. Selezionare HTTPS a meno che sia stato configurato un ambiente Kerberos funzionante. Azure Site Recovery configura automaticamente i certificati per l'autenticazione HTTPS. Non è necessaria alcuna configurazione manuale. Se si seleziona Kerberos, verrà usato un ticket Kerberos per l'autenticazione reciproca dei server host hello. Per impostazione predefinita, porte 8083 e 8084 (per i certificati) sono aperte in hello Windows Firewall nei server host Hyper-V di hello. Questa impostazione è rilevante solo per i server host Hyper-V in esecuzione su Windows Server 2012 R2.
11. In **porta**, modificare il numero di porta hello su quale origine hello e ascolto computer host per il traffico di replica di destinazione. È ad esempio possibile modificare l'impostazione di hello se si desidera tooapply Quality of Service (QoS) rete limitazione larghezza di banda per il traffico di replica. Verificare che la porta hello non sia usata da un'altra applicazione e che sia aperta nelle impostazioni firewall hello.
12. In **il metodo di replica**, specificare come verrà gestita, prima che la replica normale venga avviata la replica iniziale dei dati da posizioni di origine tootarget hello:

    * **Rete**, ovvero la copia dei dati in rete hello può richiedere tempi lunghi e risorse. È consigliabile utilizzare questa opzione se cloud hello contiene macchine virtuali con dischi rigidi virtuali relativamente piccoli e se hello sito primario sia connesso toohello secondario tramite una connessione con larghezza di banda ampia. È possibile specificare che copia hello deve avviare immediatamente oppure selezionare un'ora. Se si usa la replica tramite la rete, è consigliabile pianificarla durante le fasce orarie di minore attività.
    * **Non in linea**, questo metodo specifica che la replica iniziale hello verrà eseguita utilizzando supporti esterni. È utile se si desidera tooavoid un calo delle prestazioni di rete, oppure per percorsi remoti a livello geografico. toouse questo metodo specificare il percorso di esportazione di hello nel cloud di origine hello e hello importazione nel cloud di destinazione hello. Quando si abilita la protezione per una macchina virtuale, il disco rigido virtuale di hello è copiato toohello specificato percorso di esportazione. Si inviarlo toohello del sito di destinazione e copiarlo toohello percorso di importazione. Hello sistema copie hello importati informazioni toohello macchine virtuali di replica.
13. Selezionare **Elimina macchina virtuale di Replica** toospecify che hello macchina virtuale di replica deve essere eliminata se si interrompe la protezione macchina virtuale hello selezionando hello **eliminare la protezione dati per la macchina virtuale hello**  opzione nella scheda macchine virtuali hello delle proprietà cloud hello. Con questa impostazione è abilitata, quando si disabilita la macchina virtuale di protezione hello viene rimossa da Azure Site Recovery, hello le impostazioni di Site Recovery per la macchina virtuale hello vengono rimosse nella console VMM hello e hello replica viene eliminata.

    ![Configurare le impostazioni di protezione](./media/site-recovery-vmm-to-vmm-classic/cloud-settings-replica.png)

Dopo aver salvato le impostazioni di hello un processo verrà creato e può essere monitorato nella hello **processi** scheda. Tutti i server host Hyper-V in cloud di origine VMM hello verranno configurati per la replica. Impostazioni cloud possono essere modificate in hello **configura** scheda. Se si desidera percorso di destinazione hello toomodify o cloud di destinazione è necessario rimuovere la configurazione cloud hello e, successivamente, riconfigurare il cloud hello.

### <a name="prepare-for-offline-initial-replication"></a>Preparare la replica iniziale offline
È necessario hello toodo seguente tooprepare azioni per la replica iniziale offline:

* Nel server di origine hello, specificare il percorso dal quale hello esportazione dei dati avrà luogo. Assegnare il controllo completo per le autorizzazioni di condivisione e NTFS toohello di servizio VMM nel percorso di esportazione hello. Nel server di destinazione hello, specificare il percorso da cui importare i dati di hello si verificherà. Assegnare hello delle stesse autorizzazioni su questo percorso di importazione.
* Se hello importare o percorso di esportazione è condiviso, assegnare l'appartenenza al gruppo Administrator, Power User, Print Operator o Server Operators per l'account del servizio VMM hello nel computer remoto hello in cui hello condiviso si trova.
* Se si utilizza qualsiasi host tooadd account RunAs, su hello importare ed esportare i percorsi, assegnare di lettura e delle autorizzazioni di scrittura toohello account RunAs in VMM.
* Hello importazione ed esportazione di condivisioni non deve trovarsi in qualsiasi computer utilizzato come server host Hyper-V, perché la configurazione di loopback non è supportata da Hyper-V.
* In Active Directory, in ogni server host Hyper-V che contiene le macchine virtuali da tooprotect, abilitare e configurare la delega vincolata tootrust hello computer remoti in cui hello importazione e l'esportazione percorsi si trovano, come indicato di seguito:
  1. Nel controller di dominio hello, aprire **Active Directory Users and Computers**.
  2. Nell'albero della console hello fare clic su **DomainName** > **computer**.
  3. Nome del server host Hyper-V hello rapida > **proprietà**.
  4. In hello **delega** scheda, fare clic su T**ruggine questo computer per i servizi solo di delega toospecified**.
  5. Fare clic su **Usa un qualsiasi protocollo di autenticazione**.
  6. Fare clic su **Aggiungi** > **Utenti e computer**.
  7. Nome del computer di hello che ospita il percorso di esportazione hello hello di tipo > **OK**. Tenere premuto CTRL hello hello l'elenco dei servizi disponibili e fare clic su **cifs** > **OK**. Ripetere per il nome del computer hello hello tale percorso di importazione hello host. Ripetere l'operazione per eventuali altri server host Hyper-V.

## <a name="step-5-configure-network-mapping"></a>Passaggio 5: configurare il mapping di rete
1. Nella pagina introduttiva hello, fare clic su **mapping delle reti**.
2. Selezionare hello server VMM di origine da cui si desidera toomap reti e quindi hello hello toowhich server VMM di destinazione verranno eseguito il mapping di reti. viene visualizzato l'elenco di Hello di reti di origine e le relative reti di destinazione associate. Viene visualizzato un valore vuoto per le reti che non sono state attualmente sottoposte a mapping.
3. Selezionare una rete in **Rete nell'origine** > **Mappa**. servizio di Hello rileva le reti VM hello nel server di destinazione hello e li visualizza. Fare clic su hello informazioni icona Avanti toohello origine e destinazione nomi tooview hello subnet della rete per ogni rete.

    ![Configurare il mapping di rete](./media/site-recovery-vmm-to-vmm-classic/network-mapping1.png)
4. Nella finestra di dialogo hello selezionare una delle reti VM hello dal server VMM di destinazione hello.

    ![Selezionare una rete di destinazione](./media/site-recovery-vmm-to-vmm-classic/network-mapping2.png)
5. Quando si seleziona una rete di destinazione, hello cloud protetti che usano la rete di origine hello vengono visualizzati. Sono visualizzate anche le reti di destinazione disponibili associate ai cloud hello utilizzati per la protezione. Si consiglia di selezionare una rete di destinazione è il cloud di hello tooall disponibili che vengono usati per la protezione. O, è anche possibile passare toohello Server VMM e modificare hello cloud proprietà tooadd hello rete logica corrispondente toohello rete di macchina virtuale che si desidera toochoose.
6. Fare clic su processo di mapping hello toocomplete hello segno di spunta. Stato del mapping hello tootrack viene avviato un processo. È possibile visualizzarlo in hello **processi** scheda.

## <a name="step-6-configure-storage-mapping"></a>Passaggio 6: configurare il mapping di archiviazione
Per impostazione predefinita quando si replica una macchina virtuale in un origine Hyper-V host server tooa Hyper-V host server di destinazione, i dati replicati archiviati nel percorso predefinito di hello indicato per host Hyper-V di destinazione hello in Hyper-V Manager. Per un maggiore controllo della destinazione dell'archiviazione dei dati replicati, è possibile configurare i mapping di archiviazione nel seguente modo:

1. Definire le classificazioni di archiviazione su entrambi origine hello e i server VMM di destinazione. [Altre informazioni](https://technet.microsoft.com/library/gg610685.aspx) Le classificazioni devono essere disponibili toohello i server host Hyper-V nei cloud di origine e destinazione. Le classificazioni non devono toohave hello stesso tipo di archiviazione. Ad esempio è possibile mappare una classificazione di origine che contiene la classificazione destinazione tooa di condivisioni SMB che contiene i volumi condivisi cluster.
2. Dopo la configurazione delle classificazioni, è possibile creare i mapping. toodo questo su hello **avvio rapido** pagina > **mappare l'archiviazione**.
3. Fare clic su hello **archiviazione** scheda > **mappa classificazioni di archiviazione**.
4. In hello **mappa classificazioni di archiviazione** , selezionare le classificazioni di origine hello e i server VMM di destinazione. Salvare le impostazioni.

    ![Selezionare una rete di destinazione](./media/site-recovery-vmm-to-vmm-classic/storage-mapping.png)

## <a name="step-7-enable-virtual-machine-protection"></a>Passaggio 7: abilitare la protezione delle macchine virtuali
Dopo aver configurate correttamente i server, cloud e reti, è possibile abilitare la protezione per le macchine virtuali nel cloud hello.

1. In hello **macchine virtuali** scheda cloud hello in cui hello si trova la macchina virtuale, fare clic su **abilitare la protezione** > **aggiungere macchine virtuali**.
2. Selezionare hello uno desiderato tooprotect hello elenco di macchine virtuali nel cloud hello.

    ![Abilitare la protezione delle macchine virtuali](./media/site-recovery-vmm-to-vmm-classic/enable-protection.png)
3. Tenere traccia dell'avanzamento dell'azione Abilita protezione in hello hello **processi** scheda, inclusa la replica iniziale di hello. Macchina virtuale di hello viene eseguito il processo di finalizzazione della protezione hello è pronto per il failover. Dopo aver abilitato la protezione e le macchine virtuali vengono replicate, sarà in grado di tooview usarle in Azure.

    ![Processo di protezione delle macchine virtuali](./media/site-recovery-vmm-to-vmm-classic/vm-jobs.png)

> [!NOTE]
> È inoltre possibile abilitare la protezione per le macchine virtuali nella console VMM hello. Fare clic su **Abilita protezione** sulla barra degli strumenti hello hello **Azure Site Recovery** scheda proprietà della macchina virtuale hello.
>
>

### <a name="on-board-existing-virtual-machines"></a>Caricare le macchine virtuali esistenti
Se si dispone di macchine virtuali in VMM che sta eseguendo la replica con Replica Hyper-V è necessario tooonboard per la protezione Azure Site Recovery come indicato di seguito:

1. Verificare di avere cloud primari e secondari. Verificare che il server di hello Hyper-V ospita macchina virtuale esistente hello si trova nel cloud primario hello e server hello Hyper-V ospita macchina virtuale di replica hello si trova nel cloud secondario hello. Assicurarsi aver configurato le impostazioni di protezione per i cloud hello. impostazioni di Hello devono corrispondere a quelli attualmente configurato per la Replica Hyper-V. In caso contrario, la replica delle macchine virtuali potrebbe non funzionare come previsto.
2. Abilitare la protezione per macchina virtuale primaria hello. Azure Site Recovery e VMM garantiscono hello stesso host di replica e la macchina virtuale è stato rilevato che Azure Site Recovery riutilizzerà e ristabilirà la replica utilizzando le impostazioni di hello configurate durante la configurazione cloud.

## <a name="test-your-deployment"></a>Testare la distribuzione
pianificare la distribuzione, è possibile eseguire un failover di test per una singola macchina virtuale o creare un piano di ripristino costituita da più macchine virtuali ed eseguire un failover di test per hello tootest.  Il failover di test consente di simulare il meccanismo di failover e di ripristino in una rete isolata.

### <a name="create-a-recovery-plan"></a>Creare un piano di ripristino
1. In hello **piani di ripristino** scheda, fare clic su **crea piano di ripristino**.
2. Specificare un nome per il piano di ripristino hello e i server VMM di origine e di destinazione. server di origine di Hello deve disporre di macchine virtuali che sono abilitate per il failover e ripristino. Selezionare **Hyper-V** tooview solo cloud configurati per la replica Hyper-V.

    ![Crea piano di ripristino](./media/site-recovery-vmm-to-vmm-classic/recovery-plan1.png)
3. In **Seleziona macchine virtuali**selezionare i gruppi di replica. Tutte le macchine virtuali associate al gruppo di replica hello sarà selezionate e aggiunto toohello piano di ripristino. Queste macchine virtuali vengono aggiunte gruppo predefinito piano di ripristino toohello: gruppo 1. Se necessario, è possibile aggiungere altri gruppi. Si noti che, dopo le macchine virtuali di replica, verranno avviate in base a ordine hello dei gruppi del piano di ripristino hello.

    ![Aggiungi macchine virtuali.](./media/site-recovery-vmm-to-vmm-classic/recovery-plan2.png)

Dopo aver creato un piano di ripristino, viene visualizzato nell'elenco hello hello **piani di ripristino** scheda.

### <a name="run-a-test-failover"></a>Eseguire un failover di test
1. In hello **piani di ripristino** , selezionare il piano di hello e fare clic su **Failover di Test**.
2. In hello **conferma Failover di Test** selezionare **Nessuno**. Si noti che con questa opzione abilitata hello eseguito il failover delle macchine virtuali di replica non sarà connessa tooany rete. Per il test verrà hello ha esito negativo di macchina virtuale in come previsto, ma non esegue il test dell'ambiente di rete di replica. Osservare come troppo[eseguire un failover di test](site-recovery-failover.md) per ulteriori informazioni su come toouse diverse opzioni di rete.
3. macchina virtuale di test hello verrà creato in hello stesso host come host hello in cui hello esiste macchina virtuale di replica. Viene aggiunto toohello stesso cloud in cui hello macchina virtuale di replica si trova.

### <a name="run-a-recovery-plan"></a>Eseguire un piano di ripristino
Dopo la replica hello macchina virtuale di replica potrebbe non disporre di un indirizzo IP che è hello stesso indirizzo IP hello di hello macchina virtuale primaria. Macchine virtuali verranno aggiornati i server DNS hello che utilizzano dopo l'avvio. È anche possibile aggiungere un tooensure di Server DNS hello tooupdate script aggiornamento tempestivo.

#### <a name="script-tooretrieve-hello-ip-address"></a>Indirizzo IP di script tooretrieve hello
Eseguire questo indirizzo IP di hello tooretrieve di script di esempio.

        $vm = Get-SCVirtualMachine -Name <VM_NAME>
        $na = $vm[0].VirtualNetworkAdapters>
        $ip = Get-SCIPAddress -GrantToObjectID $na[0].id
        $ip.address  

#### <a name="script-tooupdate-dns"></a>Script tooupdate DNS
Eseguire questo tooupdate di script di esempio DNS, specificare l'indirizzo IP hello recuperati tramite script di esempio precedente hello.

        string]$Zone,
        [string]$name,
        [string]$IP
        )
        $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
        $newrecord = $record.clone()
        $newrecord.RecordData[0].IPv4Address  =  $IP
        Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord



## <a name="privacy-information-for-site-recovery"></a>Informativa sulla privacy per Site Recovery
In questa sezione fornisce informazioni aggiuntive sulla privacy per hello servizio Microsoft Azure Site Recovery ("servizio"). Informativa sulla privacy di hello tooview per servizi di Microsoft Azure, vedere la [informativa sulla Privacy di Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=324899)

**Funzionalità: registrazione**

* **Risultato**: registra il server nel Servizio in modo che le macchine virtuali possano essere protette
* **Le informazioni raccolte**: dopo la registrazione hello servizio raccoglie, elabora e trasmette le informazioni sul certificato di gestione dal server VMM hello che è designato il ripristino di emergenza tooprovide utilizzando il nome del servizio hello del server VMM, hello e il nome di hello del cloud di macchine virtuali nel server VMM.
* **Uso delle informazioni**:

  * Certificato di gestione, viene utilizzato toohelp identificare e autenticare il server VMM registrato hello per toohello di accesso del servizio. Hello servizio utilizza hello parte della chiave pubblica hello certificato toosecure registrato un token che hello solo server VMM può accedere. server Hello deve toouse questa funzionalità del servizio token toogain toohello accesso.
  * Nome del server VMM hello: nome del server VMM hello è obbligatorio tooidentify e comunicare con server VMM appropriato hello in cui hello trovano cloud.
  * Nomi dei cloud dal server VMM hello, ovvero il nome di cloud hello è obbligatorio quando si utilizza hello servizio cloud funzionalità di associazione/annullamento associazione descritta di seguito. Quando si decide di toopair il cloud da un data center principale con un altro cloud nel data center di ripristino hello, vengono presentati i nomi di hello di tutti i cloud hello dal data center di ripristino hello.
* **Scelta**: queste informazioni sono una parte essenziale del processo di registrazione del servizio hello in quanto semplifica la e hello server VMM hello tooidentify del servizio per cui si desidera tooprovide protezione di Azure Site Recovery, nonché tooidentify hello server VMM registrato corretto. Se non si desidera toosend questo toohello informazioni del servizio, non utilizzare questo servizio. Se si registra il server e quindi successivamente si desidera toounregister, è possibile farlo eliminando le informazioni sul server di hello VMM dal portale di Service hello (che è hello portale di Azure).

**Funzionalità: abilitare la protezione di Azure Site Recovery**

* **Funzione**: hello Provider di Azure Site Recovery installato nel server VMM hello è canale hello per le comunicazioni con hello del servizio. Hello Provider è una libreria di collegamento dinamico (DLL) ospitata nel processo VMM hello. Dopo aver hello che provider è installato, funzionalità "Datacenter Recovery" hello viene abilitata nella console di amministrazione VMM hello. Le macchine virtuali nuove o esistenti in un cloud può attivare una proprietà denominata "Datacenter Recovery" toohelp proteggere macchina virtuale hello. Dopo aver impostata questa proprietà, hello Provider invia hello nome e l'ID di macchina virtuale di hello toohello servizio. la protezione virtuale Hello è abilitata per la tecnologia di replica di Windows Server 2012 o Windows Server 2012 R2 Hyper-V. dati della macchina virtuale Hello vengono replicati da uno tooanother di host Hyper-V (in genere si trova in un data center di "ripristino" diverso).
* **Le informazioni raccolte**: hello servizio raccoglie, elabora e trasmette i metadati per la macchina virtuale di hello, che include il nome di hello, ID, rete virtuale e il nome di hello del cloud hello a cui appartiene.
* **Utilizzo delle informazioni**: hello servizio utilizza hello sopra informazioni toopopulate hello macchina virtuale nel portale del servizio.
* **Scelta**: questa è una parte essenziale del servizio hello e non può essere disattivata. Se non si desidera inviare toohello servizio queste informazioni, non abilitare la protezione di Azure Site Recovery per le macchine virtuali. Si noti che tutti i dati inviati dal Provider di hello toohello servizio viene inviato su HTTPS.

**Funzionalità: piano di ripristino**

* **Funzione**: questa funzionalità consente di toobuild un piano di orchestrazione del data center di "ripristino" hello. È possibile definire l'ordine di hello in quale hello macchine virtuali o un gruppo di macchine virtuali deve essere avviato nel sito di ripristino hello. È anche possibile specificare qualsiasi toobe script automatizzati eseguire o toobe qualsiasi azione manuale al momento di hello del ripristino per ogni macchina virtuale. Failover (illustrato nella sezione successiva hello) è in genere attivato a livello del piano di ripristino per un ripristino coordinato hello.
* **Le informazioni raccolte**: hello servizio raccoglie, elabora e trasmette i metadati per il piano di ripristino hello, inclusi i metadati della macchina virtuale e i metadati di qualsiasi script di automazione e note di azione manuale.
* **Utilizzo delle informazioni**: hello metadati descritti in precedenza sono piano di ripristino hello toobuild usato nel portale del servizio.
* **Scelta**: questa è una parte essenziale del servizio hello e non può essere disattivata. Se non si desidera inviare toohello servizio queste informazioni, non vengono compilati piani di ripristino nel servizio.

**Funzionalità: mapping di rete**

* **Funzione**: questa funzionalità permette di informazioni di rete toomap dal hello data center toohello ripristino data center principale. Quando le macchine virtuali hello vengono ripristinate nel sito di ripristino hello, questo mapping consente di ristabilire la connettività di rete per loro.
* **Le informazioni raccolte**: come parte della funzionalità di mapping di rete hello, hello servizio raccoglie, elabora e trasmette i metadati di hello di reti logiche di hello per ogni sito (primario e Data Center).
* **Utilizzo delle informazioni**: hello servizio utilizza hello metadati toopopulate portale del servizio in cui è possibile mappare le informazioni di rete hello.
* **Scelta**: questa è una parte essenziale del servizio hello e non può essere disattivata. Se non si desidera inviare toohello servizio queste informazioni, non utilizzare funzionalità di mapping di rete hello.

**Funzionalità: failover (pianificato, non pianificato e di test)**

* **Funzione**: questa funzionalità consente il failover di una macchina virtuale da un centro di dati gestiti da VMM tooanother del centro dati gestiti da VMM. azione di failover Hello viene attivata dall'utente hello nel portale del servizio. Le possibili cause per un failover sono un evento non pianificato (ad esempio nel caso di hello di un disaster0 naturale; un evento pianificato (ad esempio Data Center bilanciamento del carico); un failover di test (ad esempio una prova piano ripristino).

Hello Provider nel server VMM hello riceve la notifica di evento hello hello servizio ed esegue un'azione di failover in host Hyper-V hello tramite le interfacce VMM. Il failover effettivo della macchina virtuale hello da uno tooanother di host Hyper-V (in genere in esecuzione in un data center di "ripristino" diverso) viene gestito dalla tecnologia di replica di Windows Server 2012 o Windows Server 2012 R2 Hyper-V hello. Al termine del failover hello, hello Provider installato nel server VMM hello del data center di "ripristino" hello invia hello successo informazioni toohello del servizio.

* **Le informazioni raccolte**: hello servizio utilizza hello sopra lo stato di hello toopopulate informazioni di informazioni sull'azione di failover hello nel portale del servizio.
* **Utilizzo delle informazioni**: hello servizio utilizza hello sopra informazioni come segue:

  * Certificato di gestione, viene utilizzato toohelp identificare e autenticare il server VMM registrato hello per toohello di accesso del servizio. Hello servizio utilizza hello parte della chiave pubblica hello certificato toosecure registrato un token che hello solo server VMM può accedere. server Hello deve toouse questa funzionalità del servizio token toogain toohello accesso.
  * Nome del server VMM hello: nome del server VMM hello è obbligatorio tooidentify e comunicare con server VMM appropriato hello in cui hello trovano cloud.
  * Nomi dei cloud dal server VMM hello, ovvero il nome di cloud hello è obbligatorio quando si utilizza hello servizio cloud funzionalità di associazione/annullamento associazione descritta di seguito. Quando si decide di toopair il cloud da un data center principale con un altro cloud nel data center di ripristino hello, vengono presentati i nomi di hello di tutti i cloud hello dal data center di ripristino hello.
* **Scelta**: questa è una parte essenziale del servizio hello e non può essere disattivata. Se non si desidera inviare toohello servizio queste informazioni, non usare questo servizio.

## <a name="next-steps"></a>Passaggi successivi
Dopo aver eseguito un toocheck di failover di test dell'ambiente funzioni come previsto, [apprendere](site-recovery-failover.md) diversi tipi di failover.
