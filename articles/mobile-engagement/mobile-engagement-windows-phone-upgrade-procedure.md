---
title: Procedure di aggiornamento dell'SDK per Windows Phone Silverlight
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
ms.openlocfilehash: f87f65788075c7f4067e77946e1bcbc8f3709317
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="windows-phone-silverlight-sdk-upgrade-procedures"></a><span data-ttu-id="755a9-103">Procedure di aggiornamento dell'SDK per Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="755a9-103">Windows Phone Silverlight SDK Upgrade Procedures</span></span>
<span data-ttu-id="755a9-104">Se è già stata eseguita l'integrazione di una versione precedente dell'SDK nell'applicazione, sarà necessario tenere in considerazione gli aspetti seguenti durante l'aggiornamento dell'SDK.</span><span class="sxs-lookup"><span data-stu-id="755a9-104">If you already have integrated an older version of our SDK into your application, you have to consider the following points when upgrading the SDK.</span></span>

<span data-ttu-id="755a9-105">Se non sono state applicate alcune versioni dell'SDK, potrebbe essere necessario eseguire più procedure.</span><span class="sxs-lookup"><span data-stu-id="755a9-105">You may have to follow several procedures if you missed several versions of the SDK.</span></span> <span data-ttu-id="755a9-106">Se ad esempio si esegue la migrazione dalla versione 0.10.1 alla 0.11.0, sarà prima di tutto necessario eseguire la procedura per la migrazione "dalla 0.9.0 alla 0.10.1" e quindi la procedura per la migrazione "dalla 0.10.1 alla 0.11.0".</span><span class="sxs-lookup"><span data-stu-id="755a9-106">For example if you migrate from 0.10.1 to 0.11.0 you have to first follow the "from 0.9.0 to 0.10.1" procedure then the "from 0.10.1 to 0.11.0" procedure.</span></span>

## <a name="from-200-to-330"></a><span data-ttu-id="755a9-107">Dalla versione 2.0.0 alla 3.3.0</span><span class="sxs-lookup"><span data-stu-id="755a9-107">From 2.0.0 to 3.3.0</span></span>
### <a name="test-logs"></a><span data-ttu-id="755a9-108">Log di test</span><span class="sxs-lookup"><span data-stu-id="755a9-108">Test logs</span></span>
<span data-ttu-id="755a9-109">I log della console generati da SDK possono essere abilitati/disattivati/filtrati.</span><span class="sxs-lookup"><span data-stu-id="755a9-109">Console logs produced by the SDK can now be enabled/disabled/filtered.</span></span> <span data-ttu-id="755a9-110">Per eseguire una personalizzazione, aggiornare la proprietà `EngagementAgent.Instance.TestLogEnabled` scegliendo uno dei valori disponibili nell'enumerazione `EngagementTestLogLevel`, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="755a9-110">To customize this, update the property `EngagementAgent.Instance.TestLogEnabled` to one of the value available from the `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

## <a name="from-111-to-200"></a><span data-ttu-id="755a9-111">Dalla versione 1.1.1 alla 2.0.0</span><span class="sxs-lookup"><span data-stu-id="755a9-111">From 1.1.1 to 2.0.0</span></span>
<span data-ttu-id="755a9-112">La sezione seguente illustra come eseguire la migrazione di un'integrazione dell'SDK dal servizio Capptain offerto da Capptain SAS a un'app basata su Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="755a9-112">The following describes how to migrate an SDK integration from the Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="755a9-113">Capptain e Mobile Engagement sono servizi diversi e la procedura seguente illustra solo come eseguire la migrazione dell'app client.</span><span class="sxs-lookup"><span data-stu-id="755a9-113">Capptain and Mobile Engagement are not the same services and the procedure given below only highlights how to migrate the client app.</span></span> <span data-ttu-id="755a9-114">La migrazione dell'SDK nell'app NON comporta la migrazione dei dati dai server di Capptain ai server di Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="755a9-114">Migrating the SDK in the app will NOT migrate your data from the Capptain servers to the Mobile Engagement servers</span></span>
> 
> 

<span data-ttu-id="755a9-115">Se si esegue la migrazione da una versione precedente, consultare il sito web Capptain per eseguire prima la migrazione a 1.1.1, quindi applicare la procedura seguente</span><span class="sxs-lookup"><span data-stu-id="755a9-115">If you are migrating from an earlier version, please consult the Capptain web site to migrate to 1.1.1 first then apply the following procedure</span></span>

### <a name="nuget-package"></a><span data-ttu-id="755a9-116">Pacchetto NuGet</span><span class="sxs-lookup"><span data-stu-id="755a9-116">Nuget package</span></span>
<span data-ttu-id="755a9-117">Sostituire **Capptain.WindowsPhone** con il pacchetto NuGet **MicrosoftAzure.MobileEngagement**.</span><span class="sxs-lookup"><span data-stu-id="755a9-117">Replace **Capptain.WindowsPhone** by **MicrosoftAzure.MobileEngagement** Nuget package.</span></span>

### <a name="applying-mobile-engagement"></a><span data-ttu-id="755a9-118">Applicazione di Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="755a9-118">Applying Mobile Engagement</span></span>
<span data-ttu-id="755a9-119">L'SDK usa il termine `Engagement`.</span><span class="sxs-lookup"><span data-stu-id="755a9-119">The SDK uses the term `Engagement`.</span></span> <span data-ttu-id="755a9-120">È necessario aggiornare il progetto per tenere conto di questa modifica.</span><span class="sxs-lookup"><span data-stu-id="755a9-120">You need to update your project to match this change.</span></span>

<span data-ttu-id="755a9-121">È necessario disinstallare il pacchetto nuget corrente di Capptain.</span><span class="sxs-lookup"><span data-stu-id="755a9-121">You need to uninstall your current Capptain nuget package.</span></span> <span data-ttu-id="755a9-122">Si consideri che verranno rimosse tutte le modifiche nella cartella Risorse di Capptain.</span><span class="sxs-lookup"><span data-stu-id="755a9-122">Consider that all your changes in Capptain Resources folder will be removed.</span></span> <span data-ttu-id="755a9-123">Se si desidera mantenere tali file, eseguirne una copia.</span><span class="sxs-lookup"><span data-stu-id="755a9-123">If you want to keep those files then make a copy of them.</span></span>

<span data-ttu-id="755a9-124">Successivamente, installare il nuovo pacchetto NuGet di Microsoft Azure Engagement nel progetto.</span><span class="sxs-lookup"><span data-stu-id="755a9-124">After that, install the new Microsoft Azure Engagement nuget package on your project.</span></span> <span data-ttu-id="755a9-125">È possibile trovarlo direttamente sul sito Web di [NuGet](http://www.nuget.org/packages/MicrosoftAzure.MobileEngagement).</span><span class="sxs-lookup"><span data-stu-id="755a9-125">You can find it directly on [Nuget](http://www.nuget.org/packages/MicrosoftAzure.MobileEngagement).</span></span> <span data-ttu-id="755a9-126">Questa operazione sostituisce tutti i file di risorse utilizzati da Engagement e aggiunge la nuova DLL di Engagement ai riferimenti del progetto.</span><span class="sxs-lookup"><span data-stu-id="755a9-126">This action replaces all resources files used by Engagement and adds the new Engagement DLL to your project References.</span></span>

<span data-ttu-id="755a9-127">È necessario eliminare i riferimenti del progetto rimuovendo i riferimenti DLL di Capptain.</span><span class="sxs-lookup"><span data-stu-id="755a9-127">You have to clean your project references by deleting Capptain DLL references.</span></span> <span data-ttu-id="755a9-128">Se non si effettua questa operazione, la versione di Capptain creerà un conflitto e si verificheranno errori.</span><span class="sxs-lookup"><span data-stu-id="755a9-128">If you do not make this, the version of Capptain will conflict and errors will happen.</span></span>

<span data-ttu-id="755a9-129">Se sono state personalizzate risorse Capptain, copiare il contenuto dei file precedenti e incollarlo in nuovi file di progetto.</span><span class="sxs-lookup"><span data-stu-id="755a9-129">If you have customized Capptain resources, copy your old files content and paste them in the new Engagement files.</span></span> <span data-ttu-id="755a9-130">Si noti che è necessario aggiornare sia i file xaml che i file cs.</span><span class="sxs-lookup"><span data-stu-id="755a9-130">Please note that both xaml and cs files have to be updated.</span></span>

<span data-ttu-id="755a9-131">Al termine di queste operazioni, è necessario sostituire i riferimenti di Capptain precedenti con i nuovi riferimenti di Engagement.</span><span class="sxs-lookup"><span data-stu-id="755a9-131">When those steps are completed you only have to replace old Capptain references by the new Engagement references.</span></span>

1. <span data-ttu-id="755a9-132">Tutti gli spazi dei nomi Capptain devono essere aggiornati.</span><span class="sxs-lookup"><span data-stu-id="755a9-132">All Capptain namespaces have to be updated.</span></span>
   
    <span data-ttu-id="755a9-133">Prima della migrazione:</span><span class="sxs-lookup"><span data-stu-id="755a9-133">Before migration:</span></span>
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    <span data-ttu-id="755a9-134">Dopo la migrazione:</span><span class="sxs-lookup"><span data-stu-id="755a9-134">After migration:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="755a9-135">Tutte le classi Capptain che contengono "Capptain" devono contenere "Engagement".</span><span class="sxs-lookup"><span data-stu-id="755a9-135">All Capptain classes that contain "Capptain" should contain "Engagement".</span></span>
   
    <span data-ttu-id="755a9-136">Prima della migrazione:</span><span class="sxs-lookup"><span data-stu-id="755a9-136">Before migration:</span></span>
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    <span data-ttu-id="755a9-137">Dopo la migrazione:</span><span class="sxs-lookup"><span data-stu-id="755a9-137">After migration:</span></span>
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. <span data-ttu-id="755a9-138">Per i file xaml cambiano anche attributi e spazio dei nomi di Capptain.</span><span class="sxs-lookup"><span data-stu-id="755a9-138">For xaml files Capptain namespace and attributes also change.</span></span>
   
    <span data-ttu-id="755a9-139">Prima della migrazione:</span><span class="sxs-lookup"><span data-stu-id="755a9-139">Before migration:</span></span>
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    <span data-ttu-id="755a9-140">Dopo la migrazione:</span><span class="sxs-lookup"><span data-stu-id="755a9-140">After migration:</span></span>
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. <span data-ttu-id="755a9-141">Per altre risorse come le immagini di Capptain, tenere presente che sono state rinominate per l'utilizzo di "Engagement".</span><span class="sxs-lookup"><span data-stu-id="755a9-141">For the other resources like Capptain pictures, please note that they also have been renamed to use "Engagement".</span></span>

### <a name="application-id--sdk-key"></a><span data-ttu-id="755a9-142">ID applicazione / chiave SDK</span><span class="sxs-lookup"><span data-stu-id="755a9-142">Application ID / SDK Key</span></span>
<span data-ttu-id="755a9-143">Engagement utilizza una stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="755a9-143">Engagement uses a connection string.</span></span> <span data-ttu-id="755a9-144">Non è necessario specificare un ID applicazione e una chiave SDK con Mobile Engagement, è sufficiente specificare una stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="755a9-144">You don't have to specify an application ID and an SDK key with Mobile Engagement, you only have to specify a connection string.</span></span> <span data-ttu-id="755a9-145">È possibile configurarla nel file EngagementConfiguration.</span><span class="sxs-lookup"><span data-stu-id="755a9-145">You can set it up on your EngagementConfiguration file.</span></span>

<span data-ttu-id="755a9-146">La configurazione di Engagement può essere impostata nel file `Resources\EngagementConfiguration.xml` del progetto.</span><span class="sxs-lookup"><span data-stu-id="755a9-146">The Engagement configuration can be set in your `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="755a9-147">Modificare questo file per specificare:</span><span class="sxs-lookup"><span data-stu-id="755a9-147">Edit this file to specify:</span></span>

* <span data-ttu-id="755a9-148">La stringa di connessione dell'applicazione tra i tag `<connectionString>` and `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="755a9-148">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="755a9-149">Se si desidera specificarla in fase di esecuzione, è possibile chiamare il metodo seguente prima dell'inizializzazione dell'agente di Engagement:</span><span class="sxs-lookup"><span data-stu-id="755a9-149">If you want to specify it at runtime instead, you can call the following method before the Engagement agent initialization:</span></span>

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Initialize Engagement angent with above configuration. */
        EngagementAgent.Instance.Init(engagementConfiguration);

<span data-ttu-id="755a9-150">La stringa di connessione per l'applicazione viene visualizzata nel portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="755a9-150">The connection string for your application is displayed in the Azure Classic Portal.</span></span>

### <a name="items-name-change"></a><span data-ttu-id="755a9-151">Modifica del nome di elementi</span><span class="sxs-lookup"><span data-stu-id="755a9-151">Items name change</span></span>
<span data-ttu-id="755a9-152">Tutti gli elementi denominati *capptain* sono stati rinominati in *engagement*.</span><span class="sxs-lookup"><span data-stu-id="755a9-152">All items named *capptain* have been named *engagement*.</span></span> <span data-ttu-id="755a9-153">Lo stesso vale per *Capptain*, che è stato ridenominato in *Engagement*.</span><span class="sxs-lookup"><span data-stu-id="755a9-153">Similarly for *Capptain* to *Engagement*.</span></span>

<span data-ttu-id="755a9-154">Esempi di elementi di Capptain di uso comune:</span><span class="sxs-lookup"><span data-stu-id="755a9-154">Examples of commonly used Capptain items :</span></span>

* <span data-ttu-id="755a9-155">CapptainConfiguration è diventato EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="755a9-155">CapptainConfiguration now named EngagementConfiguration</span></span>
* <span data-ttu-id="755a9-156">CapptainAgent è diventato EngagementAgent</span><span class="sxs-lookup"><span data-stu-id="755a9-156">CapptainAgent now named EngagementAgent</span></span>
* <span data-ttu-id="755a9-157">CapptainReach è diventato EngagementReach</span><span class="sxs-lookup"><span data-stu-id="755a9-157">CapptainReach now named EngagementReach</span></span>
* <span data-ttu-id="755a9-158">CapptainHttpConfig è diventato EngagementHttpConfig</span><span class="sxs-lookup"><span data-stu-id="755a9-158">CapptainHttpConfig now named EngagementHttpConfig</span></span>
* <span data-ttu-id="755a9-159">GetCapptainPageName è diventato GetEngagementPageName</span><span class="sxs-lookup"><span data-stu-id="755a9-159">GetCapptainPageName now named GetEngagementPageName</span></span>

<span data-ttu-id="755a9-160">Si noti la ridenominazione influisce anche sui metodi sottoposti a override.</span><span class="sxs-lookup"><span data-stu-id="755a9-160">Note that rename also affects overridden methods.</span></span>

