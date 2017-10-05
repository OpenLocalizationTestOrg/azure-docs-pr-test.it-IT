---
title: Come usare l'API di Engagement in un'app di Windows universale
description: Come usare l'API di Engagement in un'app di Windows universale
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: bb501fca-9cfe-4495-81df-b5efd6e0137b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 75fc134a5535e6113331470cf61df9c06eb8e2ab
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-engagement-api-on-windows-universal"></a><span data-ttu-id="b96be-103">Come usare l'API di Engagement in un'app di Windows universale</span><span class="sxs-lookup"><span data-stu-id="b96be-103">How to Use the Engagement API on Windows Universal</span></span>
<span data-ttu-id="b96be-104">Questo documento è complementare all'articolo [Come integrare Engagement in un'app di Windows universale](mobile-engagement-windows-store-integrate-engagement.md)e fornisce informazioni approfondite su come usare l'API di Engagement per segnalare le statistiche dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b96be-104">This document is an add-on to the document [How to Integrate Engagement on Windows Universal](mobile-engagement-windows-store-integrate-engagement.md): it provides in depth details about how to use the Engagement API to report your application statistics.</span></span>

<span data-ttu-id="b96be-105">Tenere presente che, se si vuole impostare Engagement in modo che segnali solo le sessioni, le attività, gli arresti anomali e i dati tecnici dell'applicazione, la soluzione più semplice consiste nel fare in modo che tutte le sottoclassi `Page` ereditino dalla classe `EngagementPage`.</span><span class="sxs-lookup"><span data-stu-id="b96be-105">Keep in mind that if you only want Engagement to report your application's sessions, activities, crashes and technical information, then the simplest way is to make all your `Page` sub-classes inherit from the `EngagementPage` class.</span></span>

<span data-ttu-id="b96be-106">Se invece si hanno esigenze più complesse, ad esempio se è necessario segnalare eventi, errori e processi specifici dell'applicazione o presentare le attività dell'applicazione in modo diverso rispetto a quello implementato nelle classi `EngagementPage`, è necessario usare l'API di Engagement.</span><span class="sxs-lookup"><span data-stu-id="b96be-106">If you want to do more, for example if you need to report application specific events, errors and jobs, or if you have to report your application's activities in a different way than the one implemented in the `EngagementPage` classes, then you need to use the Engagement API.</span></span>

<span data-ttu-id="b96be-107">L'API di Engagement viene fornita dalla classe `EngagementAgent` .</span><span class="sxs-lookup"><span data-stu-id="b96be-107">The Engagement API is provided by the `EngagementAgent` class.</span></span> <span data-ttu-id="b96be-108">È possibile accedere a questi metodi tramite `EngagementAgent.Instance`.</span><span class="sxs-lookup"><span data-stu-id="b96be-108">You can access to those methods through `EngagementAgent.Instance`.</span></span>

<span data-ttu-id="b96be-109">Anche se il modulo dell'agente non è stato inizializzato, ogni chiamata all'API viene posticipata e verrà eseguita nuovamente quando l'agente è disponibile.</span><span class="sxs-lookup"><span data-stu-id="b96be-109">Even if the agent module has not been initialized, each call to the API is deferred, and will be executed again when the agent is available.</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="b96be-110">Concetti relativi a Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="b96be-110">Engagement concepts</span></span>
<span data-ttu-id="b96be-111">Le parti seguenti approfondiscono le informazioni contenute nell'articolo [Concetti relativi ad Azure Mobile Engagement](mobile-engagement-concepts.md) per la piattaforma Windows universale.</span><span class="sxs-lookup"><span data-stu-id="b96be-111">The following parts refine the common [Mobile Engagement Concepts](mobile-engagement-concepts.md) for the Windows Universal platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="b96be-112">`Session` e `Activity`</span><span class="sxs-lookup"><span data-stu-id="b96be-112">`Session` and `Activity`</span></span>
<span data-ttu-id="b96be-113">Un'*attività* è in genere associata a una pagina dell'applicazione, ovvero l'*attività* inizia quando la pagina viene visualizzata e si arresta quando la pagina viene chiusa. Questo avviene quando Engagement SDK è integrato mediante la classe `EngagementPage`.</span><span class="sxs-lookup"><span data-stu-id="b96be-113">An *activity* is usually associated with one page of the application, that is to say the *activity* starts when the page is displayed and stops when the page is closed: this is the case when the Engagement SDK is integrated by using the `EngagementPage` class.</span></span>

<span data-ttu-id="b96be-114">Le *attività* possono tuttavia essere controllate anche manualmente usando l'API di Engagement.</span><span class="sxs-lookup"><span data-stu-id="b96be-114">But *activities* can also be controlled manually by using the Engagement API.</span></span> <span data-ttu-id="b96be-115">Ciò consente di dividere una determinata pagina in più sottoparti per ottenere maggiori dettagli sull'uso della pagina (ad esempio per conoscere la frequenza e la durata dell'uso delle finestre di dialogo all'interno della pagina).</span><span class="sxs-lookup"><span data-stu-id="b96be-115">This allows you to split a given page in several sub parts to get more details about the usage of this page (for example to know how often and how long dialogs are used inside this page).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="b96be-116">Segnalazione di attività</span><span class="sxs-lookup"><span data-stu-id="b96be-116">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="b96be-117">L'utente inizia una nuova attività</span><span class="sxs-lookup"><span data-stu-id="b96be-117">User starts a new Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="b96be-118">riferimento</span><span class="sxs-lookup"><span data-stu-id="b96be-118">Reference</span></span>
            void StartActivity(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="b96be-119">È necessario chiamare `StartActivity()` ogni volta che l'attività dell'utente cambia.</span><span class="sxs-lookup"><span data-stu-id="b96be-119">You need to call `StartActivity()` each time the user activity changes.</span></span> <span data-ttu-id="b96be-120">La prima chiamata a questa funzione avvia una nuova sessione utente.</span><span class="sxs-lookup"><span data-stu-id="b96be-120">The first call to this function starts a new user session.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b96be-121">L'SDK chiama automaticamente il metodo EndActivity quando viene chiusa l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b96be-121">The SDK automatically calls the EndActivity method when the application is closed.</span></span> <span data-ttu-id="b96be-122">Di conseguenza, è ALTAMENTE consigliato chiamare il metodo StartActivity ogni volta che l'attività dell'utente cambia e non chiamare MAI il metodo EndActivity poiché la chiamata di questo metodo forza la chiusura della sessione corrente.</span><span class="sxs-lookup"><span data-stu-id="b96be-122">Thus, it is HIGHLY recommended to call the StartActivity method whenever the activity of the user changes, and to NEVER call the EndActivity method, since calling this method forces the current session to be ended.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="b96be-123">Esempio</span><span class="sxs-lookup"><span data-stu-id="b96be-123">Example</span></span>
            EngagementAgent.Instance.StartActivity("main", new Dictionary<object, object>() {{"example", "data"}});

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="b96be-124">L'utente termina l'attività corrente</span><span class="sxs-lookup"><span data-stu-id="b96be-124">User ends his current Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="b96be-125">riferimento</span><span class="sxs-lookup"><span data-stu-id="b96be-125">Reference</span></span>
            void EndActivity()

<span data-ttu-id="b96be-126">Vengono terminate l'attività e la sessione.</span><span class="sxs-lookup"><span data-stu-id="b96be-126">This ends the activity and the session.</span></span> <span data-ttu-id="b96be-127">Chiamare questo metodo solo se si è perfettamente consapevoli delle conseguenze.</span><span class="sxs-lookup"><span data-stu-id="b96be-127">You should not call this method unless you really know what you're doing.</span></span>

#### <a name="example"></a><span data-ttu-id="b96be-128">Esempio</span><span class="sxs-lookup"><span data-stu-id="b96be-128">Example</span></span>
            EngagementAgent.Instance.EndActivity();

## <a name="reporting-jobs"></a><span data-ttu-id="b96be-129">Segnalazione di processi</span><span class="sxs-lookup"><span data-stu-id="b96be-129">Reporting Jobs</span></span>
### <a name="start-a-job"></a><span data-ttu-id="b96be-130">Avviare un processo</span><span class="sxs-lookup"><span data-stu-id="b96be-130">Start a job</span></span>
#### <a name="reference"></a><span data-ttu-id="b96be-131">riferimento</span><span class="sxs-lookup"><span data-stu-id="b96be-131">Reference</span></span>
            void StartJob(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="b96be-132">È possibile utilizzare il processo per tenere traccia delle attività in un determinato periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="b96be-132">You can use the job to track certains tasks over a period of time.</span></span>

#### <a name="example"></a><span data-ttu-id="b96be-133">Esempio</span><span class="sxs-lookup"><span data-stu-id="b96be-133">Example</span></span>
            // An upload begins...

            // Set the extras
            var extras = new Dictionary<object, object>();
            extras.Add("title", "avatar");
            extras.Add("type", "image");

            EngagementAgent.Instance.StartJob("uploadData", extras);

### <a name="end-a-job"></a><span data-ttu-id="b96be-134">Terminare un processo</span><span class="sxs-lookup"><span data-stu-id="b96be-134">End a job</span></span>
#### <a name="reference"></a><span data-ttu-id="b96be-135">riferimento</span><span class="sxs-lookup"><span data-stu-id="b96be-135">Reference</span></span>
            void EndJob(string name)

<span data-ttu-id="b96be-136">Appena terminata un'attività di cui un processo tiene traccia, è necessario chiamare il metodo EndJob per questo processo, fornendo il nome del processo.</span><span class="sxs-lookup"><span data-stu-id="b96be-136">As soon as a task tracked by a job has been terminated, you should call the EndJob method for this job, by supplying the job name.</span></span>

#### <a name="example"></a><span data-ttu-id="b96be-137">Esempio</span><span class="sxs-lookup"><span data-stu-id="b96be-137">Example</span></span>
            // In the previous section, we started an upload tracking with a job
            // Then, the upload ends

            EngagementAgent.Instance.EndJob("uploadData");

## <a name="reporting-events"></a><span data-ttu-id="b96be-138">Segnalazione di eventi</span><span class="sxs-lookup"><span data-stu-id="b96be-138">Reporting Events</span></span>
<span data-ttu-id="b96be-139">Esistono tre tipi di eventi:</span><span class="sxs-lookup"><span data-stu-id="b96be-139">There is three types of events :</span></span>

* <span data-ttu-id="b96be-140">Eventi autonomi</span><span class="sxs-lookup"><span data-stu-id="b96be-140">Standalone events</span></span>
* <span data-ttu-id="b96be-141">Eventi di sessione</span><span class="sxs-lookup"><span data-stu-id="b96be-141">Session events</span></span>
* <span data-ttu-id="b96be-142">Eventi di processo</span><span class="sxs-lookup"><span data-stu-id="b96be-142">Job events</span></span>

### <a name="standalone-events"></a><span data-ttu-id="b96be-143">Eventi autonomi</span><span class="sxs-lookup"><span data-stu-id="b96be-143">Standalone Events</span></span>
#### <a name="reference"></a><span data-ttu-id="b96be-144">riferimento</span><span class="sxs-lookup"><span data-stu-id="b96be-144">Reference</span></span>
            void SendEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="b96be-145">Gli eventi autonomi possono verificarsi all'esterno del contesto di una sessione.</span><span class="sxs-lookup"><span data-stu-id="b96be-145">Standalone events can occur outside of the context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="b96be-146">Esempio</span><span class="sxs-lookup"><span data-stu-id="b96be-146">Example</span></span>
            EngagementAgent.Instance.SendEvent("event", extra);

### <a name="session-events"></a><span data-ttu-id="b96be-147">Eventi di sessione</span><span class="sxs-lookup"><span data-stu-id="b96be-147">Session events</span></span>
#### <a name="reference"></a><span data-ttu-id="b96be-148">riferimento</span><span class="sxs-lookup"><span data-stu-id="b96be-148">Reference</span></span>
            void SendSessionEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="b96be-149">Gli eventi di sessione vengono in genere usati per segnalare le azioni eseguite da un utente durante la sua sessione.</span><span class="sxs-lookup"><span data-stu-id="b96be-149">Session events are usually used to report the actions performed by a user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="b96be-150">Esempio</span><span class="sxs-lookup"><span data-stu-id="b96be-150">Example</span></span>
<span data-ttu-id="b96be-151">**Senza dati:**</span><span class="sxs-lookup"><span data-stu-id="b96be-151">**Without data :**</span></span>

            EngagementAgent.Instance.SendSessionEvent("sessionEvent");

            // or

            EngagementAgent.Instance.SendSessionEvent("sessionEvent", null);

<span data-ttu-id="b96be-152">**Con dati:**</span><span class="sxs-lookup"><span data-stu-id="b96be-152">**With data :**</span></span>

            Dictionary<object, object> extras = new Dictionary<object,object>();
            extras.Add("name", "data");
            EngagementAgent.Instance.SendSessionEvent("sessionEvent", extras);

### <a name="job-events"></a><span data-ttu-id="b96be-153">Eventi di processo</span><span class="sxs-lookup"><span data-stu-id="b96be-153">Job Events</span></span>
#### <a name="reference"></a><span data-ttu-id="b96be-154">riferimento</span><span class="sxs-lookup"><span data-stu-id="b96be-154">Reference</span></span>
            void SendJobEvent(string eventName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="b96be-155">Gli eventi di processo in genere vengono utilizzati per segnalare le azioni eseguite da un utente durante un processo.</span><span class="sxs-lookup"><span data-stu-id="b96be-155">Job events are usually used to report the actions performed by a user during a Job.</span></span>

#### <a name="example"></a><span data-ttu-id="b96be-156">Esempio</span><span class="sxs-lookup"><span data-stu-id="b96be-156">Example</span></span>
            EngagementAgent.Instance.SendJobEvent("eventName", "jobName", extras);

## <a name="reporting-errors"></a><span data-ttu-id="b96be-157">Segnalazione di errori</span><span class="sxs-lookup"><span data-stu-id="b96be-157">Reporting Errors</span></span>
<span data-ttu-id="b96be-158">Esistono tre tipi di errore:</span><span class="sxs-lookup"><span data-stu-id="b96be-158">There are three types of errors :</span></span>

* <span data-ttu-id="b96be-159">Errori autonomi</span><span class="sxs-lookup"><span data-stu-id="b96be-159">Standalone errors</span></span>
* <span data-ttu-id="b96be-160">Errori di sessione</span><span class="sxs-lookup"><span data-stu-id="b96be-160">Session errors</span></span>
* <span data-ttu-id="b96be-161">Errori di processo</span><span class="sxs-lookup"><span data-stu-id="b96be-161">Job errors</span></span>

### <a name="standalone-errors"></a><span data-ttu-id="b96be-162">Errori autonomi</span><span class="sxs-lookup"><span data-stu-id="b96be-162">Standalone errors</span></span>
#### <a name="reference"></a><span data-ttu-id="b96be-163">riferimento</span><span class="sxs-lookup"><span data-stu-id="b96be-163">Reference</span></span>
            void SendError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="b96be-164">Diversamente dagli errori di sessione, gli errori autonomi possono verificarsi all'esterno del contesto di una sessione.</span><span class="sxs-lookup"><span data-stu-id="b96be-164">Contrary to session errors, standalone errors can occur outside of the context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="b96be-165">Esempio</span><span class="sxs-lookup"><span data-stu-id="b96be-165">Example</span></span>
            EngagementAgent.Instance.SendError("errorName", extras);

### <a name="session-errors"></a><span data-ttu-id="b96be-166">Errori di sessione</span><span class="sxs-lookup"><span data-stu-id="b96be-166">Session errors</span></span>
#### <a name="reference"></a><span data-ttu-id="b96be-167">riferimento</span><span class="sxs-lookup"><span data-stu-id="b96be-167">Reference</span></span>
            void SendSessionError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="b96be-168">Gli errori di sessione vengono in genere usati per segnalare gli errori che hanno impatto sull'utente durante la sua sessione.</span><span class="sxs-lookup"><span data-stu-id="b96be-168">Session errors are usually used to report the errors impacting the user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="b96be-169">Esempio</span><span class="sxs-lookup"><span data-stu-id="b96be-169">Example</span></span>
            EngagementAgent.Instance.SendSessionError("errorName", extra);

### <a name="job-errors"></a><span data-ttu-id="b96be-170">Errori di processo</span><span class="sxs-lookup"><span data-stu-id="b96be-170">Job Errors</span></span>
#### <a name="reference"></a><span data-ttu-id="b96be-171">riferimento</span><span class="sxs-lookup"><span data-stu-id="b96be-171">Reference</span></span>
            void SendJobError(string errorName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="b96be-172">Gli errori possono essere correlati a un processo in esecuzione invece che alla sessione utente corrente.</span><span class="sxs-lookup"><span data-stu-id="b96be-172">Errors can be related to a running job instead of being related to the current user session.</span></span>

#### <a name="example"></a><span data-ttu-id="b96be-173">Esempio</span><span class="sxs-lookup"><span data-stu-id="b96be-173">Example</span></span>
            EngagementAgent.Instance.SendJobError("errorName", "jobname", extra);

## <a name="reporting-crashes"></a><span data-ttu-id="b96be-174">Segnalazione di arresti anomali</span><span class="sxs-lookup"><span data-stu-id="b96be-174">Reporting Crashes</span></span>
<span data-ttu-id="b96be-175">L'agente fornisce due metodi per gestire gli arresti anomali.</span><span class="sxs-lookup"><span data-stu-id="b96be-175">The agent provides two methods to deal with crashes.</span></span>

### <a name="send-an-exception"></a><span data-ttu-id="b96be-176">Inviare un'eccezione</span><span class="sxs-lookup"><span data-stu-id="b96be-176">Send an exception</span></span>
#### <a name="reference"></a><span data-ttu-id="b96be-177">riferimento</span><span class="sxs-lookup"><span data-stu-id="b96be-177">Reference</span></span>
            void SendCrash(Exception e, bool terminateSession = false)

#### <a name="example"></a><span data-ttu-id="b96be-178">Esempio</span><span class="sxs-lookup"><span data-stu-id="b96be-178">Example</span></span>
<span data-ttu-id="b96be-179">È possibile inviare un'eccezione in qualsiasi momento chiamando:</span><span class="sxs-lookup"><span data-stu-id="b96be-179">You can send an exception at any time by calling :</span></span>

            EngagementAgent.Instance.SendCrash(aCatchedException);

<span data-ttu-id="b96be-180">È inoltre possibile utilizzare un parametro facoltativo per terminare la sessione di Engagement contemporaneamente all'invio dell'arresto anomalo.</span><span class="sxs-lookup"><span data-stu-id="b96be-180">You can also use an optional parameter to terminate the engagement session at the same time than sending the crash.</span></span> <span data-ttu-id="b96be-181">A tale scopo, chiamare:</span><span class="sxs-lookup"><span data-stu-id="b96be-181">To do so, call :</span></span>

            EngagementAgent.Instance.SendCrash(new Exception("example"), terminateSession: true);

<span data-ttu-id="b96be-182">In questo caso la sessione e i processi verranno chiusi solo dopo l'invio dell'arresto anomalo.</span><span class="sxs-lookup"><span data-stu-id="b96be-182">If you do that, the session and jobs will be closed just after sending the crash.</span></span>

### <a name="send-an-unhandled-exception"></a><span data-ttu-id="b96be-183">Inviare un'eccezione non gestita</span><span class="sxs-lookup"><span data-stu-id="b96be-183">Send an unhandled exception</span></span>
#### <a name="reference"></a><span data-ttu-id="b96be-184">riferimento</span><span class="sxs-lookup"><span data-stu-id="b96be-184">Reference</span></span>
            void SendCrash(Exception e)

<span data-ttu-id="b96be-185">Engagement fornisce anche un metodo per inviare le eccezioni non gestite, se è stata **DISABILITATA** la segnalazione automatica degli **arresti anomali** in Engagement.</span><span class="sxs-lookup"><span data-stu-id="b96be-185">Engagement also provides a method to send unhandled exceptions if you have **DISABLED** Engagement automatic **crash** reporting.</span></span> <span data-ttu-id="b96be-186">Questa possibilità è particolarmente utile se utilizzata all'interno del gestore eventi UnhandledException.</span><span class="sxs-lookup"><span data-stu-id="b96be-186">This is especially useful when used inside the application UnhandledException event handler.</span></span>

<span data-ttu-id="b96be-187">Questo metodo terminerà **SEMPRE** la sessione di Engagement e i processi dopo essere stato chiamato.</span><span class="sxs-lookup"><span data-stu-id="b96be-187">This method will **ALWAYS** terminate the engagement session and jobs after being called.</span></span>

#### <a name="example"></a><span data-ttu-id="b96be-188">Esempio</span><span class="sxs-lookup"><span data-stu-id="b96be-188">Example</span></span>
<span data-ttu-id="b96be-189">Consente di implementare un proprio gestore UnhandledExceptionEventArgs.</span><span class="sxs-lookup"><span data-stu-id="b96be-189">You can use it to implement your own UnhandledExceptionEventArgs handler.</span></span> <span data-ttu-id="b96be-190">Ad esempio, aggiungere il metodo `Current_UnhandledException` del file `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="b96be-190">For example, add the `Current_UnhandledException` method of the `App.xaml.cs` file :</span></span>

            // In your App.xaml.cs file

            // Code to execute on Unhandled Exceptions
            void Current_UnhandledException(object sender, UnhandledExceptionEventArgs e)
            {
               EngagementAgent.Instance.SendCrash(e.Exception,false);
            }

<span data-ttu-id="b96be-191">In App.xaml.cs in "Public App(){}" aggiungere:</span><span class="sxs-lookup"><span data-stu-id="b96be-191">In App.xaml.cs in "Public App(){}" add:</span></span>

            Application.Current.UnhandledException += Current_UnhandledException;

## <a name="device-id"></a><span data-ttu-id="b96be-192">Id dispositivo</span><span class="sxs-lookup"><span data-stu-id="b96be-192">Device Id</span></span>
            String EngagementAgent.Instance.GetDeviceId()

<span data-ttu-id="b96be-193">È possibile ottenere l'id del dispositivo Engagement chiamando questo metodo.</span><span class="sxs-lookup"><span data-stu-id="b96be-193">You can get the engagement device id by calling this method.</span></span>

## <a name="extras-parameters"></a><span data-ttu-id="b96be-194">Parametri aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="b96be-194">Extras parameters</span></span>
<span data-ttu-id="b96be-195">Dati arbitrari possono essere collegati a un evento, un errore, un'attività o un processo.</span><span class="sxs-lookup"><span data-stu-id="b96be-195">Arbitrary data can be attached to an event, an error, an activity or a job.</span></span> <span data-ttu-id="b96be-196">Tali dati possono essere strutturati utilizzando un dizionario.</span><span class="sxs-lookup"><span data-stu-id="b96be-196">These data can be structured using a dictionary.</span></span> <span data-ttu-id="b96be-197">Chiavi e valori possono essere di qualsiasi tipo.</span><span class="sxs-lookup"><span data-stu-id="b96be-197">Keys and values can be of any type.</span></span>

<span data-ttu-id="b96be-198">I dati aggiuntivi vengono serializzati, per cui se si desidera inserirvi il proprio tipo è necessario aggiungere un contratto dati per questo tipo.</span><span class="sxs-lookup"><span data-stu-id="b96be-198">Extras data are serialized so if you want to insert your own type in extras you have to add a data contract for this type.</span></span>

### <a name="example"></a><span data-ttu-id="b96be-199">Esempio</span><span class="sxs-lookup"><span data-stu-id="b96be-199">Example</span></span>
<span data-ttu-id="b96be-200">Si crea una nuova classe "Person".</span><span class="sxs-lookup"><span data-stu-id="b96be-200">We create a new class "Person".</span></span>

            using System.Runtime.Serialization;

            namespace Microsoft.Azure.Engagement
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

<span data-ttu-id="b96be-201">Quindi, si include un'istanza di `Person` per un dato aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="b96be-201">Then, we will add a `Person` instance to an extra.</span></span>

            Person person = new Person("Engagement Haddock", 51);
            var extras = new Dictionary<object, object>();
            extras.Add("people", person);

            EngagementAgent.Instance.SendEvent("Event", extras);

> [!WARNING]
> <span data-ttu-id="b96be-202">Se si inseriscono altri tipi di oggetti, assicurarsi che il relativo metodo ToString() venga implementato per restituire una stringa leggibile.</span><span class="sxs-lookup"><span data-stu-id="b96be-202">If you put other types of objects, make sure their ToString() method is implemented to return a human readable string.</span></span>
> 
> 

### <a name="limits"></a><span data-ttu-id="b96be-203">Limiti</span><span class="sxs-lookup"><span data-stu-id="b96be-203">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="b96be-204">Chiavi</span><span class="sxs-lookup"><span data-stu-id="b96be-204">Keys</span></span>
<span data-ttu-id="b96be-205">Ogni chiave dell'oggetto deve corrispondere all'espressione regolare seguente:</span><span class="sxs-lookup"><span data-stu-id="b96be-205">Each key in the object must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="b96be-206">Questo significa che le chiavi devono iniziare con almeno una lettera, seguita da lettere, numeri o caratteri di sottolineatura (\_).</span><span class="sxs-lookup"><span data-stu-id="b96be-206">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="b96be-207">Dimensione</span><span class="sxs-lookup"><span data-stu-id="b96be-207">Size</span></span>
<span data-ttu-id="b96be-208">I dati aggiuntivi sono limitati a **1024** caratteri per chiamata.</span><span class="sxs-lookup"><span data-stu-id="b96be-208">Extras are limited to **1024** characters per call.</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="b96be-209">Segnalazione di informazioni sull'applicazione</span><span class="sxs-lookup"><span data-stu-id="b96be-209">Reporting Application Information</span></span>
### <a name="reference"></a><span data-ttu-id="b96be-210">riferimento</span><span class="sxs-lookup"><span data-stu-id="b96be-210">Reference</span></span>
            void SendAppInfo(Dictionary<object, object> appInfos)

<span data-ttu-id="b96be-211">È possibile segnalare manualmente le informazioni di traccia o qualsiasi altra informazione specifica dell'applicazione mediante la funzione SendAppInfo().</span><span class="sxs-lookup"><span data-stu-id="b96be-211">You can manually report tracking information (or any other application specific information) using the SendAppInfo() function.</span></span>

<span data-ttu-id="b96be-212">Questi dati possono essere inviati in modo incrementale: viene mantenuto solo l'ultimo valore per una determinata chiave per ogni dispositivo specifico.</span><span class="sxs-lookup"><span data-stu-id="b96be-212">Note that this data can be sent incrementally: only the latest value for a given key will be kept for a given device.</span></span> <span data-ttu-id="b96be-213">Come per le informazioni aggiuntive degli eventi, usare Dictionary\<object, object\> per allegare dati.</span><span class="sxs-lookup"><span data-stu-id="b96be-213">Like event extras, use a Dictionary\<object, object\> to attach data.</span></span>

### <a name="example"></a><span data-ttu-id="b96be-214">Esempio</span><span class="sxs-lookup"><span data-stu-id="b96be-214">Example</span></span>
            Dictionary<object, object> appInfo = new Dictionary<object, object>()
              {
                {"birthdate", "1983-12-07"},
                {"gender", "female"}
              };

            EngagementAgent.Instance.SendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="b96be-215">Limiti</span><span class="sxs-lookup"><span data-stu-id="b96be-215">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="b96be-216">Chiavi</span><span class="sxs-lookup"><span data-stu-id="b96be-216">Keys</span></span>
<span data-ttu-id="b96be-217">Ogni chiave dell'oggetto deve corrispondere all'espressione regolare seguente:</span><span class="sxs-lookup"><span data-stu-id="b96be-217">Each key in the object must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="b96be-218">Questo significa che le chiavi devono iniziare con almeno una lettera, seguita da lettere, numeri o caratteri di sottolineatura (\_).</span><span class="sxs-lookup"><span data-stu-id="b96be-218">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="b96be-219">Dimensione</span><span class="sxs-lookup"><span data-stu-id="b96be-219">Size</span></span>
<span data-ttu-id="b96be-220">Le informazioni sull'applicazione sono limitate a **1024** caratteri per chiamata.</span><span class="sxs-lookup"><span data-stu-id="b96be-220">Application information is limited to **1024** characters per call.</span></span>

<span data-ttu-id="b96be-221">Nell'esempio precedente il codice JSON inviato al server è lungo 44 caratteri:</span><span class="sxs-lookup"><span data-stu-id="b96be-221">In the previous example, the JSON sent to the server is 44 characters long:</span></span>

            {"birthdate":"1983-12-07","gender":"female"}

## <a name="logging"></a><span data-ttu-id="b96be-222">Registrazione</span><span class="sxs-lookup"><span data-stu-id="b96be-222">Logging</span></span>
### <a name="enable-logging"></a><span data-ttu-id="b96be-223">Abilitare la registrazione</span><span class="sxs-lookup"><span data-stu-id="b96be-223">Enable Logging</span></span>
<span data-ttu-id="b96be-224">È possibile configurare SDK per generare log di test nella console IDE.</span><span class="sxs-lookup"><span data-stu-id="b96be-224">The SDK can be configured to produce test logs in the IDE console.</span></span>
<span data-ttu-id="b96be-225">Questi log non sono abilitati per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="b96be-225">These logs are not activated by default.</span></span> <span data-ttu-id="b96be-226">Per eseguire una personalizzazione, aggiornare la proprietà `EngagementAgent.Instance.TestLogEnabled` scegliendo uno dei valori disponibili nell'enumerazione `EngagementTestLogLevel`, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="b96be-226">To customize this, update the property `EngagementAgent.Instance.TestLogEnabled` to one of the value available from the `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

