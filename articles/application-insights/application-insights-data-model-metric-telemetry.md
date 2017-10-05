---
title: Modello di dati di Azure Application Insights Telemetry - Metrica dei dati di telemetria | Microsoft Docs
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
ms.openlocfilehash: 42e55db4f932de85ee1a71c408b889e0ff9fe3e1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="metric-telemetry-application-insights-data-model"></a><span data-ttu-id="8c096-103">Metrica dei dati di telemetria: modello di dati di Application Insights</span><span class="sxs-lookup"><span data-stu-id="8c096-103">Metric telemetry: Application Insights data model</span></span>

<span data-ttu-id="8c096-104">Esistono due tipi di telemetria della metrica supportata da [Application Insights](app-insights-overview.md): la metrica a misura singola e la metrica preaggregata.</span><span class="sxs-lookup"><span data-stu-id="8c096-104">There are two types of metric telemetry supported by [Application Insights](app-insights-overview.md): single measurement and pre-aggregated metric.</span></span> <span data-ttu-id="8c096-105">La misura singola è costituita semplicemente da un nome e un valore.</span><span class="sxs-lookup"><span data-stu-id="8c096-105">Single measurement is just a name and value.</span></span> <span data-ttu-id="8c096-106">La metrica preaggregata specifica i valori minimo e massimo della metrica nell'intervallo di aggregazione e la relativa deviazione standard.</span><span class="sxs-lookup"><span data-stu-id="8c096-106">Pre-aggregated metric specifies minimum and maximum value of the metric in the aggregation interval and standard deviation of it.</span></span>

<span data-ttu-id="8c096-107">La metrica dei dati di telemetria preaggregata presuppone che il periodo di aggregazione sia di un minuto.</span><span class="sxs-lookup"><span data-stu-id="8c096-107">Pre-aggregated metric telemetry assumes that aggregation period was one minute.</span></span>

<span data-ttu-id="8c096-108">Esistono diversi nomi di metrica noti supportati da Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8c096-108">There are several well-known metric names supported by Application Insights.</span></span> 

<span data-ttu-id="8c096-109">Metrica che rappresenta i contatori di sistema e di processo:</span><span class="sxs-lookup"><span data-stu-id="8c096-109">Metric representing system and process counters:</span></span>

| <span data-ttu-id="8c096-110">**Nome .NET**</span><span class="sxs-lookup"><span data-stu-id="8c096-110">**.NET name**</span></span>             | <span data-ttu-id="8c096-111">**Nome indipendente dalla piattaforma**</span><span class="sxs-lookup"><span data-stu-id="8c096-111">**Platform agnostic name**</span></span> | <span data-ttu-id="8c096-112">**Nome API REST**</span><span class="sxs-lookup"><span data-stu-id="8c096-112">**REST API name**</span></span> | <span data-ttu-id="8c096-113">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="8c096-113">**Description**</span></span>
| ------------------------- | -------------------------- | ----------------- | ---------------- 
| `\Processor(_Total)\% Processor Time` | <span data-ttu-id="8c096-114">Lavoro in corso...</span><span class="sxs-lookup"><span data-stu-id="8c096-114">Work in progress...</span></span> | [<span data-ttu-id="8c096-115">processorCpuPercentage</span><span class="sxs-lookup"><span data-stu-id="8c096-115">processorCpuPercentage</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessorCpuPercentage) | <span data-ttu-id="8c096-116">CPU computer totale</span><span class="sxs-lookup"><span data-stu-id="8c096-116">total machine CPU</span></span>
| `\Memory\Available Bytes`                 | <span data-ttu-id="8c096-117">Lavoro in corso...</span><span class="sxs-lookup"><span data-stu-id="8c096-117">Work in progress...</span></span> | [<span data-ttu-id="8c096-118">memoryAvailableBytes</span><span class="sxs-lookup"><span data-stu-id="8c096-118">memoryAvailableBytes</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FmemoryAvailableBytes) | <span data-ttu-id="8c096-119">memoria disponibile su disco</span><span class="sxs-lookup"><span data-stu-id="8c096-119">memory available on disk</span></span>
| `\Process(??APP_WIN32_PROC??)\% Processor Time` | <span data-ttu-id="8c096-120">Lavoro in corso...</span><span class="sxs-lookup"><span data-stu-id="8c096-120">Work in progress...</span></span> | [<span data-ttu-id="8c096-121">processCpuPercentage</span><span class="sxs-lookup"><span data-stu-id="8c096-121">processCpuPercentage</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessCpuPercentage) | <span data-ttu-id="8c096-122">CPU del processo che ospita l'applicazione</span><span class="sxs-lookup"><span data-stu-id="8c096-122">CPU of the process hosting the application</span></span>
| `\Process(??APP_WIN32_PROC??)\Private Bytes`      | <span data-ttu-id="8c096-123">Lavoro in corso...</span><span class="sxs-lookup"><span data-stu-id="8c096-123">Work in progress...</span></span> | [<span data-ttu-id="8c096-124">processPrivateBytes</span><span class="sxs-lookup"><span data-stu-id="8c096-124">processPrivateBytes</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessPrivateBytes) | <span data-ttu-id="8c096-125">memoria usata dal processo che ospita l'applicazione</span><span class="sxs-lookup"><span data-stu-id="8c096-125">memory used by the process hosting the application</span></span>
| `\Process(??APP_WIN32_PROC??)\IO Data Bytes/sec` | <span data-ttu-id="8c096-126">Lavoro in corso...</span><span class="sxs-lookup"><span data-stu-id="8c096-126">Work in progress...</span></span> | [<span data-ttu-id="8c096-127">processIOBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="8c096-127">processIOBytesPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessIOBytesPerSecond) | <span data-ttu-id="8c096-128">frequenza delle operazioni I/O eseguite dal processo che ospita l'applicazione</span><span class="sxs-lookup"><span data-stu-id="8c096-128">rate of I/O operations runs by process hosting the application</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests/Sec`             | <span data-ttu-id="8c096-129">Lavoro in corso...</span><span class="sxs-lookup"><span data-stu-id="8c096-129">Work in progress...</span></span> | [<span data-ttu-id="8c096-130">requestsPerSecond</span><span class="sxs-lookup"><span data-stu-id="8c096-130">requestsPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsPerSecond) | <span data-ttu-id="8c096-131">frequenza delle richieste elaborate dall'applicazione</span><span class="sxs-lookup"><span data-stu-id="8c096-131">rate of requests processed by application</span></span> 
| `\.NET CLR Exceptions(??APP_CLR_PROC??)\# of Exceps Thrown / sec`    | <span data-ttu-id="8c096-132">Lavoro in corso...</span><span class="sxs-lookup"><span data-stu-id="8c096-132">Work in progress...</span></span> | [<span data-ttu-id="8c096-133">exceptionsPerSecond</span><span class="sxs-lookup"><span data-stu-id="8c096-133">exceptionsPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FexceptionsPerSecond) | <span data-ttu-id="8c096-134">frequenza delle eccezioni generate dall'applicazione</span><span class="sxs-lookup"><span data-stu-id="8c096-134">rate of exceptions thrown by application</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Request Execution Time`   | <span data-ttu-id="8c096-135">Lavoro in corso...</span><span class="sxs-lookup"><span data-stu-id="8c096-135">Work in progress...</span></span> | [<span data-ttu-id="8c096-136">requestExecutionTime</span><span class="sxs-lookup"><span data-stu-id="8c096-136">requestExecutionTime</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestExecutionTime) | <span data-ttu-id="8c096-137">tempo di esecuzione medio delle richieste</span><span class="sxs-lookup"><span data-stu-id="8c096-137">average requests execution time</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests In Application Queue` | <span data-ttu-id="8c096-138">Lavoro in corso...</span><span class="sxs-lookup"><span data-stu-id="8c096-138">Work in progress...</span></span> | [<span data-ttu-id="8c096-139">requestsInQueue</span><span class="sxs-lookup"><span data-stu-id="8c096-139">requestsInQueue</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsInQueue) | <span data-ttu-id="8c096-140">numero di richieste in attesa dell'elaborazione in una coda</span><span class="sxs-lookup"><span data-stu-id="8c096-140">number of requests waiting for the processing in a queue</span></span>

## <a name="name"></a><span data-ttu-id="8c096-141">Nome</span><span class="sxs-lookup"><span data-stu-id="8c096-141">Name</span></span>

<span data-ttu-id="8c096-142">Nome della metrica che si vuole visualizzare nel portale di Application Insights e nell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="8c096-142">Name of the metric you'd like to see in Application Insights portal and UI.</span></span> 

## <a name="value"></a><span data-ttu-id="8c096-143">Valore</span><span class="sxs-lookup"><span data-stu-id="8c096-143">Value</span></span>

<span data-ttu-id="8c096-144">Singolo valore per la misura.</span><span class="sxs-lookup"><span data-stu-id="8c096-144">Single value for measurement.</span></span> <span data-ttu-id="8c096-145">Somma delle singole misure per l'aggregazione.</span><span class="sxs-lookup"><span data-stu-id="8c096-145">Sum of individual measurements for the aggregation.</span></span>

## <a name="count"></a><span data-ttu-id="8c096-146">Numero</span><span class="sxs-lookup"><span data-stu-id="8c096-146">Count</span></span>

<span data-ttu-id="8c096-147">Peso della metrica aggregata.</span><span class="sxs-lookup"><span data-stu-id="8c096-147">Metric weight of the aggregated metric.</span></span> <span data-ttu-id="8c096-148">Non deve essere impostato per una misura.</span><span class="sxs-lookup"><span data-stu-id="8c096-148">Should not be set for a measurement.</span></span>

## <a name="min"></a><span data-ttu-id="8c096-149">Min</span><span class="sxs-lookup"><span data-stu-id="8c096-149">Min</span></span>

<span data-ttu-id="8c096-150">Valore minimo della metrica aggregata.</span><span class="sxs-lookup"><span data-stu-id="8c096-150">Minimum value of the aggregated metric.</span></span> <span data-ttu-id="8c096-151">Non deve essere impostato per una misura.</span><span class="sxs-lookup"><span data-stu-id="8c096-151">Should not be set for a measurement.</span></span>

## <a name="max"></a><span data-ttu-id="8c096-152">Max</span><span class="sxs-lookup"><span data-stu-id="8c096-152">Max</span></span>

<span data-ttu-id="8c096-153">Valore massimo della metrica aggregata.</span><span class="sxs-lookup"><span data-stu-id="8c096-153">Maximum value of the aggregated metric.</span></span> <span data-ttu-id="8c096-154">Non deve essere impostato per una misura.</span><span class="sxs-lookup"><span data-stu-id="8c096-154">Should not be set for a measurement.</span></span>

## <a name="standard-deviation"></a><span data-ttu-id="8c096-155">Deviazione standard</span><span class="sxs-lookup"><span data-stu-id="8c096-155">Standard deviation</span></span>

<span data-ttu-id="8c096-156">Deviazione standard della metrica aggregata.</span><span class="sxs-lookup"><span data-stu-id="8c096-156">Standard deviation of the aggregated metric.</span></span> <span data-ttu-id="8c096-157">Non deve essere impostato per una misura.</span><span class="sxs-lookup"><span data-stu-id="8c096-157">Should not be set for a measurement.</span></span>

## <a name="custom-properties"></a><span data-ttu-id="8c096-158">Proprietà personalizzate</span><span class="sxs-lookup"><span data-stu-id="8c096-158">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="next-steps"></a><span data-ttu-id="8c096-159">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8c096-159">Next steps</span></span>

- <span data-ttu-id="8c096-160">Informazioni su come usare l'[API di Application Insights per metriche ed eventi personalizzati](app-insights-api-custom-events-metrics.md#trackmetric).</span><span class="sxs-lookup"><span data-stu-id="8c096-160">Learn how to use [Application Insights API for custom events and metrics](app-insights-api-custom-events-metrics.md#trackmetric).</span></span>
- <span data-ttu-id="8c096-161">Per informazioni sul modello di dati e sui tipi di Application Insights, vedere il [modello di dati](application-insights-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="8c096-161">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="8c096-162">Verificare quali [piattaforme](app-insights-platforms.md) supportano Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8c096-162">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
