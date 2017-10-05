---
title: Informazioni sulle immagini per le macchine virtuali Windows | Microsoft Docs
description: Informazioni sull'utilizzo delle immagini con macchine virtuali Windows in Azure.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 66ff3fab-8e7f-4dff-b8da-ab1c9c9c9af8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: cynthn
ms.openlocfilehash: d421cee0becabdf81d865036d0c98b12b077152b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="about-images-for-windows-virtual-machines"></a><span data-ttu-id="0d486-103">Informazioni sulle immagini per le macchine virtuali Windows</span><span class="sxs-lookup"><span data-stu-id="0d486-103">About images for Windows virtual machines</span></span>
> [!IMPORTANT]
> <span data-ttu-id="0d486-104">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="0d486-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="0d486-105">Questo articolo illustra l'uso del modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="0d486-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="0d486-106">Microsoft consiglia di usare il modello di Gestione risorse per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="0d486-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="0d486-107">Per informazioni sulla ricerca e l'uso delle immagini con il modello di Resource Manager, vedere [qui](../../virtual-machines-windows-cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0d486-107">For information about finding and using images in the Resource Manager model, see [here](../../virtual-machines-windows-cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-classic-about-images](../../../../includes/virtual-machines-common-classic-about-images.md)]

## <a name="working-with-images"></a><span data-ttu-id="0d486-108">Utilizzo di immagini</span><span class="sxs-lookup"><span data-stu-id="0d486-108">Working with images</span></span>

<span data-ttu-id="0d486-109">È possibile usare il modulo Azure PowerShell e il portale di Azure per gestire le immagini disponibili per la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="0d486-109">You can use the Azure PowerShell module and the Azure portal to manage the images available to your Azure subscription.</span></span> <span data-ttu-id="0d486-110">Nel modulo Azure PowerShell sono disponibili più opzioni di comando, pertanto è possibile individuare esattamente gli elementi da visualizzare o le operazioni da eseguire.</span><span class="sxs-lookup"><span data-stu-id="0d486-110">The Azure PowerShell module provides more command options, so you can pinpoint exactly what you want to see or do.</span></span> <span data-ttu-id="0d486-111">Il portale di Azure offre un'interfaccia utente grafica per molte attività di amministrazione quotidiana.</span><span class="sxs-lookup"><span data-stu-id="0d486-111">The Azure portal provides a GUI for many of the everyday administrative tasks.</span></span>

<span data-ttu-id="0d486-112">Di seguito sono riportati alcuni esempi che usano il modulo Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0d486-112">Here are some examples that use the Azure PowerShell module.</span></span>

* <span data-ttu-id="0d486-113">**Ottenere tutte le immagini**: `Get-AzureVMImage` restituisce un elenco di tutte le immagini disponibili nella sottoscrizione corrente, ovvero le immagini dell'utente e quelle fornite da Azure o dai partner.</span><span class="sxs-lookup"><span data-stu-id="0d486-113">**Get all images**:`Get-AzureVMImage`returns a list of all the images available in your current subscription: your images and those provided by Azure or partners.</span></span> <span data-ttu-id="0d486-114">L'elenco risultante potrebbe essere di dimensioni elevate.</span><span class="sxs-lookup"><span data-stu-id="0d486-114">The resulting list could be large.</span></span> <span data-ttu-id="0d486-115">Negli esempi successivi viene illustrato come ottenere un elenco più breve.</span><span class="sxs-lookup"><span data-stu-id="0d486-115">The next examples show how to get a shorter list.</span></span>
* <span data-ttu-id="0d486-116">**Ottenere famiglie di immagini**: `Get-AzureVMImage | select ImageFamily` restituisce un elenco delle famiglie di immagini visualizzando la proprietà **ImageFamily** delle stringhe.</span><span class="sxs-lookup"><span data-stu-id="0d486-116">**Get image families**:`Get-AzureVMImage | select ImageFamily` gets a list of image families by showing strings **ImageFamily** property.</span></span>
* <span data-ttu-id="0d486-117">**Ottenere tutte le immagini in una famiglia specifica**: `Get-AzureVMImage | Where-Object {$_.ImageFamily -eq $family}`</span><span class="sxs-lookup"><span data-stu-id="0d486-117">**Get all images in a specific family**: `Get-AzureVMImage | Where-Object {$_.ImageFamily -eq $family}`</span></span>
* <span data-ttu-id="0d486-118">**Trovare immagini VM**: `Get-AzureVMImage | where {(gm –InputObject $_ -Name DataDiskConfigurations) -ne $null} | Select -Property Label, ImageName` funziona filtrando la proprietà DataDiskConfiguration, che si applica solo alle immagini di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0d486-118">**Find VM Images**: `Get-AzureVMImage | where {(gm –InputObject $_ -Name DataDiskConfigurations) -ne $null} | Select -Property Label, ImageName` This cmdlet works by filtering the DataDiskConfiguration property, which only applies to VM Images.</span></span> <span data-ttu-id="0d486-119">In questo esempio viene inoltre Filtra l'output solo il nome di etichetta e l'immagine.</span><span class="sxs-lookup"><span data-stu-id="0d486-119">This example also filters the output to only the label and image name.</span></span>
* <span data-ttu-id="0d486-120">**Salvare un'immagine generalizzata**: `Save-AzureVMImage –ServiceName "myServiceName" –Name "MyVMtoCapture" –OSState "Generalized" –ImageName "MyVmImage" –ImageLabel "This is my generalized image"`</span><span class="sxs-lookup"><span data-stu-id="0d486-120">**Save a generalized image**: `Save-AzureVMImage –ServiceName "myServiceName" –Name "MyVMtoCapture" –OSState "Generalized" –ImageName "MyVmImage" –ImageLabel "This is my generalized image"`</span></span>
* <span data-ttu-id="0d486-121">**Salvare un'immagine specializzata**: `Save-AzureVMImage –ServiceName "mySvc2" –Name "MyVMToCapture2" –ImageName "myFirstVMImageSP" –OSState "Specialized" -Verbose`</span><span class="sxs-lookup"><span data-stu-id="0d486-121">**Save a specialized image**: `Save-AzureVMImage –ServiceName "mySvc2" –Name "MyVMToCapture2" –ImageName "myFirstVMImageSP" –OSState "Specialized" -Verbose`</span></span>

  > [!TIP]
  > <span data-ttu-id="0d486-122">Il parametro OSState è necessario per creare un'immagine di macchina virtuale, che include il disco del sistema operativo e i dischi dati collegati.</span><span class="sxs-lookup"><span data-stu-id="0d486-122">The OSState parameter is required to create a VM image, which includes the operating system disk and attached data disks.</span></span> <span data-ttu-id="0d486-123">Se non si utilizza il parametro, il cmdlet crea un'immagine del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="0d486-123">If you don’t use the parameter, the cmdlet creates an OS image.</span></span> <span data-ttu-id="0d486-124">Il valore del parametro indica se l'immagine è generalizzata o specializzata, basati su se il disco del sistema operativo è stato preparato per il riutilizzo.</span><span class="sxs-lookup"><span data-stu-id="0d486-124">The value of the parameter indicates whether the image is generalized or specialized, based on whether the operating system disk has been prepared for reuse.</span></span>

* <span data-ttu-id="0d486-125">**Eliminare un'immagine**: `Remove-AzureVMImage –ImageName "MyOldVmImage"`</span><span class="sxs-lookup"><span data-stu-id="0d486-125">**Delete an image**: `Remove-AzureVMImage –ImageName "MyOldVmImage"`</span></span>

## <a name="next-steps"></a><span data-ttu-id="0d486-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0d486-126">Next Steps</span></span>
<span data-ttu-id="0d486-127">È anche possibile [creare una macchina Windows nel portale di Azure](tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="0d486-127">You can also [create a Windows machine using the Azure portal](tutorial.md).</span></span>
