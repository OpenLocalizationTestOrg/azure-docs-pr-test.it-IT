---
title: dati aaaCopy tooSQL Database - archiviazione Blob Azure | Documenti Microsoft
description: "Questa esercitazione viene illustrato come attività di copia in una Data Factory di Azure toouse pipeline toocopy dati dal database tooSQL di archiviazione Blob."
keywords: blob sql, archivio blob, copia di dati
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: e4035060-93bf-4e8d-bf35-35e2d15c51e0
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: a2c3fb8a4ddd63b0b6b3e75903b7a7eaf188fda4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-copy-data-from-blob-storage-toosql-database-using-data-factory"></a>Esercitazione: Copiare i dati da archiviazione Blob tooSQL Database tramite Data Factory
> [!div class="op_single_selector"]
> * [Panoramica e prerequisiti](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Copia guidata](data-factory-copy-data-wizard-tutorial.md)
> * [Portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Modello di Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [API REST](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [API .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md)

In questa esercitazione, si crea una data factory con una pipeline toocopy dati dal database tooSQL di archiviazione Blob.

Attività di copia Hello esegue lo spostamento dei dati di hello in Azure Data Factory. e si basa su un servizio disponibile a livello globale che può copiare dati tra diversi archivi dati in modo sicuro, affidabile e scalabile. Vedere [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo per informazioni dettagliate sulle attività di copia hello.  

> [!NOTE]
> Per una panoramica dettagliata di hello servizio Data Factory, vedere hello [tooAzure introduzione Data Factory](data-factory-introduction.md) articolo.
>
>

## <a name="prerequisites-for-hello-tutorial"></a>Prerequisiti per l'esercitazione hello
Prima di iniziare questa esercitazione, è necessario disporre di hello seguenti prerequisiti:

* **Sottoscrizione di Azure**.  Se non è disponibile una sottoscrizione, è possibile creare un account di valutazione gratuita in pochi minuti. Vedere hello [versione di valutazione gratuita](http://azure.microsoft.com/pricing/free-trial/) articolo per informazioni dettagliate.
* **Account di archiviazione di Azure**. Usare l'archiviazione di blob hello come un **origine** archivio dati in questa esercitazione. Se non si dispone di un account di archiviazione di Azure, vedere hello [creare un account di archiviazione](../storage/common/storage-create-storage-account.md#create-a-storage-account) articolo per passaggi toocreate uno.
* **Database SQL di Azure**. In questa esercitazione viene usato un database SQL di Azure come archivio dati di **destinazione** . Se non si dispone di un database SQL di Azure che è possibile utilizzare nell'esercitazione di hello, vedere [come toocreate e configurare un Database di SQL Azure](../sql-database/sql-database-get-started.md) toocreate uno.
* **SQL Server 2012/2014 o Visual Studio 2013**. Si utilizza SQL Server Management Studio o Visual Studio toocreate un database di esempio e dati del risultato hello tooview nel database di hello.  

## <a name="collect-blob-storage-account-name-and-key"></a>Raccogliere il nome dell'account e la chiave dell'archivio BLOB
È necessario hello account chiave nome e un account di archiviazione Azure toodo questa esercitazione. Prendere nota del **nome** e della **chiave** per l'account di archiviazione di Azure.

1. Accedi toohello [portale di Azure](https://portal.azure.com/).
2. Fare clic su **più servizi** su hello dal menu a sinistra **gli account di archiviazione**.

    ![Sfoglia - Account di archiviazione](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/browse-storage-accounts.png)
3. In hello **gli account di archiviazione** blade, seleziona hello **account di archiviazione Azure** che si desidera toouse in questa esercitazione.
4. Selezionare **Chiavi di accesso** in **IMPOSTAZIONI**.
5. Fare clic su **copia** (immagine) accanto troppo**nome account di archiviazione** testo casella e Salva e incollarlo in un punto (ad esempio: in un file di testo).
6. Ripetere toocopy passaggio precedente hello o annotare hello **key1**.

    ![Chiave di accesso alle risorse di archiviazione](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/storage-access-key.png)
7. Chiudere tutti i pannelli hello facendo **X**.

## <a name="collect-sql-server-database-user-names"></a>Raccogliere i nomi del server, del database e dell'utente per il database SQL
È necessario nomi hello del server SQL Azure, database e toodo utente in questa esercitazione. Annotare i nomi di **server**, **database** e **utente** per il database SQL di Azure.

1. In hello **portale di Azure**, fare clic su **più servizi** su hello a sinistra e seleziona **database SQL**.
2. In hello **pannello database SQL**selezionare hello **database** che si desidera toouse in questa esercitazione. Annotare hello **nome del database**.  
3. In hello **database SQL** pannello, fare clic su **proprietà** in **impostazioni**.
4. Annotare i valori hello per **nome SERVER** e **account di accesso amministratore SERVER**.
5. Chiudere tutti i pannelli hello facendo **X**.

## <a name="allow-azure-services-tooaccess-sql-server"></a>Consentire a servizi di Azure tooaccess SQL server
Verificare che **Consenti l'accesso ai servizi tooAzure** impostazione disattivata **ON** per il server SQL Azure in modo che il servizio Data Factory di hello può accedere al server di SQL Azure. tooverify e attivare questa impostazione, hello i passaggi seguenti:

1. Fare clic su **più servizi** hub hello sinistra e fare clic su **istanze di SQL Server**.
2. Selezionare il server e fare clic su **Firewall** in **IMPOSTAZIONI**.
3. In hello **le impostazioni del Firewall** pannello, fare clic su **ON** per **Consenti l'accesso ai servizi tooAzure**.
4. Chiudere tutti i pannelli hello facendo **X**.

## <a name="prepare-blob-storage-and-sql-database"></a>Preparare l'archivio BLOB e il database SQL
A questo punto, preparare l'archiviazione blob di Azure e il database SQL di Azure per l'esercitazione hello eseguendo hello alla procedura seguente:  

1. Avviare il Blocco note. Copiare hello segue testo e salvarlo come **emp.txt** troppo**C:\ADFGetStarted** cartella sul disco rigido.

    ```
    John, Doe
    Jane, Doe
    ```
2. Utilizzare strumenti come [Azure Storage Explorer](http://storageexplorer.com/) toocreate hello **adftutorial** hello contenitore e tooupload **emp.txt** contenitore toohello file.

    ![Azure Storage Explorer Copiare i dati da database tooSQL di archiviazione Blob](./media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/getstarted-storage-explorer.png)
3. Hello utilizzare hello toocreate di script SQL seguente **emp** tabella nel Database SQL di Azure.  

    ```SQL
    CREATE TABLE dbo.emp
    (
        ID int IDENTITY(1,1) NOT NULL,
        FirstName varchar(50),
        LastName varchar(50),
    )
    GO

    CREATE CLUSTERED INDEX IX_emp_ID ON dbo.emp (ID);
    ```

    **Se è installato nel computer SQL Server 2012/2014:** seguire le istruzioni da [la gestione di Database SQL Azure utilizzando SQL Server Management Studio](../sql-database/sql-database-manage-azure-ssms.md) tooconnect tooyour Azure SQL server ed eseguire hello script SQL. Questo articolo Usa hello [portale di Azure classico](http://manage.windowsazure.com), non hello [nuovo portale di Azure](https://portal.azure.com), tooconfigure firewall per un server SQL Azure.

    Se il client non è consentito server SQL di Azure di hello tooaccess, è necessario tooconfigure firewall per l'accesso di SQL Azure server tooallow dal computer (indirizzo IP). Vedere [questo articolo](../sql-database/sql-database-configure-firewall-settings.md) per firewall hello tooconfigure di passaggi per il server SQL Azure.

## <a name="create-a-data-factory"></a>Creare un'istanza di Data factory
Siano stati soddisfatti i prerequisiti di hello. È possibile creare una data factory utilizzando uno dei seguenti modi hello. Fare clic su una delle opzioni di hello nell'elenco a discesa hello nella parte superiore di hello o hello segue collegamenti tooperform hello esercitazione.     

* [Copia guidata](data-factory-copy-data-wizard-tutorial.md)
* [Portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md)
* [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
* [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
* [Modello di Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [API REST](data-factory-copy-activity-tutorial-using-rest-api.md)
* [API .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md)

> [!NOTE]
> pipeline di dati Hello in questa esercitazione consente di copiare dati da un archivio dati di origine dati archivio tooa destinazione. Non Trasforma dati di output tooproduce dati di input. Per un'esercitazione su come dati di tootransform tramite Data Factory di Azure, vedere [esercitazione: creare i primi dati tootransform pipeline utilizzando cluster Hadoop](data-factory-build-your-first-pipeline.md).
> 
> È possibile concatenare le due attività (eseguire un'attività dopo l'altro) mediante l'impostazione di set di dati di hello output di un'attività come hello input set di dati di hello altre attività. Per informazioni dettagliate, vedere [Pianificazione ed esecuzione con Data Factory](data-factory-scheduling-and-execution.md). 
