---
title: esegue una query utilizzando SELECT INTO aaaDebug Analitica di flusso di Azure | Documenti Microsoft
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
ms.openlocfilehash: 27e41af1a6ea06b4509d07a3a67087490d0ec1fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="debug-queries-by-using-select-into-statements"></a><span data-ttu-id="f5186-103">Eseguire il debug delle query mediante istruzioni SELECT INTO</span><span class="sxs-lookup"><span data-stu-id="f5186-103">Debug queries by using SELECT INTO statements</span></span>

<span data-ttu-id="f5186-104">Nell'elaborazione di dati in tempo reale, conoscere i dati di hello sembra intermedio hello di hello query può essere utile.</span><span class="sxs-lookup"><span data-stu-id="f5186-104">In real-time data processing, knowing what hello data looks like in hello middle of hello query can be helpful.</span></span> <span data-ttu-id="f5186-105">Poiché gli input o i passaggi di un processo di Analisi di flusso di Azure possono essere letti più volte, è possibile scrivere istruzioni SELECT INTO aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="f5186-105">Because inputs or steps of an Azure Stream Analytics job can be read multiple times, you can write extra SELECT INTO statements.</span></span> <span data-ttu-id="f5186-106">Questa operazione restituisce i dati intermedi nell'account di archiviazione e consente di controllare la correttezza di hello dei dati di hello, proprio come *controllare variabili* eseguire durante il debug di un programma.</span><span class="sxs-lookup"><span data-stu-id="f5186-106">Doing so outputs intermediate data into storage and lets you inspect hello correctness of hello data, just as *watch variables* do when you debug a program.</span></span>

## <a name="use-select-into-toocheck-hello-data-stream"></a><span data-ttu-id="f5186-107">Utilizzare SELECT INTO toocheck hello flusso di dati</span><span class="sxs-lookup"><span data-stu-id="f5186-107">Use SELECT INTO toocheck hello data stream</span></span>

<span data-ttu-id="f5186-108">Hello query di esempio seguente in un processo Analitica di flusso di Azure dispone di input del flusso di uno, due input di dati di riferimento e un tooAzure output archiviazione tabella.</span><span class="sxs-lookup"><span data-stu-id="f5186-108">hello following example query in an Azure Stream Analytics job has one stream input, two reference data inputs, and an output tooAzure Table Storage.</span></span> <span data-ttu-id="f5186-109">query Hello unisce i dati di hub eventi hello e due BLOB tooget hello nome e la categoria di informazioni di riferimento:</span><span class="sxs-lookup"><span data-stu-id="f5186-109">hello query joins data from hello event hub and two reference blobs tooget hello name and category information:</span></span>

![Esempio di query SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-query1.png)

<span data-ttu-id="f5186-111">Si noti che il processo di hello è in esecuzione, ma gli eventi non vengono generati nell'output di hello.</span><span class="sxs-lookup"><span data-stu-id="f5186-111">Note that hello job is running, but no events are being produced in hello output.</span></span> <span data-ttu-id="f5186-112">In hello **monitoraggio** riquadro, riportato di seguito, si noterà che l'input hello produce dati, ma non si conosce il passaggio di hello **JOIN** causato tutti hello toobe eventi eliminati.</span><span class="sxs-lookup"><span data-stu-id="f5186-112">On hello **Monitoring** tile, shown here, you can see that hello input is producing data, but you don’t know which step of hello **JOIN** caused all hello events toobe dropped.</span></span>

![riquadro monitoraggio Hello](./media/stream-analytics-select-into/stream-analytics-select-into-monitor.png)
 
<span data-ttu-id="f5186-114">In questo caso, è possibile aggiungere alcuni aggiuntivo le istruzioni SELECT INTO troppo "accesso" hello intermedia JOIN risultati e i dati di hello che viene letto dall'input hello.</span><span class="sxs-lookup"><span data-stu-id="f5186-114">In this situation, you can add a few extra SELECT INTO statements too“log” hello intermediate JOIN results and hello data that's read from hello input.</span></span>

<span data-ttu-id="f5186-115">In questo esempio sono stati aggiunti due nuovi "output temporanei".</span><span class="sxs-lookup"><span data-stu-id="f5186-115">In this example, we've added two new “temporary outputs.”</span></span> <span data-ttu-id="f5186-116">Può trattarsi di qualsiasi sink desiderato.</span><span class="sxs-lookup"><span data-stu-id="f5186-116">They can be any sink you like.</span></span> <span data-ttu-id="f5186-117">Qui si usa Archiviazione di Azure come esempio:</span><span class="sxs-lookup"><span data-stu-id="f5186-117">Here we use Azure Storage as an example:</span></span>

![Aggiunta di ulteriori istruzioni SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-outputs.png)

<span data-ttu-id="f5186-119">È quindi possibile riscrivere la query hello simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="f5186-119">You can then rewrite hello query like this:</span></span>

![Query SELECT INTO riscritta](./media/stream-analytics-select-into/stream-analytics-select-into-query2.png)

<span data-ttu-id="f5186-121">Ora avviare di nuovo il processo di hello e consentire l'esecuzione per alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="f5186-121">Now start hello job again, and let it run for a few minutes.</span></span> <span data-ttu-id="f5186-122">Quindi eseguire una query temp1 e temp2 con hello tooproduce Visual Studio Cloud Explorer le tabelle seguenti:</span><span class="sxs-lookup"><span data-stu-id="f5186-122">Then query temp1 and temp2 with Visual Studio Cloud Explorer tooproduce hello following tables:</span></span>

<span data-ttu-id="f5186-123">**temp1 table**
![SELECT INTO temp1 table](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-1.png)</span><span class="sxs-lookup"><span data-stu-id="f5186-123">**temp1 table**
![SELECT INTO temp1 table](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-1.png)</span></span>

<span data-ttu-id="f5186-124">**temp2 table**
![SELECT INTO temp2 table](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-2.png)</span><span class="sxs-lookup"><span data-stu-id="f5186-124">**temp2 table**
![SELECT INTO temp2 table](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-2.png)</span></span>

<span data-ttu-id="f5186-125">Come si può notare, temp1 e temp2 dispone di dati e colonna nome hello viene compilato correttamente in temp2.</span><span class="sxs-lookup"><span data-stu-id="f5186-125">As you can see, temp1 and temp2 both have data, and hello name column is populated correctly in temp2.</span></span> <span data-ttu-id="f5186-126">Tuttavia, poiché non sono ancora presenti dati nell'output, c'è qualcosa di sbagliato:</span><span class="sxs-lookup"><span data-stu-id="f5186-126">However, because there is still no data in output, something is wrong:</span></span>

![Tabella SELECT INTO output1 senza dati](./media/stream-analytics-select-into/stream-analytics-select-into-out-table-1.png)

<span data-ttu-id="f5186-128">Tramite il campionamento dei dati di hello, può essere quasi certo che il problema di hello sia con hello secondo JOIN.</span><span class="sxs-lookup"><span data-stu-id="f5186-128">By sampling hello data, you can be almost certain that hello issue is with hello second JOIN.</span></span> <span data-ttu-id="f5186-129">È possibile scaricare i dati di riferimento hello dal blob hello e dare un'occhiata:</span><span class="sxs-lookup"><span data-stu-id="f5186-129">You can download hello reference data from hello blob and take a look:</span></span>

![Tabella SELECT INTO riferimento](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-1.png)

<span data-ttu-id="f5186-131">Come si può notare, il formato di hello di hello GUID in questi dati di riferimento è diverso dal formato hello di hello [colonna temp2 from].</span><span class="sxs-lookup"><span data-stu-id="f5186-131">As you can see, hello format of hello GUID in this reference data is different from hello format of hello [from] column in temp2.</span></span> <span data-ttu-id="f5186-132">Per questa ragione i dati di hello non arrivano in USCITA1 come previsto.</span><span class="sxs-lookup"><span data-stu-id="f5186-132">That’s why hello data didn’t arrive in output1 as expected.</span></span>

<span data-ttu-id="f5186-133">È possibile correggere il formato di dati hello, caricarlo tooreference blob e riprovare:</span><span class="sxs-lookup"><span data-stu-id="f5186-133">You can fix hello data format, upload it tooreference blob, and try again:</span></span>

![Tabella SELECT INTO temporanea](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-2.png)

<span data-ttu-id="f5186-135">Questa volta, dati hello nell'output di hello sono formattati e compilati come previsto.</span><span class="sxs-lookup"><span data-stu-id="f5186-135">This time, hello data in hello output is formatted and populated as expected.</span></span>

![Tabella SELECT INTO finale](./media/stream-analytics-select-into/stream-analytics-select-into-final-table.png)


## <a name="get-help"></a><span data-ttu-id="f5186-137">Ottenere aiuto</span><span class="sxs-lookup"><span data-stu-id="f5186-137">Get help</span></span>

<span data-ttu-id="f5186-138">Per ulteriore assistenza, provare il [Forum di Analisi dei flussi di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="f5186-138">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5186-139">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f5186-139">Next steps</span></span>

* [<span data-ttu-id="f5186-140">Introduzione tooAzure flusso Analitica</span><span class="sxs-lookup"><span data-stu-id="f5186-140">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="f5186-141">Introduzione all'uso di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="f5186-141">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="f5186-142">Ridimensionare i processi di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="f5186-142">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="f5186-143">Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="f5186-143">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="f5186-144">Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="f5186-144">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

