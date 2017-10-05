---
title: Come creare un processo di elaborazione di analisi dei dati per Analisi di flusso | Documentazione Microsoft
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
ms.openlocfilehash: 05fdf1e20efd129cdfc27e1d37bc9e124edf5dcd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-create-a-data-analytics-processing-job-for-stream-analytics"></a><span data-ttu-id="863c5-104">Come creare un processo di elaborazione di analisi dei dati per Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="863c5-104">How to create a data analytics processing job for Stream Analytics</span></span>
<span data-ttu-id="863c5-105">La risorsa di livello principale nell’analisi di flusso di Azure è il processo di analisi del flusso.</span><span class="sxs-lookup"><span data-stu-id="863c5-105">The top-level resource in Azure Stream Analytics is a Stream Analytics Job.</span></span>  <span data-ttu-id="863c5-106">È costituito da una o più origini dati di input, una query che esprime la trasformazione dei dati e uno o più destinazioni di output in cui vengono scritti i risultati.</span><span class="sxs-lookup"><span data-stu-id="863c5-106">It consists of one or more input data sources, a query expressing the data transformation, and one or more output targets that results are written to.</span></span> <span data-ttu-id="863c5-107">Insieme questi consentono all'utente di eseguire elaborazioni di analisi dei dati per scenari di flussi di dati.</span><span class="sxs-lookup"><span data-stu-id="863c5-107">Together these enable the user to perform data analytics processing for streaming data scenarios.</span></span>

<span data-ttu-id="863c5-108">Per iniziare a usare Analisi di flusso, creare un nuovo processo di Analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="863c5-108">To start using Stream Analytics, begin by creating a new Stream Analytics job.</span></span>  <span data-ttu-id="863c5-109">Si noti che questa azione non ha implicazioni sulla fatturazione fino a quando il processo non viene avviato.</span><span class="sxs-lookup"><span data-stu-id="863c5-109">Note this action has no billing implications until the job is started.</span></span>

1. <span data-ttu-id="863c5-110">Accedere al [portale di Azure classico](http://manage.windowsazure.com) online o al [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="863c5-110">Sign in on the online [Azure classic portal](http://manage.windowsazure.com) or the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="863c5-111">Nel portale: **fare clic su Nuovo**, fare clic su **Servizi dati** o **Analisi dei dati** a seconda del portale, fare clic su **Analisi di flusso di Azure** o **Analisi di flusso** e quindi su **Creazione rapida**.</span><span class="sxs-lookup"><span data-stu-id="863c5-111">In the portal: **Click New**, then click **Data Services** or **Data Analytics** depending on your portal and then click **Azure Stream Analytics** or **Stream Analytics** and then **Quick Create**.</span></span>
   
   ![Procedura guidata del processo di elaborazione di analisi dei dati](./media/stream-analytics-create-a-job/1-stream-analytics-create-a-job.png)  
   
   ![Creare un processo di elaborazione di analisi dei dati](./media/stream-analytics-create-a-job/4-stream-analytics-create-a-job.png)  
3. <span data-ttu-id="863c5-114">Specificare la configurazione desiderata per il processo di analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="863c5-114">Specify the desired configuration for the Stream Analytics job.</span></span>
   
   * <span data-ttu-id="863c5-115">Nella casella **Nome processo** immettere un nome per identificare il processo di Analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="863c5-115">In the **Job Name** box, enter a name to identify the Stream Analytics job.</span></span> <span data-ttu-id="863c5-116">Quando il **Nome processo** viene convalidato, appare un segno di spunta verde nella relativa casella.</span><span class="sxs-lookup"><span data-stu-id="863c5-116">When the **Job Name** is validated, a green check mark appears in the Job Name box.</span></span> <span data-ttu-id="863c5-117">Il **Nome processo** può contenere solo caratteri alfanumerici e il carattere '-' e deve avere una lunghezza compresa tra 3 e 63 caratteri.</span><span class="sxs-lookup"><span data-stu-id="863c5-117">The **Job Name** may contain only alphanumeric characters and the '-' character, and must be between 3 and 63 characters.</span></span>
   * <span data-ttu-id="863c5-118">Usare **Area** o **Posizione** nel portale di Azure per specificare la posizione geografica in cui si intende eseguire il processo.</span><span class="sxs-lookup"><span data-stu-id="863c5-118">Use **Region** in the Azure portal or **Location** in the Azure portal to specify the geographic location where you want to run the job.</span></span>
   * <span data-ttu-id="863c5-119">Se si usa il portale di Azure, selezionare o creare un account di archiviazione da usare come **Account di archiviazione di monitoraggio regionale**.</span><span class="sxs-lookup"><span data-stu-id="863c5-119">If using the Azure portal, select or create a storage account to use as the **Regional Monitoring Storage Account**.</span></span> <span data-ttu-id="863c5-120">Questo account di archiviazione viene utilizzato per archiviare i dati di monitoraggio per tutti i processi di Analisi del flusso in esecuzione all'interno dell'area.</span><span class="sxs-lookup"><span data-stu-id="863c5-120">This storage account is used to store monitoring data for all Stream Analytics jobs running in this region.</span></span>
   * <span data-ttu-id="863c5-121">Se si utilizza il portale di Azure, specificare un **gruppo di risorse** nuovo o esistente per contenere le risorse correlate per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="863c5-121">If using the Azure portal, specify a new or existing **Resource Group** to hold related resources for your application.</span></span>
4. <span data-ttu-id="863c5-122">Dopo aver configurato le nuove opzioni del processo di Analisi di flusso, fare clic su **Crea processo di Analisi di flusso**.</span><span class="sxs-lookup"><span data-stu-id="863c5-122">Once the new Stream Analytics job options are configured, click **Create Stream Analytics Job**.</span></span> <span data-ttu-id="863c5-123">La creazione del processo di analisi di flusso può richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="863c5-123">It can take a few minutes for the Stream Analytics job to be created.</span></span> <span data-ttu-id="863c5-124">Per verificare lo stato, è possibile monitorare l'avanzamento nell’hub delle notifiche.</span><span class="sxs-lookup"><span data-stu-id="863c5-124">To check the status, you can monitor the progress in the Notifications hub.</span></span>
   
   ![Processo di elaborazione di analisi dei dati, hub di notifica](./media/stream-analytics-create-a-job/2-stream-analytics-create-a-job.png)  
   
   ![Portale di Azure, processo di elaborazione di analisi dei dati, creare un processo](./media/stream-analytics-create-a-job/5-stream-analytics-create-a-job.png)  
5. <span data-ttu-id="863c5-127">Il nuovo processo avrà lo stato **Creato**.</span><span class="sxs-lookup"><span data-stu-id="863c5-127">The new job will show a status of **Created**.</span></span> <span data-ttu-id="863c5-128">Si noti che il pulsante **Avvia** è disabilitato.</span><span class="sxs-lookup"><span data-stu-id="863c5-128">Notice that the **Start** button is disabled.</span></span> <span data-ttu-id="863c5-129">Prima di avviare il processo, configurare l'input, la query e l'output.</span><span class="sxs-lookup"><span data-stu-id="863c5-129">Configure the job input, query, and output before you start the job.</span></span>
   
   ![Elaborazione dell'analisi dei dati, stato processo](./media/stream-analytics-create-a-job/3-stream-analytics-create-a-job.png)  
   
   ![Portale di Azure, elaborazione dell'analisi dei dati, stato processo](./media/stream-analytics-create-a-job/6-stream-analytics-create-a-job.png)  

## <a name="get-help"></a><span data-ttu-id="863c5-132">Ottenere aiuto</span><span class="sxs-lookup"><span data-stu-id="863c5-132">Get help</span></span>
<span data-ttu-id="863c5-133">Per assistenza, provare il [Forum di Analisi di flusso di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="863c5-133">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="863c5-134">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="863c5-134">Next steps</span></span>
* [<span data-ttu-id="863c5-135">Introduzione ad Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="863c5-135">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="863c5-136">Introduzione all'uso di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="863c5-136">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="863c5-137">Ridimensionare i processi di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="863c5-137">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="863c5-138">Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="863c5-138">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="863c5-139">Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="863c5-139">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

