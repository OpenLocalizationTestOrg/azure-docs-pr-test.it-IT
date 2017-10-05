---
title: Monitorare e gestire i processi dell'analisi di flusso con PowerShell | Microsoft Docs
description: Informazioni su come usare Azure PowerShell e i cmdlet per monitorare e gestire i processi di Analisi di flusso.
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
ms.openlocfilehash: e3449ee90cc83c5e823e5948a2a2e7e633c454f1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="monitor-and-manage-stream-analytics-jobs-with-azure-powershell-cmdlets"></a><span data-ttu-id="34022-104">Monitorare e gestire i processi di Analisi di flusso con i cmdlet di Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="34022-104">Monitor and manage Stream Analytics jobs with Azure PowerShell cmdlets</span></span>
<span data-ttu-id="34022-105">Informazioni su come monitorare e gestire le risorse di Analisi di flusso con i cmdlet di Azure PowerShell e gli script di PowerShell che eseguono attività di base di Analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="34022-105">Learn how to monitor and manage Stream Analytics resources with Azure PowerShell cmdlets and powershell scripting that execute basic Stream Analytics tasks.</span></span>

## <a name="prerequisites-for-running-azure-powershell-cmdlets-for-stream-analytics"></a><span data-ttu-id="34022-106">Prerequisiti per l'esecuzione dei cmdlet di Azure PowerShell per Analisi dei flussi</span><span class="sxs-lookup"><span data-stu-id="34022-106">Prerequisites for running Azure PowerShell cmdlets for Stream Analytics</span></span>
* <span data-ttu-id="34022-107">Creare un gruppo di risorse di Azure nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="34022-107">Create an Azure Resource Group in your subscription.</span></span> <span data-ttu-id="34022-108">Di seguito è riportato un esempio di script di Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="34022-108">The following is a sample Azure PowerShell script.</span></span> <span data-ttu-id="34022-109">Per informazioni su Azure PowerShell , vedere [Installare e configurare Azure PowerShell](/powershell/azure/overview);</span><span class="sxs-lookup"><span data-stu-id="34022-109">For Azure PowerShell information, see [Install and configure Azure PowerShell](/powershell/azure/overview);</span></span>  

<span data-ttu-id="34022-110">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="34022-110">Azure PowerShell 0.9.8:</span></span>  

         # Log in to your Azure account
        Add-AzureAccount

        # Select the Azure subscription you want to use to create the resource group if you have more than one subscription on your account.
        Select-AzureSubscription -SubscriptionName <subscription name>

        # If Stream Analytics has not been registered to the subscription, remove remark symbol below (#) to run the Register-AzureProvider cmdlet to register the provider namespace.
        #Register-AzureProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>

<span data-ttu-id="34022-111">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="34022-111">Azure PowerShell 1.0:</span></span>  

         # Log in to your Azure account
        Login-AzureRmAccount

        # Select the Azure subscription you want to use to create the resource group.
        Get-AzureRmSubscription –SubscriptionName “your sub” | Select-AzureRmSubscription

        # If Stream Analytics has not been registered to the subscription, remove remark symbol below (#) to run the Register-AzureProvider cmdlet to register the provider namespace.
        #Register-AzureRmResourceProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureRMResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>



> [!NOTE]
> <span data-ttu-id="34022-112">Nei processi di Analisi di flusso creati a livello di codice il monitoraggio non è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="34022-112">Stream Analytics jobs created programmatically do not have monitoring enabled by default.</span></span>  <span data-ttu-id="34022-113">Il monitoraggio può essere attivato manualmente nel portale di Azure passando alla pagina Monitoraggio del processo e facendo clic sul pulsante Attiva o procedere a livello di codice seguendo i passaggi in [Analisi di flusso di Azure - Monitorare i processi di analisi di flusso a livello di codice](stream-analytics-monitor-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="34022-113">You can manually enable monitoring in the Azure Portal by navigating to the job’s Monitor page and clicking the Enable button or you can do this programmatically by following the steps located at [Azure Stream Analytics - Monitor Stream Analytics Jobs Programatically](stream-analytics-monitor-jobs.md).</span></span>
> 
> 

## <a name="azure-powershell-cmdlets-for-stream-analytics"></a><span data-ttu-id="34022-114">Cmdlet di Azure PowerShell per Analisi dei flussi</span><span class="sxs-lookup"><span data-stu-id="34022-114">Azure PowerShell cmdlets for Stream Analytics</span></span>
<span data-ttu-id="34022-115">I cmdlet di Azure PowerShell indicati di seguito possono essere utilizzati per monitorare e gestire i processi di Analisi dei flussi di Azure.</span><span class="sxs-lookup"><span data-stu-id="34022-115">The following Azure PowerShell cmdlets can be used to monitor and manage Azure Stream Analytics jobs.</span></span> <span data-ttu-id="34022-116">Si noti che sono disponibili diverse versioni di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="34022-116">Note that Azure PowerShell has different versions.</span></span> 
<span data-ttu-id="34022-117">**Negli esempi elencati il primo comando è per Azure PowerShell 0.9.8, il secondo comando è per Azure PowerShell 1.0.**</span><span class="sxs-lookup"><span data-stu-id="34022-117">**In the examples listed the first command is for Azure PowerShell 0.9.8, the second command is for Azure PowerShell 1.0.**</span></span> <span data-ttu-id="34022-118">Nei comandi di Azure PowerShell 1.0 è sempre presente "AzureRM".</span><span class="sxs-lookup"><span data-stu-id="34022-118">The Azure PowerShell 1.0 commands will always have "AzureRM" in the command.</span></span>

### <a name="get-azurestreamanalyticsjob--get-azurermstreamanalyticsjob"></a><span data-ttu-id="34022-119">Get-AzureStreamAnalyticsJob | Get-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="34022-119">Get-AzureStreamAnalyticsJob | Get-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="34022-120">Elenca tutti i processi di Analisi dei flussi definiti nella sottoscrizione di Azure o nel gruppo di risorse specificato oppure ottiene informazioni su uno specifico processo all'interno di un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="34022-120">Lists all Stream Analytics jobs defined in the Azure subscription or specified resource group, or gets job information about a specific job within a resource group.</span></span>

<span data-ttu-id="34022-121">**Esempio 1**</span><span class="sxs-lookup"><span data-stu-id="34022-121">**Example 1**</span></span>

<span data-ttu-id="34022-122">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="34022-122">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob

<span data-ttu-id="34022-123">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="34022-123">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob

<span data-ttu-id="34022-124">Questo comando PowerShell restituisce informazioni su tutti i processi di Analisi di flusso nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="34022-124">This PowerShell command returns information about all the Stream Analytics jobs in the Azure subscription.</span></span>

<span data-ttu-id="34022-125">**Esempio 2**</span><span class="sxs-lookup"><span data-stu-id="34022-125">**Example 2**</span></span>

<span data-ttu-id="34022-126">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="34022-126">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

<span data-ttu-id="34022-127">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="34022-127">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

<span data-ttu-id="34022-128">Questo comando di PowerShell restituisce informazioni su tutti i processi di Analisi di flusso nel gruppo di risorse StreamAnalytics-Default-Central-US.</span><span class="sxs-lookup"><span data-stu-id="34022-128">This PowerShell command returns information about all the Stream Analytics jobs in the resource group StreamAnalytics-Default-Central-US.</span></span>

<span data-ttu-id="34022-129">**Esempio 3**</span><span class="sxs-lookup"><span data-stu-id="34022-129">**Example 3**</span></span>

<span data-ttu-id="34022-130">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="34022-130">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

<span data-ttu-id="34022-131">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="34022-131">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

<span data-ttu-id="34022-132">Questo comando di PowerShell restituisce informazioni sul processo StreamingJob di Analisi di flusso nel gruppo di risorse StreamAnalytics-Default-West-US.</span><span class="sxs-lookup"><span data-stu-id="34022-132">This PowerShell command returns information about the Stream Analytics job StreamingJob in the resource group StreamAnalytics-Default-Central-US.</span></span>

### <a name="get-azurestreamanalyticsinput--get-azurermstreamanalyticsinput"></a><span data-ttu-id="34022-133">Get-AzureStreamAnalyticsInput | Get-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="34022-133">Get-AzureStreamAnalyticsInput | Get-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="34022-134">Elenca tutti gli input definiti in un processo di Analisi dei flussi specificato oppure ottiene informazioni su un input specifico.</span><span class="sxs-lookup"><span data-stu-id="34022-134">Lists all of the inputs that are defined in a specified Stream Analytics job, or gets information about a specific input.</span></span>

<span data-ttu-id="34022-135">**Esempio 1**</span><span class="sxs-lookup"><span data-stu-id="34022-135">**Example 1**</span></span>

<span data-ttu-id="34022-136">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="34022-136">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="34022-137">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="34022-137">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="34022-138">Questo comando di PowerShell restituisce informazioni su tutti gli input definiti nel processo StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="34022-138">This PowerShell command returns information about all the inputs defined in the job StreamingJob.</span></span>

<span data-ttu-id="34022-139">**Esempio 2**</span><span class="sxs-lookup"><span data-stu-id="34022-139">**Example 2**</span></span>

<span data-ttu-id="34022-140">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="34022-140">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

<span data-ttu-id="34022-141">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="34022-141">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

<span data-ttu-id="34022-142">Questo comando di PowerShell restituisce informazioni sull'input denominato EntryStream definito nel processo StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="34022-142">This PowerShell command returns information about the input named EntryStream defined in the job StreamingJob.</span></span>

### <a name="get-azurestreamanalyticsoutput--get-azurermstreamanalyticsoutput"></a><span data-ttu-id="34022-143">Get-AzureStreamAnalyticsOutput | Get-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="34022-143">Get-AzureStreamAnalyticsOutput | Get-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="34022-144">Elenca tutti gli output definiti in un processo di Analisi dei flussi specificato oppure ottiene informazioni su un output specifico.</span><span class="sxs-lookup"><span data-stu-id="34022-144">Lists all of the outputs that are defined in a specified Stream Analytics job, or gets information about a specific output.</span></span>

<span data-ttu-id="34022-145">**Esempio 1**</span><span class="sxs-lookup"><span data-stu-id="34022-145">**Example 1**</span></span>

<span data-ttu-id="34022-146">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="34022-146">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="34022-147">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="34022-147">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="34022-148">Questo comando di PowerShell restituisce informazioni sugli output definiti nel processo StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="34022-148">This PowerShell command returns information about the outputs defined in the job StreamingJob.</span></span>

<span data-ttu-id="34022-149">**Esempio 2**</span><span class="sxs-lookup"><span data-stu-id="34022-149">**Example 2**</span></span>

<span data-ttu-id="34022-150">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="34022-150">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

<span data-ttu-id="34022-151">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="34022-151">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

<span data-ttu-id="34022-152">Questo comando di PowerShell restituisce informazioni sull'output denominato Output definito nel processo StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="34022-152">This PowerShell command returns information about the output named Output defined in the job StreamingJob.</span></span>

### <a name="get-azurestreamanalyticsquota--get-azurermstreamanalyticsquota"></a><span data-ttu-id="34022-153">Get-AzureStreamAnalyticsQuota | Get-AzureRMStreamAnalyticsQuota</span><span class="sxs-lookup"><span data-stu-id="34022-153">Get-AzureStreamAnalyticsQuota | Get-AzureRMStreamAnalyticsQuota</span></span>
<span data-ttu-id="34022-154">Ottiene informazioni sulla quota di unità di streaming di un'area specificata.</span><span class="sxs-lookup"><span data-stu-id="34022-154">Gets information about the quota of streaming units in a specified region.</span></span>

<span data-ttu-id="34022-155">**Esempio 1**</span><span class="sxs-lookup"><span data-stu-id="34022-155">**Example 1**</span></span>

<span data-ttu-id="34022-156">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="34022-156">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsQuota –Location "Central US" 

<span data-ttu-id="34022-157">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="34022-157">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsQuota –Location "Central US" 

<span data-ttu-id="34022-158">Questo comando di PowerShell restituisce informazioni sulla quota di unità di streaming e sul relativo utilizzo nell'area Stati Uniti centrali.</span><span class="sxs-lookup"><span data-stu-id="34022-158">This PowerShell command returns information about the quota and usage of streaming units in the Central US region.</span></span>

### <a name="get-azurestreamanalyticstransformation--getazurermstreamanalyticstransformation"></a><span data-ttu-id="34022-159">Get-AzureStreamAnalyticsTransformation | GetAzureRMStreamAnalyticsTransformation</span><span class="sxs-lookup"><span data-stu-id="34022-159">Get-AzureStreamAnalyticsTransformation | GetAzureRMStreamAnalyticsTransformation</span></span>
<span data-ttu-id="34022-160">Ottiene informazioni su una specifica trasformazione definita nel processo di Analisi dei flussi.</span><span class="sxs-lookup"><span data-stu-id="34022-160">Gets information about a specific transformation defined in a Stream Analytics job.</span></span>

<span data-ttu-id="34022-161">**Esempio 1**</span><span class="sxs-lookup"><span data-stu-id="34022-161">**Example 1**</span></span>

<span data-ttu-id="34022-162">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="34022-162">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

<span data-ttu-id="34022-163">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="34022-163">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

<span data-ttu-id="34022-164">Questo comando di PowerShell restituisce informazioni sulla trasformazione denominata StreamingJob nel processo StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="34022-164">This PowerShell command returns information about the transformation called StreamingJob in the job StreamingJob.</span></span>

### <a name="new-azurestreamanalyticsinput--new-azurermstreamanalyticsinput"></a><span data-ttu-id="34022-165">New-AzureStreamAnalyticsInput | New-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="34022-165">New-AzureStreamAnalyticsInput | New-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="34022-166">Crea un nuovo input all'interno di un processo di Analisi dei flussi o aggiorna un input esistente specificato.</span><span class="sxs-lookup"><span data-stu-id="34022-166">Creates a new input within a Stream Analytics job, or updates an existing specified input.</span></span>

<span data-ttu-id="34022-167">Il nome dell'input può essere specificato nel file json o nella riga di comando.</span><span class="sxs-lookup"><span data-stu-id="34022-167">The name of the input can be specified in the .json file or on the command line.</span></span> <span data-ttu-id="34022-168">Se vengono specificati entrambi, il nome nella riga di comando deve corrispondere a quello nel file.</span><span class="sxs-lookup"><span data-stu-id="34022-168">If both are specified, the name on the command line must be the same as the one in the file.</span></span>

<span data-ttu-id="34022-169">Se si specifica un input già esistente e non si specifica il parametro –Force, il cmdlet chiederà se si desidera sostituire l'input esistente.</span><span class="sxs-lookup"><span data-stu-id="34022-169">If you specify an input that already exists and do not specify the –Force parameter, the cmdlet will ask whether or not to replace the existing input.</span></span>

<span data-ttu-id="34022-170">Se si specifica un nome di input esistente usando il parametro –Force, l'input verrà sostituito senza chiedere conferma.</span><span class="sxs-lookup"><span data-stu-id="34022-170">If you specify the –Force parameter and specify an existing input name, the input will be replaced without confirmation.</span></span>

<span data-ttu-id="34022-171">Per informazioni dettagliate sulla struttura e sul contenuto dei file JSON, vedere la sezione [Create Input (Analisi di flusso di Azure)][msdn-rest-api-create-stream-analytics-input] della [libreria di riferimento delle API REST di gestione di Analisi di flusso di Azure][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="34022-171">For detailed information on the JSON file structure and contents, refer to the [Create Input (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-input] section of the [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="34022-172">**Esempio 1**</span><span class="sxs-lookup"><span data-stu-id="34022-172">**Example 1**</span></span>

<span data-ttu-id="34022-173">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="34022-173">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

<span data-ttu-id="34022-174">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="34022-174">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

<span data-ttu-id="34022-175">Questo comando di PowerShell crea un nuovo input dal file Input.json.</span><span class="sxs-lookup"><span data-stu-id="34022-175">This PowerShell command creates a new input from the file Input.json.</span></span> <span data-ttu-id="34022-176">Se è già definito un input esistente con il nome specificato nel file di definizione dell'input, il cmdlet chiederà se si desidera sostituirlo.</span><span class="sxs-lookup"><span data-stu-id="34022-176">If an existing input with the name specified in the input definition file is already defined, the cmdlet will ask whether or not to replace it.</span></span>

<span data-ttu-id="34022-177">**Esempio 2**</span><span class="sxs-lookup"><span data-stu-id="34022-177">**Example 2**</span></span>

<span data-ttu-id="34022-178">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="34022-178">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

<span data-ttu-id="34022-179">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="34022-179">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

<span data-ttu-id="34022-180">Questo comando di PowerShell crea un nuovo input nel processo denominato EntryStream.</span><span class="sxs-lookup"><span data-stu-id="34022-180">This PowerShell command creates a new input in the job called EntryStream.</span></span> <span data-ttu-id="34022-181">Se un input esistente con questo nome è già definito, il cmdlet chiederà se si desidera sostituirlo.</span><span class="sxs-lookup"><span data-stu-id="34022-181">If an existing input with this name is already defined, the cmdlet will ask whether or not to replace it.</span></span>

<span data-ttu-id="34022-182">**Esempio 3**</span><span class="sxs-lookup"><span data-stu-id="34022-182">**Example 3**</span></span>

<span data-ttu-id="34022-183">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="34022-183">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

<span data-ttu-id="34022-184">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="34022-184">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

<span data-ttu-id="34022-185">Questo comando di PowerShell sostituisce la definizione dell'origine di input esistente, denominata EntryStream, con la definizione presente nel file.</span><span class="sxs-lookup"><span data-stu-id="34022-185">This PowerShell command replaces the definition of the existing input source called EntryStream with the definition from the file.</span></span>

### <a name="new-azurestreamanalyticsjob--new-azurermstreamanalyticsjob"></a><span data-ttu-id="34022-186">New-AzureStreamAnalyticsJob | New-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="34022-186">New-AzureStreamAnalyticsJob | New-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="34022-187">Crea un nuovo processo di Analisi dei flussi in Microsoft Azure o aggiorna la definizione di un processo esistente specificato.</span><span class="sxs-lookup"><span data-stu-id="34022-187">Creates a new Stream Analytics job in Microsoft Azure, or updates the definition of an existing specified job.</span></span>

<span data-ttu-id="34022-188">Il nome del processo può essere specificato nel file json o nella riga di comando.</span><span class="sxs-lookup"><span data-stu-id="34022-188">The name of the job can be specified in the .json file or on the command line.</span></span> <span data-ttu-id="34022-189">Se vengono specificati entrambi, il nome nella riga di comando deve corrispondere a quello nel file.</span><span class="sxs-lookup"><span data-stu-id="34022-189">If both are specified, the name on the command line must be the same as the one in the file.</span></span>

<span data-ttu-id="34022-190">Se si specifica un nome di processo già esistente e non si specifica il parametro –Force, il cmdlet chiederà se si desidera sostituire il processo esistente.</span><span class="sxs-lookup"><span data-stu-id="34022-190">If you specify a job name that already exists and do not specify the –Force parameter, the cmdlet will ask whether or not to replace the existing job.</span></span>

<span data-ttu-id="34022-191">Se si specifica un nome di processo esistente usando il parametro –Force, la definizione del processo verrà sostituita senza chiedere conferma.</span><span class="sxs-lookup"><span data-stu-id="34022-191">If you specify the –Force parameter and specify an existing job name, the job definition will be replaced without confirmation.</span></span>

<span data-ttu-id="34022-192">Per informazioni dettagliate sulla struttura e sul contenuto dei file JSON, vedere la sezione [Create Stream (Analisi di flusso di Azure)][msdn-rest-api-create-stream-analytics-job] della [libreria di riferimento delle API REST di gestione di Analisi di flusso di Azure][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="34022-192">For detailed information on the JSON file structure and contents, refer to the [Create Stream Analytics Job][msdn-rest-api-create-stream-analytics-job] section of the [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="34022-193">**Esempio 1**</span><span class="sxs-lookup"><span data-stu-id="34022-193">**Example 1**</span></span>

<span data-ttu-id="34022-194">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="34022-194">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

<span data-ttu-id="34022-195">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="34022-195">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

<span data-ttu-id="34022-196">Questo comando di PowerShell crea un nuovo processo dalla definizione presente in JobDefinition.json.</span><span class="sxs-lookup"><span data-stu-id="34022-196">This PowerShell command creates a new job from the definition in JobDefinition.json.</span></span> <span data-ttu-id="34022-197">Se è già definito un processo esistente con il nome specificato nel file di definizione del processo, il cmdlet chiederà se si desidera sostituirlo.</span><span class="sxs-lookup"><span data-stu-id="34022-197">If an existing job with the name specified in the job definition file is already defined, the cmdlet will ask whether or not to replace it.</span></span>

<span data-ttu-id="34022-198">**Esempio 2**</span><span class="sxs-lookup"><span data-stu-id="34022-198">**Example 2**</span></span>

<span data-ttu-id="34022-199">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="34022-199">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

<span data-ttu-id="34022-200">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="34022-200">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

<span data-ttu-id="34022-201">Questo comando di PowerShell sostituisce la definizione del processo per StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="34022-201">This PowerShell command replaces the job definition for StreamingJob.</span></span>

### <a name="new-azurestreamanalyticsoutput--new-azurermstreamanalyticsoutput"></a><span data-ttu-id="34022-202">New-AzureStreamAnalyticsOutput | New-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="34022-202">New-AzureStreamAnalyticsOutput | New-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="34022-203">Crea un nuovo output all'interno di un processo di Analisi dei flussi o aggiorna un output esistente.</span><span class="sxs-lookup"><span data-stu-id="34022-203">Creates a new output within a Stream Analytics job, or updates an existing output.</span></span>  

<span data-ttu-id="34022-204">Il nome dell'output può essere specificato nel file json o nella riga di comando.</span><span class="sxs-lookup"><span data-stu-id="34022-204">The name of the output can be specified in the .json file or on the command line.</span></span> <span data-ttu-id="34022-205">Se vengono specificati entrambi, il nome nella riga di comando deve corrispondere a quello nel file.</span><span class="sxs-lookup"><span data-stu-id="34022-205">If both are specified, the name on the command line must be the same as the one in the file.</span></span>

<span data-ttu-id="34022-206">Se si specifica un output già esistente e non si specifica il parametro –Force, il cmdlet chiederà se si desidera sostituire l'output esistente.</span><span class="sxs-lookup"><span data-stu-id="34022-206">If you specify an output that already exists and do not specify the –Force parameter, the cmdlet will ask whether or not to replace the existing output.</span></span>

<span data-ttu-id="34022-207">Se si specifica un nome di output esistente usando il parametro –Force, l'output verrà sostituito senza chiedere conferma.</span><span class="sxs-lookup"><span data-stu-id="34022-207">If you specify the –Force parameter and specify an existing output name, the output will be replaced without confirmation.</span></span>

<span data-ttu-id="34022-208">Per informazioni dettagliate sulla struttura e sul contenuto dei file JSON, vedere la sezione [Create Output (Analisi di flusso di Azure)][msdn-rest-api-create-stream-analytics-output] della [libreria di riferimento delle API REST di gestione di Analisi di flusso di Azure][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="34022-208">For detailed information on the JSON file structure and contents, refer to the [Create Output (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-output] section of the [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="34022-209">**Esempio 1**</span><span class="sxs-lookup"><span data-stu-id="34022-209">**Example 1**</span></span>

<span data-ttu-id="34022-210">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="34022-210">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

<span data-ttu-id="34022-211">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="34022-211">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

<span data-ttu-id="34022-212">Questo comando di PowerShell crea un nuovo output denominato "output" nel processo StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="34022-212">This PowerShell command creates a new output called "output" in the job StreamingJob.</span></span> <span data-ttu-id="34022-213">Se un output esistente con questo nome è già definito, il cmdlet chiederà se si desidera sostituirlo.</span><span class="sxs-lookup"><span data-stu-id="34022-213">If an existing output with this name is already defined, the cmdlet will ask whether or not to replace it.</span></span>

<span data-ttu-id="34022-214">**Esempio 2**</span><span class="sxs-lookup"><span data-stu-id="34022-214">**Example 2**</span></span>

<span data-ttu-id="34022-215">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="34022-215">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

<span data-ttu-id="34022-216">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="34022-216">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

<span data-ttu-id="34022-217">Questo comando di PowerShell sostituisce la definizione di "output" nel processo StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="34022-217">This PowerShell command replaces the definition for "output" in the job StreamingJob.</span></span>

### <a name="new-azurestreamanalyticstransformation--new-azurermstreamanalyticstransformation"></a><span data-ttu-id="34022-218">New-AzureStreamAnalyticsTransformation | New-AzureRMStreamAnalyticsTransformation</span><span class="sxs-lookup"><span data-stu-id="34022-218">New-AzureStreamAnalyticsTransformation | New-AzureRMStreamAnalyticsTransformation</span></span>
<span data-ttu-id="34022-219">Crea una nuova trasformazione all'interno di un processo di Analisi dei flussi o aggiorna la trasformazione esistente.</span><span class="sxs-lookup"><span data-stu-id="34022-219">Creates a new transformation within a Stream Analytics job, or updates the existing transformation.</span></span>

<span data-ttu-id="34022-220">Il nome della trasformazione può essere specificato nel file json o nella riga di comando.</span><span class="sxs-lookup"><span data-stu-id="34022-220">The name of the transformation can be specified in the .json file or on the command line.</span></span> <span data-ttu-id="34022-221">Se vengono specificati entrambi, il nome nella riga di comando deve corrispondere a quello nel file.</span><span class="sxs-lookup"><span data-stu-id="34022-221">If both are specified, the name on the command line must be the same as the one in the file.</span></span>

<span data-ttu-id="34022-222">Se si specifica una trasformazione già esistente e non si specifica il parametro –Force, il cmdlet chiederà se si desidera sostituire la trasformazione esistente.</span><span class="sxs-lookup"><span data-stu-id="34022-222">If you specify a transformation that already exists and do not specify the –Force parameter, the cmdlet will ask whether or not to replace the existing transformation.</span></span>

<span data-ttu-id="34022-223">Se si specifica un nome di trasformazione esistente usando il parametro –Force, la trasformazione verrà sostituita senza chiedere conferma.</span><span class="sxs-lookup"><span data-stu-id="34022-223">If you specify the –Force parameter and specify an existing transformation name, the transformation will be replaced without confirmation.</span></span>

<span data-ttu-id="34022-224">Per informazioni dettagliate sulla struttura e sul contenuto dei file JSON, vedere la sezione [Create Transformation (Analisi di flusso di Azure)][msdn-rest-api-create-stream-analytics-transformation] della [libreria di riferimento delle API REST di gestione di Analisi di flusso di Azure][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="34022-224">For detailed information on the JSON file structure and contents, refer to the [Create Transformation (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-transformation] section of the [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="34022-225">**Esempio 1**</span><span class="sxs-lookup"><span data-stu-id="34022-225">**Example 1**</span></span>

<span data-ttu-id="34022-226">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="34022-226">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

<span data-ttu-id="34022-227">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="34022-227">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

<span data-ttu-id="34022-228">Questo comando di PowerShell crea una nuova trasformazione denominata StreamingJobTransform nel processo StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="34022-228">This PowerShell command creates a new transformation called StreamingJobTransform in the job StreamingJob.</span></span> <span data-ttu-id="34022-229">Se una trasformazione esistente con questo nome è già definita, il cmdlet chiederà se si desidera sostituirla.</span><span class="sxs-lookup"><span data-stu-id="34022-229">If an existing transformation is already defined with this name, the cmdlet will ask whether or not to replace it.</span></span>

<span data-ttu-id="34022-230">**Esempio 2**</span><span class="sxs-lookup"><span data-stu-id="34022-230">**Example 2**</span></span>

<span data-ttu-id="34022-231">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="34022-231">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

<span data-ttu-id="34022-232">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="34022-232">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

 <span data-ttu-id="34022-233">Questo comando di PowerShell sostituisce la definizione di StreamingJobTransform nel processo StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="34022-233">This PowerShell command replaces the definition of StreamingJobTransform in the job StreamingJob.</span></span>

### <a name="remove-azurestreamanalyticsinput--remove-azurermstreamanalyticsinput"></a><span data-ttu-id="34022-234">Remove-AzureStreamAnalyticsInput | Remove-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="34022-234">Remove-AzureStreamAnalyticsInput | Remove-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="34022-235">Elimina in modo asincrono uno specifico input da un processo di Analisi dei flussi in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="34022-235">Asynchronously deletes a specific input from a Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="34022-236">Se si specifica il parametro –Force, l'input verrà eliminato senza chiedere conferma.</span><span class="sxs-lookup"><span data-stu-id="34022-236">If you specify the –Force parameter, the input will be deleted without confirmation.</span></span>

<span data-ttu-id="34022-237">**Esempio 1**</span><span class="sxs-lookup"><span data-stu-id="34022-237">**Example 1**</span></span>

<span data-ttu-id="34022-238">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="34022-238">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

<span data-ttu-id="34022-239">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="34022-239">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

<span data-ttu-id="34022-240">Questo comando di PowerShell rimuove l'input EventStream nel processo StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="34022-240">This PowerShell command removes the input EventStream in the job StreamingJob.</span></span>  

### <a name="remove-azurestreamanalyticsjob--remove-azurermstreamanalyticsjob"></a><span data-ttu-id="34022-241">Remove-AzureStreamAnalyticsJob | Remove-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="34022-241">Remove-AzureStreamAnalyticsJob | Remove-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="34022-242">Elimina in modo asincrono uno specifico processo di Analisi dei flussi in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="34022-242">Asynchronously deletes a specific Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="34022-243">Se si specifica il parametro –Force, il processo verrà eliminato senza chiedere conferma.</span><span class="sxs-lookup"><span data-stu-id="34022-243">If you specify the –Force parameter, the job will be deleted without confirmation.</span></span>

<span data-ttu-id="34022-244">**Esempio 1**</span><span class="sxs-lookup"><span data-stu-id="34022-244">**Example 1**</span></span>

<span data-ttu-id="34022-245">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="34022-245">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="34022-246">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="34022-246">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="34022-247">Questo comando di PowerShell rimuove il processo StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="34022-247">This PowerShell command removes the job StreamingJob.</span></span>  

### <a name="remove-azurestreamanalyticsoutput--remove-azurermstreamanalyticsoutput"></a><span data-ttu-id="34022-248">Remove-AzureStreamAnalyticsOutput | Remove-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="34022-248">Remove-AzureStreamAnalyticsOutput | Remove-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="34022-249">Elimina in modo asincrono uno specifico output da un processo di Analisi dei flussi in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="34022-249">Asynchronously deletes a specific output from a Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="34022-250">Se si specifica il parametro –Force, l’output verrà eliminato senza chiedere conferma.</span><span class="sxs-lookup"><span data-stu-id="34022-250">If you specify the –Force parameter, the output will be deleted without confirmation.</span></span>

<span data-ttu-id="34022-251">**Esempio 1**</span><span class="sxs-lookup"><span data-stu-id="34022-251">**Example 1**</span></span>

<span data-ttu-id="34022-252">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="34022-252">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="34022-253">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="34022-253">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="34022-254">Questo comando di PowerShell rimuove l'output Output nel processo StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="34022-254">This PowerShell command removes the output Output in the job StreamingJob.</span></span>  

### <a name="start-azurestreamanalyticsjob--start-azurermstreamanalyticsjob"></a><span data-ttu-id="34022-255">Start-AzureStreamAnalyticsJob | Start-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="34022-255">Start-AzureStreamAnalyticsJob | Start-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="34022-256">In modo asincrono e avvia un processo di Analisi dei flussi in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="34022-256">Asynchronously deploys and starts a Stream Analytics job in Microsoft Azure.</span></span>

<span data-ttu-id="34022-257">**Esempio 1**</span><span class="sxs-lookup"><span data-stu-id="34022-257">**Example 1**</span></span>

<span data-ttu-id="34022-258">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="34022-258">Azure PowerShell 0.9.8:</span></span>  

    Start-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

<span data-ttu-id="34022-259">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="34022-259">Azure PowerShell 1.0:</span></span>  

    Start-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

<span data-ttu-id="34022-260">Questo comando di PowerShell avvia il processo StreamingJob con un'ora di inizio output personalizzata impostata su 12 dicembre 2012 12:12:12 UTC.</span><span class="sxs-lookup"><span data-stu-id="34022-260">This PowerShell command starts the job StreamingJob with a custom output start time set to December 12, 2012, 12:12:12 UTC.</span></span>

### <a name="stop-azurestreamanalyticsjob--stop-azurermstreamanalyticsjob"></a><span data-ttu-id="34022-261">Stop-AzureStreamAnalyticsJob | Stop-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="34022-261">Stop-AzureStreamAnalyticsJob | Stop-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="34022-262">Interrompe in modo asincrono l'esecuzione di un processo di Analisi dei flussi in Microsoft Azure e dealloca le risorse in uso.</span><span class="sxs-lookup"><span data-stu-id="34022-262">Asynchronously stops a Stream Analytics job from running in Microsoft Azure and de-allocates resources that were that were being used.</span></span> <span data-ttu-id="34022-263">La definizione del processo e i metadati rimarranno disponibili all'interno della sottoscrizione tramite il portale di Azure e le API di gestione, in modo che sia possibile modificare e riavviare il processo.</span><span class="sxs-lookup"><span data-stu-id="34022-263">The job definition and metadata will remain available within your subscription through both the Azure portal and management APIs, such that the job can be edited and restarted.</span></span> <span data-ttu-id="34022-264">Non si incorre in alcun addebito per un processo in stato Arrestato.</span><span class="sxs-lookup"><span data-stu-id="34022-264">You will not be charged for a job in the stopped state.</span></span>

<span data-ttu-id="34022-265">**Esempio 1**</span><span class="sxs-lookup"><span data-stu-id="34022-265">**Example 1**</span></span>

<span data-ttu-id="34022-266">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="34022-266">Azure PowerShell 0.9.8:</span></span>  

    Stop-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="34022-267">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="34022-267">Azure PowerShell 1.0:</span></span>  

    Stop-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="34022-268">Questo comando di PowerShell arresta il processo StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="34022-268">This PowerShell command stops the job StreamingJob.</span></span>  

### <a name="test-azurestreamanalyticsinput--test-azurermstreamanalyticsinput"></a><span data-ttu-id="34022-269">Test-AzureStreamAnalyticsInput | Test-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="34022-269">Test-AzureStreamAnalyticsInput | Test-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="34022-270">Verifica la capacità di Analisi dei flussi di connettersi a un input specificato.</span><span class="sxs-lookup"><span data-stu-id="34022-270">Tests the ability of Stream Analytics to connect to a specified input.</span></span>

<span data-ttu-id="34022-271">**Esempio 1**</span><span class="sxs-lookup"><span data-stu-id="34022-271">**Example 1**</span></span>

<span data-ttu-id="34022-272">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="34022-272">Azure PowerShell 0.9.8:</span></span>  

    Test-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

<span data-ttu-id="34022-273">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="34022-273">Azure PowerShell 1.0:</span></span>  

    Test-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

<span data-ttu-id="34022-274">Questo comando di PowerShell verifica lo stato di connessione dell'input EntryStream in StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="34022-274">This PowerShell command tests the connection status of the input EntryStream in StreamingJob.</span></span>  

### <a name="test-azurestreamanalyticsoutput--test-azurermstreamanalyticsoutput"></a><span data-ttu-id="34022-275">Test-AzureStreamAnalyticsOutput | Test-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="34022-275">Test-AzureStreamAnalyticsOutput | Test-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="34022-276">Verifica la capacità di Analisi dei flussi di connettersi a un output specificato.</span><span class="sxs-lookup"><span data-stu-id="34022-276">Tests the ability of Stream Analytics to connect to a specified output.</span></span>

<span data-ttu-id="34022-277">**Esempio 1**</span><span class="sxs-lookup"><span data-stu-id="34022-277">**Example 1**</span></span>

<span data-ttu-id="34022-278">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="34022-278">Azure PowerShell 0.9.8:</span></span>  

    Test-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="34022-279">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="34022-279">Azure PowerShell 1.0:</span></span>  

    Test-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="34022-280">Questo comando di PowerShell verifica lo stato di connessione dell'output Output in StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="34022-280">This PowerShell command tests the connection status of the output Output in StreamingJob.</span></span>  

## <a name="get-support"></a><span data-ttu-id="34022-281">Supporto</span><span class="sxs-lookup"><span data-stu-id="34022-281">Get support</span></span>
<span data-ttu-id="34022-282">Per ulteriore assistenza, provare il [Forum di Analisi dei flussi di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="34022-282">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="34022-283">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="34022-283">Next steps</span></span>
* [<span data-ttu-id="34022-284">Introduzione ad Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="34022-284">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="34022-285">Introduzione all'uso di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="34022-285">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="34022-286">Ridimensionare i processi di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="34022-286">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="34022-287">Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="34022-287">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="34022-288">Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="34022-288">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

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

