---
title: domande frequenti su scala elastica SQL aaaAzure | Documenti Microsoft
description: "Domande frequenti sulla scalabilità elastica del database SQL di Azure."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: e60dde9c-bb7b-4f2f-b52c-bdb506d49fcb
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 8c77902e8ce9cbbc5e081cd9d2c911d4c8dc9e5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="elastic-database-tools-faq"></a>Domande frequenti sugli strumenti di database elastici
#### <a name="if-i-have-a-single-tenant-per-shard-and-no-sharding-key-how-do-i-populate-hello-sharding-key-for-hello-schema-info"></a>Se dispone di un singolo tenant per partizione e nessuna chiave di partizionamento orizzontale, la modalità popola la chiave di partizionamento orizzontale hello per informazioni sullo schema hello?
oggetto di informazioni dello schema di Hello è solo toosplit utilizzati gli scenari di unione. Se un'applicazione è intrinsecamente single-tenant, non richiede lo strumento di Merge Split hello e pertanto è presente alcun oggetto di informazioni dello schema di necessario toopopulate hello.

#### <a name="ive-provisioned-a-database-and-i-already-have-a-shard-map-manager-how-do-i-register-this-new-database-as-a-shard"></a>Quando è stato eseguito il provisioning di un database e si dispone già di un Gestore mappe partizioni, come è possibile registrare il nuovo database come partizione?
Vedere  **[aggiunta di un'applicazione tooan partizioni utilizzando libreria client di database elastico hello](sql-database-elastic-scale-add-a-shard.md)**. 

#### <a name="how-much-do-elastic-database-tools-cost"></a>Quanto costano gli strumenti di database elastici?
Utilizzando libreria client di database elastico hello non comporta alcun costo. Solo per i database di SQL Azure hello che utilizzano per partizioni e gestore mappe partizioni hello, nonché i ruoli web/di lavoro hello che viene effettuato il provisioning per lo strumento di Merge Split hello accumuleranno i costi.

#### <a name="why-are-my-credentials-not-working-when-i-add-a-shard-from-a-different-server"></a>Perché le credenziali personali non funzionano quando si aggiunge una partizione da un server diverso?
Non utilizzare le credenziali in formato hello "ID utente =username@servername", utilizzare semplicemente "ID utente = username".  Assicurarsi, inoltre, che tale account di accesso "username" hello dispone delle autorizzazioni per la partizione hello.

#### <a name="do-i-need-toocreate-a-shard-map-manager-and-populate-shards-every-time-i-start-my-applications"></a>È necessario un gestore mappe partizioni toocreate e popolare le partizioni a ogni avvio di applicazioni?
Non-hello creazione di hello gestore mappe partizioni (ad esempio,  **[ShardMapManagerFactory.CreateSqlShardMapManager](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx)**) è un'operazione occasionale.  L'applicazione deve utilizzare chiamata hello  **[ShardMapManagerFactory.TryGetSqlShardMapManager()](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx)**  in fase di avvio dell'applicazione.  È supportata una sola chiamata di questo tipo per dominio di applicazione.

#### <a name="i-have-questions-about-using-elastic-database-tools-how-do-i-get-them-answered"></a>In che modo è possibile ottenere risposte alle domande sugli strumenti di database elastici?
Per raggiungere toous su hello [forum di Database SQL di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted).

#### <a name="when-i-get-a-database-connection-using-a-sharding-key-i-can-still-query-data-for-other-sharding-keys-on-hello-same-shard--is-this-by-design"></a>Quando Ottiene una connessione al database utilizzando una chiave di partizionamento orizzontale, comunque possibile eseguire query sui dati per altri partizionamento orizzontale chiavi su hello stesso partizioni.  Si tratta di un comportamento previsto da progettazione?
Hello API di scalabilità elastica offrono un database di connessione toohello corretto per la chiave di partizionamento orizzontale, ma non forniscono il filtro chiave di partizionamento orizzontale.  Aggiungere **dove** clausole tooyour query toorestrict hello ambito toohello fornita la chiave di partizionamento orizzontale, se necessario.

#### <a name="can-i-use-a-different-azure-database-edition-for-each-shard-in-my-shard-set"></a>È possibile usare un'edizione del database di Azure diversa per ogni partizione nel set di partizioni?
Sì, una partizione è un database a sé, per cui è possibile che una partizione sia un'edizione Premium mentre un'altra è un'edizione Standard. Inoltre, edizione hello di una partizione può aumentare o diminuire più volte durante la durata hello di partizioni hello.

#### <a name="does-hello-split-merge-tool-provision-or-delete-a-database-during-a-split-or-merge-operation"></a>Effettuare il provisioning dello strumento di unione di menu combinato hello (o eliminare) un database durante un'operazione di divisione o di unione?
No. Per **dividere** operazioni, il database di destinazione hello deve esistere con schema appropriato hello ed essere registrato con hello gestore mappe partizioni.  Per **unione** operazioni, è necessario eliminare partizioni hello dal gestore mappe partizioni di hello e quindi eliminare il database di hello.

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

