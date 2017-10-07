---
title: aaaUse tooinstrument query in SQL Data Warehouse di etichette | Documenti Microsoft
description: Suggerimenti per l'utilizzo di query tooinstrument etichette in Azure SQL Data Warehouse per lo sviluppo di soluzioni.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 44988de8-04c1-4fed-92be-e1935661a4e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: queries
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 82e7ea98e1417134227f1d7c529fdaf2f1df3853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-labels-tooinstrument-queries-in-sql-data-warehouse"></a>Utilizzare le query tooinstrument di etichette in SQL Data Warehouse
SQL Data Warehouse supporta un concetto detto etichette di query. Prima di approfondire il concetto, eccone un esempio:

```sql
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query Label')
;
```

L'ultima riga tag query toohello di hello stringa 'My Query Label'. Ciò è particolarmente utile come etichetta di hello è in grado query tramite hello DMV. Ciò offre a un meccanismo tootrack verso il basso di query problematiche e anche toohelp identificare lo stato di avanzamento tramite un'esecuzione ETL.

Una buona convenzione di denominazione è estremamente utile in questo caso. Ad esempio qualcosa di simile a ' progetto: procedura: istruzione: commento ' Guida toouniquely identificare query hello in tra tutto il codice hello nel controllo del codice sorgente.

viste a gestione dinamica di hello toosearch dall'etichetta, è possibile utilizzare hello seguente query che utilizza:

```sql
SELECT  *
FROM    sys.dm_pdw_exec_requests r
WHERE   r.[label] = 'My Query Label'
;
```

> [!NOTE]
> È essenziale che eseguire il wrapping delle parentesi quadre o virgolette doppie etichetta parola hello quando si eseguono query. Label è una parola riservata e causa un errore se non viene delimitata.
> 
> 

## <a name="next-steps"></a>Passaggi successivi
Per altri suggerimenti sullo sviluppo, vedere la [panoramica dello sviluppo][development overview].

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
