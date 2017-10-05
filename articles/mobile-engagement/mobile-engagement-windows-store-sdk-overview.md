---
title: Azure Mobile Engagement - Integrazione di Windows Universal SDK | Documentazione Microsoft
description: Integrazione di Windows Universal per SDK per Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 9ded187d-5c07-4377-a41c-ce205dd38b50
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 11/03/2016
ms.author: piyushjo
ms.openlocfilehash: d616ad58156a19e89b3e106639a38df67cbd0abb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="windows-universal-sdk-integration-for-azure-mobile-engagement"></a><span data-ttu-id="40803-103">Integrazione di Windows Universal SDK per Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="40803-103">Windows Universal SDK Integration for Azure Mobile Engagement</span></span>
<span data-ttu-id="40803-104">Questo documento descrive tutte le opzioni di configurazione e integrazione disponibili per Windows Universal SDK per Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="40803-104">This document describes all the integration and configuration options available for the Azure Mobile Engagement Windows Universal SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="40803-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="40803-105">Prerequisites</span></span>
<span data-ttu-id="40803-106">Prima di iniziare questa esercitazione, è necessario completare l' [esercitazione di 15 minuti](mobile-engagement-windows-store-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="40803-106">Before starting this tutorial, you must first complete our [15-minute tutorial](mobile-engagement-windows-store-dotnet-get-started.md).</span></span>

## <a name="advanced-features"></a><span data-ttu-id="40803-107">Funzionalità avanzate</span><span class="sxs-lookup"><span data-stu-id="40803-107">Advanced features</span></span>
### <a name="reporting-features"></a><span data-ttu-id="40803-108">Funzionalità di segnalazione</span><span class="sxs-lookup"><span data-stu-id="40803-108">Reporting features</span></span>
<span data-ttu-id="40803-109">È possibile aggiungere queste funzionalità:</span><span class="sxs-lookup"><span data-stu-id="40803-109">You can add these features:</span></span>

1. [<span data-ttu-id="40803-110">Opzioni di segnalazione avanzata</span><span class="sxs-lookup"><span data-stu-id="40803-110">Advanced reporting options</span></span>](mobile-engagement-windows-store-advanced-reporting.md)
2. [<span data-ttu-id="40803-111">Opzioni di configurazione avanzate</span><span class="sxs-lookup"><span data-stu-id="40803-111">Advanced configuration options</span></span>](mobile-engagement-windows-store-advanced-configuration.md)

### <a name="notifications"></a><span data-ttu-id="40803-112">Notifiche</span><span class="sxs-lookup"><span data-stu-id="40803-112">Notifications</span></span>
[<span data-ttu-id="40803-113">Come integrare il servizio di copertura (di notifica) in un'app universale di Windows</span><span class="sxs-lookup"><span data-stu-id="40803-113">How to integrate Reach (Notifications) in your Windows Universal app</span></span>](mobile-engagement-windows-store-integrate-engagement-reach.md)

### <a name="tag-plan-implementation"></a><span data-ttu-id="40803-114">Implementazione del piano di tag:</span><span class="sxs-lookup"><span data-stu-id="40803-114">Tag plan implementation:</span></span>
[<span data-ttu-id="40803-115">Come usare l'API per l'assegnazione di tag avanzata di Mobile Engagement in un'app universale di Windows</span><span class="sxs-lookup"><span data-stu-id="40803-115">How to use the advanced Mobile Engagement tagging API in your Windows Universal app</span></span>](mobile-engagement-windows-store-use-engagement-api.md)

## <a name="release-notes"></a><span data-ttu-id="40803-116">Note sulla versione</span><span class="sxs-lookup"><span data-stu-id="40803-116">Release notes</span></span>
### <a name="341-11032016"></a><span data-ttu-id="40803-117">3.4.1 (11/03/2016)</span><span class="sxs-lookup"><span data-stu-id="40803-117">3.4.1 (11/03/2016)</span></span>

* <span data-ttu-id="40803-118">Miglioramenti della stabilità.</span><span class="sxs-lookup"><span data-stu-id="40803-118">Stability improvements.</span></span>

<span data-ttu-id="40803-119">Per le versioni precedenti, vedere le [note sulla versione complete](mobile-engagement-windows-store-release-notes.md)</span><span class="sxs-lookup"><span data-stu-id="40803-119">For earlier versions, see the [complete release notes](mobile-engagement-windows-store-release-notes.md)</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="40803-120">Procedure di aggiornamento</span><span class="sxs-lookup"><span data-stu-id="40803-120">Upgrade procedures</span></span>
<span data-ttu-id="40803-121">Se nell'applicazione è già stata integrata una versione precedente dell'SDK, è necessario considerare i seguenti punti quando si aggiorna l'SDK.</span><span class="sxs-lookup"><span data-stu-id="40803-121">If you already have integrated an older version of Engagement into your application, you have to consider the following points when upgrading the SDK.</span></span>

<span data-ttu-id="40803-122">Se non sono state applicate diverse versioni dell'SDK, potrebbe essere necessario eseguire più procedure.</span><span class="sxs-lookup"><span data-stu-id="40803-122">If you missed several versions of the SDK, you may have to follow several procedures.</span></span> <span data-ttu-id="40803-123">Vedere quindi le [procedure di aggiornamento](mobile-engagement-windows-store-upgrade-procedure.md)complete.</span><span class="sxs-lookup"><span data-stu-id="40803-123">See the complete [Upgrade Procedures](mobile-engagement-windows-store-upgrade-procedure.md).</span></span> <span data-ttu-id="40803-124">Se ad esempio si esegue la migrazione dalla versione 0.10.1 alla 0.11.0, sarà prima di tutto necessario eseguire la procedura per la migrazione "dalla 0.9.0 alla 0.10.1" e quindi la procedura per la migrazione "dalla 0.10.1 alla 0.11.0".</span><span class="sxs-lookup"><span data-stu-id="40803-124">For example if you migrate from 0.10.1 to 0.11.0 you have to first follow the "from 0.9.0 to 0.10.1" procedure then the "from 0.10.1 to 0.11.0" procedure.</span></span>

### <a name="from-330-to-340"></a><span data-ttu-id="40803-125">Dalla versione 3.3.0 alla 3.4.0</span><span class="sxs-lookup"><span data-stu-id="40803-125">From 3.3.0 to 3.4.0</span></span>
#### <a name="test-logs"></a><span data-ttu-id="40803-126">Log di test</span><span class="sxs-lookup"><span data-stu-id="40803-126">Test logs</span></span>
<span data-ttu-id="40803-127">I log della console generati da SDK possono essere abilitati/disattivati/filtrati.</span><span class="sxs-lookup"><span data-stu-id="40803-127">Console logs produced by the SDK can now be enabled/disabled/filtered.</span></span> <span data-ttu-id="40803-128">Per personalizzare, aggiornare la proprietà `EngagementAgent.Instance.TestLogEnabled` scegliendo uno dei valori disponibili nell'enumerazione `EngagementTestLogLevel`, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="40803-128">To customize, update the property `EngagementAgent.Instance.TestLogEnabled` to one of the values available from the `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

#### <a name="resources"></a><span data-ttu-id="40803-129">Risorse</span><span class="sxs-lookup"><span data-stu-id="40803-129">Resources</span></span>
<span data-ttu-id="40803-130">La sovrimpressione Reach è stata migliorata.</span><span class="sxs-lookup"><span data-stu-id="40803-130">The Reach overlay has been improved.</span></span> <span data-ttu-id="40803-131">Fa parte delle risorse del pacchetto NuGet di SDK.</span><span class="sxs-lookup"><span data-stu-id="40803-131">It is part of the SDK NuGet package resources.</span></span>

<span data-ttu-id="40803-132">Durante l'aggiornamento alla nuova versione di SDK, è possibile scegliere se mantenere i file esistenti contenuti nella cartella della sovrimpressione delle risorse:</span><span class="sxs-lookup"><span data-stu-id="40803-132">While upgrading to the new version of the SDK, you can choose whether you want to keep your existing files from the overlay folder of your resources or not:</span></span>

* <span data-ttu-id="40803-133">Se la sovrimpressione precedente è in funzione o si stanno integrando manualmente gli elementi `WebView` , è possibile decidere di mantenere i file esistenti per poter proseguire.</span><span class="sxs-lookup"><span data-stu-id="40803-133">If the previous overlay is working for you, or you are integrating the `WebView` elements manually, then you can decide to keep your exiting files, it will still work.</span></span>
* <span data-ttu-id="40803-134">Per passare alla sovrimpressione nuova, sostituire l'intera cartella `overlay` delle risorse con quella nuova disponibile nel pacchetto SDK. Dopo aver completo l'aggiornamento, nelle app UWP è possibile ottenere la cartella della nuova sovrimpressione da %USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources.</span><span class="sxs-lookup"><span data-stu-id="40803-134">To update to the new overlay, replace the whole `overlay` folder from your resources with the new one from the SDK package (UWP apps: after the upgrade, you can get the new overlay folder from %USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).</span></span>

> [!WARNING]
> <span data-ttu-id="40803-135">Se si usa la sovrimpressione nuova, le personalizzazioni eseguite con la versione precedente saranno sovrascritte.</span><span class="sxs-lookup"><span data-stu-id="40803-135">Using the new overlay overwrites any customizations made on the previous version.</span></span>
> 
> 

### <a name="upgrade-from-older-versions"></a><span data-ttu-id="40803-136">Eseguire l'aggiornamento da versioni precedenti</span><span class="sxs-lookup"><span data-stu-id="40803-136">Upgrade from older versions</span></span>
<span data-ttu-id="40803-137">Vedere [Upgrade Procedures](mobile-engagement-windows-store-upgrade-procedure.md)</span><span class="sxs-lookup"><span data-stu-id="40803-137">See [Upgrade Procedures](mobile-engagement-windows-store-upgrade-procedure.md)</span></span>

