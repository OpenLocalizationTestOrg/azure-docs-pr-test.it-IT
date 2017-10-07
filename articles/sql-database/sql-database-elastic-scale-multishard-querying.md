---
title: database SQL di Azure partizionati aaaQuery | Documenti Microsoft
description: Eseguire query tra partizioni utilizzando hello libreria client di database elastico.
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
editor: 
ms.assetid: a4379c15-f213-4026-ab6f-a450ee9d5758
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2016
ms.author: torsteng
ms.openlocfilehash: a1f0763935a6807b74aa9dec477714e8d117417d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="multi-shard-querying"></a>Esecuzione di query su più partizioni
## <a name="overview"></a>Panoramica
Con hello [strumenti di Database elastico](sql-database-elastic-scale-introduction.md), è possibile creare soluzioni di database partizionato. La funzionalità di **query su più partizioni** viene usata per attività che richiedono l'esecuzione di una query su più partizioni, ad esempio la raccolta o la creazione di report sui dati, (Per ovviare a questo troppo[routing dipendente dai dati](sql-database-elastic-scale-data-dependent-routing.md), che esegue tutte le operazioni in una singola partizione.) 

1. Ottenere un [ **RangeShardMap** ](https://msdn.microsoft.com/library/azure/dn807318.aspx) o [ **ListShardMap** ](https://msdn.microsoft.com/library/azure/dn807370.aspx) utilizzando hello [ **TryGetRangeShardMap** ](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), hello [ **TryGetListShardMap**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx), o hello [ **GetShardMap** ](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) metodo. Vedere [**Creazione di un oggetto ShardMapManager**](sql-database-elastic-scale-shard-map-management.md#constructing-a-shardmapmanager) e [**Ottenere una mappa RangeShardMap o ListShardMap**](sql-database-elastic-scale-shard-map-management.md#get-a-rangeshardmap-or-listshardmap).
2. Creare un oggetto **[MultiShardConnection](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardconnection.aspx)**.
3. Creare un **[MultiShardCommand](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.aspx)**. 
4. Set hello  **[proprietà CommandText](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.commandtext.aspx#P:Microsoft.Azure.SqlDatabase.ElasticScale.Query.MultiShardCommand.CommandText)**  tooa comando T-SQL.
5. Eseguire il comando hello dal chiamante hello  **[metodo ExecuteReader](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.executereader.aspx)**.
6. Visualizzare i risultati di hello utilizzando hello  **[MultiShardDataReader classe](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multisharddatareader.aspx)**. 

## <a name="example"></a>Esempio
Hello codice riportato di seguito viene illustrato hello utilizzo di più partizioni, esecuzione di query utilizzando un determinato **ShardMap** denominato *myShardMap*. 

    using (MultiShardConnection conn = new MultiShardConnection( 
                                        myShardMap.GetShards(), 
                                        myShardConnectionString) 
          ) 
    { 
    using (MultiShardCommand cmd = conn.CreateCommand())
           { 
            cmd.CommandText = "SELECT c1, c2, c3 FROM ShardedTable"; 
            cmd.CommandType = CommandType.Text; 
            cmd.ExecutionOptions = MultiShardExecutionOptions.IncludeShardNameColumn; 
            cmd.ExecutionPolicy = MultiShardExecutionPolicy.PartialResults; 

            using (MultiShardDataReader sdr = cmd.ExecuteReader()) 
                { 
                    while (sdr.Read())
                        { 
                            var c1Field = sdr.GetString(0); 
                            var c2Field = sdr.GetFieldValue<int>(1); 
                            var c3Field = sdr.GetFieldValue<Int64>(2);
                        } 
                 } 
           } 
    } 


Una differenza principale è la costruzione di hello di connessioni a più partizioni. Dove **SqlConnection** opera su un singolo database, hello **MultiShardConnection** accetta un ***raccolta di partizioni*** come input. Popolare la raccolta di hello di partizioni da una mappa partizioni. query Hello viene quindi eseguita sull'insieme di hello di partizioni utilizzando **UNION ALL** semantica tooassemble un singolo risultato complessivo. Facoltativamente, nome hello della partizione hello in riga hello ha avuto origine è possibile aggiungere l'output utilizzando hello toohello **ExecutionOptions** proprietà nel comando. 

Si noti la chiamata hello troppo**myShardMap.GetShards()**. Questo metodo recupera tutte le partizioni dalla mappa partizioni hello e fornisce un modo semplice di toorun una query in tutti i database rilevanti. Hello raccolta di partizioni per una query su più partizioni può essere suddivise ulteriormente eseguendo un LINQ query su hello raccolta restituita dalla chiamata di hello troppo**myShardMap.GetShards()**. In combinazione con criteri di risultati parziali hello, funzionalità di hello corrente di query su più partizioni è stato progettato toowork per decine di toohundreds di partizioni.

Una limitazione con più partizioni di una query è attualmente la mancanza di hello di convalida per le partizioni e shardlet che viene eseguita una query. Mentre il routing dipendente dai dati verifica che una determinata partizione fa parte di mappa partizioni hello in fase di esecuzione di query di hello, le query più partizioni non eseguono questo controllo. Questo può causare query toomulti partizioni in esecuzione nel database che sono state rimosse dalla mappa partizioni hello.

## <a name="multi-shard-queries-and-split-merge-operations"></a>Query su più partizioni e operazioni di suddivisione e unione
Le query più partizioni non verificano se gli shardlet nel database sottoposto a query hello partecipano in corso operazioni di unione di menu combinato. (Vedere [scala utilizzando lo strumento di unione di Database elastico split hello](sql-database-elastic-scale-overview-split-and-merge.md).) Questo può causare in cui le righe da hello stessa presentazione di shardlet per più database in hello tooinconsistencies stessa query su più partizioni. Tenere presenti queste limitazioni e considerare svuotamento in corso suddivisione unione operazioni e le modifiche toohello mappa partizioni durante l'esecuzione di query su più partizioni.

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

## <a name="see-also"></a>Vedere anche
Classi e metodi **[System.Data.SqlClient](http://msdn.microsoft.com/library/System.Data.SqlClient.aspx)**.

Gestire le partizioni utilizzando hello [libreria client di Database elastico](sql-database-elastic-database-client-library.md). Include uno spazio dei nomi denominato [Microsoft.Azure.SqlDatabase.ElasticScale.Query](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.aspx) tooquery possibilità hello che fornisce più partizioni, utilizzando una singola query e risultati. Fornisce l'astrazione delle query su una raccolta di partizioni, Fornisce inoltre criteri di esecuzione alternativo, risultati parziali in particolare, toodeal con errori quando si eseguono query su molte partizioni.  

