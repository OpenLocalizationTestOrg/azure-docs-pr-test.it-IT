---
title: Eseguire il debug delle query di Analisi di flusso di Azure mediante SELECT INTO | Documentazione Microsoft
description: Campionare i dati intermedi di una query mediante istruzioni SELECT INTO in Analisi di flusso
keywords: 
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9952e2cf-b335-4a5c-8f45-8d3e1eda2e20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: b05222c6d6f4fc2c5b847dd75ff7e29352cd538c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="debug-queries-by-using-select-into-statements"></a><span data-ttu-id="c5e7b-103">Eseguire il debug delle query mediante istruzioni SELECT INTO</span><span class="sxs-lookup"><span data-stu-id="c5e7b-103">Debug queries by using SELECT INTO statements</span></span>

<span data-ttu-id="c5e7b-104">Nell'elaborazione dei dati in tempo reale può essere utile conoscere l'aspetto dei dati nel mezzo di una query.</span><span class="sxs-lookup"><span data-stu-id="c5e7b-104">In real-time data processing, knowing what the data looks like in the middle of the query can be helpful.</span></span> <span data-ttu-id="c5e7b-105">Poiché gli input o i passaggi di un processo di Analisi di flusso di Azure possono essere letti più volte, è possibile scrivere istruzioni SELECT INTO aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="c5e7b-105">Because inputs or steps of an Azure Stream Analytics job can be read multiple times, you can write extra SELECT INTO statements.</span></span> <span data-ttu-id="c5e7b-106">In questo modo vengono generati dati intermedi nella risorsa di archiviazione che consentono di controllare la correttezza dei dati, esattamente come fanno le *variabili di controllo* quando si esegue il debug di un programma.</span><span class="sxs-lookup"><span data-stu-id="c5e7b-106">Doing so outputs intermediate data into storage and lets you inspect the correctness of the data, just as *watch variables* do when you debug a program.</span></span>

## <a name="use-select-into-to-check-the-data-stream"></a><span data-ttu-id="c5e7b-107">Usare SELECT INTO per controllare il flusso dei dati</span><span class="sxs-lookup"><span data-stu-id="c5e7b-107">Use SELECT INTO to check the data stream</span></span>

<span data-ttu-id="c5e7b-108">La seguente query di esempio in un processo di Analisi di flusso di Azure ha un input di flusso, due input di dati di riferimento e un output in Archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="c5e7b-108">The following example query in an Azure Stream Analytics job has one stream input, two reference data inputs, and an output to Azure Table Storage.</span></span> <span data-ttu-id="c5e7b-109">La query unisce i dati dell'hub eventi e di due BLOB di riferimento per ottenere le informazioni di nome e categoria:</span><span class="sxs-lookup"><span data-stu-id="c5e7b-109">The query joins data from the event hub and two reference blobs to get the name and category information:</span></span>

![Esempio di query SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-query1.png)

<span data-ttu-id="c5e7b-111">Si noti che il processo è in esecuzione ma non vengono generati eventi nell'output.</span><span class="sxs-lookup"><span data-stu-id="c5e7b-111">Note that the job is running, but no events are being produced in the output.</span></span> <span data-ttu-id="c5e7b-112">Nel riquadro **Monitoraggio**, illustrato di seguito, è possibile vedere che l'input produce dati, ma non sa quale passaggio del **JOIN** ha causato l'eliminazione di tutti gli eventi.</span><span class="sxs-lookup"><span data-stu-id="c5e7b-112">On the **Monitoring** tile, shown here, you can see that the input is producing data, but you don’t know which step of the **JOIN** caused all the events to be dropped.</span></span>

![Riquadro Monitoraggio](./media/stream-analytics-select-into/stream-analytics-select-into-monitor.png)
 
<span data-ttu-id="c5e7b-114">In questa situazione è possibile aggiungere alcune istruzioni SELECT INTO aggiuntive per "registrare" i risultati intermedi di JOIN e i dati che vengono letti dall'input.</span><span class="sxs-lookup"><span data-stu-id="c5e7b-114">In this situation, you can add a few extra SELECT INTO statements to “log” the intermediate JOIN results and the data that's read from the input.</span></span>

<span data-ttu-id="c5e7b-115">In questo esempio sono stati aggiunti due nuovi "output temporanei".</span><span class="sxs-lookup"><span data-stu-id="c5e7b-115">In this example, we've added two new “temporary outputs.”</span></span> <span data-ttu-id="c5e7b-116">Può trattarsi di qualsiasi sink desiderato.</span><span class="sxs-lookup"><span data-stu-id="c5e7b-116">They can be any sink you like.</span></span> <span data-ttu-id="c5e7b-117">Qui si usa Archiviazione di Azure come esempio:</span><span class="sxs-lookup"><span data-stu-id="c5e7b-117">Here we use Azure Storage as an example:</span></span>

![Aggiunta di ulteriori istruzioni SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-outputs.png)

<span data-ttu-id="c5e7b-119">È quindi possibile riscrivere la query come segue:</span><span class="sxs-lookup"><span data-stu-id="c5e7b-119">You can then rewrite the query like this:</span></span>

![Query SELECT INTO riscritta](./media/stream-analytics-select-into/stream-analytics-select-into-query2.png)

<span data-ttu-id="c5e7b-121">Ora avviare nuovamente il processo e lasciarlo in esecuzione per alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="c5e7b-121">Now start the job again, and let it run for a few minutes.</span></span> <span data-ttu-id="c5e7b-122">Quindi eseguire una query su temp1 e temp2 con Visual Studio Cloud Explorer per generare le tabelle seguenti:</span><span class="sxs-lookup"><span data-stu-id="c5e7b-122">Then query temp1 and temp2 with Visual Studio Cloud Explorer to produce the following tables:</span></span>

<span data-ttu-id="c5e7b-123">**temp1 table**
![SELECT INTO temp1 table](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-1.png)</span><span class="sxs-lookup"><span data-stu-id="c5e7b-123">**temp1 table**
![SELECT INTO temp1 table](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-1.png)</span></span>

<span data-ttu-id="c5e7b-124">**temp2 table**
![SELECT INTO temp2 table](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-2.png)</span><span class="sxs-lookup"><span data-stu-id="c5e7b-124">**temp2 table**
![SELECT INTO temp2 table](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-2.png)</span></span>

<span data-ttu-id="c5e7b-125">Come si può vedere, temp1 e temp2 hanno entrambe dati e la colonna del nome viene popolata in modo corretto in temp2.</span><span class="sxs-lookup"><span data-stu-id="c5e7b-125">As you can see, temp1 and temp2 both have data, and the name column is populated correctly in temp2.</span></span> <span data-ttu-id="c5e7b-126">Tuttavia, poiché non sono ancora presenti dati nell'output, c'è qualcosa di sbagliato:</span><span class="sxs-lookup"><span data-stu-id="c5e7b-126">However, because there is still no data in output, something is wrong:</span></span>

![Tabella SELECT INTO output1 senza dati](./media/stream-analytics-select-into/stream-analytics-select-into-out-table-1.png)

<span data-ttu-id="c5e7b-128">Tramite il campionamento dei dati, è possibile essere quasi certi che il problema riguardi il secondo JOIN.</span><span class="sxs-lookup"><span data-stu-id="c5e7b-128">By sampling the data, you can be almost certain that the issue is with the second JOIN.</span></span> <span data-ttu-id="c5e7b-129">È possibile scaricare i dati di riferimento dal BLOB e dare un'occhiata:</span><span class="sxs-lookup"><span data-stu-id="c5e7b-129">You can download the reference data from the blob and take a look:</span></span>

![Tabella SELECT INTO riferimento](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-1.png)

<span data-ttu-id="c5e7b-131">Come si può notare, il formato del GUID in questi dati di riferimento è diverso dal formato della colonna [da] di temp2.</span><span class="sxs-lookup"><span data-stu-id="c5e7b-131">As you can see, the format of the GUID in this reference data is different from the format of the [from] column in temp2.</span></span> <span data-ttu-id="c5e7b-132">Ecco perché i dati non arrivavano in output1 come previsto.</span><span class="sxs-lookup"><span data-stu-id="c5e7b-132">That’s why the data didn’t arrive in output1 as expected.</span></span>

<span data-ttu-id="c5e7b-133">È possibile correggere il formato dei dati, caricarlo nel BLOB di riferimento e riprovare:</span><span class="sxs-lookup"><span data-stu-id="c5e7b-133">You can fix the data format, upload it to reference blob, and try again:</span></span>

![Tabella SELECT INTO temporanea](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-2.png)

<span data-ttu-id="c5e7b-135">Questa volta i dati nell'output vengono formattati e popolati come previsto.</span><span class="sxs-lookup"><span data-stu-id="c5e7b-135">This time, the data in the output is formatted and populated as expected.</span></span>

![Tabella SELECT INTO finale](./media/stream-analytics-select-into/stream-analytics-select-into-final-table.png)


## <a name="get-help"></a><span data-ttu-id="c5e7b-137">Ottenere aiuto</span><span class="sxs-lookup"><span data-stu-id="c5e7b-137">Get help</span></span>

<span data-ttu-id="c5e7b-138">Per ulteriore assistenza, provare il [Forum di Analisi dei flussi di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="c5e7b-138">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c5e7b-139">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c5e7b-139">Next steps</span></span>

* [<span data-ttu-id="c5e7b-140">Introduzione ad Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="c5e7b-140">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="c5e7b-141">Introduzione all'uso di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="c5e7b-141">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="c5e7b-142">Ridimensionare i processi di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="c5e7b-142">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="c5e7b-143">Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="c5e7b-143">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="c5e7b-144">Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="c5e7b-144">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

