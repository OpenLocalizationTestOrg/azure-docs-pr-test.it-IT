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
# <a name="azure-sql-database-query-performance-insight"></a><span data-ttu-id="c8ecb-103">Query Performance Insight del database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="c8ecb-103">Azure SQL Database Query Performance Insight</span></span>
<span data-ttu-id="c8ecb-104">La gestione e ottimizzazione delle prestazioni dei database relazionali di hello è un'attività complessa che richiede una notevole esperienza e richiede tempo.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-104">Managing and tuning hello performance of relational databases is a challenging task that requires significant expertise and time investment.</span></span> <span data-ttu-id="c8ecb-105">Informazioni dettagliate prestazioni query consente toospend meno tempo di risoluzione dei problemi di prestazioni del database, fornendo seguente hello:</span><span class="sxs-lookup"><span data-stu-id="c8ecb-105">Query Performance Insight allows you toospend less time troubleshooting database performance by providing hello following:</span></span>

* <span data-ttu-id="c8ecb-106">Informazioni più approfondite sull'utilizzo delle risorse del database (DTU).</span><span class="sxs-lookup"><span data-stu-id="c8ecb-106">Deeper insight into your databases resource (DTU) consumption.</span></span> 
* <span data-ttu-id="c8ecb-107">Hello prime query per numero di CPU/Durata/esecuzione che potenzialmente possono essere ottimizzate per migliorare le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-107">hello top queries by CPU/Duration/Execution count, which can potentially be tuned for improved performance.</span></span>
* <span data-ttu-id="c8ecb-108">salve possibilità toodrill verso il basso in dettagli hello di una query, visualizzare il testo e la cronologia di utilizzo delle risorse.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-108">hello ability toodrill down into hello details of a query, view its text and history of resource utilization.</span></span> 
* <span data-ttu-id="c8ecb-109">Le annotazioni relative all'ottimizzazione delle prestazioni che descrivono le azioni eseguite da [SQL Azure Database Advisor](sql-database-advisor.md)</span><span class="sxs-lookup"><span data-stu-id="c8ecb-109">Performance tuning annotations that show actions performed by [SQL Azure Database Advisor](sql-database-advisor.md)</span></span>  



## <a name="prerequisites"></a><span data-ttu-id="c8ecb-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c8ecb-110">Prerequisites</span></span>
* <span data-ttu-id="c8ecb-111">Per Informazioni dettagliate sulle prestazioni delle query è necessario che l' [archivio query](https://msdn.microsoft.com/library/dn817826.aspx) sia attivo nel database.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-111">Query Performance Insight requires that [Query Store](https://msdn.microsoft.com/library/dn817826.aspx) is active on your database.</span></span> <span data-ttu-id="c8ecb-112">Se l'archivio Query non è in esecuzione, il portale di hello richiede tooturn sul.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-112">If Query Store is not running, hello portal prompts you tooturn it on.</span></span>

## <a name="permissions"></a><span data-ttu-id="c8ecb-113">Autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="c8ecb-113">Permissions</span></span>
<span data-ttu-id="c8ecb-114">esempio Hello [controllo di accesso basato sui ruoli](../active-directory/role-based-access-control-what-is.md) le autorizzazioni sono necessarie toouse informazioni dettagliate prestazioni Query:</span><span class="sxs-lookup"><span data-stu-id="c8ecb-114">hello following [role-based access control](../active-directory/role-based-access-control-what-is.md) permissions are required toouse Query Performance Insight:</span></span> 

* <span data-ttu-id="c8ecb-115">**Lettore**, **proprietario**, **collaboratore**, **collaboratore DB SQL**, o **collaboratore di SQL Server** sono le autorizzazioni necessario tooview hello prime consumo di risorse grafici e le query.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-115">**Reader**, **Owner**, **Contributor**, **SQL DB Contributor**, or **SQL Server Contributor** permissions are required tooview hello top resource consuming queries and charts.</span></span> 
* <span data-ttu-id="c8ecb-116">**Proprietario**, **collaboratore**, **collaboratore DB SQL**, o **collaboratore di SQL Server** le autorizzazioni sono necessarie tooview testo della query.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-116">**Owner**, **Contributor**, **SQL DB Contributor**, or **SQL Server Contributor** permissions are required tooview query text.</span></span>

## <a name="using-query-performance-insight"></a><span data-ttu-id="c8ecb-117">Uso di Query Performance Insight</span><span class="sxs-lookup"><span data-stu-id="c8ecb-117">Using Query Performance Insight</span></span>
<span data-ttu-id="c8ecb-118">Informazioni dettagliate prestazioni query è facile toouse:</span><span class="sxs-lookup"><span data-stu-id="c8ecb-118">Query Performance Insight is easy toouse:</span></span>

* <span data-ttu-id="c8ecb-119">Aprire [portale di Azure](https://portal.azure.com/) e database di ricerca che si desidera tooexamine.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-119">Open [Azure portal](https://portal.azure.com/) and find database that you want tooexamine.</span></span> 
  * <span data-ttu-id="c8ecb-120">Dal menu a sinistra, sotto la sezione dedicata al supporto e alla risoluzione dei problemi, selezionare "Informazioni dettagliate sulle prestazioni delle query".</span><span class="sxs-lookup"><span data-stu-id="c8ecb-120">From left-hand side menu, under support and troubleshooting, select “Query Performance Insight”.</span></span>
* <span data-ttu-id="c8ecb-121">Nella prima scheda hello, esaminare l'elenco di hello delle query più frequenti di consumo di risorse.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-121">On hello first tab, review hello list of top resource-consuming queries.</span></span>
* <span data-ttu-id="c8ecb-122">Selezionare i dettagli di tooview una singola query.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-122">Select an individual query tooview its details.</span></span>
* <span data-ttu-id="c8ecb-123">Aprire [SQL Azure Database Advisor](sql-database-advisor.md) e verificare se sono disponibili raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-123">Open [SQL Azure Database Advisor](sql-database-advisor.md) and check if any recommendations are available.</span></span>
* <span data-ttu-id="c8ecb-124">Utilizzare dispositivi di scorrimento Zoom avanti o indietro toochange icone osservati intervallo.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-124">Use sliders or zoom icons toochange observed interval.</span></span>
  
    ![dashboard prestazioni](./media/sql-database-query-performance/performance.png)

> [!NOTE]
> <span data-ttu-id="c8ecb-126">Un paio di ore di dati deve toobe acquisita dall'archivio Query per informazioni dettagliate prestazioni query di Database SQL tooprovide.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-126">A couple hours of data needs toobe captured by Query Store for SQL Database tooprovide query performance insights.</span></span> <span data-ttu-id="c8ecb-127">Se il database di hello non contiene attività o archivio Query non era attivo durante un determinato periodo di tempo, grafici hello sarà vuoti per la visualizzazione di questo periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-127">If hello database has no activity or Query Store was not active during a certain time period, hello charts will be empty when displaying that time period.</span></span> <span data-ttu-id="c8ecb-128">È possibile abilitare l'archivio query in qualsiasi momento, se non è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-128">You may enable Query Store at any time if it is not running.</span></span>   
> 
> 

## <a name="review-top-cpu-consuming-queries"></a><span data-ttu-id="c8ecb-129">Esaminare le query principali a livello di utilizzo di CPU</span><span class="sxs-lookup"><span data-stu-id="c8ecb-129">Review top CPU consuming queries</span></span>
<span data-ttu-id="c8ecb-130">In hello [portale](http://portal.azure.com) hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="c8ecb-130">In hello [portal](http://portal.azure.com) do hello following:</span></span>

1. <span data-ttu-id="c8ecb-131">Database SQL tooa e fare clic su **tutte le impostazioni** > **supporto + Troubleshooting** > **informazioni dettagliate prestazioni Query**.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-131">Browse tooa SQL database and click **All settings** > **Support + Troubleshooting** > **Query performance insight**.</span></span> 
   
    ![Informazioni dettagliate prestazioni query][1]
   
    <span data-ttu-id="c8ecb-133">verrà visualizzata la visualizzazione di query superiore Hello e sono elencati hello principali della CPU dispendiosa in termini di query.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-133">hello top queries view opens and hello top CPU consuming queries are listed.</span></span>
2. <span data-ttu-id="c8ecb-134">Fare clic su grafico hello per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-134">Click around hello chart for details.</span></span><br><span data-ttu-id="c8ecb-135">Hello riga superiore mostra % complessivo di DTU per database hello, mentre le barre di hello indicano % della CPU utilizzate dalle query hello selezionato durante l'intervallo selezionato hello (ad esempio, se **settimana precedente** è selezionata ogni barra rappresenta un giorno).</span><span class="sxs-lookup"><span data-stu-id="c8ecb-135">hello top line shows overall DTU% for hello database, while hello bars show CPU% consumed by hello selected queries during hello selected interval (for example, if **Past week** is selected each bar represents one day).</span></span>
   
    ![query principali][2]
   
    <span data-ttu-id="c8ecb-137">griglia inferiore Hello rappresenta informazioni aggregate per query visibile hello.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-137">hello bottom grid represents aggregated information for hello visible queries.</span></span>
   
   * <span data-ttu-id="c8ecb-138">ID query: identificatore univoco di query all'interno del database.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-138">Query ID - unique identifier of query inside database.</span></span>
   * <span data-ttu-id="c8ecb-139">Utilizzo della CPU per query durante l'intervallo osservabile (dipende dalla funzione di aggregazione).</span><span class="sxs-lookup"><span data-stu-id="c8ecb-139">CPU per query during observable interval (depends on aggregation function).</span></span>
   * <span data-ttu-id="c8ecb-140">Durata per ogni query (dipende dalla funzione di aggregazione).</span><span class="sxs-lookup"><span data-stu-id="c8ecb-140">Duration per query (depends on aggregation function).</span></span>
   * <span data-ttu-id="c8ecb-141">Numero totale di esecuzioni per una query specifica.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-141">Total number of executions for a particular query.</span></span>
     
     <span data-ttu-id="c8ecb-142">Selezionare o deselezionare singole query tooinclude o escluderli dal grafico hello utilizzando le caselle di controllo.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-142">Select or clear individual queries tooinclude or exclude them from hello chart using checkboxes.</span></span>
3. <span data-ttu-id="c8ecb-143">Se i dati non risulta più aggiornati, fare clic su hello **aggiornamento** pulsante.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-143">If your data becomes stale, click hello **Refresh** button.</span></span>
4. <span data-ttu-id="c8ecb-144">È possibile usare dispositivi di scorrimento e intervallo di osservazione toochange pulsanti zoom e analizzare i picchi: ![impostazioni](./media/sql-database-query-performance/zoom.png)</span><span class="sxs-lookup"><span data-stu-id="c8ecb-144">You can use sliders and zoom buttons toochange observation interval and investigate spikes:  ![settings](./media/sql-database-query-performance/zoom.png)</span></span>
5. <span data-ttu-id="c8ecb-145">Facoltativamente, se si desidera un'altra visualizzazione, è possibile selezionare la scheda **Personalizzata** e impostare:</span><span class="sxs-lookup"><span data-stu-id="c8ecb-145">Optionally, if you want a different view, you can select **Custom** tab and set:</span></span>
   
   * <span data-ttu-id="c8ecb-146">Metrica (CPU, durata, conteggio delle esecuzioni)</span><span class="sxs-lookup"><span data-stu-id="c8ecb-146">Metric (CPU, duration, execution count)</span></span>
   * <span data-ttu-id="c8ecb-147">Intervallo di tempo (ultime 24 ore, settimana scorsa, mese scorso).</span><span class="sxs-lookup"><span data-stu-id="c8ecb-147">Time interval (Last 24 hours, Past week, Past month).</span></span> 
   * <span data-ttu-id="c8ecb-148">Numero di query.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-148">Number of queries.</span></span>
   * <span data-ttu-id="c8ecb-149">Funzione di aggregazione.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-149">Aggregation function.</span></span>
     
     ![Impostazioni](./media/sql-database-query-performance/custom-tab.png)

## <a name="viewing-individual-query-details"></a><span data-ttu-id="c8ecb-151">Visualizzazione dei dettagli delle singole query</span><span class="sxs-lookup"><span data-stu-id="c8ecb-151">Viewing individual query details</span></span>
<span data-ttu-id="c8ecb-152">dettagli di query tooview:</span><span class="sxs-lookup"><span data-stu-id="c8ecb-152">tooview query details:</span></span>

1. <span data-ttu-id="c8ecb-153">Fare clic su qualsiasi query elenco hello delle query più frequenti.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-153">Click any query in hello list of top queries.</span></span>
   
    ![informazioni dettagliate](./media/sql-database-query-performance/details.png)
2. <span data-ttu-id="c8ecb-155">verrà visualizzata la finestra di visualizzazione dei dettagli Hello e conteggio di utilizzo/Durata/esecuzione hello query della CPU è suddivisa nel tempo.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-155">hello details view opens and hello queries CPU consumption/Duration/Execution count is broken down over time.</span></span>
3. <span data-ttu-id="c8ecb-156">Fare clic su grafico hello per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-156">Click around hello chart for details.</span></span>
   
   * <span data-ttu-id="c8ecb-157">Grafico superiore Mostra linea con % DTU complessivo del database e le barre di hello sono % della CPU utilizzata dalla query selezionata hello.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-157">Top chart shows line with overall database DTU%, and hello bars are CPU% consumed by hello selected query.</span></span>
   * <span data-ttu-id="c8ecb-158">Secondo grafico mostra la durata totale dalla query selezionata hello.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-158">Second chart shows total duration by hello selected query.</span></span>
   * <span data-ttu-id="c8ecb-159">Numero totale di esecuzioni inferiore mostra dalla query selezionata hello.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-159">Bottom chart shows total number of executions by hello selected query.</span></span>
     
     ![dettagli sulle query][3]
4. <span data-ttu-id="c8ecb-161">Facoltativamente, utilizzare dispositivi di scorrimento, pulsanti di zoom oppure fare clic su **impostazioni** toocustomize modalità di visualizzazione dati di query o toopick un periodo di tempo diverso.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-161">Optionally, use sliders, zoom buttons or click **Settings** toocustomize how query data is displayed, or toopick a different time period.</span></span>

## <a name="review-top-queries-per-duration"></a><span data-ttu-id="c8ecb-162">Esaminare le query principali in base alla durata</span><span class="sxs-lookup"><span data-stu-id="c8ecb-162">Review top queries per duration</span></span>
<span data-ttu-id="c8ecb-163">In hello recente aggiornamento di informazioni dettagliate prestazioni Query, è stata introdotta due nuove metriche che consentono di identificare potenziali colli di bottiglia: conteggio di durata e l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-163">In hello recent update of Query Performance Insight, we introduced two new metrics that can help you identify potential bottlenecks: duration and execution count.</span></span><br>

<span data-ttu-id="c8ecb-164">Query con esecuzione prolungata sono hello maggiori possibilità più risorse di blocco, blocco di altri utenti e limitare la scalabilità.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-164">Long-running queries have hello greatest potential for locking resources longer, blocking other users, and limiting scalability.</span></span> <span data-ttu-id="c8ecb-165">Sono inoltre hello di candidati ottimali per l'ottimizzazione.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-165">They are also hello best candidates for optimization.</span></span><br>

<span data-ttu-id="c8ecb-166">tooidentify query a esecuzione prolungata:</span><span class="sxs-lookup"><span data-stu-id="c8ecb-166">tooidentify long running queries:</span></span>

1. <span data-ttu-id="c8ecb-167">Aprire la scheda **Personalizza** in Informazioni dettagliate sulle prestazioni delle query del database selezionato</span><span class="sxs-lookup"><span data-stu-id="c8ecb-167">Open **Custom** tab in Query Performance Insight for selected database</span></span>
2. <span data-ttu-id="c8ecb-168">Modificare le metriche toobe **durata**</span><span class="sxs-lookup"><span data-stu-id="c8ecb-168">Change metrics toobe **duration**</span></span>
3. <span data-ttu-id="c8ecb-169">Selezionare il numero di query e l'intervallo di osservazione</span><span class="sxs-lookup"><span data-stu-id="c8ecb-169">Select number of queries and observation interval</span></span>
4. <span data-ttu-id="c8ecb-170">Selezionare la funzione di aggregazione</span><span class="sxs-lookup"><span data-stu-id="c8ecb-170">Select aggregation function</span></span>
   
   * <span data-ttu-id="c8ecb-171">**Somma** aggiunge il tempo di esecuzione di tutte le query durante l'intero intervallo di osservazione.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-171">**Sum** adds up all query execution time during whole observation interval.</span></span>
   * <span data-ttu-id="c8ecb-172">**Max** individua le query con il tempo di esecuzione massimo durante l'intero intervallo di osservazione.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-172">**Max** finds queries which execution time was maximum at whole observation interval.</span></span>
   * <span data-ttu-id="c8ecb-173">**AVG** rileva il tempo medio di esecuzione di tutte le esecuzioni di query e mostrano hello top fuori queste medie.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-173">**Avg** finds average execution time of all query executions and show you hello top out of these averages.</span></span> 
     
     ![durata query][4]

## <a name="review-top-queries-per-execution-count"></a><span data-ttu-id="c8ecb-175">Esaminare le query principali in base al conteggio delle esecuzioni</span><span class="sxs-lookup"><span data-stu-id="c8ecb-175">Review top queries per execution count</span></span>
<span data-ttu-id="c8ecb-176">Il numero elevato di esecuzioni potrebbe non influire sul database e l'utilizzo delle risorse potrebbe essere modesto, ma l'applicazione nel suo complesso potrebbe risultare rallentata.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-176">High number of executions might not be affecting database itself and resources usage can be low, but overall application might get slow.</span></span>

<span data-ttu-id="c8ecb-177">In alcuni casi, conteggio esecuzioni molto elevato può causare tooincrease di rete di andata e ritorno.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-177">In some cases, very high execution count may lead tooincrease of network round trips.</span></span> <span data-ttu-id="c8ecb-178">I round trip hanno un forte impatto sulle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-178">Round trips significantly affect performance.</span></span> <span data-ttu-id="c8ecb-179">Sono latenza toonetwork soggetto e latenza server toodownstream.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-179">They are subject toonetwork latency and toodownstream server latency.</span></span> 

<span data-ttu-id="c8ecb-180">Ad esempio, molti siti Web basati sui dati accedere frequentemente database hello per ogni richiesta dell'utente.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-180">For example, many data-driven Web sites heavily access hello database for every user request.</span></span> <span data-ttu-id="c8ecb-181">Mentre il pool di connessioni consente, hello aumentato il traffico di rete e il carico di elaborazione nel server di database hello può influire negativamente sulle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-181">While connection pooling helps, hello increased network traffic and processing load on hello database server can adversely affect performance.</span></span>  <span data-ttu-id="c8ecb-182">Consigli di carattere generale sono tookeep round trip tooan minimo.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-182">General advice is tookeep round trips tooan absolute minimum.</span></span>

<span data-ttu-id="c8ecb-183">tooidentify eseguite di frequente query query ("chatty"):</span><span class="sxs-lookup"><span data-stu-id="c8ecb-183">tooidentify frequently executed queries (“chatty”) queries:</span></span>

1. <span data-ttu-id="c8ecb-184">Aprire la scheda **Personalizza** in Informazioni dettagliate sulle prestazioni delle query del database selezionato</span><span class="sxs-lookup"><span data-stu-id="c8ecb-184">Open **Custom** tab in Query Performance Insight for selected database</span></span>
2. <span data-ttu-id="c8ecb-185">Modificare le metriche toobe **conteggio esecuzioni**</span><span class="sxs-lookup"><span data-stu-id="c8ecb-185">Change metrics toobe **execution count**</span></span>
3. <span data-ttu-id="c8ecb-186">Selezionare il numero di query e l'intervallo di osservazione</span><span class="sxs-lookup"><span data-stu-id="c8ecb-186">Select number of queries and observation interval</span></span>
   
    ![conteggio delle esecuzioni query][5]

## <a name="understanding-performance-tuning-annotations"></a><span data-ttu-id="c8ecb-188">Informazioni sulle annotazioni di ottimizzazione delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="c8ecb-188">Understanding performance tuning annotations</span></span>
<span data-ttu-id="c8ecb-189">Durante l'esplorazione del carico di lavoro di informazioni dettagliate prestazioni Query, è possibile notare le icone con linea verticale nella parte superiore del grafico hello.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-189">While exploring your workload in Query Performance Insight, you might notice icons with vertical line on top of hello chart.</span></span><br>

<span data-ttu-id="c8ecb-190">Queste icone sono annotazioni sulle prestazioni che influiscono sulle azioni eseguite da [SQL Azure Database Advisor](sql-database-advisor.md).</span><span class="sxs-lookup"><span data-stu-id="c8ecb-190">These icons are annotations; they represent performance affecting actions performed by [SQL Azure Database Advisor](sql-database-advisor.md).</span></span> <span data-ttu-id="c8ecb-191">Per questa annotazione, si ottiene le informazioni di base sull'azione hello:</span><span class="sxs-lookup"><span data-stu-id="c8ecb-191">By hovering annotation, you get basic information about hello action:</span></span>

![annotazione query][6]

<span data-ttu-id="c8ecb-193">Se si desidera più tooknow o applica l'indicazione, fare clic sull'icona di hello.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-193">If you want tooknow more or apply advisor recommendation, click hello icon.</span></span> <span data-ttu-id="c8ecb-194">in modo da visualizzare i dettagli relativi all'azione. </span><span class="sxs-lookup"><span data-stu-id="c8ecb-194">It will open details of action.</span></span> <span data-ttu-id="c8ecb-195">Se si tratta di un consiglio attivo è possibile applicarlo direttamente tramite il comando.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-195">If it’s an active recommendation you can apply it straight away using command.</span></span>

![dettagli annotazione query][7]

### <a name="multiple-annotations"></a><span data-ttu-id="c8ecb-197">Annotazioni multiple.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-197">Multiple annotations.</span></span>
<span data-ttu-id="c8ecb-198">È possibile, che a causa di livello di zoom, le annotazioni che sono Chiudi tooeach altri verranno ottenere compresso in un unico.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-198">It’s possible, that because of zoom level, annotations that are close tooeach other will get collapsed into one.</span></span> <span data-ttu-id="c8ecb-199">che verrà rappresentato dall'icona speciale; facendo clic su tale icona si aprirà un nuovo pannello con l'elenco delle annotazioni raggruppate.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-199">This will be represented by special icon, clicking it will open new blade where list of grouped annotations will be shown.</span></span>
<span data-ttu-id="c8ecb-200">Correlazione di query e le azioni di ottimizzazione delle prestazioni può comprendere toobetter il carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-200">Correlating queries and performance tuning actions can help toobetter understand your workload.</span></span> 

## <a name="optimizing-hello-query-store-configuration-for-query-performance-insight"></a><span data-ttu-id="c8ecb-201">Ottimizzazione della configurazione di archivio Query hello per informazioni dettagliate prestazioni Query</span><span class="sxs-lookup"><span data-stu-id="c8ecb-201">Optimizing hello Query Store configuration for Query Performance Insight</span></span>
<span data-ttu-id="c8ecb-202">Durante l'uso di informazioni dettagliate prestazioni Query, possono verificarsi hello messaggi dell'archivio di Query seguente:</span><span class="sxs-lookup"><span data-stu-id="c8ecb-202">During your use of Query Performance Insight, you might encounter hello following Query Store messages:</span></span>

* <span data-ttu-id="c8ecb-203">"Archivio query non è correttamente configurato in questo database.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-203">"Query Store is not properly configured on this database.</span></span> <span data-ttu-id="c8ecb-204">Fare clic qui ulteriori toolearn."</span><span class="sxs-lookup"><span data-stu-id="c8ecb-204">Click here toolearn more."</span></span>
* <span data-ttu-id="c8ecb-205">"Archivio query non è correttamente configurato in questo database.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-205">"Query Store is not properly configured on this database.</span></span> <span data-ttu-id="c8ecb-206">Fare clic qui impostazioni toochange."</span><span class="sxs-lookup"><span data-stu-id="c8ecb-206">Click here toochange settings."</span></span> 

<span data-ttu-id="c8ecb-207">Questi messaggi vengono visualizzati in genere quando l'archivio Query non è in grado di toocollect nuovi dati.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-207">These messages usually appear when Query Store is not able toocollect new data.</span></span> 

<span data-ttu-id="c8ecb-208">Il primo caso si verifica quando l'archivio query è in stato di sola lettura e i parametri sono impostati in modo ottimale.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-208">First case happens when Query Store is in Read-Only state and parameters are set optimally.</span></span> <span data-ttu-id="c8ecb-209">È possibile risolvere il problema aumentando le dimensioni dell'archivio query o svuotandolo del tutto.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-209">You can fix this by increasing size of Query Store or clearing Query Store.</span></span>

![pulsante qds][8]

<span data-ttu-id="c8ecb-211">Il secondo caso si verifica quando l'archivio query è disattivato o se i parametri non sono impostati in modo ottimale.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-211">Second case happens when Query Store is Off or parameters aren’t set optimally.</span></span> <br><span data-ttu-id="c8ecb-212">È possibile modificare hello acquisizione e memorizzazione dei criteri e abilitare archivio Query eseguendo i comandi riportati di seguito o direttamente dal portale:</span><span class="sxs-lookup"><span data-stu-id="c8ecb-212">You can change hello Retention and Capture policy and enable Query Store by executing commands below or directly from portal:</span></span>

![pulsante qds][9]

### <a name="recommended-retention-and-capture-policy"></a><span data-ttu-id="c8ecb-214">Criteri di conservazione e acquisizione consigliati</span><span class="sxs-lookup"><span data-stu-id="c8ecb-214">Recommended retention and capture policy</span></span>
<span data-ttu-id="c8ecb-215">Esistono due tipi di criteri di conservazione:</span><span class="sxs-lookup"><span data-stu-id="c8ecb-215">There are two types of retention policies:</span></span>

* <span data-ttu-id="c8ecb-216">Dimensioni basate - se viene raggiunto tooAUTO set eseguirà la pulizia dati automaticamente in prossimità di dimensioni massime.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-216">Size based - if set tooAUTO it will clean data automatically when near max size is reached.</span></span>
* <span data-ttu-id="c8ecb-217">Tempo basata - per impostazione predefinita, si imposterà too30 giorni, vale a dire che, se l'archivio Query esaurirà lo spazio, verranno eliminati, eseguire query sulle informazioni più vecchi di 30 giorni</span><span class="sxs-lookup"><span data-stu-id="c8ecb-217">Time based - by default we will set it too30 days, which means, if Query Store will run out of space, it will delete query information older than 30 days</span></span>

<span data-ttu-id="c8ecb-218">I criteri di acquisizione possono essere impostati su:</span><span class="sxs-lookup"><span data-stu-id="c8ecb-218">Capture policy could be set to:</span></span>

* <span data-ttu-id="c8ecb-219">**Tutte**: acquisisce tutte le query.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-219">**All** - Captures all queries.</span></span>
* <span data-ttu-id="c8ecb-220">**Automatico**: le query poco frequenti e con durata di compilazione ed esecuzione trascurabile vengono ignorate.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-220">**Auto** - Infrequent queries and queries with insignificant compile and execution duration are ignored.</span></span> <span data-ttu-id="c8ecb-221">Le soglie per il conteggio delle esecuzioni e la durata di compilazione ed esecuzione vengono stabilite internamente.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-221">Thresholds for execution count, compile and runtime duration are internally determined.</span></span> <span data-ttu-id="c8ecb-222">Questo è l'opzione predefinita di hello.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-222">This is hello default option.</span></span>
* <span data-ttu-id="c8ecb-223">**Nessuna**: l'archivio query interrompe l'acquisizione di nuove query, ma continua a raccogliere le statistiche di runtime per le query già acquisite.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-223">**None** - Query Store stops capturing new queries, however runtime stats for already captured queries are still collected.</span></span>

<span data-ttu-id="c8ecb-224">È consigliabile impostare tutti i criteri tooAUTO e criteri pulita too30 giorni:</span><span class="sxs-lookup"><span data-stu-id="c8ecb-224">We recommend setting all policies tooAUTO and clean policy too30 days:</span></span>

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (SIZE_BASED_CLEANUP_MODE = AUTO);

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 30));

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (QUERY_CAPTURE_MODE = AUTO);

<span data-ttu-id="c8ecb-225">Aumentare le dimensioni dell'archivio query.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-225">Increase size of Query Store.</span></span> <span data-ttu-id="c8ecb-226">Potrebbe trattarsi di operazione eseguita dal database tooa connessione ed emettere query riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="c8ecb-226">This could be performed by connecting tooa database and issuing following query:</span></span>

    ALTER DATABASE [YourDB]
    SET QUERY_STORE (MAX_STORAGE_SIZE_MB = 1024);

<span data-ttu-id="c8ecb-227">Applicazione di queste impostazioni eventualmente renderà archivio Query, la raccolta di nuove query, tuttavia, se non si desidera toowait è possibile cancellare l'archivio Query.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-227">Applying these settings will eventually make Query Store collecting new queries, however if you don’t want toowait you can clear Query Store.</span></span> 

> [!NOTE]
> <span data-ttu-id="c8ecb-228">Esecuzione della query seguente eliminerà tutte le informazioni correnti in hello archivio Query.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-228">Executing following query will delete all current information in hello Query Store.</span></span> 
> 
> 

    ALTER DATABASE [YourDB] SET QUERY_STORE CLEAR;


## <a name="summary"></a><span data-ttu-id="c8ecb-229">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="c8ecb-229">Summary</span></span>
<span data-ttu-id="c8ecb-230">Informazioni dettagliate prestazioni query consente di comprendere l'impatto di hello query del carico di lavoro e l'interrelazione toodatabase consumo delle risorse.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-230">Query Performance Insight helps you understand hello impact of your query workload and how it relates toodatabase resource consumption.</span></span> <span data-ttu-id="c8ecb-231">Con questa funzionalità, si verrà apprendere top hello query per consumo e identificare facilmente quelli hello toofix prima che diventino un problema.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-231">With this feature, you will learn about hello top consuming queries, and easily identify hello ones toofix before they become a problem.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c8ecb-232">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c8ecb-232">Next steps</span></span>
<span data-ttu-id="c8ecb-233">Per altre indicazioni sull'ottimizzazione delle prestazioni di hello del database SQL, fare clic su [indicazioni](sql-database-advisor.md) su hello **informazioni dettagliate prestazioni Query** blade.</span><span class="sxs-lookup"><span data-stu-id="c8ecb-233">For additional recommendations about improving hello performance of your SQL database, click [Recommendations](sql-database-advisor.md) on hello **Query Performance Insight** blade.</span></span>

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

