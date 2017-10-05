---
title: Informazioni dettagliate sulle prestazioni delle query per il database SQL di Azure | Documentazione Microsoft
description: Il monitoraggio delle prestazioni delle query identifica le query principali a livello di utilizzo di CPU per un database SQL di Azure.
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
ms.openlocfilehash: 1925d4ff8f5b16a0df56de987f8653cfd8441c52
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-sql-database-query-performance-insight"></a><span data-ttu-id="b3869-103">Query Performance Insight del database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="b3869-103">Azure SQL Database Query Performance Insight</span></span>
<span data-ttu-id="b3869-104">La gestione e l'ottimizzazione delle prestazioni dei database relazionali è un'attività complessa che richiede un'esperienza significativa e un investimento elevato in termini di tempo.</span><span class="sxs-lookup"><span data-stu-id="b3869-104">Managing and tuning the performance of relational databases is a challenging task that requires significant expertise and time investment.</span></span> <span data-ttu-id="b3869-105">Le Informazioni dettagliate sulle prestazioni delle query consentono di dedicare meno tempo alla risoluzione dei problemi delle prestazioni del database, offrendo i vantaggi seguenti:​</span><span class="sxs-lookup"><span data-stu-id="b3869-105">Query Performance Insight allows you to spend less time troubleshooting database performance by providing the following:</span></span>

* <span data-ttu-id="b3869-106">Informazioni più approfondite sull'utilizzo delle risorse del database (DTU).</span><span class="sxs-lookup"><span data-stu-id="b3869-106">Deeper insight into your databases resource (DTU) consumption.</span></span> 
* <span data-ttu-id="b3869-107">Query principali a livello di CPU/durata/conteggio delle esecuzioni, che possono essere potenzialmente ottimizzate per migliorare le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="b3869-107">The top queries by CPU/Duration/Execution count, which can potentially be tuned for improved performance.</span></span>
* <span data-ttu-id="b3869-108">La possibilità di eseguire il drill-down nei dettagli di una query, visualizzarne il testo e la cronologia di utilizzo delle risorse.</span><span class="sxs-lookup"><span data-stu-id="b3869-108">The ability to drill down into the details of a query, view its text and history of resource utilization.</span></span> 
* <span data-ttu-id="b3869-109">Le annotazioni relative all'ottimizzazione delle prestazioni che descrivono le azioni eseguite da [SQL Azure Database Advisor](sql-database-advisor.md)</span><span class="sxs-lookup"><span data-stu-id="b3869-109">Performance tuning annotations that show actions performed by [SQL Azure Database Advisor](sql-database-advisor.md)</span></span>  



## <a name="prerequisites"></a><span data-ttu-id="b3869-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b3869-110">Prerequisites</span></span>
* <span data-ttu-id="b3869-111">Per Informazioni dettagliate sulle prestazioni delle query è necessario che l' [archivio query](https://msdn.microsoft.com/library/dn817826.aspx) sia attivo nel database.</span><span class="sxs-lookup"><span data-stu-id="b3869-111">Query Performance Insight requires that [Query Store](https://msdn.microsoft.com/library/dn817826.aspx) is active on your database.</span></span> <span data-ttu-id="b3869-112">Se l'archivio query non è in esecuzione, il portale richiede di attivarlo.</span><span class="sxs-lookup"><span data-stu-id="b3869-112">If Query Store is not running, the portal prompts you to turn it on.</span></span>

## <a name="permissions"></a><span data-ttu-id="b3869-113">Autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="b3869-113">Permissions</span></span>
<span data-ttu-id="b3869-114">Le autorizzazioni di [controllo degli accessi in base al ruolo](../active-directory/role-based-access-control-what-is.md) seguenti sono necessarie per usare Query Performance Insight:</span><span class="sxs-lookup"><span data-stu-id="b3869-114">The following [role-based access control](../active-directory/role-based-access-control-what-is.md) permissions are required to use Query Performance Insight:</span></span> 

* <span data-ttu-id="b3869-115">Le autorizzazioni **Lettore**, **Proprietario**, **Collaboratore**, **Collaboratore database SQL** o **Collaboratore SQL Server** sono necessarie per visualizzare le query principali che usano le risorse e i grafici.</span><span class="sxs-lookup"><span data-stu-id="b3869-115">**Reader**, **Owner**, **Contributor**, **SQL DB Contributor**, or **SQL Server Contributor** permissions are required to view the top resource consuming queries and charts.</span></span> 
* <span data-ttu-id="b3869-116">Le autorizzazioni **Proprietario**, **Collaboratore**, **Collaboratore database SQL** o **Collaboratore SQL Server** sono necessarie per visualizzare il testo della query.</span><span class="sxs-lookup"><span data-stu-id="b3869-116">**Owner**, **Contributor**, **SQL DB Contributor**, or **SQL Server Contributor** permissions are required to view query text.</span></span>

## <a name="using-query-performance-insight"></a><span data-ttu-id="b3869-117">Uso di Query Performance Insight</span><span class="sxs-lookup"><span data-stu-id="b3869-117">Using Query Performance Insight</span></span>
<span data-ttu-id="b3869-118">Query Performance Insight è facile da usare:</span><span class="sxs-lookup"><span data-stu-id="b3869-118">Query Performance Insight is easy to use:</span></span>

* <span data-ttu-id="b3869-119">Aprire il [portale di Azure](https://portal.azure.com/) e individuare il database che si desidera esaminare.</span><span class="sxs-lookup"><span data-stu-id="b3869-119">Open [Azure portal](https://portal.azure.com/) and find database that you want to examine.</span></span> 
  * <span data-ttu-id="b3869-120">Dal menu a sinistra, sotto la sezione dedicata al supporto e alla risoluzione dei problemi, selezionare "Informazioni dettagliate sulle prestazioni delle query".</span><span class="sxs-lookup"><span data-stu-id="b3869-120">From left-hand side menu, under support and troubleshooting, select “Query Performance Insight”.</span></span>
* <span data-ttu-id="b3869-121">Nella prima scheda, esaminare l'elenco delle query principali a livello di utilizzo delle risorse.</span><span class="sxs-lookup"><span data-stu-id="b3869-121">On the first tab, review the list of top resource-consuming queries.</span></span>
* <span data-ttu-id="b3869-122">Selezionare una singola query per visualizzarne i dettagli.</span><span class="sxs-lookup"><span data-stu-id="b3869-122">Select an individual query to view its details.</span></span>
* <span data-ttu-id="b3869-123">Aprire [SQL Azure Database Advisor](sql-database-advisor.md) e verificare se sono disponibili raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="b3869-123">Open [SQL Azure Database Advisor](sql-database-advisor.md) and check if any recommendations are available.</span></span>
* <span data-ttu-id="b3869-124">Utilizzare i dispositivi di scorrimento o le icone dello zoom per modificare l'intervallo osservato.</span><span class="sxs-lookup"><span data-stu-id="b3869-124">Use sliders or zoom icons to change observed interval.</span></span>
  
    ![dashboard prestazioni](./media/sql-database-query-performance/performance.png)

> [!NOTE]
> <span data-ttu-id="b3869-126">Per consentire al database SQL di fornire informazioni dettagliate sulle prestazioni delle query, è necessario che l'archivio query acquisisca un paio di ore di dati.</span><span class="sxs-lookup"><span data-stu-id="b3869-126">A couple hours of data needs to be captured by Query Store for SQL Database to provide query performance insights.</span></span> <span data-ttu-id="b3869-127">Se il database non ha alcuna attività o l'archivio query non è attivo in un determinato periodo di tempo, i grafici saranno vuoti quando viene visualizzato quel periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="b3869-127">If the database has no activity or Query Store was not active during a certain time period, the charts will be empty when displaying that time period.</span></span> <span data-ttu-id="b3869-128">È possibile abilitare l'archivio query in qualsiasi momento, se non è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="b3869-128">You may enable Query Store at any time if it is not running.</span></span>   
> 
> 

## <a name="review-top-cpu-consuming-queries"></a><span data-ttu-id="b3869-129">Esaminare le query principali a livello di utilizzo di CPU</span><span class="sxs-lookup"><span data-stu-id="b3869-129">Review top CPU consuming queries</span></span>
<span data-ttu-id="b3869-130">Eseguire le operazioni seguenti nel [portale](http://portal.azure.com) :</span><span class="sxs-lookup"><span data-stu-id="b3869-130">In the [portal](http://portal.azure.com) do the following:</span></span>

1. <span data-ttu-id="b3869-131">Passare a un database SQL e fare clic su **Tutte le impostazioni** > **Supporto e risoluzione dei problemi** > **Informazioni dettagliate prestazioni query**.</span><span class="sxs-lookup"><span data-stu-id="b3869-131">Browse to a SQL database and click **All settings** > **Support + Troubleshooting** > **Query performance insight**.</span></span> 
   
    ![Informazioni dettagliate sulle prestazioni delle query][1]
   
    <span data-ttu-id="b3869-133">Verrà aperta la visualizzazione relativa alle query principali e verrà mostrato l'elenco delle query principali a livello di utilizzo di CPU.</span><span class="sxs-lookup"><span data-stu-id="b3869-133">The top queries view opens and the top CPU consuming queries are listed.</span></span>
2. <span data-ttu-id="b3869-134">Per informazioni dettagliate, fare clic nei vari punti del grafico.</span><span class="sxs-lookup"><span data-stu-id="b3869-134">Click around the chart for details.</span></span><br><span data-ttu-id="b3869-135">La prima riga visualizza la percentuale di uso di DTU complessiva per il database, mentre le barre visualizzano la percentuale di CPU usata dalle query selezionate durante l'intervallo selezionato (ad esempio, se si seleziona **Settimana precedente** ogni barra rappresenta un giorno).</span><span class="sxs-lookup"><span data-stu-id="b3869-135">The top line shows overall DTU% for the database, while the bars show CPU% consumed by the selected queries during the selected interval (for example, if **Past week** is selected each bar represents one day).</span></span>
   
    ![query principali][2]
   
    <span data-ttu-id="b3869-137">La griglia inferiore rappresenta informazioni aggregate per le query visibili.</span><span class="sxs-lookup"><span data-stu-id="b3869-137">The bottom grid represents aggregated information for the visible queries.</span></span>
   
   * <span data-ttu-id="b3869-138">ID query: identificatore univoco di query all'interno del database.</span><span class="sxs-lookup"><span data-stu-id="b3869-138">Query ID - unique identifier of query inside database.</span></span>
   * <span data-ttu-id="b3869-139">Utilizzo della CPU per query durante l'intervallo osservabile (dipende dalla funzione di aggregazione).</span><span class="sxs-lookup"><span data-stu-id="b3869-139">CPU per query during observable interval (depends on aggregation function).</span></span>
   * <span data-ttu-id="b3869-140">Durata per ogni query (dipende dalla funzione di aggregazione).</span><span class="sxs-lookup"><span data-stu-id="b3869-140">Duration per query (depends on aggregation function).</span></span>
   * <span data-ttu-id="b3869-141">Numero totale di esecuzioni per una query specifica.</span><span class="sxs-lookup"><span data-stu-id="b3869-141">Total number of executions for a particular query.</span></span>
     
     <span data-ttu-id="b3869-142">Selezionare o deselezionare singole query per includerle o escluderle dal grafico utilizzando le caselle di spunta.</span><span class="sxs-lookup"><span data-stu-id="b3869-142">Select or clear individual queries to include or exclude them from the chart using checkboxes.</span></span>
3. <span data-ttu-id="b3869-143">Se i dati non vengono più aggiornati, fare clic sul pulsante **Aggiorna** .</span><span class="sxs-lookup"><span data-stu-id="b3869-143">If your data becomes stale, click the **Refresh** button.</span></span>
4. <span data-ttu-id="b3869-144">È possibile usare i dispositivi di scorrimento e i pulsanti dello zoom per modificare l'intervallo di osservazione ed esaminare i picchi: ![impostazioni](./media/sql-database-query-performance/zoom.png)</span><span class="sxs-lookup"><span data-stu-id="b3869-144">You can use sliders and zoom buttons to change observation interval and investigate spikes:  ![settings](./media/sql-database-query-performance/zoom.png)</span></span>
5. <span data-ttu-id="b3869-145">Facoltativamente, se si desidera un'altra visualizzazione, è possibile selezionare la scheda **Personalizzata** e impostare:</span><span class="sxs-lookup"><span data-stu-id="b3869-145">Optionally, if you want a different view, you can select **Custom** tab and set:</span></span>
   
   * <span data-ttu-id="b3869-146">Metrica (CPU, durata, conteggio delle esecuzioni)</span><span class="sxs-lookup"><span data-stu-id="b3869-146">Metric (CPU, duration, execution count)</span></span>
   * <span data-ttu-id="b3869-147">Intervallo di tempo (ultime 24 ore, settimana scorsa, mese scorso).</span><span class="sxs-lookup"><span data-stu-id="b3869-147">Time interval (Last 24 hours, Past week, Past month).</span></span> 
   * <span data-ttu-id="b3869-148">Numero di query.</span><span class="sxs-lookup"><span data-stu-id="b3869-148">Number of queries.</span></span>
   * <span data-ttu-id="b3869-149">Funzione di aggregazione.</span><span class="sxs-lookup"><span data-stu-id="b3869-149">Aggregation function.</span></span>
     
     ![Impostazioni](./media/sql-database-query-performance/custom-tab.png)

## <a name="viewing-individual-query-details"></a><span data-ttu-id="b3869-151">Visualizzazione dei dettagli delle singole query</span><span class="sxs-lookup"><span data-stu-id="b3869-151">Viewing individual query details</span></span>
<span data-ttu-id="b3869-152">Per visualizzare i dettagli relativi alle query:</span><span class="sxs-lookup"><span data-stu-id="b3869-152">To view query details:</span></span>

1. <span data-ttu-id="b3869-153">Fare clic su qualsiasi query nell'elenco delle query principali.</span><span class="sxs-lookup"><span data-stu-id="b3869-153">Click any query in the list of top queries.</span></span>
   
    ![informazioni dettagliate](./media/sql-database-query-performance/details.png)
2. <span data-ttu-id="b3869-155">Verrà aperta la visualizzazione dettagliata e i valori relativi a utilizzo CPU/durata/conteggio delle esecuzioni delle query verranno suddiviso nel tempo.</span><span class="sxs-lookup"><span data-stu-id="b3869-155">The details view opens and the queries CPU consumption/Duration/Execution count is broken down over time.</span></span>
3. <span data-ttu-id="b3869-156">Per informazioni dettagliate, fare clic nei vari punti del grafico.</span><span class="sxs-lookup"><span data-stu-id="b3869-156">Click around the chart for details.</span></span>
   
   * <span data-ttu-id="b3869-157">Il grafico in altomMostra una linea con la percentuale % DTU complessiva del database e le barre rappresentano la percentuale % della CPU utilizzata dalla query selezionata.</span><span class="sxs-lookup"><span data-stu-id="b3869-157">Top chart shows line with overall database DTU%, and the bars are CPU% consumed by the selected query.</span></span>
   * <span data-ttu-id="b3869-158">Nel secondo grafico viene mostrata la durata totale della query selezionata.</span><span class="sxs-lookup"><span data-stu-id="b3869-158">Second chart shows total duration by the selected query.</span></span>
   * <span data-ttu-id="b3869-159">Nel grafico in fondo viene mostrato il numero totale delle esecuzioni effettuate dalla query selezionata.</span><span class="sxs-lookup"><span data-stu-id="b3869-159">Bottom chart shows total number of executions by the selected query.</span></span>
     
     ![dettagli sulle query][3]
4. <span data-ttu-id="b3869-161">Facoltativamente, utilizzare i dispositivi di scorrimento, i pulsanti dello zoom oppure fare clic su **Impostazioni** per personalizzare la modalità di visualizzazione dei dati della query o per mostrare un periodo di tempo diverso.</span><span class="sxs-lookup"><span data-stu-id="b3869-161">Optionally, use sliders, zoom buttons or click **Settings** to customize how query data is displayed, or to pick a different time period.</span></span>

## <a name="review-top-queries-per-duration"></a><span data-ttu-id="b3869-162">Esaminare le query principali in base alla durata</span><span class="sxs-lookup"><span data-stu-id="b3869-162">Review top queries per duration</span></span>
<span data-ttu-id="b3869-163">Nel recente aggiornamento di Informazioni dettagliate sulle prestazioni delle query, abbiamo introdotto due nuove metriche che aiutano a individuare potenziali colli di bottiglia: conteggio delle esecuzioni e durata.</span><span class="sxs-lookup"><span data-stu-id="b3869-163">In the recent update of Query Performance Insight, we introduced two new metrics that can help you identify potential bottlenecks: duration and execution count.</span></span><br>

<span data-ttu-id="b3869-164">Le query con esecuzione prolungata hanno le maggiori probabilità di bloccare gli altri utenti e le risorse più a lungo, nonché di limitare la scalabilità.</span><span class="sxs-lookup"><span data-stu-id="b3869-164">Long-running queries have the greatest potential for locking resources longer, blocking other users, and limiting scalability.</span></span> <span data-ttu-id="b3869-165">Sono anche i candidati ideali per l'ottimizzazione.</span><span class="sxs-lookup"><span data-stu-id="b3869-165">They are also the best candidates for optimization.</span></span><br>

<span data-ttu-id="b3869-166">Per identificare le query di lunga esecuzione :</span><span class="sxs-lookup"><span data-stu-id="b3869-166">To identify long running queries:</span></span>

1. <span data-ttu-id="b3869-167">Aprire la scheda **Personalizza** in Informazioni dettagliate sulle prestazioni delle query del database selezionato</span><span class="sxs-lookup"><span data-stu-id="b3869-167">Open **Custom** tab in Query Performance Insight for selected database</span></span>
2. <span data-ttu-id="b3869-168">Modificare le metriche su **Durata**</span><span class="sxs-lookup"><span data-stu-id="b3869-168">Change metrics to be **duration**</span></span>
3. <span data-ttu-id="b3869-169">Selezionare il numero di query e l'intervallo di osservazione</span><span class="sxs-lookup"><span data-stu-id="b3869-169">Select number of queries and observation interval</span></span>
4. <span data-ttu-id="b3869-170">Selezionare la funzione di aggregazione</span><span class="sxs-lookup"><span data-stu-id="b3869-170">Select aggregation function</span></span>
   
   * <span data-ttu-id="b3869-171">**Somma** aggiunge il tempo di esecuzione di tutte le query durante l'intero intervallo di osservazione.</span><span class="sxs-lookup"><span data-stu-id="b3869-171">**Sum** adds up all query execution time during whole observation interval.</span></span>
   * <span data-ttu-id="b3869-172">**Max** individua le query con il tempo di esecuzione massimo durante l'intero intervallo di osservazione.</span><span class="sxs-lookup"><span data-stu-id="b3869-172">**Max** finds queries which execution time was maximum at whole observation interval.</span></span>
   * <span data-ttu-id="b3869-173">**Media** rileva il tempo medio di esecuzione di tutte le query e mostra i valori medi più alti tra quelli rilevati.</span><span class="sxs-lookup"><span data-stu-id="b3869-173">**Avg** finds average execution time of all query executions and show you the top out of these averages.</span></span> 
     
     ![durata query][4]

## <a name="review-top-queries-per-execution-count"></a><span data-ttu-id="b3869-175">Esaminare le query principali in base al conteggio delle esecuzioni</span><span class="sxs-lookup"><span data-stu-id="b3869-175">Review top queries per execution count</span></span>
<span data-ttu-id="b3869-176">Il numero elevato di esecuzioni potrebbe non influire sul database e l'utilizzo delle risorse potrebbe essere modesto, ma l'applicazione nel suo complesso potrebbe risultare rallentata.</span><span class="sxs-lookup"><span data-stu-id="b3869-176">High number of executions might not be affecting database itself and resources usage can be low, but overall application might get slow.</span></span>

<span data-ttu-id="b3869-177">In alcuni casi, il conteggio di esecuzioni molto elevato potrebbe causare l'aumento dei round trip di rete.</span><span class="sxs-lookup"><span data-stu-id="b3869-177">In some cases, very high execution count may lead to increase of network round trips.</span></span> <span data-ttu-id="b3869-178">I round trip hanno un forte impatto sulle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="b3869-178">Round trips significantly affect performance.</span></span> <span data-ttu-id="b3869-179">Sono soggetti alla latenza di rete e alla latenza di server downstream.</span><span class="sxs-lookup"><span data-stu-id="b3869-179">They are subject to network latency and to downstream server latency.</span></span> 

<span data-ttu-id="b3869-180">Ad esempio, molti siti Web basati sui dati accedono in maniera massiccia al database per tutte le richieste dell'utente.</span><span class="sxs-lookup"><span data-stu-id="b3869-180">For example, many data-driven Web sites heavily access the database for every user request.</span></span> <span data-ttu-id="b3869-181">Mentre il pool di connessioni è di supporto, il traffico di rete aumentato e il carico di elaborazione sul server di database possono influire negativamente sulle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="b3869-181">While connection pooling helps, the increased network traffic and processing load on the database server can adversely affect performance.</span></span>  <span data-ttu-id="b3869-182">Il consiglio generico è di mantenere i round trip a un livello minimo assoluto.</span><span class="sxs-lookup"><span data-stu-id="b3869-182">General advice is to keep round trips to an absolute minimum.</span></span>

<span data-ttu-id="b3869-183">Per identificare le query eseguite di frequente ("chatty"):</span><span class="sxs-lookup"><span data-stu-id="b3869-183">To identify frequently executed queries (“chatty”) queries:</span></span>

1. <span data-ttu-id="b3869-184">Aprire la scheda **Personalizza** in Informazioni dettagliate sulle prestazioni delle query del database selezionato</span><span class="sxs-lookup"><span data-stu-id="b3869-184">Open **Custom** tab in Query Performance Insight for selected database</span></span>
2. <span data-ttu-id="b3869-185">Modificare le metriche su **Conteggio delle esecuzioni**</span><span class="sxs-lookup"><span data-stu-id="b3869-185">Change metrics to be **execution count**</span></span>
3. <span data-ttu-id="b3869-186">Selezionare il numero di query e l'intervallo di osservazione</span><span class="sxs-lookup"><span data-stu-id="b3869-186">Select number of queries and observation interval</span></span>
   
    ![conteggio delle esecuzioni query][5]

## <a name="understanding-performance-tuning-annotations"></a><span data-ttu-id="b3869-188">Informazioni sulle annotazioni di ottimizzazione delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="b3869-188">Understanding performance tuning annotations</span></span>
<span data-ttu-id="b3869-189">Durante l'esplorazione del carico di lavoro in Informazioni dettagliate sulle prestazioni delle query, è possibile notare la presenza di icone con linea verticale nella parte superiore del grafico.</span><span class="sxs-lookup"><span data-stu-id="b3869-189">While exploring your workload in Query Performance Insight, you might notice icons with vertical line on top of the chart.</span></span><br>

<span data-ttu-id="b3869-190">Queste icone sono annotazioni sulle prestazioni che influiscono sulle azioni eseguite da [SQL Azure Database Advisor](sql-database-advisor.md).</span><span class="sxs-lookup"><span data-stu-id="b3869-190">These icons are annotations; they represent performance affecting actions performed by [SQL Azure Database Advisor](sql-database-advisor.md).</span></span> <span data-ttu-id="b3869-191">Passando il cursore del mouse su un'annotazione, si ottengono le informazioni di base relative a tale azione:</span><span class="sxs-lookup"><span data-stu-id="b3869-191">By hovering annotation, you get basic information about the action:</span></span>

![annotazione query][6]

<span data-ttu-id="b3869-193">Per saperne di più o per applicare il consiglio di SQL Azure Database Advisor, fare clic sull'icona,</span><span class="sxs-lookup"><span data-stu-id="b3869-193">If you want to know more or apply advisor recommendation, click the icon.</span></span> <span data-ttu-id="b3869-194">in modo da visualizzare i dettagli relativi all'azione. </span><span class="sxs-lookup"><span data-stu-id="b3869-194">It will open details of action.</span></span> <span data-ttu-id="b3869-195">Se si tratta di un consiglio attivo è possibile applicarlo direttamente tramite il comando.</span><span class="sxs-lookup"><span data-stu-id="b3869-195">If it’s an active recommendation you can apply it straight away using command.</span></span>

![dettagli annotazione query][7]

### <a name="multiple-annotations"></a><span data-ttu-id="b3869-197">Annotazioni multiple.</span><span class="sxs-lookup"><span data-stu-id="b3869-197">Multiple annotations.</span></span>
<span data-ttu-id="b3869-198">È possibile che a causa del livello di zoom le annotazioni vicine tra loro vengano compresse in una,</span><span class="sxs-lookup"><span data-stu-id="b3869-198">It’s possible, that because of zoom level, annotations that are close to each other will get collapsed into one.</span></span> <span data-ttu-id="b3869-199">che verrà rappresentato dall'icona speciale; facendo clic su tale icona si aprirà un nuovo pannello con l'elenco delle annotazioni raggruppate.</span><span class="sxs-lookup"><span data-stu-id="b3869-199">This will be represented by special icon, clicking it will open new blade where list of grouped annotations will be shown.</span></span>
<span data-ttu-id="b3869-200">Correlare le query e le azioni di ottimizzazione delle prestazioni può servire ad avere una migliore comprensione del carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="b3869-200">Correlating queries and performance tuning actions can help to better understand your workload.</span></span> 

## <a name="optimizing-the-query-store-configuration-for-query-performance-insight"></a><span data-ttu-id="b3869-201">Ottimizzare la configurazione dell'archivio query per Informazioni dettagliate prestazioni query</span><span class="sxs-lookup"><span data-stu-id="b3869-201">Optimizing the Query Store configuration for Query Performance Insight</span></span>
<span data-ttu-id="b3869-202">Durante l'uso di Informazioni dettagliate prestazioni query, possono essere visualizzati messaggi dell'archivio query simili ai seguenti:</span><span class="sxs-lookup"><span data-stu-id="b3869-202">During your use of Query Performance Insight, you might encounter the following Query Store messages:</span></span>

* <span data-ttu-id="b3869-203">"Archivio query non è correttamente configurato in questo database.</span><span class="sxs-lookup"><span data-stu-id="b3869-203">"Query Store is not properly configured on this database.</span></span> <span data-ttu-id="b3869-204">Per altre informazioni, fare clic qui."</span><span class="sxs-lookup"><span data-stu-id="b3869-204">Click here to learn more."</span></span>
* <span data-ttu-id="b3869-205">"Archivio query non è correttamente configurato in questo database.</span><span class="sxs-lookup"><span data-stu-id="b3869-205">"Query Store is not properly configured on this database.</span></span> <span data-ttu-id="b3869-206">Fare clic qui per modificare le impostazioni."</span><span class="sxs-lookup"><span data-stu-id="b3869-206">Click here to change settings."</span></span> 

<span data-ttu-id="b3869-207">Questi messaggi in genere vengono visualizzati quando l'archivio query non è in grado di raccogliere nuovi dati.</span><span class="sxs-lookup"><span data-stu-id="b3869-207">These messages usually appear when Query Store is not able to collect new data.</span></span> 

<span data-ttu-id="b3869-208">Il primo caso si verifica quando l'archivio query è in stato di sola lettura e i parametri sono impostati in modo ottimale.</span><span class="sxs-lookup"><span data-stu-id="b3869-208">First case happens when Query Store is in Read-Only state and parameters are set optimally.</span></span> <span data-ttu-id="b3869-209">È possibile risolvere il problema aumentando le dimensioni dell'archivio query o svuotandolo del tutto.</span><span class="sxs-lookup"><span data-stu-id="b3869-209">You can fix this by increasing size of Query Store or clearing Query Store.</span></span>

![pulsante qds][8]

<span data-ttu-id="b3869-211">Il secondo caso si verifica quando l'archivio query è disattivato o se i parametri non sono impostati in modo ottimale.</span><span class="sxs-lookup"><span data-stu-id="b3869-211">Second case happens when Query Store is Off or parameters aren’t set optimally.</span></span> <br><span data-ttu-id="b3869-212">È possibile modificare i criteri di conservazione e acquisizione e abilitare l'archivio query direttamente dal portale oppure eseguendo i comandi indicati sotto:</span><span class="sxs-lookup"><span data-stu-id="b3869-212">You can change the Retention and Capture policy and enable Query Store by executing commands below or directly from portal:</span></span>

![pulsante qds][9]

### <a name="recommended-retention-and-capture-policy"></a><span data-ttu-id="b3869-214">Criteri di conservazione e acquisizione consigliati</span><span class="sxs-lookup"><span data-stu-id="b3869-214">Recommended retention and capture policy</span></span>
<span data-ttu-id="b3869-215">Esistono due tipi di criteri di conservazione:</span><span class="sxs-lookup"><span data-stu-id="b3869-215">There are two types of retention policies:</span></span>

* <span data-ttu-id="b3869-216">Basati sulle dimensioni: se impostati su AUTOMATICO i dati verranno automaticamente cancellati al raggiungimento delle dimensioni massime.</span><span class="sxs-lookup"><span data-stu-id="b3869-216">Size based - if set to AUTO it will clean data automatically when near max size is reached.</span></span>
* <span data-ttu-id="b3869-217">Basati sul tempo: per impostazione predefinita verranno impostati su 30 giorni in modo tale che, se verrà esaurito lo spazio, l'archivio query eliminerà le informazioni di query antecedenti a 30 giorni</span><span class="sxs-lookup"><span data-stu-id="b3869-217">Time based - by default we will set it to 30 days, which means, if Query Store will run out of space, it will delete query information older than 30 days</span></span>

<span data-ttu-id="b3869-218">I criteri di acquisizione possono essere impostati su:</span><span class="sxs-lookup"><span data-stu-id="b3869-218">Capture policy could be set to:</span></span>

* <span data-ttu-id="b3869-219">**Tutte**: acquisisce tutte le query.</span><span class="sxs-lookup"><span data-stu-id="b3869-219">**All** - Captures all queries.</span></span>
* <span data-ttu-id="b3869-220">**Automatico**: le query poco frequenti e con durata di compilazione ed esecuzione trascurabile vengono ignorate.</span><span class="sxs-lookup"><span data-stu-id="b3869-220">**Auto** - Infrequent queries and queries with insignificant compile and execution duration are ignored.</span></span> <span data-ttu-id="b3869-221">Le soglie per il conteggio delle esecuzioni e la durata di compilazione ed esecuzione vengono stabilite internamente.</span><span class="sxs-lookup"><span data-stu-id="b3869-221">Thresholds for execution count, compile and runtime duration are internally determined.</span></span> <span data-ttu-id="b3869-222">Questa è l'opzione predefinita.</span><span class="sxs-lookup"><span data-stu-id="b3869-222">This is the default option.</span></span>
* <span data-ttu-id="b3869-223">**Nessuna**: l'archivio query interrompe l'acquisizione di nuove query, ma continua a raccogliere le statistiche di runtime per le query già acquisite.</span><span class="sxs-lookup"><span data-stu-id="b3869-223">**None** - Query Store stops capturing new queries, however runtime stats for already captured queries are still collected.</span></span>

<span data-ttu-id="b3869-224">È consigliabile impostare tutti i criteri su AUTOMATICO e i criteri di pulizia dei dati su 30 giorni:</span><span class="sxs-lookup"><span data-stu-id="b3869-224">We recommend setting all policies to AUTO and clean policy to 30 days:</span></span>

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (SIZE_BASED_CLEANUP_MODE = AUTO);

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 30));

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (QUERY_CAPTURE_MODE = AUTO);

<span data-ttu-id="b3869-225">Aumentare le dimensioni dell'archivio query.</span><span class="sxs-lookup"><span data-stu-id="b3869-225">Increase size of Query Store.</span></span> <span data-ttu-id="b3869-226">È possibile eseguire questa operazione connettendosi a un database ed eseguendo la query seguente:</span><span class="sxs-lookup"><span data-stu-id="b3869-226">This could be performed by connecting to a database and issuing following query:</span></span>

    ALTER DATABASE [YourDB]
    SET QUERY_STORE (MAX_STORAGE_SIZE_MB = 1024);

<span data-ttu-id="b3869-227">L'applicazione di queste impostazioni porterà l'archivio query a raccogliere nuove query; tuttavia, se non si desidera aspettare è possibile svuotare l'archivio query.</span><span class="sxs-lookup"><span data-stu-id="b3869-227">Applying these settings will eventually make Query Store collecting new queries, however if you don’t want to wait you can clear Query Store.</span></span> 

> [!NOTE]
> <span data-ttu-id="b3869-228">L'esecuzione della query seguente comporta l'eliminazione di tutte le informazioni correnti nell'archivio query.</span><span class="sxs-lookup"><span data-stu-id="b3869-228">Executing following query will delete all current information in the Query Store.</span></span> 
> 
> 

    ALTER DATABASE [YourDB] SET QUERY_STORE CLEAR;


## <a name="summary"></a><span data-ttu-id="b3869-229">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="b3869-229">Summary</span></span>
<span data-ttu-id="b3869-230">Query Performance Insight semplifica la comprensione dell'impatto del carico di lavoro della query e la relativa correlazione all'utilizzo delle risorse del database.</span><span class="sxs-lookup"><span data-stu-id="b3869-230">Query Performance Insight helps you understand the impact of your query workload and how it relates to database resource consumption.</span></span> <span data-ttu-id="b3869-231">Questa funzionalità consente di ottenere informazioni sulle query principali a livello di utilizzo di risorse e di identificare facilmente le query da correggere prima che si verifichino problemi.</span><span class="sxs-lookup"><span data-stu-id="b3869-231">With this feature, you will learn about the top consuming queries, and easily identify the ones to fix before they become a problem.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b3869-232">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b3869-232">Next steps</span></span>
<span data-ttu-id="b3869-233">Per ulteriori raccomandazioni sul miglioramento delle prestazioni del database SQL, fare clic su [Consigli](sql-database-advisor.md) nel pannello **Informazioni dettagliate sulle prestazioni delle query** .</span><span class="sxs-lookup"><span data-stu-id="b3869-233">For additional recommendations about improving the performance of your SQL database, click [Recommendations](sql-database-advisor.md) on the **Query Performance Insight** blade.</span></span>

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

