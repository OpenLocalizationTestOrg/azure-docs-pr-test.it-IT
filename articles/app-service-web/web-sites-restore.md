---
title: aaaRestore un'app in Azure
description: Informazioni su come toorestore l'app da un backup.
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: 4444dbf7-363c-47e2-b24a-dbd45cb08491
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2016
ms.author: cephalin
ms.openlocfilehash: 4b54029a9197064f990f29a3c4558c8322668714
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="restore-an-app-in-azure"></a>Ripristinare un'app in Azure
In questo articolo illustra come toorestore un'app in [Azure App Service](../app-service/app-service-value-prop-what-is.md) che in precedenza è stato eseguito il (vedere [eseguire il backup dell'app in Azure](web-sites-backup.md)). È possibile ripristinare l'app con lo stato precedente su richiesta tooa database collegati o creare una nuova app basata su uno dei backup dell'applicazione originale. Servizio App di Azure supporta hello seguendo i database per il backup e ripristino:
- [Database SQL](https://azure.microsoft.com/en-us/services/sql-database/)
- [Database di Azure per MySQL (anteprima)](https://azure.microsoft.com/en-us/services/mysql)
- [Database di Azure per PostgreSQL (anteprima)](https://azure.microsoft.com/en-us/services/postgres)
- [ClearDB MySQL](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)
- [MySQL in-app](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)

Ripristino da backup è disponibile tooapps in esecuzione in **Standard** e **Premium** livello. Per informazioni sul passaggio dell'app a un piano superiore, vedere [Scalare un'app Web in Servizio app di Azure](web-sites-scale.md). **Premium** livello consente un numero maggiore di toobe di backup giornaliera eseguita rispetto a **Standard** livello.

<a name="PreviousBackup"></a>

## <a name="restore-an-app-from-an-existing-backup"></a>Ripristinare un'app da un backup esistente
1. In hello **impostazioni** fare clic su pannello dell'app nel portale di Azure, hello **backup** toodisplay hello **backup** blade. Fare quindi clic su **Ripristina**.
   
    ![Scegliere Ripristina][ChooseRestoreNow]
2. In hello **ripristinare** blade, prima origine di backup selezionare hello.
   
    ![](./media/web-sites-restore/021ChooseSource1.png)
   
    Hello **backup App** opzione Mostra tutti i backup esistenti dell'applicazione corrente hello di hello ed è possibile selezionare uno.
    Hello **archiviazione** opzione consente di selezionare qualsiasi file ZIP di backup da qualsiasi account di archiviazione di Azure e un contenitore nella sottoscrizione esistente.
    Se si sta tentando di toorestore un backup di un'altra app, utilizzare hello **archiviazione** opzione.
3. Quindi, specificare la destinazione hello per il ripristino dell'app hello in **destinazione di ripristino**.
   
    ![](./media/web-sites-restore/022ChooseDestination1.png)
   
   > [!WARNING]
   > Se si sceglie **Sovrascrivi**, tutti i dati esistenti nell'app corrente verranno cancellati e sovrascritti. Prima di scegliere **OK**, verificare che sia esattamente ciò che si desidera toodo.
   > 
   > 
   
    È possibile selezionare **App esistente** toorestore hello app tooanother backup in app hello nello stesso gruppo di risorsa. Prima di utilizzare questa opzione, è necessario avere già creato un'altra applicazione nel gruppo di risorse con il mirroring del database configurazione toohello quella definita nel backup app hello. È inoltre possibile creare un **New** app toorestore il contenuto.

4. Fare clic su **OK**.

<a name="StorageAccount"></a>

## <a name="download-or-delete-a-backup-from-a-storage-account"></a>Scaricare o eliminare un backup da un account di archiviazione
1. Da hello principale **Sfoglia** pannello del portale di Azure selezionare hello **gli account di archiviazione**. Verrà visualizzato un elenco degli account di archiviazione esistenti.
2. Selezionare l'account di archiviazione di hello contenente backup hello desiderato viene visualizzato un pannello toodownload o delete.hello hello account di archiviazione.
3. Nel Pannello di account di archiviazione hello, selezionare il contenitore di hello desiderato
   
    ![Contenitori di visualizzazione][ViewContainers]
4. Selezionare i file di backup si desidera toodownload o eliminare.
   
    ![ViewContainers](./media/web-sites-restore/03ViewFiles.png)
5. Fare clic su **scaricare** o **eliminare** a seconda di ciò che si desidera toodo.  

<a name="OperationLogs"></a>

## <a name="monitor-a-restore-operation"></a>Monitorare un'operazione di ripristino
Dettagli toosee hello riuscita o meno dell'operazione di ripristino di app hello, passare toohello **Log attività** pannello in hello portale di Azure.  
 

Scorrere verso il basso toofind hello desiderato ripristino operazione e fare clic su tooselect.

Hello pannello Visualizza hello disponibili informazioni correlate toohello l'operazione di ripristino.

## <a name="next-steps"></a>Passaggi successivi
È possibile eseguire il backup e ripristinare le applicazioni di servizio App utilizzando API REST (vedere [tooback REST di utilizzo di backup e ripristino di applicazioni di servizio App](websites-csm-backup.md)).


<!-- IMAGES -->
[ChooseRestoreNow]: ./media/web-sites-restore/02ChooseRestoreNow1.png
[ViewContainers]: ./media/web-sites-restore/03ViewContainers.png
[StorageAccountFile]: ./media/web-sites-restore/02StorageAccountFile.png
[BrowseCloudStorage]: ./media/web-sites-restore/03BrowseCloudStorage.png
[StorageAccountFileSelected]: ./media/web-sites-restore/04StorageAccountFileSelected.png
[ChooseRestoreSettings]: ./media/web-sites-restore/05ChooseRestoreSettings.png
[ChooseDBServer]: ./media/web-sites-restore/06ChooseDBServer.png
[RestoreToNewSQLDB]: ./media/web-sites-restore/07RestoreToNewSQLDB.png
[NewSQLDBConfig]: ./media/web-sites-restore/08NewSQLDBConfig.png
[RestoredContosoWebSite]: ./media/web-sites-restore/09RestoredContosoWebSite.png
[DashboardOperationLogsLink]: ./media/web-sites-restore/10DashboardOperationLogsLink.png
[ManagementServicesOperationLogsList]: ./media/web-sites-restore/11ManagementServicesOperationLogsList.png
[DetailsButton]: ./media/web-sites-restore/12DetailsButton.png
[OperationDetails]: ./media/web-sites-restore/13OperationDetails.png
