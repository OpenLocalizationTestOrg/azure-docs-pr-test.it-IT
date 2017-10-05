---
title: Modello di dati di Azure Application Insights Telemetry - Telemetria delle eccezioni | Microsoft Docs
description: Modello di dati di Application Insights per la telemetria delle eccezioni
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
ms.openlocfilehash: 6b220b0cb6719bac606f599d657d08ab847c7590
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="exception-telemetry-application-insights-data-model"></a><span data-ttu-id="4baba-103">Telemetria delle eccezioni: modello di dati di Application Insights</span><span class="sxs-lookup"><span data-stu-id="4baba-103">Exception telemetry: Application Insights data model</span></span>

<span data-ttu-id="4baba-104">In [Application Insights](app-insights-overview.md), un'istanza di eccezione rappresenta un'eccezione gestita o non gestita che si è verificata durante l'esecuzione dell'applicazione monitorata.</span><span class="sxs-lookup"><span data-stu-id="4baba-104">In [Application Insights](app-insights-overview.md), an instance of Exception represents a handled or unhandled exception that occurred during execution of the monitored application.</span></span>

## <a name="problem-id"></a><span data-ttu-id="4baba-105">ID problema</span><span class="sxs-lookup"><span data-stu-id="4baba-105">Problem Id</span></span>

<span data-ttu-id="4baba-106">Identificatore del punto nel codice in cui è stata generata l'eccezione.</span><span class="sxs-lookup"><span data-stu-id="4baba-106">Identifier of where the exception was thrown in code.</span></span> <span data-ttu-id="4baba-107">Usato per il raggruppamento delle eccezioni.</span><span class="sxs-lookup"><span data-stu-id="4baba-107">Used for exceptions grouping.</span></span> <span data-ttu-id="4baba-108">In genere una combinazione di tipo di eccezione e una funzione dallo stack di chiamate.</span><span class="sxs-lookup"><span data-stu-id="4baba-108">Typically a combination of exception type and a function from the call stack.</span></span>

<span data-ttu-id="4baba-109">Lunghezza massima: 1024 caratteri</span><span class="sxs-lookup"><span data-stu-id="4baba-109">Max length: 1024 characters</span></span>

## <a name="severity-level"></a><span data-ttu-id="4baba-110">Livello di gravità</span><span class="sxs-lookup"><span data-stu-id="4baba-110">Severity level</span></span>

<span data-ttu-id="4baba-111">Livello di gravità della traccia.</span><span class="sxs-lookup"><span data-stu-id="4baba-111">Trace severity level.</span></span> <span data-ttu-id="4baba-112">Il valore può essere `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span><span class="sxs-lookup"><span data-stu-id="4baba-112">Value can be `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span></span>

## <a name="exception-details"></a><span data-ttu-id="4baba-113">Dettagli eccezione</span><span class="sxs-lookup"><span data-stu-id="4baba-113">Exception details</span></span>

<span data-ttu-id="4baba-114">(Da aggiungere)</span><span class="sxs-lookup"><span data-stu-id="4baba-114">(To be extended)</span></span>

## <a name="custom-properties"></a><span data-ttu-id="4baba-115">Proprietà personalizzate</span><span class="sxs-lookup"><span data-stu-id="4baba-115">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="4baba-116">Misure personalizzate</span><span class="sxs-lookup"><span data-stu-id="4baba-116">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a><span data-ttu-id="4baba-117">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4baba-117">Next steps</span></span>

- <span data-ttu-id="4baba-118">Per informazioni sul modello di dati e sui tipi di Application Insights, vedere il [modello di dati](application-insights-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="4baba-118">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="4baba-119">Informazioni su come [diagnosticare le eccezioni nelle app Web con Application Insights](app-insights-asp-net-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="4baba-119">Learn how to [diagnose exceptions in your web apps with Application Insights](app-insights-asp-net-exceptions.md).</span></span>
- <span data-ttu-id="4baba-120">Verificare quali [piattaforme](app-insights-platforms.md) supportano Application Insights.</span><span class="sxs-lookup"><span data-stu-id="4baba-120">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
