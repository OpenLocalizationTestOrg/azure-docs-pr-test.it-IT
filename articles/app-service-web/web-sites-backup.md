---
title: aaaBack backup dell'app in Azure
description: Informazioni su come backup toocreate delle App in Azure App Service.
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: 6223b6bd-84ec-48df-943f-461d84605694
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2016
ms.author: cephalin
ms.openlocfilehash: e41d93d322bbc48b45b28eeaa817928d83c2b9d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-your-app-in-azure"></a>Eseguire il backup dell'app in Azure
Hello eseguire il backup e ripristino di funzionalità in [Azure App Service](../app-service/app-service-value-prop-what-is.md) consente di creare con facilità backup app manualmente o in una pianificazione. È possibile ripristinare hello app tooa istantanea dello stato precedente la sovrascrittura app esistenti di hello o tooanother ripristino. 

Per informazioni sul ripristino di un'app dal backup, vedere [Ripristinare un'app nel Servizio app di Azure](web-sites-restore.md).

<a name="whatsbackedup"></a>

## <a name="what-gets-backed-up"></a>Elementi di cui viene eseguito il backup
Servizio App può eseguire il backup seguenti hello informazioni tooan account di archiviazione Azure e di aver configurato il toouse app contenitore. 

* Configurazione dell'app
* Contenuto del file
* Database connesso tooyour app

Hello seguenti soluzioni di database è supportato con funzionalità di backup: 
   - [Database SQL](https://azure.microsoft.com/en-us/services/sql-database/)
   - [Database di Azure per MySQL (anteprima)](https://azure.microsoft.com/en-us/services/mysql)
   - [Database di Azure per PostgreSQL (anteprima)](https://azure.microsoft.com/en-us/services/postgres)
   - [ClearDB MySQL](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)
   - [MySQL in-app](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)
 

> [!NOTE]
>  Ciascun backup è una copia offline completa dell'app, non un aggiornamento incrementale.
>  

<a name="requirements"></a>

## <a name="requirements-and-restrictions"></a>Requisiti e restrizioni
* Hello eseguire il backup e ripristino funzionalità richiede hello toobe piano di servizio App in hello **Standard** livello o **Premium** livello. Per ulteriori informazioni sulla scalabilità del toouse piano di servizio App un livello superiore, vedere [scalare in verticale un'app in Azure](web-sites-scale.md).  
  Il livello **Premium** consente un maggior numero di backup giornalieri rispetto al livello **Standard**.
* È necessario un account di archiviazione di Azure e un contenitore in hello hello app che si desidera toobackup stessa sottoscrizione. Per ulteriori informazioni sugli account di archiviazione di Azure, vedere hello [collegamenti](#moreaboutstorage) alla fine di hello di questo articolo.
* I backup possono essere too10 GB di contenuto di applicazione e il database. Se dimensioni hello del backup superano questo limite, viene visualizzato un errore.

<a name="manualbackup"></a>

## <a name="create-a-manual-backup"></a>Creare un backup manuale
1. In hello [portale Azure](https://portal.azure.com), passare a pannello tooyour dell'app, selezionare **backup**. Hello **backup** pannello verrà visualizzato.
   
    ![Pagina Backups][ChooseBackupsPage]
   
   > [!NOTE]
   > Se viene visualizzato il messaggio hello riportato di seguito, scegliere tooupgrade piano di servizio App prima di procedere con i backup.
   > Per altre informazioni, vedere [Scalare un'app Web in Servizio app di Azure](web-sites-scale.md) .  
   > ![Scelta dell'account di archiviazione](./media/web-sites-backup/01UpgradePlan1.png)
   > 
   > 

2. In hello **Backup** pannello, fare clic su **configura**
![fare clic su Configura.](./media/web-sites-backup/ClickConfigure1.png)
3. In hello **la configurazione del Backup** pannello, fare clic su **archiviazione: non configurato** tooconfigure un account di archiviazione.
   
    ![Scegliere l'account di archiviazione][ChooseStorageAccount]
4. Scegliere la destinazione del backup selezionando un **Account di archiviazione** e un **Contenitore**. account di archiviazione Hello devono appartenere toohello app hello si desidera ripristinare tooback stessa sottoscrizione. Se si desidera, è possibile creare un nuovo account di archiviazione o di un nuovo contenitore in pannelli dei rispettivi hello. Al termine, fare clic su **Seleziona**.
   
    ![Scegliere l'account di archiviazione](./media/web-sites-backup/02ChooseStorageAccount1-1.png)
5. In hello **la configurazione del Backup** blade che ancora viene lasciato aperto, è possibile configurare **Backup Database**, quindi selezionare i database di hello desiderate tooinclude nei backup hello (database SQL o MySQL), quindi fare clic su **OK**.  
   
    ![Scegliere l'account di archiviazione](./media/web-sites-backup/03ConfigureDatabase1.png)
   
   > [!NOTE]
   > Per un database tooappear in questo elenco, la relativa stringa di connessione deve esistere in hello **le stringhe di connessione** sezione di hello **le impostazioni dell'applicazione** pannello per l'app.
   > 
   > 
6. In hello **la configurazione del Backup** pannello, fare clic su **salvare**.    
7. In hello **backup** pannello, fare clic su **Backup**.
   
    ![Pulsante BackUp Now][BackUpNow]
   
    Viene visualizzato un messaggio di stato di avanzamento durante il processo di backup hello.

Dopo aver configurato l'account di archiviazione di hello e contenitore è possibile avviare un backup manuale in qualsiasi momento.  

<a name="automatedbackups"></a>

## <a name="configure-automated-backups"></a>Configurazione dei backup automatici
1. In hello **la configurazione del Backup** pannello, impostare **backup pianificati** troppo**su**. 
   
    ![Scegliere l'account di archiviazione](./media/web-sites-backup/05ScheduleBackup1.png)
2. Pianificazione del backup verranno visualizzate le opzioni, impostare **Backup pianificati** troppo**su**, quindi configurare la pianificazione del backup hello come desiderato e fare clic su **OK**.
   
    ![Abilitazione dei backup automatici][SetAutomatedBackupOn]

<a name="partialbackups"></a>

## <a name="configure-partial-backups"></a>Configurare backup parziali
In alcuni casi non si desidera toobackup tutti gli elementi nella tua app. Di seguito sono disponibili alcuni esempi:

* Si [configurano backup settimanali](web-sites-backup.md#configure-automated-backups) dell'app che contiene contenuto statico che non cambia mai, ad esempio immagini o post di blog precedenti.
* L'app con oltre 10 GB di contenuto (quantità massima di hello che è possibile eseguire il backup in un momento).
* Per evitare che i file di log toobackup hello.

I backup parziali permetterà di scegliere esattamente i file a cui si desidera toobackup.

### <a name="exclude-files-from-your-backup"></a>Escludere file dal backup
Si supponga di che avere un'applicazione che contiene i file di log e le immagini statiche che sono state backup una volta e non prevede toochange. In questi casi è possibile escludere le cartelle e i file dall'archiviazione nei backup futuri. tooexclude file e cartelle dal backup, creare un `_backup.filter` file hello `D:\home\site\wwwroot` cartella dell'app. Specificare l'elenco di hello di file e cartelle che si desidera tooexclude in questo file. 

Un modo semplice tooaccess dei file è toouse Kudu. Fare clic su **strumenti avanzati -> Go** impostazione per il tooaccess app web Kudu.

![Uso del portale con Kudu][kudu-portal]

Identificare le cartelle di hello che si desidera tooexclude dal backup.  Ad esempio, si desidera toofilter hello evidenziato cartella out e file.

![Cartella delle immagini][ImagesFolder]

Creare un file denominato `_backup.filter` e inserire l'elenco di hello in precedenza nel file hello, ma rimuovere `D:\home`. Elencare una directory o un file per ogni riga. Pertanto, deve essere contenuto hello del file hello:
 ```bash
    \site\wwwroot\Images\brand.png
    \site\wwwroot\Images\2014
    \site\wwwroot\Images\2013
```

Caricare `_backup.filter` file toohello `D:\home\site\wwwroot\` directory del tuo sito con [ftp](web-sites-deploy.md#ftp) o qualsiasi altro metodo. Se si desidera, è possibile creare file hello direttamente utilizzando Kudu `DebugConsole` e inserire il contenuto di hello non esiste.

Eseguire i backup hello stesso come si farebbe normalmente, [manualmente](#create-a-manual-backup) o [automaticamente](#configure-automated-backups). Ora, eventuali file e cartelle che vengono specificate in `_backup.filter` viene esclusa dal backup futuri di hello pianificata o avviato manualmente. 

> [!NOTE]
> Ripristinare i backup parziali di hello del sito stesso modo di [ripristinare un backup regolare](web-sites-restore.md). il processo di ripristino Hello hello giusto.
> 
> Quando viene ripristinato un backup completo, tutto il contenuto nel sito hello viene sostituito con qualsiasi backup hello. Se un file nel sito di hello, ma non nel backup hello verrà eliminato. Tuttavia, quando viene ripristinato un backup parziale, qualsiasi contenuto che si trova in una delle directory hello disattivato o qualsiasi file disattivata, viene lasciato invariato.
> 


<a name="aboutbackups"></a>

## <a name="how-backups-are-stored"></a>Modalità di archiviazione dei backup
Dopo avere apportato uno o più backup per l'app, i backup hello sono visibili in hello **contenitori** blade di account di archiviazione e l'app. Nell'account di archiviazione hello, ogni backup include un`.zip` file che contiene i dati di backup hello e un `.xml` file che contiene un manifesto di hello `.zip` il contenuto del file. È possibile decomprimere e individuare questi file se si desidera tooaccess i backup senza eseguire effettivamente un ripristino dell'app.

backup del database per l'applicazione hello Hello viene archiviato nella directory radice del file the.zip hello. Per un database SQL può essere un file BACPAC (nessuna estensione di file) e può essere importato. toocreate un database SQL in base a hello esportazione BACPAC, vedere [importare tooCreate un File BACPAC un nuovo Database utente](http://technet.microsoft.com/library/hh710052.aspx).

> [!WARNING]
> Modifica di qualsiasi file hello nel **websitebackups** contenitore può causare hello toobecome backup non valido e pertanto non ripristinabile.
> 
> 

<a name="nextsteps"></a>

## <a name="next-steps"></a>Passaggi successivi
Per informazioni sul ripristino di un'app da un backup, vedere [Ripristinare un'app nel Servizio app di Azure](web-sites-restore.md). È possibile eseguire il backup e ripristinare le applicazioni di servizio App utilizzando API REST (vedere [usare REST toobackup e ripristino di App del servizio app](websites-csm-backup.md)).


<!-- IMAGES -->
[ChooseBackupsPage]: ./media/web-sites-backup/01ChooseBackupsPage1.png
[ChooseStorageAccount]: ./media/web-sites-backup/02ChooseStorageAccount-1.png
[IncludedDatabases]: ./media/web-sites-backup/03IncludedDatabases.png
[BackUpNow]: ./media/web-sites-backup/04BackUpNow1.png
[BackupProgress]: ./media/web-sites-backup/05BackupProgress.png
[SetAutomatedBackupOn]: ./media/web-sites-backup/06SetAutomatedBackupOn1.png
[Frequency]: ./media/web-sites-backup/07Frequency.png
[StartDate]: ./media/web-sites-backup/08StartDate.png
[StartTime]: ./media/web-sites-backup/09StartTime.png
[SaveIcon]: ./media/web-sites-backup/10SaveIcon.png
[ImagesFolder]: ./media/web-sites-backup/11Images.png
[LogsFolder]: ./media/web-sites-backup/12Logs.png
[GhostUpgradeWarning]: ./media/web-sites-backup/13GhostUpgradeWarning.png
[kudu-portal]:./media/web-sites-backup/kudu-portal.PNG

