---
title: Funzioni di Azure aaaMonitoring | Documenti Microsoft
description: Informazioni su come toomonitor delle funzioni di Azure.
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
ms.openlocfilehash: 254348d1cefce925654bd9532715b6def571e0ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-azure-functions"></a><span data-ttu-id="f88ca-104">Monitoraggio di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="f88ca-104">Monitoring Azure Functions</span></span>

## <a name="overview"></a><span data-ttu-id="f88ca-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="f88ca-105">Overview</span></span> 


<span data-ttu-id="f88ca-106">Hello **monitoraggio** scheda per ogni funzione consente tooreview ogni esecuzione di una funzione.</span><span class="sxs-lookup"><span data-stu-id="f88ca-106">hello **Monitor** tab for each function allows you tooreview each execution of a function.</span></span>

![Scheda Monitoraggio di Funzioni di Azure](./media/functions-monitoring/monitor-tab.png) 

<span data-ttu-id="f88ca-108">Fare clic su un'esecuzione consente si tooreview hello durata, dati di input, gli errori e i file di log associati.</span><span class="sxs-lookup"><span data-stu-id="f88ca-108">Clicking an execution allows you tooreview hello duration, input data, errors, and associated log files.</span></span> <span data-ttu-id="f88ca-109">Ciò risulta utile per il debug e per l'ottimizzazione delle prestazioni delle funzioni.</span><span class="sxs-lookup"><span data-stu-id="f88ca-109">This is useful debugging and performance tuning your functions.</span></span>


> [!IMPORTANT]
> <span data-ttu-id="f88ca-110">Quando si utilizza hello [consumo piano di hosting](functions-overview.md#pricing) per le funzioni di Azure, hello **monitoraggio** riquadro nel pannello della panoramica App funzione hello non mostreranno alcun dato.</span><span class="sxs-lookup"><span data-stu-id="f88ca-110">When using hello [Consumption hosting plan](functions-overview.md#pricing) for Azure Functions, hello **Monitoring** tile in hello Function App overview blade will not show any data.</span></span> <span data-ttu-id="f88ca-111">In questo modo piattaforma hello viene ridimensionata in modo dinamico e gestisce le istanze di calcolo, pertanto queste metriche non sono significative in un piano di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="f88ca-111">This is because hello platform dynamically scales and manages compute instances for you, so these metrics are not meaningful on a Consumption plan.</span></span> <span data-ttu-id="f88ca-112">utilizzo di hello toomonitor delle app di funzione, si dovrebbero usare invece indicazioni hello in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="f88ca-112">toomonitor hello usage of your Function Apps, you should instead use hello guidance in this article.</span></span>
> 
> <span data-ttu-id="f88ca-113">Hello cattura di schermata seguente viene illustrato un esempio:</span><span class="sxs-lookup"><span data-stu-id="f88ca-113">hello following screen-shot shows an example:</span></span>
> 
> ![Il monitoraggio nel Pannello di risorse principale hello](./media/functions-monitoring/app-service-overview-monitoring.png)



## <a name="real-time-monitoring"></a><span data-ttu-id="f88ca-115">Monitoraggio in tempo reale</span><span class="sxs-lookup"><span data-stu-id="f88ca-115">Real-time monitoring</span></span>

<span data-ttu-id="f88ca-116">Il monitoraggio in tempo reale è disponibile selezionando il **flusso eventi live**, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="f88ca-116">Real-time monitoring is available by clicking **live event stream** as shown below.</span></span> 

![Opzione di flusso di eventi per la scheda Monitoraggio hello Live](./media/functions-monitoring/monitor-tab-live-event-stream.png)

<span data-ttu-id="f88ca-118">flusso di eventi in tempo reale di Hello verrà rappresentata in una nuova scheda del browser come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="f88ca-118">hello live event stream will be graphed in a new browser tab as shown below.</span></span> 

![Esempio di flusso eventi live](./media/functions-monitoring/live-event-stream.png)


> [!NOTE]
> <span data-ttu-id="f88ca-120">Si verifica un problema noto che potrebbe causare il toobe toofail dati popolata.</span><span class="sxs-lookup"><span data-stu-id="f88ca-120">There is a known issue that may cause your data toofail toobe populated.</span></span> <span data-ttu-id="f88ca-121">Se ciò si verifica, potrebbe essere necessario tooclose hello browser scheda contenente hello in tempo reale flusso di eventi e quindi fare clic su **flusso di eventi in tempo reale** nuovamente tooallow è tooproperly popolare i dati di flusso di eventi.</span><span class="sxs-lookup"><span data-stu-id="f88ca-121">If you experience this, you may need tooclose hello browser tab containing hello live event stream and then click **live event stream** again tooallow it tooproperly populate your event stream data.</span></span> 

<span data-ttu-id="f88ca-122">flusso di eventi in tempo reale di Hello verrà graph hello statistiche per la funzione seguente:</span><span class="sxs-lookup"><span data-stu-id="f88ca-122">hello live event stream will graph hello following statistics for your function:</span></span>

* <span data-ttu-id="f88ca-123">Esecuzioni avviate al secondo</span><span class="sxs-lookup"><span data-stu-id="f88ca-123">Executions started per second</span></span>
* <span data-ttu-id="f88ca-124">Esecuzioni completate al secondo</span><span class="sxs-lookup"><span data-stu-id="f88ca-124">Executions completed per second</span></span>
* <span data-ttu-id="f88ca-125">Esecuzioni non riuscite al secondo</span><span class="sxs-lookup"><span data-stu-id="f88ca-125">Executions failed per second</span></span>
* <span data-ttu-id="f88ca-126">Tempo di esecuzione medio in millisecondi</span><span class="sxs-lookup"><span data-stu-id="f88ca-126">Average execution time in milliseconds.</span></span>

<span data-ttu-id="f88ca-127">Queste statistiche sono in tempo reale, ma hello effettiva rappresentazione grafica dei dati di esecuzione hello dispone di latenza di circa 10 secondi.</span><span class="sxs-lookup"><span data-stu-id="f88ca-127">These statistics are real-time but hello actual graphing of hello execution data may have around 10 seconds of latency.</span></span>






## <a name="monitoring-log-files-from-a-command-line"></a><span data-ttu-id="f88ca-128">Monitoraggio dei file di log da una riga di comando</span><span class="sxs-lookup"><span data-stu-id="f88ca-128">Monitoring log files from a command line</span></span>


<span data-ttu-id="f88ca-129">È possibile trasmettere sessione della riga di comando tooa i file di log in una workstation locale usando hello Azure interfaccia della riga di comando (CLI) o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f88ca-129">You can stream log files tooa command line session on a local workstation using hello Azure Command Line Interface (CLI) or PowerShell.</span></span>

### <a name="monitoring-function-app-log-files-with-hello-azure-cli"></a><span data-ttu-id="f88ca-130">Monitoraggio file di log di app di funzione con hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="f88ca-130">Monitoring function app log files with hello Azure CLI</span></span>

<span data-ttu-id="f88ca-131">avviata, tooget [installare hello CLI di Azure](../cli-install-nodejs.md)</span><span class="sxs-lookup"><span data-stu-id="f88ca-131">tooget started, [install hello Azure CLI](../cli-install-nodejs.md)</span></span>

<span data-ttu-id="f88ca-132">Accedere al proprio account Azure con i seguenti hello comando o uno qualsiasi di hello altre opzioni descritte, [Accedi tooAzure da hello Azure CLI](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="f88ca-132">Log into your Azure account using hello following command, or any of hello other options covered in, [Log in tooAzure from hello Azure CLI](../xplat-cli-connect.md).</span></span>

    azure login

<span data-ttu-id="f88ca-133">Comando che segue hello di utilizzare la modalità di Gestione servizio CLI di Azure (ASM) tooenable:.</span><span class="sxs-lookup"><span data-stu-id="f88ca-133">Use hello following command tooenable Azure CLI Service Management (ASM) mode:.</span></span>

    azure config mode asm

<span data-ttu-id="f88ca-134">Se si dispone di più sottoscrizioni, usare hello toolist i comandi seguenti, i set di hello sottoscrizione toohello sottoscrizione corrente che contiene l'app di funzione e le sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="f88ca-134">If you have multiple subscriptions, use hello following commands toolist your subscriptions and set hello current subscription toohello subscription that contains your function app.</span></span>

    azure account list
    azure account set <subscriptionNameOrId>

<span data-ttu-id="f88ca-135">Hello comando riportato di seguito verrà al flusso di file di log hello della riga di comando funzione app toohello:</span><span class="sxs-lookup"><span data-stu-id="f88ca-135">hello following command will stream hello log files of your function app toohello command line:</span></span>

    azure site log tail -v <function app name>

### <a name="monitoring-function-app-log-files-with-powershell"></a><span data-ttu-id="f88ca-136">Monitoraggio dei file di log delle app per le funzioni tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="f88ca-136">Monitoring function app log files with PowerShell</span></span>

<span data-ttu-id="f88ca-137">avviata, tooget [installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f88ca-137">tooget started, [install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="f88ca-138">Aggiungere l'account di Azure eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f88ca-138">Add your Azure account by running hello following command:</span></span>

    PS C:\> Add-AzureAccount

<span data-ttu-id="f88ca-139">Se si dispone di più sottoscrizioni, è possibile elencarli in base al nome con hello successivo comando toosee se hello corretto sottoscrizione è hello attualmente selezionato in base a `IsCurrent` proprietà:</span><span class="sxs-lookup"><span data-stu-id="f88ca-139">If you have multiple subscriptions, you can list them by name with hello following command toosee if hello correct subscription is hello currently selected based on `IsCurrent` property:</span></span>

    PS C:\> Get-AzureSubscription

<span data-ttu-id="f88ca-140">Se è necessario tooset hello sottoscrizione attiva toohello quello contenente l'app di funzione, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f88ca-140">If you need tooset hello active subscription toohello one containing your function app, use hello following command:</span></span>

    PS C:\> Get-AzureSubscription -SubscriptionName "MyFunctionAppSubscription" | Select-AzureSubscription

<span data-ttu-id="f88ca-141">Sessione di PowerShell tooyour per i log di hello flusso con hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f88ca-141">Stream hello logs tooyour PowerShell session with hello following command:</span></span>

    PS C:\> Get-AzureWebSiteLog -Name MyFunctionApp -Tail

<span data-ttu-id="f88ca-142">Per ulteriori informazioni, vedere troppo[come: flusso di log per le app web](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs).</span><span class="sxs-lookup"><span data-stu-id="f88ca-142">For more information refer too[How to: Stream logs for web apps](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="f88ca-143">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f88ca-143">Next steps</span></span>
<span data-ttu-id="f88ca-144">Per ulteriori informazioni, vedere hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="f88ca-144">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="f88ca-145">Test di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="f88ca-145">Testing a function</span></span>](functions-test-a-function.md)
* [<span data-ttu-id="f88ca-146">Scalabilità di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="f88ca-146">Scale a function</span></span>](functions-scale.md)

