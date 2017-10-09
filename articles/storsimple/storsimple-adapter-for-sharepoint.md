---
title: Adattatore StorSimple per SharePoint aaaInstall | Documenti Microsoft
description: Viene descritto come tooinstall e configurare o rimuovere hello adattatore StorSimple per SharePoint in una server farm di SharePoint.
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 36c20b75-f2e5-4184-a6b5-9c5e618f79b2
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/06/2017
ms.author: v-sharos
ms.openlocfilehash: 9a7347232fb80156d93212e6382cdd4fab98a2d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-hello-storsimple-adapter-for-sharepoint"></a>Installare e configurare hello adattatore StorSimple per SharePoint
## <a name="overview"></a>Panoramica
Hello adattatore StorSimple per SharePoint è un componente che consente di fornire l'archiviazione di Microsoft Azure StorSimple flessibili e data protection tooSharePoint server farm. È possibile utilizzare hello adapter toomove oggetto BLOB (Binary Large) contenuti hello SQL Server database del contenuto toohello Microsoft Azure StorSimple hybrid cloud dispositivo di archiviazione.

Hello adattatore StorSimple per SharePoint funziona come un provider di archiviazione BLOB remoti (RBS) e utilizza hello toostore funzionalità di archiviazione BLOB remoti di SQL Server contenuto di SharePoint non strutturato (sotto forma di hello di BLOB) in un file server supportato da un dispositivo StorSimple.

> [!NOTE]
> Hello adattatore StorSimple per SharePoint supporta SharePoint Server 2010 Remote BLOB Storage (RBS). Non supporta Archiviazione BLOB esterni di SharePoint Server 2010 (EBS).


* hello toodownload adattatore StorSimple per SharePoint, andare troppo[adattatore StorSimple per SharePoint] [ 1] in hello Microsoft Download Center.
* Per informazioni sulla pianificazione di RBS e RBS limitazioni, andare troppo[decidere toouse RBS in SharePoint 2013] [ 2] o [pianificare RBS (SharePoint Server 2010)] [3].

Hello resto di questa panoramica descrive brevemente ruolo hello hello adattatore StorSimple per SharePoint e hello capacità di SharePoint e i limiti delle prestazioni che è necessario conoscere prima di installare e configurare l'adattatore hello. Dopo avere esaminato queste informazioni, andare troppo[dell'adattatore StorSimple per l'installazione di SharePoint](#storsimple-adapter-for-sharepoint-installation) toobegin impostazione adapter hello.

### <a name="storsimple-adapter-for-sharepoint-benefits"></a>Vantaggi dell’adattatore StorSimple per SharePoint
In un sito di SharePoint, il contenuto viene archiviato come dati BLOB non strutturati in uno o più database del contenuto. Per impostazione predefinita, questi database sono ospitati in computer che eseguono SQL Server e si trovano nella server farm di SharePoint hello. Le dimensioni dei BLOB possono aumentare rapidamente, consumando ingenti quantità di spazio di archiviazione locale. Per questo motivo, è opportuno toofind soluzione meno costosa archiviazione un altro. SQL Server fornisce una tecnologia denominata archiviazione Blob remoti (RBS) che consente di archiviare il contenuto BLOB nel file system hello, all'esterno del database di SQL Server hello. BLOB possono risiedere nel sistema del file hello computer hello che esegue SQL Server con RBS, o che possano essere archiviate nel file system di hello in un altro computer server.

RBS richiede l'utilizzo di un provider RBS, ad esempio hello adattatore StorSimple per SharePoint, tooenable RBS in SharePoint. Hello adattatore StorSimple per SharePoint funziona con RBS, consentendo di spostare server tooa BLOB supportato dal sistema di Microsoft Azure StorSimple hello. Microsoft Azure StorSimple quindi Archivia i dati BLOB hello in locale o cloud hello, in base all'utilizzo. I BLOB molto attivi (in genere indicati tooas livello 1 o hot data) si trova in locale. I dati meno attivi e i dati di archiviazione si trovano nel cloud hello. Dopo aver abilitato RBS su un database di contenuto, qualsiasi nuovo contenuto BLOB creato in SharePoint viene archiviato nel dispositivo StorSimple hello e non nel database di contenuto hello.

implementazione di Microsoft Azure StorSimple Hello di RBS offre hello seguenti vantaggi:

* Lo spostamento BLOB tooa contenuto server separato, consente di ridurre il carico di query hello su SQL Server, che consente di migliorare la velocità di risposta di SQL Server. 
* Azure StorSimple Usa tecniche di deduplicazione e compressione tooreduce dimensioni dei dati.
* Azure StorSimple offre protezione dei dati in formato hello locale e gli snapshot cloud. Inoltre, se si archivia database hello nel dispositivo StorSimple hello, è possibile eseguire il backup database del contenuto hello e dei blob insieme in modo anomalo. (Lo spostamento di dispositivo toohello database del contenuto hello è supportato solo per hello dispositivo StorSimple serie 8000. Questa funzionalità non è supportata per la serie 5000 o 7000 di hello.)
* StorSimple di Azure include funzionalità di ripristino di emergenza tra cui il failover, il ripristino di file e volumi (inclusi i test di ripristino) e un ripristino rapido dei dati.
* È possibile utilizzare software di ripristino di dati, ad esempio Kroll Ontrack PowerControls, con snapshot StorSimple BLOB tooperform a livello di elemento di ripristino dei dati del contenuto di SharePoint. Questo software di ripristino dati costituisce un acquisto separato.
* Hello adattatore StorSimple per SharePoint si collega il portale di amministrazione centrale SharePoint hello, consentendo toomanage l'intera soluzione SharePoint da una posizione centrale.

Lo spostamento di sistema di file BLOB toohello contenuto può fornire altri risparmi di costi e benefici. Ad esempio, tramite RBS può ridurre hello necessità di costose di archiviazione di livello 1 e, poiché riduce i database di contenuto hello, RBS può ridurre il numero di hello di database richiesti nella server farm di SharePoint hello. Tuttavia, altri fattori, ad esempio i limiti delle dimensioni del database e la quantità di hello di contenuto non RBS, possono influenzare i requisiti di archiviazione. Per ulteriori informazioni sui costi di hello e vantaggi dell'uso di RBS, vedere [pianificare RBS (SharePoint Foundation 2010)] [ 4] e [decidere toouse RBS in SharePoint 2013] [ 5].

### <a name="capacity-and-performance-limits"></a>Limiti di capacità e prestazioni
Prima di considerare l'uso di RBS nella soluzione SharePoint, è necessario tenere in considerazione prestazioni hello testato e limiti di capacità di SharePoint Server 2010 e SharePoint Server 2013 e correlazione tooacceptable prestazioni da parte di questi limiti. Per ulteriori informazioni, vedere [Limiti del software e limiti per SharePoint 2013](https://technet.microsoft.com/library/cc262787.aspx).

Prima di configurare RBS, esaminare il seguente hello:

* Verificare che la dimensione totale hello di hello contenuto (hello dimensioni di un database del contenuto) più dimensioni di hello di tutti i BLOB esternalizzati associati superare il limite delle dimensioni RBS hello supportato da SharePoint. Questo limite è pari a 200 GB. 
  
    **database del contenuto toomeasure e le dimensioni BLOB**
  
  1. Eseguire questa query per hello WFE di amministrazione centrale. Avviare Shell di gestione SharePoint hello e quindi immettere hello dimensioni di Windows PowerShell comandi tooget hello hello dei database di contenuto seguente:
     
     `Get-SPContentDatabase | Select-Object -ExpandProperty DiskSizeRequired`
     
      Questo passaggio Ottiene le dimensioni di hello hello del database del contenuto su disco di hello.
  2. Eseguire uno dei hello seguente query SQL in SQL Management Studio nella finestra hello SQL server in ogni database del contenuto e aggiungere hello risultato toohello numero ottenuto nel passaggio 1.
     
     Nei database del contenuto di SharePoint 2013, immettere:
     
     `SELECT SUM([Size]) FROM [ContentDatabaseName].[dbo].[DocStreams] WHERE [Content] IS NULL`
     
     Nei database del contenuto di SharePoint 2010, immettere:
     
     `SELECT SUM([Size]) FROM [ContentDatabaseName].[dbo].[AllDocs] WHERE [Content] IS NULL`
     
     Questo passaggio Ottiene le dimensioni di hello di blob che sono stati esternalizzati hello.
* È consigliabile archiviare tutto il contenuto BLOB e database localmente nel dispositivo StorSimple hello. dispositivo StorSimple Hello è un cluster a due nodi per la disponibilità elevata. Inserimento di database del contenuto hello e BLOB nel dispositivo StorSimple hello garantisce un'elevata disponibilità.
  
    Utilizzare tradizionale SQL Server migrazione best practices toomove hello database del contenuto toohello dispositivo StorSimple. Spostare il database di hello solo dopo che tutto il contenuto BLOB dal database hello è stata spostata toohello condivisione di file tramite RBS. Se si sceglie il dispositivo StorSimple toohello di toomove hello database del contenuto, è consigliabile configurare hello archiviazione del database del contenuto nel dispositivo hello come volume principale.
* In Microsoft Azure StorSimple, se si utilizza volumi a livelli, non è possibile tooguarantee che contenuto archiviato localmente nel dispositivo StorSimple hello non saranno a più livelli tooMicrosoft archiviazione cloud di Azure. Di conseguenza, si consiglia di utilizzare i volumi StorSimple aggiunti in locale in combinazione con RBS di SharePoint, Questo garantisce che tutto il contenuto BLOB rimane in locale nel dispositivo StorSimple hello e non viene spostata tooMicrosoft Azure.
* Se non si archiviano i database del contenuto hello nel dispositivo StorSimple hello, utilizzare tradizionale SQL Server la disponibilità elevata procedure consigliate che supportano RBS. Il clustering di SQL Server supporta RBS, mentre il mirroring di SQL Server no. 

> [!WARNING]
> Se RBS non è stato abilitato, è preferibile non spostare dispositivo StorSimple toohello di hello database del contenuto. Si tratta di una configurazione non testata.

## <a name="storsimple-adapter-for-sharepoint-installation"></a>Installazione dell'adattatore StorSimple per SharePoint
Prima di installare hello adattatore StorSimple per SharePoint, è necessario configurare il dispositivo di StorSimple hello e verificare che server farm di SharePoint hello e le istanze di SQL Server soddisfino tutti i prerequisiti. Questa esercitazione vengono descritti i requisiti di configurazione, nonché le procedure per l'installazione e aggiornamento hello adattatore StorSimple per SharePoint.

## <a name="configure-prerequisites"></a>Configurazione dei prerequisiti
Prima di installare hello adattatore StorSimple per SharePoint, verificare che il dispositivo di StorSimple hello, server farm di SharePoint e la creazione di istanze di SQL Server soddisfino hello seguenti prerequisiti.

### <a name="system-requirements"></a>Requisiti di sistema
Adattatore StorSimple per SharePoint Hello funziona con hello dell'hardware e software:

* Sistema operativo a supportato: Windows Server 2008 R2 SP1, Windows Server 2012 o Windows Server 2012 R2.
* Versioni supportate di SharePoint: SharePoint Server 2010 o SharePoint Server 2013
* Versioni supportate di SQL Server: SQL Server 2008 Enterprise Edition, SQL Server 2008 R2 Enterprise Edition o SQL Server 2012 Enterprise Edition
* Dispositivi StorSimple supportati: StorSimple serie 8000, StorSimple serie 7000 o StorSimple serie 5000.

### <a name="storsimple-device-configuration-prerequisites"></a>Prerequisiti di configurazione del dispositivo StorSimple
dispositivo StorSimple Hello è un dispositivo a blocchi e di conseguenza è necessario un file server in cui è possono includere dati hello. È consigliabile utilizzare un server separato rispetto a un server esistente dalla farm di SharePoint hello. Questo file server deve essere in hello rete stesso locale (LAN) come computer di SQL Server hello che contiene hello i database del contenuto.

> [!TIP]
> * Se si configura la farm di SharePoint per la disponibilità elevata, è necessario distribuire anche hello file server per la disponibilità elevata.
> * Se non si archiviano i database di contenuto hello nel dispositivo StorSimple hello, usare la disponibilità elevata tradizionali procedure consigliate che supportano RBS. Il clustering di SQL Server supporta RBS, mentre il mirroring di SQL Server no. 


Assicurarsi che il dispositivo StorSimple sia configurato correttamente e che toosupport volumi appropriati della distribuzione di SharePoint sono configurati e accessibili dal computer SQL Server. Andare troppo[distribuire il dispositivo StorSimple locale](storsimple-8000-deployment-walkthrough-u2.md) se è non ancora distribuito e configurato il dispositivo StorSimple. Prendere nota hello di indirizzo IP del dispositivo StorSimple hello. sarà necessario durante l'adattatore StorSimple per l'installazione di SharePoint.

Inoltre, assicurarsi che toobe volume hello utilizzato per l'esternalizzazione dei BLOB soddisfi hello seguenti requisiti:

* Hello volume deve essere formattato con una dimensione di unità di allocazione di 64 KB.
* Il front-end web (WFE) e server applicazioni deve essere in grado di tooaccess hello tramite un percorso UNC Universal Naming Convention ().
* server farm di SharePoint Hello deve essere configurato toowrite toohello volume.

> [!NOTE]
> Dopo avere installato e configurare l'adattatore di hello, tutti i processi di esternalizzazione dei BLOB devono transitare attraverso il dispositivo di StorSimple hello (dispositivo hello presentare hello volumi tooSQL Server e gestirà i livelli di archiviazione hello). Non è possibile utilizzare altre destinazioni per l'esternalizzazione dei BLOB.


Se si prevede di toouse gestione Snapshot StorSimple tootake snapshot di hello BLOB e database di dati, essere tooinstall che StorSimple Snapshot Manager nel server di database hello in modo che è possibile usare il servizio Writer SQL tooimplement hello hello Copia Shadow del Volume di Windows Service (VSS).

> [!IMPORTANT]
> Gestione Snapshot StorSimple non supporta SharePoint VSS Writer hello e non può eseguire l'applicazione-snapshot coerenti dei dati di SharePoint. In uno scenario di SharePoint, Gestione snapshot StorSimple fornisce soltanto backup coerenti con l'arresto anomalo del sistema.


## <a name="sharepoint-farm-configuration-prerequisites"></a>Prerequisiti di configurazione di SharePoint
Assicurarsi che la server farm di SharePoint sia configurata correttamente, come indicato di seguito:

* Verificare che la server farm di SharePoint è in uno stato integro e verificare hello seguenti:
* Tutti i server applicazioni nella farm hello registrato e WFE di SharePoint sono in esecuzione e possa essere eseguito il ping dal server hello in cui verrà installato hello adattatore StorSimple per SharePoint.
* Hello servizio Timer di SharePoint (SPTimerV3 o SPTimerV4) è in esecuzione in ogni server front-end Web e server applicazioni.
* Hello servizio Timer di SharePoint sia il pool di applicazioni IIS hello in cui hello Amministrazione centrale SharePoint sito è in esecuzione con privilegi amministrativi.
* Verificare che Internet Explorer Enhanced Security Context (IE ESC) sia disabilitato. Seguire questi toodisable passaggi avanzata di Internet Explorer:
  
  1. Chiudere tutte le istanze di Internet Explorer.
  2. Avviare Server Manager hello.
  3. Nel riquadro di sinistra hello, fare clic su **Server locale**.
  4. In hello destro riquadro accanto troppo**sicurezza avanzata di Internet Explorer**, fare clic su **su**.
  5. In **Amministratori** fare clic su **Disattivo**.
  6. Fare clic su **OK**.

## <a name="remote-blob-storage-rbs-prerequisites"></a>Prerequisiti di archiviazione BLOB remoti (RBS) 
Verificare che sia in uso una versione supportata di SQL Server. Solo hello sono riportate le versioni supportate e in grado di toouse RBS:

* SQL Server 2008 Enterprise Edition
* SQL Server 2008 R2 Enterprise Edition
* SQL Server 2012 Enterprise Edition

Solo i volumi che hello dispositivo StorSimple presenta tooSQL Server, è possano esternalizzare i BLOB in. Non sono supportate altre destinazioni per l'esternalizzazione dei BLOB.

Dopo avere completato tutti i passaggi di configurazione dei prerequisiti, andare troppo[hello di installazione dell'adattatore StorSimple per SharePoint](#install-the-storsimple-adapter-for-sharepoint).

## <a name="install-hello-storsimple-adapter-for-sharepoint"></a>Installare hello adattatore StorSimple per SharePoint
Utilizzare hello seguendo i passaggi tooinstall hello adattatore StorSimple per SharePoint. Se si sta reinstallando il software di hello, vedere [aggiornare o reinstallare hello adattatore StorSimple per SharePoint](#upgrade-or-reinstall-the-storsimple-adapter-for-sharepoint). tempo Hello necessario per l'installazione di hello dipende dal numero totale di hello di database di SharePoint nella server farm di SharePoint.

[!INCLUDE [storsimple-install-sharepoint-adapter](../../includes/storsimple-install-sharepoint-adapter.md)]

## <a name="configure-rbs"></a>Configurare SSL
Dopo aver installato hello adattatore StorSimple per SharePoint, configurare RBS come descritto nella seguente procedura hello.

> [!TIP]
> pagina di amministrazione centrale SharePoint hello, consentendo di RBS toobe abilitato o disabilitato su ogni database del contenuto nella farm di SharePoint hello si collega Hello adattatore StorSimple per SharePoint. Tuttavia, abilitazione o disabilitazione di RBS nel database del contenuto hello determina la reimpostazione di IIS, che, a seconda della configurazione della farm, può interrompere momentaneamente la disponibilità di hello di hello SharePoint front-end web (WFE). (Fattori, ad esempio utilizzare hello di un front-end di bilanciamento carico di lavoro server corrente hello e così via, possono limitare o evitare l'interruzione). tooprotect agli utenti di un'interruzione, si consiglia di abilitare o disabilitare RBS solo durante una finestra di manutenzione pianificata.


[!INCLUDE [storsimple-sharepoint-adapter-configure-rbs](../../includes/storsimple-sharepoint-adapter-configure-rbs.md)]

## <a name="configure-garbage-collection"></a>Configurare Garbage Collection
Quando gli oggetti vengono eliminati da un sito di SharePoint, questi non vengono eliminati automaticamente da hello volume dell'archivio RBS. Al contrario, un asincrona, il programma di manutenzione in background Elimina BLOB orfani dall'archivio file hello. Gli amministratori di sistema è possono pianificare questo processo toorun periodicamente o avviarlo quando necessario.

Questo programma di manutenzione (Microsoft.Data.SqlRemoteBlobs.Maintainer.exe) viene installato automaticamente su tutti i server WFE e server applicazioni di SharePoint quando si abilita RBS. programma Hello viene installato nella seguente posizione hello: *unità di avvio*: \Programmi\Microsoft SQL Remote Blob Storage 10.50\Maintainer\

Per informazioni sulla configurazione e utilizzando il programma di manutenzione di hello, vedere [mantenere RBS in SharePoint Server 2013][8].

> [!IMPORTANT]
> il programma di manutenzione RBS Hello è molte risorse. È consigliabile pianificare toorun solo durante i periodi di minore attività per la farm di SharePoint hello.


### <a name="delete-orphaned-blobs-immediately"></a>Eliminare BLOB orfani immediatamente
Se è necessario immediatamente BLOB toodelete isolati (orfani), è possibile utilizzare hello attenendosi alle istruzioni. Si noti che queste istruzioni sono un esempio di come questa operazione può essere eseguita in un ambiente di SharePoint 2013 con hello seguenti componenti:

* nome del database del contenuto Hello è WSS_Content.
* nome del Server SQL Hello è SHRPT13 SQL12\SHRPT13.
* nome dell'applicazione web Hello è SharePoint – 80.

[!INCLUDE [storsimple-sharepoint-adapter-garbage-collection](../../includes/storsimple-sharepoint-adapter-garbage-collection.md)]

## <a name="upgrade-or-reinstall-hello-storsimple-adapter-for-sharepoint"></a>Aggiornare o reinstallare hello adattatore StorSimple per SharePoint
Utilizzare hello seguente server di SharePoint tooupgrade procedure e quindi reinstallare l'adattatore StorSimple per l'aggiornamento di SharePoint o toosimply o adapter hello in una server farm di SharePoint esistente.

> [!IMPORTANT]
> Esaminare le seguenti informazioni prima di tentare tooupgrade hello il software di SharePoint e/o l'aggiornamento o reinstallare hello adattatore StorSimple per SharePoint:
> 
> * Tutti i file precedentemente spostati archiviazione tooexternal tramite RBS non saranno disponibili fino al termine di reinstallazione hello e hello funzionalità RBS riabilitata. utente toolimit sulle, eseguire qualsiasi aggiornamento o reinstallazione durante una finestra di manutenzione pianificata.
> * Hello tempi hello aggiornamento o la reinstallazione possono variare in base al numero totale di hello di database di SharePoint nella server farm di SharePoint hello.
> * Al termine dell'aggiornamento o la reinstallazione hello, è necessario tooenable RBS per i database del contenuto hello. Per altre informazioni, vedere [Configurare RBS](#configure-rbs) .
> * Se si configura RBS per una farm di SharePoint che dispone di un numero molto elevato di database (maggiori di 200), hello **Amministrazione centrale SharePoint** pagina potrebbe scadere. In questo caso, aggiornare la pagina hello. Questa operazione non influenza il processo di configurazione di hello.


[!INCLUDE [storsimple-upgrade-sharepoint-adapter](../../includes/storsimple-upgrade-sharepoint-adapter.md)]

## <a name="storsimple-adapter-for-sharepoint-removal"></a>Rimozione dell’adattatore StorSimple per SharePoint
Hello, seguire le procedure seguenti descrivono come toomove BLOB hello il database del contenuto di SQL Server toohello e quindi disinstallare hello adattatore StorSimple per SharePoint. 

> [!IMPORTANT]
> Si dispone di database del contenuto nascosto toohello toomove hello BLOB prima di disinstallare il software di adapter hello.


### <a name="before-you-begin"></a>Prima di iniziare
Raccogliere le seguenti informazioni prima di spostare dati hello eseguire il backup di database del contenuto di SQL Server toohello e avviare la rimozione di hello adapter hello:

* Hello nomi di tutti i database di hello per cui RBS è abilitato
* il percorso UNC Hello di hello configurato archivio BLOB

### <a name="move-hello-blobs-back-toohello-content-databases"></a>Spostare i database del contenuto di hello BLOB toohello indietro
Prima di disinstallare hello adattatore StorSimple per il software di SharePoint, è necessario eseguire la migrazione di tutti i blob che sono stati esternalizzati toohello backup database del contenuto di SQL Server hello. Se si tenta toouninstall hello adattatore StorSimple per SharePoint prima di spostare tutti hello BLOB back toohello database del contenuto, si noterà hello seguente messaggio di avviso.

![Messaggio di avviso](./media/storsimple-adapter-for-sharepoint/sasp1.png)

#### <a name="toomove-hello-blobs-back-toohello-content-databases"></a>database del contenuto toomove hello BLOB toohello indietro
1. Scaricare tutti gli oggetti di esternalizzare hello.
2. Aprire hello **Amministrazione centrale SharePoint** pagina e passare troppo**le impostazioni di sistema**.
3. Nella sezione**Azure StorSimple** fare clic su **Configure StorSimple Adapter** (Configura adattatore StorSimple).
4. In hello **configura l'adattatore StorSimple** pagina, fare clic su hello **disabilitare** pulsante sotto ogni hello database del contenuto che si desidera tooremove dalla risorsa di archiviazione BLOB esterna. 
5. Eliminare gli oggetti di hello da SharePoint e caricarli nuovamente.

In alternativa, è possibile utilizzare Microsoft hello` RBS Migrate()` cmdlet di PowerShell incluso in SharePoint. Per ulteriori informazioni, vedere [Migrazione del contenuto in o da RBS](https://technet.microsoft.com/library/ff628255.aspx).

Dopo aver spostato i database del contenuto di hello BLOB toohello indietro, passare passaggio successivo toohello: [adapter hello Disinstalla](#uninstall-the-adapter).

### <a name="uninstall-hello-adapter"></a>Disinstallare l'adapter hello
Dopo aver spostato i database del contenuto hello BLOB back toohello SQL Server, utilizzare una delle seguenti opzioni toouninstall hello adattatore StorSimple per SharePoint hello.

#### <a name="toouse-hello-installation-program-toouninstall-hello-adapter"></a>adapter di toouse hello installazione programma toouninstall hello
1. Utilizzare un account con toolog di privilegi di amministratore nel server di toohello web front-end (WFE).
2. Fare doppio clic hello adattatore StorSimple per l'installazione di SharePoint. Avvia Hello installazione guidata.
   
    ![Installazione guidata](./media/storsimple-adapter-for-sharepoint/sasp2.png)
3. Fare clic su **Avanti**. verrà visualizzata la seguente pagina Hello.
   
    ![Pagina di rimozione dell’istallazione guidata](./media/storsimple-adapter-for-sharepoint/sasp3.png)
4. Fare clic su **rimuovere** tooselect processo di rimozione hello. verrà visualizzata la seguente pagina Hello.
   
    ![Pagina di conferma dell'installazione guidata](./media/storsimple-adapter-for-sharepoint/sasp4.png)
5. Fare clic su **rimuovere** rimozione hello tooconfirm. verrà visualizzata la finestra di Hello dopo lo stato di avanzamento.
   
    ![Pagina di stato di avanzamento dell'installazione guidata](./media/storsimple-adapter-for-sharepoint/sasp5.png)
6. Una volta completata la rimozione di hello, verrà visualizzata la pagina fine hello. Fare clic su **fine** tooclose hello installazione guidata.

#### <a name="toouse-hello-control-panel-toouninstall-hello-adapter"></a>scheda hello toouninstall di toouse hello Pannello di controllo
1. Aprire Pannello di controllo hello e quindi fare clic su **programmi e funzionalità**.
2. Selezionare **Adattatore StorSimple per SharePoint**, quindi fare clic su **Disinstalla**.

## <a name="next-steps"></a>Passaggi successivi
[Ulteriori informazioni su StorSimple](storsimple-overview.md).

<!--Reference links-->
[1]: https://www.microsoft.com/download/details.aspx?id=44073
[2]: https://technet.microsoft.com/library/ff628583(v=office.15).aspx
[3]: https://technet.microsoft.com/library/ff628583(v=office.14).aspx
[4]: https://technet.microsoft.com/library/ff628569(v=office.14).aspx
[5]: https://technet.microsoft.com/library/ff628583(v=office.15).aspx
[8]: https://technet.microsoft.com/en-us/library/ff943565.aspx
