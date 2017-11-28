---
title: aaaHow tooUse hello Engagement API in universali di Windows
description: Come tooUse hello Engagement API in universali di Windows
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
ms.openlocfilehash: 0256b839c28e4ef6c530106408d744038fa711ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-windows-universal"></a><span data-ttu-id="41107-103">Come tooUse hello Engagement API in universali di Windows</span><span class="sxs-lookup"><span data-stu-id="41107-103">How tooUse hello Engagement API on Windows Universal</span></span>
<span data-ttu-id="41107-104">Questo documento è un componente aggiuntivo toohello [come tooIntegrate Engagement in Universal Windows](mobile-engagement-windows-store-integrate-engagement.md): fornisce informazioni approfondite su come toouse hello API Engagement tooreport le statistiche dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="41107-104">This document is an add-on toohello document [How tooIntegrate Engagement on Windows Universal](mobile-engagement-windows-store-integrate-engagement.md): it provides in depth details about how toouse hello Engagement API tooreport your application statistics.</span></span>

<span data-ttu-id="41107-105">Tenere presente che se si vuole solo Engagement tooreport sessioni dell'applicazione, le attività, arresti anomali del sistema e informazioni tecniche, quindi hello semplice toomake tutti i `Page` sottoclassi ereditano hello `EngagementPage` classe.</span><span class="sxs-lookup"><span data-stu-id="41107-105">Keep in mind that if you only want Engagement tooreport your application's sessions, activities, crashes and technical information, then hello simplest way is toomake all your `Page` sub-classes inherit from hello `EngagementPage` class.</span></span>

<span data-ttu-id="41107-106">Se si desidera toodo altre, ad esempio se è necessario tooreport eventi specifici di applicazione, gli errori e i processi o se hai tooreport attività dell'applicazione in modo diverso rispetto a uno implementato in hello hello `EngagementPage` classi, è necessario toouse hello Engagement API.</span><span class="sxs-lookup"><span data-stu-id="41107-106">If you want toodo more, for example if you need tooreport application specific events, errors and jobs, or if you have tooreport your application's activities in a different way than hello one implemented in hello `EngagementPage` classes, then you need toouse hello Engagement API.</span></span>

<span data-ttu-id="41107-107">Hello Engagement API viene fornita da hello `EngagementAgent` classe.</span><span class="sxs-lookup"><span data-stu-id="41107-107">hello Engagement API is provided by hello `EngagementAgent` class.</span></span> <span data-ttu-id="41107-108">È possibile accedere tramite i metodi toothose `EngagementAgent.Instance`.</span><span class="sxs-lookup"><span data-stu-id="41107-108">You can access toothose methods through `EngagementAgent.Instance`.</span></span>

<span data-ttu-id="41107-109">Anche se il modulo hello dell'agente non è stato inizializzato, ogni API toohello chiamata è rinviata e verrà eseguito nuovamente quando l'agente di hello è disponibile.</span><span class="sxs-lookup"><span data-stu-id="41107-109">Even if hello agent module has not been initialized, each call toohello API is deferred, and will be executed again when hello agent is available.</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="41107-110">Concetti relativi a Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="41107-110">Engagement concepts</span></span>
<span data-ttu-id="41107-111">parti seguenti Hello perfezionare hello comune [concetti Engagement Mobile](mobile-engagement-concepts.md) per piattaforma universale di Windows hello.</span><span class="sxs-lookup"><span data-stu-id="41107-111">hello following parts refine hello common [Mobile Engagement Concepts](mobile-engagement-concepts.md) for hello Windows Universal platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="41107-112">`Session` e `Activity`</span><span class="sxs-lookup"><span data-stu-id="41107-112">`Session` and `Activity`</span></span>
<span data-ttu-id="41107-113">Un *attività* è generalmente associato a una pagina di un'applicazione hello, che è hello toosay *attività* inizia quando la pagina hello viene visualizzata e si arresta quando viene chiusa la pagina hello: hello caso quando hello Engagement SDK è integrato con hello `EngagementPage` classe.</span><span class="sxs-lookup"><span data-stu-id="41107-113">An *activity* is usually associated with one page of hello application, that is toosay hello *activity* starts when hello page is displayed and stops when hello page is closed: this is hello case when hello Engagement SDK is integrated by using hello `EngagementPage` class.</span></span>

<span data-ttu-id="41107-114">Ma *attività* può essere controllato anche manualmente utilizzando l'API di Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="41107-114">But *activities* can also be controlled manually by using hello Engagement API.</span></span> <span data-ttu-id="41107-115">In questo modo toosplit una determinata pagina in diversi sottotipi parti tooget ulteriori dettagli sull'utilizzo di hello della pagina (ad esempio la frequenza con cui tooknow e per quanto tempo le finestre di dialogo vengono utilizzati all'interno di questa pagina).</span><span class="sxs-lookup"><span data-stu-id="41107-115">This allows you toosplit a given page in several sub parts tooget more details about hello usage of this page (for example tooknow how often and how long dialogs are used inside this page).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="41107-116">Segnalazione di attività</span><span class="sxs-lookup"><span data-stu-id="41107-116">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="41107-117">L'utente inizia una nuova attività</span><span class="sxs-lookup"><span data-stu-id="41107-117">User starts a new Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="41107-118">riferimento</span><span class="sxs-lookup"><span data-stu-id="41107-118">Reference</span></span>
            void StartActivity(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="41107-119">È necessario toocall `StartActivity()` ogni attività utente hello in fase di modifica.</span><span class="sxs-lookup"><span data-stu-id="41107-119">You need toocall `StartActivity()` each time hello user activity changes.</span></span> <span data-ttu-id="41107-120">Hello prima chiamata toothis funzione avvia una nuova sessione utente.</span><span class="sxs-lookup"><span data-stu-id="41107-120">hello first call toothis function starts a new user session.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="41107-121">Hello SDK chiama automaticamente il metodo EndActivity hello quando un'applicazione hello viene chiuso.</span><span class="sxs-lookup"><span data-stu-id="41107-121">hello SDK automatically calls hello EndActivity method when hello application is closed.</span></span> <span data-ttu-id="41107-122">Di conseguenza, è consigliabile metodo StartActivity di hello toocall ogni volta che cambia attività hello dell'utente di hello e chiamata tooNEVER hello metodo EndActivity, dopo la chiamata di questo metodo forza toobe sessione corrente di hello è terminata.</span><span class="sxs-lookup"><span data-stu-id="41107-122">Thus, it is HIGHLY recommended toocall hello StartActivity method whenever hello activity of hello user changes, and tooNEVER call hello EndActivity method, since calling this method forces hello current session toobe ended.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="41107-123">Esempio</span><span class="sxs-lookup"><span data-stu-id="41107-123">Example</span></span>
            EngagementAgent.Instance.StartActivity("main", new Dictionary<object, object>() {{"example", "data"}});

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="41107-124">L'utente termina l'attività corrente</span><span class="sxs-lookup"><span data-stu-id="41107-124">User ends his current Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="41107-125">riferimento</span><span class="sxs-lookup"><span data-stu-id="41107-125">Reference</span></span>
            void EndActivity()

<span data-ttu-id="41107-126">Questo Termina attività hello e sessione hello.</span><span class="sxs-lookup"><span data-stu-id="41107-126">This ends hello activity and hello session.</span></span> <span data-ttu-id="41107-127">Chiamare questo metodo solo se si è perfettamente consapevoli delle conseguenze.</span><span class="sxs-lookup"><span data-stu-id="41107-127">You should not call this method unless you really know what you're doing.</span></span>

#### <a name="example"></a><span data-ttu-id="41107-128">Esempio</span><span class="sxs-lookup"><span data-stu-id="41107-128">Example</span></span>
            EngagementAgent.Instance.EndActivity();

## <a name="reporting-jobs"></a><span data-ttu-id="41107-129">Segnalazione di processi</span><span class="sxs-lookup"><span data-stu-id="41107-129">Reporting Jobs</span></span>
### <a name="start-a-job"></a><span data-ttu-id="41107-130">Avviare un processo</span><span class="sxs-lookup"><span data-stu-id="41107-130">Start a job</span></span>
#### <a name="reference"></a><span data-ttu-id="41107-131">riferimento</span><span class="sxs-lookup"><span data-stu-id="41107-131">Reference</span></span>
            void StartJob(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="41107-132">È possibile utilizzare hello processo tootrack alcune attività in un periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="41107-132">You can use hello job tootrack certains tasks over a period of time.</span></span>

#### <a name="example"></a><span data-ttu-id="41107-133">Esempio</span><span class="sxs-lookup"><span data-stu-id="41107-133">Example</span></span>
            // An upload begins...

            // Set hello extras
            var extras = new Dictionary<object, object>();
            extras.Add("title", "avatar");
            extras.Add("type", "image");

            EngagementAgent.Instance.StartJob("uploadData", extras);

### <a name="end-a-job"></a><span data-ttu-id="41107-134">Terminare un processo</span><span class="sxs-lookup"><span data-stu-id="41107-134">End a job</span></span>
#### <a name="reference"></a><span data-ttu-id="41107-135">riferimento</span><span class="sxs-lookup"><span data-stu-id="41107-135">Reference</span></span>
            void EndJob(string name)

<span data-ttu-id="41107-136">Non appena è terminata un'attività rilevata da un processo, è necessario chiamare metodo EndJob hello per questo processo, fornendo il nome di processo hello.</span><span class="sxs-lookup"><span data-stu-id="41107-136">As soon as a task tracked by a job has been terminated, you should call hello EndJob method for this job, by supplying hello job name.</span></span>

#### <a name="example"></a><span data-ttu-id="41107-137">Esempio</span><span class="sxs-lookup"><span data-stu-id="41107-137">Example</span></span>
            // In hello previous section, we started an upload tracking with a job
            // Then, hello upload ends

            EngagementAgent.Instance.EndJob("uploadData");

## <a name="reporting-events"></a><span data-ttu-id="41107-138">Segnalazione di eventi</span><span class="sxs-lookup"><span data-stu-id="41107-138">Reporting Events</span></span>
<span data-ttu-id="41107-139">Esistono tre tipi di eventi:</span><span class="sxs-lookup"><span data-stu-id="41107-139">There is three types of events :</span></span>

* <span data-ttu-id="41107-140">Eventi autonomi</span><span class="sxs-lookup"><span data-stu-id="41107-140">Standalone events</span></span>
* <span data-ttu-id="41107-141">Eventi di sessione</span><span class="sxs-lookup"><span data-stu-id="41107-141">Session events</span></span>
* <span data-ttu-id="41107-142">Eventi di processo</span><span class="sxs-lookup"><span data-stu-id="41107-142">Job events</span></span>

### <a name="standalone-events"></a><span data-ttu-id="41107-143">Eventi autonomi</span><span class="sxs-lookup"><span data-stu-id="41107-143">Standalone Events</span></span>
#### <a name="reference"></a><span data-ttu-id="41107-144">riferimento</span><span class="sxs-lookup"><span data-stu-id="41107-144">Reference</span></span>
            void SendEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="41107-145">Possono verificarsi eventi di autonomo all'esterno di contesto hello di una sessione.</span><span class="sxs-lookup"><span data-stu-id="41107-145">Standalone events can occur outside of hello context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="41107-146">Esempio</span><span class="sxs-lookup"><span data-stu-id="41107-146">Example</span></span>
            EngagementAgent.Instance.SendEvent("event", extra);

### <a name="session-events"></a><span data-ttu-id="41107-147">Eventi di sessione</span><span class="sxs-lookup"><span data-stu-id="41107-147">Session events</span></span>
#### <a name="reference"></a><span data-ttu-id="41107-148">riferimento</span><span class="sxs-lookup"><span data-stu-id="41107-148">Reference</span></span>
            void SendSessionEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="41107-149">Gli eventi di sessione sono azioni hello tooreport utilizzati in genere eseguite da un utente durante la sessione.</span><span class="sxs-lookup"><span data-stu-id="41107-149">Session events are usually used tooreport hello actions performed by a user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="41107-150">Esempio</span><span class="sxs-lookup"><span data-stu-id="41107-150">Example</span></span>
<span data-ttu-id="41107-151">**Senza dati:**</span><span class="sxs-lookup"><span data-stu-id="41107-151">**Without data :**</span></span>

            EngagementAgent.Instance.SendSessionEvent("sessionEvent");

            // or

            EngagementAgent.Instance.SendSessionEvent("sessionEvent", null);

<span data-ttu-id="41107-152">**Con dati:**</span><span class="sxs-lookup"><span data-stu-id="41107-152">**With data :**</span></span>

            Dictionary<object, object> extras = new Dictionary<object,object>();
            extras.Add("name", "data");
            EngagementAgent.Instance.SendSessionEvent("sessionEvent", extras);

### <a name="job-events"></a><span data-ttu-id="41107-153">Eventi di processo</span><span class="sxs-lookup"><span data-stu-id="41107-153">Job Events</span></span>
#### <a name="reference"></a><span data-ttu-id="41107-154">riferimento</span><span class="sxs-lookup"><span data-stu-id="41107-154">Reference</span></span>
            void SendJobEvent(string eventName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="41107-155">Eventi relativi al processo sono azioni hello tooreport utilizzati in genere eseguite da un utente durante un processo.</span><span class="sxs-lookup"><span data-stu-id="41107-155">Job events are usually used tooreport hello actions performed by a user during a Job.</span></span>

#### <a name="example"></a><span data-ttu-id="41107-156">Esempio</span><span class="sxs-lookup"><span data-stu-id="41107-156">Example</span></span>
            EngagementAgent.Instance.SendJobEvent("eventName", "jobName", extras);

## <a name="reporting-errors"></a><span data-ttu-id="41107-157">Segnalazione di errori</span><span class="sxs-lookup"><span data-stu-id="41107-157">Reporting Errors</span></span>
<span data-ttu-id="41107-158">Esistono tre tipi di errore:</span><span class="sxs-lookup"><span data-stu-id="41107-158">There are three types of errors :</span></span>

* <span data-ttu-id="41107-159">Errori autonomi</span><span class="sxs-lookup"><span data-stu-id="41107-159">Standalone errors</span></span>
* <span data-ttu-id="41107-160">Errori di sessione</span><span class="sxs-lookup"><span data-stu-id="41107-160">Session errors</span></span>
* <span data-ttu-id="41107-161">Errori di processo</span><span class="sxs-lookup"><span data-stu-id="41107-161">Job errors</span></span>

### <a name="standalone-errors"></a><span data-ttu-id="41107-162">Errori autonomi</span><span class="sxs-lookup"><span data-stu-id="41107-162">Standalone errors</span></span>
#### <a name="reference"></a><span data-ttu-id="41107-163">riferimento</span><span class="sxs-lookup"><span data-stu-id="41107-163">Reference</span></span>
            void SendError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="41107-164">Di fuori di contesto hello di una sessione possono verificarsi errori di toosession contrarie, errori autonomo.</span><span class="sxs-lookup"><span data-stu-id="41107-164">Contrary toosession errors, standalone errors can occur outside of hello context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="41107-165">Esempio</span><span class="sxs-lookup"><span data-stu-id="41107-165">Example</span></span>
            EngagementAgent.Instance.SendError("errorName", extras);

### <a name="session-errors"></a><span data-ttu-id="41107-166">Errori di sessione</span><span class="sxs-lookup"><span data-stu-id="41107-166">Session errors</span></span>
#### <a name="reference"></a><span data-ttu-id="41107-167">riferimento</span><span class="sxs-lookup"><span data-stu-id="41107-167">Reference</span></span>
            void SendSessionError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="41107-168">Sessione gli errori in genere utilizzato tooreport hello conseguenze utente hello durante la sessione.</span><span class="sxs-lookup"><span data-stu-id="41107-168">Session errors are usually used tooreport hello errors impacting hello user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="41107-169">Esempio</span><span class="sxs-lookup"><span data-stu-id="41107-169">Example</span></span>
            EngagementAgent.Instance.SendSessionError("errorName", extra);

### <a name="job-errors"></a><span data-ttu-id="41107-170">Errori di processo</span><span class="sxs-lookup"><span data-stu-id="41107-170">Job Errors</span></span>
#### <a name="reference"></a><span data-ttu-id="41107-171">riferimento</span><span class="sxs-lookup"><span data-stu-id="41107-171">Reference</span></span>
            void SendJobError(string errorName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="41107-172">Gli errori possono essere correlato tooa esecuzione processo anziché essere correlate toohello sessione utente.</span><span class="sxs-lookup"><span data-stu-id="41107-172">Errors can be related tooa running job instead of being related toohello current user session.</span></span>

#### <a name="example"></a><span data-ttu-id="41107-173">Esempio</span><span class="sxs-lookup"><span data-stu-id="41107-173">Example</span></span>
            EngagementAgent.Instance.SendJobError("errorName", "jobname", extra);

## <a name="reporting-crashes"></a><span data-ttu-id="41107-174">Segnalazione di arresti anomali</span><span class="sxs-lookup"><span data-stu-id="41107-174">Reporting Crashes</span></span>
<span data-ttu-id="41107-175">l'agente Hello fornisce due metodi toodeal con gli arresti anomali.</span><span class="sxs-lookup"><span data-stu-id="41107-175">hello agent provides two methods toodeal with crashes.</span></span>

### <a name="send-an-exception"></a><span data-ttu-id="41107-176">Inviare un'eccezione</span><span class="sxs-lookup"><span data-stu-id="41107-176">Send an exception</span></span>
#### <a name="reference"></a><span data-ttu-id="41107-177">riferimento</span><span class="sxs-lookup"><span data-stu-id="41107-177">Reference</span></span>
            void SendCrash(Exception e, bool terminateSession = false)

#### <a name="example"></a><span data-ttu-id="41107-178">Esempio</span><span class="sxs-lookup"><span data-stu-id="41107-178">Example</span></span>
<span data-ttu-id="41107-179">È possibile inviare un'eccezione in qualsiasi momento chiamando:</span><span class="sxs-lookup"><span data-stu-id="41107-179">You can send an exception at any time by calling :</span></span>

            EngagementAgent.Instance.SendCrash(aCatchedException);

<span data-ttu-id="41107-180">È inoltre possibile utilizzare una sessione di engagement hello tooterminate parametro facoltativo in hello stesso tempo rispetto all'invio di arresto anomalo di hello.</span><span class="sxs-lookup"><span data-stu-id="41107-180">You can also use an optional parameter tooterminate hello engagement session at hello same time than sending hello crash.</span></span> <span data-ttu-id="41107-181">toodo in tal caso, chiamare:</span><span class="sxs-lookup"><span data-stu-id="41107-181">toodo so, call :</span></span>

            EngagementAgent.Instance.SendCrash(new Exception("example"), terminateSession: true);

<span data-ttu-id="41107-182">Se a tale scopo, processi e sessione hello verranno chiusa immediatamente dopo l'invio di arresto anomalo di hello.</span><span class="sxs-lookup"><span data-stu-id="41107-182">If you do that, hello session and jobs will be closed just after sending hello crash.</span></span>

### <a name="send-an-unhandled-exception"></a><span data-ttu-id="41107-183">Inviare un'eccezione non gestita</span><span class="sxs-lookup"><span data-stu-id="41107-183">Send an unhandled exception</span></span>
#### <a name="reference"></a><span data-ttu-id="41107-184">riferimento</span><span class="sxs-lookup"><span data-stu-id="41107-184">Reference</span></span>
            void SendCrash(Exception e)

<span data-ttu-id="41107-185">Engagement fornisce inoltre un metodo toosend non gestite le eccezioni nel caso di **DISABILITATO** Engagement automatico **arresto anomalo del sistema** reporting.</span><span class="sxs-lookup"><span data-stu-id="41107-185">Engagement also provides a method toosend unhandled exceptions if you have **DISABLED** Engagement automatic **crash** reporting.</span></span> <span data-ttu-id="41107-186">Ciò è particolarmente utile se utilizzato all'interno di gestore dell'evento UnhandledException applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="41107-186">This is especially useful when used inside hello application UnhandledException event handler.</span></span>

<span data-ttu-id="41107-187">Questo metodo verrà **sempre** terminare una sessione engagement hello e processi dopo la chiamata.</span><span class="sxs-lookup"><span data-stu-id="41107-187">This method will **ALWAYS** terminate hello engagement session and jobs after being called.</span></span>

#### <a name="example"></a><span data-ttu-id="41107-188">Esempio</span><span class="sxs-lookup"><span data-stu-id="41107-188">Example</span></span>
<span data-ttu-id="41107-189">È possibile utilizzare tooimplement il proprio gestore UnhandledExceptionEventArgs.</span><span class="sxs-lookup"><span data-stu-id="41107-189">You can use it tooimplement your own UnhandledExceptionEventArgs handler.</span></span> <span data-ttu-id="41107-190">Ad esempio, aggiungere hello `Current_UnhandledException` metodo hello `App.xaml.cs` file:</span><span class="sxs-lookup"><span data-stu-id="41107-190">For example, add hello `Current_UnhandledException` method of hello `App.xaml.cs` file :</span></span>

            // In your App.xaml.cs file

            // Code tooexecute on Unhandled Exceptions
            void Current_UnhandledException(object sender, UnhandledExceptionEventArgs e)
            {
               EngagementAgent.Instance.SendCrash(e.Exception,false);
            }

<span data-ttu-id="41107-191">In App.xaml.cs in "Public App(){}" aggiungere:</span><span class="sxs-lookup"><span data-stu-id="41107-191">In App.xaml.cs in "Public App(){}" add:</span></span>

            Application.Current.UnhandledException += Current_UnhandledException;

## <a name="device-id"></a><span data-ttu-id="41107-192">Id dispositivo</span><span class="sxs-lookup"><span data-stu-id="41107-192">Device Id</span></span>
            String EngagementAgent.Instance.GetDeviceId()

<span data-ttu-id="41107-193">È possibile ottenere l'id dispositivo di engagement hello chiamando questo metodo.</span><span class="sxs-lookup"><span data-stu-id="41107-193">You can get hello engagement device id by calling this method.</span></span>

## <a name="extras-parameters"></a><span data-ttu-id="41107-194">Parametri aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="41107-194">Extras parameters</span></span>
<span data-ttu-id="41107-195">Dati arbitrari possono essere collegati tooan evento, un errore, un'attività o un processo.</span><span class="sxs-lookup"><span data-stu-id="41107-195">Arbitrary data can be attached tooan event, an error, an activity or a job.</span></span> <span data-ttu-id="41107-196">Tali dati possono essere strutturati utilizzando un dizionario.</span><span class="sxs-lookup"><span data-stu-id="41107-196">These data can be structured using a dictionary.</span></span> <span data-ttu-id="41107-197">Chiavi e valori possono essere di qualsiasi tipo.</span><span class="sxs-lookup"><span data-stu-id="41107-197">Keys and values can be of any type.</span></span>

<span data-ttu-id="41107-198">Se si desidera tooinsert un proprio tipo di funzionalità aggiuntive è tooadd un contratto dati per questo tipo, vengono serializzati i dati extra.</span><span class="sxs-lookup"><span data-stu-id="41107-198">Extras data are serialized so if you want tooinsert your own type in extras you have tooadd a data contract for this type.</span></span>

### <a name="example"></a><span data-ttu-id="41107-199">Esempio</span><span class="sxs-lookup"><span data-stu-id="41107-199">Example</span></span>
<span data-ttu-id="41107-200">Si crea una nuova classe "Person".</span><span class="sxs-lookup"><span data-stu-id="41107-200">We create a new class "Person".</span></span>

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

<span data-ttu-id="41107-201">Quindi, si aggiungerà un `Person` tooan istanza aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="41107-201">Then, we will add a `Person` instance tooan extra.</span></span>

            Person person = new Person("Engagement Haddock", 51);
            var extras = new Dictionary<object, object>();
            extras.Add("people", person);

            EngagementAgent.Instance.SendEvent("Event", extras);

> [!WARNING]
> <span data-ttu-id="41107-202">Se si inseriscono altri tipi di oggetti, assicurarsi che il relativo metodo ToString () è implementato tooreturn una stringa leggibile.</span><span class="sxs-lookup"><span data-stu-id="41107-202">If you put other types of objects, make sure their ToString() method is implemented tooreturn a human readable string.</span></span>
> 
> 

### <a name="limits"></a><span data-ttu-id="41107-203">Limiti</span><span class="sxs-lookup"><span data-stu-id="41107-203">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="41107-204">Chiavi</span><span class="sxs-lookup"><span data-stu-id="41107-204">Keys</span></span>
<span data-ttu-id="41107-205">Ogni chiave nell'oggetto hello deve corrispondere hello espressione regolare seguente:</span><span class="sxs-lookup"><span data-stu-id="41107-205">Each key in hello object must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="41107-206">Questo significa che le chiavi devono iniziare con almeno una lettera, seguita da lettere, cifre o caratteri di sottolineatura (\_).</span><span class="sxs-lookup"><span data-stu-id="41107-206">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="41107-207">Dimensione</span><span class="sxs-lookup"><span data-stu-id="41107-207">Size</span></span>
<span data-ttu-id="41107-208">Funzionalità aggiuntive sono troppo limitate**1024** caratteri per ogni chiamata.</span><span class="sxs-lookup"><span data-stu-id="41107-208">Extras are limited too**1024** characters per call.</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="41107-209">Segnalazione di informazioni sull'applicazione</span><span class="sxs-lookup"><span data-stu-id="41107-209">Reporting Application Information</span></span>
### <a name="reference"></a><span data-ttu-id="41107-210">riferimento</span><span class="sxs-lookup"><span data-stu-id="41107-210">Reference</span></span>
            void SendAppInfo(Dictionary<object, object> appInfos)

<span data-ttu-id="41107-211">Manualmente, è possibile segnalare informazioni (o qualsiasi altra informazione di specifici dell'applicazione) usando hello SendAppInfo() funzione di rilevamento.</span><span class="sxs-lookup"><span data-stu-id="41107-211">You can manually report tracking information (or any other application specific information) using hello SendAppInfo() function.</span></span>

<span data-ttu-id="41107-212">Si noti che questi dati possono essere inviati in modo incrementale: solo hello valore più recente per una determinata chiave verrà conservati per un determinato dispositivo.</span><span class="sxs-lookup"><span data-stu-id="41107-212">Note that this data can be sent incrementally: only hello latest value for a given key will be kept for a given device.</span></span> <span data-ttu-id="41107-213">Ad esempio funzionalità aggiuntive di evento, utilizzare un dizionario\<oggetto,\> tooattach dati.</span><span class="sxs-lookup"><span data-stu-id="41107-213">Like event extras, use a Dictionary\<object, object\> tooattach data.</span></span>

### <a name="example"></a><span data-ttu-id="41107-214">Esempio</span><span class="sxs-lookup"><span data-stu-id="41107-214">Example</span></span>
            Dictionary<object, object> appInfo = new Dictionary<object, object>()
              {
                {"birthdate", "1983-12-07"},
                {"gender", "female"}
              };

            EngagementAgent.Instance.SendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="41107-215">Limiti</span><span class="sxs-lookup"><span data-stu-id="41107-215">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="41107-216">Chiavi</span><span class="sxs-lookup"><span data-stu-id="41107-216">Keys</span></span>
<span data-ttu-id="41107-217">Ogni chiave nell'oggetto hello deve corrispondere hello espressione regolare seguente:</span><span class="sxs-lookup"><span data-stu-id="41107-217">Each key in hello object must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="41107-218">Questo significa che le chiavi devono iniziare con almeno una lettera, seguita da lettere, cifre o caratteri di sottolineatura (\_).</span><span class="sxs-lookup"><span data-stu-id="41107-218">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="41107-219">Dimensione</span><span class="sxs-lookup"><span data-stu-id="41107-219">Size</span></span>
<span data-ttu-id="41107-220">Informazioni sull'applicazione è troppo limitati**1024** caratteri per ogni chiamata.</span><span class="sxs-lookup"><span data-stu-id="41107-220">Application information is limited too**1024** characters per call.</span></span>

<span data-ttu-id="41107-221">In hello esempio precedente, hello JSON inviato server toohello è 44 caratteri:</span><span class="sxs-lookup"><span data-stu-id="41107-221">In hello previous example, hello JSON sent toohello server is 44 characters long:</span></span>

            {"birthdate":"1983-12-07","gender":"female"}

## <a name="logging"></a><span data-ttu-id="41107-222">Registrazione</span><span class="sxs-lookup"><span data-stu-id="41107-222">Logging</span></span>
### <a name="enable-logging"></a><span data-ttu-id="41107-223">Abilitare la registrazione</span><span class="sxs-lookup"><span data-stu-id="41107-223">Enable Logging</span></span>
<span data-ttu-id="41107-224">è possibile i log dei test tooproduce configurato nella console IDE hello Hello SDK.</span><span class="sxs-lookup"><span data-stu-id="41107-224">hello SDK can be configured tooproduce test logs in hello IDE console.</span></span>
<span data-ttu-id="41107-225">Questi log non sono abilitati per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="41107-225">These logs are not activated by default.</span></span> <span data-ttu-id="41107-226">toocustomize, questa proprietà hello aggiornamento `EngagementAgent.Instance.TestLogEnabled` tooone del valore di hello disponibile hello `EngagementTestLogLevel` enumerazione, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="41107-226">toocustomize this, update hello property `EngagementAgent.Instance.TestLogEnabled` tooone of hello value available from hello `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

