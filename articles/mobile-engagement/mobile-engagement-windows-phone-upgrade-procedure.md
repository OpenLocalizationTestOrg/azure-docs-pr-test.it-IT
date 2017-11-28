---
title: le procedure di aggiornamento di Phone Silverlight SDK aaaWindows
description: Procedure di aggiornamento di Azure Mobile Engagement SDK per Windows Phone Silverlight
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 87130026-9759-4659-9184-788a3627a165
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: d72e7b8a59ef2c0a95b22efbf1e5257271399ddc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-sdk-upgrade-procedures"></a><span data-ttu-id="2f3af-103">Procedure di aggiornamento dell'SDK per Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="2f3af-103">Windows Phone Silverlight SDK Upgrade Procedures</span></span>
<span data-ttu-id="2f3af-104">Se è già stata integrata una versione precedente di Windows SDK nell'applicazione, è necessario hello tooconsider seguenti punti quando si aggiorna hello SDK.</span><span class="sxs-lookup"><span data-stu-id="2f3af-104">If you already have integrated an older version of our SDK into your application, you have tooconsider hello following points when upgrading hello SDK.</span></span>

<span data-ttu-id="2f3af-105">È possibile toofollow varie procedure se sono saltate diverse versioni di hello SDK.</span><span class="sxs-lookup"><span data-stu-id="2f3af-105">You may have toofollow several procedures if you missed several versions of hello SDK.</span></span> <span data-ttu-id="2f3af-106">Ad esempio se si esegue la migrazione da 0.10.1 too0.11.0 è toofirst seguire hello "da 0.9.0 too0.10.1" routine quindi hello "da 0.10.1 too0.11.0" stored procedure.</span><span class="sxs-lookup"><span data-stu-id="2f3af-106">For example if you migrate from 0.10.1 too0.11.0 you have toofirst follow hello "from 0.9.0 too0.10.1" procedure then hello "from 0.10.1 too0.11.0" procedure.</span></span>

## <a name="from-200-too330"></a><span data-ttu-id="2f3af-107">Da 2.0.0 too3.3.0</span><span class="sxs-lookup"><span data-stu-id="2f3af-107">From 2.0.0 too3.3.0</span></span>
### <a name="test-logs"></a><span data-ttu-id="2f3af-108">Log di test</span><span class="sxs-lookup"><span data-stu-id="2f3af-108">Test logs</span></span>
<span data-ttu-id="2f3af-109">Registri della console prodotti da hello SDK ora possono essere attivato/disattivato/filtrato.</span><span class="sxs-lookup"><span data-stu-id="2f3af-109">Console logs produced by hello SDK can now be enabled/disabled/filtered.</span></span> <span data-ttu-id="2f3af-110">toocustomize, questa proprietà hello aggiornamento `EngagementAgent.Instance.TestLogEnabled` tooone del valore di hello disponibile hello `EngagementTestLogLevel` enumerazione, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="2f3af-110">toocustomize this, update hello property `EngagementAgent.Instance.TestLogEnabled` tooone of hello value available from hello `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

## <a name="from-111-too200"></a><span data-ttu-id="2f3af-111">Da 1.1.1 too2.0.0</span><span class="sxs-lookup"><span data-stu-id="2f3af-111">From 1.1.1 too2.0.0</span></span>
<span data-ttu-id="2f3af-112">Hello seguenti viene descritto come toomigrate un'integrazione SDK da hello Capptain servizio offerto da Capptain SAS in un'app con Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="2f3af-112">hello following describes how toomigrate an SDK integration from hello Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="2f3af-113">Capptain e Mobile Engagement non sono hello stessi servizi e procedura di hello indicata di seguito solo evidenziata come toomigrate hello app client.</span><span class="sxs-lookup"><span data-stu-id="2f3af-113">Capptain and Mobile Engagement are not hello same services and hello procedure given below only highlights how toomigrate hello client app.</span></span> <span data-ttu-id="2f3af-114">Migrazione hello SDK nell'applicazione hello verrà non la migrazione dei dati dai server di hello Capptain server toohello Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="2f3af-114">Migrating hello SDK in hello app will NOT migrate your data from hello Capptain servers toohello Mobile Engagement servers</span></span>
> 
> 

<span data-ttu-id="2f3af-115">Se si esegue la migrazione da una versione precedente, consultare prima hello Capptain sito web toomigrate too1.1.1 quindi applicare hello procedura</span><span class="sxs-lookup"><span data-stu-id="2f3af-115">If you are migrating from an earlier version, please consult hello Capptain web site toomigrate too1.1.1 first then apply hello following procedure</span></span>

### <a name="nuget-package"></a><span data-ttu-id="2f3af-116">Pacchetto NuGet</span><span class="sxs-lookup"><span data-stu-id="2f3af-116">Nuget package</span></span>
<span data-ttu-id="2f3af-117">Sostituire **Capptain.WindowsPhone** con il pacchetto NuGet **MicrosoftAzure.MobileEngagement**.</span><span class="sxs-lookup"><span data-stu-id="2f3af-117">Replace **Capptain.WindowsPhone** by **MicrosoftAzure.MobileEngagement** Nuget package.</span></span>

### <a name="applying-mobile-engagement"></a><span data-ttu-id="2f3af-118">Applicazione di Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="2f3af-118">Applying Mobile Engagement</span></span>
<span data-ttu-id="2f3af-119">Hello SDK viene utilizzato il termine hello `Engagement`.</span><span class="sxs-lookup"><span data-stu-id="2f3af-119">hello SDK uses hello term `Engagement`.</span></span> <span data-ttu-id="2f3af-120">È necessario tooupdate toomatch il progetto questa modifica.</span><span class="sxs-lookup"><span data-stu-id="2f3af-120">You need tooupdate your project toomatch this change.</span></span>

<span data-ttu-id="2f3af-121">È necessario toouninstall il pacchetto nuget Capptain corrente.</span><span class="sxs-lookup"><span data-stu-id="2f3af-121">You need toouninstall your current Capptain nuget package.</span></span> <span data-ttu-id="2f3af-122">Si consideri che verranno rimosse tutte le modifiche nella cartella Risorse di Capptain.</span><span class="sxs-lookup"><span data-stu-id="2f3af-122">Consider that all your changes in Capptain Resources folder will be removed.</span></span> <span data-ttu-id="2f3af-123">Se si desidera tookeep tali file, creare una copia di essi.</span><span class="sxs-lookup"><span data-stu-id="2f3af-123">If you want tookeep those files then make a copy of them.</span></span>

<span data-ttu-id="2f3af-124">Successivamente, installare il pacchetto di hello nuovo impegno di Microsoft Azure nuget nel progetto.</span><span class="sxs-lookup"><span data-stu-id="2f3af-124">After that, install hello new Microsoft Azure Engagement nuget package on your project.</span></span> <span data-ttu-id="2f3af-125">È possibile trovarlo direttamente sul sito Web di [NuGet](http://www.nuget.org/packages/MicrosoftAzure.MobileEngagement).</span><span class="sxs-lookup"><span data-stu-id="2f3af-125">You can find it directly on [Nuget](http://www.nuget.org/packages/MicrosoftAzure.MobileEngagement).</span></span> <span data-ttu-id="2f3af-126">Sostituisce questa azione, tutti i file di risorse utilizzate da Engagement e hello nuova DLL Engagement tooyour aggiunge i riferimenti al progetto.</span><span class="sxs-lookup"><span data-stu-id="2f3af-126">This action replaces all resources files used by Engagement and adds hello new Engagement DLL tooyour project References.</span></span>

<span data-ttu-id="2f3af-127">Hai tooclean riferimenti del progetto eliminando i riferimenti DLL Capptain.</span><span class="sxs-lookup"><span data-stu-id="2f3af-127">You have tooclean your project references by deleting Capptain DLL references.</span></span> <span data-ttu-id="2f3af-128">Se non si apporta questa, versione di hello di Capptain è in conflitto e si verificheranno gli errori.</span><span class="sxs-lookup"><span data-stu-id="2f3af-128">If you do not make this, hello version of Capptain will conflict and errors will happen.</span></span>

<span data-ttu-id="2f3af-129">Se è stato personalizzato Capptain risorse, copiare il contenuto del file precedente e incollarli in nuovi file di Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="2f3af-129">If you have customized Capptain resources, copy your old files content and paste them in hello new Engagement files.</span></span> <span data-ttu-id="2f3af-130">Si noti che i file xaml sia cs toobe aggiornato.</span><span class="sxs-lookup"><span data-stu-id="2f3af-130">Please note that both xaml and cs files have toobe updated.</span></span>

<span data-ttu-id="2f3af-131">Dopo avere completato questi passaggi è sufficiente tooreplace precedente Capptain i riferimenti basati sui nuovi riferimenti di Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="2f3af-131">When those steps are completed you only have tooreplace old Capptain references by hello new Engagement references.</span></span>

1. <span data-ttu-id="2f3af-132">Tutti gli spazi dei nomi di Capptain avere toobe aggiornato.</span><span class="sxs-lookup"><span data-stu-id="2f3af-132">All Capptain namespaces have toobe updated.</span></span>
   
    <span data-ttu-id="2f3af-133">Prima della migrazione:</span><span class="sxs-lookup"><span data-stu-id="2f3af-133">Before migration:</span></span>
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    <span data-ttu-id="2f3af-134">Dopo la migrazione:</span><span class="sxs-lookup"><span data-stu-id="2f3af-134">After migration:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="2f3af-135">Tutte le classi Capptain che contengono "Capptain" devono contenere "Engagement".</span><span class="sxs-lookup"><span data-stu-id="2f3af-135">All Capptain classes that contain "Capptain" should contain "Engagement".</span></span>
   
    <span data-ttu-id="2f3af-136">Prima della migrazione:</span><span class="sxs-lookup"><span data-stu-id="2f3af-136">Before migration:</span></span>
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    <span data-ttu-id="2f3af-137">Dopo la migrazione:</span><span class="sxs-lookup"><span data-stu-id="2f3af-137">After migration:</span></span>
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. <span data-ttu-id="2f3af-138">Per i file xaml cambiano anche attributi e spazio dei nomi di Capptain.</span><span class="sxs-lookup"><span data-stu-id="2f3af-138">For xaml files Capptain namespace and attributes also change.</span></span>
   
    <span data-ttu-id="2f3af-139">Prima della migrazione:</span><span class="sxs-lookup"><span data-stu-id="2f3af-139">Before migration:</span></span>
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    <span data-ttu-id="2f3af-140">Dopo la migrazione:</span><span class="sxs-lookup"><span data-stu-id="2f3af-140">After migration:</span></span>
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. <span data-ttu-id="2f3af-141">Per altre risorse come le immagini Capptain di hello, si noti che sono anche stati rinominati toouse "Engagement".</span><span class="sxs-lookup"><span data-stu-id="2f3af-141">For hello other resources like Capptain pictures, please note that they also have been renamed toouse "Engagement".</span></span>

### <a name="application-id--sdk-key"></a><span data-ttu-id="2f3af-142">ID applicazione / chiave SDK</span><span class="sxs-lookup"><span data-stu-id="2f3af-142">Application ID / SDK Key</span></span>
<span data-ttu-id="2f3af-143">Engagement utilizza una stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="2f3af-143">Engagement uses a connection string.</span></span> <span data-ttu-id="2f3af-144">Non si dispone toospecify un ID applicazione e una chiave SDK con Engagement Mobile, è sufficiente toospecify una stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="2f3af-144">You don't have toospecify an application ID and an SDK key with Mobile Engagement, you only have toospecify a connection string.</span></span> <span data-ttu-id="2f3af-145">È possibile configurarla nel file EngagementConfiguration.</span><span class="sxs-lookup"><span data-stu-id="2f3af-145">You can set it up on your EngagementConfiguration file.</span></span>

<span data-ttu-id="2f3af-146">configurazione di Engagement Hello può essere impostate nel `Resources\EngagementConfiguration.xml` file del progetto.</span><span class="sxs-lookup"><span data-stu-id="2f3af-146">hello Engagement configuration can be set in your `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="2f3af-147">Modificare questo toospecify file:</span><span class="sxs-lookup"><span data-stu-id="2f3af-147">Edit this file toospecify:</span></span>

* <span data-ttu-id="2f3af-148">La stringa di connessione dell'applicazione tra i tag `<connectionString>` and `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="2f3af-148">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="2f3af-149">Se si desidera che in fase di esecuzione, invece, si può chiamare seguente hello toospecify metodo prima dell'inizializzazione dell'agente di Engagement hello:</span><span class="sxs-lookup"><span data-stu-id="2f3af-149">If you want toospecify it at runtime instead, you can call hello following method before hello Engagement agent initialization:</span></span>

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Initialize Engagement angent with above configuration. */
        EngagementAgent.Instance.Init(engagementConfiguration);

<span data-ttu-id="2f3af-150">stringa di connessione Hello per l'applicazione viene visualizzato nel portale di Azure classico hello.</span><span class="sxs-lookup"><span data-stu-id="2f3af-150">hello connection string for your application is displayed in hello Azure Classic Portal.</span></span>

### <a name="items-name-change"></a><span data-ttu-id="2f3af-151">Modifica del nome di elementi</span><span class="sxs-lookup"><span data-stu-id="2f3af-151">Items name change</span></span>
<span data-ttu-id="2f3af-152">Tutti gli elementi denominati *capptain* sono stati rinominati in *engagement*.</span><span class="sxs-lookup"><span data-stu-id="2f3af-152">All items named *capptain* have been named *engagement*.</span></span> <span data-ttu-id="2f3af-153">Analogamente, per *Capptain* troppo*Engagement*.</span><span class="sxs-lookup"><span data-stu-id="2f3af-153">Similarly for *Capptain* too*Engagement*.</span></span>

<span data-ttu-id="2f3af-154">Esempi di elementi di Capptain di uso comune:</span><span class="sxs-lookup"><span data-stu-id="2f3af-154">Examples of commonly used Capptain items :</span></span>

* <span data-ttu-id="2f3af-155">CapptainConfiguration è diventato EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="2f3af-155">CapptainConfiguration now named EngagementConfiguration</span></span>
* <span data-ttu-id="2f3af-156">CapptainAgent è diventato EngagementAgent</span><span class="sxs-lookup"><span data-stu-id="2f3af-156">CapptainAgent now named EngagementAgent</span></span>
* <span data-ttu-id="2f3af-157">CapptainReach è diventato EngagementReach</span><span class="sxs-lookup"><span data-stu-id="2f3af-157">CapptainReach now named EngagementReach</span></span>
* <span data-ttu-id="2f3af-158">CapptainHttpConfig è diventato EngagementHttpConfig</span><span class="sxs-lookup"><span data-stu-id="2f3af-158">CapptainHttpConfig now named EngagementHttpConfig</span></span>
* <span data-ttu-id="2f3af-159">GetCapptainPageName è diventato GetEngagementPageName</span><span class="sxs-lookup"><span data-stu-id="2f3af-159">GetCapptainPageName now named GetEngagementPageName</span></span>

<span data-ttu-id="2f3af-160">Si noti la ridenominazione influisce anche sui metodi sottoposti a override.</span><span class="sxs-lookup"><span data-stu-id="2f3af-160">Note that rename also affects overridden methods.</span></span>

