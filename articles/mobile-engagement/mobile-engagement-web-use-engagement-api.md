---
title: API di Mobile Engagement Web SDK aaaAzure | Documenti Microsoft
description: "Hello procedure per hello Web SDK e gli aggiornamenti più recenti per Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8a87d5ac-d8b7-4a0d-bdee-414dbcc561b2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 06/07/2016
ms.author: piyushjo
ms.openlocfilehash: ec1261d6ad573b8c3ad6d5f616ab7bbe560d6fe2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-mobile-engagement-api-in-a-web-application"></a><span data-ttu-id="11085-103">Utilizzare l'API di Azure Mobile Engagement di hello in un'applicazione web</span><span class="sxs-lookup"><span data-stu-id="11085-103">Use hello Azure Mobile Engagement API in a web application</span></span>
<span data-ttu-id="11085-104">Questo documento è un documento di inoltre toohello che indica come troppo[integrare Mobile Engagement in un'applicazione web](mobile-engagement-web-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="11085-104">This document is an addition toohello document that tells you how too[integrate Mobile Engagement in a web application](mobile-engagement-web-integrate-engagement.md).</span></span> <span data-ttu-id="11085-105">Fornisce informazioni dettagliate su come toouse hello API di Azure Mobile Engagement tooreport le statistiche dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="11085-105">It provides in-depth details about how toouse hello Azure Mobile Engagement API tooreport your application statistics.</span></span>

<span data-ttu-id="11085-106">Hello Mobile Engagement API viene fornita da hello `engagement.agent` oggetto.</span><span class="sxs-lookup"><span data-stu-id="11085-106">hello Mobile Engagement API is provided by hello `engagement.agent` object.</span></span> <span data-ttu-id="11085-107">impostazione predefinita, Azure Mobile Engagement Web SDK alias è Hello `engagement`.</span><span class="sxs-lookup"><span data-stu-id="11085-107">hello default Azure Mobile Engagement Web SDK alias is `engagement`.</span></span> <span data-ttu-id="11085-108">È possibile ridefinire l'alias da configurazione SDK hello.</span><span class="sxs-lookup"><span data-stu-id="11085-108">You can redefine this alias from hello SDK configuration.</span></span>

## <a name="mobile-engagement-concepts"></a><span data-ttu-id="11085-109">Concetti relativi a Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="11085-109">Mobile Engagement concepts</span></span>
<span data-ttu-id="11085-110">Hello dalle parti seguenti perfezionare comuni [concetti di Mobile Engagement](mobile-engagement-concepts.md) per piattaforma web hello.</span><span class="sxs-lookup"><span data-stu-id="11085-110">hello following parts refine common [Mobile Engagement concepts](mobile-engagement-concepts.md) for hello web platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="11085-111">`Session` e `Activity`</span><span class="sxs-lookup"><span data-stu-id="11085-111">`Session` and `Activity`</span></span>
<span data-ttu-id="11085-112">Se l'utente hello rimane inattivo per più di pochi secondi tra due attività, hello sequenza dell'utente di attività è suddiviso in due sessioni distinte.</span><span class="sxs-lookup"><span data-stu-id="11085-112">If hello user stays idle for more than a few seconds between two activities, hello user's sequence of activities is split into two distinct sessions.</span></span> <span data-ttu-id="11085-113">Questi alcuni secondi vengono chiamati hello timeout della sessione.</span><span class="sxs-lookup"><span data-stu-id="11085-113">These few seconds are called hello session timeout.</span></span>

<span data-ttu-id="11085-114">Se l'applicazione web non vengono dichiarati fine hello dell'attività dell'utente da solo (dal chiamante hello `engagement.agent.endActivity` funzione), il server di Mobile Engagement hello scade automaticamente hello sessione utente all'interno di tre minuti dopo la chiusura di una pagina dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="11085-114">If your web application doesn't declare hello end of user activities by itself (by calling hello `engagement.agent.endActivity` function), hello Mobile Engagement server automatically expires hello user session within three minutes after hello application page is closed.</span></span> <span data-ttu-id="11085-115">Si tratta del timeout della sessione server hello.</span><span class="sxs-lookup"><span data-stu-id="11085-115">This is called hello server session timeout.</span></span>

### `Crash`
<span data-ttu-id="11085-116">I report automatici di eccezioni JavaScript non rilevate non vengono creati per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="11085-116">Automated reports of uncaught JavaScript exceptions are not created by default.</span></span> <span data-ttu-id="11085-117">Tuttavia, è possibile segnalare arresti anomali del sistema manualmente utilizzando hello `sendCrash` funzione (vedere la sezione hello sulla segnalazione di arresti anomali del sistema).</span><span class="sxs-lookup"><span data-stu-id="11085-117">However, you can report crashes manually by using hello `sendCrash` function (see hello section on reporting crashes).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="11085-118">Segnalazione di attività</span><span class="sxs-lookup"><span data-stu-id="11085-118">Reporting activities</span></span>
<span data-ttu-id="11085-119">Creazione di report attività utente include quando un utente avvia una nuova attività e quando l'utente hello termina l'attività corrente di hello.</span><span class="sxs-lookup"><span data-stu-id="11085-119">Reporting on user activity includes when a user starts a new activity, and when hello user ends hello current activity.</span></span>

### <a name="user-starts-a-new-activity"></a><span data-ttu-id="11085-120">L'utente avvia una nuova attività</span><span class="sxs-lookup"><span data-stu-id="11085-120">User starts a new activity</span></span>
    engagement.agent.startActivity("MyUserActivity");

<span data-ttu-id="11085-121">È necessario toocall `startActivity()` attività ogni utente in fase di modifica.</span><span class="sxs-lookup"><span data-stu-id="11085-121">You need toocall `startActivity()` each time user activity changes.</span></span> <span data-ttu-id="11085-122">Hello prima chiamata toothis funzione avvia una nuova sessione utente.</span><span class="sxs-lookup"><span data-stu-id="11085-122">hello first call toothis function starts a new user session.</span></span>

### <a name="user-ends-hello-current-activity"></a><span data-ttu-id="11085-123">Utente termina l'attività corrente hello</span><span class="sxs-lookup"><span data-stu-id="11085-123">User ends hello current activity</span></span>
    engagement.agent.endActivity();

<span data-ttu-id="11085-124">È necessario toocall `endActivity()` almeno una volta quando viene completata l'ultima attività utente hello.</span><span class="sxs-lookup"><span data-stu-id="11085-124">You need toocall `endActivity()` at least once when hello user finishes their last activity.</span></span> <span data-ttu-id="11085-125">Questo indica hello Mobile Engagement Web SDK di utente hello è attualmente inattivo, che è necessario toobe sessione utente hello chiuso alla scadenza del timeout della sessione hello.</span><span class="sxs-lookup"><span data-stu-id="11085-125">This informs hello Mobile Engagement Web SDK that hello user is currently idle, and that hello user session needs toobe closed after hello session timeout expires.</span></span> <span data-ttu-id="11085-126">Se si chiama `startActivity()` prima della scadenza del timeout della sessione hello, sessione hello viene semplicemente ripreso.</span><span class="sxs-lookup"><span data-stu-id="11085-126">If you call `startActivity()` before hello session timeout expires, hello session is simply resumed.</span></span>

<span data-ttu-id="11085-127">Poiché non esiste alcuna chiamata affidabile per la chiusura di finestra strumento di navigazione hello, è spesso fine hello difficili o impossibili toocatch di attività dell'utente all'interno di un ambiente web.</span><span class="sxs-lookup"><span data-stu-id="11085-127">Because there's no reliable call for when hello navigator window is closed, it's often difficult or impossible toocatch hello end of user activities inside a web environment.</span></span> <span data-ttu-id="11085-128">Che è hello perché Mobile Engagement server scade automaticamente sessione utente hello entro tre minuti dopo la chiusura di una pagina dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="11085-128">That's why hello Mobile Engagement server automatically expires hello user session within three minutes after hello application page is closed.</span></span>

## <a name="reporting-events"></a><span data-ttu-id="11085-129">Segnalazione di eventi</span><span class="sxs-lookup"><span data-stu-id="11085-129">Reporting events</span></span>
<span data-ttu-id="11085-130">La segnalazione di eventi include eventi di sessione ed eventi autonomi.</span><span class="sxs-lookup"><span data-stu-id="11085-130">Reporting on events covers session events and standalone events.</span></span>

### <a name="session-events"></a><span data-ttu-id="11085-131">Eventi di sessione</span><span class="sxs-lookup"><span data-stu-id="11085-131">Session events</span></span>
<span data-ttu-id="11085-132">Eventi di sessione sono in genere azioni hello tooreport utilizzati eseguite da un utente durante la sessione dell'utente hello.</span><span class="sxs-lookup"><span data-stu-id="11085-132">Session events usually are used tooreport hello actions performed by a user during hello user's session.</span></span>

<span data-ttu-id="11085-133">**Esempio senza dati aggiuntivi:**</span><span class="sxs-lookup"><span data-stu-id="11085-133">**Example without extra data:**</span></span>

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login');
      // [...]
    }

<span data-ttu-id="11085-134">**Esempio con dati aggiuntivi:**</span><span class="sxs-lookup"><span data-stu-id="11085-134">**Example with extra data:**</span></span>

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login', {user: 'alice'});
      // [...]
    }

### <a name="standalone-events"></a><span data-ttu-id="11085-135">Eventi autonomi</span><span class="sxs-lookup"><span data-stu-id="11085-135">Standalone events</span></span>
<span data-ttu-id="11085-136">A differenza degli eventi di sessione, possono verificarsi eventi di autonomo all'esterno di hello contesto di una sessione.</span><span class="sxs-lookup"><span data-stu-id="11085-136">Unlike session events, standalone events can occur outside hello context of a session.</span></span>

<span data-ttu-id="11085-137">A tale scopo, usare ``engagement.agent.sendEvent`` invece di ``engagement.agent.sendSessionEvent``.</span><span class="sxs-lookup"><span data-stu-id="11085-137">For that, use ``engagement.agent.sendEvent`` instead of ``engagement.agent.sendSessionEvent``.</span></span>

## <a name="reporting-errors"></a><span data-ttu-id="11085-138">Segnalazione di errori</span><span class="sxs-lookup"><span data-stu-id="11085-138">Reporting errors</span></span>
<span data-ttu-id="11085-139">La segnalazione di errori include errori di sessione ed errori autonomi.</span><span class="sxs-lookup"><span data-stu-id="11085-139">Reporting on errors covers session errors and standalone errors.</span></span>

### <a name="session-errors"></a><span data-ttu-id="11085-140">Errori di sessione</span><span class="sxs-lookup"><span data-stu-id="11085-140">Session errors</span></span>
<span data-ttu-id="11085-141">Sessione in genere gli errori tooreport utilizzati hello abbia un impatto sull'utente hello durante hello sessione utente.</span><span class="sxs-lookup"><span data-stu-id="11085-141">Session errors usually are used tooreport hello errors that have an impact on hello user during hello user's session.</span></span>

<span data-ttu-id="11085-142">**Esempio senza dati aggiuntivi:**</span><span class="sxs-lookup"><span data-stu-id="11085-142">**Example without extra data:**</span></span>

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short');
      }
      // [...]
    }

<span data-ttu-id="11085-143">**Esempio con dati aggiuntivi:**</span><span class="sxs-lookup"><span data-stu-id="11085-143">**Example with extra data:**</span></span>

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short', {length: 4});
      }
      // [...]
    }

### <a name="standalone-errors"></a><span data-ttu-id="11085-144">Errori autonomi</span><span class="sxs-lookup"><span data-stu-id="11085-144">Standalone errors</span></span>
<span data-ttu-id="11085-145">A differenza degli errori di sessione, possono verificarsi errori di autonomo all'esterno di hello contesto di una sessione.</span><span class="sxs-lookup"><span data-stu-id="11085-145">Unlike session errors, standalone errors can occur outside hello context of a session.</span></span>

<span data-ttu-id="11085-146">A tale scopo, usare `engagement.agent.sendError` invece di `engagement.agent.sendSessionError`.</span><span class="sxs-lookup"><span data-stu-id="11085-146">For that, use `engagement.agent.sendError` instead of `engagement.agent.sendSessionError`.</span></span>

## <a name="reporting-jobs"></a><span data-ttu-id="11085-147">Segnalazione di processi</span><span class="sxs-lookup"><span data-stu-id="11085-147">Reporting jobs</span></span>
<span data-ttu-id="11085-148">La segnalazione di processi include la segnalazione di errori ed eventi che si verificano durante un processo e la segnalazione di arresti anomali.</span><span class="sxs-lookup"><span data-stu-id="11085-148">Reporting on jobs covers reporting errors and events that occur during a job, and reporting crashes.</span></span>

<span data-ttu-id="11085-149">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="11085-149">**Example:**</span></span>

<span data-ttu-id="11085-150">Se si desidera toomonitor una richiesta AJAX, utilizzare la seguente hello:</span><span class="sxs-lookup"><span data-stu-id="11085-150">If you want toomonitor an AJAX request, you'd use hello following:</span></span>

    // [...]
    xhr.onreadystatechange = function() {
      if (xhr.readyState == 4) {
      // [...]
        engagement.agent.endJob('publish');
      }
    }
    engagement.agent.startJob('publish');
    xhr.send();
    // [...]

### <a name="reporting-errors-during-a-job"></a><span data-ttu-id="11085-151">Segnalazione di errori durante un processo</span><span class="sxs-lookup"><span data-stu-id="11085-151">Reporting errors during a job</span></span>
<span data-ttu-id="11085-152">Gli errori possono essere correlato tooa esecuzione processo anziché toohello sessione utente.</span><span class="sxs-lookup"><span data-stu-id="11085-152">Errors can be related tooa running job instead of toohello current user session.</span></span>

<span data-ttu-id="11085-153">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="11085-153">**Example:**</span></span>

<span data-ttu-id="11085-154">Se si desidera tooreport un errore se una richiesta AJAX non riesce:</span><span class="sxs-lookup"><span data-stu-id="11085-154">If you want tooreport an error if an AJAX request fails:</span></span>

    // [...]
    xhr.onreadystatechange = function() {
      if (xhr.readyState == 4) {
        // [...]
        if (xhr.status == 0 || xhr.status >= 400) {
          engagement.agent.sendJobError('publish_xhr', 'publish', {status: xhr.status, statusText: xhr.statusText});
        }
        engagement.agent.endJob('publish');
      }
    }
    engagement.agent.startJob('publish');
    xhr.send();
    // [...]

### <a name="reporting-events-during-a-job"></a><span data-ttu-id="11085-155">Segnalazione di eventi durante un processo</span><span class="sxs-lookup"><span data-stu-id="11085-155">Reporting events during a job</span></span>
<span data-ttu-id="11085-156">Gli eventi possono essere correlato tooa esecuzione processo anziché toohello la sessione utente corrente, grazie toohello `engagement.agent.sendJobEvent` (funzione).</span><span class="sxs-lookup"><span data-stu-id="11085-156">Events can be related tooa running job instead of toohello current user session, thanks toohello `engagement.agent.sendJobEvent` function.</span></span>

<span data-ttu-id="11085-157">Questa funzione opera esattamente come la funzione `engagement.agent.sendJobError`.</span><span class="sxs-lookup"><span data-stu-id="11085-157">This function works exactly like `engagement.agent.sendJobError`.</span></span>

### <a name="reporting-crashes"></a><span data-ttu-id="11085-158">Segnalazione di arresti anomali</span><span class="sxs-lookup"><span data-stu-id="11085-158">Reporting crashes</span></span>
<span data-ttu-id="11085-159">Hello utilizzare `sendCrash` tooreport funzione arresti anomali manualmente.</span><span class="sxs-lookup"><span data-stu-id="11085-159">Use hello `sendCrash` function tooreport crashes manually.</span></span>

<span data-ttu-id="11085-160">Hello `crashid` argomento è una stringa che identifica il tipo di hello di arresto anomalo del sistema.</span><span class="sxs-lookup"><span data-stu-id="11085-160">hello `crashid` argument is a string that identifies hello type of crash.</span></span>
<span data-ttu-id="11085-161">Hello `crash` argomento è in genere l'analisi dello stack hello di arresto anomalo di hello sotto forma di stringa.</span><span class="sxs-lookup"><span data-stu-id="11085-161">hello `crash` argument usually is hello stack trace of hello crash as a string.</span></span>

    engagement.agent.sendCrash(crashid, crash);

## <a name="extra-parameters"></a><span data-ttu-id="11085-162">Parametri aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="11085-162">Extra parameters</span></span>
<span data-ttu-id="11085-163">È possibile collegare l'evento tooan dati arbitrari, errore, attività o processo.</span><span class="sxs-lookup"><span data-stu-id="11085-163">You can attach arbitrary data tooan event, error, activity, or job.</span></span>

<span data-ttu-id="11085-164">dati Hello possono essere qualsiasi oggetto JSON (ma non una matrice o tipo primitivo).</span><span class="sxs-lookup"><span data-stu-id="11085-164">hello data can be any JSON object (but not an array or primitive type).</span></span>

<span data-ttu-id="11085-165">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="11085-165">**Example:**</span></span>

    var extras = {"video_id": 123, "ref_click": "http://foobar.com/blog"};
    engagement.agent.sendEvent("video_clicked", extras);

### <a name="limits"></a><span data-ttu-id="11085-166">Limiti</span><span class="sxs-lookup"><span data-stu-id="11085-166">Limits</span></span>
<span data-ttu-id="11085-167">Limiti applicati tooextra parametri sono nelle aree di hello delle espressioni regolari per le chiavi, i tipi di valore e dimensioni.</span><span class="sxs-lookup"><span data-stu-id="11085-167">Limits that apply tooextra parameters are in hello areas of regular expressions for keys, value types, and size.</span></span>

#### <a name="keys"></a><span data-ttu-id="11085-168">Chiavi</span><span class="sxs-lookup"><span data-stu-id="11085-168">Keys</span></span>
<span data-ttu-id="11085-169">Ogni chiave nell'oggetto hello deve corrispondere hello espressione regolare seguente:</span><span class="sxs-lookup"><span data-stu-id="11085-169">Each key in hello object must match hello following regular expression:</span></span>

    ^[a-zA-Z][a-zA-Z_0-9]*

<span data-ttu-id="11085-170">Questo significa che le chiavi devono iniziare con almeno una lettera seguita da lettere, cifre o caratteri di sottolineatura (\_).</span><span class="sxs-lookup"><span data-stu-id="11085-170">This means that keys must start with at least one letter, followed by letters, digits, or underscores (\_).</span></span>

#### <a name="values"></a><span data-ttu-id="11085-171">Valori</span><span class="sxs-lookup"><span data-stu-id="11085-171">Values</span></span>
<span data-ttu-id="11085-172">I valori sono limitate toostring, numero e i tipi booleani.</span><span class="sxs-lookup"><span data-stu-id="11085-172">Values are limited toostring, number, and Boolean types.</span></span>

#### <a name="size"></a><span data-ttu-id="11085-173">Dimensione</span><span class="sxs-lookup"><span data-stu-id="11085-173">Size</span></span>
<span data-ttu-id="11085-174">Funzionalità aggiuntive sono limitate too1, 024 caratteri per ogni chiamata (dopo hello Mobile Engagement Web SDK viene eseguita la codifica in JSON).</span><span class="sxs-lookup"><span data-stu-id="11085-174">Extras are limited too1,024 characters per call (after hello Mobile Engagement Web SDK encodes it in JSON).</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="11085-175">Segnalazione di informazioni sull'applicazione</span><span class="sxs-lookup"><span data-stu-id="11085-175">Reporting application information</span></span>
<span data-ttu-id="11085-176">È possibile segnalare informazioni (o qualsiasi altra informazione specifici dell'applicazione) il rilevamento delle manualmente utilizzando hello `sendAppInfo()` (funzione).</span><span class="sxs-lookup"><span data-stu-id="11085-176">You can manually report tracking information (or any other application-specific information) by using hello `sendAppInfo()` function.</span></span>

<span data-ttu-id="11085-177">Si noti che queste informazioni possono essere inviate in modo incrementale.</span><span class="sxs-lookup"><span data-stu-id="11085-177">Note that this information can be sent incrementally.</span></span> <span data-ttu-id="11085-178">Per un dispositivo specifico, verrà mantenuto solo hello valore più recente per una chiave specifica.</span><span class="sxs-lookup"><span data-stu-id="11085-178">Only hello latest value for a specific key will be kept for a specific device.</span></span>

<span data-ttu-id="11085-179">Ad esempio funzionalità aggiuntive di evento, è possibile utilizzare le informazioni di applicazione tooabstract oggetto JSON.</span><span class="sxs-lookup"><span data-stu-id="11085-179">Like event extras, you can use any JSON object tooabstract application information.</span></span> <span data-ttu-id="11085-180">Si noti che le matrici o gli oggetti secondari vengono trattati come stringhe flat, usando la serializzazione JSON.</span><span class="sxs-lookup"><span data-stu-id="11085-180">Note that arrays or sub-objects are treated as flat strings (using JSON serialization).</span></span>

<span data-ttu-id="11085-181">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="11085-181">**Example:**</span></span>

<span data-ttu-id="11085-182">Di seguito è riportato un esempio di codice per sesso dell'utente di hello l'invio e la data di nascita:</span><span class="sxs-lookup"><span data-stu-id="11085-182">Here is a code sample for sending hello user's gender and birth date:</span></span>

    var appInfos = {"birthdate":"1983-12-07","gender":"female"};
    engagement.agent.sendAppInfo(appInfos);

### <a name="limits"></a><span data-ttu-id="11085-183">Limiti</span><span class="sxs-lookup"><span data-stu-id="11085-183">Limits</span></span>
<span data-ttu-id="11085-184">Limiti applicati tooapplication informazioni sono nelle aree di hello delle espressioni regolari per le chiavi e dimensioni.</span><span class="sxs-lookup"><span data-stu-id="11085-184">Limits that apply tooapplication information are in hello areas of regular expressions for keys, and size.</span></span>

#### <a name="keys"></a><span data-ttu-id="11085-185">Chiavi</span><span class="sxs-lookup"><span data-stu-id="11085-185">Keys</span></span>
<span data-ttu-id="11085-186">Ogni chiave nell'oggetto hello deve corrispondere hello espressione regolare seguente:</span><span class="sxs-lookup"><span data-stu-id="11085-186">Each key in hello object must match hello following regular expression:</span></span>

    ^[a-zA-Z][a-zA-Z_0-9]*

<span data-ttu-id="11085-187">Questo significa che le chiavi devono iniziare con almeno una lettera seguita da lettere, cifre o caratteri di sottolineatura (\_).</span><span class="sxs-lookup"><span data-stu-id="11085-187">This means that keys must start with at least one letter, followed by letters, digits, or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="11085-188">Dimensione</span><span class="sxs-lookup"><span data-stu-id="11085-188">Size</span></span>
<span data-ttu-id="11085-189">Informazioni sull'applicazione è limitata too1, 024 caratteri per ogni chiamata (dopo hello Mobile Engagement Web SDK viene eseguita la codifica in JSON).</span><span class="sxs-lookup"><span data-stu-id="11085-189">Application information is limited too1,024 characters per call (after hello Mobile Engagement Web SDK encodes it in JSON).</span></span>

<span data-ttu-id="11085-190">In hello sopra riportato, hello JSON inviati, toohello server 44 caratteri:</span><span class="sxs-lookup"><span data-stu-id="11085-190">In hello preceding example, hello JSON sent toohello server is 44 characters long:</span></span>

    {"birthdate":"1983-12-07","gender":"female"}
