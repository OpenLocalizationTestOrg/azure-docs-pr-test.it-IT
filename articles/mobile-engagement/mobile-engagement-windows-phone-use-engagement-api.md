---
title: aaaHow tooUse hello API Engagement su Windows Phone Silverlight
description: Come tooUse hello API Engagement su Windows Phone Silverlight
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
ms.openlocfilehash: 1e84be95cc910be7f1227b4ae60eb483a1939284
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-windows-phone-silverlight"></a><span data-ttu-id="9b992-103">Come tooUse hello API Engagement su Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="9b992-103">How tooUse hello Engagement API on Windows Phone Silverlight</span></span>
<span data-ttu-id="9b992-104">Questo documento è un componente aggiuntivo toohello [come toointegrate Mobile Engagement nell'app Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="9b992-104">This document is an add-on toohello document [How toointegrate Mobile Engagement in your Windows Phone Silverlight app](mobile-engagement-windows-phone-integrate-engagement.md).</span></span> <span data-ttu-id="9b992-105">Fornisce informazioni approfondite su come toouse hello API Engagement tooreport le statistiche dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9b992-105">It provides in depth details about how toouse hello Engagement API tooreport your application statistics.</span></span>

<span data-ttu-id="9b992-106">Solo Engagement tooreport sessioni dell'applicazione, le attività, arresti anomali del sistema e informazioni tecniche, sarà quindi hello più semplice consiste nel toomake tutti i `PhoneApplicationPage` sottoclassi ereditano hello `EngagementPage` classe.</span><span class="sxs-lookup"><span data-stu-id="9b992-106">If you only want Engagement tooreport your application's sessions, activities, crashes and technical information, then hello simplest way is toomake all your `PhoneApplicationPage` sub-classes inherit from hello `EngagementPage` class.</span></span>

<span data-ttu-id="9b992-107">Se si desidera toodo altre, ad esempio se è necessario tooreport eventi specifici di applicazione, gli errori e i processi o se hai tooreport attività dell'applicazione in modo diverso rispetto a uno implementato in hello hello `EngagementPage` classi, è necessario toouse hello Engagement API.</span><span class="sxs-lookup"><span data-stu-id="9b992-107">If you want toodo more, for example if you need tooreport application specific events, errors and jobs, or if you have tooreport your application's activities in a different way than hello one implemented in hello `EngagementPage` classes, then you need toouse hello Engagement API.</span></span>

<span data-ttu-id="9b992-108">Hello Engagement API viene fornita da hello `EngagementAgent` classe.</span><span class="sxs-lookup"><span data-stu-id="9b992-108">hello Engagement API is provided by hello `EngagementAgent` class.</span></span> <span data-ttu-id="9b992-109">È possibile accedere tramite i metodi toothose `EngagementAgent.Instance`.</span><span class="sxs-lookup"><span data-stu-id="9b992-109">You can access toothose methods through `EngagementAgent.Instance`.</span></span>

<span data-ttu-id="9b992-110">Anche se il modulo hello dell'agente non è stato inizializzato, ogni API toohello chiamata è rinviata e verrà eseguito nuovamente quando l'agente di hello è disponibile.</span><span class="sxs-lookup"><span data-stu-id="9b992-110">Even if hello agent module has not been initialized, each call toohello API is deferred, and will be executed again when hello agent is available.</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="9b992-111">Concetti relativi a Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="9b992-111">Engagement concepts</span></span>
<span data-ttu-id="9b992-112">le seguenti parti Hello perfezionare hello Mobile Engagement concetti per la piattaforma Windows Phone hello.</span><span class="sxs-lookup"><span data-stu-id="9b992-112">hello following parts refine hello Mobile Engagement Concepts for hello Windows Phone platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="9b992-113">`Session` e `Activity`</span><span class="sxs-lookup"><span data-stu-id="9b992-113">`Session` and `Activity`</span></span>
<span data-ttu-id="9b992-114">Un *attività* è generalmente associato a una pagina di un'applicazione hello, che è hello toosay *attività* inizia quando la pagina hello viene visualizzata e si arresta quando viene chiusa la pagina hello: hello caso quando hello Engagement SDK è integrato con hello `EngagementPage` classe.</span><span class="sxs-lookup"><span data-stu-id="9b992-114">An *activity* is usually associated with one page of hello application, that is toosay hello *activity* starts when hello page is displayed and stops when hello page is closed: this is hello case when hello Engagement SDK is integrated by using hello `EngagementPage` class.</span></span>

<span data-ttu-id="9b992-115">Ma *attività* può essere controllato anche manualmente utilizzando l'API di Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="9b992-115">But *activities* can also be controlled manually by using hello Engagement API.</span></span> <span data-ttu-id="9b992-116">In questo modo una determinata pagina toosplit in diversi tooget di parti di sub hello di ulteriori dettagli sull'utilizzo di questa pagina (ad esempio la frequenza con cui tooknown e quanto tempo, all'interno di questa pagina, vengono utilizzate le finestre di dialogo).</span><span class="sxs-lookup"><span data-stu-id="9b992-116">This allows toosplit a given page in several sub parts tooget more details about hello usage of this page (for example tooknown how often and how long dialogs are used inside this page).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="9b992-117">Segnalazione di attività</span><span class="sxs-lookup"><span data-stu-id="9b992-117">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="9b992-118">L'utente inizia una nuova attività</span><span class="sxs-lookup"><span data-stu-id="9b992-118">User starts a new Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="9b992-119">riferimento</span><span class="sxs-lookup"><span data-stu-id="9b992-119">Reference</span></span>
            void StartActivity(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="9b992-120">È necessario toocall `StartActivity()` ogni attività utente hello in fase di modifica.</span><span class="sxs-lookup"><span data-stu-id="9b992-120">You need toocall `StartActivity()` each time hello user activity changes.</span></span> <span data-ttu-id="9b992-121">Hello prima chiamata toothis funzione avvia una nuova sessione utente.</span><span class="sxs-lookup"><span data-stu-id="9b992-121">hello first call toothis function starts a new user session.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9b992-122">Hello SDK automaticamente metodo hello EndActivity quando un'applicazione hello viene chiuso.</span><span class="sxs-lookup"><span data-stu-id="9b992-122">hello SDK automatically call hello EndActivity method when hello application is closed.</span></span> <span data-ttu-id="9b992-123">Di conseguenza, è consigliabile metodo StartActivity di hello toocall ogni volta che l'attività hello di modifica utente hello e chiamare tooNEVER hello metodo EndActivity, dopo la chiamata di questo metodo forza toobe sessione corrente di hello è terminata.</span><span class="sxs-lookup"><span data-stu-id="9b992-123">Thus, it is HIGHLY recommended toocall hello StartActivity method whenever hello activity of hello user change, and tooNEVER call hello EndActivity method, since calling this method forces hello current session toobe ended.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="9b992-124">Esempio</span><span class="sxs-lookup"><span data-stu-id="9b992-124">Example</span></span>
            EngagementAgent.Instance.StartActivity("main", new Dictionary<object, object>() {{"example", "data"}});

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="9b992-125">L'utente termina l'attività corrente</span><span class="sxs-lookup"><span data-stu-id="9b992-125">User ends his current Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="9b992-126">riferimento</span><span class="sxs-lookup"><span data-stu-id="9b992-126">Reference</span></span>
            void EndActivity()

<span data-ttu-id="9b992-127">È necessario toocall `EndActivity()` almeno una volta al termine della sua attività ultimo utente hello.</span><span class="sxs-lookup"><span data-stu-id="9b992-127">You need toocall `EndActivity()` at least once when hello user finishes his last activity.</span></span> <span data-ttu-id="9b992-128">Informa hello scadrà Engagement SDK che utente hello è attualmente inattivo e che la sessione di utente hello necessario toobe chiuso una volta hello timeout della sessione (se si chiama `StartActivity()` prima della scadenza del timeout della sessione hello, sessione hello semplicemente continua).</span><span class="sxs-lookup"><span data-stu-id="9b992-128">This informs hello Engagement SDK that hello user is currently idle, and that hello user session need toobe closed once hello session timeout will expire (if you call `StartActivity()` before hello session timeout expires, hello session is simply continued).</span></span>

#### <a name="example"></a><span data-ttu-id="9b992-129">Esempio</span><span class="sxs-lookup"><span data-stu-id="9b992-129">Example</span></span>
            EngagementAgent.Instance.EndActivity();

## <a name="reporting-jobs"></a><span data-ttu-id="9b992-130">Segnalazione di processi</span><span class="sxs-lookup"><span data-stu-id="9b992-130">Reporting Jobs</span></span>
### <a name="start-a-job"></a><span data-ttu-id="9b992-131">Avviare un processo</span><span class="sxs-lookup"><span data-stu-id="9b992-131">Start a job</span></span>
#### <a name="reference"></a><span data-ttu-id="9b992-132">riferimento</span><span class="sxs-lookup"><span data-stu-id="9b992-132">Reference</span></span>
            void StartJob(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="9b992-133">È possibile utilizzare hello processo tootrack alcune attività in un periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="9b992-133">You can use hello job tootrack certains tasks over a period of time.</span></span>

#### <a name="example"></a><span data-ttu-id="9b992-134">Esempio</span><span class="sxs-lookup"><span data-stu-id="9b992-134">Example</span></span>
            // An upload begins...

            // Set hello extras
            var extras = new Dictionary<object, object>();
            extras.Add("title", "avatar");
            extras.Add("type", "image");

            EngagementAgent.Instance.StartJob("uploadData", extras);

### <a name="end-a-job"></a><span data-ttu-id="9b992-135">Terminare un processo</span><span class="sxs-lookup"><span data-stu-id="9b992-135">End a job</span></span>
#### <a name="reference"></a><span data-ttu-id="9b992-136">riferimento</span><span class="sxs-lookup"><span data-stu-id="9b992-136">Reference</span></span>
            void EndJob(string name)

<span data-ttu-id="9b992-137">Non appena è terminata un'attività rilevata da un processo, è necessario chiamare metodo EndJob hello per questo processo, fornendo il nome di processo hello.</span><span class="sxs-lookup"><span data-stu-id="9b992-137">As soon as a task tracked by a job has been terminated, you should call hello EndJob method for this job, by supplying hello job name.</span></span>

#### <a name="example"></a><span data-ttu-id="9b992-138">Esempio</span><span class="sxs-lookup"><span data-stu-id="9b992-138">Example</span></span>
            // In hello previous section, we started an upload tracking with a job
            // Then, hello upload ends

            EngagementAgent.Instance.EndJob("uploadData");

## <a name="reporting-events"></a><span data-ttu-id="9b992-139">Segnalazione di eventi</span><span class="sxs-lookup"><span data-stu-id="9b992-139">Reporting Events</span></span>
<span data-ttu-id="9b992-140">Esistono tre tipi di eventi:</span><span class="sxs-lookup"><span data-stu-id="9b992-140">There is three types of events :</span></span>

* <span data-ttu-id="9b992-141">Eventi autonomi</span><span class="sxs-lookup"><span data-stu-id="9b992-141">Standalone events</span></span>
* <span data-ttu-id="9b992-142">Eventi di sessione</span><span class="sxs-lookup"><span data-stu-id="9b992-142">Session events</span></span>
* <span data-ttu-id="9b992-143">Eventi di processo</span><span class="sxs-lookup"><span data-stu-id="9b992-143">Job events</span></span>

### <a name="standalone-events"></a><span data-ttu-id="9b992-144">Eventi autonomi</span><span class="sxs-lookup"><span data-stu-id="9b992-144">Standalone Events</span></span>
#### <a name="reference"></a><span data-ttu-id="9b992-145">riferimento</span><span class="sxs-lookup"><span data-stu-id="9b992-145">Reference</span></span>
            void SendEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="9b992-146">Possono verificarsi eventi di autonomo all'esterno di contesto hello di una sessione.</span><span class="sxs-lookup"><span data-stu-id="9b992-146">Standalone events can occur outside of hello context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="9b992-147">Esempio</span><span class="sxs-lookup"><span data-stu-id="9b992-147">Example</span></span>
            EngagementAgent.Instance.SendEvent("event", extra);

### <a name="session-events"></a><span data-ttu-id="9b992-148">Eventi di sessione</span><span class="sxs-lookup"><span data-stu-id="9b992-148">Session events</span></span>
#### <a name="reference"></a><span data-ttu-id="9b992-149">riferimento</span><span class="sxs-lookup"><span data-stu-id="9b992-149">Reference</span></span>
            void SendSessionEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="9b992-150">Gli eventi di sessione sono azioni hello tooreport utilizzati in genere eseguite da un utente durante la sessione.</span><span class="sxs-lookup"><span data-stu-id="9b992-150">Session events are usually used tooreport hello actions performed by a user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="9b992-151">Esempio</span><span class="sxs-lookup"><span data-stu-id="9b992-151">Example</span></span>
<span data-ttu-id="9b992-152">**Senza dati:**</span><span class="sxs-lookup"><span data-stu-id="9b992-152">**Without data :**</span></span>

            EngagementAgent.Instance.SendSessionEvent("sessionEvent");

            // or

            EngagementAgent.Instance.SendSessionEvent("sessionEvent", null);

<span data-ttu-id="9b992-153">**Con dati:**</span><span class="sxs-lookup"><span data-stu-id="9b992-153">**With data :**</span></span>

            Dictionary<object, object> extras = new Dictionary<object,object>();
            extras.Add("name", "data");
            EngagementAgent.Instance.SendSessionEvent("sessionEvent", extras);

### <a name="job-events"></a><span data-ttu-id="9b992-154">Eventi di processo</span><span class="sxs-lookup"><span data-stu-id="9b992-154">Job Events</span></span>
#### <a name="reference"></a><span data-ttu-id="9b992-155">riferimento</span><span class="sxs-lookup"><span data-stu-id="9b992-155">Reference</span></span>
            void SendJobEvent(string eventName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="9b992-156">Eventi relativi al processo sono azioni hello tooreport utilizzati in genere eseguite da un utente durante un processo.</span><span class="sxs-lookup"><span data-stu-id="9b992-156">Job events are usually used tooreport hello actions performed by a user during a Job.</span></span>

#### <a name="example"></a><span data-ttu-id="9b992-157">Esempio</span><span class="sxs-lookup"><span data-stu-id="9b992-157">Example</span></span>
            EngagementAgent.Instance.SendJobEvent("eventName", "jobName", extras);

## <a name="reporting-errors"></a><span data-ttu-id="9b992-158">Segnalazione di errori</span><span class="sxs-lookup"><span data-stu-id="9b992-158">Reporting Errors</span></span>
<span data-ttu-id="9b992-159">Esistono tre tipi di errori:</span><span class="sxs-lookup"><span data-stu-id="9b992-159">There is three types of errors :</span></span>

* <span data-ttu-id="9b992-160">Errori autonomi</span><span class="sxs-lookup"><span data-stu-id="9b992-160">Standalone errors</span></span>
* <span data-ttu-id="9b992-161">Errori di sessione</span><span class="sxs-lookup"><span data-stu-id="9b992-161">Session errors</span></span>
* <span data-ttu-id="9b992-162">Errori di processo</span><span class="sxs-lookup"><span data-stu-id="9b992-162">Job errors</span></span>

### <a name="standalone-errors"></a><span data-ttu-id="9b992-163">Errori autonomi</span><span class="sxs-lookup"><span data-stu-id="9b992-163">Standalone errors</span></span>
#### <a name="reference"></a><span data-ttu-id="9b992-164">riferimento</span><span class="sxs-lookup"><span data-stu-id="9b992-164">Reference</span></span>
            void SendError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="9b992-165">Di fuori di contesto hello di una sessione possono verificarsi errori di toosession contrarie, errori autonomo.</span><span class="sxs-lookup"><span data-stu-id="9b992-165">Contrary toosession errors, standalone errors can occur outside of hello context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="9b992-166">Esempio</span><span class="sxs-lookup"><span data-stu-id="9b992-166">Example</span></span>
            EngagementAgent.Instance.SendError("errorName", extras);

### <a name="session-errors"></a><span data-ttu-id="9b992-167">Errori di sessione</span><span class="sxs-lookup"><span data-stu-id="9b992-167">Session errors</span></span>
#### <a name="reference"></a><span data-ttu-id="9b992-168">riferimento</span><span class="sxs-lookup"><span data-stu-id="9b992-168">Reference</span></span>
            void SendSessionError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="9b992-169">Sessione gli errori in genere utilizzato tooreport hello conseguenze utente hello durante la sessione.</span><span class="sxs-lookup"><span data-stu-id="9b992-169">Session errors are usually used tooreport hello errors impacting hello user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="9b992-170">Esempio</span><span class="sxs-lookup"><span data-stu-id="9b992-170">Example</span></span>
            EngagementAgent.Instance.SendSessionError("errorName", extra);

### <a name="job-errors"></a><span data-ttu-id="9b992-171">Errori di processo</span><span class="sxs-lookup"><span data-stu-id="9b992-171">Job Errors</span></span>
#### <a name="reference"></a><span data-ttu-id="9b992-172">riferimento</span><span class="sxs-lookup"><span data-stu-id="9b992-172">Reference</span></span>
            void SendJobError(string errorName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="9b992-173">Gli errori possono essere correlato tooa esecuzione processo anziché essere correlate toohello sessione utente.</span><span class="sxs-lookup"><span data-stu-id="9b992-173">Errors can be related tooa running job instead of being related toohello current user session.</span></span>

#### <a name="example"></a><span data-ttu-id="9b992-174">Esempio</span><span class="sxs-lookup"><span data-stu-id="9b992-174">Example</span></span>
            EngagementAgent.Instance.SendJobError("errorName", "jobname", extra);

## <a name="reporting-crashes"></a><span data-ttu-id="9b992-175">Segnalazione di arresti anomali</span><span class="sxs-lookup"><span data-stu-id="9b992-175">Reporting Crashes</span></span>
<span data-ttu-id="9b992-176">l'agente Hello fornisce due metodi toodeal con gli arresti anomali.</span><span class="sxs-lookup"><span data-stu-id="9b992-176">hello agent provides two methods toodeal with crashes.</span></span>

### <a name="send-an-exception"></a><span data-ttu-id="9b992-177">Inviare un'eccezione</span><span class="sxs-lookup"><span data-stu-id="9b992-177">Send an exception</span></span>
#### <a name="reference"></a><span data-ttu-id="9b992-178">riferimento</span><span class="sxs-lookup"><span data-stu-id="9b992-178">Reference</span></span>
            void SendCrash(Exception e, bool terminateSession = false)

#### <a name="example"></a><span data-ttu-id="9b992-179">Esempio</span><span class="sxs-lookup"><span data-stu-id="9b992-179">Example</span></span>
<span data-ttu-id="9b992-180">È possibile inviare un'eccezione in qualsiasi momento chiamando:</span><span class="sxs-lookup"><span data-stu-id="9b992-180">You can send an exception at any time by calling :</span></span>

            EngagementAgent.Instance.SendCrash(aCatchedException);

<span data-ttu-id="9b992-181">È inoltre possibile utilizzare una sessione di engagement hello tooterminate parametro facoltativo in hello stesso tempo rispetto all'invio di arresto anomalo di hello.</span><span class="sxs-lookup"><span data-stu-id="9b992-181">You can also use an optional parameter tooterminate hello engagement session at hello same time than sending hello crash.</span></span> <span data-ttu-id="9b992-182">toodo in tal caso, chiamare:</span><span class="sxs-lookup"><span data-stu-id="9b992-182">toodo so, call :</span></span>

            EngagementAgent.Instance.SendCrash(new Exception("example"), terminateSession: true);

<span data-ttu-id="9b992-183">Se a tale scopo, processi e sessione hello verranno chiusa immediatamente dopo l'invio di arresto anomalo di hello.</span><span class="sxs-lookup"><span data-stu-id="9b992-183">If you do that, hello session and jobs will be closed just after sending hello crash.</span></span>

### <a name="send-an-unhandled-exception"></a><span data-ttu-id="9b992-184">Inviare un'eccezione non gestita</span><span class="sxs-lookup"><span data-stu-id="9b992-184">Send an unhandled exception</span></span>
#### <a name="reference"></a><span data-ttu-id="9b992-185">riferimento</span><span class="sxs-lookup"><span data-stu-id="9b992-185">Reference</span></span>
            void SendCrash(ApplicationUnhandledExceptionEventArgs e)

<span data-ttu-id="9b992-186">Engagement fornisce inoltre un metodo toosend non gestite le eccezioni.</span><span class="sxs-lookup"><span data-stu-id="9b992-186">Engagement also provides a method toosend unhandled exceptions.</span></span> <span data-ttu-id="9b992-187">Ciò è particolarmente utile se utilizzato all'interno di gestore dell'evento UnhandledException hello silverlight.</span><span class="sxs-lookup"><span data-stu-id="9b992-187">This is especially useful when used inside hello silverlight UnhandledException event handler.</span></span>

<span data-ttu-id="9b992-188">Questo metodo verrà **sempre** terminare una sessione engagement hello e processi dopo la chiamata.</span><span class="sxs-lookup"><span data-stu-id="9b992-188">This method will **ALWAYS** terminate hello engagement session and jobs after being called.</span></span>

#### <a name="example"></a><span data-ttu-id="9b992-189">Esempio</span><span class="sxs-lookup"><span data-stu-id="9b992-189">Example</span></span>
<span data-ttu-id="9b992-190">È possibile utilizzare tooimplement il proprio gestore UnhandledException (in particolare se è stata disabilitata hello automatica degli arresti anomali delle funzionalità di impegno report).</span><span class="sxs-lookup"><span data-stu-id="9b992-190">You can use it tooimplement your own UnhandledException handler (especially if you have disabled hello automatic crash reporting feature of Engagement).</span></span> <span data-ttu-id="9b992-191">Ad esempio, in hello `Application_UnhandledException` metodo hello `App.xaml.cs` file:</span><span class="sxs-lookup"><span data-stu-id="9b992-191">For example, in hello `Application_UnhandledException` method of hello `App.xaml.cs` file :</span></span>

            // In your App.xaml.cs file

            // Code tooexecute on Unhandled Exceptions
            private void Application_UnhandledException(object sender, ApplicationUnhandledExceptionEventArgs e)
            {
              // your own code

              EngagementAgent.Instance.SendCrash(e);
            }

## <a name="onactivated"></a><span data-ttu-id="9b992-192">OnActivated</span><span class="sxs-lookup"><span data-stu-id="9b992-192">OnActivated</span></span>
### <a name="reference"></a><span data-ttu-id="9b992-193">riferimento</span><span class="sxs-lookup"><span data-stu-id="9b992-193">Reference</span></span>
            void OnActivated(ActivatedEventArgs e)

<span data-ttu-id="9b992-194">Quando l'utente hello si sposta in avanti, lontano da un'applicazione, dopo che viene generato l'evento Deactivated hello, sistema operativo hello tenterà un'applicazione hello tooput a uno stato inattivo.</span><span class="sxs-lookup"><span data-stu-id="9b992-194">When hello user navigates forward, away from an application, after hello Deactivated event is raised, hello operating system will attempt tooput hello application into a dormant state.</span></span> <span data-ttu-id="9b992-195">Quindi, un'applicazione hello è la rimozione definitiva.</span><span class="sxs-lookup"><span data-stu-id="9b992-195">Then, hello application is Tombstoning.</span></span> <span data-ttu-id="9b992-196">In questo processo viene terminata un'applicazione, ma alcuni dati sullo stato di hello di un'applicazione hello e singole pagine di hello all'interno di un'applicazione hello viene mantenuti.</span><span class="sxs-lookup"><span data-stu-id="9b992-196">In this process an application is terminated but some data about hello state of hello application and hello individual pages within hello application is preserved.</span></span>

<span data-ttu-id="9b992-197">Si dispone di tooinsert `EngagementAgent.Instance.OnActivated(e)` in hello `Application_Activated` metodo hello tooreset di file App.xaml.cs hello Engagement Agent quando un'applicazione hello è stato eliminato definitivamente.</span><span class="sxs-lookup"><span data-stu-id="9b992-197">You have tooinsert `EngagementAgent.Instance.OnActivated(e)` in hello `Application_Activated` method from hello App.xaml.cs file tooreset hello Engagement Agent when hello application has been Tombstoned.</span></span>

### <a name="example"></a><span data-ttu-id="9b992-198">Esempio</span><span class="sxs-lookup"><span data-stu-id="9b992-198">Example</span></span>
            // Inside your App.xaml.cs file

            // Code tooexecute when hello application is activated (brought tooforeground)
            // This code will not execute when hello application is first launched
            private void Application_Activated(object sender, ActivatedEventArgs e)
            {
              EngagementAgent.Instance.OnActivated(e);
            }

## <a name="device-id"></a><span data-ttu-id="9b992-199">Id dispositivo</span><span class="sxs-lookup"><span data-stu-id="9b992-199">Device Id</span></span>
            String GetDeviceId()

<span data-ttu-id="9b992-200">È possibile ottenere l'id dispositivo di engagement hello chiamando questo metodo.</span><span class="sxs-lookup"><span data-stu-id="9b992-200">You can get hello engagement device id by calling this method.</span></span>

## <a name="extras-parameters"></a><span data-ttu-id="9b992-201">Parametri aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="9b992-201">Extras parameters</span></span>
<span data-ttu-id="9b992-202">Dati arbitrari possono essere collegati tooan evento, un errore, un'attività o un processo.</span><span class="sxs-lookup"><span data-stu-id="9b992-202">Arbitrary data can be attached tooan event, an error, an activity or a job.</span></span> <span data-ttu-id="9b992-203">Tali dati possono essere strutturati utilizzando un dizionario.</span><span class="sxs-lookup"><span data-stu-id="9b992-203">These data can be structured using a dictionary.</span></span> <span data-ttu-id="9b992-204">Chiavi e valori possono essere di qualsiasi tipo.</span><span class="sxs-lookup"><span data-stu-id="9b992-204">Keys and values can be of any type.</span></span>

<span data-ttu-id="9b992-205">Se si desidera tooinsert un proprio tipo di funzionalità aggiuntive è tooadd un contratto dati per questo tipo, vengono serializzati i dati extra.</span><span class="sxs-lookup"><span data-stu-id="9b992-205">Extras data are serialized so if you want tooinsert your own type in extras you have tooadd a data contract for this type.</span></span>

### <a name="example"></a><span data-ttu-id="9b992-206">Esempio</span><span class="sxs-lookup"><span data-stu-id="9b992-206">Example</span></span>
<span data-ttu-id="9b992-207">Si crea una nuova classe "Person".</span><span class="sxs-lookup"><span data-stu-id="9b992-207">We create a new class "Person".</span></span>

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

<span data-ttu-id="9b992-208">Quindi, si aggiungerà un `Person` tooan istanza aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="9b992-208">Then, we will add a `Person` instance tooan extra.</span></span>

            Person person = new Person("Engagement Haddock", 51);
            var extras = new Dictionary<object, object>();
            extras.Add("people", person);

            EngagementAgent.Instance.SendEvent("Event", extras);

> [!WARNING]
> <span data-ttu-id="9b992-209">Se si inseriscono altri tipi di oggetti, assicurarsi che il relativo metodo ToString () è implementato tooreturn una stringa leggibile.</span><span class="sxs-lookup"><span data-stu-id="9b992-209">If you put other types of objects, make sure their ToString() method is implemented tooreturn a human readable string.</span></span>
> 
> 

### <a name="limits"></a><span data-ttu-id="9b992-210">Limiti</span><span class="sxs-lookup"><span data-stu-id="9b992-210">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="9b992-211">Chiavi</span><span class="sxs-lookup"><span data-stu-id="9b992-211">Keys</span></span>
<span data-ttu-id="9b992-212">Ogni chiave nell'oggetto hello deve corrispondere hello espressione regolare seguente:</span><span class="sxs-lookup"><span data-stu-id="9b992-212">Each key in hello object must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="9b992-213">Questo significa che le chiavi devono iniziare con almeno una lettera, seguita da lettere, cifre o caratteri di sottolineatura (\_).</span><span class="sxs-lookup"><span data-stu-id="9b992-213">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="9b992-214">Dimensione</span><span class="sxs-lookup"><span data-stu-id="9b992-214">Size</span></span>
<span data-ttu-id="9b992-215">Funzionalità aggiuntive sono troppo limitate**1024** caratteri per ogni chiamata.</span><span class="sxs-lookup"><span data-stu-id="9b992-215">Extras are limited too**1024** characters per call.</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="9b992-216">Segnalazione di informazioni sull'applicazione</span><span class="sxs-lookup"><span data-stu-id="9b992-216">Reporting Application Information</span></span>
### <a name="reference"></a><span data-ttu-id="9b992-217">riferimento</span><span class="sxs-lookup"><span data-stu-id="9b992-217">Reference</span></span>
            void SendAppInfo(Dictionary<object, object> appInfos)

<span data-ttu-id="9b992-218">Manualmente, è possibile segnalare informazioni (o qualsiasi altra informazione di specifici dell'applicazione) usando hello SendAppInfo() funzione di rilevamento.</span><span class="sxs-lookup"><span data-stu-id="9b992-218">You can manually report tracking information (or any other application specific information) using hello SendAppInfo() function.</span></span>

<span data-ttu-id="9b992-219">Si noti che queste informazioni possono essere inviate in modo incrementale: solo hello valore più recente per una determinata chiave verrà conservati per un determinato dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9b992-219">Note that these information can be sent incrementally: only hello latest value for a given key will be kept for a given device.</span></span> <span data-ttu-id="9b992-220">Ad esempio funzionalità aggiuntive di evento, utilizzare un dizionario\<oggetto,\> tooattach informazioni.</span><span class="sxs-lookup"><span data-stu-id="9b992-220">Like event extras, use a Dictionary\<object, object\> tooattach informations.</span></span>

### <a name="example"></a><span data-ttu-id="9b992-221">Esempio</span><span class="sxs-lookup"><span data-stu-id="9b992-221">Example</span></span>
            Dictionary<object, object> appInfo = new Dictionary<object, object>()
            {
               {"subscription", "2013-12-07"},
               {"premium", "true"}
            };

            EngagementAgent.Instance.SendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="9b992-222">Limiti</span><span class="sxs-lookup"><span data-stu-id="9b992-222">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="9b992-223">Chiavi</span><span class="sxs-lookup"><span data-stu-id="9b992-223">Keys</span></span>
<span data-ttu-id="9b992-224">Ogni chiave nell'oggetto hello deve corrispondere hello espressione regolare seguente:</span><span class="sxs-lookup"><span data-stu-id="9b992-224">Each key in hello object must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="9b992-225">Questo significa che le chiavi devono iniziare con almeno una lettera, seguita da lettere, cifre o caratteri di sottolineatura (\_).</span><span class="sxs-lookup"><span data-stu-id="9b992-225">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="9b992-226">Dimensione</span><span class="sxs-lookup"><span data-stu-id="9b992-226">Size</span></span>
<span data-ttu-id="9b992-227">Informazioni sull'applicazione sono troppo limitati**1024** caratteri per ogni chiamata.</span><span class="sxs-lookup"><span data-stu-id="9b992-227">Application information are limited too**1024** characters per call.</span></span>

<span data-ttu-id="9b992-228">In hello esempio precedente, hello JSON inviato server toohello è 44 caratteri:</span><span class="sxs-lookup"><span data-stu-id="9b992-228">In hello previous example, hello JSON sent toohello server is 44 characters long:</span></span>

            {"subscription":"2013-12-07","premium":"true"}

## <a name="logging"></a><span data-ttu-id="9b992-229">Registrazione</span><span class="sxs-lookup"><span data-stu-id="9b992-229">Logging</span></span>
### <a name="enable-logging"></a><span data-ttu-id="9b992-230">Abilitare la registrazione</span><span class="sxs-lookup"><span data-stu-id="9b992-230">Enable Logging</span></span>
<span data-ttu-id="9b992-231">è possibile i log dei test tooproduce configurato nella console IDE hello Hello SDK.</span><span class="sxs-lookup"><span data-stu-id="9b992-231">hello SDK can be configured tooproduce test logs in hello IDE console.</span></span>
<span data-ttu-id="9b992-232">Questi log non sono abilitati per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="9b992-232">These logs are not activated by default.</span></span> <span data-ttu-id="9b992-233">toocustomize, questa proprietà hello aggiornamento `EngagementAgent.Instance.TestLogEnabled` tooone del valore di hello disponibile hello `EngagementTestLogLevel` enumerazione, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="9b992-233">toocustomize this, update hello property `EngagementAgent.Instance.TestLogEnabled` tooone of hello value available from hello `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();
