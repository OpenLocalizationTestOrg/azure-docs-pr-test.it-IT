---
title: aaaHow tooUse hello Engagement API in Android
description: "Android SDK più recente - come tooUse hello Engagement API in Android"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 09b62659-82ae-4a55-8784-fca0b6b22eaf
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: na
ms.topic: article
ms.date: 07/25/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: e0b2d484616c0c7874e77c5283d94c3063949ed2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-android"></a><span data-ttu-id="96202-103">Come tooUse hello Engagement API in Android</span><span class="sxs-lookup"><span data-stu-id="96202-103">How tooUse hello Engagement API on Android</span></span>
<span data-ttu-id="96202-104">Questo documento è un componente aggiuntivo toohello [opzioni avanzate di segnalazione per Android Mobile Engagement SDK](mobile-engagement-android-advanced-reporting.md).</span><span class="sxs-lookup"><span data-stu-id="96202-104">This document is an add-on toohello document [Advanced Reporting options for Android Mobile Engagement SDK](mobile-engagement-android-advanced-reporting.md).</span></span> <span data-ttu-id="96202-105">Fornisce informazioni approfondite su come toouse hello API Engagement tooreport le statistiche dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="96202-105">It provides in depth details about how toouse hello Engagement API tooreport your application statistics.</span></span>

<span data-ttu-id="96202-106">Tenere presente che se si vuole solo Engagement tooreport sessioni dell'applicazione, le attività, arresti anomali del sistema e informazioni tecniche, quindi hello semplice toomake tutti i `Activity` sottoclassi ereditano hello corrispondente `EngagementActivity` classe.</span><span class="sxs-lookup"><span data-stu-id="96202-106">Keep in mind that if you only want Engagement tooreport your application's sessions, activities, crashes and technical information, then hello simplest way is toomake all your `Activity` sub-classes inherit from hello corresponding `EngagementActivity` class.</span></span>

<span data-ttu-id="96202-107">Se si desidera toodo altre, ad esempio se è necessario tooreport eventi specifici di applicazione, gli errori e i processi o se hai tooreport attività dell'applicazione in modo diverso rispetto a uno implementato in hello hello `EngagementActivity` classi, è necessario toouse hello Engagement API.</span><span class="sxs-lookup"><span data-stu-id="96202-107">If you want toodo more, for example if you need tooreport application specific events, errors and jobs, or if you have tooreport your application's activities in a different way than hello one implemented in hello `EngagementActivity` classes, then you need toouse hello Engagement API.</span></span>

<span data-ttu-id="96202-108">Hello Engagement API viene fornita da hello `EngagementAgent` classe.</span><span class="sxs-lookup"><span data-stu-id="96202-108">hello Engagement API is provided by hello `EngagementAgent` class.</span></span> <span data-ttu-id="96202-109">Un'istanza di questa classe può essere recuperata dal chiamante hello `EngagementAgent.getInstance(Context)` metodo statico (si noti che hello `EngagementAgent` oggetto restituito è un singleton).</span><span class="sxs-lookup"><span data-stu-id="96202-109">An instance of this class can be retrieved by calling hello `EngagementAgent.getInstance(Context)` static method (note that hello `EngagementAgent` object returned is a singleton).</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="96202-110">Concetti relativi a Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="96202-110">Engagement concepts</span></span>
<span data-ttu-id="96202-111">parti seguenti Hello perfezionare hello comune [concetti Engagement Mobile](mobile-engagement-concepts.md), per la piattaforma Android hello.</span><span class="sxs-lookup"><span data-stu-id="96202-111">hello following parts refine hello common [Mobile Engagement Concepts](mobile-engagement-concepts.md), for hello Android platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="96202-112">`Session` e `Activity`</span><span class="sxs-lookup"><span data-stu-id="96202-112">`Session` and `Activity`</span></span>
<span data-ttu-id="96202-113">Se più di pochi secondi di inattività tra due hello rimane *attività*, quindi la sequenza di *attività* è divisa in due distinti *sessioni*.</span><span class="sxs-lookup"><span data-stu-id="96202-113">If hello user stays more than a few seconds idle between two *activities*, then his sequence of *activities* is split in two distinct *sessions*.</span></span> <span data-ttu-id="96202-114">Questi alcuni secondi vengono chiamati hello "timeout della sessione".</span><span class="sxs-lookup"><span data-stu-id="96202-114">These few seconds are called hello "session timeout".</span></span>

<span data-ttu-id="96202-115">Un *attività* è generalmente associato a una schermata dell'applicazione hello, che è hello toosay *attività* inizia quando la schermata Ciao viene visualizzato e si arresta alla chiusura della schermata hello: si tratta di hello caso in cui Hello Engagement SDK è integrato con hello `EngagementActivity` classi.</span><span class="sxs-lookup"><span data-stu-id="96202-115">An *activity* is usually associated with one screen of hello application, that is toosay hello *activity* starts when hello screen is displayed and stops when hello screen is closed: this is hello case when hello Engagement SDK is integrated by using hello `EngagementActivity` classes.</span></span>

<span data-ttu-id="96202-116">Ma *attività* può essere controllato anche manualmente utilizzando l'API di Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="96202-116">But *activities* can also be controlled manually by using hello Engagement API.</span></span> <span data-ttu-id="96202-117">In questo modo una schermata determinata toosplit in diversi tooget di parti di sub hello di ulteriori dettagli sull'utilizzo di questa schermata (ad esempio la frequenza con cui tooknown e per quanto tempo, all'interno di questa schermata, vengono utilizzate le finestre di dialogo).</span><span class="sxs-lookup"><span data-stu-id="96202-117">This allows toosplit a given screen in several sub parts tooget more details about hello usage of this screen (for example tooknown how often and how long dialogs are used inside this screen).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="96202-118">Segnalazione di attività</span><span class="sxs-lookup"><span data-stu-id="96202-118">Reporting Activities</span></span>
> [!IMPORTANT]
> <span data-ttu-id="96202-119">Non è necessario tooreport le attività, come descritto in questa sezione se si utilizza hello `EngagementActivity` classe e le sue varianti, come illustrato in hello tooIntegrate Engagement documento Android.</span><span class="sxs-lookup"><span data-stu-id="96202-119">You don't need tooreport activities like described in this section if you are using hello `EngagementActivity` class and its variants as explained in hello How tooIntegrate Engagement on Android document.</span></span>
> 
> 

### <a name="user-starts-a-new-activity"></a><span data-ttu-id="96202-120">L'utente inizia una nuova attività</span><span class="sxs-lookup"><span data-stu-id="96202-120">User starts a new Activity</span></span>
            EngagementAgent.getInstance(this).startActivity(this, "MyUserActivity", null);
            // Passing hello current activity is required for Reach toodisplay in-app notifications, passing null will postpone such announcements and polls.

<span data-ttu-id="96202-121">È necessario toocall `startActivity()` ogni attività utente hello in fase di modifica.</span><span class="sxs-lookup"><span data-stu-id="96202-121">You need toocall `startActivity()` each time hello user activity changes.</span></span> <span data-ttu-id="96202-122">Hello prima chiamata toothis funzione avvia una nuova sessione utente.</span><span class="sxs-lookup"><span data-stu-id="96202-122">hello first call toothis function starts a new user session.</span></span>

<span data-ttu-id="96202-123">Hello migliore toocall sul posto questa funzione è in ogni attività `onResume` callback.</span><span class="sxs-lookup"><span data-stu-id="96202-123">hello best place toocall this function is on each activity `onResume` callback.</span></span>

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="96202-124">L'utente termina l'attività corrente</span><span class="sxs-lookup"><span data-stu-id="96202-124">User ends his current Activity</span></span>
            EngagementAgent.getInstance(this).endActivity();

<span data-ttu-id="96202-125">È necessario toocall `endActivity()` almeno una volta al termine della sua attività ultimo utente hello.</span><span class="sxs-lookup"><span data-stu-id="96202-125">You need toocall `endActivity()` at least once when hello user finishes his last activity.</span></span> <span data-ttu-id="96202-126">Informa hello scadrà Engagement SDK che utente hello è attualmente inattivo e che la sessione di utente hello necessario toobe chiuso una volta hello timeout della sessione (se si chiama `startActivity()` prima della scadenza del timeout della sessione hello, sessione hello viene semplicemente ripreso).</span><span class="sxs-lookup"><span data-stu-id="96202-126">This informs hello Engagement SDK that hello user is currently idle, and that hello user session need toobe closed once hello session timeout will expire (if you call `startActivity()` before hello session timeout expires, hello session is simply resumed).</span></span>

<span data-ttu-id="96202-127">Hello migliore toocall sul posto questa funzione è in ogni attività `onPause` callback.</span><span class="sxs-lookup"><span data-stu-id="96202-127">hello best place toocall this function is on each activity `onPause` callback.</span></span>

## <a name="reporting-events"></a><span data-ttu-id="96202-128">Segnalazione di eventi</span><span class="sxs-lookup"><span data-stu-id="96202-128">Reporting Events</span></span>
### <a name="session-events"></a><span data-ttu-id="96202-129">Eventi di sessione</span><span class="sxs-lookup"><span data-stu-id="96202-129">Session events</span></span>
<span data-ttu-id="96202-130">Gli eventi di sessione sono azioni hello tooreport utilizzati in genere eseguite da un utente durante la sessione.</span><span class="sxs-lookup"><span data-stu-id="96202-130">Session events are usually used tooreport hello actions performed by a user during his session.</span></span>

<span data-ttu-id="96202-131">**Esempio senza dati aggiuntivi:**</span><span class="sxs-lookup"><span data-stu-id="96202-131">**Example without extra data:**</span></span>

            public MyActivity extends EngagementActivity {
               [...]
               @Override
               public boolean onPrepareOptionsMenu(Menu menu) {
                  getEngagementAgent().sendSessionEvent("menu_shown", null);
               }
               [...]
            }

<span data-ttu-id="96202-132">**Esempio con dati aggiuntivi:**</span><span class="sxs-lookup"><span data-stu-id="96202-132">**Example with extra data:**</span></span>

            public MyActivity extends EngagementActivity {
              [...]
              @Override
              public boolean onMenuItemSelected(int featureId, MenuItem item) {
                Bundle extras = new Bundle();
                extras.putInt("id", item.getItemId());
                getEngagementAgent().sendSessionEvent("menu_selected", extras);
              }
              [...]
            }

### <a name="standalone-events"></a><span data-ttu-id="96202-133">Eventi autonomi</span><span class="sxs-lookup"><span data-stu-id="96202-133">Standalone Events</span></span>
<span data-ttu-id="96202-134">Di fuori di contesto hello di una sessione possono verificarsi eventi di toosession contrarie, gli eventi autonomo.</span><span class="sxs-lookup"><span data-stu-id="96202-134">Contrary toosession events, standalone events can occur outside of hello context of a session.</span></span>

<span data-ttu-id="96202-135">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="96202-135">**Example:**</span></span>

<span data-ttu-id="96202-136">Si supponga di che voler tooreport eventi che si verificano quando viene attivato un ricevitore di trasmissione:</span><span class="sxs-lookup"><span data-stu-id="96202-136">Suppose you want tooreport events occurring when a broadcast receiver is triggered:</span></span>

            /** Triggered by Intent.ACTION_BATTERY_LOW */
            public BatteryLowReceiver extends BroadcastReceiver {
              [...]
              @Override
              public void onReceive(Context context, Intent intent) {
                EngagementAgent.getInstance(context).sendEvent("battery_low", null);
              }
              [...]
            }

## <a name="reporting-errors"></a><span data-ttu-id="96202-137">Segnalazione di errori</span><span class="sxs-lookup"><span data-stu-id="96202-137">Reporting Errors</span></span>
### <a name="session-errors"></a><span data-ttu-id="96202-138">Errori di sessione</span><span class="sxs-lookup"><span data-stu-id="96202-138">Session errors</span></span>
<span data-ttu-id="96202-139">Sessione gli errori in genere utilizzato tooreport hello conseguenze utente hello durante la sessione.</span><span class="sxs-lookup"><span data-stu-id="96202-139">Session errors are usually used tooreport hello errors impacting hello user during his session.</span></span>

<span data-ttu-id="96202-140">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="96202-140">**Example:**</span></span>

            /** hello user has entered invalid data in a form */
            public MyActivity extends EngagementActivity {
              [...]
              public void onMyFormSubmitted(MyForm form) {
                [...]
                /* hello user has entered an invalid email address */
                getEngagementAgent().sendSessionError("sign_up_email", null);
                [...]
              }
              [...]
            }

### <a name="standalone-errors"></a><span data-ttu-id="96202-141">Errori autonomi</span><span class="sxs-lookup"><span data-stu-id="96202-141">Standalone errors</span></span>
<span data-ttu-id="96202-142">Di fuori di contesto hello di una sessione possono verificarsi errori di toosession contrarie, errori autonomo.</span><span class="sxs-lookup"><span data-stu-id="96202-142">Contrary toosession errors, standalone errors can occur outside of hello context of a session.</span></span>

<span data-ttu-id="96202-143">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="96202-143">**Example:**</span></span>

<span data-ttu-id="96202-144">Hello esempio seguente viene illustrato come tooreport errore ogni volta che la memoria hello diventa insufficiente phone hello durante il processo di applicazione è in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="96202-144">hello following example shows how tooreport an error whenever hello memory becomes low on hello phone while your application process is running.</span></span>

            public MyApplication extends EngagementApplication {

              @Override
              protected void onApplicationProcessLowMemory() {
                EngagementAgent.getInstance(this).sendError("low_memory", null);
              }
            }

## <a name="reporting-jobs"></a><span data-ttu-id="96202-145">Segnalazione di processi</span><span class="sxs-lookup"><span data-stu-id="96202-145">Reporting Jobs</span></span>
### <a name="example"></a><span data-ttu-id="96202-146">Esempio</span><span class="sxs-lookup"><span data-stu-id="96202-146">Example</span></span>
<span data-ttu-id="96202-147">Si supponga che si desidera tooreport hello durata del processo di accesso:</span><span class="sxs-lookup"><span data-stu-id="96202-147">Suppose you want tooreport hello duration of your login process:</span></span>

            [...]
            public void signIn(Context context, ...) {

              /* We need an Android context toocall hello Engagement API, if you are extending Activity, Service, you can pass "this" */
              EngagementAgent engagementAgent = EngagementAgent.getInstance(context);

              /* Report sign in job has started */
              engagementAgent.startJob("sign_in", null);

              [... sign in ...]

              /* Report sign in job is now ended */
              engagementAgent.endJob("sign_in");
            }
            [...]

### <a name="report-errors-during-a-job"></a><span data-ttu-id="96202-148">Segnalazione di errori durante un processo</span><span class="sxs-lookup"><span data-stu-id="96202-148">Report Errors during a Job</span></span>
<span data-ttu-id="96202-149">Gli errori possono essere correlato tooa esecuzione processo anziché essere correlate toohello sessione utente.</span><span class="sxs-lookup"><span data-stu-id="96202-149">Errors can be related tooa running job instead of being related toohello current user session.</span></span>

<span data-ttu-id="96202-150">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="96202-150">**Example:**</span></span>

<span data-ttu-id="96202-151">Si supponga che si desidera tooreport un errore durante la si accesso processo:</span><span class="sxs-lookup"><span data-stu-id="96202-151">Suppose you want tooreport an error during you login process:</span></span>

<span data-ttu-id="96202-152">[...] public void signIn(Context context, ...) {</span><span class="sxs-lookup"><span data-stu-id="96202-152">[...] public void signIn(Context context, ...) {</span></span>

              /* We need an Android context toocall hello Engagement API, if you are extending Activity, Service, you can pass "this" */
              EngagementAgent engagementAgent = EngagementAgent.getInstance(context);

              /* Report sign in job has been started */
              engagementAgent.startJob("sign_in", null);

              /* Try toosign in */
              while(true)
                try {
                  trySignin();
                  break;
                }
                catch(Exception e) {
                  /* Report hello error tooEngagement */
                  engagementAgent.sendJobError("sign_in_error", "sign_in", null);

                  /* Retry after a moment */
                  sleep(2000);
                }
              [...]
              /* Report sign in job is now ended */
              engagementAgent.endJob("sign_in");
            }
            [...]

### <a name="reporting-events-during-a-job"></a><span data-ttu-id="96202-153">Segnalazione di eventi durante un processo</span><span class="sxs-lookup"><span data-stu-id="96202-153">Reporting Events during a job</span></span>
<span data-ttu-id="96202-154">Gli eventi possono essere correlato tooa esecuzione processo anziché essere correlate toohello sessione utente.</span><span class="sxs-lookup"><span data-stu-id="96202-154">Events can be related tooa running job instead of being related toohello current user session.</span></span>

<span data-ttu-id="96202-155">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="96202-155">**Example:**</span></span>

<span data-ttu-id="96202-156">Si supponga che abbiamo un social network ed è possibile usare un processo tooreport hello totale tempo durante cui hello utente è connesso toohello server.</span><span class="sxs-lookup"><span data-stu-id="96202-156">Suppose we have a social network, and we use a job tooreport hello total time during which hello user is connected toohello server.</span></span> <span data-ttu-id="96202-157">utente Hello può rimanere connessi in background anche quando si utilizza un'altra applicazione o quando è inattivo phone hello, pertanto non c'è alcuna sessione.</span><span class="sxs-lookup"><span data-stu-id="96202-157">hello user can stay connected in background even when he's using another application or when hello phone is sleeping, so there is no session.</span></span>

<span data-ttu-id="96202-158">utente Hello può ricevere messaggi dai suoi amici, si tratta di un evento di processo.</span><span class="sxs-lookup"><span data-stu-id="96202-158">hello user can receive messages from his friends, this is a job event.</span></span>

            [...]
            public void signin(Context context, ...) {
              [...Sign in code...]
              EngagementAgent.getInstance(context).startJob("connection", null);
            }
            [...]
            public void signout(Context context) {
              [...Sign out code...]
              EngagementAgent.getInstance(context).endJob("connection");
            }
            [...]
            public void onMessageReceived(Context context) {
              [...Notify in status bar...]
              EngagementAgent.getInstance(context).sendJobEvent("message_received", "connection", null);
            }
            [...]

## <a name="extra-parameters"></a><span data-ttu-id="96202-159">Parametri aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="96202-159">Extra parameters</span></span>
<span data-ttu-id="96202-160">Dati arbitrari possono essere collegati tooevents, errori, le attività e processi.</span><span class="sxs-lookup"><span data-stu-id="96202-160">Arbitrary data can be attached tooevents, errors, activities and jobs.</span></span>

<span data-ttu-id="96202-161">Questi dati possono essere strutturati, usando la classe Bundle di Android (in realtà, funziona come i parametri aggiuntivi negli intenti di Android).</span><span class="sxs-lookup"><span data-stu-id="96202-161">This data can be structured, it uses Android's Bundle class (actually, it works like extra parameters in Android Intents).</span></span> <span data-ttu-id="96202-162">Notare che una classe Bundle può contenere matrici o altre istanze Bundle.</span><span class="sxs-lookup"><span data-stu-id="96202-162">Note that a Bundle can contain arrays or another Bundle instances.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="96202-163">Se si inserisce in parametri parcelable o serializable, assicurarsi che i relativi `toString()` metodo è implementato tooreturn una stringa leggibile.</span><span class="sxs-lookup"><span data-stu-id="96202-163">If you put in parcelable or serializable parameters, make sure their `toString()` method is implemented tooreturn a human-readable string.</span></span> <span data-ttu-id="96202-164">Le classi serializzabili che contengono campi non temporanei non serializzabili provocano l'arresto anomalo di Android quando si chiama `bundle.putSerializable("key",value);`</span><span class="sxs-lookup"><span data-stu-id="96202-164">Serializable classes that contain non transient fields that are not serializable will make Android crash when you will call `bundle.putSerializable("key",value);`</span></span>
> 
> [!WARNING]
> <span data-ttu-id="96202-165">Le matrici di tipo sparse non sono supportate nei parametri aggiuntivi, ovvero non vengono serializzate come matrice.</span><span class="sxs-lookup"><span data-stu-id="96202-165">Sparse arrays in extra parameters are not supported, that is, it won't be serialized as an array.</span></span> <span data-ttu-id="96202-166">Prima di usarle nei parametri aggiuntivi, è consigliabile convertirle in matrici standard.</span><span class="sxs-lookup"><span data-stu-id="96202-166">You should convert them into standard arrays before using it in extra parameters.</span></span>
> 
> 

### <a name="example"></a><span data-ttu-id="96202-167">Esempio</span><span class="sxs-lookup"><span data-stu-id="96202-167">Example</span></span>
            Bundle extras = new Bundle();
            extras.putString("video_id", 123);
            extras.putString("ref_click", "http://foobar.com/blog");
            EngagementAgent.getInstance(context).sendEvent("video_clicked", extras);

### <a name="limits"></a><span data-ttu-id="96202-168">Limiti</span><span class="sxs-lookup"><span data-stu-id="96202-168">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="96202-169">Chiavi</span><span class="sxs-lookup"><span data-stu-id="96202-169">Keys</span></span>
<span data-ttu-id="96202-170">Ogni chiave hello `Bundle` deve corrispondere hello espressione regolare seguente:</span><span class="sxs-lookup"><span data-stu-id="96202-170">Each key in hello `Bundle` must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="96202-171">Questo significa che le chiavi devono iniziare con almeno una lettera, seguita da lettere, cifre o caratteri di sottolineatura (\_).</span><span class="sxs-lookup"><span data-stu-id="96202-171">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="96202-172">Dimensione</span><span class="sxs-lookup"><span data-stu-id="96202-172">Size</span></span>
<span data-ttu-id="96202-173">Funzionalità aggiuntive sono troppo limitate**1024** caratteri per ogni chiamata (una volta codificato in JSON dal servizio di Engagement hello).</span><span class="sxs-lookup"><span data-stu-id="96202-173">Extras are limited too**1024** characters per call (once encoded in JSON by hello Engagement service).</span></span>

<span data-ttu-id="96202-174">In hello esempio precedente, hello JSON inviato server toohello è 58 caratteri:</span><span class="sxs-lookup"><span data-stu-id="96202-174">In hello previous example, hello JSON sent toohello server is 58 characters long:</span></span>

            {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a><span data-ttu-id="96202-175">Segnalazione di informazioni sull'applicazione</span><span class="sxs-lookup"><span data-stu-id="96202-175">Reporting Application Information</span></span>
<span data-ttu-id="96202-176">È possibile segnalare manualmente traccia informazioni o qualsiasi altra informazione di specifici dell'applicazione mediante hello `sendAppInfo()` (funzione).</span><span class="sxs-lookup"><span data-stu-id="96202-176">You can manually report tracking information (or any other application specific information) using hello `sendAppInfo()` function.</span></span>

<span data-ttu-id="96202-177">Si noti che queste informazioni possono essere inviate in modo incrementale: solo hello valore più recente per una determinata chiave verrà conservati per un determinato dispositivo.</span><span class="sxs-lookup"><span data-stu-id="96202-177">Note that these information can be sent incrementally: only hello latest value for a given key will be kept for a given device.</span></span>

<span data-ttu-id="96202-178">Come funzionalità aggiuntive di evento, hello classe Bundle è usato tooabstract informazioni dell'applicazione, si noti che le matrici o Sub Raggruppa verranno considerati come stringhe flat (con la serializzazione JSON).</span><span class="sxs-lookup"><span data-stu-id="96202-178">Like event extras, hello Bundle class is used tooabstract application information, note that arrays or sub-bundles will be treated as flat strings (using JSON serialization).</span></span>

### <a name="example"></a><span data-ttu-id="96202-179">Esempio</span><span class="sxs-lookup"><span data-stu-id="96202-179">Example</span></span>
<span data-ttu-id="96202-180">Ecco un sesso utente toosend esempio di codice e la data di nascita:</span><span class="sxs-lookup"><span data-stu-id="96202-180">Here is a code sample toosend user gender and birthdate:</span></span>

            Bundle appInfo = new Bundle();
            appInfo.putString("status", "premium");
            appInfo.putString("expiration", "2016-12-07"); // December 7th 2016
            EngagementAgent.getInstance(context).sendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="96202-181">Limiti</span><span class="sxs-lookup"><span data-stu-id="96202-181">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="96202-182">Chiavi</span><span class="sxs-lookup"><span data-stu-id="96202-182">Keys</span></span>
<span data-ttu-id="96202-183">Ogni chiave hello `Bundle` deve corrispondere hello espressione regolare seguente:</span><span class="sxs-lookup"><span data-stu-id="96202-183">Each key in hello `Bundle` must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="96202-184">Questo significa che le chiavi devono iniziare con almeno una lettera, seguita da lettere, cifre o caratteri di sottolineatura (\_).</span><span class="sxs-lookup"><span data-stu-id="96202-184">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="96202-185">Dimensione</span><span class="sxs-lookup"><span data-stu-id="96202-185">Size</span></span>
<span data-ttu-id="96202-186">Informazioni sull'applicazione sono troppo limitati**1024** caratteri per ogni chiamata (una volta codificato in JSON dal servizio di Engagement hello).</span><span class="sxs-lookup"><span data-stu-id="96202-186">Application information are limited too**1024** characters per call (once encoded in JSON by hello Engagement service).</span></span>

<span data-ttu-id="96202-187">In hello esempio precedente, hello JSON inviato server toohello è 44 caratteri:</span><span class="sxs-lookup"><span data-stu-id="96202-187">In hello previous example, hello JSON sent toohello server is 44 characters long:</span></span>

            {"expiration":"2016-12-07","status":"premium"}
