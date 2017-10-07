---
title: gruppi aaaManage di database SQL di Azure | Documenti Microsoft
description: Informazioni sulla creazione e la gestione di un processo elastico.
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: f858344d-085b-4022-935e-1b5fa20adbac
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: a73c4fb24c332fae0e917c18272724cccd56f29a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-scaled-out-azure-sql-databases-using-elastic-jobs-preview"></a>Creare e gestire database SQL di Azure con scalabilità orizzontale tramite processi elastici (anteprima)


**processi di database elastico** semplificano la gestione dei gruppi di database con l'esecuzione di operazioni amministrative, come le modifiche dello schema, la gestione delle credenziali, gli aggiornamenti dei dati di riferimento, la raccolta dei dati sulle prestazioni o la raccolta dei dati di telemetria dei tenant (clienti). I processi di Database elastici è attualmente disponibile tramite hello portale di Azure e i cmdlet di PowerShell. Tuttavia, hello aree del portale di Azure con funzionalità ridotte limitate tooexecution in tutti i database in un [pool elastico (anteprima)](sql-database-elastic-pool.md). set di funzionalità aggiuntive di tooaccess e l'esecuzione di script in un gruppo di database tra un insieme personalizzato o una partizione (creato utilizzando [libreria client di Database elastico](sql-database-elastic-scale-introduction.md)), vedere [creazione e gestione i processi tramite PowerShell](sql-database-elastic-jobs-powershell.md). Per ulteriori informazioni sui processi, vedere [Panoramica dei processi di database elastici](sql-database-elastic-jobs-overview.md). 

## <a name="prerequisites"></a>Prerequisiti
* Una sottoscrizione di Azure. Per una versione di valutazione gratuita, vedere [Versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Un pool elastico. Vedere l'articolo sui [pool elastici](sql-database-elastic-pool.md).
* Installazione dei componenti del servizio relativo ai processi elastici di database. Vedere [installazione del servizio processo di database elastico hello](sql-database-elastic-jobs-service-installation.md).

## <a name="creating-jobs"></a>Creazione di processi
1. Utilizzo di hello [portale di Azure](https://portal.azure.com), da un pool di processi di database elastici esistente, fare clic su **processo di creazione**.
2. Digitare nome utente hello e la password dell'amministratore del database hello (creato al momento dell'installazione dei processi) per il database di controllo processi hello (archiviazione di metadati per i processi).
   
    ![Nome del processo hello, digitare o incollare nel codice e fare clic su Esegui][1]
3. In hello **Crea processo** pannello, digitare un nome per il processo di hello.
4. Digitare hello nome e la password tooconnect toohello destinazione database utente con autorizzazioni sufficienti per toosucceed di esecuzione di script.
5. Incollare o digitare nello script T-SQL hello.
6. Fare clic su **Salva** e quindi su **Esegui**.
   
    ![Creare processi ed eseguirli][5]

## <a name="run-idempotent-jobs"></a>Eseguire processi idempotenti
Quando si esegue uno script con un set di database, è necessario assicurarsi che script hello è idempotente. Vale a dire hello script deve essere in grado di toorun più volte, anche se non è riuscito prima in uno stato incompleto. Ad esempio, quando uno script non riesce, il processo di hello verrà automaticamente ritentato fino al completamento (entro i limiti, come ripetere hello logica infine smetteranno hello ritentare). Hello modo toodo questo è hello toouse una clausola "IF EXISTS" e l'eliminazione di qualsiasi istanza presente prima di creare un nuovo oggetto. Di seguito è riportato un esempio:

    IF EXISTS (SELECT name FROM sys.indexes
            WHERE name = N'IX_ProductVendor_VendorID')
    DROP INDEX IX_ProductVendor_VendorID ON Purchasing.ProductVendor;
    GO
    CREATE INDEX IX_ProductVendor_VendorID
    ON Purchasing.ProductVendor (VendorID);

In alternativa, usare una clausola "IF NOT EXISTS" prima di creare una nuova istanza:

    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
     CREATE TABLE TestTable(
      TestTableId INT PRIMARY KEY IDENTITY,
      InsertionTime DATETIME2
     );
    END
    GO

    INSERT INTO TestTable(InsertionTime) VALUES (sysutcdatetime());
    GO

Questo script Aggiorna tabella hello creata in precedenza.

    IF NOT EXISTS (SELECT columns.name FROM sys.columns INNER JOIN sys.tables on columns.object_id = tables.object_id WHERE tables.name = 'TestTable' AND columns.name = 'AdditionalInformation')
    BEGIN

    ALTER TABLE TestTable

    ADD AdditionalInformation NVARCHAR(400);
    END
    GO

    INSERT INTO TestTable(InsertionTime, AdditionalInformation) VALUES (sysutcdatetime(), 'test');
    GO


## <a name="checking-job-status"></a>Verifica dello stato del processo
Dopo aver iniziato un processo, è possibile controllarne lo stato di avanzamento.

1. Dalla pagina di pool elastico hello, fare clic su **gestire processi**.
   
    ![Fare clic su "Gestione processi"][2]
2. Fare clic su hello Nome (a) di un processo. Hello **stato** può essere "Completed" o "Failed". dettagli del processo di Hello vengono visualizzate (b) con data e ora di creazione e l'esecuzione. elenco di Hello (c) seguito hello che mostra lo stato di avanzamento hello dello script hello in tutti i database nel pool di hello, fornendo i dettagli di data e ora.
   
    ![Controllo di un processo completato][3]

## <a name="checking-failed-jobs"></a>Controllo dei processi non riusciti
Se un processo ha esito negativo, è disponibile un log dell'esecuzione. Fare clic su nome hello di hello non è stato possibile processo toosee i dettagli.

![Controllo di un processo non riuscito][4]

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-create-and-manage/screen-1.png
[2]: ./media/sql-database-elastic-jobs-create-and-manage/click-manage-jobs.png
[3]: ./media/sql-database-elastic-jobs-create-and-manage/running-jobs.png
[4]: ./media/sql-database-elastic-jobs-create-and-manage/failed.png
[5]: ./media/sql-database-elastic-jobs-create-and-manage/screen-2.png


