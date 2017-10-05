---
title: Introduzione alle funzioni finestra di Analisi di flusso | Documentazione Microsoft
description: Informazioni sulle tre funzioni finestra in Analisi di flusso (finestra a cascata, finestra di salto, finestra temporale scorrevole).
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
ms.openlocfilehash: 09915ad747153210f655b152355c551046066a88
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="introduction-to-stream-analytics-window-functions"></a><span data-ttu-id="3fa26-104">Introduzione alle funzioni finestra di Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="3fa26-104">Introduction to Stream Analytics Window functions</span></span>
<span data-ttu-id="3fa26-105">In molti scenari di flusso in tempo reale è necessario eseguire operazioni solo sui dati contenuti in finestre temporali.</span><span class="sxs-lookup"><span data-stu-id="3fa26-105">In many real time streaming scenarios, it is necessary to perform operations only on the data contained in temporal windows.</span></span> <span data-ttu-id="3fa26-106">Il supporto nativo delle funzioni finestra è una funzionalità cruciale di Analisi di flusso di Azure che pone l'accento sulla produttività degli sviluppatori per la creazione di processi di elaborazione di flussi complessi.</span><span class="sxs-lookup"><span data-stu-id="3fa26-106">Native support for windowing functions is a key feature of Azure Stream Analytics that moves the needle on developer productivity in authoring complex stream processing jobs.</span></span> <span data-ttu-id="3fa26-107">Analisi di flusso consente agli sviluppatori di usare finestre [**a cascata**](https://msdn.microsoft.com/library/dn835055.aspx), [**di salto**](https://msdn.microsoft.com/library/dn835041.aspx) e [**temporali scorrevoli**](https://msdn.microsoft.com/library/dn835051.aspx) per eseguire operazioni temporali sui dati di flusso.</span><span class="sxs-lookup"><span data-stu-id="3fa26-107">Stream Analytics enables developers to use [**Tumbling**](https://msdn.microsoft.com/library/dn835055.aspx), [**Hopping**](https://msdn.microsoft.com/library/dn835041.aspx) and [**Sliding**](https://msdn.microsoft.com/library/dn835051.aspx) windows to perform temporal operations on streaming data.</span></span> <span data-ttu-id="3fa26-108">Vale la pena di sottolineare che tutte le operazioni [finestra](https://msdn.microsoft.com/library/dn835019.aspx) restituiscono i risultati alla **fine** della finestra.</span><span class="sxs-lookup"><span data-stu-id="3fa26-108">It is worth noting that all [Window](https://msdn.microsoft.com/library/dn835019.aspx) operations output results at the **end** of the window.</span></span> <span data-ttu-id="3fa26-109">L'output della finestra sarà un singolo evento basato sulla funzione di aggregazione usata.</span><span class="sxs-lookup"><span data-stu-id="3fa26-109">The output of the window will be single event based on the aggregate function used.</span></span> <span data-ttu-id="3fa26-110">All'evento sarà associato il timestamp di fine della finestra e tutte le funzioni finestra sono definite con una lunghezza fissa.</span><span class="sxs-lookup"><span data-stu-id="3fa26-110">The event will have the time stamp of the end of the window and all Window functions are defined with a fixed length.</span></span> <span data-ttu-id="3fa26-111">Infine, è importante segnalare che tutte le funzioni finestra devono essere usate in una clausola [**GROUP BY**](https://msdn.microsoft.com/library/dn835023.aspx).</span><span class="sxs-lookup"><span data-stu-id="3fa26-111">Lastly it is important to note that all Window functions should be used in a [**GROUP BY**](https://msdn.microsoft.com/library/dn835023.aspx) clause.</span></span>

![Concetti delle funzioni finestra di Analisi di flusso](media/stream-analytics-window-functions/stream-analytics-window-functions-conceptual.png)

## <a name="tumbling-window"></a><span data-ttu-id="3fa26-113">Finestra a cascata</span><span class="sxs-lookup"><span data-stu-id="3fa26-113">Tumbling Window</span></span>
<span data-ttu-id="3fa26-114">Le funzioni finestra a cascata vengono usate per segmentare un flusso di dati in segmenti temporali distinti e per eseguire una funzione su tali segmenti, come nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="3fa26-114">Tumbling window functions are used to segment a data stream into distinct time segments and perform a function against them, such as the example below.</span></span> <span data-ttu-id="3fa26-115">I principali elementi distintivi di una finestra a cascata sono la ripetitività e la non sovrapposizione, oltre al fatto che un evento non può appartenere a più di una finestra a cascata.</span><span class="sxs-lookup"><span data-stu-id="3fa26-115">The key differentiators of a Tumbling window are that they repeat, do not overlap and an event cannot belong to more than one tumbling window.</span></span>

![Introduzione alle funzioni finestra a cascata di Analisi di flusso](media/stream-analytics-window-functions/stream-analytics-window-functions-tumbling-intro.png)

## <a name="hopping-window"></a><span data-ttu-id="3fa26-117">Finestra di salto</span><span class="sxs-lookup"><span data-stu-id="3fa26-117">Hopping Window</span></span>
<span data-ttu-id="3fa26-118">Le funzioni finestra di salto consentono di avanzare nel tempo di un periodo fisso.</span><span class="sxs-lookup"><span data-stu-id="3fa26-118">Hopping window functions hop forward in time by a fixed period.</span></span> <span data-ttu-id="3fa26-119">Può essere utile pensare a queste finestre come finestre a cascata che possono essere sovrapposte, quindi gli eventi possono appartenere a più di un set di risultati della finestra di salto.</span><span class="sxs-lookup"><span data-stu-id="3fa26-119">It may be easy to think of them as Tumbling windows that can overlap, so events can belong to more than one Hopping window result set.</span></span> <span data-ttu-id="3fa26-120">Per creare una finestra di salto uguale a una finestra a cascata, basterebbe specificare dimensioni del salto uguali alle dimensioni della finestra.</span><span class="sxs-lookup"><span data-stu-id="3fa26-120">To make a Hopping window the same as a Tumbling window one would simply specify the hop size to be the same as the window size.</span></span> 

![Introduzione alle funzioni finestra di salto di Analisi di flusso](media/stream-analytics-window-functions/stream-analytics-window-functions-hopping-intro.png)

## <a name="sliding-window"></a><span data-ttu-id="3fa26-122">Finestra temporale scorrevole</span><span class="sxs-lookup"><span data-stu-id="3fa26-122">Sliding Window</span></span>
<span data-ttu-id="3fa26-123">Le funzioni finestra temporale scorrevole, diversamente dalle finestre a cascata o di salto, generano un output **solo** quando si verifica un evento.</span><span class="sxs-lookup"><span data-stu-id="3fa26-123">Sliding window functions, unlike Tumbling or Hopping windows, produce an output **only**  when an event occurs.</span></span> <span data-ttu-id="3fa26-124">Ogni finestra avrà almeno un evento e la finestra si sposta continuamente in avanti di un € (epsilon).</span><span class="sxs-lookup"><span data-stu-id="3fa26-124">Every window will have at least one event and the window continuously moves forward by an € (epsilon).</span></span> <span data-ttu-id="3fa26-125">Come le finestre di salto, gli eventi possono appartenere a più di una finestra temporale scorrevole.</span><span class="sxs-lookup"><span data-stu-id="3fa26-125">Like Hopping Windows, events can belong to more than one Sliding Window.</span></span>

![Introduzione alle funzioni finestra temporale scorrevole di Analisi di flusso](media/stream-analytics-window-functions/stream-analytics-window-functions-sliding-intro.png)

## <a name="getting-help-with-window-functions"></a><span data-ttu-id="3fa26-127">Risorse della Guida per le funzioni finestra</span><span class="sxs-lookup"><span data-stu-id="3fa26-127">Getting help with Window functions</span></span>
<span data-ttu-id="3fa26-128">Per ulteriore assistenza, provare il [Forum di Analisi dei flussi di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="3fa26-128">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="3fa26-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3fa26-129">Next steps</span></span>
* [<span data-ttu-id="3fa26-130">Introduzione ad Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="3fa26-130">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="3fa26-131">Introduzione all'uso di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="3fa26-131">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="3fa26-132">Ridimensionare i processi di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="3fa26-132">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="3fa26-133">Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="3fa26-133">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="3fa26-134">Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="3fa26-134">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

