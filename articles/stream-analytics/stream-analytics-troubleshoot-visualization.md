---
title: Visualizzare e risolvere i problemi dei processi dell'analisi di flusso | Microsoft Docs
description: "Informazioni su come visualizzare una pipeline dei processi di Analisi di flusso per risolvere i problemi in modo autonomo mediante la funzionalità Diagramma diagnosi."
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: d87841cd-c59f-4a46-b46e-8b904fdc12e9
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 18c39a025f750cf5a17c535ab40923b7cafe413d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="visualize-and-troubleshoot-stream-analytics-jobs"></a><span data-ttu-id="6be7b-103">Visualizzare e risolvere i problemi di Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="6be7b-103">Visualize and troubleshoot Stream Analytics jobs</span></span>
<span data-ttu-id="6be7b-104">In Analisi di flusso, come in altre tecnologie basate su cloud, è talvolta necessario eseguire operazioni di risoluzione dei problemi per comprendere il motivo per cui un processo non produce l'output previsto o non ne produce alcuno.</span><span class="sxs-lookup"><span data-stu-id="6be7b-104">In Stream Analytics, as with other cloud-based technologies, troubleshooting is sometimes needed to look into why a job does not produce the expected output (or any output for that matter).</span></span> <span data-ttu-id="6be7b-105">Tenendo presente tale premessa, Analisi di flusso offre la possibilità di visualizzare un processo di streaming.</span><span class="sxs-lookup"><span data-stu-id="6be7b-105">With this in mind, Stream Analytics provides the capability for visualizing a streaming job.</span></span> <span data-ttu-id="6be7b-106">Questa funzionalità si rivela utile anche come strumento di modellazione e risulta vantaggiosa per gli utenti che hanno la necessità di documentare il proprio lavoro.</span><span class="sxs-lookup"><span data-stu-id="6be7b-106">This is also handy as a modeling tool and has the side benefit for those requiring documentation of their work.</span></span>

<span data-ttu-id="6be7b-107">Nel pannello di visualizzazione sono visibili non solo gli input ma anche la query in fase di esecuzione e quindi tutti gli output configurati.</span><span class="sxs-lookup"><span data-stu-id="6be7b-107">In the visualization panel the inputs are visible as well as the query being executed and then all the outputs configured.</span></span> <span data-ttu-id="6be7b-108">È possibile visualizzare con maggiore evidenza i problemi di connettività o configurazione. Può inoltre essere utile avere una rappresentazione visiva della configurazione.</span><span class="sxs-lookup"><span data-stu-id="6be7b-108">Connectivity or configuration issues can become more apparent and it can also be helpful to see a visual representation of your configuration.</span></span>

## <a name="using-the-diagnosis-diagram-tool"></a><span data-ttu-id="6be7b-109">Uso dello strumento Diagramma diagnosi</span><span class="sxs-lookup"><span data-stu-id="6be7b-109">Using the diagnosis diagram tool</span></span>
<span data-ttu-id="6be7b-110">Per accedere a questo visualizzatore è sufficiente fare clic sul pulsante Diagramma diagnosi nel pannello Impostazioni del processo di Analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="6be7b-110">To access this visualizer, simply click on the “Diagnosis diagram” button in the “Settings” blade of the of the Stream Analytics job.</span></span>

![stream-analytics-troubleshoot-visualization-diagnosis-diagram](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-diagnosis-diagram1.png)

<span data-ttu-id="6be7b-112">Ogni input e output è contraddistinto dal colore per indicare lo stato corrente del componente, come mostrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="6be7b-112">Every input and output is color coded to indicate the current state of that component, as shown below.</span></span>

![stream-analytics-troubleshoot-visualization-input-map](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-input-map.png)

<span data-ttu-id="6be7b-114">Se l'utente desidera esaminare i passaggi intermedi della query per comprendere i modelli del flusso di dati all'interno di un processo, lo strumento di visualizzazione mostra la scomposizione della query nei passaggi che la compongono nonché la sequenza del flusso.</span><span class="sxs-lookup"><span data-stu-id="6be7b-114">When the user wants to look at intermediate query steps to understand the data flow patterns inside a job, the visualization tool provides a view of the breakdown of the query into its component steps and the flow sequence.</span></span> <span data-ttu-id="6be7b-115">Facendo clic su ciascun passaggio della query verrà visualizzata la sezione corrispondente in un apposito riquadro di modifica, come mostrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="6be7b-115">Clicking on each query step will show the corresponding section in a query editing pane as illustrated.</span></span> 

![stream-analytics-troubleshoot-visualization-intermediate-steps](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-intermediate-steps.png)

## <a name="next-steps"></a><span data-ttu-id="6be7b-117">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6be7b-117">Next steps</span></span>
* [<span data-ttu-id="6be7b-118">Introduzione ad Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="6be7b-118">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="6be7b-119">Introduzione all'uso di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="6be7b-119">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="6be7b-120">Ridimensionare i processi di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="6be7b-120">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="6be7b-121">Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="6be7b-121">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="6be7b-122">Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="6be7b-122">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

