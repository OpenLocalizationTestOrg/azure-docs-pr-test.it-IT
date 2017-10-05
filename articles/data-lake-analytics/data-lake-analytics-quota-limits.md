---
title: Limiti di quota di Azure Data Lake Analytics | Documentazione Microsoft
description: Informazioni su come modificare e aumentare i limiti di quota nell'account di Azure Data Lake Analytics (ADLA).
services: data-lake-analytics
keywords: Azure Data Lake Analytics.
documentationcenter: 
author: omidm1
editor: omidm1
ms.assetid: 49416f38-fcc7-476f-a55e-d67f3f9c1d34
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: omidm
ms.openlocfilehash: 957f306ea0e80b5830ad64e5ef06c6d122d9eccc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="azure-data-lake-analytics-quota-limits"></a><span data-ttu-id="86d33-104">Limiti di quota di Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="86d33-104">Azure Data Lake Analytics Quota Limits</span></span>

<span data-ttu-id="86d33-105">Informazioni su come modificare e aumentare i limiti di quota nell'account di Azure Data Lake Analytics (ADLA).</span><span class="sxs-lookup"><span data-stu-id="86d33-105">Learn how to adjust and increase quota limits in Azure Data Lake Analytics (ADLA) accounts.</span></span> <span data-ttu-id="86d33-106">La conoscenza di questi limiti può aiutare a comprendere il comportamento del processo U-SQL.</span><span class="sxs-lookup"><span data-stu-id="86d33-106">Knowing these limits may help you understand your U-SQL job behavior.</span></span> <span data-ttu-id="86d33-107">Tutti i limiti di quota sono flessibili, quindi è possibile aumentare i limiti massimi rivolgendosi a Microsoft.</span><span class="sxs-lookup"><span data-stu-id="86d33-107">All quota limits are soft, so you can increase the maximum limits by reaching out to us.</span></span>

## <a name="azure-subscriptions-limits"></a><span data-ttu-id="86d33-108">Limiti delle sottoscrizioni Azure</span><span class="sxs-lookup"><span data-stu-id="86d33-108">Azure subscriptions limits</span></span>

<span data-ttu-id="86d33-109">**Numero massimo di account di ADLA per sottoscrizione:**  5</span><span class="sxs-lookup"><span data-stu-id="86d33-109">**Maximum number of ADLA accounts per subscription:**  5</span></span>

 <span data-ttu-id="86d33-110">Questo è il numero massimo di account di Azure Data Lake Analytics che è possibile creare per ogni sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="86d33-110">This is the maximum number of ADLA accounts you can create per subscription.</span></span> <span data-ttu-id="86d33-111">Se si tenta di creare un sesto account di ADLA, si ottiene un messaggio di errore che indica che è stato raggiunto il numero massimo di account di Data Lake Analytics consentiti (5) nell'area sotto il nome della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="86d33-111">If you try to create a sixth ADLA account, you will get an error "You have reached the maximum number of Data Lake Analytics accounts allowed (5) in region under subscription name".</span></span> <span data-ttu-id="86d33-112">In questo caso, eliminare qualsiasi account ADLA non usato o rivolgersi a Microsoft da [Apertura di un ticket di supporto](#increase-maximum-quota-limits).</span><span class="sxs-lookup"><span data-stu-id="86d33-112">In this case, either delete any unused ADLA accounts, or reach out to us by [opening a support ticket](#increase-maximum-quota-limits).</span></span>

## <a name="adla-account-limits"></a><span data-ttu-id="86d33-113">Limiti degli account di ADLA</span><span class="sxs-lookup"><span data-stu-id="86d33-113">ADLA account limits</span></span>

<span data-ttu-id="86d33-114">**Numero massimo di unità di analisi per account:** 250</span><span class="sxs-lookup"><span data-stu-id="86d33-114">**Maximum number of Analytics Units (AUs) per account:** 250</span></span>

<span data-ttu-id="86d33-115">Questo è il numero massimo di unità di analisi che si possono eseguire contemporaneamente nell'account.</span><span class="sxs-lookup"><span data-stu-id="86d33-115">This is the maximum number of AUs that can run concurrently in your account.</span></span> <span data-ttu-id="86d33-116">Se il totale delle unità di analisi dei processi in esecuzione supera questo limite, i processi più recenti vengono accodati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="86d33-116">If your total running AUs across all jobs exceeds this limit, newer jobs are queued automatically.</span></span> <span data-ttu-id="86d33-117">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="86d33-117">For example:</span></span>

* <span data-ttu-id="86d33-118">Se si ha un solo processo in esecuzione con 250 unità di analisi, quando si invia un secondo processo, esso rimarrà in attesa nella coda finché il primo non viene completato.</span><span class="sxs-lookup"><span data-stu-id="86d33-118">If you have only one job running with 250 AUs, when you submit a second job it will wait in the job queue until the first job completes.</span></span>
* <span data-ttu-id="86d33-119">Se si dispone di cinque processi in esecuzione e ognuno usa 50 Australia, quando si invia un processo sesto necessarie 20 AUs è in attesa nella coda dei processi fino a quando non sono presenti 20 AUs disponibili.</span><span class="sxs-lookup"><span data-stu-id="86d33-119">If you already have five jobs running and each is using 50 AUs, when you submit a sixth job that needs 20 AUs it waits in the job queue until there are 20 AUs available.</span></span>

<span data-ttu-id="86d33-120">**Numero massimo di processi simultanei di U-SQL per ogni account:** 20</span><span class="sxs-lookup"><span data-stu-id="86d33-120">**Maximum number of concurrent U-SQL jobs per account:** 20</span></span>

<span data-ttu-id="86d33-121">Questo è il numero massimo di processi che si possono eseguire contemporaneamente nell'account.</span><span class="sxs-lookup"><span data-stu-id="86d33-121">This is the maximum number of jobs that can run concurrently in your account.</span></span> <span data-ttu-id="86d33-122">Al di sopra di questo valore, i processi più recenti vengono accodati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="86d33-122">Above this value, newer jobs are queued automatically.</span></span>

## <a name="adjust-adla-quota-limits-per-account"></a><span data-ttu-id="86d33-123">Modificare i limiti di quota di Azure Data Lake Analytics per ogni account</span><span class="sxs-lookup"><span data-stu-id="86d33-123">Adjust ADLA quota limits per account</span></span>

1. <span data-ttu-id="86d33-124">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="86d33-124">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="86d33-125">Scegliere un account ADLA esistente.</span><span class="sxs-lookup"><span data-stu-id="86d33-125">Choose an existing ADLA account.</span></span>
3. <span data-ttu-id="86d33-126">Fare clic su **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="86d33-126">Click **Properties**.</span></span>
4. <span data-ttu-id="86d33-127">Adeguare **Parallelismo** e **Processi simultanei** alle proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="86d33-127">Adjust **Parallelism** and **Concurrent Jobs** to suit your needs.</span></span>

    ![Pannello del portale di Azure Data Lake Analytics](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-properties.png)

## <a name="increase-maximum-quota-limits"></a><span data-ttu-id="86d33-129">Aumentare i limiti massimi di quota</span><span class="sxs-lookup"><span data-stu-id="86d33-129">Increase maximum quota limits</span></span>

1. <span data-ttu-id="86d33-130">Aprire una richiesta di supporto nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="86d33-130">Open a support request in Azure Portal.</span></span>

    ![Pannello del portale di Azure Data Lake Analytics](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-help-support.png)

    ![Pannello del portale di Azure Data Lake Analytics](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request.png)
2. <span data-ttu-id="86d33-133">Selezionare il tipo di problema **Quota**.</span><span class="sxs-lookup"><span data-stu-id="86d33-133">Select the issue type **Quota**.</span></span>
3. <span data-ttu-id="86d33-134">Selezionare la propria **sottoscrizione** (assicurarsi che non sia una sottoscrizione di "prova").</span><span class="sxs-lookup"><span data-stu-id="86d33-134">Select your **Subscription** (make sure it is not a "trial" subscription).</span></span>
4. <span data-ttu-id="86d33-135">Selezionare il tipo di quota **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="86d33-135">Select quota type **Data Lake Analytics**.</span></span>

    ![Pannello del portale di Azure Data Lake Analytics](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-basics.png)

5. <span data-ttu-id="86d33-137">Nel pannello del problema, indicare la richiesta di aumenti dei limiti con i **dettagli** del motivo per cui viene richiesta la capacità aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="86d33-137">In the problem blade, explain your requested increase limit with **Details** of why you need this extra capacity.</span></span>

    ![Pannello del portale di Azure Data Lake Analytics](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-details.png)

6. <span data-ttu-id="86d33-139">Verificare le informazioni di contatto e creare la richiesta di supporto.</span><span class="sxs-lookup"><span data-stu-id="86d33-139">Verify your contact information and create the support request.</span></span>

<span data-ttu-id="86d33-140">Microsoft esamina la richiesta e tenta di eseguire l’operazione richiesta appena possibile.</span><span class="sxs-lookup"><span data-stu-id="86d33-140">Microsoft reviews your request and tries to accommodate your business needs as soon as possible.</span></span>

## <a name="next-steps"></a><span data-ttu-id="86d33-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="86d33-141">Next steps</span></span>

* [<span data-ttu-id="86d33-142">Panoramica di Analisi Microsoft Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="86d33-142">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="86d33-143">Gestire Azure Data Lake Analytics tramite Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="86d33-143">Manage Azure Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-manage-use-powershell.md)
* [<span data-ttu-id="86d33-144">Monitorare e risolvere i problemi dei processi di Azure Data Lake Analytics tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="86d33-144">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
