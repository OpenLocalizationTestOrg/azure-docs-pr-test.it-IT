---
title: gli schemi definiti aaaUser in SQL Data Warehouse | Documenti Microsoft
description: Suggerimenti per l'uso di schemi Transact-SQL in Azure SQL Data Warehouse per lo sviluppo di soluzioni.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 52af5bd5-d5d3-4f9b-8704-06829fb924e3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: c411d6fed68e67c444a5871eab06182eaeb6dbf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="user-defined-schemas-in-sql-data-warehouse"></a>Schemi definiti dall'utente in SQL Data Warehouse
Data warehouse tradizionali spesso utilizzare database separati toocreate limiti per le applicazioni in base a carico di lavoro, dominio o sicurezza. Ad esempio, un data warehouse di SQL Server tradizionale potrebbe includere un database di gestione temporanea, un database del data warehouse e alcuni database del data mart. In questa topologia ogni database funziona come un carico di lavoro e il limite di sicurezza nell'architettura di hello.

Al contrario, SQL Data Warehouse viene eseguito hello intero data warehouse del carico di lavoro all'interno di un database. I join tra database non sono consentiti. Di conseguenza SQL Data Warehouse prevede che tutte le tabelle utilizzate da hello warehouse toobe archiviati all'interno di un database di hello.

> [!NOTE]
> SQL Data Warehouse non supporta query tra database di alcun tipo. Di conseguenza, implementazioni di data warehouse che utilizzano questo schema saranno necessario toobe rivisto.
> 
> 

## <a name="recommendations"></a>Raccomandazioni
Si tratta di indicazioni per il consolidamento di carichi di lavoro, sicurezza, dominio e i limiti funzionali mediante l'uso di schemi definiti dall'utente.

1. Utilizzare un Data Warehouse di SQL database toorun il carico di lavoro intero data warehouse
2. Consolidare dati warehouse ambiente toouse un Data Warehouse di SQL database esistente
3. Usare **degli schemi definiti dall'utente** limite hello tooprovide precedentemente implementata utilizzando i database.

Se gli schemi definiti dall'utente non sono stati usati in precedenza, si avrà uno slate pulito. Consente di usare semplicemente il nome di database precedente hello come base di hello per gli schemi definiti dall'utente nel database di SQL Data Warehouse hello.

Se gli schemi sono già stati usati, sono disponibili alcune opzioni:

1. Rimuovere i nomi di schema legacy hello e iniziare
2. Mantenere i nomi di schema legacy hello dal nome di tabella toohello nome schema legacy hello già in sospeso
3. Mantenere i nomi di schema legacy hello implementando viste su tabella hello in un toore aggiuntivo schema-creare una struttura dello schema precedente hello.

> [!NOTE]
> Al primo opzione 3 può sembrare opzione più interessante hello. È tuttavia importante sottolineare hello in dettaglio hello. Le viste sono di sola lettura in SQL Data Warehouse. Qualsiasi modifica di dati o la tabella sarà necessario toobe eseguita sulla tabella di base hello. L'opzione 3 introduce anche un livello di viste nel sistema. È possibile toogive questo un lavoro aggiuntivo se si utilizza le viste dell'architettura già.
> 
> 

### <a name="examples"></a>Esempi:
Implementare schemi definiti dall'utente in base ai nomi di database.

```sql
CREATE SCHEMA [stg]; -- stg previously database name for staging database
GO
CREATE SCHEMA [edw]; -- edw previously database name for hello data warehouse
GO
CREATE TABLE [stg].[customer] -- create staging tables in hello stg schema
(       CustKey BIGINT NOT NULL
,       ...
);
GO
CREATE TABLE [edw].[customer] -- create data warehouse tables in hello edw schema
(       CustKey BIGINT NOT NULL
,       ...
);
```

Mantenere schema legacy assegna un nome mediante il nome di tabella toohello. Usare gli schemi per il limite di carico di lavoro hello.

```sql
CREATE SCHEMA [stg]; -- stg defines hello staging boundary
GO
CREATE SCHEMA [edw]; -- edw defines hello data warehouse boundary
GO
CREATE TABLE [stg].[dim_customer] --pre-pend hello old schema name toohello table and create in hello staging boundary
(       CustKey BIGINT NOT NULL
,       ...
);
GO
CREATE TABLE [edw].[dim_customer] --pre-pend hello old schema name toohello table and create in hello data warehouse boundary
(       CustKey BIGINT NOT NULL
,       ...
);
```

Mantenere i nomi di schemi legacy usando viste.

```sql
CREATE SCHEMA [stg]; -- stg defines hello staging boundary
GO
CREATE SCHEMA [edw]; -- stg defines hello data warehouse boundary
GO
CREATE SCHEMA [dim]; -- edw defines hello legacy schema name boundary
GO
CREATE TABLE [stg].[customer] -- create hello base staging tables in hello staging boundary
(       CustKey    BIGINT NOT NULL
,       ...
)
GO
CREATE TABLE [edw].[customer] -- create hello base data warehouse tables in hello data warehouse boundary
(       CustKey    BIGINT NOT NULL
,       ...
)
GO
CREATE VIEW [dim].[customer] -- create a view in hello legacy schema name boundary for presentation consistency purposes only
AS
SELECT  CustKey
,       ...
FROM    [edw].customer
;
```

> [!NOTE]
> Qualsiasi modifica nella strategia di schema deve una revisione del modello di sicurezza hello per database hello. In molti casi potrebbe essere in grado di toosimplify modello di sicurezza hello assegnando le autorizzazioni a livello di schema hello. Se sono necessarie autorizzazioni più granulari, è possibile utilizzare i ruoli del database.
> 
> 

## <a name="next-steps"></a>Passaggi successivi
Per altri suggerimenti sullo sviluppo, vedere la [panoramica dello sviluppo][development overview].

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
