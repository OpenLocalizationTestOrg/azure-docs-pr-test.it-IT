---
title: "Eseguire attività in background con processi Web"
description: "Informazioni su come eseguire attività in background nelle app Web di Azure."
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
ms.openlocfilehash: 3f8ae748e3d9c6b4e342536926a52b4e8f37ee51
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="run-background-tasks-with-webjobs"></a><span data-ttu-id="a6962-103">Eseguire attività in background con processi Web</span><span class="sxs-lookup"><span data-stu-id="a6962-103">Run Background tasks with WebJobs</span></span>
## <a name="overview"></a><span data-ttu-id="a6962-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="a6962-104">Overview</span></span>
<span data-ttu-id="a6962-105">È possibile eseguire programmi o script in Processi Web nell'app Web del [servizio app di Azure](http://go.microsoft.com/fwlink/?LinkId=529714) in tre modi: su richiesta, sempre, in base a una pianificazione.</span><span class="sxs-lookup"><span data-stu-id="a6962-105">You can run programs or scripts in WebJobs in your [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) web app in three ways: on demand, continuously, or on a schedule.</span></span> <span data-ttu-id="a6962-106">Non sono previsti costi aggiuntivi per l'uso di Processi Web.</span><span class="sxs-lookup"><span data-stu-id="a6962-106">There is no additional cost to use WebJobs.</span></span>

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

<span data-ttu-id="a6962-107">Nell'articolo viene descritto come distribuire Processi Web utilizzando il [Portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a6962-107">This article shows how to deploy WebJobs by using the [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="a6962-108">Per informazioni sulla distribuzione mediante Visual Studio o un processo di distribuzione continua, vedere [Come distribuire Processi Web di Azure nelle App Web](websites-dotnet-deploy-webjobs.md).</span><span class="sxs-lookup"><span data-stu-id="a6962-108">For information about how to deploy by using Visual Studio or a continuous delivery process, see [How to Deploy Azure WebJobs to Web Apps](websites-dotnet-deploy-webjobs.md).</span></span>

<span data-ttu-id="a6962-109">Azure WebJobs SDK semplifica molte attività di programmazione dei processi Web.</span><span class="sxs-lookup"><span data-stu-id="a6962-109">The Azure WebJobs SDK simplifies many WebJobs programming tasks.</span></span> <span data-ttu-id="a6962-110">Per ulteriori informazioni, vedere [Definizione dell'SDK di Processi Web](websites-dotnet-webjobs-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="a6962-110">For more information, see [What is the WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span></span>

 <span data-ttu-id="a6962-111">Funzioni di Azure offre un altro modo per eseguire programmi e script da un ambiente senza server o da un'app Servizio app.</span><span class="sxs-lookup"><span data-stu-id="a6962-111">Azure Functions provides another way to run programs and scripts from either a serverless environment or from an App Service app.</span></span> <span data-ttu-id="a6962-112">Per altre informazioni, vedere [Panoramica di Funzioni di Azure](../azure-functions/functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a6962-112">For more information, see [Azure Functions overview](../azure-functions/functions-overview.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="a6962-113"><a name="acceptablefiles"></a>Tipi di file consentiti per script e programmi</span><span class="sxs-lookup"><span data-stu-id="a6962-113"><a name="acceptablefiles"></a>Acceptable file types for scripts or programs</span></span>
<span data-ttu-id="a6962-114">Sono consentiti i tipi di file seguenti:</span><span class="sxs-lookup"><span data-stu-id="a6962-114">The following file types are accepted:</span></span>

* <span data-ttu-id="a6962-115">.cmd, .bat, .exe (Prompt dei comandi di Windows)</span><span class="sxs-lookup"><span data-stu-id="a6962-115">.cmd, .bat, .exe (using windows cmd)</span></span>
* <span data-ttu-id="a6962-116">.ps1 (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="a6962-116">.ps1 (using powershell)</span></span>
* <span data-ttu-id="a6962-117">.sh (Bash)</span><span class="sxs-lookup"><span data-stu-id="a6962-117">.sh (using bash)</span></span>
* <span data-ttu-id="a6962-118">.php (PHP)</span><span class="sxs-lookup"><span data-stu-id="a6962-118">.php (using php)</span></span>
* <span data-ttu-id="a6962-119">.py (Python)</span><span class="sxs-lookup"><span data-stu-id="a6962-119">.py (using python)</span></span>
* <span data-ttu-id="a6962-120">.js (Node)</span><span class="sxs-lookup"><span data-stu-id="a6962-120">.js (using node)</span></span>
* <span data-ttu-id="a6962-121">JAR (Java)</span><span class="sxs-lookup"><span data-stu-id="a6962-121">.jar (using java)</span></span>

## <span data-ttu-id="a6962-122"><a name="CreateOnDemand"></a>Creare un processo Web su richiesta nel portale</span><span class="sxs-lookup"><span data-stu-id="a6962-122"><a name="CreateOnDemand"></a>Create an on demand WebJob in the portal</span></span>
1. <span data-ttu-id="a6962-123">Nel pannello **App Web** del [Portale di Azure](https://portal.azure.com) fare clic su **Tutte le impostazioni > Processi Web** per visualizzare il pannello **Processi Web**.</span><span class="sxs-lookup"><span data-stu-id="a6962-123">In the **Web App** blade of the [Azure Portal](https://portal.azure.com), click **All settings > WebJobs** to show the **WebJobs** blade.</span></span>
   
    ![Pannello Processi Web](./media/web-sites-create-web-jobs/wjblade.png)
2. <span data-ttu-id="a6962-125">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="a6962-125">Click **Add**.</span></span> <span data-ttu-id="a6962-126">Viene visualizzata la finestra di dialogo **Aggiungi processo Web** .</span><span class="sxs-lookup"><span data-stu-id="a6962-126">The **Add WebJob** dialog appears.</span></span>
   
    ![Pannello Aggiungi processo Web](./media/web-sites-create-web-jobs/addwjblade.png)
3. <span data-ttu-id="a6962-128">In **Name**indicare un nome per il processo Web.</span><span class="sxs-lookup"><span data-stu-id="a6962-128">Under **Name**, provide a name for the WebJob.</span></span> <span data-ttu-id="a6962-129">Il nome deve iniziare con una lettera o un numero e non può contenere caratteri speciali diversi da "-" e "_".</span><span class="sxs-lookup"><span data-stu-id="a6962-129">The name must start with a letter or a number and cannot contain any special characters other than "-" and "_".</span></span>
4. <span data-ttu-id="a6962-130">Nella casella **Modalità di esecuzione** selezionare **Esegui su richiesta**.</span><span class="sxs-lookup"><span data-stu-id="a6962-130">In the **How to Run** box, choose **Run on Demand**.</span></span>
5. <span data-ttu-id="a6962-131">Nella casella **Caricamento file** , fare clic sull'icona della cartella e accedere al file zip che contiene lo script.</span><span class="sxs-lookup"><span data-stu-id="a6962-131">In the **File Upload** box, click the folder icon and browse to the zip file that contains your script.</span></span> <span data-ttu-id="a6962-132">Il file ZIP deve contenere il file eseguibile (con estensione .exe, .cmd, .bat, .sh, .php, .py, .js) e gli eventuali file di supporto necessari per eseguire il programma o lo script.</span><span class="sxs-lookup"><span data-stu-id="a6962-132">The zip file should contain your executable (.exe .cmd .bat .sh .php .py .js) as well as any supporting files needed to run the program or script.</span></span>
6. <span data-ttu-id="a6962-133">Selezionare **Crea** per caricare lo script nell'app Web.</span><span class="sxs-lookup"><span data-stu-id="a6962-133">Check **Create** to upload the script to your web app.</span></span> 
   
    <span data-ttu-id="a6962-134">Il nome indicato per il processo Web viene visualizzato nell'elenco del pannello **Processi Web** .</span><span class="sxs-lookup"><span data-stu-id="a6962-134">The name you specified for the WebJob appears in the list on the **WebJobs** blade.</span></span>
7. <span data-ttu-id="a6962-135">Per eseguire il processo Web, fare clic con il pulsante destro del mouse sul nome visualizzato nell'elenco e scegliere **Esegui**.</span><span class="sxs-lookup"><span data-stu-id="a6962-135">To run the WebJob, right-click its name in the list and click **Run**.</span></span>
   
    ![Eseguire un processo Web](./media/web-sites-create-web-jobs/runondemand.png)

## <span data-ttu-id="a6962-137"><a name="CreateContinuous"></a>Creare un processo Web con esecuzione continua</span><span class="sxs-lookup"><span data-stu-id="a6962-137"><a name="CreateContinuous"></a>Create a continuously running WebJob</span></span>
1. <span data-ttu-id="a6962-138">Per creare un processo Web eseguito in modo continuo, seguire la stessa procedura usata per creare un processo Web eseguito una sola volta, ma nella casella **Modalità di esecuzione** selezionare **Continuo**.</span><span class="sxs-lookup"><span data-stu-id="a6962-138">To create a continuously executing WebJob, follow the same steps for creating a WebJob that runs once, but in the **How to Run** box, choose **Continuous**.</span></span>
2. <span data-ttu-id="a6962-139">Per avviare o interrompere un processo Web continuo, selezionarlo con il pulsante destro del mouse nell'elenco, quindi fare clic su **Avvia** o **Interrompi**.</span><span class="sxs-lookup"><span data-stu-id="a6962-139">To start or stop a continuous WebJob, right-click the WebJob in the list and click **Start** or **Stop**.</span></span>

> [!NOTE]
> <span data-ttu-id="a6962-140">Se l'app Web è in esecuzione su più di un'istanza, il processo Web con esecuzione continua verrà eseguito su tutte le istanze.</span><span class="sxs-lookup"><span data-stu-id="a6962-140">If your web app runs on more than one instance, a continuously running WebJob will run on all of your instances.</span></span> <span data-ttu-id="a6962-141">I processi Web su richiesta e pianificati vengono eseguiti su una singola istanza selezionata per il bilanciamento del carico da Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="a6962-141">On-demand and scheduled WebJobs run on a single instance selected for load balancing by Microsoft Azure.</span></span>
> 
> <span data-ttu-id="a6962-142">Per i processi Web continui da eseguire in modo affidabile su tutte le istanze, abilitare l'impostazione di configurazione Always On* per l'app Web, altrimenti è possibile che l'esecuzione dei processi venga interrotta quando il sito host SCM rimane inattivo per troppo tempo.</span><span class="sxs-lookup"><span data-stu-id="a6962-142">For Continuous WebJobs to run reliably and on all instances, enable the Always On* configuration setting for the web app otherwise they can stop running when the SCM host site has been idle for too long.</span></span>
> 
> 

## <span data-ttu-id="a6962-143"><a name="CreateScheduledCRON"></a>Creare un processo Web pianificato utilizzando un'espressione CRON</span><span class="sxs-lookup"><span data-stu-id="a6962-143"><a name="CreateScheduledCRON"></a>Create a scheduled WebJob using a CRON expression</span></span>
<span data-ttu-id="a6962-144">Questa tecnica, disponibile per le app Web in esecuzione in modalità Basic, Standard o Premium, richiede che nell'app sia abilitata l'impostazione **Always On** .</span><span class="sxs-lookup"><span data-stu-id="a6962-144">This technique is available to Web Apps running in Basic, Standard or Premium mode, and requires the **Always On** setting to be enabled on the app.</span></span>

<span data-ttu-id="a6962-145">Per trasformare un processo Web On Demand in un processo Web pianificato, includere semplicemente un file `settings.job` nella directory principale del file zip del processo Web.</span><span class="sxs-lookup"><span data-stu-id="a6962-145">To turn an On Demand WebJob into a scheduled WebJob, simply include a `settings.job` file at the root of your WebJob zip file.</span></span> <span data-ttu-id="a6962-146">Questo file JSON deve includere una `schedule` proprietà con un [espressione CRON](https://en.wikipedia.org/wiki/Cron), per esempio quanto riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="a6962-146">This JSON file should include a `schedule` property with a [CRON expression](https://en.wikipedia.org/wiki/Cron), per example below.</span></span>

<span data-ttu-id="a6962-147">L'espressione CRON è composta da 6 campi: `{second} {minute} {hour} {day} {month} {day of the week}`.</span><span class="sxs-lookup"><span data-stu-id="a6962-147">The CRON expression is composed of 6 fields: `{second} {minute} {hour} {day} {month} {day of the week}`.</span></span>

<span data-ttu-id="a6962-148">Ad esempio, per attivare il processo Web ogni 15 minuti, `settings.job` avrebbe:</span><span class="sxs-lookup"><span data-stu-id="a6962-148">For example, to trigger your WebJob every 15 minutes, your `settings.job` would have:</span></span>

```json
{
    "schedule": "0 */15 * * * *"
}
``` 

<span data-ttu-id="a6962-149">Altri esempi di programmazione CRON:</span><span class="sxs-lookup"><span data-stu-id="a6962-149">Other CRON schedule examples:</span></span>

* <span data-ttu-id="a6962-150">Ogni ora (ad esempio ogni volta che il numero di minuti è 0): `0 0 * * * *`</span><span class="sxs-lookup"><span data-stu-id="a6962-150">Every hour (i.e. whenever the count of minutes is 0): `0 0 * * * *`</span></span> 
* <span data-ttu-id="a6962-151">Ogni ora dalle 9 di mattina alle 5 del pomeriggio: `0 0 9-17 * * *`</span><span class="sxs-lookup"><span data-stu-id="a6962-151">Every hour from 9 AM to 5 PM: `0 0 9-17 * * *`</span></span> 
* <span data-ttu-id="a6962-152">Alle 9:30 di mattina ogni giorno: `0 30 9 * * *`</span><span class="sxs-lookup"><span data-stu-id="a6962-152">At 9:30 AM every day: `0 30 9 * * *`</span></span>
* <span data-ttu-id="a6962-153">Alle 9:30 di mattina ogni giorno della settimana: `0 30 9 * * 1-5`</span><span class="sxs-lookup"><span data-stu-id="a6962-153">At 9:30 AM every week day: `0 30 9 * * 1-5`</span></span>

<span data-ttu-id="a6962-154">**Nota**: quando si distribuisce un processo Web da Visual Studio, assicurarsi di contrassegnare le proprietà del file `settings.job` come "Copia se più recente".</span><span class="sxs-lookup"><span data-stu-id="a6962-154">**Note**: when deploying a WebJob from Visual Studio, make sure to mark your `settings.job` file properties as 'Copy if newer'.</span></span>

## <span data-ttu-id="a6962-155"><a name="CreateScheduled"></a>Creare un processo Web pianificato utilizzando l’Utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="a6962-155"><a name="CreateScheduled"></a>Create a scheduled WebJob using the Azure Scheduler</span></span>
<span data-ttu-id="a6962-156">La tecnica alternativa seguente usa l'utilità di pianificazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a6962-156">The following alternate technique makes use of the Azure Scheduler.</span></span> <span data-ttu-id="a6962-157">In questo caso, il processo Web non dispone di alcuna conoscenza diretta della pianificazione.</span><span class="sxs-lookup"><span data-stu-id="a6962-157">In this case, your WebJob does not have any direct knowledge of the schedule.</span></span> <span data-ttu-id="a6962-158">Al contrario, l'utilità di pianificazione di Azure verrà configurata per attivare il processo Web in una pianificazione.</span><span class="sxs-lookup"><span data-stu-id="a6962-158">Instead, the Azure Scheduler gets configured to trigger your WebJob on a schedule.</span></span> 

<span data-ttu-id="a6962-159">Il portale di Azure non permette ancora di creare un processo Web pianificato; tuttavia, attualmente è possibile eseguire questa operazione utilizzando il [portale classico](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="a6962-159">The Azure Portal doesn't yet have the ability to create a scheduled WebJob, but until that feature is added you can do it by using the [classic portal](http://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="a6962-160">Nel [portale classico](http://manage.windowsazure.com) , accedere alla pagina del processo Web e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="a6962-160">In the [classic portal](http://manage.windowsazure.com) go to the WebJob page and click **Add**.</span></span>
2. <span data-ttu-id="a6962-161">Nella casella **Modalità di esecuzione** scegliere **Esegui in base a una pianificazione**.</span><span class="sxs-lookup"><span data-stu-id="a6962-161">In the **How to Run** box, choose **Run on a schedule**.</span></span>
   
    ![Nuovo processo pianificato][NewScheduledJob]
3. <span data-ttu-id="a6962-163">Scegliere una voce in **Scheduler Region** per il processo e quindi fare clic sulla freccia nella parte inferiore destra della finestra di dialogo per passare alla schermata successiva.</span><span class="sxs-lookup"><span data-stu-id="a6962-163">Choose the **Scheduler Region** for your job, and then click the arrow on the bottom right of the dialog to proceed to the next screen.</span></span>
4. <span data-ttu-id="a6962-164">Nella finestra di dialogo **Crea processo** scegliere il tipo di **Ricorrenza** desiderata: **Processo con singola occorrenza** o **Processo ricorrente**.</span><span class="sxs-lookup"><span data-stu-id="a6962-164">In the **Create Job** dialog, choose the type of **Recurrence** you want: **One-time job** or **Recurring job**.</span></span>
   
    ![Pianificare la ricorrenza][SchdRecurrence]
5. <span data-ttu-id="a6962-166">Scegliere un'ora di **inizio**: **Ora** o **A un orario specifico**.</span><span class="sxs-lookup"><span data-stu-id="a6962-166">Also choose a **Starting** time: **Now** or **At a specific time**.</span></span>
   
    ![Pianificare l'ora di inizio][SchdStart]
6. <span data-ttu-id="a6962-168">Se si desidera che la pianificazione venga avviata a un'ora specifica, scegliere i valori dell'ora di inizio in **Starting On**.</span><span class="sxs-lookup"><span data-stu-id="a6962-168">If you want to start at a specific time, choose your starting time values under **Starting On**.</span></span>
   
    ![Pianificare l'avvio a un'ora specifica][SchdStartOn]
7. <span data-ttu-id="a6962-170">Se si sceglie un processo ricorrente, è disponibile l'opzione **Ricorre ogni** per specificare la frequenza di ricorrenza e l'opzione **Data di fine** per specificare la data e l'ora di fine.</span><span class="sxs-lookup"><span data-stu-id="a6962-170">If you chose a recurring job, you have the **Recur Every** option to specify the frequency of occurrence and the **Ending On** option to specify an ending time.</span></span>
   
    ![Pianificare la ricorrenza][SchdRecurEvery]
8. <span data-ttu-id="a6962-172">Se si sceglie **Settimane**, è possibile selezionare la casella **In una pianificazione specifica** e specificare i giorni della settimana in cui verrà eseguito il processo.</span><span class="sxs-lookup"><span data-stu-id="a6962-172">If you choose **Weeks**, you can select the **On a Particular Schedule** box and specify the days of the week that you want the job to run.</span></span>
   
    ![Pianificare i giorni della settimana][SchdWeeksOnParticular]
9. <span data-ttu-id="a6962-174">Se si sceglie **Mesi** e si seleziona la casella **In una pianificazione specifica**, è possibile impostare l'esecuzione del processo in determinati giorni del mese in **Giorni**.</span><span class="sxs-lookup"><span data-stu-id="a6962-174">If you choose **Months** and select the **On a Particular Schedule** box, you can set the job to run on particular numbered **Days** in the month.</span></span> 
   
    ![Pianificare date specifiche nel mese][SchdMonthsOnPartDays]
10. <span data-ttu-id="a6962-176">Se si sceglie **Week Days**, è possibile selezionare il giorno o i giorni della settimana del mese nei quali deve essere eseguito il processo.</span><span class="sxs-lookup"><span data-stu-id="a6962-176">If you choose **Week Days**, you can select which day or days of the week in the month you want the job to run on.</span></span>
    
     ![Pianificare giorni della settimana specifici in un mese][SchdMonthsOnPartWeekDays]
11. <span data-ttu-id="a6962-178">Infine, è possibile usare l'opzione **Occorrenze** per scegliere la settimana del mese (prima, seconda, terza e così via) in cui deve essere eseguito il processo nei giorni della settimana specificati.</span><span class="sxs-lookup"><span data-stu-id="a6962-178">Finally, you can also use the **Occurrences** option to choose which week in the month (first, second, third etc.) you want the job to run on the week days you specified.</span></span>
    
    ![Pianificare giorni della settimana specifici per determinate settimane in un mese][SchdMonthsOnPartWeekDaysOccurences]
12. <span data-ttu-id="a6962-180">Dopo avere creato uno o più processi, i relativi nomi verranno visualizzati nella scheda WebJobs insieme a stato, tipo di pianificazione e altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="a6962-180">After you have created one or more jobs, their names will appear on the WebJobs tab with their status, schedule type, and other information.</span></span> <span data-ttu-id="a6962-181">Vengono mantenute le informazioni cronologiche sugli ultimi 30 processi Web.</span><span class="sxs-lookup"><span data-stu-id="a6962-181">Historical information for the last 30  WebJobs is maintained.</span></span>
    
    ![Elenco processi][WebJobsListWithSeveralJobs]

### <span data-ttu-id="a6962-183"><a name="Scheduler"></a>Processi pianificati e Utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="a6962-183"><a name="Scheduler"></a>Scheduled jobs and Azure Scheduler</span></span>
<span data-ttu-id="a6962-184">I processi pianificati possono essere ulteriormente configurati nell'Utilità di pianificazione di Azure del [portale classico](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="a6962-184">Scheduled jobs can be further configured in the Azure Scheduler pages of the [classic portal](http://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="a6962-185">Nella pagina WebJobs fare clic sul collegamento **schedule** del processo per passare alla pagina del portale dell'Utilità di pianificazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a6962-185">On the WebJobs page, click the job's **schedule** link to navigate to the Azure Scheduler portal page.</span></span> 
   
   ![Collegamento all'Utilità di pianificazione di Azure][LinkToScheduler]
2. <span data-ttu-id="a6962-187">Nella pagina Scheduler fare clic sul processo.</span><span class="sxs-lookup"><span data-stu-id="a6962-187">On the Scheduler page, click the job.</span></span>
   
    ![Processo nella pagina del portale dell'Utilità di pianificazione][SchedulerPortal]
3. <span data-ttu-id="a6962-189">Verrà visualizzata la pagina **Job Action** in cui è possibile configurare ulteriormente il processo.</span><span class="sxs-lookup"><span data-stu-id="a6962-189">The **Job Action** page opens, where you can further configure the job.</span></span> 
   
    ![Pagina Job Action nell'Utilità di pianificazione][JobActionPageInScheduler]

## <span data-ttu-id="a6962-191"><a name="ViewJobHistory"></a>Visualizzare la cronologia processo</span><span class="sxs-lookup"><span data-stu-id="a6962-191"><a name="ViewJobHistory"></a>View the job history</span></span>
1. <span data-ttu-id="a6962-192">Per visualizzare la cronologia di esecuzione di un processo, inclusi i processi creati con WebJobs SDK, fare clic sul collegamento corrispondente nella colonna **Log** nel pannello dei processi Web.</span><span class="sxs-lookup"><span data-stu-id="a6962-192">To view the execution history of a job, including jobs created with the WebJobs SDK, click  its corresponding link under the **Logs** column of the WebJobs blade.</span></span> <span data-ttu-id="a6962-193">È possibile utilizzare l'icona degli Appunti per copiare l'URL della pagina del file di log negli Appunti, se lo si desidera.</span><span class="sxs-lookup"><span data-stu-id="a6962-193">(You can use the clipboard icon to copy the URL of the log file page to the clipboard if you wish.)</span></span>
   
    ![Collegamento Log](./media/web-sites-create-web-jobs/wjbladelogslink.png)
2. <span data-ttu-id="a6962-195">Se si fa clic sul collegamento, viene visualizzata la pagina dei dettagli per il processo Web.</span><span class="sxs-lookup"><span data-stu-id="a6962-195">Clicking the link opens the details page for the WebJob.</span></span> <span data-ttu-id="a6962-196">In questa pagina è indicato il nome del comando eseguito, le ore delle ultime esecuzioni e il relativo esito positivo o negativo.</span><span class="sxs-lookup"><span data-stu-id="a6962-196">This page shows you the name of the command run, the last times it ran, and its success or failure.</span></span> <span data-ttu-id="a6962-197">In **Recent job runs**fare clic su un'ora per visualizzare ulteriori dettagli.</span><span class="sxs-lookup"><span data-stu-id="a6962-197">Under **Recent job runs**, click a time to see further details.</span></span>
   
    ![WebJobDetails][WebJobDetails]
3. <span data-ttu-id="a6962-199">Verrà visualizzata la pagina **WebJob Run Details** .</span><span class="sxs-lookup"><span data-stu-id="a6962-199">The **WebJob Run Details** page appears.</span></span> <span data-ttu-id="a6962-200">Fare clic su **Toggle Output** per visualizzare il testo dei contenuti del log.</span><span class="sxs-lookup"><span data-stu-id="a6962-200">Click **Toggle Output** to see the text of the log contents.</span></span> <span data-ttu-id="a6962-201">Il log di output è in formato testo.</span><span class="sxs-lookup"><span data-stu-id="a6962-201">The output log is in text format.</span></span> 
   
    ![Dettagli dell'esecuzione del processo Web][WebJobRunDetails]
4. <span data-ttu-id="a6962-203">Per visualizzare il testo dell'output in un'altra finestra del browser, fare clic sul collegamento **download** .</span><span class="sxs-lookup"><span data-stu-id="a6962-203">To see the output text in a separate browser window, click the **download** link.</span></span> <span data-ttu-id="a6962-204">Per scaricare il testo stesso, fare clic con il pulsante destro del mouse sul collegamento e utilizzare le opzioni del browser in uso per salvare il contenuto del file.</span><span class="sxs-lookup"><span data-stu-id="a6962-204">To download the text itself, right-click the link and use your browser options to save the file contents.</span></span>
   
    ![Download dell'output del log][DownloadLogOutput]
5. <span data-ttu-id="a6962-206">Il collegamento **Processi Web** nella parte superiore della pagina offre un modo pratico per ottenere un elenco di processi Web nel dashboard della cronologia.</span><span class="sxs-lookup"><span data-stu-id="a6962-206">The **WebJobs** link at the top of the page provides a convenient way to get to a list of WebJobs on the history dashboard.</span></span>
   
    ![Collegamento all'elenco dei processi Web][WebJobsLinkToDashboardList]
   
    ![Elenco dei processi nel dashboard della cronologia][WebJobsListInJobsDashboard]
   
    <span data-ttu-id="a6962-209">Quando si fa clic su questi collegamenti, si viene reindirizzati alla pagina WebJob Details per il processo selezionato.</span><span class="sxs-lookup"><span data-stu-id="a6962-209">Clicking one of these links takes you to the WebJob Details page for the job you selected.</span></span>

## <span data-ttu-id="a6962-210"><a name="WHPNotes"></a>Note</span><span class="sxs-lookup"><span data-stu-id="a6962-210"><a name="WHPNotes"></a>Notes</span></span>
* <span data-ttu-id="a6962-211">Le app Web in modalità gratuita possono scadere dopo 20 minuti, se non vengono inviate richieste al sito scm (distribuzione) e se il portale dell'app Web non è aperto in Azure.</span><span class="sxs-lookup"><span data-stu-id="a6962-211">Web apps in Free mode can time out after 20 minutes if there are no requests to the scm (deployment) site and the web app's portal is not open in Azure.</span></span> <span data-ttu-id="a6962-212">Le richieste al sito effettivo non comportano la reimpostazione del timeout.</span><span class="sxs-lookup"><span data-stu-id="a6962-212">Requests to the actual site will not reset this.</span></span>
* <span data-ttu-id="a6962-213">Il codice per un processo continuo deve essere scritto per l'esecuzione in un ciclo infinito.</span><span class="sxs-lookup"><span data-stu-id="a6962-213">Code for a continuous job needs to be written to run in an endless loop.</span></span>
* <span data-ttu-id="a6962-214">I processi continui vengono eseguiti in modo continuo solo quando l'app è attiva.</span><span class="sxs-lookup"><span data-stu-id="a6962-214">Continuous jobs run continuously only when the web app is up.</span></span>
* <span data-ttu-id="a6962-215">Le modalità di base e standard offrono la funzionalità Sempre attivata che, se abilitata, impedisce alle app Web di diventare inattive.</span><span class="sxs-lookup"><span data-stu-id="a6962-215">Basic and Standard modes offer the Always On feature which, when enabled, prevents web apps from becoming idle.</span></span>
* <span data-ttu-id="a6962-216">È possibile solo eseguire il debug di processi Web con esecuzione continua.</span><span class="sxs-lookup"><span data-stu-id="a6962-216">You can only debug continuously running WebJobs.</span></span> <span data-ttu-id="a6962-217">Il debug di processi Web pianificati o su richiesta non è supportato.</span><span class="sxs-lookup"><span data-stu-id="a6962-217">Debugging scheduled or on-demand WebJobs is not supported.</span></span>

## <span data-ttu-id="a6962-218"><a name="NextSteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a6962-218"><a name="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="a6962-219">Per altre informazioni, vedere l'articolo relativo alle [risorse consigliate per i processi Web di Azure][WebJobsRecommendedResources].</span><span class="sxs-lookup"><span data-stu-id="a6962-219">For more information, see [Azure WebJobs Recommended Resources][WebJobsRecommendedResources].</span></span>

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

