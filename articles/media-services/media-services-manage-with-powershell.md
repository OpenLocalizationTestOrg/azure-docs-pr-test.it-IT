---
title: Gestire gli account di Servizi multimediali di Azure con PowerShell
description: Informazioni su come gestire gli account di Servizi multimediali di Azure con i cmdlet di PowerShell.
author: Juliako
manager: erikre
editor: 
services: media-services
documentationcenter: 
ms.assetid: 17a10c25-d94f-421c-b6bc-ae0958e2ac96
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/03/2016
ms.author: juliako
ms.openlocfilehash: 3d999d9e27844bc0164cc3572522b9ec022118a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-media-services-accounts-with-powershell"></a><span data-ttu-id="02030-103">Gestire gli account di Servizi multimediali di Azure con PowerShell</span><span class="sxs-lookup"><span data-stu-id="02030-103">Manage Azure Media Services Accounts with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="02030-104">Portale</span><span class="sxs-lookup"><span data-stu-id="02030-104">Portal</span></span>](media-services-portal-create-account.md)
> * [<span data-ttu-id="02030-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="02030-105">PowerShell</span></span>](media-services-manage-with-powershell.md)
> * [<span data-ttu-id="02030-106">REST</span><span class="sxs-lookup"><span data-stu-id="02030-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/mediaservice)
> 
> [!NOTE]
> <span data-ttu-id="02030-107">Per poter creare un account di Servizi multimediali di Azure, è necessario un account di Azure.</span><span class="sxs-lookup"><span data-stu-id="02030-107">To be able to create an Azure Media Services account, you must have an Azure account.</span></span> <span data-ttu-id="02030-108">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="02030-108">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="02030-109">Per informazioni dettagliate, vedere la pagina relativa alla <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A8A8397B5" target="_blank">versione di valutazione gratuita di Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="02030-109">For details, see <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A8A8397B5" target="_blank">Azure Free Trial</a>.</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="02030-110">Panoramica</span><span class="sxs-lookup"><span data-stu-id="02030-110">Overview</span></span>
<span data-ttu-id="02030-111">Questo articolo fornisce un elenco dei cmdlet di Azure PowerShell per Servizi multimediali di Azure (AMS) nel framework di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="02030-111">This article lists the Azure PowerShell cmdlets for Azure Media Services (AMS) in the Azure Resource Manager framework.</span></span> <span data-ttu-id="02030-112">I cmdlet esistono nello spazio dei nomi **Microsoft.Azure.Commands.Media** .</span><span class="sxs-lookup"><span data-stu-id="02030-112">The cmdlets exist in the **Microsoft.Azure.Commands.Media** namespace.</span></span>

## <a name="versions"></a><span data-ttu-id="02030-113">Versioni</span><span class="sxs-lookup"><span data-stu-id="02030-113">Versions</span></span>
<span data-ttu-id="02030-114">**ApiVersion**:   "2015-10-01"</span><span class="sxs-lookup"><span data-stu-id="02030-114">**ApiVersion**:   "2015-10-01"</span></span>

## <a name="new-azurermmediaservice"></a><span data-ttu-id="02030-115">New-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="02030-115">New-AzureRmMediaService</span></span>
<span data-ttu-id="02030-116">Crea un servizio multimediale.</span><span class="sxs-lookup"><span data-stu-id="02030-116">Creates a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="02030-117">Sintassi</span><span class="sxs-lookup"><span data-stu-id="02030-117">Syntax</span></span>
<span data-ttu-id="02030-118">Set di parametri: StorageAccountIdParamSet</span><span class="sxs-lookup"><span data-stu-id="02030-118">Parameter Set: StorageAccountIdParamSet</span></span>

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccountId] <string> [-Tags <hashtable>]  [<CommonParameters>]

<span data-ttu-id="02030-119">Set di parametri: StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="02030-119">Parameter Set: StorageAccountsParamSet</span></span>

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccounts] <PSStorageAccount[]> [-Tags <hashtable>]  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="02030-120">Parametri</span><span class="sxs-lookup"><span data-stu-id="02030-120">Parameters</span></span>
<span data-ttu-id="02030-121">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="02030-121">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="02030-122">Specifica il nome del gruppo di risorse a cui appartiene questo servizio multimediale.</span><span class="sxs-lookup"><span data-stu-id="02030-122">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="02030-123">Alias</span><span class="sxs-lookup"><span data-stu-id="02030-123">Aliases</span></span> | <span data-ttu-id="02030-124">nessuno</span><span class="sxs-lookup"><span data-stu-id="02030-124">none</span></span> |
| --- | --- |
| <span data-ttu-id="02030-125">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="02030-125">Required?</span></span> |<span data-ttu-id="02030-126">true</span><span class="sxs-lookup"><span data-stu-id="02030-126">true</span></span> |
| <span data-ttu-id="02030-127">Posizione?</span><span class="sxs-lookup"><span data-stu-id="02030-127">Position?</span></span> |<span data-ttu-id="02030-128">0</span><span class="sxs-lookup"><span data-stu-id="02030-128">0</span></span> |
| <span data-ttu-id="02030-129">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="02030-129">Default value</span></span> |<span data-ttu-id="02030-130">nessuno</span><span class="sxs-lookup"><span data-stu-id="02030-130">none</span></span> |
| <span data-ttu-id="02030-131">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="02030-131">Accept pipeline input?</span></span> |<span data-ttu-id="02030-132">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="02030-132">true(ByPropertyName)</span></span> |
| <span data-ttu-id="02030-133">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="02030-133">Accept wildcard characters?</span></span> |<span data-ttu-id="02030-134">false</span><span class="sxs-lookup"><span data-stu-id="02030-134">false</span></span> |

<span data-ttu-id="02030-135">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="02030-135">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="02030-136">Specifica il nome del servizio multimediale.</span><span class="sxs-lookup"><span data-stu-id="02030-136">Specifies the name of the media service.</span></span>

| <span data-ttu-id="02030-137">Alias</span><span class="sxs-lookup"><span data-stu-id="02030-137">Aliases</span></span> | <span data-ttu-id="02030-138">Nome</span><span class="sxs-lookup"><span data-stu-id="02030-138">Name</span></span> |
| --- | --- |
| <span data-ttu-id="02030-139">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="02030-139">Required?</span></span> |<span data-ttu-id="02030-140">true</span><span class="sxs-lookup"><span data-stu-id="02030-140">true</span></span> |
| <span data-ttu-id="02030-141">Posizione?</span><span class="sxs-lookup"><span data-stu-id="02030-141">Position?</span></span> |<span data-ttu-id="02030-142">1</span><span class="sxs-lookup"><span data-stu-id="02030-142">1</span></span> |
| <span data-ttu-id="02030-143">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="02030-143">Default value</span></span> |<span data-ttu-id="02030-144">nessuno</span><span class="sxs-lookup"><span data-stu-id="02030-144">none</span></span> |
| <span data-ttu-id="02030-145">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="02030-145">Accept pipeline input?</span></span> |<span data-ttu-id="02030-146">false</span><span class="sxs-lookup"><span data-stu-id="02030-146">false</span></span> |
| <span data-ttu-id="02030-147">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="02030-147">Accept wildcard characters?</span></span> |<span data-ttu-id="02030-148">false</span><span class="sxs-lookup"><span data-stu-id="02030-148">false</span></span> |

<span data-ttu-id="02030-149">**-Location &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="02030-149">**-Location &lt;String&gt;**</span></span>

<span data-ttu-id="02030-150">Specifica la posizione della risorsa del servizio multimediale.</span><span class="sxs-lookup"><span data-stu-id="02030-150">Specifies the resource location of the media service.</span></span>

| <span data-ttu-id="02030-151">Alias</span><span class="sxs-lookup"><span data-stu-id="02030-151">Aliases</span></span> | <span data-ttu-id="02030-152">nessuno</span><span class="sxs-lookup"><span data-stu-id="02030-152">none</span></span> |
| --- | --- |
| <span data-ttu-id="02030-153">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="02030-153">Required?</span></span> |<span data-ttu-id="02030-154">true</span><span class="sxs-lookup"><span data-stu-id="02030-154">true</span></span> |
| <span data-ttu-id="02030-155">Posizione?</span><span class="sxs-lookup"><span data-stu-id="02030-155">Position?</span></span> |<span data-ttu-id="02030-156">2</span><span class="sxs-lookup"><span data-stu-id="02030-156">2</span></span> |
| <span data-ttu-id="02030-157">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="02030-157">Default value</span></span> |<span data-ttu-id="02030-158">nessuno</span><span class="sxs-lookup"><span data-stu-id="02030-158">none</span></span> |
| <span data-ttu-id="02030-159">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="02030-159">Accept pipeline input?</span></span> |<span data-ttu-id="02030-160">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="02030-160">true(ByPropertyName)</span></span> |
| <span data-ttu-id="02030-161">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="02030-161">Accept wildcard characters?</span></span> |<span data-ttu-id="02030-162">false</span><span class="sxs-lookup"><span data-stu-id="02030-162">false</span></span> |

<span data-ttu-id="02030-163">**-StorageAccountId &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="02030-163">**-StorageAccountId &lt;String&gt;**</span></span>

<span data-ttu-id="02030-164">Specifica un account di archiviazione primario associato al servizio multimediale.</span><span class="sxs-lookup"><span data-stu-id="02030-164">Specifies a primary storage account that associated with the media service.</span></span>

* <span data-ttu-id="02030-165">È supportato solo il nuovo account di archiviazione creato con l'API di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="02030-165">New storage account (created with the Resource Manager API) supported only.</span></span>
* <span data-ttu-id="02030-166">L'account di archiviazione deve esistere e ha la stessa posizione del servizio multimediale.</span><span class="sxs-lookup"><span data-stu-id="02030-166">The storage account must exist and has the same location with the media service.</span></span>

| <span data-ttu-id="02030-167">Alias</span><span class="sxs-lookup"><span data-stu-id="02030-167">Aliases</span></span> | <span data-ttu-id="02030-168">nessuno</span><span class="sxs-lookup"><span data-stu-id="02030-168">none</span></span> |
| --- | --- |
| <span data-ttu-id="02030-169">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="02030-169">Required?</span></span> |<span data-ttu-id="02030-170">true</span><span class="sxs-lookup"><span data-stu-id="02030-170">true</span></span> |
| <span data-ttu-id="02030-171">Posizione?</span><span class="sxs-lookup"><span data-stu-id="02030-171">Position?</span></span> |<span data-ttu-id="02030-172">3</span><span class="sxs-lookup"><span data-stu-id="02030-172">3</span></span> |
| <span data-ttu-id="02030-173">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="02030-173">Default value</span></span> |<span data-ttu-id="02030-174">nessuno</span><span class="sxs-lookup"><span data-stu-id="02030-174">none</span></span> |
| <span data-ttu-id="02030-175">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="02030-175">Accept pipeline input?</span></span> |<span data-ttu-id="02030-176">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="02030-176">true(ByPropertyName)</span></span> |
| <span data-ttu-id="02030-177">Nome del set di parametri</span><span class="sxs-lookup"><span data-stu-id="02030-177">Parameter set name</span></span> |<span data-ttu-id="02030-178">StorageAccountIdParamSet</span><span class="sxs-lookup"><span data-stu-id="02030-178">StorageAccountIdParamSet</span></span> |
| <span data-ttu-id="02030-179">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="02030-179">Accept wildcard characters?</span></span> |<span data-ttu-id="02030-180">false</span><span class="sxs-lookup"><span data-stu-id="02030-180">false</span></span> |

<span data-ttu-id="02030-181">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span><span class="sxs-lookup"><span data-stu-id="02030-181">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span></span>

<span data-ttu-id="02030-182">Specifica gli account di archiviazione associati al servizio multimediale.</span><span class="sxs-lookup"><span data-stu-id="02030-182">Specifies storage accounts that associated with the media service.</span></span>

* <span data-ttu-id="02030-183">È supportato solo il nuovo account di archiviazione creato con l'API di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="02030-183">New storage account (created with the Resource Manager API) supported only.</span></span>
* <span data-ttu-id="02030-184">L'account di archiviazione deve esistere e ha la stessa posizione del servizio multimediale.</span><span class="sxs-lookup"><span data-stu-id="02030-184">The storage account must exist and has the same location with the media service.</span></span>
* <span data-ttu-id="02030-185">È possibile specificare come primario un solo account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="02030-185">Only one storage account can be specified as primary.</span></span>

| <span data-ttu-id="02030-186">Alias</span><span class="sxs-lookup"><span data-stu-id="02030-186">Aliases</span></span> | <span data-ttu-id="02030-187">nessuno</span><span class="sxs-lookup"><span data-stu-id="02030-187">none</span></span> |
| --- | --- |
| <span data-ttu-id="02030-188">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="02030-188">Required?</span></span> |<span data-ttu-id="02030-189">true</span><span class="sxs-lookup"><span data-stu-id="02030-189">true</span></span> |
| <span data-ttu-id="02030-190">Posizione?</span><span class="sxs-lookup"><span data-stu-id="02030-190">Position?</span></span> |<span data-ttu-id="02030-191">3</span><span class="sxs-lookup"><span data-stu-id="02030-191">3</span></span> |
| <span data-ttu-id="02030-192">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="02030-192">Default value</span></span> |<span data-ttu-id="02030-193">nessuno</span><span class="sxs-lookup"><span data-stu-id="02030-193">none</span></span> |
| <span data-ttu-id="02030-194">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="02030-194">Accept pipeline input?</span></span> |<span data-ttu-id="02030-195">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="02030-195">true(ByPropertyName)</span></span> |
| <span data-ttu-id="02030-196">Nome del set di parametri</span><span class="sxs-lookup"><span data-stu-id="02030-196">Parameter set name</span></span> |<span data-ttu-id="02030-197">StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="02030-197">StorageAccountsParamSet</span></span> |
| <span data-ttu-id="02030-198">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="02030-198">Accept wildcard characters?</span></span> |<span data-ttu-id="02030-199">false</span><span class="sxs-lookup"><span data-stu-id="02030-199">false</span></span> |

<span data-ttu-id="02030-200">**-Tags &lt;Hashtable&gt;**</span><span class="sxs-lookup"><span data-stu-id="02030-200">**-Tags &lt;Hashtable&gt;**</span></span>

<span data-ttu-id="02030-201">Specifica una tabella hash dei tag associati al servizio multimediale.</span><span class="sxs-lookup"><span data-stu-id="02030-201">Specifies a hash table of the tags that are associated with the media service.</span></span>

* <span data-ttu-id="02030-202">Esempio: @{"tag1"="Valore1";" tag2 "=: value2"}</span><span class="sxs-lookup"><span data-stu-id="02030-202">Example: @{"tag1"="value1";"tag2"=:value2"}</span></span>

| <span data-ttu-id="02030-203">Alias</span><span class="sxs-lookup"><span data-stu-id="02030-203">Aliases</span></span> | <span data-ttu-id="02030-204">nessuno</span><span class="sxs-lookup"><span data-stu-id="02030-204">none</span></span> |
| --- | --- |
| <span data-ttu-id="02030-205">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="02030-205">Required?</span></span> |<span data-ttu-id="02030-206">false</span><span class="sxs-lookup"><span data-stu-id="02030-206">false</span></span> |
| <span data-ttu-id="02030-207">Posizione?</span><span class="sxs-lookup"><span data-stu-id="02030-207">Position?</span></span> |<span data-ttu-id="02030-208">denominata</span><span class="sxs-lookup"><span data-stu-id="02030-208">named</span></span> |
| <span data-ttu-id="02030-209">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="02030-209">Default value</span></span> |<span data-ttu-id="02030-210">nessuno</span><span class="sxs-lookup"><span data-stu-id="02030-210">none</span></span> |
| <span data-ttu-id="02030-211">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="02030-211">Accept pipeline input?</span></span> |<span data-ttu-id="02030-212">false</span><span class="sxs-lookup"><span data-stu-id="02030-212">false</span></span> |
| <span data-ttu-id="02030-213">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="02030-213">Accept wildcard characters?</span></span> |<span data-ttu-id="02030-214">false</span><span class="sxs-lookup"><span data-stu-id="02030-214">false</span></span> |

<span data-ttu-id="02030-215">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="02030-215">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="02030-216">Questo cmdlet supporta i parametri comuni seguenti: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction e -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="02030-216">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="02030-217">Input</span><span class="sxs-lookup"><span data-stu-id="02030-217">Inputs</span></span>
<span data-ttu-id="02030-218">Il tipo di input è il tipo degli oggetti che è possibile inviare tramite pipe al cmdlet.</span><span class="sxs-lookup"><span data-stu-id="02030-218">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="02030-219">Output</span><span class="sxs-lookup"><span data-stu-id="02030-219">Outputs</span></span>
<span data-ttu-id="02030-220">Il tipo di output è il tipo degli oggetti generati dal cmdlet.</span><span class="sxs-lookup"><span data-stu-id="02030-220">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="set-azurermmediaservice"></a><span data-ttu-id="02030-221">Set-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="02030-221">Set-AzureRmMediaService</span></span>
<span data-ttu-id="02030-222">Aggiorna un servizio multimediale.</span><span class="sxs-lookup"><span data-stu-id="02030-222">Updates a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="02030-223">Sintassi</span><span class="sxs-lookup"><span data-stu-id="02030-223">Syntax</span></span>
    Set-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Tags <hashtable>] [-StorageAccounts <PSStorageAccount[]>]  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="02030-224">Parametri</span><span class="sxs-lookup"><span data-stu-id="02030-224">Parameters</span></span>
<span data-ttu-id="02030-225">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="02030-225">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="02030-226">Specifica il nome del gruppo di risorse a cui appartiene questo servizio multimediale.</span><span class="sxs-lookup"><span data-stu-id="02030-226">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="02030-227">Alias</span><span class="sxs-lookup"><span data-stu-id="02030-227">Aliases</span></span> | <span data-ttu-id="02030-228">nessuno</span><span class="sxs-lookup"><span data-stu-id="02030-228">none</span></span> |
| --- | --- |
| <span data-ttu-id="02030-229">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="02030-229">Required?</span></span> |<span data-ttu-id="02030-230">true</span><span class="sxs-lookup"><span data-stu-id="02030-230">true</span></span> |
| <span data-ttu-id="02030-231">Posizione?</span><span class="sxs-lookup"><span data-stu-id="02030-231">Position?</span></span> |<span data-ttu-id="02030-232">0</span><span class="sxs-lookup"><span data-stu-id="02030-232">0</span></span> |
| <span data-ttu-id="02030-233">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="02030-233">Default Value</span></span> |<span data-ttu-id="02030-234">nessuno</span><span class="sxs-lookup"><span data-stu-id="02030-234">none</span></span> |
| <span data-ttu-id="02030-235">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="02030-235">Accept Pipeline Input?</span></span> |<span data-ttu-id="02030-236">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="02030-236">true(ByPropertyName)</span></span> |
| <span data-ttu-id="02030-237">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="02030-237">Accept wildcard characters?</span></span> |<span data-ttu-id="02030-238">false</span><span class="sxs-lookup"><span data-stu-id="02030-238">false</span></span> |

<span data-ttu-id="02030-239">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="02030-239">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="02030-240">Specifica il nome del servizio multimediale.</span><span class="sxs-lookup"><span data-stu-id="02030-240">Specifies the name of the media service.</span></span>

| <span data-ttu-id="02030-241">Alias</span><span class="sxs-lookup"><span data-stu-id="02030-241">Aliases</span></span> | <span data-ttu-id="02030-242">Nome</span><span class="sxs-lookup"><span data-stu-id="02030-242">Name</span></span> |
| --- | --- |
| <span data-ttu-id="02030-243">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="02030-243">Required?</span></span> |<span data-ttu-id="02030-244">true</span><span class="sxs-lookup"><span data-stu-id="02030-244">True</span></span> |
| <span data-ttu-id="02030-245">Posizione?</span><span class="sxs-lookup"><span data-stu-id="02030-245">Position?</span></span> |<span data-ttu-id="02030-246">1</span><span class="sxs-lookup"><span data-stu-id="02030-246">1</span></span> |
| <span data-ttu-id="02030-247">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="02030-247">Default value</span></span> |<span data-ttu-id="02030-248">nessuno</span><span class="sxs-lookup"><span data-stu-id="02030-248">None</span></span> |
| <span data-ttu-id="02030-249">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="02030-249">Accept pipeline input?</span></span> |<span data-ttu-id="02030-250">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="02030-250">true(ByPropertyName)</span></span> |
| <span data-ttu-id="02030-251">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="02030-251">Accept wildcard characters?</span></span> |<span data-ttu-id="02030-252">False</span><span class="sxs-lookup"><span data-stu-id="02030-252">False</span></span> |

<span data-ttu-id="02030-253">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span><span class="sxs-lookup"><span data-stu-id="02030-253">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span></span>

<span data-ttu-id="02030-254">Specifica gli account di archiviazione associati al servizio multimediale.</span><span class="sxs-lookup"><span data-stu-id="02030-254">Specifies storage accounts that associated with the media service.</span></span>

* <span data-ttu-id="02030-255">È supportato solo il nuovo account di archiviazione creato con l'API di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="02030-255">New storage account (created with the Resource Manager API) supported only.</span></span>
* <span data-ttu-id="02030-256">L'account di archiviazione deve esistere e ha la stessa posizione del servizio multimediale.</span><span class="sxs-lookup"><span data-stu-id="02030-256">The storage account must exist and has the same location with the media service.</span></span>
* <span data-ttu-id="02030-257">È possibile specificare come primario un solo account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="02030-257">Only one storage account can be specified as primary.</span></span>

| <span data-ttu-id="02030-258">Alias</span><span class="sxs-lookup"><span data-stu-id="02030-258">Aliases</span></span> | <span data-ttu-id="02030-259">nessuno</span><span class="sxs-lookup"><span data-stu-id="02030-259">none</span></span> |
| --- | --- |
| <span data-ttu-id="02030-260">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="02030-260">Required?</span></span> |<span data-ttu-id="02030-261">false</span><span class="sxs-lookup"><span data-stu-id="02030-261">false</span></span> |
| <span data-ttu-id="02030-262">Posizione?</span><span class="sxs-lookup"><span data-stu-id="02030-262">Position?</span></span> |<span data-ttu-id="02030-263">denominata</span><span class="sxs-lookup"><span data-stu-id="02030-263">Named</span></span> |
| <span data-ttu-id="02030-264">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="02030-264">Default value</span></span> |<span data-ttu-id="02030-265">nessuno</span><span class="sxs-lookup"><span data-stu-id="02030-265">none</span></span> |
| <span data-ttu-id="02030-266">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="02030-266">Accept pipeline input?</span></span> |<span data-ttu-id="02030-267">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="02030-267">true(ByPropertyName)</span></span> |
| <span data-ttu-id="02030-268">Nome del set di parametri</span><span class="sxs-lookup"><span data-stu-id="02030-268">Parameter set name</span></span> |<span data-ttu-id="02030-269">StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="02030-269">StorageAccountsParamSet</span></span> |
| <span data-ttu-id="02030-270">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="02030-270">Accept wildcard characters?</span></span> |<span data-ttu-id="02030-271">false</span><span class="sxs-lookup"><span data-stu-id="02030-271">false</span></span> |

<span data-ttu-id="02030-272">**-Tags &lt;Hashtable&gt;**</span><span class="sxs-lookup"><span data-stu-id="02030-272">**-Tags &lt;Hashtable&gt;**</span></span>

<span data-ttu-id="02030-273">Specifica una tabella hash dei tag associati a questo servizio multimediale.</span><span class="sxs-lookup"><span data-stu-id="02030-273">Specifies a hash table of the tags that are associated with this media service.</span></span>

* <span data-ttu-id="02030-274">I tag associati al servizio multimediale vengono sostituiti con il valore specificato dal cliente.</span><span class="sxs-lookup"><span data-stu-id="02030-274">The tags that are associated with the media service are replaced with value specified by the customer.</span></span>

| <span data-ttu-id="02030-275">Alias</span><span class="sxs-lookup"><span data-stu-id="02030-275">Aliases</span></span> | <span data-ttu-id="02030-276">nessuno</span><span class="sxs-lookup"><span data-stu-id="02030-276">none</span></span> |
| --- | --- |
| <span data-ttu-id="02030-277">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="02030-277">Required?</span></span> |<span data-ttu-id="02030-278">false</span><span class="sxs-lookup"><span data-stu-id="02030-278">False</span></span> |
| <span data-ttu-id="02030-279">Posizione?</span><span class="sxs-lookup"><span data-stu-id="02030-279">Position?</span></span> |<span data-ttu-id="02030-280">denominata</span><span class="sxs-lookup"><span data-stu-id="02030-280">Named</span></span> |
| <span data-ttu-id="02030-281">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="02030-281">Default value</span></span> |<span data-ttu-id="02030-282">nessuno</span><span class="sxs-lookup"><span data-stu-id="02030-282">None</span></span> |
| <span data-ttu-id="02030-283">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="02030-283">Accept pipeline input?</span></span> |<span data-ttu-id="02030-284">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="02030-284">true(ByPropertyName)</span></span> |
| <span data-ttu-id="02030-285">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="02030-285">Accept wildcard characters?</span></span> |<span data-ttu-id="02030-286">false</span><span class="sxs-lookup"><span data-stu-id="02030-286">false</span></span> |

<span data-ttu-id="02030-287">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="02030-287">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="02030-288">Questo cmdlet supporta i parametri comuni seguenti: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction e -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="02030-288">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="02030-289">Input</span><span class="sxs-lookup"><span data-stu-id="02030-289">Inputs</span></span>
<span data-ttu-id="02030-290">Il tipo di input è il tipo degli oggetti che è possibile inviare tramite pipe al cmdlet.</span><span class="sxs-lookup"><span data-stu-id="02030-290">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="02030-291">Output</span><span class="sxs-lookup"><span data-stu-id="02030-291">Outputs</span></span>
<span data-ttu-id="02030-292">Il tipo di output è il tipo degli oggetti generati dal cmdlet.</span><span class="sxs-lookup"><span data-stu-id="02030-292">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="remove-azurermmediaservice"></a><span data-ttu-id="02030-293">Remove-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="02030-293">Remove-AzureRmMediaService</span></span>
<span data-ttu-id="02030-294">Rimuove un servizio multimediale.</span><span class="sxs-lookup"><span data-stu-id="02030-294">Removes a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="02030-295">Sintassi</span><span class="sxs-lookup"><span data-stu-id="02030-295">Syntax</span></span>
    Remove-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="02030-296">Parametri</span><span class="sxs-lookup"><span data-stu-id="02030-296">Parameters</span></span>
<span data-ttu-id="02030-297">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="02030-297">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="02030-298">Specifica il nome del gruppo di risorse a cui appartiene questo servizio multimediale.</span><span class="sxs-lookup"><span data-stu-id="02030-298">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="02030-299">Alias</span><span class="sxs-lookup"><span data-stu-id="02030-299">Aliases</span></span> | <span data-ttu-id="02030-300">nessuno</span><span class="sxs-lookup"><span data-stu-id="02030-300">none</span></span> |
| --- | --- |
| <span data-ttu-id="02030-301">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="02030-301">Required?</span></span> |<span data-ttu-id="02030-302">true</span><span class="sxs-lookup"><span data-stu-id="02030-302">true</span></span> |
| <span data-ttu-id="02030-303">Posizione?</span><span class="sxs-lookup"><span data-stu-id="02030-303">Position?</span></span> |<span data-ttu-id="02030-304">0</span><span class="sxs-lookup"><span data-stu-id="02030-304">0</span></span> |
| <span data-ttu-id="02030-305">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="02030-305">Default value</span></span> |<span data-ttu-id="02030-306">nessuno</span><span class="sxs-lookup"><span data-stu-id="02030-306">none</span></span> |
| <span data-ttu-id="02030-307">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="02030-307">Accept pipeline input?</span></span> |<span data-ttu-id="02030-308">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="02030-308">true(ByPropertyName)</span></span> |
| <span data-ttu-id="02030-309">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="02030-309">Accept wildcard characters?</span></span> |<span data-ttu-id="02030-310">false</span><span class="sxs-lookup"><span data-stu-id="02030-310">false</span></span> |

<span data-ttu-id="02030-311">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="02030-311">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="02030-312">Specifica il nome del servizio multimediale.</span><span class="sxs-lookup"><span data-stu-id="02030-312">Specifies the name of the media service.</span></span>

| <span data-ttu-id="02030-313">Alias</span><span class="sxs-lookup"><span data-stu-id="02030-313">Aliases</span></span> | <span data-ttu-id="02030-314">nessuno</span><span class="sxs-lookup"><span data-stu-id="02030-314">none</span></span> |
| --- | --- |
| <span data-ttu-id="02030-315">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="02030-315">Required?</span></span> |<span data-ttu-id="02030-316">true</span><span class="sxs-lookup"><span data-stu-id="02030-316">true</span></span> |
| <span data-ttu-id="02030-317">Posizione?</span><span class="sxs-lookup"><span data-stu-id="02030-317">Position?</span></span> |<span data-ttu-id="02030-318">2</span><span class="sxs-lookup"><span data-stu-id="02030-318">2</span></span> |
| <span data-ttu-id="02030-319">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="02030-319">Default value</span></span> |<span data-ttu-id="02030-320">nessuno</span><span class="sxs-lookup"><span data-stu-id="02030-320">None</span></span> |
| <span data-ttu-id="02030-321">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="02030-321">Accept pipeline input?</span></span> |<span data-ttu-id="02030-322">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="02030-322">true(ByPropertyName)</span></span> |
| <span data-ttu-id="02030-323">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="02030-323">Accept wildcard characters?</span></span> |<span data-ttu-id="02030-324">False</span><span class="sxs-lookup"><span data-stu-id="02030-324">False</span></span> |

<span data-ttu-id="02030-325">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="02030-325">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="02030-326">Questo cmdlet supporta i parametri comuni seguenti: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction e -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="02030-326">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="02030-327">Input</span><span class="sxs-lookup"><span data-stu-id="02030-327">Inputs</span></span>
<span data-ttu-id="02030-328">Il tipo di input è il tipo degli oggetti che è possibile inviare tramite pipe al cmdlet.</span><span class="sxs-lookup"><span data-stu-id="02030-328">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="02030-329">Output</span><span class="sxs-lookup"><span data-stu-id="02030-329">Outputs</span></span>
<span data-ttu-id="02030-330">Il tipo di output è il tipo degli oggetti generati dal cmdlet.</span><span class="sxs-lookup"><span data-stu-id="02030-330">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="get-azurermmediaservice"></a><span data-ttu-id="02030-331">Get-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="02030-331">Get-AzureRmMediaService</span></span>
<span data-ttu-id="02030-332">Ottiene tutti i servizi multimediali in un gruppo di risorse o un servizio multimediale con un nome specificato.</span><span class="sxs-lookup"><span data-stu-id="02030-332">Gets all media services in a resource group or a media service with a given name.</span></span>

### <a name="syntax"></a><span data-ttu-id="02030-333">Sintassi</span><span class="sxs-lookup"><span data-stu-id="02030-333">Syntax</span></span>
<span data-ttu-id="02030-334">Set di parametri: ResourceGroupParameterSet</span><span class="sxs-lookup"><span data-stu-id="02030-334">ParameterSet: ResourceGroupParameterSet</span></span>

    Get-AzureRmMediaService [-ResourceGroupName] <string>  [<CommonParameters>]    

<span data-ttu-id="02030-335">Set di parametri: AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="02030-335">ParameterSet: AccountNameParameterSet</span></span>

    Get-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="02030-336">Parametri</span><span class="sxs-lookup"><span data-stu-id="02030-336">Parameters</span></span>
<span data-ttu-id="02030-337">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="02030-337">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="02030-338">Specifica il nome del gruppo di risorse a cui appartiene questo servizio multimediale.</span><span class="sxs-lookup"><span data-stu-id="02030-338">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="02030-339">Alias</span><span class="sxs-lookup"><span data-stu-id="02030-339">Aliases</span></span> | <span data-ttu-id="02030-340">nessuno</span><span class="sxs-lookup"><span data-stu-id="02030-340">none</span></span> |
| --- | --- |
| <span data-ttu-id="02030-341">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="02030-341">Required?</span></span> |<span data-ttu-id="02030-342">true</span><span class="sxs-lookup"><span data-stu-id="02030-342">true</span></span> |
| <span data-ttu-id="02030-343">Posizione?</span><span class="sxs-lookup"><span data-stu-id="02030-343">Position?</span></span> |<span data-ttu-id="02030-344">0</span><span class="sxs-lookup"><span data-stu-id="02030-344">0</span></span> |
| <span data-ttu-id="02030-345">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="02030-345">Default value</span></span> |<span data-ttu-id="02030-346">nessuno</span><span class="sxs-lookup"><span data-stu-id="02030-346">none</span></span> |
| <span data-ttu-id="02030-347">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="02030-347">Accept pipeline input?</span></span> |<span data-ttu-id="02030-348">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="02030-348">true(ByPropertyName)</span></span> |
| <span data-ttu-id="02030-349">Nome del set di parametri</span><span class="sxs-lookup"><span data-stu-id="02030-349">Parameter set name</span></span> |<span data-ttu-id="02030-350">ResourceGroupParameterSet, AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="02030-350">ResourceGroupParameterSet, AccountNameParameterSet</span></span> |

<span data-ttu-id="02030-351">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="02030-351">Accept wildcard characters?</span></span>   <span data-ttu-id="02030-352">false</span><span class="sxs-lookup"><span data-stu-id="02030-352">false</span></span>

<span data-ttu-id="02030-353">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="02030-353">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="02030-354">Specifica il nome del servizio multimediale.</span><span class="sxs-lookup"><span data-stu-id="02030-354">Specifies the name of the media service.</span></span>

| <span data-ttu-id="02030-355">Alias</span><span class="sxs-lookup"><span data-stu-id="02030-355">Aliases</span></span> | <span data-ttu-id="02030-356">nessuno</span><span class="sxs-lookup"><span data-stu-id="02030-356">none</span></span> |
| --- | --- |
| <span data-ttu-id="02030-357">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="02030-357">Required?</span></span> |<span data-ttu-id="02030-358">true</span><span class="sxs-lookup"><span data-stu-id="02030-358">true</span></span> |
| <span data-ttu-id="02030-359">Posizione?</span><span class="sxs-lookup"><span data-stu-id="02030-359">Position?</span></span> |<span data-ttu-id="02030-360">1</span><span class="sxs-lookup"><span data-stu-id="02030-360">1</span></span> |
| <span data-ttu-id="02030-361">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="02030-361">Default value</span></span> |<span data-ttu-id="02030-362">nessuno</span><span class="sxs-lookup"><span data-stu-id="02030-362">none</span></span> |
| <span data-ttu-id="02030-363">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="02030-363">Accept pipeline input?</span></span> |<span data-ttu-id="02030-364">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="02030-364">true(ByPropertyName)</span></span> |
| <span data-ttu-id="02030-365">Nome del set di parametri</span><span class="sxs-lookup"><span data-stu-id="02030-365">Parameter set name</span></span> |<span data-ttu-id="02030-366">AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="02030-366">AccountNameParameterSet</span></span> |
| <span data-ttu-id="02030-367">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="02030-367">Accept wildcard characters?</span></span> |<span data-ttu-id="02030-368">false</span><span class="sxs-lookup"><span data-stu-id="02030-368">false</span></span> |

<span data-ttu-id="02030-369">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="02030-369">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="02030-370">Questo cmdlet supporta i parametri comuni seguenti: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction e -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="02030-370">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="02030-371">Input</span><span class="sxs-lookup"><span data-stu-id="02030-371">Inputs</span></span>
<span data-ttu-id="02030-372">Il tipo di input è il tipo degli oggetti che è possibile inviare tramite pipe al cmdlet.</span><span class="sxs-lookup"><span data-stu-id="02030-372">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="02030-373">Output</span><span class="sxs-lookup"><span data-stu-id="02030-373">Outputs</span></span>
<span data-ttu-id="02030-374">Il tipo di output è il tipo degli oggetti generati dal cmdlet.</span><span class="sxs-lookup"><span data-stu-id="02030-374">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="get-azurermmediaservicekeys"></a><span data-ttu-id="02030-375">Get-AzureRmMediaServiceKeys</span><span class="sxs-lookup"><span data-stu-id="02030-375">Get-AzureRmMediaServiceKeys</span></span>
<span data-ttu-id="02030-376">Ottiene le chiavi di un servizio multimediale.</span><span class="sxs-lookup"><span data-stu-id="02030-376">Gets keys of a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="02030-377">Sintassi</span><span class="sxs-lookup"><span data-stu-id="02030-377">Syntax</span></span>
    Get-AzureRmMediaServiceKeys [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="02030-378">Parametri</span><span class="sxs-lookup"><span data-stu-id="02030-378">Parameters</span></span>
<span data-ttu-id="02030-379">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="02030-379">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="02030-380">Specifica il nome del gruppo di risorse a cui appartiene questo servizio multimediale.</span><span class="sxs-lookup"><span data-stu-id="02030-380">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="02030-381">Alias</span><span class="sxs-lookup"><span data-stu-id="02030-381">Aliases</span></span> | <span data-ttu-id="02030-382">nessuno</span><span class="sxs-lookup"><span data-stu-id="02030-382">none</span></span> |
| --- | --- |
| <span data-ttu-id="02030-383">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="02030-383">Required?</span></span> |<span data-ttu-id="02030-384">true</span><span class="sxs-lookup"><span data-stu-id="02030-384">true</span></span> |
| <span data-ttu-id="02030-385">Posizione?</span><span class="sxs-lookup"><span data-stu-id="02030-385">Position?</span></span> |<span data-ttu-id="02030-386">0</span><span class="sxs-lookup"><span data-stu-id="02030-386">0</span></span> |
| <span data-ttu-id="02030-387">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="02030-387">Default value</span></span> |<span data-ttu-id="02030-388">nessuno</span><span class="sxs-lookup"><span data-stu-id="02030-388">none</span></span> |
| <span data-ttu-id="02030-389">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="02030-389">Accept pipeline input?</span></span> |<span data-ttu-id="02030-390">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="02030-390">true(ByPropertyName)</span></span> |
| <span data-ttu-id="02030-391">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="02030-391">Accept wildcard characters?</span></span> |<span data-ttu-id="02030-392">false</span><span class="sxs-lookup"><span data-stu-id="02030-392">false</span></span> |

<span data-ttu-id="02030-393">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="02030-393">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="02030-394">Specifica il nome del servizio multimediale.</span><span class="sxs-lookup"><span data-stu-id="02030-394">Specifies the name of the media service.</span></span>

| <span data-ttu-id="02030-395">Alias</span><span class="sxs-lookup"><span data-stu-id="02030-395">Aliases</span></span> | <span data-ttu-id="02030-396">nessuno</span><span class="sxs-lookup"><span data-stu-id="02030-396">none</span></span> |
| --- | --- |
| <span data-ttu-id="02030-397">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="02030-397">Required?</span></span> |<span data-ttu-id="02030-398">true</span><span class="sxs-lookup"><span data-stu-id="02030-398">true</span></span> |
| <span data-ttu-id="02030-399">Posizione?</span><span class="sxs-lookup"><span data-stu-id="02030-399">Position?</span></span> |<span data-ttu-id="02030-400">1</span><span class="sxs-lookup"><span data-stu-id="02030-400">1</span></span> |
| <span data-ttu-id="02030-401">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="02030-401">Default value</span></span> |<span data-ttu-id="02030-402">nessuno</span><span class="sxs-lookup"><span data-stu-id="02030-402">none</span></span> |
| <span data-ttu-id="02030-403">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="02030-403">Accept pipeline input?</span></span> |<span data-ttu-id="02030-404">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="02030-404">true(ByPropertyName)</span></span> |
| <span data-ttu-id="02030-405">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="02030-405">Accept wildcard characters?</span></span> |<span data-ttu-id="02030-406">false</span><span class="sxs-lookup"><span data-stu-id="02030-406">false</span></span> |

<span data-ttu-id="02030-407">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="02030-407">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="02030-408">Questo cmdlet supporta i parametri comuni seguenti: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction e -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="02030-408">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="02030-409">Input</span><span class="sxs-lookup"><span data-stu-id="02030-409">Inputs</span></span>
<span data-ttu-id="02030-410">Il tipo di input è il tipo degli oggetti che è possibile inviare tramite pipe al cmdlet.</span><span class="sxs-lookup"><span data-stu-id="02030-410">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="02030-411">Output</span><span class="sxs-lookup"><span data-stu-id="02030-411">Outputs</span></span>
<span data-ttu-id="02030-412">Il tipo di output è il tipo degli oggetti generati dal cmdlet.</span><span class="sxs-lookup"><span data-stu-id="02030-412">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="set-azurermmediaservicekey"></a><span data-ttu-id="02030-413">Set-AzureRmMediaServiceKey</span><span class="sxs-lookup"><span data-stu-id="02030-413">Set-AzureRmMediaServiceKey</span></span>
<span data-ttu-id="02030-414">Rigenera una chiave primaria o secondaria di un servizio multimediale.</span><span class="sxs-lookup"><span data-stu-id="02030-414">Regenerates a primary or secondary key of a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="02030-415">Sintassi</span><span class="sxs-lookup"><span data-stu-id="02030-415">Syntax</span></span>
    Set-AzureRmMediaServiceKey [-ResourceGroupName] <string> [-AccountName] <string> [-KeyType] <KeyType> {Primary | Secondary}  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="02030-416">Parametri</span><span class="sxs-lookup"><span data-stu-id="02030-416">Parameters</span></span>
<span data-ttu-id="02030-417">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="02030-417">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="02030-418">Specifica il nome del gruppo di risorse a cui appartiene questo servizio multimediale.</span><span class="sxs-lookup"><span data-stu-id="02030-418">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="02030-419">Alias</span><span class="sxs-lookup"><span data-stu-id="02030-419">Aliases</span></span> | <span data-ttu-id="02030-420">nessuno</span><span class="sxs-lookup"><span data-stu-id="02030-420">none</span></span> |
| --- | --- |
| <span data-ttu-id="02030-421">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="02030-421">Required?</span></span> |<span data-ttu-id="02030-422">true</span><span class="sxs-lookup"><span data-stu-id="02030-422">true</span></span> |
| <span data-ttu-id="02030-423">Posizione?</span><span class="sxs-lookup"><span data-stu-id="02030-423">Position?</span></span> |<span data-ttu-id="02030-424">0</span><span class="sxs-lookup"><span data-stu-id="02030-424">0</span></span> |
| <span data-ttu-id="02030-425">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="02030-425">Default value</span></span> |<span data-ttu-id="02030-426">nessuno</span><span class="sxs-lookup"><span data-stu-id="02030-426">none</span></span> |
| <span data-ttu-id="02030-427">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="02030-427">Accept pipeline input?</span></span> |<span data-ttu-id="02030-428">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="02030-428">true(ByPropertyName)</span></span> |
| <span data-ttu-id="02030-429">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="02030-429">Accept wildcard characters?</span></span> |<span data-ttu-id="02030-430">false</span><span class="sxs-lookup"><span data-stu-id="02030-430">false</span></span> |

<span data-ttu-id="02030-431">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="02030-431">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="02030-432">Specifica il nome del servizio multimediale.</span><span class="sxs-lookup"><span data-stu-id="02030-432">Specifies the name of the media service.</span></span>

| <span data-ttu-id="02030-433">Alias</span><span class="sxs-lookup"><span data-stu-id="02030-433">Aliases</span></span> | <span data-ttu-id="02030-434">nessuno</span><span class="sxs-lookup"><span data-stu-id="02030-434">none</span></span> |
| --- | --- |
| <span data-ttu-id="02030-435">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="02030-435">Required?</span></span> |<span data-ttu-id="02030-436">true</span><span class="sxs-lookup"><span data-stu-id="02030-436">true</span></span> |
| <span data-ttu-id="02030-437">Posizione?</span><span class="sxs-lookup"><span data-stu-id="02030-437">Position?</span></span> |<span data-ttu-id="02030-438">1</span><span class="sxs-lookup"><span data-stu-id="02030-438">1</span></span> |
| <span data-ttu-id="02030-439">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="02030-439">Default value</span></span> |<span data-ttu-id="02030-440">nessuno</span><span class="sxs-lookup"><span data-stu-id="02030-440">none</span></span> |
| <span data-ttu-id="02030-441">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="02030-441">Accept pipeline input?</span></span> |<span data-ttu-id="02030-442">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="02030-442">true(ByPropertyName)</span></span> |
| <span data-ttu-id="02030-443">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="02030-443">Accept wildcard characters?</span></span> |<span data-ttu-id="02030-444">false</span><span class="sxs-lookup"><span data-stu-id="02030-444">false</span></span> |

<span data-ttu-id="02030-445">**-KeyType &lt;KeyType&gt;**</span><span class="sxs-lookup"><span data-stu-id="02030-445">**-KeyType &lt;KeyType&gt;**</span></span>

<span data-ttu-id="02030-446">Specifica il tipo di chiave del servizio multimediale.</span><span class="sxs-lookup"><span data-stu-id="02030-446">Specifies the key type of the media service.</span></span>

* <span data-ttu-id="02030-447">Primaria o secondaria</span><span class="sxs-lookup"><span data-stu-id="02030-447">Primary or Secondary</span></span>

| <span data-ttu-id="02030-448">Alias</span><span class="sxs-lookup"><span data-stu-id="02030-448">Aliases</span></span> | <span data-ttu-id="02030-449">nessuno</span><span class="sxs-lookup"><span data-stu-id="02030-449">none</span></span> |
| --- | --- |
| <span data-ttu-id="02030-450">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="02030-450">Required?</span></span> |<span data-ttu-id="02030-451">true</span><span class="sxs-lookup"><span data-stu-id="02030-451">true</span></span> |
| <span data-ttu-id="02030-452">Posizione?</span><span class="sxs-lookup"><span data-stu-id="02030-452">Position?</span></span> |<span data-ttu-id="02030-453">2</span><span class="sxs-lookup"><span data-stu-id="02030-453">2</span></span> |
| <span data-ttu-id="02030-454">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="02030-454">Default value</span></span> |<span data-ttu-id="02030-455">nessuno</span><span class="sxs-lookup"><span data-stu-id="02030-455">none</span></span> |
| <span data-ttu-id="02030-456">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="02030-456">Accept pipeline input?</span></span> |<span data-ttu-id="02030-457">false</span><span class="sxs-lookup"><span data-stu-id="02030-457">false</span></span> |
| <span data-ttu-id="02030-458">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="02030-458">Accept wildcard characters?</span></span> |<span data-ttu-id="02030-459">false</span><span class="sxs-lookup"><span data-stu-id="02030-459">false</span></span> |

<span data-ttu-id="02030-460">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="02030-460">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="02030-461">Questo cmdlet supporta i parametri comuni seguenti: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction e -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="02030-461">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="02030-462">Input</span><span class="sxs-lookup"><span data-stu-id="02030-462">Inputs</span></span>
<span data-ttu-id="02030-463">Il tipo di input è il tipo degli oggetti che è possibile inviare tramite pipe al cmdlet.</span><span class="sxs-lookup"><span data-stu-id="02030-463">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="02030-464">Output</span><span class="sxs-lookup"><span data-stu-id="02030-464">Outputs</span></span>
<span data-ttu-id="02030-465">Il tipo di output è il tipo degli oggetti generati dal cmdlet.</span><span class="sxs-lookup"><span data-stu-id="02030-465">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="sync-azurermmediaservicestoragekeys"></a><span data-ttu-id="02030-466">Sync-AzureRmMediaServiceStorageKeys</span><span class="sxs-lookup"><span data-stu-id="02030-466">Sync-AzureRmMediaServiceStorageKeys</span></span>
<span data-ttu-id="02030-467">Sincronizza le chiavi dell'account di archiviazione per un account di archiviazione associato al servizio multimediale.</span><span class="sxs-lookup"><span data-stu-id="02030-467">Synchronizes storage account keys for a storage account associated with the media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="02030-468">Sintassi</span><span class="sxs-lookup"><span data-stu-id="02030-468">Syntax</span></span>
    Sync-AzureRmMediaServiceStorageKeys [-ResourceGroupName] <string> [-MediaServiceAccountName] <string>    [-StorageAccountId] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="02030-469">Parametri</span><span class="sxs-lookup"><span data-stu-id="02030-469">Parameters</span></span>
<span data-ttu-id="02030-470">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="02030-470">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="02030-471">Specifica il nome del gruppo di risorse a cui appartiene questo servizio multimediale.</span><span class="sxs-lookup"><span data-stu-id="02030-471">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="02030-472">Alias</span><span class="sxs-lookup"><span data-stu-id="02030-472">Aliases</span></span> | <span data-ttu-id="02030-473">nessuno</span><span class="sxs-lookup"><span data-stu-id="02030-473">none</span></span> |
| --- | --- |
| <span data-ttu-id="02030-474">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="02030-474">Required?</span></span> |<span data-ttu-id="02030-475">true</span><span class="sxs-lookup"><span data-stu-id="02030-475">true</span></span> |
| <span data-ttu-id="02030-476">Posizione?</span><span class="sxs-lookup"><span data-stu-id="02030-476">Position?</span></span> |<span data-ttu-id="02030-477">0</span><span class="sxs-lookup"><span data-stu-id="02030-477">0</span></span> |
| <span data-ttu-id="02030-478">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="02030-478">Default value</span></span> |<span data-ttu-id="02030-479">nessuno</span><span class="sxs-lookup"><span data-stu-id="02030-479">none</span></span> |
| <span data-ttu-id="02030-480">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="02030-480">Accept pipeline input?</span></span> |<span data-ttu-id="02030-481">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="02030-481">true(ByPropertyName)</span></span> |
| <span data-ttu-id="02030-482">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="02030-482">Accept wildcard characters?</span></span> |<span data-ttu-id="02030-483">false</span><span class="sxs-lookup"><span data-stu-id="02030-483">false</span></span> |

<span data-ttu-id="02030-484">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="02030-484">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="02030-485">Specifica il nome del servizio multimediale.</span><span class="sxs-lookup"><span data-stu-id="02030-485">Specifies the name of the media service.</span></span>

| <span data-ttu-id="02030-486">Alias</span><span class="sxs-lookup"><span data-stu-id="02030-486">Aliases</span></span> | <span data-ttu-id="02030-487">nessuno</span><span class="sxs-lookup"><span data-stu-id="02030-487">none</span></span> |
| --- | --- |
| <span data-ttu-id="02030-488">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="02030-488">Required?</span></span> |<span data-ttu-id="02030-489">true</span><span class="sxs-lookup"><span data-stu-id="02030-489">true</span></span> |
| <span data-ttu-id="02030-490">Posizione?</span><span class="sxs-lookup"><span data-stu-id="02030-490">Position?</span></span> |<span data-ttu-id="02030-491">1</span><span class="sxs-lookup"><span data-stu-id="02030-491">1</span></span> |
| <span data-ttu-id="02030-492">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="02030-492">Default value</span></span> |<span data-ttu-id="02030-493">nessuno</span><span class="sxs-lookup"><span data-stu-id="02030-493">none</span></span> |
| <span data-ttu-id="02030-494">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="02030-494">Accept pipeline input?</span></span> |<span data-ttu-id="02030-495">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="02030-495">true(ByPropertyName)</span></span> |
| <span data-ttu-id="02030-496">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="02030-496">Accept wildcard characters?</span></span> |<span data-ttu-id="02030-497">false</span><span class="sxs-lookup"><span data-stu-id="02030-497">false</span></span> |

<span data-ttu-id="02030-498">**-StorageAccountId &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="02030-498">**-StorageAccountId &lt;String&gt;**</span></span>

<span data-ttu-id="02030-499">Specifica l'account di archiviazione associato al servizio multimediale.</span><span class="sxs-lookup"><span data-stu-id="02030-499">Specifies the storage account associated with the media service.</span></span>

| <span data-ttu-id="02030-500">Alias</span><span class="sxs-lookup"><span data-stu-id="02030-500">Aliases</span></span> | <span data-ttu-id="02030-501">ID</span><span class="sxs-lookup"><span data-stu-id="02030-501">Id</span></span> |
| --- | --- |
| <span data-ttu-id="02030-502">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="02030-502">Required?</span></span> |<span data-ttu-id="02030-503">true</span><span class="sxs-lookup"><span data-stu-id="02030-503">true</span></span> |
| <span data-ttu-id="02030-504">Posizione?</span><span class="sxs-lookup"><span data-stu-id="02030-504">Position?</span></span> |<span data-ttu-id="02030-505">2</span><span class="sxs-lookup"><span data-stu-id="02030-505">2</span></span> |
| <span data-ttu-id="02030-506">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="02030-506">Default value</span></span> |<span data-ttu-id="02030-507">nessuno</span><span class="sxs-lookup"><span data-stu-id="02030-507">none</span></span> |
| <span data-ttu-id="02030-508">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="02030-508">Accept pipeline input?</span></span> |<span data-ttu-id="02030-509">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="02030-509">true(ByPropertyName)</span></span> |
| <span data-ttu-id="02030-510">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="02030-510">Accept wildcard characters?</span></span> |<span data-ttu-id="02030-511">false</span><span class="sxs-lookup"><span data-stu-id="02030-511">false</span></span> |

<span data-ttu-id="02030-512">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="02030-512">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="02030-513">Questo cmdlet supporta i parametri comuni seguenti: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction e -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="02030-513">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="02030-514">Input</span><span class="sxs-lookup"><span data-stu-id="02030-514">Inputs</span></span>
<span data-ttu-id="02030-515">Il tipo di input è il tipo degli oggetti che è possibile inviare tramite pipe al cmdlet.</span><span class="sxs-lookup"><span data-stu-id="02030-515">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="02030-516">Output</span><span class="sxs-lookup"><span data-stu-id="02030-516">Outputs</span></span>
<span data-ttu-id="02030-517">Il tipo di output è il tipo degli oggetti generati dal cmdlet.</span><span class="sxs-lookup"><span data-stu-id="02030-517">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="next-step"></a><span data-ttu-id="02030-518">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="02030-518">Next step</span></span>
<span data-ttu-id="02030-519">Vedere i percorsi di apprendimento di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="02030-519">Check out Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="02030-520">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="02030-520">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

