---
title: aaaGet avviato con Azure Data Lake Analitica tramite il portale di Azure | Documenti Microsoft
description: 'Informazioni su come creare un processo di Data Lake Analitica con U-SQL, hello toouse toocreate portale Azure un account Data Lake Analitica e inviare il processo di hello. '
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
ms.openlocfilehash: 6bb54404fa42cfed25b18bc2bfb7c72e6c361149
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-portal"></a><span data-ttu-id="85c4f-103">Introduzione ad Azure Data Lake Analytics con il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="85c4f-103">Get started with Azure Data Lake Analytics using Azure portal</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="85c4f-104">Informazioni su come toouse hello Azure toocreate portale account di Azure Data Lake Analitica, definire i processi in [U-SQL](data-lake-analytics-u-sql-get-started.md)e l'invio del servizio Data Lake Analitica toohello di processi.</span><span class="sxs-lookup"><span data-stu-id="85c4f-104">Learn how toouse hello Azure portal toocreate Azure Data Lake Analytics accounts, define jobs in [U-SQL](data-lake-analytics-u-sql-get-started.md), and submit jobs toohello Data Lake Analytics service.</span></span> <span data-ttu-id="85c4f-105">Per altre informazioni su Data Lake Analytics, vedere [Panoramica di Azure Data Lake Analytics](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="85c4f-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="85c4f-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="85c4f-106">Prerequisites</span></span>

<span data-ttu-id="85c4f-107">Prima di iniziare questa esercitazione, è necessaria una **sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="85c4f-107">Before you begin this tutorial, you must have an **Azure subscription**.</span></span> <span data-ttu-id="85c4f-108">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="85c4f-108">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="85c4f-109">Creare un account di Analisi Data Lake</span><span class="sxs-lookup"><span data-stu-id="85c4f-109">Create a Data Lake Analytics account</span></span>

<span data-ttu-id="85c4f-110">A questo punto, si creerà un Analitica Lake dati e un archivio Data Lake account in hello stesso tempo.</span><span class="sxs-lookup"><span data-stu-id="85c4f-110">Now, you will create a Data Lake Analytics and a Data Lake Store account at hello same time.</span></span>  <span data-ttu-id="85c4f-111">Questo passaggio è semplice e richiede solo circa 60 secondi toofinish.</span><span class="sxs-lookup"><span data-stu-id="85c4f-111">This step is simple and only takes about 60 seconds toofinish.</span></span>

1. <span data-ttu-id="85c4f-112">Accesso toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="85c4f-112">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="85c4f-113">Fare clic su **Nuovo** >  **Dati e analisi** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="85c4f-113">Click **New** >  **Data + Analytics** > **Data Lake Analytics**.</span></span>
3. <span data-ttu-id="85c4f-114">Selezionare i valori per hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="85c4f-114">Select values for hello following items:</span></span>
   * <span data-ttu-id="85c4f-115">**Nome**: il nome dell'account di Data Lake Analytics deve contenere solo lettere minuscole e numeri.</span><span class="sxs-lookup"><span data-stu-id="85c4f-115">**Name**: Name your Data Lake Analytics account (Only lower case letters and numbers allowed).</span></span>
   * <span data-ttu-id="85c4f-116">**Sottoscrizione**: scegliere una sottoscrizione di Azure usata per hello account Analitica hello.</span><span class="sxs-lookup"><span data-stu-id="85c4f-116">**Subscription**: Choose hello Azure subscription used for hello Analytics account.</span></span>
   * <span data-ttu-id="85c4f-117">**Gruppo di risorse**.</span><span class="sxs-lookup"><span data-stu-id="85c4f-117">**Resource Group**.</span></span> <span data-ttu-id="85c4f-118">Selezionare un gruppo di risorse di Azure esistente o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="85c4f-118">Select an existing Azure Resource Group or create a new one.</span></span>
   * <span data-ttu-id="85c4f-119">**Località**.</span><span class="sxs-lookup"><span data-stu-id="85c4f-119">**Location**.</span></span> <span data-ttu-id="85c4f-120">Selezionare un data center di Azure per l'account Data Lake Analitica hello.</span><span class="sxs-lookup"><span data-stu-id="85c4f-120">Select an Azure data center for hello Data Lake Analytics account.</span></span>
   * <span data-ttu-id="85c4f-121">**Archivio Data Lake**: seguire hello istruzione toocreate un nuovo account archivio Data Lake o selezionarne uno esistente.</span><span class="sxs-lookup"><span data-stu-id="85c4f-121">**Data Lake Store**: Follow hello instruction toocreate a new Data Lake Store account, or select an existing one.</span></span> 
4. <span data-ttu-id="85c4f-122">Selezionare eventualmente un piano tariffario per l'account di Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="85c4f-122">Optionally, select a pricing tier for your Data Lake Analytics account.</span></span>
5. <span data-ttu-id="85c4f-123">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="85c4f-123">Click **Create**.</span></span> 


## <a name="your-first-u-sql-script"></a><span data-ttu-id="85c4f-124">Il primo script U-SQL</span><span class="sxs-lookup"><span data-stu-id="85c4f-124">Your first U-SQL script</span></span>

<span data-ttu-id="85c4f-125">Dopo il testo Hello è un semplice script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="85c4f-125">hello following text is a very simple U-SQL script.</span></span> <span data-ttu-id="85c4f-126">Non è di definire un piccolo set di dati all'interno dello script hello e quindi scrivere set di dati all'archivio Data Lake di toohello predefinito come un file denominato `/data.csv`.</span><span class="sxs-lookup"><span data-stu-id="85c4f-126">All it does is define a small dataset within hello script and then write that dataset out toohello default Data Lake Store as a file called `/data.csv`.</span></span>

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
```

## <a name="submit-a-u-sql-job"></a><span data-ttu-id="85c4f-127">Inviare un processo U-SQL</span><span class="sxs-lookup"><span data-stu-id="85c4f-127">Submit a U-SQL job</span></span>

1. <span data-ttu-id="85c4f-128">Hello account Data Lake Analitica, fare clic su **nuovo processo**.</span><span class="sxs-lookup"><span data-stu-id="85c4f-128">From hello Data Lake Analytics account, click **New Job**.</span></span>
2. <span data-ttu-id="85c4f-129">Incolla il testo hello di hello script U-SQL illustrato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="85c4f-129">Paste in hello text of hello U-SQL script shown above.</span></span> 
3. <span data-ttu-id="85c4f-130">Fare clic su **Submit Job**.</span><span class="sxs-lookup"><span data-stu-id="85c4f-130">Click **Submit Job**.</span></span>   
4. <span data-ttu-id="85c4f-131">Attendere finché le modifiche di stato processo hello troppo**Succeeded**.</span><span class="sxs-lookup"><span data-stu-id="85c4f-131">Wait until hello job status changes too**Succeeded**.</span></span>
5. <span data-ttu-id="85c4f-132">Se il processo di hello non riuscito, vedere [monitoraggio e risoluzione dei problemi dei processi di Data Lake Analitica](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="85c4f-132">If hello job failed, see [Monitor and troubleshoot Data Lake Analytics jobs](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span></span>
6. <span data-ttu-id="85c4f-133">Fare clic su hello **Output** scheda e quindi fare clic su `data.csv`.</span><span class="sxs-lookup"><span data-stu-id="85c4f-133">Click hello **Output** tab, and then click `data.csv`.</span></span> 

## <a name="see-also"></a><span data-ttu-id="85c4f-134">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="85c4f-134">See also</span></span>

* <span data-ttu-id="85c4f-135">tooget iniziare a sviluppare applicazioni U-SQL, vedere [script U-SQL sviluppare utilizzando Data Lake Tools per Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="85c4f-135">tooget started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="85c4f-136">toolearn U-SQL, vedere [Guida introduttiva di Azure Data Lake Analitica U-SQL language](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="85c4f-136">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="85c4f-137">Per informazioni sulle attività di gestione, vedere [Gestire Azure Data Lake Analytics tramite il portale di Azure](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="85c4f-137">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
