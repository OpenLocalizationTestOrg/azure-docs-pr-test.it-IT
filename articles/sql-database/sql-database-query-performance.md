---
title: informazioni dettagliate prestazioni aaaQuery per Database SQL di Azure | Documenti Microsoft
description: Monitoraggio delle prestazioni delle query identifica hello utilizzo CPU la maggior parte delle query per un Database di SQL Azure.
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: c2f580b2-3835-453f-89f5-140e02dd2ea7
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: sstein
ms.openlocfilehash: 01cca26f85193c679365585cd676449c9db00e1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-query-performance-insight"></a>Query Performance Insight del database SQL di Azure
La gestione e ottimizzazione delle prestazioni dei database relazionali di hello è un'attività complessa che richiede una notevole esperienza e richiede tempo. Informazioni dettagliate prestazioni query consente toospend meno tempo di risoluzione dei problemi di prestazioni del database, fornendo seguente hello:

* Informazioni più approfondite sull'utilizzo delle risorse del database (DTU). 
* Hello prime query per numero di CPU/Durata/esecuzione che potenzialmente possono essere ottimizzate per migliorare le prestazioni.
* salve possibilità toodrill verso il basso in dettagli hello di una query, visualizzare il testo e la cronologia di utilizzo delle risorse. 
* Le annotazioni relative all'ottimizzazione delle prestazioni che descrivono le azioni eseguite da [SQL Azure Database Advisor](sql-database-advisor.md)  



## <a name="prerequisites"></a>Prerequisiti
* Per Informazioni dettagliate sulle prestazioni delle query è necessario che l' [archivio query](https://msdn.microsoft.com/library/dn817826.aspx) sia attivo nel database. Se l'archivio Query non è in esecuzione, il portale di hello richiede tooturn sul.

## <a name="permissions"></a>Autorizzazioni
esempio Hello [controllo di accesso basato sui ruoli](../active-directory/role-based-access-control-what-is.md) le autorizzazioni sono necessarie toouse informazioni dettagliate prestazioni Query: 

* **Lettore**, **proprietario**, **collaboratore**, **collaboratore DB SQL**, o **collaboratore di SQL Server** sono le autorizzazioni necessario tooview hello prime consumo di risorse grafici e le query. 
* **Proprietario**, **collaboratore**, **collaboratore DB SQL**, o **collaboratore di SQL Server** le autorizzazioni sono necessarie tooview testo della query.

## <a name="using-query-performance-insight"></a>Uso di Query Performance Insight
Informazioni dettagliate prestazioni query è facile toouse:

* Aprire [portale di Azure](https://portal.azure.com/) e database di ricerca che si desidera tooexamine. 
  * Dal menu a sinistra, sotto la sezione dedicata al supporto e alla risoluzione dei problemi, selezionare "Informazioni dettagliate sulle prestazioni delle query".
* Nella prima scheda hello, esaminare l'elenco di hello delle query più frequenti di consumo di risorse.
* Selezionare i dettagli di tooview una singola query.
* Aprire [SQL Azure Database Advisor](sql-database-advisor.md) e verificare se sono disponibili raccomandazioni.
* Utilizzare dispositivi di scorrimento Zoom avanti o indietro toochange icone osservati intervallo.
  
    ![dashboard prestazioni](./media/sql-database-query-performance/performance.png)

> [!NOTE]
> Un paio di ore di dati deve toobe acquisita dall'archivio Query per informazioni dettagliate prestazioni query di Database SQL tooprovide. Se il database di hello non contiene attività o archivio Query non era attivo durante un determinato periodo di tempo, grafici hello sarà vuoti per la visualizzazione di questo periodo di tempo. È possibile abilitare l'archivio query in qualsiasi momento, se non è in esecuzione.   
> 
> 

## <a name="review-top-cpu-consuming-queries"></a>Esaminare le query principali a livello di utilizzo di CPU
In hello [portale](http://portal.azure.com) hello seguenti:

1. Database SQL tooa e fare clic su **tutte le impostazioni** > **supporto + Troubleshooting** > **informazioni dettagliate prestazioni Query**. 
   
    ![Informazioni dettagliate prestazioni query][1]
   
    verrà visualizzata la visualizzazione di query superiore Hello e sono elencati hello principali della CPU dispendiosa in termini di query.
2. Fare clic su grafico hello per informazioni dettagliate.<br>Hello riga superiore mostra % complessivo di DTU per database hello, mentre le barre di hello indicano % della CPU utilizzate dalle query hello selezionato durante l'intervallo selezionato hello (ad esempio, se **settimana precedente** è selezionata ogni barra rappresenta un giorno).
   
    ![query principali][2]
   
    griglia inferiore Hello rappresenta informazioni aggregate per query visibile hello.
   
   * ID query: identificatore univoco di query all'interno del database.
   * Utilizzo della CPU per query durante l'intervallo osservabile (dipende dalla funzione di aggregazione).
   * Durata per ogni query (dipende dalla funzione di aggregazione).
   * Numero totale di esecuzioni per una query specifica.
     
     Selezionare o deselezionare singole query tooinclude o escluderli dal grafico hello utilizzando le caselle di controllo.
3. Se i dati non risulta più aggiornati, fare clic su hello **aggiornamento** pulsante.
4. È possibile usare dispositivi di scorrimento e intervallo di osservazione toochange pulsanti zoom e analizzare i picchi: ![impostazioni](./media/sql-database-query-performance/zoom.png)
5. Facoltativamente, se si desidera un'altra visualizzazione, è possibile selezionare la scheda **Personalizzata** e impostare:
   
   * Metrica (CPU, durata, conteggio delle esecuzioni)
   * Intervallo di tempo (ultime 24 ore, settimana scorsa, mese scorso). 
   * Numero di query.
   * Funzione di aggregazione.
     
     ![Impostazioni](./media/sql-database-query-performance/custom-tab.png)

## <a name="viewing-individual-query-details"></a>Visualizzazione dei dettagli delle singole query
dettagli di query tooview:

1. Fare clic su qualsiasi query elenco hello delle query più frequenti.
   
    ![informazioni dettagliate](./media/sql-database-query-performance/details.png)
2. verrà visualizzata la finestra di visualizzazione dei dettagli Hello e conteggio di utilizzo/Durata/esecuzione hello query della CPU è suddivisa nel tempo.
3. Fare clic su grafico hello per informazioni dettagliate.
   
   * Grafico superiore Mostra linea con % DTU complessivo del database e le barre di hello sono % della CPU utilizzata dalla query selezionata hello.
   * Secondo grafico mostra la durata totale dalla query selezionata hello.
   * Numero totale di esecuzioni inferiore mostra dalla query selezionata hello.
     
     ![dettagli sulle query][3]
4. Facoltativamente, utilizzare dispositivi di scorrimento, pulsanti di zoom oppure fare clic su **impostazioni** toocustomize modalità di visualizzazione dati di query o toopick un periodo di tempo diverso.

## <a name="review-top-queries-per-duration"></a>Esaminare le query principali in base alla durata
In hello recente aggiornamento di informazioni dettagliate prestazioni Query, è stata introdotta due nuove metriche che consentono di identificare potenziali colli di bottiglia: conteggio di durata e l'esecuzione.<br>

Query con esecuzione prolungata sono hello maggiori possibilità più risorse di blocco, blocco di altri utenti e limitare la scalabilità. Sono inoltre hello di candidati ottimali per l'ottimizzazione.<br>

tooidentify query a esecuzione prolungata:

1. Aprire la scheda **Personalizza** in Informazioni dettagliate sulle prestazioni delle query del database selezionato
2. Modificare le metriche toobe **durata**
3. Selezionare il numero di query e l'intervallo di osservazione
4. Selezionare la funzione di aggregazione
   
   * **Somma** aggiunge il tempo di esecuzione di tutte le query durante l'intero intervallo di osservazione.
   * **Max** individua le query con il tempo di esecuzione massimo durante l'intero intervallo di osservazione.
   * **AVG** rileva il tempo medio di esecuzione di tutte le esecuzioni di query e mostrano hello top fuori queste medie. 
     
     ![durata query][4]

## <a name="review-top-queries-per-execution-count"></a>Esaminare le query principali in base al conteggio delle esecuzioni
Il numero elevato di esecuzioni potrebbe non influire sul database e l'utilizzo delle risorse potrebbe essere modesto, ma l'applicazione nel suo complesso potrebbe risultare rallentata.

In alcuni casi, conteggio esecuzioni molto elevato può causare tooincrease di rete di andata e ritorno. I round trip hanno un forte impatto sulle prestazioni. Sono latenza toonetwork soggetto e latenza server toodownstream. 

Ad esempio, molti siti Web basati sui dati accedere frequentemente database hello per ogni richiesta dell'utente. Mentre il pool di connessioni consente, hello aumentato il traffico di rete e il carico di elaborazione nel server di database hello può influire negativamente sulle prestazioni.  Consigli di carattere generale sono tookeep round trip tooan minimo.

tooidentify eseguite di frequente query query ("chatty"):

1. Aprire la scheda **Personalizza** in Informazioni dettagliate sulle prestazioni delle query del database selezionato
2. Modificare le metriche toobe **conteggio esecuzioni**
3. Selezionare il numero di query e l'intervallo di osservazione
   
    ![conteggio delle esecuzioni query][5]

## <a name="understanding-performance-tuning-annotations"></a>Informazioni sulle annotazioni di ottimizzazione delle prestazioni
Durante l'esplorazione del carico di lavoro di informazioni dettagliate prestazioni Query, è possibile notare le icone con linea verticale nella parte superiore del grafico hello.<br>

Queste icone sono annotazioni sulle prestazioni che influiscono sulle azioni eseguite da [SQL Azure Database Advisor](sql-database-advisor.md). Per questa annotazione, si ottiene le informazioni di base sull'azione hello:

![annotazione query][6]

Se si desidera più tooknow o applica l'indicazione, fare clic sull'icona di hello. in modo da visualizzare i dettagli relativi all'azione.  Se si tratta di un consiglio attivo è possibile applicarlo direttamente tramite il comando.

![dettagli annotazione query][7]

### <a name="multiple-annotations"></a>Annotazioni multiple.
È possibile, che a causa di livello di zoom, le annotazioni che sono Chiudi tooeach altri verranno ottenere compresso in un unico. che verrà rappresentato dall'icona speciale; facendo clic su tale icona si aprirà un nuovo pannello con l'elenco delle annotazioni raggruppate.
Correlazione di query e le azioni di ottimizzazione delle prestazioni può comprendere toobetter il carico di lavoro. 

## <a name="optimizing-hello-query-store-configuration-for-query-performance-insight"></a>Ottimizzazione della configurazione di archivio Query hello per informazioni dettagliate prestazioni Query
Durante l'uso di informazioni dettagliate prestazioni Query, possono verificarsi hello messaggi dell'archivio di Query seguente:

* "Archivio query non è correttamente configurato in questo database. Fare clic qui ulteriori toolearn."
* "Archivio query non è correttamente configurato in questo database. Fare clic qui impostazioni toochange." 

Questi messaggi vengono visualizzati in genere quando l'archivio Query non è in grado di toocollect nuovi dati. 

Il primo caso si verifica quando l'archivio query è in stato di sola lettura e i parametri sono impostati in modo ottimale. È possibile risolvere il problema aumentando le dimensioni dell'archivio query o svuotandolo del tutto.

![pulsante qds][8]

Il secondo caso si verifica quando l'archivio query è disattivato o se i parametri non sono impostati in modo ottimale. <br>È possibile modificare hello acquisizione e memorizzazione dei criteri e abilitare archivio Query eseguendo i comandi riportati di seguito o direttamente dal portale:

![pulsante qds][9]

### <a name="recommended-retention-and-capture-policy"></a>Criteri di conservazione e acquisizione consigliati
Esistono due tipi di criteri di conservazione:

* Dimensioni basate - se viene raggiunto tooAUTO set eseguirà la pulizia dati automaticamente in prossimità di dimensioni massime.
* Tempo basata - per impostazione predefinita, si imposterà too30 giorni, vale a dire che, se l'archivio Query esaurirà lo spazio, verranno eliminati, eseguire query sulle informazioni più vecchi di 30 giorni

I criteri di acquisizione possono essere impostati su:

* **Tutte**: acquisisce tutte le query.
* **Automatico**: le query poco frequenti e con durata di compilazione ed esecuzione trascurabile vengono ignorate. Le soglie per il conteggio delle esecuzioni e la durata di compilazione ed esecuzione vengono stabilite internamente. Questo è l'opzione predefinita di hello.
* **Nessuna**: l'archivio query interrompe l'acquisizione di nuove query, ma continua a raccogliere le statistiche di runtime per le query già acquisite.

È consigliabile impostare tutti i criteri tooAUTO e criteri pulita too30 giorni:

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (SIZE_BASED_CLEANUP_MODE = AUTO);

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 30));

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (QUERY_CAPTURE_MODE = AUTO);

Aumentare le dimensioni dell'archivio query. Potrebbe trattarsi di operazione eseguita dal database tooa connessione ed emettere query riportata di seguito:

    ALTER DATABASE [YourDB]
    SET QUERY_STORE (MAX_STORAGE_SIZE_MB = 1024);

Applicazione di queste impostazioni eventualmente renderà archivio Query, la raccolta di nuove query, tuttavia, se non si desidera toowait è possibile cancellare l'archivio Query. 

> [!NOTE]
> Esecuzione della query seguente eliminerà tutte le informazioni correnti in hello archivio Query. 
> 
> 

    ALTER DATABASE [YourDB] SET QUERY_STORE CLEAR;


## <a name="summary"></a>Riepilogo
Informazioni dettagliate prestazioni query consente di comprendere l'impatto di hello query del carico di lavoro e l'interrelazione toodatabase consumo delle risorse. Con questa funzionalità, si verrà apprendere top hello query per consumo e identificare facilmente quelli hello toofix prima che diventino un problema.

## <a name="next-steps"></a>Passaggi successivi
Per altre indicazioni sull'ottimizzazione delle prestazioni di hello del database SQL, fare clic su [indicazioni](sql-database-advisor.md) su hello **informazioni dettagliate prestazioni Query** blade.

![Performance Advisor](./media/sql-database-query-performance/ia.png)

<!--Image references-->
[1]: ./media/sql-database-query-performance/tile.png
[2]: ./media/sql-database-query-performance/top-queries.png
[3]: ./media/sql-database-query-performance/query-details.png
[4]: ./media/sql-database-query-performance/top-duration.png
[5]: ./media/sql-database-query-performance/top-execution.png
[6]: ./media/sql-database-query-performance/annotation.png
[7]: ./media/sql-database-query-performance/annotation-details.png
[8]: ./media/sql-database-query-performance/qds-off.png
[9]: ./media/sql-database-query-performance/qds-button.png

