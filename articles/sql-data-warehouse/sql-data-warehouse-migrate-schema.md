---
title: aaaMigrate il tooSQL dello schema del Data Warehouse | Documenti Microsoft
description: Suggerimenti per la migrazione del tooAzure schema SQL Data Warehouse per lo sviluppo di soluzioni.
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 538b60c9-a07f-49bf-9ea3-1082ed6699fb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 10/31/2016
ms.author: joeyong;barbkess
ms.openlocfilehash: 1309b743b78564575695038a4856d9d25a2b18d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-schemas-toosql-data-warehouse"></a>Eseguire la migrazione del Data Warehouse di tooSQL schemi
Indicazioni per la migrazione del tooSQL gli schemi SQL Data Warehouse. 

## <a name="plan-your-schema-migration"></a>Pianificare la migrazione dello schema

Quando si pianifica una migrazione, vedere hello [Cenni preliminari su tabella] [ table overview] toobecome familiarità con le considerazioni sulla progettazione di tabella, ad esempio le statistiche, distribuzione, il partizionamento e l'indicizzazione.  Vengono anche presentate alcune [funzionalità non supportate per le tabelle][unsupported table features] e le soluzioni alternative.

## <a name="use-user-defined-schemas-tooconsolidate-databases"></a>Utilizzare i database tooconsolidate degli schemi definiti dall'utente

È probabile che carico di lavoro esistente includa più di un database. Ad esempio un data warehouse di SQL Server può includere un database di staging, un database del data warehouse e alcuni database del data mart. In questa topologia ogni database viene eseguito come carico di lavoro separato con criteri di protezione separati.

Al contrario, SQL Data Warehouse viene eseguito hello intero data warehouse del carico di lavoro all'interno di un database. I join tra database non sono consentiti. Pertanto, Data Warehouse di SQL prevede che tutte le tabelle utilizzate da hello dati warehouse toobe archiviati all'interno di un database di hello.

È consigliabile utilizzare gli schemi definiti dall'utente tooconsolidate il carico di lavoro esistente in un database. Per esempi, vedere [Schemi definiti dall'utente](sql-data-warehouse-develop-user-defined-schemas.md)

## <a name="use-compatible-data-types"></a>Usare tipi di dati compatibili
Modificare il toobe di tipi di dati compatibile con SQL Data Warehouse. Per l'elenco dei tipi di dati supportati e non supportati, vedere [Tipi di dati][data types]. Questo argomento offre soluzioni alternative per i tipi di hello non supportato. Fornisce inoltre una query tooidentify i tipi esistenti che non sono supportati in SQL Data Warehouse.

## <a name="minimize-row-size"></a>Ridurre al minimo le dimensioni delle righe
Per prestazioni ottimali, ridurre al minimo la lunghezza di riga hello delle tabelle. Poiché le lunghezze riga più brevi comportare prestazioni toobetter, utilizzare i tipi di dati più piccolo hello che funzionano per i dati. 

Per la larghezza della riga della tabella, PolyBase ha un limite pari a 1 MB.  Se si prevede dati tooload in SQL Data Warehouse con PolyBase, aggiornare le larghezze di riga massimo tabelle toohave di minore di 1 MB. 

<!--
- For example, this table uses variable length data but hello largest possible size of hello row is still less than 1 MB. PolyBase will load data into this table.

- This table uses variable length data and hello defined row width is less than one MB. When loading rows, PolyBase allocates hello full length of hello variable-length data. hello full length of this row is greater than one MB.  PolyBase will not load data into this table.  

-->

## <a name="specify-hello-distribution-option"></a>Specificare l'opzione di distribuzione hello
SQL Data Warehouse è un sistema di database distribuito. Ogni tabella è distribuita o replicato in nodi di calcolo hello. È disponibile un'opzione di tabella che consente di specificare la modalità toodistribute hello dati. scelte di Hello sono round-robin, replicate, o hash distribuito. Ognuna presenta vantaggi e svantaggi. Se non si specifica l'opzione di distribuzione hello, SQL Data Warehouse userà round robin come predefinito hello.

- Round-robin è predefinito hello. È più semplice toouse di hello e carica i dati di hello più rapidamente possibile, ma join richiede lo spostamento dei dati che determina un rallentamento delle prestazioni delle query.
- Replicati archivia una copia della tabella hello in ogni nodo di calcolo. Le tabelle replicate sono efficienti perché non richiedono lo spostamento di dati per i join e le aggregazioni. Tuttavia richiedono risorse di archiviazione aggiuntive e di conseguenza sono la scelta migliore per tabelle di dimensioni contenute.
- Hash distribuita distribuisce le righe di hello in tutti i nodi di hello tramite una funzione hash. Poiché sono progettate tooprovide prestazioni elevate delle query in tabelle di grandi dimensioni, tabelle hash distribuiti sono cuore hello del Data Warehouse di SQL. Questa opzione richiede alcune pianificazione tooselect hello migliore colonna sulla quale toodistribute hello. Tuttavia, se non si sceglie hello colonna migliore hello prima volta, è possibile nuovamente distribuire facilmente hello dati in una colonna diversa. 

toochoose hello migliore opzione di distribuzione per ogni tabella, vedere [Distributed tabelle](sql-data-warehouse-tables-distribute.md).


## <a name="next-steps"></a>Passaggi successivi
Dopo avere eseguito la migrazione tooSQL di schema del database del Data Warehouse, procedere tooone di hello seguenti articoli:

* [Eseguire la migrazione dei dati][Migrate your data]
* [Eseguire la migrazione del codice][Migrate your code]

Per ulteriori informazioni sulle procedure consigliate di SQL Data Warehouse, vedere hello [consigliate] [ best practices] articolo.

<!--Image references-->

<!--Article references-->
[Migrate your code]: ./sql-data-warehouse-migrate-code.md
[Migrate your data]: ./sql-data-warehouse-migrate-data.md
[best practices]: ./sql-data-warehouse-best-practices.md
[table overview]: ./sql-data-warehouse-tables-overview.md
[unsupported table features]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features
[data types]: ./sql-data-warehouse-tables-data-types.md
[unsupported data types]: ./sql-data-warehouse-tables-data-types.md#unsupported-data-types

<!--MSDN references-->


<!--Other Web references-->
