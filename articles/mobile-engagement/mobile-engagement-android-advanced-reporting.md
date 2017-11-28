---
title: opzioni di Azure Mobile Engagement SDK Android reporting aaaAdvanced
description: Viene descritto come toodo avanzate reporting toocapture analitica per Azure Mobile Engagement SDK Android
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 7da7abd5-19d6-4892-94d8-818e5424b2cd
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/10/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 5c8f4ea36c54715f4e09fd43c96132c15019a71b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-reporting-with-engagement-on-android"></a><span data-ttu-id="7344a-103">Segnalazione avanzata con Engagement in Android</span><span class="sxs-lookup"><span data-stu-id="7344a-103">Advanced Reporting with Engagement on Android</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7344a-104">Windows universale</span><span class="sxs-lookup"><span data-stu-id="7344a-104">Universal Windows</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="7344a-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="7344a-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="7344a-106">iOS</span><span class="sxs-lookup"><span data-stu-id="7344a-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="7344a-107">Android</span><span class="sxs-lookup"><span data-stu-id="7344a-107">Android</span></span>](mobile-engagement-android-advanced-reporting.md)
> 
> 

<span data-ttu-id="7344a-108">Questo argomento descrive scenari di segnalazione aggiuntivi nell'applicazione Android.</span><span class="sxs-lookup"><span data-stu-id="7344a-108">This topic describes additional reporting scenarios in your Android application.</span></span> <span data-ttu-id="7344a-109">È possibile applicare queste app toohello opzioni creato in hello [Introduzione](mobile-engagement-android-get-started.md) esercitazione.</span><span class="sxs-lookup"><span data-stu-id="7344a-109">You can apply these options toohello app created in hello [Getting Started](mobile-engagement-android-get-started.md) tutorial.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7344a-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7344a-110">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

<span data-ttu-id="7344a-111">esercitazione Hello è completata è stata volutamente semplice e diretto, ma vi sono le opzioni avanzate è possibile scegliere.</span><span class="sxs-lookup"><span data-stu-id="7344a-111">hello tutorial you completed was deliberately direct and simple, but there are advanced options you can choose.</span></span>

## <a name="modifying-your-activity-classes"></a><span data-ttu-id="7344a-112">Modifica delle classi `Activity`</span><span class="sxs-lookup"><span data-stu-id="7344a-112">Modifying your `Activity` classes</span></span>
<span data-ttu-id="7344a-113">In hello [esercitazione introduttiva](mobile-engagement-android-get-started.md), tutti toodo era stata toomake il `*Activity` sottoclassi ereditano hello corrispondente `Engagement*Activity` classi.</span><span class="sxs-lookup"><span data-stu-id="7344a-113">In hello [Getting Started tutorial](mobile-engagement-android-get-started.md), all you had toodo was toomake your `*Activity` subclasses inherit from hello corresponding `Engagement*Activity` classes.</span></span> <span data-ttu-id="7344a-114">Se, ad esempio, l'attività legacy estende `ListActivity`, si fa in modo di estendere `EngagementListActivity`.</span><span class="sxs-lookup"><span data-stu-id="7344a-114">For example, if your legacy activity extended `ListActivity`, you would make it extend `EngagementListActivity`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7344a-115">Quando si utilizza `EngagementListActivity` o `EngagementExpandableListActivity`, assicurarsi che tutte le chiamate troppo`requestWindowFeature(...);` diventa troppo prima chiamata hello`super.onCreate(...);`, in caso contrario si verifica un arresto anomalo.</span><span class="sxs-lookup"><span data-stu-id="7344a-115">When using `EngagementListActivity` or `EngagementExpandableListActivity`, make sure any call too`requestWindowFeature(...);` is made before hello call too`super.onCreate(...);`, otherwise a crash occurs.</span></span>
> 
> 

<span data-ttu-id="7344a-116">È possibile trovare queste classi in hello `src` cartella e possono copiare nel progetto.</span><span class="sxs-lookup"><span data-stu-id="7344a-116">You can find these classes in hello `src` folder, and can copy them into your project.</span></span> <span data-ttu-id="7344a-117">classi di Hello sono anche in hello **JavaDoc**.</span><span class="sxs-lookup"><span data-stu-id="7344a-117">hello classes are also in hello **JavaDoc**.</span></span>

## <a name="alternate-method-call-startactivity-and-endactivity-manually"></a><span data-ttu-id="7344a-118">Metodo alternativo: chiamare manualmente `startActivity()` e `endActivity()`</span><span class="sxs-lookup"><span data-stu-id="7344a-118">Alternate method: call `startActivity()` and `endActivity()` manually</span></span>
<span data-ttu-id="7344a-119">Se non è possibile o non si desidera toooverload il `Activity` classi, è possibile invece iniziare e terminare le attività chiamando hello `EngagementAgent`del diretta dei metodi.</span><span class="sxs-lookup"><span data-stu-id="7344a-119">If you cannot or do not want toooverload your `Activity` classes, you can instead start and end your activities by calling hello `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7344a-120">Hello, Android SDK non chiama mai hello `endActivity()` (metodo), anche quando viene chiusa l'applicazione hello (in Android, non chiudere le applicazioni sono mai).</span><span class="sxs-lookup"><span data-stu-id="7344a-120">hello Android SDK never calls hello `endActivity()` method, even when hello application is closed (on Android, applications are never closed).</span></span> <span data-ttu-id="7344a-121">È pertanto *elevata* consigliato hello toocall `startActivity()` metodo hello `onResume` callback di *tutti* le attività e hello `endActivity()` metodo hello `onPause()` callback di *tutti* delle attività.</span><span class="sxs-lookup"><span data-stu-id="7344a-121">Thus, it is *HIGHLY* recommended toocall hello `startActivity()` method in hello `onResume` callback of *ALL* your activities, and hello `endActivity()` method in hello `onPause()` callback of *ALL* your activities.</span></span> <span data-ttu-id="7344a-122">Si tratta di hello solo modo toobe assicurarsi che le sessioni non vengano comunicate.</span><span class="sxs-lookup"><span data-stu-id="7344a-122">This is hello only way toobe sure that sessions are not leaked.</span></span> <span data-ttu-id="7344a-123">Se una sessione viene perso, hello servizio Engagement non disconnette mai dal back-end Engagement hello (dal momento che il servizio di hello rimane connesso, purché una sessione è in sospeso).</span><span class="sxs-lookup"><span data-stu-id="7344a-123">If a session is leaked, hello Engagement service never disconnects from hello Engagement backend (since hello service stays connected as long as a session is pending).</span></span>
> 
> 

<span data-ttu-id="7344a-124">Di seguito è fornito un esempio:</span><span class="sxs-lookup"><span data-stu-id="7344a-124">Here is an example:</span></span>

    public class MyActivity extends Some3rdPartyActivity
    {
      @Override
      protected void onResume()
      {
        super.onResume();
        String activityNameOnEngagement = EngagementAgentUtils.buildEngagementActivityName(getClass()); // Uses short class name and removes "Activity" at hello end.
        EngagementAgent.getInstance(this).startActivity(this, activityNameOnEngagement, null);
      }

      @Override
      protected void onPause()
      {
        super.onPause();
        EngagementAgent.getInstance(this).endActivity();
      }
    }

<span data-ttu-id="7344a-125">Questo esempio è simile toohello `EngagementActivity` classe e le sue varianti, il cui codice sorgente viene fornito in hello `src` cartella.</span><span class="sxs-lookup"><span data-stu-id="7344a-125">This example is similar toohello `EngagementActivity` class and its variants, whose source code is provided in hello `src` folder.</span></span>

## <a name="using-applicationoncreate"></a><span data-ttu-id="7344a-126">Uso di Application.onCreate()</span><span class="sxs-lookup"><span data-stu-id="7344a-126">Using Application.onCreate()</span></span>
<span data-ttu-id="7344a-127">Inserire nel codice `Application.onCreate()` e in un'altra applicazione callback viene eseguito per tutti i processi dell'applicazione, incluso hello Engagement servizio.</span><span class="sxs-lookup"><span data-stu-id="7344a-127">Any code you place in `Application.onCreate()` and in other application callbacks is run for all your application's processes, including hello Engagement service.</span></span> <span data-ttu-id="7344a-128">Potrebbe disporre gli effetti collaterali indesiderati, come le allocazioni di memoria non necessari e i thread nel processo di Engagement hello, o duplicato broadcast ricevitori o servizi.</span><span class="sxs-lookup"><span data-stu-id="7344a-128">It may have unwanted side effects, like unneeded memory allocations and threads in hello Engagement's process, or duplicate broadcast receivers or services.</span></span>

<span data-ttu-id="7344a-129">Se esegue l'override `Application.onCreate()`, è consigliabile aggiungere hello seguente frammento di codice all'inizio di hello del `Application.onCreate()` funzione:</span><span class="sxs-lookup"><span data-stu-id="7344a-129">If you override `Application.onCreate()`, we recommend adding hello following code snippet at hello beginning of your `Application.onCreate()` function:</span></span>

     public void onCreate()
     {
       if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
         return;

       ... Your code...
     }

<span data-ttu-id="7344a-130">È possibile eseguire hello stessa operazione per `Application.onTerminate()`, `Application.onLowMemory()`, e `Application.onConfigurationChanged(...)`.</span><span class="sxs-lookup"><span data-stu-id="7344a-130">You can do hello same thing for `Application.onTerminate()`, `Application.onLowMemory()`, and `Application.onConfigurationChanged(...)`.</span></span>

<span data-ttu-id="7344a-131">È anche possibile estendere `EngagementApplication` anziché estensione `Application`: hello callback `Application.onCreate()` hello controllo processo e chiama `Application.onApplicationProcessCreate()` solo se il processo corrente hello è non hello uno hello Engagement servizio di hosting, hello stesse regole valide per Hello altre richiamate.</span><span class="sxs-lookup"><span data-stu-id="7344a-131">You can also extend `EngagementApplication` instead of extending `Application`: hello callback `Application.onCreate()` does hello process check and calls `Application.onApplicationProcessCreate()` only if hello current process is not hello one hosting hello Engagement service, hello same rules apply for hello other callbacks.</span></span>

## <a name="tags-in-hello-androidmanifestxml-file"></a><span data-ttu-id="7344a-132">Tag nel file AndroidManifest.xml hello</span><span class="sxs-lookup"><span data-stu-id="7344a-132">Tags in hello AndroidManifest.xml file</span></span>
<span data-ttu-id="7344a-133">Nel tag di servizio hello nel file AndroidManifest.xml hello, hello `android:label` attributo consente un nome hello toochoose di hello servizio Engagement così come viene visualizzato agli utenti di tooend nella schermata di "Servizi in esecuzione" hello del telefono.</span><span class="sxs-lookup"><span data-stu-id="7344a-133">In hello service tag in hello AndroidManifest.xml file, hello `android:label` attribute allows you toochoose hello name of hello Engagement service as it appears tooend users in hello "Running services" screen of their phone.</span></span> <span data-ttu-id="7344a-134">È consigliabile impostare questo attributo troppo`"<Your application name>Service"` (ad esempio, `"AcmeFunGameService"`).</span><span class="sxs-lookup"><span data-stu-id="7344a-134">We recommended setting this attribute too`"<Your application name>Service"` (for example, `"AcmeFunGameService"`).</span></span>

<span data-ttu-id="7344a-135">Se si specifica hello `android:process` attributo assicura che hello viene eseguito il servizio Engagement in un processo (Engagement in esecuzione nella stessa procedura adottata l'applicazione esegue il thread principale o dell'interfaccia utente potenzialmente tempi hello).</span><span class="sxs-lookup"><span data-stu-id="7344a-135">Specifying hello `android:process` attribute ensures that hello Engagement service runs in its own process (running Engagement in hello same process as your application makes your main/UI thread potentially less responsive).</span></span>

## <a name="building-with-proguard"></a><span data-ttu-id="7344a-136">Compilazione con ProGuard</span><span class="sxs-lookup"><span data-stu-id="7344a-136">Building with ProGuard</span></span>
<span data-ttu-id="7344a-137">Se si compila il pacchetto dell'applicazione con ProGuard, è necessario tookeep alcune classi.</span><span class="sxs-lookup"><span data-stu-id="7344a-137">If you build your application package with ProGuard, you need tookeep some classes.</span></span> <span data-ttu-id="7344a-138">È possibile utilizzare hello seguente frammento di configurazione:</span><span class="sxs-lookup"><span data-stu-id="7344a-138">You can use hello following configuration snippet:</span></span>

    -keep public class * extends android.os.IInterface
    -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
    <methods>;
     }
