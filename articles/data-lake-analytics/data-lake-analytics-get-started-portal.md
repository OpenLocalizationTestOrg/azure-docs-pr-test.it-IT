---
title: Introduzione ad Azure Data Lake Analytics con il portale di Azure | Documentazione Microsoft
description: 'Informazioni su come usare il portale di Azure per creare un account Data Lake Analytics, creare un processo di Data Lake Analytics con U-SQL e inviare il processo. '
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: b1584d16-e0d2-4019-ad1f-f04be8c5b430
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/21/2017
ms.author: edmaca
ms.openlocfilehash: 2722a2d72ed90ea0005362563ecaee30750c040a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-portal"></a><span data-ttu-id="9261f-103">Introduzione ad Azure Data Lake Analytics con il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="9261f-103">Get started with Azure Data Lake Analytics using Azure portal</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="9261f-104">Informazioni su come usare il portale di Azure per creare account Azure Data Lake Analytics, definire processi in [U-SQL](data-lake-analytics-u-sql-get-started.md) e inviare processi al servizio Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="9261f-104">Learn how to use the Azure portal to create Azure Data Lake Analytics accounts, define jobs in [U-SQL](data-lake-analytics-u-sql-get-started.md), and submit jobs to the Data Lake Analytics service.</span></span> <span data-ttu-id="9261f-105">Per altre informazioni su Data Lake Analytics, vedere [Panoramica di Azure Data Lake Analytics](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9261f-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9261f-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="9261f-106">Prerequisites</span></span>

<span data-ttu-id="9261f-107">Prima di iniziare questa esercitazione, è necessaria una **sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="9261f-107">Before you begin this tutorial, you must have an **Azure subscription**.</span></span> <span data-ttu-id="9261f-108">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9261f-108">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="9261f-109">Creare un account di Analisi Data Lake</span><span class="sxs-lookup"><span data-stu-id="9261f-109">Create a Data Lake Analytics account</span></span>

<span data-ttu-id="9261f-110">A questo punto verranno creati un account Data Lake Analytics e un account Data Lake Store contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="9261f-110">Now, you will create a Data Lake Analytics and a Data Lake Store account at the same time.</span></span>  <span data-ttu-id="9261f-111">Questo passaggio è semplice e richiede solo 60 secondi.</span><span class="sxs-lookup"><span data-stu-id="9261f-111">This step is simple and only takes about 60 seconds to finish.</span></span>

1. <span data-ttu-id="9261f-112">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9261f-112">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9261f-113">Fare clic su **Nuovo** >  **Dati e analisi** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="9261f-113">Click **New** >  **Data + Analytics** > **Data Lake Analytics**.</span></span>
3. <span data-ttu-id="9261f-114">Selezionare i valori per gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="9261f-114">Select values for the following items:</span></span>
   * <span data-ttu-id="9261f-115">**Nome**: il nome dell'account di Data Lake Analytics deve contenere solo lettere minuscole e numeri.</span><span class="sxs-lookup"><span data-stu-id="9261f-115">**Name**: Name your Data Lake Analytics account (Only lower case letters and numbers allowed).</span></span>
   * <span data-ttu-id="9261f-116">**Sottoscrizione**: scegliere la sottoscrizione di Azure usata per l'account di Analytics.</span><span class="sxs-lookup"><span data-stu-id="9261f-116">**Subscription**: Choose the Azure subscription used for the Analytics account.</span></span>
   * <span data-ttu-id="9261f-117">**Gruppo di risorse**.</span><span class="sxs-lookup"><span data-stu-id="9261f-117">**Resource Group**.</span></span> <span data-ttu-id="9261f-118">Selezionare un gruppo di risorse di Azure esistente o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="9261f-118">Select an existing Azure Resource Group or create a new one.</span></span>
   * <span data-ttu-id="9261f-119">**Località**.</span><span class="sxs-lookup"><span data-stu-id="9261f-119">**Location**.</span></span> <span data-ttu-id="9261f-120">Selezionare un data center di Azure per l'account di Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="9261f-120">Select an Azure data center for the Data Lake Analytics account.</span></span>
   * <span data-ttu-id="9261f-121">**Data Lake Store**: seguire le istruzioni per creare un nuovo account Data Lake Store o selezionarne uno esistente.</span><span class="sxs-lookup"><span data-stu-id="9261f-121">**Data Lake Store**: Follow the instruction to create a new Data Lake Store account, or select an existing one.</span></span> 
4. <span data-ttu-id="9261f-122">Selezionare eventualmente un piano tariffario per l'account di Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="9261f-122">Optionally, select a pricing tier for your Data Lake Analytics account.</span></span>
5. <span data-ttu-id="9261f-123">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="9261f-123">Click **Create**.</span></span> 


## <a name="your-first-u-sql-script"></a><span data-ttu-id="9261f-124">Il primo script U-SQL</span><span class="sxs-lookup"><span data-stu-id="9261f-124">Your first U-SQL script</span></span>

<span data-ttu-id="9261f-125">Il testo seguente è uno script U-SQL molto semplice.</span><span class="sxs-lookup"><span data-stu-id="9261f-125">The following text is a very simple U-SQL script.</span></span> <span data-ttu-id="9261f-126">Definisce un set di dati di piccole dimensioni nello script e quindi scrive tale set di dati nell'istanza predefinita di Data Lake Store come file denominato `/data.csv`.</span><span class="sxs-lookup"><span data-stu-id="9261f-126">All it does is define a small dataset within the script and then write that dataset out to the default Data Lake Store as a file called `/data.csv`.</span></span>

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    TO "/data.csv"
    USING Outputters.Csv();
```

## <a name="submit-a-u-sql-job"></a><span data-ttu-id="9261f-127">Inviare un processo U-SQL</span><span class="sxs-lookup"><span data-stu-id="9261f-127">Submit a U-SQL job</span></span>

1. <span data-ttu-id="9261f-128">Dall'account Data Lake Analytics fare clic su **Nuovo processo**.</span><span class="sxs-lookup"><span data-stu-id="9261f-128">From the Data Lake Analytics account, click **New Job**.</span></span>
2. <span data-ttu-id="9261f-129">Incollare il testo dello script U-SQL illustrato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9261f-129">Paste in the text of the U-SQL script shown above.</span></span> 
3. <span data-ttu-id="9261f-130">Fare clic su **Submit Job**.</span><span class="sxs-lookup"><span data-stu-id="9261f-130">Click **Submit Job**.</span></span>   
4. <span data-ttu-id="9261f-131">Attendere finché lo stato del processo non viene modificato in **Riuscito**.</span><span class="sxs-lookup"><span data-stu-id="9261f-131">Wait until the job status changes to **Succeeded**.</span></span>
5. <span data-ttu-id="9261f-132">In caso di esito negativo del processo, vedere [Monitorare e risolvere i problemi dei processi di Data Lake Analytics](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="9261f-132">If the job failed, see [Monitor and troubleshoot Data Lake Analytics jobs](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span></span>
6. <span data-ttu-id="9261f-133">Fare clic sulla scheda **Output** e quindi su `data.csv`.</span><span class="sxs-lookup"><span data-stu-id="9261f-133">Click the **Output** tab, and then click `data.csv`.</span></span> 

## <a name="see-also"></a><span data-ttu-id="9261f-134">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9261f-134">See also</span></span>

* <span data-ttu-id="9261f-135">Per iniziare a sviluppare applicazioni U-SQL, vedere [Sviluppare script U-SQL tramite Strumenti di Data Lake per Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9261f-135">To get started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="9261f-136">Per informazioni su U-SQL, vedere [Introduzione al linguaggio U-SQL di Azure Data Lake Analytics](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9261f-136">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="9261f-137">Per informazioni sulle attività di gestione, vedere [Gestire Azure Data Lake Analytics tramite il portale di Azure](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9261f-137">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
