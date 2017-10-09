---
title: OLTP in memoria di aaaIn migliora le prestazioni SQL txn | Documenti Microsoft
description: OLTP In memoria adottino tooimprove transazionale delle prestazioni in un database SQL esistente.
services: sql-database
documentationcenter: 
author: jodebrui
manager: jhubbard
editor: MightyPen
ms.assetid: c2bf14a0-905b-47b4-afb6-efe9a61147d5
ms.service: sql-database
ms.custom: develop databases
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/22/2016
ms.author: jodebrui
ms.openlocfilehash: 1bed796069565eb6741953837cf0477c2ddd8519
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-in-memory-oltp-tooimprove-your-application-performance-in-sql-database"></a>OLTP In memoria utilizzare tooimprove le prestazioni dell'applicazione nel Database SQL
[OLTP in memoria](sql-database-in-memory.md) può essere utilizzato tooimprove hello prestazioni di elaborazione delle transazioni, inserimento di dati e gli scenari di dati temporanei, in [Premium](sql-database-service-tiers.md) database SQL di Azure senza aumentare hello piano tariffario. 

> [!NOTE] 
> Informazioni in [Quorum doubles key database's workload while lowering DTU by 70% with SQL Database](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database) (Il quorum raddoppia il carico di lavoro del database principale riducendo il DTU del 70% con il database SQL)


Seguire questi passaggi tooadopt OLTP In memoria, nel database esistente.

## <a name="step-1-ensure-you-are-using-a-premium-database"></a>Passaggio 1: assicurarsi di usare un database Premium
OLTP in memoria è supportato solo nei database Premium. In memoria è supportata se hello ha restituito il risultato è 1 (non 0):

```
SELECT DatabasePropertyEx(Db_Name(), 'IsXTPSupported');
```

*XTP* è l'acronimo di *Extreme Transaction Processing*



## <a name="step-2-identify-objects-toomigrate-tooin-memory-oltp"></a>Passaggio 2: Identificare gli oggetti toomigrate tooIn memoria OLTP
SSMS include un report **Panoramica analisi delle prestazioni per le transazioni** che è possibile eseguire su un database con un carico di lavoro attivo. report di Hello identifica le tabelle e stored procedure candidate per la migrazione OLTP in memoria di tooIn.

In SSMS, report hello toogenerate:

* In hello **Esplora oggetti**, fare doppio clic sul nodo del database.
* Fare clic su **Report** > **Report standard** > **Panoramica dell'analisi delle prestazioni transazioni**.

Per ulteriori informazioni, vedere [determinare se una tabella o una Stored Procedure deve essere trasferita OLTP in memoria di tooIn](http://msdn.microsoft.com/library/dn205133.aspx).

## <a name="step-3-create-a-comparable-test-database"></a>Passaggio 3: Creare un database di prova confrontabile
Si supponga che il report hello indica il database è una tabella che può costituire un vantaggio viene convertita tooa nella tabella con ottimizzazione per la memoria. È consigliabile testare indicazione hello tooconfirm eseguendo i test.

È necessaria una copia di test del database di produzione. Hello database di test deve essere in hello stesso servizio livello del database di produzione.

tooease test, modificare il database di test come segue:

1. Connettersi toohello test database tramite SQL Server Management Studio.
2. tooavoid necessità hello opzione WITH (SNAPSHOT) nelle query, impostare l'opzione di database hello come illustrato nella seguente istruzione T-SQL hello:
   
   ```
   ALTER DATABASE CURRENT
    SET
        MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = ON;
   ```

## <a name="step-4-migrate-tables"></a>Passaggio 4: Eseguire la migrazione delle tabelle
È necessario creare e popolare una copia con ottimizzazione per la memoria della tabella hello desiderato tootest. È possibile crearla usando:

* Hello utile memoria Ottimizzazione guidata in SQL Server Management Studio.
* T-SQL manuale.

#### <a name="memory-optimization-wizard-in-ssms"></a>Ottimizzazione guidata per la memoria di SSMS
toouse questa opzione di migrazione:

1. Connettere il database di prova toohello con SQL Server Management Studio.
2. In hello **Esplora oggetti**, fare clic su tabella hello e quindi fare clic su **Memory Optimization Advisor**.
   
   * Hello **tabella memoria Query Optimizer Advisor** procedura guidata viene visualizzata.
3. Nella procedura guidata hello, fare clic su **convalida migrazione** (o hello **Avanti** pulsante) toosee se la tabella hello contiene funzionalità non supportate che non sono supportate nelle tabelle con ottimizzazione per la memoria. Per altre informazioni, vedere:
   
   * Hello *checklist Ottimizzazione memoria* in [Memory Optimization Advisor](http://msdn.microsoft.com/library/dn284308.aspx).
   * [Costrutti transact-SQL non supportati da OLTP in memoria](http://msdn.microsoft.com/library/dn246937.aspx).
   * [Migrazione OLTP in memoria di tooIn](http://msdn.microsoft.com/library/dn247639.aspx).
4. Se la tabella hello non dispone di funzionalità supportate, advisor hello eseguibili schema effettivo hello e la migrazione dei dati per l'utente.

#### <a name="manual-t-sql"></a>T-SQL manuale
toouse questa opzione di migrazione:

1. Connettersi tooyour test database tramite SQL Server Management Studio (o un'utilità analoga).
2. Ottenere script T-SQL completo hello per la tabella e i relativi indici.
   
   * In SSMS fare clic con il pulsante destro del mouse sul nodo della tabella.
   * Fare clic su **Crea script per tabella** > **CREATE in** > **Nuova finestra Query**.
3. Nella finestra di script hello, aggiungere WITH (MEMORY_OPTIMIZED = ON) toohello istruzione CREATE TABLE.
4. Se è presente un indice cluster, modificare tooNONCLUSTERED.
5. Rinominare la tabella esistente hello tramite SP_RENAME.
6. Creare hello con ottimizzazione per la memoria copia della tabella hello eseguendo lo script CREATE TABLE modificato.
7. Copia una tabella con ottimizzazione per la memoria di hello dati tooyour utilizzando l'istruzione INSERT... SELEZIONARE * IN:

```
INSERT INTO <new_memory_optimized_table>
        SELECT * FROM <old_disk_based_table>;
```


## <a name="step-5-optional-migrate-stored-procedures"></a>Passaggio 5 (facoltativo): Eseguire la migrazione di stored procedure
funzionalità In memoria Hello è inoltre possibile modificare una stored procedure per migliorare le prestazioni.

### <a name="considerations-with-natively-compiled-stored-procedures"></a>Considerazioni sulle stored procedure compilate in modo nativo
Una stored procedure compilata in modo nativo deve avere hello nella relativa clausola T-SQL con le opzioni seguenti:

* NATIVE_COMPILATION
* SCHEMABINDING: tabelle significato hello stored procedure non possono contenere definizioni di colonna modificate in alcun modo che hanno effetto sulla procedura hello archiviato, a meno che non si rilascia di hello stored procedure.

Un modulo nativo deve usare [blocchi ATOMICI](http://msdn.microsoft.com/library/dn452281.aspx) di grandi dimensioni per la gestione delle transazioni. Non esiste un ruolo per un'istruzione BEGIN TRANSACTION o ROLLBACK TRANSACTION esplicita. Se viene rilevata una violazione di una regola business, è possibile terminare il blocco atomico hello con un [generare](http://msdn.microsoft.com/library/ee677615.aspx) istruzione.

### <a name="typical-create-procedure-for-natively-compiled"></a>CREATE PROCEDURE tipica per le stored procedure compilate in modo nativo
In genere hello T-SQL toocreate una stored procedure compilata in modo nativo è simile toohello seguente modello:

```
CREATE PROCEDURE schemaname.procedurename
    @param1 type1, …
    WITH NATIVE_COMPILATION, SCHEMABINDING
    AS
        BEGIN ATOMIC WITH
            (TRANSACTION ISOLATION LEVEL = SNAPSHOT,
            LANGUAGE = N'your_language__see_sys.languages'
            )
        …
        END;
```

* Per hello TRANSACTION_ISOLATION_LEVEL, SNAPSHOT è di hello più comuni valore per hello compilata in modo nativo stored procedura. Tuttavia, un subset di hello altri valori sono inoltre supportati:
  
  * REPEATABLE READ
  * SERIALIZABLE
* Hello valore lingua deve essere presente nella visualizzazione sys.languages hello.

### <a name="how-toomigrate-a-stored-procedure"></a>Come toomigrate una stored procedure
i passaggi della migrazione Hello sono:

1. Ottenere hello CREATE PROCEDURE script toohello stored procedure interpretata regolarmente.
2. Riscrivere il relativo modello di intestazione toomatch hello precedente.
3. Verificare se la procedura hello archiviato codice T-SQL utilizza le caratteristiche che non sono supportate per le stored procedure compilate in modo nativo. Se necessario, implementare le soluzioni alternative.
   
   * Per altre informazioni vedere [Problemi di migrazione relativi alle stored procedure compilate in modo nativo](http://msdn.microsoft.com/library/dn296678.aspx).
4. Rinominare una stored procedure precedente hello tramite SP_RENAME. In alternativa usare semplicemente DROP.
5. Eseguire lo script CREATE PROCEDURE T-SQL modificato.

## <a name="step-6-run-your-workload-in-test"></a>Passaggio 6: Eseguire il carico di lavoro nel test
Eseguire un carico di lavoro nel database di test di carico di lavoro toohello simile che viene eseguito nel database di produzione. Si rivelano miglioramento delle prestazioni hello ottenuto per l'utilizzo della funzionalità In memoria hello per le tabelle e stored procedure.

Gli attributi principali di carico di lavoro hello sono:

* Numero di connessioni simultanee.
* Rapporto di lettura/scrittura.

tootailor e carico di lavoro di hello esecuzione dei test, è consigliabile usare uno strumento utile ostress.exe hello che illustrate nella [qui](sql-database-in-memory.md).

latenza di rete toominimize, eseguire il test in hello stessa area geografica Azure in cui è presente il database di hello.

## <a name="step-7-post-implementation-monitoring"></a>Passaggio 7: Monitoraggio post-implementazione
Si consideri il monitoraggio di effetti sulle prestazioni di hello delle implementazioni In memoria nell'ambiente di produzione:

* [Monitorare l'archiviazione in memoria](sql-database-in-memory-oltp-monitoring.md).
* [Monitoraggio del database SQL di Azure tramite le visualizzazioni di gestione dinamica](sql-database-monitoring-with-dmvs.md)

## <a name="related-links"></a>Collegamenti correlati
* [OLTP in memoria (ottimizzazione in memoria)](http://msdn.microsoft.com/library/dn133186.aspx)
* [Introduzione tooNatively Compiled Stored Procedures](http://msdn.microsoft.com/library/dn133184.aspx)
* [Ottimizzazione guidata per la memoria](http://msdn.microsoft.com/library/dn284308.aspx)

