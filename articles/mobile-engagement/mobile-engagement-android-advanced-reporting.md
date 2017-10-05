---
title: Opzioni di segnalazione avanzata per Android SDK per Azure Mobile Engagement
description: Descrive come eseguire la segnalazione avanzata per l'acquisizione di analisi per Android SDK per Azure Mobile Engagement
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
ms.openlocfilehash: 2a1445afa2c2fca1a31ad9c012b9c8a917ebf65c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="advanced-reporting-with-engagement-on-android"></a><span data-ttu-id="6c15e-103">Segnalazione avanzata con Engagement in Android</span><span class="sxs-lookup"><span data-stu-id="6c15e-103">Advanced Reporting with Engagement on Android</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6c15e-104">Windows universale</span><span class="sxs-lookup"><span data-stu-id="6c15e-104">Universal Windows</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="6c15e-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="6c15e-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="6c15e-106">iOS</span><span class="sxs-lookup"><span data-stu-id="6c15e-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="6c15e-107">Android</span><span class="sxs-lookup"><span data-stu-id="6c15e-107">Android</span></span>](mobile-engagement-android-advanced-reporting.md)
> 
> 

<span data-ttu-id="6c15e-108">Questo argomento descrive scenari di segnalazione aggiuntivi nell'applicazione Android.</span><span class="sxs-lookup"><span data-stu-id="6c15e-108">This topic describes additional reporting scenarios in your Android application.</span></span> <span data-ttu-id="6c15e-109">È possibile applicare queste opzioni all'app creata nell'esercitazione [introduttiva](mobile-engagement-android-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="6c15e-109">You can apply these options to the app created in the [Getting Started](mobile-engagement-android-get-started.md) tutorial.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6c15e-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6c15e-110">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

<span data-ttu-id="6c15e-111">Anche se l'esercitazione completata è stata volutamente diretta e semplice, sono disponibili opzioni avanzate.</span><span class="sxs-lookup"><span data-stu-id="6c15e-111">The tutorial you completed was deliberately direct and simple, but there are advanced options you can choose.</span></span>

## <a name="modifying-your-activity-classes"></a><span data-ttu-id="6c15e-112">Modifica delle classi `Activity`</span><span class="sxs-lookup"><span data-stu-id="6c15e-112">Modifying your `Activity` classes</span></span>
<span data-ttu-id="6c15e-113">Nell'[esercitazione introduttiva](mobile-engagement-android-get-started.md) è stato sufficiente fare in modo che le sottoclassi `*Activity` ereditassero dalle corrispondenti classi `Engagement*Activity`.</span><span class="sxs-lookup"><span data-stu-id="6c15e-113">In the [Getting Started tutorial](mobile-engagement-android-get-started.md), all you had to do was to make your `*Activity` subclasses inherit from the corresponding `Engagement*Activity` classes.</span></span> <span data-ttu-id="6c15e-114">Se, ad esempio, l'attività legacy estende `ListActivity`, si fa in modo di estendere `EngagementListActivity`.</span><span class="sxs-lookup"><span data-stu-id="6c15e-114">For example, if your legacy activity extended `ListActivity`, you would make it extend `EngagementListActivity`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6c15e-115">Quando si usa `EngagementListActivity` o `EngagementExpandableListActivity`, assicurarsi che tutte le chiamate a `requestWindowFeature(...);` vengano eseguite prima della chiamata a `super.onCreate(...);`. In caso contrario, si verificherà un arresto anomalo del sistema.</span><span class="sxs-lookup"><span data-stu-id="6c15e-115">When using `EngagementListActivity` or `EngagementExpandableListActivity`, make sure any call to `requestWindowFeature(...);` is made before the call to `super.onCreate(...);`, otherwise a crash occurs.</span></span>
> 
> 

<span data-ttu-id="6c15e-116">Queste classi sono incluse nella cartella `src` e possono essere copiate nel progetto.</span><span class="sxs-lookup"><span data-stu-id="6c15e-116">You can find these classes in the `src` folder, and can copy them into your project.</span></span> <span data-ttu-id="6c15e-117">Sono reperibili anche in **JavaDoc**.</span><span class="sxs-lookup"><span data-stu-id="6c15e-117">The classes are also in the **JavaDoc**.</span></span>

## <a name="alternate-method-call-startactivity-and-endactivity-manually"></a><span data-ttu-id="6c15e-118">Metodo alternativo: chiamare manualmente `startActivity()` e `endActivity()`</span><span class="sxs-lookup"><span data-stu-id="6c15e-118">Alternate method: call `startActivity()` and `endActivity()` manually</span></span>
<span data-ttu-id="6c15e-119">Se non si può o non si vuole eseguire l'overload delle classi `Activity`, è possibile avviare e terminare le attività chiamando direttamente i metodi di `EngagementAgent`.</span><span class="sxs-lookup"><span data-stu-id="6c15e-119">If you cannot or do not want to overload your `Activity` classes, you can instead start and end your activities by calling the `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6c15e-120">Android SDK non chiama mai il metodo `endActivity()`, neanche alla chiusura dell'applicazione; in Android le applicazioni in realtà non vengono mai chiuse.</span><span class="sxs-lookup"><span data-stu-id="6c15e-120">The Android SDK never calls the `endActivity()` method, even when the application is closed (on Android, applications are never closed).</span></span> <span data-ttu-id="6c15e-121">Per questo motivo, è *ALTAMENTE* consigliabile chiamare il metodo `startActivity()` nel callback `onResume` di *TUTTE* le attività e il metodo `endActivity()` nel callback `onPause()` di *TUTTE* le attività.</span><span class="sxs-lookup"><span data-stu-id="6c15e-121">Thus, it is *HIGHLY* recommended to call the `startActivity()` method in the `onResume` callback of *ALL* your activities, and the `endActivity()` method in the `onPause()` callback of *ALL* your activities.</span></span> <span data-ttu-id="6c15e-122">È l'unico modo per evitare la perdita di sessioni.</span><span class="sxs-lookup"><span data-stu-id="6c15e-122">This is the only way to be sure that sessions are not leaked.</span></span> <span data-ttu-id="6c15e-123">In caso di perdita di una sessione, il servizio Engagement non si disconnetterà mai dal back-end di Engagement, dato che il servizio rimane connesso fintanto che una sessione è in sospeso.</span><span class="sxs-lookup"><span data-stu-id="6c15e-123">If a session is leaked, the Engagement service never disconnects from the Engagement backend (since the service stays connected as long as a session is pending).</span></span>
> 
> 

<span data-ttu-id="6c15e-124">Di seguito è fornito un esempio:</span><span class="sxs-lookup"><span data-stu-id="6c15e-124">Here is an example:</span></span>

    public class MyActivity extends Some3rdPartyActivity
    {
      @Override
      protected void onResume()
      {
        super.onResume();
        String activityNameOnEngagement = EngagementAgentUtils.buildEngagementActivityName(getClass()); // Uses short class name and removes "Activity" at the end.
        EngagementAgent.getInstance(this).startActivity(this, activityNameOnEngagement, null);
      }

      @Override
      protected void onPause()
      {
        super.onPause();
        EngagementAgent.getInstance(this).endActivity();
      }
    }

<span data-ttu-id="6c15e-125">Questo esempio è simile alla classe `EngagementActivity` e alle relative varianti, il cui codice di origine è disponibile nella cartella `src`.</span><span class="sxs-lookup"><span data-stu-id="6c15e-125">This example is similar to the `EngagementActivity` class and its variants, whose source code is provided in the `src` folder.</span></span>

## <a name="using-applicationoncreate"></a><span data-ttu-id="6c15e-126">Uso di Application.onCreate()</span><span class="sxs-lookup"><span data-stu-id="6c15e-126">Using Application.onCreate()</span></span>
<span data-ttu-id="6c15e-127">Il codice inserito in `Application.onCreate()` e in altri callback dell'applicazione verrà eseguito per tutti i processi dell'applicazione, incluso il servizio Engagement.</span><span class="sxs-lookup"><span data-stu-id="6c15e-127">Any code you place in `Application.onCreate()` and in other application callbacks is run for all your application's processes, including the Engagement service.</span></span> <span data-ttu-id="6c15e-128">È possibile che si verifichino effetti collaterali indesiderati, ad esempio allocazioni di memoria e thread superflui nel processo di Engagement oppure ricevitori o servizi di trasmissione duplicati.</span><span class="sxs-lookup"><span data-stu-id="6c15e-128">It may have unwanted side effects, like unneeded memory allocations and threads in the Engagement's process, or duplicate broadcast receivers or services.</span></span>

<span data-ttu-id="6c15e-129">Se si esegue l'override di `Application.onCreate()`, è consigliabile aggiungere il frammento di codice seguente all'inizio della funzione `Application.onCreate()`:</span><span class="sxs-lookup"><span data-stu-id="6c15e-129">If you override `Application.onCreate()`, we recommend adding the following code snippet at the beginning of your `Application.onCreate()` function:</span></span>

     public void onCreate()
     {
       if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
         return;

       ... Your code...
     }

<span data-ttu-id="6c15e-130">È possibile eseguire la stessa operazione per `Application.onTerminate()`, `Application.onLowMemory()` e `Application.onConfigurationChanged(...)`.</span><span class="sxs-lookup"><span data-stu-id="6c15e-130">You can do the same thing for `Application.onTerminate()`, `Application.onLowMemory()`, and `Application.onConfigurationChanged(...)`.</span></span>

<span data-ttu-id="6c15e-131">È anche possibile estendere `EngagementApplication` anziché `Application`: il callback esegue il controllo del processo `Application.onCreate()` e chiama `Application.onApplicationProcessCreate()` solo se il processo corrente non è quello che ospita il servizio Engagement. Per gli altri callback vengono applicate le stesse regole.</span><span class="sxs-lookup"><span data-stu-id="6c15e-131">You can also extend `EngagementApplication` instead of extending `Application`: the callback `Application.onCreate()` does the process check and calls `Application.onApplicationProcessCreate()` only if the current process is not the one hosting the Engagement service, the same rules apply for the other callbacks.</span></span>

## <a name="tags-in-the-androidmanifestxml-file"></a><span data-ttu-id="6c15e-132">Tag nel file AndroidManifest.xml</span><span class="sxs-lookup"><span data-stu-id="6c15e-132">Tags in the AndroidManifest.xml file</span></span>
<span data-ttu-id="6c15e-133">Nel tag service nel file AndroidManifest.xml l'attributo `android:label` consente di scegliere il nome del servizio Engagement così come verrà presentato agli utenti finali nella schermata dei servizi in esecuzione sul telefono.</span><span class="sxs-lookup"><span data-stu-id="6c15e-133">In the service tag in the AndroidManifest.xml file, the `android:label` attribute allows you to choose the name of the Engagement service as it appears to end users in the "Running services" screen of their phone.</span></span> <span data-ttu-id="6c15e-134">È consigliabile impostare questo attributo su `"<Your application name>Service"`, ad esempio `"AcmeFunGameService"`.</span><span class="sxs-lookup"><span data-stu-id="6c15e-134">We recommended setting this attribute to `"<Your application name>Service"` (for example, `"AcmeFunGameService"`).</span></span>

<span data-ttu-id="6c15e-135">Se si specifica l'attributo `android:process` , il servizio Engagement verrà eseguito nel relativo processo; l'esecuzione di Engagement nello stesso processo dell'applicazione può ridurre la reattività del thread principale o dell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="6c15e-135">Specifying the `android:process` attribute ensures that the Engagement service runs in its own process (running Engagement in the same process as your application makes your main/UI thread potentially less responsive).</span></span>

## <a name="building-with-proguard"></a><span data-ttu-id="6c15e-136">Compilazione con ProGuard</span><span class="sxs-lookup"><span data-stu-id="6c15e-136">Building with ProGuard</span></span>
<span data-ttu-id="6c15e-137">Se si compila il pacchetto dell'applicazione con ProGuard, è necessario mantenere alcune classi.</span><span class="sxs-lookup"><span data-stu-id="6c15e-137">If you build your application package with ProGuard, you need to keep some classes.</span></span> <span data-ttu-id="6c15e-138">È possibile usare il frammento di codice di configurazione seguente:</span><span class="sxs-lookup"><span data-stu-id="6c15e-138">You can use the following configuration snippet:</span></span>

    -keep public class * extends android.os.IInterface
    -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
    <methods>;
     }
