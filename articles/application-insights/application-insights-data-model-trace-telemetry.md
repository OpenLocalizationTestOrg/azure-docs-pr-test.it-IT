---
title: Modello di dati di Azure Application Insights Telemetry - Telemetria delle tracce | Microsoft Docs
description: Modello di dati di Application Insights per la telemetria delle tracce
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
ms.openlocfilehash: e1da0d6a6fbd9ca5486936c326ade667d7b01006
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="trace-telemetry-application-insights-data-model"></a><span data-ttu-id="30235-103">Telemetria delle tracce: modello di dati di Application Insights</span><span class="sxs-lookup"><span data-stu-id="30235-103">Trace telemetry: Application Insights data model</span></span>

<span data-ttu-id="30235-104">In [Application Insights](app-insights-overview.md), la telemetria di traccia rappresenta le istruzioni di traccia in stile `printf` che vengono cercate come testo.</span><span class="sxs-lookup"><span data-stu-id="30235-104">Trace telemetry (in [Application Insights](app-insights-overview.md)) represents `printf` style trace statements that are text-searched.</span></span> <span data-ttu-id="30235-105">`Log4Net`, `NLog` e altre voci del file di log basato su testo vengono convertite in istanze di questo tipo.</span><span class="sxs-lookup"><span data-stu-id="30235-105">`Log4Net`, `NLog`, and other text-based log file entries are translated into instances of this type.</span></span> <span data-ttu-id="30235-106">La traccia non dispone di misure come l'estendibilità.</span><span class="sxs-lookup"><span data-stu-id="30235-106">The trace does not have measurements as an extensibility.</span></span>

## <a name="message"></a><span data-ttu-id="30235-107">Message</span><span class="sxs-lookup"><span data-stu-id="30235-107">Message</span></span>

<span data-ttu-id="30235-108">Messaggio di traccia.</span><span class="sxs-lookup"><span data-stu-id="30235-108">Trace message.</span></span>

<span data-ttu-id="30235-109">Lunghezza massima: 32.768 caratteri</span><span class="sxs-lookup"><span data-stu-id="30235-109">Max length: 32768 characters</span></span>

## <a name="severity-level"></a><span data-ttu-id="30235-110">Livello di gravità</span><span class="sxs-lookup"><span data-stu-id="30235-110">Severity level</span></span>

<span data-ttu-id="30235-111">Livello di gravità della traccia.</span><span class="sxs-lookup"><span data-stu-id="30235-111">Trace severity level.</span></span> <span data-ttu-id="30235-112">Il valore può essere `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span><span class="sxs-lookup"><span data-stu-id="30235-112">Value can be `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span></span>

## <a name="custom-properties"></a><span data-ttu-id="30235-113">Proprietà personalizzate</span><span class="sxs-lookup"><span data-stu-id="30235-113">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="next-steps"></a><span data-ttu-id="30235-114">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="30235-114">Next steps</span></span>

- <span data-ttu-id="30235-115">[Esplorare i log di traccia .NET in Application Insights](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="30235-115">[Explore .NET trace logs in Application Insights](app-insights-asp-net-trace-logs.md).</span></span>
- <span data-ttu-id="30235-116">[Esplorare i log di traccia Java in Application Insights](app-insights-java-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="30235-116">[Explore Java trace logs in Application Insights](app-insights-java-trace-logs.md).</span></span>
- <span data-ttu-id="30235-117">Per informazioni sul modello di dati e sui tipi di Application Insights, vedere il [modello di dati](application-insights-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="30235-117">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- [<span data-ttu-id="30235-118">Scrivere dati di telemetria di traccia personalizzata</span><span class="sxs-lookup"><span data-stu-id="30235-118">Write custom trace telemetry</span></span>](app-insights-api-custom-events-metrics.md#tracktrace)
- <span data-ttu-id="30235-119">Verificare quali [piattaforme](app-insights-platforms.md) supportano Application Insights.</span><span class="sxs-lookup"><span data-stu-id="30235-119">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
