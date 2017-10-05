---
title: Elaborazione degli eventi in tempo reale con l'elaborazione degli eventi dell'analisi di flusso | Microsoft Docs
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
ms.openlocfilehash: b3057be995e551aac0761c3ce40a8dbf828a5f29
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="reference-architecture-real-time-event-processing-with-microsoft-azure-stream-analytics"></a><span data-ttu-id="dbe60-104">Architettura di riferimento: elaborazione di eventi in tempo reale con Analisi di flusso di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="dbe60-104">Reference architecture: Real-time event processing with Microsoft Azure Stream Analytics</span></span>
<span data-ttu-id="dbe60-105">L'architettura di riferimento per l'elaborazione di eventi in tempo reale con Analisi dei flussi di Azure è destinata a fornire un progetto generico per la distribuzione in tempo reale di una soluzione di elaborazione dei flussi PaaS con Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="dbe60-105">The reference architecture for real-time event processing with Azure Stream Analytics is intended to provide a generic blueprint for deploying a real-time platform as a service (PaaS) stream-processing solution with Microsoft Azure.</span></span>

## <a name="summary"></a><span data-ttu-id="dbe60-106">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="dbe60-106">Summary</span></span>
<span data-ttu-id="dbe60-107">In genere, le soluzioni di analisi sono basate su funzionalità, ad esempio ETL (estrazione, trasformazione e caricamento) e data warehouse, in cui sono archiviati i dati prima dell'analisi.</span><span class="sxs-lookup"><span data-stu-id="dbe60-107">Traditionally, analytics solutions have been based on capabilities such as ETL (extract, transform, load) and data warehousing, where data is stored prior to analysis.</span></span> <span data-ttu-id="dbe60-108">Le esigenze di modifica, tra cui i dati in arrivo con una maggiore rapidità, spingono al limite il modello esistente.</span><span class="sxs-lookup"><span data-stu-id="dbe60-108">Changing requirements, including more rapidly arriving data, are pushing this existing model to the limit.</span></span> <span data-ttu-id="dbe60-109">Una soluzione è rappresentata dalla possibilità di analizzare i dati all'interno di flussi in movimento prima dell'archiviazione, e sebbene non si tratti di una nuova funzionalità, l'approccio non è stato adottato ampiamente in tutti i settori industriali verticali.</span><span class="sxs-lookup"><span data-stu-id="dbe60-109">The ability to analyze data within moving streams prior to storage is one solution, and while it is not a new capability, the approach has not been widely adopted across all industry verticals.</span></span> 

<span data-ttu-id="dbe60-110">Microsoft Azure fornisce un catalogo esteso di tecnologie di analisi in grado di supportare una matrice di scenari di soluzioni e requisiti diversi.</span><span class="sxs-lookup"><span data-stu-id="dbe60-110">Microsoft Azure provides an extensive catalog of analytics technologies that are capable of supporting an array of different solution scenarios and requirements.</span></span> <span data-ttu-id="dbe60-111">Scegliere i servizi Azure da distribuire per una soluzione end-to-end può essere difficile data la vasta gamma di offerte.</span><span class="sxs-lookup"><span data-stu-id="dbe60-111">Selecting which Azure services to deploy for an end-to-end solution can be a challenge given the breadth of offerings.</span></span> <span data-ttu-id="dbe60-112">Questo documento è progettato per descrivere le funzionalità e l'interazione tra i vari servizi Azure che supportano una soluzione di flusso di eventi.</span><span class="sxs-lookup"><span data-stu-id="dbe60-112">This paper is designed to describe the capabilities and interoperation of the various Azure services that support an event-streaming solution.</span></span> <span data-ttu-id="dbe60-113">Vengono inoltre illustrati alcuni degli scenari in cui i clienti possono trarre vantaggio da questo tipo di approccio.</span><span class="sxs-lookup"><span data-stu-id="dbe60-113">It also explains some of the scenarios in which customers can benefit from this type of approach.</span></span>

## <a name="contents"></a><span data-ttu-id="dbe60-114">Sommario</span><span class="sxs-lookup"><span data-stu-id="dbe60-114">Contents</span></span>
* <span data-ttu-id="dbe60-115">Sunto</span><span class="sxs-lookup"><span data-stu-id="dbe60-115">Executive Summary</span></span>
* <span data-ttu-id="dbe60-116">Introduzione all'analisi in tempo reale</span><span class="sxs-lookup"><span data-stu-id="dbe60-116">Introduction to Real-Time Analytics</span></span>
* <span data-ttu-id="dbe60-117">Proposta di valore dei dati in tempo reale in Azure</span><span class="sxs-lookup"><span data-stu-id="dbe60-117">Value Proposition of Real-Time Data in Azure</span></span>
* <span data-ttu-id="dbe60-118">Scenari comuni per l’analisi in tempo reale</span><span class="sxs-lookup"><span data-stu-id="dbe60-118">Common Scenarios for Real-Time Analytics</span></span>
* <span data-ttu-id="dbe60-119">Architettura e componenti</span><span class="sxs-lookup"><span data-stu-id="dbe60-119">Architecture and Components</span></span>
  * <span data-ttu-id="dbe60-120">Origini dati</span><span class="sxs-lookup"><span data-stu-id="dbe60-120">Data Sources</span></span>
  * <span data-ttu-id="dbe60-121">Livello di integrazione dei dati</span><span class="sxs-lookup"><span data-stu-id="dbe60-121">Data-Integration Layer</span></span>
  * <span data-ttu-id="dbe60-122">Livello di analisi in tempo reale</span><span class="sxs-lookup"><span data-stu-id="dbe60-122">Real-time Analytics Layer</span></span>
  * <span data-ttu-id="dbe60-123">Livello di archiviazione dei dati</span><span class="sxs-lookup"><span data-stu-id="dbe60-123">Data Storage Layer</span></span>
  * <span data-ttu-id="dbe60-124">Livello presentazione / consumo</span><span class="sxs-lookup"><span data-stu-id="dbe60-124">Presentation / Consumption Layer</span></span>
* <span data-ttu-id="dbe60-125">Conclusioni</span><span class="sxs-lookup"><span data-stu-id="dbe60-125">Conclusion</span></span>

<span data-ttu-id="dbe60-126">**Autore:** Charles Feddersen, Solution Architect, Data Insights Center of Excellence, Microsoft Corporation</span><span class="sxs-lookup"><span data-stu-id="dbe60-126">**Author:** Charles Feddersen, Solution Architect, Data Insights Center of Excellence, Microsoft Corporation</span></span>

<span data-ttu-id="dbe60-127">**Pubblicato:** gennaio 2015</span><span class="sxs-lookup"><span data-stu-id="dbe60-127">**Published:** January 2015</span></span>

<span data-ttu-id="dbe60-128">**Revisione:** 1.0</span><span class="sxs-lookup"><span data-stu-id="dbe60-128">**Revision:** 1.0</span></span>

<span data-ttu-id="dbe60-129">**Download:** [Elaborazione di eventi in tempo reale con Analisi dei flussi di Microsoft Azure](http://download.microsoft.com/download/6/2/3/623924DE-B083-4561-9624-C1AB62B5F82B/real-time-event-processing-with-microsoft-azure-stream-analytics.pdf)</span><span class="sxs-lookup"><span data-stu-id="dbe60-129">**Download:** [Real-Time Event Processing with Microsoft Azure Stream Analytics](http://download.microsoft.com/download/6/2/3/623924DE-B083-4561-9624-C1AB62B5F82B/real-time-event-processing-with-microsoft-azure-stream-analytics.pdf)</span></span>

## <a name="get-help"></a><span data-ttu-id="dbe60-130">Ottenere aiuto</span><span class="sxs-lookup"><span data-stu-id="dbe60-130">Get help</span></span>
<span data-ttu-id="dbe60-131">Per assistenza, provare il [Forum di Analisi di flusso di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="dbe60-131">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="dbe60-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dbe60-132">Next steps</span></span>
* [<span data-ttu-id="dbe60-133">Introduzione ad Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="dbe60-133">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="dbe60-134">Introduzione all'uso di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="dbe60-134">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="dbe60-135">Ridimensionare i processi di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="dbe60-135">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="dbe60-136">Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="dbe60-136">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="dbe60-137">Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="dbe60-137">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

