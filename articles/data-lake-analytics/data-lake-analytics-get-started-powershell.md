---
title: Introduzione ad Azure Data Lake Analytics con Azure PowerShell | Documentazione Microsoft
description: 'Usare Azure PowerShell per creare un account di Data Lake Analytics, definire un processo di Data Lake Analytics con U-SQL e inviare il processo. '
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
ms.openlocfilehash: 4f73e27c733edae658d1ea3bdabe48076328279b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-powershell"></a><span data-ttu-id="65cba-103">Introduzione ad Azure Data Lake Analytics con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="65cba-103">Get started with Azure Data Lake Analytics using Azure PowerShell</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="65cba-104">Questo articolo illustra come usare Azure PowerShell per creare account Azure Data Lake Analytics e quindi inviare ed eseguire processi U-SQL.</span><span class="sxs-lookup"><span data-stu-id="65cba-104">Learn how to use Azure PowerShell to create Azure Data Lake Analytics accounts and then submit and run U-SQL jobs.</span></span> <span data-ttu-id="65cba-105">Per altre informazioni su Data Lake Analytics, vedere [Panoramica di Azure Data Lake Analytics](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="65cba-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="65cba-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="65cba-106">Prerequisites</span></span>

<span data-ttu-id="65cba-107">Prima di iniziare questa esercitazione sono necessari le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="65cba-107">Before you begin this tutorial, you must have the following information:</span></span>

* <span data-ttu-id="65cba-108">Un **account di Azure Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="65cba-108">**An Azure Data Lake Analytics account**.</span></span> <span data-ttu-id="65cba-109">Vedere [Introduzione a Data Lake Analytics](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-get-started-portal).</span><span class="sxs-lookup"><span data-stu-id="65cba-109">See [Get started with Data Lake Analytics](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-get-started-portal).</span></span>
* <span data-ttu-id="65cba-110">**Workstation con Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="65cba-110">**A workstation with Azure PowerShell**.</span></span> <span data-ttu-id="65cba-111">Vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="65cba-111">See [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="65cba-112">Accedere ad Azure</span><span class="sxs-lookup"><span data-stu-id="65cba-112">Log in to Azure</span></span>

<span data-ttu-id="65cba-113">Questa esercitazione presuppone che si abbia già familiarità con l'uso di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="65cba-113">This tutorial assumes you are already familiar with using Azure PowerShell.</span></span> <span data-ttu-id="65cba-114">In particolare, è necessario sapere come accedere ad Azure.</span><span class="sxs-lookup"><span data-stu-id="65cba-114">In particular, you need to know how to log in to Azure.</span></span> <span data-ttu-id="65cba-115">Per istruzioni, vedere [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps) (Introduzione ad Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="65cba-115">See the [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps) if you need help.</span></span>

<span data-ttu-id="65cba-116">Per accedere con un nome di sottoscrizione:</span><span class="sxs-lookup"><span data-stu-id="65cba-116">To log in with a subscription name:</span></span>

```
Login-AzureRmAccount -SubscriptionName "ContosoSubscription"
```

<span data-ttu-id="65cba-117">Invece del nome della sottoscrizione, è anche possibile usare un ID sottoscrizione per l'accesso:</span><span class="sxs-lookup"><span data-stu-id="65cba-117">Instead of the subscription name, you can also use a subscription id to log in:</span></span>

```
Login-AzureRmAccount -SubscriptionId "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
```

<span data-ttu-id="65cba-118">In caso di esito positivo, l'output di questo comando è simile al testo seguente:</span><span class="sxs-lookup"><span data-stu-id="65cba-118">If  successful, the output of this command looks like the following text:</span></span>

```
Environment           : AzureCloud
Account               : joe@contoso.com
TenantId              : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionId        : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionName      : ContosoSubscription
CurrentStorageAccount :
```

## <a name="preparing-for-the-tutorial"></a><span data-ttu-id="65cba-119">Preparazione dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="65cba-119">Preparing for the tutorial</span></span>

<span data-ttu-id="65cba-120">I frammenti di codice di PowerShell in questa esercitazione usano le variabili seguenti per archiviare queste informazioni:</span><span class="sxs-lookup"><span data-stu-id="65cba-120">The PowerShell snippets in this tutorial use these variables to store this information:</span></span>

```
$rg = "<ResourceGroupName>"
$adls = "<DataLakeStoreAccountName>"
$adla = "<DataLakeAnalyticsAccountName>"
$location = "East US 2"
```

## <a name="get-information-about-a-data-lake-analytics-account"></a><span data-ttu-id="65cba-121">Ottenere informazioni su un account Data Lake Analytics account</span><span class="sxs-lookup"><span data-stu-id="65cba-121">Get information about a Data Lake Analytics account</span></span>

```
Get-AdlAnalyticsAccount -ResourceGroupName $rg -Name $adla  
```

## <a name="submit-a-u-sql-job"></a><span data-ttu-id="65cba-122">Inviare un processo U-SQL</span><span class="sxs-lookup"><span data-stu-id="65cba-122">Submit a U-SQL job</span></span>

<span data-ttu-id="65cba-123">Creare una variabile di PowerShell per contenere lo script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="65cba-123">Create a PowerShell variable to hold the U-SQL script.</span></span>

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
    TO "/data.csv"
    USING Outputters.Csv();

"@
```

<span data-ttu-id="65cba-124">Inviare lo script.</span><span class="sxs-lookup"><span data-stu-id="65cba-124">Submit the script.</span></span>

```
$job = Submit-AdlJob -AccountName $adla –Script $script
```

<span data-ttu-id="65cba-125">In alternativa, è possibile salvare lo script come file ed eseguire l'invio con il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="65cba-125">Alternatively, you could save the script as a file and submit with the following command:</span></span>

```
$filename = "d:\test.usql"
$script | out-File $filename
$job = Submit-AdlJob -AccountName $adla –ScriptPath $filename
```


<span data-ttu-id="65cba-126">Ottenere lo stato di un processo specifico.</span><span class="sxs-lookup"><span data-stu-id="65cba-126">Get the status of a specific job.</span></span> <span data-ttu-id="65cba-127">Continuare a usare questo cmdlet fino al completamento del processo.</span><span class="sxs-lookup"><span data-stu-id="65cba-127">Keep using this cmdlet until you see the job is done.</span></span>

```
$job = Get-AdlJob -AccountName $adla -JobId $job.JobId
```

<span data-ttu-id="65cba-128">Invece di continuare a chiamare Get-AdlAnalyticsJob fino al termine di un processo, è possibile usare il cmdlet Wait-AdlJob.</span><span class="sxs-lookup"><span data-stu-id="65cba-128">Instead of calling Get-AdlAnalyticsJob over and over until a job finishes, you can use the Wait-AdlJob cmdlet.</span></span>

```
Wait-AdlJob -Account $adla -JobId $job.JobId
```

<span data-ttu-id="65cba-129">Scaricare il file di output.</span><span class="sxs-lookup"><span data-stu-id="65cba-129">Download the output file.</span></span>

```
Export-AdlStoreItem -AccountName $adls -Path "/data.csv" -Destination "C:\data.csv"
```

## <a name="see-also"></a><span data-ttu-id="65cba-130">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="65cba-130">See also</span></span>
* <span data-ttu-id="65cba-131">Per visualizzare la stessa esercitazione usando altri strumenti, scegliere i selettori di scheda nella parte superiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="65cba-131">To see the same tutorial using other tools, click the tab selectors on the top of the page.</span></span>
* <span data-ttu-id="65cba-132">Per informazioni su U-SQL, vedere [Introduzione al linguaggio U-SQL di Azure Data Lake Analytics](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="65cba-132">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="65cba-133">Per informazioni sulle attività di gestione, vedere [Gestire Azure Data Lake Analytics tramite il portale di Azure](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="65cba-133">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
