---
title: le funzioni finestra Analitica di aaaIntroduction tooStream | Documenti Microsoft
description: Informazioni sui tre funzioni finestra hello in flusso Analitica (a cascata, di salto, scorrimento).
keywords: finestra a cascata, finestra temporale scorrevole, finestra di salto
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 0d8d8717-5d23-43f0-b475-af078ab4627d
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 7fc36eb9afb2b28e2791d925d26923145eb38074
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toostream-analytics-window-functions"></a><span data-ttu-id="28b8f-104">Funzioni finestra Analitica tooStream di introduzione</span><span class="sxs-lookup"><span data-stu-id="28b8f-104">Introduction tooStream Analytics Window functions</span></span>
<span data-ttu-id="28b8f-105">È necessario tooperform operazioni solo sui dati di hello contenuti nelle finestre temporali in tempo reale molti gli scenari di flusso.</span><span class="sxs-lookup"><span data-stu-id="28b8f-105">In many real time streaming scenarios, it is necessary tooperform operations only on hello data contained in temporal windows.</span></span> <span data-ttu-id="28b8f-106">Il supporto nativo per funzioni di windowing è una funzionalità chiave di Analitica di flusso di Azure che consente di spostare lancetta hello sulla produttività da sviluppatore per la creazione di processi di elaborazione di flusso complessi.</span><span class="sxs-lookup"><span data-stu-id="28b8f-106">Native support for windowing functions is a key feature of Azure Stream Analytics that moves hello needle on developer productivity in authoring complex stream processing jobs.</span></span> <span data-ttu-id="28b8f-107">Flusso Analitica consente agli sviluppatori toouse [ **a cascata**](https://msdn.microsoft.com/library/dn835055.aspx), [ **Hopping** ](https://msdn.microsoft.com/library/dn835041.aspx) e [ **estendibile** ](https://msdn.microsoft.com/library/dn835051.aspx) operazioni temporali tooperform di windows nel flusso di dati.</span><span class="sxs-lookup"><span data-stu-id="28b8f-107">Stream Analytics enables developers toouse [**Tumbling**](https://msdn.microsoft.com/library/dn835055.aspx), [**Hopping**](https://msdn.microsoft.com/library/dn835041.aspx) and [**Sliding**](https://msdn.microsoft.com/library/dn835051.aspx) windows tooperform temporal operations on streaming data.</span></span> <span data-ttu-id="28b8f-108">Vale la pena notare che tutti i [finestra](https://msdn.microsoft.com/library/dn835019.aspx) operazioni di output risultati hello **fine** della finestra hello.</span><span class="sxs-lookup"><span data-stu-id="28b8f-108">It is worth noting that all [Window](https://msdn.microsoft.com/library/dn835019.aspx) operations output results at hello **end** of hello window.</span></span> <span data-ttu-id="28b8f-109">output di Hello di finestra hello sarà singolo evento basato sulla funzione di aggregazione hello utilizzato.</span><span class="sxs-lookup"><span data-stu-id="28b8f-109">hello output of hello window will be single event based on hello aggregate function used.</span></span> <span data-ttu-id="28b8f-110">evento Hello avrà timestamp hello della fine hello finestra hello e tutte le funzioni finestra sono definite con una lunghezza fissa.</span><span class="sxs-lookup"><span data-stu-id="28b8f-110">hello event will have hello time stamp of hello end of hello window and all Window functions are defined with a fixed length.</span></span> <span data-ttu-id="28b8f-111">Infine è importante toonote che tutte le funzioni finestra devono essere utilizzate in un [ **GROUP BY** ](https://msdn.microsoft.com/library/dn835023.aspx) clausola.</span><span class="sxs-lookup"><span data-stu-id="28b8f-111">Lastly it is important toonote that all Window functions should be used in a [**GROUP BY**](https://msdn.microsoft.com/library/dn835023.aspx) clause.</span></span>

![Concetti delle funzioni finestra di Analisi di flusso](media/stream-analytics-window-functions/stream-analytics-window-functions-conceptual.png)

## <a name="tumbling-window"></a><span data-ttu-id="28b8f-113">Finestra a cascata</span><span class="sxs-lookup"><span data-stu-id="28b8f-113">Tumbling Window</span></span>
<span data-ttu-id="28b8f-114">Le funzioni finestra a cascata sono toosegment usato un flusso di dati in segmenti di tempo specifico ed eseguono una funzione su di essi, ad esempio esempio hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="28b8f-114">Tumbling window functions are used toosegment a data stream into distinct time segments and perform a function against them, such as hello example below.</span></span> <span data-ttu-id="28b8f-115">principali differenze di Hello di una finestra a cascata sono che ripetono, non si sovrappongano e un evento non può appartenere toomore rispetto a una finestra a cascata.</span><span class="sxs-lookup"><span data-stu-id="28b8f-115">hello key differentiators of a Tumbling window are that they repeat, do not overlap and an event cannot belong toomore than one tumbling window.</span></span>

![Introduzione alle funzioni finestra a cascata di Analisi di flusso](media/stream-analytics-window-functions/stream-analytics-window-functions-tumbling-intro.png)

## <a name="hopping-window"></a><span data-ttu-id="28b8f-117">Finestra di salto</span><span class="sxs-lookup"><span data-stu-id="28b8f-117">Hopping Window</span></span>
<span data-ttu-id="28b8f-118">Le funzioni finestra di salto consentono di avanzare nel tempo di un periodo fisso.</span><span class="sxs-lookup"><span data-stu-id="28b8f-118">Hopping window functions hop forward in time by a fixed period.</span></span> <span data-ttu-id="28b8f-119">Potrebbe essere facile toothink di essi come finestre a cascata che può essere sovrapposta, quindi gli eventi possono appartenere toomore rispetto a un set di risultati Hopping finestra.</span><span class="sxs-lookup"><span data-stu-id="28b8f-119">It may be easy toothink of them as Tumbling windows that can overlap, so events can belong toomore than one Hopping window result set.</span></span> <span data-ttu-id="28b8f-120">una finestra Hopping toomake hello stesso come una finestra a cascata semplicemente uno specificherà toobe di dimensioni hop hello hello stesso come dimensione della finestra hello.</span><span class="sxs-lookup"><span data-stu-id="28b8f-120">toomake a Hopping window hello same as a Tumbling window one would simply specify hello hop size toobe hello same as hello window size.</span></span> 

![Introduzione alle funzioni finestra di salto di Analisi di flusso](media/stream-analytics-window-functions/stream-analytics-window-functions-hopping-intro.png)

## <a name="sliding-window"></a><span data-ttu-id="28b8f-122">Finestra temporale scorrevole</span><span class="sxs-lookup"><span data-stu-id="28b8f-122">Sliding Window</span></span>
<span data-ttu-id="28b8f-123">Le funzioni finestra temporale scorrevole, diversamente dalle finestre a cascata o di salto, generano un output **solo** quando si verifica un evento.</span><span class="sxs-lookup"><span data-stu-id="28b8f-123">Sliding window functions, unlike Tumbling or Hopping windows, produce an output **only**  when an event occurs.</span></span> <span data-ttu-id="28b8f-124">Ogni finestra sarà necessario almeno un evento e finestra hello continuamente sposta in avanti un € (epsilon).</span><span class="sxs-lookup"><span data-stu-id="28b8f-124">Every window will have at least one event and hello window continuously moves forward by an € (epsilon).</span></span> <span data-ttu-id="28b8f-125">Ad esempio finestre di salto, gli eventi possono appartenere toomore rispetto a una finestra temporale scorrevole.</span><span class="sxs-lookup"><span data-stu-id="28b8f-125">Like Hopping Windows, events can belong toomore than one Sliding Window.</span></span>

![Introduzione alle funzioni finestra temporale scorrevole di Analisi di flusso](media/stream-analytics-window-functions/stream-analytics-window-functions-sliding-intro.png)

## <a name="getting-help-with-window-functions"></a><span data-ttu-id="28b8f-127">Risorse della Guida per le funzioni finestra</span><span class="sxs-lookup"><span data-stu-id="28b8f-127">Getting help with Window functions</span></span>
<span data-ttu-id="28b8f-128">Per ulteriore assistenza, provare il [Forum di Analisi dei flussi di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="28b8f-128">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="28b8f-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="28b8f-129">Next steps</span></span>
* [<span data-ttu-id="28b8f-130">Introduzione tooAzure flusso Analitica</span><span class="sxs-lookup"><span data-stu-id="28b8f-130">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="28b8f-131">Introduzione all'uso di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="28b8f-131">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="28b8f-132">Ridimensionare i processi di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="28b8f-132">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="28b8f-133">Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="28b8f-133">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="28b8f-134">Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="28b8f-134">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

