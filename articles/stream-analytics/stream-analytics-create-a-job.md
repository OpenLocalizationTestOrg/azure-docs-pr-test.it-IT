---
title: aaaHow toocreate un processo di elaborazione analitica dei dati per flusso Analitica | Documenti Microsoft
description: Creare un processo di elaborazione di analisi dei dati per Analisi di flusso | segmento del percorso di apprendimento.
keywords: elaborazione di analisi dei dati
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: e825fbcf-69e9-443f-b402-3b7a4568f415
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: d4a3c89d8862d59688d06a1719b063efa2ab1c93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-data-analytics-processing-job-for-stream-analytics"></a><span data-ttu-id="46dea-104">Come toocreate processo un'elaborazione analitica dei dati per flusso Analitica</span><span class="sxs-lookup"><span data-stu-id="46dea-104">How toocreate a data analytics processing job for Stream Analytics</span></span>
<span data-ttu-id="46dea-105">risorsa di primo livello Hello in Analitica di flusso di Azure è un processo di flusso Analitica.</span><span class="sxs-lookup"><span data-stu-id="46dea-105">hello top-level resource in Azure Stream Analytics is a Stream Analytics Job.</span></span>  <span data-ttu-id="46dea-106">È costituito da uno o più input di origini dati, una query che esprime la trasformazione dei dati hello e una o più destinazioni di output che i risultati vengono scritti.</span><span class="sxs-lookup"><span data-stu-id="46dea-106">It consists of one or more input data sources, a query expressing hello data transformation, and one or more output targets that results are written to.</span></span> <span data-ttu-id="46dea-107">Insieme questi abilitare analitica di hello utente tooperform dati per flusso di dati degli scenari di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="46dea-107">Together these enable hello user tooperform data analytics processing for streaming data scenarios.</span></span>

<span data-ttu-id="46dea-108">toostart tramite flusso Analitica, iniziare creando un nuovo processo di flusso Analitica.</span><span class="sxs-lookup"><span data-stu-id="46dea-108">toostart using Stream Analytics, begin by creating a new Stream Analytics job.</span></span>  <span data-ttu-id="46dea-109">Si noti che l'azione non ha costi di fatturazione fino a quando non viene avviato il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="46dea-109">Note this action has no billing implications until hello job is started.</span></span>

1. <span data-ttu-id="46dea-110">Accedi a hello online [portale di Azure classico](http://manage.windowsazure.com) o hello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="46dea-110">Sign in on hello online [Azure classic portal](http://manage.windowsazure.com) or hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="46dea-111">Nel portale di hello: **fare clic su nuovo**, quindi fare clic su **Data Services** o **dati Analitica** a seconda del portale e quindi fare clic su **Azure flusso Analitica** o **flusso Analitica** e quindi **creazione rapida**.</span><span class="sxs-lookup"><span data-stu-id="46dea-111">In hello portal: **Click New**, then click **Data Services** or **Data Analytics** depending on your portal and then click **Azure Stream Analytics** or **Stream Analytics** and then **Quick Create**.</span></span>
   
   ![Procedura guidata del processo di elaborazione di analisi dei dati](./media/stream-analytics-create-a-job/1-stream-analytics-create-a-job.png)  
   
   ![Creare un processo di elaborazione di analisi dei dati](./media/stream-analytics-create-a-job/4-stream-analytics-create-a-job.png)  
3. <span data-ttu-id="46dea-114">Specificare hello configurazione desiderata per il processo di flusso Analitica hello.</span><span class="sxs-lookup"><span data-stu-id="46dea-114">Specify hello desired configuration for hello Stream Analytics job.</span></span>
   
   * <span data-ttu-id="46dea-115">In hello **nome del processo** , immettere un nome tooidentify hello Analitica di flusso del processo.</span><span class="sxs-lookup"><span data-stu-id="46dea-115">In hello **Job Name** box, enter a name tooidentify hello Stream Analytics job.</span></span> <span data-ttu-id="46dea-116">Quando hello **nome del processo** viene convalidato, viene visualizzato un segno di spunta verde nella casella nome del processo di hello.</span><span class="sxs-lookup"><span data-stu-id="46dea-116">When hello **Job Name** is validated, a green check mark appears in hello Job Name box.</span></span> <span data-ttu-id="46dea-117">Hello **nome del processo** possono contenere solo caratteri alfanumerici e hello '-' caratteri e deve essere compresa tra 3 e 63 caratteri.</span><span class="sxs-lookup"><span data-stu-id="46dea-117">hello **Job Name** may contain only alphanumeric characters and hello '-' character, and must be between 3 and 63 characters.</span></span>
   * <span data-ttu-id="46dea-118">Utilizzare **area** nel portale di Azure hello o **percorso** in hello Azure toospecify portale hello posizione geografica in cui si desidera che il processo di hello toorun.</span><span class="sxs-lookup"><span data-stu-id="46dea-118">Use **Region** in hello Azure portal or **Location** in hello Azure portal toospecify hello geographic location where you want toorun hello job.</span></span>
   * <span data-ttu-id="46dea-119">Se tramite hello portale di Azure, selezionare o creare un toouse di account di archiviazione come hello **Account di archiviazione di monitoraggio regionale**.</span><span class="sxs-lookup"><span data-stu-id="46dea-119">If using hello Azure portal, select or create a storage account toouse as hello **Regional Monitoring Storage Account**.</span></span> <span data-ttu-id="46dea-120">Questo account di archiviazione è toostore utilizzati dati di monitoraggio di tutti i processi di flusso Analitica in esecuzione in questa area.</span><span class="sxs-lookup"><span data-stu-id="46dea-120">This storage account is used toostore monitoring data for all Stream Analytics jobs running in this region.</span></span>
   * <span data-ttu-id="46dea-121">Se tramite hello portale di Azure, specificare un nuovo o esistente **gruppo di risorse** toohold relative risorse per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="46dea-121">If using hello Azure portal, specify a new or existing **Resource Group** toohold related resources for your application.</span></span>
4. <span data-ttu-id="46dea-122">Dopo aver configurate le opzioni di hello nuovo flusso Analitica processo, fare clic su **Crea processo di flusso Analitica**.</span><span class="sxs-lookup"><span data-stu-id="46dea-122">Once hello new Stream Analytics job options are configured, click **Create Stream Analytics Job**.</span></span> <span data-ttu-id="46dea-123">Può richiedere alcuni minuti per hello Analitica flusso processo toobe creato.</span><span class="sxs-lookup"><span data-stu-id="46dea-123">It can take a few minutes for hello Stream Analytics job toobe created.</span></span> <span data-ttu-id="46dea-124">stato hello toocheck, è possibile monitorare lo stato di avanzamento hello nell'hub notifiche hello.</span><span class="sxs-lookup"><span data-stu-id="46dea-124">toocheck hello status, you can monitor hello progress in hello Notifications hub.</span></span>
   
   ![Processo di elaborazione di analisi dei dati, hub di notifica](./media/stream-analytics-create-a-job/2-stream-analytics-create-a-job.png)  
   
   ![Portale di Azure, processo di elaborazione di analisi dei dati, creare un processo](./media/stream-analytics-create-a-job/5-stream-analytics-create-a-job.png)  
5. <span data-ttu-id="46dea-127">il nuovo processo di Hello mostrerà lo stato di **creato**.</span><span class="sxs-lookup"><span data-stu-id="46dea-127">hello new job will show a status of **Created**.</span></span> <span data-ttu-id="46dea-128">Si noti che hello **avviare** pulsante è disabilitato.</span><span class="sxs-lookup"><span data-stu-id="46dea-128">Notice that hello **Start** button is disabled.</span></span> <span data-ttu-id="46dea-129">Prima di iniziare il processo di hello, configurare hello processo input, query e output.</span><span class="sxs-lookup"><span data-stu-id="46dea-129">Configure hello job input, query, and output before you start hello job.</span></span>
   
   ![Elaborazione dell'analisi dei dati, stato processo](./media/stream-analytics-create-a-job/3-stream-analytics-create-a-job.png)  
   
   ![Portale di Azure, elaborazione dell'analisi dei dati, stato processo](./media/stream-analytics-create-a-job/6-stream-analytics-create-a-job.png)  

## <a name="get-help"></a><span data-ttu-id="46dea-132">Ottenere aiuto</span><span class="sxs-lookup"><span data-stu-id="46dea-132">Get help</span></span>
<span data-ttu-id="46dea-133">Per assistenza, provare il [Forum di Analisi di flusso di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="46dea-133">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="46dea-134">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="46dea-134">Next steps</span></span>
* [<span data-ttu-id="46dea-135">Introduzione tooAzure flusso Analitica</span><span class="sxs-lookup"><span data-stu-id="46dea-135">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="46dea-136">Introduzione all'uso di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="46dea-136">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="46dea-137">Ridimensionare i processi di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="46dea-137">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="46dea-138">Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="46dea-138">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="46dea-139">Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="46dea-139">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

