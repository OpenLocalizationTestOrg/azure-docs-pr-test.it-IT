---
title: Selezionare immagini di VM Windows in Azure | Microsoft Docs
description: Imparare a usare Azure PowerSHell per determinare l'editore, l'offerta, lo SKU e la versione per le immagini di VM del Marketplace.
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 188b8974-fabd-4cd3-b7dc-559cbb86b98a
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/12/2017
ms.author: danlep
ms.openlocfilehash: 814ae260123c045d4b6766bf4b312f874cd77068
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-find-windows-vm-images-in-the-azure-marketplace-with-azure-powershell"></a><span data-ttu-id="c96e3-103">Come trovare immagini di VM Windows in Azure Marketplace con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c96e3-103">How to find Windows VM images in the Azure Marketplace with Azure PowerShell</span></span>

<span data-ttu-id="c96e3-104">Questo argomento descrive come usare Azure PowerShell per trovare immagini di VM in Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="c96e3-104">This topic describes how to use Azure PowerShell to find VM images in the Azure Marketplace.</span></span> <span data-ttu-id="c96e3-105">Usare queste informazioni per specificare un'immagine del Marketplace quando si crea una VM Windows.</span><span class="sxs-lookup"><span data-stu-id="c96e3-105">Use this information to specify a Marketplace image when you create a Windows VM.</span></span>

<span data-ttu-id="c96e3-106">Verificare di aver prima installato e configurato il [modulo di Azure PowerShell](/powershell/azure/install-azurerm-ps) più recente.</span><span class="sxs-lookup"><span data-stu-id="c96e3-106">Make sure that you installed and configured the latest [Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>



## <a name="table-of-commonly-used-windows-images"></a><span data-ttu-id="c96e3-107">Tabella delle immagini Windows usate comunemente</span><span class="sxs-lookup"><span data-stu-id="c96e3-107">Table of commonly used Windows images</span></span>
| <span data-ttu-id="c96e3-108">PublisherName</span><span class="sxs-lookup"><span data-stu-id="c96e3-108">PublisherName</span></span> | <span data-ttu-id="c96e3-109">Offerta</span><span class="sxs-lookup"><span data-stu-id="c96e3-109">Offer</span></span> | <span data-ttu-id="c96e3-110">Sku</span><span class="sxs-lookup"><span data-stu-id="c96e3-110">Sku</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c96e3-111">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="c96e3-111">MicrosoftWindowsServer</span></span> |<span data-ttu-id="c96e3-112">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="c96e3-112">WindowsServer</span></span> |<span data-ttu-id="c96e3-113">2016-Datacenter</span><span class="sxs-lookup"><span data-stu-id="c96e3-113">2016-Datacenter</span></span> |
| <span data-ttu-id="c96e3-114">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="c96e3-114">MicrosoftWindowsServer</span></span> |<span data-ttu-id="c96e3-115">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="c96e3-115">WindowsServer</span></span> |<span data-ttu-id="c96e3-116">2016-Datacenter-Server-Core</span><span class="sxs-lookup"><span data-stu-id="c96e3-116">2016-Datacenter-Server-Core</span></span> |
| <span data-ttu-id="c96e3-117">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="c96e3-117">MicrosoftWindowsServer</span></span> |<span data-ttu-id="c96e3-118">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="c96e3-118">WindowsServer</span></span> |<span data-ttu-id="c96e3-119">2016-Datacenter-with-Containers</span><span class="sxs-lookup"><span data-stu-id="c96e3-119">2016-Datacenter-with-Containers</span></span> |
| <span data-ttu-id="c96e3-120">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="c96e3-120">MicrosoftWindowsServer</span></span> |<span data-ttu-id="c96e3-121">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="c96e3-121">WindowsServer</span></span> |<span data-ttu-id="c96e3-122">2016-Nano-Server</span><span class="sxs-lookup"><span data-stu-id="c96e3-122">2016-Nano-Server</span></span> |
| <span data-ttu-id="c96e3-123">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="c96e3-123">MicrosoftWindowsServer</span></span> |<span data-ttu-id="c96e3-124">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="c96e3-124">WindowsServer</span></span> |<span data-ttu-id="c96e3-125">2012-R2-Datacenter</span><span class="sxs-lookup"><span data-stu-id="c96e3-125">2012-R2-Datacenter</span></span> |
| <span data-ttu-id="c96e3-126">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="c96e3-126">MicrosoftWindowsServer</span></span> |<span data-ttu-id="c96e3-127">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="c96e3-127">WindowsServer</span></span> |<span data-ttu-id="c96e3-128">2008 R2-SP1</span><span class="sxs-lookup"><span data-stu-id="c96e3-128">2008-R2-SP1</span></span> |
| <span data-ttu-id="c96e3-129">MicrosoftDynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="c96e3-129">MicrosoftDynamicsNAV</span></span> |<span data-ttu-id="c96e3-130">DynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="c96e3-130">DynamicsNAV</span></span> |<span data-ttu-id="c96e3-131">2017</span><span class="sxs-lookup"><span data-stu-id="c96e3-131">2017</span></span> |
| <span data-ttu-id="c96e3-132">MicrosoftSharePoint</span><span class="sxs-lookup"><span data-stu-id="c96e3-132">MicrosoftSharePoint</span></span> |<span data-ttu-id="c96e3-133">MicrosoftSharePointServer</span><span class="sxs-lookup"><span data-stu-id="c96e3-133">MicrosoftSharePointServer</span></span> |<span data-ttu-id="c96e3-134">2016</span><span class="sxs-lookup"><span data-stu-id="c96e3-134">2016</span></span> |
| <span data-ttu-id="c96e3-135">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="c96e3-135">MicrosoftSQLServer</span></span> |<span data-ttu-id="c96e3-136">SQL2016-WS2016</span><span class="sxs-lookup"><span data-stu-id="c96e3-136">SQL2016-WS2016</span></span> |<span data-ttu-id="c96e3-137">Enterprise</span><span class="sxs-lookup"><span data-stu-id="c96e3-137">Enterprise</span></span> |
| <span data-ttu-id="c96e3-138">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="c96e3-138">MicrosoftSQLServer</span></span> |<span data-ttu-id="c96e3-139">SQL2014SP2-WS2012R2</span><span class="sxs-lookup"><span data-stu-id="c96e3-139">SQL2014SP2-WS2012R2</span></span> |<span data-ttu-id="c96e3-140">Enterprise</span><span class="sxs-lookup"><span data-stu-id="c96e3-140">Enterprise</span></span> |
| <span data-ttu-id="c96e3-141">MicrosoftWindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="c96e3-141">MicrosoftWindowsServerHPCPack</span></span> |<span data-ttu-id="c96e3-142">WindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="c96e3-142">WindowsServerHPCPack</span></span> |<span data-ttu-id="c96e3-143">2012R2</span><span class="sxs-lookup"><span data-stu-id="c96e3-143">2012R2</span></span> |
| <span data-ttu-id="c96e3-144">MicrosoftWindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="c96e3-144">MicrosoftWindowsServerEssentials</span></span> |<span data-ttu-id="c96e3-145">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="c96e3-145">WindowsServerEssentials</span></span> |<span data-ttu-id="c96e3-146">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="c96e3-146">WindowsServerEssentials</span></span> |

## <a name="find-specific-images"></a><span data-ttu-id="c96e3-147">Trovare immagini specifiche</span><span class="sxs-lookup"><span data-stu-id="c96e3-147">Find specific images</span></span>


<span data-ttu-id="c96e3-148">Quando si crea una nuova macchina virtuale con Gestione risorse di Azure, in alcuni casi è necessario specificare un'immagine combinando le seguenti proprietà dell'immagine:</span><span class="sxs-lookup"><span data-stu-id="c96e3-148">When creating a new virtual machine with Azure Resource Manager, in some cases you need to specify an image with the combination of the following image properties:</span></span>

* <span data-ttu-id="c96e3-149">Editore</span><span class="sxs-lookup"><span data-stu-id="c96e3-149">Publisher</span></span>
* <span data-ttu-id="c96e3-150">Offerta</span><span class="sxs-lookup"><span data-stu-id="c96e3-150">Offer</span></span>
* <span data-ttu-id="c96e3-151">SKU</span><span class="sxs-lookup"><span data-stu-id="c96e3-151">SKU</span></span>

<span data-ttu-id="c96e3-152">Ad esempio, usare questi valori con il cmdlet di PowerShell [Set-AzureRMVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) o con un modello di gruppo di risorse in cui è necessario specificare il tipo di VM da creare.</span><span class="sxs-lookup"><span data-stu-id="c96e3-152">For example, use these values with the [Set-AzureRMVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) PowerShell cmdlet, or with a resource group template in which you must specify the type of VM to be created.</span></span>

<span data-ttu-id="c96e3-153">Se è necessario determinare questi valori, è possibile eseguire i cmdlet [Get-AzureRMVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher), [Get-AzureRMVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer) e [Get-AzureRMVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) per passare alle immagini.</span><span class="sxs-lookup"><span data-stu-id="c96e3-153">If you need to determine these values, you can run the [Get-AzureRMVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher), [Get-AzureRMVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer), and [Get-AzureRMVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) cmdlets to navigate the images.</span></span> <span data-ttu-id="c96e3-154">Questi valori possono essere determinati:</span><span class="sxs-lookup"><span data-stu-id="c96e3-154">You determine these values:</span></span>

1. <span data-ttu-id="c96e3-155">Elencando gli editori di immagini.</span><span class="sxs-lookup"><span data-stu-id="c96e3-155">List the image publishers.</span></span>
2. <span data-ttu-id="c96e3-156">Elencando le offerte di un determinato editore.</span><span class="sxs-lookup"><span data-stu-id="c96e3-156">For a given publisher, list their offers.</span></span>
3. <span data-ttu-id="c96e3-157">Elencando le SKU di una determinata offerta.</span><span class="sxs-lookup"><span data-stu-id="c96e3-157">For a given offer, list their SKUs.</span></span>

<span data-ttu-id="c96e3-158">In primo luogo, elencare gli editori con i seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="c96e3-158">First, list the publishers with the following commands:</span></span>

```powershell
$locName="<Azure location, such as West US>"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName
```

<span data-ttu-id="c96e3-159">Specificare il nome dell'editore prescelto ed eseguire i seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="c96e3-159">Fill in your chosen publisher name and run the following commands:</span></span>

```powershell
$pubName="<publisher>"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

<span data-ttu-id="c96e3-160">Specificare il nome dell'offerta prescelta ed eseguire i seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="c96e3-160">Fill in your chosen offer name and run the following commands:</span></span>

```powershell
$offerName="<offer>"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

<span data-ttu-id="c96e3-161">Nell'output del comando `Get-AzureRMVMImageSku` ci sono tutte le informazioni necessarie per specificare l'immagine per una nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c96e3-161">From the output of the `Get-AzureRMVMImageSku` command, you have all the information you need to specify the image for a new virtual machine.</span></span>

<span data-ttu-id="c96e3-162">Di seguito è riportato un esempio completo:</span><span class="sxs-lookup"><span data-stu-id="c96e3-162">The following shows a full example:</span></span>

```powershell
$locName="West US"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName

```

<span data-ttu-id="c96e3-163">Output:</span><span class="sxs-lookup"><span data-stu-id="c96e3-163">Output:</span></span>

```
PublisherName
-------------
a10networks
aiscaler-cache-control-ddos-and-url-rewriting-
alertlogic
AlertLogic.Extension
Barracuda.Azure.ConnectivityAgent
barracudanetworks
basho
boxless
bssw
Canonical
...
```

<span data-ttu-id="c96e3-164">Per l'editore "MicrosoftWindowsServer":</span><span class="sxs-lookup"><span data-stu-id="c96e3-164">For the "MicrosoftWindowsServer" publisher:</span></span>

```powershell
$pubName="MicrosoftWindowsServer"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

<span data-ttu-id="c96e3-165">Output:</span><span class="sxs-lookup"><span data-stu-id="c96e3-165">Output:</span></span>

```
Offer
-----
Windows-HUB
WindowsServer
WindowsServer-HUB
```

<span data-ttu-id="c96e3-166">Per l'offerta "WindowsServer":</span><span class="sxs-lookup"><span data-stu-id="c96e3-166">For the "WindowsServer" offer:</span></span>

```powershell
$offerName="WindowsServer"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

<span data-ttu-id="c96e3-167">Output:</span><span class="sxs-lookup"><span data-stu-id="c96e3-167">Output:</span></span>

```
Skus
----
2008-R2-SP1
2008-R2-SP1-smalldisk
2012-Datacenter
2012-Datacenter-smalldisk
2012-R2-Datacenter
2012-R2-Datacenter-smalldisk
2016-Datacenter
2016-Datacenter-Server-Core
2016-Datacenter-Server-Core-smalldisk
2016-Datacenter-smalldisk
2016-Datacenter-with-Containers
2016-Nano-Server
```

<span data-ttu-id="c96e3-168">In questo elenco, copiare il nome della SKU scelta per disporre di tutte le informazioni per il cmdlet di PowerShell `Set-AzureRMVMSourceImage` o per un modello di gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="c96e3-168">From this list, copy the chosen SKU name, and you have all the information for the `Set-AzureRMVMSourceImage` PowerShell cmdlet or for a resource group template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c96e3-169">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c96e3-169">Next steps</span></span>
<span data-ttu-id="c96e3-170">A questo punto è possibile scegliere con precisione l'immagine da usare.</span><span class="sxs-lookup"><span data-stu-id="c96e3-170">Now you can choose precisely the image you want to use.</span></span> <span data-ttu-id="c96e3-171">Per creare rapidamente una macchina virtuale usando le informazioni dell'immagine, appena trovate, vedere [Creare una macchina virtuale Windows con PowerShell](quick-create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="c96e3-171">To create a virtual machine quickly by using the image information, which you just found, see [Create a Windows virtual machine with PowerShell](quick-create-powershell.md).</span></span>
