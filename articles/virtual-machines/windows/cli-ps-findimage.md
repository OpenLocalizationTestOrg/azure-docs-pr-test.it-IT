---
title: le immagini di macchina virtuale Windows aaaSelect in Azure | Documenti Microsoft
description: Informazioni su come toouse Azure PowerSHell toodetermine hello editore, offerta, SKU e la versione per le immagini VM Marketplace.
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
ms.openlocfilehash: 752edcd0935f5141832e49503ae800ea0145e219
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofind-windows-vm-images-in-hello-azure-marketplace-with-azure-powershell"></a><span data-ttu-id="a987d-103">La modalità di immagini toofind macchina virtuale Windows in hello Azure Marketplace con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a987d-103">How toofind Windows VM images in hello Azure Marketplace with Azure PowerShell</span></span>

<span data-ttu-id="a987d-104">In questo argomento viene descritto come toouse Azure PowerShell toofind VM immagini in hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="a987d-104">This topic describes how toouse Azure PowerShell toofind VM images in hello Azure Marketplace.</span></span> <span data-ttu-id="a987d-105">Quando si crea una macchina virtuale di Windows, utilizzare questo toospecify informazioni un'immagine del Marketplace.</span><span class="sxs-lookup"><span data-stu-id="a987d-105">Use this information toospecify a Marketplace image when you create a Windows VM.</span></span>

<span data-ttu-id="a987d-106">Assicurarsi che è installato e configurato hello più recente [modulo Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="a987d-106">Make sure that you installed and configured hello latest [Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>



## <a name="table-of-commonly-used-windows-images"></a><span data-ttu-id="a987d-107">Tabella delle immagini Windows usate comunemente</span><span class="sxs-lookup"><span data-stu-id="a987d-107">Table of commonly used Windows images</span></span>
| <span data-ttu-id="a987d-108">PublisherName</span><span class="sxs-lookup"><span data-stu-id="a987d-108">PublisherName</span></span> | <span data-ttu-id="a987d-109">Offerta</span><span class="sxs-lookup"><span data-stu-id="a987d-109">Offer</span></span> | <span data-ttu-id="a987d-110">Sku</span><span class="sxs-lookup"><span data-stu-id="a987d-110">Sku</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a987d-111">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="a987d-111">MicrosoftWindowsServer</span></span> |<span data-ttu-id="a987d-112">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="a987d-112">WindowsServer</span></span> |<span data-ttu-id="a987d-113">2016-Datacenter</span><span class="sxs-lookup"><span data-stu-id="a987d-113">2016-Datacenter</span></span> |
| <span data-ttu-id="a987d-114">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="a987d-114">MicrosoftWindowsServer</span></span> |<span data-ttu-id="a987d-115">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="a987d-115">WindowsServer</span></span> |<span data-ttu-id="a987d-116">2016-Datacenter-Server-Core</span><span class="sxs-lookup"><span data-stu-id="a987d-116">2016-Datacenter-Server-Core</span></span> |
| <span data-ttu-id="a987d-117">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="a987d-117">MicrosoftWindowsServer</span></span> |<span data-ttu-id="a987d-118">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="a987d-118">WindowsServer</span></span> |<span data-ttu-id="a987d-119">2016-Datacenter-with-Containers</span><span class="sxs-lookup"><span data-stu-id="a987d-119">2016-Datacenter-with-Containers</span></span> |
| <span data-ttu-id="a987d-120">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="a987d-120">MicrosoftWindowsServer</span></span> |<span data-ttu-id="a987d-121">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="a987d-121">WindowsServer</span></span> |<span data-ttu-id="a987d-122">2016-Nano-Server</span><span class="sxs-lookup"><span data-stu-id="a987d-122">2016-Nano-Server</span></span> |
| <span data-ttu-id="a987d-123">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="a987d-123">MicrosoftWindowsServer</span></span> |<span data-ttu-id="a987d-124">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="a987d-124">WindowsServer</span></span> |<span data-ttu-id="a987d-125">2012-R2-Datacenter</span><span class="sxs-lookup"><span data-stu-id="a987d-125">2012-R2-Datacenter</span></span> |
| <span data-ttu-id="a987d-126">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="a987d-126">MicrosoftWindowsServer</span></span> |<span data-ttu-id="a987d-127">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="a987d-127">WindowsServer</span></span> |<span data-ttu-id="a987d-128">2008 R2-SP1</span><span class="sxs-lookup"><span data-stu-id="a987d-128">2008-R2-SP1</span></span> |
| <span data-ttu-id="a987d-129">MicrosoftDynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="a987d-129">MicrosoftDynamicsNAV</span></span> |<span data-ttu-id="a987d-130">DynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="a987d-130">DynamicsNAV</span></span> |<span data-ttu-id="a987d-131">2017</span><span class="sxs-lookup"><span data-stu-id="a987d-131">2017</span></span> |
| <span data-ttu-id="a987d-132">MicrosoftSharePoint</span><span class="sxs-lookup"><span data-stu-id="a987d-132">MicrosoftSharePoint</span></span> |<span data-ttu-id="a987d-133">MicrosoftSharePointServer</span><span class="sxs-lookup"><span data-stu-id="a987d-133">MicrosoftSharePointServer</span></span> |<span data-ttu-id="a987d-134">2016</span><span class="sxs-lookup"><span data-stu-id="a987d-134">2016</span></span> |
| <span data-ttu-id="a987d-135">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="a987d-135">MicrosoftSQLServer</span></span> |<span data-ttu-id="a987d-136">SQL2016-WS2016</span><span class="sxs-lookup"><span data-stu-id="a987d-136">SQL2016-WS2016</span></span> |<span data-ttu-id="a987d-137">Enterprise</span><span class="sxs-lookup"><span data-stu-id="a987d-137">Enterprise</span></span> |
| <span data-ttu-id="a987d-138">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="a987d-138">MicrosoftSQLServer</span></span> |<span data-ttu-id="a987d-139">SQL2014SP2-WS2012R2</span><span class="sxs-lookup"><span data-stu-id="a987d-139">SQL2014SP2-WS2012R2</span></span> |<span data-ttu-id="a987d-140">Enterprise</span><span class="sxs-lookup"><span data-stu-id="a987d-140">Enterprise</span></span> |
| <span data-ttu-id="a987d-141">MicrosoftWindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="a987d-141">MicrosoftWindowsServerHPCPack</span></span> |<span data-ttu-id="a987d-142">WindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="a987d-142">WindowsServerHPCPack</span></span> |<span data-ttu-id="a987d-143">2012R2</span><span class="sxs-lookup"><span data-stu-id="a987d-143">2012R2</span></span> |
| <span data-ttu-id="a987d-144">MicrosoftWindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="a987d-144">MicrosoftWindowsServerEssentials</span></span> |<span data-ttu-id="a987d-145">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="a987d-145">WindowsServerEssentials</span></span> |<span data-ttu-id="a987d-146">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="a987d-146">WindowsServerEssentials</span></span> |

## <a name="find-specific-images"></a><span data-ttu-id="a987d-147">Trovare immagini specifiche</span><span class="sxs-lookup"><span data-stu-id="a987d-147">Find specific images</span></span>


<span data-ttu-id="a987d-148">Quando si crea una nuova macchina virtuale con Azure Resource Manager, in alcuni casi è necessario toospecify un'immagine con una combinazione hello di hello le proprietà di immagine seguenti:</span><span class="sxs-lookup"><span data-stu-id="a987d-148">When creating a new virtual machine with Azure Resource Manager, in some cases you need toospecify an image with hello combination of hello following image properties:</span></span>

* <span data-ttu-id="a987d-149">Autore</span><span class="sxs-lookup"><span data-stu-id="a987d-149">Publisher</span></span>
* <span data-ttu-id="a987d-150">Offerta</span><span class="sxs-lookup"><span data-stu-id="a987d-150">Offer</span></span>
* <span data-ttu-id="a987d-151">SKU</span><span class="sxs-lookup"><span data-stu-id="a987d-151">SKU</span></span>

<span data-ttu-id="a987d-152">Ad esempio, utilizzare questi valori con hello [Set AzureRMVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) cmdlet di PowerShell o con un modello di gruppo di risorse in cui è necessario specificare il tipo di hello di toobe macchina virtuale creata.</span><span class="sxs-lookup"><span data-stu-id="a987d-152">For example, use these values with hello [Set-AzureRMVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) PowerShell cmdlet, or with a resource group template in which you must specify hello type of VM toobe created.</span></span>

<span data-ttu-id="a987d-153">Se è necessario toodetermine questi valori, è possibile eseguire hello [Get AzureRMVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher), [Get AzureRMVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer), e [Get AzureRMVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) cmdlet immagini di hello toonavigate.</span><span class="sxs-lookup"><span data-stu-id="a987d-153">If you need toodetermine these values, you can run hello [Get-AzureRMVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher), [Get-AzureRMVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer), and [Get-AzureRMVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) cmdlets toonavigate hello images.</span></span> <span data-ttu-id="a987d-154">Questi valori possono essere determinati:</span><span class="sxs-lookup"><span data-stu-id="a987d-154">You determine these values:</span></span>

1. <span data-ttu-id="a987d-155">Elenco hello immagine server di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="a987d-155">List hello image publishers.</span></span>
2. <span data-ttu-id="a987d-156">Elencando le offerte di un determinato editore.</span><span class="sxs-lookup"><span data-stu-id="a987d-156">For a given publisher, list their offers.</span></span>
3. <span data-ttu-id="a987d-157">Elencando le SKU di una determinata offerta.</span><span class="sxs-lookup"><span data-stu-id="a987d-157">For a given offer, list their SKUs.</span></span>

<span data-ttu-id="a987d-158">In primo luogo, elenco publishers hello con hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="a987d-158">First, list hello publishers with hello following commands:</span></span>

```powershell
$locName="<Azure location, such as West US>"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName
```

<span data-ttu-id="a987d-159">Immettere il nome del server di pubblicazione selezionato ed eseguire hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="a987d-159">Fill in your chosen publisher name and run hello following commands:</span></span>

```powershell
$pubName="<publisher>"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

<span data-ttu-id="a987d-160">Immettere il nome scelto offerta ed eseguire hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="a987d-160">Fill in your chosen offer name and run hello following commands:</span></span>

```powershell
$offerName="<offer>"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

<span data-ttu-id="a987d-161">Output di hello di hello `Get-AzureRMVMImageSku` comando, si dispongano di tutte le informazioni di hello immagine hello toospecify è necessario per una nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a987d-161">From hello output of hello `Get-AzureRMVMImageSku` command, you have all hello information you need toospecify hello image for a new virtual machine.</span></span>

<span data-ttu-id="a987d-162">Hello seguito è riportato un esempio completo è:</span><span class="sxs-lookup"><span data-stu-id="a987d-162">hello following shows a full example:</span></span>

```powershell
$locName="West US"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName

```

<span data-ttu-id="a987d-163">Output:</span><span class="sxs-lookup"><span data-stu-id="a987d-163">Output:</span></span>

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

<span data-ttu-id="a987d-164">Per server di pubblicazione "MicrosoftWindowsServer" hello:</span><span class="sxs-lookup"><span data-stu-id="a987d-164">For hello "MicrosoftWindowsServer" publisher:</span></span>

```powershell
$pubName="MicrosoftWindowsServer"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

<span data-ttu-id="a987d-165">Output:</span><span class="sxs-lookup"><span data-stu-id="a987d-165">Output:</span></span>

```
Offer
-----
Windows-HUB
WindowsServer
WindowsServer-HUB
```

<span data-ttu-id="a987d-166">Per l'offerta di "Windows Server" hello:</span><span class="sxs-lookup"><span data-stu-id="a987d-166">For hello "WindowsServer" offer:</span></span>

```powershell
$offerName="WindowsServer"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

<span data-ttu-id="a987d-167">Output:</span><span class="sxs-lookup"><span data-stu-id="a987d-167">Output:</span></span>

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

<span data-ttu-id="a987d-168">Da questo elenco, copiare hello scelto nome SKU e si dispongano di tutte le informazioni per hello hello `Set-AzureRMVMSourceImage` cmdlet di PowerShell o per un modello di gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="a987d-168">From this list, copy hello chosen SKU name, and you have all hello information for hello `Set-AzureRMVMSourceImage` PowerShell cmdlet or for a resource group template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a987d-169">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a987d-169">Next steps</span></span>
<span data-ttu-id="a987d-170">Ora è possibile scegliere l'immagine di hello precisamente desiderato toouse.</span><span class="sxs-lookup"><span data-stu-id="a987d-170">Now you can choose precisely hello image you want toouse.</span></span> <span data-ttu-id="a987d-171">toocreate una macchina virtuale rapidamente utilizzando informazioni sulle immagini hello solo disponibili, vedere [creare una macchina virtuale Windows con PowerShell](quick-create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="a987d-171">toocreate a virtual machine quickly by using hello image information, which you just found, see [Create a Windows virtual machine with PowerShell](quick-create-powershell.md).</span></span>
