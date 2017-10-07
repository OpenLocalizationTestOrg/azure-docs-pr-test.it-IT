---
title: 'Piattaforme Analitica: Apache Storm confronto tooStream Analitica | Documenti Microsoft'
description: "Scelta di una piattaforma di cloud analitica utilizzando un tooStream confronto Apache Storm Analitica indicazioni. Comprendere le funzionalità e le differenze."
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
ms.openlocfilehash: 5a0ec5b2439596f0da962f04b776472031660062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="choosing-a-streaming-analytics-platform-comparing-apache-storm-and-azure-stream-analytics"></a><span data-ttu-id="edfcb-105">Scegliere una piattaforma di analisi di flusso: confronto tra Apache Storm e Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="edfcb-105">Choosing a streaming analytics platform: comparing Apache Storm and Azure Stream Analytics</span></span>
<span data-ttu-id="edfcb-106">Azure offre diverse soluzioni per l'analisi dei flussi di dati: [Analisi di flusso di Azure](https://docs.microsoft.com/azure/stream-analytics/) e [Apache Storm in Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-storm/).</span><span class="sxs-lookup"><span data-stu-id="edfcb-106">Azure provides multiple solutions for analyzing streaming data: [Azure Streaming Analytics](https://docs.microsoft.com/azure/stream-analytics/) and [Apache Storm on Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-storm/).</span></span> <span data-ttu-id="edfcb-107">Entrambe le piattaforme analitica hello vantaggi di una soluzione PaaS.</span><span class="sxs-lookup"><span data-stu-id="edfcb-107">Both analytics platforms provide hello benefits of a PaaS solution.</span></span> <span data-ttu-id="edfcb-108">Ma piattaforme hello presentano alcune differenze significative anche le funzionalità come illustrato come configurare e gestirli.</span><span class="sxs-lookup"><span data-stu-id="edfcb-108">But hello platforms have some significant differences in their capabilities as well as in how you configure and manage them.</span></span> 

<span data-ttu-id="edfcb-109">Questo articolo fornisce un confronto side-by-side di funzionalità toohelp che si sceglie tra Apache Storm e Analitica di flusso di Azure come piattaforma cloud analitica.</span><span class="sxs-lookup"><span data-stu-id="edfcb-109">This article provides a side-by-side comparison of features toohelp you choose between Apache Storm and Azure Stream Analytics as a cloud analytics platform.</span></span> 

## <a name="general-features"></a><span data-ttu-id="edfcb-110">Funzionalità generali</span><span class="sxs-lookup"><span data-stu-id="edfcb-110">General features</span></span>

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="edfcb-111">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="edfcb-111">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="edfcb-112">
                    <strong>Analisi di flusso di Azure</strong>
                </span><span class="sxs-lookup"><span data-stu-id="edfcb-112">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="edfcb-113">
                    <strong>Apache Storm in HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="edfcb-113">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="edfcb-114">
                    <strong>Open source?</strong>
                </span><span class="sxs-lookup"><span data-stu-id="edfcb-114">
                    <strong>Open source?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="edfcb-115">No.</span><span class="sxs-lookup"><span data-stu-id="edfcb-115">No.</span></span> <span data-ttu-id="edfcb-116">Analisi di flusso di Azure è un'offerta proprietaria Microsoft.</span><span class="sxs-lookup"><span data-stu-id="edfcb-116">Azure Stream Analytics is a Microsoft proprietary offering.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="edfcb-117">Sì.</span><span class="sxs-lookup"><span data-stu-id="edfcb-117">Yes.</span></span> <span data-ttu-id="edfcb-118">Apache Storm è una tecnologia concessa in licenza da Apache.</span><span class="sxs-lookup"><span data-stu-id="edfcb-118">Apache Storm is an Apache licensed technology.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="edfcb-119">
                    <strong>Supporto tecnico Microsoft?</strong>
                </span><span class="sxs-lookup"><span data-stu-id="edfcb-119">
                    <strong>Microsoft support?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="edfcb-120">Sì</span><span class="sxs-lookup"><span data-stu-id="edfcb-120">Yes</span></span> </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="edfcb-121">Sì</span><span class="sxs-lookup"><span data-stu-id="edfcb-121">Yes</span></span> </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="edfcb-122">
                    <strong>Requisiti hardware</strong>
                </span><span class="sxs-lookup"><span data-stu-id="edfcb-122">
                    <strong>Hardware requirements</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="edfcb-123">Nessuno.</span><span class="sxs-lookup"><span data-stu-id="edfcb-123">None.</span></span> <span data-ttu-id="edfcb-124">Analisi di flusso di Azure è un servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="edfcb-124">Azure Stream Analytics is an Azure Service.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="edfcb-125">Nessuno.</span><span class="sxs-lookup"><span data-stu-id="edfcb-125">None.</span></span> <span data-ttu-id="edfcb-126">Apache Storm è un servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="edfcb-126">Apache Storm is an Azure Service.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="edfcb-127">
                    <strong>Unità di livello superiore</strong>
                </span><span class="sxs-lookup"><span data-stu-id="edfcb-127">
                    <strong>Top-level unit</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="edfcb-128">Gli utenti distribuiscono e monitorano i processi di streaming.</span><span class="sxs-lookup"><span data-stu-id="edfcb-128">Users deploy and monitor streaming jobs.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="edfcb-129">Gli utenti distribuiscono e monitorano un intero cluster, che può ospitare più processi di Storm nonché altri carichi di lavoro (incluso il batch).</span><span class="sxs-lookup"><span data-stu-id="edfcb-129">Users deploy and monitor a whole cluster, which can host multiple Storm jobs as well as other workloads (including batch).</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="edfcb-130">
                    <strong>Prezzi</strong>
                </span><span class="sxs-lookup"><span data-stu-id="edfcb-130">
                    <strong>Pricing</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="edfcb-131">Prezzo al volume dei dati elaborati e hello numero di unità di streaming necessarie per ogni ora che hello processo è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="edfcb-131">Priced by volume of data processed and hello number of streaming units required per hour that hello job is running.</span></span> 
                </p>
                    <p><span data-ttu-id="edfcb-132">Per altre informazioni, vedere <a href="http://azure.microsoft.com/pricing/details/stream-analytics/">Prezzi di Analisi di flusso</a>.</span><span class="sxs-lookup"><span data-stu-id="edfcb-132">For more information, see <a href="http://azure.microsoft.com/pricing/details/stream-analytics/">Stream Analytics Pricing</a>.</span></span></p>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="edfcb-133">unità di Hello di acquisto è basata su cluster e viene addebitato in base a ora hello hello cluster è in esecuzione, indipendente da processi di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="edfcb-133">hello unit of purchase is cluster-based, and is charged based on hello time hello cluster is running, independent of jobs deployed.</span></span>
                </p>
                <p>
<span data-ttu-id="edfcb-134">Per altre informazioni, vedere <a href="http://azure.microsoft.com/pricing/details/hdinsight/">Prezzi di HDInsight</a>.</span><span class="sxs-lookup"><span data-stu-id="edfcb-134">For more information, see <a href="http://azure.microsoft.com/pricing/details/hdinsight/">HDInsight pricing</a>.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="authoring"></a><span data-ttu-id="edfcb-135">Creazione</span><span class="sxs-lookup"><span data-stu-id="edfcb-135">Authoring</span></span>

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="edfcb-136">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="edfcb-136">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="edfcb-137">
                    <strong>Analisi di flusso di Azure</strong>
                </span><span class="sxs-lookup"><span data-stu-id="edfcb-137">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="edfcb-138">
                    <strong>Apache Storm in HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="edfcb-138">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="edfcb-139">
                    <strong>Funzionalità: DSL SQL?</strong>
                </span><span class="sxs-lookup"><span data-stu-id="edfcb-139">
                    <strong>Capabilities: SQL DSL?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="edfcb-140">Sì.</span><span class="sxs-lookup"><span data-stu-id="edfcb-140">Yes.</span></span> <span data-ttu-id="edfcb-141">Analisi di flusso di Azure fornisce un linguaggio simile a SQL per la creazione di trasformazioni.</span><span class="sxs-lookup"><span data-stu-id="edfcb-141">Stream Analytics provides a SQL-like language for creating transformations.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="edfcb-142">No.</span><span class="sxs-lookup"><span data-stu-id="edfcb-142">No.</span></span> <span data-ttu-id="edfcb-143">Gli utenti devono scrivere il codice in Java o C# o usare le API Trident.</span><span class="sxs-lookup"><span data-stu-id="edfcb-143">Users write code in Java or C#, or use Trident APIs.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="edfcb-144">
                    <strong>Funzionalità: operatori temporali?</strong>
                </span><span class="sxs-lookup"><span data-stu-id="edfcb-144">
                    <strong>Capabilities: Temporal operators?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="edfcb-145">Per impostazione predefinita sono supportati i join temporali e le aggregazioni finestra.</span><span class="sxs-lookup"><span data-stu-id="edfcb-145">Windowed aggregates and temporal joins are supported by default.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="edfcb-146">Gli operatori temporali devono essere implementati da utente hello.</span><span class="sxs-lookup"><span data-stu-id="edfcb-146">Temporal operators must be implemented by hello user.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="edfcb-147">
                    <strong>Esperienza di sviluppo</strong>
                </span><span class="sxs-lookup"><span data-stu-id="edfcb-147">
                    <strong>Development experience</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="edfcb-148">Gli utenti possono creare, eseguire il debug e monitorare i processi tramite il portale di Azure, hello utilizzando dati di esempio derivati da un flusso in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="edfcb-148">Users can create, debug, and monitor jobs through hello Azure portal, using sample data derived from a live stream.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="edfcb-149">Gli utenti che utilizzano .NET possono sviluppare, eseguire il debug e monitorare tramite Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="edfcb-149">Users using .NET can develop, debug, and monitor through Visual Studio.</span></span> <span data-ttu-id="edfcb-150">Gli utenti utilizzando Java o in altri linguaggi possono utilizzare hello IDE di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="edfcb-150">Users using Java or other languages can use hello IDE of their choice.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="edfcb-151">
                    <strong>Supporto per il debug</strong>
                </span><span class="sxs-lookup"><span data-stu-id="edfcb-151">
                    <strong>Debugging support</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="edfcb-152">I registri di stato e le operazioni di processo di base sono disponibili toohelp debug.</span><span class="sxs-lookup"><span data-stu-id="edfcb-152">Basic job status and operations logs are available toohelp debug.</span></span> <span data-ttu-id="edfcb-153">Flusso Analitica attualmente non consentire agli utenti di specificare il tipo di contenuto o la quantità di contenuto è incluso nei registri hello (ad esempio, la modalità dettagliata).</span><span class="sxs-lookup"><span data-stu-id="edfcb-153">Stream Analytics currently does not let users specify what content or how much content is included in hello logs (i.e., verbose mode).</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="edfcb-154">Sono disponibili log dettagliati.</span><span class="sxs-lookup"><span data-stu-id="edfcb-154">Detailed logs are available.</span></span> <span data-ttu-id="edfcb-155">Gli utenti possono accedere i log in Visual Studio o dal cluster toohello accesso a registri hello direttamente.</span><span class="sxs-lookup"><span data-stu-id="edfcb-155">Users can access logs in Visual Studio or by logging in toohello cluster and accessing hello logs directly.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="edfcb-156">
                    <strong>Estensibilità tramite codice personalizzato?</strong>
                </span><span class="sxs-lookup"><span data-stu-id="edfcb-156">
                    <strong>Extensibility using custom code?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="edfcb-157">Supporto parziale con UDF JavaScript.</span><span class="sxs-lookup"><span data-stu-id="edfcb-157">Partially support with JavaScript UDFs.</span></span> <span data-ttu-id="edfcb-158">Per ulteriori informazioni, vedere <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-javascript-user-defined-functions">Integrazione UDF di JavaScript</a>.</span><span class="sxs-lookup"><span data-stu-id="edfcb-158">For more information, see <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-javascript-user-defined-functions">JavaScript UDF integration</a>.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="edfcb-159">Sì.</span><span class="sxs-lookup"><span data-stu-id="edfcb-159">Yes.</span></span> <span data-ttu-id="edfcb-160">Gli utenti possono scrivere codice personalizzato in C#, Java o qualsiasi altro linguaggio supportato in Storm.</span><span class="sxs-lookup"><span data-stu-id="edfcb-160">Users can write custom code in C#, Java, or any other language supported on Storm.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="data-sources-inputs-and-outputs"></a><span data-ttu-id="edfcb-161">Origini dati (input) e output</span><span class="sxs-lookup"><span data-stu-id="edfcb-161">Data sources (inputs) and outputs</span></span> ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="edfcb-162">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="edfcb-162">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="edfcb-163">
                    <strong>Analisi di flusso di Azure</strong>
                </span><span class="sxs-lookup"><span data-stu-id="edfcb-163">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="edfcb-164">
                    <strong>Apache Storm in HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="edfcb-164">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="edfcb-165">
                 <strong>Origini dati di input</strong>
                </span><span class="sxs-lookup"><span data-stu-id="edfcb-165">
                 <strong>Input data sources</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="edfcb-166">Hub eventi di Azure e Archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="edfcb-166">Azure Event Hubs and Azure Blob storage.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="edfcb-167">I connettori sono disponibili per l'Hub eventi di Azure, Bus di servizio di Microsoft Azure, Kafka e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="edfcb-167">Connectors are available for Azure Event Hubs, Azure Service Bus, Kafka, and more.</span></span> <span data-ttu-id="edfcb-168">Gli utenti possono creare connettori aggiuntivi con codice personalizzato.</span><span class="sxs-lookup"><span data-stu-id="edfcb-168">Users can create additional connectors using custom code.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="edfcb-169">
                    <strong>Formati di dati di input</strong>
                </span><span class="sxs-lookup"><span data-stu-id="edfcb-169">
                    <strong>Input data formats</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="edfcb-170">Avro, JSON, CSV</span><span class="sxs-lookup"><span data-stu-id="edfcb-170">Avro, JSON, CSV</span></span> </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="edfcb-171">Gli utenti possono implementare tutti i formati utilizzando codice personalizzato.</span><span class="sxs-lookup"><span data-stu-id="edfcb-171">Users can implement any format using custom code.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="edfcb-172">
                    <strong>Output</strong>
                </span><span class="sxs-lookup"><span data-stu-id="edfcb-172">
                    <strong>Outputs</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="edfcb-173">Un processo di streaming può avere più output.</span><span class="sxs-lookup"><span data-stu-id="edfcb-173">A streaming job can have multiple outputs.</span></span> <span data-ttu-id="edfcb-174">Output supportati: Hub eventi di Azure, Archiviazione BLOB di Azure, Archiviazione tabelle di Azure, Azure SQL DB e Power BI.</span><span class="sxs-lookup"><span data-stu-id="edfcb-174">Supported outputs are Azure Event Hubs, Azure Blob storage, Azure Table storage, Azure SQL DB, and Power BI.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="edfcb-175">Storm supporta più output in una topologia e ogni output può avere una logica personalizzata per l'elaborazione downstream.</span><span class="sxs-lookup"><span data-stu-id="edfcb-175">Storm supports many outputs in a topology, and each output can have custom logic for downstream processing.</span></span> <span data-ttu-id="edfcb-176">Storm include connettori predefiniti per Power BI, Hub eventi di Azure, Archiviazione BLOB di Azure, Azure Cosmos DB, SQL e HBase.</span><span class="sxs-lookup"><span data-stu-id="edfcb-176">Storm includes connectors for Power BI, Azure Event Hubs, Azure Blob storage, Azure Cosmos DB, SQL, and HBase.</span></span> <span data-ttu-id="edfcb-177">Gli utenti possono creare connettori aggiuntivi con codice personalizzato.</span><span class="sxs-lookup"><span data-stu-id="edfcb-177">Users can create additional connectors using custom code.</span></span>    
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="edfcb-178">
                    <strong>Formati di codifica dei dati</strong>
                </span><span class="sxs-lookup"><span data-stu-id="edfcb-178">
                    <strong>Data-encoding formats</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="edfcb-179">Dati devono essere formattati usando UTF-8.</span><span class="sxs-lookup"><span data-stu-id="edfcb-179">Data must be formatted using UTF-8.</span></span>
                </p>
            </td>   
            <td width="246" valign="top">
                <p>
<span data-ttu-id="edfcb-180">Gli utenti possono implementare tutti i formati di codifica dei dati usando codice personalizzato.</span><span class="sxs-lookup"><span data-stu-id="edfcb-180">Users can implement any data encoding format using custom code.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="management-and-operations"></a><span data-ttu-id="edfcb-181">Gestione e operazioni</span><span class="sxs-lookup"><span data-stu-id="edfcb-181">Management and operations</span></span> ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="edfcb-182">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="edfcb-182">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="edfcb-183">
                    <strong>Analisi di flusso di Azure</strong>
                </span><span class="sxs-lookup"><span data-stu-id="edfcb-183">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="edfcb-184">
                    <strong>Apache Storm in HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="edfcb-184">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="edfcb-185">
                    <strong>Modello di distribuzione dei processi</strong>
                </span><span class="sxs-lookup"><span data-stu-id="edfcb-185">
                    <strong>Job deployment model</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="edfcb-186">Portale di Azure, PowerShell e API REST.</span><span class="sxs-lookup"><span data-stu-id="edfcb-186">Azure portal, PowerShell, and REST APIs.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="edfcb-187">Portale di Azure, PowerShell, Visual Studio e API REST.</span><span class="sxs-lookup"><span data-stu-id="edfcb-187">Azure portal, PowerShell, Visual Studio, and REST APIs.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="edfcb-188">
                    <strong>Monitoraggio (statistiche, contatori e così via)</strong>
                </span><span class="sxs-lookup"><span data-stu-id="edfcb-188">
                    <strong>Monitoring (stats, counters, etc.)</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="edfcb-189">Il monitoraggio viene implementato tramite il portale di Azure e le API REST.</span><span class="sxs-lookup"><span data-stu-id="edfcb-189">Monitoring is implemented using Azure portal and REST APIs.</span></span> <span data-ttu-id="edfcb-190">Gli utenti possono inoltre configurare gli avvisi di Azure.</span><span class="sxs-lookup"><span data-stu-id="edfcb-190">Users can also configure Azure alerts.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="edfcb-191">Il monitoraggio viene implementato tramite hello Storm UI e le API REST.</span><span class="sxs-lookup"><span data-stu-id="edfcb-191">Monitoring is implemented using hello Storm UI and REST APIs.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="edfcb-192">
                    <strong>Scalabilità</strong>
                </span><span class="sxs-lookup"><span data-stu-id="edfcb-192">
                    <strong>Scalability</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="edfcb-193">La scalabilità è determinata dal numero di hello di unità di Streaming (SUs) per ogni processo.</span><span class="sxs-lookup"><span data-stu-id="edfcb-193">Scalability is determined by hello number of Streaming Units (SUs) for each job.</span></span> <span data-ttu-id="edfcb-194">Ogni unità di Streaming elabora backup too1 MB al secondo, con un massimo di 50 unità.</span><span class="sxs-lookup"><span data-stu-id="edfcb-194">Each Streaming Unit processes up too1 MB/second, with a maximum 50 units.</span></span> <span data-ttu-id="edfcb-195">Per ulteriori informazioni, vedere <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-jobs">velocità effettiva di scala tooincrease</a>.</span><span class="sxs-lookup"><span data-stu-id="edfcb-195">For more information, see <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-jobs">Scale tooincrease throughput</a>.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="edfcb-196">La scalabilità è determinata dal numero di hello di nodi nel cluster HDInsight Storm hello.</span><span class="sxs-lookup"><span data-stu-id="edfcb-196">Scalability is determined by hello number of nodes in hello HDInsight Storm cluster.</span></span> <span data-ttu-id="edfcb-197">limite superiore di Hello numero hello di nodi è definito dalla quota di Azure dell'utente hello.</span><span class="sxs-lookup"><span data-stu-id="edfcb-197">hello top limit on hello number of nodes is defined by hello user's Azure quota.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="edfcb-198">
                    <strong>Limiti di elaborazione dei dati</strong>
                </span><span class="sxs-lookup"><span data-stu-id="edfcb-198">
                    <strong>Data processing limits</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="edfcb-199">Gli utenti possono aumentare l'elaborazione dati o ottimizzare i costi aumentando o diminuendo hello numero di unità di Streaming, con un limite superiore di 1 GB al secondo.</span><span class="sxs-lookup"><span data-stu-id="edfcb-199">Users can increase data processing or optimize costs by increasing or decreasing hello number of Streaming Units, with an upper limit of 1 GB/second.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="edfcb-200">Gli utenti possono scalare le dimensioni cluster per aumentarle o diminuirle.</span><span class="sxs-lookup"><span data-stu-id="edfcb-200">Users can scale cluster size up or down.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="edfcb-201">
                    <strong>Arresto/ripresa</strong>
                </span><span class="sxs-lookup"><span data-stu-id="edfcb-201">
                    <strong>Stop/Resume</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="edfcb-202">Arrestare e riprendere dall'ultimo punto di arresto.</span><span class="sxs-lookup"><span data-stu-id="edfcb-202">Stop and resume from last place stopped.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="edfcb-203">Arrestare e riprendere dall'ultimo punto di arresto in base al limite.</span><span class="sxs-lookup"><span data-stu-id="edfcb-203">Stop and resume from last place stopped based on a watermark.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="edfcb-204">
                    <strong>Aggiornamento del servizio e del framework</strong>
                </span><span class="sxs-lookup"><span data-stu-id="edfcb-204">
                    <strong>Service and framework update</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="edfcb-205">Applicazione di patch automatica senza tempi di inattività.</span><span class="sxs-lookup"><span data-stu-id="edfcb-205">Automatic patching with no downtime.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="edfcb-206">Applicazione di patch automatica senza tempi di inattività.</span><span class="sxs-lookup"><span data-stu-id="edfcb-206">Automatic patching with no downtime.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="edfcb-207">
                    <strong>Continuità aziendale grazie a un servizio a disponibilità elevata con contratti di servizio garantiti</strong>
                </span><span class="sxs-lookup"><span data-stu-id="edfcb-207">
                    <strong>Business continuity through a Highly Available Service with guaranteed SLAs</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <ul>
                <li><span data-ttu-id="edfcb-208">Tempo di attività per il contratto di servizio del 99,9%</span><span class="sxs-lookup"><span data-stu-id="edfcb-208">SLA of 99.9% uptime</span></span></li>
                <li><span data-ttu-id="edfcb-209">Ripristino automatico in caso di errori</span><span class="sxs-lookup"><span data-stu-id="edfcb-209">Auto-recovery from failures</span></span></li>
                <li><span data-ttu-id="edfcb-210">Ripristino predefinito degli operatori temporali con stato</span><span class="sxs-lookup"><span data-stu-id="edfcb-210">Built-in recovery of stateful temporal operators</span></span></li>
                </ul>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="edfcb-211">Contratto di servizio del 99,9% tempo di attività del cluster Storm hello.</span><span class="sxs-lookup"><span data-stu-id="edfcb-211">SLA of 99.9% uptime of hello Storm cluster.</span></span> 
                </p>
                <p>
<span data-ttu-id="edfcb-212">Apache Storm è una piattaforma di streaming a tolleranza di errore.</span><span class="sxs-lookup"><span data-stu-id="edfcb-212">Apache Storm is a fault-tolerant streaming platform.</span></span> <span data-ttu-id="edfcb-213">Tuttavia, è tooensure responsabilità dell'utente hello che il flusso di esecuzione dei processi senza interruzioni.</span><span class="sxs-lookup"><span data-stu-id="edfcb-213">However, it is hello user's responsibility tooensure that streaming jobs run uninterrupted.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="advanced-features"></a><span data-ttu-id="edfcb-214">Funzionalità avanzate</span><span class="sxs-lookup"><span data-stu-id="edfcb-214">Advanced features</span></span> ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="edfcb-215">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="edfcb-215">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="edfcb-216">
                    <strong>Analisi di flusso di Azure</strong>
                </span><span class="sxs-lookup"><span data-stu-id="edfcb-216">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="edfcb-217">
                    <strong>Apache Storm in HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="edfcb-217">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="edfcb-218">
                    <strong>Gestione di eventi di arrivo in ritardo e con ordine non corretto</strong>
                </span><span class="sxs-lookup"><span data-stu-id="edfcb-218">
                    <strong>Late arrival and out-of-order event handling</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="edfcb-219">Criteri configurabili predefiniti per riordinare e rilasciare gli eventi o modificare l'ora degli eventi.</span><span class="sxs-lookup"><span data-stu-id="edfcb-219">Built-in configurable policies can reorder events, drop events, or adjust event time.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="edfcb-220">Gli utenti devono implementare logica toohandle questo scenario.</span><span class="sxs-lookup"><span data-stu-id="edfcb-220">Users must implement logic toohandle this scenario.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="edfcb-221">
                    <strong>Dati di riferimento</strong>
                </span><span class="sxs-lookup"><span data-stu-id="edfcb-221">
                    <strong>Reference data</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="edfcb-222">Dati di riferimento sono disponibili dall'archiviazione BLOB di Azure con un massimo di 100 MB di cache in memoria.</span><span class="sxs-lookup"><span data-stu-id="edfcb-222">Reference data is available from Azure Blob storage with a maximum of 100 MB of in-memory cache.</span></span> <span data-ttu-id="edfcb-223">Dati di riferimento viene aggiornati dal servizio hello.</span><span class="sxs-lookup"><span data-stu-id="edfcb-223">Reference data is refreshed by hello service.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="edfcb-224">Nessun limite alle dimensioni dei dati.</span><span class="sxs-lookup"><span data-stu-id="edfcb-224">No limits on data size.</span></span> <span data-ttu-id="edfcb-225">I connettori sono disponibili per HBase, Azure Cosmos DB, SQL Server e Azure.</span><span class="sxs-lookup"><span data-stu-id="edfcb-225">Connectors are available for HBase, Azure Cosmos DB, SQL Server, and Azure.</span></span> <span data-ttu-id="edfcb-226">Gli utenti possono creare connettori aggiuntivi con codice personalizzato.</span><span class="sxs-lookup"><span data-stu-id="edfcb-226">Users can create additional connectors using custom code.</span></span> <span data-ttu-id="edfcb-227">I dati di riferimento devono essere aggiornati con un codice personalizzato.</span><span class="sxs-lookup"><span data-stu-id="edfcb-227">Reference data must be refreshed using custom code.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="edfcb-228">
                    <strong>Integrazione con Machine Learning</strong>
                </span><span class="sxs-lookup"><span data-stu-id="edfcb-228">
                    <strong>Integration with Machine Learning</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="edfcb-229">I modelli di Azure Machine Learning pubblicati possono essere configurati come funzioni durante la creazione dei processi.</span><span class="sxs-lookup"><span data-stu-id="edfcb-229">Published Azure Machine Learning models can be configured as functions during job creation.</span></span> <span data-ttu-id="edfcb-230">Per altre informazioni, vedere <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-with-machine-learning-functions">Scalabilità per le funzioni di Machine Learning</a>.</span><span class="sxs-lookup"><span data-stu-id="edfcb-230">For more information, see <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-with-machine-learning-functions">Scale for Machine Learning functions</a>.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="edfcb-231">Disponibile tramite i bolt di Storm.</span><span class="sxs-lookup"><span data-stu-id="edfcb-231">Available through Storm Bolts.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>
