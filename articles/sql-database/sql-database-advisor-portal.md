---
title: Applicare le raccomandazioni per le prestazioni - Database SQL di Azure | Microsoft Docs
description: "È possibile usare il portale di Azure per trovare raccomandazioni per le prestazioni che consentono di ottimizzare le prestazioni del database SQL di Azure o per correggere eventuali problemi individuati nel carico di lavoro."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: cda8a646-0584-4368-b28a-85cdd9b54fcd
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: sstein
ms.openlocfilehash: 018afaa8b08bd001e55693390e80c8e2c4f33a30
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="find-and-apply-performance-recommendations"></a><span data-ttu-id="5a6f5-103">Trovare e applicare raccomandazioni per le prestazioni</span><span class="sxs-lookup"><span data-stu-id="5a6f5-103">Find and apply performance recommendations</span></span>

<span data-ttu-id="5a6f5-104">È possibile usare il portale di Azure per trovare raccomandazioni per le prestazioni che consentono di ottimizzare le prestazioni del database SQL di Azure o per correggere eventuali problemi individuati nel carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-104">You can use the Azure portal to find performance recommendations that can optimize performance of your Azure SQL Database or to correct some issue identified in your workload.</span></span> <span data-ttu-id="5a6f5-105">La pagina **Raccomandazioni per le prestazioni** nel portale di Azure consente di trovare le raccomandazioni principali in base all'impatto potenziale.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-105">**Performance recommendation** page in Azure portal enables you to find the top recommendations based on their potential impact.</span></span> 

## <a name="viewing-recommendations"></a><span data-ttu-id="5a6f5-106">Visualizzazione delle raccomandazioni</span><span class="sxs-lookup"><span data-stu-id="5a6f5-106">Viewing recommendations</span></span>

<span data-ttu-id="5a6f5-107">Per visualizzare e applicare le raccomandazioni, sono necessarie le autorizzazioni di [controllo degli accessi in base al ruolo](../active-directory/role-based-access-control-what-is.md) corrette in Azure.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-107">To view and apply performance recommendations, you need the correct [role-based access control](../active-directory/role-based-access-control-what-is.md) permissions in Azure.</span></span> <span data-ttu-id="5a6f5-108">Le autorizzazioni **Lettore** e **Collaboratore Database SQL** sono necessarie per visualizzare le raccomandazioni, mentre le autorizzazioni **Proprietario** e **Collaboratore Database SQL** sono necessarie per eseguire qualsiasi operazione, creare o eliminare indici e annullare la creazione di un indice.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-108">**Reader**, **SQL DB Contributor** permissions are required to view recommendations, and **Owner**, **SQL DB Contributor** permissions are required to execute any actions; create or drop indexes and cancel index creation.</span></span>

<span data-ttu-id="5a6f5-109">Usare la procedura seguente per trovare raccomandazioni per le prestazioni nel portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="5a6f5-109">Use the following steps to find performance recommendations on Azure portal:</span></span>

1. <span data-ttu-id="5a6f5-110">Accedere al [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5a6f5-110">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="5a6f5-111">Passare ad **Altri servizi** > **Database SQL** e selezionare il database.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-111">Go to **More services** > **SQL databases**, and select your database.</span></span>
3. <span data-ttu-id="5a6f5-112">Fare clic su **Raccomandazione per le prestazioni** per visualizzare le raccomandazioni disponibili per il database selezionato.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-112">Navigate to **Performance recommendation** to view available recommendations for the selected database.</span></span>

<span data-ttu-id="5a6f5-113">Le raccomandazioni per le prestazioni vengono visualizzate in una tabella simile a quella illustrata nella figura seguente:</span><span class="sxs-lookup"><span data-stu-id="5a6f5-113">Performance recommendations are shonw in the table similar to the one shown on the following figure:</span></span>

![Consigli](./media/sql-database-advisor-portal/recommendations.png)

<span data-ttu-id="5a6f5-115">Le raccomandazioni vengono ordinate in base all'impatto potenziale sulle prestazioni nelle categorie seguenti:</span><span class="sxs-lookup"><span data-stu-id="5a6f5-115">Recommendations are sorted by their potential impact on performance into the following categories:</span></span>

| <span data-ttu-id="5a6f5-116">Impatto</span><span class="sxs-lookup"><span data-stu-id="5a6f5-116">Impact</span></span> | <span data-ttu-id="5a6f5-117">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5a6f5-117">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="5a6f5-118">Alto</span><span class="sxs-lookup"><span data-stu-id="5a6f5-118">High</span></span> |<span data-ttu-id="5a6f5-119">Le indicazioni ad alto impatto devono fornire l'impatto più significativo sulle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-119">High impact recommendations should provide the most significant performance impact.</span></span> |
| <span data-ttu-id="5a6f5-120">Medio</span><span class="sxs-lookup"><span data-stu-id="5a6f5-120">Medium</span></span> |<span data-ttu-id="5a6f5-121">Le raccomandazioni a impatto medio devono migliorare le prestazioni, ma non sostanzialmente.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-121">Medium impact recommendations should improve performance, but not substantially.</span></span> |
| <span data-ttu-id="5a6f5-122">Basso</span><span class="sxs-lookup"><span data-stu-id="5a6f5-122">Low</span></span> |<span data-ttu-id="5a6f5-123">Le raccomandazioni a basso impatto devono offrire prestazioni migliori, ma i miglioramenti potrebbero non essere significativi.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-123">Low impact recommendations should provide better performance than without, but improvements might not be significant.</span></span> |


> [!NOTE]
> <span data-ttu-id="5a6f5-124">Il database SQL di Azure deve monitorare le attività almeno per un giorno per poter individuare alcune raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-124">Azure SQL Database needs to monitor activities at least for a day in order to identify some recommendations.</span></span> <span data-ttu-id="5a6f5-125">Il database SQL di Azure può ottimizzare più facilmente modelli di query coerenti anziché picchi irregolari casuali di attività.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-125">The Azure SQL Database can more easily optimize for consistent query patterns than it can for random spotty bursts of activity.</span></span> <span data-ttu-id="5a6f5-126">Se non sono disponibili raccomandazioni, nella pagina **Raccomandazione per le prestazioni** viene visualizzato un messaggio che ne spiega il motivo.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-126">If recommendations are not corrently available, the **Performance recommendation** page provides a message explaining why.</span></span>
> 

<span data-ttu-id="5a6f5-127">È anche possibile visualizzare lo stato delle ultime operazioni storiche.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-127">You can also view the status of the historical operations.</span></span> <span data-ttu-id="5a6f5-128">Selezionare un'indicazione o lo stato per visualizzare altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-128">Select a recommendation or status to see  more details.</span></span>

<span data-ttu-id="5a6f5-129">Di seguito è riportato un esempio della raccomandazione "Crea indice" nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-129">Here is an example of "Create index" recommendation in the Azure portal.</span></span>

![Creare un indice](./media/sql-database-advisor-portal/sql-database-performance-recommendation.png)

## <a name="applying-recommendations"></a><span data-ttu-id="5a6f5-131">Applicazione delle raccomandazioni</span><span class="sxs-lookup"><span data-stu-id="5a6f5-131">Applying recommendations</span></span>
<span data-ttu-id="5a6f5-132">Il database SQL di Azure offre il controllo completo sull'attivazione delle raccomandazioni tramite una delle tre opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="5a6f5-132">Azure SQL Database gives you full control over how recommendations are enabled using any of the following three options:</span></span> 

* <span data-ttu-id="5a6f5-133">Applicare le singole indicazioni una alla volta.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-133">Apply individual recommendations one at a time.</span></span>
* <span data-ttu-id="5a6f5-134">Abilitare l'ottimizzazione automatica per applicare automaticamente le raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-134">Enable the Automatic tuning to automatically apply recommendations.</span></span>
* <span data-ttu-id="5a6f5-135">Per implementare una raccomandazione manualmente, eseguire lo script T-SQL consigliato nel database.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-135">To implement a recommendation manually, run the recommended T-SQL script against your database.</span></span>

<span data-ttu-id="5a6f5-136">Selezionare una raccomandazione per visualizzarne i dettagli e quindi fare clic su **Visualizza script** per esaminare in dettaglio come viene creata la raccomandazione.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-136">Select any recommendation to view its details and then click **View script** to review the exact details of how the recommendation is created.</span></span>

<span data-ttu-id="5a6f5-137">Il database rimane online mentre viene applicata la raccomandazione. Un database non viene mai portato offline per l'uso di una raccomandazione per le prestazioni o per l'ottimizzazione automatica.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-137">The database remains online while the recommendation is applied -- using performance recommendation or automatic tuning never takes a database offline.</span></span>

### <a name="apply-an-individual-recommendation"></a><span data-ttu-id="5a6f5-138">Applicare una singola indicazione</span><span class="sxs-lookup"><span data-stu-id="5a6f5-138">Apply an individual recommendation</span></span>
<span data-ttu-id="5a6f5-139">È possibile leggere e accettare le indicazioni una alla volta.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-139">You can review and accept recommendations one at a time.</span></span>

1. <span data-ttu-id="5a6f5-140">Nel pannello **Raccomandazioni** selezionare una raccomandazione.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-140">On the **Recommendations** blade, select a recommendation.</span></span>
2. <span data-ttu-id="5a6f5-141">Nel pannello **Dettagli** fare clic sul pulsante **Applica**.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-141">On the **Details** blade click **Apply** button.</span></span>
   
    ![Applica suggerimento](./media/sql-database-advisor-portal/apply.png)

<span data-ttu-id="5a6f5-143">La raccomandazione selezionata verrà applicata nel database.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-143">Selected recommendation will be applied on the database.</span></span>

### <a name="removing-recommendations-from-the-list"></a><span data-ttu-id="5a6f5-144">Rimozione delle raccomandazioni dall'elenco</span><span class="sxs-lookup"><span data-stu-id="5a6f5-144">Removing recommendations from the list</span></span>
<span data-ttu-id="5a6f5-145">Se l'elenco di raccomandazioni contiene voci che si vuole rimuovere dall'elenco, ignorare la raccomandazione:</span><span class="sxs-lookup"><span data-stu-id="5a6f5-145">If your list of recommendations contains items that you want to remove from the list, you can discard the recommendation:</span></span>

1. <span data-ttu-id="5a6f5-146">Selezionare una raccomandazione nell'elenco **Raccomandazioni** per aprire i dettagli.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-146">Select a recommendation in the list of **Recommendations** to open the details.</span></span>
2. <span data-ttu-id="5a6f5-147">Fare clic su **Ignora** nel pannello **Dettagli**.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-147">Click **Discard** on the **Details** blade.</span></span>

<span data-ttu-id="5a6f5-148">Se si vuole, è possibile aggiungere nuovamente gli elementi ignorati all'elenco **Raccomandazioni** :</span><span class="sxs-lookup"><span data-stu-id="5a6f5-148">If desired, you can add discarded items back to the **Recommendations** list:</span></span>

1. <span data-ttu-id="5a6f5-149">Nel pannello **Raccomandazioni** fare clic su **Visualizza rimosse**.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-149">On the **Recommendations** blade click **View discarded**.</span></span>
2. <span data-ttu-id="5a6f5-150">Selezionare un elemento ignorato nell'elenco per visualizzarne i dettagli.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-150">Select a discarded item from the list to view its details.</span></span>
3. <span data-ttu-id="5a6f5-151">Facoltativamente, fare clic su **Annulla rimozione** per aggiungere nuovamente l'indice all'elenco principale di **Raccomandazioni**.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-151">Optionally, click **Undo Discard** to add the index back to the main list of **Recommendations**.</span></span>


### <a name="enable-automatic-tuning"></a><span data-ttu-id="5a6f5-152">Abilitare l'ottimizzazione automatica</span><span class="sxs-lookup"><span data-stu-id="5a6f5-152">Enable automatic tuning</span></span>
<span data-ttu-id="5a6f5-153">È possibile impostare il database SQL di Azure in modo che implementi automaticamente le raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-153">You can set the Azure SQL Database to implement recommendations automatically.</span></span> <span data-ttu-id="5a6f5-154">Man mano che le indicazioni vengono rese disponibili, verranno applicate automaticamente.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-154">As recommendations become available they will automatically be applied.</span></span> <span data-ttu-id="5a6f5-155">Come per tutte le raccomandazioni gestite dal servizio, se l'impatto sulle prestazioni è negativo le raccomandazioni verranno annullate.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-155">As with all recommendations managed by the service if the performance impact is negative the recommendation will be reverted.</span></span>

1. <span data-ttu-id="5a6f5-156">Nel pannello **Raccomandazioni** fare clic su **Automatizza**:</span><span class="sxs-lookup"><span data-stu-id="5a6f5-156">On the **Recommendations** blade, click **Automate**:</span></span>
   
    ![Impostazioni di Advisor](./media/sql-database-advisor-portal/settings.png)
2. <span data-ttu-id="5a6f5-158">Selezionare le azioni da automatizzare:</span><span class="sxs-lookup"><span data-stu-id="5a6f5-158">Select actions to automate:</span></span>
   
    ![Indici consigliati](./media/sql-database-advisor-portal/automation.png)

### <a name="manually-run-the-recommended-t-sql-script"></a><span data-ttu-id="5a6f5-160">Eseguire manualmente lo script T-SQL consigliato</span><span class="sxs-lookup"><span data-stu-id="5a6f5-160">Manually run the recommended T-SQL script</span></span>
<span data-ttu-id="5a6f5-161">Selezionare qualsiasi raccomandazione e quindi fare clic su **Visualizza script**.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-161">Select any recommendation and then click **View script**.</span></span> <span data-ttu-id="5a6f5-162">Eseguire questo script nel database per applicare manualmente l'indicazione.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-162">Run this script against your database to manually apply the recommendation.</span></span>

<span data-ttu-id="5a6f5-163">*Gli indici eseguiti manualmente non vengono monitorati e convalidati per l'impatto sulle prestazioni da parte del servizio* , quindi è consigliabile monitorarli dopo la creazione per verificare che offrano miglioramenti delle prestazioni e modificarli o eliminarli se necessario.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-163">*Indexes that are manually executed are not monitored and validated for performance impact by the service* so it is suggested that you monitor these indexes after creation to verify they provide performance gains and adjust or delete them if necessary.</span></span> <span data-ttu-id="5a6f5-164">Per informazioni dettagliate sulla creazione di indici, vedere [CREAZIONE INDICE (Transact-SQL)](https://msdn.microsoft.com/library/ms188783.aspx).</span><span class="sxs-lookup"><span data-stu-id="5a6f5-164">For details about creating indexes, see [CREATE INDEX (Transact-SQL)](https://msdn.microsoft.com/library/ms188783.aspx).</span></span>

### <a name="canceling-recommendations"></a><span data-ttu-id="5a6f5-165">Annullamento delle raccomandazioni</span><span class="sxs-lookup"><span data-stu-id="5a6f5-165">Canceling recommendations</span></span>
<span data-ttu-id="5a6f5-166">Le raccomandazioni con stato **In sospeso**, **Verifica** o **Operazione completata** possono essere annullate.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-166">Recommendations that are in a **Pending**, **Verifying**, or **Success** status can be canceled.</span></span> <span data-ttu-id="5a6f5-167">Le raccomandazioni con stato **In esecuzione** non possono essere annullate.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-167">Recommendations with a status of **Executing** cannot be canceled.</span></span>

1. <span data-ttu-id="5a6f5-168">Selezionare una raccomandazione nell'area **Cronologia ottimizzazione** per aprire il pannello dei **dettagli della raccomandazione**.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-168">Select a recommendation in the **Tuning History** area to open the **recommendations details** blade.</span></span>
2. <span data-ttu-id="5a6f5-169">Fare clic su **Annulla** per interrompere il processo di applicazione della raccomandazione.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-169">Click **Cancel** to abort the process of applying the recommendation.</span></span>

## <a name="monitoring-operations"></a><span data-ttu-id="5a6f5-170">Monitoraggio delle operazioni</span><span class="sxs-lookup"><span data-stu-id="5a6f5-170">Monitoring operations</span></span>
<span data-ttu-id="5a6f5-171">L'applicazione di un'indicazione potrebbe non avvenire in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-171">Applying a recommendation might not happen instantaneously.</span></span> <span data-ttu-id="5a6f5-172">Il portale fornisce dettagli sullo stato della raccomandazione.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-172">The portal provides details regarding the status of recommendation.</span></span> <span data-ttu-id="5a6f5-173">Di seguito sono indicati gli stati possibili di un indice:</span><span class="sxs-lookup"><span data-stu-id="5a6f5-173">The following are possible states that an index can be in:</span></span>

| <span data-ttu-id="5a6f5-174">Stato</span><span class="sxs-lookup"><span data-stu-id="5a6f5-174">Status</span></span> | <span data-ttu-id="5a6f5-175">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5a6f5-175">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="5a6f5-176">In sospeso</span><span class="sxs-lookup"><span data-stu-id="5a6f5-176">Pending</span></span> |<span data-ttu-id="5a6f5-177">Il comando di applicazione della raccomandazione è stato ricevuto ed è pianificato per l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-177">Apply recommendation command has been received and is scheduled for execution.</span></span> |
| <span data-ttu-id="5a6f5-178">In esecuzione</span><span class="sxs-lookup"><span data-stu-id="5a6f5-178">Executing</span></span> |<span data-ttu-id="5a6f5-179">La raccomandazione viene applicata.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-179">The recommendation is being applied.</span></span> |
| <span data-ttu-id="5a6f5-180">Verifica</span><span class="sxs-lookup"><span data-stu-id="5a6f5-180">Verifying</span></span> |<span data-ttu-id="5a6f5-181">La raccomandazione è stata applicata e il servizio sta valutando i vantaggi.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-181">Recommendation was successfully applied and the service is measuring the benefits.</span></span> |
| <span data-ttu-id="5a6f5-182">Operazione completata</span><span class="sxs-lookup"><span data-stu-id="5a6f5-182">Success</span></span> |<span data-ttu-id="5a6f5-183">La raccomandazione è stata applicata e i vantaggi sono stati misurati.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-183">Recommendation was successfully applied and benefits have been measured.</span></span> |
| <span data-ttu-id="5a6f5-184">Errore</span><span class="sxs-lookup"><span data-stu-id="5a6f5-184">Error</span></span> |<span data-ttu-id="5a6f5-185">Si è verificato un errore durante il processo di applicazione della raccomandazione.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-185">An error occurred during the process of applying the recommendation.</span></span> <span data-ttu-id="5a6f5-186">Può trattarsi di un problema temporaneo o eventualmente di una modifica dello schema della tabella e lo script non è più valido.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-186">This can be a transient issue, or possibly a schema change to the table and the script is no longer valid.</span></span> |
| <span data-ttu-id="5a6f5-187">Ripristino</span><span class="sxs-lookup"><span data-stu-id="5a6f5-187">Reverting</span></span> |<span data-ttu-id="5a6f5-188">La raccomandazione è stata applicata, ma è stata considerata non efficiente e verrà ripristinata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-188">The recommendation was applied, but has been deemed non-performant and is being automatically reverted.</span></span> |
| <span data-ttu-id="5a6f5-189">Ripristinato</span><span class="sxs-lookup"><span data-stu-id="5a6f5-189">Reverted</span></span> |<span data-ttu-id="5a6f5-190">La raccomandazione è stata ripristinata.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-190">The recommendation was reverted.</span></span> |

<span data-ttu-id="5a6f5-191">Fare clic su una raccomandazione in-process nell'elenco per visualizzare altri dettagli:</span><span class="sxs-lookup"><span data-stu-id="5a6f5-191">Click an in-process recommendation from the list to see more details:</span></span>

![Indici consigliati](./media/sql-database-advisor-portal/operations.png)

### <a name="reverting-a-recommendation"></a><span data-ttu-id="5a6f5-193">Ripristino di una raccomandazione</span><span class="sxs-lookup"><span data-stu-id="5a6f5-193">Reverting a recommendation</span></span>
<span data-ttu-id="5a6f5-194">Se sono state usate le raccomandazioni per le prestazioni per applicare la raccomandazione, ovvero non è stato eseguito manualmente lo script T-SQL, la raccomandazione verrà annullata automaticamente se viene rilevato un impatto negativo sulle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-194">If you used the performance recommendations to apply the recommendation (meaning you did not manually run the T-SQL script) it will automatically revert it if it finds the performance impact to be negative.</span></span> <span data-ttu-id="5a6f5-195">Se per qualsiasi motivo si vuole semplicemente annullare una raccomandazione, procedere come segue:</span><span class="sxs-lookup"><span data-stu-id="5a6f5-195">If for any reason you simply want to revert a recommendation you can do the following:</span></span>

1. <span data-ttu-id="5a6f5-196">Selezionare una raccomandazione applicata nell'area **Cronologia ottimizzazione** .</span><span class="sxs-lookup"><span data-stu-id="5a6f5-196">Select a successfully applied recommendation in the **Tuning history** area.</span></span>
2. <span data-ttu-id="5a6f5-197">Fare clic su **Ripristina** nel pannello dei **dettagli della raccomandazione**.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-197">Click **Revert** on the **recommendation details** blade.</span></span>

![Indici consigliati](./media/sql-database-advisor-portal/details.png)

## <a name="monitoring-performance-impact-of-index-recommendations"></a><span data-ttu-id="5a6f5-199">Monitoraggio dell'impatto sulle prestazioni delle indicazioni relative agli indici</span><span class="sxs-lookup"><span data-stu-id="5a6f5-199">Monitoring performance impact of index recommendations</span></span>
<span data-ttu-id="5a6f5-200">Dopo aver implementato correttamente le raccomandazioni (attualmente, solo raccomandazioni relative alle operazioni sugli indici e alle query con parametri), fare clic su **Informazioni dettagliate query** nel pannello dei dettagli delle raccomandazioni per aprire [Informazioni dettagliate prestazioni query](sql-database-query-performance.md) ed esaminare l'impatto sulle prestazioni delle query principali.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-200">After recommendations are successfully implemented (currently, index operations and parameterize queries recommendations only) you can click **Query Insights** on the recommendation details blade to open [Query Performance Insights](sql-database-query-performance.md) and see the performance impact of your top queries.</span></span>

![Monitorare l'impatto sulle prestazioni](./media/sql-database-advisor-portal/query-insights.png)

## <a name="summary"></a><span data-ttu-id="5a6f5-202">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="5a6f5-202">Summary</span></span>
<span data-ttu-id="5a6f5-203">Il database SQL di Azure fornisce raccomandazioni per migliorare le prestazioni del database SQL.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-203">Azure SQL Database provides recommendations for improving SQL database performance.</span></span> <span data-ttu-id="5a6f5-204">Questa funzionalità offre script T-SQL, nonché opzioni singole e completamente automatizzate, e risulta molto utile per ottimizzare il database e quindi per migliorare le prestazioni delle query.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-204">By providing T-SQL scripts, as well as individual and fully-automatic, you get a helpful assistance in optimizing your database and ultimately improving query performance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a6f5-205">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5a6f5-205">Next steps</span></span>
<span data-ttu-id="5a6f5-206">Monitorare le raccomandazioni e continuare ad applicarle in modo da migliorare le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-206">Monitor your recommendations and continue to apply them to refine performance.</span></span> <span data-ttu-id="5a6f5-207">I carichi di lavoro dei database sono dinamici e cambiano in modo continuo.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-207">Database workloads are dynamic and change continuously.</span></span> <span data-ttu-id="5a6f5-208">Il database SQL di Azure continuerà a monitorare e fornire raccomandazioni potenzialmente utili per migliorare le prestazioni del database.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-208">Azure SQL Database will continue to monitor and provide recommendations that can potentially improve your database's performance.</span></span> 

* <span data-ttu-id="5a6f5-209">Vedere [Ottimizzazione automatica](sql-database-automatic-tuning.md) per altre informazioni sull'ottimizzazione automatica nel database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-209">See [Automatic tuning](sql-database-automatic-tuning.md) to learn more about the automatic tuning in Azure SQL Database.</span></span>
* <span data-ttu-id="5a6f5-210">Vedere le [Raccomandazioni per le prestazioni](sql-database-advisor.md) per una panoramica delle raccomandazioni per le prestazioni per il database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-210">See [Performance recommendations](sql-database-advisor.md) for an overview of Azure SQL Database performance recommendations.</span></span>
* <span data-ttu-id="5a6f5-211">Vedere l'articolo [Informazioni dettagliate prestazioni query](sql-database-query-performance.md) per informazioni sull'analisi dell'impatto sulle prestazioni delle query principali.</span><span class="sxs-lookup"><span data-stu-id="5a6f5-211">See [Query Performance Insights](sql-database-query-performance.md) to learn about viewing the performance impact of your top queries.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5a6f5-212">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="5a6f5-212">Additional resources</span></span>
* [<span data-ttu-id="5a6f5-213">Archivio query</span><span class="sxs-lookup"><span data-stu-id="5a6f5-213">Query Store</span></span>](https://msdn.microsoft.com/library/dn817826.aspx)
* [<span data-ttu-id="5a6f5-214">CREATE INDEX</span><span class="sxs-lookup"><span data-stu-id="5a6f5-214">CREATE INDEX</span></span>](https://msdn.microsoft.com/library/ms188783.aspx)
* [<span data-ttu-id="5a6f5-215">Controllo degli accessi in base al ruolo</span><span class="sxs-lookup"><span data-stu-id="5a6f5-215">Role-based access control</span></span>](../active-directory/role-based-access-control-what-is.md)

