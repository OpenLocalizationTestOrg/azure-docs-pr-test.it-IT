---
title: aaaMonitor e gestire i processi di flusso Analitica con PowerShell | Documenti Microsoft
description: Informazioni su come toouse toomonitor di cmdlet e PowerShell di Azure e gestire i processi di flusso Analitica.
keywords: Azure PowerShell, cmdlet di Azure PowerShell, comando di PowerShell, script di PowerShell
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 514f454e-d18c-4081-8304-ab48577e15e8
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 44abc82f1c44a5ebc1701badd6547b84dac239b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-stream-analytics-jobs-with-azure-powershell-cmdlets"></a><span data-ttu-id="25d8a-104">Monitorare e gestire i processi di Analisi di flusso con i cmdlet di Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="25d8a-104">Monitor and manage Stream Analytics jobs with Azure PowerShell cmdlets</span></span>
<span data-ttu-id="25d8a-105">Informazioni su come toomonitor e gestire le risorse di flusso Analitica con i cmdlet di Azure PowerShell e script di powershell che eseguono attività Analitica di flusso di base.</span><span class="sxs-lookup"><span data-stu-id="25d8a-105">Learn how toomonitor and manage Stream Analytics resources with Azure PowerShell cmdlets and powershell scripting that execute basic Stream Analytics tasks.</span></span>

## <a name="prerequisites-for-running-azure-powershell-cmdlets-for-stream-analytics"></a><span data-ttu-id="25d8a-106">Prerequisiti per l'esecuzione dei cmdlet di Azure PowerShell per Analisi dei flussi</span><span class="sxs-lookup"><span data-stu-id="25d8a-106">Prerequisites for running Azure PowerShell cmdlets for Stream Analytics</span></span>
* <span data-ttu-id="25d8a-107">Creare un gruppo di risorse di Azure nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="25d8a-107">Create an Azure Resource Group in your subscription.</span></span> <span data-ttu-id="25d8a-108">Hello seguito è riportato un esempio di script di PowerShell di Azure.</span><span class="sxs-lookup"><span data-stu-id="25d8a-108">hello following is a sample Azure PowerShell script.</span></span> <span data-ttu-id="25d8a-109">Per informazioni su Azure PowerShell , vedere [Installare e configurare Azure PowerShell](/powershell/azure/overview);</span><span class="sxs-lookup"><span data-stu-id="25d8a-109">For Azure PowerShell information, see [Install and configure Azure PowerShell](/powershell/azure/overview);</span></span>  

<span data-ttu-id="25d8a-110">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="25d8a-110">Azure PowerShell 0.9.8:</span></span>  

         # Log in tooyour Azure account
        Add-AzureAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group if you have more than one subscription on your account.
        Select-AzureSubscription -SubscriptionName <subscription name>

        # If Stream Analytics has not been registered toohello subscription, remove remark symbol below (#) toorun hello Register-AzureProvider cmdlet tooregister hello provider namespace.
        #Register-AzureProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>

<span data-ttu-id="25d8a-111">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="25d8a-111">Azure PowerShell 1.0:</span></span>  

         # Log in tooyour Azure account
        Login-AzureRmAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group.
        Get-AzureRmSubscription –SubscriptionName “your sub” | Select-AzureRmSubscription

        # If Stream Analytics has not been registered toohello subscription, remove remark symbol below (#) toorun hello Register-AzureProvider cmdlet tooregister hello provider namespace.
        #Register-AzureRmResourceProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureRMResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>



> [!NOTE]
> <span data-ttu-id="25d8a-112">Nei processi di Analisi di flusso creati a livello di codice il monitoraggio non è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="25d8a-112">Stream Analytics jobs created programmatically do not have monitoring enabled by default.</span></span>  <span data-ttu-id="25d8a-113">È possibile abilitare manualmente il monitoraggio nel portale di Azure passando la pagina di monitoraggio del processo toohello hello e fare clic sul pulsante Abilita hello o è possibile farlo a livello di codice attenendosi alla seguente procedura hello [Analitica di flusso di Azure - Monitoraggio flusso Analitica processi a livello di programmazione](stream-analytics-monitor-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="25d8a-113">You can manually enable monitoring in hello Azure Portal by navigating toohello job’s Monitor page and clicking hello Enable button or you can do this programmatically by following hello steps located at [Azure Stream Analytics - Monitor Stream Analytics Jobs Programatically](stream-analytics-monitor-jobs.md).</span></span>
> 
> 

## <a name="azure-powershell-cmdlets-for-stream-analytics"></a><span data-ttu-id="25d8a-114">Cmdlet di Azure PowerShell per Analisi dei flussi</span><span class="sxs-lookup"><span data-stu-id="25d8a-114">Azure PowerShell cmdlets for Stream Analytics</span></span>
<span data-ttu-id="25d8a-115">Hello seguendo i cmdlet PowerShell di Azure possa essere utilizzati toomonitor e gestire i processi di Analitica di flusso di Azure.</span><span class="sxs-lookup"><span data-stu-id="25d8a-115">hello following Azure PowerShell cmdlets can be used toomonitor and manage Azure Stream Analytics jobs.</span></span> <span data-ttu-id="25d8a-116">Si noti che sono disponibili diverse versioni di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="25d8a-116">Note that Azure PowerShell has different versions.</span></span> 
<span data-ttu-id="25d8a-117">**Negli esempi di hello è primo comando hello elencati per Azure PowerShell 0.9.8, hello secondo comando è per Azure PowerShell 1.0.**</span><span class="sxs-lookup"><span data-stu-id="25d8a-117">**In hello examples listed hello first command is for Azure PowerShell 0.9.8, hello second command is for Azure PowerShell 1.0.**</span></span> <span data-ttu-id="25d8a-118">i comandi di Azure PowerShell 1.0 Hello avrà sempre "Azure Resource Manager" nel comando hello.</span><span class="sxs-lookup"><span data-stu-id="25d8a-118">hello Azure PowerShell 1.0 commands will always have "AzureRM" in hello command.</span></span>

### <a name="get-azurestreamanalyticsjob--get-azurermstreamanalyticsjob"></a><span data-ttu-id="25d8a-119">Get-AzureStreamAnalyticsJob | Get-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="25d8a-119">Get-AzureStreamAnalyticsJob | Get-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="25d8a-120">Elenca tutti i processi di flusso Analitica definiti nella sottoscrizione di Azure hello o gruppo di risorse specificato oppure ottiene informazioni sul processo su un processo specifico all'interno di un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="25d8a-120">Lists all Stream Analytics jobs defined in hello Azure subscription or specified resource group, or gets job information about a specific job within a resource group.</span></span>

<span data-ttu-id="25d8a-121">**Esempio 1**</span><span class="sxs-lookup"><span data-stu-id="25d8a-121">**Example 1**</span></span>

<span data-ttu-id="25d8a-122">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="25d8a-122">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob

<span data-ttu-id="25d8a-123">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="25d8a-123">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob

<span data-ttu-id="25d8a-124">Questo comando di PowerShell restituisce informazioni su tutti i processi di flusso Analitica hello hello sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="25d8a-124">This PowerShell command returns information about all hello Stream Analytics jobs in hello Azure subscription.</span></span>

<span data-ttu-id="25d8a-125">**Esempio 2**</span><span class="sxs-lookup"><span data-stu-id="25d8a-125">**Example 2**</span></span>

<span data-ttu-id="25d8a-126">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="25d8a-126">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

<span data-ttu-id="25d8a-127">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="25d8a-127">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

<span data-ttu-id="25d8a-128">Questo comando di PowerShell restituisce informazioni su tutti i processi di flusso Analitica hello nel gruppo di risorse hello analisi dei flussi-predefinito-centrale-US.</span><span class="sxs-lookup"><span data-stu-id="25d8a-128">This PowerShell command returns information about all hello Stream Analytics jobs in hello resource group StreamAnalytics-Default-Central-US.</span></span>

<span data-ttu-id="25d8a-129">**Esempio 3**</span><span class="sxs-lookup"><span data-stu-id="25d8a-129">**Example 3**</span></span>

<span data-ttu-id="25d8a-130">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="25d8a-130">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

<span data-ttu-id="25d8a-131">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="25d8a-131">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

<span data-ttu-id="25d8a-132">Questo comando di PowerShell restituisce informazioni sul processo di flusso Analitica hello StreamingJob nel gruppo di risorse hello analisi dei flussi-predefinito-centrale-US.</span><span class="sxs-lookup"><span data-stu-id="25d8a-132">This PowerShell command returns information about hello Stream Analytics job StreamingJob in hello resource group StreamAnalytics-Default-Central-US.</span></span>

### <a name="get-azurestreamanalyticsinput--get-azurermstreamanalyticsinput"></a><span data-ttu-id="25d8a-133">Get-AzureStreamAnalyticsInput | Get-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="25d8a-133">Get-AzureStreamAnalyticsInput | Get-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="25d8a-134">Elenca tutti gli input hello definiti in un processo di flusso Analitica specificato oppure ottiene informazioni su un input specifico.</span><span class="sxs-lookup"><span data-stu-id="25d8a-134">Lists all of hello inputs that are defined in a specified Stream Analytics job, or gets information about a specific input.</span></span>

<span data-ttu-id="25d8a-135">**Esempio 1**</span><span class="sxs-lookup"><span data-stu-id="25d8a-135">**Example 1**</span></span>

<span data-ttu-id="25d8a-136">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="25d8a-136">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="25d8a-137">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="25d8a-137">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="25d8a-138">Questo comando di PowerShell restituisce informazioni su tutti gli input hello definito nel processo di hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="25d8a-138">This PowerShell command returns information about all hello inputs defined in hello job StreamingJob.</span></span>

<span data-ttu-id="25d8a-139">**Esempio 2**</span><span class="sxs-lookup"><span data-stu-id="25d8a-139">**Example 2**</span></span>

<span data-ttu-id="25d8a-140">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="25d8a-140">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

<span data-ttu-id="25d8a-141">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="25d8a-141">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

<span data-ttu-id="25d8a-142">Questo comando di PowerShell restituisce informazioni sull'input hello denominato definito nel processo di hello StreamingJob EntryStream.</span><span class="sxs-lookup"><span data-stu-id="25d8a-142">This PowerShell command returns information about hello input named EntryStream defined in hello job StreamingJob.</span></span>

### <a name="get-azurestreamanalyticsoutput--get-azurermstreamanalyticsoutput"></a><span data-ttu-id="25d8a-143">Get-AzureStreamAnalyticsOutput | Get-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="25d8a-143">Get-AzureStreamAnalyticsOutput | Get-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="25d8a-144">Elenca tutti gli output di hello definiti in un processo di flusso Analitica specificato oppure ottiene informazioni su un output specifico.</span><span class="sxs-lookup"><span data-stu-id="25d8a-144">Lists all of hello outputs that are defined in a specified Stream Analytics job, or gets information about a specific output.</span></span>

<span data-ttu-id="25d8a-145">**Esempio 1**</span><span class="sxs-lookup"><span data-stu-id="25d8a-145">**Example 1**</span></span>

<span data-ttu-id="25d8a-146">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="25d8a-146">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="25d8a-147">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="25d8a-147">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="25d8a-148">Questo comando di PowerShell restituisce informazioni sull'output di hello definito nel processo di hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="25d8a-148">This PowerShell command returns information about hello outputs defined in hello job StreamingJob.</span></span>

<span data-ttu-id="25d8a-149">**Esempio 2**</span><span class="sxs-lookup"><span data-stu-id="25d8a-149">**Example 2**</span></span>

<span data-ttu-id="25d8a-150">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="25d8a-150">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

<span data-ttu-id="25d8a-151">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="25d8a-151">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

<span data-ttu-id="25d8a-152">Questo comando di PowerShell restituisce informazioni sull'output di hello denominato definito nel processo di hello StreamingJob di Output.</span><span class="sxs-lookup"><span data-stu-id="25d8a-152">This PowerShell command returns information about hello output named Output defined in hello job StreamingJob.</span></span>

### <a name="get-azurestreamanalyticsquota--get-azurermstreamanalyticsquota"></a><span data-ttu-id="25d8a-153">Get-AzureStreamAnalyticsQuota | Get-AzureRMStreamAnalyticsQuota</span><span class="sxs-lookup"><span data-stu-id="25d8a-153">Get-AzureStreamAnalyticsQuota | Get-AzureRMStreamAnalyticsQuota</span></span>
<span data-ttu-id="25d8a-154">Ottiene informazioni sulla quota di hello di streaming unità in una regione specificata.</span><span class="sxs-lookup"><span data-stu-id="25d8a-154">Gets information about hello quota of streaming units in a specified region.</span></span>

<span data-ttu-id="25d8a-155">**Esempio 1**</span><span class="sxs-lookup"><span data-stu-id="25d8a-155">**Example 1**</span></span>

<span data-ttu-id="25d8a-156">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="25d8a-156">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsQuota –Location "Central US" 

<span data-ttu-id="25d8a-157">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="25d8a-157">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsQuota –Location "Central US" 

<span data-ttu-id="25d8a-158">Questo comando di PowerShell restituisce informazioni sulla quota di hello e utilizzo di unità di streaming nell'area Stati Uniti centro hello.</span><span class="sxs-lookup"><span data-stu-id="25d8a-158">This PowerShell command returns information about hello quota and usage of streaming units in hello Central US region.</span></span>

### <a name="get-azurestreamanalyticstransformation--getazurermstreamanalyticstransformation"></a><span data-ttu-id="25d8a-159">Get-AzureStreamAnalyticsTransformation | GetAzureRMStreamAnalyticsTransformation</span><span class="sxs-lookup"><span data-stu-id="25d8a-159">Get-AzureStreamAnalyticsTransformation | GetAzureRMStreamAnalyticsTransformation</span></span>
<span data-ttu-id="25d8a-160">Ottiene informazioni su una specifica trasformazione definita nel processo di Analisi dei flussi.</span><span class="sxs-lookup"><span data-stu-id="25d8a-160">Gets information about a specific transformation defined in a Stream Analytics job.</span></span>

<span data-ttu-id="25d8a-161">**Esempio 1**</span><span class="sxs-lookup"><span data-stu-id="25d8a-161">**Example 1**</span></span>

<span data-ttu-id="25d8a-162">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="25d8a-162">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

<span data-ttu-id="25d8a-163">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="25d8a-163">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

<span data-ttu-id="25d8a-164">Questo comando di PowerShell restituisce informazioni sulla trasformazione hello chiamato StreamingJob nel processo di hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="25d8a-164">This PowerShell command returns information about hello transformation called StreamingJob in hello job StreamingJob.</span></span>

### <a name="new-azurestreamanalyticsinput--new-azurermstreamanalyticsinput"></a><span data-ttu-id="25d8a-165">New-AzureStreamAnalyticsInput | New-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="25d8a-165">New-AzureStreamAnalyticsInput | New-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="25d8a-166">Crea un nuovo input all'interno di un processo di Analisi dei flussi o aggiorna un input esistente specificato.</span><span class="sxs-lookup"><span data-stu-id="25d8a-166">Creates a new input within a Stream Analytics job, or updates an existing specified input.</span></span>

<span data-ttu-id="25d8a-167">Hello nome dell'input hello può essere specificato nel file con estensione JSON hello o sulla riga di comando hello.</span><span class="sxs-lookup"><span data-stu-id="25d8a-167">hello name of hello input can be specified in hello .json file or on hello command line.</span></span> <span data-ttu-id="25d8a-168">Se vengono specificati entrambi, il nome di hello nella riga di comando hello deve hello come hello file hello.</span><span class="sxs-lookup"><span data-stu-id="25d8a-168">If both are specified, hello name on hello command line must be hello same as hello one in hello file.</span></span>

<span data-ttu-id="25d8a-169">Se si specifica un input che esiste già e non si specifica hello: il parametro Force, hello cmdlet chiederà se tooreplace hello input esistente.</span><span class="sxs-lookup"><span data-stu-id="25d8a-169">If you specify an input that already exists and do not specify hello –Force parameter, hello cmdlet will ask whether or not tooreplace hello existing input.</span></span>

<span data-ttu-id="25d8a-170">Se si specificano hello – parametro Force e nome di input esistente, verrà sostituita hello input senza conferma.</span><span class="sxs-lookup"><span data-stu-id="25d8a-170">If you specify hello –Force parameter and specify an existing input name, hello input will be replaced without confirmation.</span></span>

<span data-ttu-id="25d8a-171">Per informazioni dettagliate sulla struttura dei file JSON hello e il contenuto, vedere toohello [Create Input (Analitica del flusso di Azure)] [ msdn-rest-api-create-stream-analytics-input] sezione di hello [flusso Analitica API REST di gestione Libreria riferimenti a][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="25d8a-171">For detailed information on hello JSON file structure and contents, refer toohello [Create Input (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-input] section of hello [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="25d8a-172">**Esempio 1**</span><span class="sxs-lookup"><span data-stu-id="25d8a-172">**Example 1**</span></span>

<span data-ttu-id="25d8a-173">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="25d8a-173">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

<span data-ttu-id="25d8a-174">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="25d8a-174">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

<span data-ttu-id="25d8a-175">Questo comando di PowerShell crea un nuovo input dal file hello Input.json.</span><span class="sxs-lookup"><span data-stu-id="25d8a-175">This PowerShell command creates a new input from hello file Input.json.</span></span> <span data-ttu-id="25d8a-176">Se un input esistente con nome hello specificato nel file di definizione input hello è già definito, verrà chiesto di cmdlet hello o meno tooreplace è.</span><span class="sxs-lookup"><span data-stu-id="25d8a-176">If an existing input with hello name specified in hello input definition file is already defined, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="25d8a-177">**Esempio 2**</span><span class="sxs-lookup"><span data-stu-id="25d8a-177">**Example 2**</span></span>

<span data-ttu-id="25d8a-178">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="25d8a-178">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

<span data-ttu-id="25d8a-179">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="25d8a-179">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

<span data-ttu-id="25d8a-180">Questo comando di PowerShell crea un nuovo input nel processo di hello chiamato EntryStream.</span><span class="sxs-lookup"><span data-stu-id="25d8a-180">This PowerShell command creates a new input in hello job called EntryStream.</span></span> <span data-ttu-id="25d8a-181">Se un input esistente con questo nome è già definito, verrà chiesto di cmdlet hello o meno tooreplace è.</span><span class="sxs-lookup"><span data-stu-id="25d8a-181">If an existing input with this name is already defined, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="25d8a-182">**Esempio 3**</span><span class="sxs-lookup"><span data-stu-id="25d8a-182">**Example 3**</span></span>

<span data-ttu-id="25d8a-183">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="25d8a-183">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

<span data-ttu-id="25d8a-184">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="25d8a-184">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

<span data-ttu-id="25d8a-185">Questo comando di PowerShell sostituisce definizione hello hello esistente origine di input denominato EntryStream con definizione hello dal file hello.</span><span class="sxs-lookup"><span data-stu-id="25d8a-185">This PowerShell command replaces hello definition of hello existing input source called EntryStream with hello definition from hello file.</span></span>

### <a name="new-azurestreamanalyticsjob--new-azurermstreamanalyticsjob"></a><span data-ttu-id="25d8a-186">New-AzureStreamAnalyticsJob | New-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="25d8a-186">New-AzureStreamAnalyticsJob | New-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="25d8a-187">Crea un nuovo processo di flusso Analitica in Microsoft Azure o aggiorna la definizione di hello di un processo esistente specificato.</span><span class="sxs-lookup"><span data-stu-id="25d8a-187">Creates a new Stream Analytics job in Microsoft Azure, or updates hello definition of an existing specified job.</span></span>

<span data-ttu-id="25d8a-188">nome di Hello del processo di hello può essere specificato nel file con estensione JSON hello o sulla riga di comando hello.</span><span class="sxs-lookup"><span data-stu-id="25d8a-188">hello name of hello job can be specified in hello .json file or on hello command line.</span></span> <span data-ttu-id="25d8a-189">Se vengono specificati entrambi, il nome di hello nella riga di comando hello deve hello come hello file hello.</span><span class="sxs-lookup"><span data-stu-id="25d8a-189">If both are specified, hello name on hello command line must be hello same as hello one in hello file.</span></span>

<span data-ttu-id="25d8a-190">Se si specifica un nome di processo che esiste già e non si specifica hello: il parametro Force, hello cmdlet chiederà se tooreplace hello processo esistente.</span><span class="sxs-lookup"><span data-stu-id="25d8a-190">If you specify a job name that already exists and do not specify hello –Force parameter, hello cmdlet will ask whether or not tooreplace hello existing job.</span></span>

<span data-ttu-id="25d8a-191">Se si specifica hello – parametro Force e specificare un nome di processo esistente, definizione del processo hello verrà sostituito senza conferma.</span><span class="sxs-lookup"><span data-stu-id="25d8a-191">If you specify hello –Force parameter and specify an existing job name, hello job definition will be replaced without confirmation.</span></span>

<span data-ttu-id="25d8a-192">Per informazioni dettagliate sulla struttura dei file JSON hello e il contenuto, vedere toohello [Crea processo di flusso Analitica] [ msdn-rest-api-create-stream-analytics-job] sezione di hello [riferimento all'API REST di flusso Analitica gestione Libreria][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="25d8a-192">For detailed information on hello JSON file structure and contents, refer toohello [Create Stream Analytics Job][msdn-rest-api-create-stream-analytics-job] section of hello [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="25d8a-193">**Esempio 1**</span><span class="sxs-lookup"><span data-stu-id="25d8a-193">**Example 1**</span></span>

<span data-ttu-id="25d8a-194">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="25d8a-194">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

<span data-ttu-id="25d8a-195">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="25d8a-195">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

<span data-ttu-id="25d8a-196">Questo comando di PowerShell crea un nuovo processo dalla definizione di hello in JobDefinition.json.</span><span class="sxs-lookup"><span data-stu-id="25d8a-196">This PowerShell command creates a new job from hello definition in JobDefinition.json.</span></span> <span data-ttu-id="25d8a-197">Se un processo esistente con nome hello specificato nel file di definizione del processo hello è già definito, verrà chiesto di cmdlet hello o meno tooreplace è.</span><span class="sxs-lookup"><span data-stu-id="25d8a-197">If an existing job with hello name specified in hello job definition file is already defined, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="25d8a-198">**Esempio 2**</span><span class="sxs-lookup"><span data-stu-id="25d8a-198">**Example 2**</span></span>

<span data-ttu-id="25d8a-199">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="25d8a-199">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

<span data-ttu-id="25d8a-200">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="25d8a-200">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

<span data-ttu-id="25d8a-201">Questo comando di PowerShell sostituisce la definizione di processo hello per StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="25d8a-201">This PowerShell command replaces hello job definition for StreamingJob.</span></span>

### <a name="new-azurestreamanalyticsoutput--new-azurermstreamanalyticsoutput"></a><span data-ttu-id="25d8a-202">New-AzureStreamAnalyticsOutput | New-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="25d8a-202">New-AzureStreamAnalyticsOutput | New-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="25d8a-203">Crea un nuovo output all'interno di un processo di Analisi dei flussi o aggiorna un output esistente.</span><span class="sxs-lookup"><span data-stu-id="25d8a-203">Creates a new output within a Stream Analytics job, or updates an existing output.</span></span>  

<span data-ttu-id="25d8a-204">nome di Hello dell'output di hello può essere specificato nel file con estensione JSON hello o sulla riga di comando hello.</span><span class="sxs-lookup"><span data-stu-id="25d8a-204">hello name of hello output can be specified in hello .json file or on hello command line.</span></span> <span data-ttu-id="25d8a-205">Se vengono specificati entrambi, il nome di hello nella riga di comando hello deve hello come hello file hello.</span><span class="sxs-lookup"><span data-stu-id="25d8a-205">If both are specified, hello name on hello command line must be hello same as hello one in hello file.</span></span>

<span data-ttu-id="25d8a-206">Se si specifica un output che esiste già e non si specifica hello: il parametro Force, hello cmdlet chiederà se tooreplace hello output esistente.</span><span class="sxs-lookup"><span data-stu-id="25d8a-206">If you specify an output that already exists and do not specify hello –Force parameter, hello cmdlet will ask whether or not tooreplace hello existing output.</span></span>

<span data-ttu-id="25d8a-207">Se si specificano hello – parametro Force e nome di output esistente, l'output di hello verrà sostituita senza conferma.</span><span class="sxs-lookup"><span data-stu-id="25d8a-207">If you specify hello –Force parameter and specify an existing output name, hello output will be replaced without confirmation.</span></span>

<span data-ttu-id="25d8a-208">Per informazioni dettagliate sulla struttura dei file JSON hello e il contenuto, vedere toohello [Create Output (Analitica del flusso di Azure)] [ msdn-rest-api-create-stream-analytics-output] sezione di hello [flusso Analitica API REST di gestione Libreria riferimenti a][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="25d8a-208">For detailed information on hello JSON file structure and contents, refer toohello [Create Output (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-output] section of hello [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="25d8a-209">**Esempio 1**</span><span class="sxs-lookup"><span data-stu-id="25d8a-209">**Example 1**</span></span>

<span data-ttu-id="25d8a-210">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="25d8a-210">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

<span data-ttu-id="25d8a-211">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="25d8a-211">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

<span data-ttu-id="25d8a-212">Questo comando di PowerShell crea un nuovo output chiamato "output" nel processo di hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="25d8a-212">This PowerShell command creates a new output called "output" in hello job StreamingJob.</span></span> <span data-ttu-id="25d8a-213">Se un output esistente con questo nome è già definito, verrà chiesto di cmdlet hello o meno tooreplace è.</span><span class="sxs-lookup"><span data-stu-id="25d8a-213">If an existing output with this name is already defined, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="25d8a-214">**Esempio 2**</span><span class="sxs-lookup"><span data-stu-id="25d8a-214">**Example 2**</span></span>

<span data-ttu-id="25d8a-215">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="25d8a-215">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

<span data-ttu-id="25d8a-216">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="25d8a-216">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

<span data-ttu-id="25d8a-217">Questo comando di PowerShell sostituisce definizione hello per "output" nel processo di hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="25d8a-217">This PowerShell command replaces hello definition for "output" in hello job StreamingJob.</span></span>

### <a name="new-azurestreamanalyticstransformation--new-azurermstreamanalyticstransformation"></a><span data-ttu-id="25d8a-218">New-AzureStreamAnalyticsTransformation | New-AzureRMStreamAnalyticsTransformation</span><span class="sxs-lookup"><span data-stu-id="25d8a-218">New-AzureStreamAnalyticsTransformation | New-AzureRMStreamAnalyticsTransformation</span></span>
<span data-ttu-id="25d8a-219">Crea una nuova trasformazione in un processo di flusso Analitica o aggiorna una trasformazione esistente hello.</span><span class="sxs-lookup"><span data-stu-id="25d8a-219">Creates a new transformation within a Stream Analytics job, or updates hello existing transformation.</span></span>

<span data-ttu-id="25d8a-220">nome di Hello della trasformazione hello può essere specificato nel file con estensione JSON hello o sulla riga di comando hello.</span><span class="sxs-lookup"><span data-stu-id="25d8a-220">hello name of hello transformation can be specified in hello .json file or on hello command line.</span></span> <span data-ttu-id="25d8a-221">Se vengono specificati entrambi, il nome di hello nella riga di comando hello deve hello come hello file hello.</span><span class="sxs-lookup"><span data-stu-id="25d8a-221">If both are specified, hello name on hello command line must be hello same as hello one in hello file.</span></span>

<span data-ttu-id="25d8a-222">Se si specifica una trasformazione che esiste già e non si specifica hello: il parametro Force, hello cmdlet chiederà se tooreplace hello trasformazione esistente.</span><span class="sxs-lookup"><span data-stu-id="25d8a-222">If you specify a transformation that already exists and do not specify hello –Force parameter, hello cmdlet will ask whether or not tooreplace hello existing transformation.</span></span>

<span data-ttu-id="25d8a-223">Se si specifica hello – parametro Force e specificare un nome di trasformazione esistente verrà sostituito trasformazione hello senza conferma.</span><span class="sxs-lookup"><span data-stu-id="25d8a-223">If you specify hello –Force parameter and specify an existing transformation name, hello transformation will be replaced without confirmation.</span></span>

<span data-ttu-id="25d8a-224">Per informazioni dettagliate sulla struttura dei file JSON hello e il contenuto, vedere toohello [Create Transformation (Analitica del flusso di Azure)] [ msdn-rest-api-create-stream-analytics-transformation] sezione di hello [gestione Analitica di flusso Raccolta di informazioni di riferimento API REST][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="25d8a-224">For detailed information on hello JSON file structure and contents, refer toohello [Create Transformation (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-transformation] section of hello [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="25d8a-225">**Esempio 1**</span><span class="sxs-lookup"><span data-stu-id="25d8a-225">**Example 1**</span></span>

<span data-ttu-id="25d8a-226">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="25d8a-226">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

<span data-ttu-id="25d8a-227">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="25d8a-227">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

<span data-ttu-id="25d8a-228">Questo comando di PowerShell crea una nuova trasformazione chiamata StreamingJobTransform nel processo di hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="25d8a-228">This PowerShell command creates a new transformation called StreamingJobTransform in hello job StreamingJob.</span></span> <span data-ttu-id="25d8a-229">Se una trasformazione esistente è già stata definita con lo stesso nome, verrà chiesto di cmdlet hello o meno tooreplace è.</span><span class="sxs-lookup"><span data-stu-id="25d8a-229">If an existing transformation is already defined with this name, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="25d8a-230">**Esempio 2**</span><span class="sxs-lookup"><span data-stu-id="25d8a-230">**Example 2**</span></span>

<span data-ttu-id="25d8a-231">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="25d8a-231">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

<span data-ttu-id="25d8a-232">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="25d8a-232">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

 <span data-ttu-id="25d8a-233">Questo comando di PowerShell sostituisce la definizione di hello di StreamingJobTransform nel processo di hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="25d8a-233">This PowerShell command replaces hello definition of StreamingJobTransform in hello job StreamingJob.</span></span>

### <a name="remove-azurestreamanalyticsinput--remove-azurermstreamanalyticsinput"></a><span data-ttu-id="25d8a-234">Remove-AzureStreamAnalyticsInput | Remove-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="25d8a-234">Remove-AzureStreamAnalyticsInput | Remove-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="25d8a-235">Elimina in modo asincrono uno specifico input da un processo di Analisi dei flussi in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="25d8a-235">Asynchronously deletes a specific input from a Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="25d8a-236">Se si specifica hello – parametro Force, hello di input verrà eliminato senza conferma.</span><span class="sxs-lookup"><span data-stu-id="25d8a-236">If you specify hello –Force parameter, hello input will be deleted without confirmation.</span></span>

<span data-ttu-id="25d8a-237">**Esempio 1**</span><span class="sxs-lookup"><span data-stu-id="25d8a-237">**Example 1**</span></span>

<span data-ttu-id="25d8a-238">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="25d8a-238">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

<span data-ttu-id="25d8a-239">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="25d8a-239">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

<span data-ttu-id="25d8a-240">Questo comando di PowerShell rimuove hello EventStream input nel processo di hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="25d8a-240">This PowerShell command removes hello input EventStream in hello job StreamingJob.</span></span>  

### <a name="remove-azurestreamanalyticsjob--remove-azurermstreamanalyticsjob"></a><span data-ttu-id="25d8a-241">Remove-AzureStreamAnalyticsJob | Remove-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="25d8a-241">Remove-AzureStreamAnalyticsJob | Remove-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="25d8a-242">Elimina in modo asincrono uno specifico processo di Analisi dei flussi in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="25d8a-242">Asynchronously deletes a specific Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="25d8a-243">Se si specifica hello: il parametro Force, hello processo sarà eliminato senza conferma.</span><span class="sxs-lookup"><span data-stu-id="25d8a-243">If you specify hello –Force parameter, hello job will be deleted without confirmation.</span></span>

<span data-ttu-id="25d8a-244">**Esempio 1**</span><span class="sxs-lookup"><span data-stu-id="25d8a-244">**Example 1**</span></span>

<span data-ttu-id="25d8a-245">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="25d8a-245">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="25d8a-246">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="25d8a-246">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="25d8a-247">Questo comando di PowerShell rimuove il processo di hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="25d8a-247">This PowerShell command removes hello job StreamingJob.</span></span>  

### <a name="remove-azurestreamanalyticsoutput--remove-azurermstreamanalyticsoutput"></a><span data-ttu-id="25d8a-248">Remove-AzureStreamAnalyticsOutput | Remove-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="25d8a-248">Remove-AzureStreamAnalyticsOutput | Remove-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="25d8a-249">Elimina in modo asincrono uno specifico output da un processo di Analisi dei flussi in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="25d8a-249">Asynchronously deletes a specific output from a Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="25d8a-250">Se si specifica hello: il parametro Force, hello output sarà eliminato senza conferma.</span><span class="sxs-lookup"><span data-stu-id="25d8a-250">If you specify hello –Force parameter, hello output will be deleted without confirmation.</span></span>

<span data-ttu-id="25d8a-251">**Esempio 1**</span><span class="sxs-lookup"><span data-stu-id="25d8a-251">**Example 1**</span></span>

<span data-ttu-id="25d8a-252">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="25d8a-252">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="25d8a-253">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="25d8a-253">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="25d8a-254">Questo comando di PowerShell rimuove hello output Output nel processo di hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="25d8a-254">This PowerShell command removes hello output Output in hello job StreamingJob.</span></span>  

### <a name="start-azurestreamanalyticsjob--start-azurermstreamanalyticsjob"></a><span data-ttu-id="25d8a-255">Start-AzureStreamAnalyticsJob | Start-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="25d8a-255">Start-AzureStreamAnalyticsJob | Start-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="25d8a-256">In modo asincrono e avvia un processo di Analisi dei flussi in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="25d8a-256">Asynchronously deploys and starts a Stream Analytics job in Microsoft Azure.</span></span>

<span data-ttu-id="25d8a-257">**Esempio 1**</span><span class="sxs-lookup"><span data-stu-id="25d8a-257">**Example 1**</span></span>

<span data-ttu-id="25d8a-258">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="25d8a-258">Azure PowerShell 0.9.8:</span></span>  

    Start-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

<span data-ttu-id="25d8a-259">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="25d8a-259">Azure PowerShell 1.0:</span></span>  

    Start-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

<span data-ttu-id="25d8a-260">Questo comando di PowerShell avvia hello processo StreamingJob con un'ora di inizio di output personalizzato impostato tooDecember 12, 2012, 12:12:12 UTC.</span><span class="sxs-lookup"><span data-stu-id="25d8a-260">This PowerShell command starts hello job StreamingJob with a custom output start time set tooDecember 12, 2012, 12:12:12 UTC.</span></span>

### <a name="stop-azurestreamanalyticsjob--stop-azurermstreamanalyticsjob"></a><span data-ttu-id="25d8a-261">Stop-AzureStreamAnalyticsJob | Stop-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="25d8a-261">Stop-AzureStreamAnalyticsJob | Stop-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="25d8a-262">Interrompe in modo asincrono l'esecuzione di un processo di Analisi dei flussi in Microsoft Azure e dealloca le risorse in uso.</span><span class="sxs-lookup"><span data-stu-id="25d8a-262">Asynchronously stops a Stream Analytics job from running in Microsoft Azure and de-allocates resources that were that were being used.</span></span> <span data-ttu-id="25d8a-263">Hello metadati e definizione del processo saranno comunque disponibili nella sottoscrizione tramite il portale di Azure hello e API di gestione, in modo che hello processo può essere modificato e riavviato.</span><span class="sxs-lookup"><span data-stu-id="25d8a-263">hello job definition and metadata will remain available within your subscription through both hello Azure portal and management APIs, such that hello job can be edited and restarted.</span></span> <span data-ttu-id="25d8a-264">È non verrà addebitato un processo in stato arrestato hello.</span><span class="sxs-lookup"><span data-stu-id="25d8a-264">You will not be charged for a job in hello stopped state.</span></span>

<span data-ttu-id="25d8a-265">**Esempio 1**</span><span class="sxs-lookup"><span data-stu-id="25d8a-265">**Example 1**</span></span>

<span data-ttu-id="25d8a-266">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="25d8a-266">Azure PowerShell 0.9.8:</span></span>  

    Stop-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="25d8a-267">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="25d8a-267">Azure PowerShell 1.0:</span></span>  

    Stop-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="25d8a-268">Questo comando di PowerShell Arresta il processo di hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="25d8a-268">This PowerShell command stops hello job StreamingJob.</span></span>  

### <a name="test-azurestreamanalyticsinput--test-azurermstreamanalyticsinput"></a><span data-ttu-id="25d8a-269">Test-AzureStreamAnalyticsInput | Test-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="25d8a-269">Test-AzureStreamAnalyticsInput | Test-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="25d8a-270">Possibilità di hello test del flusso Analitica tooconnect tooa specificato di input.</span><span class="sxs-lookup"><span data-stu-id="25d8a-270">Tests hello ability of Stream Analytics tooconnect tooa specified input.</span></span>

<span data-ttu-id="25d8a-271">**Esempio 1**</span><span class="sxs-lookup"><span data-stu-id="25d8a-271">**Example 1**</span></span>

<span data-ttu-id="25d8a-272">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="25d8a-272">Azure PowerShell 0.9.8:</span></span>  

    Test-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

<span data-ttu-id="25d8a-273">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="25d8a-273">Azure PowerShell 1.0:</span></span>  

    Test-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

<span data-ttu-id="25d8a-274">Questo stato di connessione PowerShell comando test hello di hello EntryStream in StreamingJob di input.</span><span class="sxs-lookup"><span data-stu-id="25d8a-274">This PowerShell command tests hello connection status of hello input EntryStream in StreamingJob.</span></span>  

### <a name="test-azurestreamanalyticsoutput--test-azurermstreamanalyticsoutput"></a><span data-ttu-id="25d8a-275">Test-AzureStreamAnalyticsOutput | Test-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="25d8a-275">Test-AzureStreamAnalyticsOutput | Test-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="25d8a-276">Possibilità di hello test del flusso Analitica tooconnect tooa specificato output.</span><span class="sxs-lookup"><span data-stu-id="25d8a-276">Tests hello ability of Stream Analytics tooconnect tooa specified output.</span></span>

<span data-ttu-id="25d8a-277">**Esempio 1**</span><span class="sxs-lookup"><span data-stu-id="25d8a-277">**Example 1**</span></span>

<span data-ttu-id="25d8a-278">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="25d8a-278">Azure PowerShell 0.9.8:</span></span>  

    Test-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="25d8a-279">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="25d8a-279">Azure PowerShell 1.0:</span></span>  

    Test-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="25d8a-280">Questo stato di connessione PowerShell comando test hello di hello output Output in StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="25d8a-280">This PowerShell command tests hello connection status of hello output Output in StreamingJob.</span></span>  

## <a name="get-support"></a><span data-ttu-id="25d8a-281">Supporto</span><span class="sxs-lookup"><span data-stu-id="25d8a-281">Get support</span></span>
<span data-ttu-id="25d8a-282">Per ulteriore assistenza, provare il [Forum di Analisi dei flussi di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="25d8a-282">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="25d8a-283">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="25d8a-283">Next steps</span></span>
* [<span data-ttu-id="25d8a-284">Introduzione tooAzure flusso Analitica</span><span class="sxs-lookup"><span data-stu-id="25d8a-284">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="25d8a-285">Introduzione all'uso di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="25d8a-285">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="25d8a-286">Ridimensionare i processi di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="25d8a-286">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="25d8a-287">Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="25d8a-287">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="25d8a-288">Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="25d8a-288">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

[msdn-switch-azuremode]: http://msdn.microsoft.com/library/dn722470.aspx
[powershell-install]: http://azure.microsoft.com/documentation/articles/powershell-install-configure/
[msdn-rest-api-create-stream-analytics-job]: https://msdn.microsoft.com/library/dn834994.aspx
[msdn-rest-api-create-stream-analytics-input]: https://msdn.microsoft.com/library/dn835010.aspx
[msdn-rest-api-create-stream-analytics-output]: https://msdn.microsoft.com/library/dn835015.aspx
[msdn-rest-api-create-stream-analytics-transformation]: https://msdn.microsoft.com/library/dn835007.aspx

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301

