---
title: "macchine virtuali in un Set di scalabilità della macchina virtuale aaaManage | Documenti Microsoft"
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
ms.openlocfilehash: 7d848729c0fc708bd596b61feb528cf4bf4bafd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machines-in-a-virtual-machine-scale-set"></a><span data-ttu-id="acb33-103">Gestire le macchine virtuali in un set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="acb33-103">Manage virtual machines in a virtual machine scale set</span></span>
<span data-ttu-id="acb33-104">Usare le attività di hello in questo macchine virtuali di toomanage articolo nel set di scalabilità di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="acb33-104">Use hello tasks in this article toomanage virtual machines in your virtual machine scale set.</span></span>

<span data-ttu-id="acb33-105">La maggior parte delle attività hello che implicano la gestione di una macchina virtuale in un set di scalabilità è necessario conoscere hello ID di istanza di macchina hello che si desidera toomanage.</span><span class="sxs-lookup"><span data-stu-id="acb33-105">Most of hello tasks that involve managing a virtual machine in a scale set require that you know hello instance ID of hello machine that you want toomanage.</span></span> <span data-ttu-id="acb33-106">È possibile utilizzare [Esplora inventario risorse di Azure](https://resources.azure.com) toofind hello istanza ID di una macchina virtuale in un set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="acb33-106">You can use [Azure Resource Explorer](https://resources.azure.com) toofind hello instance ID of a virtual machine in a scale set.</span></span> <span data-ttu-id="acb33-107">È anche possibile usare Esplora inventario risorse tooverify hello stato attività hello da completare.</span><span class="sxs-lookup"><span data-stu-id="acb33-107">You also use Resource Explorer tooverify hello status of hello tasks that you finish.</span></span>

<span data-ttu-id="acb33-108">Vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) per informazioni sull'installazione hello la versione più recente di Azure PowerShell, selezionando la sottoscrizione e la firma nell'account tooyour.</span><span class="sxs-lookup"><span data-stu-id="acb33-108">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for information about installing hello latest version of Azure PowerShell, selecting your subscription, and signing in tooyour account.</span></span>

## <a name="display-information-about-a-scale-set"></a><span data-ttu-id="acb33-109">Visualizzare informazioni relative a un set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="acb33-109">Display information about a scale set</span></span>
<span data-ttu-id="acb33-110">È possibile ottenere informazioni generali su un set di scalabilità, è anche la visualizzazione dell'istanza hello tooas cui viene fatto riferimento.</span><span class="sxs-lookup"><span data-stu-id="acb33-110">You can get general information about a scale set, which is also referred tooas hello instance view.</span></span> <span data-ttu-id="acb33-111">In alternativa, è possibile ottenere informazioni più specifiche, ad esempio informazioni sulle risorse hello in set di scalabilità hello.</span><span class="sxs-lookup"><span data-stu-id="acb33-111">Or, you can get more specific information, such as information about hello resources in hello scale set.</span></span>

<span data-ttu-id="acb33-112">Sostituire hello racchiuso tra virgolette i valori con nome hello o il gruppo di risorse e scala, impostare e quindi eseguire il comando hello:</span><span class="sxs-lookup"><span data-stu-id="acb33-112">Replace hello quoted values with hello name or your resource group and scale set and then run hello command:</span></span>

    Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"

<span data-ttu-id="acb33-113">Verrà visualizzata una schermata simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="acb33-113">It returns something like this:</span></span>

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

<span data-ttu-id="acb33-114">Sostituire hello racchiuso tra virgolette i valori con nome hello del set di risorse gruppo e la scala.</span><span class="sxs-lookup"><span data-stu-id="acb33-114">Replace hello quoted values with hello name of your resource group and scale set.</span></span> <span data-ttu-id="acb33-115">Sostituire  *#*  con identificatore hello dell'istanza di macchina virtuale di hello che si desiderano tooget informazioni e quindi eseguirlo:</span><span class="sxs-lookup"><span data-stu-id="acb33-115">Replace *#* with hello instance identifier of hello virtual machine that you want tooget information about and then run it:</span></span>

    Get-AzureRmVmssVM -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="acb33-116">Verrà visualizzata una schermata simile a all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="acb33-116">It returns something like this example:</span></span>

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

## <a name="start-a-virtual-machine-in-a-scale-set"></a><span data-ttu-id="acb33-117">Avviare una macchina virtuale in un set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="acb33-117">Start a virtual machine in a scale set</span></span>
<span data-ttu-id="acb33-118">Sostituire hello racchiuso tra virgolette i valori con nome hello del set di risorse gruppo e la scala.</span><span class="sxs-lookup"><span data-stu-id="acb33-118">Replace hello quoted values with hello name of your resource group and scale set.</span></span> <span data-ttu-id="acb33-119">Sostituire  *#*  con identificatore hello della macchina virtuale di hello toostart desiderati e quindi eseguirlo:</span><span class="sxs-lookup"><span data-stu-id="acb33-119">Replace *#* with hello identifier of hello virtual machine that you want toostart and then run it:</span></span>

    Start-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="acb33-120">In Esplora inventario risorse, possiamo vedere che è stato hello dell'istanza di hello **esecuzione**:</span><span class="sxs-lookup"><span data-stu-id="acb33-120">In Resource Explorer, we can see that hello status of hello instance is **running**:</span></span>

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

<span data-ttu-id="acb33-121">È possibile avviare tutte le macchine virtuali hello in scala di hello impostata se non si utilizza il parametro - InstanceId hello.</span><span class="sxs-lookup"><span data-stu-id="acb33-121">You can start all hello virtual machines in hello scale set by not using hello -InstanceId parameter.</span></span>

## <a name="stop-a-virtual-machine-in-a-scale-set"></a><span data-ttu-id="acb33-122">Arrestare una macchina virtuale in un set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="acb33-122">Stop a virtual machine in a scale set</span></span>
<span data-ttu-id="acb33-123">Sostituire hello racchiuso tra virgolette i valori con nome hello del set di risorse gruppo e la scala.</span><span class="sxs-lookup"><span data-stu-id="acb33-123">Replace hello quoted values with hello name of your resource group and scale set.</span></span> <span data-ttu-id="acb33-124">Sostituire  *#*  con identificatore hello della macchina virtuale di hello toostop desiderati e quindi eseguirlo:</span><span class="sxs-lookup"><span data-stu-id="acb33-124">Replace *#* with hello identifier of hello virtual machine that you want toostop and then run it:</span></span>

    Stop-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="acb33-125">In Esplora inventario risorse, possiamo vedere che è stato hello dell'istanza di hello **deallocato**:</span><span class="sxs-lookup"><span data-stu-id="acb33-125">In Resource Explorer, we can see that hello status of hello instance is **deallocated**:</span></span>

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

<span data-ttu-id="acb33-126">toostop una macchina virtuale e non deallocarlo, usare il parametro - StayProvisioned hello.</span><span class="sxs-lookup"><span data-stu-id="acb33-126">toostop a virtual machine and not deallocate it, use hello -StayProvisioned parameter.</span></span> <span data-ttu-id="acb33-127">È possibile arrestare tutte le macchine virtuali hello in un'impostazione non si utilizza il parametro - InstanceId hello hello.</span><span class="sxs-lookup"><span data-stu-id="acb33-127">You can stop all hello virtual machines in hello set by not using hello -InstanceId parameter.</span></span>

## <a name="restart-a-virtual-machine-in-a-scale-set"></a><span data-ttu-id="acb33-128">Riavviare una macchina virtuale in un set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="acb33-128">Restart a virtual machine in a scale set</span></span>
<span data-ttu-id="acb33-129">Sostituire hello racchiuso tra virgolette i valori con nome hello del set di scalabilità hello e di gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="acb33-129">Replace hello quoted values with hello name of your resource group and hello scale set.</span></span> <span data-ttu-id="acb33-130">Sostituire  *#*  con identificatore hello della macchina virtuale di hello toorestart desiderati e quindi eseguirlo:</span><span class="sxs-lookup"><span data-stu-id="acb33-130">Replace *#* with hello identifier of hello virtual machine that you want toorestart and then run it:</span></span>

    Restart-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="acb33-131">È possibile riavviare tutte le macchine virtuali hello in un'impostazione non si utilizza il parametro - InstanceId hello hello.</span><span class="sxs-lookup"><span data-stu-id="acb33-131">You can restart all hello virtual machines in hello set by not using hello -InstanceId parameter.</span></span>

## <a name="remove-a-virtual-machine-from-a-scale-set"></a><span data-ttu-id="acb33-132">Rimuovere una macchina virtuale da un set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="acb33-132">Remove a virtual machine from a scale set</span></span>
<span data-ttu-id="acb33-133">Sostituire hello racchiuso tra virgolette i valori con nome hello del set di scalabilità hello e di gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="acb33-133">Replace hello quoted values with hello name of your resource group and hello scale set.</span></span> <span data-ttu-id="acb33-134">Sostituire  *#*  con identificatore hello della macchina virtuale di hello tooremove desiderati e quindi eseguirlo:</span><span class="sxs-lookup"><span data-stu-id="acb33-134">Replace *#* with hello identifier of hello virtual machine that you want tooremove and then run it:</span></span>  

    Remove-AzureRmVmss -ResourceGroupName "resource group name" –VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="acb33-135">È possibile rimuovere contemporaneamente tutti i set di scalabilità macchina virtuale hello non si usa il parametro - InstanceId hello.</span><span class="sxs-lookup"><span data-stu-id="acb33-135">You can remove hello virtual machine scale set all at once by not using hello -InstanceId parameter.</span></span>

## <a name="change-hello-capacity-of-a-scale-set"></a><span data-ttu-id="acb33-136">Capacità di hello modifica di un set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="acb33-136">Change hello capacity of a scale set</span></span>
<span data-ttu-id="acb33-137">È possibile aggiungere o rimuovere le macchine virtuali modificando la capacità di hello del set di hello.</span><span class="sxs-lookup"><span data-stu-id="acb33-137">You can add or remove virtual machines by changing hello capacity of hello set.</span></span> <span data-ttu-id="acb33-138">Ottiene il set di scalabilità hello che si desidera toochange, set hello capacità toowhat desiderato toobe e quindi aggiornare il set di scalabilità di hello con nuova capacità di hello.</span><span class="sxs-lookup"><span data-stu-id="acb33-138">Get hello scale set that you want toochange, set hello capacity toowhat you want it toobe, and then update hello scale set with hello new capacity.</span></span> <span data-ttu-id="acb33-139">In questi comandi, sostituire hello racchiuso tra virgolette i valori con nome hello del set di scalabilità hello e di gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="acb33-139">In these commands, replace hello quoted values with hello name of your resource group and hello scale set.</span></span>

    $vmss = Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"
    $vmss.sku.capacity = 5
    Update-AzureRmVmss -ResourceGroupName "resource group name" -Name "scale set name" -VirtualMachineScaleSet $vmss 

<span data-ttu-id="acb33-140">Se si desidera rimuovere le macchine virtuali dal set di scalabilità di hello, hello le macchine virtuali con ID più alto hello verranno rimosse per prime.</span><span class="sxs-lookup"><span data-stu-id="acb33-140">If you are removing virtual machines from hello scale set, hello virtual machines with hello highest ids are removed first.</span></span>

