---
title: soluzioni aaaBuild integrate con SQL Data Warehouse | Documenti Microsoft
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
ms.openlocfilehash: c8a4202dd84305bea4e4c2faf0e4791d026e794f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="leverage-other-services-with-sql-data-warehouse"></a><span data-ttu-id="852d3-103">Utilizzare altri servizi con SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="852d3-103">Leverage other services with SQL Data Warehouse</span></span>
<span data-ttu-id="852d3-104">Inoltre tooits principali funzionalità, SQL Data Warehouse consente agli utenti tooleverage molti hello altri servizi in Azure visualizzato.</span><span class="sxs-lookup"><span data-stu-id="852d3-104">In addition tooits core functionality, SQL Data Warehouse enables users tooleverage many of hello other services in Azure alongside it.</span></span>  <span data-ttu-id="852d3-105">Nello specifico, abbiamo adottato attualmente toodeeply integrarlo seguente hello passaggi:</span><span class="sxs-lookup"><span data-stu-id="852d3-105">Specifically, we have currently taken steps toodeeply integrate with hello following:</span></span>

* <span data-ttu-id="852d3-106">Power BI</span><span class="sxs-lookup"><span data-stu-id="852d3-106">Power BI</span></span>
* <span data-ttu-id="852d3-107">Data factory di Azure</span><span class="sxs-lookup"><span data-stu-id="852d3-107">Azure Data Factory</span></span>
* <span data-ttu-id="852d3-108">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="852d3-108">Azure Machine Learning</span></span>
* <span data-ttu-id="852d3-109">Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="852d3-109">Azure Stream Analytics</span></span>

<span data-ttu-id="852d3-110">Stiamo tooconnect con più servizi hello ecosistema di Azure.</span><span class="sxs-lookup"><span data-stu-id="852d3-110">We are working tooconnect with more services across hello Azure ecosystem.</span></span>

## <a name="power-bi"></a><span data-ttu-id="852d3-111">Power BI</span><span class="sxs-lookup"><span data-stu-id="852d3-111">Power BI</span></span>
<span data-ttu-id="852d3-112">Integrazione di Power BI permette di potenza di calcolo di hello tooleverage di SQL Data Warehouse con reporting dinamico hello e visualizzazione di Power BI.</span><span class="sxs-lookup"><span data-stu-id="852d3-112">Power BI integration allows you tooleverage hello compute power of SQL Data Warehouse with hello dynamic reporting and visualization of Power BI.</span></span> <span data-ttu-id="852d3-113">L’integrazione di Power BI include attualmente:</span><span class="sxs-lookup"><span data-stu-id="852d3-113">Power BI integration currently includes:</span></span>

* <span data-ttu-id="852d3-114">**Connessione diretta**: una connessione più avanzata con caratteristiche logiche SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="852d3-114">**Direct Connect**: A more advanced connection with logical pushdown against SQL Data Warehouse.</span></span>  <span data-ttu-id="852d3-115">Questo fornisce un'analisi veloce su vasta scala.</span><span class="sxs-lookup"><span data-stu-id="852d3-115">This provides faster analysis on a larger scale.</span></span>
* <span data-ttu-id="852d3-116">**Apri in Power BI**: pulsante 'Apri in Power BI' hello passa tooPower informazioni istanza BI, consentendo una connessione più semplice.</span><span class="sxs-lookup"><span data-stu-id="852d3-116">**Open in Power BI**: hello 'Open in Power BI' button passes instance information tooPower BI, allowing for a more seamless connection.</span></span>

<span data-ttu-id="852d3-117">Vedere [integrazione con Power BI](sql-data-warehouse-integrate-power-bi.md) o hello [documentazione di Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/06/24/exploring-azure-sql-data-warehouse-with-power-bi.aspx) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="852d3-117">See [Integrate with Power BI](sql-data-warehouse-integrate-power-bi.md) or hello [Power BI documentation](http://blogs.msdn.com/b/powerbi/archive/2015/06/24/exploring-azure-sql-data-warehouse-with-power-bi.aspx) for more information.</span></span>

## <a name="azure-data-factory"></a><span data-ttu-id="852d3-118">Data factory di Azure</span><span class="sxs-lookup"><span data-stu-id="852d3-118">Azure Data Factory</span></span>
<span data-ttu-id="852d3-119">Data Factory di Azure offre agli utenti un toocreate piattaforma gestita che Extract-Load complessi delle pipeline.</span><span class="sxs-lookup"><span data-stu-id="852d3-119">Azure Data Factory gives users a managed platform toocreate complex Extract-Load pipelines.</span></span>  <span data-ttu-id="852d3-120">Integrazione di SQL Data Warehouse con Data Factory di Azure include seguente hello:</span><span class="sxs-lookup"><span data-stu-id="852d3-120">SQL Data Warehouse's integration with Azure Data Factory includes hello following:</span></span>

* <span data-ttu-id="852d3-121">**Stored procedure**: orchestrare esecuzione hello di stored procedure in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="852d3-121">**Stored Procedures**: Orchestrate hello execution of stored procedures on SQL Data Warehouse.</span></span>
* <span data-ttu-id="852d3-122">**Copia**: dati di utilizzo ADF toomove in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="852d3-122">**Copy**: Use ADF toomove data into SQL Data Warehouse.</span></span>  <span data-ttu-id="852d3-123">Questa operazione è possibile utilizzare meccanismo di spostamento dei dati standard del file ADF o copre PolyBase in hello.</span><span class="sxs-lookup"><span data-stu-id="852d3-123">This operation can use ADF's standard data movement mechanism or PolyBase under hello covers.</span></span> 

<span data-ttu-id="852d3-124">Vedere [integrazione con Azure Data Factory](sql-data-warehouse-integrate-azure-data-factory.md) o hello [documentazione di Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="852d3-124">See [Integrate with Azure Data Factory](sql-data-warehouse-integrate-azure-data-factory.md) or hello [Azure Data Factory documentation](https://azure.microsoft.com/documentation/services/data-factory/) for more information.</span></span>

## <a name="azure-machine-learning"></a><span data-ttu-id="852d3-125">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="852d3-125">Azure Machine Learning</span></span>
<span data-ttu-id="852d3-126">Azure Machine Learning è un servizio analitica completamente gestito che consente agli utenti i modelli più complessi toocreate sfruttando un ampio set di strumenti di previsione.</span><span class="sxs-lookup"><span data-stu-id="852d3-126">Azure Machine Learning is a fully managed analytics service which allows users toocreate intricate models leveraging a large set of predictive tools.</span></span>  <span data-ttu-id="852d3-127">SQL Data Warehouse è supportato come un'origine e di destinazione per questi modelli con hello seguenti funzionalità:</span><span class="sxs-lookup"><span data-stu-id="852d3-127">SQL Data Warehouse is supported as both a source and destination for these models with hello following functionality:</span></span>

* <span data-ttu-id="852d3-128">**Lettura dati:** Guida i modelli su larga scala mediante T-SQL su SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="852d3-128">**Read Data:** Drive models at scale using T-SQL against SQL Data Warehouse.</span></span>
* <span data-ttu-id="852d3-129">**Scrittura di dati:** il Commit delle modifiche da qualsiasi modello di eseguire il backup tooSQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="852d3-129">**Write Data:** Commit changes from any model back tooSQL Data Warehouse.</span></span>

<span data-ttu-id="852d3-130">Vedere [integrazione con Azure Machine Learning](sql-data-warehouse-integrate-azure-machine-learning.md) o hello [documentazione di Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="852d3-130">See [Integrate with Azure Machine Learning](sql-data-warehouse-integrate-azure-machine-learning.md) or hello [Azure Machine Learning documentation](https://azure.microsoft.com/services/machine-learning/) for more information.</span></span>

## <a name="azure-stream-analytics"></a><span data-ttu-id="852d3-131">Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="852d3-131">Azure Stream Analytics</span></span>
<span data-ttu-id="852d3-132">L’Analisi dei flussi di Azure è un'infrastruttura complessa, completamente gestita per l'elaborazione e l'utilizzo di dati degli eventi generati da Hub eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="852d3-132">Azure Stream Analytics is a complex, fully managed infrastructure for processing and consuming event data generated from Azure Event Hub.</span></span>  <span data-ttu-id="852d3-133">Integrazione con SQL Data Warehouse consente la trasmissione toobe dati elaborati in modo efficace e archiviato insieme ai dati relazionali, consentendo più approfondita, più avanzate di analisi.</span><span class="sxs-lookup"><span data-stu-id="852d3-133">Integration with SQL Data Warehouse allows for streaming data toobe effectively processed and stored alongside relational data enabling deeper, more advanced analysis.</span></span>  

* <span data-ttu-id="852d3-134">**Output del processo:** Analitica di flusso di output invia i processi direttamente tooSQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="852d3-134">**Job Output:** Send output from Stream Analytics jobs directly tooSQL Data Warehouse.</span></span>

<span data-ttu-id="852d3-135">Vedere [integrazione con Azure flusso Analitica](sql-data-warehouse-integrate-azure-stream-analytics.md) o hello [documentazione di Azure flusso Analitica](https://azure.microsoft.com/documentation/services/stream-analytics/) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="852d3-135">See [Integrate with Azure Stream Analytics](sql-data-warehouse-integrate-azure-stream-analytics.md) or hello [Azure Stream Analytics documentation](https://azure.microsoft.com/documentation/services/stream-analytics/) for more information.</span></span>

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
