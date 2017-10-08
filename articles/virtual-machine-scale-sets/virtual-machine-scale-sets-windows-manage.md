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
# <a name="manage-virtual-machines-in-a-virtual-machine-scale-set"></a>Gestire le macchine virtuali in un set di scalabilità di macchine virtuali
Usare le attività di hello in questo macchine virtuali di toomanage articolo nel set di scalabilità di macchine virtuali.

La maggior parte delle attività hello che implicano la gestione di una macchina virtuale in un set di scalabilità è necessario conoscere hello ID di istanza di macchina hello che si desidera toomanage. È possibile utilizzare [Esplora inventario risorse di Azure](https://resources.azure.com) toofind hello istanza ID di una macchina virtuale in un set di scalabilità. È anche possibile usare Esplora inventario risorse tooverify hello stato attività hello da completare.

Vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) per informazioni sull'installazione hello la versione più recente di Azure PowerShell, selezionando la sottoscrizione e la firma nell'account tooyour.

## <a name="display-information-about-a-scale-set"></a>Visualizzare informazioni relative a un set di scalabilità
È possibile ottenere informazioni generali su un set di scalabilità, è anche la visualizzazione dell'istanza hello tooas cui viene fatto riferimento. In alternativa, è possibile ottenere informazioni più specifiche, ad esempio informazioni sulle risorse hello in set di scalabilità hello.

Sostituire hello racchiuso tra virgolette i valori con nome hello o il gruppo di risorse e scala, impostare e quindi eseguire il comando hello:

    Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"

Verrà visualizzata una schermata simile alla seguente:

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

Sostituire hello racchiuso tra virgolette i valori con nome hello del set di risorse gruppo e la scala. Sostituire  *#*  con identificatore hello dell'istanza di macchina virtuale di hello che si desiderano tooget informazioni e quindi eseguirlo:

    Get-AzureRmVmssVM -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

Verrà visualizzata una schermata simile a all'esempio seguente:

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

## <a name="start-a-virtual-machine-in-a-scale-set"></a>Avviare una macchina virtuale in un set di scalabilità
Sostituire hello racchiuso tra virgolette i valori con nome hello del set di risorse gruppo e la scala. Sostituire  *#*  con identificatore hello della macchina virtuale di hello toostart desiderati e quindi eseguirlo:

    Start-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

In Esplora inventario risorse, possiamo vedere che è stato hello dell'istanza di hello **esecuzione**:

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

È possibile avviare tutte le macchine virtuali hello in scala di hello impostata se non si utilizza il parametro - InstanceId hello.

## <a name="stop-a-virtual-machine-in-a-scale-set"></a>Arrestare una macchina virtuale in un set di scalabilità
Sostituire hello racchiuso tra virgolette i valori con nome hello del set di risorse gruppo e la scala. Sostituire  *#*  con identificatore hello della macchina virtuale di hello toostop desiderati e quindi eseguirlo:

    Stop-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

In Esplora inventario risorse, possiamo vedere che è stato hello dell'istanza di hello **deallocato**:

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

toostop una macchina virtuale e non deallocarlo, usare il parametro - StayProvisioned hello. È possibile arrestare tutte le macchine virtuali hello in un'impostazione non si utilizza il parametro - InstanceId hello hello.

## <a name="restart-a-virtual-machine-in-a-scale-set"></a>Riavviare una macchina virtuale in un set di scalabilità
Sostituire hello racchiuso tra virgolette i valori con nome hello del set di scalabilità hello e di gruppo di risorse. Sostituire  *#*  con identificatore hello della macchina virtuale di hello toorestart desiderati e quindi eseguirlo:

    Restart-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

È possibile riavviare tutte le macchine virtuali hello in un'impostazione non si utilizza il parametro - InstanceId hello hello.

## <a name="remove-a-virtual-machine-from-a-scale-set"></a>Rimuovere una macchina virtuale da un set di scalabilità
Sostituire hello racchiuso tra virgolette i valori con nome hello del set di scalabilità hello e di gruppo di risorse. Sostituire  *#*  con identificatore hello della macchina virtuale di hello tooremove desiderati e quindi eseguirlo:  

    Remove-AzureRmVmss -ResourceGroupName "resource group name" –VMScaleSetName "scale set name" -InstanceId #

È possibile rimuovere contemporaneamente tutti i set di scalabilità macchina virtuale hello non si usa il parametro - InstanceId hello.

## <a name="change-hello-capacity-of-a-scale-set"></a>Capacità di hello modifica di un set di scalabilità
È possibile aggiungere o rimuovere le macchine virtuali modificando la capacità di hello del set di hello. Ottiene il set di scalabilità hello che si desidera toochange, set hello capacità toowhat desiderato toobe e quindi aggiornare il set di scalabilità di hello con nuova capacità di hello. In questi comandi, sostituire hello racchiuso tra virgolette i valori con nome hello del set di scalabilità hello e di gruppo di risorse.

    $vmss = Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"
    $vmss.sku.capacity = 5
    Update-AzureRmVmss -ResourceGroupName "resource group name" -Name "scale set name" -VirtualMachineScaleSet $vmss 

Se si desidera rimuovere le macchine virtuali dal set di scalabilità di hello, hello le macchine virtuali con ID più alto hello verranno rimosse per prime.

