---
title: credenziali aaaManaging nella libreria client di database elastico hello | Documenti Microsoft
description: Come tooset hello corretto livello di credenziali di amministratore tooread solo per le applicazioni di database elastico
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 72e0edaf-795e-4856-84a5-6594f735fb7e
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 218783ca2a07e3c0a4b089aa92634f32c41386e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="credentials-used-tooaccess-hello-elastic-database-client-library"></a>Libreria client di Database elastico hello tooaccess utilizzate le credenziali
Hello [libreria client di Database elastico](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/) utilizza tre tipi diversi di hello tooaccess credenziali [gestore mappe partizioni](sql-database-elastic-scale-shard-map-management.md). A seconda delle necessità di hello, utilizzare credenziali hello con livello più basso di hello di possibili di accesso.

* **Credenziali di gestione**: per la creazione o la modifica di un gestore di mappa di partizionamento. (Vedere hello [glossario](sql-database-elastic-scale-glossary.md).) 
* **Le credenziali di accesso**: tooaccess una partizione esistente, eseguire il mapping manager tooobtain informazioni sulle partizioni.
* **Le credenziali di connessione**: tooconnect tooshards. 

Vedere anche [Gestione di database e account di accesso in database SQL di Azure](sql-database-manage-logins.md). 

## <a name="about-management-credentials"></a>Informazioni sulle credenziali di gestione
Le credenziali di gestione vengono utilizzati toocreate un [ **ShardMapManager** ](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) oggetto per le applicazioni che consentono di modificare mappe partizioni. (Ad esempio, vedere [aggiunta di una partizione utilizzando gli strumenti di Database elastico](sql-database-elastic-scale-add-a-shard.md) e [routing dipendente dai dati](sql-database-elastic-scale-data-dependent-routing.md)) utente hello della libreria client di scalabilità elastica hello crea utenti SQL hello e account di accesso SQL e assicura ogni concesso le autorizzazioni di lettura/scrittura hello in partizioni globale hello eseguire il mapping del database e anche tutti i database di partizione. Queste credenziali sono mappa partizioni globale di hello toomaintain utilizzato e mappe di partizioni locale hello quando vengono eseguite mappa partizioni toohello di modifiche. Ad esempio, utilizzare hello Gestione credenziali toocreate hello partizioni manager oggetto map (utilizzando [ **GetSqlShardMapManager**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx): 

    // Obtain a shard map manager. 
    ShardMapManager shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager( 
            smmAdminConnectionString, 
            ShardMapManagerLoadPolicy.Lazy 
    ); 

variabile Hello **smmAdminConnectionString** è una stringa di connessione che contiene le credenziali di gestione di hello. ID utente Hello e una password fornisce database di lettura/scrittura access tooboth partizioni della mappa e singole partizioni. stringa di connessione gestione Hello inoltre include hello nome e il database nome tooidentify hello partizioni globale mappa database del server. La seguente è una stringa di connessione tipica usata a tale scopo:

     "Server=<yourserver>.database.windows.net;Database=<yourdatabase>;User ID=<yourmgmtusername>;Password=<yourmgmtpassword>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;” 

Non utilizzare valori sotto forma di hello di "username@server", usare semplicemente il valore di "username" hello.  Questo avviene perché le credenziali devono funzionare con database di gestione della mappa partizioni hello sia singole partizioni, che possono essere su server diversi.

## <a name="access-credentials"></a>Credenziali di accesso
Quando si crea una partizione gestore mappe in un'applicazione che non amministrare mappe partizioni, utilizzare le credenziali che dispongono delle autorizzazioni di sola lettura nella mappa partizioni globale hello. salve le informazioni recuperate da una mappa di partizioni globale hello in queste credenziali vengono utilizzati per [routing dipendente dai dati](sql-database-elastic-scale-data-dependent-routing.md) e partizioni hello toopopulate eseguire il mapping della cache sul client hello. salve le credenziali vengono specificate tramite hello troppo stesso call (modello)**GetSqlShardMapManager** come illustrato in precedenza: 

    // Obtain shard map manager. 
    ShardMapManager shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager( 
            smmReadOnlyConnectionString, 
            ShardMapManagerLoadPolicy.Lazy
    );  

Si noti utilizzo hello di hello **smmReadOnlyConnectionString** tooreflect hello ricorso credenziali diverse per l'accesso per conto di **senza privilegi di amministratore** gli utenti: queste credenziali non devono fornire scrittura autorizzazioni in una mappa di partizioni globale hello. 

## <a name="connection-credentials"></a>Credenziali di connessione
Sono necessarie credenziali aggiuntive quando si utilizza hello [ **OpenConnectionForKey** ](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx) tooaccess metodo una partizione associata a una chiave di partizionamento orizzontale. Le credenziali necessarie le autorizzazioni di tooprovide per tabelle di mapping delle partizioni locale di accesso in sola lettura toohello che risiedono in partizioni hello. Si tratta di convalida della connessione tooperform necessari per il routing dipendente dai dati nella partizione hello. Questo frammento di codice consente l'accesso ai dati nel contesto di hello del routing dipendente dai dati: 

    using (SqlConnection conn = rangeMap.OpenConnectionForKey<int>( 
    targetWarehouse, smmUserConnectionString, ConnectionOptions.Validate)) 

In questo esempio, **smmUserConnectionString** contiene la stringa di connessione hello per hello le credenziali dell'utente. Questa è invece una stringa di connessione tipica per le credenziali utente per il database SQL di Azure: 

    "User ID=<yourusername>; Password=<youruserpassword>; Trusted_Connection=False; Encrypt=True; Connection Timeout=30;”  

Come con le credenziali di amministratore hello non valori sotto forma di hello di "username@server". Usare invece solo "username".  Si noti inoltre che la stringa di connessione hello non contenga un nome del server e il nome del database. Ciò accade perché hello **OpenConnectionForKey** chiamata indirizzerà automaticamente hello connessione toohello corretto di partizioni in base a hello chiave. Di conseguenza, il nome di database hello e server non disponibili. 

## <a name="see-also"></a>Vedere anche
[Gestione di database e account di accesso in database SQL di Azure](sql-database-manage-logins.md)

[Protezione del Database SQL](sql-database-security-overview.md)

[Introduzione ai processi di Database Elastici](sql-database-elastic-jobs-getting-started.md)

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

