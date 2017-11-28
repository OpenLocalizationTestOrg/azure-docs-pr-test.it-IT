---
title: consigli relativi alle prestazioni aaaApply - Database SQL di Azure | Documenti Microsoft
description: "È possibile utilizzare hello toofind portale Azure suggerimenti relativi alle prestazioni che è possibile ottimizzare le prestazioni del Database SQL di Azure o toocorrect un problema identificato nel carico di lavoro."
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
ms.openlocfilehash: 0b2234840fc3254d235db9e7d18f5bc912851c6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="find-and-apply-performance-recommendations"></a><span data-ttu-id="d8d8c-103">Trovare e applicare raccomandazioni per le prestazioni</span><span class="sxs-lookup"><span data-stu-id="d8d8c-103">Find and apply performance recommendations</span></span>

<span data-ttu-id="d8d8c-104">È possibile utilizzare hello toofind portale Azure suggerimenti relativi alle prestazioni che è possibile ottimizzare le prestazioni del Database SQL di Azure o toocorrect un problema identificato nel carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-104">You can use hello Azure portal toofind performance recommendations that can optimize performance of your Azure SQL Database or toocorrect some issue identified in your workload.</span></span> <span data-ttu-id="d8d8c-105">**Indicazione delle prestazioni** pagina nel portale di Azure consente principale indicazioni in base a impatto potenziale hello toofind.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-105">**Performance recommendation** page in Azure portal enables you toofind hello top recommendations based on their potential impact.</span></span> 

## <a name="viewing-recommendations"></a><span data-ttu-id="d8d8c-106">Visualizzazione delle raccomandazioni</span><span class="sxs-lookup"><span data-stu-id="d8d8c-106">Viewing recommendations</span></span>

<span data-ttu-id="d8d8c-107">tooview e applicare i consigli relativi alle prestazioni, è necessario hello corretto [controllo di accesso basato sui ruoli](../active-directory/role-based-access-control-what-is.md) autorizzazioni in Azure.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-107">tooview and apply performance recommendations, you need hello correct [role-based access control](../active-directory/role-based-access-control-what-is.md) permissions in Azure.</span></span> <span data-ttu-id="d8d8c-108">**Lettore**, **collaboratore DB SQL** le autorizzazioni sono necessarie tooview indicazioni, e **proprietario**, **collaboratore DB SQL** sono necessarie le autorizzazioni tooexecute eventuali azioni; creare o eliminare gli indici e annullare la creazione dell'indice.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-108">**Reader**, **SQL DB Contributor** permissions are required tooview recommendations, and **Owner**, **SQL DB Contributor** permissions are required tooexecute any actions; create or drop indexes and cancel index creation.</span></span>

<span data-ttu-id="d8d8c-109">Consigli relativi alle prestazioni toofind i passaggi da utilizzare hello seguenti nel portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="d8d8c-109">Use hello following steps toofind performance recommendations on Azure portal:</span></span>

1. <span data-ttu-id="d8d8c-110">Accedi toohello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d8d8c-110">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="d8d8c-111">Andare troppo**più servizi** > **database SQL**e selezionare il database.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-111">Go too**More services** > **SQL databases**, and select your database.</span></span>
3. <span data-ttu-id="d8d8c-112">Passare troppo**raccomandazione prestazioni** tooview le indicazioni disponibili per il database selezionato hello.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-112">Navigate too**Performance recommendation** tooview available recommendations for hello selected database.</span></span>

<span data-ttu-id="d8d8c-113">Consigli relativi alle prestazioni sono shonw in hello tabella simile toohello illustrato nella seguente illustrazione hello:</span><span class="sxs-lookup"><span data-stu-id="d8d8c-113">Performance recommendations are shonw in hello table similar toohello one shown on hello following figure:</span></span>

![Raccomandazioni](./media/sql-database-advisor-portal/recommendations.png)

<span data-ttu-id="d8d8c-115">Indicazioni vengono ordinate in base il potenziale impatto sulle prestazioni in hello seguenti categorie:</span><span class="sxs-lookup"><span data-stu-id="d8d8c-115">Recommendations are sorted by their potential impact on performance into hello following categories:</span></span>

| <span data-ttu-id="d8d8c-116">Impatto</span><span class="sxs-lookup"><span data-stu-id="d8d8c-116">Impact</span></span> | <span data-ttu-id="d8d8c-117">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d8d8c-117">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="d8d8c-118">Alto</span><span class="sxs-lookup"><span data-stu-id="d8d8c-118">High</span></span> |<span data-ttu-id="d8d8c-119">Indicazioni di alto impatto devono fornire l'impatto più significativo sulle prestazioni di hello.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-119">High impact recommendations should provide hello most significant performance impact.</span></span> |
| <span data-ttu-id="d8d8c-120">Media</span><span class="sxs-lookup"><span data-stu-id="d8d8c-120">Medium</span></span> |<span data-ttu-id="d8d8c-121">Le raccomandazioni a impatto medio devono migliorare le prestazioni, ma non sostanzialmente.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-121">Medium impact recommendations should improve performance, but not substantially.</span></span> |
| <span data-ttu-id="d8d8c-122">Basso</span><span class="sxs-lookup"><span data-stu-id="d8d8c-122">Low</span></span> |<span data-ttu-id="d8d8c-123">Le raccomandazioni a basso impatto devono offrire prestazioni migliori, ma i miglioramenti potrebbero non essere significativi.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-123">Low impact recommendations should provide better performance than without, but improvements might not be significant.</span></span> |


> [!NOTE]
> <span data-ttu-id="d8d8c-124">Database SQL di Azure richiede attività toomonitor almeno per un giorno in ordine tooidentify alcune raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-124">Azure SQL Database needs toomonitor activities at least for a day in order tooidentify some recommendations.</span></span> <span data-ttu-id="d8d8c-125">Hello Database SQL di Azure può ottimizzare più facilmente modelli di query coerente anziché casuale irregolare picchi di attività.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-125">hello Azure SQL Database can more easily optimize for consistent query patterns than it can for random spotty bursts of activity.</span></span> <span data-ttu-id="d8d8c-126">Se indicazioni non sono disponibili corrently, hello **raccomandazione prestazioni** pagina fornisce un messaggio che spiega il motivo.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-126">If recommendations are not corrently available, hello **Performance recommendation** page provides a message explaining why.</span></span>
> 

<span data-ttu-id="d8d8c-127">Inoltre, è possibile visualizzare lo stato di hello di operazioni storiche hello.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-127">You can also view hello status of hello historical operations.</span></span> <span data-ttu-id="d8d8c-128">Selezionare un suggerimento o lo stato di toosee ulteriori dettagli.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-128">Select a recommendation or status toosee  more details.</span></span>

<span data-ttu-id="d8d8c-129">Di seguito è riportato un esempio di "Creazione dell'indice di" azione consigliata nell'hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-129">Here is an example of "Create index" recommendation in hello Azure portal.</span></span>

![Creare un indice](./media/sql-database-advisor-portal/sql-database-performance-recommendation.png)

## <a name="applying-recommendations"></a><span data-ttu-id="d8d8c-131">Applicazione delle raccomandazioni</span><span class="sxs-lookup"><span data-stu-id="d8d8c-131">Applying recommendations</span></span>
<span data-ttu-id="d8d8c-132">Database SQL di Azure offre controllo completo su come indicazioni vengono abilitati usando una qualsiasi delle tre opzioni seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="d8d8c-132">Azure SQL Database gives you full control over how recommendations are enabled using any of hello following three options:</span></span> 

* <span data-ttu-id="d8d8c-133">Applicare le singole indicazioni una alla volta.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-133">Apply individual recommendations one at a time.</span></span>
* <span data-ttu-id="d8d8c-134">Abilita hello tooautomatically ottimizzazione automatica applica indicazioni.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-134">Enable hello Automatic tuning tooautomatically apply recommendations.</span></span>
* <span data-ttu-id="d8d8c-135">tooimplement un'indicazione di eseguire manualmente, hello consigliato script T-SQL nel database.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-135">tooimplement a recommendation manually, run hello recommended T-SQL script against your database.</span></span>

<span data-ttu-id="d8d8c-136">Selezionare qualsiasi tooview raccomandazione i dettagli e quindi fare clic su **visualizzare script** tooreview hello dettagli esatti di modalità di creazione di raccomandazione hello.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-136">Select any recommendation tooview its details and then click **View script** tooreview hello exact details of how hello recommendation is created.</span></span>

<span data-ttu-id="d8d8c-137">database Hello rimane online durante raccomandazione hello viene applicato, l'utilizzo di suggerimento di prestazioni o l'ottimizzazione automatica mai richiede un database offline.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-137">hello database remains online while hello recommendation is applied -- using performance recommendation or automatic tuning never takes a database offline.</span></span>

### <a name="apply-an-individual-recommendation"></a><span data-ttu-id="d8d8c-138">Applicare una singola indicazione</span><span class="sxs-lookup"><span data-stu-id="d8d8c-138">Apply an individual recommendation</span></span>
<span data-ttu-id="d8d8c-139">È possibile leggere e accettare le indicazioni una alla volta.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-139">You can review and accept recommendations one at a time.</span></span>

1. <span data-ttu-id="d8d8c-140">In hello **indicazioni** pannello, selezionare una raccomandazione.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-140">On hello **Recommendations** blade, select a recommendation.</span></span>
2. <span data-ttu-id="d8d8c-141">In hello **dettagli** fare clic su pannello **applica** pulsante.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-141">On hello **Details** blade click **Apply** button.</span></span>
   
    ![Applica suggerimento](./media/sql-database-advisor-portal/apply.png)

<span data-ttu-id="d8d8c-143">Indicazione selezionata verrà applicata nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-143">Selected recommendation will be applied on hello database.</span></span>

### <a name="removing-recommendations-from-hello-list"></a><span data-ttu-id="d8d8c-144">Rimozione di indicazioni dall'elenco di hello</span><span class="sxs-lookup"><span data-stu-id="d8d8c-144">Removing recommendations from hello list</span></span>
<span data-ttu-id="d8d8c-145">Se l'elenco di suggerimenti contiene elementi che si desidera tooremove dall'elenco di hello, è possibile ignorare l'indicazione di hello:</span><span class="sxs-lookup"><span data-stu-id="d8d8c-145">If your list of recommendations contains items that you want tooremove from hello list, you can discard hello recommendation:</span></span>

1. <span data-ttu-id="d8d8c-146">Selezionare una raccomandazione nell'elenco di hello di **indicazioni** dettagli hello tooopen.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-146">Select a recommendation in hello list of **Recommendations** tooopen hello details.</span></span>
2. <span data-ttu-id="d8d8c-147">Fare clic su **ignorare** su hello **dettagli** blade.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-147">Click **Discard** on hello **Details** blade.</span></span>

<span data-ttu-id="d8d8c-148">Se si desidera, è possibile aggiungere elementi eliminati, eseguire il backup toohello **indicazioni** elenco:</span><span class="sxs-lookup"><span data-stu-id="d8d8c-148">If desired, you can add discarded items back toohello **Recommendations** list:</span></span>

1. <span data-ttu-id="d8d8c-149">In hello **indicazioni** fare clic su pannello **visualizzazione scartati**.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-149">On hello **Recommendations** blade click **View discarded**.</span></span>
2. <span data-ttu-id="d8d8c-150">Selezionare un elemento rimosso dall'hello elenco tooview i dettagli.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-150">Select a discarded item from hello list tooview its details.</span></span>
3. <span data-ttu-id="d8d8c-151">Facoltativamente, fare clic su **Annulla Elimina** tooadd hello indice toohello indietro elenco principale di **indicazioni**.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-151">Optionally, click **Undo Discard** tooadd hello index back toohello main list of **Recommendations**.</span></span>


### <a name="enable-automatic-tuning"></a><span data-ttu-id="d8d8c-152">Abilitare l'ottimizzazione automatica</span><span class="sxs-lookup"><span data-stu-id="d8d8c-152">Enable automatic tuning</span></span>
<span data-ttu-id="d8d8c-153">È possibile impostare automaticamente indicazioni tooimplement di hello Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-153">You can set hello Azure SQL Database tooimplement recommendations automatically.</span></span> <span data-ttu-id="d8d8c-154">Man mano che le indicazioni vengono rese disponibili, verranno applicate automaticamente.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-154">As recommendations become available they will automatically be applied.</span></span> <span data-ttu-id="d8d8c-155">Come con tutte le indicazioni gestite da hello servizio se l'impatto sulle prestazioni di hello è raccomandazione hello negativo verrà annullata.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-155">As with all recommendations managed by hello service if hello performance impact is negative hello recommendation will be reverted.</span></span>

1. <span data-ttu-id="d8d8c-156">In hello **indicazioni** pannello, fare clic su **automatizzare**:</span><span class="sxs-lookup"><span data-stu-id="d8d8c-156">On hello **Recommendations** blade, click **Automate**:</span></span>
   
    ![Impostazioni di Advisor](./media/sql-database-advisor-portal/settings.png)
2. <span data-ttu-id="d8d8c-158">Selezionare le azioni tooautomate:</span><span class="sxs-lookup"><span data-stu-id="d8d8c-158">Select actions tooautomate:</span></span>
   
    ![Indici consigliati](./media/sql-database-advisor-portal/automation.png)

### <a name="manually-run-hello-recommended-t-sql-script"></a><span data-ttu-id="d8d8c-160">Eseguire manualmente hello consigliato script T-SQL</span><span class="sxs-lookup"><span data-stu-id="d8d8c-160">Manually run hello recommended T-SQL script</span></span>
<span data-ttu-id="d8d8c-161">Selezionare qualsiasi raccomandazione e quindi fare clic su **Visualizza script**.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-161">Select any recommendation and then click **View script**.</span></span> <span data-ttu-id="d8d8c-162">Eseguire questo script per il database toomanually applicare l'indicazione di hello.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-162">Run this script against your database toomanually apply hello recommendation.</span></span>

<span data-ttu-id="d8d8c-163">*Gli indici che vengono eseguiti manualmente non monitorati e convalidati per verificarne l'impatto sulle prestazioni dal servizio hello* pertanto è consigliabile monitorare tali indici dopo la creazione tooverify forniscono i miglioramenti delle prestazioni e regolare o eliminarli se necessario.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-163">*Indexes that are manually executed are not monitored and validated for performance impact by hello service* so it is suggested that you monitor these indexes after creation tooverify they provide performance gains and adjust or delete them if necessary.</span></span> <span data-ttu-id="d8d8c-164">Per informazioni dettagliate sulla creazione di indici, vedere [CREAZIONE INDICE (Transact-SQL)](https://msdn.microsoft.com/library/ms188783.aspx).</span><span class="sxs-lookup"><span data-stu-id="d8d8c-164">For details about creating indexes, see [CREATE INDEX (Transact-SQL)](https://msdn.microsoft.com/library/ms188783.aspx).</span></span>

### <a name="canceling-recommendations"></a><span data-ttu-id="d8d8c-165">Annullamento delle raccomandazioni</span><span class="sxs-lookup"><span data-stu-id="d8d8c-165">Canceling recommendations</span></span>
<span data-ttu-id="d8d8c-166">Le raccomandazioni con stato **In sospeso**, **Verifica** o **Operazione completata** possono essere annullate.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-166">Recommendations that are in a **Pending**, **Verifying**, or **Success** status can be canceled.</span></span> <span data-ttu-id="d8d8c-167">Le raccomandazioni con stato **In esecuzione** non possono essere annullate.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-167">Recommendations with a status of **Executing** cannot be canceled.</span></span>

1. <span data-ttu-id="d8d8c-168">Selezionare un'indicazione in hello **cronologia ottimizzazione** hello tooopen area **dettagli indicazioni** blade.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-168">Select a recommendation in hello **Tuning History** area tooopen hello **recommendations details** blade.</span></span>
2. <span data-ttu-id="d8d8c-169">Fare clic su **Annulla** processo hello tooabort dell'applicazione hello dell'indicazione.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-169">Click **Cancel** tooabort hello process of applying hello recommendation.</span></span>

## <a name="monitoring-operations"></a><span data-ttu-id="d8d8c-170">Monitoraggio delle operazioni</span><span class="sxs-lookup"><span data-stu-id="d8d8c-170">Monitoring operations</span></span>
<span data-ttu-id="d8d8c-171">L'applicazione di un'indicazione potrebbe non avvenire in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-171">Applying a recommendation might not happen instantaneously.</span></span> <span data-ttu-id="d8d8c-172">portale Hello fornisce informazioni dettagliate relative allo stato di hello della raccomandazione.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-172">hello portal provides details regarding hello status of recommendation.</span></span> <span data-ttu-id="d8d8c-173">di seguito Hello sono stati possibili di un indice di:</span><span class="sxs-lookup"><span data-stu-id="d8d8c-173">hello following are possible states that an index can be in:</span></span>

| <span data-ttu-id="d8d8c-174">Stato</span><span class="sxs-lookup"><span data-stu-id="d8d8c-174">Status</span></span> | <span data-ttu-id="d8d8c-175">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d8d8c-175">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="d8d8c-176">In sospeso</span><span class="sxs-lookup"><span data-stu-id="d8d8c-176">Pending</span></span> |<span data-ttu-id="d8d8c-177">Il comando di applicazione della raccomandazione è stato ricevuto ed è pianificato per l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-177">Apply recommendation command has been received and is scheduled for execution.</span></span> |
| <span data-ttu-id="d8d8c-178">In esecuzione</span><span class="sxs-lookup"><span data-stu-id="d8d8c-178">Executing</span></span> |<span data-ttu-id="d8d8c-179">indicazione di Hello viene applicata.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-179">hello recommendation is being applied.</span></span> |
| <span data-ttu-id="d8d8c-180">Verifica</span><span class="sxs-lookup"><span data-stu-id="d8d8c-180">Verifying</span></span> |<span data-ttu-id="d8d8c-181">Indicazione è stata applicata e servizio hello misurati vantaggi hello.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-181">Recommendation was successfully applied and hello service is measuring hello benefits.</span></span> |
| <span data-ttu-id="d8d8c-182">Success</span><span class="sxs-lookup"><span data-stu-id="d8d8c-182">Success</span></span> |<span data-ttu-id="d8d8c-183">La raccomandazione è stata applicata e i vantaggi sono stati misurati.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-183">Recommendation was successfully applied and benefits have been measured.</span></span> |
| <span data-ttu-id="d8d8c-184">Errore</span><span class="sxs-lookup"><span data-stu-id="d8d8c-184">Error</span></span> |<span data-ttu-id="d8d8c-185">Si è verificato un errore durante il processo di hello dell'applicazione hello dell'indicazione.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-185">An error occurred during hello process of applying hello recommendation.</span></span> <span data-ttu-id="d8d8c-186">Può trattarsi di un problema temporaneo o eventualmente una tabella toohello delle modifiche dello schema e script hello non è più valido.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-186">This can be a transient issue, or possibly a schema change toohello table and hello script is no longer valid.</span></span> |
| <span data-ttu-id="d8d8c-187">Ripristino</span><span class="sxs-lookup"><span data-stu-id="d8d8c-187">Reverting</span></span> |<span data-ttu-id="d8d8c-188">indicazione di Hello è stato applicato, ma è stato considerato non ad alte prestazioni e viene viene ripristinato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-188">hello recommendation was applied, but has been deemed non-performant and is being automatically reverted.</span></span> |
| <span data-ttu-id="d8d8c-189">Ripristinato</span><span class="sxs-lookup"><span data-stu-id="d8d8c-189">Reverted</span></span> |<span data-ttu-id="d8d8c-190">indicazione di Hello è stata annullata.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-190">hello recommendation was reverted.</span></span> |

<span data-ttu-id="d8d8c-191">Fare clic su una raccomandazione in-process hello elenco toosee ulteriori dettagli:</span><span class="sxs-lookup"><span data-stu-id="d8d8c-191">Click an in-process recommendation from hello list toosee more details:</span></span>

![Indici consigliati](./media/sql-database-advisor-portal/operations.png)

### <a name="reverting-a-recommendation"></a><span data-ttu-id="d8d8c-193">Ripristino di una raccomandazione</span><span class="sxs-lookup"><span data-stu-id="d8d8c-193">Reverting a recommendation</span></span>
<span data-ttu-id="d8d8c-194">Se è stata utilizzata la raccomandazione hello hello prestazioni indicazioni tooapply (ovvero che non è stato eseguito manualmente script hello T-SQL) verrà automaticamente ripristinata, se trova toobe impatto sulle prestazioni di hello negativo.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-194">If you used hello performance recommendations tooapply hello recommendation (meaning you did not manually run hello T-SQL script) it will automatically revert it if it finds hello performance impact toobe negative.</span></span> <span data-ttu-id="d8d8c-195">Se per qualsiasi motivo si desidera semplicemente toorevert una raccomandazione non è seguito hello:</span><span class="sxs-lookup"><span data-stu-id="d8d8c-195">If for any reason you simply want toorevert a recommendation you can do hello following:</span></span>

1. <span data-ttu-id="d8d8c-196">Selezionare una raccomandazione applicata in hello **ottimizzazione cronologia** area.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-196">Select a successfully applied recommendation in hello **Tuning history** area.</span></span>
2. <span data-ttu-id="d8d8c-197">Fare clic su **Revert** su hello **dettagli sulle raccomandazioni** blade.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-197">Click **Revert** on hello **recommendation details** blade.</span></span>

![Indici consigliati](./media/sql-database-advisor-portal/details.png)

## <a name="monitoring-performance-impact-of-index-recommendations"></a><span data-ttu-id="d8d8c-199">Monitoraggio dell'impatto sulle prestazioni delle indicazioni relative agli indici</span><span class="sxs-lookup"><span data-stu-id="d8d8c-199">Monitoring performance impact of index recommendations</span></span>
<span data-ttu-id="d8d8c-200">Dopo aver indicazioni sono correttamente implementate (attualmente, operazioni sugli indici e parametrizzare solo i suggerimenti di query) è possibile fare clic su **informazioni dettagliate Query** su hello raccomandazione dettagli pannello tooopen [Query Informazioni dettagliate prestazioni](sql-database-query-performance.md) per verificarne l'impatto sulle prestazioni hello per le prime query.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-200">After recommendations are successfully implemented (currently, index operations and parameterize queries recommendations only) you can click **Query Insights** on hello recommendation details blade tooopen [Query Performance Insights](sql-database-query-performance.md) and see hello performance impact of your top queries.</span></span>

![Monitorare l'impatto sulle prestazioni](./media/sql-database-advisor-portal/query-insights.png)

## <a name="summary"></a><span data-ttu-id="d8d8c-202">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="d8d8c-202">Summary</span></span>
<span data-ttu-id="d8d8c-203">Il database SQL di Azure fornisce raccomandazioni per migliorare le prestazioni del database SQL.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-203">Azure SQL Database provides recommendations for improving SQL database performance.</span></span> <span data-ttu-id="d8d8c-204">Questa funzionalità offre script T-SQL, nonché opzioni singole e completamente automatizzate, e risulta molto utile per ottimizzare il database e quindi per migliorare le prestazioni delle query.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-204">By providing T-SQL scripts, as well as individual and fully-automatic, you get a helpful assistance in optimizing your database and ultimately improving query performance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d8d8c-205">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d8d8c-205">Next steps</span></span>
<span data-ttu-id="d8d8c-206">Monitorare le raccomandazioni e continuare tooapply li toorefine prestazioni.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-206">Monitor your recommendations and continue tooapply them toorefine performance.</span></span> <span data-ttu-id="d8d8c-207">I carichi di lavoro dei database sono dinamici e cambiano in modo continuo.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-207">Database workloads are dynamic and change continuously.</span></span> <span data-ttu-id="d8d8c-208">Database SQL di Azure continuerà toomonitor e fornire indicazioni che possono potenzialmente migliorare le prestazioni del database.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-208">Azure SQL Database will continue toomonitor and provide recommendations that can potentially improve your database's performance.</span></span> 

* <span data-ttu-id="d8d8c-209">Vedere [ottimizzazione automatica](sql-database-automatic-tuning.md) toolearn ulteriori informazioni sugli hello ottimizzazione automatica nel Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-209">See [Automatic tuning](sql-database-automatic-tuning.md) toolearn more about hello automatic tuning in Azure SQL Database.</span></span>
* <span data-ttu-id="d8d8c-210">Vedere le [Raccomandazioni per le prestazioni](sql-database-advisor.md) per una panoramica delle raccomandazioni per le prestazioni per il database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-210">See [Performance recommendations](sql-database-advisor.md) for an overview of Azure SQL Database performance recommendations.</span></span>
* <span data-ttu-id="d8d8c-211">Vedere [informazioni dettagliate prestazioni Query](sql-database-query-performance.md) toolearn sulla visualizzazione impatto sulle prestazioni hello per le prime query.</span><span class="sxs-lookup"><span data-stu-id="d8d8c-211">See [Query Performance Insights](sql-database-query-performance.md) toolearn about viewing hello performance impact of your top queries.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d8d8c-212">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="d8d8c-212">Additional resources</span></span>
* [<span data-ttu-id="d8d8c-213">Archivio query</span><span class="sxs-lookup"><span data-stu-id="d8d8c-213">Query Store</span></span>](https://msdn.microsoft.com/library/dn817826.aspx)
* [<span data-ttu-id="d8d8c-214">CREATE INDEX</span><span class="sxs-lookup"><span data-stu-id="d8d8c-214">CREATE INDEX</span></span>](https://msdn.microsoft.com/library/ms188783.aspx)
* [<span data-ttu-id="d8d8c-215">Controllo degli accessi in base al ruolo</span><span class="sxs-lookup"><span data-stu-id="d8d8c-215">Role-based access control</span></span>](../active-directory/role-based-access-control-what-is.md)

