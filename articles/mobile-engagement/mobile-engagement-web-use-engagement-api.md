---
title: API dell'SDK per Web per Azure Mobile Engagement | Microsoft Docs
description: Ultimi aggiornamenti e procedure relativi all'SDK per Web per Azure Mobile Engagement
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
ms.openlocfilehash: 54c22ce6a03e382b1bbde102bccc97deec249b30
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-azure-mobile-engagement-api-in-a-web-application"></a><span data-ttu-id="7e247-103">Usare l'API di Azure Mobile Engagement in un'applicazione Web</span><span class="sxs-lookup"><span data-stu-id="7e247-103">Use the Azure Mobile Engagement API in a web application</span></span>
<span data-ttu-id="7e247-104">Questo documento è un'aggiunta al documento [Integrare Azure Mobile Engagement in un'applicazione Web](mobile-engagement-web-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="7e247-104">This document is an addition to the document that tells you how to [integrate Mobile Engagement in a web application](mobile-engagement-web-integrate-engagement.md).</span></span> <span data-ttu-id="7e247-105">Offre informazioni approfondite su come usare l'API di Azure Mobile Engagement per segnalare le statistiche dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7e247-105">It provides in-depth details about how to use the Azure Mobile Engagement API to report your application statistics.</span></span>

<span data-ttu-id="7e247-106">L'API di Mobile Engagement viene messa a disposizione dall'oggetto `engagement.agent` .</span><span class="sxs-lookup"><span data-stu-id="7e247-106">The Mobile Engagement API is provided by the `engagement.agent` object.</span></span> <span data-ttu-id="7e247-107">L'alias predefinito di Azure Mobile Engagement Web SDK è `engagement`.</span><span class="sxs-lookup"><span data-stu-id="7e247-107">The default Azure Mobile Engagement Web SDK alias is `engagement`.</span></span> <span data-ttu-id="7e247-108">È possibile ridefinire l'alias dalla configurazione dell'SDK.</span><span class="sxs-lookup"><span data-stu-id="7e247-108">You can redefine this alias from the SDK configuration.</span></span>

## <a name="mobile-engagement-concepts"></a><span data-ttu-id="7e247-109">Concetti relativi a Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="7e247-109">Mobile Engagement concepts</span></span>
<span data-ttu-id="7e247-110">Le parti seguenti approfondiscono le informazioni contenute nell'articolo [Concetti relativi ad Azure Mobile Engagement](mobile-engagement-concepts.md) per la piattaforma Web.</span><span class="sxs-lookup"><span data-stu-id="7e247-110">The following parts refine common [Mobile Engagement concepts](mobile-engagement-concepts.md) for the web platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="7e247-111">`Session` e `Activity`</span><span class="sxs-lookup"><span data-stu-id="7e247-111">`Session` and `Activity`</span></span>
<span data-ttu-id="7e247-112">Se l'utente resta inattivo per più di alcuni secondi tra due attività, la sequenza di attività dell'utente viene divisa in due sessioni distinte.</span><span class="sxs-lookup"><span data-stu-id="7e247-112">If the user stays idle for more than a few seconds between two activities, the user's sequence of activities is split into two distinct sessions.</span></span> <span data-ttu-id="7e247-113">Questi pochi secondi vengono chiamati timeout della sessione.</span><span class="sxs-lookup"><span data-stu-id="7e247-113">These few seconds are called the session timeout.</span></span>

<span data-ttu-id="7e247-114">Se l'applicazione Web non dichiara la fine delle attività utente chiamando la funzione `engagement.agent.endActivity` , il server di Mobile Engagement terminerà automaticamente la sessione utente entro tre minuti dalla chiusura della pagina dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7e247-114">If your web application doesn't declare the end of user activities by itself (by calling the `engagement.agent.endActivity` function), the Mobile Engagement server automatically expires the user session within three minutes after the application page is closed.</span></span> <span data-ttu-id="7e247-115">Questo comportamento viene definito timeout della sessione del server.</span><span class="sxs-lookup"><span data-stu-id="7e247-115">This is called the server session timeout.</span></span>

### `Crash`
<span data-ttu-id="7e247-116">I report automatici di eccezioni JavaScript non rilevate non vengono creati per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="7e247-116">Automated reports of uncaught JavaScript exceptions are not created by default.</span></span> <span data-ttu-id="7e247-117">È tuttavia possibile segnalare manualmente gli arresti anomali usando la funzione `sendCrash`. Vedere la sezione sulla segnalazione degli arresti anomali.</span><span class="sxs-lookup"><span data-stu-id="7e247-117">However, you can report crashes manually by using the `sendCrash` function (see the section on reporting crashes).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="7e247-118">Segnalazione di attività</span><span class="sxs-lookup"><span data-stu-id="7e247-118">Reporting activities</span></span>
<span data-ttu-id="7e247-119">La segnalazione delle attività utente include il momento in cui un utente avvia una nuova attività e il momento in cui l'utente termina l'attività corrente.</span><span class="sxs-lookup"><span data-stu-id="7e247-119">Reporting on user activity includes when a user starts a new activity, and when the user ends the current activity.</span></span>

### <a name="user-starts-a-new-activity"></a><span data-ttu-id="7e247-120">L'utente avvia una nuova attività</span><span class="sxs-lookup"><span data-stu-id="7e247-120">User starts a new activity</span></span>
    engagement.agent.startActivity("MyUserActivity");

<span data-ttu-id="7e247-121">È necessario chiamare `startActivity()` ogni volta che l'attività dell'utente cambia.</span><span class="sxs-lookup"><span data-stu-id="7e247-121">You need to call `startActivity()` each time user activity changes.</span></span> <span data-ttu-id="7e247-122">La prima chiamata a questa funzione avvia una nuova sessione utente.</span><span class="sxs-lookup"><span data-stu-id="7e247-122">The first call to this function starts a new user session.</span></span>

### <a name="user-ends-the-current-activity"></a><span data-ttu-id="7e247-123">L'utente termina l'attività corrente</span><span class="sxs-lookup"><span data-stu-id="7e247-123">User ends the current activity</span></span>
    engagement.agent.endActivity();

<span data-ttu-id="7e247-124">È necessario chiamare `endActivity()` almeno una volta quando l'utente termina l'ultima attività.</span><span class="sxs-lookup"><span data-stu-id="7e247-124">You need to call `endActivity()` at least once when the user finishes their last activity.</span></span> <span data-ttu-id="7e247-125">In questo modo si indica a Mobile Engagement Web SDK che l'utente è attualmente inattivo e che la sessione utente deve essere chiusa allo scadere del timeout.</span><span class="sxs-lookup"><span data-stu-id="7e247-125">This informs the Mobile Engagement Web SDK that the user is currently idle, and that the user session needs to be closed after the session timeout expires.</span></span> <span data-ttu-id="7e247-126">Se si chiama `startActivity()` prima dello scadere del timeout, la sessione viene semplicemente ripresa.</span><span class="sxs-lookup"><span data-stu-id="7e247-126">If you call `startActivity()` before the session timeout expires, the session is simply resumed.</span></span>

<span data-ttu-id="7e247-127">Data l'assenza di una chiamata affidabile per il momento in cui la finestra dello strumento di navigazione viene chiusa, è spesso difficile o impossibile rilevare la fine delle attività utente all'interno di ambienti Web.</span><span class="sxs-lookup"><span data-stu-id="7e247-127">Because there's no reliable call for when the navigator window is closed, it's often difficult or impossible to catch the end of user activities inside a web environment.</span></span> <span data-ttu-id="7e247-128">Per questo motivo il server di Mobile Engagement termina automaticamente la sessione utente entro tre minuti dalla chiusura della pagina dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7e247-128">That's why the Mobile Engagement server automatically expires the user session within three minutes after the application page is closed.</span></span>

## <a name="reporting-events"></a><span data-ttu-id="7e247-129">Segnalazione di eventi</span><span class="sxs-lookup"><span data-stu-id="7e247-129">Reporting events</span></span>
<span data-ttu-id="7e247-130">La segnalazione di eventi include eventi di sessione ed eventi autonomi.</span><span class="sxs-lookup"><span data-stu-id="7e247-130">Reporting on events covers session events and standalone events.</span></span>

### <a name="session-events"></a><span data-ttu-id="7e247-131">Eventi di sessione</span><span class="sxs-lookup"><span data-stu-id="7e247-131">Session events</span></span>
<span data-ttu-id="7e247-132">Gli eventi di sessione vengono in genere usati per segnalare le azioni eseguite da un utente durante la sua sessione.</span><span class="sxs-lookup"><span data-stu-id="7e247-132">Session events usually are used to report the actions performed by a user during the user's session.</span></span>

<span data-ttu-id="7e247-133">**Esempio senza dati aggiuntivi:**</span><span class="sxs-lookup"><span data-stu-id="7e247-133">**Example without extra data:**</span></span>

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login');
      // [...]
    }

<span data-ttu-id="7e247-134">**Esempio con dati aggiuntivi:**</span><span class="sxs-lookup"><span data-stu-id="7e247-134">**Example with extra data:**</span></span>

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login', {user: 'alice'});
      // [...]
    }

### <a name="standalone-events"></a><span data-ttu-id="7e247-135">Eventi autonomi</span><span class="sxs-lookup"><span data-stu-id="7e247-135">Standalone events</span></span>
<span data-ttu-id="7e247-136">A differenza degli eventi di sessione, gli eventi autonomi possono verificarsi all'esterno del contesto di una sessione.</span><span class="sxs-lookup"><span data-stu-id="7e247-136">Unlike session events, standalone events can occur outside the context of a session.</span></span>

<span data-ttu-id="7e247-137">A tale scopo, usare ``engagement.agent.sendEvent`` invece di ``engagement.agent.sendSessionEvent``.</span><span class="sxs-lookup"><span data-stu-id="7e247-137">For that, use ``engagement.agent.sendEvent`` instead of ``engagement.agent.sendSessionEvent``.</span></span>

## <a name="reporting-errors"></a><span data-ttu-id="7e247-138">Segnalazione di errori</span><span class="sxs-lookup"><span data-stu-id="7e247-138">Reporting errors</span></span>
<span data-ttu-id="7e247-139">La segnalazione di errori include errori di sessione ed errori autonomi.</span><span class="sxs-lookup"><span data-stu-id="7e247-139">Reporting on errors covers session errors and standalone errors.</span></span>

### <a name="session-errors"></a><span data-ttu-id="7e247-140">Errori di sessione</span><span class="sxs-lookup"><span data-stu-id="7e247-140">Session errors</span></span>
<span data-ttu-id="7e247-141">Gli errori di sessione vengono in genere usati per segnalare gli errori che hanno impatto sull'utente durante la sua sessione.</span><span class="sxs-lookup"><span data-stu-id="7e247-141">Session errors usually are used to report the errors that have an impact on the user during the user's session.</span></span>

<span data-ttu-id="7e247-142">**Esempio senza dati aggiuntivi:**</span><span class="sxs-lookup"><span data-stu-id="7e247-142">**Example without extra data:**</span></span>

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short');
      }
      // [...]
    }

<span data-ttu-id="7e247-143">**Esempio con dati aggiuntivi:**</span><span class="sxs-lookup"><span data-stu-id="7e247-143">**Example with extra data:**</span></span>

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short', {length: 4});
      }
      // [...]
    }

### <a name="standalone-errors"></a><span data-ttu-id="7e247-144">Errori autonomi</span><span class="sxs-lookup"><span data-stu-id="7e247-144">Standalone errors</span></span>
<span data-ttu-id="7e247-145">A differenza degli errori di sessione, gli errori autonomi possono verificarsi all'esterno del contesto di una sessione.</span><span class="sxs-lookup"><span data-stu-id="7e247-145">Unlike session errors, standalone errors can occur outside the context of a session.</span></span>

<span data-ttu-id="7e247-146">A tale scopo, usare `engagement.agent.sendError` invece di `engagement.agent.sendSessionError`.</span><span class="sxs-lookup"><span data-stu-id="7e247-146">For that, use `engagement.agent.sendError` instead of `engagement.agent.sendSessionError`.</span></span>

## <a name="reporting-jobs"></a><span data-ttu-id="7e247-147">Segnalazione di processi</span><span class="sxs-lookup"><span data-stu-id="7e247-147">Reporting jobs</span></span>
<span data-ttu-id="7e247-148">La segnalazione di processi include la segnalazione di errori ed eventi che si verificano durante un processo e la segnalazione di arresti anomali.</span><span class="sxs-lookup"><span data-stu-id="7e247-148">Reporting on jobs covers reporting errors and events that occur during a job, and reporting crashes.</span></span>

<span data-ttu-id="7e247-149">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="7e247-149">**Example:**</span></span>

<span data-ttu-id="7e247-150">Per monitorare una richiesta AJAX, usare il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="7e247-150">If you want to monitor an AJAX request, you'd use the following:</span></span>

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

### <a name="reporting-errors-during-a-job"></a><span data-ttu-id="7e247-151">Segnalazione di errori durante un processo</span><span class="sxs-lookup"><span data-stu-id="7e247-151">Reporting errors during a job</span></span>
<span data-ttu-id="7e247-152">Gli errori possono essere correlati a un processo in esecuzione invece che alla sessione utente corrente.</span><span class="sxs-lookup"><span data-stu-id="7e247-152">Errors can be related to a running job instead of to the current user session.</span></span>

<span data-ttu-id="7e247-153">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="7e247-153">**Example:**</span></span>

<span data-ttu-id="7e247-154">Per segnalare un errore in caso di esito negativo di una richiesta AJAX:</span><span class="sxs-lookup"><span data-stu-id="7e247-154">If you want to report an error if an AJAX request fails:</span></span>

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

### <a name="reporting-events-during-a-job"></a><span data-ttu-id="7e247-155">Segnalazione di eventi durante un processo</span><span class="sxs-lookup"><span data-stu-id="7e247-155">Reporting events during a job</span></span>
<span data-ttu-id="7e247-156">Gli eventi possono essere correlati a un processo in esecuzione invece che alla sessione utente corrente grazie alla funzione `engagement.agent.sendJobEvent` .</span><span class="sxs-lookup"><span data-stu-id="7e247-156">Events can be related to a running job instead of to the current user session, thanks to the `engagement.agent.sendJobEvent` function.</span></span>

<span data-ttu-id="7e247-157">Questa funzione opera esattamente come la funzione `engagement.agent.sendJobError`.</span><span class="sxs-lookup"><span data-stu-id="7e247-157">This function works exactly like `engagement.agent.sendJobError`.</span></span>

### <a name="reporting-crashes"></a><span data-ttu-id="7e247-158">Segnalazione di arresti anomali</span><span class="sxs-lookup"><span data-stu-id="7e247-158">Reporting crashes</span></span>
<span data-ttu-id="7e247-159">Usare la funzione `sendCrash` per segnalare manualmente gli arresti anomali.</span><span class="sxs-lookup"><span data-stu-id="7e247-159">Use the `sendCrash` function to report crashes manually.</span></span>

<span data-ttu-id="7e247-160">L'argomento `crashid` è una stringa che identifica il tipo di arresto anomalo.</span><span class="sxs-lookup"><span data-stu-id="7e247-160">The `crashid` argument is a string that identifies the type of crash.</span></span>
<span data-ttu-id="7e247-161">L'argomento `crash` è in genere l'analisi dello stack dell'arresto anomalo sotto forma di stringa.</span><span class="sxs-lookup"><span data-stu-id="7e247-161">The `crash` argument usually is the stack trace of the crash as a string.</span></span>

    engagement.agent.sendCrash(crashid, crash);

## <a name="extra-parameters"></a><span data-ttu-id="7e247-162">Parametri aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="7e247-162">Extra parameters</span></span>
<span data-ttu-id="7e247-163">È possibile collegare dati arbitrari a un evento, errore, attività o processo.</span><span class="sxs-lookup"><span data-stu-id="7e247-163">You can attach arbitrary data to an event, error, activity, or job.</span></span>

<span data-ttu-id="7e247-164">Questi dati possono essere qualsiasi oggetto JSON, ma non una matrice o un tipo primitivo.</span><span class="sxs-lookup"><span data-stu-id="7e247-164">The data can be any JSON object (but not an array or primitive type).</span></span>

<span data-ttu-id="7e247-165">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="7e247-165">**Example:**</span></span>

    var extras = {"video_id": 123, "ref_click": "http://foobar.com/blog"};
    engagement.agent.sendEvent("video_clicked", extras);

### <a name="limits"></a><span data-ttu-id="7e247-166">Limiti</span><span class="sxs-lookup"><span data-stu-id="7e247-166">Limits</span></span>
<span data-ttu-id="7e247-167">I limiti che si applicano ai parametri aggiuntivi riguardano le aree delle espressioni regolari per chiavi, tipi di valore e dimensioni.</span><span class="sxs-lookup"><span data-stu-id="7e247-167">Limits that apply to extra parameters are in the areas of regular expressions for keys, value types, and size.</span></span>

#### <a name="keys"></a><span data-ttu-id="7e247-168">Chiavi</span><span class="sxs-lookup"><span data-stu-id="7e247-168">Keys</span></span>
<span data-ttu-id="7e247-169">Ogni chiave dell'oggetto deve corrispondere all'espressione regolare seguente:</span><span class="sxs-lookup"><span data-stu-id="7e247-169">Each key in the object must match the following regular expression:</span></span>

    ^[a-zA-Z][a-zA-Z_0-9]*

<span data-ttu-id="7e247-170">Questo significa che le chiavi devono iniziare con almeno una lettera seguita da lettere, cifre o caratteri di sottolineatura (\_).</span><span class="sxs-lookup"><span data-stu-id="7e247-170">This means that keys must start with at least one letter, followed by letters, digits, or underscores (\_).</span></span>

#### <a name="values"></a><span data-ttu-id="7e247-171">Valori</span><span class="sxs-lookup"><span data-stu-id="7e247-171">Values</span></span>
<span data-ttu-id="7e247-172">I valori sono limitati a tipi string, number e boolean.</span><span class="sxs-lookup"><span data-stu-id="7e247-172">Values are limited to string, number, and Boolean types.</span></span>

#### <a name="size"></a><span data-ttu-id="7e247-173">Dimensione</span><span class="sxs-lookup"><span data-stu-id="7e247-173">Size</span></span>
<span data-ttu-id="7e247-174">I dati aggiuntivi sono limitati a 1.024 caratteri per chiamata, dopo che la chiamata è stata codificata in JSON da Mobile Engagement Web SDK.</span><span class="sxs-lookup"><span data-stu-id="7e247-174">Extras are limited to 1,024 characters per call (after the Mobile Engagement Web SDK encodes it in JSON).</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="7e247-175">Segnalazione di informazioni sull'applicazione</span><span class="sxs-lookup"><span data-stu-id="7e247-175">Reporting application information</span></span>
<span data-ttu-id="7e247-176">È possibile segnalare manualmente le informazioni di traccia o qualsiasi altra informazione specifica dell'applicazione con la funzione `sendAppInfo()` .</span><span class="sxs-lookup"><span data-stu-id="7e247-176">You can manually report tracking information (or any other application-specific information) by using the `sendAppInfo()` function.</span></span>

<span data-ttu-id="7e247-177">Si noti che queste informazioni possono essere inviate in modo incrementale.</span><span class="sxs-lookup"><span data-stu-id="7e247-177">Note that this information can be sent incrementally.</span></span> <span data-ttu-id="7e247-178">Verrà mantenuto solo l'ultimo valore per una chiave specifica per un dispositivo specifico.</span><span class="sxs-lookup"><span data-stu-id="7e247-178">Only the latest value for a specific key will be kept for a specific device.</span></span>

<span data-ttu-id="7e247-179">Come per i dati aggiuntivi degli eventi, è possibile usare qualsiasi oggetto JSON per astrarre le informazioni sull'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7e247-179">Like event extras, you can use any JSON object to abstract application information.</span></span> <span data-ttu-id="7e247-180">Si noti che le matrici o gli oggetti secondari vengono trattati come stringhe flat, usando la serializzazione JSON.</span><span class="sxs-lookup"><span data-stu-id="7e247-180">Note that arrays or sub-objects are treated as flat strings (using JSON serialization).</span></span>

<span data-ttu-id="7e247-181">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="7e247-181">**Example:**</span></span>

<span data-ttu-id="7e247-182">Di seguito è riportato un esempio di codice per inviare il sesso e la data di nascita dell'utente:</span><span class="sxs-lookup"><span data-stu-id="7e247-182">Here is a code sample for sending the user's gender and birth date:</span></span>

    var appInfos = {"birthdate":"1983-12-07","gender":"female"};
    engagement.agent.sendAppInfo(appInfos);

### <a name="limits"></a><span data-ttu-id="7e247-183">Limiti</span><span class="sxs-lookup"><span data-stu-id="7e247-183">Limits</span></span>
<span data-ttu-id="7e247-184">I limiti che si applicano alle informazioni sull'applicazione riguardano le aree delle espressioni regolari per chiavi e dimensioni.</span><span class="sxs-lookup"><span data-stu-id="7e247-184">Limits that apply to application information are in the areas of regular expressions for keys, and size.</span></span>

#### <a name="keys"></a><span data-ttu-id="7e247-185">Chiavi</span><span class="sxs-lookup"><span data-stu-id="7e247-185">Keys</span></span>
<span data-ttu-id="7e247-186">Ogni chiave dell'oggetto deve corrispondere all'espressione regolare seguente:</span><span class="sxs-lookup"><span data-stu-id="7e247-186">Each key in the object must match the following regular expression:</span></span>

    ^[a-zA-Z][a-zA-Z_0-9]*

<span data-ttu-id="7e247-187">Questo significa che le chiavi devono iniziare con almeno una lettera seguita da lettere, cifre o caratteri di sottolineatura (\_).</span><span class="sxs-lookup"><span data-stu-id="7e247-187">This means that keys must start with at least one letter, followed by letters, digits, or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="7e247-188">Dimensione</span><span class="sxs-lookup"><span data-stu-id="7e247-188">Size</span></span>
<span data-ttu-id="7e247-189">Le informazioni sull'applicazione sono limitate a 1.024 caratteri per chiamata, dopo che la chiamata è stata codificata in JSON da Mobile Engagement Web SDK.</span><span class="sxs-lookup"><span data-stu-id="7e247-189">Application information is limited to 1,024 characters per call (after the Mobile Engagement Web SDK encodes it in JSON).</span></span>

<span data-ttu-id="7e247-190">Nell'esempio precedente, il codice JSON inviato al server è lungo 44 caratteri:</span><span class="sxs-lookup"><span data-stu-id="7e247-190">In the preceding example, the JSON sent to the server is 44 characters long:</span></span>

    {"birthdate":"1983-12-07","gender":"female"}
