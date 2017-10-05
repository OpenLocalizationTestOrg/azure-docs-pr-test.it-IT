---
title: Creare soluzioni integrate con SQL Data Warehouse | Documentazione Microsoft
description: 'Strumenti e partner con soluzioni che interagiscono con SQL Data Warehouse. '
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: e2dc8f3f-10e3-4589-a4e2-50c67dfcf67f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: d407c29f99fd7537590ec787febd84a9e3f4f353
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="leverage-other-services-with-sql-data-warehouse"></a><span data-ttu-id="6b2e3-103">Utilizzare altri servizi con SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="6b2e3-103">Leverage other services with SQL Data Warehouse</span></span>
<span data-ttu-id="6b2e3-104">Oltre alle funzionalità di base, SQL Data Warehouse consente agli utenti di utilizzare molti altri servizi in Azure insieme a esso.</span><span class="sxs-lookup"><span data-stu-id="6b2e3-104">In addition to its core functionality, SQL Data Warehouse enables users to leverage many of the other services in Azure alongside it.</span></span>  <span data-ttu-id="6b2e3-105">In particolare, sono state attualmente intraprese azioni per integrare completamente le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="6b2e3-105">Specifically, we have currently taken steps to deeply integrate with the following:</span></span>

* <span data-ttu-id="6b2e3-106">Power BI</span><span class="sxs-lookup"><span data-stu-id="6b2e3-106">Power BI</span></span>
* <span data-ttu-id="6b2e3-107">Data factory di Azure</span><span class="sxs-lookup"><span data-stu-id="6b2e3-107">Azure Data Factory</span></span>
* <span data-ttu-id="6b2e3-108">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="6b2e3-108">Azure Machine Learning</span></span>
* <span data-ttu-id="6b2e3-109">Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6b2e3-109">Azure Stream Analytics</span></span>

<span data-ttu-id="6b2e3-110">Stiamo lavorando per connettersi con altri servizi attraverso l'ecosistema di Azure.</span><span class="sxs-lookup"><span data-stu-id="6b2e3-110">We are working to connect with more services across the Azure ecosystem.</span></span>

## <a name="power-bi"></a><span data-ttu-id="6b2e3-111">Power BI</span><span class="sxs-lookup"><span data-stu-id="6b2e3-111">Power BI</span></span>
<span data-ttu-id="6b2e3-112">Integrazione di Power BI consente di sfruttare la potenza di calcolo di Data Warehouse di SQL con la creazione di report dinamici e visualizzazione di Power BI.</span><span class="sxs-lookup"><span data-stu-id="6b2e3-112">Power BI integration allows you to leverage the compute power of SQL Data Warehouse with the dynamic reporting and visualization of Power BI.</span></span> <span data-ttu-id="6b2e3-113">L’integrazione di Power BI include attualmente:</span><span class="sxs-lookup"><span data-stu-id="6b2e3-113">Power BI integration currently includes:</span></span>

* <span data-ttu-id="6b2e3-114">**Connessione diretta**: una connessione più avanzata con caratteristiche logiche SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="6b2e3-114">**Direct Connect**: A more advanced connection with logical pushdown against SQL Data Warehouse.</span></span>  <span data-ttu-id="6b2e3-115">Questo fornisce un'analisi veloce su vasta scala.</span><span class="sxs-lookup"><span data-stu-id="6b2e3-115">This provides faster analysis on a larger scale.</span></span>
* <span data-ttu-id="6b2e3-116">**Aprire in Power BI**: il tasto 'Apri in Power BI' passa informazioni istanza a Power BI, consentendo una connessione più trasparente.</span><span class="sxs-lookup"><span data-stu-id="6b2e3-116">**Open in Power BI**: The 'Open in Power BI' button passes instance information to Power BI, allowing for a more seamless connection.</span></span>

<span data-ttu-id="6b2e3-117">Vedere [Integrazione con Power BI](sql-data-warehouse-integrate-power-bi.md) o fare riferimento alla [documentazione di Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/06/24/exploring-azure-sql-data-warehouse-with-power-bi.aspx) per altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="6b2e3-117">See [Integrate with Power BI](sql-data-warehouse-integrate-power-bi.md) or the [Power BI documentation](http://blogs.msdn.com/b/powerbi/archive/2015/06/24/exploring-azure-sql-data-warehouse-with-power-bi.aspx) for more information.</span></span>

## <a name="azure-data-factory"></a><span data-ttu-id="6b2e3-118">Data factory di Azure</span><span class="sxs-lookup"><span data-stu-id="6b2e3-118">Azure Data Factory</span></span>
<span data-ttu-id="6b2e3-119">Azure Data Factory offre agli utenti una piattaforma gestita per creare pipeline estrazione-caricamento complesse.</span><span class="sxs-lookup"><span data-stu-id="6b2e3-119">Azure Data Factory gives users a managed platform to create complex Extract-Load pipelines.</span></span>  <span data-ttu-id="6b2e3-120">L’integrazione di SQL Data Warehouse con Azure Data Factory include quanto segue:</span><span class="sxs-lookup"><span data-stu-id="6b2e3-120">SQL Data Warehouse's integration with Azure Data Factory includes the following:</span></span>

* <span data-ttu-id="6b2e3-121">**Procedure di archiviazione**: orchestrare l'esecuzione delle procedure di archiviazione in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="6b2e3-121">**Stored Procedures**: Orchestrate the execution of stored procedures on SQL Data Warehouse.</span></span>
* <span data-ttu-id="6b2e3-122">**Copia**: usare ADF per spostare dati in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="6b2e3-122">**Copy**: Use ADF to move data into SQL Data Warehouse.</span></span>  <span data-ttu-id="6b2e3-123">Questa operazione può usare un meccanismo di spostamento dati ADF standard oppure PolyBase in background.</span><span class="sxs-lookup"><span data-stu-id="6b2e3-123">This operation can use ADF's standard data movement mechanism or PolyBase under the covers.</span></span> 

<span data-ttu-id="6b2e3-124">Vedere [Integrazione con Azure Data Factory](sql-data-warehouse-integrate-azure-data-factory.md) o [Documentazione di Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) per altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="6b2e3-124">See [Integrate with Azure Data Factory](sql-data-warehouse-integrate-azure-data-factory.md) or the [Azure Data Factory documentation](https://azure.microsoft.com/documentation/services/data-factory/) for more information.</span></span>

## <a name="azure-machine-learning"></a><span data-ttu-id="6b2e3-125">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="6b2e3-125">Azure Machine Learning</span></span>
<span data-ttu-id="6b2e3-126">Azure Machine Learning è un servizio di analisi completamente gestito che consente agli utenti di creare modelli complessi sfruttando un ampio set di strumenti di previsione.</span><span class="sxs-lookup"><span data-stu-id="6b2e3-126">Azure Machine Learning is a fully managed analytics service which allows users to create intricate models leveraging a large set of predictive tools.</span></span>  <span data-ttu-id="6b2e3-127">SQL Data Warehouse è supportato come origine e destinazione per questi modelli con le funzionalità seguenti:</span><span class="sxs-lookup"><span data-stu-id="6b2e3-127">SQL Data Warehouse is supported as both a source and destination for these models with the following functionality:</span></span>

* <span data-ttu-id="6b2e3-128">**Lettura dati:** Guida i modelli su larga scala mediante T-SQL su SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="6b2e3-128">**Read Data:** Drive models at scale using T-SQL against SQL Data Warehouse.</span></span>
* <span data-ttu-id="6b2e3-129">**Scrittura dati:** registra le modifiche da qualsiasi modello a SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="6b2e3-129">**Write Data:** Commit changes from any model back to SQL Data Warehouse.</span></span>

<span data-ttu-id="6b2e3-130">Vedere [Integrazione con Azure Machine Learning](sql-data-warehouse-integrate-azure-machine-learning.md) o fare riferimento alla [documentazione di Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) per altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="6b2e3-130">See [Integrate with Azure Machine Learning](sql-data-warehouse-integrate-azure-machine-learning.md) or the [Azure Machine Learning documentation](https://azure.microsoft.com/services/machine-learning/) for more information.</span></span>

## <a name="azure-stream-analytics"></a><span data-ttu-id="6b2e3-131">Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="6b2e3-131">Azure Stream Analytics</span></span>
<span data-ttu-id="6b2e3-132">L’Analisi dei flussi di Azure è un'infrastruttura complessa, completamente gestita per l'elaborazione e l'utilizzo di dati degli eventi generati da Hub eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="6b2e3-132">Azure Stream Analytics is a complex, fully managed infrastructure for processing and consuming event data generated from Azure Event Hub.</span></span>  <span data-ttu-id="6b2e3-133">L’integrazione con SQL Data Warehouse consente la trasmissione di dati in modo efficace da elaborare e archiviare insieme ai dati relazionali permettendo un’analisi più approfondita, più avanzata.</span><span class="sxs-lookup"><span data-stu-id="6b2e3-133">Integration with SQL Data Warehouse allows for streaming data to be effectively processed and stored alongside relational data enabling deeper, more advanced analysis.</span></span>  

* <span data-ttu-id="6b2e3-134">**Output del processo:** inviare l'output da processi di analisi di flusso direttamente a SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="6b2e3-134">**Job Output:** Send output from Stream Analytics jobs directly to SQL Data Warehouse.</span></span>

<span data-ttu-id="6b2e3-135">Vedere [Integrazione con Analisi di flusso di Azure](sql-data-warehouse-integrate-azure-stream-analytics.md) o [Documentazione dell'analisi di flusso di Azure](https://azure.microsoft.com/documentation/services/stream-analytics/) per altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="6b2e3-135">See [Integrate with Azure Stream Analytics](sql-data-warehouse-integrate-azure-stream-analytics.md) or the [Azure Stream Analytics documentation](https://azure.microsoft.com/documentation/services/stream-analytics/) for more information.</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop/

[Azure Data Factory]: sql-data-warehouse-integrate-azure-data-factory.md
[Azure Machine Learning]: sql-data-warehouse-integrate-azure-machine-learning.md
[Azure Stream Analytics]: sql-data-warehouse-integrate-azure-stream-analytics.md
[Power BI]: sql-data-warehouse-integrate-power-bi.md
[Partners]: sql-data-warehouse-partner-business-intelligence.md

<!--MSDN references-->

<!--Other Web references-->
