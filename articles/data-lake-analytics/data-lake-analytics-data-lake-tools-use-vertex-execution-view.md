---
title: Usare la visualizzazione esecuzioni vertici in Azure Data Lake Tools per Visual Studio | Microsoft Docs
description: Informazioni su come usare la visualizzazione esecuzioni vertici per esaminare i processi di Data Lake Analytics.
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
ms.openlocfilehash: b788e7bc8ded86ebd49cc0be73e5b4e1bcbeaba3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-vertex-execution-view-in-data-lake-tools-for-visual-studio"></a><span data-ttu-id="d4c3b-103">Usare la visualizzazione esecuzioni vertici in Azure Data Lake Tools per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d4c3b-103">Use the Vertex Execution View in Data Lake Tools for Visual Studio</span></span>
<span data-ttu-id="d4c3b-104">Informazioni su come usare la visualizzazione esecuzioni vertici per esaminare i processi di Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="d4c3b-104">Learn how to use the Vertex Execution View to exam Data Lake Analytics jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d4c3b-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d4c3b-105">Prerequisites</span></span>

<span data-ttu-id="d4c3b-106">È necessario conoscere i concetti di base dell'uso di Strumenti Data Lake per Visual Studio per sviluppare script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="d4c3b-106">You need basic knowledge of using Data Lake Tools for Visual Studio to develop U-SQL script.</span></span>  <span data-ttu-id="d4c3b-107">Vedere [Esercitazione: Sviluppare script U-SQL tramite Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d4c3b-107">See [Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>

## <a name="open-the-vertex-execution-view"></a><span data-ttu-id="d4c3b-108">Aprire la visualizzazione esecuzioni vertici</span><span class="sxs-lookup"><span data-stu-id="d4c3b-108">Open the Vertex Execution View</span></span>
<span data-ttu-id="d4c3b-109">Aprire un processo U-SQL in Strumenti Data Lake per Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d4c3b-109">Open a U-SQL job in Data Lake Tools for Visual Studio.</span></span> <span data-ttu-id="d4c3b-110">Fare clic su **Vista esecuzione vertici** nell'angolo in basso a sinistra.</span><span class="sxs-lookup"><span data-stu-id="d4c3b-110">Click **Vertex Execution View** in the bottom left corner.</span></span> <span data-ttu-id="d4c3b-111">È possibile che venga chiesto di caricare prima i profili e l'operazione può richiedere alcuni minuti in base alla connettività di rete.</span><span class="sxs-lookup"><span data-stu-id="d4c3b-111">You may be prompted to load profiles first and it can take some time depending on your network connectivity.</span></span>

![Visualizzazione esecuzioni vertici di Data Lake Analytics Tools](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-open-vertex-execution-view.png)

## <a name="understand-vertex-execution-view"></a><span data-ttu-id="d4c3b-113">Informazioni sulla visualizzazione esecuzioni vertici</span><span class="sxs-lookup"><span data-stu-id="d4c3b-113">Understand Vertex Execution View</span></span>
<span data-ttu-id="d4c3b-114">La visualizzazione esecuzioni vertici comprende tre parti:</span><span class="sxs-lookup"><span data-stu-id="d4c3b-114">The Vertex Execution View has three parts:</span></span>

![Visualizzazione esecuzioni vertici di Data Lake Analytics Tools](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view.png)

<span data-ttu-id="d4c3b-116">**Selettore vertice** a sinistra consente di selezionare i vertici in base alle funzionalità, ad esempio i primi 10 dati letti, o di scegliere in base alla fase.</span><span class="sxs-lookup"><span data-stu-id="d4c3b-116">The **Vertex selector** on the left lets you select vertices by features (such as top 10 data read, or choose by stage).</span></span> <span data-ttu-id="d4c3b-117">Uno dei filtri di uso più comune è quello per visualizzare i **vertici sul percorso critico**.</span><span class="sxs-lookup"><span data-stu-id="d4c3b-117">One of the most commonly-used filters is to see the **vertices on critical path**.</span></span> <span data-ttu-id="d4c3b-118">**Percorso critico** è la catena di vertici più lunga di un processo U-SQL.</span><span class="sxs-lookup"><span data-stu-id="d4c3b-118">The **Critical path** is the longest chain of vertices of a U-SQL job.</span></span> <span data-ttu-id="d4c3b-119">Conoscere il percorso critico è utile per ottimizzare i processi controllando il vertice che richiede maggiore tempo.</span><span class="sxs-lookup"><span data-stu-id="d4c3b-119">Understanding the critical path is useful for optimizing your jobs by checking which vertex takes the longest time.</span></span>
  
![Visualizzazione esecuzioni vertici di Data Lake Analytics Tools](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane2.png)

<span data-ttu-id="d4c3b-121">Il riquadro in alto al centro mostra lo **stato di esecuzione di tutti i vertici**.</span><span class="sxs-lookup"><span data-stu-id="d4c3b-121">The top center pane shows the **running status of all the vertices**.</span></span>
  
![Visualizzazione esecuzioni vertici di Data Lake Analytics Tools](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane3.png)

<span data-ttu-id="d4c3b-123">Il riquadro in basso al centro mostra le informazioni su ogni vertice:</span><span class="sxs-lookup"><span data-stu-id="d4c3b-123">The bottom center pane shows information about each vertex:</span></span>
* <span data-ttu-id="d4c3b-124">Process Name (Nome processo): il nome dell'istanza del vertice,</span><span class="sxs-lookup"><span data-stu-id="d4c3b-124">Process Name: The name of the vertex instance.</span></span> <span data-ttu-id="d4c3b-125">costituito da parti differenti in NomeFase | NomeVertice | IstanzaEsecuzioneVertice.</span><span class="sxs-lookup"><span data-stu-id="d4c3b-125">It is composed of different parts in StageName|VertexName|VertexRunInstance.</span></span> <span data-ttu-id="d4c3b-126">Ad esempio, il vertice SV7_Split[62].v1 indica la seconda istanza in esecuzione (.v1, l'indice inizia da 0) del vertice numero 62 nella fase SV7_Split.</span><span class="sxs-lookup"><span data-stu-id="d4c3b-126">For example, the SV7_Split[62].v1 vertex stands for the second running instance (.v1, index starting from 0) of Vertex number 62 in Stage SV7_Split.</span></span>
* <span data-ttu-id="d4c3b-127">Totale dati letti/scritti: i dati letti/scritti da questo vertice.</span><span class="sxs-lookup"><span data-stu-id="d4c3b-127">Total Data Read/Written: The data was read/written by this vertex.</span></span>
* <span data-ttu-id="d4c3b-128">State/Exit Status (Stato/Stato uscita): lo stato finale quando il vertice viene terminato.</span><span class="sxs-lookup"><span data-stu-id="d4c3b-128">State/Exit Status: The final status when the vertex is ended.</span></span>
* <span data-ttu-id="d4c3b-129">Exit Code/Failure Type (Codice uscita/Tipo di errore): l'errore in caso di non riuscita del vertice.</span><span class="sxs-lookup"><span data-stu-id="d4c3b-129">Exit Code/Failure Type: The error when the vertex failed.</span></span>
* <span data-ttu-id="d4c3b-130">Creation Reason (Motivo creazione): il motivo per cui il vertice è stato creato.</span><span class="sxs-lookup"><span data-stu-id="d4c3b-130">Creation Reason: Why the vertex was created.</span></span>
* <span data-ttu-id="d4c3b-131">Resource Latency/Process Latency/PN Queue Latency: (Latenza risorsa/Latenza processo/Latenza coda elaborazione dati): il tempo in cui il vertice rimane di attesa delle risorse, per elaborare i dati e che rimane in coda.</span><span class="sxs-lookup"><span data-stu-id="d4c3b-131">Resource Latency/Process Latency/PN Queue Latency: the time taken for the vertex to wait for resources, to process data, and to stay in the queue.</span></span>
* <span data-ttu-id="d4c3b-132">Process/Creator GUID (GUID processo/creatore): il GUID per il vertice in esecuzione corrente o per il relativo creatore.</span><span class="sxs-lookup"><span data-stu-id="d4c3b-132">Process/Creator GUID: GUID for the current running vertex or its creator.</span></span>
* <span data-ttu-id="d4c3b-133">Version (Versione): il numero di istanza del vertice in esecuzione; il sistema potrebbe pianificare nuove istanze di un vertice per diversi motivi, ad esempio in caso di failover, ridondanza di calcolo e così via.</span><span class="sxs-lookup"><span data-stu-id="d4c3b-133">Version: the N-th instance of the running vertex (the system might schedule new instances of a vertex for many reasons, for example failover, compute redundancy, etc.)</span></span>
* <span data-ttu-id="d4c3b-134">Version Created Time (Data e ora creazione versione).</span><span class="sxs-lookup"><span data-stu-id="d4c3b-134">Version Created Time.</span></span>
* <span data-ttu-id="d4c3b-135">Process Create Start Time/Process Queued Time/Process Start Time/Process Complete Time (Ora inizio creazione processo/Ora inserimento in coda processo/Ora inizio processo/Ora completamento processo): il momento in cui è iniziato il processo di creazione del vertice o di inserimento in coda del vertice, è iniziato o è stato completato il processo del vertice specifico.</span><span class="sxs-lookup"><span data-stu-id="d4c3b-135">Process Create Start Time/Process Queued Time/Process Start Time/Process Complete Time: when the vertex process starts creation; when the vertex process starts to queue; when the certain vertex process starts; when the certain vertex is completed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d4c3b-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d4c3b-136">Next steps</span></span>
* <span data-ttu-id="d4c3b-137">Per registrare informazioni di diagnostica, vedere [Accessing diagnostics logs for Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md)</span><span class="sxs-lookup"><span data-stu-id="d4c3b-137">To log diagnostics information, see [Accessing diagnostics logs for Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md)</span></span>
* <span data-ttu-id="d4c3b-138">Per visualizzare una query più complessa, vedere [Analizzare i log del sito Web mediante Analisi Data Lake di Azure](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="d4c3b-138">To see a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="d4c3b-139">Per visualizzare i dettagli del processo, vedere [Usare Job Browser e Job View (Visualizzazione processo) per i processi di Azure Data Lake Analytics](data-lake-analytics-data-lake-tools-view-jobs.md)</span><span class="sxs-lookup"><span data-stu-id="d4c3b-139">To view job details, see [Use Job Browser and Job View for Azure Data lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md)</span></span>
