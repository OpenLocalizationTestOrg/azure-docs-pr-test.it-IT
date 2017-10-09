---
title: aaaAzure modello dati di telemetria Insights di applicazione - evento di telemetria | Documenti Microsoft
description: Modello di dati di Application Insights per la telemetria degli eventi
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
ms.openlocfilehash: cd7dc3c5f4f3df22b7a52ee79fcad566a27a9f4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="event-telemetry-application-insights-data-model"></a><span data-ttu-id="f71f1-103">Telemetria degli eventi: modello di dati di Application Insights</span><span class="sxs-lookup"><span data-stu-id="f71f1-103">Event telemetry: Application Insights data model</span></span>

<span data-ttu-id="f71f1-104">È possibile creare elementi di dati di telemetria evento (in [Application Insights](app-insights-overview.md)) toorepresent un evento che si sono verificati nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f71f1-104">You can create event telemetry items (in [Application Insights](app-insights-overview.md)) toorepresent an event that occurred in your application.</span></span> <span data-ttu-id="f71f1-105">Si tratta in genere di un'interazione dell'utente, ad esempio il clic su un pulsante o il completamento della transazione di un ordine.</span><span class="sxs-lookup"><span data-stu-id="f71f1-105">Typically it is a user interaction such as button click or order checkout.</span></span> <span data-ttu-id="f71f1-106">Può inoltre essere un evento del ciclo di vita dell'applicazione come l'inizializzazione o l'aggiornamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="f71f1-106">It can also be an application life cycle event like initialization or configuration update.</span></span> 

<span data-ttu-id="f71f1-107">Semanticamente, gli eventi potrebbero non essere toorequests correlato.</span><span class="sxs-lookup"><span data-stu-id="f71f1-107">Semantically, events may or may not be correlated toorequests.</span></span> <span data-ttu-id="f71f1-108">Se usata correttamente, la telemetria degli eventi è tuttavia più importante delle richieste o delle tracce.</span><span class="sxs-lookup"><span data-stu-id="f71f1-108">However, if used properly, event telemetry is more important than requests or traces.</span></span> <span data-ttu-id="f71f1-109">Eventi rappresentano dati di telemetria business e deve essere un oggetto tooseparate, meno rigide [campionamento](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="f71f1-109">Events represent business telemetry and should be a subject tooseparate, less aggressive [sampling](app-insights-api-filtering-sampling.md).</span></span>

## <a name="name"></a><span data-ttu-id="f71f1-110">Nome</span><span class="sxs-lookup"><span data-stu-id="f71f1-110">Name</span></span>

<span data-ttu-id="f71f1-111">Nome evento.</span><span class="sxs-lookup"><span data-stu-id="f71f1-111">Event name.</span></span> <span data-ttu-id="f71f1-112">raggruppamento appropriate tooallow e metriche utile limitare l'applicazione in modo che generi un numero ridotto di nomi di evento separato.</span><span class="sxs-lookup"><span data-stu-id="f71f1-112">tooallow proper grouping and useful metrics, restrict your application so that it generates a small number of separate event names.</span></span> <span data-ttu-id="f71f1-113">Ad esempio, non usare un nome distinto per ogni istanza generata di un evento.</span><span class="sxs-lookup"><span data-stu-id="f71f1-113">For example, don't use a separate name for each generated instance of an event.</span></span>

<span data-ttu-id="f71f1-114">Lunghezza massima: 512 caratteri</span><span class="sxs-lookup"><span data-stu-id="f71f1-114">Max length: 512 characters</span></span>

## <a name="custom-properties"></a><span data-ttu-id="f71f1-115">Proprietà personalizzate</span><span class="sxs-lookup"><span data-stu-id="f71f1-115">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="f71f1-116">Misure personalizzate</span><span class="sxs-lookup"><span data-stu-id="f71f1-116">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a><span data-ttu-id="f71f1-117">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f71f1-117">Next steps</span></span>

- <span data-ttu-id="f71f1-118">Per informazioni sul modello di dati e sui tipi di Application Insights, vedere il [modello di dati](application-insights-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="f71f1-118">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- [<span data-ttu-id="f71f1-119">Scrivere dati di telemetria di eventi personalizzati</span><span class="sxs-lookup"><span data-stu-id="f71f1-119">Write custom event telemetry</span></span>](app-insights-api-custom-events-metrics.md#trackevent)
- <span data-ttu-id="f71f1-120">Verificare quali [piattaforme](app-insights-platforms.md) supportano Application Insights.</span><span class="sxs-lookup"><span data-stu-id="f71f1-120">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
