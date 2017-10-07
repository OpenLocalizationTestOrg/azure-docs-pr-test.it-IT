---
title: i limiti di Quota Data Lake Analitica aaaAzure | Documenti Microsoft
description: Informazioni su come tooadjust e aumento della quota limita negli account di Azure Data Lake Analitica (ADLA).
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
ms.openlocfilehash: 875c4d00e0c57414031e50754495c02162bdca48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-lake-analytics-quota-limits"></a><span data-ttu-id="06eda-104">Limiti di quota di Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="06eda-104">Azure Data Lake Analytics Quota Limits</span></span>

<span data-ttu-id="06eda-105">Informazioni su come tooadjust e aumento della quota limita negli account di Azure Data Lake Analitica (ADLA).</span><span class="sxs-lookup"><span data-stu-id="06eda-105">Learn how tooadjust and increase quota limits in Azure Data Lake Analytics (ADLA) accounts.</span></span> <span data-ttu-id="06eda-106">La conoscenza di questi limiti può aiutare a comprendere il comportamento del processo U-SQL.</span><span class="sxs-lookup"><span data-stu-id="06eda-106">Knowing these limits may help you understand your U-SQL job behavior.</span></span> <span data-ttu-id="06eda-107">Tutti i limiti di quota sono trasferibili, pertanto è possibile aumentare i limiti massimi di hello raggiungendo toous.</span><span class="sxs-lookup"><span data-stu-id="06eda-107">All quota limits are soft, so you can increase hello maximum limits by reaching out toous.</span></span>

## <a name="azure-subscriptions-limits"></a><span data-ttu-id="06eda-108">Limiti delle sottoscrizioni Azure</span><span class="sxs-lookup"><span data-stu-id="06eda-108">Azure subscriptions limits</span></span>

<span data-ttu-id="06eda-109">**Numero massimo di account di ADLA per sottoscrizione:**  5</span><span class="sxs-lookup"><span data-stu-id="06eda-109">**Maximum number of ADLA accounts per subscription:**  5</span></span>

 <span data-ttu-id="06eda-110">Si tratta hello il numero massimo di account ADLA che è possibile creare per ogni sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="06eda-110">This is hello maximum number of ADLA accounts you can create per subscription.</span></span> <span data-ttu-id="06eda-111">Se si tenta di account ADLA toocreate un sesto, si verificherà un errore "È stato raggiunto numero massimo di hello di account Data Lake Analitica consentiti (5) nell'area sotto il nome di sottoscrizione".</span><span class="sxs-lookup"><span data-stu-id="06eda-111">If you try toocreate a sixth ADLA account, you will get an error "You have reached hello maximum number of Data Lake Analytics accounts allowed (5) in region under subscription name".</span></span> <span data-ttu-id="06eda-112">In questo caso, eliminare qualsiasi account ADLA inutilizzati o raggiungere toous da [aprendo un ticket di supporto](#increase-maximum-quota-limits).</span><span class="sxs-lookup"><span data-stu-id="06eda-112">In this case, either delete any unused ADLA accounts, or reach out toous by [opening a support ticket](#increase-maximum-quota-limits).</span></span>

## <a name="adla-account-limits"></a><span data-ttu-id="06eda-113">Limiti degli account di ADLA</span><span class="sxs-lookup"><span data-stu-id="06eda-113">ADLA account limits</span></span>

<span data-ttu-id="06eda-114">**Numero massimo di unità di analisi per account:** 250</span><span class="sxs-lookup"><span data-stu-id="06eda-114">**Maximum number of Analytics Units (AUs) per account:** 250</span></span>

<span data-ttu-id="06eda-115">Si tratta di numero massimo di hello di AUs che possono essere eseguiti contemporaneamente nel tuo account.</span><span class="sxs-lookup"><span data-stu-id="06eda-115">This is hello maximum number of AUs that can run concurrently in your account.</span></span> <span data-ttu-id="06eda-116">Se il totale delle unità di analisi dei processi in esecuzione supera questo limite, i processi più recenti vengono accodati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="06eda-116">If your total running AUs across all jobs exceeds this limit, newer jobs are queued automatically.</span></span> <span data-ttu-id="06eda-117">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="06eda-117">For example:</span></span>

* <span data-ttu-id="06eda-118">Se si dispone di un solo processo in esecuzione con 250 Australia, quando si invia un secondo processo rimarrà in attesa nella coda del processo hello finché hello primo processo viene completato.</span><span class="sxs-lookup"><span data-stu-id="06eda-118">If you have only one job running with 250 AUs, when you submit a second job it will wait in hello job queue until hello first job completes.</span></span>
* <span data-ttu-id="06eda-119">Se si dispone di cinque processi in esecuzione e ognuno utilizza 50 Australia, quando si invia un processo sesto necessarie 20 AUs è in attesa nella coda del processo hello fino a quando non sono presenti 20 AUs disponibili.</span><span class="sxs-lookup"><span data-stu-id="06eda-119">If you already have five jobs running and each is using 50 AUs, when you submit a sixth job that needs 20 AUs it waits in hello job queue until there are 20 AUs available.</span></span>

<span data-ttu-id="06eda-120">**Numero massimo di processi simultanei di U-SQL per ogni account:** 20</span><span class="sxs-lookup"><span data-stu-id="06eda-120">**Maximum number of concurrent U-SQL jobs per account:** 20</span></span>

<span data-ttu-id="06eda-121">Si tratta hello numero massimo di processi che possono essere eseguiti contemporaneamente nel tuo account.</span><span class="sxs-lookup"><span data-stu-id="06eda-121">This is hello maximum number of jobs that can run concurrently in your account.</span></span> <span data-ttu-id="06eda-122">Al di sopra di questo valore, i processi più recenti vengono accodati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="06eda-122">Above this value, newer jobs are queued automatically.</span></span>

## <a name="adjust-adla-quota-limits-per-account"></a><span data-ttu-id="06eda-123">Modificare i limiti di quota di Azure Data Lake Analytics per ogni account</span><span class="sxs-lookup"><span data-stu-id="06eda-123">Adjust ADLA quota limits per account</span></span>

1. <span data-ttu-id="06eda-124">Accesso toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="06eda-124">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="06eda-125">Scegliere un account ADLA esistente.</span><span class="sxs-lookup"><span data-stu-id="06eda-125">Choose an existing ADLA account.</span></span>
3. <span data-ttu-id="06eda-126">Fare clic su **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="06eda-126">Click **Properties**.</span></span>
4. <span data-ttu-id="06eda-127">Regolare **parallelismo** e **processi simultanei** toosuit le proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="06eda-127">Adjust **Parallelism** and **Concurrent Jobs** toosuit your needs.</span></span>

    ![Pannello del portale di Azure Data Lake Analytics](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-properties.png)

## <a name="increase-maximum-quota-limits"></a><span data-ttu-id="06eda-129">Aumentare i limiti massimi di quota</span><span class="sxs-lookup"><span data-stu-id="06eda-129">Increase maximum quota limits</span></span>

1. <span data-ttu-id="06eda-130">Aprire una richiesta di supporto nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="06eda-130">Open a support request in Azure Portal.</span></span>

    ![Pannello del portale di Azure Data Lake Analytics](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-help-support.png)

    ![Pannello del portale di Azure Data Lake Analytics](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request.png)
2. <span data-ttu-id="06eda-133">Selezionare il tipo di problema hello **Quota**.</span><span class="sxs-lookup"><span data-stu-id="06eda-133">Select hello issue type **Quota**.</span></span>
3. <span data-ttu-id="06eda-134">Selezionare la propria **sottoscrizione** (assicurarsi che non sia una sottoscrizione di "prova").</span><span class="sxs-lookup"><span data-stu-id="06eda-134">Select your **Subscription** (make sure it is not a "trial" subscription).</span></span>
4. <span data-ttu-id="06eda-135">Selezionare il tipo di quota **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="06eda-135">Select quota type **Data Lake Analytics**.</span></span>

    ![Pannello del portale di Azure Data Lake Analytics](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-basics.png)

5. <span data-ttu-id="06eda-137">Nel pannello problema hello, spiegare il limite di aumento richiesto con **dettagli** di motivo per cui è necessario questa capacità aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="06eda-137">In hello problem blade, explain your requested increase limit with **Details** of why you need this extra capacity.</span></span>

    ![Pannello del portale di Azure Data Lake Analytics](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-details.png)

6. <span data-ttu-id="06eda-139">Verificare le informazioni di contatto e creare la richiesta di supporto hello.</span><span class="sxs-lookup"><span data-stu-id="06eda-139">Verify your contact information and create hello support request.</span></span>

<span data-ttu-id="06eda-140">Microsoft esamina la richiesta e tenta di tooaccommodate le esigenze aziendali appena possibile.</span><span class="sxs-lookup"><span data-stu-id="06eda-140">Microsoft reviews your request and tries tooaccommodate your business needs as soon as possible.</span></span>

## <a name="next-steps"></a><span data-ttu-id="06eda-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="06eda-141">Next steps</span></span>

* [<span data-ttu-id="06eda-142">Panoramica di Analisi Microsoft Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="06eda-142">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="06eda-143">Gestire Azure Data Lake Analytics tramite Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="06eda-143">Manage Azure Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-manage-use-powershell.md)
* [<span data-ttu-id="06eda-144">Monitorare e risolvere i problemi dei processi di Azure Data Lake Analytics tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="06eda-144">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
