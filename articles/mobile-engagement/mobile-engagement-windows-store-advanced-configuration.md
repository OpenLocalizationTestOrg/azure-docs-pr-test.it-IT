---
title: Configurazione avanzata per Engagement SDK per app universali di Windows
description: Opzioni di configurazione avanzata per Azure Mobile Engagement per app universali di Windows
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6d85dd5d-ac07-43ba-bbe4-e91c3a17690b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 10/04/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: cb9454212c94cf65093219c3d24c71277ede7877
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="advanced-configuration-for-windows-universal-apps-engagement-sdk"></a><span data-ttu-id="d6d23-103">Configurazione avanzata per Engagement SDK per app universali di Windows</span><span class="sxs-lookup"><span data-stu-id="d6d23-103">Advanced Configuration for Windows Universal Apps Engagement SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d6d23-104">Windows universale</span><span class="sxs-lookup"><span data-stu-id="d6d23-104">Universal Windows</span></span>](mobile-engagement-windows-store-advanced-configuration.md)
> * [<span data-ttu-id="d6d23-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="d6d23-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="d6d23-106">iOS</span><span class="sxs-lookup"><span data-stu-id="d6d23-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="d6d23-107">Android</span><span class="sxs-lookup"><span data-stu-id="d6d23-107">Android</span></span>](mobile-engagement-android-advanced-configuration.md)
> 
> 

<span data-ttu-id="d6d23-108">Questa procedura descrive come configurare le diverse opzioni di configurazione per le app Android di Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="d6d23-108">This procedure describes how to configure various configuration options for Azure Mobile Engagement Android apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d6d23-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d6d23-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="advanced-configuration"></a><span data-ttu-id="d6d23-110">Configurazione avanzata</span><span class="sxs-lookup"><span data-stu-id="d6d23-110">Advanced configuration</span></span>
### <a name="disable-automatic-crash-reporting"></a><span data-ttu-id="d6d23-111">Disabilitare la segnalazione automatica degli arresti anomali</span><span class="sxs-lookup"><span data-stu-id="d6d23-111">Disable automatic crash reporting</span></span>
<span data-ttu-id="d6d23-112">È possibile disabilitare la funzionalità di segnalazione automatica degli arresti anomali di Engagement.</span><span class="sxs-lookup"><span data-stu-id="d6d23-112">You can disable the automatic crash reporting feature of Engagement.</span></span> <span data-ttu-id="d6d23-113">Quando si verifica un'eccezione non gestita, Engagement non eseguirà alcuna azione.</span><span class="sxs-lookup"><span data-stu-id="d6d23-113">Then, when an unhandled exception occurs, Engagement does nothing.</span></span>

> [!WARNING]
> <span data-ttu-id="d6d23-114">Se si disabilita questa funzionalità, quando si verifica un arresto anomalo non gestito nell'app, Engagement non lo invierà **E** non chiuderà la sessione e i processi.</span><span class="sxs-lookup"><span data-stu-id="d6d23-114">If you disable this feature, then when an unhandled crash occurs in your app, Engagement does not send the crash **AND** does not close the session and jobs.</span></span>
> 
> 

<span data-ttu-id="d6d23-115">Per disabilitare la segnalazione automatica degli arresti anomali, personalizzare la configurazione in base al modo in cui che è stata dichiarata:</span><span class="sxs-lookup"><span data-stu-id="d6d23-115">To disable automatic crash reporting, customize your configuration depending on the way you declared it:</span></span>

#### <a name="from-engagementconfigurationxml-file"></a><span data-ttu-id="d6d23-116">Dal file `EngagementConfiguration.xml`</span><span class="sxs-lookup"><span data-stu-id="d6d23-116">From `EngagementConfiguration.xml` file</span></span>
<span data-ttu-id="d6d23-117">Impostare la segnalazione degli arresti anomali su `false` tra i tag `<reportCrash>` e `</reportCrash>`.</span><span class="sxs-lookup"><span data-stu-id="d6d23-117">Set report crash to `false` between `<reportCrash>` and `</reportCrash>` tags.</span></span>

#### <a name="from-engagementconfiguration-object-at-run-time"></a><span data-ttu-id="d6d23-118">Dall'oggetto `EngagementConfiguration` in fase di esecuzione</span><span class="sxs-lookup"><span data-stu-id="d6d23-118">From `EngagementConfiguration` object at run time</span></span>
<span data-ttu-id="d6d23-119">Impostare la segnalazione degli arresti anomali su false usando l'oggetto EngagementConfiguration.</span><span class="sxs-lookup"><span data-stu-id="d6d23-119">Set report crash to false using your EngagementConfiguration object.</span></span>

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Disable Engagement crash reporting. */
        engagementConfiguration.Agent.ReportCrash = false;

### <a name="disable-real-time-reporting"></a><span data-ttu-id="d6d23-120">Disabilitare la segnalazione in tempo reale</span><span class="sxs-lookup"><span data-stu-id="d6d23-120">Disable real time reporting</span></span>
<span data-ttu-id="d6d23-121">Per impostazione predefinita, il servizio Engagement segnala i log in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="d6d23-121">By default, the Engagement service reports logs in real time.</span></span> <span data-ttu-id="d6d23-122">Se l'applicazione segnala spesso i log, è preferibile memorizzare i log nel buffer e segnalarli tutti insieme con cadenza regolare,</span><span class="sxs-lookup"><span data-stu-id="d6d23-122">If your application reports logs frequently, it is better to buffer the logs and to report them all at once on a regular time basis.</span></span> <span data-ttu-id="d6d23-123">la cosiddetta "modalità burst".</span><span class="sxs-lookup"><span data-stu-id="d6d23-123">This is called “burst mode”.</span></span>

<span data-ttu-id="d6d23-124">A tale scopo, chiamare il metodo:</span><span class="sxs-lookup"><span data-stu-id="d6d23-124">To do so, call the method:</span></span>

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

<span data-ttu-id="d6d23-125">L'argomento è un valore in **millisecondi**.</span><span class="sxs-lookup"><span data-stu-id="d6d23-125">The argument is a value in **milliseconds**.</span></span> <span data-ttu-id="d6d23-126">Ogni volta che si vuole riattivare la registrazione in tempo reale, chiamare il metodo senza alcun parametro o con il valore 0.</span><span class="sxs-lookup"><span data-stu-id="d6d23-126">Whenever you want to reactivate the real-time logging, call the method without any parameter, or with the 0 value.</span></span>

<span data-ttu-id="d6d23-127">La modalità burst aumenta lievemente la durata della batteria ma ha un impatto su Monitor di Engagement: la durata di tutte le sessioni e di tutti i processi viene arrotondata alla soglia di burst e, di conseguenza, le sessioni e i processi inferiori alla soglia di burst potrebbero non essere visibili.</span><span class="sxs-lookup"><span data-stu-id="d6d23-127">Burst mode slightly increases the battery life but has an impact on the Engagement Monitor: all sessions and jobs duration are rounded to the burst threshold (thus, sessions and jobs shorter than the burst threshold may not be visible).</span></span> <span data-ttu-id="d6d23-128">È consigliabile usare una soglia di burst non maggiore di 30000, ovvero 30 secondi.</span><span class="sxs-lookup"><span data-stu-id="d6d23-128">We recommend using a burst threshold no longer than 30000 (30s).</span></span> <span data-ttu-id="d6d23-129">Per i log salvati è previsto un limite di 300 elementi.</span><span class="sxs-lookup"><span data-stu-id="d6d23-129">Saved logs are limited to 300 items.</span></span> <span data-ttu-id="d6d23-130">Se l'invio richiede troppo tempo, è possibile che alcuni log vadano persi.</span><span class="sxs-lookup"><span data-stu-id="d6d23-130">If sending is too long, you can lose some logs.</span></span>

> [!WARNING]
> <span data-ttu-id="d6d23-131">La soglia di burst non può essere configurata per un periodo inferiore a un secondo.</span><span class="sxs-lookup"><span data-stu-id="d6d23-131">The burst threshold cannot be configured to a period less than one second.</span></span> <span data-ttu-id="d6d23-132">Se si imposta un valore minore, l'SDK mostrerà una traccia con l'errore e verrà reimpostato automaticamente sul valore predefinito, vale a dire, zero secondi.</span><span class="sxs-lookup"><span data-stu-id="d6d23-132">If you do so, the SDK shows a trace with the error and automatically resets to the default value, zero seconds.</span></span> <span data-ttu-id="d6d23-133">In questo modo si attiva l'SDK per la segnalazione dei log in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="d6d23-133">This triggers the SDK to report the logs in real-time.</span></span>
> 
> 

[here]:http://www.nuget.org/packages/Capptain.WindowsCS
[NuGet website]:http://docs.nuget.org/docs/start-here/overview
