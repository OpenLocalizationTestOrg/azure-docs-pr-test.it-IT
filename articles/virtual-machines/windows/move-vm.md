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
# <a name="move-a-windows-vm-tooanother-azure-subscription-or-resource-group"></a>Spostare una macchina virtuale Windows tooanother sottoscrizione di Azure o un gruppo di risorse
In questo articolo viene descritta la procedura toomove una macchina virtuale Windows tra gruppi di risorse o le sottoscrizioni. Lo spostamento tra sottoscrizioni può essere utile se è stato originariamente creato una macchina virtuale in una sottoscrizione personale e si decide toomove è toocontinue sottoscrizione della società tooyour il lavoro.

> [!IMPORTANT]
>Non è possibile spostare Managed Disks in questa fase. 
>
>Nuovi ID di risorsa vengono creati come parte di spostamento hello. Una volta hello VM è stato spostato, è necessario tooupdate lo strumenti e script toouse hello nuovi ID di risorsa. 
> 
> 

[!INCLUDE [virtual-machines-common-move-vm](../../../includes/virtual-machines-common-move-vm.md)]

## <a name="use-powershell-toomove-a-vm"></a>Utilizzare Powershell toomove una macchina virtuale
toomove un gruppo di risorse tooanother macchina virtuale, è necessario assicurarsi di spostare anche tutte le risorse dipendenti hello toomake. cmdlet Move-AzureRMResource di hello toouse, è necessario che il nome di risorsa hello e il tipo di hello della risorsa. È possibile ottenere sia dal cmdlet Find-AzureRMResource hello.

    Find-AzureRMResource -ResourceGroupNameContains "<sourceResourceGroupName>"


toomove una macchina virtuale è necessario toomove più risorse. È sufficiente creare variabili separate per ogni risorsa e quindi elencarle. Questo esempio è inclusa la maggior parte delle risorse di base hello per una macchina virtuale, ma è possibile aggiungere più in base alle esigenze.

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

toomove hello toodifferent la sottoscrizione alle risorse, includere hello **- DestinationSubscriptionId** parametro. 

    Move-AzureRmResource -DestinationSubscriptionId "<destinationSubscriptionID>" -DestinationResourceGroupName $destinationRG -ResourceId $vm.ResourceId, $storageAccount.ResourceId, $diagStorageAccount.ResourceId, $vNet.ResourceId, $nic.ResourceId, $ip.ResourceId, $nsg.ResourceId



Verrà richiesto che si desidera hello toomove tooconfirm delle risorse specificate. Tipo **Y** tooconfirm che si desidera risorse hello toomove.

## <a name="next-steps"></a>Passaggi successivi
È possibile spostare molti tipi diversi di risorse tra gruppi di risorse e sottoscrizioni. Per ulteriori informazioni, vedere [spostare sottoscrizione o il gruppo di risorse toonew risorse](../../resource-group-move-resources.md).    

