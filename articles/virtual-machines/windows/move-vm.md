---
title: una risorsa di macchina virtuale Windows Azure aaaMove | Documenti Microsoft
description: Spostare una macchina virtuale Windows tooanother sottoscrizione di Azure o un gruppo di risorse nel modello di distribuzione di gestione risorse di hello.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4e383427-4aff-4bf3-a0f4-dbff5c6f0c81
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 859e78dce9acf1168780d4ee8e9f6dac0e3c11cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-windows-vm-tooanother-azure-subscription-or-resource-group"></a><span data-ttu-id="8c4c2-103">Spostare una macchina virtuale Windows tooanother sottoscrizione di Azure o un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="8c4c2-103">Move a Windows VM tooanother Azure subscription or resource group</span></span>
<span data-ttu-id="8c4c2-104">In questo articolo viene descritta la procedura toomove una macchina virtuale Windows tra gruppi di risorse o le sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="8c4c2-104">This article walks you through how toomove a Windows VM between resource groups or subscriptions.</span></span> <span data-ttu-id="8c4c2-105">Lo spostamento tra sottoscrizioni può essere utile se è stato originariamente creato una macchina virtuale in una sottoscrizione personale e si decide toomove è toocontinue sottoscrizione della società tooyour il lavoro.</span><span class="sxs-lookup"><span data-stu-id="8c4c2-105">Moving between subscriptions can be handy if you originally created a VM in a personal subscription and now want toomove it tooyour company's subscription toocontinue your work.</span></span>

> [!IMPORTANT]
><span data-ttu-id="8c4c2-106">Non è possibile spostare Managed Disks in questa fase.</span><span class="sxs-lookup"><span data-stu-id="8c4c2-106">You cannot move Managed Disks at this time.</span></span> 
>
><span data-ttu-id="8c4c2-107">Nuovi ID di risorsa vengono creati come parte di spostamento hello.</span><span class="sxs-lookup"><span data-stu-id="8c4c2-107">New resource IDs are created as part of hello move.</span></span> <span data-ttu-id="8c4c2-108">Una volta hello VM è stato spostato, è necessario tooupdate lo strumenti e script toouse hello nuovi ID di risorsa.</span><span class="sxs-lookup"><span data-stu-id="8c4c2-108">Once hello VM has been moved, you need tooupdate your tools and scripts toouse hello new resource IDs.</span></span> 
> 
> 

[!INCLUDE [virtual-machines-common-move-vm](../../../includes/virtual-machines-common-move-vm.md)]

## <a name="use-powershell-toomove-a-vm"></a><span data-ttu-id="8c4c2-109">Utilizzare Powershell toomove una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="8c4c2-109">Use Powershell toomove a VM</span></span>
<span data-ttu-id="8c4c2-110">toomove un gruppo di risorse tooanother macchina virtuale, è necessario assicurarsi di spostare anche tutte le risorse dipendenti hello toomake.</span><span class="sxs-lookup"><span data-stu-id="8c4c2-110">toomove a virtual machine tooanother resource group, you need toomake sure that you also move all of hello dependent resources.</span></span> <span data-ttu-id="8c4c2-111">cmdlet Move-AzureRMResource di hello toouse, è necessario che il nome di risorsa hello e il tipo di hello della risorsa.</span><span class="sxs-lookup"><span data-stu-id="8c4c2-111">toouse hello Move-AzureRMResource cmdlet, you need hello resource name and hello type of resource.</span></span> <span data-ttu-id="8c4c2-112">È possibile ottenere sia dal cmdlet Find-AzureRMResource hello.</span><span class="sxs-lookup"><span data-stu-id="8c4c2-112">You can get both from hello Find-AzureRMResource cmdlet.</span></span>

    Find-AzureRMResource -ResourceGroupNameContains "<sourceResourceGroupName>"


<span data-ttu-id="8c4c2-113">toomove una macchina virtuale è necessario toomove più risorse.</span><span class="sxs-lookup"><span data-stu-id="8c4c2-113">toomove a VM we need toomove multiple resources.</span></span> <span data-ttu-id="8c4c2-114">È sufficiente creare variabili separate per ogni risorsa e quindi elencarle.</span><span class="sxs-lookup"><span data-stu-id="8c4c2-114">We can just create separate variables for each resource and then list them.</span></span> <span data-ttu-id="8c4c2-115">Questo esempio è inclusa la maggior parte delle risorse di base hello per una macchina virtuale, ma è possibile aggiungere più in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="8c4c2-115">This example includes most of hello basic resources for a VM, but you can add more as needed.</span></span>

    $sourceRG = "<sourceResourceGroupName>"
    $destinationRG = "<destinationResourceGroupName>"

    $vm = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Compute/virtualMachines" -ResourceName "<vmName>"
    $storageAccount = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Storage/storageAccounts" -ResourceName "<storageAccountName>"
    $diagStorageAccount = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Storage/storageAccounts" -ResourceName "<diagnosticStorageAccountName>"
    $vNet = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/virtualNetworks" -ResourceName "<vNetName>"
    $nic = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/networkInterfaces" -ResourceName "<nicName>"
    $ip = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/publicIPAddresses" -ResourceName "<ipName>"
    $nsg = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/networkSecurityGroups" -ResourceName "<nsgName>"

    Move-AzureRmResource -DestinationResourceGroupName $destinationRG -ResourceId $vm.ResourceId, $storageAccount.ResourceId, $diagStorageAccount.ResourceId, $vNet.ResourceId, $nic.ResourceId, $ip.ResourceId, $nsg.ResourceId

<span data-ttu-id="8c4c2-116">toomove hello toodifferent la sottoscrizione alle risorse, includere hello **- DestinationSubscriptionId** parametro.</span><span class="sxs-lookup"><span data-stu-id="8c4c2-116">toomove hello resources toodifferent subscription, include hello **-DestinationSubscriptionId** parameter.</span></span> 

    Move-AzureRmResource -DestinationSubscriptionId "<destinationSubscriptionID>" -DestinationResourceGroupName $destinationRG -ResourceId $vm.ResourceId, $storageAccount.ResourceId, $diagStorageAccount.ResourceId, $vNet.ResourceId, $nic.ResourceId, $ip.ResourceId, $nsg.ResourceId



<span data-ttu-id="8c4c2-117">Verrà richiesto che si desidera hello toomove tooconfirm delle risorse specificate.</span><span class="sxs-lookup"><span data-stu-id="8c4c2-117">You will be asked tooconfirm that you want toomove hello specified resources.</span></span> <span data-ttu-id="8c4c2-118">Tipo **Y** tooconfirm che si desidera risorse hello toomove.</span><span class="sxs-lookup"><span data-stu-id="8c4c2-118">Type **Y** tooconfirm that you want toomove hello resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c4c2-119">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8c4c2-119">Next steps</span></span>
<span data-ttu-id="8c4c2-120">È possibile spostare molti tipi diversi di risorse tra gruppi di risorse e sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="8c4c2-120">You can move many different types of resources between resource groups and subscriptions.</span></span> <span data-ttu-id="8c4c2-121">Per ulteriori informazioni, vedere [spostare sottoscrizione o il gruppo di risorse toonew risorse](../../resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="8c4c2-121">For more information, see [Move resources toonew resource group or subscription](../../resource-group-move-resources.md).</span></span>    

