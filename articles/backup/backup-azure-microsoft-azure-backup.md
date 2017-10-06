---
title: aaaUse tooback di Azure Backup Server dei carichi di lavoro tooAzure | Documenti Microsoft
description: Utilizzare Server di Backup di Azure tooprotect o eseguire il backup dei carichi di lavoro toohello portale di Azure.
services: backup
documentationcenter: 
author: PVRK
manager: shivamg
editor: 
keywords: server di Backup di Azure; protezione dei carichi di lavoro; backup dei carichi di lavoro
ms.assetid: e7fb1907-9dc1-4ca1-8c61-50423d86540c
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/20/2017
ms.author: masaran;trinadhk;pullabhk;markgal
ms.openlocfilehash: a99b2919ffd44c6133960e3a935038a2bb1281c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-tooback-up-workloads-using-azure-backup-server"></a>Preparazione tooback dei carichi di lavoro tramite il Server di Backup di Azure
> [!div class="op_single_selector"]
> * [Server di backup di Azure](backup-azure-microsoft-azure-backup.md)
> * [SCDPM](backup-azure-dpm-introduction.md)
>
>

Questo articolo viene illustrato come tooprepare tooback l'ambiente dei carichi di lavoro tramite il Server di Backup di Azure. Con il server di Backup di Azure è possibile proteggere i carichi di lavoro dell'applicazione, ad esempio le VM Hyper-V, Microsoft SQL Server, SharePoint Server, Microsoft Exchange e i client di Windows, da una singola console.

> [!NOTE]
> Il server di Backup di Azure ora consente di proteggere le VM VMware e offre migliori funzionalità di sicurezza. Installare il prodotto di hello, come illustrato nelle sezioni hello sottostante. applicare l'aggiornamento 1 e hello più recente di Azure Backup Agent. toolearn più informazioni sul backup dei server VMware con il Server di Backup di Azure, vedere l'articolo hello [tooback utilizzare Azure Backup Server di un server VMware](backup-azure-backup-server-vmware.md). toolearn sulle funzionalità di sicurezza, fare riferimento troppo[sicurezza backup di Azure include documentazione](backup-azure-security-feature.md).
>
>

È anche possibile proteggere carichi di lavoro dell'infrastruttura distribuita come servizio (IaaS), ad esempio VM in Azure.

> [!NOTE]
> Azure offre due modelli di distribuzione per creare e usare le risorse: [Resource Manager e distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md). Questo articolo fornisce informazioni di hello e le procedure per il ripristino di macchine virtuali distribuite tramite il modello di gestione risorse hello.
>
>

Server di Backup di Azure gran parte delle funzionalità di backup del carico di lavoro hello eredita da Data Protection Manager (DPM). In questo articolo collega tooDPM documentazione tooexplain alcune hello le funzionalità condivise. Se il Server di Backup di Azure condivide molte delle hello stessa funzionalità di DPM. Server di Backup di Azure non eseguire il backup tootape, né si integra con System Center.

## <a name="1-choose-an-installation-platform"></a>1. Scegliere una piattaforma di installazione
Hello primo passo verso introduzione hello Azure Backup Server è tooset di un Server di Windows. in Azure o in locale.

### <a name="using-a-server-in-azure"></a>Uso di un server in Azure
Quando si sceglie un server per eseguire il server di Backup di Azure, è consigliabile usare come punto di partenza un'immagine della raccolta di Windows Server 2012 R2 Datacenter. articolo Hello [creare la prima macchina virtuale di Windows nel portale di Azure hello](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), viene fornita un'esercitazione per introduzione hello consigliata una macchina virtuale in Azure, anche se non si è mai utilizzato Azure in precedenza. Hello requisiti minimi consigliati per hello server virtual machine (VM) deve essere: A2 Standard con due core e 3,5 GB di RAM.

La protezione dei carichi di lavoro con il server di Backup di Azure è piuttosto complessa. articolo Hello [installare DPM come macchina virtuale di Azure](https://technet.microsoft.com/library/jj852163.aspx), aiuta a capire le sfumature. Prima di distribuire la macchina hello, leggere questo articolo completamente.

### <a name="using-an-on-premises-server"></a>Uso di un server locale
Se non si desidera toorun server di base hello in Azure, è possibile eseguire server hello in una macchina virtuale Hyper-V, una VM di VMware o un host fisico. Hello consigliabile requisiti minimi per l'hardware del server hello sono due core e 4 GB di RAM. in hello nella tabella seguente sono elencati i sistemi operativi supportato Hello:

| Sistema operativo | Piattaforma | SKU |
|:--- | --- |:--- |
| Windows Server 2012 R2 e più recenti SPs |64 bit |Standard, Datacenter, Foundation |
| Windows Server 2012 e versioni più recenti di SP |64 bit |Datacenter, Foundation, Standard |
| Windows Storage Server 2012 R2 e versioni più recenti di SP |64 bit |Standard, Workgroup |
| Windows Storage Server 2012 e versioni più recenti di SP |64 bit |Standard, Workgroup |

È possibile deduplicare l'archiviazione DPM hello con la deduplicazione di Windows Server. Vedere altre informazioni sull'interazione di [DPM e deduplicazione](https://technet.microsoft.com/library/dn891438.aspx) in caso di distribuzione in macchine virtuali Hyper-V.

> [!NOTE]
> Server di Backup di Azure è toorun progettato su un server dedicato esclusivamente alle funzioni. Non è possibile installare il server di Backup di Azure su:
> - Un computer in esecuzione come controller di dominio
> - Un computer in cui hello Server applicazioni è installato ruolo
> - Un computer che sia un server di gestione di System Center Operations Manager
> - Un computer su cui è in esecuzione Exchange Server
> - Un computer che sia un nodo di un cluster

Aggiungere sempre dominio tooa del Server di Backup di Azure. Se si prevede di dominio diverso tooa toomove hello server, è consigliabile unire in join i nuovo dominio hello server toohello prima di installare il Server di Backup di Azure. Lo spostamento di un Server di Backup di Azure esistente tooa nuovo dominio del computer dopo la distribuzione è *non supportato*.

## <a name="2-recovery-services-vault"></a>2. Insieme di credenziali dei servizi di ripristino
Se si invia dati di backup tooAzure o mantenerlo in locale, il software di hello deve tooAzure toobe connesso. toobe più specifici, computer Server di Backup di Azure hello deve toobe registrato con un insieme di credenziali di servizi di ripristino.

un ripristino toocreate services insieme di credenziali:

1. Accedi toohello [portale di Azure](https://portal.azure.com/).
2. Nel menu Hub hello, fare clic su **Sfoglia** e nell'elenco di hello delle risorse, digitare **servizi di ripristino**. Si inizia a digitare, hello filtri di elenco in base all'input. Fare clic su **Insiemi di credenziali dei servizi di ripristino**.

    ![Creare un insieme di credenziali dei servizi di ripristino - Passaggio 1](./media/backup-azure-microsoft-azure-backup/open-recovery-services-vault.png) <br/>

    viene visualizzato l'elenco di Hello degli insiemi di credenziali di servizi di ripristino.
3. In hello **insiemi di credenziali di servizi di ripristino** menu, fare clic su **Aggiungi**.

    ![Creare un insieme di credenziali dei servizi di ripristino - Passaggio 2](./media/backup-azure-microsoft-azure-backup/rs-vault-menu.png)

    Servizi di ripristino Hello insieme di credenziali si apre Pannello chiesto tooprovide un **nome**, **sottoscrizione**, **gruppo di risorse**, e **percorso**.

    ![Creare un insieme di credenziali dei servizi di ripristino - Passaggio 5](./media/backup-azure-microsoft-azure-backup/rs-vault-attributes.png)
4. Per **nome**, immettere un insieme di credenziali di nome descrittivo tooidentify hello. nome di Hello deve toobe univoco per la sottoscrizione di Azure hello. Digitare un nome che contenga tra i 2 e i 50 caratteri. Deve iniziare con una lettera e può contenere solo lettere, numeri e trattini.
5. Fare clic su **sottoscrizione** elenco disponibile di hello toosee delle sottoscrizioni. Se non sei sicuro che toouse di sottoscrizione, utilizzare predefinito hello (o suggerito) sottoscrizione. Sono disponibili più scelte solo se l'account dell'organizzazione è associato a più sottoscrizioni di Azure.
6. Fare clic su **gruppo di risorse** toosee hello l'elenco dei gruppi di risorse disponibili, oppure fare clic su **New** toocreate un nuovo gruppo di risorse. Per informazioni complete sui gruppi di risorse, vedere [Panoramica di Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)
7. Fare clic su **percorso** tooselect hello località geografica per l'insieme di credenziali hello.
8. Fare clic su **Crea**. Può richiedere un po' di tempo per hello toobe creato insieme di credenziali di servizi di ripristino. Monitorare le notifiche di stato hello in hello superiore destro area hello portale.
   Una volta creato l'insieme di credenziali, viene aperto nel portale di hello.

### <a name="set-storage-replication"></a>Impostare la replica di archiviazione
opzione di replica di archiviazione Hello consente toochoose tra l'archiviazione con ridondanza geografica e l'archiviazione con ridondanza locale. Per impostazione predefinita, l'insieme di credenziali prevede l'archiviazione con ridondanza geografica. Se questo insieme di credenziali è l'insieme di credenziali primario, lasciare hello archiviazione opzione set l'archiviazione con ridondanza toogeo. Se si vuole un'opzione più economica ma non altrettanto permanente, scegliere l'archiviazione con ridondanza locale. Altre informazioni sui [con ridondanza geografica](../storage/common/storage-redundancy.md#geo-redundant-storage) e [ridondanza locale](../storage/common/storage-redundancy.md#locally-redundant-storage) opzioni di archiviazione in hello [Cenni preliminari sulla replica di archiviazione di Azure](../storage/common/storage-redundancy.md).

impostazione di replica tooedit hello archiviazione:

1. Selezionare il dashboard dell'insieme di credenziali di insieme di credenziali tooopen hello e il pannello impostazioni hello. Se hello **impostazioni** non apre pannello, fare clic su **tutte le impostazioni** nel dashboard dell'insieme di credenziali hello.
2. In hello **impostazioni** pannello, fare clic su **Backup infrastruttura** > **la configurazione del Backup** tooopen hello **laconfigurazionedelBackup** blade. In hello **la configurazione del Backup** pannello, scegliere l'opzione di replica di archiviazione di hello per l'insieme di credenziali.

    ![Elenco degli insiemi di credenziali per il backup](./media/backup-azure-vms-first-look-arm/choose-storage-configuration-rs-vault.png)

    Dopo aver scelto l'opzione di archiviazione hello per l'insieme di credenziali, si è pronti tooassociate hello VM con insieme di credenziali hello. associazione hello toobegin, è necessario individuare e registrare hello macchine virtuali di Azure.

## <a name="3-software-package"></a>3. Pacchetto software
### <a name="downloading-hello-software-package"></a>Download del pacchetto software di hello
1. Accedi toohello [portale di Azure](https://portal.azure.com/).
2. Se è già aperto un insieme di credenziali di servizi di ripristino, procedere toostep 3. Se non è aperto un insieme di credenziali di servizi di ripristino, ma nel portale di Azure, nel menu Hub hello hello fare clic su **Sfoglia**.

   * Nell'elenco di hello delle risorse, digitare **servizi di ripristino**.
   * Si inizia a digitare, elenco hello verrà filtrato in base all'input. Quando viene visualizzata l'opzione, fare clic su **Insiemi di credenziali dei servizi di ripristino**.

     ![Creare un insieme di credenziali dei servizi di ripristino - Passaggio 1](./media/backup-azure-microsoft-azure-backup/open-recovery-services-vault.png)

     viene visualizzato l'elenco di Hello degli insiemi di credenziali di servizi di ripristino.
   * Hello l'elenco degli insiemi di credenziali di servizi di ripristino, selezionare un insieme di credenziali.

     Apre il dashboard di Hello insieme di credenziali selezionato.

     ![Pannello dell'insieme di credenziali aperto](./media/backup-azure-microsoft-azure-backup/vault-dashboard.png)
3. Hello **impostazioni** pannello visualizzata per impostazione predefinita. Se è chiuso, fare clic su **impostazioni** pannello delle impostazioni di tooopen hello.

    ![Pannello dell'insieme di credenziali aperto](./media/backup-azure-microsoft-azure-backup/vault-setting.png)
4. Fare clic su **Backup** attività iniziali guidate di hello tooopen.

    ![Attività iniziali di backup](./media/backup-azure-microsoft-azure-backup/getting-started-backup.png)

    In hello **Introduzione a backup** blade che viene aperta, **obiettivi Backup** verrà selezionato automaticamente.

    ![Backup-obiettivi-predefinito-aperto](./media/backup-azure-microsoft-azure-backup/getting-started.png)

5. In hello **Backup obiettivo** pannello da hello **in cui viene eseguito il carico di lavoro** dal menu **locale**.

    ![locale e carichi di lavoro come obiettivi](./media/backup-azure-microsoft-azure-backup/backup-goals-azure-backup-server.png)

    Da hello **cosa si desidera toobackup?** dal menu a discesa, i carichi di lavoro selezionare hello desidera tooprotect tramite il Server di Backup di Azure e quindi fare clic su **OK**.

    Hello **Introduzione a backup** guidata commutatori hello **Prepare infrastruttura** tooback opzione backup tooAzure i carichi di lavoro.

   > [!NOTE]
   > Se si vuole solo tooback backup di file e cartelle, è consigliabile tramite hello Azure Backup agent e hello istruzioni disponibili nell'articolo hello [innanzitutto: eseguire il backup dei file e cartelle](backup-try-azure-backup-in-10-mins.md). Se si intende tooprotect più file e cartelle o si intende protezione hello tooexpand è necessario in futuro hello, selezionare i carichi di lavoro.
   >
   >

    ![Attività iniziali guidate modifica](./media/backup-azure-microsoft-azure-backup/getting-started-prep-infra.png)

6. In hello **Prepare infrastruttura** blade che viene visualizzata, fare clic su hello **scaricare** collegamenti per installare Server di Backup di Azure e scarica credenziali. Utilizzare le credenziali dell'insieme di hello durante la registrazione dell'insieme di credenziali di Azure Backup Server toohello recovery services. Hello collegamenti è possibile toohello Download Center in cui hello pacchetto software può essere scaricato.

    ![Preparare l'infrastruttura per il Server di Backup di Azure](./media/backup-azure-microsoft-azure-backup/azure-backup-server-prep-infra.png)

7. Selezionare tutti i file hello e fare clic su **Avanti**. Download che tutti hello file provenienti da una pagina di download di Microsoft Azure Backup hello e sul posto che tutti hello file hello stessa cartella.

    ![Area download 1](./media/backup-azure-microsoft-azure-backup/downloadcenter.png)

    In quanto hello download dimensione di tutti i file hello insieme > 3G, su un collegamento di download di 10 Mbps che potrebbe richiedere fino a too60 minuti per hello scaricare toocomplete.

### <a name="extracting-hello-software-package"></a>L'estrazione del pacchetto software hello
Dopo aver scaricato tutti i file hello, fare clic su **MicrosoftAzureBackupInstaller.exe**. Verrà avviata hello **installazione guidata di Microsoft Azure Backup** tooextract hello sono presenti i file tooa percorso specificato dall'utente. Continua con la procedura guidata hello e fare clic su hello **estrarre** pulsante toobegin processo di estrazione hello.

> [!WARNING]
> Almeno 4GB di spazio libero è obbligatorio tooextract hello file di installazione.
>
>

![Backup di Microsoft Azure](./media/backup-azure-microsoft-azure-backup/extract/03.png)

Una volta processo di estrazione hello completo, hello toolaunch casella di controllo hello appena estratti *setup.exe* toobegin l'installazione di Microsoft Azure Backup Server, fare clic su hello **fine** pulsante.

### <a name="installing-hello-software-package"></a>L'installazione del pacchetto software hello
1. Fare clic su **Backup di Microsoft Azure** installazione guidata di toolaunch hello.

    ![Backup di Microsoft Azure](./media/backup-azure-microsoft-azure-backup/launch-screen2.png)
2. Nella schermata iniziale di hello fare clic su hello **Avanti** pulsante. Consente di passare toohello *Prerequisite Checks* sezione. In questa schermata, fare clic su **controllare** toodetermine se sono stati soddisfatti prerequisiti hardware e software di hello per il Server di Backup di Azure. Se tutti i prerequisiti vengono soddisfatti, si verrà visualizzato un messaggio che indica che tale macchina hello soddisfa i requisiti di hello. Fare clic su hello **Avanti** pulsante.

    ![Server di backup di Azure - Pagina iniziale e controllo dei prerequisiti](./media/backup-azure-microsoft-azure-backup/prereq/prereq-screen2.png)
3. Pacchetto di installazione del Server di Backup di Azure hello fornito in dotazione con hello appropriato SQL Server i file binari necessiti Server di Backup di Microsoft Azure richiede SQL Server Standard. Quando si avvia con una nuova installazione di Server di Backup di Azure, è consigliabile scegliere l'opzione hello **installare nuovi istanza di SQL Server con il programma di installazione** e fare clic su hello **controlla e installa** pulsante. Una volta installati i prerequisiti di hello correttamente, fare clic su **Avanti**.

    ![Server di backup di Azure - Controllo SQL](./media/backup-azure-microsoft-azure-backup/sql/01.png)

    Se si verifica un errore con una macchina di hello toorestart raccomandazione, eseguire questa operazione e fare clic su **controlla di nuovo**.

   > [!NOTE]
   > Il server di Backup di Azure non funzionerà con un'istanza remota di SQL Server. istanza di Hello utilizzato dal Server di Backup di Azure deve toobe locale.
   >
   >
4. Specificare un percorso di installazione di hello dei file server di Backup di Microsoft Azure e fare clic su **Avanti**.

    ![PreReq2 di Backup di Microsoft Azure](./media/backup-azure-microsoft-azure-backup/space-screen.png)

    percorso di file temporanei Hello è un requisito necessario per eseguire il backup tooAzure. Verificare il percorso di file temporanei di hello trovi almeno il 5% dei dati di hello pianificati backup cloud toohello toobe. Per la protezione disco, i dischi separati devono toobe configurati al termine dell'installazione di hello. Per altre informazioni sui pool di archiviazione, vedere [Configurare i pool di archiviazione e l'archiviazione su disco](https://technet.microsoft.com/library/hh758075.aspx).
5. Fornire una password complessa per gli account utente locali con restrizioni e fare clic su **Avanti**.

    ![PreReq2 di Backup di Microsoft Azure](./media/backup-azure-microsoft-azure-backup/security-screen.png)
6. Selezionare se si desidera toouse *Microsoft Update* toocheck per gli aggiornamenti e fare clic su **Avanti**.

   > [!NOTE]
   > Si consiglia di gestire Windows Update reindirizzare tooMicrosoft aggiornamento, che offre protezione e importanti aggiornamenti per Windows e altri prodotti come Server di Backup di Microsoft Azure.
   >
   >

    ![PreReq2 di Backup di Microsoft Azure](./media/backup-azure-microsoft-azure-backup/update-opt-screen2.png)
7. Hello revisione *Riepilogo impostazioni* e fare clic su **installare**.

    ![PreReq2 di Backup di Microsoft Azure](./media/backup-azure-microsoft-azure-backup/summary-screen.png)
8. installazione di Hello avviene in fasi. In hello fase prima hello agente servizi di ripristino di Microsoft Azure è installato nel server di hello. procedura guidata di Hello controlla anche la connettività Internet. Se è disponibile la connettività Internet è possibile procedere con l'installazione, in caso contrario è necessario tooprovide proxy dettagli tooconnect toohello Internet.

    passaggio successivo Hello è hello tooconfigure agente servizi di ripristino di Microsoft Azure. Come parte della configurazione di hello, sarà necessario tooprovide i servizi di ripristino di insieme di credenziali le credenziali tooregister hello macchina toohello insieme di credenziali. Fornirà anche un passphrase tooencrypt/decrittografare hello i dati inviati tra Azure e locale. È possibile generare automaticamente una passphrase o fornire una passphrase personalizzata con un minimo di 16 caratteri. Per procedere con la procedura guidata hello hello agente è stato configurato.

    ![PreReq2 del server di backup di Azure](./media/backup-azure-microsoft-azure-backup/mars/04.png)
9. Una volta completata correttamente la registrazione del server di Backup di Microsoft Azure hello, hello complessivo installazione guidata procede toohello installazione e configurazione di SQL Server e i componenti Server di Backup di Azure hello. Al termine dell'installazione componenti di SQL Server hello, vengono installati i componenti Server di Backup di Azure hello.

    ![Server di backup di Azure](./media/backup-azure-microsoft-azure-backup/final-install/venus-installation-screen.png)

Al termine della procedura di installazione di hello, hello icone sul desktop del prodotto è state create anche. Fare doppio clic sul prodotto di hello icona toolaunch hello.

### <a name="add-backup-storage"></a>Aggiungere risorse di archiviazione di backup
copia di backup prima di Hello viene mantenuta in archiviazione collegata toohello macchina Server di Backup di Azure. Per altre informazioni sull'aggiunta di dischi, vedere [Configurare i pool di archiviazione e l'archiviazione su disco](https://technet.microsoft.com/library/hh758075.aspx).

> [!NOTE]
> È necessario un archivio di backup tooadd anche se si prevede di toosend tooAzure di dati. Nell'architettura corrente di hello del Server di Backup di Azure, insieme di credenziali di Backup di Azure hello contiene hello *secondo* copia dei dati di hello durante l'archiviazione locale hello contiene hello primo (e obbligatorio) copia di backup.
>
>

## <a name="4-network-connectivity"></a>4. Connettività di rete
Server di Backup di Azure richiede servizio Azure Backup toohello di connettività per hello prodotto toowork correttamente. toovalidate se macchina hello è hello connettività tooAzure, utilizzare hello ```Get-DPMCloudConnection``` cmdlet nella console di PowerShell per Azure Backup Server hello. Se hello output del cmdlet hello è TRUE, quindi la connettività è presente, altrimenti è possibile nessuna connettività.

Hello contemporaneamente, hello sottoscrizione di Azure deve toobe in uno stato integro. toofind stato hello di sottoscrizione e toomanage Accedi toohello [portale sottoscrizione](https://account.windowsazure.com/Subscriptions).

Quando si conosce lo stato di hello di hello Azure connettività e di hello sottoscrizione di Azure, è possibile utilizzare tabella hello seguente toofind out impatto hello sulla funzionalità di backup/ripristino hello offerto.

| Stato di connettività | Sottoscrizione di Azure | Eseguire il backup tooAzure | Eseguire il backup toodisk | Ripristino da Azure | Ripristino da disco |
| --- | --- | --- | --- | --- | --- |
| Connesso |Attivo |Consentito |Consentito |Consentito |Consentito |
| Connesso |Scaduto |Arrestato |Arrestato |Consentito |Consentito |
| Connesso |Deprovisioning eseguito |Arrestato |Arrestato |Arrestato e punti di ripristino di Azure eliminati |Arrestato |
| Connettività persa > 15 giorni |Attivo |Arrestato |Arrestato |Consentito |Consentito |
| Connettività persa > 15 giorni |Scaduto |Arrestato |Arrestato |Consentito |Consentito |
| Connettività persa > 15 giorni |Deprovisioning eseguito |Arrestato |Arrestato |Arrestato e punti di ripristino di Azure eliminati |Arrestato |

### <a name="recovering-from-loss-of-connectivity"></a>Recupero dalla perdita di connettività
Se si dispone di un firewall o un proxy che impedisce l'accesso tooAzure, è necessario hello toowhitelist seguito gli indirizzi di dominio nel profilo del firewall/proxy hello:

* www.msftncsi.com
* \*.Microsoft.com
* \*.WindowsAzure.com
* \*.microsoftonline.com
* \*.windows.net

Una volta connettività tooAzure toohello ripristinato macchina del Server di Backup di Azure, operazioni hello che possono essere eseguite dipendono dalle hello lo stato della sottoscrizione di Azure. tabella Hello precedente include dettagli sulle operazioni di hello è consentite una volta macchina hello è "connesso".

### <a name="handling-subscription-states"></a>Gestione degli stati della sottoscrizione
È possibile tootake una sottoscrizione di Azure da un *scaduto* o *Deprovisioned* stato toohello *Active* stato. Tuttavia questo fatto ha alcune implicazioni sul comportamento del prodotto hello mentre non è stato hello *Active*:

* Oggetto *Deprovisioned* sottoscrizione perde la funzionalità per il periodo hello che viene sottoposta a deprovisioning. In attivazione *Active*, le funzionalità del prodotto hello di backup o ripristino vengano ripristinata. dati di backup Hello sul disco locale hello possono essere recuperati anche se è stata mantenuta con un periodo di memorizzazione sufficientemente grande. Tuttavia, dati di backup hello in Azure sono perditi definitiva dopo la sottoscrizione hello immette hello *Deprovisioned* stato.
* Una sottoscrizione *Scaduta* perde funzionalità solo fino a quando non viene resa di nuovo *Attiva*. Stato di tutti i backup pianificati per il periodo di hello hello sottoscrizione *scaduto* non verrà eseguito.

## <a name="troubleshooting"></a>Risoluzione dei problemi
Se il server di Microsoft Azure Backup ha esito negativo con errori durante la fase di installazione hello (o di backup o ripristino), fare riferimento toothis [documento i codici di errore](https://support.microsoft.com/kb/3041338) per ulteriori informazioni.
È anche possibile fare riferimento troppo[Backup di Azure correlate domande frequenti](backup-azure-backup-faq.md)

## <a name="next-steps"></a>Passaggi successivi
È possibile ottenere informazioni dettagliate [preparazione dell'ambiente per DPM](https://technet.microsoft.com/library/hh758176.aspx) nel sito Microsoft TechNet hello. Contiene anche informazioni sulle configurazioni supportate in cui è possibile distribuire e usare il server di Backup di Azure.

È possibile utilizzare questi toogain articoli una comprensione più approfondita di protezione del carico di lavoro utilizzando il server di Backup di Microsoft Azure.

* [Backup di SQL Server](backup-azure-backup-sql.md)
* [Backup di SharePoint Server](backup-azure-backup-sharepoint.md)
* [Backup del server alternativo](backup-azure-alternate-dpm-server.md)
