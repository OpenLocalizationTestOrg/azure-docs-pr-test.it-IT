---
title: aaaAdding una partizione utilizzando gli strumenti di database elastico | Documenti Microsoft
description: "Come imposta toouse API di scalabilità elastica tooadd nuova partizioni tooa partizione."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 62a349db-bebe-406f-a120-2f1986f2b286
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: f44b59578376d1238b3012a3cb52339978079f0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="adding-a-shard-using-elastic-database-tools"></a>Aggiunta di una partizione utilizzando gli strumenti di database elastici
## <a name="tooadd-a-shard-for-a-new-range-or-key"></a>tooadd una partizione per un nuovo intervallo o una chiave
Le applicazioni spesso necessario toosimply aggiungere nuovi dati toohandle partizioni che si prevedono di nuove chiavi o intervalli di chiavi per una mappa partizioni è già esistente. Ad esempio, un'applicazione partizionata in base l'ID Tenant potrebbe essere necessario tooprovision una nuova partizione per un nuovo tenant o mensile partizionati dati potrebbe essere una nuova partizione provisioning prima dell'inizio hello di ogni nuovo mese. 

Se il nuovo intervallo di valori di chiave di hello non fa già parte di un mapping esistente, è molto semplice tooadd hello nuova partizione e associare hello nuova chiave o un intervallo toothat partizione. 

### <a name="example--adding-a-shard-and-its-range-tooan-existing-shard-map"></a>Esempio: aggiunta di una partizione e la mappa di partizione esistente intervallo tooan
In questo esempio utilizza hello [TryGetShard](https://msdn.microsoft.com/library/azure/dn823929.aspx) hello [CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx), [CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn807221.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeShardMap`1.CreateRangeMapping\(Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeMappingCreationInfo{`0}\)) metodi e crea un'istanza di hello [ShardLocation](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardlocation.shardlocation.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardLocation.) classe. Esempio hello riportato di seguito, un database denominato **sample_shard_2** e tutti gli oggetti necessarie per lo schema in essa sono stati creati toohold intervallo [300, 400).  

    // sm is a RangeShardMap object.
    // Add a new shard toohold hello range being added. 
    Shard shard2 = null; 

    if (!sm.TryGetShard(new ShardLocation(shardServer, "sample_shard_2"),out shard2)) 
    { 
        shard2 = sm.CreateShard(new ShardLocation(shardServer, "sample_shard_2"));  
    } 

    // Create hello mapping and associate it with hello new shard 
    sm.CreateRangeMapping(new RangeMappingCreationInfo<long> 
                            (new Range<long>(300, 400), shard2, MappingStatus.Online)); 


In alternativa, è possibile utilizzare Powershell toocreate un nuovo gestore mappe partizioni. Un esempio è disponibile [qui](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).

## <a name="tooadd-a-shard-for-an-empty-part-of-an-existing-range"></a>tooadd una partizione per una parte vuota di un intervallo esistente
In alcuni casi, si possono avere già eseguito il mapping di una partizione tooa intervallo e parzialmente viene riempita con i dati, ma ora è diverse partizioni di dati futuri toobe tooa diretto. Ad esempio, si partizioni dal giorno intervallo e hanno già allocato partizione tooa 50 giorni, ma giorno 24, si desidera che i dati futuri tooland in una partizione diversa. database elastico Hello [strumento di merge di divisione](sql-database-elastic-scale-overview-split-and-merge.md) possono eseguire questa operazione, ma se lo spostamento dei dati non è necessario (ad esempio dati per intervallo hello di giorni [25, 50), ad esempio, giorno 25 inclusivo too50 esclusivo, non esiste ancora) è possibile eseguire Questo utilizzo completamente hello direttamente le API di gestione di partizioni della mappa.

### <a name="example-splitting-a-range-and-assigning-hello-empty-portion-tooa-newly-added-shard"></a>Esempio: suddivisione di un intervallo e l'assegnazione di hello vuote partizione appena aggiunti tooa di parte
È stato creato un database denominato "sample_shard_2" contenente tutti gli oggetti di schema necessari.  

    // sm is a RangeShardMap object.
    // Add a new shard toohold hello range we will move 
    Shard shard2 = null; 

    if (!sm.TryGetShard(new ShardLocation(shardServer, "sample_shard_2"),out shard2)) 
    { 

        shard2 = sm.CreateShard(new ShardLocation(shardServer, "sample_shard_2"));  
    } 

    // Split hello Range holding Key 25 

    sm.SplitMapping(sm.GetMappingForKey(25), 25); 

    // Map new range holding [25-50) toodifferent shard: 
    // first take existing mapping offline 
    sm.MarkMappingOffline(sm.GetMappingForKey(25)); 
    // now map while offline tooa different shard and take online 
    RangeMappingUpdate upd = new RangeMappingUpdate(); 
    upd.Shard = shard2; 
    sm.MarkMappingOnline(sm.UpdateMapping(sm.GetMappingForKey(25), upd)); 

**Importante**: utilizzare questa tecnica solo se si è certi che hello intervallo per il mapping di hello aggiornato è vuoto.  dati per intervallo hello spostato non controllati da metodi Hello precedenti, è preferibile tooinclude verifica nel codice.  Se sono presenti righe nell'intervallo di hello viene spostato, distribuzione di dati effettivi hello non corrisponderanno mappa partizioni aggiornato hello. Hello utilizzare [strumento di merge di divisione](sql-database-elastic-scale-overview-split-and-merge.md) tooperform hello invece l'operazione in questi casi.  

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

