---
title: Come contrassegnare una risorsa di macchina virtuale Windows in Azure | Documentazione Microsoft
description: "Informazioni sull’assegnazione di tag a una macchina virtuale Windows creata in Azure con il modello di distribuzione di Resource Manager"
services: virtual-machines-windows
documentationcenter: 
author: mmccrory
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 56d17f45-e4a7-4d84-8022-b40334ae49d2
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/05/2016
ms.author: memccror
ms.openlocfilehash: 5f00c4265cea3db02dbb09a7f81be636a3fdd3d1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-tag-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="65f82-103">Come assegnare un tag a una macchina virtuale Windows in Azure</span><span class="sxs-lookup"><span data-stu-id="65f82-103">How to tag a Windows virtual machine in Azure</span></span>
<span data-ttu-id="65f82-104">Questo articolo descrive diversi modi per contrassegnare una macchina virtuale Windows in Azure tramite il modello di distribuzione Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="65f82-104">This article describes different ways to tag a Windows virtual machine in Azure through the Resource Manager deployment model.</span></span> <span data-ttu-id="65f82-105">I tag sono coppie chiave/valore definite dall'utente che possono essere inserite direttamente in una risorsa o un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="65f82-105">Tags are user-defined key/value pairs which can be placed directly on a resource or a resource group.</span></span> <span data-ttu-id="65f82-106">Attualmente, Azure supporta fino a 15 tag per ogni risorsa e gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="65f82-106">Azure currently supports up to 15 tags per resource and resource group.</span></span> <span data-ttu-id="65f82-107">I tag possono essere posizionati su una risorsa al momento della creazione o aggiunti a una risorsa esistente.</span><span class="sxs-lookup"><span data-stu-id="65f82-107">Tags may be placed on a resource at the time of creation or added to an existing resource.</span></span> <span data-ttu-id="65f82-108">Si noti che i tag sono supportati solo per le risorse create tramite il modello di distribuzione Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="65f82-108">Please note that tags are supported for resources created via the Resource Manager deployment model only.</span></span> <span data-ttu-id="65f82-109">Se si desidera assegnare un tag a una macchina virtuale Linux, vedere l'articolo relativo a [come assegnare un tag a una macchina virtuale Linux in Azure](../linux/tag.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="65f82-109">If you want to tag a Linux virtual machine, see [How to tag a Linux virtual machine in Azure](../linux/tag.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-powershell"></a><span data-ttu-id="65f82-110">Assegnazione di tag tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="65f82-110">Tagging with PowerShell</span></span>
<span data-ttu-id="65f82-111">Per creare, aggiungere ed eliminare i tag tramite PowerShell, è prima necessario configurare l'[ambiente PowerShell con Azure Resource Manager][PowerShell environment with Azure Resource Manager].</span><span class="sxs-lookup"><span data-stu-id="65f82-111">To create, add, and delete tags through PowerShell, you first need to set up your [PowerShell environment with Azure Resource Manager][PowerShell environment with Azure Resource Manager].</span></span> <span data-ttu-id="65f82-112">Dopo aver completato l'installazione, è possibile inserire tag su risorse di calcolo, rete e archiviazione al momento della creazione o dopo la creazione della risorsa tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="65f82-112">Once you have completed the setup, you can place tags on Compute, Network, and Storage resources at creation or after the resource is created via PowerShell.</span></span> <span data-ttu-id="65f82-113">Questo articolo si concentrerà su come visualizzare o modificare tag inseriti nelle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="65f82-113">This article will concentrate on viewing/editing tags placed on Virtual Machines.</span></span>

<span data-ttu-id="65f82-114">Per prima cosa, spostarsi su una macchina virtuale tramite il `Get-AzureRmVM` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="65f82-114">First, navigate to a Virtual Machine through the `Get-AzureRmVM` cmdlet.</span></span>

        PS C:\> Get-AzureRmVM -ResourceGroupName "MyResourceGroup" -Name "MyTestVM"

<span data-ttu-id="65f82-115">Se la macchina virtuale contiene già dei tag, verranno visualizzati tutti i tag per la risorsa:</span><span class="sxs-lookup"><span data-stu-id="65f82-115">If your Virtual Machine already contains tags, you will then see all the tags on your resource:</span></span>

        Tags : {
                "Application": "MyApp1",
                "Created By": "MyName",
                "Department": "MyDepartment",
                "Environment": "Production"
               }

<span data-ttu-id="65f82-116">Se si desidera aggiungere i tag tramite PowerShell, è possibile utilizzare il comando `Set-AzureRmResource` .</span><span class="sxs-lookup"><span data-stu-id="65f82-116">If you would like to add tags through PowerShell, you can use the `Set-AzureRmResource` command.</span></span> <span data-ttu-id="65f82-117">Nota: Quando si aggiornano i tag tramite PowerShell, i tag vengono aggiornati nel loro complesso.</span><span class="sxs-lookup"><span data-stu-id="65f82-117">Note when updating tags through PowerShell, tags are updated as a whole.</span></span> <span data-ttu-id="65f82-118">Se si aggiunge un tag a una risorsa che già dispone di tag, sarà pertanto necessario includere tutti i tag che si desidera inserire nella risorsa.</span><span class="sxs-lookup"><span data-stu-id="65f82-118">So if you are adding one tag to a resource that already has tags, you will need to include all the tags that you want to be placed on the resource.</span></span> <span data-ttu-id="65f82-119">Di seguito è riportato un esempio di come aggiungere ulteriori tag a una risorsa tramite Cmdlets di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="65f82-119">Below is an example of how to add additional tags to a resource through PowerShell Cmdlets.</span></span>

<span data-ttu-id="65f82-120">Questo primo cmdlet imposta tutti i tag inseriti in *MyTestVM* sulla variabile *$tags* usando `Get-AzureRmResource` e la proprietà `Tags`.</span><span class="sxs-lookup"><span data-stu-id="65f82-120">This first cmdlet sets all of the tags placed on *MyTestVM* to the *$tags* variable, using the `Get-AzureRmResource` and `Tags` property.</span></span>

        PS C:\> $tags = (Get-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM).Tags

<span data-ttu-id="65f82-121">Il secondo comando consente di visualizzare i tag per la variabile specificata.</span><span class="sxs-lookup"><span data-stu-id="65f82-121">The second command displays the tags for the given variable.</span></span>

        PS C:\> $tags

        Name        Value
        ----                           -----
        Value        MyDepartment
        Name        Department
        Value        MyApp1
        Name        Application
        Value        MyName
        Name        Created By
        Value        Production
        Name        Environment

<span data-ttu-id="65f82-122">Il terzo comando aggiunge un altro tag alla variabile *$tags* .</span><span class="sxs-lookup"><span data-stu-id="65f82-122">The third command adds an additional tag to the *$tags* variable.</span></span> <span data-ttu-id="65f82-123">Si noti l'uso di **+=** per aggiungere la nuova coppia chiave/valore all'elenco *$tags* .</span><span class="sxs-lookup"><span data-stu-id="65f82-123">Note the use of the **+=** to append the new key/value pair to the *$tags* list.</span></span>

        PS C:\> $tags += @{Name="Location";Value="MyLocation"}

<span data-ttu-id="65f82-124">Il quarto comando imposta tutti i tag definiti nella variabile *$tags* sulla risorsa specificata.</span><span class="sxs-lookup"><span data-stu-id="65f82-124">The fourth command sets all of the tags defined in the *$tags* variable to the given resource.</span></span> <span data-ttu-id="65f82-125">In questo caso, è MyTestVM.</span><span class="sxs-lookup"><span data-stu-id="65f82-125">In this case, it is MyTestVM.</span></span>

        PS C:\> Set-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM -ResourceType "Microsoft.Compute/VirtualMachines" -Tag $tags

<span data-ttu-id="65f82-126">Il quinto comando visualizza tutti i tag sulla risorsa.</span><span class="sxs-lookup"><span data-stu-id="65f82-126">The fifth command displays all of the tags on the resource.</span></span> <span data-ttu-id="65f82-127">Come si può vedere, *Location* è ora definito come un tag con *MyLocation* come valore.</span><span class="sxs-lookup"><span data-stu-id="65f82-127">As you can see, *Location* is now defined as a tag with *MyLocation* as the value.</span></span>

        PS C:\> (Get-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM).Tags

        Name        Value
        ----                           -----
        Value        MyDepartment
        Name        Department
        Value        MyApp1
        Name        Application
        Value        MyName
        Name        Created By
        Value        Production
        Name        Environment
        Value        MyLocation
        Name        Location

<span data-ttu-id="65f82-128">Per altre informazioni sull'assegnazione di tag tramite PowerShell, vedere l'articolo relativo ai [cmdlet di Azure Resource Manager][Azure Resource Cmdlets].</span><span class="sxs-lookup"><span data-stu-id="65f82-128">To learn more about tagging through PowerShell, check out the [Azure Resource Cmdlets][Azure Resource Cmdlets].</span></span>

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a><span data-ttu-id="65f82-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="65f82-129">Next steps</span></span>
* <span data-ttu-id="65f82-130">Per altre informazioni sull'uso dei tag nelle risorse di Azure, vedere [Panoramica di Azure Resource Manager][Azure Resource Manager Overview] e [Uso dei tag per organizzare le risorse di Azure][Using Tags to organize your Azure Resources].</span><span class="sxs-lookup"><span data-stu-id="65f82-130">To learn more about tagging your Azure resources, see [Azure Resource Manager Overview][Azure Resource Manager Overview] and [Using Tags to organize your Azure Resources][Using Tags to organize your Azure Resources].</span></span>
* <span data-ttu-id="65f82-131">Per informazioni sull'utilità dei tag nella gestione dell'uso delle risorse di Azure, vedere [Informazioni sulla fattura di Azure][Understanding your Azure Bill] e [Ottenere informazioni dettagliate sul consumo di risorse di Microsoft Azure][Gain insights into your Microsoft Azure resource consumption].</span><span class="sxs-lookup"><span data-stu-id="65f82-131">To see how tags can help you manage your use of Azure resources, see [Understanding your Azure Bill][Understanding your Azure Bill] and [Gain insights into your Microsoft Azure resource consumption][Gain insights into your Microsoft Azure resource consumption].</span></span>

[PowerShell environment with Azure Resource Manager]: ../../azure-resource-manager/powershell-azure-resource-manager.md
[Azure Resource Cmdlets]: https://msdn.microsoft.com/library/azure/dn757692.aspx
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags to organize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
