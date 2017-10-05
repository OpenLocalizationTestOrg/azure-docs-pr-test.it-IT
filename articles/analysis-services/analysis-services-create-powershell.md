---
title: Creare un server di Azure Analysis Services tramite PowerShell | Microsoft Docs
description: Informazioni su come creare un server di Azure Analysis Services tramite PowerShell
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
ms.openlocfilehash: cb42fd3ed51364cf478848cc51ebbb2f175e96d2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-azure-analysis-services-server-by-using-powershell"></a><span data-ttu-id="1fec3-103">Creare un server di Azure Analysis Services tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="1fec3-103">Create an Azure Analysis Services server by using PowerShell</span></span>

<span data-ttu-id="1fec3-104">Questa esercitazione introduttiva illustra l'uso di PowerShell dalla riga di comando per la creazione di un server di Azure Analysis Services in un [gruppo di risorse di Azure](../azure-resource-manager/resource-group-overview.md) nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="1fec3-104">This quickstart describes using PowerShell from the command line to create an Azure Analysis Services server in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in your Azure subscription.</span></span>

<span data-ttu-id="1fec3-105">Questa attività richiede il modulo Azure PowerShell 4.0 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="1fec3-105">This task requires Azure PowerShell module version 4.0 or later.</span></span> <span data-ttu-id="1fec3-106">Per trovare la versione, eseguire ` Get-Module -ListAvailable AzureRM`.</span><span class="sxs-lookup"><span data-stu-id="1fec3-106">To find the version, run ` Get-Module -ListAvailable AzureRM`.</span></span> <span data-ttu-id="1fec3-107">Per eseguire l'installazione o l'aggiornamento, vedere [Installare il modulo di Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="1fec3-107">To install or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> 

> [!NOTE]
> <span data-ttu-id="1fec3-108">La creazione di un server può avere come risultato un nuovo servizio fatturabile.</span><span class="sxs-lookup"><span data-stu-id="1fec3-108">Creating a server might result in a new billable service.</span></span> <span data-ttu-id="1fec3-109">Per altre informazioni, vedere [Azure Analysis Services Prezzi](https://azure.microsoft.com/pricing/details/analysis-services/).</span><span class="sxs-lookup"><span data-stu-id="1fec3-109">To learn more, see [Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1fec3-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1fec3-110">Prerequisites</span></span>
<span data-ttu-id="1fec3-111">Per completare l'esercitazione introduttiva, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="1fec3-111">To complete this quickstart, you need:</span></span>

* <span data-ttu-id="1fec3-112">**Sottoscrizione di Azure**: visitare la pagina [Versione di valutazione gratuita di Azure](https://azure.microsoft.com/offers/ms-azr-0044p/) per creare un account.</span><span class="sxs-lookup"><span data-stu-id="1fec3-112">**Azure subscription**: Visit [Azure Free Trial](https://azure.microsoft.com/offers/ms-azr-0044p/) to create an account.</span></span>
* <span data-ttu-id="1fec3-113">**Azure Active Directory**: la sottoscrizione deve essere associata a un tenant Azure Active Directory ed è necessario avere un account in tale directory.</span><span class="sxs-lookup"><span data-stu-id="1fec3-113">**Azure Active Directory**: Your subscription must be associated with an Azure Active Directory tenant and you must have an account in that directory.</span></span> <span data-ttu-id="1fec3-114">Per altre informazioni, vedere [Autenticazione e autorizzazioni utente](analysis-services-manage-users.md).</span><span class="sxs-lookup"><span data-stu-id="1fec3-114">To learn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>

## <a name="import-azurermanalysisservices-module"></a><span data-ttu-id="1fec3-115">Importare il modulo AzureRm.AnalysisServices</span><span class="sxs-lookup"><span data-stu-id="1fec3-115">Import AzureRm.AnalysisServices module</span></span>
<span data-ttu-id="1fec3-116">Per creare un server nella sottoscrizione, usare il modulo [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices) del componente.</span><span class="sxs-lookup"><span data-stu-id="1fec3-116">To create a server in your subscription, you use the [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices)  component module.</span></span> <span data-ttu-id="1fec3-117">Caricare il modulo AzureRm.AnalysisServices nella sessione di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1fec3-117">Load the AzureRm.AnalysisServices module into your PowerShell session.</span></span>

```powershell
Import-Module AzureRM.AnalysisServices
```

## <a name="sign-in-to-azure"></a><span data-ttu-id="1fec3-118">Accedere ad Azure</span><span class="sxs-lookup"><span data-stu-id="1fec3-118">Sign in to Azure</span></span>

<span data-ttu-id="1fec3-119">Accedere alla sottoscrizione di Azure usando il comando [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount).</span><span class="sxs-lookup"><span data-stu-id="1fec3-119">Sign in to your Azure subscription by using the [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) command.</span></span> <span data-ttu-id="1fec3-120">Seguire le istruzioni visualizzate sullo schermo.</span><span class="sxs-lookup"><span data-stu-id="1fec3-120">Follow the on-screen directions.</span></span>

```powershell
Add-AzureRmAccount
```

## <a name="create-a-resource-group"></a><span data-ttu-id="1fec3-121">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="1fec3-121">Create a resource group</span></span>
 
<span data-ttu-id="1fec3-122">Un [gruppo di risorse di Azure](../azure-resource-manager/resource-group-overview.md) è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite come gruppo.</span><span class="sxs-lookup"><span data-stu-id="1fec3-122">An [Azure resource group](../azure-resource-manager/resource-group-overview.md) is a logical container where Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="1fec3-123">Quando si crea il server, è necessario specificare un gruppo di risorse nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="1fec3-123">When you create your server, you must specify a resource group in your subscription.</span></span> <span data-ttu-id="1fec3-124">Se non si ha già un gruppo di risorse, è possibile crearne uno nuovo tramite il comando [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="1fec3-124">If you do not already have a resource group, you can create a new one by using the [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span> <span data-ttu-id="1fec3-125">L'esempio seguente crea un gruppo di risorse denominato `myResourceGroup` nell'area Stati Uniti occidentali.</span><span class="sxs-lookup"><span data-stu-id="1fec3-125">The following example creates a resource group named `myResourceGroup` in the West US region.</span></span>

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "West US"
```

## <a name="create-a-server"></a><span data-ttu-id="1fec3-126">Creare un server</span><span class="sxs-lookup"><span data-stu-id="1fec3-126">Create a server</span></span>

<span data-ttu-id="1fec3-127">Creare un nuovo server usando il comando [New-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver).</span><span class="sxs-lookup"><span data-stu-id="1fec3-127">Create a new server by using the [New-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) command.</span></span> <span data-ttu-id="1fec3-128">L'esempio seguente crea un server denominato myServer in myResourceGroup nell'area Stati Uniti occidentali al livello D1 e specifica philipc@adventureworks.com come amministratore del server.</span><span class="sxs-lookup"><span data-stu-id="1fec3-128">The following example creates a server named myServer in myResourceGroup, in the West US region, at the D1 tier, and specifies philipc@adventureworks.com as a server administrator.</span></span>

```powershell
New-AzureRmAnalysisServicesServer -ResourceGroupName "myResourceGroup" -Name "myServer" -Location West US -Sku D1 -Administrator "philipc@adventure-works.com"
```

## <a name="clean-up-resources"></a><span data-ttu-id="1fec3-129">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="1fec3-129">Clean up resources</span></span>

<span data-ttu-id="1fec3-130">È possibile rimuovere il server dalla sottoscrizione usando il comando [Remove-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver).</span><span class="sxs-lookup"><span data-stu-id="1fec3-130">You can remove the server from your subscription by using the [Remove-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) command.</span></span> <span data-ttu-id="1fec3-131">Se si prevede di passare ad altre esercitazioni introduttive ed esercitazioni in questa raccolta, non rimuovere il server.</span><span class="sxs-lookup"><span data-stu-id="1fec3-131">If you continue with other quickstarts and tutorials in this collection, do not remove your server.</span></span> <span data-ttu-id="1fec3-132">L'esempio seguente rimuove il server creato nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="1fec3-132">The following example removes the server created in the previous step.</span></span>


```powershell
Remove-AzureRmAnalysisServicesServer -Name "myServer" -ResourceGroupName "myResourceGroup"
```

## <a name="next-steps"></a><span data-ttu-id="1fec3-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1fec3-133">Next steps</span></span>
<span data-ttu-id="1fec3-134">[Gestire Azure Analysis Services con PowerShell](analysis-services-powershell.md) </span><span class="sxs-lookup"><span data-stu-id="1fec3-134">[Manage Azure Analysis Services with PowerShell](analysis-services-powershell.md) </span></span>  
<span data-ttu-id="1fec3-135">[Distribuire un modello da SSDT](analysis-services-deploy.md) </span><span class="sxs-lookup"><span data-stu-id="1fec3-135">[Deploy a model from SSDT](analysis-services-deploy.md) </span></span>  
[<span data-ttu-id="1fec3-136">Creare un modello nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="1fec3-136">Create a model in Azure portal</span></span>](analysis-services-create-model-portal.md)