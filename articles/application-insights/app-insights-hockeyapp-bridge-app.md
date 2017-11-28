---
title: Esplorazione dei dati HockeyApp in Application Insights | Microsoft Docs
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
ms.openlocfilehash: 450ca10613d137393090578619f3766734d1d493
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="exploring-hockeyapp-data-in-application-insights"></a><span data-ttu-id="bfdb5-103">Esplorazione dei dati HockeyApp in Application Insights</span><span class="sxs-lookup"><span data-stu-id="bfdb5-103">Exploring HockeyApp data in Application Insights</span></span>
<span data-ttu-id="bfdb5-104">[HockeyApp](https://azure.microsoft.com/services/hockeyapp/) è la piattaforma consigliata per il monitoraggio di live app per desktop e per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="bfdb5-104">[HockeyApp](https://azure.microsoft.com/services/hockeyapp/) is the recommended platform for monitoring live desktop and mobile apps.</span></span> <span data-ttu-id="bfdb5-105">Da HockeyApp è possibile inviare dati di telemetria di traccia e personalizzata per monitorare l'utilizzo e facilitare la diagnosi, oltre a ottenere dati di arresto anomalo.</span><span class="sxs-lookup"><span data-stu-id="bfdb5-105">From HockeyApp, you can send custom and trace telemetry to monitor usage and assist in diagnosis (in addition to getting crash data).</span></span> <span data-ttu-id="bfdb5-106">È possibile effettuare una query di questo flusso di dati di telemetria con la funzionalità [Analytics](app-insights-analytics.md) di [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bfdb5-106">This stream of telemetry can be queried using the powerful [Analytics](app-insights-analytics.md) feature of [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="bfdb5-107">È anche possibile [esportare i dati di telemetria di traccia e personalizzata](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="bfdb5-107">In addition, you can [export the custom and trace telemetry](app-insights-export-telemetry.md).</span></span> <span data-ttu-id="bfdb5-108">Per abilitare queste funzionalità, configurare un bridge che inoltra i dati HockeyApp personalizzati ad Application Insights.</span><span class="sxs-lookup"><span data-stu-id="bfdb5-108">To enable these features, you set up a bridge that relays HockeyApp custom data to Application Insights.</span></span>

## <a name="the-hockeyapp-bridge-app"></a><span data-ttu-id="bfdb5-109">App bridge HockeyApp</span><span class="sxs-lookup"><span data-stu-id="bfdb5-109">The HockeyApp Bridge app</span></span>
<span data-ttu-id="bfdb5-110">L'app bridge HockeyApp è la funzionalità di base che consente di accedere ai dati di telemetria di traccia e personalizzata HockeyApp in Application Insights tramite le funzionalità Analisi ed Esportazione continua.</span><span class="sxs-lookup"><span data-stu-id="bfdb5-110">The HockeyApp Bridge App is the core feature that enables you to access your HockeyApp custom and trace telemetry in Application Insights through the Analytics and Continuous Export features.</span></span> <span data-ttu-id="bfdb5-111">Gli eventi di traccia e personalizzati raccolti da HockeyApp dopo la creazione dell'app bridge HockeyApp saranno accessibili da queste funzionalità.</span><span class="sxs-lookup"><span data-stu-id="bfdb5-111">Custom and trace events collected by HockeyApp after the creation of the HockeyApp Bridge App will be accessible from these features.</span></span> <span data-ttu-id="bfdb5-112">Ora verrà descritto come configurare una di queste app bridge.</span><span class="sxs-lookup"><span data-stu-id="bfdb5-112">Let’s see how to set up one of these Bridge Apps.</span></span>

<span data-ttu-id="bfdb5-113">In HockeyApp aprire Account Settings (Impostazioni account), [API Tokens](https://rink.hockeyapp.net/manage/auth_tokens)(Token API).</span><span class="sxs-lookup"><span data-stu-id="bfdb5-113">In HockeyApp, open Account Settings, [API Tokens](https://rink.hockeyapp.net/manage/auth_tokens).</span></span> <span data-ttu-id="bfdb5-114">Creare un token oppure usarne uno esistente.</span><span class="sxs-lookup"><span data-stu-id="bfdb5-114">Either create a new token or reuse an existing one.</span></span> <span data-ttu-id="bfdb5-115">I diritti minimi necessari sono "Read Only" (Sola lettura).</span><span class="sxs-lookup"><span data-stu-id="bfdb5-115">The minimum rights required are "read only".</span></span> <span data-ttu-id="bfdb5-116">Eseguire una copia del token API.</span><span class="sxs-lookup"><span data-stu-id="bfdb5-116">Take a copy of the API token.</span></span>

![Ottenere un token API HockeyApp](./media/app-insights-hockeyapp-bridge-app/01.png)

<span data-ttu-id="bfdb5-118">Accedere al portale di Microsoft Azure e [creare una risorsa di Application Insights](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="bfdb5-118">Open the Microsoft Azure portal and [create an Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="bfdb5-119">Impostare il tipo di applicazione su "Applicazione bridge HockeyApp":</span><span class="sxs-lookup"><span data-stu-id="bfdb5-119">Set Application Type to “HockeyApp bridge application”:</span></span>

![Nuova risorsa di Application Insights](./media/app-insights-hockeyapp-bridge-app/02.png)

<span data-ttu-id="bfdb5-121">Non è necessario impostare un nome, verrà impostato automaticamente dal nome HockeyApp.</span><span class="sxs-lookup"><span data-stu-id="bfdb5-121">You don't need to set a name - this will automatically be set from the HockeyApp name.</span></span>

<span data-ttu-id="bfdb5-122">Verranno visualizzati i campi dell'applicazione bridge HockeyApp.</span><span class="sxs-lookup"><span data-stu-id="bfdb5-122">The HockeyApp bridge fields appear.</span></span> 

![Immettere i campi dell'app bridge](./media/app-insights-hockeyapp-bridge-app/03.png)

<span data-ttu-id="bfdb5-124">Immettere il token HockeyApp annotato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="bfdb5-124">Enter the HockeyApp token you noted earlier.</span></span> <span data-ttu-id="bfdb5-125">Questa azione consente di popolare il menu a discesa "Applicazione HockeyApp" con tutte le applicazioni HockeyApp.</span><span class="sxs-lookup"><span data-stu-id="bfdb5-125">This action populates the “HockeyApp Application” dropdown menu with all your HockeyApp applications.</span></span> <span data-ttu-id="bfdb5-126">Selezionare l'applicazione da usare e compilare gli altri campi.</span><span class="sxs-lookup"><span data-stu-id="bfdb5-126">Select the one you want to use, and complete the remainder of the fields.</span></span> 

<span data-ttu-id="bfdb5-127">Aprire la nuova risorsa.</span><span class="sxs-lookup"><span data-stu-id="bfdb5-127">Open the new resource.</span></span> 

<span data-ttu-id="bfdb5-128">Si noti che l'avvio del flusso di dati richiede del tempo.</span><span class="sxs-lookup"><span data-stu-id="bfdb5-128">Note that the data takes a while to start flowing.</span></span>

![Risorsa di Application Insights in attesa dei dati](./media/app-insights-hockeyapp-bridge-app/04.png)

<span data-ttu-id="bfdb5-130">La procedura è terminata.</span><span class="sxs-lookup"><span data-stu-id="bfdb5-130">That’s it!</span></span> <span data-ttu-id="bfdb5-131">Da questo momento, i dati di traccia e personalizzati raccolti nell'app instrumentata HockeyApp saranno disponibili anche nelle funzionalità Analisi ed Esportazione continua di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="bfdb5-131">Custom and trace data collected in your HockeyApp-instrumented app from this point forward is now also available to you in the Analytics and Continuous Export features of Application Insights.</span></span>

<span data-ttu-id="bfdb5-132">Verranno brevemente esaminate queste funzionalità ora disponibili.</span><span class="sxs-lookup"><span data-stu-id="bfdb5-132">Let’s briefly review each of these features now available to you.</span></span>

## <a name="analytics"></a><span data-ttu-id="bfdb5-133">Analytics</span><span class="sxs-lookup"><span data-stu-id="bfdb5-133">Analytics</span></span>
<span data-ttu-id="bfdb5-134">Analisi è uno strumento avanzato per query ad hoc che consente di diagnosticare e analizzare i dati di telemetria e di individuare rapidamente cause radice e modelli.</span><span class="sxs-lookup"><span data-stu-id="bfdb5-134">Analytics is a powerful tool for ad-hoc querying of your data, allowing you to diagnose and analyze your telemetry and quickly discover root causes and patterns.</span></span>

![Analytics](./media/app-insights-hockeyapp-bridge-app/05.png)

* [<span data-ttu-id="bfdb5-136">Altre informazioni su Analisi</span><span class="sxs-lookup"><span data-stu-id="bfdb5-136">Learn more about Analytics</span></span>](app-insights-analytics-tour.md)

## <a name="continuous-export"></a><span data-ttu-id="bfdb5-137">Esportazione continua</span><span class="sxs-lookup"><span data-stu-id="bfdb5-137">Continuous export</span></span>
<span data-ttu-id="bfdb5-138">Esportazione continua consente di esportare i dati in un contenitore dell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="bfdb5-138">Continuous Export allows you to export your data into an Azure Blob Storage container.</span></span> <span data-ttu-id="bfdb5-139">Ciò è molto utile se è necessario mantenere i dati per un tempo maggiore rispetto al periodo di conservazione attualmente offerto da Application Insights.</span><span class="sxs-lookup"><span data-stu-id="bfdb5-139">This is very useful if you need to keep your data for longer than the retention period currently offered by Application Insights.</span></span> <span data-ttu-id="bfdb5-140">È possibile conservare i dati nell'archivio BLOB ed elaborarli in un database SQL o nella soluzione di data warehousing scelta.</span><span class="sxs-lookup"><span data-stu-id="bfdb5-140">You can keep the data in blob storage, process it into a SQL Database, or your preferred data warehousing solution.</span></span>

[<span data-ttu-id="bfdb5-141">Altre informazioni su Esportazione continua</span><span class="sxs-lookup"><span data-stu-id="bfdb5-141">Learn more about Continuous Export</span></span>](app-insights-export-telemetry.md)

## <a name="next-steps"></a><span data-ttu-id="bfdb5-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bfdb5-142">Next steps</span></span>
* [<span data-ttu-id="bfdb5-143">Applicare Analisi ai dati</span><span class="sxs-lookup"><span data-stu-id="bfdb5-143">Apply Analytics to your data</span></span>](app-insights-analytics-tour.md)

