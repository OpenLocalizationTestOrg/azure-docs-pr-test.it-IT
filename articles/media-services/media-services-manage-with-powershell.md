---
title: aaaManage account servizi multimediali di Azure con PowerShell
description: Informazioni su come account di toomanage servizi multimediali di Azure con i cmdlet di PowerShell.
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
ms.openlocfilehash: e8f97bb2393343e45fabf9c437b4fc09f2525dc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-media-services-accounts-with-powershell"></a><span data-ttu-id="b0d81-103">Gestire gli account di Servizi multimediali di Azure con PowerShell</span><span class="sxs-lookup"><span data-stu-id="b0d81-103">Manage Azure Media Services Accounts with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b0d81-104">Portale</span><span class="sxs-lookup"><span data-stu-id="b0d81-104">Portal</span></span>](media-services-portal-create-account.md)
> * [<span data-ttu-id="b0d81-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b0d81-105">PowerShell</span></span>](media-services-manage-with-powershell.md)
> * [<span data-ttu-id="b0d81-106">REST</span><span class="sxs-lookup"><span data-stu-id="b0d81-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/mediaservice)
> 
> [!NOTE]
> <span data-ttu-id="b0d81-107">toobe toocreate in grado di un account di servizi multimediali di Azure, è necessario disporre di un account di Azure.</span><span class="sxs-lookup"><span data-stu-id="b0d81-107">toobe able toocreate an Azure Media Services account, you must have an Azure account.</span></span> <span data-ttu-id="b0d81-108">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="b0d81-108">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="b0d81-109">Per informazioni dettagliate, vedere la pagina relativa alla <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A8A8397B5" target="_blank">versione di valutazione gratuita di Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="b0d81-109">For details, see <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A8A8397B5" target="_blank">Azure Free Trial</a>.</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="b0d81-110">Panoramica</span><span class="sxs-lookup"><span data-stu-id="b0d81-110">Overview</span></span>
<span data-ttu-id="b0d81-111">Questo articolo vengono elencati i cmdlet di hello Azure PowerShell per Azure Media Services (AMS) nel framework di gestione risorse di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="b0d81-111">This article lists hello Azure PowerShell cmdlets for Azure Media Services (AMS) in hello Azure Resource Manager framework.</span></span> <span data-ttu-id="b0d81-112">i cmdlet di Hello esistono in hello **Microsoft.Azure.Commands.Media** dello spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="b0d81-112">hello cmdlets exist in hello **Microsoft.Azure.Commands.Media** namespace.</span></span>

## <a name="versions"></a><span data-ttu-id="b0d81-113">Versioni</span><span class="sxs-lookup"><span data-stu-id="b0d81-113">Versions</span></span>
<span data-ttu-id="b0d81-114">**ApiVersion**:   "2015-10-01"</span><span class="sxs-lookup"><span data-stu-id="b0d81-114">**ApiVersion**:   "2015-10-01"</span></span>

## <a name="new-azurermmediaservice"></a><span data-ttu-id="b0d81-115">New-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="b0d81-115">New-AzureRmMediaService</span></span>
<span data-ttu-id="b0d81-116">Crea un servizio multimediale.</span><span class="sxs-lookup"><span data-stu-id="b0d81-116">Creates a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="b0d81-117">Sintassi</span><span class="sxs-lookup"><span data-stu-id="b0d81-117">Syntax</span></span>
<span data-ttu-id="b0d81-118">Set di parametri: StorageAccountIdParamSet</span><span class="sxs-lookup"><span data-stu-id="b0d81-118">Parameter Set: StorageAccountIdParamSet</span></span>

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccountId] <string> [-Tags <hashtable>]  [<CommonParameters>]

<span data-ttu-id="b0d81-119">Set di parametri: StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="b0d81-119">Parameter Set: StorageAccountsParamSet</span></span>

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccounts] <PSStorageAccount[]> [-Tags <hashtable>]  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="b0d81-120">Parametri</span><span class="sxs-lookup"><span data-stu-id="b0d81-120">Parameters</span></span>
<span data-ttu-id="b0d81-121">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="b0d81-121">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="b0d81-122">Specifica il nome di hello di hello toowhich di gruppo di risorse che appartiene questo servizio di supporto.</span><span class="sxs-lookup"><span data-stu-id="b0d81-122">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="b0d81-123">Alias</span><span class="sxs-lookup"><span data-stu-id="b0d81-123">Aliases</span></span> | <span data-ttu-id="b0d81-124">nessuno</span><span class="sxs-lookup"><span data-stu-id="b0d81-124">none</span></span> |
| --- | --- |
| <span data-ttu-id="b0d81-125">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="b0d81-125">Required?</span></span> |<span data-ttu-id="b0d81-126">true</span><span class="sxs-lookup"><span data-stu-id="b0d81-126">true</span></span> |
| <span data-ttu-id="b0d81-127">Posizione?</span><span class="sxs-lookup"><span data-stu-id="b0d81-127">Position?</span></span> |<span data-ttu-id="b0d81-128">0</span><span class="sxs-lookup"><span data-stu-id="b0d81-128">0</span></span> |
| <span data-ttu-id="b0d81-129">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="b0d81-129">Default value</span></span> |<span data-ttu-id="b0d81-130">nessuno</span><span class="sxs-lookup"><span data-stu-id="b0d81-130">none</span></span> |
| <span data-ttu-id="b0d81-131">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="b0d81-131">Accept pipeline input?</span></span> |<span data-ttu-id="b0d81-132">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="b0d81-132">true(ByPropertyName)</span></span> |
| <span data-ttu-id="b0d81-133">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="b0d81-133">Accept wildcard characters?</span></span> |<span data-ttu-id="b0d81-134">false</span><span class="sxs-lookup"><span data-stu-id="b0d81-134">false</span></span> |

<span data-ttu-id="b0d81-135">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="b0d81-135">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="b0d81-136">Specifica il nome di hello del servizio multimediale hello.</span><span class="sxs-lookup"><span data-stu-id="b0d81-136">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="b0d81-137">Alias</span><span class="sxs-lookup"><span data-stu-id="b0d81-137">Aliases</span></span> | <span data-ttu-id="b0d81-138">Nome</span><span class="sxs-lookup"><span data-stu-id="b0d81-138">Name</span></span> |
| --- | --- |
| <span data-ttu-id="b0d81-139">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="b0d81-139">Required?</span></span> |<span data-ttu-id="b0d81-140">true</span><span class="sxs-lookup"><span data-stu-id="b0d81-140">true</span></span> |
| <span data-ttu-id="b0d81-141">Posizione?</span><span class="sxs-lookup"><span data-stu-id="b0d81-141">Position?</span></span> |<span data-ttu-id="b0d81-142">1</span><span class="sxs-lookup"><span data-stu-id="b0d81-142">1</span></span> |
| <span data-ttu-id="b0d81-143">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="b0d81-143">Default value</span></span> |<span data-ttu-id="b0d81-144">nessuno</span><span class="sxs-lookup"><span data-stu-id="b0d81-144">none</span></span> |
| <span data-ttu-id="b0d81-145">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="b0d81-145">Accept pipeline input?</span></span> |<span data-ttu-id="b0d81-146">false</span><span class="sxs-lookup"><span data-stu-id="b0d81-146">false</span></span> |
| <span data-ttu-id="b0d81-147">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="b0d81-147">Accept wildcard characters?</span></span> |<span data-ttu-id="b0d81-148">false</span><span class="sxs-lookup"><span data-stu-id="b0d81-148">false</span></span> |

<span data-ttu-id="b0d81-149">**-Location &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="b0d81-149">**-Location &lt;String&gt;**</span></span>

<span data-ttu-id="b0d81-150">Specifica percorso della risorsa del servizio di supporto hello hello.</span><span class="sxs-lookup"><span data-stu-id="b0d81-150">Specifies hello resource location of hello media service.</span></span>

| <span data-ttu-id="b0d81-151">Alias</span><span class="sxs-lookup"><span data-stu-id="b0d81-151">Aliases</span></span> | <span data-ttu-id="b0d81-152">nessuno</span><span class="sxs-lookup"><span data-stu-id="b0d81-152">none</span></span> |
| --- | --- |
| <span data-ttu-id="b0d81-153">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="b0d81-153">Required?</span></span> |<span data-ttu-id="b0d81-154">true</span><span class="sxs-lookup"><span data-stu-id="b0d81-154">true</span></span> |
| <span data-ttu-id="b0d81-155">Posizione?</span><span class="sxs-lookup"><span data-stu-id="b0d81-155">Position?</span></span> |<span data-ttu-id="b0d81-156">2</span><span class="sxs-lookup"><span data-stu-id="b0d81-156">2</span></span> |
| <span data-ttu-id="b0d81-157">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="b0d81-157">Default value</span></span> |<span data-ttu-id="b0d81-158">nessuno</span><span class="sxs-lookup"><span data-stu-id="b0d81-158">none</span></span> |
| <span data-ttu-id="b0d81-159">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="b0d81-159">Accept pipeline input?</span></span> |<span data-ttu-id="b0d81-160">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="b0d81-160">true(ByPropertyName)</span></span> |
| <span data-ttu-id="b0d81-161">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="b0d81-161">Accept wildcard characters?</span></span> |<span data-ttu-id="b0d81-162">false</span><span class="sxs-lookup"><span data-stu-id="b0d81-162">false</span></span> |

<span data-ttu-id="b0d81-163">**-StorageAccountId &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="b0d81-163">**-StorageAccountId &lt;String&gt;**</span></span>

<span data-ttu-id="b0d81-164">Specifica un account di archiviazione primario associato al servizio multimediale hello.</span><span class="sxs-lookup"><span data-stu-id="b0d81-164">Specifies a primary storage account that associated with hello media service.</span></span>

* <span data-ttu-id="b0d81-165">Nuovo account di archiviazione (creata con l'API di gestione risorse di hello) è supportato solo.</span><span class="sxs-lookup"><span data-stu-id="b0d81-165">New storage account (created with hello Resource Manager API) supported only.</span></span>
* <span data-ttu-id="b0d81-166">deve esistere Hello account di archiviazione e ha hello stessa località del servizio di supporto hello.</span><span class="sxs-lookup"><span data-stu-id="b0d81-166">hello storage account must exist and has hello same location with hello media service.</span></span>

| <span data-ttu-id="b0d81-167">Alias</span><span class="sxs-lookup"><span data-stu-id="b0d81-167">Aliases</span></span> | <span data-ttu-id="b0d81-168">nessuno</span><span class="sxs-lookup"><span data-stu-id="b0d81-168">none</span></span> |
| --- | --- |
| <span data-ttu-id="b0d81-169">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="b0d81-169">Required?</span></span> |<span data-ttu-id="b0d81-170">true</span><span class="sxs-lookup"><span data-stu-id="b0d81-170">true</span></span> |
| <span data-ttu-id="b0d81-171">Posizione?</span><span class="sxs-lookup"><span data-stu-id="b0d81-171">Position?</span></span> |<span data-ttu-id="b0d81-172">3</span><span class="sxs-lookup"><span data-stu-id="b0d81-172">3</span></span> |
| <span data-ttu-id="b0d81-173">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="b0d81-173">Default value</span></span> |<span data-ttu-id="b0d81-174">nessuno</span><span class="sxs-lookup"><span data-stu-id="b0d81-174">none</span></span> |
| <span data-ttu-id="b0d81-175">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="b0d81-175">Accept pipeline input?</span></span> |<span data-ttu-id="b0d81-176">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="b0d81-176">true(ByPropertyName)</span></span> |
| <span data-ttu-id="b0d81-177">Nome del set di parametri</span><span class="sxs-lookup"><span data-stu-id="b0d81-177">Parameter set name</span></span> |<span data-ttu-id="b0d81-178">StorageAccountIdParamSet</span><span class="sxs-lookup"><span data-stu-id="b0d81-178">StorageAccountIdParamSet</span></span> |
| <span data-ttu-id="b0d81-179">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="b0d81-179">Accept wildcard characters?</span></span> |<span data-ttu-id="b0d81-180">false</span><span class="sxs-lookup"><span data-stu-id="b0d81-180">false</span></span> |

<span data-ttu-id="b0d81-181">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span><span class="sxs-lookup"><span data-stu-id="b0d81-181">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span></span>

<span data-ttu-id="b0d81-182">Specifica l'account di archiviazione associato al servizio multimediale hello.</span><span class="sxs-lookup"><span data-stu-id="b0d81-182">Specifies storage accounts that associated with hello media service.</span></span>

* <span data-ttu-id="b0d81-183">Nuovo account di archiviazione (creata con l'API di gestione risorse di hello) è supportato solo.</span><span class="sxs-lookup"><span data-stu-id="b0d81-183">New storage account (created with hello Resource Manager API) supported only.</span></span>
* <span data-ttu-id="b0d81-184">deve esistere Hello account di archiviazione e ha hello stessa località del servizio di supporto hello.</span><span class="sxs-lookup"><span data-stu-id="b0d81-184">hello storage account must exist and has hello same location with hello media service.</span></span>
* <span data-ttu-id="b0d81-185">È possibile specificare come primario un solo account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="b0d81-185">Only one storage account can be specified as primary.</span></span>

| <span data-ttu-id="b0d81-186">Alias</span><span class="sxs-lookup"><span data-stu-id="b0d81-186">Aliases</span></span> | <span data-ttu-id="b0d81-187">nessuno</span><span class="sxs-lookup"><span data-stu-id="b0d81-187">none</span></span> |
| --- | --- |
| <span data-ttu-id="b0d81-188">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="b0d81-188">Required?</span></span> |<span data-ttu-id="b0d81-189">true</span><span class="sxs-lookup"><span data-stu-id="b0d81-189">true</span></span> |
| <span data-ttu-id="b0d81-190">Posizione?</span><span class="sxs-lookup"><span data-stu-id="b0d81-190">Position?</span></span> |<span data-ttu-id="b0d81-191">3</span><span class="sxs-lookup"><span data-stu-id="b0d81-191">3</span></span> |
| <span data-ttu-id="b0d81-192">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="b0d81-192">Default value</span></span> |<span data-ttu-id="b0d81-193">nessuno</span><span class="sxs-lookup"><span data-stu-id="b0d81-193">none</span></span> |
| <span data-ttu-id="b0d81-194">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="b0d81-194">Accept pipeline input?</span></span> |<span data-ttu-id="b0d81-195">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="b0d81-195">true(ByPropertyName)</span></span> |
| <span data-ttu-id="b0d81-196">Nome del set di parametri</span><span class="sxs-lookup"><span data-stu-id="b0d81-196">Parameter set name</span></span> |<span data-ttu-id="b0d81-197">StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="b0d81-197">StorageAccountsParamSet</span></span> |
| <span data-ttu-id="b0d81-198">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="b0d81-198">Accept wildcard characters?</span></span> |<span data-ttu-id="b0d81-199">false</span><span class="sxs-lookup"><span data-stu-id="b0d81-199">false</span></span> |

<span data-ttu-id="b0d81-200">**-Tags &lt;Hashtable&gt;**</span><span class="sxs-lookup"><span data-stu-id="b0d81-200">**-Tags &lt;Hashtable&gt;**</span></span>

<span data-ttu-id="b0d81-201">Specifica una tabella hash di tag hello associati al servizio multimediale hello.</span><span class="sxs-lookup"><span data-stu-id="b0d81-201">Specifies a hash table of hello tags that are associated with hello media service.</span></span>

* <span data-ttu-id="b0d81-202">Esempio: @{"tag1"="Valore1";" tag2 "=: value2"}</span><span class="sxs-lookup"><span data-stu-id="b0d81-202">Example: @{"tag1"="value1";"tag2"=:value2"}</span></span>

| <span data-ttu-id="b0d81-203">Alias</span><span class="sxs-lookup"><span data-stu-id="b0d81-203">Aliases</span></span> | <span data-ttu-id="b0d81-204">nessuno</span><span class="sxs-lookup"><span data-stu-id="b0d81-204">none</span></span> |
| --- | --- |
| <span data-ttu-id="b0d81-205">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="b0d81-205">Required?</span></span> |<span data-ttu-id="b0d81-206">false</span><span class="sxs-lookup"><span data-stu-id="b0d81-206">false</span></span> |
| <span data-ttu-id="b0d81-207">Posizione?</span><span class="sxs-lookup"><span data-stu-id="b0d81-207">Position?</span></span> |<span data-ttu-id="b0d81-208">denominata</span><span class="sxs-lookup"><span data-stu-id="b0d81-208">named</span></span> |
| <span data-ttu-id="b0d81-209">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="b0d81-209">Default value</span></span> |<span data-ttu-id="b0d81-210">nessuno</span><span class="sxs-lookup"><span data-stu-id="b0d81-210">none</span></span> |
| <span data-ttu-id="b0d81-211">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="b0d81-211">Accept pipeline input?</span></span> |<span data-ttu-id="b0d81-212">false</span><span class="sxs-lookup"><span data-stu-id="b0d81-212">false</span></span> |
| <span data-ttu-id="b0d81-213">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="b0d81-213">Accept wildcard characters?</span></span> |<span data-ttu-id="b0d81-214">false</span><span class="sxs-lookup"><span data-stu-id="b0d81-214">false</span></span> |

<span data-ttu-id="b0d81-215">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="b0d81-215">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="b0d81-216">Questo cmdlet supporta i parametri comuni di hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction e - WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="b0d81-216">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="b0d81-217">Input</span><span class="sxs-lookup"><span data-stu-id="b0d81-217">Inputs</span></span>
<span data-ttu-id="b0d81-218">tipo di input Hello è di tipo hello di hello oggetti che è possibile inviare tramite pipe toohello cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b0d81-218">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="b0d81-219">outputs</span><span class="sxs-lookup"><span data-stu-id="b0d81-219">Outputs</span></span>
<span data-ttu-id="b0d81-220">tipo di output di Hello è di tipo hello di oggetti hello hello cmdlet genera.</span><span class="sxs-lookup"><span data-stu-id="b0d81-220">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="set-azurermmediaservice"></a><span data-ttu-id="b0d81-221">Set-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="b0d81-221">Set-AzureRmMediaService</span></span>
<span data-ttu-id="b0d81-222">Aggiorna un servizio multimediale.</span><span class="sxs-lookup"><span data-stu-id="b0d81-222">Updates a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="b0d81-223">Sintassi</span><span class="sxs-lookup"><span data-stu-id="b0d81-223">Syntax</span></span>
    Set-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Tags <hashtable>] [-StorageAccounts <PSStorageAccount[]>]  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="b0d81-224">Parametri</span><span class="sxs-lookup"><span data-stu-id="b0d81-224">Parameters</span></span>
<span data-ttu-id="b0d81-225">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="b0d81-225">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="b0d81-226">Specifica il nome di hello di hello toowhich di gruppo di risorse che appartiene questo servizio di supporto.</span><span class="sxs-lookup"><span data-stu-id="b0d81-226">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="b0d81-227">Alias</span><span class="sxs-lookup"><span data-stu-id="b0d81-227">Aliases</span></span> | <span data-ttu-id="b0d81-228">nessuno</span><span class="sxs-lookup"><span data-stu-id="b0d81-228">none</span></span> |
| --- | --- |
| <span data-ttu-id="b0d81-229">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="b0d81-229">Required?</span></span> |<span data-ttu-id="b0d81-230">true</span><span class="sxs-lookup"><span data-stu-id="b0d81-230">true</span></span> |
| <span data-ttu-id="b0d81-231">Posizione?</span><span class="sxs-lookup"><span data-stu-id="b0d81-231">Position?</span></span> |<span data-ttu-id="b0d81-232">0</span><span class="sxs-lookup"><span data-stu-id="b0d81-232">0</span></span> |
| <span data-ttu-id="b0d81-233">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="b0d81-233">Default Value</span></span> |<span data-ttu-id="b0d81-234">nessuno</span><span class="sxs-lookup"><span data-stu-id="b0d81-234">none</span></span> |
| <span data-ttu-id="b0d81-235">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="b0d81-235">Accept Pipeline Input?</span></span> |<span data-ttu-id="b0d81-236">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="b0d81-236">true(ByPropertyName)</span></span> |
| <span data-ttu-id="b0d81-237">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="b0d81-237">Accept wildcard characters?</span></span> |<span data-ttu-id="b0d81-238">false</span><span class="sxs-lookup"><span data-stu-id="b0d81-238">false</span></span> |

<span data-ttu-id="b0d81-239">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="b0d81-239">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="b0d81-240">Specifica il nome di hello del servizio multimediale hello.</span><span class="sxs-lookup"><span data-stu-id="b0d81-240">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="b0d81-241">Alias</span><span class="sxs-lookup"><span data-stu-id="b0d81-241">Aliases</span></span> | <span data-ttu-id="b0d81-242">Nome</span><span class="sxs-lookup"><span data-stu-id="b0d81-242">Name</span></span> |
| --- | --- |
| <span data-ttu-id="b0d81-243">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="b0d81-243">Required?</span></span> |<span data-ttu-id="b0d81-244">true</span><span class="sxs-lookup"><span data-stu-id="b0d81-244">True</span></span> |
| <span data-ttu-id="b0d81-245">Posizione?</span><span class="sxs-lookup"><span data-stu-id="b0d81-245">Position?</span></span> |<span data-ttu-id="b0d81-246">1</span><span class="sxs-lookup"><span data-stu-id="b0d81-246">1</span></span> |
| <span data-ttu-id="b0d81-247">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="b0d81-247">Default value</span></span> |<span data-ttu-id="b0d81-248">nessuno</span><span class="sxs-lookup"><span data-stu-id="b0d81-248">None</span></span> |
| <span data-ttu-id="b0d81-249">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="b0d81-249">Accept pipeline input?</span></span> |<span data-ttu-id="b0d81-250">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="b0d81-250">true(ByPropertyName)</span></span> |
| <span data-ttu-id="b0d81-251">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="b0d81-251">Accept wildcard characters?</span></span> |<span data-ttu-id="b0d81-252">False</span><span class="sxs-lookup"><span data-stu-id="b0d81-252">False</span></span> |

<span data-ttu-id="b0d81-253">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span><span class="sxs-lookup"><span data-stu-id="b0d81-253">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span></span>

<span data-ttu-id="b0d81-254">Specifica l'account di archiviazione associato al servizio multimediale hello.</span><span class="sxs-lookup"><span data-stu-id="b0d81-254">Specifies storage accounts that associated with hello media service.</span></span>

* <span data-ttu-id="b0d81-255">Nuovo account di archiviazione (creata con l'API di gestione risorse di hello) è supportato solo.</span><span class="sxs-lookup"><span data-stu-id="b0d81-255">New storage account (created with hello Resource Manager API) supported only.</span></span>
* <span data-ttu-id="b0d81-256">deve esistere Hello account di archiviazione e ha hello stessa località del servizio di supporto hello.</span><span class="sxs-lookup"><span data-stu-id="b0d81-256">hello storage account must exist and has hello same location with hello media service.</span></span>
* <span data-ttu-id="b0d81-257">È possibile specificare come primario un solo account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="b0d81-257">Only one storage account can be specified as primary.</span></span>

| <span data-ttu-id="b0d81-258">Alias</span><span class="sxs-lookup"><span data-stu-id="b0d81-258">Aliases</span></span> | <span data-ttu-id="b0d81-259">nessuno</span><span class="sxs-lookup"><span data-stu-id="b0d81-259">none</span></span> |
| --- | --- |
| <span data-ttu-id="b0d81-260">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="b0d81-260">Required?</span></span> |<span data-ttu-id="b0d81-261">false</span><span class="sxs-lookup"><span data-stu-id="b0d81-261">false</span></span> |
| <span data-ttu-id="b0d81-262">Posizione?</span><span class="sxs-lookup"><span data-stu-id="b0d81-262">Position?</span></span> |<span data-ttu-id="b0d81-263">denominata</span><span class="sxs-lookup"><span data-stu-id="b0d81-263">Named</span></span> |
| <span data-ttu-id="b0d81-264">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="b0d81-264">Default value</span></span> |<span data-ttu-id="b0d81-265">nessuno</span><span class="sxs-lookup"><span data-stu-id="b0d81-265">none</span></span> |
| <span data-ttu-id="b0d81-266">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="b0d81-266">Accept pipeline input?</span></span> |<span data-ttu-id="b0d81-267">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="b0d81-267">true(ByPropertyName)</span></span> |
| <span data-ttu-id="b0d81-268">Nome del set di parametri</span><span class="sxs-lookup"><span data-stu-id="b0d81-268">Parameter set name</span></span> |<span data-ttu-id="b0d81-269">StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="b0d81-269">StorageAccountsParamSet</span></span> |
| <span data-ttu-id="b0d81-270">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="b0d81-270">Accept wildcard characters?</span></span> |<span data-ttu-id="b0d81-271">false</span><span class="sxs-lookup"><span data-stu-id="b0d81-271">false</span></span> |

<span data-ttu-id="b0d81-272">**-Tags &lt;Hashtable&gt;**</span><span class="sxs-lookup"><span data-stu-id="b0d81-272">**-Tags &lt;Hashtable&gt;**</span></span>

<span data-ttu-id="b0d81-273">Specifica una tabella hash di tag hello che sono associati a questo servizio di supporto.</span><span class="sxs-lookup"><span data-stu-id="b0d81-273">Specifies a hash table of hello tags that are associated with this media service.</span></span>

* <span data-ttu-id="b0d81-274">i tag associati al servizio multimediale hello Hello vengono sostituiti con il valore specificato dal cliente hello.</span><span class="sxs-lookup"><span data-stu-id="b0d81-274">hello tags that are associated with hello media service are replaced with value specified by hello customer.</span></span>

| <span data-ttu-id="b0d81-275">Alias</span><span class="sxs-lookup"><span data-stu-id="b0d81-275">Aliases</span></span> | <span data-ttu-id="b0d81-276">nessuno</span><span class="sxs-lookup"><span data-stu-id="b0d81-276">none</span></span> |
| --- | --- |
| <span data-ttu-id="b0d81-277">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="b0d81-277">Required?</span></span> |<span data-ttu-id="b0d81-278">false</span><span class="sxs-lookup"><span data-stu-id="b0d81-278">False</span></span> |
| <span data-ttu-id="b0d81-279">Posizione?</span><span class="sxs-lookup"><span data-stu-id="b0d81-279">Position?</span></span> |<span data-ttu-id="b0d81-280">denominata</span><span class="sxs-lookup"><span data-stu-id="b0d81-280">Named</span></span> |
| <span data-ttu-id="b0d81-281">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="b0d81-281">Default value</span></span> |<span data-ttu-id="b0d81-282">nessuno</span><span class="sxs-lookup"><span data-stu-id="b0d81-282">None</span></span> |
| <span data-ttu-id="b0d81-283">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="b0d81-283">Accept pipeline input?</span></span> |<span data-ttu-id="b0d81-284">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="b0d81-284">true(ByPropertyName)</span></span> |
| <span data-ttu-id="b0d81-285">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="b0d81-285">Accept wildcard characters?</span></span> |<span data-ttu-id="b0d81-286">false</span><span class="sxs-lookup"><span data-stu-id="b0d81-286">false</span></span> |

<span data-ttu-id="b0d81-287">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="b0d81-287">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="b0d81-288">Questo cmdlet supporta i parametri comuni di hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction e - WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="b0d81-288">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="b0d81-289">Input</span><span class="sxs-lookup"><span data-stu-id="b0d81-289">Inputs</span></span>
<span data-ttu-id="b0d81-290">tipo di input Hello è di tipo hello di hello oggetti che è possibile inviare tramite pipe toohello cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b0d81-290">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="b0d81-291">outputs</span><span class="sxs-lookup"><span data-stu-id="b0d81-291">Outputs</span></span>
<span data-ttu-id="b0d81-292">tipo di output di Hello è di tipo hello di oggetti hello hello cmdlet genera.</span><span class="sxs-lookup"><span data-stu-id="b0d81-292">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="remove-azurermmediaservice"></a><span data-ttu-id="b0d81-293">Remove-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="b0d81-293">Remove-AzureRmMediaService</span></span>
<span data-ttu-id="b0d81-294">Rimuove un servizio multimediale.</span><span class="sxs-lookup"><span data-stu-id="b0d81-294">Removes a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="b0d81-295">Sintassi</span><span class="sxs-lookup"><span data-stu-id="b0d81-295">Syntax</span></span>
    Remove-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="b0d81-296">Parametri</span><span class="sxs-lookup"><span data-stu-id="b0d81-296">Parameters</span></span>
<span data-ttu-id="b0d81-297">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="b0d81-297">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="b0d81-298">Specifica il nome di hello di hello toowhich di gruppo di risorse che appartiene questo servizio di supporto.</span><span class="sxs-lookup"><span data-stu-id="b0d81-298">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="b0d81-299">Alias</span><span class="sxs-lookup"><span data-stu-id="b0d81-299">Aliases</span></span> | <span data-ttu-id="b0d81-300">nessuno</span><span class="sxs-lookup"><span data-stu-id="b0d81-300">none</span></span> |
| --- | --- |
| <span data-ttu-id="b0d81-301">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="b0d81-301">Required?</span></span> |<span data-ttu-id="b0d81-302">true</span><span class="sxs-lookup"><span data-stu-id="b0d81-302">true</span></span> |
| <span data-ttu-id="b0d81-303">Posizione?</span><span class="sxs-lookup"><span data-stu-id="b0d81-303">Position?</span></span> |<span data-ttu-id="b0d81-304">0</span><span class="sxs-lookup"><span data-stu-id="b0d81-304">0</span></span> |
| <span data-ttu-id="b0d81-305">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="b0d81-305">Default value</span></span> |<span data-ttu-id="b0d81-306">nessuno</span><span class="sxs-lookup"><span data-stu-id="b0d81-306">none</span></span> |
| <span data-ttu-id="b0d81-307">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="b0d81-307">Accept pipeline input?</span></span> |<span data-ttu-id="b0d81-308">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="b0d81-308">true(ByPropertyName)</span></span> |
| <span data-ttu-id="b0d81-309">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="b0d81-309">Accept wildcard characters?</span></span> |<span data-ttu-id="b0d81-310">false</span><span class="sxs-lookup"><span data-stu-id="b0d81-310">false</span></span> |

<span data-ttu-id="b0d81-311">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="b0d81-311">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="b0d81-312">Specifica il nome di hello del servizio multimediale hello.</span><span class="sxs-lookup"><span data-stu-id="b0d81-312">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="b0d81-313">Alias</span><span class="sxs-lookup"><span data-stu-id="b0d81-313">Aliases</span></span> | <span data-ttu-id="b0d81-314">nessuno</span><span class="sxs-lookup"><span data-stu-id="b0d81-314">none</span></span> |
| --- | --- |
| <span data-ttu-id="b0d81-315">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="b0d81-315">Required?</span></span> |<span data-ttu-id="b0d81-316">true</span><span class="sxs-lookup"><span data-stu-id="b0d81-316">true</span></span> |
| <span data-ttu-id="b0d81-317">Posizione?</span><span class="sxs-lookup"><span data-stu-id="b0d81-317">Position?</span></span> |<span data-ttu-id="b0d81-318">2</span><span class="sxs-lookup"><span data-stu-id="b0d81-318">2</span></span> |
| <span data-ttu-id="b0d81-319">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="b0d81-319">Default value</span></span> |<span data-ttu-id="b0d81-320">nessuno</span><span class="sxs-lookup"><span data-stu-id="b0d81-320">None</span></span> |
| <span data-ttu-id="b0d81-321">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="b0d81-321">Accept pipeline input?</span></span> |<span data-ttu-id="b0d81-322">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="b0d81-322">true(ByPropertyName)</span></span> |
| <span data-ttu-id="b0d81-323">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="b0d81-323">Accept wildcard characters?</span></span> |<span data-ttu-id="b0d81-324">False</span><span class="sxs-lookup"><span data-stu-id="b0d81-324">False</span></span> |

<span data-ttu-id="b0d81-325">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="b0d81-325">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="b0d81-326">Questo cmdlet supporta i parametri comuni di hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction e - WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="b0d81-326">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="b0d81-327">Input</span><span class="sxs-lookup"><span data-stu-id="b0d81-327">Inputs</span></span>
<span data-ttu-id="b0d81-328">tipo di input Hello è di tipo hello di hello oggetti che è possibile inviare tramite pipe toohello cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b0d81-328">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="b0d81-329">outputs</span><span class="sxs-lookup"><span data-stu-id="b0d81-329">Outputs</span></span>
<span data-ttu-id="b0d81-330">tipo di output di Hello è di tipo hello di oggetti hello hello cmdlet genera.</span><span class="sxs-lookup"><span data-stu-id="b0d81-330">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="get-azurermmediaservice"></a><span data-ttu-id="b0d81-331">Get-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="b0d81-331">Get-AzureRmMediaService</span></span>
<span data-ttu-id="b0d81-332">Ottiene tutti i servizi multimediali in un gruppo di risorse o un servizio multimediale con un nome specificato.</span><span class="sxs-lookup"><span data-stu-id="b0d81-332">Gets all media services in a resource group or a media service with a given name.</span></span>

### <a name="syntax"></a><span data-ttu-id="b0d81-333">Sintassi</span><span class="sxs-lookup"><span data-stu-id="b0d81-333">Syntax</span></span>
<span data-ttu-id="b0d81-334">Set di parametri: ResourceGroupParameterSet</span><span class="sxs-lookup"><span data-stu-id="b0d81-334">ParameterSet: ResourceGroupParameterSet</span></span>

    Get-AzureRmMediaService [-ResourceGroupName] <string>  [<CommonParameters>]    

<span data-ttu-id="b0d81-335">Set di parametri: AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="b0d81-335">ParameterSet: AccountNameParameterSet</span></span>

    Get-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="b0d81-336">Parametri</span><span class="sxs-lookup"><span data-stu-id="b0d81-336">Parameters</span></span>
<span data-ttu-id="b0d81-337">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="b0d81-337">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="b0d81-338">Specifica il nome di hello di hello toowhich di gruppo di risorse che appartiene questo servizio di supporto.</span><span class="sxs-lookup"><span data-stu-id="b0d81-338">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="b0d81-339">Alias</span><span class="sxs-lookup"><span data-stu-id="b0d81-339">Aliases</span></span> | <span data-ttu-id="b0d81-340">nessuno</span><span class="sxs-lookup"><span data-stu-id="b0d81-340">none</span></span> |
| --- | --- |
| <span data-ttu-id="b0d81-341">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="b0d81-341">Required?</span></span> |<span data-ttu-id="b0d81-342">true</span><span class="sxs-lookup"><span data-stu-id="b0d81-342">true</span></span> |
| <span data-ttu-id="b0d81-343">Posizione?</span><span class="sxs-lookup"><span data-stu-id="b0d81-343">Position?</span></span> |<span data-ttu-id="b0d81-344">0</span><span class="sxs-lookup"><span data-stu-id="b0d81-344">0</span></span> |
| <span data-ttu-id="b0d81-345">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="b0d81-345">Default value</span></span> |<span data-ttu-id="b0d81-346">nessuno</span><span class="sxs-lookup"><span data-stu-id="b0d81-346">none</span></span> |
| <span data-ttu-id="b0d81-347">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="b0d81-347">Accept pipeline input?</span></span> |<span data-ttu-id="b0d81-348">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="b0d81-348">true(ByPropertyName)</span></span> |
| <span data-ttu-id="b0d81-349">Nome del set di parametri</span><span class="sxs-lookup"><span data-stu-id="b0d81-349">Parameter set name</span></span> |<span data-ttu-id="b0d81-350">ResourceGroupParameterSet, AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="b0d81-350">ResourceGroupParameterSet, AccountNameParameterSet</span></span> |

<span data-ttu-id="b0d81-351">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="b0d81-351">Accept wildcard characters?</span></span>   <span data-ttu-id="b0d81-352">false</span><span class="sxs-lookup"><span data-stu-id="b0d81-352">false</span></span>

<span data-ttu-id="b0d81-353">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="b0d81-353">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="b0d81-354">Specifica il nome di hello del servizio multimediale hello.</span><span class="sxs-lookup"><span data-stu-id="b0d81-354">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="b0d81-355">Alias</span><span class="sxs-lookup"><span data-stu-id="b0d81-355">Aliases</span></span> | <span data-ttu-id="b0d81-356">nessuno</span><span class="sxs-lookup"><span data-stu-id="b0d81-356">none</span></span> |
| --- | --- |
| <span data-ttu-id="b0d81-357">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="b0d81-357">Required?</span></span> |<span data-ttu-id="b0d81-358">true</span><span class="sxs-lookup"><span data-stu-id="b0d81-358">true</span></span> |
| <span data-ttu-id="b0d81-359">Posizione?</span><span class="sxs-lookup"><span data-stu-id="b0d81-359">Position?</span></span> |<span data-ttu-id="b0d81-360">1</span><span class="sxs-lookup"><span data-stu-id="b0d81-360">1</span></span> |
| <span data-ttu-id="b0d81-361">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="b0d81-361">Default value</span></span> |<span data-ttu-id="b0d81-362">nessuno</span><span class="sxs-lookup"><span data-stu-id="b0d81-362">none</span></span> |
| <span data-ttu-id="b0d81-363">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="b0d81-363">Accept pipeline input?</span></span> |<span data-ttu-id="b0d81-364">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="b0d81-364">true(ByPropertyName)</span></span> |
| <span data-ttu-id="b0d81-365">Nome del set di parametri</span><span class="sxs-lookup"><span data-stu-id="b0d81-365">Parameter set name</span></span> |<span data-ttu-id="b0d81-366">AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="b0d81-366">AccountNameParameterSet</span></span> |
| <span data-ttu-id="b0d81-367">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="b0d81-367">Accept wildcard characters?</span></span> |<span data-ttu-id="b0d81-368">false</span><span class="sxs-lookup"><span data-stu-id="b0d81-368">false</span></span> |

<span data-ttu-id="b0d81-369">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="b0d81-369">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="b0d81-370">Questo cmdlet supporta i parametri comuni di hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction e - WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="b0d81-370">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="b0d81-371">Input</span><span class="sxs-lookup"><span data-stu-id="b0d81-371">Inputs</span></span>
<span data-ttu-id="b0d81-372">tipo di input Hello è di tipo hello di hello oggetti che è possibile inviare tramite pipe toohello cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b0d81-372">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="b0d81-373">outputs</span><span class="sxs-lookup"><span data-stu-id="b0d81-373">Outputs</span></span>
<span data-ttu-id="b0d81-374">tipo di output di Hello è di tipo hello di oggetti hello hello cmdlet genera.</span><span class="sxs-lookup"><span data-stu-id="b0d81-374">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="get-azurermmediaservicekeys"></a><span data-ttu-id="b0d81-375">Get-AzureRmMediaServiceKeys</span><span class="sxs-lookup"><span data-stu-id="b0d81-375">Get-AzureRmMediaServiceKeys</span></span>
<span data-ttu-id="b0d81-376">Ottiene le chiavi di un servizio multimediale.</span><span class="sxs-lookup"><span data-stu-id="b0d81-376">Gets keys of a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="b0d81-377">Sintassi</span><span class="sxs-lookup"><span data-stu-id="b0d81-377">Syntax</span></span>
    Get-AzureRmMediaServiceKeys [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="b0d81-378">Parametri</span><span class="sxs-lookup"><span data-stu-id="b0d81-378">Parameters</span></span>
<span data-ttu-id="b0d81-379">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="b0d81-379">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="b0d81-380">Specifica il nome di hello di hello toowhich di gruppo di risorse che appartiene questo servizio di supporto.</span><span class="sxs-lookup"><span data-stu-id="b0d81-380">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="b0d81-381">Alias</span><span class="sxs-lookup"><span data-stu-id="b0d81-381">Aliases</span></span> | <span data-ttu-id="b0d81-382">nessuno</span><span class="sxs-lookup"><span data-stu-id="b0d81-382">none</span></span> |
| --- | --- |
| <span data-ttu-id="b0d81-383">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="b0d81-383">Required?</span></span> |<span data-ttu-id="b0d81-384">true</span><span class="sxs-lookup"><span data-stu-id="b0d81-384">true</span></span> |
| <span data-ttu-id="b0d81-385">Posizione?</span><span class="sxs-lookup"><span data-stu-id="b0d81-385">Position?</span></span> |<span data-ttu-id="b0d81-386">0</span><span class="sxs-lookup"><span data-stu-id="b0d81-386">0</span></span> |
| <span data-ttu-id="b0d81-387">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="b0d81-387">Default value</span></span> |<span data-ttu-id="b0d81-388">nessuno</span><span class="sxs-lookup"><span data-stu-id="b0d81-388">none</span></span> |
| <span data-ttu-id="b0d81-389">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="b0d81-389">Accept pipeline input?</span></span> |<span data-ttu-id="b0d81-390">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="b0d81-390">true(ByPropertyName)</span></span> |
| <span data-ttu-id="b0d81-391">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="b0d81-391">Accept wildcard characters?</span></span> |<span data-ttu-id="b0d81-392">false</span><span class="sxs-lookup"><span data-stu-id="b0d81-392">false</span></span> |

<span data-ttu-id="b0d81-393">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="b0d81-393">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="b0d81-394">Specifica il nome di hello del servizio multimediale hello.</span><span class="sxs-lookup"><span data-stu-id="b0d81-394">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="b0d81-395">Alias</span><span class="sxs-lookup"><span data-stu-id="b0d81-395">Aliases</span></span> | <span data-ttu-id="b0d81-396">nessuno</span><span class="sxs-lookup"><span data-stu-id="b0d81-396">none</span></span> |
| --- | --- |
| <span data-ttu-id="b0d81-397">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="b0d81-397">Required?</span></span> |<span data-ttu-id="b0d81-398">true</span><span class="sxs-lookup"><span data-stu-id="b0d81-398">true</span></span> |
| <span data-ttu-id="b0d81-399">Posizione?</span><span class="sxs-lookup"><span data-stu-id="b0d81-399">Position?</span></span> |<span data-ttu-id="b0d81-400">1</span><span class="sxs-lookup"><span data-stu-id="b0d81-400">1</span></span> |
| <span data-ttu-id="b0d81-401">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="b0d81-401">Default value</span></span> |<span data-ttu-id="b0d81-402">nessuno</span><span class="sxs-lookup"><span data-stu-id="b0d81-402">none</span></span> |
| <span data-ttu-id="b0d81-403">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="b0d81-403">Accept pipeline input?</span></span> |<span data-ttu-id="b0d81-404">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="b0d81-404">true(ByPropertyName)</span></span> |
| <span data-ttu-id="b0d81-405">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="b0d81-405">Accept wildcard characters?</span></span> |<span data-ttu-id="b0d81-406">false</span><span class="sxs-lookup"><span data-stu-id="b0d81-406">false</span></span> |

<span data-ttu-id="b0d81-407">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="b0d81-407">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="b0d81-408">Questo cmdlet supporta i parametri comuni di hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction e - WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="b0d81-408">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="b0d81-409">Input</span><span class="sxs-lookup"><span data-stu-id="b0d81-409">Inputs</span></span>
<span data-ttu-id="b0d81-410">tipo di input Hello è di tipo hello di hello oggetti che è possibile inviare tramite pipe toohello cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b0d81-410">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="b0d81-411">outputs</span><span class="sxs-lookup"><span data-stu-id="b0d81-411">Outputs</span></span>
<span data-ttu-id="b0d81-412">tipo di output di Hello è di tipo hello di oggetti hello hello cmdlet genera.</span><span class="sxs-lookup"><span data-stu-id="b0d81-412">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="set-azurermmediaservicekey"></a><span data-ttu-id="b0d81-413">Set-AzureRmMediaServiceKey</span><span class="sxs-lookup"><span data-stu-id="b0d81-413">Set-AzureRmMediaServiceKey</span></span>
<span data-ttu-id="b0d81-414">Rigenera una chiave primaria o secondaria di un servizio multimediale.</span><span class="sxs-lookup"><span data-stu-id="b0d81-414">Regenerates a primary or secondary key of a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="b0d81-415">Sintassi</span><span class="sxs-lookup"><span data-stu-id="b0d81-415">Syntax</span></span>
    Set-AzureRmMediaServiceKey [-ResourceGroupName] <string> [-AccountName] <string> [-KeyType] <KeyType> {Primary | Secondary}  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="b0d81-416">Parametri</span><span class="sxs-lookup"><span data-stu-id="b0d81-416">Parameters</span></span>
<span data-ttu-id="b0d81-417">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="b0d81-417">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="b0d81-418">Specifica il nome di hello di hello toowhich di gruppo di risorse che appartiene questo servizio di supporto.</span><span class="sxs-lookup"><span data-stu-id="b0d81-418">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="b0d81-419">Alias</span><span class="sxs-lookup"><span data-stu-id="b0d81-419">Aliases</span></span> | <span data-ttu-id="b0d81-420">nessuno</span><span class="sxs-lookup"><span data-stu-id="b0d81-420">none</span></span> |
| --- | --- |
| <span data-ttu-id="b0d81-421">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="b0d81-421">Required?</span></span> |<span data-ttu-id="b0d81-422">true</span><span class="sxs-lookup"><span data-stu-id="b0d81-422">true</span></span> |
| <span data-ttu-id="b0d81-423">Posizione?</span><span class="sxs-lookup"><span data-stu-id="b0d81-423">Position?</span></span> |<span data-ttu-id="b0d81-424">0</span><span class="sxs-lookup"><span data-stu-id="b0d81-424">0</span></span> |
| <span data-ttu-id="b0d81-425">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="b0d81-425">Default value</span></span> |<span data-ttu-id="b0d81-426">nessuno</span><span class="sxs-lookup"><span data-stu-id="b0d81-426">none</span></span> |
| <span data-ttu-id="b0d81-427">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="b0d81-427">Accept pipeline input?</span></span> |<span data-ttu-id="b0d81-428">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="b0d81-428">true(ByPropertyName)</span></span> |
| <span data-ttu-id="b0d81-429">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="b0d81-429">Accept wildcard characters?</span></span> |<span data-ttu-id="b0d81-430">false</span><span class="sxs-lookup"><span data-stu-id="b0d81-430">false</span></span> |

<span data-ttu-id="b0d81-431">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="b0d81-431">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="b0d81-432">Specifica il nome di hello del servizio multimediale hello.</span><span class="sxs-lookup"><span data-stu-id="b0d81-432">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="b0d81-433">Alias</span><span class="sxs-lookup"><span data-stu-id="b0d81-433">Aliases</span></span> | <span data-ttu-id="b0d81-434">nessuno</span><span class="sxs-lookup"><span data-stu-id="b0d81-434">none</span></span> |
| --- | --- |
| <span data-ttu-id="b0d81-435">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="b0d81-435">Required?</span></span> |<span data-ttu-id="b0d81-436">true</span><span class="sxs-lookup"><span data-stu-id="b0d81-436">true</span></span> |
| <span data-ttu-id="b0d81-437">Posizione?</span><span class="sxs-lookup"><span data-stu-id="b0d81-437">Position?</span></span> |<span data-ttu-id="b0d81-438">1</span><span class="sxs-lookup"><span data-stu-id="b0d81-438">1</span></span> |
| <span data-ttu-id="b0d81-439">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="b0d81-439">Default value</span></span> |<span data-ttu-id="b0d81-440">nessuno</span><span class="sxs-lookup"><span data-stu-id="b0d81-440">none</span></span> |
| <span data-ttu-id="b0d81-441">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="b0d81-441">Accept pipeline input?</span></span> |<span data-ttu-id="b0d81-442">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="b0d81-442">true(ByPropertyName)</span></span> |
| <span data-ttu-id="b0d81-443">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="b0d81-443">Accept wildcard characters?</span></span> |<span data-ttu-id="b0d81-444">false</span><span class="sxs-lookup"><span data-stu-id="b0d81-444">false</span></span> |

<span data-ttu-id="b0d81-445">**-KeyType &lt;KeyType&gt;**</span><span class="sxs-lookup"><span data-stu-id="b0d81-445">**-KeyType &lt;KeyType&gt;**</span></span>

<span data-ttu-id="b0d81-446">Specifica tipo di chiave del servizio di supporto hello hello.</span><span class="sxs-lookup"><span data-stu-id="b0d81-446">Specifies hello key type of hello media service.</span></span>

* <span data-ttu-id="b0d81-447">Primaria o secondaria</span><span class="sxs-lookup"><span data-stu-id="b0d81-447">Primary or Secondary</span></span>

| <span data-ttu-id="b0d81-448">Alias</span><span class="sxs-lookup"><span data-stu-id="b0d81-448">Aliases</span></span> | <span data-ttu-id="b0d81-449">nessuno</span><span class="sxs-lookup"><span data-stu-id="b0d81-449">none</span></span> |
| --- | --- |
| <span data-ttu-id="b0d81-450">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="b0d81-450">Required?</span></span> |<span data-ttu-id="b0d81-451">true</span><span class="sxs-lookup"><span data-stu-id="b0d81-451">true</span></span> |
| <span data-ttu-id="b0d81-452">Posizione?</span><span class="sxs-lookup"><span data-stu-id="b0d81-452">Position?</span></span> |<span data-ttu-id="b0d81-453">2</span><span class="sxs-lookup"><span data-stu-id="b0d81-453">2</span></span> |
| <span data-ttu-id="b0d81-454">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="b0d81-454">Default value</span></span> |<span data-ttu-id="b0d81-455">nessuno</span><span class="sxs-lookup"><span data-stu-id="b0d81-455">none</span></span> |
| <span data-ttu-id="b0d81-456">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="b0d81-456">Accept pipeline input?</span></span> |<span data-ttu-id="b0d81-457">false</span><span class="sxs-lookup"><span data-stu-id="b0d81-457">false</span></span> |
| <span data-ttu-id="b0d81-458">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="b0d81-458">Accept wildcard characters?</span></span> |<span data-ttu-id="b0d81-459">false</span><span class="sxs-lookup"><span data-stu-id="b0d81-459">false</span></span> |

<span data-ttu-id="b0d81-460">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="b0d81-460">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="b0d81-461">Questo cmdlet supporta i parametri comuni di hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction e - WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="b0d81-461">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="b0d81-462">Input</span><span class="sxs-lookup"><span data-stu-id="b0d81-462">Inputs</span></span>
<span data-ttu-id="b0d81-463">tipo di input Hello è di tipo hello di hello oggetti che è possibile inviare tramite pipe toothe cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b0d81-463">hello input type is hello type of hello objects that you can pipe toothe cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="b0d81-464">outputs</span><span class="sxs-lookup"><span data-stu-id="b0d81-464">Outputs</span></span>
<span data-ttu-id="b0d81-465">tipo di output di Hello è di tipo hello di oggetti hello hello cmdlet genera.</span><span class="sxs-lookup"><span data-stu-id="b0d81-465">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="sync-azurermmediaservicestoragekeys"></a><span data-ttu-id="b0d81-466">Sync-AzureRmMediaServiceStorageKeys</span><span class="sxs-lookup"><span data-stu-id="b0d81-466">Sync-AzureRmMediaServiceStorageKeys</span></span>
<span data-ttu-id="b0d81-467">Consente di sincronizzare le chiavi di account di archiviazione per un account di archiviazione associato al servizio multimediale hello.</span><span class="sxs-lookup"><span data-stu-id="b0d81-467">Synchronizes storage account keys for a storage account associated with hello media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="b0d81-468">Sintassi</span><span class="sxs-lookup"><span data-stu-id="b0d81-468">Syntax</span></span>
    Sync-AzureRmMediaServiceStorageKeys [-ResourceGroupName] <string> [-MediaServiceAccountName] <string>    [-StorageAccountId] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="b0d81-469">Parametri</span><span class="sxs-lookup"><span data-stu-id="b0d81-469">Parameters</span></span>
<span data-ttu-id="b0d81-470">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="b0d81-470">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="b0d81-471">Specifica il nome di hello di hello toowhich di gruppo di risorse che appartiene questo servizio di supporto.</span><span class="sxs-lookup"><span data-stu-id="b0d81-471">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="b0d81-472">Alias</span><span class="sxs-lookup"><span data-stu-id="b0d81-472">Aliases</span></span> | <span data-ttu-id="b0d81-473">nessuno</span><span class="sxs-lookup"><span data-stu-id="b0d81-473">none</span></span> |
| --- | --- |
| <span data-ttu-id="b0d81-474">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="b0d81-474">Required?</span></span> |<span data-ttu-id="b0d81-475">true</span><span class="sxs-lookup"><span data-stu-id="b0d81-475">true</span></span> |
| <span data-ttu-id="b0d81-476">Posizione?</span><span class="sxs-lookup"><span data-stu-id="b0d81-476">Position?</span></span> |<span data-ttu-id="b0d81-477">0</span><span class="sxs-lookup"><span data-stu-id="b0d81-477">0</span></span> |
| <span data-ttu-id="b0d81-478">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="b0d81-478">Default value</span></span> |<span data-ttu-id="b0d81-479">nessuno</span><span class="sxs-lookup"><span data-stu-id="b0d81-479">none</span></span> |
| <span data-ttu-id="b0d81-480">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="b0d81-480">Accept pipeline input?</span></span> |<span data-ttu-id="b0d81-481">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="b0d81-481">true(ByPropertyName)</span></span> |
| <span data-ttu-id="b0d81-482">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="b0d81-482">Accept wildcard characters?</span></span> |<span data-ttu-id="b0d81-483">false</span><span class="sxs-lookup"><span data-stu-id="b0d81-483">false</span></span> |

<span data-ttu-id="b0d81-484">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="b0d81-484">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="b0d81-485">Specifica il nome di hello del servizio multimediale hello.</span><span class="sxs-lookup"><span data-stu-id="b0d81-485">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="b0d81-486">Alias</span><span class="sxs-lookup"><span data-stu-id="b0d81-486">Aliases</span></span> | <span data-ttu-id="b0d81-487">nessuno</span><span class="sxs-lookup"><span data-stu-id="b0d81-487">none</span></span> |
| --- | --- |
| <span data-ttu-id="b0d81-488">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="b0d81-488">Required?</span></span> |<span data-ttu-id="b0d81-489">true</span><span class="sxs-lookup"><span data-stu-id="b0d81-489">true</span></span> |
| <span data-ttu-id="b0d81-490">Posizione?</span><span class="sxs-lookup"><span data-stu-id="b0d81-490">Position?</span></span> |<span data-ttu-id="b0d81-491">1</span><span class="sxs-lookup"><span data-stu-id="b0d81-491">1</span></span> |
| <span data-ttu-id="b0d81-492">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="b0d81-492">Default value</span></span> |<span data-ttu-id="b0d81-493">nessuno</span><span class="sxs-lookup"><span data-stu-id="b0d81-493">none</span></span> |
| <span data-ttu-id="b0d81-494">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="b0d81-494">Accept pipeline input?</span></span> |<span data-ttu-id="b0d81-495">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="b0d81-495">true(ByPropertyName)</span></span> |
| <span data-ttu-id="b0d81-496">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="b0d81-496">Accept wildcard characters?</span></span> |<span data-ttu-id="b0d81-497">false</span><span class="sxs-lookup"><span data-stu-id="b0d81-497">false</span></span> |

<span data-ttu-id="b0d81-498">**-StorageAccountId &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="b0d81-498">**-StorageAccountId &lt;String&gt;**</span></span>

<span data-ttu-id="b0d81-499">Specifica l'account di archiviazione hello associato al servizio multimediale hello.</span><span class="sxs-lookup"><span data-stu-id="b0d81-499">Specifies hello storage account associated with hello media service.</span></span>

| <span data-ttu-id="b0d81-500">Alias</span><span class="sxs-lookup"><span data-stu-id="b0d81-500">Aliases</span></span> | <span data-ttu-id="b0d81-501">ID</span><span class="sxs-lookup"><span data-stu-id="b0d81-501">Id</span></span> |
| --- | --- |
| <span data-ttu-id="b0d81-502">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="b0d81-502">Required?</span></span> |<span data-ttu-id="b0d81-503">true</span><span class="sxs-lookup"><span data-stu-id="b0d81-503">true</span></span> |
| <span data-ttu-id="b0d81-504">Posizione?</span><span class="sxs-lookup"><span data-stu-id="b0d81-504">Position?</span></span> |<span data-ttu-id="b0d81-505">2</span><span class="sxs-lookup"><span data-stu-id="b0d81-505">2</span></span> |
| <span data-ttu-id="b0d81-506">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="b0d81-506">Default value</span></span> |<span data-ttu-id="b0d81-507">nessuno</span><span class="sxs-lookup"><span data-stu-id="b0d81-507">none</span></span> |
| <span data-ttu-id="b0d81-508">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="b0d81-508">Accept pipeline input?</span></span> |<span data-ttu-id="b0d81-509">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="b0d81-509">true(ByPropertyName)</span></span> |
| <span data-ttu-id="b0d81-510">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="b0d81-510">Accept wildcard characters?</span></span> |<span data-ttu-id="b0d81-511">false</span><span class="sxs-lookup"><span data-stu-id="b0d81-511">false</span></span> |

<span data-ttu-id="b0d81-512">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="b0d81-512">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="b0d81-513">Questo cmdlet supporta i parametri comuni di hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction e - WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="b0d81-513">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="b0d81-514">Input</span><span class="sxs-lookup"><span data-stu-id="b0d81-514">Inputs</span></span>
<span data-ttu-id="b0d81-515">tipo di input Hello è di tipo hello di hello oggetti che è possibile inviare tramite pipe toohello cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b0d81-515">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="b0d81-516">outputs</span><span class="sxs-lookup"><span data-stu-id="b0d81-516">Outputs</span></span>
<span data-ttu-id="b0d81-517">tipo di output di Hello è di tipo hello di oggetti hello hello cmdlet genera.</span><span class="sxs-lookup"><span data-stu-id="b0d81-517">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="next-step"></a><span data-ttu-id="b0d81-518">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="b0d81-518">Next step</span></span>
<span data-ttu-id="b0d81-519">Vedere i percorsi di apprendimento di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="b0d81-519">Check out Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b0d81-520">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="b0d81-520">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

