---
title: 'Backup di Azure: Preparare tooback backup di macchine virtuali | Documenti Microsoft'
description: Assicurarsi che l'ambiente sia pronto per il backup di macchine virtuali in Azure.
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: backup; eseguire il backup;
ms.assetid: e87e8db2-b4d9-40e1-a481-1aa560c03395
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: 5c3a41b5d3bd56e62ca5f207442867913aa99816
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-environment-tooback-up-resource-manager-deployed-virtual-machines"></a>Preparare l'ambiente tooback backup distribuiti Gestione risorse di macchine virtuali
> [!div class="op_single_selector"]
> * [Modello di Resource Manager](backup-azure-arm-vms-prepare.md)
> * [Modello classico](backup-azure-vms-prepare.md)
>
>

In questo articolo viene descritta la procedura hello per preparare l'ambiente tooback rapidamente una macchina virtuale (VM) di distribuzione di gestione risorse. Hello passaggi illustrati nelle procedure hello utilizzano hello portale di Azure.  

Hello servizio Backup di Azure è disponibili due tipi di archivi (backup di insiemi di credenziali e gli archivi di servizi di ripristino) per proteggere le macchine virtuali. Un insieme di credenziali di backup consente di proteggere le macchine virtuali distribuite con modello di distribuzione classica hello. L'insieme di credenziali dei servizi di ripristino protegge **le macchine virtuali distribuite sia con il modello di distribuzione classica sia con il modello di distribuzione Resource Manager**. È necessario utilizzare un tooprotect di insieme di credenziali per una macchina virtuale distribuita di gestione risorse di servizi di ripristino.

> [!NOTE]
> Azure offre due modelli di distribuzione per creare e usare le risorse: [Resource Manager e distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md). Vedere [preparare tooback l'ambiente di macchine virtuali di Azure](backup-azure-vms-prepare.md) per informazioni dettagliate sull'utilizzo di distribuzione classica le macchine virtuali del modello.
>
>

Prima di proteggere o eseguire il backup di una macchina virtuale (VM) di Resource Manager, verificare che siano disponibili i prerequisiti seguenti:

* Creare un insieme di credenziali di servizi di ripristino (o identificare un insieme di credenziali di recovery services esistente) *in hello stesso percorso di una macchina virtuale*.
* Selezionare uno scenario, definire i criteri di backup hello e definire gli elementi tooprotect.
* Il controllo hello installazione dell'agente di macchine Virtuali nella macchina virtuale.
* Verificare la connettività della rete
* Per le macchine virtuali Linux, nel caso in cui si desidera toocustomize dell'ambiente di backup per backup coerenti con l'applicazione seguire hello [tooconfigure passaggi pre-snapshot e script di post-snapshot](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent)

Se si è certi di queste condizioni già esistono nell'ambiente in uso e quindi toohello [eseguire il backup di un articolo di macchine virtuali](backup-azure-vms.md). Se è necessario tooset backup o controllare, uno di questi prerequisiti, in questo articolo illustra hello passaggi tooprepare dei prerequisiti.

##<a name="supported-operating-system-for-backup"></a>Sistema operativo supportato per il backup
 * **Linux**: Backup di Azure supporta [un elenco di distribuzioni approvate da Azure](../virtual-machines/linux/endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) , ad eccezione di CoreOS Linux. _Altri Bring-Your-proprietari-distribuzioni di Linux potrebbe essere inoltre funzionare, purché sia disponibile nella macchina virtuale hello agente VM hello e il supporto per Python esiste. Microsoft tuttavia non consiglia queste distribuzioni per il backup._
 * **Windows Server**: le versioni precedenti a Windows Server 2008 R2 non sono supportate.

## <a name="limitations-when-backing-up-and-restoring-a-vm"></a>Limitazioni durante il backup e il ripristino di una VM
Prima di preparare l'ambiente, per comprendere le limitazioni di hello.

* Il backup di macchine virtuali con più di 16 dischi dati non è supportato.
* Il backup delle macchine virtuali con dischi dati maggiori di 1023 GB non è supportato.
* Il backup di macchine virtuali con un indirizzo IP riservato e nessun endpoint definito non è supportato.
* Il backup di macchine virtuali crittografate solo con BEK non è supportato. Il backup delle macchine virtuali Linux crittografate con la crittografia LUKS non è supportato.
* Il backup delle VM nelle configurazioni di file server scalabili orizzontalmente non è consigliato.
* Dati di backup non includono tooVM unità collegate rete montato.
* La sostituzione di una macchina virtuale esistente durante il ripristino non è supportata. Se si tenta di hello toorestore VM quando hello VM esiste, l'operazione di ripristino hello ha esito negativo.
* L'operazione di backup e ripristino tra aree geografiche diverse non è supportata.
* È possibile eseguire il backup di macchine virtuali in tutte le aree pubbliche di Azure (vedere hello [checklist](https://azure.microsoft.com/regions/#services) delle aree geografiche supportate). Se l'area hello che si sta cercando è attualmente supportata, non verrà visualizzato nell'elenco a discesa hello durante la creazione dell'insieme di credenziali.
* Il ripristino di un controller di dominio di VM che fa parte di una configurazione con controller di dominio è supportato solo tramite PowerShell. Altre informazioni sul [ripristino di un controller di dominio con più controller di dominio](backup-azure-restore-vms.md#restoring-domain-controller-vms).
* Ripristino delle macchine virtuali che dispongono delle seguenti configurazioni di rete speciali hello è supportato solo tramite PowerShell. Macchine virtuali create utilizzando del flusso di lavoro ripristino hello in hello dell'interfaccia utente non avrà queste configurazioni di rete al termine dell'operazione di ripristino hello. vedere, più toolearn [il ripristino di macchine virtuali con configurazioni di rete speciali](backup-azure-restore-vms.md#restoring-vms-with-special-network-configurations).
  * Macchine virtuali con configurazione del servizio di bilanciamento del carico (interno ed esterno)
  * Macchine virtuali con più indirizzi IP riservati
  * Macchine virtuali con più schede di rete

## <a name="create-a-recovery-services-vault-for-a-vm"></a>Creare l'insieme di credenziali dei servizi di ripristino per una macchina virtuale
Un insieme di credenziali di servizi di ripristino è un'entità a cui sono archiviati i backup hello e punti di ripristino che sono stati creati nel corso del tempo. insieme di credenziali di Hello recovery services contiene anche i criteri di backup hello associati alle macchine virtuali protetta hello.

un ripristino toocreate services insieme di credenziali:

1. Accedi toohello [portale di Azure](https://portal.azure.com/).
2. Nel menu Hub hello, fare clic su **Sfoglia** e nell'elenco di hello delle risorse, digitare **servizi di ripristino**. Si inizia a digitare, elenco hello verrà filtrato in base all'input. Fare clic su **Insiemi di credenziali dei servizi di ripristino**.

    ![Fare clic sul pulsante Sfoglia hello e digitare i servizi di ripristino. La presenza di servizi di ripristino hello opzione dell'insieme di credenziali, selezionarlo hello tooopen servizi di ripristino dell'insieme di credenziali blade.](./media/backup-azure-arm-vms-prepare/browse-to-rs-vaults-updated.png) <br/>

    viene visualizzato l'elenco di Hello degli insiemi di credenziali di servizi di ripristino.
3. In hello **insiemi di credenziali di servizi di ripristino** menu, fare clic su **Aggiungi**.

    ![Creare un insieme di credenziali dei servizi di ripristino - Passaggio 2](./media/backup-azure-arm-vms-prepare/rs-vault-menu.png)

    Servizi di ripristino Hello insieme di credenziali si apre Pannello chiesto tooprovide un **nome**, **sottoscrizione**, **gruppo di risorse**, e **percorso**.

    ![Creare un insieme di credenziali dei servizi di ripristino - Passaggio 5](./media/backup-azure-arm-vms-prepare/rs-vault-attributes.png)
4. Per **nome**, immettere un insieme di credenziali di nome descrittivo tooidentify hello. nome di Hello deve toobe univoco per la sottoscrizione di Azure hello. Digitare un nome che contenga tra i 2 e i 50 caratteri. Deve iniziare con una lettera e può contenere solo lettere, numeri e trattini.
5. Fare clic su **sottoscrizione** elenco disponibile di hello toosee delle sottoscrizioni. Se non sei sicuro che toouse di sottoscrizione, utilizzare predefinito hello (o suggerito) sottoscrizione. Sono presenti scelte multiple solo se l'account dell'organizzazione è associato a più sottoscrizioni di Azure.
6. Fare clic su **gruppo di risorse** toosee hello l'elenco dei gruppi di risorse disponibili, oppure fare clic su **New** toocreate un nuovo gruppo di risorse. Per informazioni complete sui gruppi di risorse, vedere [Panoramica di Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)
7. Fare clic su **percorso** tooselect hello località geografica per l'insieme di credenziali hello. insieme di credenziali Hello **deve** in hello hello le macchine virtuali che si desidera tooprotect stessa area.

   > [!IMPORTANT]
   > Se si è certi della posizione di hello in cui esiste la macchina virtuale, chiudere la finestra di dialogo Creazione dell'insieme di credenziali hello e passare toohello elenco di macchine virtuali nel portale di hello. Se si dispongono di macchine virtuali in più aree, è necessario toocreate un insieme di credenziali di servizi di ripristino in ogni area. Creare hello nella prima posizione hello prima di passare alla posizione successiva toohello. È presente alcun account di archiviazione necessario toospecify toostore hello dati di backup - insieme di credenziali di servizi di ripristino hello e hello servizio Backup di Azure gestisce automaticamente questo.
   >
   >

8. Fare clic su **Crea**. Può richiedere un po' di tempo per hello toobe creato insieme di credenziali di servizi di ripristino. Monitorare le notifiche di stato hello in hello superiore destro area hello portale. Una volta creato l'insieme di credenziali, viene visualizzato nell'elenco hello degli insiemi di credenziali di servizi di ripristino. Se l'insieme di credenziali non viene visualizzato, fare clic su **Aggiorna** per

    ![Elenco degli insiemi di credenziali per il backup](./media/backup-azure-arm-vms-prepare/rs-list-of-vaults.png)

    Dopo aver creato l'insieme di credenziali, informazioni su come tooset hello replica di archiviazione.

## <a name="set-storage-replication"></a>Impostare la replica di archiviazione
opzione di replica di archiviazione Hello consente toochoose tra l'archiviazione con ridondanza geografica e l'archiviazione con ridondanza locale. Per impostazione predefinita, l'insieme di credenziali prevede l'archiviazione con ridondanza geografica. Lasciare l'archiviazione con ridondanza toogeo hello opzione set, se si tratta del backup primario. Se si vuole un'opzione più economica ma non altrettanto permanente, scegliere l'archiviazione con ridondanza locale.

impostazione di replica tooedit hello archiviazione:

1. In hello **insiemi di credenziali di servizi di ripristino** pannello, selezionare l'insieme di credenziali.
    Quando si sceglie l'insieme di credenziali, hello pannello impostazioni (*che ha il nome di hello dell'insieme di credenziali hello nella parte superiore di hello*) e i dettagli di insieme di credenziali hello apre blade.

    ![Scegliere l'insieme di credenziali dall'elenco hello degli archivi di backup](./media/backup-azure-arm-vms-prepare/new-vault-settings-blade.png)

2. In hello **impostazioni** pannello, utilizzare hello dispositivo di scorrimento verticale tooscroll verso il basso toohello **Gestisci** sezione. Fare clic su **Backup infrastruttura** tooopen il pannello. In hello **generale** fare clic su sezione **la configurazione del Backup** tooopen il pannello. In hello **la configurazione del Backup** pannello, scegliere l'opzione di replica di archiviazione di hello per l'insieme di credenziali. Per impostazione predefinita, l'insieme di credenziali prevede l'archiviazione con ridondanza geografica. Se si modifica il tipo di replica di hello archiviazione, fare clic su **salvare**.

    ![Elenco degli insiemi di credenziali per il backup](./media/backup-azure-arm-vms-prepare/full-blade.png)

     Se si usa Azure come endpoint primario di archiviazione dei backup, continuare a usare l'archiviazione con ridondanza geografica. Se si usa Azure come endpoint non primario di archiviazione dei backup, è consigliabile scegliere l'opzione di archiviazione con ridondanza locale. Altre informazioni sui [con ridondanza geografica](../storage/common/storage-redundancy.md#geo-redundant-storage) e [ridondanza locale](../storage/common/storage-redundancy.md#locally-redundant-storage) opzioni di archiviazione in hello [Cenni preliminari sulla replica di archiviazione di Azure](../storage/common/storage-redundancy.md).
    Dopo aver scelto l'opzione di archiviazione hello per l'insieme di credenziali, si è pronti tooassociate hello VM con insieme di credenziali hello. associazione hello toobegin, è necessario individuare e registrare hello macchine virtuali di Azure.

## <a name="select-a-backup-goal-set-policy-and-define-items-tooprotect"></a>Selezionare un obiettivo di backup, impostare criteri e definire gli elementi tooprotect
Prima di registrare una macchina virtuale con un insieme di credenziali, eseguire hello tooensure di processo di individuazione che eventuali nuove macchine virtuali che sono stati aggiunti toohello sottoscrizione vengono identificate. le query di processo di Hello Azure per elenco hello delle macchine virtuali nella sottoscrizione di hello, insieme a informazioni aggiuntive come nome del servizio cloud hello e area hello. Nel portale di Azure hello, scenario si riferisce toowhat sarà tooput nell'insieme di credenziali di hello recovery services. Criteri sono pianificazione hello per la frequenza e quando vengono eseguiti i punti di ripristino. Criteri includono anche periodo di mantenimento dei punti di ripristino hello hello.

1. Se è già aperto un insieme di credenziali di servizi di ripristino, procedere toostep 2. Se non è un insieme di credenziali di servizi di ripristino aperto, quindi aprire hello [portale di Azure](https://portal.azure.com/) nel menu Hub hello, fare clic su **più servizi**.

   * Nell'elenco di hello delle risorse, digitare **servizi di ripristino**.
   * Si inizia a digitare, elenco hello verrà filtrato in base all'input. Quando viene visualizzata l'opzione, fare clic su **Insiemi di credenziali dei servizi di ripristino**.

     ![Creare un insieme di credenziali dei servizi di ripristino - Passaggio 1](./media/backup-azure-arm-vms-prepare/browse-to-rs-vaults-updated.png) <br/>

     viene visualizzato l'elenco di Hello degli insiemi di credenziali di servizi di ripristino. Se non esistono insiemi di credenziali nella sottoscrizione, questo elenco sarà vuoto.

    ![Visualizzazione di hello servizi di ripristino di insiemi di credenziali di elenco](./media/backup-azure-arm-vms-prepare/rs-list-of-vaults.png)

   * Dall'elenco a hello degli insiemi di credenziali di servizi di ripristino, selezionare un insieme di credenziali tooopen relativo dashboard.

     pannello impostazioni Hello e hello archivio dashboard per l'insieme di credenziali hello scelto, verrà visualizzata.

     ![Pannello dell'insieme di credenziali aperto](./media/backup-azure-arm-vms-prepare/new-vault-settings-blade.png)
2. Scegliere dal menu del dashboard dell'insieme di credenziali di hello **Backup** blade di Backup tooopen hello.

    ![Pannello Backup aperto](./media/backup-azure-arm-vms-prepare/backup-button.png)

    Aprire i pannelli di Backup e Backup obiettivo Hello.

    ![Pannello Scenario aperto](./media/backup-azure-arm-vms-prepare/select-backup-goal-1.png)

3. Nel Pannello di hello obiettivo di Backup, impostare **in cui viene eseguito il carico di lavoro** tooAzure e **cosa si desidera toobackup** tooVirtual computer, quindi fare clic su **OK**.

    In questo modo viene registrata hello estensione della macchina virtuale con l'insieme di credenziali hello. Obiettivo di Backup pannello chiude Hello e hello **criteri di Backup** apre blade.

    ![Pannello Scenario aperto](./media/backup-azure-arm-vms-prepare/select-backup-goal-2.png)
4. Nel Pannello di criteri di Backup hello, selezionare i criteri di backup hello da tooapply toohello insieme di credenziali.

    ![Selezionare il criterio di backup](./media/backup-azure-arm-vms-prepare/setting-rs-backup-policy-new.png)

    Dettagli Hello del criterio predefinito hello sono elencati nel menu di scelta rapida hello. Se si desidera toocreate un nuovo criterio, selezionare **Crea nuovo** dal menu a discesa hello. Per istruzioni sulla definizione di un criterio di backup, vedere [Definizione di un criterio di backup](backup-azure-vms-first-look-arm.md#defining-a-backup-policy).
    Fare clic su **OK** tooassociate dei criteri di backup hello con insieme di credenziali hello.

    Hello chiude pannello dei criteri di Backup e hello **selezionare le macchine virtuali** apre blade.
5. In hello **selezionare le macchine virtuali** pannello, scegliere hello tooassociate di macchine virtuali con hello specificato criteri e fare clic su **OK**.

    ![Selezionare il carico di lavoro](./media/backup-azure-arm-vms-prepare/select-vms-to-backup.png)

    macchina virtuale Hello selezionato viene convalidato. Se non hello le macchine virtuali che toosee previste, verificare che esistano in hello Azure stesso percorso hello insieme di credenziali di servizi di ripristino e non sono già protetti in un altro insieme di credenziali. percorso Hello di hello che insieme di credenziali di servizi di ripristino viene visualizzato nel dashboard dell'insieme di credenziali hello.

6. Dopo aver definito tutte le impostazioni per l'insieme di credenziali hello, nel pannello Backup hello fare clic su **abilitare il Backup**. Consente di distribuire insieme di credenziali toohello hello criteri e le macchine virtuali hello. Ciò non crea punto di ripristino iniziale hello per la macchina virtuale hello.

    ![Abilita backup](./media/backup-azure-arm-vms-prepare/vm-validated-click-enable.png)

Dopo avere abilitato correttamente il backup di hello, i criteri di backup verranno eseguito su pianificazione. Se si desidera ora toogenerate tooback un processo di backup su richiesta backup di macchine virtuali hello, vedere [processo di Backup hello Triggering](./backup-azure-arm-vms.md#triggering-the-backup-job).

Nel caso di problemi durante la registrazione di macchina virtuale hello, vedere le seguenti informazioni sull'installazione hello agente della macchina virtuale e la connettività di rete hello. Probabilmente non è necessario hello le seguenti informazioni se si desidera proteggere le macchine virtuali create in Azure. Tuttavia se è eseguita la migrazione di macchine virtuali in Azure, quindi assicurarsi che è stato installato correttamente l'agente VM hello e che la macchina virtuale possa comunicare con la rete virtuale hello.

## <a name="install-hello-vm-agent-on-hello-virtual-machine"></a>Installare hello agente della macchina virtuale nella macchina virtuale hello
Hello agente VM di Azure deve essere installato nella macchina virtuale di Azure per hello Backup estensione toowork hello. Se la macchina virtuale è stata creata da una raccolta di Azure hello, hello agente VM è già presente nella macchina virtuale hello. Queste informazioni vengono fornite per hello situazioni in cui *non* utilizza una macchina virtuale creata da hello raccolta di Azure, ad esempio la migrazione di una macchina virtuale da un data center locale. In tal caso, hello agente VM deve toobe installata nella macchina virtuale di ordine tooprotect hello. Informazioni su hello [agente VM](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux).

Se si verificano problemi di backup hello macchina virtuale di Azure, verificare che hello agente VM di Azure sia installato correttamente nella macchina virtuale hello (vedere la tabella hello seguente). Hello nella tabella seguente fornisce informazioni aggiuntive su hello agente VM per Windows e le macchine virtuali Linux.

| **Operazione** | **Windows** | **Linux** |
| --- | --- | --- |
| L'installazione dell'agente VM hello |Scaricare e installare hello [agente MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Sarà necessario installazione hello toocomplete privilegi di amministratore. |<li> Installare più recente hello [agente Linux](../virtual-machines/linux/agent-user-guide.md). Sarà necessario installazione hello toocomplete privilegi di amministratore. È consigliabile installare l'agente dal repository di distribuzione. **Non è consigliabile** installare l'agente di macchine virtuali Linux direttamente da GitHub.  |
| Aggiornamento agente VM hello |Aggiornamento hello agente della macchina virtuale è semplice come reinstallare hello [binari agente VM](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). <br>Verificare che non venga eseguita alcuna operazione di backup durante l'aggiornamento dell'agente VM hello. |Seguire le istruzioni di hello [aggiornamento hello agente VM Linux](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). È consigliabile aggiornare l'agente dal repository di distribuzione. **Non è consigliabile** aggiornare l'agente di macchine virtuali Linux direttamente da GitHub.<br>Verificare che nessuna operazione di backup è in esecuzione durante hello che agente VM viene aggiornata. |
| Convalida di installazione dell'agente VM hello |<li>Passare toohello *C:\WindowsAzure\Packages* cartella hello macchina virtuale di Azure. <li>È necessario trovare un file WaAppAgent.exe hello presentano.<li> Fare clic sul file hello, andare troppo**proprietà**, quindi selezionare hello **dettagli** campo versione prodotto di hello scheda deve essere 2.6.1198.718 o versione successiva. |N/D |

### <a name="backup-extension"></a>Estensione di backup
Una volta hello che agente VM viene installato nella macchina virtuale hello hello servizio Azure Backup installa hello estensione backup toohello agente della macchina virtuale. Hello servizio Azure Backup facilmente aggiornamenti e patch estensione backup hello.

estensione del backup Hello viene installato per il servizio di Backup hello hello macchina virtuale è in esecuzione o meno. Una macchina virtuale in esecuzione fornisce hello maggiore probabilità di riuscire a ottenere un punto di ripristino coerenti con l'applicazione. Tuttavia, hello servizio Backup di Azure continua tooback backup hello VM anche se è stato disattivato e non è stato installato l'estensione hello. Questa situazione è detta macchina virtuale offline. In questo caso, si sarà il punto di ripristino hello *anomalo*.

## <a name="network-connectivity"></a>Connettività di rete
In snapshot VM hello toomanage ordine, estensione backup hello deve toohello connettività Azure gli indirizzi IP pubblici. Senza hello destra la connettività Internet, HTTP richieste hello e timeout operazione di backup della macchina virtuale hello non riesce. Se la distribuzione ha restrizioni di accesso, ad esempio, un gruppo di sicurezza di rete (NSG), scegliere una delle opzioni seguenti per specificare un percorso chiaro per il traffico di backup:

* [Gli intervalli di IP whitelist hello Data Center di Azure](http://www.microsoft.com/en-us/download/details.aspx?id=41653) -vedere hello per le istruzioni su come toowhitelist hello gli indirizzi IP.
* Distribuire un server proxy HTTP per eseguire il routing del traffico

Quando si decide quale toouse opzione, hello compromessi sono compresi tra gestibilità, un controllo granulare e costi.

| Opzione | Vantaggi | Svantaggi: |
| --- | --- | --- |
| Aggiungere gli intervalli IP all'elenco elementi consentiti  |Senza costi aggiuntivi.<br><br>Per l'apertura in un gruppo di accesso, utilizzare hello <i>Set AzureNetworkSecurityRule</i> cmdlet. |Toomanage complesse come cambiano di intervalli IP hello interessato nel tempo.<br><br>Fornisce l'intero toohello di accesso di Azure e non solo l'archiviazione. |
| Proxy HTTP |Un controllo granulare proxy hello archiviazione hello URL consentiti.<br>TooVMs accesso singolo punto di Internet.<br>Non soggetto tooAzure modifiche all'indirizzo IP. |Costi aggiuntivi per l'esecuzione di una macchina virtuale con il software proxy hello. |

### <a name="whitelist-hello-azure-datacenter-ip-ranges"></a>Intervalli di IP whitelist hello Data Center di Azure
intervalli IP toowhitelist hello Data Center di Azure, vedere hello [sito Web di Azure](http://www.microsoft.com/en-us/download/details.aspx?id=41653) per informazioni dettagliate su intervalli IP hello e le istruzioni.

### <a name="using-an-http-proxy-for-vm-backups"></a>Uso di un proxy HTTP per i backup delle VM
Per eseguire il backup di una macchina virtuale, estensione di backup hello in hello VM invia tooAzure i comandi di gestione snapshot hello archiviazione mediante un'API di HTTPS. Instradare il traffico di estensione del backup hello mediante il proxy HTTP hello poiché è l'unico componente hello configurato per l'accesso toohello rete Internet pubblica.

> [!NOTE]
> Non è consigliato per il software proxy hello che deve essere utilizzato. Assicurarsi di selezionare un proxy che è compatibile con i passaggi di configurazione hello riportato di seguito.
>
>

immagine di esempio Hello riportata di seguito viene illustrato come passaggi di configurazione tre hello necessarie toouse HTTP proxy:

* Tutto il traffico HTTP associato per le route di VM App hello pubblica Internet tramite Proxy VM.
* Proxy VM consente il traffico in ingresso da macchine virtuali nella rete virtuale hello.
* Sicurezza gruppo (rete) denominato Scoperto lockdown Hello deve un sicurezza regola consentire Internet il traffico in uscita dalla macchina virtuale di Proxy.

![Diagramma della distribuzione gruppo di sicurezza di rete con proxy HTTP](./media/backup-azure-vms-prepare/nsg-with-http-proxy.png)

toouse HTTP proxy toocommunicating toohello rete Internet pubblica, seguire questi passaggi:

#### <a name="step-1-configure-outgoing-network-connections"></a>Passaggio 1. Configurare le connessioni di rete in uscita
###### <a name="for-windows-machines"></a>Per macchine Windows
Questa procedura consente di impostare la configurazione del server proxy per l'account del sistema locale.

1. Scaricare [PsExec](https://technet.microsoft.com/sysinternals/bb897553)
2. Eseguire il comando seguente dal prompt dei comandi con privilegi elevati,

     ```
     psexec -i -s "c:\Program Files\Internet Explorer\iexplore.exe"
     ```
     Si apre la finestra di Explorer.
3. Passare tooTools -> Opzioni Internet -> connessioni -> Impostazioni LAN.
4. Verificare le impostazioni del proxy per l'account di sistema. Impostare l'IP del Proxy e la porta.
5. Chiudere Internet Explorer.

Questo comando esegue una configurazione proxy a livello di computer e verrà usato per tutto il traffico HTTP/HTTPS in uscita.

Se è stato impostato un server proxy in un account utente corrente (non un Account di sistema locale), utilizzare hello seguenti script tooapply li tooSYSTEMACCOUNT:

```
   $obj = Get-ItemProperty -Path Registry::”HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections"
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" -Name DefaultConnectionSettings -Value $obj.DefaultConnectionSettings
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" -Name SavedLegacySettings -Value $obj.SavedLegacySettings
   $obj = Get-ItemProperty -Path Registry::”HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings"
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings" -Name ProxyEnable -Value $obj.ProxyEnable
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings" -Name Proxyserver -Value $obj.Proxyserver
```

> [!NOTE]
> Se si nota il messaggio "(407) Autenticazione proxy obbligatoria" nel log del server proxy, verificare che l'autenticazione sia impostata correttamente.
>
>

###### <a name="for-linux-machines"></a>Per macchine Linux
Aggiungere hello seguente riga toohello ```/etc/environment``` file:

```
http_proxy=http://<proxy IP>:<proxy port>
```

Aggiungere hello seguenti righe toohello ```/etc/waagent.conf``` file:

```
HttpProxy.Host=<proxy IP>
HttpProxy.Port=<proxy port>
```

#### <a name="step-2-allow-incoming-connections-on-hello-proxy-server"></a>Passaggio 2. Consenti connessioni in ingresso nel server proxy hello:
1. Nel server proxy hello, aprire Windows Firewall. firewall Hello più semplice modo tooaccess hello è toosearch per Windows Firewall con sicurezza avanzata.

    ![Aprire hello Firewall](./media/backup-azure-vms-prepare/firewall-01.png)
2. Nella finestra di dialogo Windows Firewall hello destro **regole connessioni in entrata** e fare clic su **nuova regola...** .

    ![Creare una nuova regola](./media/backup-azure-vms-prepare/firewall-02.png)
3. In hello **in ingresso Creazione guidata nuova regola**, scegliere hello **personalizzato** opzione per hello **tipo di regola** e fare clic su **Avanti**.
4. In hello di hello pagina tooselect **programma**, scegliere **tutti i programmi** e fare clic su **Avanti**.
5. In hello **protocollo e porte** immettere hello le seguenti informazioni e fare clic su **Avanti**:

    ![Creare una nuova regola](./media/backup-azure-vms-prepare/firewall-03.png)

   * Nel campo *Tipo di protocollo* scegliere *TCP*.
   * per *porta locale* scegliere *porte specifiche*, nel campo hello specificare hello ```<Proxy Port>``` che è stato configurato.
   * Nel campo *Porta remota* selezionare *Tutte le porte*.

     Per rest hello della procedura guidata hello, fare clic su fine di toohello modo hello tutti e assegnare un nome di questa regola.

#### <a name="step-3-add-an-exception-rule-toohello-nsg"></a>Passaggio 3. Aggiungere un toohello regola eccezione gruppo:
In un prompt dei comandi di Azure PowerShell, immettere hello comando seguente:

Hello comando seguente consente di aggiungere un gruppo di toohello di eccezione. Questa eccezione consente il traffico TCP da qualsiasi porta 10.0.0.5 tooany indirizzo Internet sulla porta 80 (HTTP) o 443 (HTTPS). Se è necessaria una porta specifica in hello rete Internet pubblica, essere tooadd assicurarsi che la porta toohello ```-DestinationPortRange``` anche.

```
Get-AzureNetworkSecurityGroup -Name "NSG-lockdown" |
Set-AzureNetworkSecurityRule -Name "allow-proxy " -Action Allow -Protocol TCP -Type Outbound -Priority 200 -SourceAddressPrefix "10.0.0.5/32" -SourcePortRange "*" -DestinationAddressPrefix Internet -DestinationPortRange "80-443"
```


*Questi passaggi includono nomi e valori di esempio. Utilizzare nomi hello e i valori per la distribuzione di quando si immette, o tagliare e incollare il codice di dettagli.*

Ora che si conoscono che si dispone di connettività di rete, sta tooback pronto backup di una macchina virtuale. Vedere [Eseguire il backup di macchine virtuali distribuite con il modello di distribuzione Resource Manager](backup-azure-arm-vms.md).

## <a name="questions"></a>Domande?
Se si hanno domande o se è presente una funzionalità che si desidera toosee incluso, [inviare commenti e suggerimenti](http://aka.ms/azurebackup_feedback).

## <a name="next-steps"></a>Passaggi successivi
Ora che è stato preparato l'ambiente per il backup di una macchina virtuale, il passaggio successivo logico è toocreate una copia di backup. Hello pianificazione articolo fornisce informazioni più dettagliate sul backup di macchine virtuali.

* [Eseguire il backup di macchine virtuali](backup-azure-vms.md)
* [Pianificare l'infrastruttura di backup delle VM](backup-azure-vms-introduction.md)
* [Gestire backup di macchine virtuali](backup-azure-manage-vms.md)
