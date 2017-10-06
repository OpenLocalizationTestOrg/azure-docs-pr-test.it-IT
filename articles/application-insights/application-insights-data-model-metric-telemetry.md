---
title: aaaAzure modello dati di telemetria Insights di applicazione - metrica telemetria | Documenti Microsoft
description: Modello di dati di Application Insights per la metrica dei dati di telemetria
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/25/2017
ms.author: bwren
ms.openlocfilehash: 005e218a8451007458185f1e457a20cee93fa630
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="metric-telemetry-application-insights-data-model"></a><span data-ttu-id="b8c44-103">Metrica dei dati di telemetria: modello di dati di Application Insights</span><span class="sxs-lookup"><span data-stu-id="b8c44-103">Metric telemetry: Application Insights data model</span></span>

<span data-ttu-id="b8c44-104">Esistono due tipi di telemetria della metrica supportata da [Application Insights](app-insights-overview.md): la metrica a misura singola e la metrica preaggregata.</span><span class="sxs-lookup"><span data-stu-id="b8c44-104">There are two types of metric telemetry supported by [Application Insights](app-insights-overview.md): single measurement and pre-aggregated metric.</span></span> <span data-ttu-id="b8c44-105">La misura singola è costituita semplicemente da un nome e un valore.</span><span class="sxs-lookup"><span data-stu-id="b8c44-105">Single measurement is just a name and value.</span></span> <span data-ttu-id="b8c44-106">Metrica preaggregato consente di specificare il valore minimo e massimo della metrica hello nell'intervallo di aggregazione hello e deviazione standard di esso.</span><span class="sxs-lookup"><span data-stu-id="b8c44-106">Pre-aggregated metric specifies minimum and maximum value of hello metric in hello aggregation interval and standard deviation of it.</span></span>

<span data-ttu-id="b8c44-107">La metrica dei dati di telemetria preaggregata presuppone che il periodo di aggregazione sia di un minuto.</span><span class="sxs-lookup"><span data-stu-id="b8c44-107">Pre-aggregated metric telemetry assumes that aggregation period was one minute.</span></span>

<span data-ttu-id="b8c44-108">Esistono diversi nomi di metrica noti supportati da Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b8c44-108">There are several well-known metric names supported by Application Insights.</span></span> 

<span data-ttu-id="b8c44-109">Metrica che rappresenta i contatori di sistema e di processo:</span><span class="sxs-lookup"><span data-stu-id="b8c44-109">Metric representing system and process counters:</span></span>

| <span data-ttu-id="b8c44-110">**Nome .NET**</span><span class="sxs-lookup"><span data-stu-id="b8c44-110">**.NET name**</span></span>             | <span data-ttu-id="b8c44-111">**Nome indipendente dalla piattaforma**</span><span class="sxs-lookup"><span data-stu-id="b8c44-111">**Platform agnostic name**</span></span> | <span data-ttu-id="b8c44-112">**Nome API REST**</span><span class="sxs-lookup"><span data-stu-id="b8c44-112">**REST API name**</span></span> | <span data-ttu-id="b8c44-113">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="b8c44-113">**Description**</span></span>
| ------------------------- | -------------------------- | ----------------- | ---------------- 
| `\Processor(_Total)\% Processor Time` | <span data-ttu-id="b8c44-114">Lavoro in corso...</span><span class="sxs-lookup"><span data-stu-id="b8c44-114">Work in progress...</span></span> | [<span data-ttu-id="b8c44-115">processorCpuPercentage</span><span class="sxs-lookup"><span data-stu-id="b8c44-115">processorCpuPercentage</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessorCpuPercentage) | <span data-ttu-id="b8c44-116">CPU computer totale</span><span class="sxs-lookup"><span data-stu-id="b8c44-116">total machine CPU</span></span>
| `\Memory\Available Bytes`                 | <span data-ttu-id="b8c44-117">Lavoro in corso...</span><span class="sxs-lookup"><span data-stu-id="b8c44-117">Work in progress...</span></span> | [<span data-ttu-id="b8c44-118">memoryAvailableBytes</span><span class="sxs-lookup"><span data-stu-id="b8c44-118">memoryAvailableBytes</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FmemoryAvailableBytes) | <span data-ttu-id="b8c44-119">memoria disponibile su disco</span><span class="sxs-lookup"><span data-stu-id="b8c44-119">memory available on disk</span></span>
| `\Process(??APP_WIN32_PROC??)\% Processor Time` | <span data-ttu-id="b8c44-120">Lavoro in corso...</span><span class="sxs-lookup"><span data-stu-id="b8c44-120">Work in progress...</span></span> | [<span data-ttu-id="b8c44-121">processCpuPercentage</span><span class="sxs-lookup"><span data-stu-id="b8c44-121">processCpuPercentage</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessCpuPercentage) | <span data-ttu-id="b8c44-122">CPU del processo di hello ospita un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="b8c44-122">CPU of hello process hosting hello application</span></span>
| `\Process(??APP_WIN32_PROC??)\Private Bytes`      | <span data-ttu-id="b8c44-123">Lavoro in corso...</span><span class="sxs-lookup"><span data-stu-id="b8c44-123">Work in progress...</span></span> | [<span data-ttu-id="b8c44-124">processPrivateBytes</span><span class="sxs-lookup"><span data-stu-id="b8c44-124">processPrivateBytes</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessPrivateBytes) | <span data-ttu-id="b8c44-125">memoria utilizzata dal processo di hello che ospita un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="b8c44-125">memory used by hello process hosting hello application</span></span>
| `\Process(??APP_WIN32_PROC??)\IO Data Bytes/sec` | <span data-ttu-id="b8c44-126">Lavoro in corso...</span><span class="sxs-lookup"><span data-stu-id="b8c44-126">Work in progress...</span></span> | [<span data-ttu-id="b8c44-127">processIOBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="b8c44-127">processIOBytesPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessIOBytesPerSecond) | <span data-ttu-id="b8c44-128">frequenza delle operazioni dei / o di esecuzione di processo che ospita un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="b8c44-128">rate of I/O operations runs by process hosting hello application</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests/Sec`             | <span data-ttu-id="b8c44-129">Lavoro in corso...</span><span class="sxs-lookup"><span data-stu-id="b8c44-129">Work in progress...</span></span> | [<span data-ttu-id="b8c44-130">requestsPerSecond</span><span class="sxs-lookup"><span data-stu-id="b8c44-130">requestsPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsPerSecond) | <span data-ttu-id="b8c44-131">frequenza delle richieste elaborate dall'applicazione</span><span class="sxs-lookup"><span data-stu-id="b8c44-131">rate of requests processed by application</span></span> 
| `\.NET CLR Exceptions(??APP_CLR_PROC??)\# of Exceps Thrown / sec`    | <span data-ttu-id="b8c44-132">Lavoro in corso...</span><span class="sxs-lookup"><span data-stu-id="b8c44-132">Work in progress...</span></span> | [<span data-ttu-id="b8c44-133">exceptionsPerSecond</span><span class="sxs-lookup"><span data-stu-id="b8c44-133">exceptionsPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FexceptionsPerSecond) | <span data-ttu-id="b8c44-134">frequenza delle eccezioni generate dall'applicazione</span><span class="sxs-lookup"><span data-stu-id="b8c44-134">rate of exceptions thrown by application</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Request Execution Time`   | <span data-ttu-id="b8c44-135">Lavoro in corso...</span><span class="sxs-lookup"><span data-stu-id="b8c44-135">Work in progress...</span></span> | [<span data-ttu-id="b8c44-136">requestExecutionTime</span><span class="sxs-lookup"><span data-stu-id="b8c44-136">requestExecutionTime</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestExecutionTime) | <span data-ttu-id="b8c44-137">tempo di esecuzione medio delle richieste</span><span class="sxs-lookup"><span data-stu-id="b8c44-137">average requests execution time</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests In Application Queue` | <span data-ttu-id="b8c44-138">Lavoro in corso...</span><span class="sxs-lookup"><span data-stu-id="b8c44-138">Work in progress...</span></span> | [<span data-ttu-id="b8c44-139">requestsInQueue</span><span class="sxs-lookup"><span data-stu-id="b8c44-139">requestsInQueue</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsInQueue) | <span data-ttu-id="b8c44-140">numero di richieste in attesa di hello in una coda di elaborazione</span><span class="sxs-lookup"><span data-stu-id="b8c44-140">number of requests waiting for hello processing in a queue</span></span>

## <a name="name"></a><span data-ttu-id="b8c44-141">Nome</span><span class="sxs-lookup"><span data-stu-id="b8c44-141">Name</span></span>

<span data-ttu-id="b8c44-142">Nome della metrica hello desideri toosee nel portale Application Insights e l'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="b8c44-142">Name of hello metric you'd like toosee in Application Insights portal and UI.</span></span> 

## <a name="value"></a><span data-ttu-id="b8c44-143">Valore</span><span class="sxs-lookup"><span data-stu-id="b8c44-143">Value</span></span>

<span data-ttu-id="b8c44-144">Singolo valore per la misura.</span><span class="sxs-lookup"><span data-stu-id="b8c44-144">Single value for measurement.</span></span> <span data-ttu-id="b8c44-145">Somma delle singole misure per l'aggregazione di hello.</span><span class="sxs-lookup"><span data-stu-id="b8c44-145">Sum of individual measurements for hello aggregation.</span></span>

## <a name="count"></a><span data-ttu-id="b8c44-146">Numero</span><span class="sxs-lookup"><span data-stu-id="b8c44-146">Count</span></span>

<span data-ttu-id="b8c44-147">Peso della metrica di metrica hello aggregato.</span><span class="sxs-lookup"><span data-stu-id="b8c44-147">Metric weight of hello aggregated metric.</span></span> <span data-ttu-id="b8c44-148">Non deve essere impostato per una misura.</span><span class="sxs-lookup"><span data-stu-id="b8c44-148">Should not be set for a measurement.</span></span>

## <a name="min"></a><span data-ttu-id="b8c44-149">Min</span><span class="sxs-lookup"><span data-stu-id="b8c44-149">Min</span></span>

<span data-ttu-id="b8c44-150">Valore minimo della metrica hello aggregato.</span><span class="sxs-lookup"><span data-stu-id="b8c44-150">Minimum value of hello aggregated metric.</span></span> <span data-ttu-id="b8c44-151">Non deve essere impostato per una misura.</span><span class="sxs-lookup"><span data-stu-id="b8c44-151">Should not be set for a measurement.</span></span>

## <a name="max"></a><span data-ttu-id="b8c44-152">max</span><span class="sxs-lookup"><span data-stu-id="b8c44-152">Max</span></span>

<span data-ttu-id="b8c44-153">Valore massimo della metrica hello aggregato.</span><span class="sxs-lookup"><span data-stu-id="b8c44-153">Maximum value of hello aggregated metric.</span></span> <span data-ttu-id="b8c44-154">Non deve essere impostato per una misura.</span><span class="sxs-lookup"><span data-stu-id="b8c44-154">Should not be set for a measurement.</span></span>

## <a name="standard-deviation"></a><span data-ttu-id="b8c44-155">Deviazione standard</span><span class="sxs-lookup"><span data-stu-id="b8c44-155">Standard deviation</span></span>

<span data-ttu-id="b8c44-156">Deviazione standard della metrica hello aggregato.</span><span class="sxs-lookup"><span data-stu-id="b8c44-156">Standard deviation of hello aggregated metric.</span></span> <span data-ttu-id="b8c44-157">Non deve essere impostato per una misura.</span><span class="sxs-lookup"><span data-stu-id="b8c44-157">Should not be set for a measurement.</span></span>

## <a name="custom-properties"></a><span data-ttu-id="b8c44-158">Proprietà personalizzate</span><span class="sxs-lookup"><span data-stu-id="b8c44-158">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="next-steps"></a><span data-ttu-id="b8c44-159">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b8c44-159">Next steps</span></span>

- <span data-ttu-id="b8c44-160">Informazioni su come toouse [Application Insights API per gli eventi personalizzati e le metriche](app-insights-api-custom-events-metrics.md#trackmetric).</span><span class="sxs-lookup"><span data-stu-id="b8c44-160">Learn how toouse [Application Insights API for custom events and metrics](app-insights-api-custom-events-metrics.md#trackmetric).</span></span>
- <span data-ttu-id="b8c44-161">Per informazioni sul modello di dati e sui tipi di Application Insights, vedere il [modello di dati](application-insights-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="b8c44-161">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="b8c44-162">Verificare quali [piattaforme](app-insights-platforms.md) supportano Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b8c44-162">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
