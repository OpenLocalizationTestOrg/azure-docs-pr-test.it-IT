---
title: aaaHow tooUse hello Engagement API in iOS
description: "IOS più recente SDK - come tooUse hello Engagement API in iOS"
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
ms.openlocfilehash: 7fb9b95ad319cf3b1e2de81b5d6aee5b30266069
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-ios"></a><span data-ttu-id="38b1f-103">Come tooUse hello Engagement API in iOS</span><span class="sxs-lookup"><span data-stu-id="38b1f-103">How tooUse hello Engagement API on iOS</span></span>
<span data-ttu-id="38b1f-104">Questo documento è un componente aggiuntivo toohello come tooIntegrate Engagement in iOS: fornisce informazioni approfondite su come toouse hello API Engagement tooreport le statistiche dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="38b1f-104">This document is an add-on toohello document How tooIntegrate Engagement on iOS: it provides in depth details about how toouse hello Engagement API tooreport your application statistics.</span></span>

<span data-ttu-id="38b1f-105">Tenere presente che se si desidera solo Engagement tooreport sessioni dell'applicazione, le attività, arresti anomali del sistema e informazioni tecniche, hello più semplice consiste nel toomake tutti personalizzato `UIViewController` oggetti ereditano hello corrispondente `EngagementViewController` classe .</span><span class="sxs-lookup"><span data-stu-id="38b1f-105">Keep in mind that if you only want Engagement tooreport your application's sessions, activities, crashes and technical information, then hello simplest way is toomake all your custom `UIViewController` objects inherit from hello corresponding `EngagementViewController` class.</span></span>

<span data-ttu-id="38b1f-106">Se si desidera toodo altre, ad esempio se è necessario tooreport eventi specifici di applicazione, gli errori e i processi o se hai tooreport attività dell'applicazione in modo diverso rispetto a uno implementato in hello hello `EngagementViewController` classi, è necessario toouse hello Engagement API.</span><span class="sxs-lookup"><span data-stu-id="38b1f-106">If you want toodo more, for example if you need tooreport application specific events, errors and jobs, or if you have tooreport your application's activities in a different way than hello one implemented in hello `EngagementViewController` classes, then you need toouse hello Engagement API.</span></span>

<span data-ttu-id="38b1f-107">Hello Engagement API viene fornita da hello `EngagementAgent` classe.</span><span class="sxs-lookup"><span data-stu-id="38b1f-107">hello Engagement API is provided by hello `EngagementAgent` class.</span></span> <span data-ttu-id="38b1f-108">Un'istanza di questa classe può essere recuperata dal chiamante hello `[EngagementAgent shared]` metodo statico (si noti che hello `EngagementAgent` oggetto restituito è un singleton).</span><span class="sxs-lookup"><span data-stu-id="38b1f-108">An instance of this class can be retrieved by calling hello `[EngagementAgent shared]` static method (note that hello `EngagementAgent` object returned is a singleton).</span></span>

<span data-ttu-id="38b1f-109">Prima di qualsiasi chiamate API, hello `EngagementAgent` necessario inizializzare l'oggetto chiamando il metodo hello`[EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];`</span><span class="sxs-lookup"><span data-stu-id="38b1f-109">Before any API calls, hello `EngagementAgent` object must be initialized by calling hello method `[EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];`</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="38b1f-110">Concetti relativi a Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="38b1f-110">Engagement concepts</span></span>
<span data-ttu-id="38b1f-111">parti seguenti Hello perfezionare hello comune [concetti Engagement Mobile](mobile-engagement-concepts.md) per la piattaforma iOS hello.</span><span class="sxs-lookup"><span data-stu-id="38b1f-111">hello following parts refine hello common [Mobile Engagement Concepts](mobile-engagement-concepts.md) for hello iOS platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="38b1f-112">`Session` e `Activity`</span><span class="sxs-lookup"><span data-stu-id="38b1f-112">`Session` and `Activity`</span></span>
<span data-ttu-id="38b1f-113">Un *attività* è generalmente associato a una schermata dell'applicazione hello, che è hello toosay *attività* inizia quando la schermata Ciao viene visualizzato e si arresta alla chiusura della schermata hello: si tratta di hello caso in cui Hello Engagement SDK è integrato con hello `EngagementViewController` classi.</span><span class="sxs-lookup"><span data-stu-id="38b1f-113">An *activity* is usually associated with one screen of hello application, that is toosay hello *activity* starts when hello screen is displayed and stops when hello screen is closed: this is hello case when hello Engagement SDK is integrated by using hello `EngagementViewController` classes.</span></span>

<span data-ttu-id="38b1f-114">Ma *attività* può essere controllato anche manualmente utilizzando l'API di Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="38b1f-114">But *activities* can also be controlled manually by using hello Engagement API.</span></span> <span data-ttu-id="38b1f-115">In questo modo una schermata determinata toosplit in diversi tooget di parti di sub hello di ulteriori dettagli sull'utilizzo di questa schermata (ad esempio la frequenza con cui tooknown e per quanto tempo, all'interno di questa schermata, vengono utilizzate le finestre di dialogo).</span><span class="sxs-lookup"><span data-stu-id="38b1f-115">This allows toosplit a given screen in several sub parts tooget more details about hello usage of this screen (for example tooknown how often and how long dialogs are used inside this screen).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="38b1f-116">Segnalazione di attività</span><span class="sxs-lookup"><span data-stu-id="38b1f-116">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="38b1f-117">L'utente inizia una nuova attività</span><span class="sxs-lookup"><span data-stu-id="38b1f-117">User starts a new Activity</span></span>
            [[EngagementAgent shared] startActivity:@"MyUserActivity" extras:nil];

<span data-ttu-id="38b1f-118">È necessario toocall `startActivity()` ogni attività utente hello in fase di modifica.</span><span class="sxs-lookup"><span data-stu-id="38b1f-118">You need toocall `startActivity()` each time hello user activity changes.</span></span> <span data-ttu-id="38b1f-119">Hello prima chiamata toothis funzione avvia una nuova sessione utente.</span><span class="sxs-lookup"><span data-stu-id="38b1f-119">hello first call toothis function starts a new user session.</span></span>

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="38b1f-120">L'utente termina l'attività corrente</span><span class="sxs-lookup"><span data-stu-id="38b1f-120">User ends his current Activity</span></span>
            [[EngagementAgent shared] endActivity];

> [!WARNING]
> <span data-ttu-id="38b1f-121">È necessario **mai** chiamare questa funzione personalmente, tranne se si desidera toosplit un utilizzo dell'applicazione in diverse sessioni: una chiamata di funzione toothis interromperebbe hello la sessione corrente immediatamente, pertanto, una chiamata successiva troppo`startActivity()`avvia una nuova sessione.</span><span class="sxs-lookup"><span data-stu-id="38b1f-121">You should **NEVER** call this function by yourself, except if you want toosplit one use of your application into several sessions: a call toothis function would end hello current session immediately, so, a subsequent call too`startActivity()` would start a new session.</span></span> <span data-ttu-id="38b1f-122">Questa funzione viene chiamata automaticamente da hello SDK alla chiusura dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="38b1f-122">This function is automatically called by hello SDK when your application is closed.</span></span>
> 
> 

## <a name="reporting-events"></a><span data-ttu-id="38b1f-123">Segnalazione di eventi</span><span class="sxs-lookup"><span data-stu-id="38b1f-123">Reporting Events</span></span>
### <a name="session-events"></a><span data-ttu-id="38b1f-124">Eventi di sessione</span><span class="sxs-lookup"><span data-stu-id="38b1f-124">Session events</span></span>
<span data-ttu-id="38b1f-125">Gli eventi di sessione sono azioni hello tooreport utilizzati in genere eseguite da un utente durante la sessione.</span><span class="sxs-lookup"><span data-stu-id="38b1f-125">Session events are usually used tooreport hello actions performed by a user during his session.</span></span>

<span data-ttu-id="38b1f-126">**Esempio senza dati aggiuntivi:**</span><span class="sxs-lookup"><span data-stu-id="38b1f-126">**Example without extra data:**</span></span>

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

<span data-ttu-id="38b1f-127">**Esempio con dati aggiuntivi:**</span><span class="sxs-lookup"><span data-stu-id="38b1f-127">**Example with extra data:**</span></span>

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

### <a name="standalone-events"></a><span data-ttu-id="38b1f-128">Eventi autonomi</span><span class="sxs-lookup"><span data-stu-id="38b1f-128">Standalone events</span></span>
<span data-ttu-id="38b1f-129">Eventi di toosession contrarie, autonoma eventi possono essere usati all'esterno di contesto hello di una sessione.</span><span class="sxs-lookup"><span data-stu-id="38b1f-129">Contrary toosession events, standalone events can be used outside of hello context of a session.</span></span>

<span data-ttu-id="38b1f-130">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="38b1f-130">**Example:**</span></span>

    [[EngagementAgent shared] sendEvent:@"received_notification" extras:nil];

## <a name="reporting-errors"></a><span data-ttu-id="38b1f-131">Segnalazione di errori</span><span class="sxs-lookup"><span data-stu-id="38b1f-131">Reporting Errors</span></span>
### <a name="session-errors"></a><span data-ttu-id="38b1f-132">Errori di sessione</span><span class="sxs-lookup"><span data-stu-id="38b1f-132">Session errors</span></span>
<span data-ttu-id="38b1f-133">Sessione gli errori in genere utilizzato tooreport hello conseguenze utente hello durante la sessione.</span><span class="sxs-lookup"><span data-stu-id="38b1f-133">Session errors are usually used tooreport hello errors impacting hello user during his session.</span></span>

<span data-ttu-id="38b1f-134">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="38b1f-134">**Example:**</span></span>

    /** hello user has entered invalid data in a form */
    @implementation MyViewController {
      [...]
      -(void)onMyFormSubmitted:(MyForm*)form {
        [...]
        /* hello user has entered an invalid email address */
        [[EngagementAgent shared] sendSessionError:@"sign_up_email" extras:nil]
        [...]
      }
      [...]
    }

### <a name="standalone-errors"></a><span data-ttu-id="38b1f-135">Errori autonomi</span><span class="sxs-lookup"><span data-stu-id="38b1f-135">Standalone errors</span></span>
<span data-ttu-id="38b1f-136">Errori toosession contrarie, autonomo possono essere utilizzati all'esterno di contesto hello di una sessione.</span><span class="sxs-lookup"><span data-stu-id="38b1f-136">Contrary toosession errors, standalone errors can be used outside of hello context of a session.</span></span>

<span data-ttu-id="38b1f-137">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="38b1f-137">**Example:**</span></span>

    [[EngagementAgent shared] sendError:@"something_failed" extras:nil];

## <a name="reporting-jobs"></a><span data-ttu-id="38b1f-138">Segnalazione di processi</span><span class="sxs-lookup"><span data-stu-id="38b1f-138">Reporting Jobs</span></span>
<span data-ttu-id="38b1f-139">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="38b1f-139">**Example:**</span></span>

<span data-ttu-id="38b1f-140">Si supponga che si desidera tooreport hello durata del processo di accesso:</span><span class="sxs-lookup"><span data-stu-id="38b1f-140">Suppose you want tooreport hello duration of your login process:</span></span>

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

### <a name="report-errors-during-a-job"></a><span data-ttu-id="38b1f-141">Segnalazione di errori durante un processo</span><span class="sxs-lookup"><span data-stu-id="38b1f-141">Report Errors during a Job</span></span>
<span data-ttu-id="38b1f-142">Gli errori possono essere correlato tooa esecuzione processo anziché essere correlate toohello sessione utente.</span><span class="sxs-lookup"><span data-stu-id="38b1f-142">Errors can be related tooa running job instead of being related toohello current user session.</span></span>

<span data-ttu-id="38b1f-143">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="38b1f-143">**Example:**</span></span>

<span data-ttu-id="38b1f-144">Si supponga di che voler tooreport un errore durante il processo di accesso:</span><span class="sxs-lookup"><span data-stu-id="38b1f-144">Suppose you want tooreport an error during your login process:</span></span>

    [...]
    -(void)signin
    {
      /* Start job */
      [[EngagementAgent shared] startJob:@"sign_in" extras:nil];

      BOOL success = NO;
      while (!success) {
        /* Try toosign in */
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

### <a name="events-during-a-job"></a><span data-ttu-id="38b1f-145">Eventi durante un processo</span><span class="sxs-lookup"><span data-stu-id="38b1f-145">Events during a job</span></span>
<span data-ttu-id="38b1f-146">Gli eventi possono essere correlato tooa esecuzione processo anziché essere correlate toohello sessione utente.</span><span class="sxs-lookup"><span data-stu-id="38b1f-146">Events can be related tooa running job instead of being related toohello current user session.</span></span>

<span data-ttu-id="38b1f-147">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="38b1f-147">**Example:**</span></span>

<span data-ttu-id="38b1f-148">Si supponga che abbiamo un social network ed è possibile usare un processo tooreport hello totale tempo durante cui hello utente è connesso toohello server.</span><span class="sxs-lookup"><span data-stu-id="38b1f-148">Suppose we have a social network, and we use a job tooreport hello total time during which hello user is connected toohello server.</span></span> <span data-ttu-id="38b1f-149">utente Hello può ricevere messaggi dai suoi amici, si tratta di un evento di processo.</span><span class="sxs-lookup"><span data-stu-id="38b1f-149">hello user can receive messages from his friends, this is a job event.</span></span>

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

## <a name="extra-parameters"></a><span data-ttu-id="38b1f-150">Parametri aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="38b1f-150">Extra parameters</span></span>
<span data-ttu-id="38b1f-151">Dati arbitrari possono essere collegati tooevents, errori, le attività e processi.</span><span class="sxs-lookup"><span data-stu-id="38b1f-151">Arbitrary data can be attached tooevents, errors, activities and jobs.</span></span>

<span data-ttu-id="38b1f-152">Questi dati possono essere strutturati e utilizzano la classe NSDictionary di iOS.</span><span class="sxs-lookup"><span data-stu-id="38b1f-152">This data can be structured, it uses iOS's NSDictionary class.</span></span>

<span data-ttu-id="38b1f-153">Tenere presente che i dati aggiuntivi possono includere `arrays(NSArray, NSMutableArray)`, `numbers(NSNumber class)`, `strings(NSString, NSMutableString)`, `urls(NSURL)`, `data(NSData, NSMutableData)` o altre istanze di `NSDictionary`.</span><span class="sxs-lookup"><span data-stu-id="38b1f-153">Note that extras can contain `arrays(NSArray, NSMutableArray)`, `numbers(NSNumber class)`, `strings(NSString, NSMutableString)`, `urls(NSURL)`, `data(NSData, NSMutableData)` or other `NSDictionary` instances.</span></span>

> [!NOTE]
> <span data-ttu-id="38b1f-154">parametro aggiuntivo Hello viene serializzato in JSON.</span><span class="sxs-lookup"><span data-stu-id="38b1f-154">hello extra parameter is serialized in JSON.</span></span> <span data-ttu-id="38b1f-155">Se si desidera toopass oggetti diversi rispetto a quelli descritti sopra hello, è necessario implementare hello metodo nella classe seguente:</span><span class="sxs-lookup"><span data-stu-id="38b1f-155">If you want toopass different objects than hello ones described above, you must implement hello following method in your class:</span></span>
> 
> <span data-ttu-id="38b1f-156">-(NSString*)JSONRepresentation;</span><span class="sxs-lookup"><span data-stu-id="38b1f-156">-(NSString*)JSONRepresentation;</span></span>
> 
> <span data-ttu-id="38b1f-157">metodo Hello deve restituire la rappresentazione JSON dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="38b1f-157">hello method should return a JSON representation of your object.</span></span>
> 
> 

### <a name="example"></a><span data-ttu-id="38b1f-158">Esempio</span><span class="sxs-lookup"><span data-stu-id="38b1f-158">Example</span></span>
    NSMutableDictionary* extras = [NSMutableDictionary dictionaryWithCapacity:2];
    [extras setObject:[NSNumber numberWithInt:123] forKey:@"video_id"];
    [extras setObject:@"http://foobar.com/blog" forKey:@"ref_click"];
    [[EngagementAgent shared] sendEvent:@"video_clicked" extras:extras];

### <a name="limits"></a><span data-ttu-id="38b1f-159">Limiti</span><span class="sxs-lookup"><span data-stu-id="38b1f-159">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="38b1f-160">Chiavi</span><span class="sxs-lookup"><span data-stu-id="38b1f-160">Keys</span></span>
<span data-ttu-id="38b1f-161">Ogni chiave hello `NSDictionary` deve corrispondere hello espressione regolare seguente:</span><span class="sxs-lookup"><span data-stu-id="38b1f-161">Each key in hello `NSDictionary` must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="38b1f-162">Questo significa che le chiavi devono iniziare con almeno una lettera, seguita da lettere, cifre o caratteri di sottolineatura (\_).</span><span class="sxs-lookup"><span data-stu-id="38b1f-162">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="38b1f-163">Dimensione</span><span class="sxs-lookup"><span data-stu-id="38b1f-163">Size</span></span>
<span data-ttu-id="38b1f-164">Funzionalità aggiuntive sono troppo limitate**1024** caratteri per ogni chiamata (una volta codificato in JSON dall'agente di Engagement hello).</span><span class="sxs-lookup"><span data-stu-id="38b1f-164">Extras are limited too**1024** characters per call (once encoded in JSON by hello Engagement agent).</span></span>

<span data-ttu-id="38b1f-165">In hello esempio precedente, hello JSON inviato server toohello è 58 caratteri:</span><span class="sxs-lookup"><span data-stu-id="38b1f-165">In hello previous example, hello JSON sent toohello server is 58 characters long:</span></span>

    {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a><span data-ttu-id="38b1f-166">Segnalazione di informazioni sull'applicazione</span><span class="sxs-lookup"><span data-stu-id="38b1f-166">Reporting Application Information</span></span>
<span data-ttu-id="38b1f-167">È possibile segnalare manualmente traccia informazioni o qualsiasi altra informazione di specifici dell'applicazione mediante hello `sendAppInfo:` (funzione).</span><span class="sxs-lookup"><span data-stu-id="38b1f-167">You can manually report tracking information (or any other application specific information) using hello `sendAppInfo:` function.</span></span>

<span data-ttu-id="38b1f-168">Si noti che queste informazioni possono essere inviate in modo incrementale: solo hello valore più recente per una determinata chiave verrà conservati per un determinato dispositivo.</span><span class="sxs-lookup"><span data-stu-id="38b1f-168">Note that these information can be sent incrementally: only hello latest value for a given key will be kept for a given device.</span></span>

<span data-ttu-id="38b1f-169">Ad esempio funzionalità aggiuntive di evento, hello `NSDictionary` classe è usato tooabstract informazioni dell'applicazione, tenere presente che le matrici o dizionari secondari verranno considerati come stringhe flat (con la serializzazione JSON).</span><span class="sxs-lookup"><span data-stu-id="38b1f-169">Like event extras, hello `NSDictionary` class is used tooabstract application information, note that arrays or sub-dictionaries will be treated as flat strings (using JSON serialization).</span></span>

<span data-ttu-id="38b1f-170">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="38b1f-170">**Example:**</span></span>

    NSMutableDictionary* appInfo = [NSMutableDictionary dictionaryWithCapacity:2];
    [appInfo setObject:@"female" forKey:@"gender"];
    [appInfo setObject:@"1983-12-07" forKey:@"birthdate"]; // December 7th 1983
    [[EngagementAgent shared] sendAppInfo:appInfo];

### <a name="limits"></a><span data-ttu-id="38b1f-171">Limiti</span><span class="sxs-lookup"><span data-stu-id="38b1f-171">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="38b1f-172">Chiavi</span><span class="sxs-lookup"><span data-stu-id="38b1f-172">Keys</span></span>
<span data-ttu-id="38b1f-173">Ogni chiave hello `NSDictionary` deve corrispondere hello espressione regolare seguente:</span><span class="sxs-lookup"><span data-stu-id="38b1f-173">Each key in hello `NSDictionary` must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="38b1f-174">Questo significa che le chiavi devono iniziare con almeno una lettera, seguita da lettere, cifre o caratteri di sottolineatura (\_).</span><span class="sxs-lookup"><span data-stu-id="38b1f-174">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="38b1f-175">Dimensione</span><span class="sxs-lookup"><span data-stu-id="38b1f-175">Size</span></span>
<span data-ttu-id="38b1f-176">Informazioni sull'applicazione sono troppo limitati**1024** caratteri per ogni chiamata (una volta codificato in JSON dall'agente di Engagement hello).</span><span class="sxs-lookup"><span data-stu-id="38b1f-176">Application information are limited too**1024** characters per call (once encoded in JSON by hello Engagement agent).</span></span>

<span data-ttu-id="38b1f-177">In hello esempio precedente, hello JSON inviato server toohello è 44 caratteri:</span><span class="sxs-lookup"><span data-stu-id="38b1f-177">In hello previous example, hello JSON sent toohello server is 44 characters long:</span></span>

    {"birthdate":"1983-12-07","gender":"female"}
