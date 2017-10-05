---
title: Monitoraggio di Funzioni di Azure | Documentazione Microsoft
description: Informazioni su come monitorare Funzioni di Azure.
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: Funzioni di Azure, Funzioni, elaborazione eventi, webhook, calcolo dinamico, architettura senza server
ms.assetid: 501722c3-f2f7-4224-a220-6d59da08a320
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/03/2016
ms.author: wesmc
ms.openlocfilehash: b70214593b1417265387f42306a633bb0df2920e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="monitoring-azure-functions"></a><span data-ttu-id="c65ec-104">Monitoraggio di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="c65ec-104">Monitoring Azure Functions</span></span>

## <a name="overview"></a><span data-ttu-id="c65ec-105">Overview</span><span class="sxs-lookup"><span data-stu-id="c65ec-105">Overview</span></span> 


<span data-ttu-id="c65ec-106">La scheda **Monitoraggio** per ogni funzione consente di esaminare ogni esecuzione di una funzione.</span><span class="sxs-lookup"><span data-stu-id="c65ec-106">The **Monitor** tab for each function allows you to review each execution of a function.</span></span>

![Scheda Monitoraggio di Funzioni di Azure](./media/functions-monitoring/monitor-tab.png) 

<span data-ttu-id="c65ec-108">La selezione di un'esecuzione consente di verificare la durata, i dati di input, gli errori e i file di log associati.</span><span class="sxs-lookup"><span data-stu-id="c65ec-108">Clicking an execution allows you to review the duration, input data, errors, and associated log files.</span></span> <span data-ttu-id="c65ec-109">Ciò risulta utile per il debug e per l'ottimizzazione delle prestazioni delle funzioni.</span><span class="sxs-lookup"><span data-stu-id="c65ec-109">This is useful debugging and performance tuning your functions.</span></span>


> [!IMPORTANT]
> <span data-ttu-id="c65ec-110">Quando si usa il [piano di hosting a consumo](functions-overview.md#pricing) per Funzioni di Azure, il riquadro **Monitoraggio** nel pannello di panoramica dell'app per le funzioni non mostrerà alcun dato.</span><span class="sxs-lookup"><span data-stu-id="c65ec-110">When using the [Consumption hosting plan](functions-overview.md#pricing) for Azure Functions, the **Monitoring** tile in the Function App overview blade will not show any data.</span></span> <span data-ttu-id="c65ec-111">La piattaforma, infatti, ridimensiona e gestisce automaticamente le istanze di calcolo, quindi queste metriche non sono significative per un piano a consumo.</span><span class="sxs-lookup"><span data-stu-id="c65ec-111">This is because the platform dynamically scales and manages compute instances for you, so these metrics are not meaningful on a Consumption plan.</span></span> <span data-ttu-id="c65ec-112">Per monitorare l'utilizzo delle app per le funzioni, è necessario usare invece le indicazioni disponibili in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="c65ec-112">To monitor the usage of your Function Apps, you should instead use the guidance in this article.</span></span>
> 
> <span data-ttu-id="c65ec-113">Lo screenshot seguente mostra un esempio:</span><span class="sxs-lookup"><span data-stu-id="c65ec-113">The following screen-shot shows an example:</span></span>
> 
> ![Monitoraggio nel pannello principale delle risorse](./media/functions-monitoring/app-service-overview-monitoring.png)



## <a name="real-time-monitoring"></a><span data-ttu-id="c65ec-115">Monitoraggio in tempo reale</span><span class="sxs-lookup"><span data-stu-id="c65ec-115">Real-time monitoring</span></span>

<span data-ttu-id="c65ec-116">Il monitoraggio in tempo reale è disponibile selezionando il **flusso eventi live**, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="c65ec-116">Real-time monitoring is available by clicking **live event stream** as shown below.</span></span> 

![Opzione flusso eventi live per la scheda Monitoraggio](./media/functions-monitoring/monitor-tab-live-event-stream.png)

<span data-ttu-id="c65ec-118">Il flusso eventi live verrà visualizzato come grafico in una nuova scheda del browser, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="c65ec-118">The live event stream will be graphed in a new browser tab as shown below.</span></span> 

![Esempio di flusso eventi live](./media/functions-monitoring/live-event-stream.png)


> [!NOTE]
> <span data-ttu-id="c65ec-120">A causa di un problema noto, è possibile che il popolamento dei dati abbia esito negativo.</span><span class="sxs-lookup"><span data-stu-id="c65ec-120">There is a known issue that may cause your data to fail to be populated.</span></span> <span data-ttu-id="c65ec-121">Se si verifica questo problema, potrebbe essere necessario chiudere la scheda del browser che include il flusso eventi live e quindi fare di nuovo clic su **flusso eventi live** per consentire il popolamento corretto dei dati del flusso di eventi.</span><span class="sxs-lookup"><span data-stu-id="c65ec-121">If you experience this, you may need to close the browser tab containing the live event stream and then click **live event stream** again to allow it to properly populate your event stream data.</span></span> 

<span data-ttu-id="c65ec-122">Il flusso eventi live produrrà un grafico delle statistiche seguenti per la funzione:</span><span class="sxs-lookup"><span data-stu-id="c65ec-122">The live event stream will graph the following statistics for your function:</span></span>

* <span data-ttu-id="c65ec-123">Esecuzioni avviate al secondo</span><span class="sxs-lookup"><span data-stu-id="c65ec-123">Executions started per second</span></span>
* <span data-ttu-id="c65ec-124">Esecuzioni completate al secondo</span><span class="sxs-lookup"><span data-stu-id="c65ec-124">Executions completed per second</span></span>
* <span data-ttu-id="c65ec-125">Esecuzioni non riuscite al secondo</span><span class="sxs-lookup"><span data-stu-id="c65ec-125">Executions failed per second</span></span>
* <span data-ttu-id="c65ec-126">Tempo di esecuzione medio in millisecondi</span><span class="sxs-lookup"><span data-stu-id="c65ec-126">Average execution time in milliseconds.</span></span>

<span data-ttu-id="c65ec-127">Queste statistiche sono in tempo reale, ma la creazione effettiva dei grafici relativi ai dati dell'esecuzione potrebbe comportare circa 10 secondi di latenza.</span><span class="sxs-lookup"><span data-stu-id="c65ec-127">These statistics are real-time but the actual graphing of the execution data may have around 10 seconds of latency.</span></span>






## <a name="monitoring-log-files-from-a-command-line"></a><span data-ttu-id="c65ec-128">Monitoraggio dei file di log da una riga di comando</span><span class="sxs-lookup"><span data-stu-id="c65ec-128">Monitoring log files from a command line</span></span>


<span data-ttu-id="c65ec-129">È possibile trasmettere i file di log a una sessione della riga di comando su una workstation locale usando l'interfaccia della riga di comando di Azure o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c65ec-129">You can stream log files to a command line session on a local workstation using the Azure Command Line Interface (CLI) or PowerShell.</span></span>

### <a name="monitoring-function-app-log-files-with-the-azure-cli"></a><span data-ttu-id="c65ec-130">Monitoraggio dei file di log dell'app per le funzioni con l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="c65ec-130">Monitoring function app log files with the Azure CLI</span></span>

<span data-ttu-id="c65ec-131">Per iniziare, [installare l'interfaccia della riga di comando di Azure](../cli-install-nodejs.md)</span><span class="sxs-lookup"><span data-stu-id="c65ec-131">To get started, [install the Azure CLI](../cli-install-nodejs.md)</span></span>

<span data-ttu-id="c65ec-132">Accedere all'account di Azure usando il comando seguente o una delle altre opzioni illustrate in [Accedere ad Azure dall'interfaccia della riga di comando di Azure](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="c65ec-132">Log into your Azure account using the following command, or any of the other options covered in, [Log in to Azure from the Azure CLI](../xplat-cli-connect.md).</span></span>

    azure login

<span data-ttu-id="c65ec-133">Usare il comando seguente per abilitare la modalità Gestione dei servizi dell'interfaccia della riga di comando di Azure:</span><span class="sxs-lookup"><span data-stu-id="c65ec-133">Use the following command to enable Azure CLI Service Management (ASM) mode:.</span></span>

    azure config mode asm

<span data-ttu-id="c65ec-134">Se sono presenti più sottoscrizioni, usare i comandi seguenti per elencare le sottoscrizioni e impostare la sottoscrizione corrente sulla sottoscrizione che include l'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="c65ec-134">If you have multiple subscriptions, use the following commands to list your subscriptions and set the current subscription to the subscription that contains your function app.</span></span>

    azure account list
    azure account set <subscriptionNameOrId>

<span data-ttu-id="c65ec-135">Il comando seguente consentirà di trasmettere i file di log dell'app per le funzioni alla riga di comando:</span><span class="sxs-lookup"><span data-stu-id="c65ec-135">The following command will stream the log files of your function app to the command line:</span></span>

    azure site log tail -v <function app name>

### <a name="monitoring-function-app-log-files-with-powershell"></a><span data-ttu-id="c65ec-136">Monitoraggio dei file di log delle app per le funzioni tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="c65ec-136">Monitoring function app log files with PowerShell</span></span>

<span data-ttu-id="c65ec-137">Per iniziare, [installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c65ec-137">To get started, [install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="c65ec-138">Aggiungere il proprio account di Azure usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="c65ec-138">Add your Azure account by running the following command:</span></span>

    PS C:\> Add-AzureAccount

<span data-ttu-id="c65ec-139">Se sono presenti più sottoscrizioni, è possibile elencarle per nome con il comando seguente, in modo da verificare che sia attualmente selezionata la sottoscrizione corretta in base alla proprietà `IsCurrent`:</span><span class="sxs-lookup"><span data-stu-id="c65ec-139">If you have multiple subscriptions, you can list them by name with the following command to see if the correct subscription is the currently selected based on `IsCurrent` property:</span></span>

    PS C:\> Get-AzureSubscription

<span data-ttu-id="c65ec-140">Se è necessario impostare la sottoscrizione attiva sulla sottoscrizione che include l'app per le funzioni, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="c65ec-140">If you need to set the active subscription to the one containing your function app, use the following command:</span></span>

    PS C:\> Get-AzureSubscription -SubscriptionName "MyFunctionAppSubscription" | Select-AzureSubscription

<span data-ttu-id="c65ec-141">Trasmettere i log alla sessione di PowerShell con il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="c65ec-141">Stream the logs to your PowerShell session with the following command:</span></span>

    PS C:\> Get-AzureWebSiteLog -Name MyFunctionApp -Tail

<span data-ttu-id="c65ec-142">Per altre informazioni, vedere [Procedura: Eseguire lo streaming dei log per le app Web](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs).</span><span class="sxs-lookup"><span data-stu-id="c65ec-142">For more information refer to [How to: Stream logs for web apps](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c65ec-143">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c65ec-143">Next steps</span></span>
<span data-ttu-id="c65ec-144">Per altre informazioni, vedere le seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="c65ec-144">For more information, see the following resources:</span></span>

* [<span data-ttu-id="c65ec-145">Test di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="c65ec-145">Testing a function</span></span>](functions-test-a-function.md)
* [<span data-ttu-id="c65ec-146">Scalabilità di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="c65ec-146">Scale a function</span></span>](functions-scale.md)

