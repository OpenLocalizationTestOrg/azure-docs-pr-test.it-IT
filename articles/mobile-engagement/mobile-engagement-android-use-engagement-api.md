---
title: Come usare l'API di Engagement in Android
description: "Android SDK più recente - Come usare l'API di Engagement in Android"
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
ms.openlocfilehash: d353cd2fe47c54a0282cc5bb1b22b4a56e0cd82c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-engagement-api-on-android"></a><span data-ttu-id="2dc1c-103">Come usare l'API di Engagement in Android</span><span class="sxs-lookup"><span data-stu-id="2dc1c-103">How to Use the Engagement API on Android</span></span>
<span data-ttu-id="2dc1c-104">Questo documento è un'aggiunta al documento [Opzioni di segnalazione avanzata per Android Mobile Engagement SDK](mobile-engagement-android-advanced-reporting.md).</span><span class="sxs-lookup"><span data-stu-id="2dc1c-104">This document is an add-on to the document [Advanced Reporting options for Android Mobile Engagement SDK](mobile-engagement-android-advanced-reporting.md).</span></span> <span data-ttu-id="2dc1c-105">Fornisce informazioni approfondite su come usare l'API di Engagement per segnalare le statistiche dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2dc1c-105">It provides in depth details about how to use the Engagement API to report your application statistics.</span></span>

<span data-ttu-id="2dc1c-106">Tenere presente che, se si vuole impostare Engagement in modo che segnali solo le sessioni, le attività, gli arresti anomali e i dati tecnici dell'applicazione, la soluzione più semplice consiste nel fare in modo che tutte le sottoclassi `Activity` ereditino dalla classe `EngagementActivity` corrispondente.</span><span class="sxs-lookup"><span data-stu-id="2dc1c-106">Keep in mind that if you only want Engagement to report your application's sessions, activities, crashes and technical information, then the simplest way is to make all your `Activity` sub-classes inherit from the corresponding `EngagementActivity` class.</span></span>

<span data-ttu-id="2dc1c-107">Se invece si hanno esigenze più complesse, ad esempio se è necessario segnalare eventi, errori e processi specifici dell'applicazione o presentare le attività dell'applicazione in modo diverso rispetto a quello implementato nelle classi `EngagementActivity` , è necessario usare l'API di Engagement.</span><span class="sxs-lookup"><span data-stu-id="2dc1c-107">If you want to do more, for example if you need to report application specific events, errors and jobs, or if you have to report your application's activities in a different way than the one implemented in the `EngagementActivity` classes, then you need to use the Engagement API.</span></span>

<span data-ttu-id="2dc1c-108">L'API di Engagement viene fornita dalla classe `EngagementAgent` .</span><span class="sxs-lookup"><span data-stu-id="2dc1c-108">The Engagement API is provided by the `EngagementAgent` class.</span></span> <span data-ttu-id="2dc1c-109">Un'istanza di questa classe può essere recuperata chiamando il metodo statico `EngagementAgent.getInstance(Context)` (tenere presente che l'oggetto `EngagementAgent` restituito è un singleton).</span><span class="sxs-lookup"><span data-stu-id="2dc1c-109">An instance of this class can be retrieved by calling the `EngagementAgent.getInstance(Context)` static method (note that the `EngagementAgent` object returned is a singleton).</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="2dc1c-110">Concetti relativi a Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="2dc1c-110">Engagement concepts</span></span>
<span data-ttu-id="2dc1c-111">Le parti seguenti approfondiscono le informazioni contenute nell'articolo [Concetti relativi ad Azure Mobile Engagement](mobile-engagement-concepts.md)per la piattaforma Android.</span><span class="sxs-lookup"><span data-stu-id="2dc1c-111">The following parts refine the common [Mobile Engagement Concepts](mobile-engagement-concepts.md), for the Android platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="2dc1c-112">`Session` e `Activity`</span><span class="sxs-lookup"><span data-stu-id="2dc1c-112">`Session` and `Activity`</span></span>
<span data-ttu-id="2dc1c-113">Se l'utente resta inattivo per più di due secondi tra due *attività*, la sequenza di *attività* viene divisa in due *sessioni* distinte.</span><span class="sxs-lookup"><span data-stu-id="2dc1c-113">If the user stays more than a few seconds idle between two *activities*, then his sequence of *activities* is split in two distinct *sessions*.</span></span> <span data-ttu-id="2dc1c-114">Questi pochi secondi vengono chiamati "timeout della sessione".</span><span class="sxs-lookup"><span data-stu-id="2dc1c-114">These few seconds are called the "session timeout".</span></span>

<span data-ttu-id="2dc1c-115">Un'*attività* è in genere associata a una schermata dell'applicazione, ovvero l'*attività* inizia quando la schermata viene visualizzata e si arresta quando la schermata viene chiusa. Questo avviene quando Engagement SDK è integrato mediante le classi `EngagementActivity`.</span><span class="sxs-lookup"><span data-stu-id="2dc1c-115">An *activity* is usually associated with one screen of the application, that is to say the *activity* starts when the screen is displayed and stops when the screen is closed: this is the case when the Engagement SDK is integrated by using the `EngagementActivity` classes.</span></span>

<span data-ttu-id="2dc1c-116">Le *attività* possono tuttavia essere controllate anche manualmente usando l'API di Engagement.</span><span class="sxs-lookup"><span data-stu-id="2dc1c-116">But *activities* can also be controlled manually by using the Engagement API.</span></span> <span data-ttu-id="2dc1c-117">In questo modo, è possibile dividere una schermata specifica in diverse parti secondarie per ottenere maggiori dettagli sull'utilizzo della schermata, ad esempio per definire la frequenza e la durata in base alle quali le finestre di dialogo vengono usate all'interno della schermata.</span><span class="sxs-lookup"><span data-stu-id="2dc1c-117">This allows to split a given screen in several sub parts to get more details about the usage of this screen (for example to known how often and how long dialogs are used inside this screen).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="2dc1c-118">Segnalazione di attività</span><span class="sxs-lookup"><span data-stu-id="2dc1c-118">Reporting Activities</span></span>
> [!IMPORTANT]
> <span data-ttu-id="2dc1c-119">Non è necessario segnalare le attività nel modo indicato in questa sezione se si usa la classe `EngagementActivity` e le sue varianti in base alle istruzioni disponibili nell'articolo relativo all'integrazione di Engagement in Android.</span><span class="sxs-lookup"><span data-stu-id="2dc1c-119">You don't need to report activities like described in this section if you are using the `EngagementActivity` class and its variants as explained in the How to Integrate Engagement on Android document.</span></span>
> 
> 

### <a name="user-starts-a-new-activity"></a><span data-ttu-id="2dc1c-120">L'utente inizia una nuova attività</span><span class="sxs-lookup"><span data-stu-id="2dc1c-120">User starts a new Activity</span></span>
            EngagementAgent.getInstance(this).startActivity(this, "MyUserActivity", null);
            // Passing the current activity is required for Reach to display in-app notifications, passing null will postpone such announcements and polls.

<span data-ttu-id="2dc1c-121">È necessario chiamare `startActivity()` ogni volta che l'attività dell'utente cambia.</span><span class="sxs-lookup"><span data-stu-id="2dc1c-121">You need to call `startActivity()` each time the user activity changes.</span></span> <span data-ttu-id="2dc1c-122">La prima chiamata a questa funzione avvia una nuova sessione utente.</span><span class="sxs-lookup"><span data-stu-id="2dc1c-122">The first call to this function starts a new user session.</span></span>

<span data-ttu-id="2dc1c-123">Il punto migliore in cui chiamare questa funzione corrisponde a ogni callback `onResume` dell'attività.</span><span class="sxs-lookup"><span data-stu-id="2dc1c-123">The best place to call this function is on each activity `onResume` callback.</span></span>

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="2dc1c-124">L'utente termina l'attività corrente</span><span class="sxs-lookup"><span data-stu-id="2dc1c-124">User ends his current Activity</span></span>
            EngagementAgent.getInstance(this).endActivity();

<span data-ttu-id="2dc1c-125">È necessario chiamare `endActivity()` almeno una volta quando l'utente termina la sua ultima attività.</span><span class="sxs-lookup"><span data-stu-id="2dc1c-125">You need to call `endActivity()` at least once when the user finishes his last activity.</span></span> <span data-ttu-id="2dc1c-126">In questo modo, si indica all'SDK di Engagement che l'utente è attualmente inattivo e che la sessione utente deve essere chiusa allo scadere del timeout. Se si chiama `startActivity()` prima dello scadere del timeout, la sessione viene semplicemente ripresa.</span><span class="sxs-lookup"><span data-stu-id="2dc1c-126">This informs the Engagement SDK that the user is currently idle, and that the user session need to be closed once the session timeout will expire (if you call `startActivity()` before the session timeout expires, the session is simply resumed).</span></span>

<span data-ttu-id="2dc1c-127">Il punto migliore in cui chiamare questa funzione corrisponde a ogni callback `onPause` dell'attività.</span><span class="sxs-lookup"><span data-stu-id="2dc1c-127">The best place to call this function is on each activity `onPause` callback.</span></span>

## <a name="reporting-events"></a><span data-ttu-id="2dc1c-128">Segnalazione di eventi</span><span class="sxs-lookup"><span data-stu-id="2dc1c-128">Reporting Events</span></span>
### <a name="session-events"></a><span data-ttu-id="2dc1c-129">Eventi di sessione</span><span class="sxs-lookup"><span data-stu-id="2dc1c-129">Session events</span></span>
<span data-ttu-id="2dc1c-130">Gli eventi di sessione vengono in genere usati per segnalare le azioni eseguite da un utente durante la sua sessione.</span><span class="sxs-lookup"><span data-stu-id="2dc1c-130">Session events are usually used to report the actions performed by a user during his session.</span></span>

<span data-ttu-id="2dc1c-131">**Esempio senza dati aggiuntivi:**</span><span class="sxs-lookup"><span data-stu-id="2dc1c-131">**Example without extra data:**</span></span>

            public MyActivity extends EngagementActivity {
               [...]
               @Override
               public boolean onPrepareOptionsMenu(Menu menu) {
                  getEngagementAgent().sendSessionEvent("menu_shown", null);
               }
               [...]
            }

<span data-ttu-id="2dc1c-132">**Esempio con dati aggiuntivi:**</span><span class="sxs-lookup"><span data-stu-id="2dc1c-132">**Example with extra data:**</span></span>

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

### <a name="standalone-events"></a><span data-ttu-id="2dc1c-133">Eventi autonomi</span><span class="sxs-lookup"><span data-stu-id="2dc1c-133">Standalone Events</span></span>
<span data-ttu-id="2dc1c-134">Diversamente dagli eventi di sessione, gli eventi autonomi possono verificarsi all'esterno del contesto di una sessione.</span><span class="sxs-lookup"><span data-stu-id="2dc1c-134">Contrary to session events, standalone events can occur outside of the context of a session.</span></span>

<span data-ttu-id="2dc1c-135">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="2dc1c-135">**Example:**</span></span>

<span data-ttu-id="2dc1c-136">Si supponga di voler segnalare eventi verificatisi all'attivazione di un ricevitore di trasmissione:</span><span class="sxs-lookup"><span data-stu-id="2dc1c-136">Suppose you want to report events occurring when a broadcast receiver is triggered:</span></span>

            /** Triggered by Intent.ACTION_BATTERY_LOW */
            public BatteryLowReceiver extends BroadcastReceiver {
              [...]
              @Override
              public void onReceive(Context context, Intent intent) {
                EngagementAgent.getInstance(context).sendEvent("battery_low", null);
              }
              [...]
            }

## <a name="reporting-errors"></a><span data-ttu-id="2dc1c-137">Segnalazione di errori</span><span class="sxs-lookup"><span data-stu-id="2dc1c-137">Reporting Errors</span></span>
### <a name="session-errors"></a><span data-ttu-id="2dc1c-138">Errori di sessione</span><span class="sxs-lookup"><span data-stu-id="2dc1c-138">Session errors</span></span>
<span data-ttu-id="2dc1c-139">Gli errori di sessione vengono in genere usati per segnalare gli errori che hanno impatto sull'utente durante la sua sessione.</span><span class="sxs-lookup"><span data-stu-id="2dc1c-139">Session errors are usually used to report the errors impacting the user during his session.</span></span>

<span data-ttu-id="2dc1c-140">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="2dc1c-140">**Example:**</span></span>

            /** The user has entered invalid data in a form */
            public MyActivity extends EngagementActivity {
              [...]
              public void onMyFormSubmitted(MyForm form) {
                [...]
                /* The user has entered an invalid email address */
                getEngagementAgent().sendSessionError("sign_up_email", null);
                [...]
              }
              [...]
            }

### <a name="standalone-errors"></a><span data-ttu-id="2dc1c-141">Errori autonomi</span><span class="sxs-lookup"><span data-stu-id="2dc1c-141">Standalone errors</span></span>
<span data-ttu-id="2dc1c-142">Diversamente dagli errori di sessione, gli errori autonomi possono verificarsi all'esterno del contesto di una sessione.</span><span class="sxs-lookup"><span data-stu-id="2dc1c-142">Contrary to session errors, standalone errors can occur outside of the context of a session.</span></span>

<span data-ttu-id="2dc1c-143">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="2dc1c-143">**Example:**</span></span>

<span data-ttu-id="2dc1c-144">L'esempio seguente mostra come segnalare un errore ogni volta che la memoria nel telefono è insufficiente durante l'esecuzione del processo dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2dc1c-144">The following example shows how to report an error whenever the memory becomes low on the phone while your application process is running.</span></span>

            public MyApplication extends EngagementApplication {

              @Override
              protected void onApplicationProcessLowMemory() {
                EngagementAgent.getInstance(this).sendError("low_memory", null);
              }
            }

## <a name="reporting-jobs"></a><span data-ttu-id="2dc1c-145">Segnalazione di processi</span><span class="sxs-lookup"><span data-stu-id="2dc1c-145">Reporting Jobs</span></span>
### <a name="example"></a><span data-ttu-id="2dc1c-146">Esempio</span><span class="sxs-lookup"><span data-stu-id="2dc1c-146">Example</span></span>
<span data-ttu-id="2dc1c-147">Si supponga di voler segnalare la durata del processo di accesso:</span><span class="sxs-lookup"><span data-stu-id="2dc1c-147">Suppose you want to report the duration of your login process:</span></span>

            [...]
            public void signIn(Context context, ...) {

              /* We need an Android context to call the Engagement API, if you are extending Activity, Service, you can pass "this" */
              EngagementAgent engagementAgent = EngagementAgent.getInstance(context);

              /* Report sign in job has started */
              engagementAgent.startJob("sign_in", null);

              [... sign in ...]

              /* Report sign in job is now ended */
              engagementAgent.endJob("sign_in");
            }
            [...]

### <a name="report-errors-during-a-job"></a><span data-ttu-id="2dc1c-148">Segnalazione di errori durante un processo</span><span class="sxs-lookup"><span data-stu-id="2dc1c-148">Report Errors during a Job</span></span>
<span data-ttu-id="2dc1c-149">Gli errori possono essere correlati a un processo in esecuzione invece che alla sessione utente corrente.</span><span class="sxs-lookup"><span data-stu-id="2dc1c-149">Errors can be related to a running job instead of being related to the current user session.</span></span>

<span data-ttu-id="2dc1c-150">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="2dc1c-150">**Example:**</span></span>

<span data-ttu-id="2dc1c-151">Si supponga di voler segnalare un errore durante il processo di accesso:</span><span class="sxs-lookup"><span data-stu-id="2dc1c-151">Suppose you want to report an error during you login process:</span></span>

<span data-ttu-id="2dc1c-152">[...] public void signIn(Context context, ...) {</span><span class="sxs-lookup"><span data-stu-id="2dc1c-152">[...] public void signIn(Context context, ...) {</span></span>

              /* We need an Android context to call the Engagement API, if you are extending Activity, Service, you can pass "this" */
              EngagementAgent engagementAgent = EngagementAgent.getInstance(context);

              /* Report sign in job has been started */
              engagementAgent.startJob("sign_in", null);

              /* Try to sign in */
              while(true)
                try {
                  trySignin();
                  break;
                }
                catch(Exception e) {
                  /* Report the error to Engagement */
                  engagementAgent.sendJobError("sign_in_error", "sign_in", null);

                  /* Retry after a moment */
                  sleep(2000);
                }
              [...]
              /* Report sign in job is now ended */
              engagementAgent.endJob("sign_in");
            }
            [...]

### <a name="reporting-events-during-a-job"></a><span data-ttu-id="2dc1c-153">Segnalazione di eventi durante un processo</span><span class="sxs-lookup"><span data-stu-id="2dc1c-153">Reporting Events during a job</span></span>
<span data-ttu-id="2dc1c-154">Gli eventi possono essere correlati a un processo in esecuzione invece che alla sessione utente corrente.</span><span class="sxs-lookup"><span data-stu-id="2dc1c-154">Events can be related to a running job instead of being related to the current user session.</span></span>

<span data-ttu-id="2dc1c-155">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="2dc1c-155">**Example:**</span></span>

<span data-ttu-id="2dc1c-156">Si supponga di disporre di un social network e di usare un processo per segnalare il tempo totale durante il quale l'utente è connesso al server.</span><span class="sxs-lookup"><span data-stu-id="2dc1c-156">Suppose we have a social network, and we use a job to report the total time during which the user is connected to the server.</span></span> <span data-ttu-id="2dc1c-157">Poiché l'utente può restare connesso in background anche quando usa un'altra applicazione o quando il telefono è inattivo, potrebbe non esservi alcuna sessione.</span><span class="sxs-lookup"><span data-stu-id="2dc1c-157">The user can stay connected in background even when he's using another application or when the phone is sleeping, so there is no session.</span></span>

<span data-ttu-id="2dc1c-158">Se l'utente riceve messaggi dagli amici, si tratta di un evento di processo.</span><span class="sxs-lookup"><span data-stu-id="2dc1c-158">The user can receive messages from his friends, this is a job event.</span></span>

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

## <a name="extra-parameters"></a><span data-ttu-id="2dc1c-159">Parametri aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="2dc1c-159">Extra parameters</span></span>
<span data-ttu-id="2dc1c-160">È possibile collegare dati arbitrari a eventi, errori, attività e processi.</span><span class="sxs-lookup"><span data-stu-id="2dc1c-160">Arbitrary data can be attached to events, errors, activities and jobs.</span></span>

<span data-ttu-id="2dc1c-161">Questi dati possono essere strutturati, usando la classe Bundle di Android (in realtà, funziona come i parametri aggiuntivi negli intenti di Android).</span><span class="sxs-lookup"><span data-stu-id="2dc1c-161">This data can be structured, it uses Android's Bundle class (actually, it works like extra parameters in Android Intents).</span></span> <span data-ttu-id="2dc1c-162">Notare che una classe Bundle può contenere matrici o altre istanze Bundle.</span><span class="sxs-lookup"><span data-stu-id="2dc1c-162">Note that a Bundle can contain arrays or another Bundle instances.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2dc1c-163">Se si inseriscono parametri parcellizzabili o serializzabili, assicurarsi che venga implementato il rispettivo metodo `toString()` per restituire una stringa leggibile.</span><span class="sxs-lookup"><span data-stu-id="2dc1c-163">If you put in parcelable or serializable parameters, make sure their `toString()` method is implemented to return a human-readable string.</span></span> <span data-ttu-id="2dc1c-164">Le classi serializzabili che contengono campi non temporanei non serializzabili provocano l'arresto anomalo di Android quando si chiama `bundle.putSerializable("key",value);`</span><span class="sxs-lookup"><span data-stu-id="2dc1c-164">Serializable classes that contain non transient fields that are not serializable will make Android crash when you will call `bundle.putSerializable("key",value);`</span></span>
> 
> [!WARNING]
> <span data-ttu-id="2dc1c-165">Le matrici di tipo sparse non sono supportate nei parametri aggiuntivi, ovvero non vengono serializzate come matrice.</span><span class="sxs-lookup"><span data-stu-id="2dc1c-165">Sparse arrays in extra parameters are not supported, that is, it won't be serialized as an array.</span></span> <span data-ttu-id="2dc1c-166">Prima di usarle nei parametri aggiuntivi, è consigliabile convertirle in matrici standard.</span><span class="sxs-lookup"><span data-stu-id="2dc1c-166">You should convert them into standard arrays before using it in extra parameters.</span></span>
> 
> 

### <a name="example"></a><span data-ttu-id="2dc1c-167">Esempio</span><span class="sxs-lookup"><span data-stu-id="2dc1c-167">Example</span></span>
            Bundle extras = new Bundle();
            extras.putString("video_id", 123);
            extras.putString("ref_click", "http://foobar.com/blog");
            EngagementAgent.getInstance(context).sendEvent("video_clicked", extras);

### <a name="limits"></a><span data-ttu-id="2dc1c-168">Limiti</span><span class="sxs-lookup"><span data-stu-id="2dc1c-168">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="2dc1c-169">Chiavi</span><span class="sxs-lookup"><span data-stu-id="2dc1c-169">Keys</span></span>
<span data-ttu-id="2dc1c-170">Ogni chiave in `Bundle` deve corrispondere all'espressione regolare seguente:</span><span class="sxs-lookup"><span data-stu-id="2dc1c-170">Each key in the `Bundle` must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="2dc1c-171">Questo significa che le chiavi devono iniziare con almeno una lettera, seguita da lettere, cifre o caratteri di sottolineatura (\_).</span><span class="sxs-lookup"><span data-stu-id="2dc1c-171">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="2dc1c-172">Dimensione</span><span class="sxs-lookup"><span data-stu-id="2dc1c-172">Size</span></span>
<span data-ttu-id="2dc1c-173">I dati aggiuntivi sono limitati a **1024** caratteri per chiamata, una volta codificati in JSON dal servizio Engagement.</span><span class="sxs-lookup"><span data-stu-id="2dc1c-173">Extras are limited to **1024** characters per call (once encoded in JSON by the Engagement service).</span></span>

<span data-ttu-id="2dc1c-174">Nell'esempio precedente il codice JSON inviato al server è lungo 58 caratteri:</span><span class="sxs-lookup"><span data-stu-id="2dc1c-174">In the previous example, the JSON sent to the server is 58 characters long:</span></span>

            {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a><span data-ttu-id="2dc1c-175">Segnalazione di informazioni sull'applicazione</span><span class="sxs-lookup"><span data-stu-id="2dc1c-175">Reporting Application Information</span></span>
<span data-ttu-id="2dc1c-176">È possibile segnalare manualmente le informazioni di traccia o qualsiasi altra informazione specifica dell'applicazione mediante la funzione `sendAppInfo()` .</span><span class="sxs-lookup"><span data-stu-id="2dc1c-176">You can manually report tracking information (or any other application specific information) using the `sendAppInfo()` function.</span></span>

<span data-ttu-id="2dc1c-177">Queste informazioni possono essere inviate in modo incrementale: viene mantenuto solo l'ultimo valore per una determinata chiave per ogni dispositivo specifico.</span><span class="sxs-lookup"><span data-stu-id="2dc1c-177">Note that these information can be sent incrementally: only the latest value for a given key will be kept for a given device.</span></span>

<span data-ttu-id="2dc1c-178">Come per i dati aggiuntivi degli eventi, la classe Bundle viene usata per astrarre le informazioni sull'applicazione. Tenere presente che le matrici o i bundle secondari vengono trattati come stringhe flat (usando la serializzazione JSON).</span><span class="sxs-lookup"><span data-stu-id="2dc1c-178">Like event extras, the Bundle class is used to abstract application information, note that arrays or sub-bundles will be treated as flat strings (using JSON serialization).</span></span>

### <a name="example"></a><span data-ttu-id="2dc1c-179">Esempio</span><span class="sxs-lookup"><span data-stu-id="2dc1c-179">Example</span></span>
<span data-ttu-id="2dc1c-180">Ecco un esempio di codice per inviare il sesso e la data di nascita dell'utente:</span><span class="sxs-lookup"><span data-stu-id="2dc1c-180">Here is a code sample to send user gender and birthdate:</span></span>

            Bundle appInfo = new Bundle();
            appInfo.putString("status", "premium");
            appInfo.putString("expiration", "2016-12-07"); // December 7th 2016
            EngagementAgent.getInstance(context).sendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="2dc1c-181">Limiti</span><span class="sxs-lookup"><span data-stu-id="2dc1c-181">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="2dc1c-182">Chiavi</span><span class="sxs-lookup"><span data-stu-id="2dc1c-182">Keys</span></span>
<span data-ttu-id="2dc1c-183">Ogni chiave in `Bundle` deve corrispondere all'espressione regolare seguente:</span><span class="sxs-lookup"><span data-stu-id="2dc1c-183">Each key in the `Bundle` must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="2dc1c-184">Questo significa che le chiavi devono iniziare con almeno una lettera, seguita da lettere, cifre o caratteri di sottolineatura (\_).</span><span class="sxs-lookup"><span data-stu-id="2dc1c-184">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="2dc1c-185">Dimensione</span><span class="sxs-lookup"><span data-stu-id="2dc1c-185">Size</span></span>
<span data-ttu-id="2dc1c-186">Le informazioni sull'applicazione sono limitate a **1024** caratteri per chiamata, una volta codificate in JSON dal servizio Engagement.</span><span class="sxs-lookup"><span data-stu-id="2dc1c-186">Application information are limited to **1024** characters per call (once encoded in JSON by the Engagement service).</span></span>

<span data-ttu-id="2dc1c-187">Nell'esempio precedente il codice JSON inviato al server è lungo 44 caratteri:</span><span class="sxs-lookup"><span data-stu-id="2dc1c-187">In the previous example, the JSON sent to the server is 44 characters long:</span></span>

            {"expiration":"2016-12-07","status":"premium"}
