---
title: "Gestire VM in un set di scalabilità di macchine virtuali | Microsoft Docs"
description: "Gestire le macchine virtuali in un set di scalabilità di macchine virtuali tramite Azure PowerShell."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d35fa77a-de96-4ccd-a332-eb181d1f4273
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: adegeo
ms.openlocfilehash: d09a020b903e5f43afe03b86c675bcc1eb536cbc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="manage-virtual-machines-in-a-virtual-machine-scale-set"></a><span data-ttu-id="12ce4-103">Gestire le macchine virtuali in un set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="12ce4-103">Manage virtual machines in a virtual machine scale set</span></span>
<span data-ttu-id="12ce4-104">Usare le attività descritte in questo articolo per gestire le macchine virtuali nel set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="12ce4-104">Use the tasks in this article to manage virtual machines in your virtual machine scale set.</span></span>

<span data-ttu-id="12ce4-105">La maggior parte delle attività che implicano la gestione di una macchina virtuale in un set di scalabilità richiede di conoscere l'ID dell'istanza della macchina virtuale che si vuole gestire.</span><span class="sxs-lookup"><span data-stu-id="12ce4-105">Most of the tasks that involve managing a virtual machine in a scale set require that you know the instance ID of the machine that you want to manage.</span></span> <span data-ttu-id="12ce4-106">È possibile usare [Esplora risorse di Azure](https://resources.azure.com) per trovare l'ID dell'istanza di una macchina virtuale in un set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="12ce4-106">You can use [Azure Resource Explorer](https://resources.azure.com) to find the instance ID of a virtual machine in a scale set.</span></span> <span data-ttu-id="12ce4-107">È anche possibile usare Esplora risorse per verificare lo stato delle attività da completare.</span><span class="sxs-lookup"><span data-stu-id="12ce4-107">You also use Resource Explorer to verify the status of the tasks that you finish.</span></span>

<span data-ttu-id="12ce4-108">Per informazioni su come installare la versione più recente di Azure PowerShell, selezionare la sottoscrizione e accedere all'account, vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="12ce4-108">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for information about installing the latest version of Azure PowerShell, selecting your subscription, and signing in to your account.</span></span>

## <a name="display-information-about-a-scale-set"></a><span data-ttu-id="12ce4-109">Visualizzare informazioni relative a un set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="12ce4-109">Display information about a scale set</span></span>
<span data-ttu-id="12ce4-110">È possibile ottenere informazioni generali su un set di scalabilità, ovvero una visualizzazione delle istanze.</span><span class="sxs-lookup"><span data-stu-id="12ce4-110">You can get general information about a scale set, which is also referred to as the instance view.</span></span> <span data-ttu-id="12ce4-111">In alternativa, è possibile ottenere informazioni più specifiche, ad esempio informazioni sulle risorse nel set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="12ce4-111">Or, you can get more specific information, such as information about the resources in the scale set.</span></span>

<span data-ttu-id="12ce4-112">Sostituire i valori tra virgolette con il nome del gruppo di risorse e il set di scalabilità, quindi eseguire il comando:</span><span class="sxs-lookup"><span data-stu-id="12ce4-112">Replace the quoted values with the name or your resource group and scale set and then run the command:</span></span>

    Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"

<span data-ttu-id="12ce4-113">Verrà visualizzata una schermata simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="12ce4-113">It returns something like this:</span></span>

    Id                                          : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/virtualMachineScaleSets/myvmss1
    Name                                        : myvmss1
    Type                                        : Microsoft.Compute/virtualMachineScaleSets
    Location                                    : centralus
    Sku                                         :
      Name                                      : Standard_A0
      Tier                                      : Standard
      Capacity                                  : 3
    UpgradePolicy                               :
      Mode                                      : Manual
    VirtualMachineProfile                       :
      OsProfile                                 :
        ComputerNamePrefix                      : vmss1
        AdminUsername                           : admin1
        WindowsConfiguration                    :
          ProvisionVMAgent                      : True
          EnableAutomaticUpdates                : True
    StorageProfile                              :
      ImageReference                            :
        Publisher                               : MicrosoftWindowsServer
        Offer                                   : WindowsServer
        Sku                                     : 2012-R2-Datacenter
        Version                                 : latest
      OsDisk                                    :
        Name                                    : vmssosdisk
        Caching                                 : ReadOnly
        CreateOption                            : FromImage
        VhdContainers[0]                        : https://astore.blob.core.windows.net/vmss
        VhdContainers[1]                        : https://gstore.blob.core.windows.net/vmss
        VhdContainers[2]                        : https://mstore.blob.core.windows.net/vmss
        VhdContainers[3]                        : https://sstore.blob.core.windows.net/vmss
        VhdContainers[4]                        : https://ystore.blob.core.windows.net/vmss
    NetworkProfile                              :
      NetworkInterfaceConfigurations[0]         :
        Name                                    : mync1
        Primary                                 : True
        IpConfigurations[0]                     :
          Name                                  : ip1
          Subnet                                :
            Id                                  : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Network/virtualNetworks/myvn1/subnets/mysn1
          LoadBalancerBackendAddressPools[0]    :
            Id                                  : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Network/loadBalancers/mylb1/backendAddressPools/bepool1
        LoadBalancerInboundNatPools[0]          :
            Id                                  : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Network/loadBalancers/mylb1/inboundNatPools/natpool1
    ExtensionProfile                            :
      Extensions[0]                             :
        Name                                    : Microsoft.Insights.VMDiagnosticsSettings
        Publisher                               : Microsoft.Azure.Diagnostics
        Type                                    : IaaSDiagnostics
        TypeHandlerVersion                      : 1.5
        AutoUpgradeMinorVersion                 : True
        Settings                                : {"xmlCfg":"...","storageAccount":"astore"}
    ProvisioningState                           : Succeeded

<span data-ttu-id="12ce4-114">Sostituire i valori tra virgolette con il nome del gruppo di risorse e il set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="12ce4-114">Replace the quoted values with the name of your resource group and scale set.</span></span> <span data-ttu-id="12ce4-115">Sostituire *#* con l'identificatore dell'istanza della macchina virtuale di cui si desidera ottenere informazioni, quindi eseguirlo:</span><span class="sxs-lookup"><span data-stu-id="12ce4-115">Replace *#* with the instance identifier of the virtual machine that you want to get information about and then run it:</span></span>

    Get-AzureRmVmssVM -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="12ce4-116">Verrà visualizzata una schermata simile a all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="12ce4-116">It returns something like this example:</span></span>

    Id                            : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/
                                    virtualMachineScaleSets/myvmss1/virtualMachines/0
    Name                          : myvmss1_0
    Type                          : Microsoft.Compute/virtualMachineScaleSets/virtualMachines
    Location                      : centralus
    InstanceId                    : 0
    Sku                           :
      Name                        : Standard_A0
      Tier                        : Standard
    LatestModelApplied            : True
    StorageProfile                :
      ImageReference              :
        Publisher                 : MicrosoftWindowsServer
        Offer                     : WindowsServer
        Sku                       : 2012-R2-Datacenter
        Version                   : 4.0.20160617
      OsDisk                      :
        OsType                    : Windows
        Name                      : vmssosdisk-os-0-e11cad52959b4b76a8d9f26c5190c4f8
        Vhd                       :
          Uri                     : https://astore.blob.core.windows.net/vmss/vmssosdisk-os-0-e11cad52959b4b76a8d9f26c5190c4f8.vhd
        Caching                   : ReadOnly
        CreateOption              : FromImage
    OsProfile                     :
      ComputerName                : myvmss1-0
      AdminUsername               : admin1
      WindowsConfiguration        :
        ProvisionVMAgent          : True
        EnableAutomaticUpdates    : True
    NetworkProfile                :
      NetworkInterfaces[0]        :
        Id                        : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/virtualMachineScaleSets/
                                    myvmss1/virtualMachines/0/networkInterfaces/mync1
    ProvisioningState             : Succeeded
    Resources[0]                  :
      Id                          : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/virtualMachines/
                                    myvmss1_0/extensions/Microsoft.Insights.VMDiagnosticsSettings
      Name                        : Microsoft.Insights.VMDiagnosticsSettings
      Type                        : Microsoft.Compute/virtualMachines/extensions
      Location                    : centralus
      Publisher                   : Microsoft.Azure.Diagnostics
      VirtualMachineExtensionType : IaaSDiagnostics
      TypeHandlerVersion          : 1.5
      AutoUpgradeMinorVersion     : True
      Settings                    : {"xmlCfg":"...","storageAccount":"astore"}
      ProvisioningState           : Succeeded

## <a name="start-a-virtual-machine-in-a-scale-set"></a><span data-ttu-id="12ce4-117">Avviare una macchina virtuale in un set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="12ce4-117">Start a virtual machine in a scale set</span></span>
<span data-ttu-id="12ce4-118">Sostituire i valori tra virgolette con il nome del gruppo di risorse e il set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="12ce4-118">Replace the quoted values with the name of your resource group and scale set.</span></span> <span data-ttu-id="12ce4-119">Sostituire *#* con l'identificatore della macchina virtuale che si desidera avviare, quindi eseguirlo:</span><span class="sxs-lookup"><span data-stu-id="12ce4-119">Replace *#* with the identifier of the virtual machine that you want to start and then run it:</span></span>

    Start-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="12ce4-120">In Esplora risorse è possibile vedere che lo stato dell'istanza è **running**:</span><span class="sxs-lookup"><span data-stu-id="12ce4-120">In Resource Explorer, we can see that the status of the instance is **running**:</span></span>

    "statuses": [
      {
        "code": "ProvisioningState/succeeded",
        "level": "Info",
        "displayStatus": "Provisioning succeeded",
        "time": "2016-03-15T02:10:08.0730839+00:00"
      },
      {
        "code": "PowerState/running",
        "level": "Info",
        "displayStatus": "VM running"
      }
    ]

<span data-ttu-id="12ce4-121">È possibile avviare tutte le macchine virtuali nel set di scalabilità senza usare il parametro - InstanceId.</span><span class="sxs-lookup"><span data-stu-id="12ce4-121">You can start all the virtual machines in the scale set by not using the -InstanceId parameter.</span></span>

## <a name="stop-a-virtual-machine-in-a-scale-set"></a><span data-ttu-id="12ce4-122">Arrestare una macchina virtuale in un set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="12ce4-122">Stop a virtual machine in a scale set</span></span>
<span data-ttu-id="12ce4-123">Sostituire i valori tra virgolette con il nome del gruppo di risorse e il set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="12ce4-123">Replace the quoted values with the name of your resource group and scale set.</span></span> <span data-ttu-id="12ce4-124">Sostituire *#* con l'identificatore della macchina virtuale che si desidera arrestare, quindi eseguirlo:</span><span class="sxs-lookup"><span data-stu-id="12ce4-124">Replace *#* with the identifier of the virtual machine that you want to stop and then run it:</span></span>

    Stop-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="12ce4-125">In Esplora risorse è possibile vedere che lo stato dell'istanza è **deallocated**:</span><span class="sxs-lookup"><span data-stu-id="12ce4-125">In Resource Explorer, we can see that the status of the instance is **deallocated**:</span></span>

    "statuses": [
      {
        "code": "ProvisioningState/succeeded",
        "level": "Info",
        "displayStatus": "Provisioning succeeded",
        "time": "2016-03-15T01:25:17.8792929+00:00"
      },
      {
        "code": "PowerState/deallocated",
        "level": "Info",
        "displayStatus": "VM deallocated"
      }
    ]

<span data-ttu-id="12ce4-126">Per arrestare una macchina virtuale e non deallocarla, usare il parametro -StayProvisioned.</span><span class="sxs-lookup"><span data-stu-id="12ce4-126">To stop a virtual machine and not deallocate it, use the -StayProvisioned parameter.</span></span> <span data-ttu-id="12ce4-127">È possibile arrestare tutte le macchine virtuali nel set senza usare il parametro - InstanceId.</span><span class="sxs-lookup"><span data-stu-id="12ce4-127">You can stop all the virtual machines in the set by not using the -InstanceId parameter.</span></span>

## <a name="restart-a-virtual-machine-in-a-scale-set"></a><span data-ttu-id="12ce4-128">Riavviare una macchina virtuale in un set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="12ce4-128">Restart a virtual machine in a scale set</span></span>
<span data-ttu-id="12ce4-129">Sostituire i valori tra virgolette con il nome del gruppo di risorse e il set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="12ce4-129">Replace the quoted values with the name of your resource group and the scale set.</span></span> <span data-ttu-id="12ce4-130">Sostituire *#* con l'identificatore della macchina virtuale che si desidera riavviare, quindi eseguirlo:</span><span class="sxs-lookup"><span data-stu-id="12ce4-130">Replace *#* with the identifier of the virtual machine that you want to restart and then run it:</span></span>

    Restart-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="12ce4-131">È possibile riavviare tutte le macchine virtuali nel set senza usare il parametro - InstanceId.</span><span class="sxs-lookup"><span data-stu-id="12ce4-131">You can restart all the virtual machines in the set by not using the -InstanceId parameter.</span></span>

## <a name="remove-a-virtual-machine-from-a-scale-set"></a><span data-ttu-id="12ce4-132">Rimuovere una macchina virtuale da un set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="12ce4-132">Remove a virtual machine from a scale set</span></span>
<span data-ttu-id="12ce4-133">Sostituire i valori tra virgolette con il nome del gruppo di risorse e il set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="12ce4-133">Replace the quoted values with the name of your resource group and the scale set.</span></span> <span data-ttu-id="12ce4-134">Sostituire *#* con l'identificatore della macchina virtuale che si desidera rimuovere, quindi eseguirlo:</span><span class="sxs-lookup"><span data-stu-id="12ce4-134">Replace *#* with the identifier of the virtual machine that you want to remove and then run it:</span></span>  

    Remove-AzureRmVmss -ResourceGroupName "resource group name" –VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="12ce4-135">Per rimuovere il set di scalabilità di macchine virtuali tutto in una volta, non usare il parametro - InstanceId.</span><span class="sxs-lookup"><span data-stu-id="12ce4-135">You can remove the virtual machine scale set all at once by not using the -InstanceId parameter.</span></span>

## <a name="change-the-capacity-of-a-scale-set"></a><span data-ttu-id="12ce4-136">Modificare la capacità di un set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="12ce4-136">Change the capacity of a scale set</span></span>
<span data-ttu-id="12ce4-137">È possibile aggiungere o rimuovere le macchine virtuali modificando la capacità del set.</span><span class="sxs-lookup"><span data-stu-id="12ce4-137">You can add or remove virtual machines by changing the capacity of the set.</span></span> <span data-ttu-id="12ce4-138">Ottenere il set di scalabilità che si desidera modificare, impostare il valore di capacità desiderato, quindi aggiornare il set di scalabilità con la nuova capacità.</span><span class="sxs-lookup"><span data-stu-id="12ce4-138">Get the scale set that you want to change, set the capacity to what you want it to be, and then update the scale set with the new capacity.</span></span> <span data-ttu-id="12ce4-139">Nei comandi riportati sotto, sostituire i valori tra virgolette con il nome del gruppo di risorse e il set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="12ce4-139">In these commands, replace the quoted values with the name of your resource group and the scale set.</span></span>

    $vmss = Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"
    $vmss.sku.capacity = 5
    Update-AzureRmVmss -ResourceGroupName "resource group name" -Name "scale set name" -VirtualMachineScaleSet $vmss 

<span data-ttu-id="12ce4-140">Se si rimuovono le macchine virtuali dal set di scalabilità, per prime verranno rimosse le macchine virtuali con gli ID più elevati.</span><span class="sxs-lookup"><span data-stu-id="12ce4-140">If you are removing virtual machines from the scale set, the virtual machines with the highest ids are removed first.</span></span>

