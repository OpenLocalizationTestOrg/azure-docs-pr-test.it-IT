---
title: ambiente di Azure ora serie Insights di aaaAdd riferimento set di dati tooyour | Documenti Microsoft
description: In questa esercitazione si aggiunta ambiente ora serie Insights tooyour set di dati di riferimento
keywords: 
services: time-series-insights
documentationcenter: 
author: venkatgct
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: venkatja
ms.openlocfilehash: 05e626ed81a22f2a8710b23a931ccd17c0f38ca5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-reference-data-set-for-your-time-series-insights-environment-using-hello-ibiza-portal"></a><span data-ttu-id="496ad-103">Creare un set di dati di riferimento per l'ambiente di tempo serie Insights utilizzando portale Ibiza hello</span><span class="sxs-lookup"><span data-stu-id="496ad-103">Create a reference data set for your Time Series Insights environment using hello Ibiza portal</span></span>

<span data-ttu-id="496ad-104">Un Set di dati di riferimento è una raccolta di elementi che sono dotati di eventi di hello dall'origine evento.</span><span class="sxs-lookup"><span data-stu-id="496ad-104">A Reference Data Set is a collection of items that are augmented with hello events from your event source.</span></span> <span data-ttu-id="496ad-105">Il motore in ingresso di Time Series Insights esegue il join di un evento dell'origine evento con un elemento del set di dati di riferimento.</span><span class="sxs-lookup"><span data-stu-id="496ad-105">Time Series Insights ingress engine joins an event from your event source with an item in your reference data set.</span></span> <span data-ttu-id="496ad-106">Questo evento aumentato sarà quindi disponibile per le query.</span><span class="sxs-lookup"><span data-stu-id="496ad-106">This augmented event is then available for query.</span></span> <span data-ttu-id="496ad-107">Questo join è basato su chiavi hello definite nel set di dati di riferimento.</span><span class="sxs-lookup"><span data-stu-id="496ad-107">This join is based on hello keys defined in your reference data set.</span></span>

## <a name="steps-tooadd-a-reference-data-set-tooyour-environment"></a><span data-ttu-id="496ad-108">Tooadd passaggi dell'ambiente tooyour un set di dati di riferimento</span><span class="sxs-lookup"><span data-stu-id="496ad-108">Steps tooadd a reference data set tooyour environment</span></span>

1. <span data-ttu-id="496ad-109">Accedi toohello [portale Ibiza](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="496ad-109">Sign in toohello [Ibiza portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="496ad-110">Fare clic su "Tutte le risorse" nel menu hello sul lato sinistro di hello del portale Ibiza hello.</span><span class="sxs-lookup"><span data-stu-id="496ad-110">Click “All resources” in hello menu on hello left side of hello Ibiza portal.</span></span>
3. <span data-ttu-id="496ad-111">Selezionare l'ambiente Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="496ad-111">Select your Time Series Insights environment.</span></span>

    ![Creare set di dati di riferimento ora serie Insights hello](media/add-reference-data-set/getstarted-create-reference-data-set-1.png)

4. <span data-ttu-id="496ad-113">Selezionare "Set di dati di riferimento" e fare clic su "+ Aggiungi".</span><span class="sxs-lookup"><span data-stu-id="496ad-113">Select “Reference Data Sets”, click “+ Add.”</span></span>

    ![Creare set di dati riferimento ora serie Insights hello - dettagli](media/add-reference-data-set/getstarted-create-reference-data-set-2.png)

5. <span data-ttu-id="496ad-115">Specificare il nome di hello hello riferimento del set di dati.</span><span class="sxs-lookup"><span data-stu-id="496ad-115">Specify hello name of hello reference data set.</span></span>
6. <span data-ttu-id="496ad-116">Specificare un nome della chiave hello e il relativo tipo.</span><span class="sxs-lookup"><span data-stu-id="496ad-116">Specify hello key name and its type.</span></span> <span data-ttu-id="496ad-117">Questo nome e il tipo è proprietà corretta di hello toopick utilizzato dall'evento hello nell'origine evento.</span><span class="sxs-lookup"><span data-stu-id="496ad-117">This name and type is used toopick hello correct property from hello event in your event source.</span></span> <span data-ttu-id="496ad-118">Ad esempio, se si forniscono come "DeviceId" nome della chiave e tipo "String", quindi hello ora serie Insights motore in ingresso esegue la ricerca di una proprietà con nome hello "DeviceId" di tipo "String" in caso di hello in arrivo.</span><span class="sxs-lookup"><span data-stu-id="496ad-118">For instance, if you provide key name as “DeviceId” and type as “String”, then hello Time Series Insights ingress engine looks for a property with hello name “DeviceId” of type “String” in hello incoming event.</span></span> <span data-ttu-id="496ad-119">È possibile fornire più toojoin chiave evento hello.</span><span class="sxs-lookup"><span data-stu-id="496ad-119">You can provide more than one key toojoin with hello event.</span></span> <span data-ttu-id="496ad-120">corrispondenza del nome di proprietà Hello è tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="496ad-120">hello property name match is case-sensitive.</span></span>

     ![Creare set di dati riferimento ora serie Insights hello - dettagli](media/add-reference-data-set/getstarted-create-reference-data-set-3.png)

7. <span data-ttu-id="496ad-122">Fare clic su "Crea".</span><span class="sxs-lookup"><span data-stu-id="496ad-122">Click “Create.”</span></span>

## <a name="next-steps"></a><span data-ttu-id="496ad-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="496ad-123">Next steps</span></span>

* <span data-ttu-id="496ad-124">[Gestire i dati di riferimento](time-series-insights-manage-reference-data-csharp.md) a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="496ad-124">[Manage reference data](time-series-insights-manage-reference-data-csharp.md) programmatically.</span></span>
* <span data-ttu-id="496ad-125">Per hello riferimento completo alle API, vedere [API di dati di riferimento](/rest/api/time-series-insights/time-series-insights-reference-reference-data-api) documento.</span><span class="sxs-lookup"><span data-stu-id="496ad-125">For hello complete API reference, see [Reference Data API](/rest/api/time-series-insights/time-series-insights-reference-reference-data-api) document.</span></span>
