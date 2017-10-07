---
title: aaaUse DPM tooback backup portale tooAzure i carichi di lavoro | Documenti Microsoft
description: Toobacking un'introduzione dei server DPM con il servizio di Azure Backup hello
services: backup
documentationcenter: 
author: adigan
manager: nkolli
editor: 
keywords: System Center Data Protection Manager, data protection manager, backup di dpm
ms.assetid: c8c322cf-f5eb-422c-a34c-04a4801bfec7
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: adigan;giridham;jimpark;markgal;trinadhk
ms.openlocfilehash: 1dd988ae55012ac7dc485d2416458542c60b6ae3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-tooback-up-workloads-tooazure-with-dpm"></a>Preparazione tooback dei carichi di lavoro tooAzure con Data Protection Manager
> [!div class="op_single_selector"]
> * [Server di backup di Azure](backup-azure-microsoft-azure-backup.md)
> * [SCDPM](backup-azure-dpm-introduction.md)
> * [Server di Backup di Azure (classico)](backup-azure-microsoft-azure-backup-classic.md)
> * [SCDPM (classico)](backup-azure-dpm-introduction-classic.md)
>
>

Questo articolo fornisce un tooprotect di Microsoft Azure Backup toousing Introduzione i server di System Center Data Protection Manager (DPM) e i carichi di lavoro. Le informazioni dell'articolo riguardano:

* Il funzionamento del backup del server DPM di Azure
* Hello prerequisiti tooachieve un'esperienza uniforme di backup
* Hello tipico errori rilevati e in che modo toodeal con essi
* Scenari supportati

> [!NOTE]
> Azure offre due modelli di distribuzione per creare e usare le risorse: [Resource Manager e distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md). Questo articolo fornisce informazioni di hello e le procedure per il ripristino di macchine virtuali distribuite tramite il modello di gestione risorse hello.
>
>

DPM di System Center esegue il backup di file e dati delle applicazioni. Dati sottoposti a backup tooDPM possono essere archiviati su nastro, disco, o backup tooAzure con Backup di Microsoft Azure. DPM interagisce con Backup di Azure nei modi seguenti:

* **DPM distribuito come macchina virtuale locale o server fisica** -se DPM viene distribuito come server fisico o come macchina virtuale Hyper-V locale è possibile eseguire il backup dei dati tooa servizi di ripristino credenziali inoltre toodisk e backup su nastro.
* **DPM distribuito come macchina virtuale di Azure** : a partire dalla versione di System Center 2012 R2 con aggiornamento 3, DPM può essere distribuito come macchina virtuale di Azure. Se DPM viene distribuito come macchina virtuale di Azure che è possibile eseguire il backup dei dati tooAzure dischi collegati toohello macchina virtuale Azure DPM oppure puoi eseguire l'offload archiviazione dei dati hello eseguendone il backup tooa che insieme di credenziali di servizi di ripristino.

## <a name="why-backup-from-dpm-tooazure"></a>Motivo per cui eseguire il backup da Data Protection Manager tooAzure?
Hello business vantaggi dell'utilizzo di Azure Backup per il backup dei server DPM includono:

* Per la distribuzione di DPM in locale, è possibile utilizzare Azure come un tootape distribuzione termine toolong alternativo.
* Per le distribuzioni DPM in Azure, Backup di Azure consente archiviazione toooffload dal disco di Azure, hello e tooscale backup archiviando i dati precedenti nell'insieme di credenziali di servizi di ripristino e i nuovi dati sul disco.

## <a name="prerequisites"></a>Prerequisiti
Preparare il Backup di Azure tooback backup dei dati DPM come segue:

1. **Creare un insieme di credenziali di Servizi di ripristino** : creare un insieme di credenziali nel portale di Azure.
2. **Scaricare l'insieme di credenziali** , scaricare le credenziali di hello utilizzabile tooregister hello DPM server tooRecovery Services insieme di credenziali.
3. **Installare Azure Backup Agent hello** : da Backup di Azure, installare l'agente hello in ogni server DPM.
4. **Registrare server hello** : registro hello DPM server tooRecovery Services dell'insieme di credenziali.

### <a name="1-create-a-recovery-services-vault"></a>1. Creare un insieme di credenziali di Servizi di ripristino
un ripristino toocreate services insieme di credenziali:

1. Accedi toohello [portale di Azure](https://portal.azure.com/).
2. Nel menu Hub hello, fare clic su **Sfoglia** e nell'elenco di hello delle risorse, digitare **servizi di ripristino**. Si inizia a digitare, elenco hello verrà filtrato in base all'input. Fare clic su **Insiemi di credenziali dei servizi di ripristino**.

    ![Creare un insieme di credenziali dei servizi di ripristino - Passaggio 1](./media/backup-azure-dpm-introduction/open-recovery-services-vault.png)

    viene visualizzato l'elenco di Hello degli insiemi di credenziali di servizi di ripristino.
3. In hello **insiemi di credenziali di servizi di ripristino** menu, fare clic su **Aggiungi**.

    ![Creare un insieme di credenziali dei servizi di ripristino - Passaggio 2](./media/backup-azure-dpm-introduction/rs-vault-menu.png)

    Servizi di ripristino Hello insieme di credenziali si apre Pannello chiesto tooprovide un **nome**, **sottoscrizione**, **gruppo di risorse**, e **percorso**.

    ![Creare un insieme di credenziali dei servizi di ripristino - Passaggio 5](./media/backup-azure-dpm-introduction/rs-vault-attributes.png)
4. Per **nome**, immettere un insieme di credenziali di nome descrittivo tooidentify hello. nome di Hello deve toobe univoco per la sottoscrizione di Azure hello. Digitare un nome che contenga tra i 2 e i 50 caratteri. Deve iniziare con una lettera e può contenere solo lettere, numeri e trattini.
5. Fare clic su **sottoscrizione** elenco disponibile di hello toosee delle sottoscrizioni. Se non sei sicuro che toouse di sottoscrizione, utilizzare predefinito hello (o suggerito) sottoscrizione. Sono presenti scelte multiple solo se l'account dell'organizzazione è associato a più sottoscrizioni di Azure.
6. Fare clic su **gruppo di risorse** toosee hello l'elenco dei gruppi di risorse disponibili, oppure fare clic su **New** toocreate un nuovo gruppo di risorse. Per informazioni complete sui gruppi di risorse, vedere [Panoramica di Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)
7. Fare clic su **percorso** tooselect hello località geografica per l'insieme di credenziali hello.
8. Fare clic su **Crea**. Può richiedere un po' di tempo per hello toobe creato insieme di credenziali di servizi di ripristino. Monitorare le notifiche di stato hello in hello superiore destro area hello portale.
   Una volta creato l'insieme di credenziali, viene aperto nel portale di hello.

### <a name="set-storage-replication"></a>Impostare la replica di archiviazione
opzione di replica di archiviazione Hello consente toochoose tra l'archiviazione con ridondanza geografica e l'archiviazione con ridondanza locale. Per impostazione predefinita, l'insieme di credenziali prevede l'archiviazione con ridondanza geografica. Lasciare l'archiviazione con ridondanza toogeo hello opzione set, se si tratta del backup primario. Se si vuole un'opzione più economica ma non altrettanto permanente, scegliere l'archiviazione con ridondanza locale. Altre informazioni sui [con ridondanza geografica](../storage/common/storage-redundancy.md#geo-redundant-storage) e [ridondanza locale](../storage/common/storage-redundancy.md#locally-redundant-storage) opzioni di archiviazione in hello [Cenni preliminari sulla replica di archiviazione di Azure](../storage/common/storage-redundancy.md).

impostazione di replica tooedit hello archiviazione:

1. Selezionare il dashboard dell'insieme di credenziali di insieme di credenziali tooopen hello e il pannello impostazioni hello. Se hello **impostazioni** non apre pannello, fare clic su **tutte le impostazioni** nel dashboard dell'insieme di credenziali hello.
2. In hello **impostazioni** pannello, fare clic su **Backup infrastruttura** > **la configurazione del Backup** tooopen hello **laconfigurazionedelBackup** blade. In hello **la configurazione del Backup** pannello, scegliere l'opzione di replica di archiviazione di hello per l'insieme di credenziali.

    ![Elenco degli insiemi di credenziali per il backup](./media/backup-azure-vms-first-look-arm/choose-storage-configuration-rs-vault.png)

    Dopo aver scelto l'opzione di archiviazione hello per l'insieme di credenziali, si è pronti tooassociate hello VM con insieme di credenziali hello. associazione hello toobegin, è necessario individuare e registrare hello macchine virtuali di Azure.

### <a name="2-download-vault-credentials"></a>2. Scaricare le credenziali dell’insieme di credenziali
file delle credenziali dell'insieme di credenziali Hello è un certificato generato dal portale hello per ogni insieme di credenziali di backup. portale Hello carica quindi hello toohello chiave pubblica del servizio di controllo di accesso (ACS). chiave privata di Hello del certificato di hello è attivata la modalità utente toohello disponibile come parte del flusso di lavoro hello fornito come input per il flusso di lavoro di hello macchina registrazione. Consente di autenticare hello macchina toosend dati di backup identificato tooan insieme di credenziali in hello servizio Azure Backup.

insieme di credenziali Hello viene utilizzato solo durante il flusso di lavoro di hello registrazione. È tooensure responsabilità dell'utente hello che l'insieme di credenziali non venga compromessa file hello. Se si trova in mani hello di qualsiasi utente non autorizzato, hello insieme di credenziali le credenziali file può essere utilizzato tooregister altre macchine hello stesso insieme di credenziali. Tuttavia, come dati di backup hello sono crittografati con una passphrase che appartiene toohello cliente, i dati di backup esistenti non possono essere compromesso. toomitigate questo problema, l'insieme di credenziali viene impostata tooexpire in 48hrs. È possibile scaricare l'insieme di credenziali hello di servizi di ripristino di un qualsiasi numero di volte, ma è applicabile solo hello file più recente dell'insieme di credenziali delle credenziali durante il flusso di lavoro di hello registrazione.

file delle credenziali dell'insieme di credenziali Hello viene scaricato tramite un canale protetto da hello portale di Azure. Hello servizio Azure Backup non è a conoscenza della chiave privata di hello del certificato hello e la chiave privata di hello non è persistenti nel portale di hello o servizio hello. Utilizzare hello seguendo i passaggi toodownload hello archivio credenziali file tooa computer locale.

1. Accedi toohello [portale di Azure](https://portal.azure.com/).
2. Aprire toowhich della toowhich insieme di credenziali di servizi di ripristino si desidera tooregister DPM macchina.
3. Per impostazione predefinita si apre il pannello Impostazioni. Se è chiuso, fare clic su **impostazioni** nel pannello impostazioni hello tooopen dei dashboard dell'insieme di credenziali. Nel pannello Impostazioni fare clic su **Proprietà**.

    ![Pannello dell'insieme di credenziali aperto](./media/backup-azure-dpm-introduction/vault-settings-dpm.png)
4. Nella pagina delle proprietà hello, fare clic su **scaricare** in **le credenziali di Backup**. portale di Hello genera i file di credenziali dell'insieme di credenziali di hello, che viene reso disponibili per il download.

    ![Scaricare](./media/backup-azure-dpm-introduction/vault-credentials.png)

portale Hello genererà un insieme di credenziali utilizzando una combinazione di nome insieme di credenziali hello e hello data corrente. Fare clic su **salvare** toodownload hello archivio credenziali toohello account locale cartella di download o scegliere Salva con nome hello salvare menu toospecify un percorso per l'insieme di credenziali hello. Occuperà minuto tooa per toobe file hello generato.

### <a name="note"></a>Nota
* Verificare che hello insieme di credenziali delle credenziali viene salvato in una posizione accessibile dal computer. Se è stata archiviata in un condivisione di file/SMB, la verifica delle autorizzazioni di accesso hello.
* file delle credenziali dell'insieme di credenziali Hello viene utilizzato solo durante il flusso di lavoro di hello registrazione.
* file delle credenziali dell'insieme di credenziali Hello scade dopo 48hrs e può essere scaricato dal portale hello.

### <a name="3-install-backup-agent"></a>3. Installare un agente di Backup
Dopo aver creato l'insieme di credenziali di Backup di Azure hello, deve essere installato un agente in ogni computer Windows (Windows Server, client di Windows, server System Center Data Protection Manager o il computer Server di Backup di Azure) che consente di eseguire il backup dei dati e delle applicazioni tooAzure.

1. Aprire toowhich della toowhich insieme di credenziali di servizi di ripristino si desidera tooregister DPM macchina.
2. Per impostazione predefinita si apre il pannello Impostazioni. Se è chiuso, fare clic su **impostazioni** pannello delle impostazioni di tooopen hello. Nel pannello Impostazioni fare clic su **Proprietà**.

    ![Pannello dell'insieme di credenziali aperto](./media/backup-azure-dpm-introduction/vault-settings-dpm.png)
3. Nella pagina Impostazioni hello, fare clic su **scaricare** in **Azure Backup Agent**.

    ![Scaricare](./media/backup-azure-dpm-introduction/azure-backup-agent.png)

   Una volta scaricate agente hello, fare doppio clic su installazione di hello toolaunch MARSAgentInstaller.exe dell'agente di Backup di Azure hello. Scegliere la cartella di installazione hello e la cartella dei file temporanei necessari per l'agente di hello. percorso della cache di Hello specificato deve disporre di spazio disponibile ovvero almeno il 5% dei dati di backup hello.
4. Se si utilizza un toohello tooconnect di server proxy internet, hello **configurazione Proxy** schermata, immettere i dettagli del server proxy hello. Se si utilizza un proxy autenticato, immettere i dettagli di nome e una password utente hello in questa schermata.
5. l'agente di Backup di Azure Hello installazione di .NET Framework 4.5 e Windows PowerShell (se non è già disponibile) toocomplete hello.
6. Dopo aver installato l'agente di hello, **Chiudi** finestra hello.

   ![Chiudi](../../includes/media/backup-install-agent/dpm_FinishInstallation.png)
7. troppo**registro hello Server DPM** toohello insieme di credenziali, in hello **Management** scheda, fare clic su **Online**. Selezionare quindi **Registra**. Si aprirà hello registrazione guidata di installazione.
8. Se si utilizza un toohello tooconnect di server proxy internet, hello **configurazione Proxy** schermata, immettere i dettagli del server proxy hello. Se si utilizza un proxy autenticato, immettere i dettagli di nome e una password utente hello in questa schermata.

    ![Configurazione proxy](../../includes/media/backup-install-agent/DPM_SetupOnlineBackup_Proxy.png)
9. Nella schermata di credenziali dell'insieme di credenziali di hello, Sfoglia tooand hello selezionare insieme di credenziali le credenziali che è stato scaricato in precedenza.

    ![Credenziali di insieme](../../includes/media/backup-install-agent/DPM_SetupOnlineBackup_Credentials.jpg)

    file delle credenziali dell'insieme di credenziali Hello è valido solo per 48 ore (dopo che è stato scaricato dal portale hello). Se si verifica un errore in questa schermata (ad esempio, "Insieme di credenziali le credenziali di file specificato è scaduto"), account di accesso toohello Azure portal e scaricare hello archivio credenziali file nuovamente.

    Verificare che il file di credenziali dell'insieme di credenziali hello è disponibile in una posizione in cui è possibile accedere da un'applicazione hello il programma di installazione. Se si verificano errori correlati di accedere, hello copia l'insieme di credenziali file tooa percorso temporaneo in questo computer e riprova l'operazione di hello.

    Se si verifica un errore di credenziali dell'insieme di credenziali non valido (ad esempio, "non valido insieme di credenziali fornito") è danneggiato o non avere hello credenziali più recenti associate al servizio di ripristino hello di file hello. Ripetere l'operazione di hello dopo il download di un nuovo file delle credenziali dell'insieme di credenziali dal portale hello. Questo errore si verifica in genere se hello utente fa clic su hello **Download insieme di credenziali** opzione nel portale di Azure in rapida successione hello. In questo caso, solo hello secondo insieme di credenziali file delle credenziali è valido.
10. utilizzo di hello toocontrol di larghezza di banda di rete durante il lavoro e le ore non lavorative, in hello **la limitazione delle richieste di impostazione** schermata, è possibile impostare i limiti di utilizzo della larghezza di banda hello e definire il lavoro hello e non lavorative ore.

    ![Impostazione di limitazione](../../includes/media/backup-install-agent/DPM_SetupOnlineBackup_Throttling.png)
11. In hello **impostazione cartella ripristino** schermata, Sfoglia per cartelle di hello in cui scaricare i file hello da Azure verranno inserite temporaneamente.

    ![Impostazioni cartella di ripristino](../../includes/media/backup-install-agent/DPM_SetupOnlineBackup_RecoveryFolder.png)
12. In hello **impostazione di crittografia** schermata, è possibile generare una passphrase o fornire una passphrase (minimo 16 caratteri). Tenere presente che toosave hello passphrase in un luogo sicuro.

    ![Crittografia](../../includes/media/backup-install-agent/DPM_SetupOnlineBackup_Encryption.png)

    > [!WARNING]
    > Se hello passphrase viene persa o dimenticata; Consente di recuperare i dati di backup hello non consente di Microsoft. Microsoft non abbiano visibilità sul passphrase hello utilizzata dall'utente finale di hello utente finale di Hello proprietario hello passphrase di crittografia. Salvare il file hello in un luogo sicuro in quanto è necessario durante un'operazione di ripristino.
    >
    >
13. Dopo aver scelto hello **registrare** pulsante, hello macchina è stata registrata toohello insieme di credenziali e si sono ora pronti toostart backup tooMicrosoft Azure.
14. Quando si usa Data Protection Manager, è possibile modificare le impostazioni di hello specificate durante il flusso di lavoro di hello registrazione facendo hello **configura** opzione selezionando **Online** in hello  **Gestione** scheda.

## <a name="requirements-and-limitations"></a>Requisiti e limitazioni
* DPM può essere eseguito come server fisico o come macchina virtuale Hyper-V installata in System Center 2012 SP1 o System Center 2012 R2. Inoltre, è possibile eseguirlo come macchina virtuale di Azure in System Center 2012 R2 (con almeno l'aggiornamento cumulativo 3 di DPM 2012 R2) oppure come macchina virtuale di Windows in VMware con System Center 2012 R2 e almeno il relativo aggiornamento cumulativo 5.
* Se DPM viene eseguito con System Center 2012 SP1, è necessario installare l'aggiornamento cumulativo 2 per System Center Data Protection Manager SP1. Ciò è necessario prima di poter installare hello Azure Backup Agent.
* server di Data Protection Manager Hello deve disporre di Windows PowerShell e .net Framework 4.5 installati.
* DPM può eseguire il backup la maggior parte dei carichi di lavoro tooAzure Backup. Per un elenco completo dei componenti supportati, vedere hello Backup di Azure supporta i seguenti elementi.
* Impossibile ripristinare i dati archiviati in Azure Backup con l'opzione "copia tootape" hello.
* È necessario un account Azure con funzionalità di Backup di Azure hello abilitata. Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti. Informazioni sui [prezzi di Backup di Azure](https://azure.microsoft.com/pricing/details/backup/).
* Tramite Azure Backup richiede hello Azure Backup Agent toobe installato nei server di hello tooback da backup. Ogni server deve essere almeno il 5% delle dimensioni hello dati hello che viene eseguito il backup, disponibile come archiviazione locale disponibile. Ad esempio backup 100 GB di dati richiede un minimo di 5 GB di spazio disponibile nel percorso temporaneo hello.
* Verranno archiviati i dati in archiviazione di Azure dell'insieme di credenziali hello. Nessun importo toohello limite dei dati che è possibile eseguire il backup tooan Azure Backup vault ma dimensioni hello di un'origine dati (ad esempio una macchina virtuale o un database) non devono superare 54400 GB.

Questi tipi di file sono supportati per eseguire il backup tooAzure:

* Crittografati (solo backup completi)
* Compressi (backup incrementali supportati)
* Sparse (backup incrementali supportati)
* Compressi e sparse (considerati come sparse)

Questi tipi di file non sono supportati:

* I server nei file system che distinguono fra minuscole e maiuscole non sono supportati.
* Collegamenti reali (ignorati)
* Reparse point (ignorati)
* Crittografati e compressi (ignorati)
* Crittografati e sparse (ignorati)
* Flusso compresso
* Flusso di tipo sparse

> [!NOTE]
> Da in System Center 2012 DPM con SP1 in poi, è possibile eseguire il backup dei carichi di lavoro protetti da DPM tooAzure con Backup di Microsoft Azure.
>
>
