---
title: Come usare l'API di Engagement in iOS
description: "iOS SDK più recente: come usare l'API di Engagement in iOS"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 1fb4509e-3804-46c1-949f-1cf727f91f9f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: a31424da98205e97bdf57010cccfd044360f03dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-engagement-api-on-ios"></a><span data-ttu-id="c1766-103">Come usare l'API di Engagement in iOS</span><span class="sxs-lookup"><span data-stu-id="c1766-103">How to Use the Engagement API on iOS</span></span>
<span data-ttu-id="c1766-104">Questo documento è complementare all'articolo relativo all'integrazione di Engagement in iOS e fornisce informazioni approfondite su come usare l'API di Engagement per segnalare le statistiche dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c1766-104">This document is an add-on to the document How to Integrate Engagement on iOS: it provides in depth details about how to use the Engagement API to report your application statistics.</span></span>

<span data-ttu-id="c1766-105">Tenere presente che, se si vuole impostare Engagement in modo che segnali solo le sessioni, le attività, gli arresti anomali e i dati tecnici dell'applicazione, la soluzione più semplice consiste nel fare in modo che tutti gli oggetti `UIViewController` personalizzati ereditino dalla classe `EngagementViewController` corrispondente.</span><span class="sxs-lookup"><span data-stu-id="c1766-105">Keep in mind that if you only want Engagement to report your application's sessions, activities, crashes and technical information, then the simplest way is to make all your custom `UIViewController` objects inherit from the corresponding `EngagementViewController` class.</span></span>

<span data-ttu-id="c1766-106">Se invece si hanno esigenze più complesse, ad esempio se è necessario segnalare eventi, errori e processi specifici dell'applicazione o presentare le attività dell'applicazione in modo diverso rispetto a quello implementato nelle classi `EngagementViewController`, è necessario usare l'API di Engagement.</span><span class="sxs-lookup"><span data-stu-id="c1766-106">If you want to do more, for example if you need to report application specific events, errors and jobs, or if you have to report your application's activities in a different way than the one implemented in the `EngagementViewController` classes, then you need to use the Engagement API.</span></span>

<span data-ttu-id="c1766-107">L'API di Engagement viene fornita dalla classe `EngagementAgent` .</span><span class="sxs-lookup"><span data-stu-id="c1766-107">The Engagement API is provided by the `EngagementAgent` class.</span></span> <span data-ttu-id="c1766-108">Un'istanza di questa classe può essere recuperata chiamando il metodo statico `[EngagementAgent shared]` (tenere presente che l'oggetto `EngagementAgent` restituito è un singleton).</span><span class="sxs-lookup"><span data-stu-id="c1766-108">An instance of this class can be retrieved by calling the `[EngagementAgent shared]` static method (note that the `EngagementAgent` object returned is a singleton).</span></span>

<span data-ttu-id="c1766-109">Prima di eseguire chiamate API, è necessario inizializzare l'oggetto `EngagementAgent` chiamando il metodo `[EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];`</span><span class="sxs-lookup"><span data-stu-id="c1766-109">Before any API calls, the `EngagementAgent` object must be initialized by calling the method `[EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];`</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="c1766-110">Concetti relativi a Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="c1766-110">Engagement concepts</span></span>
<span data-ttu-id="c1766-111">Le parti seguenti approfondiscono le informazioni contenute nell'articolo [Concetti relativi ad Azure Mobile Engagement](mobile-engagement-concepts.md) per la piattaforma iOS.</span><span class="sxs-lookup"><span data-stu-id="c1766-111">The following parts refine the common [Mobile Engagement Concepts](mobile-engagement-concepts.md) for the iOS platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="c1766-112">`Session` e `Activity`</span><span class="sxs-lookup"><span data-stu-id="c1766-112">`Session` and `Activity`</span></span>
<span data-ttu-id="c1766-113">Un'*attività* è in genere associata a una schermata dell'applicazione, ovvero l'*attività* inizia quando la schermata viene visualizzata e si arresta quando la schermata viene chiusa. Questo avviene quando l'SDK di Engagement è integrato mediante le classi `EngagementViewController`.</span><span class="sxs-lookup"><span data-stu-id="c1766-113">An *activity* is usually associated with one screen of the application, that is to say the *activity* starts when the screen is displayed and stops when the screen is closed: this is the case when the Engagement SDK is integrated by using the `EngagementViewController` classes.</span></span>

<span data-ttu-id="c1766-114">Le *attività* possono tuttavia essere controllate anche manualmente usando l'API di Engagement.</span><span class="sxs-lookup"><span data-stu-id="c1766-114">But *activities* can also be controlled manually by using the Engagement API.</span></span> <span data-ttu-id="c1766-115">In questo modo, è possibile dividere una schermata specifica in diverse parti secondarie per ottenere maggiori dettagli sull'utilizzo della schermata, ad esempio per definire la frequenza e la durata in base alle quali le finestre di dialogo vengono usate all'interno della schermata.</span><span class="sxs-lookup"><span data-stu-id="c1766-115">This allows to split a given screen in several sub parts to get more details about the usage of this screen (for example to known how often and how long dialogs are used inside this screen).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="c1766-116">Segnalazione di attività</span><span class="sxs-lookup"><span data-stu-id="c1766-116">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="c1766-117">L'utente inizia una nuova attività</span><span class="sxs-lookup"><span data-stu-id="c1766-117">User starts a new Activity</span></span>
            [[EngagementAgent shared] startActivity:@"MyUserActivity" extras:nil];

<span data-ttu-id="c1766-118">È necessario chiamare `startActivity()` ogni volta che l'attività dell'utente cambia.</span><span class="sxs-lookup"><span data-stu-id="c1766-118">You need to call `startActivity()` each time the user activity changes.</span></span> <span data-ttu-id="c1766-119">La prima chiamata a questa funzione avvia una nuova sessione utente.</span><span class="sxs-lookup"><span data-stu-id="c1766-119">The first call to this function starts a new user session.</span></span>

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="c1766-120">L'utente termina l'attività corrente</span><span class="sxs-lookup"><span data-stu-id="c1766-120">User ends his current Activity</span></span>
            [[EngagementAgent shared] endActivity];

> [!WARNING]
> <span data-ttu-id="c1766-121">Questa funzione non deve **MAI** essere chiamata autonomamente, a meno che non si desideri dividere un uso dell'applicazione in più sessioni. Una chiamata a questa funzione interromperebbe immediatamente la sessione corrente e quindi una successiva chiamata a `startActivity()` avvierebbe una nuova sessione.</span><span class="sxs-lookup"><span data-stu-id="c1766-121">You should **NEVER** call this function by yourself, except if you want to split one use of your application into several sessions: a call to this function would end the current session immediately, so, a subsequent call to `startActivity()` would start a new session.</span></span> <span data-ttu-id="c1766-122">Questa funzionalità viene chiamata automaticamente dall'SDK durante la chiusura dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c1766-122">This function is automatically called by the SDK when your application is closed.</span></span>
> 
> 

## <a name="reporting-events"></a><span data-ttu-id="c1766-123">Segnalazione di eventi</span><span class="sxs-lookup"><span data-stu-id="c1766-123">Reporting Events</span></span>
### <a name="session-events"></a><span data-ttu-id="c1766-124">Eventi di sessione</span><span class="sxs-lookup"><span data-stu-id="c1766-124">Session events</span></span>
<span data-ttu-id="c1766-125">Gli eventi di sessione vengono in genere usati per segnalare le azioni eseguite da un utente durante la sua sessione.</span><span class="sxs-lookup"><span data-stu-id="c1766-125">Session events are usually used to report the actions performed by a user during his session.</span></span>

<span data-ttu-id="c1766-126">**Esempio senza dati aggiuntivi:**</span><span class="sxs-lookup"><span data-stu-id="c1766-126">**Example without extra data:**</span></span>

    @implementation MyViewController {
       [...]
       - (void)willRotateToInterfaceOrientation:(UIInterfaceOrientation)toInterfaceOrientation duration:(NSTimeInterval)duration
       {
        [super willRotateToInterfaceOrientation:toInterfaceOrientation duration:duration];
            ...
        [[EngagementAgent shared] sendSessionEvent:@"will_rotate" extras:nil];
            ...
       }
       [...]
    }

<span data-ttu-id="c1766-127">**Esempio con dati aggiuntivi:**</span><span class="sxs-lookup"><span data-stu-id="c1766-127">**Example with extra data:**</span></span>

    @implementation MyViewController {
       [...]
       - (void)willRotateToInterfaceOrientation:(UIInterfaceOrientation)toInterfaceOrientation duration:(NSTimeInterval)duration
       {
        [super willRotateToInterfaceOrientation:toInterfaceOrientation duration:duration];
            ...
        NSMutableDictionary* extras = [NSMutableDictionary dictionary];
        [extras setObject:[NSNumber numberWithInt:toInterfaceOrientation] forKey:@"to_orientation_id"];
        [extras setObject:[NSNumber numberWithDouble:duration] forKey:@"duration"];
        [[EngagementAgent shared] sendSessionEvent:@"will_rotate" extras:extras];
            ...
       }
       [...]
    }

### <a name="standalone-events"></a><span data-ttu-id="c1766-128">Eventi autonomi</span><span class="sxs-lookup"><span data-stu-id="c1766-128">Standalone events</span></span>
<span data-ttu-id="c1766-129">Contrariamente agli eventi della sessione, quelli autonomi possono essere utilizzati al di fuori del contesto di una sessione.</span><span class="sxs-lookup"><span data-stu-id="c1766-129">Contrary to session events, standalone events can be used outside of the context of a session.</span></span>

<span data-ttu-id="c1766-130">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="c1766-130">**Example:**</span></span>

    [[EngagementAgent shared] sendEvent:@"received_notification" extras:nil];

## <a name="reporting-errors"></a><span data-ttu-id="c1766-131">Segnalazione di errori</span><span class="sxs-lookup"><span data-stu-id="c1766-131">Reporting Errors</span></span>
### <a name="session-errors"></a><span data-ttu-id="c1766-132">Errori di sessione</span><span class="sxs-lookup"><span data-stu-id="c1766-132">Session errors</span></span>
<span data-ttu-id="c1766-133">Gli errori di sessione vengono in genere usati per segnalare gli errori che hanno impatto sull'utente durante la sua sessione.</span><span class="sxs-lookup"><span data-stu-id="c1766-133">Session errors are usually used to report the errors impacting the user during his session.</span></span>

<span data-ttu-id="c1766-134">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="c1766-134">**Example:**</span></span>

    /** The user has entered invalid data in a form */
    @implementation MyViewController {
      [...]
      -(void)onMyFormSubmitted:(MyForm*)form {
        [...]
        /* The user has entered an invalid email address */
        [[EngagementAgent shared] sendSessionError:@"sign_up_email" extras:nil]
        [...]
      }
      [...]
    }

### <a name="standalone-errors"></a><span data-ttu-id="c1766-135">Errori autonomi</span><span class="sxs-lookup"><span data-stu-id="c1766-135">Standalone errors</span></span>
<span data-ttu-id="c1766-136">Contrariamente agli errori della sessione, quelli autonomi possono essere utilizzati al di fuori del contesto di una sessione.</span><span class="sxs-lookup"><span data-stu-id="c1766-136">Contrary to session errors, standalone errors can be used outside of the context of a session.</span></span>

<span data-ttu-id="c1766-137">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="c1766-137">**Example:**</span></span>

    [[EngagementAgent shared] sendError:@"something_failed" extras:nil];

## <a name="reporting-jobs"></a><span data-ttu-id="c1766-138">Segnalazione di processi</span><span class="sxs-lookup"><span data-stu-id="c1766-138">Reporting Jobs</span></span>
<span data-ttu-id="c1766-139">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="c1766-139">**Example:**</span></span>

<span data-ttu-id="c1766-140">Si supponga di voler segnalare la durata del processo di accesso:</span><span class="sxs-lookup"><span data-stu-id="c1766-140">Suppose you want to report the duration of your login process:</span></span>

    [...]
    -(void)signIn
    {
      /* Start job */
      [[EngagementAgent shared] startJob:@"sign_in" extras:nil];

      [... sign in ...]

      /* End job */
      [[EngagementAgent shared] endJob:@"sign_in"];
    }
    [...]

### <a name="report-errors-during-a-job"></a><span data-ttu-id="c1766-141">Segnalazione di errori durante un processo</span><span class="sxs-lookup"><span data-stu-id="c1766-141">Report Errors during a Job</span></span>
<span data-ttu-id="c1766-142">Gli errori possono essere correlati a un processo in esecuzione invece che alla sessione utente corrente.</span><span class="sxs-lookup"><span data-stu-id="c1766-142">Errors can be related to a running job instead of being related to the current user session.</span></span>

<span data-ttu-id="c1766-143">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="c1766-143">**Example:**</span></span>

<span data-ttu-id="c1766-144">Si consideri una situazione nella quale l'utente desidera segnalare un errore durante il processo di accesso:</span><span class="sxs-lookup"><span data-stu-id="c1766-144">Suppose you want to report an error during your login process:</span></span>

    [...]
    -(void)signin
    {
      /* Start job */
      [[EngagementAgent shared] startJob:@"sign_in" extras:nil];

      BOOL success = NO;
      while (!success) {
        /* Try to sign in */
        NSError* error = nil;
        [self trySigin:&error];
        success = error == nil;

        /* If an error occured report it */
        if(!success)
        {
          [[EngagementAgent shared] sendJobError:@"sign_in_error"
                         jobName:@"sign_in"
                          extras:[NSDictionary dictionaryWithObject:[error localizedDescription] forKey:@"error"]];

          /* Retry after a moment */
          [NSThread sleepForTimeInterval:20];
        }
      }

      /* End job */
      [[EngagementAgent shared] endJob:@"sign_in"];
    };
    [...]

### <a name="events-during-a-job"></a><span data-ttu-id="c1766-145">Eventi durante un processo</span><span class="sxs-lookup"><span data-stu-id="c1766-145">Events during a job</span></span>
<span data-ttu-id="c1766-146">Gli eventi possono essere correlati a un processo in esecuzione invece che alla sessione utente corrente.</span><span class="sxs-lookup"><span data-stu-id="c1766-146">Events can be related to a running job instead of being related to the current user session.</span></span>

<span data-ttu-id="c1766-147">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="c1766-147">**Example:**</span></span>

<span data-ttu-id="c1766-148">Si supponga di disporre di un social network e di usare un processo per segnalare il tempo totale durante il quale l'utente è connesso al server.</span><span class="sxs-lookup"><span data-stu-id="c1766-148">Suppose we have a social network, and we use a job to report the total time during which the user is connected to the server.</span></span> <span data-ttu-id="c1766-149">Se l'utente riceve messaggi dagli amici, si tratta di un evento di processo.</span><span class="sxs-lookup"><span data-stu-id="c1766-149">The user can receive messages from his friends, this is a job event.</span></span>

    [...]
    - (void) signin
    {
      [...Sign in code...]
      [[EngagementAgent shared] startJob:@"connection" extras:nil];
    }
    [...]
    - (void) signout
    {
      [...Sign out code...]
      [[EngagementAgent shared] endJob:@"connection"];
    }
    [...]
    - (void) onMessageReceived
    {
      [...Notify user...]
      [[EngagementAgent shared] sendJobEvent:@"connection" jobName:@"message_received" extras:nil];
    }
    [...]

## <a name="extra-parameters"></a><span data-ttu-id="c1766-150">Parametri aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="c1766-150">Extra parameters</span></span>
<span data-ttu-id="c1766-151">È possibile collegare dati arbitrari a eventi, errori, attività e processi.</span><span class="sxs-lookup"><span data-stu-id="c1766-151">Arbitrary data can be attached to events, errors, activities and jobs.</span></span>

<span data-ttu-id="c1766-152">Questi dati possono essere strutturati e utilizzano la classe NSDictionary di iOS.</span><span class="sxs-lookup"><span data-stu-id="c1766-152">This data can be structured, it uses iOS's NSDictionary class.</span></span>

<span data-ttu-id="c1766-153">Tenere presente che i dati aggiuntivi possono includere `arrays(NSArray, NSMutableArray)`, `numbers(NSNumber class)`, `strings(NSString, NSMutableString)`, `urls(NSURL)`, `data(NSData, NSMutableData)` o altre istanze di `NSDictionary`.</span><span class="sxs-lookup"><span data-stu-id="c1766-153">Note that extras can contain `arrays(NSArray, NSMutableArray)`, `numbers(NSNumber class)`, `strings(NSString, NSMutableString)`, `urls(NSURL)`, `data(NSData, NSMutableData)` or other `NSDictionary` instances.</span></span>

> [!NOTE]
> <span data-ttu-id="c1766-154">Il parametro aggiuntivo viene serializzato in JSON.</span><span class="sxs-lookup"><span data-stu-id="c1766-154">The extra parameter is serialized in JSON.</span></span> <span data-ttu-id="c1766-155">Se si desidera passare oggetti diversi da quelli descritti in precedenza, è necessario implementare il metodo seguente nella classe:</span><span class="sxs-lookup"><span data-stu-id="c1766-155">If you want to pass different objects than the ones described above, you must implement the following method in your class:</span></span>
> 
> <span data-ttu-id="c1766-156">-(NSString*)JSONRepresentation;</span><span class="sxs-lookup"><span data-stu-id="c1766-156">-(NSString*)JSONRepresentation;</span></span>
> 
> <span data-ttu-id="c1766-157">Il metodo deve restituire una rappresentazione JSON dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="c1766-157">The method should return a JSON representation of your object.</span></span>
> 
> 

### <a name="example"></a><span data-ttu-id="c1766-158">Esempio</span><span class="sxs-lookup"><span data-stu-id="c1766-158">Example</span></span>
    NSMutableDictionary* extras = [NSMutableDictionary dictionaryWithCapacity:2];
    [extras setObject:[NSNumber numberWithInt:123] forKey:@"video_id"];
    [extras setObject:@"http://foobar.com/blog" forKey:@"ref_click"];
    [[EngagementAgent shared] sendEvent:@"video_clicked" extras:extras];

### <a name="limits"></a><span data-ttu-id="c1766-159">Limiti</span><span class="sxs-lookup"><span data-stu-id="c1766-159">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="c1766-160">Chiavi</span><span class="sxs-lookup"><span data-stu-id="c1766-160">Keys</span></span>
<span data-ttu-id="c1766-161">Ogni chiave in `NSDictionary` deve corrispondere all'espressione regolare seguente:</span><span class="sxs-lookup"><span data-stu-id="c1766-161">Each key in the `NSDictionary` must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="c1766-162">Questo significa che le chiavi devono iniziare con almeno una lettera, seguita da lettere, cifre o caratteri di sottolineatura (\_).</span><span class="sxs-lookup"><span data-stu-id="c1766-162">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="c1766-163">Dimensione</span><span class="sxs-lookup"><span data-stu-id="c1766-163">Size</span></span>
<span data-ttu-id="c1766-164">I dati aggiuntivi sono limitati a **1024** caratteri per chiamata, una volta codificati in JSON dall'agente di Engagement.</span><span class="sxs-lookup"><span data-stu-id="c1766-164">Extras are limited to **1024** characters per call (once encoded in JSON by the Engagement agent).</span></span>

<span data-ttu-id="c1766-165">Nell'esempio precedente il codice JSON inviato al server è lungo 58 caratteri:</span><span class="sxs-lookup"><span data-stu-id="c1766-165">In the previous example, the JSON sent to the server is 58 characters long:</span></span>

    {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a><span data-ttu-id="c1766-166">Segnalazione di informazioni sull'applicazione</span><span class="sxs-lookup"><span data-stu-id="c1766-166">Reporting Application Information</span></span>
<span data-ttu-id="c1766-167">È possibile segnalare manualmente le informazioni di traccia o qualsiasi altra informazione specifica dell'applicazione mediante la funzione `sendAppInfo:` .</span><span class="sxs-lookup"><span data-stu-id="c1766-167">You can manually report tracking information (or any other application specific information) using the `sendAppInfo:` function.</span></span>

<span data-ttu-id="c1766-168">Queste informazioni possono essere inviate in modo incrementale: viene mantenuto solo l'ultimo valore per una determinata chiave per ogni dispositivo specifico.</span><span class="sxs-lookup"><span data-stu-id="c1766-168">Note that these information can be sent incrementally: only the latest value for a given key will be kept for a given device.</span></span>

<span data-ttu-id="c1766-169">Come per i dati aggiuntivi degli eventi, la classe `NSDictionary` viene usata per astrarre le informazioni sull'applicazione. Tenere presente che le matrici o i dizionari secondari vengono trattati come stringhe flat (usando la serializzazione JSON).</span><span class="sxs-lookup"><span data-stu-id="c1766-169">Like event extras, the `NSDictionary` class is used to abstract application information, note that arrays or sub-dictionaries will be treated as flat strings (using JSON serialization).</span></span>

<span data-ttu-id="c1766-170">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="c1766-170">**Example:**</span></span>

    NSMutableDictionary* appInfo = [NSMutableDictionary dictionaryWithCapacity:2];
    [appInfo setObject:@"female" forKey:@"gender"];
    [appInfo setObject:@"1983-12-07" forKey:@"birthdate"]; // December 7th 1983
    [[EngagementAgent shared] sendAppInfo:appInfo];

### <a name="limits"></a><span data-ttu-id="c1766-171">Limiti</span><span class="sxs-lookup"><span data-stu-id="c1766-171">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="c1766-172">Chiavi</span><span class="sxs-lookup"><span data-stu-id="c1766-172">Keys</span></span>
<span data-ttu-id="c1766-173">Ogni chiave in `NSDictionary` deve corrispondere all'espressione regolare seguente:</span><span class="sxs-lookup"><span data-stu-id="c1766-173">Each key in the `NSDictionary` must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="c1766-174">Questo significa che le chiavi devono iniziare con almeno una lettera, seguita da lettere, cifre o caratteri di sottolineatura (\_).</span><span class="sxs-lookup"><span data-stu-id="c1766-174">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="c1766-175">Dimensione</span><span class="sxs-lookup"><span data-stu-id="c1766-175">Size</span></span>
<span data-ttu-id="c1766-176">Le informazioni sull'applicazione sono limitate a **1024** caratteri per chiamata, una volta codificate in JSON dall'agente di Engagement.</span><span class="sxs-lookup"><span data-stu-id="c1766-176">Application information are limited to **1024** characters per call (once encoded in JSON by the Engagement agent).</span></span>

<span data-ttu-id="c1766-177">Nell'esempio precedente il codice JSON inviato al server è lungo 44 caratteri:</span><span class="sxs-lookup"><span data-stu-id="c1766-177">In the previous example, the JSON sent to the server is 44 characters long:</span></span>

    {"birthdate":"1983-12-07","gender":"female"}
