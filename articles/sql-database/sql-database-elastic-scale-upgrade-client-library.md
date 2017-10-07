---
title: "libreria di client più recente del database elastico di aaaUpgrade toohello | Documenti Microsoft"
description: Eseguire l'aggiornamento alle applicazioni e librerie mediante Nuget
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 0a546510-76e7-465e-9271-f15ff0cfa959
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: ddove
ms.openlocfilehash: cc2c9179be4c53ca59cd24d832127cf277c6e695
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-an-app-toouse-hello-latest-elastic-database-client-library"></a>Aggiornare un'app toouse hello più recente database elastico libreria client
Le nuove versioni di hello [libreria client di Database elastico](sql-database-elastic-database-client-library.md) sono disponibili tramite l'interfaccia di gestione NuGetPackage NuGetand hello in Visual Studio. Gli aggiornamenti contengono correzioni di bug e supportano per le nuove funzionalità della libreria client hello.

**Per la versione più recente di hello:** andare troppo[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).

Ricompilare l'applicazione con una nuova libreria di hello, nonché modificare i metadati di gestore mappe partizioni esistenti archiviati in nuove funzionalità di toosupport il database SQL di Azure.

Eseguire questi passaggi nell'ordine assicura che le versioni precedenti della libreria client hello non sono più presenti nell'ambiente in uso quando vengono aggiornati gli oggetti di metadati, il che significa che gli oggetti di metadati della versione precedente non verrà creati dopo l'aggiornamento.   

## <a name="upgrade-steps"></a>Passaggi dell'aggiornamento
**1. Aggiornare le applicazioni.** In Visual Studio, download e riferimento hello più recente versione della libreria client in tutti i progetti di sviluppo che usano la libreria hello. quindi ricompilare e distribuire. 

* Nella soluzione Visual Studio in uso selezionare **Strumenti** --> **Gestione pacchetti NuGet** -->  **Gestisci pacchetti NuGet per la soluzione**. 
* (Visual Studio 2013) Nel riquadro sinistro hello selezionare **aggiornamenti**e quindi selezionare hello **aggiornamento** pulsante pacchetto hello **Azure SQL Database elastico scala libreria Client** che compare nella hello finestra.
* (Visual Studio 2015) Impostare la casella di filtro hello troppo**disponibile**. Selezionare tooupdate pacchetto hello e fare clic su hello **aggiornamento** pulsante.
* (2017 di visual Studio) Nella parte superiore di hello della finestra di dialogo hello, selezionare **aggiornamenti**. Selezionare tooupdate pacchetto hello e fare clic su hello **aggiornamento** pulsante.
* Compilare e distribuire. 

**2. Aggiornare gli script.** Se si utilizza **PowerShell** script toomanage partizioni, [scaricare una nuova versione della libreria hello](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/) e copiarlo nella directory hello da cui eseguire gli script. 

**3. Aggiornare il servizio di divisione e unione.** Se si utilizzano hello database elastico dello strumento di merge di divisione tooreorganize dati partizionati, [scaricare e distribuire hello la versione più recente dello strumento hello](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge/). Aggiornamento passaggi dettagliati per hello è possibile trovare servizio [qui](sql-database-elastic-scale-overview-split-and-merge.md). 

**4. Aggiornare i database di Gestore mappe partizioni**. Aggiornare i metadati di hello supporto mappe partizioni nel Database SQL di Azure.  Esistono due modi per eseguire questa operazione, tramite PowerShell o C#. Entrambe le opzioni sono mostrate di seguito.

***Opzione 1: aggiornare i metadati tramite PowerShell***

1. Scaricare l'utilità della riga di comando più recente di hello per NuGet da [qui](http://nuget.org/nuget.exe) e salvare la cartella tooa. 
2. Aprire un prompt dei comandi, passare toohello stessa cartella e del comando hello problema:`nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Client`
3. Passare toohello sottocartella contenente hello nuova DLL versione del client che è stato appena scaricato, ad esempio:`cd .\Microsoft.Azure.SqlDatabase.ElasticScale.Client.1.0.0\lib\net45`
4. Scaricare scriptlet aggiornamento client di database elastico hello da hello [Script Center](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-Elastic-6442e6a9), e salvarlo in hello stessa cartella contenente hello DLL.
5. In tale cartella eseguire "PowerShell.\upgrade.ps1" dal prompt dei comandi di hello e seguire le istruzioni di hello.

***Opzione 2: aggiornare i metadati tramite C#***

In alternativa, creare un'applicazione di Visual Studio che apre il ShardMapManager, scorre tutte le partizioni ed esegue l'aggiornamento dei metadati hello chiamando i metodi di hello [UpgradeLocalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradelocalstore.aspx) e [ UpgradeGlobalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradeglobalstore.aspx) come nel seguente esempio: 

    ShardMapManager smm =
       ShardMapManagerFactory.GetSqlShardMapManager
       (connStr, ShardMapManagerLoadPolicy.Lazy); 
    smm.UpgradeGlobalStore(); 

    foreach (ShardLocation loc in
     smm.GetDistinctShardLocations()) 
    {   
       smm.UpgradeLocalStore(loc); 
    } 

Tali tecniche di aggiornamento dei metadati possono essere applicate più volte senza creare problemi. Ad esempio, se una versione precedente del client crea inavvertitamente una partizione dopo aver già aggiornato, è possibile eseguire l'aggiornamento nuovamente tra tutte le partizioni tooensure tale hello versione più recente di metadati è presente nell'intera infrastruttura. 

**Nota:** nuove versioni della libreria client hello pubblicato a data continuare toowork con le versioni precedenti di hello gestore mappe partizioni metadati nel database SQL di Azure e viceversa.   Tuttavia è necessario toobe aggiornato tootake sfruttare alcune delle nuove funzionalità di hello client più recente di hello, i metadati.   Si noti che gli aggiornamenti dei metadati non influirà sulle eventuali dati utente o dati specifici dell'applicazione, solo gli oggetti creati e utilizzati da hello gestore mappe partizioni.  E le applicazioni continuano toooperate tramite una sequenza di aggiornamento hello descritto in precedenza. 

## <a name="elastic-database-client-version-history"></a>Cronologia delle versioni del client di database elastico
Per la cronologia delle versioni, andare troppo[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]:./media/sql-database-elastic-scale-upgrade-client-library/nuget-upgrade.png

