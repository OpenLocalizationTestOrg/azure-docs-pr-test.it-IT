---
title: OLTP in memoria migliora le prestazioni delle transazioni SQL | Documentazione Microsoft
description: Adottare OLTP in memoria per migliorare le prestazioni transazionali in un database SQL esistente.
services: sql-database
documentationcenter: 
author: jodebrui
manager: jhubbard
editor: MightyPen
ms.assetid: c2bf14a0-905b-47b4-afb6-efe9a61147d5
ms.service: sql-database
ms.custom: develop databases
ms.workload: Inactive
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/22/2016
ms.author: jodebrui
ms.openlocfilehash: 71dd7d36eee210b80ed6a791b52f977a416b6bb7
ms.sourcegitcommit: e5355615d11d69fc8d3101ca97067b3ebb3a45ef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/31/2017
---
# <a name="use-in-memory-oltp-to-improve-your-application-performance-in-sql-database"></a>Uso di OLTP in memoria per migliorare le prestazioni delle applicazioni nel database SQL
[OLTP in memoria](sql-database-in-memory.md) può essere usato per migliorare le prestazioni di elaborazione delle transazioni, l'inserimento dei dati e gli scenari di dati temporanei, nei database SQL di Azure [Premium](sql-database-service-tiers.md), senza aumentare il piano tariffario. 

> [!NOTE] 
> Informazioni in [Quorum doubles key database's workload while lowering DTU by 70% with SQL Database](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database) (Il quorum raddoppia il carico di lavoro del database principale riducendo il DTU del 70% con il database SQL)


Seguire i passaggi seguenti per adottare OLTP in memoria nel database esistente.

## <a name="step-1-ensure-you-are-using-a-premium-database"></a>Passaggio 1: assicurarsi di usare un database Premium
OLTP in memoria è supportato solo nei database Premium. La funzionalità in memoria è supportata se il risultato restituito è 1 (non 0):

```
SELECT DatabasePropertyEx(Db_Name(), 'IsXTPSupported');
```

*XTP* è l'acronimo di *Extreme Transaction Processing*



## <a name="step-2-identify-objects-to-migrate-to-in-memory-oltp"></a>Passaggio 2: Identificare gli oggetti per eseguire la migrazione a OLTP In memoria
SSMS include un report **Panoramica analisi delle prestazioni per le transazioni** che è possibile eseguire su un database con un carico di lavoro attivo. Il report identifica le tabelle e le stored procedure candidate per la migrazione a OLTP in memoria.

In SSMS, per generare il report:

* In **Esplora oggetti**fare clic con il pulsante destro del mouse sul nodo del database.
* Fare clic su **Report** > **Report standard** > **Panoramica dell'analisi delle prestazioni transazioni**.

Per altre informazioni, vedere [Determinare se una tabella o una stored procedure deve essere trasferita a OLTP in memoria](http://msdn.microsoft.com/library/dn205133.aspx).

## <a name="step-3-create-a-comparable-test-database"></a>Passaggio 3: Creare un database di prova confrontabile
Si supponga che il report indichi che il database include una tabella che può trarre vantaggio dalla conversione in una tabella con ottimizzazione per la memoria. È consigliabile verificare prima di tutto l'indicazione eseguendo il test.

È necessaria una copia di test del database di produzione. Il database di test deve avere lo stesso livello di servizio del database di produzione.

Per semplificare il test, perfezionare il database di test come segue:

1. Connettersi al database di test usando SSMS.
2. Per evitare di dover usare l'opzione WITH (SNAPSHOT) nelle query, impostare l'opzione di database come illustrato nell'istruzione T-SQL seguente:
   
   ```
   ALTER DATABASE CURRENT
    SET
        MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = ON;
   ```

## <a name="step-4-migrate-tables"></a>Passaggio 4: Eseguire la migrazione delle tabelle
È necessario creare e popolare una copia con ottimizzazione per la memoria della tabella che si vuole testare. È possibile crearla usando:

* La pratica Ottimizzazione guidata per la memoria di SSMS.
* T-SQL manuale.

#### <a name="memory-optimization-wizard-in-ssms"></a>Ottimizzazione guidata per la memoria di SSMS
Per usare questa opzione di migrazione:

1. Connettersi al database di test con SSMS.
2. In **Esplora oggetti** fare clic con il pulsante destro del mouse sulla tabella e quindi fare clic su **Ottimizzazione guidata per la memoria**.
   
   * Verrà visualizzata l' **Ottimizzazione guidata per la memoria della tabella** .
3. Nella procedura guidata fare clic su **Convalida della migrazione** o sul pulsante **Avanti** per verificare se la tabella include eventuali funzionalità non supportate nelle tabelle con ottimizzazione per la memoria. Per altre informazioni, vedere:
   
   * *Elenco di controllo relativo all'ottimizzazione per la memoria* in [Ottimizzazione guidata per la memoria](http://msdn.microsoft.com/library/dn284308.aspx).
   * [Costrutti transact-SQL non supportati da OLTP in memoria](http://msdn.microsoft.com/library/dn246937.aspx).
   * [Migrazione a OLTP in memoria](http://msdn.microsoft.com/library/dn247639.aspx).
4. Se la tabella non include funzionalità non supportate, la procedura guidata può eseguire automaticamente la migrazione effettiva dello schema e dei dati.

#### <a name="manual-t-sql"></a>T-SQL manuale
Per usare questa opzione di migrazione:

1. Connettersi al database di test tramite SSMS o un'utilità analoga.
2. Ottenere lo script T-SQL completo per la tabella e i relativi indici.
   
   * In SSMS fare clic con il pulsante destro del mouse sul nodo della tabella.
   * Fare clic su **Crea script per tabella** > **CREATE in** > **Nuova finestra Query**.
3. Nella finestra dello script aggiungere WITH (MEMORY_OPTIMIZED = ON) all'istruzione CREATE TABLE.
4. Se esiste un indice CLUSTERED, modificarlo in NONCLUSTERED.
5. Rinominare la tabella esistente in SP_RENAME.
6. Creare la nuova copia della tabella con ottimizzazione per la memoria eseguendo lo script modificato CREATE TABLE.
7. Copiare i dati nella tabella con ottimizzazione per la memoria usando l'istruzione INSERT...SELECT * INTO:

```
INSERT INTO <new_memory_optimized_table>
        SELECT * FROM <old_disk_based_table>;
```


## <a name="step-5-optional-migrate-stored-procedures"></a>Passaggio 5 (facoltativo): Eseguire la migrazione di stored procedure
La funzionalità in memoria può anche modificare una stored procedure per migliorare le prestazioni.

### <a name="considerations-with-natively-compiled-stored-procedures"></a>Considerazioni sulle stored procedure compilate in modo nativo
Una stored procedure compilata in modo nativo deve avere le opzioni seguenti nella relativa clausola WITH T-SQL:

* NATIVE_COMPILATION
* SCHEMABINDING: indica le tabelle in cui la stored procedure non può modificare le definizioni di colonna in alcun modo che abbia effetto sulla stored procedure, a meno che non si rimuova la stored procedure.

Un modulo nativo deve usare [blocchi ATOMICI](http://msdn.microsoft.com/library/dn452281.aspx) di grandi dimensioni per la gestione delle transazioni. Non esiste un ruolo per un'istruzione BEGIN TRANSACTION o ROLLBACK TRANSACTION esplicita. Se il codice rileva una violazione di una regola business, è possibile che il blocco atomico venga terminato con un'istruzione [THROW](http://msdn.microsoft.com/library/ee677615.aspx) .

### <a name="typical-create-procedure-for-natively-compiled"></a>CREATE PROCEDURE tipica per le stored procedure compilate in modo nativo
In genere l'istruzione T-SQL per creare una stored procedure compilata in modo nativo è simile al modello seguente:

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

* Per TRANSACTION_ISOLATION_LEVEL, SNAPSHOT è il valore più comune per la stored procedure compilata in modo nativo. Tuttavia, è supportato anche un subset degli altri valori:
  
  * REPEATABLE READ
  * SERIALIZABLE
* Il valore LANGUAGE deve essere presente nella vista sys.languages.

### <a name="how-to-migrate-a-stored-procedure"></a>Come eseguire la migrazione di una stored procedure
Passaggi della migrazione:

1. Ottenere lo script CREATE PROCEDURE per la stored procedure interpretata regolare.
2. Riscrivere l'intestazione in modo che corrisponda al modello precedente.
3. Verificare se il codice T-SQL della stored procedure usa funzionalità non supportate per le stored procedure compilate in modo nativo. Se necessario, implementare le soluzioni alternative.
   
   * Per altre informazioni vedere [Problemi di migrazione relativi alle stored procedure compilate in modo nativo](http://msdn.microsoft.com/library/dn296678.aspx).
4. Rinominare la stored procedure precedente tramite SP_RENAME. In alternativa usare semplicemente DROP.
5. Eseguire lo script CREATE PROCEDURE T-SQL modificato.

## <a name="step-6-run-your-workload-in-test"></a>Passaggio 6: Eseguire il carico di lavoro nel test
Eseguire un carico di lavoro nel database di test simile al carico di lavoro eseguito nel database di produzione. Dovrebbe indicare il miglioramento delle prestazioni ottenuto con l'uso della funzionalità in memoria per tabelle e stored procedure.

Gli attributi principali del carico di lavoro sono i seguenti:

* Numero di connessioni simultanee.
* Rapporto di lettura/scrittura.

Per personalizzare ed eseguire il carico di lavoro di test, si consiglia di usare il pratico strumento ostress.exe, illustrato [qui](sql-database-in-memory.md).

Per ridurre al minimo la latenza di rete, eseguire il test nella stessa area geografica di Azure in cui è disponibile il database.

## <a name="step-7-post-implementation-monitoring"></a>Passaggio 7: Monitoraggio post-implementazione
Tenere sotto controllo gli effetti sulle prestazioni delle implementazioni in memoria nell'ambiente di produzione:

* [Monitorare l'archiviazione in memoria](sql-database-in-memory-oltp-monitoring.md).
* [Monitoraggio del database SQL di Azure tramite le visualizzazioni di gestione dinamica](sql-database-monitoring-with-dmvs.md)

## <a name="related-links"></a>Collegamenti correlati
* [OLTP in memoria (ottimizzazione in memoria)](http://msdn.microsoft.com/library/dn133186.aspx)
* [Stored procedure compilate in modo nativo](http://msdn.microsoft.com/library/dn133184.aspx)
* [Ottimizzazione guidata per la memoria](http://msdn.microsoft.com/library/dn284308.aspx)

