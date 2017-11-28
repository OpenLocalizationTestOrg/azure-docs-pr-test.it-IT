---
title: aaaVisualize e risolvere i problemi relativi a processi di flusso Analitica | Documenti Microsoft
description: "Informazioni su come un processo di flusso Analitica toovisualize della pipeline per la risoluzione dei problemi mediante funzionalità diagramma di diagnostica hello di Self-Service."
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
ms.openlocfilehash: 8a6715be601fdc47b8d9caf4112da161dad22618
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-and-troubleshoot-stream-analytics-jobs"></a><span data-ttu-id="de21f-103">Visualizzare e risolvere i problemi di Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="de21f-103">Visualize and troubleshoot Stream Analytics jobs</span></span>
<span data-ttu-id="de21f-104">Nel flusso Analitica, come con altre tecnologie basate su cloud, risoluzione dei problemi è talvolta toolook necessari in un processo perché non produrre output previsto hello (o qualsiasi output a tale scopo).</span><span class="sxs-lookup"><span data-stu-id="de21f-104">In Stream Analytics, as with other cloud-based technologies, troubleshooting is sometimes needed toolook into why a job does not produce hello expected output (or any output for that matter).</span></span> <span data-ttu-id="de21f-105">A tal fine, Analitica di flusso fornisce le funzionalità di hello per la visualizzazione di un processo di streaming.</span><span class="sxs-lookup"><span data-stu-id="de21f-105">With this in mind, Stream Analytics provides hello capability for visualizing a streaming job.</span></span> <span data-ttu-id="de21f-106">È inoltre utile come strumento di modellazione e ha vantaggio hello per quelle che richiedono la documentazione del proprio lavoro.</span><span class="sxs-lookup"><span data-stu-id="de21f-106">This is also handy as a modeling tool and has hello side benefit for those requiring documentation of their work.</span></span>

<span data-ttu-id="de21f-107">In visualizzazione hello input hello pannello sono visibili e query hello in esecuzione e quindi tutti gli output di hello configurato.</span><span class="sxs-lookup"><span data-stu-id="de21f-107">In hello visualization panel hello inputs are visible as well as hello query being executed and then all hello outputs configured.</span></span> <span data-ttu-id="de21f-108">Problemi di connettività o di configurazione possono diventare più evidenti e può anche essere utile toosee una rappresentazione visiva della configurazione.</span><span class="sxs-lookup"><span data-stu-id="de21f-108">Connectivity or configuration issues can become more apparent and it can also be helpful toosee a visual representation of your configuration.</span></span>

## <a name="using-hello-diagnosis-diagram-tool"></a><span data-ttu-id="de21f-109">Lo strumento hello diagnosi diagramma</span><span class="sxs-lookup"><span data-stu-id="de21f-109">Using hello diagnosis diagram tool</span></span>
<span data-ttu-id="de21f-110">questo visualizzatore, è sufficiente fare clic sul pulsante "Diagramma diagnosi" di hello tooaccess hello blade "Impostazioni" di hello del processo di flusso Analitica hello.</span><span class="sxs-lookup"><span data-stu-id="de21f-110">tooaccess this visualizer, simply click on hello “Diagnosis diagram” button in hello “Settings” blade of hello of hello Stream Analytics job.</span></span>

![stream-analytics-troubleshoot-visualization-diagnosis-diagram](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-diagnosis-diagram1.png)

<span data-ttu-id="de21f-112">Ogni input e output è codificato tramite colori tooindicate hello stato corrente del componente, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="de21f-112">Every input and output is color coded tooindicate hello current state of that component, as shown below.</span></span>

![stream-analytics-troubleshoot-visualization-input-map](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-input-map.png)

<span data-ttu-id="de21f-114">Con toolook query intermedi passaggi toounderstand hello dati flusso modelli all'interno di un processo di consenso dell'utente hello, strumento di visualizzazione hello fornisce una visualizzazione di riepilogo hello delle query hello in relativi passaggi dei componenti e di sequenza del flusso di hello.</span><span class="sxs-lookup"><span data-stu-id="de21f-114">When hello user wants toolook at intermediate query steps toounderstand hello data flow patterns inside a job, hello visualization tool provides a view of hello breakdown of hello query into its component steps and hello flow sequence.</span></span> <span data-ttu-id="de21f-115">Facendo clic su ogni passaggio della query mostrerà la sezione corrispondente di hello in una query, la modifica di riquadro, come illustrato.</span><span class="sxs-lookup"><span data-stu-id="de21f-115">Clicking on each query step will show hello corresponding section in a query editing pane as illustrated.</span></span> 

![stream-analytics-troubleshoot-visualization-intermediate-steps](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-intermediate-steps.png)

## <a name="next-steps"></a><span data-ttu-id="de21f-117">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="de21f-117">Next steps</span></span>
* [<span data-ttu-id="de21f-118">Introduzione tooAzure flusso Analitica</span><span class="sxs-lookup"><span data-stu-id="de21f-118">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="de21f-119">Introduzione all'uso di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="de21f-119">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="de21f-120">Ridimensionare i processi di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="de21f-120">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="de21f-121">Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="de21f-121">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="de21f-122">Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="de21f-122">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

