---
title: un server di Azure Analysis Services utilizzando PowerShell aaaCreate | Documenti Microsoft
description: Informazioni su come toocreate un Azure Analysis Services server utilizzando PowerShell
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 08/01/2017
ms.author: owend
ms.custom: mvc
ms.openlocfilehash: 269b78983410f773d47c4cea34d6d353b19f9e91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-analysis-services-server-by-using-powershell"></a><span data-ttu-id="3b885-103">Creare un server di Azure Analysis Services tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="3b885-103">Create an Azure Analysis Services server by using PowerShell</span></span>

<span data-ttu-id="3b885-104">Questa Guida introduttiva viene illustrato l'utilizzo di PowerShell da hello riga di comando toocreate un server di Azure Analysis Services in un [gruppo di risorse](../azure-resource-manager/resource-group-overview.md) nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="3b885-104">This quickstart describes using PowerShell from hello command line toocreate an Azure Analysis Services server in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in your Azure subscription.</span></span>

<span data-ttu-id="3b885-105">Questa attività richiede il modulo Azure PowerShell 4.0 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="3b885-105">This task requires Azure PowerShell module version 4.0 or later.</span></span> <span data-ttu-id="3b885-106">versione di hello toofind, eseguire ` Get-Module -ListAvailable AzureRM`.</span><span class="sxs-lookup"><span data-stu-id="3b885-106">toofind hello version, run ` Get-Module -ListAvailable AzureRM`.</span></span> <span data-ttu-id="3b885-107">tooinstall o l'aggiornamento, vedere [modulo installare Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="3b885-107">tooinstall or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> 

> [!NOTE]
> <span data-ttu-id="3b885-108">La creazione di un server può avere come risultato un nuovo servizio fatturabile.</span><span class="sxs-lookup"><span data-stu-id="3b885-108">Creating a server might result in a new billable service.</span></span> <span data-ttu-id="3b885-109">vedere, più toolearn [dei prezzi di Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).</span><span class="sxs-lookup"><span data-stu-id="3b885-109">toolearn more, see [Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3b885-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="3b885-110">Prerequisites</span></span>
<span data-ttu-id="3b885-111">toocomplete questa Guida rapida, è necessario:</span><span class="sxs-lookup"><span data-stu-id="3b885-111">toocomplete this quickstart, you need:</span></span>

* <span data-ttu-id="3b885-112">**Sottoscrizione di Azure**: visitare [versione di valutazione gratuita di Azure](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate un account.</span><span class="sxs-lookup"><span data-stu-id="3b885-112">**Azure subscription**: Visit [Azure Free Trial](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate an account.</span></span>
* <span data-ttu-id="3b885-113">**Azure Active Directory**: la sottoscrizione deve essere associata a un tenant Azure Active Directory ed è necessario avere un account in tale directory.</span><span class="sxs-lookup"><span data-stu-id="3b885-113">**Azure Active Directory**: Your subscription must be associated with an Azure Active Directory tenant and you must have an account in that directory.</span></span> <span data-ttu-id="3b885-114">vedere, più toolearn [l'autenticazione e le autorizzazioni utente](analysis-services-manage-users.md).</span><span class="sxs-lookup"><span data-stu-id="3b885-114">toolearn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>

## <a name="import-azurermanalysisservices-module"></a><span data-ttu-id="3b885-115">Importare il modulo AzureRm.AnalysisServices</span><span class="sxs-lookup"><span data-stu-id="3b885-115">Import AzureRm.AnalysisServices module</span></span>
<span data-ttu-id="3b885-116">toocreate un server nella sottoscrizione, utilizzare hello [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices) modulo componente.</span><span class="sxs-lookup"><span data-stu-id="3b885-116">toocreate a server in your subscription, you use hello [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices)  component module.</span></span> <span data-ttu-id="3b885-117">Caricare il modulo di AzureRm.AnalysisServices hello nella sessione di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3b885-117">Load hello AzureRm.AnalysisServices module into your PowerShell session.</span></span>

```powershell
Import-Module AzureRM.AnalysisServices
```

## <a name="sign-in-tooazure"></a><span data-ttu-id="3b885-118">Accedi tooAzure</span><span class="sxs-lookup"><span data-stu-id="3b885-118">Sign in tooAzure</span></span>

<span data-ttu-id="3b885-119">Accedi tooyour sottoscrizione di Azure tramite hello [Aggiungi AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) comando.</span><span class="sxs-lookup"><span data-stu-id="3b885-119">Sign in tooyour Azure subscription by using hello [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) command.</span></span> <span data-ttu-id="3b885-120">Seguire hello le direzioni.</span><span class="sxs-lookup"><span data-stu-id="3b885-120">Follow hello on-screen directions.</span></span>

```powershell
Add-AzureRmAccount
```

## <a name="create-a-resource-group"></a><span data-ttu-id="3b885-121">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="3b885-121">Create a resource group</span></span>
 
<span data-ttu-id="3b885-122">Un [gruppo di risorse di Azure](../azure-resource-manager/resource-group-overview.md) è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite come gruppo.</span><span class="sxs-lookup"><span data-stu-id="3b885-122">An [Azure resource group](../azure-resource-manager/resource-group-overview.md) is a logical container where Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="3b885-123">Quando si crea il server, è necessario specificare un gruppo di risorse nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="3b885-123">When you create your server, you must specify a resource group in your subscription.</span></span> <span data-ttu-id="3b885-124">Se si dispone già di un gruppo di risorse, è possibile creare una nuova istanza utilizzando hello [New AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) comando.</span><span class="sxs-lookup"><span data-stu-id="3b885-124">If you do not already have a resource group, you can create a new one by using hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span> <span data-ttu-id="3b885-125">esempio Hello crea un gruppo di risorse denominato `myResourceGroup` nell'area Stati Uniti occidentali hello.</span><span class="sxs-lookup"><span data-stu-id="3b885-125">hello following example creates a resource group named `myResourceGroup` in hello West US region.</span></span>

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "West US"
```

## <a name="create-a-server"></a><span data-ttu-id="3b885-126">Creare un server</span><span class="sxs-lookup"><span data-stu-id="3b885-126">Create a server</span></span>

<span data-ttu-id="3b885-127">Creare un nuovo server tramite hello [New AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) comando.</span><span class="sxs-lookup"><span data-stu-id="3b885-127">Create a new server by using hello [New-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) command.</span></span> <span data-ttu-id="3b885-128">Hello esempio seguente viene creato un server denominato Server1 in myResourceGroup, nell'area Stati Uniti occidentali hello, a livello di hello D1 e philipc@adventureworks.com come un amministratore del server.</span><span class="sxs-lookup"><span data-stu-id="3b885-128">hello following example creates a server named myServer in myResourceGroup, in hello West US region, at hello D1 tier, and specifies philipc@adventureworks.com as a server administrator.</span></span>

```powershell
New-AzureRmAnalysisServicesServer -ResourceGroupName "myResourceGroup" -Name "myServer" -Location West US -Sku D1 -Administrator "philipc@adventure-works.com"
```

## <a name="clean-up-resources"></a><span data-ttu-id="3b885-129">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="3b885-129">Clean up resources</span></span>

<span data-ttu-id="3b885-130">È possibile rimuovere il server di hello dalla sottoscrizione utilizzando hello [Remove AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) comando.</span><span class="sxs-lookup"><span data-stu-id="3b885-130">You can remove hello server from your subscription by using hello [Remove-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) command.</span></span> <span data-ttu-id="3b885-131">Se si prevede di passare ad altre esercitazioni introduttive ed esercitazioni in questa raccolta, non rimuovere il server.</span><span class="sxs-lookup"><span data-stu-id="3b885-131">If you continue with other quickstarts and tutorials in this collection, do not remove your server.</span></span> <span data-ttu-id="3b885-132">Hello esempio seguente rimuove il server di hello creato nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="3b885-132">hello following example removes hello server created in hello previous step.</span></span>


```powershell
Remove-AzureRmAnalysisServicesServer -Name "myServer" -ResourceGroupName "myResourceGroup"
```

## <a name="next-steps"></a><span data-ttu-id="3b885-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3b885-133">Next steps</span></span>
<span data-ttu-id="3b885-134">[Gestire Azure Analysis Services con PowerShell](analysis-services-powershell.md) </span><span class="sxs-lookup"><span data-stu-id="3b885-134">[Manage Azure Analysis Services with PowerShell](analysis-services-powershell.md) </span></span>  
<span data-ttu-id="3b885-135">[Distribuire un modello da SSDT](analysis-services-deploy.md) </span><span class="sxs-lookup"><span data-stu-id="3b885-135">[Deploy a model from SSDT](analysis-services-deploy.md) </span></span>  
[<span data-ttu-id="3b885-136">Creare un modello nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="3b885-136">Create a model in Azure portal</span></span>](analysis-services-create-model-portal.md)