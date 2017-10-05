---
title: Come usare l'API di Engagement in Windows Phone Silverlight
description: Come usare l'API di Engagement in Windows Phone Silverlight
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: ae2ba2e8-f75b-4dee-a164-a7dd65d35a23
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: ec8b6c13ea052c8063dfde4321cdd286ab6cb817
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-engagement-api-on-windows-phone-silverlight"></a><span data-ttu-id="8e225-103">Come usare l'API di Engagement in Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="8e225-103">How to Use the Engagement API on Windows Phone Silverlight</span></span>
<span data-ttu-id="8e225-104">Questo documento è complementare all'articolo [Come integrare Mobile Engagement in un'app per Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="8e225-104">This document is an add-on to the document [How to integrate Mobile Engagement in your Windows Phone Silverlight app](mobile-engagement-windows-phone-integrate-engagement.md).</span></span> <span data-ttu-id="8e225-105">Fornisce informazioni approfondite su come usare l'API di Engagement per segnalare le statistiche dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8e225-105">It provides in depth details about how to use the Engagement API to report your application statistics.</span></span>

<span data-ttu-id="8e225-106">Se si vuole impostare Engagement in modo che segnali solo le sessioni, le attività, gli arresti anomali e i dati tecnici dell'applicazione, la soluzione più semplice consiste nel fare in modo che tutte le sottoclassi `PhoneApplicationPage` ereditino dalla classe `EngagementPage`.</span><span class="sxs-lookup"><span data-stu-id="8e225-106">If you only want Engagement to report your application's sessions, activities, crashes and technical information, then the simplest way is to make all your `PhoneApplicationPage` sub-classes inherit from the `EngagementPage` class.</span></span>

<span data-ttu-id="8e225-107">Se invece si hanno esigenze più complesse, ad esempio se è necessario segnalare eventi, errori e processi specifici dell'applicazione o presentare le attività dell'applicazione in modo diverso rispetto a quello implementato nelle classi `EngagementPage`, è necessario usare l'API di Engagement.</span><span class="sxs-lookup"><span data-stu-id="8e225-107">If you want to do more, for example if you need to report application specific events, errors and jobs, or if you have to report your application's activities in a different way than the one implemented in the `EngagementPage` classes, then you need to use the Engagement API.</span></span>

<span data-ttu-id="8e225-108">L'API di Engagement viene fornita dalla classe `EngagementAgent` .</span><span class="sxs-lookup"><span data-stu-id="8e225-108">The Engagement API is provided by the `EngagementAgent` class.</span></span> <span data-ttu-id="8e225-109">È possibile accedere a questi metodi tramite `EngagementAgent.Instance`.</span><span class="sxs-lookup"><span data-stu-id="8e225-109">You can access to those methods through `EngagementAgent.Instance`.</span></span>

<span data-ttu-id="8e225-110">Anche se il modulo dell'agente non è stato inizializzato, ogni chiamata all'API viene posticipata e verrà eseguita nuovamente quando l'agente è disponibile.</span><span class="sxs-lookup"><span data-stu-id="8e225-110">Even if the agent module has not been initialized, each call to the API is deferred, and will be executed again when the agent is available.</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="8e225-111">Concetti relativi a Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="8e225-111">Engagement concepts</span></span>
<span data-ttu-id="8e225-112">Le parti seguenti approfondiscono le informazioni contenute nell'articolo "Concetti relativi ad Azure Mobile Engagement" per la piattaforma Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="8e225-112">The following parts refine the Mobile Engagement Concepts for the Windows Phone platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="8e225-113">`Session` e `Activity`</span><span class="sxs-lookup"><span data-stu-id="8e225-113">`Session` and `Activity`</span></span>
<span data-ttu-id="8e225-114">Un'*attività* è in genere associata a una pagina dell'applicazione, ovvero l'*attività* inizia quando la pagina viene visualizzata e si arresta quando la pagina viene chiusa. Questo avviene quando Engagement SDK è integrato mediante la classe `EngagementPage`.</span><span class="sxs-lookup"><span data-stu-id="8e225-114">An *activity* is usually associated with one page of the application, that is to say the *activity* starts when the page is displayed and stops when the page is closed: this is the case when the Engagement SDK is integrated by using the `EngagementPage` class.</span></span>

<span data-ttu-id="8e225-115">Le *attività* possono tuttavia essere controllate anche manualmente usando l'API di Engagement.</span><span class="sxs-lookup"><span data-stu-id="8e225-115">But *activities* can also be controlled manually by using the Engagement API.</span></span> <span data-ttu-id="8e225-116">Ciò consente di dividere una determinata pagina in più sottoparti per ottenere maggiori dettagli sull'utilizzo della pagina (ad esempio per conoscere la frequenza e la durata dell'uso delle finestre di dialogo all'interno della pagina).</span><span class="sxs-lookup"><span data-stu-id="8e225-116">This allows to split a given page in several sub parts to get more details about the usage of this page (for example to known how often and how long dialogs are used inside this page).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="8e225-117">Segnalazione di attività</span><span class="sxs-lookup"><span data-stu-id="8e225-117">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="8e225-118">L'utente inizia una nuova attività</span><span class="sxs-lookup"><span data-stu-id="8e225-118">User starts a new Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="8e225-119">riferimento</span><span class="sxs-lookup"><span data-stu-id="8e225-119">Reference</span></span>
            void StartActivity(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="8e225-120">È necessario chiamare `StartActivity()` ogni volta che l'attività dell'utente cambia.</span><span class="sxs-lookup"><span data-stu-id="8e225-120">You need to call `StartActivity()` each time the user activity changes.</span></span> <span data-ttu-id="8e225-121">La prima chiamata a questa funzione avvia una nuova sessione utente.</span><span class="sxs-lookup"><span data-stu-id="8e225-121">The first call to this function starts a new user session.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8e225-122">L'SDK chiama automaticamente il metodo EndActivity quando viene chiusa l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8e225-122">The SDK automatically call the EndActivity method when the application is closed.</span></span> <span data-ttu-id="8e225-123">Di conseguenza, è ALTAMENTE consigliato chiamare il metodo StartActivity ogni volta che l'attività dell'utente cambia e non chiamare MAI il metodo EndActivity poiché la chiamata di questo metodo forza la chiusura della sessione corrente.</span><span class="sxs-lookup"><span data-stu-id="8e225-123">Thus, it is HIGHLY recommended to call the StartActivity method whenever the activity of the user change, and to NEVER call the EndActivity method, since calling this method forces the current session to be ended.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="8e225-124">Esempio</span><span class="sxs-lookup"><span data-stu-id="8e225-124">Example</span></span>
            EngagementAgent.Instance.StartActivity("main", new Dictionary<object, object>() {{"example", "data"}});

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="8e225-125">L'utente termina l'attività corrente</span><span class="sxs-lookup"><span data-stu-id="8e225-125">User ends his current Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="8e225-126">riferimento</span><span class="sxs-lookup"><span data-stu-id="8e225-126">Reference</span></span>
            void EndActivity()

<span data-ttu-id="8e225-127">È necessario chiamare `EndActivity()` almeno una volta quando l'utente termina la sua ultima attività.</span><span class="sxs-lookup"><span data-stu-id="8e225-127">You need to call `EndActivity()` at least once when the user finishes his last activity.</span></span> <span data-ttu-id="8e225-128">In questo modo, si indica all'SDK di Engagement che l'utente è attualmente inattivo e che la sessione utente deve essere chiusa allo scadere del timeout. Se si chiama `StartActivity()` prima dello scadere del timeout, la sessione rimane semplicemente attiva.</span><span class="sxs-lookup"><span data-stu-id="8e225-128">This informs the Engagement SDK that the user is currently idle, and that the user session need to be closed once the session timeout will expire (if you call `StartActivity()` before the session timeout expires, the session is simply continued).</span></span>

#### <a name="example"></a><span data-ttu-id="8e225-129">Esempio</span><span class="sxs-lookup"><span data-stu-id="8e225-129">Example</span></span>
            EngagementAgent.Instance.EndActivity();

## <a name="reporting-jobs"></a><span data-ttu-id="8e225-130">Segnalazione di processi</span><span class="sxs-lookup"><span data-stu-id="8e225-130">Reporting Jobs</span></span>
### <a name="start-a-job"></a><span data-ttu-id="8e225-131">Avviare un processo</span><span class="sxs-lookup"><span data-stu-id="8e225-131">Start a job</span></span>
#### <a name="reference"></a><span data-ttu-id="8e225-132">riferimento</span><span class="sxs-lookup"><span data-stu-id="8e225-132">Reference</span></span>
            void StartJob(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="8e225-133">È possibile utilizzare il processo per tenere traccia delle attività in un determinato periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="8e225-133">You can use the job to track certains tasks over a period of time.</span></span>

#### <a name="example"></a><span data-ttu-id="8e225-134">Esempio</span><span class="sxs-lookup"><span data-stu-id="8e225-134">Example</span></span>
            // An upload begins...

            // Set the extras
            var extras = new Dictionary<object, object>();
            extras.Add("title", "avatar");
            extras.Add("type", "image");

            EngagementAgent.Instance.StartJob("uploadData", extras);

### <a name="end-a-job"></a><span data-ttu-id="8e225-135">Terminare un processo</span><span class="sxs-lookup"><span data-stu-id="8e225-135">End a job</span></span>
#### <a name="reference"></a><span data-ttu-id="8e225-136">riferimento</span><span class="sxs-lookup"><span data-stu-id="8e225-136">Reference</span></span>
            void EndJob(string name)

<span data-ttu-id="8e225-137">Appena terminata un'attività di cui un processo tiene traccia, è necessario chiamare il metodo EndJob per questo processo, fornendo il nome del processo.</span><span class="sxs-lookup"><span data-stu-id="8e225-137">As soon as a task tracked by a job has been terminated, you should call the EndJob method for this job, by supplying the job name.</span></span>

#### <a name="example"></a><span data-ttu-id="8e225-138">Esempio</span><span class="sxs-lookup"><span data-stu-id="8e225-138">Example</span></span>
            // In the previous section, we started an upload tracking with a job
            // Then, the upload ends

            EngagementAgent.Instance.EndJob("uploadData");

## <a name="reporting-events"></a><span data-ttu-id="8e225-139">Segnalazione di eventi</span><span class="sxs-lookup"><span data-stu-id="8e225-139">Reporting Events</span></span>
<span data-ttu-id="8e225-140">Esistono tre tipi di eventi:</span><span class="sxs-lookup"><span data-stu-id="8e225-140">There is three types of events :</span></span>

* <span data-ttu-id="8e225-141">Eventi autonomi</span><span class="sxs-lookup"><span data-stu-id="8e225-141">Standalone events</span></span>
* <span data-ttu-id="8e225-142">Eventi di sessione</span><span class="sxs-lookup"><span data-stu-id="8e225-142">Session events</span></span>
* <span data-ttu-id="8e225-143">Eventi di processo</span><span class="sxs-lookup"><span data-stu-id="8e225-143">Job events</span></span>

### <a name="standalone-events"></a><span data-ttu-id="8e225-144">Eventi autonomi</span><span class="sxs-lookup"><span data-stu-id="8e225-144">Standalone Events</span></span>
#### <a name="reference"></a><span data-ttu-id="8e225-145">riferimento</span><span class="sxs-lookup"><span data-stu-id="8e225-145">Reference</span></span>
            void SendEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="8e225-146">Gli eventi autonomi possono verificarsi all'esterno del contesto di una sessione.</span><span class="sxs-lookup"><span data-stu-id="8e225-146">Standalone events can occur outside of the context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="8e225-147">Esempio</span><span class="sxs-lookup"><span data-stu-id="8e225-147">Example</span></span>
            EngagementAgent.Instance.SendEvent("event", extra);

### <a name="session-events"></a><span data-ttu-id="8e225-148">Eventi di sessione</span><span class="sxs-lookup"><span data-stu-id="8e225-148">Session events</span></span>
#### <a name="reference"></a><span data-ttu-id="8e225-149">riferimento</span><span class="sxs-lookup"><span data-stu-id="8e225-149">Reference</span></span>
            void SendSessionEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="8e225-150">Gli eventi di sessione vengono in genere usati per segnalare le azioni eseguite da un utente durante la sua sessione.</span><span class="sxs-lookup"><span data-stu-id="8e225-150">Session events are usually used to report the actions performed by a user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="8e225-151">Esempio</span><span class="sxs-lookup"><span data-stu-id="8e225-151">Example</span></span>
<span data-ttu-id="8e225-152">**Senza dati:**</span><span class="sxs-lookup"><span data-stu-id="8e225-152">**Without data :**</span></span>

            EngagementAgent.Instance.SendSessionEvent("sessionEvent");

            // or

            EngagementAgent.Instance.SendSessionEvent("sessionEvent", null);

<span data-ttu-id="8e225-153">**Con dati:**</span><span class="sxs-lookup"><span data-stu-id="8e225-153">**With data :**</span></span>

            Dictionary<object, object> extras = new Dictionary<object,object>();
            extras.Add("name", "data");
            EngagementAgent.Instance.SendSessionEvent("sessionEvent", extras);

### <a name="job-events"></a><span data-ttu-id="8e225-154">Eventi di processo</span><span class="sxs-lookup"><span data-stu-id="8e225-154">Job Events</span></span>
#### <a name="reference"></a><span data-ttu-id="8e225-155">riferimento</span><span class="sxs-lookup"><span data-stu-id="8e225-155">Reference</span></span>
            void SendJobEvent(string eventName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="8e225-156">Gli eventi di processo in genere vengono utilizzati per segnalare le azioni eseguite da un utente durante un processo.</span><span class="sxs-lookup"><span data-stu-id="8e225-156">Job events are usually used to report the actions performed by a user during a Job.</span></span>

#### <a name="example"></a><span data-ttu-id="8e225-157">Esempio</span><span class="sxs-lookup"><span data-stu-id="8e225-157">Example</span></span>
            EngagementAgent.Instance.SendJobEvent("eventName", "jobName", extras);

## <a name="reporting-errors"></a><span data-ttu-id="8e225-158">Segnalazione di errori</span><span class="sxs-lookup"><span data-stu-id="8e225-158">Reporting Errors</span></span>
<span data-ttu-id="8e225-159">Esistono tre tipi di errori:</span><span class="sxs-lookup"><span data-stu-id="8e225-159">There is three types of errors :</span></span>

* <span data-ttu-id="8e225-160">Errori autonomi</span><span class="sxs-lookup"><span data-stu-id="8e225-160">Standalone errors</span></span>
* <span data-ttu-id="8e225-161">Errori di sessione</span><span class="sxs-lookup"><span data-stu-id="8e225-161">Session errors</span></span>
* <span data-ttu-id="8e225-162">Errori di processo</span><span class="sxs-lookup"><span data-stu-id="8e225-162">Job errors</span></span>

### <a name="standalone-errors"></a><span data-ttu-id="8e225-163">Errori autonomi</span><span class="sxs-lookup"><span data-stu-id="8e225-163">Standalone errors</span></span>
#### <a name="reference"></a><span data-ttu-id="8e225-164">riferimento</span><span class="sxs-lookup"><span data-stu-id="8e225-164">Reference</span></span>
            void SendError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="8e225-165">Diversamente dagli errori di sessione, gli errori autonomi possono verificarsi all'esterno del contesto di una sessione.</span><span class="sxs-lookup"><span data-stu-id="8e225-165">Contrary to session errors, standalone errors can occur outside of the context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="8e225-166">Esempio</span><span class="sxs-lookup"><span data-stu-id="8e225-166">Example</span></span>
            EngagementAgent.Instance.SendError("errorName", extras);

### <a name="session-errors"></a><span data-ttu-id="8e225-167">Errori di sessione</span><span class="sxs-lookup"><span data-stu-id="8e225-167">Session errors</span></span>
#### <a name="reference"></a><span data-ttu-id="8e225-168">riferimento</span><span class="sxs-lookup"><span data-stu-id="8e225-168">Reference</span></span>
            void SendSessionError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="8e225-169">Gli errori di sessione vengono in genere usati per segnalare gli errori che hanno impatto sull'utente durante la sua sessione.</span><span class="sxs-lookup"><span data-stu-id="8e225-169">Session errors are usually used to report the errors impacting the user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="8e225-170">Esempio</span><span class="sxs-lookup"><span data-stu-id="8e225-170">Example</span></span>
            EngagementAgent.Instance.SendSessionError("errorName", extra);

### <a name="job-errors"></a><span data-ttu-id="8e225-171">Errori di processo</span><span class="sxs-lookup"><span data-stu-id="8e225-171">Job Errors</span></span>
#### <a name="reference"></a><span data-ttu-id="8e225-172">riferimento</span><span class="sxs-lookup"><span data-stu-id="8e225-172">Reference</span></span>
            void SendJobError(string errorName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="8e225-173">Gli errori possono essere correlati a un processo in esecuzione invece che alla sessione utente corrente.</span><span class="sxs-lookup"><span data-stu-id="8e225-173">Errors can be related to a running job instead of being related to the current user session.</span></span>

#### <a name="example"></a><span data-ttu-id="8e225-174">Esempio</span><span class="sxs-lookup"><span data-stu-id="8e225-174">Example</span></span>
            EngagementAgent.Instance.SendJobError("errorName", "jobname", extra);

## <a name="reporting-crashes"></a><span data-ttu-id="8e225-175">Segnalazione di arresti anomali</span><span class="sxs-lookup"><span data-stu-id="8e225-175">Reporting Crashes</span></span>
<span data-ttu-id="8e225-176">L'agente fornisce due metodi per gestire gli arresti anomali.</span><span class="sxs-lookup"><span data-stu-id="8e225-176">The agent provides two methods to deal with crashes.</span></span>

### <a name="send-an-exception"></a><span data-ttu-id="8e225-177">Inviare un'eccezione</span><span class="sxs-lookup"><span data-stu-id="8e225-177">Send an exception</span></span>
#### <a name="reference"></a><span data-ttu-id="8e225-178">riferimento</span><span class="sxs-lookup"><span data-stu-id="8e225-178">Reference</span></span>
            void SendCrash(Exception e, bool terminateSession = false)

#### <a name="example"></a><span data-ttu-id="8e225-179">Esempio</span><span class="sxs-lookup"><span data-stu-id="8e225-179">Example</span></span>
<span data-ttu-id="8e225-180">È possibile inviare un'eccezione in qualsiasi momento chiamando:</span><span class="sxs-lookup"><span data-stu-id="8e225-180">You can send an exception at any time by calling :</span></span>

            EngagementAgent.Instance.SendCrash(aCatchedException);

<span data-ttu-id="8e225-181">È inoltre possibile utilizzare un parametro facoltativo per terminare la sessione di Engagement contemporaneamente all'invio dell'arresto anomalo.</span><span class="sxs-lookup"><span data-stu-id="8e225-181">You can also use an optional parameter to terminate the engagement session at the same time than sending the crash.</span></span> <span data-ttu-id="8e225-182">A tale scopo, chiamare:</span><span class="sxs-lookup"><span data-stu-id="8e225-182">To do so, call :</span></span>

            EngagementAgent.Instance.SendCrash(new Exception("example"), terminateSession: true);

<span data-ttu-id="8e225-183">In questo caso la sessione e i processi verranno chiusi solo dopo l'invio dell'arresto anomalo.</span><span class="sxs-lookup"><span data-stu-id="8e225-183">If you do that, the session and jobs will be closed just after sending the crash.</span></span>

### <a name="send-an-unhandled-exception"></a><span data-ttu-id="8e225-184">Inviare un'eccezione non gestita</span><span class="sxs-lookup"><span data-stu-id="8e225-184">Send an unhandled exception</span></span>
#### <a name="reference"></a><span data-ttu-id="8e225-185">riferimento</span><span class="sxs-lookup"><span data-stu-id="8e225-185">Reference</span></span>
            void SendCrash(ApplicationUnhandledExceptionEventArgs e)

<span data-ttu-id="8e225-186">Engagement fornisce inoltre un metodo per inviare le eccezioni non gestite.</span><span class="sxs-lookup"><span data-stu-id="8e225-186">Engagement also provides a method to send unhandled exceptions.</span></span> <span data-ttu-id="8e225-187">Questa possibilità è particolarmente utile se utilizzata all'interno del gestore eventi UnhandledException Silverlight.</span><span class="sxs-lookup"><span data-stu-id="8e225-187">This is especially useful when used inside the silverlight UnhandledException event handler.</span></span>

<span data-ttu-id="8e225-188">Questo metodo terminerà **SEMPRE** la sessione di Engagement e i processi dopo essere stato chiamato.</span><span class="sxs-lookup"><span data-stu-id="8e225-188">This method will **ALWAYS** terminate the engagement session and jobs after being called.</span></span>

#### <a name="example"></a><span data-ttu-id="8e225-189">Esempio</span><span class="sxs-lookup"><span data-stu-id="8e225-189">Example</span></span>
<span data-ttu-id="8e225-190">È possibile utilizzarlo per implementare il proprio gestore UnhandledException (specialmente se è stata disattivata la funzione di segnalazione automatica degli arresti anomali di Engagement).</span><span class="sxs-lookup"><span data-stu-id="8e225-190">You can use it to implement your own UnhandledException handler (especially if you have disabled the automatic crash reporting feature of Engagement).</span></span> <span data-ttu-id="8e225-191">Ad esempio, nel metodo `Application_UnhandledException` del file `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="8e225-191">For example, in the `Application_UnhandledException` method of the `App.xaml.cs` file :</span></span>

            // In your App.xaml.cs file

            // Code to execute on Unhandled Exceptions
            private void Application_UnhandledException(object sender, ApplicationUnhandledExceptionEventArgs e)
            {
              // your own code

              EngagementAgent.Instance.SendCrash(e);
            }

## <a name="onactivated"></a><span data-ttu-id="8e225-192">OnActivated</span><span class="sxs-lookup"><span data-stu-id="8e225-192">OnActivated</span></span>
### <a name="reference"></a><span data-ttu-id="8e225-193">riferimento</span><span class="sxs-lookup"><span data-stu-id="8e225-193">Reference</span></span>
            void OnActivated(ActivatedEventArgs e)

<span data-ttu-id="8e225-194">Quando l'utente procede con la navigazione, lontano da un'applicazione, una volta generato l'evento di disattivazione il sistema operativo tenterà di mettere l'applicazione in stato di inattività.</span><span class="sxs-lookup"><span data-stu-id="8e225-194">When the user navigates forward, away from an application, after the Deactivated event is raised, the operating system will attempt to put the application into a dormant state.</span></span> <span data-ttu-id="8e225-195">Quindi, l'applicazione viene rimossa definitivamente.</span><span class="sxs-lookup"><span data-stu-id="8e225-195">Then, the application is Tombstoning.</span></span> <span data-ttu-id="8e225-196">In questo processo viene terminata un'applicazione, ma alcuni dati relativi allo stato dell'applicazione e alle singole pagine all'interno dell'applicazione vengono mantenute.</span><span class="sxs-lookup"><span data-stu-id="8e225-196">In this process an application is terminated but some data about the state of the application and the individual pages within the application is preserved.</span></span>

<span data-ttu-id="8e225-197">È necessario inserire `EngagementAgent.Instance.OnActivated(e)` nel metodo `Application_Activated` dal file App.xaml.cs per reimpostare l'agente di Engagement quando l'applicazione è stata rimossa definitivamente.</span><span class="sxs-lookup"><span data-stu-id="8e225-197">You have to insert `EngagementAgent.Instance.OnActivated(e)` in the `Application_Activated` method from the App.xaml.cs file to reset the Engagement Agent when the application has been Tombstoned.</span></span>

### <a name="example"></a><span data-ttu-id="8e225-198">Esempio</span><span class="sxs-lookup"><span data-stu-id="8e225-198">Example</span></span>
            // Inside your App.xaml.cs file

            // Code to execute when the application is activated (brought to foreground)
            // This code will not execute when the application is first launched
            private void Application_Activated(object sender, ActivatedEventArgs e)
            {
              EngagementAgent.Instance.OnActivated(e);
            }

## <a name="device-id"></a><span data-ttu-id="8e225-199">Id dispositivo</span><span class="sxs-lookup"><span data-stu-id="8e225-199">Device Id</span></span>
            String GetDeviceId()

<span data-ttu-id="8e225-200">È possibile ottenere l'id del dispositivo Engagement chiamando questo metodo.</span><span class="sxs-lookup"><span data-stu-id="8e225-200">You can get the engagement device id by calling this method.</span></span>

## <a name="extras-parameters"></a><span data-ttu-id="8e225-201">Parametri aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="8e225-201">Extras parameters</span></span>
<span data-ttu-id="8e225-202">Dati arbitrari possono essere collegati a un evento, un errore, un'attività o un processo.</span><span class="sxs-lookup"><span data-stu-id="8e225-202">Arbitrary data can be attached to an event, an error, an activity or a job.</span></span> <span data-ttu-id="8e225-203">Tali dati possono essere strutturati utilizzando un dizionario.</span><span class="sxs-lookup"><span data-stu-id="8e225-203">These data can be structured using a dictionary.</span></span> <span data-ttu-id="8e225-204">Chiavi e valori possono essere di qualsiasi tipo.</span><span class="sxs-lookup"><span data-stu-id="8e225-204">Keys and values can be of any type.</span></span>

<span data-ttu-id="8e225-205">I dati aggiuntivi vengono serializzati, per cui se si desidera inserirvi il proprio tipo è necessario aggiungere un contratto dati per questo tipo.</span><span class="sxs-lookup"><span data-stu-id="8e225-205">Extras data are serialized so if you want to insert your own type in extras you have to add a data contract for this type.</span></span>

### <a name="example"></a><span data-ttu-id="8e225-206">Esempio</span><span class="sxs-lookup"><span data-stu-id="8e225-206">Example</span></span>
<span data-ttu-id="8e225-207">Si crea una nuova classe "Person".</span><span class="sxs-lookup"><span data-stu-id="8e225-207">We create a new class "Person".</span></span>

            using System.Runtime.Serialization;

            namespace Engagement.Agent
            {
              [DataContract]
              public class Person
              {
                public Person(string name, int age)
                {
                  Age = age;
                  Name = name;
                }

                // Properties

                [DataMember]
                public int Age
                {
                  get;
                  set;
                }

                [DataMember]
                public string Name
                {
                  get;
                  set; 
                }
              }
            }

<span data-ttu-id="8e225-208">Quindi, si include un'istanza di `Person` per un dato aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="8e225-208">Then, we will add a `Person` instance to an extra.</span></span>

            Person person = new Person("Engagement Haddock", 51);
            var extras = new Dictionary<object, object>();
            extras.Add("people", person);

            EngagementAgent.Instance.SendEvent("Event", extras);

> [!WARNING]
> <span data-ttu-id="8e225-209">Se si inseriscono altri tipi di oggetti, assicurarsi che il relativo metodo ToString() venga implementato per restituire una stringa leggibile.</span><span class="sxs-lookup"><span data-stu-id="8e225-209">If you put other types of objects, make sure their ToString() method is implemented to return a human readable string.</span></span>
> 
> 

### <a name="limits"></a><span data-ttu-id="8e225-210">Limiti</span><span class="sxs-lookup"><span data-stu-id="8e225-210">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="8e225-211">Chiavi</span><span class="sxs-lookup"><span data-stu-id="8e225-211">Keys</span></span>
<span data-ttu-id="8e225-212">Ogni chiave dell'oggetto deve corrispondere all'espressione regolare seguente:</span><span class="sxs-lookup"><span data-stu-id="8e225-212">Each key in the object must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="8e225-213">Questo significa che le chiavi devono iniziare con almeno una lettera, seguita da lettere, numeri o caratteri di sottolineatura (\_).</span><span class="sxs-lookup"><span data-stu-id="8e225-213">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="8e225-214">Dimensione</span><span class="sxs-lookup"><span data-stu-id="8e225-214">Size</span></span>
<span data-ttu-id="8e225-215">I dati aggiuntivi sono limitati a **1024** caratteri per chiamata.</span><span class="sxs-lookup"><span data-stu-id="8e225-215">Extras are limited to **1024** characters per call.</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="8e225-216">Segnalazione di informazioni sull'applicazione</span><span class="sxs-lookup"><span data-stu-id="8e225-216">Reporting Application Information</span></span>
### <a name="reference"></a><span data-ttu-id="8e225-217">riferimento</span><span class="sxs-lookup"><span data-stu-id="8e225-217">Reference</span></span>
            void SendAppInfo(Dictionary<object, object> appInfos)

<span data-ttu-id="8e225-218">È possibile segnalare manualmente le informazioni di traccia o qualsiasi altra informazione specifica dell'applicazione mediante la funzione SendAppInfo().</span><span class="sxs-lookup"><span data-stu-id="8e225-218">You can manually report tracking information (or any other application specific information) using the SendAppInfo() function.</span></span>

<span data-ttu-id="8e225-219">Queste informazioni possono essere inviate in modo incrementale: viene mantenuto solo l'ultimo valore per una determinata chiave per ogni dispositivo specifico.</span><span class="sxs-lookup"><span data-stu-id="8e225-219">Note that these information can be sent incrementally: only the latest value for a given key will be kept for a given device.</span></span> <span data-ttu-id="8e225-220">Come per i dati aggiuntivi degli eventi, usare Dictionary\<object, object\> per allegare informazioni.</span><span class="sxs-lookup"><span data-stu-id="8e225-220">Like event extras, use a Dictionary\<object, object\> to attach informations.</span></span>

### <a name="example"></a><span data-ttu-id="8e225-221">Esempio</span><span class="sxs-lookup"><span data-stu-id="8e225-221">Example</span></span>
            Dictionary<object, object> appInfo = new Dictionary<object, object>()
            {
               {"subscription", "2013-12-07"},
               {"premium", "true"}
            };

            EngagementAgent.Instance.SendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="8e225-222">Limiti</span><span class="sxs-lookup"><span data-stu-id="8e225-222">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="8e225-223">Chiavi</span><span class="sxs-lookup"><span data-stu-id="8e225-223">Keys</span></span>
<span data-ttu-id="8e225-224">Ogni chiave dell'oggetto deve corrispondere all'espressione regolare seguente:</span><span class="sxs-lookup"><span data-stu-id="8e225-224">Each key in the object must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="8e225-225">Questo significa che le chiavi devono iniziare con almeno una lettera, seguita da lettere, numeri o caratteri di sottolineatura (\_).</span><span class="sxs-lookup"><span data-stu-id="8e225-225">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="8e225-226">Dimensione</span><span class="sxs-lookup"><span data-stu-id="8e225-226">Size</span></span>
<span data-ttu-id="8e225-227">Le informazioni sull'applicazione sono limitate a **1024** caratteri per chiamata.</span><span class="sxs-lookup"><span data-stu-id="8e225-227">Application information are limited to **1024** characters per call.</span></span>

<span data-ttu-id="8e225-228">Nell'esempio precedente il codice JSON inviato al server è lungo 44 caratteri:</span><span class="sxs-lookup"><span data-stu-id="8e225-228">In the previous example, the JSON sent to the server is 44 characters long:</span></span>

            {"subscription":"2013-12-07","premium":"true"}

## <a name="logging"></a><span data-ttu-id="8e225-229">Registrazione</span><span class="sxs-lookup"><span data-stu-id="8e225-229">Logging</span></span>
### <a name="enable-logging"></a><span data-ttu-id="8e225-230">Abilitare la registrazione</span><span class="sxs-lookup"><span data-stu-id="8e225-230">Enable Logging</span></span>
<span data-ttu-id="8e225-231">È possibile configurare SDK per generare log di test nella console IDE.</span><span class="sxs-lookup"><span data-stu-id="8e225-231">The SDK can be configured to produce test logs in the IDE console.</span></span>
<span data-ttu-id="8e225-232">Questi log non sono abilitati per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="8e225-232">These logs are not activated by default.</span></span> <span data-ttu-id="8e225-233">Per eseguire una personalizzazione, aggiornare la proprietà `EngagementAgent.Instance.TestLogEnabled` scegliendo uno dei valori disponibili nell'enumerazione `EngagementTestLogLevel`, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="8e225-233">To customize this, update the property `EngagementAgent.Instance.TestLogEnabled` to one of the value available from the `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();
