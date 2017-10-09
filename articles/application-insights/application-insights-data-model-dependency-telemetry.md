---
title: aaaAzure modello dati di telemetria Insights di applicazione - i dati di telemetria | Documenti Microsoft
description: Modello di dati di Application Insights per la telemetria delle dipendenze
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/17/2017
ms.author: bwren
ms.openlocfilehash: cd5ab7c61d3498e4aa2a0aa0c8b0d106a92912e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="dependency-telemetry-application-insights-data-model"></a><span data-ttu-id="4bf3d-103">Telemetria delle dipendenze: modello di dati di Application Insights</span><span class="sxs-lookup"><span data-stu-id="4bf3d-103">Dependency telemetry: Application Insights data model</span></span>

<span data-ttu-id="4bf3d-104">I dati di telemetria (in [Application Insights](app-insights-overview.md)) rappresenta un'interazione del componente monitorato hello con un componente remoto, ad esempio SQL o un endpoint HTTP.</span><span class="sxs-lookup"><span data-stu-id="4bf3d-104">Dependency Telemetry (in [Application Insights](app-insights-overview.md)) represents an interaction of hello monitored component with a remote component such as SQL or an HTTP endpoint.</span></span>

## <a name="name"></a><span data-ttu-id="4bf3d-105">Nome</span><span class="sxs-lookup"><span data-stu-id="4bf3d-105">Name</span></span>

<span data-ttu-id="4bf3d-106">Nome del comando hello avviata con questa chiamata della dipendenza.</span><span class="sxs-lookup"><span data-stu-id="4bf3d-106">Name of hello command initiated with this dependency call.</span></span> <span data-ttu-id="4bf3d-107">Valore di cardinalità basso.</span><span class="sxs-lookup"><span data-stu-id="4bf3d-107">Low cardinality value.</span></span> <span data-ttu-id="4bf3d-108">Esempi sono il nome della stored procedure e il modello di percorso URL.</span><span class="sxs-lookup"><span data-stu-id="4bf3d-108">Examples are stored procedure name and URL path template.</span></span>

## <a name="id"></a><span data-ttu-id="4bf3d-109">ID</span><span class="sxs-lookup"><span data-stu-id="4bf3d-109">ID</span></span>

<span data-ttu-id="4bf3d-110">Identificatore dell'istanza di una chiamata delle dipendenze.</span><span class="sxs-lookup"><span data-stu-id="4bf3d-110">Identifier of a dependency call instance.</span></span> <span data-ttu-id="4bf3d-111">Utilizzato per la correlazione con l'elemento di dati di telemetria richiesta hello corrispondente chiamata della dipendenza toothis.</span><span class="sxs-lookup"><span data-stu-id="4bf3d-111">Used for correlation with hello request telemetry item corresponding toothis dependency call.</span></span> <span data-ttu-id="4bf3d-112">Per altre informazioni vedere la pagina relativa alla [correlazione](application-insights-correlation.md).</span><span class="sxs-lookup"><span data-stu-id="4bf3d-112">For more information, see [correlation](application-insights-correlation.md) page.</span></span>

## <a name="data"></a><span data-ttu-id="4bf3d-113">Dati</span><span class="sxs-lookup"><span data-stu-id="4bf3d-113">Data</span></span>

<span data-ttu-id="4bf3d-114">Comando avviato con questa chiamata delle dipendenze.</span><span class="sxs-lookup"><span data-stu-id="4bf3d-114">Command initiated by this dependency call.</span></span> <span data-ttu-id="4bf3d-115">Esempi sono l'istruzione SQL e l'URL HTTP con tutti i parametri di query.</span><span class="sxs-lookup"><span data-stu-id="4bf3d-115">Examples are SQL statement and HTTP URL with all query parameters.</span></span>

## <a name="type"></a><span data-ttu-id="4bf3d-116">Tipo</span><span class="sxs-lookup"><span data-stu-id="4bf3d-116">Type</span></span>

<span data-ttu-id="4bf3d-117">Nome del tipo di dipendenza.</span><span class="sxs-lookup"><span data-stu-id="4bf3d-117">Dependency type name.</span></span> <span data-ttu-id="4bf3d-118">Valore di cardinalità basso per un raggruppamento logico delle dipendenze e l'interpretazione di altri campi come commandName e resultCode.</span><span class="sxs-lookup"><span data-stu-id="4bf3d-118">Low cardinality value for logical grouping of dependencies and interpretation of other fields like commandName and resultCode.</span></span> <span data-ttu-id="4bf3d-119">Esempi sono SQL, tabelle di Azure e HTTP.</span><span class="sxs-lookup"><span data-stu-id="4bf3d-119">Examples are SQL, Azure table, and HTTP.</span></span>

## <a name="target"></a><span data-ttu-id="4bf3d-120">Destinazione</span><span class="sxs-lookup"><span data-stu-id="4bf3d-120">Target</span></span>

<span data-ttu-id="4bf3d-121">Sito di destinazione di una chiamata delle dipendenze.</span><span class="sxs-lookup"><span data-stu-id="4bf3d-121">Target site of a dependency call.</span></span> <span data-ttu-id="4bf3d-122">Esempi sono nome del server, indirizzo host.</span><span class="sxs-lookup"><span data-stu-id="4bf3d-122">Examples are server name, host address.</span></span> <span data-ttu-id="4bf3d-123">Per altre informazioni vedere la pagina relativa alla [correlazione](application-insights-correlation.md).</span><span class="sxs-lookup"><span data-stu-id="4bf3d-123">For more information, see [correlation](application-insights-correlation.md) page.</span></span>

## <a name="duration"></a><span data-ttu-id="4bf3d-124">Durata</span><span class="sxs-lookup"><span data-stu-id="4bf3d-124">Duration</span></span>

<span data-ttu-id="4bf3d-125">Durata della richiesta in formato: `DD.HH:MM:SS.MMMMMM`.</span><span class="sxs-lookup"><span data-stu-id="4bf3d-125">Request duration in format: `DD.HH:MM:SS.MMMMMM`.</span></span> <span data-ttu-id="4bf3d-126">Deve essere inferiore a `1000` giorni.</span><span class="sxs-lookup"><span data-stu-id="4bf3d-126">Must be less than `1000` days.</span></span>

## <a name="result-code"></a><span data-ttu-id="4bf3d-127">Codice risultato</span><span class="sxs-lookup"><span data-stu-id="4bf3d-127">Result code</span></span>

<span data-ttu-id="4bf3d-128">Codice risultato di una chiamata delle dipendenze.</span><span class="sxs-lookup"><span data-stu-id="4bf3d-128">Result code of a dependency call.</span></span> <span data-ttu-id="4bf3d-129">Esempi sono il codice di errore SQL e il codice di stato HTTP.</span><span class="sxs-lookup"><span data-stu-id="4bf3d-129">Examples are SQL error code and HTTP status code.</span></span>

## <a name="success"></a><span data-ttu-id="4bf3d-130">Success</span><span class="sxs-lookup"><span data-stu-id="4bf3d-130">Success</span></span>

<span data-ttu-id="4bf3d-131">Indicazione di chiamata con esito positivo o con esito negativo.</span><span class="sxs-lookup"><span data-stu-id="4bf3d-131">Indication of successful or unsuccessful call.</span></span>

## <a name="custom-properties"></a><span data-ttu-id="4bf3d-132">Proprietà personalizzate</span><span class="sxs-lookup"><span data-stu-id="4bf3d-132">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="4bf3d-133">Misure personalizzate</span><span class="sxs-lookup"><span data-stu-id="4bf3d-133">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]


## <a name="next-steps"></a><span data-ttu-id="4bf3d-134">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4bf3d-134">Next steps</span></span>

- <span data-ttu-id="4bf3d-135">Impostare il rilevamento delle dipendenze per [.NET](app-insights-asp-net-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="4bf3d-135">Set up dependency tracking for [.NET](app-insights-asp-net-dependencies.md).</span></span>
- <span data-ttu-id="4bf3d-136">Impostare il rilevamento delle dipendenze per [Java](app-insights-java-agent.md).</span><span class="sxs-lookup"><span data-stu-id="4bf3d-136">Set up dependency tracking for [Java](app-insights-java-agent.md).</span></span>
- [<span data-ttu-id="4bf3d-137">Scrivere dati di telemetria delle dipendenze personalizzate</span><span class="sxs-lookup"><span data-stu-id="4bf3d-137">Write custom dependency telemetry</span></span>](app-insights-api-custom-events-metrics.md#trackdependency)
- <span data-ttu-id="4bf3d-138">Per informazioni sul modello di dati e sui tipi di Application Insights, vedere il [modello di dati](application-insights-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="4bf3d-138">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="4bf3d-139">Verificare quali [piattaforme](app-insights-platforms.md) supportano Application Insights.</span><span class="sxs-lookup"><span data-stu-id="4bf3d-139">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
