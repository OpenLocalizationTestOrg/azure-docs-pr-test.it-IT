---
title: "query di analitica aaaRun ad hoc in più database SQL di Azure | Documenti Microsoft"
description: "Eseguire query ad hoc analitica tra più database SQL in app di hello Wingtip SaaS multi-tenant."
keywords: esercitazione database SQL
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: billgib; sstein
ms.openlocfilehash: 140cd51fdd03b5a548147282b51ceb0ad80c944d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-ad-hoc-analytics-queries-across-all-wingtip-saas-tenants"></a>Eseguire query di analisi ad-hoc su tutti i tenant SaaS Wingtip

In questa esercitazione, eseguire le query distribuite tra l'intero set di database di tenant di hello tooenable ad hoc analitica. Query elastico è usato tooenable distribuita query, che richiede un database aggiuntivo analitica viene distribuito (server di catalogo toohello). Queste query possono estrarre informazioni far parte di hello quotidiane sui dati operativi di app SaaS Wingtip hello.


In questa esercitazione si apprenderà:

> [!div class="checklist"]

> * Informazioni sulle viste globali di hello in ogni database, che consentono l'esecuzione di query efficienti tra tenant
> * Come toodeploy un database analitica ad hoc
> * Come toorun query distribuite tra tutti i database tenant



toocomplete completamento di questa esercitazione, assicurarsi che i hello seguenti prerequisiti:

* app SaaS Wingtip Hello viene distribuita. toodeploy in meno di cinque minuti, vedere [Distribuisci ed esplorare l'applicazione SaaS Wingtip hello](sql-database-saas-tutorial.md)
* Azure PowerShell è installato. Per informazioni dettagliate, vedere [Introduzione ad Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)
* SQL Server Management Studio (SSMS) è installato. toodownload e installare SQL Server Management Studio, vedere [scaricare SQL Server Management Studio (SQL Server Management Studio)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).


## <a name="ad-hoc-analytics-pattern"></a>Modello di analisi ad hoc

Uno dei hello delle opportunità con applicazioni SaaS è quantità hello toouse di dati archiviati centralmente nel cloud hello del tenant. Utilizzare questo dati toogain approfondite operazione hello e l'utilizzo di applicazione, i tenant, i relativi utenti, le preferenze, comportamenti, e così via. Queste informazioni possono essere utili come base per progettare sviluppi futuri, miglioramenti dell'usabilità e altri investimenti per app e servizi.

L'accesso a questi dati è semplice quando sono raccolti in un singolo database multi-tenant, ma non è altrettanto semplice in una distribuzione su larga scala potenzialmente in migliaia di database. Un approccio consiste toouse [Query elastico](sql-database-elastic-query-overview.md), che consente l'esecuzione di query su un set distribuito di database con schema comune. Query elastico utilizza un singolo *head* database in cui sono definite le tabelle esterne che mirror tabelle o viste in hello distribuiti database (tenant). Le query inviate toothis head database è tooproduce compilato un piano di query distribuite con parti di query hello propagati database tenant toohello in base alle esigenze. Query elastico utilizza mappa partizioni hello hello catalogo database tooprovide hello il percorso del database tenant hello. La configurazione e l'esecuzione di query sono semplici con il linguaggio [Transact-SQL](https://docs.microsoft.com/sql/t-sql/language-reference) standard e sono supportate query ad hoc da strumenti come Power BI ed Excel.

Distribuendo le query tra database tenant hello, elastico Query fornisce informazioni dettagliate immediate sui dati di produzione in tempo reale. Tuttavia, come Query elastico estrae i dati da molti database, latenza a volte può essere superiore per le query equivalente query inviati tooa singolo database di multi-tenant. Deve prestare attenzione quando si progetta una query toominimize hello i dati restituiti. Query elastico è spesso adatto principalmente per piccole quantità di dati in tempo reale, l'esecuzione di query anziché toobuilding utilizzati di frequente, le query complesse analitica o report. Se le query non eseguono correttamente, esaminare hello [piano di esecuzione](https://docs.microsoft.com/sql/relational-databases/performance/display-an-actual-execution-plan) toosee quale parte di query hello è stato inserito il database remoto toohello e viene restituita la quantità di dati. Per ottenere un servizio migliore per le query che richiedono un'elaborazione analitica complessa, in alcuni casi è consigliabile estrarre i dati tenant in un database dedicato o in un data warehouse ottimizzato per le query analitiche. Questo modello è illustrato in hello [esercitazione analitica tenant](sql-database-saas-tutorial-tenant-analytics.md). 

## <a name="get-hello-wingtip-application-scripts"></a>Ottenere script per l'applicazione hello Wingtip

Hello Wingtip SaaS script e codice sorgente dell'applicazione sono disponibili in hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) repository github. [I passaggi di script di SaaS Wingtip hello toodownload](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).

## <a name="create-ticket-sales-data"></a>Creare i dati di vendita dei biglietti

toorun esegue query su un set di dati più interessante, creare i dati di vendita ticket eseguendo il ticket hello-generatore.

1. In hello *PowerShell ISE*aprire hello... \\Moduli learning\\Analitica Operational\\Analitica ad hoc\\*Demo AdhocAnalytics.ps1* script e impostare hello seguenti valori:
   * **$DemoScenario** = 1, **Acquistare biglietti per gli eventi in tutte le sedi**.
2. Premere **F5** per eseguire script hello e generare le vendite di ticket. Durante l'esecuzione di script hello continuare passaggi hello in questa esercitazione. viene eseguita una query di dati del ticket Hello in hello *eseguire query ad hoc distribuita* sezione, quindi attendere hello ticket generatore toocomplete se è ancora in esecuzione quando si otterrà toothat esercizio.

## <a name="explore-hello-global-views"></a>Esplorazione delle viste globali hello

applicazione SaaS Wingtip Hello viene creato utilizzando un modello di database per ogni tenant, in modo che lo schema del database tenant hello è definito da una prospettiva single-tenant. Le informazioni specifiche sul tenant sono presenti in una sola tabella *Venue*, che contiene sempre una singola riga ed è implementata come heap, senza una chiave primaria. Non è necessario aprire altre tabelle nello schema hello toobe correlati toohello *luogo* tabella, perché in uso normale, non è mai dubbi tenant hello dati appartengono.

Tuttavia, quando si eseguono query in tutti i database, è importante che Query elastico può gestire dati hello come se fosse parte di un singolo database logico partizionato dal tenant. tooachieve questo set di viste 'globale' sono database tenant toohello aggiunto che un id tenant del progetto in ognuna delle tabelle di hello che vengono eseguita una query a livello globale. Ad esempio, hello *VenueEvents* visualizzazione aggiunge calcolato *VenueId* toohello colonne proiettata dai hello *eventi* tabella. Mediante la definizione di tabella esterna di hello nel database head hello su *VenueEvents* (anziché hello sottostante *eventi* tabella), Query elastico è in grado di toopush verso il basso di join basati su *VenueId* affinché possano essere eseguite in parallelo in ogni database remoto (anziché nel database head hello). Questo riduce notevolmente hello quantità di dati viene restituiti, che comporta un miglioramento significativo delle prestazioni per molte query. Queste viste globali sono state già create in tutti i database tenant e in *basetenantdb*.

1. Aprire SQL Server Management Studio e [connessione toohello tenants1 -&lt;utente&gt; server](sql-database-wtp-overview.md#explore-database-schema-and-execute-sql-queries-using-ssms).
2. Espandere **Database**, fare clic con il pulsante destro del mouse su **contosoconcerthall** e selezionare **Nuova query**.
3. Eseguire hello differenza hello tooexplore di query tra tabelle single-tenant hello e viste globali hello seguenti:

   ```T-SQL
   -- hello base Venue table, that has no VenueId associated.
   SELECT * FROM Venue

   -- Notice hello plural name 'Venues'. This view projects a VenueId column.
   SELECT * FROM Venues

   -- hello base Events table, which has no VenueId column.
   SELECT * FROM Events

   -- This view projects hello VenueId retrieved from hello Venues table.
   SELECT * FROM VenueEvents
   ```

In queste visualizzazioni, hello *VenueId* viene calcolata come un hash di nome per eventi hello, ma qualsiasi approccio potrebbe essere toointroduce utilizzato un valore univoco. Questo approccio è simile a toohello chiave del tenant hello viene calcolata per l'utilizzo nel catalogo di hello.

definizione di hello tooexamine di hello *eventi* Vista:

1. In **Esplora oggetti** espandere **contosoconcethall** > **Viste**:

   ![Viste](media/sql-database-saas-tutorial-adhoc-analytics/views.png)

2. Fare clic con il pulsante destro del mouse su **dbo.Venues**.
3. Selezionare **Crea script per vista** > **CREATE in** > **Nuova finestra editor di query**.

Script qualsiasi altri hello *luogo* toosee Visualizza la modalità di aggiunta hello *VenueId*.

## <a name="deploy-hello-database-used-for-ad-hoc-distributed-queries"></a>Distribuire database hello per le query distribuite ad hoc

Questo esercizio distribuisce hello *adhocanalytics* database. Si tratta di database hello head conterrà schema hello utilizzato per l'esecuzione di query in tutti i database tenant. database Hello è distribuito toohello esistente di server di catalogo, ovvero server hello utilizzato per i database relative alla gestione di app di esempio hello.

1. Apri... \\Moduli learning\\Analitica Operational\\Analitica ad hoc\\*Demo AdhocAnalytics.ps1* in hello *PowerShell ISE* e hello set valori seguenti:
   * **$DemoScenario** = 2, **Distribuire un database di analisi ad hoc**.

2. Premere **F5** toorun hello script e creare hello *adhocanalytics* database.

Nella sezione successiva hello, aggiungere database toohello schema può quindi essere utilizzato toorun distribuita query.

## <a name="configure-hello-database-for-running-distributed-queries"></a>Configurare il database di hello per l'esecuzione di query distribuite

Questo esercizio aggiunge schema (origine dati esterna hello e definizioni di tabella esterna) toohello ad hoc analitica database consente l'esecuzione di query in tutti i database tenant.

1. Aprire SQL Server Management Studio e connettersi toohello database Analitica ad hoc creato nel passaggio precedente hello. nome di Hello del database hello sarà adhocanalytics.
2. Aprire ...\Learning Modules\Operational Analytics\Adhoc Analytics\ *Initialize-AdhocAnalyticsDB.sql* in SSMS.
3. Rivedere lo script SQL hello e prendere nota delle seguenti hello:

   Elastico Query utilizza una credenziale con ambito database tooaccess ogni database tenant hello. Questa credenziale deve toobe disponibile in tutti i database hello e deve essere concesse in genere necessari i diritti minimi hello tooenable queste query ad hoc.

    ![creare le credenziali](media/sql-database-saas-tutorial-adhoc-analytics/create-credential.png)

   Hello origine dati esterna, che viene definita mappa partizioni di toouse hello tenant nel database di catalogo hello. Tramite questo come origine dati esterna hello, le query sono distribuiti tooall database registrati nel catalogo di hello quando viene eseguita la query hello. Poiché i nomi dei server sono diversi per ogni distribuzione, questo script di inizializzazione Ottiene il percorso di hello del database del catalogo hello tramite il recupero dei server corrente hello (@@servername) in cui viene eseguito uno script hello.

    ![creare l'origine dati esterna](media/sql-database-saas-tutorial-adhoc-analytics/create-external-data-source.png)

   tabelle esterne che fanno riferimento a viste globali di hello descritto nella sezione precedente hello e definita con Hello **distribuzione = SHARDED(VenueId)**. Poiché ogni *VenueId* tooa singolo database, viene eseguito il mapping Ciò migliora le prestazioni per molti scenari come illustrato nella sezione successiva hello.

    ![creare tabelle esterne](media/sql-database-saas-tutorial-adhoc-analytics/external-tables.png)

   tabella locale Hello *VenueTypes* che viene creata e popolata. Questa tabella di dati di riferimento è comune in tutti i database tenant, pertanto può essere rappresentato come una tabella locale e popolati con dati comuni hello. Per alcune query questo potrebbe ridurre hello quantità di dati spostati tra i database tenant hello e hello *adhocanalytics* database.

    ![creare la tabella](media/sql-database-saas-tutorial-adhoc-analytics/create-table.png)

   Se si includono tabelle di riferimento in questo modo, sia dati e schema della tabella hello tooupdate che ogni volta che si aggiornano i database tenant hello.

4. Premere **F5** toorun hello script e inizializzare hello *adhocanalytics* database. 

È ora possibile eseguire query distribuite e ottenere informazioni dettagliate da tutti i tenant.

## <a name="run-ad-hoc-distributed-queries"></a>Eseguire query distribuite ad hoc

Ora che hello *adhocanalytics* database è impostato, vado Avanti ed eseguire alcune query distribuite. Includi piano di esecuzione hello per una migliore comprensione di in cui è in corso l'elaborazione delle query hello. 

Quando si esamina il piano di esecuzione hello, passare il mouse sulle icone di hello piano per i dettagli. 

Toonote importanti, è l'impostazione **distribuzione = SHARDED(VenueId)** quando è definito l'origine dati esterna hello, migliora le prestazioni per molti scenari. Poiché ogni *VenueId* tooa viene eseguito il mapping solo database, il filtro è dati hello solo facilmente eseguite in modalità remota, la restituzione è necessario.

1. Aprire ...\\Learning Modules\\Operational Analytics\\Adhoc Analytics\\*Demo-AdhocAnalyticsQueries.sql* in SSMS.
2. Verificare di essere connesso toohello **adhocanalytics** database.
3. Seleziona hello **Query** menu e fare clic su **Includi piano di esecuzione effettivo**
4. Evidenziare hello *quali eventi sono registrati?* query e premere **F5**.

   query di Hello restituisce l'elenco di eventi intera hello, che illustra la modalità rapida ed è facile tooquery in tutti i dati restituiti da ogni tenant e tenant.

   Esaminare il piano di hello e verificare che intero costo di hello è query remota hello perché siamo semplicemente database tenant di corso tooeach e selezionando informazioni luogo hello.

   ![SELECT * FROM dbo.Venues](media/sql-database-saas-tutorial-adhoc-analytics/query1-plan.png)

5. La query successiva selezionare hello e premere **F5**.

   La query unisce i dati dal database tenant hello e hello locale *VenueTypes* tabella (locale, perché è una tabella di hello *adhocanalytics* database).

   Esaminare il piano di hello e vedere tale hello maggioranza dei costi è query remota hello perché viene eseguita una query info per eventi di ciascun tenant (dbo. Eventi), quindi effettuare un rapido join locale con hello locale *VenueTypes* nome descrittivo della tabella toodisplay hello.

   ![Creare un join su dati remoti e locali](media/sql-database-saas-tutorial-adhoc-analytics/query2-plan.png)

6. A questo punto selezionare hello *il giorno in cui sono stati hello la maggior parte dei ticket vendute?* query e premere **F5**.

   Questa query esegue operazioni un po' più complesse di join e aggregazione. Che cos'è toonote importante è che la maggior parte dell'elaborazione hello viene eseguita in modalità remota, e in questo caso, è ripristinare solo le righe di hello che è necessario restituire un'unica riga per il conteggio di vendita per ogni sessione ticket di aggregazione al giorno.

   ![query](media/sql-database-saas-tutorial-adhoc-analytics/query3-plan.png)


## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione si è appreso come:

> [!div class="checklist"]

> * Eseguire query distribuite su tutti i database tenant
> * Distribuire un database analitica ad hoc e aggiungere le query di schema tooit toorun distribuita.


Ora provare hello [esercitazione Tenant Analitica](sql-database-saas-tutorial-tenant-analytics.md) tooexplore l'estrazione dei dati tooa analitica separato database per l'elaborazione analitica più complessa...

## <a name="additional-resources"></a>Risorse aggiuntive

* Ulteriori [esercitazioni in cui si basano su hello applicazione SaaS Wingtip](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Query elastica](sql-database-elastic-query-overview.md)
