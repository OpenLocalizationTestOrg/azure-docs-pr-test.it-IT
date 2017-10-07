---
title: viste aaaUsing T-SQL in Azure SQL Data Warehouse | Documenti Microsoft
description: Suggerimenti per l'uso di viste Transact-SQL in Azure SQL Data Warehouse per lo sviluppo di soluzioni.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: b5208f32-8f4a-4056-8788-2adbb253d9fd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 3990b133946621691bdfa4b09523d21867470c74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="views-in-sql-data-warehouse"></a>Viste in SQL Data Warehouse
Le viste sono particolarmente utili in SQL Data Warehouse. Possono essere utilizzati in numerosi modi diversi tooimprove hello di qualità della soluzione.  In questo articolo sono illustrati alcuni esempi di come tooenrich la soluzione con le visualizzazioni, oltre alle limitazioni di hello necessarie toobe considerati.

> [!NOTE]
> La sintassi per `CREATE VIEW` non viene illustrata in questo articolo. Consultare toohello [CREATE VIEW] [ CREATE VIEW] articolo in MSDN per queste informazioni di riferimento.
> 
> 

## <a name="architectural-abstraction"></a>Astrazione dell'architettura
Uno schema molto comune di applicazione è toore-creare le tabelle mediante creazione tabella AS selezionare (un'istruzione CTAS) seguito da un oggetto ridenominazione modello durante il caricamento dei dati.

esempio Hello seguente aggiunge una nuova record tooa data dimensione Data. Si noti come un nuovo tabble, DimDate_New, viene creato e quindi rinominato versione originale di hello tooreplace della tabella hello.

```sql
CREATE TABLE dbo.DimDate_New
WITH (DISTRIBUTION = ROUND_ROBIN
, CLUSTERED INDEX (DateKey ASC)
)
AS
SELECT *
FROM   dbo.DimDate  AS prod
UNION ALL
SELECT *
FROM   dbo.DimDate_stg AS stg
;

RENAME OBJECT DimDate tooDimDate_Old;
RENAME OBJECT DimDate_New tooDimDate;

```

Tuttavia, usando questo approccio la visualizzazione delle tabelle nella vista dell'utente potrebbe non essere costante e potrebbero essere restituiti messaggi di errore di tabella non esistente. Viste possono essere utilizzati tooprovide gli utenti con un livello di presentazione coerente al contempo agli oggetti sottostanti hello vengono rinominati. Consentendo agli utenti l'accesso toohello dati tramite una visualizzazione, significa che non devono essere toohave visibilità delle tabelle sottostanti hello. Ciò offre un'esperienza utente coerente assicurando che le finestre di progettazione di hello data warehouse possono sviluppare il modello di dati di hello e ottimizzare le prestazioni utilizzando un'istruzione CTAS durante il processo di caricamento dati hello.    

## <a name="performance-optimization"></a>Ottimizzazione delle prestazioni
Viste possono essere inoltre utilizzato tooenforce prestazioni join tra tabelle. Ad esempio, una vista è possibile incorporare una chiave di distribuzione ridondante come parte di hello lo spostamento dei dati toominimize di criteri di unione.  Un altro vantaggio di una vista può essere una query specifica tooforce o hint di join. Utilizzo di visualizzazioni in questo modo garantisce che i join vengono sempre eseguiti in modo ottimale eliminando la necessità hello per costrutto corretto hello tooremember di utenti per i join.

## <a name="limitations"></a>Limitazioni
Le viste in SQL Data Warehouse sono solo metadati.  Di conseguenza hello le opzioni seguenti non sono disponibile:

* Non esiste alcuna opzione di binding dello schema
* Impossibile aggiornare le tabelle di base tramite la vista hello
* Non è possibile creare visualizzazioni sulle tabelle temporanee
* Nessun supporto per hello ESPANDI / hint NOEXPAND
* Non sono disponibili viste indicizzate in SQL Data Warehouse

## <a name="next-steps"></a>Passaggi successivi
Per altri suggerimenti sullo sviluppo, vedere [Panoramica sullo sviluppo per SQL Data Warehouse][SQL Data Warehouse development overview].
Per `CREATE VIEW` sintassi, vedere troppo[CREATE VIEW][CREATE VIEW].

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[CREATE VIEW]: https://msdn.microsoft.com/en-us/library/ms187956.aspx

<!--Other Web references-->
