---
title: Configurazione per Windows Universal App Engagement SDK aaaAdvanced
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
ms.openlocfilehash: 23bd05012bc25d438d8d4985a112280bed0292b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-configuration-for-windows-universal-apps-engagement-sdk"></a><span data-ttu-id="f5229-103">Configurazione avanzata per Engagement SDK per app universali di Windows</span><span class="sxs-lookup"><span data-stu-id="f5229-103">Advanced Configuration for Windows Universal Apps Engagement SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f5229-104">Windows universale</span><span class="sxs-lookup"><span data-stu-id="f5229-104">Universal Windows</span></span>](mobile-engagement-windows-store-advanced-configuration.md)
> * [<span data-ttu-id="f5229-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="f5229-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="f5229-106">iOS</span><span class="sxs-lookup"><span data-stu-id="f5229-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="f5229-107">Android</span><span class="sxs-lookup"><span data-stu-id="f5229-107">Android</span></span>](mobile-engagement-android-advanced-configuration.md)
> 
> 

<span data-ttu-id="f5229-108">Questa procedura viene descritto come tooconfigure varie opzioni di configurazione per le app Android di Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="f5229-108">This procedure describes how tooconfigure various configuration options for Azure Mobile Engagement Android apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f5229-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f5229-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="advanced-configuration"></a><span data-ttu-id="f5229-110">Configurazione avanzata</span><span class="sxs-lookup"><span data-stu-id="f5229-110">Advanced configuration</span></span>
### <a name="disable-automatic-crash-reporting"></a><span data-ttu-id="f5229-111">Disabilitare la segnalazione automatica degli arresti anomali</span><span class="sxs-lookup"><span data-stu-id="f5229-111">Disable automatic crash reporting</span></span>
<span data-ttu-id="f5229-112">È possibile disabilitare hello automatica degli arresti anomali delle funzionalità di impegno report.</span><span class="sxs-lookup"><span data-stu-id="f5229-112">You can disable hello automatic crash reporting feature of Engagement.</span></span> <span data-ttu-id="f5229-113">Quando si verifica un'eccezione non gestita, Engagement non eseguirà alcuna azione.</span><span class="sxs-lookup"><span data-stu-id="f5229-113">Then, when an unhandled exception occurs, Engagement does nothing.</span></span>

> [!WARNING]
> <span data-ttu-id="f5229-114">Se si disabilita questa funzionalità, quindi quando si verifica un arresto anomalo del sistema non gestita dell'app, Engagement non invia l'arresto anomalo di hello **AND** non comporta la chiusura della sessione hello e processi.</span><span class="sxs-lookup"><span data-stu-id="f5229-114">If you disable this feature, then when an unhandled crash occurs in your app, Engagement does not send hello crash **AND** does not close hello session and jobs.</span></span>
> 
> 

<span data-ttu-id="f5229-115">toodisable automatico segnalazioni di arresti anomali, personalizzare la configurazione a seconda della modalità di hello è stata dichiarata:</span><span class="sxs-lookup"><span data-stu-id="f5229-115">toodisable automatic crash reporting, customize your configuration depending on hello way you declared it:</span></span>

#### <a name="from-engagementconfigurationxml-file"></a><span data-ttu-id="f5229-116">Dal file `EngagementConfiguration.xml`</span><span class="sxs-lookup"><span data-stu-id="f5229-116">From `EngagementConfiguration.xml` file</span></span>
<span data-ttu-id="f5229-117">Impostare i report dell'arresto anomalo troppo`false` tra `<reportCrash>` e `</reportCrash>` tag.</span><span class="sxs-lookup"><span data-stu-id="f5229-117">Set report crash too`false` between `<reportCrash>` and `</reportCrash>` tags.</span></span>

#### <a name="from-engagementconfiguration-object-at-run-time"></a><span data-ttu-id="f5229-118">Dall'oggetto `EngagementConfiguration` in fase di esecuzione</span><span class="sxs-lookup"><span data-stu-id="f5229-118">From `EngagementConfiguration` object at run time</span></span>
<span data-ttu-id="f5229-119">Impostare toofalse di arresto anomalo di report utilizzando l'oggetto EngagementConfiguration.</span><span class="sxs-lookup"><span data-stu-id="f5229-119">Set report crash toofalse using your EngagementConfiguration object.</span></span>

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Disable Engagement crash reporting. */
        engagementConfiguration.Agent.ReportCrash = false;

### <a name="disable-real-time-reporting"></a><span data-ttu-id="f5229-120">Disabilitare la segnalazione in tempo reale</span><span class="sxs-lookup"><span data-stu-id="f5229-120">Disable real time reporting</span></span>
<span data-ttu-id="f5229-121">Per impostazione predefinita, i report del servizio di Engagement hello registra in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="f5229-121">By default, hello Engagement service reports logs in real time.</span></span> <span data-ttu-id="f5229-122">Se l'applicazione indica spesso i registri, è preferibile toobuffer hello registri e tooreport usarle in una sola volta in una base di tempo regolari.</span><span class="sxs-lookup"><span data-stu-id="f5229-122">If your application reports logs frequently, it is better toobuffer hello logs and tooreport them all at once on a regular time basis.</span></span> <span data-ttu-id="f5229-123">la cosiddetta "modalità burst".</span><span class="sxs-lookup"><span data-stu-id="f5229-123">This is called “burst mode”.</span></span>

<span data-ttu-id="f5229-124">toodo in tal caso, chiamare il metodo hello:</span><span class="sxs-lookup"><span data-stu-id="f5229-124">toodo so, call hello method:</span></span>

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

<span data-ttu-id="f5229-125">argomento Hello è un valore in **millisecondi**.</span><span class="sxs-lookup"><span data-stu-id="f5229-125">hello argument is a value in **milliseconds**.</span></span> <span data-ttu-id="f5229-126">Ogni volta che si desidera la registrazione in tempo reale di tooreactivate hello, chiamare il metodo hello senza alcun parametro, o con valore 0 hello.</span><span class="sxs-lookup"><span data-stu-id="f5229-126">Whenever you want tooreactivate hello real-time logging, call hello method without any parameter, or with hello 0 value.</span></span>

<span data-ttu-id="f5229-127">Modalità burst leggermente aumenta la durata della batteria hello ma ha un impatto sulle hello Engagement Monitor: durata di tutte le sessioni e i processi vengono arrotondati toohello burst soglia (in questo modo, le sessioni e i processi è inferiore a soglia burst hello potrebbe non essere visibile).</span><span class="sxs-lookup"><span data-stu-id="f5229-127">Burst mode slightly increases hello battery life but has an impact on hello Engagement Monitor: all sessions and jobs duration are rounded toohello burst threshold (thus, sessions and jobs shorter than hello burst threshold may not be visible).</span></span> <span data-ttu-id="f5229-128">È consigliabile usare una soglia di burst non maggiore di 30000, ovvero 30 secondi.</span><span class="sxs-lookup"><span data-stu-id="f5229-128">We recommend using a burst threshold no longer than 30000 (30s).</span></span> <span data-ttu-id="f5229-129">Registri salvati sono elementi too300 limitato.</span><span class="sxs-lookup"><span data-stu-id="f5229-129">Saved logs are limited too300 items.</span></span> <span data-ttu-id="f5229-130">Se l'invio richiede troppo tempo, è possibile che alcuni log vadano persi.</span><span class="sxs-lookup"><span data-stu-id="f5229-130">If sending is too long, you can lose some logs.</span></span>

> [!WARNING]
> <span data-ttu-id="f5229-131">soglia burst Hello non può essere configurato tooa periodo minore secondo.</span><span class="sxs-lookup"><span data-stu-id="f5229-131">hello burst threshold cannot be configured tooa period less than one second.</span></span> <span data-ttu-id="f5229-132">Se in tal caso, hello SDK Mostra una traccia con l'errore hello e reimposta automaticamente toohello valore predefinito zero secondi.</span><span class="sxs-lookup"><span data-stu-id="f5229-132">If you do so, hello SDK shows a trace with hello error and automatically resets toohello default value, zero seconds.</span></span> <span data-ttu-id="f5229-133">Questo trigger prova SDK tooreport prova l'accesso in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="f5229-133">This triggers hello SDK tooreport hello logs in real-time.</span></span>
> 
> 

[here]:http://www.nuget.org/packages/Capptain.WindowsCS
[NuGet website]:http://docs.nuget.org/docs/start-here/overview
