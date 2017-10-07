---
title: aaaUse tooback di Server di Backup di Azure backup portale classico di carichi di lavoro tooAzure | Documenti Microsoft
description: Verificare che l'ambiente sia preparato correttamente tooback dei carichi di lavoro tramite il Server di Backup di Azure
services: backup
documentationcenter: 
author: pvrk
manager: shivamg
editor: 
keywords: server di backup di azure; insieme di credenziali di backup
ms.assetid: d86450e8-da63-4283-8fd7-2ee629fa14ab
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: masaran;trinadhk;pullabhk;markgal
ms.openlocfilehash: 7b574824c448096e0c0ba74a872ab8f2a434f6a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-tooback-up-workloads-using-azure-backup-server"></a>Preparazione tooback dei carichi di lavoro tramite il Server di Backup di Azure
> [!div class="op_single_selector"]
> * [Server di backup di Azure](backup-azure-microsoft-azure-backup.md)
> * [SCDPM](backup-azure-dpm-introduction.md)
> * [Server di Backup di Azure (classico)](backup-azure-microsoft-azure-backup-classic.md)
> * [SCDPM (classico)](backup-azure-dpm-introduction-classic.md)
>
>

Questo articolo contiene informazioni sulla preparazione tooback l'ambiente dei carichi di lavoro tramite il Server di Backup di Azure. Con il server di Backup di Azure è possibile proteggere i carichi di lavoro dell'applicazione, ad esempio macchine virtuali Hyper-V, Microsoft SQL Server, SharePoint Server, Microsoft Exchange e i client di Windows, da una singola console.

> [!WARNING]
> Server di Backup di Azure eredita le funzionalità di hello di Data Protection Manager (DPM) per il backup del carico di lavoro. Sono disponibili puntatori documentazione tooDPM per alcune di queste funzionalità. Il server di Backup di Azure, tuttavia, non fornisce la protezione su nastro o l'integrazione con System Center.
>
>

## <a name="1-windows-server-machine"></a>1. Computer Windows Server
![passaggio1](./media/backup-azure-microsoft-azure-backup/step1.png)

Hello primo passo verso introduzione hello Azure Backup Server è toohave una macchina Windows Server.

| Percorso | Requisiti minimi | Istruzioni aggiuntive |
| --- | --- | --- |
| Azure |Macchina virtuale IaaS di Azure<br><br>A2 Standard: 2 core, 3,5 GB di RAM |È possibile iniziare con una semplice immagine della raccolta di Windows Server 2012 R2 Datacenter. [protezione dei carichi di lavoro IaaS con il server di Backup di Azure (DPM)](https://technet.microsoft.com/library/jj852163.aspx) è piuttosto complessa. Assicurarsi di leggere articolo hello completamente prima di distribuire la macchina hello. |
| Locale |Macchina virtuale Hyper-V,<br> Macchina virtuale di VMware<br> o un host fisico<br><br>2 core e 4 GB di RAM |È possibile deduplicare l'archiviazione DPM hello con la deduplicazione di Windows Server. Vedere altre informazioni sull'interazione di [DPM e deduplicazione](https://technet.microsoft.com/library/dn891438.aspx) in caso di distribuzione in macchine virtuali Hyper-V. |

> [!NOTE]
> È consigliabile installare il server di Backup di Azure in un computer con Windows Server 2012 R2 Datacenter. I prerequisiti di hello rientrano automaticamente con la versione più recente di hello del sistema operativo di Windows hello.
>
>

Se si prevede di dominio di tooa toojoin Server di Backup di Azure, è consigliabile aggiungere i server fisico hello o dominio toohello macchina virtuale prima di installare software Server di Backup di Azure hello. Lo spostamento di un Server di Backup di Azure tooa nuovo dominio, dopo la distribuzione, è *non supportato*.

## <a name="2-backup-vault"></a>2. Insieme di credenziali per il backup
![passaggio2](./media/backup-azure-microsoft-azure-backup/step2.png)

Se si invia dati di backup tooAzure o mantenerlo localmente, hello Azure Backup Server deve essere registrato tooa insieme di credenziali. Se un nuovo Backup di Azure gli utenti toouse Server di Backup di Azure, vedere hello Azure versione del portale di questo articolo - [preparare tooback dei carichi di lavoro tramite il Server di Backup di Azure](backup-azure-microsoft-azure-backup.md).

> [!IMPORTANT]
> A partire da marzo 2017, è possibile utilizzare non è più insiemi di credenziali Backup hello toocreate portale classico.
> È ora possibile aggiornare i servizi archivi di Backup gli insiemi di credenziali tooRecovery. Per informazioni dettagliate, vedere l'articolo hello [aggiornare un tooa insieme di credenziali di Backup dell'insieme di credenziali di servizi di ripristino](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft incoraggia gli utenti tooupgrade insiemi di credenziali di servizi tooRecovery insiemi di credenziali di Backup.<br/> Dopo 15 ottobre 2017, è possibile utilizzare gli insiemi di credenziali di PowerShell toocreate Backup. **Entro il 1° novembre 2017**:
>- Tutti gli archivi di Backup rimanenti verrà automaticamente aggiornato tooRecovery servizi insiemi di credenziali.
>- Si sarà in grado di tooaccess ai dati di backup nel portale classico hello. Utilizzare invece hello Azure tooaccess portale i dati di backup in insiemi di servizi di ripristino.
>



## <a name="3-software-package"></a>3. Pacchetto software
![passaggio3](./media/backup-azure-microsoft-azure-backup/step3.png)

### <a name="downloading-hello-software-package"></a>Download del pacchetto software di hello
Credenziali toovault simili, è possibile scaricare Microsoft Azure Backup per i carichi di lavoro dell'applicazione da hello **pagina avvio rapido** dell'insieme di credenziali di backup hello.

1. Fare clic su **per applicazione carichi di lavoro (disco tooDisk tooCloud)**. Questa operazione richiederà pagina dell'area Download toohello dal quale pacchetto software hello può essere scaricato.

    ![Schermata iniziale di Backup di Microsoft Azure](./media/backup-azure-microsoft-azure-backup/dpm-venus1.png)
2. Fare clic su **Download**.

    ![Area download 1](./media/backup-azure-microsoft-azure-backup/downloadcenter1.png)
3. Selezionare tutti i file hello e fare clic su **Avanti**. Download che tutti hello file provenienti da una pagina di download di Microsoft Azure Backup hello e sul posto che tutti hello file hello stessa cartella.
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
2. Nella schermata iniziale di hello fare clic su hello **Avanti** pulsante. Consente di passare toohello *Prerequisite Checks* sezione. In questa schermata, fare clic su hello **controllare** pulsante toodetermine se sono stati soddisfatti prerequisiti hardware e software di hello per il Server di Backup di Azure. Se tutti i prerequisiti siano hello sono stati soddisfatti correttamente, si verrà visualizzato un messaggio che indica che tale macchina hello soddisfa i requisiti di hello. Fare clic su hello **Avanti** pulsante.

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

    passaggio successivo Hello è hello tooconfigure agente servizi di ripristino di Microsoft Azure. Come parte della configurazione di hello, sarà necessario tooprovide l'hello archivio credenziali tooregister hello macchina toohello backup insieme di credenziali. Fornirà anche un passphrase tooencrypt/decrittografare hello i dati inviati tra Azure e locale. È possibile generare automaticamente una passphrase o fornire una passphrase personalizzata con un minimo di 16 caratteri. Per procedere con la procedura guidata hello hello agente è stato configurato.

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
![passaggio4](./media/backup-azure-microsoft-azure-backup/step4.png)

Server di Backup di Azure richiede servizio Azure Backup toohello di connettività per hello prodotto toowork correttamente. toovalidate se macchina hello è hello connettività tooAzure, utilizzare hello ```Get-DPMCloudConnection``` cmdlet nella console di PowerShell per Azure Backup Server hello. Se hello output del cmdlet hello è TRUE, quindi la connettività è presente, altrimenti è possibile nessuna connettività.

Hello contemporaneamente, hello sottoscrizione di Azure deve toobe in uno stato integro. toofind stato hello di sottoscrizione e toomanage Accedi toohello [portale sottoscrizione](https://account.windowsazure.com/Subscriptions).

Quando si conosce lo stato di hello di hello Azure connettività e di hello sottoscrizione di Azure, è possibile utilizzare tabella hello seguente toofind out impatto hello sulla funzionalità di backup/ripristino hello offerto.

| Stato di connettività | Sottoscrizione di Azure | Backup tooAzure | Backup toodisk | Ripristino da Azure | Ripristino da disco |
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
