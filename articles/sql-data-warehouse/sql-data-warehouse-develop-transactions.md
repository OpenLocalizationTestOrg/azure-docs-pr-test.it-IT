---
title: in SQL Data Warehouse aaaTransactions | Documenti Microsoft
description: Suggerimenti per l'implementazione di transazioni in Azure SQL Data Warehouse per lo sviluppo di soluzioni.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: ae621788-e575-41f5-8bfe-fa04dc4b0b53
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 7c541648553238443b407666612561918096eb61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="transactions-in-sql-data-warehouse"></a>Transazioni in SQL Data Warehouse
Come prevedibile, SQL Data Warehouse supporta le transazioni come parte del carico di lavoro di hello data warehouse. Prestazioni di hello tooensure di SQL Data Warehouse vengono comunque mantenute su larga scala, che alcune funzionalità sono limitate quando confrontati tooSQL Server. Questo articolo evidenzia le differenze di hello e gli elenchi di hello ad altri utenti. 

## <a name="transaction-isolation-levels"></a>Livelli di isolamento delle transazioni
SQL Data Warehouse implementa le transazioni ACID. Tuttavia, l'isolamento del supporto transazionale hello hello è limitato troppo`READ UNCOMMITTED` e non può essere modificato. È possibile implementare un numero di metodi di codifica tooprevent dirty legge dei dati se si tratta di un problema per l'utente. Hello metodi più diffusi sfruttano un'istruzione CTAS e cambio della partizione nella tabella (spesso noto come modello di finestra temporale scorrevole hello) tooprevent agli utenti di eseguire query sui dati che è ancora in corso di preparazione. Visualizzazioni dati pre-filtro hello sono anche un approccio comune.  

## <a name="transaction-size"></a>Dimensioni delle transazioni
Le dimensioni di una singola transazione di modifica dati sono limitate. oggi viene applicato il limite di Hello "per ogni distribuzione". Pertanto, l'allocazione totale hello può essere calcolato moltiplicando il limite di hello per il conteggio di distribuzione hello. numero massimo di hello tooapproximate di righe nella transazione hello divide perno distribuzione hello per dimensioni totali di hello di ogni riga. Per prendere in considerazione le colonne a lunghezza variabile richiede una lunghezza di colonna medio anziché la dimensione massima di hello.

Nella tabella hello seguito hello seguenti presupposti:

* Si è verificata una distribuzione uniforme dei dati 
* lunghezza media della riga Hello è 250 byte

| [DWU][DWU] | Limite per ogni distribuzione (GiB) | Numero di distribuzioni | Dimensioni MAX delle transazioni (GiB) | # Righe per la distribuzione | Righe max per transazione |
| --- | --- | --- | --- | --- | --- |
| DW100 |1 |60 |60 |4.000.000 |240.000.000 |
| DW200 |1,5 |60 |90 |6.000.000 |360.000.000 |
| DW300 |2.25 |60 |135 |9.000.000 |540.000.000 |
| DW400 |3 |60 |180 |12.000.000 |720.000.000 |
| DW500 |3,75 |60 |225 |15.000.000 |900.000.000 |
| DW600 |4.5 |60 |270 |18.000.000 |1.080.000.000 |
| DW1000 |7.5 |60 |450 |30.000.000 |1.800.000.000 |
| DW1200 |9 |60 |540 |36.000.000 |2.160.000.000 |
| DW1500 |11,25 |60 |675 |45.000.000 |2.700.000.000 |
| DW2000 |15 |60 |900 |60.000.000 |3.600.000.000 |
| DW3000 |22,5 |60 |1.350 |90.000.000 |5.400.000.000 |
| DW6000 |45 |60 |2.700 |180.000.000 |10.800.000.000 |

limite delle dimensioni delle transazioni Hello viene applicato per ogni transazione o operazione. Non viene applicato in tutte le transazioni simultanee. Pertanto ogni transazione è consentito toowrite questa quantità di dati toohello log. 

toooptimize e ridurre al minimo la quantità hello dei dati scritti toohello log, vedere toohello [procedure consigliate per le transazioni] [ Transactions best practices] articolo.

> [!WARNING]
> massima dimensione delle transazioni può essere ottenuta solo HASH o tabelle ROUND_ROBIN distribuiti in cui di diffondersi hello hello dati Hello è pari. Se la transazione hello scrive i dati in modo asimmetrici toohello distribuzioni quindi hello limite è probabilmente toobe raggiunto dimensioni di transazione massimo toohello precedente.
> <!--REPLICATED_TABLE-->
> 
> 

## <a name="transaction-state"></a>Stato della transazione
SQL Data Warehouse utilizza hello xact_state funzione tooreport una transazione non riuscita con il valore di hello -2. Ciò significa che la transazione hello non è riuscita ed è contrassegnata per il rollback solo

> [!NOTE]
> Hello utilizzare-2 hello XACT_STATE funzione toodenote un tooSQL di un comportamento diverso rappresenta Server transazione non riuscita. SQL Server utilizza hello valore -1 toorepresent una transazione non eseguire il commit. SQL Server è in grado di tollerare errori all'interno di una transazione senza che questo disponga toobe contrassegnato come non eseguire il commit. Ad esempio, `SELECT 1/0` causa un errore, ma non applica alla transazione lo stato per cui non è possibile eseguire il commit. SQL Server consente inoltre di operazioni di lettura nella transazione non eseguire il commit di hello. SQL Data Warehouse, invece, non consente questa operazione. Se si verifica un errore in una transazione SQL Data Warehouse passerà automaticamente allo stato hello -2 e non sarà in grado di toomake eventuali altre istruzioni select fino a quando non è stato eseguito il rollback dell'istruzione hello. È pertanto importante toocheck che il codice di applicazione toosee se utilizza xact_state come si potrebbe essere necessario toomake modifiche del codice.
> 
> 

Ad esempio, in SQL Server potrebbe essere visualizzata una transazione simile alla seguente:

```sql
SET NOCOUNT ON;
DECLARE @xact_state smallint = 0;

BEGIN TRAN
    BEGIN TRY
        DECLARE @i INT;
        SET     @i = CONVERT(INT,'ABC');
    END TRY
    BEGIN CATCH
        SET @xact_state = XACT_STATE();

        SELECT  ERROR_NUMBER()    AS ErrNumber
        ,       ERROR_SEVERITY()  AS ErrSeverity
        ,       ERROR_STATE()     AS ErrState
        ,       ERROR_PROCEDURE() AS ErrProcedure
        ,       ERROR_MESSAGE()   AS ErrMessage
        ;

        IF @@TRANCOUNT > 0
        BEGIN
            PRINT 'ROLLBACK';
            ROLLBACK TRAN;
        END

    END CATCH;

IF @@TRANCOUNT >0
BEGIN
    PRINT 'COMMIT';
    COMMIT TRAN;
END

SELECT @xact_state AS TransactionState;
```

Se si lascia il codice perché è di sopra verrà visualizzato hello seguente messaggio di errore:

Messaggio 111233, livello 16, stato 1, riga 1 111233; hello corrente transazione è stata interrotta e le modifiche in sospeso sottoposta a rollback. Causa: non è stato eseguito il rollback in modo esplicito di una transazione in uno stato di solo rollback prima di un'istruzione DDL, DML o SELECT.

Potranno inoltre ottenere output di hello di errore. il * funzioni hello non.

In SQL Data Warehouse codice hello deve toobe leggermente modificato:

```sql
SET NOCOUNT ON;
DECLARE @xact_state smallint = 0;

BEGIN TRAN
    BEGIN TRY
        DECLARE @i INT;
        SET     @i = CONVERT(INT,'ABC');
    END TRY
    BEGIN CATCH
        SET @xact_state = XACT_STATE();

        IF @@TRANCOUNT > 0
        BEGIN
            PRINT 'ROLLBACK';
            ROLLBACK TRAN;
        END

        SELECT  ERROR_NUMBER()    AS ErrNumber
        ,       ERROR_SEVERITY()  AS ErrSeverity
        ,       ERROR_STATE()     AS ErrState
        ,       ERROR_PROCEDURE() AS ErrProcedure
        ,       ERROR_MESSAGE()   AS ErrMessage
        ;
    END CATCH;

IF @@TRANCOUNT >0
BEGIN
    PRINT 'COMMIT';
    COMMIT TRAN;
END

SELECT @xact_state AS TransactionState;
```

Hello previsto ora venga rispettato il comportamento. Errore Hello in transazione hello è gestito ed errore. il * funzioni hello forniscono i valori come previsto.

Tutto ciò che è stata modificata è che hello `ROLLBACK` di hello transazione era toohappen prima hello lettura delle informazioni di errore hello in hello `CATCH` blocco.

## <a name="errorline-function"></a>Funzione Error_Line()
È inoltre importante notare che SQL Data Warehouse non è in implementare o funzione di hello error_line (). Se hai nel codice, è necessario tooremove è toobe conforme a SQL Data Warehouse. Utilizzare le etichette di query nel codice tooimplement una funzionalità equivalente. Consultare toohello [etichetta] [ LABEL] articolo per ulteriori informazioni su questa funzionalità.

## <a name="using-throw-and-raiserror"></a>Uso di THROW e RAISERROR
THROW è hello più moderno implementazione per la generazione di eccezioni in SQL Data Warehouse ma è supportato anche RAISERROR. Esistono alcune differenze che vale la pena prestando attenzione toohowever.

* I numeri non possono essere hello 100.000 a 150.000 intervallo per la generazione di messaggi di errore definiti dall'utente
* I messaggi di errore di RAISERROR sono fissati a 50.000.
* L'uso di sys.messages non è supportato.

## <a name="limitiations"></a>Limitazioni
SQL Data Warehouse sono poche altre restrizioni relativi tootransactions.

Ecco quali sono:

* Nessuna transazione distribuita
* Non sono consentite transazioni annidate
* Non sono consentiti punti di salvataggio
* Nessuna transazione denominata
* Nessuna transazione contrassegnata
* Nessun supporto per DDL come `CREATE TABLE` all'interno di una transazione definita dall'utente

## <a name="next-steps"></a>Passaggi successivi
toolearn più sull'ottimizzazione delle transazioni, vedere [procedure consigliate per le transazioni][Transactions best practices].  toolearn su altre procedure consigliate di SQL Data Warehouse, vedere [le procedure consigliate di SQL Data Warehouse][SQL Data Warehouse best practices].

<!--Image references-->

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Transactions best practices]: ./sql-data-warehouse-develop-best-practices-transactions.md
[SQL Data Warehouse best practices]: ./sql-data-warehouse-best-practices.md
[LABEL]: ./sql-data-warehouse-develop-label.md

<!--MSDN references-->

<!--Other Web references-->
