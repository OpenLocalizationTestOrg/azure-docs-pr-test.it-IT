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
# <a name="move-a-linux-vm-tooanother-subscription-or-resource-group"></a><span data-ttu-id="71b40-103">Spostare un gruppo di sottoscrizione o la risorsa tooanother VM Linux</span><span class="sxs-lookup"><span data-stu-id="71b40-103">Move a Linux VM tooanother subscription or resource group</span></span>
<span data-ttu-id="71b40-104">In questo articolo viene descritta la procedura toomove una VM Linux tra gruppi di risorse o le sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="71b40-104">This article walks you through how toomove a Linux VM between resource groups or subscriptions.</span></span> <span data-ttu-id="71b40-105">Lo spostamento tra le sottoscrizioni di una macchina virtuale può essere utile se si crea una macchina virtuale in una sottoscrizione personale e si decide toomove è tooyour sottoscrizione aziendale.</span><span class="sxs-lookup"><span data-stu-id="71b40-105">Moving a VM between subscriptions can be handy if you created a VM in a personal subscription and now want toomove it tooyour company's subscription.</span></span>

> [!IMPORTANT]
><span data-ttu-id="71b40-106">Non è possibile spostare Managed Disks in questa fase.</span><span class="sxs-lookup"><span data-stu-id="71b40-106">You cannot move Managed Disks at this time.</span></span> 
>
><span data-ttu-id="71b40-107">Nuovi ID di risorsa vengono creati come parte di spostamento hello.</span><span class="sxs-lookup"><span data-stu-id="71b40-107">New resource IDs are created as part of hello move.</span></span> <span data-ttu-id="71b40-108">Una volta hello VM è stato spostato, è necessario tooupdate lo strumenti e script toouse hello nuovi ID di risorsa.</span><span class="sxs-lookup"><span data-stu-id="71b40-108">Once hello VM has been moved, you need tooupdate your tools and scripts toouse hello new resource IDs.</span></span> 
> 
> 

## <a name="use-hello-azure-cli-toomove-a-vm"></a><span data-ttu-id="71b40-109">Utilizzare hello Azure CLI toomove una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="71b40-109">Use hello Azure CLI toomove a VM</span></span>
<span data-ttu-id="71b40-110">toosuccessfully spostare una macchina virtuale, è necessario toomove hello VM e tutte le risorse di supporto.</span><span class="sxs-lookup"><span data-stu-id="71b40-110">toosuccessfully move a VM, you need toomove hello VM and all its supporting resources.</span></span> <span data-ttu-id="71b40-111">Hello utilizzare **Mostra gruppo azure** comando toolist tutte le risorse di hello in un gruppo di risorse e i relativi ID.</span><span class="sxs-lookup"><span data-stu-id="71b40-111">Use hello **azure group show** command toolist all hello resources in a resource group and their IDs.</span></span> <span data-ttu-id="71b40-112">Output di hello toopipe di questo file di comando tooa è utile in modo è possibile copiare e incollare hello ID comandi successive.</span><span class="sxs-lookup"><span data-stu-id="71b40-112">It helps toopipe hello output of this command tooa file so you can copy and paste hello IDs into later commands.</span></span>

    azure group show <resourceGroupName>

<span data-ttu-id="71b40-113">toomove una macchina virtuale e il relativo gruppo di risorse tooanother di risorse, utilizzare hello **dello spostamento delle risorse azure** comando CLI.</span><span class="sxs-lookup"><span data-stu-id="71b40-113">toomove a VM and its resources tooanother resource group, use hello **azure resource move** CLI command.</span></span> <span data-ttu-id="71b40-114">Hello di esempio seguente viene illustrato come toomove una macchina virtuale e le risorse più comuni di hello richiede.</span><span class="sxs-lookup"><span data-stu-id="71b40-114">hello following example shows how toomove a VM and hello most common resources it requires.</span></span> <span data-ttu-id="71b40-115">Utilizziamo hello **-i** parametro e passare un elenco delimitato da virgole (senza spazi) di ID per toomove risorse hello.</span><span class="sxs-lookup"><span data-stu-id="71b40-115">We use hello **-i** parameter and pass in a comma-separated list (without spaces) of IDs for hello resources toomove.</span></span>

    vm=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Compute/virtualMachines/<vmName>
    nic=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/networkInterfaces/<nicName>
    nsg=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/networkSecurityGroups/<nsgName>
    pip=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/publicIPAddresses/<publicIPName>
    vnet=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/virtualNetworks/<vnetName>
    diag=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Storage/storageAccounts/<diagnosticStorageAccountName>
    storage=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Storage/storageAccounts/<storageAcountName>      

    azure resource move --ids $vm,$nic,$nsg,$pip,$vnet,$storage,$diag -d "<destinationResourceGroup>"

<span data-ttu-id="71b40-116">Se si desidera toomove hello macchina virtuale e la sottoscrizione di risorse tooa diverso, aggiungere hello **-destinazione subscriptionId &#60; destinationSubscriptionID &#62;** sottoscrizione di destinazione parametro toospecify hello.</span><span class="sxs-lookup"><span data-stu-id="71b40-116">If you want toomove hello VM and its resources tooa different subscription, add hello **--destination-subscriptionId &#60;destinationSubscriptionID&#62;** parameter toospecify hello destination subscription.</span></span>

<span data-ttu-id="71b40-117">Se si sta utilizzando hello prompt dei comandi in un computer Windows, è necessario tooadd un  **$**  davanti hello i nomi delle variabili quando queste vengono dichiarate.</span><span class="sxs-lookup"><span data-stu-id="71b40-117">If you are working from hello Command Prompt on a Windows computer, you need tooadd a **$** in front of hello variable names when you declare them.</span></span> <span data-ttu-id="71b40-118">Questo prefisso non è necessario in Linux.</span><span class="sxs-lookup"><span data-stu-id="71b40-118">This isn't needed in Linux.</span></span>

<span data-ttu-id="71b40-119">Viene richiesto che si desidera toomove hello tooconfirm risorsa specificata.</span><span class="sxs-lookup"><span data-stu-id="71b40-119">You are asked tooconfirm that you want toomove hello specified resource.</span></span> <span data-ttu-id="71b40-120">Tipo **Y** tooconfirm che si desidera risorse hello toomove.</span><span class="sxs-lookup"><span data-stu-id="71b40-120">Type **Y** tooconfirm that you want toomove hello resources.</span></span>

[!INCLUDE [virtual-machines-common-move-vm](../../../includes/virtual-machines-common-move-vm.md)]

## <a name="next-steps"></a><span data-ttu-id="71b40-121">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="71b40-121">Next steps</span></span>
<span data-ttu-id="71b40-122">È possibile spostare molti tipi diversi di risorse tra gruppi di risorse e sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="71b40-122">You can move many different types of resources between resource groups and subscriptions.</span></span> <span data-ttu-id="71b40-123">Per ulteriori informazioni, vedere [spostare sottoscrizione o il gruppo di risorse toonew risorse](../../resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="71b40-123">For more information, see [Move resources toonew resource group or subscription](../../resource-group-move-resources.md).</span></span>    

