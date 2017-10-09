---
title: gestione aaaConcurrency e carico di lavoro in SQL Data Warehouse | Documenti Microsoft
description: Informazioni sulla gestione della concorrenza e del carico di lavoro nel Data Warehouse di SQL Azure per lo sviluppo di soluzioni.
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: ef170f39-ae24-4b04-af76-53bb4c4d16d3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 08/23/2017
ms.author: joeyong;barbkess;kavithaj
ms.openlocfilehash: 7f7e77aa687760252aed16573b609817ed9111c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="concurrency-and-workload-management-in-sql-data-warehouse"></a>Gestione della concorrenza e del carico di lavoro in SQL Data Warehouse
toodeliver prestazioni prevedibili su larga scala, Microsoft Azure SQL Data Warehouse consentono di controllare i livelli di concorrenza e allocazioni di risorse come la memoria e assegnazione di priorità di CPU. Questo articolo illustra i concetti di toohello della gestione della concorrenza e carico di lavoro, che spiega come entrambe le funzionalità sono state implementate e come sia possibile controllare in data warehouse. La gestione del carico di lavoro di SQL Data Warehouse è toohelp previsto è supportare ambienti con più utenti. Non è concepita per i carichi di lavoro multi-tenant.

## <a name="concurrency-limits"></a>Limiti di concorrenza
SQL Data Warehouse consente di too1, 024 connessioni simultanee. Tutte le 1.024 connessioni possono inviare query contemporaneamente. Tuttavia, toooptimize una velocità effettiva, SQL Data Warehouse può accodare tooensure alcune query che una concessione di memoria minima assegnata a ogni query. L'accodamento avviene in fase di esecuzione della query. Dalle query di accodamento dei messaggi quando vengono raggiunti i limiti, concorrenza SQL Data Warehouse è possibile aumentare velocità effettiva totale per garantire che query attive toocritically di accesso necessarie risorse di memoria.  

I limiti di concorrenza sono regolati da due concetti, *query simultanee* e *slot di concorrenza*. Per tooexecute una query, deve essere eseguito entro il limite di concorrenza delle query hello sia allocazione slot di concorrenza hello.

* Le query simultanee sono query hello in esecuzione in hello stesso tempo. SQL Data Warehouse supporta le query simultanee di too32 su dimensioni maggiori del numero di DWU hello.
* In base alle Unità Data Warehouse (DWU), vengono allocati slot di concorrenza. Ogni 100 DWU, vengono forniti 4 slot di concorrenza. Ad esempio, per DW100 vengono allocati 4 slot di concorrenza e per DW1000 ne vengono allocati 40. Ogni query utilizza uno o più concorrenza slot, dipende hello [classe di risorse](#resource-classes) di query hello. Query in esecuzione in una classe di risorse smallrc hello utilizzano uno slot di concorrenza. Le query in esecuzione in una classe di risorse superiore usano più slot di concorrenza.

Hello nella tabella seguente descrive i limiti di hello per le query simultanee e slot di concorrenza in hello diverse dimensioni DWU.

### <a name="concurrency-limits"></a>Limiti di concorrenza
| DWU | Numero massimo di query simultanee | Numero di slot di concorrenza allocati |
|:--- |:---:|:---:|
| DW100 |4 |4 |
| DW200 |8 |8 |
| DW300 |12 |12 |
| DW400 |16 |16 |
| DW500 |20 |20 |
| DW600 |24 |24 |
| DW1000 |32 |40 |
| DW1200 |32 |48 |
| DW1500 |32 |60 |
| DW2000 |32 |80 |
| DW3000 |32 |120 |
| DW6000 |32 |240 |

Quando viene raggiunta una di queste soglie, le nuove query vengono accodate e vengono eseguite in base al principio FIFO (First-In-First-Out).  Come al termine di una query e hello query e slot scende di sotto dei limiti di hello, vengono rilasciate le query in coda. 

> [!NOTE]  
> *Selezionare* query esecuzione esclusivamente su viste a gestione dinamica (DMV) o viste del catalogo non dipendono da uno qualsiasi dei limiti di concorrenza hello. È possibile monitorare il sistema hello indipendentemente dal numero di hello di query in esecuzione su di esso.
> 
> 

## <a name="resource-classes"></a>Classi di risorse
Risorsa classi consente di controllare l'allocazione della memoria e cicli di CPU tooa query specificati. È possibile assegnare due tipi di risorsa classi tooa utente nel formato hello dei ruoli predefiniti del database. Hello due tipi di classi di risorse sono i seguenti:
1. Classi di risorse dinamiche (**smallrc, mediumrc, largerc, xlargerc**) allocare una quantità di memoria a seconda di hello variabile DWU corrente. Ciò significa che quando si aumenta il backup tooa DWU più grandi, le query ottengono automaticamente maggiore quantità di memoria. 
2. Le classi di risorse statiche (**staticrc10, staticrc20, staticrc30, staticrc40, staticrc50, staticrc60, staticrc70, staticrc80**) allocare hello stessa quantità di memoria indipendentemente dal valore hello DWU corrente (purché hello DWU stesso disponga di sufficiente memoria). Ciò significa che nelle DWU più grandi è possibile eseguire più query in ogni classe di risorse contemporaneamente.

Agli utenti delle classi **smallrc** e **staticrc10** viene assegnata una quantità di memoria più piccola e ciò permette di sfruttare una concorrenza maggiore. Al contrario, gli utenti assegnati troppo**xlargerc** o **staticrc80** figurano grandi quantità di memoria, e pertanto meno le query possono essere eseguiti contemporaneamente.

Per impostazione predefinita, ogni utente è un membro di classe di risorse ridotto hello, **smallrc**. Hello procedure `sp_addrolemember` è utilizzata una classe di risorse tooincrease hello e `sp_droprolemember` viene utilizzata una classe di risorse toodecrease hello. Ad esempio, questo comando potrebbe aumentare la classe di risorse hello di loaduser troppo**largerc**:

```sql
EXEC sp_addrolemember 'largerc', 'loaduser'
```


### <a name="queries-that-do-not-honor-resource-classes"></a>Query che non rispettano le classi di risorse

Esistono alcuni tipi di query che non traggono vantaggio da un'allocazione di memoria maggiore. sistema Hello ignora l'allocazione di classe di risorse e sempre esecuzione queste query nella classe di risorse ridotto hello invece. Se tali query vengono eseguite sempre nella classe di risorse ridotto hello, essi possono verificarsi quando gli slot di concorrenza sono sotto pressione e non utilizzano più slot quelle necessarie. Vedere [Eccezioni della classe di risorse](#query-exceptions-to-concurrency-limits) per ulteriori informazioni.

## <a name="details-on-resource-class-assignment"></a>Dettagli sull'assegnazione della classe di risorse


Altri dettagli sulla classe di risorse:

* *Modificare ruolo* è necessaria l'autorizzazione classe di risorse toochange hello di un utente.
* Sebbene sia possibile aggiungere un utente tooone o più classi di risorse superiore hello, classi di risorse dinamiche hanno la precedenza sulle classi di risorse statiche. Ovvero, se un utente è assegnato tooboth **mediumrc**(dinamico) e **staticrc80**(statico), **mediumrc** è una classe di risorse hello che viene rispettato.
 * Quando un utente viene assegnato toomore classe di una risorsa in un tipo di classe di risorse (più di una classe di risorse dinamiche o più di una classe di risorse statiche), classe di risorse massimo hello viene rispettata. Ovvero, se un utente è assegnato largerc e tooboth mediumrc, classe di risorse superiore hello (largerc) viene rispettata. E se un utente è assegnato tooboth **staticrc20** e **statirc80**, **staticrc80** viene tenuto in considerazione.
* Impossibile modificare la classe di risorse Hello di utente amministratore di sistema hello.

Per un esempio dettagliato, vedere [Esempio di modifica della classe di risorse di un utente](#changing-user-resource-class-example).

## <a name="memory-allocation"></a>Allocazione della memoria
Esistono vantaggi e svantaggi tooincreasing classe di risorse dell'utente. Sebbene l'aumento di una classe di risorse per un utente, le query offre memoria toomore di accesso, che può indicare le query eseguite più velocemente.  Tuttavia, le classi di risorse superiore riducono il numero di hello di query simultanee che è possibile eseguire. Si tratta di compromesso hello tra allocare grandi quantità di singola query di memoria tooa o consentire altre query, nonché le allocazioni di memoria, toorun contemporaneamente. Se un utente di elevata allocazioni di memoria per una query, gli altri utenti non potranno toothat accesso stesso memoria toorun una query.

Hello nella tabella seguente viene eseguito il mapping hello memoria distribuzione tooeach dalla classe DWU e risorse.

### <a name="memory-allocations-per-distribution-for-dynamic-resource-classes-mb"></a>Allocazioni di memoria per ogni distribuzione per le classi di risorse dinamiche (MB)
| DWU | smallrc | mediumrc | largerc | xlargerc |
|:--- |:---:|:---:|:---:|:---:|
| DW100 |100 |100 |200 |400 |
| DW200 |100 |200 |400 |800 |
| DW300 |100 |200 |400 |800 |
| DW400 |100 |400 |800 |1.600 |
| DW500 |100 |400 |800 |1.600 |
| DW600 |100 |400 |800 |1.600 |
| DW1000 |100 |800 |1.600 |3.200 |
| DW1200 |100 |800 |1.600 |3.200 |
| DW1500 |100 |800 |1.600 |3.200 |
| DW2000 |100 |1.600 |3.200 |6.400 |
| DW3000 |100 |1.600 |3.200 |6.400 |
| DW6000 |100 |3.200 |6.400 |12.800 |

Hello nella tabella seguente viene eseguito il mapping hello memoria distribuzione tooeach DWU e classe di risorse statiche. Si noti che le classi di risorse superiore hello abbiano la memoria ridotti i limiti DWU toohonor hello globali.

### <a name="memory-allocations-per-distribution-for-static-resource-classes-mb"></a>Allocazioni di memoria per ogni distribuzione per le classi di risorse statiche (MB)
| DWU | staticrc10 | staticrc20 | staticrc30 | staticrc40 | staticrc50 | staticrc60 | staticrc70 | staticrc80 |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DW100 |100 |200 |400 |400 |400 |400 |400 |400 |
| DW200 |100 |200 |400 |800 |800 |800 |800 |800 |
| DW300 |100 |200 |400 |800 |800 |800 |800 |800 |
| DW400 |100 |200 |400 |800 |1.600 |1.600 |1.600 |1.600 |
| DW500 |100 |200 |400 |800 |1.600 |1.600 |1.600 |1.600 |
| DW600 |100 |200 |400 |800 |1.600 |1.600 |1.600 |1.600 |
| DW1000 |100 |200 |400 |800 |1.600 |3.200 |3.200 |3.200 |
| DW1200 |100 |200 |400 |800 |1.600 |3.200 |3.200 |3.200 |
| DW1500 |100 |200 |400 |800 |1.600 |3.200 |3.200 |3.200 |
| DW2000 |100 |200 |400 |800 |1.600 |3.200 |6.400 |6.400 |
| DW3000 |100 |200 |400 |800 |1.600 |3.200 |6.400 |6.400 |
| DW6000 |100 |200 |400 |800 |1.600 |3.200 |6.400 |12.800 |

Da hello nella tabella precedente, è possibile vedere che una query in esecuzione in un DW2000 in hello **xlargerc** classe di risorse avrebbe accesso too6, 400 MB di memoria all'interno di ogni database distribuiti 60 hello.  In SQL Data Warehouse sono presenti 60 distribuzioni. Allocazione di memoria totale hello toocalculate per una query in una classe di risorse specifico, hello sopra i valori, pertanto, deve essere moltiplicata per 60.

### <a name="memory-allocations-system-wide-gb"></a>Allocazioni di memoria a livello di sistema (GB)
| DWU | smallrc | mediumrc | largerc | xlargerc |
|:--- |:---:|:---:|:---:|:---:|
| DW100 |6 |6 |12 |23 |
| DW200 |6 |12 |23 |47 |
| DW300 |6 |12 |23 |47 |
| DW400 |6 |23 |47 |94 |
| DW500 |6 |23 |47 |94 |
| DW600 |6 |23 |47 |94 |
| DW1000 |6 |47 |94 |188 |
| DW1200 |6 |47 |94 |188 |
| DW1500 |6 |47 |94 |188 |
| DW2000 |6 |94 |188 |375 |
| DW3000 |6 |94 |188 |375 |
| DW6000 |6 |188 |375 |750 |

Da questa tabella delle allocazioni di memoria a livello di sistema, è possibile notare che una query in esecuzione in un DW2000 nella classe della risorsa xlargerc hello viene allocata un totale di 375 GB di memoria (MB * 60 6.400 distribuzioni / 1.024 tooconvert tooGB) su interamente hello del proprio SQL Data Warehouse.

Hello stesso calcolo si applica toostatic classi di risorse.
 
## <a name="concurrency-slot-consumption"></a>Utilizzo di slot di concorrenza  
SQL Data Warehouse concede tooqueries di memoria più in esecuzione in più classi di risorse. La memoria è una risorsa fissa.  Pertanto, hello maggiore quantità di memoria allocata per ogni query, hello possono eseguire un minor numero di query simultanee. Hello nella tabella seguente sono reiterates tutti hello concetti precedente in una singola visualizzazione che mostra il numero di hello di slot di concorrenza disponibili da DWU e slot hello utilizzato da ogni classe di risorse.  

### <a name="allocation-and-consumption-of-concurrency-slots-for-dynamic-resource-classes"></a>Allocazione e consumo degli slot di concorrenza per le classi di risorse dinamiche  
| DWU | Numero massimo di query simultanee | Numero di slot di concorrenza allocati | Slot utilizzati da smallrc | Slot utilizzati da mediumrc | Slot utilizzati da largerc | Slot utilizzati da xlargerc |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|
| DW100 |4 |4 |1 |1 |2 |4 |
| DW200 |8 |8 |1 |2 |4 |8 |
| DW300 |12 |12 |1 |2 |4 |8 |
| DW400 |16 |16 |1 |4 |8 |16 |
| DW500 |20 |20 |1 |4 |8 |16 |
| DW600 |24 |24 |1 |4 |8 |16 |
| DW1000 |32 |40 |1 |8 |16 |32 |
| DW1200 |32 |48 |1 |8 |16 |32 |
| DW1500 |32 |60 |1 |8 |16 |32 |
| DW2000 |32 |80 |1 |16 |32 |64 |
| DW3000 |32 |120 |1 |16 |32 |64 |
| DW6000 |32 |240 |1 |32 |64 |128 |

### <a name="allocation-and-consumption-of-concurrency-slots-for-static-resource-classes"></a>Allocazione e consumo degli slot di concorrenza per le classi di risorse statiche  
| DWU | Numero massimo di query simultanee | Numero di slot di concorrenza allocati |staticrc10 | staticrc20 | staticrc30 | staticrc40 | staticrc50 | staticrc60 | staticrc70 | staticrc80 |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DW100 |4 |4 |1 |2 |4 |4 |4 |4 |4 |4 |
| DW200 |8 |8 |1 |2 |4 |8 |8 |8 |8 |8 |
| DW300 |12 |12 |1 |2 |4 |8 |8 |8 |8 |8 |
| DW400 |16 |16 |1 |2 |4 |8 |16 |16 |16 |16 |
| DW500 | 20| 20| 1| 2| 4| 8| 16| 16| 16| 16|
| DW600 | 24| 24| 1| 2| 4| 8| 16| 16| 16| 16|
| DW1000 | 32| 40| 1| 2| 4| 8| 16| 32| 32| 32|
| DW1200 | 32| 48| 1| 2| 4| 8| 16| 32| 32| 32|
| DW1500 | 32| 60| 1| 2| 4| 8| 16| 32| 32| 32|
| DW2000 | 32| 80| 1| 2| 4| 8| 16| 32| 64| 64|
| DW3000 | 32| 120| 1| 2| 4| 8| 16| 32| 64| 64|
| DW6000 | 32| 240| 1| 2| 4| 8| 16| 32| 64| 128|

Come si può notare da queste tabelle, l'esecuzione di SQL Data Warehouse come DW1000 alloca un massimo di 32 query simultanee e un totale di 40 slot di concorrenza. Se l'esecuzione avviene da parte di tutti gli utenti nella classe smallrc, vengono consentite 32 query simultanee, poiché ognuna richiede 1 slot di concorrenza. Se tutti gli utenti di un DW1000 erano in esecuzione in mediumrc, ogni query viene allocata 800 MB per ogni distribuzione di un'allocazione di memoria totale di 47 GB per ogni query e concorrenza sarebbe utenti too5 limitato (40 slot concorrenza slot 8 per ogni utente mediumrc /).

## <a name="selecting-proper-resource-class"></a>Scelta della classe di risorse appropriata  
Una buona norma è una classe di risorse tooa toopermanently assegnare gli utenti, anziché modificare le classi di risorse. Ad esempio, le tabelle columnstore tooclustered di carichi di creare gli indici di qualità superiore quando allocata più memoria. tooensure che dispongono di accesso toohigher memoria carichi, creare un utente in modo specifico per il caricamento dei dati e assegnata in modo permanente questa classe di risorse utente tooa superiore.
Esistono un paio di procedure consigliate, toofollow qui. Come indicato in precedenza, SQL Data Warehouse supporta due tipi di classi di risorse: le classi di risorse statiche e quelle dinamiche.
### <a name="loading-best-practices"></a>Procedure consigliate per il caricamento
1.  Se le aspettative hello caricamenti regolari quantità di dati, una classe di risorse statiche è una scelta ottimale. In un secondo momento, quando la scalabilità verticale tooget ulteriori capacità di calcolo, data warehouse di hello sarà in grado di toorun simultanea di più query out-of-the-box, come l'utente hello non utilizzata più memoria.
2.  Se le aspettative hello Carica più grande in alcuni casi, una classe di risorse dinamiche è una scelta ottimale. In un secondo momento, nel caso di aumento tooget maggiore potenza di calcolo, hello carico utente riceverà più memoria out-of-the-box, pertanto consentendo hello carico tooperform più velocemente.

Hello carichi tooprocess memoria necessaria in modo efficiente dipende dalla natura hello della tabella hello caricata e quantità hello dei dati elaborati. Ad esempio, il caricamento di dati nelle tabelle CCI richiede che alcuni gruppi di righe di memoria toolet CCI raggiungere validità. Per ulteriori informazioni, vedere gli indici Columnstore hello - Guida di caricamento dei dati.

Come procedura consigliata, si consiglia di toouse almeno 200MB di memoria per i caricamenti.

### <a name="querying-best-practices"></a>Procedure consigliate per le query
Le query hanno diversi requisiti a seconda della complessità. Aumentare la memoria per ogni query o ad aumentare la concorrenza hello sono entrambi tooaugment validi velocità effettiva globale a seconda delle esigenze di query hello.
1.  Se le aspettative hello sono query complesse, regolare (ad esempio, toogenerate report giornaliero e settimanale) e non richiedono alcun vantaggio tootake di concorrenza, una classe di risorse dinamiche è una scelta ottimale. Se hello sistema dispone di ulteriori dati tooprocess, l'aumento di data warehouse di hello verrà pertanto automaticamente fornire più memoria toohello utente che esegue query hello.
2.  Se le aspettative hello sono modelli di concorrenza diurna o variabile (ad esempio se viene eseguita una query di database hello tramite un web su vasta scala accessibile dell'interfaccia utente), una classe di risorse statiche è una scelta ottimale. In un secondo momento, nel caso di aumento warehouse toodata utente hello associata alla classe di risorse statiche hello verrà automaticamente essere in grado di toorun simultanea di più query.

Selezionando concessione di memoria appropriata a seconda delle necessità di hello della query è considerevole, in quanto dipende molti fattori, ad esempio quantità hello di dati sottoposti a query, natura hello gli schemi di tabella hello e vari join, selezione e predicati di gruppo. Dal punto di vista generale, allocazione di ulteriore memoria consentirà toocomplete query più veloce, ma consentirebbe di ridurre hello concorrenza complessiva. Se la concorrenza non è un problema, un'allocazione eccessiva di memoria non causa alcun danno. velocità effettiva toofine ottimizzazione, durante il tentativo varie caratteristiche di classi di risorse potrebbe essere necessario.

È possibile utilizzare hello seguente stored procedure toofigure out concessione di memoria e concorrenza per ogni classe di risorse in corrispondenza di una determinata SLO e hello più vicino migliore classe di risorse per operazioni CCI con uso intensivo della memoria nella tabella non partizionata di CCI in una classe di risorse specificato:

#### <a name="description"></a>Descrizione:  
Ecco scopo hello della stored procedure:  
1. toohelp utente individuare concessione di memoria e concorrenza per ogni classe di risorse in un determinato SLO. Utente deve tooprovide NULL per lo schema e tablename per questo oggetto, come illustrato nel seguente esempio hello.  
2. utente toohelp scoprire hello più vicino migliore classe di risorse per hello memoria intensed operazioni CCI (caricamento, la tabella di copia, ricompilazione dell'indice e così via) nella tabella non partizionata di CCI in una classe di risorse specificato. Hello stored procedure utilizza toofind dello schema di tabella out hello concessione di memoria necessaria per questo oggetto.

#### <a name="dependencies--restrictions"></a>Dipendenze e restrizioni:
- Questa stored procedure non è il requisito di memoria toocalculate progettato per la tabella partizionata indice ColumnStore cluster.    
- Questa stored procedure non accetta requisito di memoria in considerazione per hello della parte SELECT di un'istruzione CTAS/INSERT-SELECT e presume che sia toobe un'istruzione SELECT semplice.
- Questa stored procedure utilizza una tabella temporanea in modo utilizzabile nella sessione hello in cui è stata creata questa stored procedure.    
- Questa stored procedure dipende da hello attuali offerte (ad esempio, la configurazione hardware, configurazione DMS) e se uno qualsiasi di tale modifica quindi questa stored procedure non funzionerà correttamente.  
- Questa stored procedure dipende dal limite di concorrenza esistente e in caso di modifiche non funziona più correttamente.  
- Questa stored procedure dipende dalle classi di risorse esistenti e in caso di modifiche non funziona più correttamente.  

>  [!NOTE]  
>  Se non si ottiene alcun output dopo l'esecuzione della stored procedure con i parametri forniti, i motivi potrebbero essere due. <br />1. Uno dei parametri di Data Warehouse contiene un valore SLO non valido <br />2. OPPURE non ci sono classi di risorse corrispondenti per l'operazione CCI se è stato fornito il nome della tabella. <br />Ad esempio, DW100, concessione di memoria massima disponibile è 400MB e se lo schema della tabella è di tipo wide sufficiente toocross hello requisito di 400MB.
      
#### <a name="usage-example"></a>Esempio d'uso:
Sintassi:  
`EXEC dbo.prc_workload_management_by_DWU @DWU VARCHAR(7), @SCHEMA_NAME VARCHAR(128), @TABLE_NAME VARCHAR(128)`  
1. @DWU:Fornire un tooextract di parametro NULL hello DWU corrente dal database di data Warehouse hello o fornire qualsiasi supportato DWU sotto forma di hello di 'DW100'
2. @SCHEMA_NAME:Specificare un nome di schema della tabella hello
3. @TABLE_NAME:Specificare un nome di tabella di interesse hello

Esempi di esecuzione di questa stored procedure:  
```sql  
EXEC dbo.prc_workload_management_by_DWU 'DW2000', 'dbo', 'Table1';  
EXEC dbo.prc_workload_management_by_DWU NULL, 'dbo', 'Table1';  
EXEC dbo.prc_workload_management_by_DWU 'DW6000', NULL, NULL;  
EXEC dbo.prc_workload_management_by_DWU NULL, NULL, NULL;  
```

È stato possibile creare Table1 utilizzato in hello esempi sopra riportati come indicato di seguito:  
`CREATE TABLE Table1 (a int, b varchar(50), c decimal (18,10), d char(10), e varbinary(15), f float, g datetime, h date);`

#### <a name="heres-hello-stored-procedure-definition"></a>Ecco hello stored procedure definizione:
```sql  
-------------------------------------------------------------------------------
-- Dropping prc_workload_management_by_DWU procedure if it exists.
-------------------------------------------------------------------------------
IF EXISTS (SELECT * FROM sys.objects WHERE type = 'P' AND name = 'prc_workload_management_by_DWU')
DROP PROCEDURE dbo.prc_workload_management_by_DWU
GO

-------------------------------------------------------------------------------
-- Creating prc_workload_management_by_DWU.
-------------------------------------------------------------------------------
CREATE PROCEDURE dbo.prc_workload_management_by_DWU
(   @DWU VARCHAR(7),
      @SCHEMA_NAME VARCHAR(128),
       @TABLE_NAME VARCHAR(128)
)
AS
IF @DWU IS NULL
BEGIN
-- Selecting proper DWU for hello current DB if not specified.
SET @DWU = (
  SELECT 'DW'+CAST(COUNT(*)*100 AS VARCHAR(10))
  FROM sys.dm_pdw_nodes
  WHERE type = 'COMPUTE')
END

DECLARE @DWU_NUM INT
SET @DWU_NUM = CAST (SUBSTRING(@DWU, 3, LEN(@DWU)-2) AS INT)

-- Raise error if either schema name or table name is supplied but not both them supplied
--IF ((@SCHEMA_NAME IS NOT NULL AND @TABLE_NAME IS NULL) OR (@TABLE_NAME IS NULL AND @SCHEMA_NAME IS NOT NULL))
--     RAISEERROR('User need toosupply either both Schema Name and Table Name or none of them')
       
-- Dropping temp table if exists.
IF OBJECT_ID('tempdb..#ref') IS NOT NULL
BEGIN
  DROP TABLE #ref;
END

-- Creating ref. temptable (CTAS) toohold mapping info.
-- CREATE TABLE #ref
CREATE TABLE #ref
WITH (DISTRIBUTION = ROUND_ROBIN)
AS 
WITH
-- Creating concurrency slots mapping for various DWUs.
alloc
AS
(
  SELECT 'DW100' AS DWU, 4 AS max_queries, 4 AS max_slots, 1 AS slots_used_smallrc, 1 AS slots_used_mediumrc,
        2 AS slots_used_largerc, 4 AS slots_used_xlargerc, 1 AS slots_used_staticrc10, 2 AS slots_used_staticrc20,
        4 AS slots_used_staticrc30, 4 AS slots_used_staticrc40, 4 AS slots_used_staticrc50,
        4 AS slots_used_staticrc60, 4 AS slots_used_staticrc70, 4 AS slots_used_staticrc80
  UNION ALL
    SELECT 'DW200', 8, 8, 1, 2, 4, 8, 1, 2, 4, 8, 8, 8, 8, 8
  UNION ALL
    SELECT 'DW300', 12, 12, 1, 2, 4, 8, 1, 2, 4, 8, 8, 8, 8, 8
  UNION ALL
    SELECT 'DW400', 16, 16, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
     SELECT 'DW500', 20, 20, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
    SELECT 'DW600', 24, 24, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
    SELECT 'DW1000', 32, 40, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW1200', 32, 48, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW1500', 32, 60, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW2000', 32, 80, 1, 16, 32, 64, 1, 2, 4, 8, 16, 32, 64, 64
  UNION ALL
   SELECT 'DW3000', 32, 120, 1, 16, 32, 64, 1, 2, 4, 8, 16, 32, 64, 64
  UNION ALL
    SELECT 'DW6000', 32, 240, 1, 32, 64, 128, 1, 2, 4, 8, 16, 32, 64, 128
)
-- Creating workload mapping tootheir corresponding slot consumption and default memory grant.
,map
AS
(
  SELECT 'SloDWGroupC00' AS wg_name,1 AS slots_used,100 AS tgt_mem_grant_MB
  UNION ALL
    SELECT 'SloDWGroupC01',2,200
  UNION ALL
    SELECT 'SloDWGroupC02',4,400
  UNION ALL
    SELECT 'SloDWGroupC03',8,800
  UNION ALL
    SELECT 'SloDWGroupC04',16,1600
  UNION ALL
    SELECT 'SloDWGroupC05',32,3200
  UNION ALL
    SELECT 'SloDWGroupC06',64,6400
  UNION ALL
    SELECT 'SloDWGroupC07',128,12800
)
-- Creating ref based on current / asked DWU.
, ref
AS
(
  SELECT  a1.*
  ,       m1.wg_name          AS wg_name_smallrc
  ,       m1.tgt_mem_grant_MB AS tgt_mem_grant_MB_smallrc
  ,       m2.wg_name          AS wg_name_mediumrc
  ,       m2.tgt_mem_grant_MB AS tgt_mem_grant_MB_mediumrc
  ,       m3.wg_name          AS wg_name_largerc
  ,       m3.tgt_mem_grant_MB AS tgt_mem_grant_MB_largerc
  ,       m4.wg_name          AS wg_name_xlargerc
  ,       m4.tgt_mem_grant_MB AS tgt_mem_grant_MB_xlargerc
  ,       m5.wg_name          AS wg_name_staticrc10
  ,       m5.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc10
  ,       m6.wg_name          AS wg_name_staticrc20
  ,       m6.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc20
  ,       m7.wg_name          AS wg_name_staticrc30
  ,       m7.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc30
  ,       m8.wg_name          AS wg_name_staticrc40
  ,       m8.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc40
  ,       m9.wg_name          AS wg_name_staticrc50
  ,       m9.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc50
  ,       m10.wg_name          AS wg_name_staticrc60
  ,       m10.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc60
  ,       m11.wg_name          AS wg_name_staticrc70
  ,       m11.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc70
  ,       m12.wg_name          AS wg_name_staticrc80
  ,       m12.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc80
  FROM alloc a1
  JOIN map   m1  ON a1.slots_used_smallrc     = m1.slots_used
  JOIN map   m2  ON a1.slots_used_mediumrc    = m2.slots_used
  JOIN map   m3  ON a1.slots_used_largerc     = m3.slots_used
  JOIN map   m4  ON a1.slots_used_xlargerc    = m4.slots_used
  JOIN map   m5  ON a1.slots_used_staticrc10    = m5.slots_used
  JOIN map   m6  ON a1.slots_used_staticrc20    = m6.slots_used
  JOIN map   m7  ON a1.slots_used_staticrc30    = m7.slots_used
  JOIN map   m8  ON a1.slots_used_staticrc40    = m8.slots_used
  JOIN map   m9  ON a1.slots_used_staticrc50    = m9.slots_used
  JOIN map   m10  ON a1.slots_used_staticrc60    = m10.slots_used
  JOIN map   m11  ON a1.slots_used_staticrc70    = m11.slots_used
  JOIN map   m12  ON a1.slots_used_staticrc80    = m12.slots_used
-- WHERE   a1.DWU = @DWU
  WHERE   a1.DWU = UPPER(@DWU)
)
SELECT  DWU
,       max_queries
,       max_slots
,       slots_used
,       wg_name
,       tgt_mem_grant_MB
,       up1 as rc
,       (ROW_NUMBER() OVER(PARTITION BY DWU ORDER BY DWU)) as rc_id
FROM
(
    SELECT  DWU
    ,       max_queries
    ,       max_slots
    ,       slots_used
    ,       wg_name
    ,       tgt_mem_grant_MB
    ,       REVERSE(SUBSTRING(REVERSE(wg_names),1,CHARINDEX('_',REVERSE(wg_names),1)-1)) as up1
    ,       REVERSE(SUBSTRING(REVERSE(tgt_mem_grant_MBs),1,CHARINDEX('_',REVERSE(tgt_mem_grant_MBs),1)-1)) as up2
    ,       REVERSE(SUBSTRING(REVERSE(slots_used_all),1,CHARINDEX('_',REVERSE(slots_used_all),1)-1)) as up3
    FROM    ref AS r1
    UNPIVOT
    (
        wg_name FOR wg_names IN (wg_name_smallrc,wg_name_mediumrc,wg_name_largerc,wg_name_xlargerc,
        wg_name_staticrc10, wg_name_staticrc20, wg_name_staticrc30, wg_name_staticrc40, wg_name_staticrc50,
        wg_name_staticrc60, wg_name_staticrc70, wg_name_staticrc80)
    ) AS r2
    UNPIVOT
    (
        tgt_mem_grant_MB FOR tgt_mem_grant_MBs IN (tgt_mem_grant_MB_smallrc,tgt_mem_grant_MB_mediumrc,
        tgt_mem_grant_MB_largerc,tgt_mem_grant_MB_xlargerc, tgt_mem_grant_MB_staticrc10, tgt_mem_grant_MB_staticrc20,
        tgt_mem_grant_MB_staticrc30, tgt_mem_grant_MB_staticrc40, tgt_mem_grant_MB_staticrc50,
        tgt_mem_grant_MB_staticrc60, tgt_mem_grant_MB_staticrc70, tgt_mem_grant_MB_staticrc80)
    ) AS r3
    UNPIVOT
    (
        slots_used FOR slots_used_all IN (slots_used_smallrc,slots_used_mediumrc,slots_used_largerc,
        slots_used_xlargerc, slots_used_staticrc10, slots_used_staticrc20, slots_used_staticrc30,
        slots_used_staticrc40, slots_used_staticrc50, slots_used_staticrc60, slots_used_staticrc70,
        slots_used_staticrc80)
    ) AS r4
) a
WHERE   up1 = up2
AND     up1 = up3
;
-- Getting current info about workload groups.
WITH  
dmv  
AS  
(
  SELECT
          rp.name                                           AS rp_name
  ,       rp.max_memory_kb*1.0/1048576                      AS rp_max_mem_GB
  ,       (rp.max_memory_kb*1.0/1024)
          *(request_max_memory_grant_percent/100)           AS max_memory_grant_MB
  ,       (rp.max_memory_kb*1.0/1048576)
          *(request_max_memory_grant_percent/100)           AS max_memory_grant_GB
  ,       wg.name                                           AS wg_name
  ,       wg.importance                                     AS importance
  ,       wg.request_max_memory_grant_percent               AS request_max_memory_grant_percent
  FROM    sys.dm_pdw_nodes_resource_governor_workload_groups wg
  JOIN    sys.dm_pdw_nodes_resource_governor_resource_pools rp    ON  wg.pdw_node_id  = rp.pdw_node_id
                                                                  AND wg.pool_id      = rp.pool_id
  WHERE   rp.name = 'SloDWPool'
  GROUP BY
          rp.name
  ,       rp.max_memory_kb
  ,       wg.name
  ,       wg.importance
  ,       wg.request_max_memory_grant_percent
)
-- Creating resource class name mapping.
,names
AS
(
  SELECT 'smallrc' as resource_class, 1 as rc_id
  UNION ALL
    SELECT 'mediumrc', 2
  UNION ALL
    SELECT 'largerc', 3
  UNION ALL
    SELECT 'xlargerc', 4
  UNION ALL
    SELECT 'staticrc10', 5
  UNION ALL
    SELECT 'staticrc20', 6
  UNION ALL
    SELECT 'staticrc30', 7
  UNION ALL
    SELECT 'staticrc40', 8
  UNION ALL
    SELECT 'staticrc50', 9
  UNION ALL
    SELECT 'staticrc60', 10
  UNION ALL
    SELECT 'staticrc70', 11
  UNION ALL
    SELECT 'staticrc80', 12
)
,base AS
(   SELECT  schema_name
    ,       table_name
    ,       SUM(column_count)                   AS column_count
    ,       ISNULL(SUM(short_string_column_count),0)   AS short_string_column_count
    ,       ISNULL(SUM(long_string_column_count),0)    AS long_string_column_count
    FROM    (   SELECT  sm.name                                             AS schema_name
                ,       tb.name                                             AS table_name
                ,       COUNT(co.column_id)                                 AS column_count
                           ,       CASE    WHEN co.system_type_id IN (36,43,106,108,165,167,173,175,231,239) 
                                AND  co.max_length <= 32 
                                THEN COUNT(co.column_id) 
                        END                                                 AS short_string_column_count
                ,       CASE    WHEN co.system_type_id IN (165,167,173,175,231,239) 
                                AND  co.max_length > 32 and co.max_length <=8000
                                THEN COUNT(co.column_id) 
                        END                                                 AS long_string_column_count
                FROM    sys.schemas AS sm
                JOIN    sys.tables  AS tb   on sm.[schema_id] = tb.[schema_id]
                JOIN    sys.columns AS co   ON tb.[object_id] = co.[object_id]
                           WHERE tb.name = @TABLE_NAME AND sm.name = @SCHEMA_NAME
                GROUP BY sm.name
                ,        tb.name
                ,        co.system_type_id
                ,        co.max_length            ) a
GROUP BY schema_name
,        table_name
)
, size AS
(
SELECT  schema_name
,       table_name
,       75497472                                            AS table_overhead

,       column_count*1048576*8                              AS column_size
,       short_string_column_count*1048576*32                       AS short_string_size,       (long_string_column_count*16777216) AS long_string_size
FROM    base
UNION
SELECT CASE WHEN COUNT(*) = 0 THEN 'EMPTY' END as schema_name
         ,CASE WHEN COUNT(*) = 0 THEN 'EMPTY' END as table_name
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as table_overhead
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as column_size
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as short_string_size

,CASE WHEN COUNT(*) = 0 THEN 0 END as long_string_size
FROM   base
)
, load_multiplier as 
(
SELECT  CASE 
                     WHEN FLOOR(8 * (CAST (@DWU_NUM AS FLOAT)/6000)) > 0 THEN FLOOR(8 * (CAST (@DWU_NUM AS FLOAT)/6000)) 
                     ELSE 1 
              END AS multipliplication_factor
) 
       SELECT  r1.DWU
       , schema_name
       , table_name
       , rc.resource_class as closest_rc_in_increasing_order
       , max_queries_at_this_rc = CASE
             WHEN (r1.max_slots / r1.slots_used > r1.max_queries)
                  THEN r1.max_queries
             ELSE r1.max_slots / r1.slots_used
                  END
       , r1.max_slots as max_concurrency_slots
       , r1.slots_used as required_slots_for_the_rc
       , r1.tgt_mem_grant_MB  as rc_mem_grant_MB
       , CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) AS est_mem_grant_required_for_cci_operation_MB       
       FROM    size, load_multiplier, #ref r1, names  rc
       WHERE r1.rc_id=rc.rc_id
                     AND CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) < r1.tgt_mem_grant_MB
       ORDER BY ABS(CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) - r1.tgt_mem_grant_MB)
GO
```

## <a name="query-importance"></a>Priorità delle query
SQL Data Warehouse implementa le classi di risorse utilizzando i gruppi del carico di lavoro. Sono disponibili un totale di otto gruppi di carico di lavoro che controllano il comportamento di hello delle classi di risorse hello hello diverse dimensioni DWU. Per qualsiasi numero di DWU SQL Data Warehouse viene utilizzato solo quattro delle otto gruppi di carico di lavoro hello. Ciò è utile perché ogni gruppo di carico di lavoro viene assegnato tooone di quattro classi di risorse: smallrc mediumrc, largerc, o xlargerc. Hello importanza delle informazioni sui gruppi del carico di lavoro hello è che alcuni di questi gruppi di carico di lavoro siano impostate toohigher *importanza*. La priorità viene usata per la pianificazione della CPU. Le query eseguite con priorità alta otterranno tre volte più cicli della CPU rispetto a quelle con priorità media. Di conseguenza, i mapping degli slot della concorrenza determinano anche la priorità della CPU. Quando una query utilizza 16 o più slot, viene eseguita con priorità alta.

Hello nella tabella seguente sono illustrati i mapping di importanza hello per ogni gruppo di carico di lavoro.

### <a name="workload-group-mappings-tooconcurrency-slots-and-importance"></a>Importanza e slot tooconcurrency mapping di gruppo del carico di lavoro
| Gruppi di carichi di lavoro | Mapping degli slot di concorrenza | MB/Distribuzione | Mapping delle priorità |
|:--- |:---:|:---:|:--- |
| SloDWGroupC00 |1 |100 |Media |
| SloDWGroupC01 |2 |200 |Media |
| SloDWGroupC02 |4 |400 |Media |
| SloDWGroupC03 |8 |800 |Media |
| SloDWGroupC04 |16 |1.600 |Alto |
| SloDWGroupC05 |32 |3.200 |Alto |
| SloDWGroupC06 |64 |6.400 |Alto |
| SloDWGroupC07 |128 |12.800 |Alto |

Da hello **allocazione e utilizzo di slot concorrenza** grafico, è possibile verificare che un DW500 Usa 1, 4, 8 o slot di concorrenza 16 per smallrc, mediumrc, largerc e xlargerc, rispettivamente. È possibile cercare i valori in hello precede l'importanza di hello toofind grafico per ogni classe di risorse.

### <a name="dw500-mapping-of-resource-classes-tooimportance"></a>Mapping di DW500 di tooimportance classi di risorse
| classe di risorse | Gruppo del carico di lavoro | Numero di slot di concorrenza usati | MB/Distribuzione | priorità |
|:--- |:--- |:---:|:---:|:--- |
| smallrc |SloDWGroupC00 |1 |100 |Media |
| mediumrc |SloDWGroupC02 |4 |400 |Media |
| largerc |SloDWGroupC03 |8 |800 |Media |
| xlargerc |SloDWGroupC04 |16 |1.600 |Alto |
| staticrc10 |SloDWGroupC00 |1 |100 |Media |
| staticrc20 |SloDWGroupC01 |2 |200 |Media |
| staticrc30 |SloDWGroupC02 |4 |400 |Media |
| staticrc40 |SloDWGroupC03 |8 |800 |Media |
| staticrc50 |SloDWGroupC03 |16 |1.600 |Alto |
| staticrc60 |SloDWGroupC03 |16 |1.600 |Alto |
| staticrc70 |SloDWGroupC03 |16 |1.600 |Alto |
| staticrc80 |SloDWGroupC03 |16 |1.600 |Alto |

È possibile utilizzare hello seguenti toolook query DMV in differenze hello nell'allocazione di risorse di memoria in modo dettagliato da prospettiva hello di carichi hello o tooanalyze active e cronologici l'utilizzo di gruppi di carico di lavoro hello. risoluzione dei problemi.

```sql
WITH rg
AS
(   SELECT  
     pn.name                        AS node_name
    ,pn.[type]                        AS node_type
    ,pn.pdw_node_id                    AS node_id
    ,rp.name                        AS pool_name
    ,rp.max_memory_kb*1.0/1024                AS pool_max_mem_MB
    ,wg.name                        AS group_name
    ,wg.importance                    AS group_importance
    ,wg.request_max_memory_grant_percent        AS group_request_max_memory_grant_pcnt
    ,wg.max_dop                        AS group_max_dop
    ,wg.effective_max_dop                AS group_effective_max_dop
    ,wg.total_request_count                AS group_total_request_count
    ,wg.total_queued_request_count            AS group_total_queued_request_count
    ,wg.active_request_count                AS group_active_request_count
    ,wg.queued_request_count                AS group_queued_request_count
    FROM    sys.dm_pdw_nodes_resource_governor_workload_groups wg
    JOIN    sys.dm_pdw_nodes_resource_governor_resource_pools rp    
            ON  wg.pdw_node_id  = rp.pdw_node_id
            AND wg.pool_id      = rp.pool_id
    JOIN    sys.dm_pdw_nodes pn
            ON    wg.pdw_node_id    = pn.pdw_node_id
    WHERE   wg.name like 'SloDWGroup%'
        AND     rp.name = 'SloDWPool'
)
SELECT    pool_name
,        pool_max_mem_MB
,        group_name
,        group_importance
,        (pool_max_mem_MB/100)*group_request_max_memory_grant_pcnt AS max_memory_grant_MB
,        node_name
,        node_type
,       group_total_request_count
,       group_total_queued_request_count
,       group_active_request_count
,       group_queued_request_count
FROM    rg
ORDER BY
    node_name
,    group_request_max_memory_grant_pcnt
,    group_importance
;
```

## <a name="queries-that-honor-concurrency-limits"></a>Query che rispettano i limiti di concorrenza
La maggior parte delle query è regolata da classi di risorse. Queste query devono adattarsi all'interno di query simultanee hello e le soglie dello slot di concorrenza. L'utente non è possibile scegliere tooexclude una query dal modello di hello concorrenza slot.

tooreiterate, hello istruzioni seguenti rispettano le classi di risorse:

* INSERT SELECT
* AGGIORNAMENTO
* DELETE
* SELEZIONARE (quando si esegue una query sulle tabelle utente)
* ALTER INDEX REBUILD
* ALTER INDEX REORGANIZE
* MODIFICA TABELLA RICOMPILAZIONE
* CREATE INDEX
* CREARE L'INDICE COLUMNSTORE CLUSTER
* CREATE TABLE AS SELECT (CTAS)
* Caricamento dei dati
* Operazioni di spostamento dei dati eseguite dal servizio lo spostamento dei dati (DMS) hello

## <a name="query-exceptions-tooconcurrency-limits"></a>Limiti tooconcurrency eccezioni di query
Alcune query non rispettano risorse hello classe toowhich hello utente è assegnato. Questi limiti di concorrenza toohello le eccezioni vengono effettuati quando le risorse di memoria hello necessari per un particolare comando sono ridotte, spesso perché il comando hello è un'operazione di metadati. obiettivo di Hello di queste eccezioni è tooavoid maggiori delle allocazioni di memoria per le query che non saranno mai necessario. In questi casi, classe di risorse ridotto (smallrc) viene sempre utilizzata indipendentemente dalla classe di risorsa effettiva hello predefinito di hello assegnato toohello utente. Ad esempio, in smallrc verrà sempre eseguita `CREATE LOGIN` . Hello risorse richieste toofulfill questa operazione sono molto bassa, pertanto non rende la query di hello tooinclude senso nel modello di hello concorrenza slot.  Queste query non dipendono anche dal limite di 32 hello utente concorrenza, un numero illimitato di tali query è possibile eseguire backup toohello limite di sessioni di 1.024 sessioni.

Hello seguendo le istruzioni non rispetta le classi di risorse:

* CREATE o DROP TABLE
* ALTER TABLE... SWITCH, SPLIT o MERGE PARTITION
* ALTER INDEX DISABLE
* DROP INDEX
* CREATE, UPDATE o DROP STATISTICS
* TRUNCATE TABLE
* ALTER AUTHORIZATION
* CREATE LOGIN
* CREATE, ALTER o DROP USER
* CREATE, ALTER o DROP PROCEDURE
* CREATE o DROP VIEW
* INSERT VALUES
* SELECT da viste di sistema e DMV
* EXPLAIN
* DBCC

<!--
Removed as these two are not confirmed / supported under SQLDW
- CREATE REMOTE TABLE AS SELECT
- CREATE EXTERNAL TABLE AS SELECT
- REDISTRIBUTE
-->

##  <a name="changing-user-resource-class-example"></a> Esempio di modifica della classe di risorse di un utente
1. **Creare account di accesso:** aprire una connessione tooyour **master** database hello SQL server che ospita il database di SQL Data Warehouse ed eseguire i seguenti comandi hello.
   
    ```sql
    CREATE LOGIN newperson WITH PASSWORD = 'mypassword';
    CREATE USER newperson for LOGIN newperson;
    ```
   
   > [!NOTE]
   > È un toocreate buona un utente nel database master di hello per gli utenti di Azure SQL Data Warehouse. Creazione di un utente nel database master consente a un utente toologin usando strumenti come SQL Server Management Studio senza specificare un nome di database.  Inoltre, consente loro toouse hello oggetto explorer tooview tutti i database in SQL server.  Per altre informazioni su creazione e gestione degli utenti, vedere [Proteggere un database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].
   > 
   > 
2. **Creare l'utente di SQL Data Warehouse:** aprire una connessione toohello **SQL Data Warehouse** database ed eseguire hello comando seguente.
   
    ```sql
    CREATE USER newperson FOR LOGIN newperson;
    ```
3. **Concedere le autorizzazioni:** hello seguenti concessioni di esempio `CONTROL` su hello **SQL Data Warehouse** database. `CONTROL`in hello livello di database è hello equivalente del ruolo db_owner in SQL Server.
   
    ```sql
    GRANT CONTROL ON DATABASE::MySQLDW toonewperson;
    ```
4. **Aumentare la classe di risorse:** tooadd di query seguente hello di utilizzare un ruolo utente tooa maggiore carico di lavoro gestione.
   
    ```sql
    EXEC sp_addrolemember 'largerc', 'newperson'
    ```
5. **Classe di risorse di diminuire:** tooremove di query seguente hello di usare un utente a un ruolo di gestione del carico di lavoro.
   
    ```sql
    EXEC sp_droprolemember 'largerc', 'newperson';
    ```
   
   > [!NOTE]
   > Non è possibile tooremove smallrc di un utente.
   > 
   > 

## <a name="queued-query-detection-and-other-dmvs"></a>Rilevamento di query in coda e altre viste a gestione dinamica
È possibile utilizzare hello `sys.dm_pdw_exec_requests` query DMV tooidentify che sono in attesa in una coda di concorrenza. Le query in attesa di uno slot di concorrenza saranno in stato **sospeso**.

```sql
SELECT      r.[request_id]                 AS Request_ID
        ,r.[status]                 AS Request_Status
        ,r.[submit_time]             AS Request_SubmitTime
        ,r.[start_time]                 AS Request_StartTime
        ,DATEDIFF(ms,[submit_time],[start_time]) AS Request_InitiateDuration_ms
        ,r.resource_class                         AS Request_resource_class
FROM    sys.dm_pdw_exec_requests r;
```

I ruoli di gestione del carico di lavoro possono essere visualizzati con `sys.database_principals`.

```sql
SELECT  ro.[name]           AS [db_role_name]
FROM    sys.database_principals ro
WHERE   ro.[type_desc]      = 'DATABASE_ROLE'
AND     ro.[is_fixed_role]  = 0;
```

Hello query seguente viene illustrato il ruolo di cui ogni utente è assegnato.

```sql
SELECT     r.name AS role_principal_name
        ,m.name AS member_principal_name
FROM    sys.database_role_members rm
JOIN    sys.database_principals AS r            ON rm.role_principal_id        = r.principal_id
JOIN    sys.database_principals AS m            ON rm.member_principal_id    = m.principal_id
WHERE    r.name IN ('mediumrc','largerc', 'xlargerc');
```

SQL Data Warehouse è hello seguenti tipi di attesa:

* **LocalQueriesConcurrencyResourceType**: le query che si trovano di fuori di framework di hello concorrenza slot. Le query DMV e le funzioni di sistema  come `SELECT @@VERSION` sono esempi di query locali.
* **UserConcurrencyResourceType**: le query che si trovano all'interno di hello concorrenza slot framework. Le query sulle tabelle dell'utente finale rappresentano esempi in cui si usa questo tipo di risorsa.
* **DmsConcurrencyResourceType**: attese risultanti dalle operazioni di spostamento dei dati.
* **BackupConcurrencyResourceType**: indica che è in esecuzione il backup di un database. valore massimo di Hello per questo tipo di risorsa è 1. Se più copie di backup sono stati richiesti in hello contemporaneamente, hello ad altri utenti verranno inseriti nella coda.

Hello `sys.dm_pdw_waits` DMV può essere utilizzato toosee quali risorse di una richiesta è in attesa di.

```sql
SELECT  w.[wait_id]
,       w.[session_id]
,       w.[type]            AS Wait_type
,       w.[object_type]
,       w.[object_name]
,       w.[request_id]
,       w.[request_time]
,       w.[acquire_time]
,       w.[state]
,       w.[priority]
,    SESSION_ID()            AS Current_session
,    s.[status]            AS Session_status
,    s.[login_name]
,    s.[query_count]
,    s.[client_id]
,    s.[sql_spid]
,    r.[command]            AS Request_command
,    r.[label]
,    r.[status]            AS Request_status
,    r.[submit_time]
,    r.[start_time]
,    r.[end_compile_time]
,    r.[end_time]
,    DATEDIFF(ms,r.[submit_time],r.[start_time])        AS Request_queue_time_ms
,    DATEDIFF(ms,r.[start_time],r.[end_compile_time])    AS Request_compile_time_ms
,    DATEDIFF(ms,r.[end_compile_time],r.[end_time])        AS Request_execution_time_ms
,    r.[total_elapsed_time]
FROM    sys.dm_pdw_waits w
JOIN    sys.dm_pdw_exec_sessions s  ON w.[session_id] = s.[session_id]
JOIN    sys.dm_pdw_exec_requests r  ON w.[request_id] = r.[request_id]
WHERE    w.[session_id] <> SESSION_ID();
```

Hello `sys.dm_pdw_resource_waits` DMV Mostra solo le attese risorse hello utilizzate da una determinata query. Tempo di attesa di risorse solo misura il tempo di hello in attesa di risorse toobe fornito, come toosignal anziché di attesa, ovvero hello tempo impiegato per hello sottostante una query SQL Server tooschedule hello nella CPU hello.

```sql
SELECT  [session_id]
,       [type]
,       [object_type]
,       [object_name]
,       [request_id]
,       [request_time]
,       [acquire_time]
,       DATEDIFF(ms,[request_time],[acquire_time])  AS acquire_duration_ms
,       [concurrency_slots_used]                    AS concurrency_slots_reserved
,       [resource_class]
,       [wait_id]                                   AS queue_position
FROM    sys.dm_pdw_resource_waits
WHERE    [session_id] <> SESSION_ID();
```

Hello `sys.dm_pdw_wait_stats` può essere utilizzata per l'analisi delle tendenze cronologiche di attese.

```sql
SELECT    w.[pdw_node_id]
,        w.[wait_name]
,        w.[max_wait_time]
,        w.[request_count]
,        w.[signal_time]
,        w.[completed_count]
,        w.[wait_time]
FROM    sys.dm_pdw_wait_stats w;
```

## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni sulla gestione degli utenti e della sicurezza del database, vedere [Proteggere un database in SQL Data Warehouse][Secure a database in SQL Data Warehouse]. Per ulteriori informazioni sulle classi di risorse come dimensioni maggiori possono migliorare la qualità di indice columnstore cluster, vedere [la ricompilazione di indici tooimprove segmento di qualità].

<!--Image references-->

<!--Article references-->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[la ricompilazione di indici tooimprove segmento di qualità]: ./sql-data-warehouse-tables-index.md#rebuilding-indexes-to-improve-segment-quality
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md

<!--MSDN references-->
[Managing Databases and Logins in Azure SQL Database]:https://msdn.microsoft.com/library/azure/ee336235.aspx

<!--Other Web references-->
