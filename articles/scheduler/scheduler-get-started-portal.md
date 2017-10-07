---
title: "aaaGet introduzione dell'utilità di pianificazione di Azure nel portale di Azure | Documenti Microsoft"
description: "Introduzione all'Utilità di pianificazione di Azure nel portale di Azure"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: e69542ec-d10f-4f17-9b7a-2ee441ee7d68
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/10/2016
ms.author: deli
ms.openlocfilehash: 58255c0ad19da65932f8b1d36cb8fef1ff6e651b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-scheduler-in-azure-portal"></a><span data-ttu-id="75452-103">Introduzione all'Utilità di pianificazione di Azure nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="75452-103">Get started with Azure Scheduler in Azure portal</span></span>
<span data-ttu-id="75452-104">È facile toocreate pianificati processi nell'utilità di pianificazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="75452-104">It's easy toocreate scheduled jobs in Azure Scheduler.</span></span> <span data-ttu-id="75452-105">In questa esercitazione si apprenderà come toocreate un processo.</span><span class="sxs-lookup"><span data-stu-id="75452-105">In this tutorial, you'll learn how toocreate a job.</span></span> <span data-ttu-id="75452-106">Si apprenderanno anche le funzionalità di monitoraggio e gestione dell'Utilità di pianificazione.</span><span class="sxs-lookup"><span data-stu-id="75452-106">You'll also learn Scheduler's monitoring and management capabilities.</span></span>

## <a name="create-a-job"></a><span data-ttu-id="75452-107">Creare un processo</span><span class="sxs-lookup"><span data-stu-id="75452-107">Create a job</span></span>
1. <span data-ttu-id="75452-108">Accedi troppo[portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="75452-108">Sign in too[Azure portal](https://portal.azure.com/).</span></span>  
2. <span data-ttu-id="75452-109">Fare clic su **+ nuovo** > tipo *dell'utilità di pianificazione* nella casella di ricerca hello > selezionare **dell'utilità di pianificazione** nei risultati > fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="75452-109">Click **+New** > type *Scheduler* in hello search box >  select **Scheduler** in results > click **Create**.</span></span>
   
    ![][marketplace-create]
3. <span data-ttu-id="75452-110">Creiamo un processo che accede semplicemente a http://www.microsoft.com/ con una richiesta GET.</span><span class="sxs-lookup"><span data-stu-id="75452-110">Let’s create a job that simply hits http://www.microsoft.com/ with a GET request.</span></span> <span data-ttu-id="75452-111">In hello **dell'utilità di pianificazione** immettere hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="75452-111">In hello **Scheduler Job** screen, enter hello following information:</span></span>
   
   1. <span data-ttu-id="75452-112">**Nome:** `getmicrosoft`</span><span class="sxs-lookup"><span data-stu-id="75452-112">**Name:** `getmicrosoft`</span></span>  
   2. <span data-ttu-id="75452-113">**Sottoscrizione:** sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="75452-113">**Subscription:** Your Azure subscription</span></span>   
   3. <span data-ttu-id="75452-114">**Raccolta processi:** selezionare una raccolta di processi esistente oppure fare clic su **Crea nuovo** e immettere un nome.</span><span class="sxs-lookup"><span data-stu-id="75452-114">**Job Collection:** Select an existing job collection, or click **Create New** > enter a name.</span></span>
4. <span data-ttu-id="75452-115">Successivamente, nel **Impostazioni azione**, definire hello seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="75452-115">Next, in **Action Settings**, define hello following values:</span></span>
   
   1. <span data-ttu-id="75452-116">**Tipo di azione:** ` HTTP`</span><span class="sxs-lookup"><span data-stu-id="75452-116">**Action Type:** ` HTTP`</span></span>  
   2. <span data-ttu-id="75452-117">**Metodo:** `GET`</span><span class="sxs-lookup"><span data-stu-id="75452-117">**Method:** `GET`</span></span>  
   3. <span data-ttu-id="75452-118">**URL:** ` http://www.microsoft.com`</span><span class="sxs-lookup"><span data-stu-id="75452-118">**URL:** ` http://www.microsoft.com`</span></span>  
      
      ![][action-settings]
5. <span data-ttu-id="75452-119">Infine, definire una pianificazione.</span><span class="sxs-lookup"><span data-stu-id="75452-119">Finally, let's define a schedule.</span></span> <span data-ttu-id="75452-120">il processo di Hello può essere definito come processo occasionale, ma si seleziona una pianificazione ricorrenza:</span><span class="sxs-lookup"><span data-stu-id="75452-120">hello job could be defined as a one-time job, but let’s pick a recurrence schedule:</span></span>
   
   1. <span data-ttu-id="75452-121">**Ricorrenza:**`Recurring`</span><span class="sxs-lookup"><span data-stu-id="75452-121">**Recurrence**: `Recurring`</span></span>
   2. <span data-ttu-id="75452-122">**Inizia**: data odierna</span><span class="sxs-lookup"><span data-stu-id="75452-122">**Start**: Today's date</span></span>
   3. <span data-ttu-id="75452-123">**Ricorre ogni:** `12 Hours`</span><span class="sxs-lookup"><span data-stu-id="75452-123">**Recur every**: `12 Hours`</span></span>
   4. <span data-ttu-id="75452-124">**Termina entro**: due giorni dalla data odierna</span><span class="sxs-lookup"><span data-stu-id="75452-124">**End by**: Two days from today's date</span></span>  
      
      ![][recurrence-schedule]
6. <span data-ttu-id="75452-125">Fare clic su **Crea**</span><span class="sxs-lookup"><span data-stu-id="75452-125">Click **Create**</span></span>

## <a name="manage-and-monitor-jobs"></a><span data-ttu-id="75452-126">Gestire e monitorare i processi</span><span class="sxs-lookup"><span data-stu-id="75452-126">Manage and monitor jobs</span></span>
<span data-ttu-id="75452-127">Dopo aver creato un processo, viene visualizzato nel dashboard di Azure principale hello.</span><span class="sxs-lookup"><span data-stu-id="75452-127">Once a job is created, it appears in hello main Azure dashboard.</span></span> <span data-ttu-id="75452-128">Fare clic su processo hello e un nuovo verrà visualizzata la finestra con hello seguenti schede:</span><span class="sxs-lookup"><span data-stu-id="75452-128">Click hello job and a new window opens with hello following tabs:</span></span>

1. <span data-ttu-id="75452-129">Proprietà</span><span class="sxs-lookup"><span data-stu-id="75452-129">Properties</span></span>  
2. <span data-ttu-id="75452-130">Impostazioni azione</span><span class="sxs-lookup"><span data-stu-id="75452-130">Action Settings</span></span>  
3. <span data-ttu-id="75452-131">Pianificazione</span><span class="sxs-lookup"><span data-stu-id="75452-131">Schedule</span></span>  
4. <span data-ttu-id="75452-132">Cronologia</span><span class="sxs-lookup"><span data-stu-id="75452-132">History</span></span>
5. <span data-ttu-id="75452-133">Utenti</span><span class="sxs-lookup"><span data-stu-id="75452-133">Users</span></span>
   
   ![][job-overview]

### <a name="properties"></a><span data-ttu-id="75452-134">Proprietà</span><span class="sxs-lookup"><span data-stu-id="75452-134">Properties</span></span>
<span data-ttu-id="75452-135">Queste proprietà di sola lettura descrivono i metadati di gestione di hello per il processo dell'utilità di pianificazione hello.</span><span class="sxs-lookup"><span data-stu-id="75452-135">These read-only properties describe hello management metadata for hello Scheduler job.</span></span>

   ![][job-properties]

### <a name="action-settings"></a><span data-ttu-id="75452-136">Impostazioni azione</span><span class="sxs-lookup"><span data-stu-id="75452-136">Action settings</span></span>
<span data-ttu-id="75452-137">Facendo clic su un processo in hello **processi** schermata consente tooconfigure che del processo.</span><span class="sxs-lookup"><span data-stu-id="75452-137">Clicking on a job in hello **Jobs** screen allows you tooconfigure that job.</span></span> <span data-ttu-id="75452-138">Ciò consente di configurare le impostazioni avanzate, se non sono stati configurati in hello della procedura guidata di creazione rapida.</span><span class="sxs-lookup"><span data-stu-id="75452-138">This lets you configure advanced settings, if you didn't configure them in hello quick-create wizard.</span></span>

<span data-ttu-id="75452-139">Per tutti i tipi di azione, è possibile modificare i criteri di ripetizione hello e azione di errore hello.</span><span class="sxs-lookup"><span data-stu-id="75452-139">For all action types, you may change hello retry policy and hello error action.</span></span>

<span data-ttu-id="75452-140">Per i tipi di azione del processo HTTP e HTTPS, è possibile modificare tooany metodo hello verbo HTTP consentito.</span><span class="sxs-lookup"><span data-stu-id="75452-140">For HTTP and HTTPS job action types, you may change hello method tooany allowed HTTP verb.</span></span> <span data-ttu-id="75452-141">È anche possibile aggiungere, eliminare o modificare intestazioni hello e le informazioni di autenticazione di base.</span><span class="sxs-lookup"><span data-stu-id="75452-141">You may also add, delete, or change hello headers and basic authentication information.</span></span>

<span data-ttu-id="75452-142">Per i tipi di azione della coda di archiviazione, è possibile modificare l'account di archiviazione hello, nome, token di firma di accesso condiviso della coda e corpo.</span><span class="sxs-lookup"><span data-stu-id="75452-142">For storage queue action types, you may change hello storage account, queue name, SAS token, and body.</span></span>

<span data-ttu-id="75452-143">Per i tipi di azione bus di servizio, è possibile modificare lo spazio dei nomi hello, percorso coda o argomento, le impostazioni di autenticazione, il tipo di trasporto, le proprietà del messaggio e corpo del messaggio.</span><span class="sxs-lookup"><span data-stu-id="75452-143">For service bus action types, you may change hello namespace, topic/queue path, authentication settings, transport type, message properties, and message body.</span></span>

   ![][job-action-settings]

### <a name="schedule"></a><span data-ttu-id="75452-144">Pianificazione</span><span class="sxs-lookup"><span data-stu-id="75452-144">Schedule</span></span>
<span data-ttu-id="75452-145">Ciò consente di riconfigurare pianificazione hello, se si desidera pianificazione hello toochange che è stato creato in hello della procedura guidata di creazione rapida.</span><span class="sxs-lookup"><span data-stu-id="75452-145">This lets you reconfigure hello schedule, if you'd like toochange hello schedule you created in hello quick-create wizard.</span></span>

<span data-ttu-id="75452-146">Si tratta di un'opportunità toobuild [pianificazioni complesse e ricorrenza avanzate nel processo](scheduler-advanced-complexity.md)</span><span class="sxs-lookup"><span data-stu-id="75452-146">This is an opportunity toobuild [complex schedules and advanced recurrence in your job](scheduler-advanced-complexity.md)</span></span>

<span data-ttu-id="75452-147">È possibile modificare la data di inizio hello e tempo, pianificazione ricorrenza e hello data di fine e l'ora (se il processo di hello è ricorrente.)</span><span class="sxs-lookup"><span data-stu-id="75452-147">You may change hello start date and time, recurrence schedule, and hello end date and time (if hello job is recurring.)</span></span>

   ![][job-schedule]

### <a name="history"></a><span data-ttu-id="75452-148">Cronologia</span><span class="sxs-lookup"><span data-stu-id="75452-148">History</span></span>
<span data-ttu-id="75452-149">Hello **cronologia** scheda vengono visualizzate le metriche selezionate per ogni esecuzione del processo nel sistema hello per processo selezionato hello.</span><span class="sxs-lookup"><span data-stu-id="75452-149">hello **History** tab displays selected metrics for every job execution in hello system for hello selected job.</span></span> <span data-ttu-id="75452-150">Queste metriche forniscono valori in tempo reale relativamente hello integrità dell'utilità di pianificazione:</span><span class="sxs-lookup"><span data-stu-id="75452-150">These metrics provide real-time values regarding hello health of your Scheduler:</span></span>

1. <span data-ttu-id="75452-151">Stato</span><span class="sxs-lookup"><span data-stu-id="75452-151">Status</span></span>  
2. <span data-ttu-id="75452-152">Dettagli</span><span class="sxs-lookup"><span data-stu-id="75452-152">Details</span></span>  
3. <span data-ttu-id="75452-153">Tentativi</span><span class="sxs-lookup"><span data-stu-id="75452-153">Retry attempts</span></span>
4. <span data-ttu-id="75452-154">Occorrenza: 1, 2, 3 e così via</span><span class="sxs-lookup"><span data-stu-id="75452-154">Occurrence: 1st, 2nd, 3rd, etc.</span></span>
5. <span data-ttu-id="75452-155">Ora di inizio dell'esecuzione</span><span class="sxs-lookup"><span data-stu-id="75452-155">Start time of execution</span></span>  
6. <span data-ttu-id="75452-156">Ora di fine dell'esecuzione</span><span class="sxs-lookup"><span data-stu-id="75452-156">End time of execution</span></span>
   
   ![][job-history]

<span data-ttu-id="75452-157">È possibile fare clic su una fase tooview relativo **i dettagli della cronologia**, inclusi l'intera risposta di hello per ogni esecuzione.</span><span class="sxs-lookup"><span data-stu-id="75452-157">You can click on a run tooview its **History Details**, including hello whole response for every execution.</span></span> <span data-ttu-id="75452-158">Questa finestra di dialogo consente anche negli Appunti di toohello toocopy hello risposta.</span><span class="sxs-lookup"><span data-stu-id="75452-158">This dialog box also allows you toocopy hello response toohello clipboard.</span></span>

   ![][job-history-details]

### <a name="users"></a><span data-ttu-id="75452-159">Utenti</span><span class="sxs-lookup"><span data-stu-id="75452-159">Users</span></span>
<span data-ttu-id="75452-160">Il controllo degli accessi in base al ruolo di Azure consente una gestione degli accessi specifica per l'Utilità di pianificazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="75452-160">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure Scheduler.</span></span> <span data-ttu-id="75452-161">toolearn come toouse hello scheda utenti, fare riferimento troppo[gestire il controllo di accesso](../active-directory/role-based-access-control-configure.md)</span><span class="sxs-lookup"><span data-stu-id="75452-161">toolearn how toouse hello Users tab, refer too[Azure Role-Based Access Control](../active-directory/role-based-access-control-configure.md)</span></span>

## <a name="see-also"></a><span data-ttu-id="75452-162">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="75452-162">See also</span></span>
 [<span data-ttu-id="75452-163">Che cos'è l'Utilità di pianificazione?</span><span class="sxs-lookup"><span data-stu-id="75452-163">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="75452-164">Concetti, terminologia e gerarchia di entità dell'Utilità di pianificazione</span><span class="sxs-lookup"><span data-stu-id="75452-164">Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="75452-165">Piani e fatturazione nell'utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="75452-165">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="75452-166">Come toobuild complesso pianifica e ricorrenza avanzata con utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="75452-166">How toobuild complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="75452-167">Riferimento API REST dell'utilità di pianificazione</span><span class="sxs-lookup"><span data-stu-id="75452-167">Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="75452-168">Informazioni di riferimento sui cmdlet PowerShell dell'Utilità di pianificazione</span><span class="sxs-lookup"><span data-stu-id="75452-168">Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="75452-169">Livelli elevati di disponibilità e affidabilità dell'Utilità di pianificazione</span><span class="sxs-lookup"><span data-stu-id="75452-169">Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="75452-170">Limiti, valori predefiniti e codici di errore dell'Utilità di pianificazione</span><span class="sxs-lookup"><span data-stu-id="75452-170">Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="75452-171">Autenticazione in uscita dell'Utilità di pianificazione</span><span class="sxs-lookup"><span data-stu-id="75452-171">Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

[marketplace-create]: ./media/scheduler-get-started-portal/scheduler-v2-portal-marketplace-create.png
[action-settings]: ./media/scheduler-get-started-portal/scheduler-v2-portal-action-settings.png
[recurrence-schedule]: ./media/scheduler-get-started-portal/scheduler-v2-portal-recurrence-schedule.png
[job-properties]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-properties.png
[job-overview]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-overview-1.png
[job-action-settings]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-action-settings.png
[job-schedule]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-schedule.png
[job-history]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-history.png
[job-history-details]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-history-details.png


[1]: ./media/scheduler-get-started-portal/scheduler-get-started-portal001.png
[2]: ./media/scheduler-get-started-portal/scheduler-get-started-portal002.png
[3]: ./media/scheduler-get-started-portal/scheduler-get-started-portal003.png
[4]: ./media/scheduler-get-started-portal/scheduler-get-started-portal004.png
[5]: ./media/scheduler-get-started-portal/scheduler-get-started-portal005.png
[6]: ./media/scheduler-get-started-portal/scheduler-get-started-portal006.png
[7]: ./media/scheduler-get-started-portal/scheduler-get-started-portal007.png
[8]: ./media/scheduler-get-started-portal/scheduler-get-started-portal008.png
[9]: ./media/scheduler-get-started-portal/scheduler-get-started-portal009.png
[10]: ./media/scheduler-get-started-portal/scheduler-get-started-portal010.png
[11]: ./media/scheduler-get-started-portal/scheduler-get-started-portal011.png
[12]: ./media/scheduler-get-started-portal/scheduler-get-started-portal012.png
[13]: ./media/scheduler-get-started-portal/scheduler-get-started-portal013.png
[14]: ./media/scheduler-get-started-portal/scheduler-get-started-portal014.png
[15]: ./media/scheduler-get-started-portal/scheduler-get-started-portal015.png
