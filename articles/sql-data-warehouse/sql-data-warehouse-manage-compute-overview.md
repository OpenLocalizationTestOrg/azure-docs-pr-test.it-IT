---
title: aaaManage calcolo power in Azure SQL Data Warehouse (panoramica) | Documenti Microsoft
description: "Funzionalità relative alla scalabilità orizzontale delle prestazioni in Azure SQL Data Warehouse. Scalabilità orizzontale grazie alla regolazione Dwu o sospendere e riprendere toosave risorse di calcolo dei costi."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: 
ms.assetid: e13a82b0-abfe-429f-ac3c-f2b6789a70c6
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 03/22/2017
ms.author: elbutter
ms.openlocfilehash: 1ffbe8d694ac181eaeb6f585a2cee87a570ed7d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-overview"></a>Gestire la potenza di calcolo in Azure SQL Data Warehouse (Panoramica)
> [!div class="op_single_selector"]
> * [Panoramica](sql-data-warehouse-manage-compute-overview.md)
> * [Portale](sql-data-warehouse-manage-compute-portal.md)
> * [PowerShell](sql-data-warehouse-manage-compute-powershell.md)
> * [REST](sql-data-warehouse-manage-compute-rest-api.md)
> * [TSQL](sql-data-warehouse-manage-compute-tsql.md)
>
>

architettura di SQL Data Warehouse di Hello separa l'archiviazione e calcolo, consentendo di ogni tooscale in modo indipendente. Di conseguenza, calcolo può essere scalato toomeet prestazioni richieste indipendente della quantità di hello di dati. Come conseguenza logica di questa architettura, la [fatturazione][billed] è separata per calcolo e archiviazione. 

Questa panoramica descrive la scalabilità orizzontale con SQL Data Warehouse e come tooutilize hello sospendere, riprendere e funzionalità di scalabilità di SQL Data Warehouse. Consultare hello [del data warehouse di unità (Dwu)] [ data warehouse units (DWUs)] toolearn pagina correlazione Dwu e prestazioni. 

## <a name="how-compute-management-operations-work-in-sql-data-warehouse"></a>Funzionamento delle operazioni di gestione del calcolo in SQL Data Warehouse
architettura di Hello per SQL Data Warehouse è costituita da un nodo del controllo, nodi di calcolo e hello a livello di archiviazione distribuiti tra le distribuzioni di 60. 

Durante una sessione attiva normale in SQL Data Warehouse, nodo head del sistema gestisce i metadati di hello e contiene query optimizer di hello distribuita. Al di sotto del nodo head si trovano i nodi di calcolo e il livello di archiviazione. Per un numero di DWU di 400, il sistema dispone di un nodo head, quattro nodi di calcolo e il livello di archiviazione hello, composta da 60 distribuzioni. 

Quando si essere sottoposto a una scala o sospesa l'operazione, sistema hello innanzitutto termina tutte le query in ingresso e quindi eseguire il rollback delle transazioni tooensure uno stato coerente. Per le operazioni di scalabilità, quest'ultima si verificherà solamente al completamento del rollback di transazione. Per un'operazione di scalabilità verticale, disposizioni sistema hello hello numero di nodi di calcolo molto desiderato e quindi inizia a livello di archiviazione toohello nodi calcolo hello ricollegamento. Per un'operazione di scalabilità orizzontale, hello nodi non necessari vengono rilasciati e nodi di calcolo rimanenti hello ricollegare stessi toohello numero appropriato di distribuzioni. Per un'operazione di sospensione, tutte di calcolo vengono rilasciati i nodi e il sistema verrà sottoposta ad un'ampia gamma di metadati operazioni tooleave sistema finale in uno stato stabile.

| DWU  | \# di nodi di calcolo | \# di distribuzioni per nodo |
| ---- | ------------------ | ---------------------------- |
| 100  | 1                  | 60                           |
| 200  | 2                  | 30                           |
| 300  | 3                  | 20                           |
| 400  | 4                  | 15                           |
| 500  | 5                  | 12                           |
| 600  | 6                  | 10                           |
| 1000 | 10                 | 6                            |
| 1200 | 12                 | 5                            |
| 1500 | 15                 | 4                            |
| 2000 | 20                 | 3                            |
| 3000 | 30                 | 2                            |
| 6000 | 60                 | 1                            |

sono tre funzioni principali di Hello per la gestione di calcolo:

1. Sospendi
2. Riprendi
3. Scalabilità

Ognuna di queste operazioni potrebbe richiedere diversi minuti toocomplete. Se si scala, sospensione/ripresa automaticamente, è consigliabile tooimplement logica tooensure determinate operazioni completate prima di procedere con un'altra azione. 

Verifica dello stato del database hello tramite vari endpoint consentirà toocorrectly implementare automazione di tali operazioni. portale Hello invierà una notifica al completamento di un'operazione e hello database corrente dello stato, ma non per il controllo a livello di codice di stato. 

>  [!NOTE]
>
>  La funzionalità di gestione del calcolo non è presente in tutti gli endpoint.
>
>  

|              | Sospensione/ripresa | Scalabilità | Controllare lo stato del database |
| ------------ | ------------ | ----- | -------------------- |
| Portale di Azure | Sì          | Sì   | **No**               |
| PowerShell   | Sì          | Sì   | Sì                  |
| API REST     | Sì          | Sì   | Sì                  |
| T-SQL        | **No**       | Sì   | Sì                  |



<a name="scale-compute-bk"></a>

## <a name="scale-compute"></a>Ridimensionare le risorse di calcolo

Le prestazioni in SQL Data Warehouse vengono misurate in [Unità Data Warehouse (DWU)][data warehouse units (DWUs)], una misura astratta delle risorse di calcolo come CPU, memoria e larghezza di banda I/O. Un utente che desidera tooscale le prestazioni del sistema relativi a tale scopo in vari modi, ad esempio tramite il portale di hello, T-SQL e le API REST. 

### <a name="how-do-i-scale-compute"></a>In che modo è possibile ridimensionare le risorse di calcolo?
Potenza di calcolo viene gestita SQL Data Warehouse modificando l'impostazione DWU hello. Le prestazioni aumentano in modo [lineare][linearly] man mano che si aggiungono più DWU per determinate operazioni.  Esistono varie offerte di DWU per assicurare un cambiamento netto delle prestazioni durante il ridimensionamento verticale del sistema. 

tooadjust Dwu, è possibile utilizzare uno di questi singoli metodi.

* [Ridimensionare la potenza di calcolo con il portale di Azure][Scale compute power with Azure portal]
* [Ridimensionare la potenza di calcolo con PowerShell][Scale compute power with PowerShell]
* [Ridimensionare la potenza di calcolo con le API REST][Scale compute power with REST APIs]
* [Ridimensionare la potenza di calcolo con TSQL][Scale compute power with TSQL]

### <a name="how-many-dwus-should-i-use"></a>Quante DWU è consigliabile usare?

toounderstand è il valore DWU ideale, provare a scalabilità verticale e l'esecuzione di alcune query dopo il caricamento dei dati. Poiché il ridimensionamento è rapido, è possibile provare diversi livelli di prestazioni in un'ora o meno. 

> [!Note] 
> SQL Data Warehouse è progettata tooprocess grandi quantità di dati. toosee capacità true per la scalabilità, soprattutto in più grande Dwu, si desidera toouse grandi set di dati che si avvicina o supera 1 TB.

Indicazioni per la ricerca hello DWU migliore per il carico di lavoro:

1. Per un data warehouse in sviluppo, iniziare con un numero più limitato di prestazioni DWU.  Un buon punto di partenza è DW400 o DW200.
2. Monitorare le prestazioni dell'applicazione, osservare il numero di hello di Dwu selezionato confrontato prestazioni toohello che è osservare.
3. Determinare la quantità delle prestazioni di velocità superiore o inferiore devono essere per si tooreach hello ottimale livello di prestazioni per le proprie esigenze, presupponendo una scala lineare.
4. Aumentare o diminuire il numero di hello di Dwu in proporzione toohow molto più veloce o lenta desiderato tooperform il carico di lavoro. 
5. Continuare ad apportare modifiche finché non si raggiunge un livello di prestazioni ottimale per i propri requisiti aziendali.

> [!NOTE]
>
> Le prestazioni delle query aumentano solo con la parallelizzazione ulteriori se lavoro hello può essere suddivise tra nodi di calcolo. Se si ritiene che il ridimensionamento non sta cambiando le prestazioni, estrarre il nostro toocheck articoli se i dati non viene distribuiti o se si stanno introducendo una grande quantità di spostamento dei dati di ottimizzazione delle prestazioni. 

### <a name="when-should-i-scale-dwus"></a>Quando è necessario ridimensionare le DWU?
Scalabilità Dwu modifica hello scenari importanti seguenti:

1. Modifica in modo lineare delle prestazioni del sistema hello per le analisi, le aggregazioni e un'istruzione CTAS istruzioni
2. Aumentare il numero di hello di reader e writer durante il caricamento con PolyBase
3. Numero massimo di query simultanee e slot di concorrenza

Indicazioni relative al tooscale Dwu:

1. Prima di eseguire un'operazione di caricamento o trasformazione di quantità di dati elevate, ridimensionare le DWU in modo che i dati siano disponibili più rapidamente.
2. Durante le ore, la scalabilità tooaccommodate un numero maggiore di query simultanee. 

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a>Sospendere le risorse di calcolo
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

toopause un database, utilizzare uno di questi singoli metodi.

* [Sospendere le risorse di calcolo con il portale di Azure][Pause compute with Azure portal]
* [Sospendere le risorse di calcolo con PowerShell][Pause compute with PowerShell]
* [Sospendere le risorse di calcolo con le API REST][Pause compute with REST APIs]

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a>Riavviare le risorse di calcolo
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

tooresume un database, utilizzare uno di questi singoli metodi.

* [Riavviare le risorse di calcolo con il portale di Azure][Resume compute with Azure portal]
* [Riavviare le risorse di calcolo con PowerShell][Resume compute with PowerShell]
* [Riavviare le risorse di calcolo con le API REST][Resume compute with REST APIs]

<a name="check-compute-bk"></a>

## <a name="check-database-state"></a>Controllare lo stato del database 

tooresume un database, utilizzare uno di questi singoli metodi.

- [Controllare lo stato del database con T-SQL][Check database state with T-SQL]
- [Controllare lo stato del database con PowerShell][Check database state with PowerShell]
- [Controllare lo stato del database con le API REST][Check database state with REST APIs]

## <a name="permissions"></a>Autorizzazioni

Scala database hello richiede autorizzazioni hello descritte in [ALTER DATABASE][ALTER DATABASE].  Sospendere e riprendere richiedono hello [collaboratore DB SQL] [ SQL DB Contributor] autorizzazione, in particolare Microsoft.Sql/servers/databases/action.

<a name="next-steps-bk"></a>

## <a name="next-steps"></a>Passaggi successivi
Fare riferimento toohello toohelp articoli è comprendere alcuni concetti di prestazioni chiave aggiuntive seguenti:

* [Gestione della concorrenza e del carico di lavoro][Workload and concurrency management]
* [Panoramica delle tabelle][Table design overview]
* [Distribuzione di tabelle][Table distribution]
* [Indicizzazione di tabelle][Table indexing]
* [Partizionamento di tabelle][Table partitioning]
* [Statistiche delle tabelle][Table statistics]
* [Procedure consigliate][Best practices]

<!--Image reference-->

<!--Article references-->
[data warehouse units (DWUs)]: ./sql-data-warehouse-overview-what-is.md#predictable-and-scalable-performance-with-data-warehouse-units
[billed]: https://azure.microsoft.com/en-us/pricing/details/sql-data-warehouse/
[linearly]: ./sql-data-warehouse-overview-what-is.md#predictable-and-scalable-performance-with-data-warehouse-units
[Scale compute power with Azure portal]: ./sql-data-warehouse-manage-compute-portal.md#scale-compute-power
[Scale compute power with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#scale-compute-bk
[Scale compute power with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#scale-compute-bk
[Scale compute power with TSQL]: ./sql-data-warehouse-manage-compute-tsql.md#scale-compute-bk

[capacity limits]: ./sql-data-warehouse-service-capacity-limits.md

[Pause compute with Azure portal]:  ./sql-data-warehouse-manage-compute-portal.md#pause-compute-bk
[Pause compute with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#pause-compute-bk
[Pause compute with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#pause-compute-bk

[Resume compute with Azure portal]:  ./sql-data-warehouse-manage-compute-portal.md#resume-compute-bk
[Resume compute with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#resume-compute-bk
[Resume compute with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#resume-compute-bk

[Check database state with T-SQL]: ./sql-data-warehouse-manage-compute-tsql.md#check-database-state-and-operation-progress
[Check database state with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#check-database-state
[Check database state with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#check-database-state

[Workload and concurrency management]: ./sql-data-warehouse-develop-concurrency.md
[Table design overview]: ./sql-data-warehouse-tables-overview.md
[Table distribution]: ./sql-data-warehouse-tables-distribute.md
[Table indexing]: ./sql-data-warehouse-tables-index.md
[Table partitioning]: ./sql-data-warehouse-tables-partition.md
[Table statistics]: ./sql-data-warehouse-tables-statistics.md
[Best practices]: ./sql-data-warehouse-best-practices.md
[development overview]: ./sql-data-warehouse-overview-develop.md

[SQL DB Contributor]: ../active-directory/role-based-access-built-in-roles.md#sql-db-contributor

<!--MSDN references-->
[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx

<!--Other Web references-->
[Azure portal]: http://portal.azure.com/
