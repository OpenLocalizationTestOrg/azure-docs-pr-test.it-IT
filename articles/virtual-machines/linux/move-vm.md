---
title: aaaMove una VM Linux di Azure | Documenti Microsoft
description: Spostare una VM Linux tooanother sottoscrizione di Azure o un gruppo di risorse nel modello di distribuzione di gestione risorse di hello.
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d635f0a5-4458-4b95-a5f8-eed4f41eb4d4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 938d04234059111912f03e72d14dabd338bc0678
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-linux-vm-tooanother-subscription-or-resource-group"></a>Spostare un gruppo di sottoscrizione o la risorsa tooanother VM Linux
In questo articolo viene descritta la procedura toomove una VM Linux tra gruppi di risorse o le sottoscrizioni. Lo spostamento tra le sottoscrizioni di una macchina virtuale può essere utile se si crea una macchina virtuale in una sottoscrizione personale e si decide toomove è tooyour sottoscrizione aziendale.

> [!IMPORTANT]
>Non è possibile spostare Managed Disks in questa fase. 
>
>Nuovi ID di risorsa vengono creati come parte di spostamento hello. Una volta hello VM è stato spostato, è necessario tooupdate lo strumenti e script toouse hello nuovi ID di risorsa. 
> 
> 

## <a name="use-hello-azure-cli-toomove-a-vm"></a>Utilizzare hello Azure CLI toomove una macchina virtuale
toosuccessfully spostare una macchina virtuale, è necessario toomove hello VM e tutte le risorse di supporto. Hello utilizzare **Mostra gruppo azure** comando toolist tutte le risorse di hello in un gruppo di risorse e i relativi ID. Output di hello toopipe di questo file di comando tooa è utile in modo è possibile copiare e incollare hello ID comandi successive.

    azure group show <resourceGroupName>

toomove una macchina virtuale e il relativo gruppo di risorse tooanother di risorse, utilizzare hello **dello spostamento delle risorse azure** comando CLI. Hello di esempio seguente viene illustrato come toomove una macchina virtuale e le risorse più comuni di hello richiede. Utilizziamo hello **-i** parametro e passare un elenco delimitato da virgole (senza spazi) di ID per toomove risorse hello.

    vm=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Compute/virtualMachines/<vmName>
    nic=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/networkInterfaces/<nicName>
    nsg=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/networkSecurityGroups/<nsgName>
    pip=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/publicIPAddresses/<publicIPName>
    vnet=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/virtualNetworks/<vnetName>
    diag=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Storage/storageAccounts/<diagnosticStorageAccountName>
    storage=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Storage/storageAccounts/<storageAcountName>      

    azure resource move --ids $vm,$nic,$nsg,$pip,$vnet,$storage,$diag -d "<destinationResourceGroup>"

Se si desidera toomove hello macchina virtuale e la sottoscrizione di risorse tooa diverso, aggiungere hello **-destinazione subscriptionId &#60; destinationSubscriptionID &#62;** sottoscrizione di destinazione parametro toospecify hello.

Se si sta utilizzando hello prompt dei comandi in un computer Windows, è necessario tooadd un  **$**  davanti hello i nomi delle variabili quando queste vengono dichiarate. Questo prefisso non è necessario in Linux.

Viene richiesto che si desidera toomove hello tooconfirm risorsa specificata. Tipo **Y** tooconfirm che si desidera risorse hello toomove.

[!INCLUDE [virtual-machines-common-move-vm](../../../includes/virtual-machines-common-move-vm.md)]

## <a name="next-steps"></a>Passaggi successivi
È possibile spostare molti tipi diversi di risorse tra gruppi di risorse e sottoscrizioni. Per ulteriori informazioni, vedere [spostare sottoscrizione o il gruppo di risorse toonew risorse](../../resource-group-move-resources.md).    

