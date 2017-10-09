---
title: aaaExploring HockeyApp dati in Azure Application Insights | Documenti Microsoft
description: Analizzare l'utilizzo e le prestazioni dell'app Azure con Application Insights.
services: application-insights
documentationcenter: windows
author: CFreemanwa
manager: carmonm
ms.assetid: 97783cc6-67d6-465f-9926-cb9821f4176e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: bwren
ms.openlocfilehash: ed7cf99b48f5ec78d6b401bb954cfcd014b9d1f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="exploring-hockeyapp-data-in-application-insights"></a><span data-ttu-id="1fdc9-103">Esplorazione dei dati HockeyApp in Application Insights</span><span class="sxs-lookup"><span data-stu-id="1fdc9-103">Exploring HockeyApp data in Application Insights</span></span>
<span data-ttu-id="1fdc9-104">[HockeyApp](https://azure.microsoft.com/services/hockeyapp/) hello consiglia di piattaforma per il monitoraggio in tempo reale App desktop e mobile.</span><span class="sxs-lookup"><span data-stu-id="1fdc9-104">[HockeyApp](https://azure.microsoft.com/services/hockeyapp/) is hello recommended platform for monitoring live desktop and mobile apps.</span></span> <span data-ttu-id="1fdc9-105">Da HockeyApp, è possibile inviare personalizzato e di traccia dell'utilizzo di dati di telemetria toomonitor e facilitare la diagnosi (nei dati di arresto anomalo di addizione toogetting).</span><span class="sxs-lookup"><span data-stu-id="1fdc9-105">From HockeyApp, you can send custom and trace telemetry toomonitor usage and assist in diagnosis (in addition toogetting crash data).</span></span> <span data-ttu-id="1fdc9-106">Questo flusso di dati di telemetria è possibile eseguire query tramite hello avanzato [Analitica](app-insights-analytics.md) funzionalità di [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1fdc9-106">This stream of telemetry can be queried using hello powerful [Analytics](app-insights-analytics.md) feature of [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="1fdc9-107">È inoltre possibile [esportare hello personalizzato e i dati di telemetria di traccia](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="1fdc9-107">In addition, you can [export hello custom and trace telemetry](app-insights-export-telemetry.md).</span></span> <span data-ttu-id="1fdc9-108">tooenable queste funzionalità, è possibile impostare un bridge che inoltra i dati personalizzati di HockeyApp tooApplication Insights.</span><span class="sxs-lookup"><span data-stu-id="1fdc9-108">tooenable these features, you set up a bridge that relays HockeyApp custom data tooApplication Insights.</span></span>

## <a name="hello-hockeyapp-bridge-app"></a><span data-ttu-id="1fdc9-109">app HockeyApp Bridge Hello</span><span class="sxs-lookup"><span data-stu-id="1fdc9-109">hello HockeyApp Bridge app</span></span>
<span data-ttu-id="1fdc9-110">Hello HockeyApp Bridge App è una funzionalità principale hello che consente di tooaccess la telemetria di traccia in Application Insights tramite hello Analitica HockeyApp personalizzati e le funzionalità di esportazione continua.</span><span class="sxs-lookup"><span data-stu-id="1fdc9-110">hello HockeyApp Bridge App is hello core feature that enables you tooaccess your HockeyApp custom and trace telemetry in Application Insights through hello Analytics and Continuous Export features.</span></span> <span data-ttu-id="1fdc9-111">Eventi personalizzati e di traccia raccolti da HockeyApp dopo la creazione di hello di hello HockeyApp Bridge App sarà accessibili da queste funzionalità.</span><span class="sxs-lookup"><span data-stu-id="1fdc9-111">Custom and trace events collected by HockeyApp after hello creation of hello HockeyApp Bridge App will be accessible from these features.</span></span> <span data-ttu-id="1fdc9-112">Di seguito viene illustrato come tooset di una di queste App Bridge.</span><span class="sxs-lookup"><span data-stu-id="1fdc9-112">Let’s see how tooset up one of these Bridge Apps.</span></span>

<span data-ttu-id="1fdc9-113">In HockeyApp aprire Account Settings (Impostazioni account), [API Tokens](https://rink.hockeyapp.net/manage/auth_tokens)(Token API).</span><span class="sxs-lookup"><span data-stu-id="1fdc9-113">In HockeyApp, open Account Settings, [API Tokens](https://rink.hockeyapp.net/manage/auth_tokens).</span></span> <span data-ttu-id="1fdc9-114">Creare un token oppure usarne uno esistente.</span><span class="sxs-lookup"><span data-stu-id="1fdc9-114">Either create a new token or reuse an existing one.</span></span> <span data-ttu-id="1fdc9-115">diritti minimi Hello necessarie sono "di sola lettura".</span><span class="sxs-lookup"><span data-stu-id="1fdc9-115">hello minimum rights required are "read only".</span></span> <span data-ttu-id="1fdc9-116">Eseguire una copia di hello API token.</span><span class="sxs-lookup"><span data-stu-id="1fdc9-116">Take a copy of hello API token.</span></span>

![Ottenere un token API HockeyApp](./media/app-insights-hockeyapp-bridge-app/01.png)

<span data-ttu-id="1fdc9-118">Portale di Microsoft Azure aprire hello e [creare una risorsa di Application Insights](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="1fdc9-118">Open hello Microsoft Azure portal and [create an Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="1fdc9-119">Impostare il tipo di applicazione troppo "Applicazione bridge HockeyApp":</span><span class="sxs-lookup"><span data-stu-id="1fdc9-119">Set Application Type too“HockeyApp bridge application”:</span></span>

![Nuova risorsa di Application Insights](./media/app-insights-hockeyapp-bridge-app/02.png)

<span data-ttu-id="1fdc9-121">Non devi tooset un nome, questo verrà impostato automaticamente dal nome HockeyApp hello.</span><span class="sxs-lookup"><span data-stu-id="1fdc9-121">You don't need tooset a name - this will automatically be set from hello HockeyApp name.</span></span>

<span data-ttu-id="1fdc9-122">Hello HockeyApp bridge campi vengono visualizzati.</span><span class="sxs-lookup"><span data-stu-id="1fdc9-122">hello HockeyApp bridge fields appear.</span></span> 

![Immettere i campi dell'app bridge](./media/app-insights-hockeyapp-bridge-app/03.png)

<span data-ttu-id="1fdc9-124">Immettere il token di HockeyApp hello annotati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="1fdc9-124">Enter hello HockeyApp token you noted earlier.</span></span> <span data-ttu-id="1fdc9-125">Questa azione consente di popolare menu a discesa di "HockeyApp applicazione" hello con tutte le applicazioni HockeyApp.</span><span class="sxs-lookup"><span data-stu-id="1fdc9-125">This action populates hello “HockeyApp Application” dropdown menu with all your HockeyApp applications.</span></span> <span data-ttu-id="1fdc9-126">Selezionare hello uno desiderata toouse e resto hello completo di campi di hello.</span><span class="sxs-lookup"><span data-stu-id="1fdc9-126">Select hello one you want toouse, and complete hello remainder of hello fields.</span></span> 

<span data-ttu-id="1fdc9-127">Aprire una nuova risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="1fdc9-127">Open hello new resource.</span></span> 

<span data-ttu-id="1fdc9-128">Si noti che i dati di hello richiede un po' di tempo toostart propagazione.</span><span class="sxs-lookup"><span data-stu-id="1fdc9-128">Note that hello data takes a while toostart flowing.</span></span>

![Risorsa di Application Insights in attesa dei dati](./media/app-insights-hockeyapp-bridge-app/04.png)

<span data-ttu-id="1fdc9-130">La procedura è terminata.</span><span class="sxs-lookup"><span data-stu-id="1fdc9-130">That’s it!</span></span> <span data-ttu-id="1fdc9-131">Dati personalizzati e di traccia raccolti nell'applicazione instrumentata HockeyApp da questo punto in avanti sono anche disponibile tooyou in hello Analitica e funzionalità esportazione continua di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="1fdc9-131">Custom and trace data collected in your HockeyApp-instrumented app from this point forward is now also available tooyou in hello Analytics and Continuous Export features of Application Insights.</span></span>

<span data-ttu-id="1fdc9-132">Brevemente esaminare ognuno di questi tooyou ora disponibili le funzionalità.</span><span class="sxs-lookup"><span data-stu-id="1fdc9-132">Let’s briefly review each of these features now available tooyou.</span></span>

## <a name="analytics"></a><span data-ttu-id="1fdc9-133">Analytics</span><span class="sxs-lookup"><span data-stu-id="1fdc9-133">Analytics</span></span>
<span data-ttu-id="1fdc9-134">Analitica è uno strumento potente per ad hoc l'esecuzione di query dei dati, consentendo toodiagnose e analizza i dati di telemetria e individua rapidamente le cause principali e modelli.</span><span class="sxs-lookup"><span data-stu-id="1fdc9-134">Analytics is a powerful tool for ad-hoc querying of your data, allowing you toodiagnose and analyze your telemetry and quickly discover root causes and patterns.</span></span>

![Analytics](./media/app-insights-hockeyapp-bridge-app/05.png)

* [<span data-ttu-id="1fdc9-136">Altre informazioni su Analisi</span><span class="sxs-lookup"><span data-stu-id="1fdc9-136">Learn more about Analytics</span></span>](app-insights-analytics-tour.md)

## <a name="continuous-export"></a><span data-ttu-id="1fdc9-137">Esportazione continua</span><span class="sxs-lookup"><span data-stu-id="1fdc9-137">Continuous export</span></span>
<span data-ttu-id="1fdc9-138">Tooexport consente l'esportazione continua dei dati in un contenitore di archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="1fdc9-138">Continuous Export allows you tooexport your data into an Azure Blob Storage container.</span></span> <span data-ttu-id="1fdc9-139">È molto utile se occorre tookeep i dati per più di periodo di memorizzazione hello attualmente offerto da Application Insights.</span><span class="sxs-lookup"><span data-stu-id="1fdc9-139">This is very useful if you need tookeep your data for longer than hello retention period currently offered by Application Insights.</span></span> <span data-ttu-id="1fdc9-140">È possibile mantenere i dati di hello nell'archiviazione blob, convertirlo in un Database SQL o i preferito soluzione di data warehousing.</span><span class="sxs-lookup"><span data-stu-id="1fdc9-140">You can keep hello data in blob storage, process it into a SQL Database, or your preferred data warehousing solution.</span></span>

[<span data-ttu-id="1fdc9-141">Altre informazioni su Esportazione continua</span><span class="sxs-lookup"><span data-stu-id="1fdc9-141">Learn more about Continuous Export</span></span>](app-insights-export-telemetry.md)

## <a name="next-steps"></a><span data-ttu-id="1fdc9-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1fdc9-142">Next steps</span></span>
* [<span data-ttu-id="1fdc9-143">Applicare tooyour Analitica dei dati</span><span class="sxs-lookup"><span data-stu-id="1fdc9-143">Apply Analytics tooyour data</span></span>](app-insights-analytics-tour.md)

