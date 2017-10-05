---
title: 'Piattaforme di analisi: confronto tra Apache Storm e Analisi di flusso | Microsoft Docs'
description: "Informazioni utili per scegliere una piattaforma di analisi cloud tramite confronto tra Apache Storm e Analisi di flusso. Comprendere le funzionalità e le differenze."
keywords: piattaforma di analisi, piattaforme di analisi, piattaforma di analisi cloud, confronto con Storm
services: stream-analytics
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: b9aac017-9866-4d0a-b98f-6f03881e9339
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/27/2017
ms.author: samacha
ms.openlocfilehash: 97044cb5d7b0b3fcb3b85328df618a265bc59b61
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="choosing-a-streaming-analytics-platform-comparing-apache-storm-and-azure-stream-analytics"></a><span data-ttu-id="7300a-105">Scegliere una piattaforma di analisi di flusso: confronto tra Apache Storm e Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="7300a-105">Choosing a streaming analytics platform: comparing Apache Storm and Azure Stream Analytics</span></span>
<span data-ttu-id="7300a-106">Azure offre diverse soluzioni per l'analisi dei flussi di dati: [Analisi di flusso di Azure](https://docs.microsoft.com/azure/stream-analytics/) e [Apache Storm in Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-storm/).</span><span class="sxs-lookup"><span data-stu-id="7300a-106">Azure provides multiple solutions for analyzing streaming data: [Azure Streaming Analytics](https://docs.microsoft.com/azure/stream-analytics/) and [Apache Storm on Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-storm/).</span></span> <span data-ttu-id="7300a-107">Entrambe le piattaforme di analisi offrono i vantaggi di una soluzione PaaS.</span><span class="sxs-lookup"><span data-stu-id="7300a-107">Both analytics platforms provide the benefits of a PaaS solution.</span></span> <span data-ttu-id="7300a-108">Tuttavia, le piattaforme presentano differenze significative nelle loro funzionalità, nonché nel modo in cui vengono configurate e gestite.</span><span class="sxs-lookup"><span data-stu-id="7300a-108">But the platforms have some significant differences in their capabilities as well as in how you configure and manage them.</span></span> 

<span data-ttu-id="7300a-109">Questo articolo fornisce un confronto delle funzionalità che consente di scegliere tra Apache Storm e Analisi di flusso di Azure come piattaforma di analisi cloud.</span><span class="sxs-lookup"><span data-stu-id="7300a-109">This article provides a side-by-side comparison of features to help you choose between Apache Storm and Azure Stream Analytics as a cloud analytics platform.</span></span> 

## <a name="general-features"></a><span data-ttu-id="7300a-110">Funzionalità generali</span><span class="sxs-lookup"><span data-stu-id="7300a-110">General features</span></span>

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7300a-111">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="7300a-111">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="7300a-112">
                    <strong>Analisi di flusso di Azure</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7300a-112">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="7300a-113">
                    <strong>Apache Storm in HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7300a-113">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7300a-114">
                    <strong>Open source?</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7300a-114">
                    <strong>Open source?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="7300a-115">No.</span><span class="sxs-lookup"><span data-stu-id="7300a-115">No.</span></span> <span data-ttu-id="7300a-116">Analisi di flusso di Azure è un'offerta proprietaria Microsoft.</span><span class="sxs-lookup"><span data-stu-id="7300a-116">Azure Stream Analytics is a Microsoft proprietary offering.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="7300a-117">Sì.</span><span class="sxs-lookup"><span data-stu-id="7300a-117">Yes.</span></span> <span data-ttu-id="7300a-118">Apache Storm è una tecnologia concessa in licenza da Apache.</span><span class="sxs-lookup"><span data-stu-id="7300a-118">Apache Storm is an Apache licensed technology.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7300a-119">
                    <strong>Supporto tecnico Microsoft?</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7300a-119">
                    <strong>Microsoft support?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="7300a-120">Sì</span><span class="sxs-lookup"><span data-stu-id="7300a-120">Yes</span></span> </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="7300a-121">Sì</span><span class="sxs-lookup"><span data-stu-id="7300a-121">Yes</span></span> </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7300a-122">
                    <strong>Requisiti hardware</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7300a-122">
                    <strong>Hardware requirements</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="7300a-123">Nessuno.</span><span class="sxs-lookup"><span data-stu-id="7300a-123">None.</span></span> <span data-ttu-id="7300a-124">Analisi di flusso di Azure è un servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="7300a-124">Azure Stream Analytics is an Azure Service.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="7300a-125">Nessuno.</span><span class="sxs-lookup"><span data-stu-id="7300a-125">None.</span></span> <span data-ttu-id="7300a-126">Apache Storm è un servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="7300a-126">Apache Storm is an Azure Service.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7300a-127">
                    <strong>Unità di livello superiore</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7300a-127">
                    <strong>Top-level unit</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="7300a-128">Gli utenti distribuiscono e monitorano i processi di streaming.</span><span class="sxs-lookup"><span data-stu-id="7300a-128">Users deploy and monitor streaming jobs.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="7300a-129">Gli utenti distribuiscono e monitorano un intero cluster, che può ospitare più processi di Storm nonché altri carichi di lavoro (incluso il batch).</span><span class="sxs-lookup"><span data-stu-id="7300a-129">Users deploy and monitor a whole cluster, which can host multiple Storm jobs as well as other workloads (including batch).</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7300a-130">
                    <strong>Prezzi</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7300a-130">
                    <strong>Pricing</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="7300a-131">Il prezzo viene determinato dal volume dei dati elaborati e dal numero di unità di streaming necessarie per ogni ora di esecuzione del processo.</span><span class="sxs-lookup"><span data-stu-id="7300a-131">Priced by volume of data processed and the number of streaming units required per hour that the job is running.</span></span> 
                </p>
                    <p><span data-ttu-id="7300a-132">Per altre informazioni, vedere <a href="http://azure.microsoft.com/pricing/details/stream-analytics/">Prezzi di Analisi di flusso</a>.</span><span class="sxs-lookup"><span data-stu-id="7300a-132">For more information, see <a href="http://azure.microsoft.com/pricing/details/stream-analytics/">Stream Analytics Pricing</a>.</span></span></p>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="7300a-133">L'unità di acquisto è basata su cluster e l'addebito avviene in base al tempo di esecuzione del cluster, indipendentemente dai processi distribuiti.</span><span class="sxs-lookup"><span data-stu-id="7300a-133">The unit of purchase is cluster-based, and is charged based on the time the cluster is running, independent of jobs deployed.</span></span>
                </p>
                <p>
<span data-ttu-id="7300a-134">Per altre informazioni, vedere <a href="http://azure.microsoft.com/pricing/details/hdinsight/">Prezzi di HDInsight</a>.</span><span class="sxs-lookup"><span data-stu-id="7300a-134">For more information, see <a href="http://azure.microsoft.com/pricing/details/hdinsight/">HDInsight pricing</a>.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="authoring"></a><span data-ttu-id="7300a-135">Creazione</span><span class="sxs-lookup"><span data-stu-id="7300a-135">Authoring</span></span>

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7300a-136">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="7300a-136">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="7300a-137">
                    <strong>Analisi di flusso di Azure</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7300a-137">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="7300a-138">
                    <strong>Apache Storm in HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7300a-138">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7300a-139">
                    <strong>Funzionalità: DSL SQL?</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7300a-139">
                    <strong>Capabilities: SQL DSL?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="7300a-140">Sì.</span><span class="sxs-lookup"><span data-stu-id="7300a-140">Yes.</span></span> <span data-ttu-id="7300a-141">Analisi di flusso di Azure fornisce un linguaggio simile a SQL per la creazione di trasformazioni.</span><span class="sxs-lookup"><span data-stu-id="7300a-141">Stream Analytics provides a SQL-like language for creating transformations.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="7300a-142">No.</span><span class="sxs-lookup"><span data-stu-id="7300a-142">No.</span></span> <span data-ttu-id="7300a-143">Gli utenti devono scrivere il codice in Java o C# o usare le API Trident.</span><span class="sxs-lookup"><span data-stu-id="7300a-143">Users write code in Java or C#, or use Trident APIs.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7300a-144">
                    <strong>Funzionalità: operatori temporali?</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7300a-144">
                    <strong>Capabilities: Temporal operators?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="7300a-145">Per impostazione predefinita sono supportati i join temporali e le aggregazioni finestra.</span><span class="sxs-lookup"><span data-stu-id="7300a-145">Windowed aggregates and temporal joins are supported by default.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="7300a-146">Gli operatori temporali devono essere implementati dall'utente.</span><span class="sxs-lookup"><span data-stu-id="7300a-146">Temporal operators must be implemented by the user.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7300a-147">
                    <strong>Esperienza di sviluppo</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7300a-147">
                    <strong>Development experience</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="7300a-148">Gli utenti possono creare, eseguire il debug e monitorare i processi tramite il portale di Azure usando i dati di esempio derivati da Live Stream.</span><span class="sxs-lookup"><span data-stu-id="7300a-148">Users can create, debug, and monitor jobs through the Azure portal, using sample data derived from a live stream.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="7300a-149">Gli utenti che utilizzano .NET possono sviluppare, eseguire il debug e monitorare tramite Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7300a-149">Users using .NET can develop, debug, and monitor through Visual Studio.</span></span> <span data-ttu-id="7300a-150">Gli utenti che utilizzano Java o altri linguaggi possono usare l'IDE preferito.</span><span class="sxs-lookup"><span data-stu-id="7300a-150">Users using Java or other languages can use the IDE of their choice.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7300a-151">
                    <strong>Supporto per il debug</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7300a-151">
                    <strong>Debugging support</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="7300a-152">Lo stato dei processi di base e i log delle operazioni sono disponibili per facilitare il debug.</span><span class="sxs-lookup"><span data-stu-id="7300a-152">Basic job status and operations logs are available to help debug.</span></span> <span data-ttu-id="7300a-153">Analisi di flusso di Azure attualmente non consente agli utenti di specificare il tipo o la quantità di contenuto inclusi nei log (ad esempio, la modalità dettagliata).</span><span class="sxs-lookup"><span data-stu-id="7300a-153">Stream Analytics currently does not let users specify what content or how much content is included in the logs (i.e., verbose mode).</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="7300a-154">Sono disponibili log dettagliati.</span><span class="sxs-lookup"><span data-stu-id="7300a-154">Detailed logs are available.</span></span> <span data-ttu-id="7300a-155">Gli utenti possono accedere ai log in Visual Studio o accedendo al cluster e accedendo direttamente ai log.</span><span class="sxs-lookup"><span data-stu-id="7300a-155">Users can access logs in Visual Studio or by logging in to the cluster and accessing the logs directly.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7300a-156">
                    <strong>Estensibilità tramite codice personalizzato?</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7300a-156">
                    <strong>Extensibility using custom code?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="7300a-157">Supporto parziale con UDF JavaScript.</span><span class="sxs-lookup"><span data-stu-id="7300a-157">Partially support with JavaScript UDFs.</span></span> <span data-ttu-id="7300a-158">Per ulteriori informazioni, vedere <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-javascript-user-defined-functions">Integrazione UDF di JavaScript</a>.</span><span class="sxs-lookup"><span data-stu-id="7300a-158">For more information, see <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-javascript-user-defined-functions">JavaScript UDF integration</a>.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="7300a-159">Sì.</span><span class="sxs-lookup"><span data-stu-id="7300a-159">Yes.</span></span> <span data-ttu-id="7300a-160">Gli utenti possono scrivere codice personalizzato in C#, Java o qualsiasi altro linguaggio supportato in Storm.</span><span class="sxs-lookup"><span data-stu-id="7300a-160">Users can write custom code in C#, Java, or any other language supported on Storm.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="data-sources-inputs-and-outputs"></a><span data-ttu-id="7300a-161">Origini dati (input) e output</span><span class="sxs-lookup"><span data-stu-id="7300a-161">Data sources (inputs) and outputs</span></span> ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7300a-162">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="7300a-162">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="7300a-163">
                    <strong>Analisi di flusso di Azure</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7300a-163">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="7300a-164">
                    <strong>Apache Storm in HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7300a-164">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7300a-165">
                 <strong>Origini dati di input</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7300a-165">
                 <strong>Input data sources</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="7300a-166">Hub eventi di Azure e Archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="7300a-166">Azure Event Hubs and Azure Blob storage.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="7300a-167">I connettori sono disponibili per l'Hub eventi di Azure, Bus di servizio di Microsoft Azure, Kafka e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="7300a-167">Connectors are available for Azure Event Hubs, Azure Service Bus, Kafka, and more.</span></span> <span data-ttu-id="7300a-168">Gli utenti possono creare connettori aggiuntivi con codice personalizzato.</span><span class="sxs-lookup"><span data-stu-id="7300a-168">Users can create additional connectors using custom code.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7300a-169">
                    <strong>Formati di dati di input</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7300a-169">
                    <strong>Input data formats</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="7300a-170">Avro, JSON, CSV</span><span class="sxs-lookup"><span data-stu-id="7300a-170">Avro, JSON, CSV</span></span> </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="7300a-171">Gli utenti possono implementare tutti i formati utilizzando codice personalizzato.</span><span class="sxs-lookup"><span data-stu-id="7300a-171">Users can implement any format using custom code.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7300a-172">
                    <strong>Output</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7300a-172">
                    <strong>Outputs</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="7300a-173">Un processo di streaming può avere più output.</span><span class="sxs-lookup"><span data-stu-id="7300a-173">A streaming job can have multiple outputs.</span></span> <span data-ttu-id="7300a-174">Output supportati: Hub eventi di Azure, Archiviazione BLOB di Azure, Archiviazione tabelle di Azure, Azure SQL DB e Power BI.</span><span class="sxs-lookup"><span data-stu-id="7300a-174">Supported outputs are Azure Event Hubs, Azure Blob storage, Azure Table storage, Azure SQL DB, and Power BI.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="7300a-175">Storm supporta più output in una topologia e ogni output può avere una logica personalizzata per l'elaborazione downstream.</span><span class="sxs-lookup"><span data-stu-id="7300a-175">Storm supports many outputs in a topology, and each output can have custom logic for downstream processing.</span></span> <span data-ttu-id="7300a-176">Storm include connettori predefiniti per Power BI, Hub eventi di Azure, Archiviazione BLOB di Azure, Azure Cosmos DB, SQL e HBase.</span><span class="sxs-lookup"><span data-stu-id="7300a-176">Storm includes connectors for Power BI, Azure Event Hubs, Azure Blob storage, Azure Cosmos DB, SQL, and HBase.</span></span> <span data-ttu-id="7300a-177">Gli utenti possono creare connettori aggiuntivi con codice personalizzato.</span><span class="sxs-lookup"><span data-stu-id="7300a-177">Users can create additional connectors using custom code.</span></span>    
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7300a-178">
                    <strong>Formati di codifica dei dati</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7300a-178">
                    <strong>Data-encoding formats</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="7300a-179">Dati devono essere formattati usando UTF-8.</span><span class="sxs-lookup"><span data-stu-id="7300a-179">Data must be formatted using UTF-8.</span></span>
                </p>
            </td>   
            <td width="246" valign="top">
                <p>
<span data-ttu-id="7300a-180">Gli utenti possono implementare tutti i formati di codifica dei dati usando codice personalizzato.</span><span class="sxs-lookup"><span data-stu-id="7300a-180">Users can implement any data encoding format using custom code.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="management-and-operations"></a><span data-ttu-id="7300a-181">Gestione e operazioni</span><span class="sxs-lookup"><span data-stu-id="7300a-181">Management and operations</span></span> ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7300a-182">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="7300a-182">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="7300a-183">
                    <strong>Analisi di flusso di Azure</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7300a-183">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="7300a-184">
                    <strong>Apache Storm in HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7300a-184">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7300a-185">
                    <strong>Modello di distribuzione dei processi</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7300a-185">
                    <strong>Job deployment model</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="7300a-186">Portale di Azure, PowerShell e API REST.</span><span class="sxs-lookup"><span data-stu-id="7300a-186">Azure portal, PowerShell, and REST APIs.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="7300a-187">Portale di Azure, PowerShell, Visual Studio e API REST.</span><span class="sxs-lookup"><span data-stu-id="7300a-187">Azure portal, PowerShell, Visual Studio, and REST APIs.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7300a-188">
                    <strong>Monitoraggio (statistiche, contatori e così via)</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7300a-188">
                    <strong>Monitoring (stats, counters, etc.)</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="7300a-189">Il monitoraggio viene implementato tramite il portale di Azure e le API REST.</span><span class="sxs-lookup"><span data-stu-id="7300a-189">Monitoring is implemented using Azure portal and REST APIs.</span></span> <span data-ttu-id="7300a-190">Gli utenti possono inoltre configurare gli avvisi di Azure.</span><span class="sxs-lookup"><span data-stu-id="7300a-190">Users can also configure Azure alerts.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="7300a-191">Il monitoraggio viene implementato tramite l'interfaccia utente di Storm e le API REST.</span><span class="sxs-lookup"><span data-stu-id="7300a-191">Monitoring is implemented using the Storm UI and REST APIs.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7300a-192">
                    <strong>Scalabilità</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7300a-192">
                    <strong>Scalability</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="7300a-193">La scalabilità è determinata dal numero di unità di streaming (SUs) per ogni processo.</span><span class="sxs-lookup"><span data-stu-id="7300a-193">Scalability is determined by the number of Streaming Units (SUs) for each job.</span></span> <span data-ttu-id="7300a-194">Ogni unità di streaming elabora fino a 1 MB al secondo, con un massimo di 50 unità.</span><span class="sxs-lookup"><span data-stu-id="7300a-194">Each Streaming Unit processes up to 1 MB/second, with a maximum 50 units.</span></span> <span data-ttu-id="7300a-195">Per ulteriori informazioni, vedere <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-jobs">Ridimensionare i processi di Analisi di flusso di Azure per aumentare la velocità effettiva dell'elaborazione dei flussi di dati</a>.</span><span class="sxs-lookup"><span data-stu-id="7300a-195">For more information, see <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-jobs">Scale to increase throughput</a>.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="7300a-196">La scalabilità è determinata dal numero di nodi del cluster HDInsight Storm.</span><span class="sxs-lookup"><span data-stu-id="7300a-196">Scalability is determined by the number of nodes in the HDInsight Storm cluster.</span></span> <span data-ttu-id="7300a-197">Il limite superiore al numero di nodi è definito dalla quota di Azure dell'utente.</span><span class="sxs-lookup"><span data-stu-id="7300a-197">The top limit on the number of nodes is defined by the user's Azure quota.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7300a-198">
                    <strong>Limiti di elaborazione dei dati</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7300a-198">
                    <strong>Data processing limits</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="7300a-199">Gli utenti possono aumentare l'elaborazione dati o ottimizzare i costi aumentando o diminuendo il numero di unità di streaming, con un limite superiore di 1 GB al secondo.</span><span class="sxs-lookup"><span data-stu-id="7300a-199">Users can increase data processing or optimize costs by increasing or decreasing the number of Streaming Units, with an upper limit of 1 GB/second.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="7300a-200">Gli utenti possono scalare le dimensioni cluster per aumentarle o diminuirle.</span><span class="sxs-lookup"><span data-stu-id="7300a-200">Users can scale cluster size up or down.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7300a-201">
                    <strong>Arresto/ripresa</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7300a-201">
                    <strong>Stop/Resume</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="7300a-202">Arrestare e riprendere dall'ultimo punto di arresto.</span><span class="sxs-lookup"><span data-stu-id="7300a-202">Stop and resume from last place stopped.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="7300a-203">Arrestare e riprendere dall'ultimo punto di arresto in base al limite.</span><span class="sxs-lookup"><span data-stu-id="7300a-203">Stop and resume from last place stopped based on a watermark.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7300a-204">
                    <strong>Aggiornamento del servizio e del framework</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7300a-204">
                    <strong>Service and framework update</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="7300a-205">Applicazione di patch automatica senza tempi di inattività.</span><span class="sxs-lookup"><span data-stu-id="7300a-205">Automatic patching with no downtime.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="7300a-206">Applicazione di patch automatica senza tempi di inattività.</span><span class="sxs-lookup"><span data-stu-id="7300a-206">Automatic patching with no downtime.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7300a-207">
                    <strong>Continuità aziendale grazie a un servizio a disponibilità elevata con contratti di servizio garantiti</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7300a-207">
                    <strong>Business continuity through a Highly Available Service with guaranteed SLAs</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <ul>
                <li><span data-ttu-id="7300a-208">Tempo di attività per il contratto di servizio del 99,9%</span><span class="sxs-lookup"><span data-stu-id="7300a-208">SLA of 99.9% uptime</span></span></li>
                <li><span data-ttu-id="7300a-209">Ripristino automatico in caso di errori</span><span class="sxs-lookup"><span data-stu-id="7300a-209">Auto-recovery from failures</span></span></li>
                <li><span data-ttu-id="7300a-210">Ripristino predefinito degli operatori temporali con stato</span><span class="sxs-lookup"><span data-stu-id="7300a-210">Built-in recovery of stateful temporal operators</span></span></li>
                </ul>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="7300a-211">Tempo di attività per il contratto di servizio del 99,9% del cluster Storm.</span><span class="sxs-lookup"><span data-stu-id="7300a-211">SLA of 99.9% uptime of the Storm cluster.</span></span> 
                </p>
                <p>
<span data-ttu-id="7300a-212">Apache Storm è una piattaforma di streaming a tolleranza di errore.</span><span class="sxs-lookup"><span data-stu-id="7300a-212">Apache Storm is a fault-tolerant streaming platform.</span></span> <span data-ttu-id="7300a-213">Tuttavia, è responsabilità dell'utente assicurare che i processi di streaming vengano eseguiti senza interruzioni.</span><span class="sxs-lookup"><span data-stu-id="7300a-213">However, it is the user's responsibility to ensure that streaming jobs run uninterrupted.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="advanced-features"></a><span data-ttu-id="7300a-214">Funzionalità avanzate</span><span class="sxs-lookup"><span data-stu-id="7300a-214">Advanced features</span></span> ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7300a-215">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="7300a-215">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="7300a-216">
                    <strong>Analisi di flusso di Azure</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7300a-216">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="7300a-217">
                    <strong>Apache Storm in HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7300a-217">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7300a-218">
                    <strong>Gestione di eventi di arrivo in ritardo e con ordine non corretto</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7300a-218">
                    <strong>Late arrival and out-of-order event handling</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="7300a-219">Criteri configurabili predefiniti per riordinare e rilasciare gli eventi o modificare l'ora degli eventi.</span><span class="sxs-lookup"><span data-stu-id="7300a-219">Built-in configurable policies can reorder events, drop events, or adjust event time.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="7300a-220">Gli utenti devono deve implementare la logica per gestire questo scenario.</span><span class="sxs-lookup"><span data-stu-id="7300a-220">Users must implement logic to handle this scenario.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7300a-221">
                    <strong>Dati di riferimento</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7300a-221">
                    <strong>Reference data</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="7300a-222">Dati di riferimento sono disponibili dall'archiviazione BLOB di Azure con un massimo di 100 MB di cache in memoria.</span><span class="sxs-lookup"><span data-stu-id="7300a-222">Reference data is available from Azure Blob storage with a maximum of 100 MB of in-memory cache.</span></span> <span data-ttu-id="7300a-223">I dati di riferimento vengono aggiornati dal servizio.</span><span class="sxs-lookup"><span data-stu-id="7300a-223">Reference data is refreshed by the service.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="7300a-224">Nessun limite alle dimensioni dei dati.</span><span class="sxs-lookup"><span data-stu-id="7300a-224">No limits on data size.</span></span> <span data-ttu-id="7300a-225">I connettori sono disponibili per HBase, Azure Cosmos DB, SQL Server e Azure.</span><span class="sxs-lookup"><span data-stu-id="7300a-225">Connectors are available for HBase, Azure Cosmos DB, SQL Server, and Azure.</span></span> <span data-ttu-id="7300a-226">Gli utenti possono creare connettori aggiuntivi con codice personalizzato.</span><span class="sxs-lookup"><span data-stu-id="7300a-226">Users can create additional connectors using custom code.</span></span> <span data-ttu-id="7300a-227">I dati di riferimento devono essere aggiornati con un codice personalizzato.</span><span class="sxs-lookup"><span data-stu-id="7300a-227">Reference data must be refreshed using custom code.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7300a-228">
                    <strong>Integrazione con Machine Learning</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7300a-228">
                    <strong>Integration with Machine Learning</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="7300a-229">I modelli di Azure Machine Learning pubblicati possono essere configurati come funzioni durante la creazione dei processi.</span><span class="sxs-lookup"><span data-stu-id="7300a-229">Published Azure Machine Learning models can be configured as functions during job creation.</span></span> <span data-ttu-id="7300a-230">Per altre informazioni, vedere <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-with-machine-learning-functions">Scalabilità per le funzioni di Machine Learning</a>.</span><span class="sxs-lookup"><span data-stu-id="7300a-230">For more information, see <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-with-machine-learning-functions">Scale for Machine Learning functions</a>.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="7300a-231">Disponibile tramite i bolt di Storm.</span><span class="sxs-lookup"><span data-stu-id="7300a-231">Available through Storm Bolts.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>
