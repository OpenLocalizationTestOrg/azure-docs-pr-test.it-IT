---
title: materiale sussidiario aaaDesign per tabelle replicate al fine - Azure SQL Data Warehouse | Documenti Microsoft
description: Consigli per la progettazione di tabelle replicate nello schema Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: ronortloff
manager: jhubbard
editor: 
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 07/14/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 5d405b8c404c65177b387ba959126839c1cf8799
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="design-guidance-for-using-replicated-tables-in-azure-sql-data-warehouse"></a>Linee guida di progettazione per l'uso di tabelle replicate in Azure SQL Data Warehouse
Questo articolo offre alcuni consigli per la progettazione di tabelle replicate nello schema Azure SQL Data Warehouse. Utilizzare le prestazioni delle query tooimprove queste indicazioni per ridurre la complessità di query e lo spostamento dei dati.

> [!NOTE]
> funzionalità di tabella replicata Hello è attualmente in anteprima pubblica. Alcuni comportamenti sono toochange soggetto.
> 

## <a name="prerequisites"></a>Prerequisiti
Questo articolo presuppone una certa familiarità con i concetti di distribuzione e spostamento dei dati in SQL Data Warehouse.  Per altre informazioni, vedere [Dati distribuiti](sql-data-warehouse-distributed-data.md). 

Come parte della struttura di tabella, comprendere il più possibile sulle modalità con cui viene eseguita una query di dati hello e dei dati.  Ad esempio, considerare queste domande:

- Le dimensioni è tabella hello?   
- Frequenza di aggiornamento tabella hello?   
- Sono presenti tabelle dei fatti e delle dimensioni in un data warehouse?   

## <a name="what-is-a-replicated-table"></a>Che cos'è una tabella replicata?
Una tabella replicata è una copia completa della tabella hello accessibile su ogni nodo di calcolo. La replica di una tabella rimuove i dati di tootransfer necessità di hello tra i nodi di calcolo prima di un'operazione join o aggregazione. Poiché la tabella hello dispone di più copie, le tabelle replicate funzionano meglio quando dimensioni della tabella hello sono minore di 2 GB compressi.

Hello diagramma seguente mostra una tabella replicata è accessibile in ogni nodo di calcolo. In SQL Data Warehouse, tabella replicata hello è il database di distribuzione tooa completamente copiato in ogni nodo di calcolo. 

![Tabella replicata](media/guidance-for-using-replicated-tables/replicated-table.png "Tabella replicata")  

Le tabelle replicate sono più adatte per piccole tabelle delle dimensioni in uno schema star. Le tabelle delle dimensioni sono generalmente di dimensioni che rende possibile toostore e mantengono più copie. Nelle dimensioni sono archiviati dati descrittivi che cambiano raramente, come il nome e l'indirizzo di un cliente e i dettagli del prodotto. Hello a modifica lenta natura dei dati hello comporta la ricompilazione di una tabella replicata hello toofewer. 

Provare a usare una tabella replicata nei casi seguenti:

- dimensioni tabella Hello su disco sono inferiore a 2 GB, indipendentemente dal numero di hello di righe. dimensioni di hello toofind di una tabella, è possibile utilizzare hello [DBCC PDW_SHOWSPACEUSED](https://docs.microsoft.com/en-us/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql) comando: `DBCC PDW_SHOWSPACEUSED('ReplTableCandidate')`. 
- Hello tabella viene utilizzata nelle operazioni di join che altrimenti richiederebbero lo spostamento dei dati. Ad esempio, un join sulle tabelle hash distribuita richiede lo spostamento dei dati quando le colonne di join hello non sono hello stessa colonna di distribuzione. Se una delle tabelle hash distribuita hello è ridotta, si consideri una tabella replicata. Un join in una tabella round robin richiede lo spostamento dei dati. È consigliabile usare tabelle replicate invece di tabelle round robin nella maggior parte dei casi. 


Prendere in considerazione la conversione di un oggetto esistente distribuito tooa tabella replicata tabella quando:

- Operazioni di spostamento dati di utilizzo che trasmettono i nodi di calcolo di hello dati tooall hello piani di query. Hello BroadcastMoveOperation è costoso e rallenta le prestazioni delle query. operazioni di spostamento dei dati tooview nei piani di query, utilizzare [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql).
 
Le tabelle replicate non possono produrre migliori prestazioni di query hello quando:

- tabella Hello è inserimento frequenti, aggiornamento ed eliminazione. Queste operazioni di data manipulation language (DML) richiedono una ricompilazione della tabella replicata hello. La ricompilazione causa spesso un rallentamento delle prestazioni.
- data warehouse di Hello viene ridotto di frequente. Ridimensionamento di un data warehouse Modifica numero hello dei nodi di calcolo, che comporta una ricompilazione.
- tabella Hello è un numero elevato di colonne, ma in genere, le operazioni sui dati accedere solo un numero limitato di colonne. In questo scenario, anziché replicare hello dell'intera tabella, potrebbe essere più efficace toohash distribuire tabella hello e quindi creare un indice sulle colonne hello si accede di frequente. Quando una query richiede lo spostamento dei dati, SQL Data Warehouse solo Sposta i dati in hello richieste colonne. 



## <a name="use-replicated-tables-with-simple-query-predicates"></a>Usare tabelle replicate con predicati di query semplici
Prima di scegliere toodistribute o replicare una tabella, considerare i tipi di hello di query toorun tabella hello. Se possibile:

- Usare tabelle replicate per query con predicati di query semplici, come le query di uguaglianza o disuguaglianza.
- Usare tabelle distribuite per query con predicati di query complessi, come LIKE o NOT LIKE.

Query di utilizzo elevato di CPU risultare migliori se lavoro hello è distribuito in tutti i nodi di calcolo hello. Ad esempio, le query che eseguono calcoli in ogni riga di una tabella hanno prestazioni migliori nelle tabelle distribuite che non nelle tabelle replicate. Tabella intera hello viene eseguita una query con utilizzo intensivo della CPU rispetto a una tabella replicata in ogni nodo di calcolo poiché una tabella replicata verrà archiviata in modo completo in ogni nodo di calcolo. Hello calcolo supplementare può rallentare le prestazioni delle query.

Questa query, ad esempio, ha un predicato complesso.  Viene eseguita più rapidamente quando il fornitore è una tabella distribuita invece di una tabella replicata. In questo esempio il fornitore può avere una distribuzione hash o una distribuzione round robin.

```sql

SELECT EnglishProductName 
FROM DimProduct 
WHERE EnglishDescription LIKE '%frame%comfortable%'

```

## <a name="convert-existing-round-robin-tables-tooreplicated-tables"></a>Convertire le tabelle tooreplicated round-robin tabelle esistenti
Se si dispongono già di tabelle algoritmo round-robin, è consigliabile convertire in tabelle tooreplicated se soddisfano i criteri descritti in questo articolo. Le tabelle replicate migliorare le prestazioni rispetto alle tabelle algoritmo round-robin perché eliminano hello necessario per lo spostamento dei dati.  Una tabella round robin richiede lo spostamento dei dati per i join. 

Questo esempio viene utilizzato [un'istruzione CTAS](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse) toochange hello DimSalesTerritory tabella tooa tabella replicata. Questo esempio funziona indipendentemente dal fatto che per DimSalesTerritory sia stata eseguita una distribuzione hash o round robin.

```sql
CREATE TABLE [dbo].[DimSalesTerritory_REPLICATE]   
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = REPLICATE  
  )  
AS SELECT * FROM [dbo].[DimSalesTerritory]
OPTION  (LABEL  = 'CTAS : DimSalesTerritory_REPLICATE') 

--Create statistics on new table
CREATE STATISTICS [SalesTerritoryKey] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryKey]);
CREATE STATISTICS [SalesTerritoryAlternateKey] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryAlternateKey]);
CREATE STATISTICS [SalesTerritoryRegion] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryRegion]);
CREATE STATISTICS [SalesTerritoryCountry] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryCountry]);
CREATE STATISTICS [SalesTerritoryGroup] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryGroup]);

-- Switch table names
RENAME OBJECT [dbo].[DimSalesTerritory] too[DimSalesTerritory_old];
RENAME OBJECT [dbo].[DimSalesTerritory_REPLICATE] too[DimSalesTerritory];

DROP TABLE [dbo].[DimSalesTerritory_old];
```  

### <a name="query-performance-example-for-round-robin-versus-replicated"></a>Esempio di prestazioni delle query delle tabelle round robin rispetto alle tabelle replicate 

Una tabella replicata non richiede alcuno spostamento dei dati per i join perché l'intera tabella hello è già presente in ogni nodo di calcolo. Se le tabelle delle dimensioni hello sono round-robin distribuito, un join copia tabella della dimensione hello tooeach completo del nodo di calcolo. dati hello toomove, piano di query hello contiene un'operazione denominata BroadcastMoveOperation. Questo tipo di operazione di spostamento dei dati rallenta le prestazioni delle query e viene eliminato usando tabelle replicate. passaggi di piano di query tooview, utilizzare hello [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql) vista del catalogo sys. 

Ad esempio, nella query seguente in base allo schema AdventureWorks hello, hello ` FactInternetSales` tabella è distribuita hash. Hello `DimDate` e `DimSalesTerritory` le tabelle sono tabelle delle dimensioni più piccole. Questa query restituisce le vendite totali hello in Nord America per l'anno fiscale 2004:
 
```sql
SELECT [TotalSalesAmount] = SUM(SalesAmount)
FROM dbo.FactInternetSales s
INNER JOIN dbo.DimDate d
  ON d.DateKey = s.OrderDateKey
INNER JOIN dbo.DimSalesTerritory t
  ON t.SalesTerritoryKey = s.SalesTerritoryKey
WHERE d.FiscalYear = 2004
  AND t.SalesTerritoryGroup = 'North America'
```
`DimDate` e `DimSalesTerritory` sono state ricreate come tabelle round robin. Di conseguenza, query hello ha dimostrato hello piano di query che ha più trasmissione spostare le operazioni seguenti: 
 
![Piano di query round robin](media/design-guidance-for-replicated-tables/round-robin-tables-query-plan.jpg) 

È stato creato nuovamente `DimDate` e `DimSalesTerritory` come tabelle duplicate ed è stato eseguito query hello nuovamente. piano di query risultante Hello è molto più breve e non hanno uno trasmette passa.

![Piano di query di tabelle replicate](media/design-guidance-for-replicated-tables/replicated-tables-query-plan.jpg) 


## <a name="performance-considerations-for-modifying-replicated-tables"></a>Considerazioni sulle prestazioni per la modifica di tabelle replicate
SQL Data Warehouse implementa una tabella replicata dal mantenimento di una versione principale della tabella di hello. Copia database di distribuzione tooone versione master hello in ogni nodo di calcolo. Quando viene apportata una modifica, SQL Data Warehouse prima Aggiorna tabella master hello. Richiede quindi una ricompilazione delle tabelle di hello in ogni nodo di calcolo. Una ricompilazione di una tabella replicata include la copia del nodo di calcolo tooeach hello tabella e quindi ricompilare gli indici di hello.

Le compilazioni sono necessarie dopo le operazioni seguenti:
- Vengono caricati o modificati dati
- Hello data warehouse è l'impostazione DWU diversa scalato tooa
- Viene aggiornata la definizione di tabella

Le ricompilazioni non sono necessarie dopo le operazioni seguenti:
- Operazione di sospensione
- Operazione di ripresa

ricompilazione di Hello non avviene immediatamente dopo la modifica di dati. Invece di attivazione di ricompilazione hello hello prima volta una query vengono selezionati dalla tabella hello.  All'interno di hello iniziale from dell'istruzione select nella tabella hello sono tabella replicata di passaggi toorebuild hello.  Poiché hello ricompilazione viene eseguita all'interno di query hello, istruzione select iniziale toohello hello impatto potrebbe essere significativo a seconda delle dimensioni di hello della tabella hello.  Se più tabelle replicate sono coinvolte che richiedono la ricompilazione, ogni copia viene ricompilato in serie di passaggi all'interno di istruzione hello.  la coerenza dei dati durante la ricompilazione hello di hello toomaintain replicati tabella che acquisizione di un blocco esclusivo sulla tabella hello.  blocco di Hello impedisce tutte tabella toohello di accesso per la durata di hello di ricompilazione hello. 

### <a name="use-indexes-conservatively"></a>Usare gli indici con moderazione
Procedure consigliate di indicizzazione standard si applicano tooreplicated tabelle. Ogni indice di tabella replicata come parte di ricompilazione hello viene ricompilato SQL Data Warehouse. Utilizzare solo indici quando miglioramento delle prestazioni hello supera il costo di hello di ricompilazione di indici hello.  
 
### <a name="batch-data-loads"></a>Caricare in batch i dati
Quando si caricano dati in tabelle replicate, provare la ricompilazione toominimize da inviare in batch carica. Eseguire tutti i carichi di hello in batch prima di eseguire le istruzioni select.

Ad esempio, questo modello di carico carica dati da quattro origini e richiama quattro ricompilazioni. 

- Caricamento dall'origine 1.
- L'istruzione di selezione attiva la ricompilazione 1.
- Caricamento dall'origine 2.
- L'istruzione di selezione attiva la ricompilazione 2.
- Caricamento dall'origine 3.
- L'istruzione di selezione attiva la ricompilazione 3.
- Caricamento dall'origine 4.
- L'istruzione di selezione attiva la ricompilazione 4.

Ad esempio, questo modello di carico carica dati da quattro origini, ma richiama una sola ricompilazione.

- Caricamento dall'origine 1.
- Caricamento dall'origine 2.
- Caricamento dall'origine 3.
- Caricamento dall'origine 4.
- L'istruzione di selezione attiva la ricompilazione.


### <a name="rebuild-a-replicated-table-after-a-batch-load"></a>Ricompilare una tabella replicata dopo un caricamento in batch
tempi di esecuzione di query coerente tooensure, è consigliabile forzare un aggiornamento di tabelle hello replicata dopo un carico batch. In caso contrario, prima query hello deve attendere hello tabelle toorefresh, che include la ricompilazione degli indici hello. A seconda delle dimensioni di hello e numero di tabelle replicate interessati, l'impatto sulle prestazioni di hello può essere significativo.  

Questa query utilizza hello [sys.pdw_replicated_table_cache_state](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-pdw-replicated-table-cache-state-transact-sql) hello toolist DMV replicati tabelle modificate, ma non è state ricompilate.

```sql 
SELECT [ReplicatedTable] = t.[name]
  FROM sys.tables t  
  JOIN sys.pdw_replicated_table_cache_state c  
    ON c.object_id = t.object_id 
  JOIN sys.pdw_table_distribution_properties p 
    ON p.object_id = t.object_id 
  WHERE c.[state] = 'NotReady'
    AND p.[distribution_policy_desc] = 'REPLICATE'
```
 
tooforce una ricompilazione, eseguire hello successiva istruzione di ciascuna tabella hello output precedente. 

```sql
SELECT TOP 1 * FROM [ReplicatedTable]
``` 
 
## <a name="next-steps"></a>Passaggi successivi 
toocreate una tabella replicata, utilizzare una di queste istruzioni:

- [CREATE TABLE (Azure SQL Data Warehouse)](https://docs.microsoft.com/sql/t-sql/statements/create-table-azure-sql-data-warehouse)
- [CREATE TABLE AS SELECT (Azure SQL Data Warehouse](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse)

Per una panoramica delle tabelle distribuite, vedere [Tabelle distribuite](sql-data-warehouse-tables-distribute.md).



