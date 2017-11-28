---
title: aaaAbout immagini per le macchine virtuali Windows | Documenti Microsoft
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
ms.openlocfilehash: c7cfa1d018a5e99d5b68f559ec9ae1f14e4dec8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="about-images-for-windows-virtual-machines"></a><span data-ttu-id="c4c51-103">Informazioni sulle immagini per le macchine virtuali Windows</span><span class="sxs-lookup"><span data-stu-id="c4c51-103">About images for Windows virtual machines</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c4c51-104">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="c4c51-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="c4c51-105">In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="c4c51-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="c4c51-106">Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="c4c51-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="c4c51-107">Per informazioni sulla ricerca e utilizzo di immagini nel modello di gestione risorse di hello, vedere [qui](../../virtual-machines-windows-cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c4c51-107">For information about finding and using images in hello Resource Manager model, see [here](../../virtual-machines-windows-cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-classic-about-images](../../../../includes/virtual-machines-common-classic-about-images.md)]

## <a name="working-with-images"></a><span data-ttu-id="c4c51-108">Utilizzo di immagini</span><span class="sxs-lookup"><span data-stu-id="c4c51-108">Working with images</span></span>

<span data-ttu-id="c4c51-109">È possibile utilizzare il modulo di Azure PowerShell hello e hello toomanage portale Azure hello immagini disponibili tooyour sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c4c51-109">You can use hello Azure PowerShell module and hello Azure portal toomanage hello images available tooyour Azure subscription.</span></span> <span data-ttu-id="c4c51-110">modulo di Azure PowerShell Hello fornisce più opzioni di comando, individuare esattamente ciò che si desidera toosee o eseguire.</span><span class="sxs-lookup"><span data-stu-id="c4c51-110">hello Azure PowerShell module provides more command options, so you can pinpoint exactly what you want toosee or do.</span></span> <span data-ttu-id="c4c51-111">Hello portale di Azure fornisce un'interfaccia utente grafica per la maggior parte delle attività amministrative quotidiane hello.</span><span class="sxs-lookup"><span data-stu-id="c4c51-111">hello Azure portal provides a GUI for many of hello everyday administrative tasks.</span></span>

<span data-ttu-id="c4c51-112">Di seguito sono riportati alcuni esempi che utilizzano il modulo di Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="c4c51-112">Here are some examples that use hello Azure PowerShell module.</span></span>

* <span data-ttu-id="c4c51-113">**Ottenere tutte le immagini**:`Get-AzureVMImage`restituisce un elenco di tutte le immagini di hello disponibili nella sottoscrizione corrente: le immagini e quelle fornite da Azure o i partner.</span><span class="sxs-lookup"><span data-stu-id="c4c51-113">**Get all images**:`Get-AzureVMImage`returns a list of all hello images available in your current subscription: your images and those provided by Azure or partners.</span></span> <span data-ttu-id="c4c51-114">elenco di Hello risultante potrebbe essere elevato.</span><span class="sxs-lookup"><span data-stu-id="c4c51-114">hello resulting list could be large.</span></span> <span data-ttu-id="c4c51-115">Hello esempi successivi viene illustrato come tooget un elenco più breve.</span><span class="sxs-lookup"><span data-stu-id="c4c51-115">hello next examples show how tooget a shorter list.</span></span>
* <span data-ttu-id="c4c51-116">**Ottenere famiglie di immagini**: `Get-AzureVMImage | select ImageFamily` restituisce un elenco delle famiglie di immagini visualizzando la proprietà **ImageFamily** delle stringhe.</span><span class="sxs-lookup"><span data-stu-id="c4c51-116">**Get image families**:`Get-AzureVMImage | select ImageFamily` gets a list of image families by showing strings **ImageFamily** property.</span></span>
* <span data-ttu-id="c4c51-117">**Ottenere tutte le immagini in una famiglia specifica**: `Get-AzureVMImage | Where-Object {$_.ImageFamily -eq $family}`</span><span class="sxs-lookup"><span data-stu-id="c4c51-117">**Get all images in a specific family**: `Get-AzureVMImage | Where-Object {$_.ImageFamily -eq $family}`</span></span>
* <span data-ttu-id="c4c51-118">**Trovare le immagini VM**: `Get-AzureVMImage | where {(gm –InputObject $_ -Name DataDiskConfigurations) -ne $null} | Select -Property Label, ImageName` questo cmdlet funziona filtrando la proprietà DataDiskConfiguration di hello, che si applica solo le immagini tooVM.</span><span class="sxs-lookup"><span data-stu-id="c4c51-118">**Find VM Images**: `Get-AzureVMImage | where {(gm –InputObject $_ -Name DataDiskConfigurations) -ne $null} | Select -Property Label, ImageName` This cmdlet works by filtering hello DataDiskConfiguration property, which only applies tooVM Images.</span></span> <span data-ttu-id="c4c51-119">In questo esempio viene inoltre Filtra hello output tooonly hello etichetta e il nome.</span><span class="sxs-lookup"><span data-stu-id="c4c51-119">This example also filters hello output tooonly hello label and image name.</span></span>
* <span data-ttu-id="c4c51-120">**Salvare un'immagine generalizzata**: `Save-AzureVMImage –ServiceName "myServiceName" –Name "MyVMtoCapture" –OSState "Generalized" –ImageName "MyVmImage" –ImageLabel "This is my generalized image"`</span><span class="sxs-lookup"><span data-stu-id="c4c51-120">**Save a generalized image**: `Save-AzureVMImage –ServiceName "myServiceName" –Name "MyVMtoCapture" –OSState "Generalized" –ImageName "MyVmImage" –ImageLabel "This is my generalized image"`</span></span>
* <span data-ttu-id="c4c51-121">**Salvare un'immagine specializzata**: `Save-AzureVMImage –ServiceName "mySvc2" –Name "MyVMToCapture2" –ImageName "myFirstVMImageSP" –OSState "Specialized" -Verbose`</span><span class="sxs-lookup"><span data-stu-id="c4c51-121">**Save a specialized image**: `Save-AzureVMImage –ServiceName "mySvc2" –Name "MyVMToCapture2" –ImageName "myFirstVMImageSP" –OSState "Specialized" -Verbose`</span></span>

  > [!TIP]
  > <span data-ttu-id="c4c51-122">Hello parametro OSState è necessario toocreate un'immagine di macchina virtuale, che include disco del sistema operativo hello e i dischi dati collegati.</span><span class="sxs-lookup"><span data-stu-id="c4c51-122">hello OSState parameter is required toocreate a VM image, which includes hello operating system disk and attached data disks.</span></span> <span data-ttu-id="c4c51-123">Se non si utilizza il parametro hello, hello cmdlet crea un'immagine del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="c4c51-123">If you don’t use hello parameter, hello cmdlet creates an OS image.</span></span> <span data-ttu-id="c4c51-124">valore di Hello del parametro hello indica se l'immagine hello è generalizzata o specializzata, in base se disco del sistema operativo hello è stato preparato per il riutilizzo.</span><span class="sxs-lookup"><span data-stu-id="c4c51-124">hello value of hello parameter indicates whether hello image is generalized or specialized, based on whether hello operating system disk has been prepared for reuse.</span></span>

* <span data-ttu-id="c4c51-125">**Eliminare un'immagine**: `Remove-AzureVMImage –ImageName "MyOldVmImage"`</span><span class="sxs-lookup"><span data-stu-id="c4c51-125">**Delete an image**: `Remove-AzureVMImage –ImageName "MyOldVmImage"`</span></span>

## <a name="next-steps"></a><span data-ttu-id="c4c51-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c4c51-126">Next Steps</span></span>
<span data-ttu-id="c4c51-127">È anche possibile [creare una macchina Windows hello portale di Azure usando](tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="c4c51-127">You can also [create a Windows machine using hello Azure portal](tutorial.md).</span></span>
