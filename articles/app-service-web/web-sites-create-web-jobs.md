---
title: "aaaRun attività in Background con processi Web"
description: "Informazioni su come attività in background toorun in Azure web app."
services: app-service
documentationcenter: 
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: af01771e-54eb-4aea-af5f-f883ff39572b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/27/2016
ms.author: glenga
ms.openlocfilehash: 96a3d977a806e7192207f0f4da79dfd248694336
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-background-tasks-with-webjobs"></a><span data-ttu-id="eceaf-103">Eseguire attività in background con processi Web</span><span class="sxs-lookup"><span data-stu-id="eceaf-103">Run Background tasks with WebJobs</span></span>
## <a name="overview"></a><span data-ttu-id="eceaf-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="eceaf-104">Overview</span></span>
<span data-ttu-id="eceaf-105">È possibile eseguire programmi o script in Processi Web nell'app Web del [servizio app di Azure](http://go.microsoft.com/fwlink/?LinkId=529714) in tre modi: su richiesta, sempre, in base a una pianificazione.</span><span class="sxs-lookup"><span data-stu-id="eceaf-105">You can run programs or scripts in WebJobs in your [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) web app in three ways: on demand, continuously, or on a schedule.</span></span> <span data-ttu-id="eceaf-106">Non vi è alcun toouse costi aggiuntivi processi Web.</span><span class="sxs-lookup"><span data-stu-id="eceaf-106">There is no additional cost toouse WebJobs.</span></span>

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

<span data-ttu-id="eceaf-107">Questo articolo illustra come toodeploy processi Web usando hello [portale Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="eceaf-107">This article shows how toodeploy WebJobs by using hello [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="eceaf-108">Per informazioni su come toodeploy utilizzando Visual Studio o in un processo di distribuzione continua, vedere [come tooDeploy processi Web di Azure tooWeb app](websites-dotnet-deploy-webjobs.md).</span><span class="sxs-lookup"><span data-stu-id="eceaf-108">For information about how toodeploy by using Visual Studio or a continuous delivery process, see [How tooDeploy Azure WebJobs tooWeb Apps](websites-dotnet-deploy-webjobs.md).</span></span>

<span data-ttu-id="eceaf-109">Hello Azure WebJobs SDK semplifica molte attività di programmazione di processi Web.</span><span class="sxs-lookup"><span data-stu-id="eceaf-109">hello Azure WebJobs SDK simplifies many WebJobs programming tasks.</span></span> <span data-ttu-id="eceaf-110">Per ulteriori informazioni, vedere [novità hello WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="eceaf-110">For more information, see [What is hello WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span></span>

 <span data-ttu-id="eceaf-111">Funzioni di Azure fornisce un altro toorun programmi e script da un ambiente senza server o da un'applicazione di servizio App.</span><span class="sxs-lookup"><span data-stu-id="eceaf-111">Azure Functions provides another way toorun programs and scripts from either a serverless environment or from an App Service app.</span></span> <span data-ttu-id="eceaf-112">Per altre informazioni, vedere [Panoramica di Funzioni di Azure](../azure-functions/functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="eceaf-112">For more information, see [Azure Functions overview](../azure-functions/functions-overview.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="eceaf-113"><a name="acceptablefiles"></a>Tipi di file consentiti per script e programmi</span><span class="sxs-lookup"><span data-stu-id="eceaf-113"><a name="acceptablefiles"></a>Acceptable file types for scripts or programs</span></span>
<span data-ttu-id="eceaf-114">viene accettato i seguenti tipi di file Hello:</span><span class="sxs-lookup"><span data-stu-id="eceaf-114">hello following file types are accepted:</span></span>

* <span data-ttu-id="eceaf-115">.cmd, .bat, .exe (Prompt dei comandi di Windows)</span><span class="sxs-lookup"><span data-stu-id="eceaf-115">.cmd, .bat, .exe (using windows cmd)</span></span>
* <span data-ttu-id="eceaf-116">.ps1 (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="eceaf-116">.ps1 (using powershell)</span></span>
* <span data-ttu-id="eceaf-117">.sh (Bash)</span><span class="sxs-lookup"><span data-stu-id="eceaf-117">.sh (using bash)</span></span>
* <span data-ttu-id="eceaf-118">.php (PHP)</span><span class="sxs-lookup"><span data-stu-id="eceaf-118">.php (using php)</span></span>
* <span data-ttu-id="eceaf-119">.py (Python)</span><span class="sxs-lookup"><span data-stu-id="eceaf-119">.py (using python)</span></span>
* <span data-ttu-id="eceaf-120">.js (Node)</span><span class="sxs-lookup"><span data-stu-id="eceaf-120">.js (using node)</span></span>
* <span data-ttu-id="eceaf-121">JAR (Java)</span><span class="sxs-lookup"><span data-stu-id="eceaf-121">.jar (using java)</span></span>

## <span data-ttu-id="eceaf-122"><a name="CreateOnDemand"></a>Creare un processo Web report su richiesta nel portale di hello</span><span class="sxs-lookup"><span data-stu-id="eceaf-122"><a name="CreateOnDemand"></a>Create an on demand WebJob in hello portal</span></span>
1. <span data-ttu-id="eceaf-123">In hello **App Web** blade di hello [portale Azure](https://portal.azure.com), fare clic su **tutte le impostazioni > processi Web** tooshow hello **processi Web** blade.</span><span class="sxs-lookup"><span data-stu-id="eceaf-123">In hello **Web App** blade of hello [Azure Portal](https://portal.azure.com), click **All settings > WebJobs** tooshow hello **WebJobs** blade.</span></span>
   
    ![Pannello Processi Web](./media/web-sites-create-web-jobs/wjblade.png)
2. <span data-ttu-id="eceaf-125">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="eceaf-125">Click **Add**.</span></span> <span data-ttu-id="eceaf-126">Hello **Aggiungi processo Web** viene visualizzata la finestra.</span><span class="sxs-lookup"><span data-stu-id="eceaf-126">hello **Add WebJob** dialog appears.</span></span>
   
    ![Pannello Aggiungi processo Web](./media/web-sites-create-web-jobs/addwjblade.png)
3. <span data-ttu-id="eceaf-128">In **nome**, specificare un nome per hello processo Web.</span><span class="sxs-lookup"><span data-stu-id="eceaf-128">Under **Name**, provide a name for hello WebJob.</span></span> <span data-ttu-id="eceaf-129">nome di Hello deve iniziare con una lettera o un numero e può contenere caratteri speciali diversi da "-" e "_".</span><span class="sxs-lookup"><span data-stu-id="eceaf-129">hello name must start with a letter or a number and cannot contain any special characters other than "-" and "_".</span></span>
4. <span data-ttu-id="eceaf-130">In hello **come tooRun** scegliere **eseguiti su richiesta**.</span><span class="sxs-lookup"><span data-stu-id="eceaf-130">In hello **How tooRun** box, choose **Run on Demand**.</span></span>
5. <span data-ttu-id="eceaf-131">In hello **caricamento File** fare clic sull'icona di cartella hello e individuare i file zip toohello contenente lo script.</span><span class="sxs-lookup"><span data-stu-id="eceaf-131">In hello **File Upload** box, click hello folder icon and browse toohello zip file that contains your script.</span></span> <span data-ttu-id="eceaf-132">file zip Hello deve contenere il file eseguibile (.exe cmd. bat. sh. PHP. py. js) nonché eventuali file di supporto necessari toorun hello programmi o script.</span><span class="sxs-lookup"><span data-stu-id="eceaf-132">hello zip file should contain your executable (.exe .cmd .bat .sh .php .py .js) as well as any supporting files needed toorun hello program or script.</span></span>
6. <span data-ttu-id="eceaf-133">Controllare **crea** tooupload hello script tooyour web app.</span><span class="sxs-lookup"><span data-stu-id="eceaf-133">Check **Create** tooupload hello script tooyour web app.</span></span> 
   
    <span data-ttu-id="eceaf-134">Hello nome specificato per hello processo Web viene visualizzato nell'elenco hello hello **processi Web** blade.</span><span class="sxs-lookup"><span data-stu-id="eceaf-134">hello name you specified for hello WebJob appears in hello list on hello **WebJobs** blade.</span></span>
7. <span data-ttu-id="eceaf-135">hello toorun processo Web, mouse sul nome nell'elenco di hello e fare clic su **eseguire**.</span><span class="sxs-lookup"><span data-stu-id="eceaf-135">toorun hello WebJob, right-click its name in hello list and click **Run**.</span></span>
   
    ![Eseguire un processo Web](./media/web-sites-create-web-jobs/runondemand.png)

## <span data-ttu-id="eceaf-137"><a name="CreateContinuous"></a>Creare un processo Web con esecuzione continua</span><span class="sxs-lookup"><span data-stu-id="eceaf-137"><a name="CreateContinuous"></a>Create a continuously running WebJob</span></span>
1. <span data-ttu-id="eceaf-138">toocreate un processo Web continuamente in esecuzione, seguire hello stessi passaggi per la creazione di un processo Web che viene eseguito una volta, ma in hello **come tooRun** scegliere **continuo**.</span><span class="sxs-lookup"><span data-stu-id="eceaf-138">toocreate a continuously executing WebJob, follow hello same steps for creating a WebJob that runs once, but in hello **How tooRun** box, choose **Continuous**.</span></span>
2. <span data-ttu-id="eceaf-139">toostart o arrestare un processo Web continuo, fare doppio clic su hello processo Web nell'elenco di hello e fare clic su **avviare** o **arrestare**.</span><span class="sxs-lookup"><span data-stu-id="eceaf-139">toostart or stop a continuous WebJob, right-click hello WebJob in hello list and click **Start** or **Stop**.</span></span>

> [!NOTE]
> <span data-ttu-id="eceaf-140">Se l'app Web è in esecuzione su più di un'istanza, il processo Web con esecuzione continua verrà eseguito su tutte le istanze.</span><span class="sxs-lookup"><span data-stu-id="eceaf-140">If your web app runs on more than one instance, a continuously running WebJob will run on all of your instances.</span></span> <span data-ttu-id="eceaf-141">I processi Web su richiesta e pianificati vengono eseguiti su una singola istanza selezionata per il bilanciamento del carico da Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="eceaf-141">On-demand and scheduled WebJobs run on a single instance selected for load balancing by Microsoft Azure.</span></span>
> 
> <span data-ttu-id="eceaf-142">Per i processi Web continui toorun in modo affidabile e in tutte le istanze, abilitare hello Always On * impostazione di configurazione per hello app web in caso contrario è possibile interrompere l'esecuzione quando il sito di host SCM hello è rimasto inattivo per troppo tempo.</span><span class="sxs-lookup"><span data-stu-id="eceaf-142">For Continuous WebJobs toorun reliably and on all instances, enable hello Always On* configuration setting for hello web app otherwise they can stop running when hello SCM host site has been idle for too long.</span></span>
> 
> 

## <span data-ttu-id="eceaf-143"><a name="CreateScheduledCRON"></a>Creare un processo Web pianificato utilizzando un'espressione CRON</span><span class="sxs-lookup"><span data-stu-id="eceaf-143"><a name="CreateScheduledCRON"></a>Create a scheduled WebJob using a CRON expression</span></span>
<span data-ttu-id="eceaf-144">Questa tecnica è disponibile tooWeb App in esecuzione in modalità Basic, Standard o Premium e richiede hello **Always On** impostazione toobe attivata app hello.</span><span class="sxs-lookup"><span data-stu-id="eceaf-144">This technique is available tooWeb Apps running in Basic, Standard or Premium mode, and requires hello **Always On** setting toobe enabled on hello app.</span></span>

<span data-ttu-id="eceaf-145">tooturn sul processo Web richiesta in un processo Web pianificato, includere semplicemente un `settings.job` file alla radice di hello del file zip processo Web.</span><span class="sxs-lookup"><span data-stu-id="eceaf-145">tooturn an On Demand WebJob into a scheduled WebJob, simply include a `settings.job` file at hello root of your WebJob zip file.</span></span> <span data-ttu-id="eceaf-146">Questo file JSON deve includere una `schedule` proprietà con un [espressione CRON](https://en.wikipedia.org/wiki/Cron), per esempio quanto riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="eceaf-146">This JSON file should include a `schedule` property with a [CRON expression](https://en.wikipedia.org/wiki/Cron), per example below.</span></span>

<span data-ttu-id="eceaf-147">espressione CRON Hello è costituita da 6 campi: `{second} {minute} {hour} {day} {month} {day of hello week}`.</span><span class="sxs-lookup"><span data-stu-id="eceaf-147">hello CRON expression is composed of 6 fields: `{second} {minute} {hour} {day} {month} {day of hello week}`.</span></span>

<span data-ttu-id="eceaf-148">Ad esempio, tootrigger del processo Web ogni 15 minuti, il `settings.job` sarebbe:</span><span class="sxs-lookup"><span data-stu-id="eceaf-148">For example, tootrigger your WebJob every 15 minutes, your `settings.job` would have:</span></span>

```json
{
    "schedule": "0 */15 * * * *"
}
``` 

<span data-ttu-id="eceaf-149">Altri esempi di programmazione CRON:</span><span class="sxs-lookup"><span data-stu-id="eceaf-149">Other CRON schedule examples:</span></span>

* <span data-ttu-id="eceaf-150">Ogni ora (ad esempio ogni volta che il numero di hello di minuti è 0):`0 0 * * * *`</span><span class="sxs-lookup"><span data-stu-id="eceaf-150">Every hour (i.e. whenever hello count of minutes is 0): `0 0 * * * *`</span></span> 
* <span data-ttu-id="eceaf-151">Ogni ora da too5 09: 00 PM:`0 0 9-17 * * *`</span><span class="sxs-lookup"><span data-stu-id="eceaf-151">Every hour from 9 AM too5 PM: `0 0 9-17 * * *`</span></span> 
* <span data-ttu-id="eceaf-152">Alle 9:30 di mattina ogni giorno: `0 30 9 * * *`</span><span class="sxs-lookup"><span data-stu-id="eceaf-152">At 9:30 AM every day: `0 30 9 * * *`</span></span>
* <span data-ttu-id="eceaf-153">Alle 9:30 di mattina ogni giorno della settimana: `0 30 9 * * 1-5`</span><span class="sxs-lookup"><span data-stu-id="eceaf-153">At 9:30 AM every week day: `0 30 9 * * 1-5`</span></span>

<span data-ttu-id="eceaf-154">**Nota**: quando si distribuisce un processo Web da Visual Studio, assicurarsi che toomark il `settings.job` proprietà file come 'Copia se più recente'.</span><span class="sxs-lookup"><span data-stu-id="eceaf-154">**Note**: when deploying a WebJob from Visual Studio, make sure toomark your `settings.job` file properties as 'Copy if newer'.</span></span>

## <span data-ttu-id="eceaf-155"><a name="CreateScheduled"></a>Creare un processo Web pianificato usando hello dell'utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="eceaf-155"><a name="CreateScheduled"></a>Create a scheduled WebJob using hello Azure Scheduler</span></span>
<span data-ttu-id="eceaf-156">Hello tecnica alternativa seguente si avvalgono di hello dell'utilità di pianificazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="eceaf-156">hello following alternate technique makes use of hello Azure Scheduler.</span></span> <span data-ttu-id="eceaf-157">In questo caso, il processo Web ha alcuna conoscenza diretta della pianificazione hello.</span><span class="sxs-lookup"><span data-stu-id="eceaf-157">In this case, your WebJob does not have any direct knowledge of hello schedule.</span></span> <span data-ttu-id="eceaf-158">Al contrario, hello dell'utilità di pianificazione di Azure Ottiene tootrigger configurato del processo Web su una pianificazione.</span><span class="sxs-lookup"><span data-stu-id="eceaf-158">Instead, hello Azure Scheduler gets configured tootrigger your WebJob on a schedule.</span></span> 

<span data-ttu-id="eceaf-159">Hello portale di Azure non dispone ancora di hello possibilità toocreate un processo Web pianificato, ma solo dopo l'aggiunta di tale funzionalità è possibile farlo tramite hello [portale classico](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="eceaf-159">hello Azure Portal doesn't yet have hello ability toocreate a scheduled WebJob, but until that feature is added you can do it by using hello [classic portal](http://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="eceaf-160">In hello [portale classico](http://manage.windowsazure.com) toohello processo Web pagina, fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="eceaf-160">In hello [classic portal](http://manage.windowsazure.com) go toohello WebJob page and click **Add**.</span></span>
2. <span data-ttu-id="eceaf-161">In hello **come tooRun** scegliere **eseguita in una pianificazione**.</span><span class="sxs-lookup"><span data-stu-id="eceaf-161">In hello **How tooRun** box, choose **Run on a schedule**.</span></span>
   
    ![Nuovo processo pianificato][NewScheduledJob]
3. <span data-ttu-id="eceaf-163">Scegliere hello **area dell'utilità di pianificazione** per il processo, quindi fare clic sulla freccia di hello in hello basso a destra hello finestra di dialogo tooproceed toohello nella schermata successiva.</span><span class="sxs-lookup"><span data-stu-id="eceaf-163">Choose hello **Scheduler Region** for your job, and then click hello arrow on hello bottom right of hello dialog tooproceed toohello next screen.</span></span>
4. <span data-ttu-id="eceaf-164">In hello **Crea processo** finestra di dialogo, scegliere il tipo di hello di **ricorrenza** desiderato: **processo occasionale** o **processo ricorrente**.</span><span class="sxs-lookup"><span data-stu-id="eceaf-164">In hello **Create Job** dialog, choose hello type of **Recurrence** you want: **One-time job** or **Recurring job**.</span></span>
   
    ![Pianificare la ricorrenza][SchdRecurrence]
5. <span data-ttu-id="eceaf-166">Scegliere un'ora di **inizio**: **Ora** o **A un orario specifico**.</span><span class="sxs-lookup"><span data-stu-id="eceaf-166">Also choose a **Starting** time: **Now** or **At a specific time**.</span></span>
   
    ![Pianificare l'ora di inizio][SchdStart]
6. <span data-ttu-id="eceaf-168">Se si desidera toostart in un momento specifico, scegliere i valori di ora iniziale in **avvio su**.</span><span class="sxs-lookup"><span data-stu-id="eceaf-168">If you want toostart at a specific time, choose your starting time values under **Starting On**.</span></span>
   
    ![Pianificare l'avvio a un'ora specifica][SchdStartOn]
7. <span data-ttu-id="eceaf-170">Se si sceglie un processo ricorrente, è necessario hello **ricorre ogni** opzione frequenza hello toospecify di occorrenza e hello **che terminano in** toospecify opzione un'ora di fine.</span><span class="sxs-lookup"><span data-stu-id="eceaf-170">If you chose a recurring job, you have hello **Recur Every** option toospecify hello frequency of occurrence and hello **Ending On** option toospecify an ending time.</span></span>
   
    ![Pianificare la ricorrenza][SchdRecurEvery]
8. <span data-ttu-id="eceaf-172">Se si sceglie **settimane**, è possibile selezionare hello **su una determinata pianificazione** e specificare hello giorni hello che si desidera hello toorun di processo.</span><span class="sxs-lookup"><span data-stu-id="eceaf-172">If you choose **Weeks**, you can select hello **On a Particular Schedule** box and specify hello days of hello week that you want hello job toorun.</span></span>
   
    ![Giorni di pianificazione di hello settimana][SchdWeeksOnParticular]
9. <span data-ttu-id="eceaf-174">Se si sceglie **mesi** e seleziona hello **su una determinata pianificazione** casella, è possibile impostare toorun processo hello in particolare numerati **giorni** nel mese di hello.</span><span class="sxs-lookup"><span data-stu-id="eceaf-174">If you choose **Months** and select hello **On a Particular Schedule** box, you can set hello job toorun on particular numbered **Days** in hello month.</span></span> 
   
    ![Pianificare le date particolare hello mese][SchdMonthsOnPartDays]
10. <span data-ttu-id="eceaf-176">Se si sceglie **giorni della settimana**, è possibile selezionare quale giorno o giorni della settimana hello desiderato hello toorun processo nel mese di hello.</span><span class="sxs-lookup"><span data-stu-id="eceaf-176">If you choose **Week Days**, you can select which day or days of hello week in hello month you want hello job toorun on.</span></span>
    
     ![Pianificare giorni della settimana specifici in un mese][SchdMonthsOnPartWeekDays]
11. <span data-ttu-id="eceaf-178">Infine, è inoltre possibile utilizzare hello **occorrenze** opzione toochoose la settimana del mese hello (primo, secondo, terzo e così via) si desidera toorun processo hello in hello giorni della settimana specificato.</span><span class="sxs-lookup"><span data-stu-id="eceaf-178">Finally, you can also use hello **Occurrences** option toochoose which week in hello month (first, second, third etc.) you want hello job toorun on hello week days you specified.</span></span>
    
    ![Pianificare giorni della settimana specifici per determinate settimane in un mese][SchdMonthsOnPartWeekDaysOccurences]
12. <span data-ttu-id="eceaf-180">Dopo aver creato uno o più processi, i relativi nomi verranno visualizzati nella scheda processi Web hello con relativo stato, il tipo di pianificazione e altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="eceaf-180">After you have created one or more jobs, their names will appear on hello WebJobs tab with their status, schedule type, and other information.</span></span> <span data-ttu-id="eceaf-181">Informazioni cronologiche per hello ultimi 30 processi Web viene mantenute.</span><span class="sxs-lookup"><span data-stu-id="eceaf-181">Historical information for hello last 30  WebJobs is maintained.</span></span>
    
    ![Elenco processi][WebJobsListWithSeveralJobs]

### <span data-ttu-id="eceaf-183"><a name="Scheduler"></a>Processi pianificati e Utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="eceaf-183"><a name="Scheduler"></a>Scheduled jobs and Azure Scheduler</span></span>
<span data-ttu-id="eceaf-184">I processi pianificati possono essere ulteriormente configurati nelle pagine di pianificazione di Azure hello di hello [portale classico](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="eceaf-184">Scheduled jobs can be further configured in hello Azure Scheduler pages of hello [classic portal](http://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="eceaf-185">Nella pagina processi Web hello, fare clic su del processo di hello **pianificazione** pagina del portale di collegamento toonavigate toohello dell'utilità di pianificazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="eceaf-185">On hello WebJobs page, click hello job's **schedule** link toonavigate toohello Azure Scheduler portal page.</span></span> 
   
   ![Collegamento tooAzure dell'utilità di pianificazione][LinkToScheduler]
2. <span data-ttu-id="eceaf-187">Nella pagina di hello dell'utilità di pianificazione, fare clic su processo hello.</span><span class="sxs-lookup"><span data-stu-id="eceaf-187">On hello Scheduler page, click hello job.</span></span>
   
    ![Processo nella pagina del portale di hello dell'utilità di pianificazione][SchedulerPortal]
3. <span data-ttu-id="eceaf-189">Hello **azione del processo** pagina visualizzata, in cui è possibile configurare ulteriormente il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="eceaf-189">hello **Job Action** page opens, where you can further configure hello job.</span></span> 
   
    ![Pagina Job Action nell'Utilità di pianificazione][JobActionPageInScheduler]

## <span data-ttu-id="eceaf-191"><a name="ViewJobHistory"></a>Visualizza cronologia processi hello</span><span class="sxs-lookup"><span data-stu-id="eceaf-191"><a name="ViewJobHistory"></a>View hello job history</span></span>
1. <span data-ttu-id="eceaf-192">cronologia di esecuzione hello tooview di un processo, inclusi i processi creati con hello WebJobs SDK, fare clic sul collegamento corrispondente in hello **registri** colonna del Pannello di processi Web hello.</span><span class="sxs-lookup"><span data-stu-id="eceaf-192">tooview hello execution history of a job, including jobs created with hello WebJobs SDK, click  its corresponding link under hello **Logs** column of hello WebJobs blade.</span></span> <span data-ttu-id="eceaf-193">(È possibile utilizzare URL hello toocopy hello Appunti icona degli Appunti toohello di hello log file pagina se si desidera).</span><span class="sxs-lookup"><span data-stu-id="eceaf-193">(You can use hello clipboard icon toocopy hello URL of hello log file page toohello clipboard if you wish.)</span></span>
   
    ![Collegamento Log](./media/web-sites-create-web-jobs/wjbladelogslink.png)
2. <span data-ttu-id="eceaf-195">Facendo clic su collegamento hello verrà visualizzata la pagina dei dettagli hello per hello processo Web.</span><span class="sxs-lookup"><span data-stu-id="eceaf-195">Clicking hello link opens hello details page for hello WebJob.</span></span> <span data-ttu-id="eceaf-196">Viene illustrata questa pagina hello nome dell'esecuzione del comando hello, hello ora dell'ultima esecuzione, e il relativo esito positivo o negativo.</span><span class="sxs-lookup"><span data-stu-id="eceaf-196">This page shows you hello name of hello command run, hello last times it ran, and its success or failure.</span></span> <span data-ttu-id="eceaf-197">In **processi recenti**, fare clic su un toosee di tempo ulteriori dettagli.</span><span class="sxs-lookup"><span data-stu-id="eceaf-197">Under **Recent job runs**, click a time toosee further details.</span></span>
   
    ![WebJobDetails][WebJobDetails]
3. <span data-ttu-id="eceaf-199">Hello **Dettagli esecuzione attività** verrà visualizzata la pagina.</span><span class="sxs-lookup"><span data-stu-id="eceaf-199">hello **WebJob Run Details** page appears.</span></span> <span data-ttu-id="eceaf-200">Fare clic su **attiva/disattiva Output** testo hello toosee del contenuto del log hello.</span><span class="sxs-lookup"><span data-stu-id="eceaf-200">Click **Toggle Output** toosee hello text of hello log contents.</span></span> <span data-ttu-id="eceaf-201">log di output di Hello è in formato testo.</span><span class="sxs-lookup"><span data-stu-id="eceaf-201">hello output log is in text format.</span></span> 
   
    ![Dettagli dell'esecuzione del processo Web][WebJobRunDetails]
4. <span data-ttu-id="eceaf-203">testo di output di hello toosee in una finestra distinta del browser, fare clic su hello **scaricare** collegamento.</span><span class="sxs-lookup"><span data-stu-id="eceaf-203">toosee hello output text in a separate browser window, click hello **download** link.</span></span> <span data-ttu-id="eceaf-204">testo hello toodownload, fare doppio clic su collegamento hello e utilizzare il contenuto del file hello toosave opzioni del browser.</span><span class="sxs-lookup"><span data-stu-id="eceaf-204">toodownload hello text itself, right-click hello link and use your browser options toosave hello file contents.</span></span>
   
    ![Download dell'output del log][DownloadLogOutput]
5. <span data-ttu-id="eceaf-206">Hello **processi Web** collegamento nella parte superiore di hello della pagina hello fornisce un elenco di tooa tooget di pratica di processi Web nel dashboard di cronologia hello.</span><span class="sxs-lookup"><span data-stu-id="eceaf-206">hello **WebJobs** link at hello top of hello page provides a convenient way tooget tooa list of WebJobs on hello history dashboard.</span></span>
   
    ![Elenco di collegamenti tooWebJobs][WebJobsLinkToDashboardList]
   
    ![Elenco dei processi nel dashboard della cronologia][WebJobsListInJobsDashboard]
   
    <span data-ttu-id="eceaf-209">Fare clic su uno di questi collegamenti accetta pagina dettagli attività toohello per processo hello selezionato.</span><span class="sxs-lookup"><span data-stu-id="eceaf-209">Clicking one of these links takes you toohello WebJob Details page for hello job you selected.</span></span>

## <span data-ttu-id="eceaf-210"><a name="WHPNotes"></a>Note</span><span class="sxs-lookup"><span data-stu-id="eceaf-210"><a name="WHPNotes"></a>Notes</span></span>
* <span data-ttu-id="eceaf-211">App Web in modalità disponibile può causare il timeout dopo 20 minuti se sono non presenti Nessun sito di richieste toohello scm (distribuzione) e portale hello app web non è aperta in Azure.</span><span class="sxs-lookup"><span data-stu-id="eceaf-211">Web apps in Free mode can time out after 20 minutes if there are no requests toohello scm (deployment) site and hello web app's portal is not open in Azure.</span></span> <span data-ttu-id="eceaf-212">Del sito effettivo di richieste toohello non verrà reimpostate questo.</span><span class="sxs-lookup"><span data-stu-id="eceaf-212">Requests toohello actual site will not reset this.</span></span>
* <span data-ttu-id="eceaf-213">Il codice per un processo continuo deve toobe scritto toorun in un ciclo infinito.</span><span class="sxs-lookup"><span data-stu-id="eceaf-213">Code for a continuous job needs toobe written toorun in an endless loop.</span></span>
* <span data-ttu-id="eceaf-214">I processi continui eseguiti continuamente solo quando l'applicazione web hello è attiva.</span><span class="sxs-lookup"><span data-stu-id="eceaf-214">Continuous jobs run continuously only when hello web app is up.</span></span>
* <span data-ttu-id="eceaf-215">Base e la modalità Standard offerta hello sempre nella funzionalità che, se abilitata, impedisce alle App web di diventa inattivo.</span><span class="sxs-lookup"><span data-stu-id="eceaf-215">Basic and Standard modes offer hello Always On feature which, when enabled, prevents web apps from becoming idle.</span></span>
* <span data-ttu-id="eceaf-216">È possibile solo eseguire il debug di processi Web con esecuzione continua.</span><span class="sxs-lookup"><span data-stu-id="eceaf-216">You can only debug continuously running WebJobs.</span></span> <span data-ttu-id="eceaf-217">Il debug di processi Web pianificati o su richiesta non è supportato.</span><span class="sxs-lookup"><span data-stu-id="eceaf-217">Debugging scheduled or on-demand WebJobs is not supported.</span></span>

## <span data-ttu-id="eceaf-218"><a name="NextSteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="eceaf-218"><a name="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="eceaf-219">Per altre informazioni, vedere l'articolo relativo alle [risorse consigliate per i processi Web di Azure][WebJobsRecommendedResources].</span><span class="sxs-lookup"><span data-stu-id="eceaf-219">For more information, see [Azure WebJobs Recommended Resources][WebJobsRecommendedResources].</span></span>

[PSonWebJobs]:http://blogs.msdn.com/b/nicktrog/archive/2014/01/22/running-powershell-web-jobs-on-azure-websites.aspx
[WebJobsRecommendedResources]:http://go.microsoft.com/fwlink/?LinkId=390226

[OnDemandWebJob]: ./media/web-sites-create-web-jobs/01aOnDemandWebJob.png
[WebJobsList]: ./media/web-sites-create-web-jobs/02aWebJobsList.png
[NewContinuousJob]: ./media/web-sites-create-web-jobs/03aNewContinuousJob.png
[NewScheduledJob]: ./media/web-sites-create-web-jobs/04aNewScheduledJob.png
[SchdRecurrence]: ./media/web-sites-create-web-jobs/05SchdRecurrence.png
[SchdStart]: ./media/web-sites-create-web-jobs/06SchdStart.png
[SchdStartOn]: ./media/web-sites-create-web-jobs/07SchdStartOn.png
[SchdRecurEvery]: ./media/web-sites-create-web-jobs/08SchdRecurEvery.png
[SchdWeeksOnParticular]: ./media/web-sites-create-web-jobs/09SchdWeeksOnParticular.png
[SchdMonthsOnPartDays]: ./media/web-sites-create-web-jobs/10SchdMonthsOnPartDays.png
[SchdMonthsOnPartWeekDays]: ./media/web-sites-create-web-jobs/11SchdMonthsOnPartWeekDays.png
[SchdMonthsOnPartWeekDaysOccurences]: ./media/web-sites-create-web-jobs/12SchdMonthsOnPartWeekDaysOccurences.png
[RunOnce]: ./media/web-sites-create-web-jobs/13RunOnce.png
[WebJobsListWithSeveralJobs]: ./media/web-sites-create-web-jobs/13WebJobsListWithSeveralJobs.png
[WebJobLogs]: ./media/web-sites-create-web-jobs/14WebJobLogs.png
[WebJobDetails]: ./media/web-sites-create-web-jobs/15WebJobDetails.png
[WebJobRunDetails]: ./media/web-sites-create-web-jobs/16WebJobRunDetails.png
[DownloadLogOutput]: ./media/web-sites-create-web-jobs/17DownloadLogOutput.png
[WebJobsLinkToDashboardList]: ./media/web-sites-create-web-jobs/18WebJobsLinkToDashboardList.png
[WebJobsListInJobsDashboard]: ./media/web-sites-create-web-jobs/19WebJobsListInJobsDashboard.png
[LinkToScheduler]: ./media/web-sites-create-web-jobs/31LinkToScheduler.png
[SchedulerPortal]: ./media/web-sites-create-web-jobs/32SchedulerPortal.png
[JobActionPageInScheduler]: ./media/web-sites-create-web-jobs/33JobActionPageInScheduler.png

