---
title: hello aaaUse visualizzazione esecuzione vertice in Data Lake Tools per Visual Studio | Documenti Microsoft
description: Informazioni su come toouse hello i processi di Data Lake Analitica tooexam visualizzazione esecuzione vertice.
services: data-lake-analytics
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 5366d852-e7d6-44cf-a88c-e9f52f15f7df
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/13/2016
ms.author: jgao
ms.openlocfilehash: fb54d2af8a32aa27a54ff50a73c1b4903677a21e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-vertex-execution-view-in-data-lake-tools-for-visual-studio"></a><span data-ttu-id="e0ed4-103">Utilizzare Visualizzazione esecuzione vertice hello in Data Lake Tools per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e0ed4-103">Use hello Vertex Execution View in Data Lake Tools for Visual Studio</span></span>
<span data-ttu-id="e0ed4-104">Informazioni su come toouse hello i processi di Data Lake Analitica tooexam visualizzazione esecuzione vertice.</span><span class="sxs-lookup"><span data-stu-id="e0ed4-104">Learn how toouse hello Vertex Execution View tooexam Data Lake Analytics jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e0ed4-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e0ed4-105">Prerequisites</span></span>

<span data-ttu-id="e0ed4-106">Occorre una conoscenza di base dell'utilizzo di Data Lake strumenti per lo script U-SQL toodevelop di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e0ed4-106">You need basic knowledge of using Data Lake Tools for Visual Studio toodevelop U-SQL script.</span></span>  <span data-ttu-id="e0ed4-107">Vedere [Esercitazione: Sviluppare script U-SQL tramite Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e0ed4-107">See [Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>

## <a name="open-hello-vertex-execution-view"></a><span data-ttu-id="e0ed4-108">Aprire visualizzazione esecuzione vertice hello</span><span class="sxs-lookup"><span data-stu-id="e0ed4-108">Open hello Vertex Execution View</span></span>
<span data-ttu-id="e0ed4-109">Aprire un processo U-SQL in Strumenti Data Lake per Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e0ed4-109">Open a U-SQL job in Data Lake Tools for Visual Studio.</span></span> <span data-ttu-id="e0ed4-110">Fare clic su **visualizzazione esecuzione vertice** nell'angolo inferiore sinistro di hello.</span><span class="sxs-lookup"><span data-stu-id="e0ed4-110">Click **Vertex Execution View** in hello bottom left corner.</span></span> <span data-ttu-id="e0ed4-111">È possibile profili tooload richiesta innanzitutto e può richiedere alcuni minuti in base la connettività di rete.</span><span class="sxs-lookup"><span data-stu-id="e0ed4-111">You may be prompted tooload profiles first and it can take some time depending on your network connectivity.</span></span>

![Visualizzazione esecuzioni vertici di Data Lake Analytics Tools](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-open-vertex-execution-view.png)

## <a name="understand-vertex-execution-view"></a><span data-ttu-id="e0ed4-113">Informazioni sulla visualizzazione esecuzioni vertici</span><span class="sxs-lookup"><span data-stu-id="e0ed4-113">Understand Vertex Execution View</span></span>
<span data-ttu-id="e0ed4-114">Visualizzazione esecuzione vertice Hello include tre parti:</span><span class="sxs-lookup"><span data-stu-id="e0ed4-114">hello Vertex Execution View has three parts:</span></span>

![Visualizzazione esecuzioni vertici di Data Lake Analytics Tools](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view.png)

<span data-ttu-id="e0ed4-116">Hello **selettore vertice** sulla sinistra consente di hello selezionate vertici dalle funzionalità (ad esempio le prime 10 dati di lettura o scegliere dalla fase).</span><span class="sxs-lookup"><span data-stu-id="e0ed4-116">hello **Vertex selector** on hello left lets you select vertices by features (such as top 10 data read, or choose by stage).</span></span> <span data-ttu-id="e0ed4-117">Uno dei filtri di uso frequente hello è hello toosee **vertici sul percorso critico**.</span><span class="sxs-lookup"><span data-stu-id="e0ed4-117">One of hello most commonly-used filters is toosee hello **vertices on critical path**.</span></span> <span data-ttu-id="e0ed4-118">Hello **percorso critico** hello catena più lungo di vertici di un processo U-SQL.</span><span class="sxs-lookup"><span data-stu-id="e0ed4-118">hello **Critical path** is hello longest chain of vertices of a U-SQL job.</span></span> <span data-ttu-id="e0ed4-119">Percorso critico di conoscenza hello è utile per ottimizzare i processi controllando il vertice richiede tempo più lungo di hello.</span><span class="sxs-lookup"><span data-stu-id="e0ed4-119">Understanding hello critical path is useful for optimizing your jobs by checking which vertex takes hello longest time.</span></span>
  
![Visualizzazione esecuzioni vertici di Data Lake Analytics Tools](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane2.png)

<span data-ttu-id="e0ed4-121">riquadro superiore centrale Hello Mostra hello **allo stato di tutti i vertici hello in esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="e0ed4-121">hello top center pane shows hello **running status of all hello vertices**.</span></span>
  
![Visualizzazione esecuzioni vertici di Data Lake Analytics Tools](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane3.png)

<span data-ttu-id="e0ed4-123">riquadro centrale inferiore di Hello Mostra informazioni su ogni vertice:</span><span class="sxs-lookup"><span data-stu-id="e0ed4-123">hello bottom center pane shows information about each vertex:</span></span>
* <span data-ttu-id="e0ed4-124">Nome processo: hello Nome istanza vertice hello.</span><span class="sxs-lookup"><span data-stu-id="e0ed4-124">Process Name: hello name of hello vertex instance.</span></span> <span data-ttu-id="e0ed4-125">costituito da parti differenti in NomeFase | NomeVertice | IstanzaEsecuzioneVertice.</span><span class="sxs-lookup"><span data-stu-id="e0ed4-125">It is composed of different parts in StageName|VertexName|VertexRunInstance.</span></span> <span data-ttu-id="e0ed4-126">Ad esempio, vertice .v1 [62] hello SV7_Split è l'acronimo di hello seconda istanza in esecuzione (.v1, indice, a partire da 0) del numero di vertici 62 nella fase SV7_Split.</span><span class="sxs-lookup"><span data-stu-id="e0ed4-126">For example, hello SV7_Split[62].v1 vertex stands for hello second running instance (.v1, index starting from 0) of Vertex number 62 in Stage SV7_Split.</span></span>
* <span data-ttu-id="e0ed4-127">Totale dei dati in lettura/scrittura: hello dati sono stati letti/scritti da questo vertice.</span><span class="sxs-lookup"><span data-stu-id="e0ed4-127">Total Data Read/Written: hello data was read/written by this vertex.</span></span>
* <span data-ttu-id="e0ed4-128">Stato e lo stato di uscita: hello stato finale quando vertice hello viene terminata.</span><span class="sxs-lookup"><span data-stu-id="e0ed4-128">State/Exit Status: hello final status when hello vertex is ended.</span></span>
* <span data-ttu-id="e0ed4-129">Tipo di errori o codice di uscita: hello quando vertice hello non riuscita.</span><span class="sxs-lookup"><span data-stu-id="e0ed4-129">Exit Code/Failure Type: hello error when hello vertex failed.</span></span>
* <span data-ttu-id="e0ed4-130">Motivo di creazione: Perché vertice hello è stato creato.</span><span class="sxs-lookup"><span data-stu-id="e0ed4-130">Creation Reason: Why hello vertex was created.</span></span>
* <span data-ttu-id="e0ed4-131">Risorsa o il processo latenza latenza/PN coda latenza: hello durata toowait vertice hello per le risorse e dati tooprocess toostay nella coda di hello.</span><span class="sxs-lookup"><span data-stu-id="e0ed4-131">Resource Latency/Process Latency/PN Queue Latency: hello time taken for hello vertex toowait for resources, tooprocess data, and toostay in hello queue.</span></span>
* <span data-ttu-id="e0ed4-132">GUID processo/creatore: GUID per vertice di esecuzione corrente di hello o il relativo autore.</span><span class="sxs-lookup"><span data-stu-id="e0ed4-132">Process/Creator GUID: GUID for hello current running vertex or its creator.</span></span>
* <span data-ttu-id="e0ed4-133">Versione: istanza hello ennesima hello in esecuzione vertice (sistema hello possibile pianificare nuove istanze di un vertice per diversi motivi, ad esempio il failover, calcolano la ridondanza, ecc.)</span><span class="sxs-lookup"><span data-stu-id="e0ed4-133">Version: hello N-th instance of hello running vertex (hello system might schedule new instances of a vertex for many reasons, for example failover, compute redundancy, etc.)</span></span>
* <span data-ttu-id="e0ed4-134">Version Created Time (Data e ora creazione versione).</span><span class="sxs-lookup"><span data-stu-id="e0ed4-134">Version Created Time.</span></span>
* <span data-ttu-id="e0ed4-135">Elaborare crea inizio ora o il processo in coda o il processo ora inizio ora/processo completa tempo: quando il processo di vertex hello avvii la creazione; Quando il processo di vertex hello avvia tooqueue; hello quando l'inizio del processo determinati vertice. Quando hello determinati vertice viene completata.</span><span class="sxs-lookup"><span data-stu-id="e0ed4-135">Process Create Start Time/Process Queued Time/Process Start Time/Process Complete Time: when hello vertex process starts creation; when hello vertex process starts tooqueue; when hello certain vertex process starts; when hello certain vertex is completed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0ed4-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e0ed4-136">Next steps</span></span>
* <span data-ttu-id="e0ed4-137">informazioni di diagnostica toolog, vedere [accesso ai log di diagnostica per Azure Data Lake Analitica](data-lake-analytics-diagnostic-logs.md)</span><span class="sxs-lookup"><span data-stu-id="e0ed4-137">toolog diagnostics information, see [Accessing diagnostics logs for Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md)</span></span>
* <span data-ttu-id="e0ed4-138">toosee una query più complessa, vedere [sito Web di analizzare i log di Azure Data Lake Analitica](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="e0ed4-138">toosee a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="e0ed4-139">vedere i dettagli dei processi, tooview [Browser di processo di utilizzo e visualizzazione dei processi per i processi di Azure Data lake Analitica](data-lake-analytics-data-lake-tools-view-jobs.md)</span><span class="sxs-lookup"><span data-stu-id="e0ed4-139">tooview job details, see [Use Job Browser and Job View for Azure Data lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md)</span></span>
