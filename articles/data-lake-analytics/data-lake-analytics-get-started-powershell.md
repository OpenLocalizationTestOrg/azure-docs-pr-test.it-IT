---
title: aaaGet avviato con Azure Data Lake Analitica con Azure PowerShell | Documenti Microsoft
description: 'Usare Azure PowerShell toocreate un account Data Lake Analitica, creare un processo di Data Lake Analitica utilizzando U-SQL e inviare il processo di hello. '
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 8a4e901e-9656-4a60-90d0-d78ff2f00656
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/04/2017
ms.author: edmaca
ms.openlocfilehash: cb9b35352d1cc9a78337448b1d6835875a212e08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-powershell"></a><span data-ttu-id="aa823-103">Introduzione ad Azure Data Lake Analytics con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="aa823-103">Get started with Azure Data Lake Analytics using Azure PowerShell</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="aa823-104">Informazioni su come toouse toocreate Azure PowerShell Azure Data Lake Analitica account e quindi inviare ed eseguire i processi di U-SQL.</span><span class="sxs-lookup"><span data-stu-id="aa823-104">Learn how toouse Azure PowerShell toocreate Azure Data Lake Analytics accounts and then submit and run U-SQL jobs.</span></span> <span data-ttu-id="aa823-105">Per altre informazioni su Data Lake Analytics, vedere [Panoramica di Azure Data Lake Analytics](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="aa823-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aa823-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="aa823-106">Prerequisites</span></span>

<span data-ttu-id="aa823-107">Prima di iniziare questa esercitazione, è necessario disporre di hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="aa823-107">Before you begin this tutorial, you must have hello following information:</span></span>

* <span data-ttu-id="aa823-108">Un **account di Azure Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="aa823-108">**An Azure Data Lake Analytics account**.</span></span> <span data-ttu-id="aa823-109">Vedere [Introduzione a Data Lake Analytics](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-get-started-portal).</span><span class="sxs-lookup"><span data-stu-id="aa823-109">See [Get started with Data Lake Analytics](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-get-started-portal).</span></span>
* <span data-ttu-id="aa823-110">**Workstation con Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="aa823-110">**A workstation with Azure PowerShell**.</span></span> <span data-ttu-id="aa823-111">Vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="aa823-111">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="aa823-112">Accedi tooAzure</span><span class="sxs-lookup"><span data-stu-id="aa823-112">Log in tooAzure</span></span>

<span data-ttu-id="aa823-113">Questa esercitazione presuppone che si abbia già familiarità con l'uso di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="aa823-113">This tutorial assumes you are already familiar with using Azure PowerShell.</span></span> <span data-ttu-id="aa823-114">In particolare, è necessario come tooknow toolog in tooAzure.</span><span class="sxs-lookup"><span data-stu-id="aa823-114">In particular, you need tooknow how toolog in tooAzure.</span></span> <span data-ttu-id="aa823-115">Vedere hello [Guida introduttiva di Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps) per assistenza.</span><span class="sxs-lookup"><span data-stu-id="aa823-115">See hello [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps) if you need help.</span></span>

<span data-ttu-id="aa823-116">toolog con un nome di sottoscrizione:</span><span class="sxs-lookup"><span data-stu-id="aa823-116">toolog in with a subscription name:</span></span>

```
Login-AzureRmAccount -SubscriptionName "ContosoSubscription"
```

<span data-ttu-id="aa823-117">Anziché il nome di sottoscrizione hello, è inoltre possibile utilizzare un toolog id sottoscrizione in:</span><span class="sxs-lookup"><span data-stu-id="aa823-117">Instead of hello subscription name, you can also use a subscription id toolog in:</span></span>

```
Login-AzureRmAccount -SubscriptionId "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
```

<span data-ttu-id="aa823-118">Se ha esito positivo, l'output di hello di questo comando sarà analogo hello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="aa823-118">If  successful, hello output of this command looks like hello following text:</span></span>

```
Environment           : AzureCloud
Account               : joe@contoso.com
TenantId              : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionId        : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionName      : ContosoSubscription
CurrentStorageAccount :
```

## <a name="preparing-for-hello-tutorial"></a><span data-ttu-id="aa823-119">Preparazione per l'esercitazione hello</span><span class="sxs-lookup"><span data-stu-id="aa823-119">Preparing for hello tutorial</span></span>

<span data-ttu-id="aa823-120">frammenti di codice PowerShell Hello in questa esercitazione usare questi toostore variabili queste informazioni:</span><span class="sxs-lookup"><span data-stu-id="aa823-120">hello PowerShell snippets in this tutorial use these variables toostore this information:</span></span>

```
$rg = "<ResourceGroupName>"
$adls = "<DataLakeStoreAccountName>"
$adla = "<DataLakeAnalyticsAccountName>"
$location = "East US 2"
```

## <a name="get-information-about-a-data-lake-analytics-account"></a><span data-ttu-id="aa823-121">Ottenere informazioni su un account Data Lake Analytics account</span><span class="sxs-lookup"><span data-stu-id="aa823-121">Get information about a Data Lake Analytics account</span></span>

```
Get-AdlAnalyticsAccount -ResourceGroupName $rg -Name $adla  
```

## <a name="submit-a-u-sql-job"></a><span data-ttu-id="aa823-122">Inviare un processo U-SQL</span><span class="sxs-lookup"><span data-stu-id="aa823-122">Submit a U-SQL job</span></span>

<span data-ttu-id="aa823-123">Creare uno script di PowerShell toohold variabile hello U-SQL.</span><span class="sxs-lookup"><span data-stu-id="aa823-123">Create a PowerShell variable toohold hello U-SQL script.</span></span>

```
$script = @"
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

"@
```

<span data-ttu-id="aa823-124">Inviare script hello.</span><span class="sxs-lookup"><span data-stu-id="aa823-124">Submit hello script.</span></span>

```
$job = Submit-AdlJob -AccountName $adla –Script $script
```

<span data-ttu-id="aa823-125">In alternativa, è possibile salvare script hello come un file e inviare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="aa823-125">Alternatively, you could save hello script as a file and submit with hello following command:</span></span>

```
$filename = "d:\test.usql"
$script | out-File $filename
$job = Submit-AdlJob -AccountName $adla –ScriptPath $filename
```


<span data-ttu-id="aa823-126">Ottenere lo stato di hello di un processo specifico.</span><span class="sxs-lookup"><span data-stu-id="aa823-126">Get hello status of a specific job.</span></span> <span data-ttu-id="aa823-127">Continuare a utilizzare questo cmdlet fino a visualizzare hello processo viene eseguito.</span><span class="sxs-lookup"><span data-stu-id="aa823-127">Keep using this cmdlet until you see hello job is done.</span></span>

```
$job = Get-AdlJob -AccountName $adla -JobId $job.JobId
```

<span data-ttu-id="aa823-128">Anziché chiamare Get AdlAnalyticsJob ripetutamente finché non termina un processo, è possibile utilizzare i cmdlet di attesa AdlJob hello.</span><span class="sxs-lookup"><span data-stu-id="aa823-128">Instead of calling Get-AdlAnalyticsJob over and over until a job finishes, you can use hello Wait-AdlJob cmdlet.</span></span>

```
Wait-AdlJob -Account $adla -JobId $job.JobId
```

<span data-ttu-id="aa823-129">Scaricare il file di output di hello.</span><span class="sxs-lookup"><span data-stu-id="aa823-129">Download hello output file.</span></span>

```
Export-AdlStoreItem -AccountName $adls -Path "/data.csv" -Destination "C:\data.csv"
```

## <a name="see-also"></a><span data-ttu-id="aa823-130">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="aa823-130">See also</span></span>
* <span data-ttu-id="aa823-131">toosee hello stesso esercitazione con altri strumenti, fare clic sui selettori di hello scheda nella parte superiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="aa823-131">toosee hello same tutorial using other tools, click hello tab selectors on hello top of hello page.</span></span>
* <span data-ttu-id="aa823-132">toolearn U-SQL, vedere [Guida introduttiva di Azure Data Lake Analitica U-SQL language](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="aa823-132">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="aa823-133">Per informazioni sulle attività di gestione, vedere [Gestire Azure Data Lake Analytics tramite il portale di Azure](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="aa823-133">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
