---
title: evento aaaReal-tempo di elaborazione con l'elaborazione degli eventi di flusso Analitica | Documenti Microsoft
description: "Informazioni su come un set di servizi di Azure è in grado di interagire per consentire l’elaborazione e l’analisi in tempo reale degli eventi."
keywords: elaborazione in tempo reale, elaborazione di eventi, architettura di riferimento
services: stream-analytics,event-hubs,storage,sql-database
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: 
ms.assetid: 11af48bc-313c-4527-8c80-91088dc9f3c6
ms.service: stream-analytics
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.author: jeffstok
ms.openlocfilehash: a43c503d709609ba61e9932822d30bc2208906ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="reference-architecture-real-time-event-processing-with-microsoft-azure-stream-analytics"></a><span data-ttu-id="220f5-104">Architettura di riferimento: elaborazione di eventi in tempo reale con Analisi di flusso di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="220f5-104">Reference architecture: Real-time event processing with Microsoft Azure Stream Analytics</span></span>
<span data-ttu-id="220f5-105">architettura di riferimento per l'elaborazione con Azure Analitica di flusso di eventi in tempo reale di Hello è previsto tooprovide generico linee guida per la distribuzione di una piattaforma in tempo reale come una soluzione di elaborazione del flusso di servizio (PaaS) con Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="220f5-105">hello reference architecture for real-time event processing with Azure Stream Analytics is intended tooprovide a generic blueprint for deploying a real-time platform as a service (PaaS) stream-processing solution with Microsoft Azure.</span></span>

## <a name="summary"></a><span data-ttu-id="220f5-106">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="220f5-106">Summary</span></span>
<span data-ttu-id="220f5-107">Tradizionalmente, soluzioni analitica sono basate sulle funzionalità, ad esempio ETL (extract, transform, load) e data warehouse, in cui i dati sono stored tooanalysis precedente.</span><span class="sxs-lookup"><span data-stu-id="220f5-107">Traditionally, analytics solutions have been based on capabilities such as ETL (extract, transform, load) and data warehousing, where data is stored prior tooanalysis.</span></span> <span data-ttu-id="220f5-108">Modifica di requisiti, inclusi i dati più rapidamente in arrivo sono push questo limite di toohello modello esistente.</span><span class="sxs-lookup"><span data-stu-id="220f5-108">Changing requirements, including more rapidly arriving data, are pushing this existing model toohello limit.</span></span> <span data-ttu-id="220f5-109">anche se non è una nuova funzionalità, approccio hello non è stato ampiamente adottato nei tutti i settori verticali Hello possibilità tooanalyze dati mobile toostorage precedente di flussi sono una soluzione.</span><span class="sxs-lookup"><span data-stu-id="220f5-109">hello ability tooanalyze data within moving streams prior toostorage is one solution, and while it is not a new capability, hello approach has not been widely adopted across all industry verticals.</span></span> 

<span data-ttu-id="220f5-110">Microsoft Azure fornisce un catalogo esteso di tecnologie di analisi in grado di supportare una matrice di scenari di soluzioni e requisiti diversi.</span><span class="sxs-lookup"><span data-stu-id="220f5-110">Microsoft Azure provides an extensive catalog of analytics technologies that are capable of supporting an array of different solution scenarios and requirements.</span></span> <span data-ttu-id="220f5-111">Selezione toodeploy quali servizi di Azure per una soluzione end-to-end può rappresentare un problema dato breadth hello delle offerte.</span><span class="sxs-lookup"><span data-stu-id="220f5-111">Selecting which Azure services toodeploy for an end-to-end solution can be a challenge given hello breadth of offerings.</span></span> <span data-ttu-id="220f5-112">In questo documento è progettato toodescribe hello funzionalità e l'interoperabilità di hello vari servizi di Azure che supportano una soluzione flusso di eventi.</span><span class="sxs-lookup"><span data-stu-id="220f5-112">This paper is designed toodescribe hello capabilities and interoperation of hello various Azure services that support an event-streaming solution.</span></span> <span data-ttu-id="220f5-113">Vengono inoltre illustrati alcuni degli scenari di hello in cui i clienti possono trarre vantaggio da questo tipo di approccio.</span><span class="sxs-lookup"><span data-stu-id="220f5-113">It also explains some of hello scenarios in which customers can benefit from this type of approach.</span></span>

## <a name="contents"></a><span data-ttu-id="220f5-114">Sommario</span><span class="sxs-lookup"><span data-stu-id="220f5-114">Contents</span></span>
* <span data-ttu-id="220f5-115">Sunto</span><span class="sxs-lookup"><span data-stu-id="220f5-115">Executive Summary</span></span>
* <span data-ttu-id="220f5-116">Introduzione tooReal fase Analitica</span><span class="sxs-lookup"><span data-stu-id="220f5-116">Introduction tooReal-Time Analytics</span></span>
* <span data-ttu-id="220f5-117">Proposta di valore dei dati in tempo reale in Azure</span><span class="sxs-lookup"><span data-stu-id="220f5-117">Value Proposition of Real-Time Data in Azure</span></span>
* <span data-ttu-id="220f5-118">Scenari comuni per l’analisi in tempo reale</span><span class="sxs-lookup"><span data-stu-id="220f5-118">Common Scenarios for Real-Time Analytics</span></span>
* <span data-ttu-id="220f5-119">Architettura e componenti</span><span class="sxs-lookup"><span data-stu-id="220f5-119">Architecture and Components</span></span>
  * <span data-ttu-id="220f5-120">Origini dati</span><span class="sxs-lookup"><span data-stu-id="220f5-120">Data Sources</span></span>
  * <span data-ttu-id="220f5-121">Livello di integrazione dei dati</span><span class="sxs-lookup"><span data-stu-id="220f5-121">Data-Integration Layer</span></span>
  * <span data-ttu-id="220f5-122">Livello di analisi in tempo reale</span><span class="sxs-lookup"><span data-stu-id="220f5-122">Real-time Analytics Layer</span></span>
  * <span data-ttu-id="220f5-123">Livello di archiviazione dei dati</span><span class="sxs-lookup"><span data-stu-id="220f5-123">Data Storage Layer</span></span>
  * <span data-ttu-id="220f5-124">Livello presentazione / consumo</span><span class="sxs-lookup"><span data-stu-id="220f5-124">Presentation / Consumption Layer</span></span>
* <span data-ttu-id="220f5-125">Conclusioni</span><span class="sxs-lookup"><span data-stu-id="220f5-125">Conclusion</span></span>

<span data-ttu-id="220f5-126">**Autore:** Charles Feddersen, Solution Architect, Data Insights Center of Excellence, Microsoft Corporation</span><span class="sxs-lookup"><span data-stu-id="220f5-126">**Author:** Charles Feddersen, Solution Architect, Data Insights Center of Excellence, Microsoft Corporation</span></span>

<span data-ttu-id="220f5-127">**Pubblicato:** gennaio 2015</span><span class="sxs-lookup"><span data-stu-id="220f5-127">**Published:** January 2015</span></span>

<span data-ttu-id="220f5-128">**Revisione:** 1.0</span><span class="sxs-lookup"><span data-stu-id="220f5-128">**Revision:** 1.0</span></span>

<span data-ttu-id="220f5-129">**Download:** [Elaborazione di eventi in tempo reale con Analisi dei flussi di Microsoft Azure](http://download.microsoft.com/download/6/2/3/623924DE-B083-4561-9624-C1AB62B5F82B/real-time-event-processing-with-microsoft-azure-stream-analytics.pdf)</span><span class="sxs-lookup"><span data-stu-id="220f5-129">**Download:** [Real-Time Event Processing with Microsoft Azure Stream Analytics](http://download.microsoft.com/download/6/2/3/623924DE-B083-4561-9624-C1AB62B5F82B/real-time-event-processing-with-microsoft-azure-stream-analytics.pdf)</span></span>

## <a name="get-help"></a><span data-ttu-id="220f5-130">Ottenere aiuto</span><span class="sxs-lookup"><span data-stu-id="220f5-130">Get help</span></span>
<span data-ttu-id="220f5-131">Per assistenza, provare il [Forum di Analisi di flusso di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="220f5-131">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="220f5-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="220f5-132">Next steps</span></span>
* [<span data-ttu-id="220f5-133">Introduzione tooAzure flusso Analitica</span><span class="sxs-lookup"><span data-stu-id="220f5-133">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="220f5-134">Introduzione all'uso di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="220f5-134">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="220f5-135">Ridimensionare i processi di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="220f5-135">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="220f5-136">Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="220f5-136">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="220f5-137">Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="220f5-137">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

