---
title: Risolvere i problemi dei processi di Azure Data Lake Analytics con il portale di Azure | Documentazione Microsoft
description: 'Informazioni su come usare il portale di Azure per risolvere i problemi relativi ai processi di Analisi Data Lake. '
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: b7066d81-3142-474f-8a34-32b0b39656dc
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: b9c7453cc0a94f70d0098ed83e5f127832065a62
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-azure-data-lake-analytics-jobs-using-azure-portal"></a><span data-ttu-id="a8c60-103">Risolvere i problemi dei processi di Analisi di Azure Data Lake mediante il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="a8c60-103">Troubleshoot Azure Data Lake Analytics jobs using Azure Portal</span></span>
<span data-ttu-id="a8c60-104">Informazioni su come usare il portale di Azure per risolvere i problemi relativi ai processi di Analisi Data Lake.</span><span class="sxs-lookup"><span data-stu-id="a8c60-104">Learn how to use the Azure Portal to troubleshoot Data Lake Analytics jobs.</span></span>

<span data-ttu-id="a8c60-105">In questa esercitazione verrà impostato un problema relativo a un file di origine mancante e verrà usato il portale di Azure per risolvere il problema.</span><span class="sxs-lookup"><span data-stu-id="a8c60-105">In this tutorial, you will setup a missing source file problem, and use the Azure Portal to troubleshoot the problem.</span></span>

## <a name="submit-a-data-lake-analytics-job"></a><span data-ttu-id="a8c60-106">Inviare un processo di Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="a8c60-106">Submit a Data Lake Analytics job</span></span>

<span data-ttu-id="a8c60-107">Inviare il processo U-SQL seguente:</span><span class="sxs-lookup"><span data-stu-id="a8c60-107">Submit the following U-SQL job:</span></span>

```
@searchlog =
   EXTRACT UserId          int,
           Start           DateTime,
           Region          string,
           Query           string,
           Duration        int?,
           Urls            string,
           ClickedUrls     string
   FROM "/Samples/Data/SearchLog.tsv1"
   USING Extractors.Tsv();

OUTPUT @searchlog   
   TO "/output/SearchLog-from-adls.csv"
   USING Outputters.Csv();
```
    
<span data-ttu-id="a8c60-108">Il file di origine definito nello script è **/Samples/Data/SearchLog.tsv1**, ma dovrebbe essere modificato in **/Samples/Data/SearchLog.tsv**.</span><span class="sxs-lookup"><span data-stu-id="a8c60-108">The source file defined in the script is **/Samples/Data/SearchLog.tsv1**, where it should be **/Samples/Data/SearchLog.tsv**.</span></span>


## <a name="troubleshoot-the-job"></a><span data-ttu-id="a8c60-109">Risolvere i problemi relativi al processo</span><span class="sxs-lookup"><span data-stu-id="a8c60-109">Troubleshoot the job</span></span>

<span data-ttu-id="a8c60-110">**Per visualizzare tutti i processi**</span><span class="sxs-lookup"><span data-stu-id="a8c60-110">**To see all the jobs**</span></span>

1. <span data-ttu-id="a8c60-111">Nel portale di Azure fare clic su **Microsoft Azure** nell'angolo superiore sinistro.</span><span class="sxs-lookup"><span data-stu-id="a8c60-111">From the Azure portal, click **Microsoft Azure** in the upper left corner.</span></span>
2. <span data-ttu-id="a8c60-112">Fare clic nel riquadro contenente il nome dell'account di Analisi Data Lake personale.</span><span class="sxs-lookup"><span data-stu-id="a8c60-112">Click the tile with your Data Lake Analytics account name.</span></span>  <span data-ttu-id="a8c60-113">Viene visualizzato il riepilogo del processo nel riquadro **Gestione processo** .</span><span class="sxs-lookup"><span data-stu-id="a8c60-113">The job summary is shown on the **Job Management** tile.</span></span>

    ![Azure Data Lake Analytics - Gestione dei processi](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-job-management.png)

    <span data-ttu-id="a8c60-115">Nel riquadro Gestione processo viene fornito un riepilogo dello stato del processo.</span><span class="sxs-lookup"><span data-stu-id="a8c60-115">The job Management gives you a glance of the job status.</span></span> <span data-ttu-id="a8c60-116">Si noti che è presente un processo non riuscito.</span><span class="sxs-lookup"><span data-stu-id="a8c60-116">Notice there is a failed job.</span></span>
3. <span data-ttu-id="a8c60-117">Fare clic nel riquadro **Gestione processo** per visualizzare i processi.</span><span class="sxs-lookup"><span data-stu-id="a8c60-117">Click the **Job Management** tile to see the jobs.</span></span> <span data-ttu-id="a8c60-118">I processi sono classificati in base agli stati **In esecuzione**, **In coda** e **Terminato**.</span><span class="sxs-lookup"><span data-stu-id="a8c60-118">The jobs are categorized in **Running**, **Queued**, and **Ended**.</span></span> <span data-ttu-id="a8c60-119">Il processo non riuscito verrà visualizzato nella sezione **Terminato**</span><span class="sxs-lookup"><span data-stu-id="a8c60-119">You shall see your failed job in the **Ended** section.</span></span> <span data-ttu-id="a8c60-120">e occuperà la prima posizione nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="a8c60-120">It shall be first one in the list.</span></span> <span data-ttu-id="a8c60-121">Quando sono presenti molti processi, è possibile fare clic su **Filtro** per semplificare l'individuazione dei processi.</span><span class="sxs-lookup"><span data-stu-id="a8c60-121">When you have a lot of jobs, you can click **Filter** to help you to locate jobs.</span></span>

    ![Azure Data Lake Analytics - Filtrare i processi](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-filter-jobs.png)
4. <span data-ttu-id="a8c60-123">Fare clic sul processo non riuscito nell'elenco per aprire i relativi dettagli in un nuovo pannello:</span><span class="sxs-lookup"><span data-stu-id="a8c60-123">Click the failed job from the list to open the job details in a new blade:</span></span>

    ![Azure Data Lake Analytics - Processo non riuscito](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job.png)

    <span data-ttu-id="a8c60-125">Si noti il pulsante **Invia di nuovo** .</span><span class="sxs-lookup"><span data-stu-id="a8c60-125">Notice the **Resubmit** button.</span></span> <span data-ttu-id="a8c60-126">Dopo aver risolto il problema, è possibile inviare nuovamente il processo.</span><span class="sxs-lookup"><span data-stu-id="a8c60-126">After you fix the problem, you can resubmit the job.</span></span>
5. <span data-ttu-id="a8c60-127">Fare clic sulla parte evidenziata nella schermata precedente per aprire i dettagli dell'errore.</span><span class="sxs-lookup"><span data-stu-id="a8c60-127">Click highlighted part from the previous screenshot to open the error details.</span></span>  <span data-ttu-id="a8c60-128">Verrà visualizzato qualcosa di simile a quanto segue:</span><span class="sxs-lookup"><span data-stu-id="a8c60-128">You shall see something like:</span></span>

    ![Azure Data Lake Analytics - Dettagli del processo non riuscito](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job-details.png)

    <span data-ttu-id="a8c60-130">Indica che la cartella di origine non è disponibile.</span><span class="sxs-lookup"><span data-stu-id="a8c60-130">It tells you the source folder is not found.</span></span>
6. <span data-ttu-id="a8c60-131">Fare clic su **Duplicate Script**.</span><span class="sxs-lookup"><span data-stu-id="a8c60-131">Click **Duplicate Script**.</span></span>
7. <span data-ttu-id="a8c60-132">Aggiornare il percorso nella riga **FROM** impostando il seguente percorso:</span><span class="sxs-lookup"><span data-stu-id="a8c60-132">Update the **FROM** path to the following:</span></span>

    <span data-ttu-id="a8c60-133">"/Samples/Data/SearchLog.tsv"</span><span class="sxs-lookup"><span data-stu-id="a8c60-133">"/Samples/Data/SearchLog.tsv"</span></span>
8. <span data-ttu-id="a8c60-134">Fare clic su **Submit Job**.</span><span class="sxs-lookup"><span data-stu-id="a8c60-134">Click **Submit Job**.</span></span>

## <a name="see-also"></a><span data-ttu-id="a8c60-135">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="a8c60-135">See also</span></span>
* [<span data-ttu-id="a8c60-136">Panoramica di Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="a8c60-136">Azure Data Lake Analytics overview</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="a8c60-137">Introduzione ad Azure Data Lake Analytics con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a8c60-137">Get started with Azure Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="a8c60-138">Introduzione ad Azure Data Lake Analytics e U-SQL con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a8c60-138">Get started with Azure Data Lake Analytics and U-SQL using Visual Studio</span></span>](data-lake-analytics-u-sql-get-started.md)
* [<span data-ttu-id="a8c60-139">Gestire Analisi di Azure Data Lake tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="a8c60-139">Manage Azure Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-manage-use-portal.md)
