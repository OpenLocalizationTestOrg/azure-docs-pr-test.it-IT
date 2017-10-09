---
title: aaaHow tootag una risorsa di macchina virtuale Windows in Azure | Documenti Microsoft
description: Informazioni sull'uso dei tag di una macchina virtuale Windows creata in Azure tramite il modello di distribuzione di gestione risorse di hello
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
ms.openlocfilehash: 160416ddc35998b3c98c6e579668a6a5eb6de6e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootag-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="4a604-103">Come tootag una macchina virtuale Windows Azure</span><span class="sxs-lookup"><span data-stu-id="4a604-103">How tootag a Windows virtual machine in Azure</span></span>
<span data-ttu-id="4a604-104">Questo articolo descrive diversi modi tootag una macchina virtuale Windows in Azure tramite il modello di distribuzione del hello Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="4a604-104">This article describes different ways tootag a Windows virtual machine in Azure through hello Resource Manager deployment model.</span></span> <span data-ttu-id="4a604-105">I tag sono coppie chiave/valore definite dall'utente che possono essere inserite direttamente in una risorsa o un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="4a604-105">Tags are user-defined key/value pairs which can be placed directly on a resource or a resource group.</span></span> <span data-ttu-id="4a604-106">Azure supporta attualmente i tag too15 per ogni risorsa e gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="4a604-106">Azure currently supports up too15 tags per resource and resource group.</span></span> <span data-ttu-id="4a604-107">Tag possono essere inseriti su una risorsa in fase di hello della creazione o aggiunta di risorse esistente tooan.</span><span class="sxs-lookup"><span data-stu-id="4a604-107">Tags may be placed on a resource at hello time of creation or added tooan existing resource.</span></span> <span data-ttu-id="4a604-108">Si noti che i tag sono supportati per le risorse create tramite solo modello di distribuzione di gestione delle risorse hello.</span><span class="sxs-lookup"><span data-stu-id="4a604-108">Please note that tags are supported for resources created via hello Resource Manager deployment model only.</span></span> <span data-ttu-id="4a604-109">Se si desidera tootag una macchina virtuale Linux, vedere [come una macchina virtuale di Linux in Azure tootag](../linux/tag.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4a604-109">If you want tootag a Linux virtual machine, see [How tootag a Linux virtual machine in Azure](../linux/tag.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-powershell"></a><span data-ttu-id="4a604-110">Assegnazione di tag tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="4a604-110">Tagging with PowerShell</span></span>
<span data-ttu-id="4a604-111">toocreate, aggiungere ed eliminare i tag mediante PowerShell, è necessario innanzitutto tooset backup il [ambiente di PowerShell con Gestione risorse di Azure][PowerShell environment with Azure Resource Manager].</span><span class="sxs-lookup"><span data-stu-id="4a604-111">toocreate, add, and delete tags through PowerShell, you first need tooset up your [PowerShell environment with Azure Resource Manager][PowerShell environment with Azure Resource Manager].</span></span> <span data-ttu-id="4a604-112">Dopo aver completato l'installazione di hello, è possibile inserire tag sulle risorse di calcolo, rete e archiviazione al momento della creazione o dopo la creazione di risorse hello tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4a604-112">Once you have completed hello setup, you can place tags on Compute, Network, and Storage resources at creation or after hello resource is created via PowerShell.</span></span> <span data-ttu-id="4a604-113">Questo articolo si concentrerà su come visualizzare o modificare tag inseriti nelle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="4a604-113">This article will concentrate on viewing/editing tags placed on Virtual Machines.</span></span>

<span data-ttu-id="4a604-114">Passare innanzitutto tooa macchina virtuale tramite hello `Get-AzureRmVM` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4a604-114">First, navigate tooa Virtual Machine through hello `Get-AzureRmVM` cmdlet.</span></span>

        PS C:\> Get-AzureRmVM -ResourceGroupName "MyResourceGroup" -Name "MyTestVM"

<span data-ttu-id="4a604-115">Se la macchina virtuale contiene già i tag, tutti i tag di hello verrà quindi visualizzato nella risorsa:</span><span class="sxs-lookup"><span data-stu-id="4a604-115">If your Virtual Machine already contains tags, you will then see all hello tags on your resource:</span></span>

        Tags : {
                "Application": "MyApp1",
                "Created By": "MyName",
                "Department": "MyDepartment",
                "Environment": "Production"
               }

<span data-ttu-id="4a604-116">Se si desidera tooadd tag tramite PowerShell, è possibile utilizzare hello `Set-AzureRmResource` comando.</span><span class="sxs-lookup"><span data-stu-id="4a604-116">If you would like tooadd tags through PowerShell, you can use hello `Set-AzureRmResource` command.</span></span> <span data-ttu-id="4a604-117">Nota: Quando si aggiornano i tag tramite PowerShell, i tag vengono aggiornati nel loro complesso.</span><span class="sxs-lookup"><span data-stu-id="4a604-117">Note when updating tags through PowerShell, tags are updated as a whole.</span></span> <span data-ttu-id="4a604-118">Pertanto se si aggiunge una risorsa tooa tag che dispone già di tag, sarà necessario tooinclude tutti i tag di hello che si desidera toobe posizionato sulla risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="4a604-118">So if you are adding one tag tooa resource that already has tags, you will need tooinclude all hello tags that you want toobe placed on hello resource.</span></span> <span data-ttu-id="4a604-119">Di seguito è riportato un esempio di come tooadd ulteriori tag risorsa tooa tramite Cmdlets di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4a604-119">Below is an example of how tooadd additional tags tooa resource through PowerShell Cmdlets.</span></span>

<span data-ttu-id="4a604-120">Questo cmdlet prima imposta tutti i tag hello sul *MyTestVM* toohello *$tags* variabile, utilizzando hello `Get-AzureRmResource` e `Tags` proprietà.</span><span class="sxs-lookup"><span data-stu-id="4a604-120">This first cmdlet sets all of hello tags placed on *MyTestVM* toohello *$tags* variable, using hello `Get-AzureRmResource` and `Tags` property.</span></span>

        PS C:\> $tags = (Get-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM).Tags

<span data-ttu-id="4a604-121">Hello secondo comando Visualizza tag hello per hello condizione variabile.</span><span class="sxs-lookup"><span data-stu-id="4a604-121">hello second command displays hello tags for hello given variable.</span></span>

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

<span data-ttu-id="4a604-122">Hello terzo comando aggiunge un toohello ulteriori tag *$tags* variabile.</span><span class="sxs-lookup"><span data-stu-id="4a604-122">hello third command adds an additional tag toohello *$tags* variable.</span></span> <span data-ttu-id="4a604-123">Si noti utilizzo hello di hello  **+=**  tooappend hello toohello di coppia chiave/valore nuovo *$tags* elenco.</span><span class="sxs-lookup"><span data-stu-id="4a604-123">Note hello use of hello **+=** tooappend hello new key/value pair toohello *$tags* list.</span></span>

        PS C:\> $tags += @{Name="Location";Value="MyLocation"}

<span data-ttu-id="4a604-124">quarto comando Hello imposta tutti i tag hello definiti in hello *$tags* toohello variabile assegnato risorsa.</span><span class="sxs-lookup"><span data-stu-id="4a604-124">hello fourth command sets all of hello tags defined in hello *$tags* variable toohello given resource.</span></span> <span data-ttu-id="4a604-125">In questo caso, è MyTestVM.</span><span class="sxs-lookup"><span data-stu-id="4a604-125">In this case, it is MyTestVM.</span></span>

        PS C:\> Set-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM -ResourceType "Microsoft.Compute/VirtualMachines" -Tag $tags

<span data-ttu-id="4a604-126">Hello quinto comando Visualizza tutti i tag hello sulla risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="4a604-126">hello fifth command displays all of hello tags on hello resource.</span></span> <span data-ttu-id="4a604-127">Come si può notare, *percorso* è ora definito come un tag con *MyLocation* come valore di hello.</span><span class="sxs-lookup"><span data-stu-id="4a604-127">As you can see, *Location* is now defined as a tag with *MyLocation* as hello value.</span></span>

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

<span data-ttu-id="4a604-128">toolearn altre informazioni sull'assegnazione di tag tramite PowerShell, estrarre hello [cmdlet delle risorse Azure][Azure Resource Cmdlets].</span><span class="sxs-lookup"><span data-stu-id="4a604-128">toolearn more about tagging through PowerShell, check out hello [Azure Resource Cmdlets][Azure Resource Cmdlets].</span></span>

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a><span data-ttu-id="4a604-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4a604-129">Next steps</span></span>
* <span data-ttu-id="4a604-130">toolearn ulteriori informazioni sull'assegnazione di tag delle risorse di Azure, vedere [Panoramica di gestione risorse di Azure] [ Azure Resource Manager Overview] e [tooorganize tag usando le risorse di Azure] [ Using Tags tooorganize your Azure Resources].</span><span class="sxs-lookup"><span data-stu-id="4a604-130">toolearn more about tagging your Azure resources, see [Azure Resource Manager Overview][Azure Resource Manager Overview] and [Using Tags tooorganize your Azure Resources][Using Tags tooorganize your Azure Resources].</span></span>
* <span data-ttu-id="4a604-131">toosee come tag consentono di gestire l'utilizzo delle risorse di Azure, vedere [comprendere la fattura di Azure] [ Understanding your Azure Bill] e [ottenere informazioni approfondite del consumo di risorse di Microsoft Azure] [Gain insights into your Microsoft Azure resource consumption].</span><span class="sxs-lookup"><span data-stu-id="4a604-131">toosee how tags can help you manage your use of Azure resources, see [Understanding your Azure Bill][Understanding your Azure Bill] and [Gain insights into your Microsoft Azure resource consumption][Gain insights into your Microsoft Azure resource consumption].</span></span>

[PowerShell environment with Azure Resource Manager]: ../../azure-resource-manager/powershell-azure-resource-manager.md
[Azure Resource Cmdlets]: https://msdn.microsoft.com/library/azure/dn757692.aspx
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags tooorganize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
