---
title: "chiavi surrogate aaaCreate utilizzando identità | Documenti Microsoft"
description: "Informazioni su come surrogato toocreate di identità toouse chiavi per le tabelle."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: faa1034d-314c-4f9d-af81-f5a9aedf33e4
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 06/13/2017
ms.author: jrj;barbkess
ms.openlocfilehash: 502cdd2b510b229b2a19c1f78b11862a7386ae3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-surrogate-keys-by-using-identity"></a>Creare chiavi surrogate con IDENTITY
> [!div class="op_single_selector"]
> * [Panoramica][Overview]
> * [Tipi di dati][Data Types]
> * [Distribuzione][Distribute]
> * [Indice][Index]
> * [Partizione][Partition]
> * [Statistiche][Statistics]
> * [Temporanee][Temporary]
> * [Identità][Identity]
> 
> 

Quando si progettano i modelli di data warehouse, molti progettisti di dati come chiavi surrogate toocreate le tabelle. È possibile utilizzare hello identità proprietà tooachieve questo obiettivo semplice ed efficace senza influenzare le prestazioni del carico. 

## <a name="get-started-with-identity"></a>Introduzione a IDENTITY
È possibile definire una tabella con proprietà IDENTITY hello quando si crea la tabella hello utilizzando la sintassi simile toohello istruzione:

```sql
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1) NOT NULL
,   C2 INT NULL
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;
```

È quindi possibile utilizzare `INSERT..SELECT` tabella hello toopopulate.

## <a name="behavior"></a>Comportamento
Hello proprietà IDENTITY è progettato tooscale out tra tutte le distribuzioni di hello nel data warehouse di hello senza influenzare le prestazioni del carico. Pertanto, l'implementazione hello dell'identità è orientato per raggiungere questi obiettivi. In questa sezione evidenzia sfumature hello di hello implementazione toohelp comprenderne meglio.  

### <a name="allocation-of-values"></a>Allocazione dei valori
Hello proprietà IDENTITY non garantisce l'ordine di hello in cui hello vengono allocati valori surrogati, che riflette il comportamento di hello di SQL Server e Database SQL di Azure. Tuttavia, in Azure SQL Data Warehouse, mancanza di hello di una garanzia è più evidente. 

Hello di esempio seguente viene illustrato questo concetto:

```sql
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1)    NOT NULL
,   C2 VARCHAR(30)              NULL
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;

INSERT INTO dbo.T1
VALUES (NULL);

INSERT INTO dbo.T1
VALUES (NULL);

SELECT *
FROM dbo.T1;

DBCC PDW_SHOWSPACEUSED('dbo.T1');
```

In hello sopra riportato, due righe ottenuto nella distribuzione 1. prima riga Hello ha hello surrogato valore 1 nella colonna `C1`, e hello seconda riga ha valore surrogato hello 61. Entrambi questi valori sono stati generati da hello proprietà IDENTITY. Allocazione di hello dei valori hello, tuttavia, non è contiguo. Questo comportamento dipende dalla progettazione.

### <a name="skewed-data"></a>Dati asimmetrici 
Hello intervallo di valori per il tipo di dati hello sono distribuiti uniformemente tra le distribuzioni di hello. In caso di una tabella distribuita da dati asimmetrici, hello quindi l'intervallo di valori può esaurirsi toohello disponibile il tipo di dati in modo anomalo. Ad esempio, se tutti i dati di hello finisce in una singola distribuzione, quindi in modo efficace hello tabella ha accesso tooonly sessantesimo a uno dei valori hello hello del tipo di dati. Per questo motivo, la proprietà IDENTITY hello è limitato troppo`INT` e `BIGINT` solo i tipi di dati.

### <a name="selectinto"></a>SELECT..INTO
Quando una colonna IDENTITY esistente è selezionata in una nuova tabella, hello nuova colonna eredita la proprietà IDENTITY hello, a meno che non viene soddisfatta una delle seguenti condizioni hello:
- istruzione SELECT Hello contiene un join.
- Più istruzioni SELECT sono unite in join tramite l'istruzione UNION.
- colonna IDENTITY Hello è elencata più di una volta nell'elenco di selezione hello.
- colonna IDENTITY Hello fa parte di un'espressione.
    
Se una di queste condizioni è true, la colonna hello viene creata non NULL, anziché ereditare proprietà IDENTITY hello.

### <a name="create-table-as-select"></a>CREATE TABLE AS SELECT
Crea tabella AS selezionare (un'istruzione CTAS) segue hello stesso comportamento SQL Server che è documentato per SELECT... IN. Tuttavia, è possibile specificare una proprietà IDENTITY in una definizione di colonna hello di hello `CREATE TABLE` fa parte dell'istruzione hello. È inoltre possibile utilizzare la funzione di identità hello in hello `SELECT` fa parte di un'istruzione CTAS hello. toopopulate una tabella, è necessario toouse `CREATE TABLE` toodefine hello tabella seguite dalle `INSERT..SELECT` toopopulate è.

## <a name="explicitly-insert-values-into-an-identity-column"></a>Inserire in modo esplicito valori in una colonna IDENTITY 
SQL Data Warehouse supporta la sintassi `SET IDENTITY_INSERT <your table> ON|OFF`. È possibile utilizzare i valori di insert tooexplicitly questa sintassi nella colonna IDENTITY hello.

Molti progettisti di dati come negativo predefiniti toouse i valori per alcune righe relative dimensioni. Un esempio è hello -1 o la riga "membro sconosciuto". 

passare allo script successivo Hello viene illustrato come tooexplicitly aggiungere questa riga tramite SET IDENTITY_INSERT:

```sql
SET IDENTITY_INSERT dbo.T1 ON;

INSERT INTO dbo.T1
(   C1
,   C2
)
VALUES (-1,'UNKNOWN')
;

SET IDENTITY_INSERT dbo.T1 OFF;

SELECT  *
FROM    dbo.T1
;
```    

## <a name="load-data-into-a-table-with-identity"></a>Caricare i dati in una tabella con IDENTITY

presenza di Hello di hello proprietà IDENTITY include codice implicazioni tooyour il caricamento di dati. Questa sezione evidenzia alcuni modelli di base per il caricamento di dati nelle tabelle usando IDENTITY. 

### <a name="load-data-with-polybase"></a>Caricare dati con PolyBase
dati tooload in una tabella e generare una chiave surrogata utilizzando l'identità, creare la tabella hello e quindi utilizza l'istruzione INSERT... SELECT o INSERT... I valori tooperform hello carico.

Hello esempio seguente vengono evidenziate modello di base hello:
 
```sql
--CREATE TABLE with IDENTITY
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1)
,   C2 VARCHAR(30)
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;

--Use INSERT..SELECT toopopulate hello table from an external table
INSERT INTO dbo.T1
(C2)
SELECT  C2
FROM    ext.T1
;

SELECT  *
FROM    dbo.T1
;

DBCC PDW_SHOWSPACEUSED('dbo.T1');
```

> [!NOTE] 
> Non è possibile toouse `CREATE TABLE AS SELECT` attualmente durante il caricamento di dati in una tabella con una colonna IDENTITY.
> 

Per ulteriori informazioni sul caricamento dei dati tramite lo strumento programma (BCP) di copia bulk di hello, vedere hello seguenti articoli:

- [Caricare dati con PolyBase][]
- [Procedure consigliate per PolyBase][]

### <a name="load-data-with-bcp"></a>Caricare dati con BCP
BCP è uno strumento da riga di comando che è possibile utilizzare dati tooload in SQL Data Warehouse. Uno dei relativi parametri (-E) controlli hello comportamento dell'utilità BCP quando si caricano dati in una tabella con una colonna IDENTITY. 

Quando viene specificato -E, vengono mantenuti i valori hello contenuti nel file di input per la colonna hello hello con identità. Se -E è *non* specificato, i valori hello in questa colonna vengono ignorati. Se la colonna identity hello non è inclusa, dati hello viene caricati come di consueto. i valori Hello vengono generati in base a criteri toohello di incremento e valore di inizializzazione della proprietà hello.

Per ulteriori informazioni sul caricamento dei dati tramite BCP in, vedere hello seguenti articoli:

- [Caricare dati con BCP][]
- [BCP in MSDN][]

## <a name="catalog-views"></a>Viste del catalogo
SQL Data Warehouse supporta hello `sys.identity_columns` vista del catalogo. Questa vista può essere utilizzato tooidentify una colonna che contiene la proprietà IDENTITY hello.

toohelp è comprendere meglio lo schema del database hello, questo esempio viene illustrato come toointegrate `sys.identity_columns` con altre viste del catalogo di sistema:

```sql
SELECT  sm.name
,       tb.name
,       co.name
,       CASE WHEN ic.column_id IS NOT NULL
             THEN 1
        ELSE 0
        END AS is_identity 
FROM        sys.schemas AS sm
JOIN        sys.tables  AS tb           ON  sm.schema_id = tb.schema_id
JOIN        sys.columns AS co           ON  tb.object_id = co.object_id
LEFT JOIN   sys.identity_columns AS ic  ON  co.object_id = ic.object_id
                                        AND co.column_id = ic.column_id
WHERE   sm.name = 'dbo'
AND     tb.name = 'T1'
;
```

## <a name="limitations"></a>Limitazioni
Hello proprietà IDENTITY non può essere utilizzato in hello seguenti scenari:
- In cui hello colonna non è di tipo INT o BIGINT
- In cui la colonna hello è anche la chiave di distribuzione hello
- In cui la tabella hello è una tabella esterna 

Hello seguenti funzioni correlate non è supportata in SQL Data Warehouse:

- [IDENTITY()][]
- [@@IDENTITY][]
- [SCOPE_IDENTITY][]
- [IDENT_CURRENT][]
- [IDENT_INCR][]
- [IDENT_SEED][]
- [DBCC CHECK_IDENT()][]

## <a name="tasks"></a>Attività

In questa sezione fornisce alcuni esempi di codice è possibile utilizzare le attività comuni tooperform quando si lavora con le colonne IDENTITY.

> [!NOTE] 
> Colonna C1 è hello identità in hello tutte le seguenti attività.
> 
 
### <a name="find-hello-highest-allocated-value-for-a-table"></a>Trovare il valore di hello massima allocata per una tabella
Hello utilizzare `MAX()` funzione toodetermine hello valore massima allocata per una tabella distribuita:

```sql
SELECT  MAX(C1)
FROM    dbo.T1
``` 

### <a name="find-hello-seed-and-increment-for-hello-identity-property"></a>Trovare hello inizializzazione e incremento per la proprietà IDENTITY hello
È possibile utilizzare hello catalogo viste toodiscover hello identità di incremento e valore di inizializzazione valori di configurazione per una tabella utilizzando hello seguente query: 

```sql
SELECT  sm.name
,       tb.name
,       co.name
,       ic.seed_value
,       ic.increment_value 
FROM        sys.schemas AS sm
JOIN        sys.tables  AS tb           ON  sm.schema_id = tb.schema_id
JOIN        sys.columns AS co           ON  tb.object_id = co.object_id
JOIN        sys.identity_columns AS ic  ON  co.object_id = ic.object_id
                                        AND co.column_id = ic.column_id
WHERE   sm.name = 'dbo'
AND     tb.name = 'T1'
;
```

## <a name="next-steps"></a>Passaggi successivi

* toolearn più sullo sviluppo di tabelle, vedere [Cenni preliminari su tabella][Overview], [tipi di dati di tabella][Data Types], [distribuireunatabella] [ Distribute], [Indicizzare una tabella][Index], [una tabella di partizione][Partition], e [ Tabelle temporanee][Temporary]. 
* Per altre informazioni sulle procedure consigliate, vedere [Procedure consigliate per SQL Data Warehouse][SQL Data Warehouse Best Practices].  

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[Identity]: ./sql-data-warehouse-tables-identity.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

[Caricare dati con BCP]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-with-bcp/
[Caricare dati con PolyBase]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-from-azure-blob-storage-with-polybase/
[Procedure consigliate per PolyBase]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-polybase-guide/


<!--MSDN references-->
[Identity property]: https://msdn.microsoft.com/library/ms186775.aspx
[sys.identity_columns]: https://msdn.microsoft.com/library/ms187334.aspx
[IDENTITY()]: https://msdn.microsoft.com/library/ms189838.aspx
[@@IDENTITY]: https://msdn.microsoft.com/library/ms187342.aspx
[SCOPE_IDENTITY]: https://msdn.microsoft.com/library/ms190315.aspx
[IDENT_CURRENT]: https://msdn.microsoft.com/library/ms175098.aspx
[IDENT_INCR]: https://msdn.microsoft.com/library/ms189795.aspx
[IDENT_SEED]: https://msdn.microsoft.com/library/ms189834.aspx
[DBCC CHECK_IDENT()]: https://msdn.microsoft.com/library/ms176057.aspx

[bcp in MSDN]: https://msdn.microsoft.com/library/ms162802.aspx
  

<!--Other Web references-->  
