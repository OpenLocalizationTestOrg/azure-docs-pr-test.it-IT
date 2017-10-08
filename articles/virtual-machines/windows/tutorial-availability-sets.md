---
title: aaaAvailability imposta esercitazione per le macchine virtuali Windows in Azure | Documenti Microsoft
description: "Informazioni su hello disponibilità set per le macchine virtuali Windows in Azure."
documentationcenter: 
services: virtual-machines-windows
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 853775c5f126dd815c1933f9d71d2274a75ea661
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-availability-sets"></a>Il set di disponibilità di toouse

In questa esercitazione si apprenderà come tooincrease hello disponibilità e affidabilità delle soluzioni di macchina virtuale in Azure mediante una funzionalità denominata set di disponibilità. Set di disponibilità garantiscono che hello macchine virtuali di distribuire in Azure vengono distribuite tra più cluster hardware isolato. Questa operazione assicura che se si verifica un errore hardware o software all'interno di Azure, solo un sottoinsieme di macchine virtuali che verrà interessato e che la soluzione complessiva rimangono disponibili e operative dal punto di vista hello dei clienti di utilizzarlo. 

In questa esercitazione si apprenderà come:

> [!div class="checklist"]
> * Creare un set di disponibilità
> * Creare una macchina virtuale in un set di disponibilità
> * Controllare le dimensioni delle macchine virtuali disponibili

Questa esercitazione richiede hello Azure PowerShell versione 3.6 o versioni successive del modulo. Eseguire ` Get-Module -ListAvailable AzureRM` versione hello toofind. Se è necessario tooupgrade, vedere [modulo installare Azure PowerShell](/powershell/azure/install-azurerm-ps).

## <a name="availability-set-overview"></a>Informazioni generali sui set di disponibilità

Un Set di disponibilità è una raggruppamento logico di funzionalità che è possibile utilizzare in Azure tooensure che le risorse VM hello posizionate all'interno di essa sono isolate tra loro quando vengono distribuiti all'interno di un Data Center Azure. Azure garantisce che le macchine virtuali posizionate all'interno di un Set di disponibilità esegue tra più server fisici hello, calcolo rack, unità di archiviazione e commutatori di rete. Ciò garantisce che nell'evento hello di un errore hardware o software di Azure, solo un subset delle macchine virtuali sarà interessato e in generale l'applicazione rimanere e continuare toobe tooyour disponibili clienti. Utilizzo di set di disponibilità è un tooleverage funzionalità essenziali quando si desidera che le soluzioni di cloud affidabile toobuild.

Si consideri una soluzione tipica basata su macchine virtuali, in cui si dispone di 4 server Web front-end e vengono usate 2 macchine virtuali di back-end che ospitano un database. Con Azure, si toodefine due set di disponibilità prima di distribuire le macchine virtuali: set di disponibilità di uno per il livello di "web" hello e un set di disponibilità per il livello di "database" hello. Quando si crea una nuova macchina virtuale, è possibile specificare la disponibilità di hello imposta come comando di creazione di una macchina virtuale az toohello di parametro e di Azure automaticamente verificare che le macchine virtuali create all'interno di hello disponibile hello set vengono isolati in più risorse hardware fisiche. Ciò significa che se si è verificato un problema hardware fisico hello in esecuzione in uno dei Server Web o macchine virtuali del Server di Database, si conosce tale hello altre istanze del Server Web e macchine virtuali del Database rimarrà in esecuzione correttamente perché sono in un hardware diverso.

Quando si desidera toodeploy affidabili soluzioni di macchina virtuale in base all'interno di Azure, è necessario utilizzare sempre i set di disponibilità.

## <a name="create-an-availability-set"></a>Creare un set di disponibilità

È possibile creare un set di disponibilità con il comando [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset). In questo esempio, è impostato sia il numero di domini di aggiornamento e di errore hello *2* per la disponibilità di hello set denominata *myAvailabilitySet* in hello *myResourceGroupAvailability*gruppo di risorse.

Creare un gruppo di risorse.

```powershell
New-AzureRmResourceGroup -Name myResourceGroupAvailability -Location EastUS
```


```powershell
New-AzureRmAvailabilitySet `
   -Location EastUS `
   -Name myAvailabilitySet `
   -ResourceGroupName myResourceGroupAvailability `
   -Managed `
   -PlatformFaultDomainCount 2 `
   -PlatformUpdateDomainCount 2
```

## <a name="create-vms-inside-an-availability-set"></a>Creare macchine virtuali in un set di disponibilità

Macchine virtuali devono toobe creati all'interno di hello toomake set di disponibilità che vengono distribuite correttamente su hardware hello. È possibile aggiungere un gruppo di disponibilità tooan VM impostato dopo la sua creazione. 

hardware Hello in un percorso è suddiviso in domini di aggiornamento toomultiple e domini di errore. Un **dominio di aggiornamento** è un gruppo di macchine virtuali e l'hardware fisico sottostante che può essere riavviata in hello contemporaneamente. Macchine virtuali in hello stesso **dominio di errore** condividere archiviazione comune, nonché un commutatore power di origine e di rete comune. 

Quando si crea una macchina virtuale utilizzando configurazione [New AzureRMVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) specificare hello set di disponibilità usando hello `-AvailabilitySetId` parametro toospecify hello ID hello del set di disponibilità.

Creare 2 macchine virtuali con [New AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) nel set di disponibilità hello.

```powershell
$availabilitySet = Get-AzureRmAvailabilitySet `
    -ResourceGroupName myResourceGroupAvailability `
    -Name myAvailabilitySet

$cred = Get-Credential -Message "Enter a username and password for hello virtual machine."

$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupAvailability `
    -Location EastUS `
    -Name MYvNET `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

for ($i=1; $i -le 2; $i++)
{
   $pip = New-AzureRmPublicIpAddress `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -Name "mypublicdns$(Get-Random)" `
        -AllocationMethod Static `
        -IdleTimeoutInMinutes 4

   $nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
        -Name myNetworkSecurityGroupRuleRDP$i `
        -Protocol Tcp `
        -Direction Inbound `
        -Priority 1000 `
        -SourceAddressPrefix * `
        -SourcePortRange * `
        -DestinationAddressPrefix * `
        -DestinationPortRange 3389 `
        -Access Allow

   $nsg = New-AzureRmNetworkSecurityGroup `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -Name myNetworkSecurityGroup$i `
        -SecurityRules $nsgRuleRDP

   $nic = New-AzureRmNetworkInterface `
        -Name myNic$i `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -SubnetId $vnet.Subnets[0].Id `
        -PublicIpAddressId $pip.Id `
        -NetworkSecurityGroupId $nsg.Id

   # Here is where we specify hello availability set
   $vm = New-AzureRmVMConfig `
        -VMName myVM$i `
        -VMSize Standard_D1 `
        -AvailabilitySetId $availabilitySet.Id

   $vm = Set-AzureRmVMOperatingSystem `
        -VM $vm `
        -Windows -ComputerName myVM$i `   
        -Credential $cred `
        -ProvisionVMAgent `
        -EnableAutoUpdate
   $vm = Set-AzureRmVMSourceImage `
        -VM $vm `
        -PublisherName MicrosoftWindowsServer `
        -Offer WindowsServer `
        -Skus 2016-Datacenter `
        -Version latest
   $vm = Set-AzureRmVMOSDisk `
        -VM $vm `
        -Name myOsDisk$i `
        -DiskSizeInGB 128 `
        -CreateOption FromImage `
        -Caching ReadWrite
   $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
   New-AzureRmVM `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -VM $vm
}

```

Accetta toocreate di pochi minuti e configurare entrambe le macchine virtuali. Al termine, si avrà 2 macchine virtuali distribuite tra hello hardware sottostante. 

## <a name="check-for-available-vm-sizes"></a>Controllare le dimensioni delle macchine virtuali disponibili 

È possibile aggiungere ulteriori disponibilità toohello di macchine virtuali in un momento successivo, ma è necessario tooknow le dimensioni delle macchine Virtuali sono disponibili su hardware hello. Utilizzare [Get AzureRMVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) toolist tutte le dimensioni disponibili hello hardware hello del cluster per il set di disponibilità hello.

```powershell
Get-AzureRmVMSize `
   -AvailabilitySetName myAvailabilitySet `
   -ResourceGroupName myResourceGroupAvailability  
```

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione si è appreso come:

> [!div class="checklist"]
> * Creare un set di disponibilità
> * Creare una macchina virtuale in un set di disponibilità
> * Controllare le dimensioni delle macchine virtuali disponibili

Spostare toohello toolearn esercitazione successiva sui set di scalabilità di macchine virtuali.

> [!div class="nextstepaction"]
> [Creare un set di scalabilità di macchine virtuali](tutorial-create-vmss.md)


