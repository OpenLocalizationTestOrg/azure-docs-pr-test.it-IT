---
title: i processi di Azure Data Lake Analitica aaaTroubleshoot tramite il portale di Azure | Documenti Microsoft
description: 'Informazioni su come toouse hello i processi di Data Lake Analitica tootroubleshoot portale di Azure. '
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
ms.openlocfilehash: e810d56bab8f1a8254721ec9906bb6a4508dc22a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-data-lake-analytics-jobs-using-azure-portal"></a><span data-ttu-id="b78c7-103">Risolvere i problemi dei processi di Analisi di Azure Data Lake mediante il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="b78c7-103">Troubleshoot Azure Data Lake Analytics jobs using Azure Portal</span></span>
<span data-ttu-id="b78c7-104">Informazioni su come toouse hello i processi di Data Lake Analitica tootroubleshoot portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b78c7-104">Learn how toouse hello Azure Portal tootroubleshoot Data Lake Analytics jobs.</span></span>

<span data-ttu-id="b78c7-105">In questa esercitazione, è un problema di file di origine mancanti del programma di installazione e utilizzare problema hello tootroubleshoot di hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b78c7-105">In this tutorial, you will setup a missing source file problem, and use hello Azure Portal tootroubleshoot hello problem.</span></span>

## <a name="submit-a-data-lake-analytics-job"></a><span data-ttu-id="b78c7-106">Inviare un processo di Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="b78c7-106">Submit a Data Lake Analytics job</span></span>

<span data-ttu-id="b78c7-107">Inviare hello processo U-SQL seguente:</span><span class="sxs-lookup"><span data-stu-id="b78c7-107">Submit hello following U-SQL job:</span></span>

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
   too"/output/SearchLog-from-adls.csv"
   USING Outputters.Csv();
```
    
<span data-ttu-id="b78c7-108">Hello file di origine definiti nello script hello è **/Samples/Data/SearchLog.tsv1**, in cui deve essere **/Samples/Data/SearchLog.tsv**.</span><span class="sxs-lookup"><span data-stu-id="b78c7-108">hello source file defined in hello script is **/Samples/Data/SearchLog.tsv1**, where it should be **/Samples/Data/SearchLog.tsv**.</span></span>


## <a name="troubleshoot-hello-job"></a><span data-ttu-id="b78c7-109">Risoluzione dei problemi hello processo</span><span class="sxs-lookup"><span data-stu-id="b78c7-109">Troubleshoot hello job</span></span>

<span data-ttu-id="b78c7-110">**toosee tutti i processi di hello**</span><span class="sxs-lookup"><span data-stu-id="b78c7-110">**toosee all hello jobs**</span></span>

1. <span data-ttu-id="b78c7-111">Dal portale di Azure hello, fare clic su **Microsoft Azure** nell'angolo superiore sinistro di hello.</span><span class="sxs-lookup"><span data-stu-id="b78c7-111">From hello Azure portal, click **Microsoft Azure** in hello upper left corner.</span></span>
2. <span data-ttu-id="b78c7-112">Fare clic sul riquadro hello con il nome dell'account Data Lake Analitica.</span><span class="sxs-lookup"><span data-stu-id="b78c7-112">Click hello tile with your Data Lake Analytics account name.</span></span>  <span data-ttu-id="b78c7-113">riepilogo dei processi Hello è mostrato sul hello **gestione dei processi** riquadro.</span><span class="sxs-lookup"><span data-stu-id="b78c7-113">hello job summary is shown on hello **Job Management** tile.</span></span>

    ![Azure Data Lake Analytics - Gestione dei processi](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-job-management.png)

    <span data-ttu-id="b78c7-115">il processo di Hello Management offre immediatamente hello lo stato del processo.</span><span class="sxs-lookup"><span data-stu-id="b78c7-115">hello job Management gives you a glance of hello job status.</span></span> <span data-ttu-id="b78c7-116">Si noti che è presente un processo non riuscito.</span><span class="sxs-lookup"><span data-stu-id="b78c7-116">Notice there is a failed job.</span></span>
3. <span data-ttu-id="b78c7-117">Fare clic su hello **gestione dei processi** riquadro processi hello toosee.</span><span class="sxs-lookup"><span data-stu-id="b78c7-117">Click hello **Job Management** tile toosee hello jobs.</span></span> <span data-ttu-id="b78c7-118">i processi di Hello sono classificati in **esecuzione**, **in coda**, e **finito**.</span><span class="sxs-lookup"><span data-stu-id="b78c7-118">hello jobs are categorized in **Running**, **Queued**, and **Ended**.</span></span> <span data-ttu-id="b78c7-119">Verrà visualizzato il processo non riuscito in hello **finito** sezione.</span><span class="sxs-lookup"><span data-stu-id="b78c7-119">You shall see your failed job in hello **Ended** section.</span></span> <span data-ttu-id="b78c7-120">Deve essere primo elenco hello.</span><span class="sxs-lookup"><span data-stu-id="b78c7-120">It shall be first one in hello list.</span></span> <span data-ttu-id="b78c7-121">Quando si dispone di molti processi, è possibile fare clic su **filtro** toohelp si toolocate processi.</span><span class="sxs-lookup"><span data-stu-id="b78c7-121">When you have a lot of jobs, you can click **Filter** toohelp you toolocate jobs.</span></span>

    ![Azure Data Lake Analytics - Filtrare i processi](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-filter-jobs.png)
4. <span data-ttu-id="b78c7-123">Fare clic su hello processo non riuscito da hello elenco tooopen hello i dettagli dei processi in un nuovo pannello:</span><span class="sxs-lookup"><span data-stu-id="b78c7-123">Click hello failed job from hello list tooopen hello job details in a new blade:</span></span>

    ![Azure Data Lake Analytics - Processo non riuscito](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job.png)

    <span data-ttu-id="b78c7-125">Hello preavviso **inviare di nuovo** pulsante.</span><span class="sxs-lookup"><span data-stu-id="b78c7-125">Notice hello **Resubmit** button.</span></span> <span data-ttu-id="b78c7-126">Dopo aver risolto il problema di hello, è possibile inviare di nuovo il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="b78c7-126">After you fix hello problem, you can resubmit hello job.</span></span>
5. <span data-ttu-id="b78c7-127">Fare clic sulla parte evidenziata da hello precedente schermata tooopen hello i dettagli dell'errore.</span><span class="sxs-lookup"><span data-stu-id="b78c7-127">Click highlighted part from hello previous screenshot tooopen hello error details.</span></span>  <span data-ttu-id="b78c7-128">Verrà visualizzato qualcosa di simile a quanto segue:</span><span class="sxs-lookup"><span data-stu-id="b78c7-128">You shall see something like:</span></span>

    ![Azure Data Lake Analytics - Dettagli del processo non riuscito](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job-details.png)

    <span data-ttu-id="b78c7-130">Indica la cartella di origine hello non viene trovata.</span><span class="sxs-lookup"><span data-stu-id="b78c7-130">It tells you hello source folder is not found.</span></span>
6. <span data-ttu-id="b78c7-131">Fare clic su **Duplicate Script**.</span><span class="sxs-lookup"><span data-stu-id="b78c7-131">Click **Duplicate Script**.</span></span>
7. <span data-ttu-id="b78c7-132">Hello aggiornamento **FROM** seguente toohello percorso:</span><span class="sxs-lookup"><span data-stu-id="b78c7-132">Update hello **FROM** path toohello following:</span></span>

    <span data-ttu-id="b78c7-133">"/Samples/Data/SearchLog.tsv"</span><span class="sxs-lookup"><span data-stu-id="b78c7-133">"/Samples/Data/SearchLog.tsv"</span></span>
8. <span data-ttu-id="b78c7-134">Fare clic su **Submit Job**.</span><span class="sxs-lookup"><span data-stu-id="b78c7-134">Click **Submit Job**.</span></span>

## <a name="see-also"></a><span data-ttu-id="b78c7-135">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="b78c7-135">See also</span></span>
* [<span data-ttu-id="b78c7-136">Panoramica di Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="b78c7-136">Azure Data Lake Analytics overview</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="b78c7-137">Introduzione ad Azure Data Lake Analytics con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b78c7-137">Get started with Azure Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="b78c7-138">Introduzione ad Azure Data Lake Analytics e U-SQL con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b78c7-138">Get started with Azure Data Lake Analytics and U-SQL using Visual Studio</span></span>](data-lake-analytics-u-sql-get-started.md)
* [<span data-ttu-id="b78c7-139">Gestire Analisi di Azure Data Lake tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="b78c7-139">Manage Azure Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-manage-use-portal.md)
