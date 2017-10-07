---
title: aaaAzure modello dati di telemetria Insights di applicazione - telemetria delle eccezioni | Documenti Microsoft
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
ms.openlocfilehash: 4c2b7d1ac3816d5623db9a35819a48a68a13a9cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="exception-telemetry-application-insights-data-model"></a><span data-ttu-id="f643b-103">Telemetria delle eccezioni: modello di dati di Application Insights</span><span class="sxs-lookup"><span data-stu-id="f643b-103">Exception telemetry: Application Insights data model</span></span>

<span data-ttu-id="f643b-104">In [Application Insights](app-insights-overview.md), un'istanza di eccezione rappresenta un'eccezione gestita o non gestita che si è verificato durante l'esecuzione di un'applicazione hello monitorato.</span><span class="sxs-lookup"><span data-stu-id="f643b-104">In [Application Insights](app-insights-overview.md), an instance of Exception represents a handled or unhandled exception that occurred during execution of hello monitored application.</span></span>

## <a name="problem-id"></a><span data-ttu-id="f643b-105">ID problema</span><span class="sxs-lookup"><span data-stu-id="f643b-105">Problem Id</span></span>

<span data-ttu-id="f643b-106">Identificatore di in cui hello eccezione nel codice.</span><span class="sxs-lookup"><span data-stu-id="f643b-106">Identifier of where hello exception was thrown in code.</span></span> <span data-ttu-id="f643b-107">Usato per il raggruppamento delle eccezioni.</span><span class="sxs-lookup"><span data-stu-id="f643b-107">Used for exceptions grouping.</span></span> <span data-ttu-id="f643b-108">In genere una combinazione di tipo di eccezione e una funzione dallo stack di chiamate hello.</span><span class="sxs-lookup"><span data-stu-id="f643b-108">Typically a combination of exception type and a function from hello call stack.</span></span>

<span data-ttu-id="f643b-109">Lunghezza massima: 1024 caratteri</span><span class="sxs-lookup"><span data-stu-id="f643b-109">Max length: 1024 characters</span></span>

## <a name="severity-level"></a><span data-ttu-id="f643b-110">Livello di gravità</span><span class="sxs-lookup"><span data-stu-id="f643b-110">Severity level</span></span>

<span data-ttu-id="f643b-111">Livello di gravità della traccia.</span><span class="sxs-lookup"><span data-stu-id="f643b-111">Trace severity level.</span></span> <span data-ttu-id="f643b-112">Il valore può essere `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span><span class="sxs-lookup"><span data-stu-id="f643b-112">Value can be `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span></span>

## <a name="exception-details"></a><span data-ttu-id="f643b-113">Dettagli eccezione</span><span class="sxs-lookup"><span data-stu-id="f643b-113">Exception details</span></span>

<span data-ttu-id="f643b-114">(toobe esteso)</span><span class="sxs-lookup"><span data-stu-id="f643b-114">(toobe extended)</span></span>

## <a name="custom-properties"></a><span data-ttu-id="f643b-115">Proprietà personalizzate</span><span class="sxs-lookup"><span data-stu-id="f643b-115">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="f643b-116">Misure personalizzate</span><span class="sxs-lookup"><span data-stu-id="f643b-116">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a><span data-ttu-id="f643b-117">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f643b-117">Next steps</span></span>

- <span data-ttu-id="f643b-118">Per informazioni sul modello di dati e sui tipi di Application Insights, vedere il [modello di dati](application-insights-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="f643b-118">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="f643b-119">Informazioni su come troppo[diagnosi delle eccezioni nelle App web con Application Insights](app-insights-asp-net-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="f643b-119">Learn how too[diagnose exceptions in your web apps with Application Insights](app-insights-asp-net-exceptions.md).</span></span>
- <span data-ttu-id="f643b-120">Verificare quali [piattaforme](app-insights-platforms.md) supportano Application Insights.</span><span class="sxs-lookup"><span data-stu-id="f643b-120">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
