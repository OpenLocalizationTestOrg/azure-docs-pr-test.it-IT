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
# <a name="how-toouse-availability-sets"></a><span data-ttu-id="207d1-103">Il set di disponibilità di toouse</span><span class="sxs-lookup"><span data-stu-id="207d1-103">How toouse availability sets</span></span>

<span data-ttu-id="207d1-104">In questa esercitazione si apprenderà come tooincrease hello disponibilità e affidabilità delle soluzioni di macchina virtuale in Azure mediante una funzionalità denominata set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="207d1-104">In this tutorial, you will learn how tooincrease hello availability and reliability of your Virtual Machine solutions on Azure using a capability called Availability Sets.</span></span> <span data-ttu-id="207d1-105">Set di disponibilità garantiscono che hello macchine virtuali di distribuire in Azure vengono distribuite tra più cluster hardware isolato.</span><span class="sxs-lookup"><span data-stu-id="207d1-105">Availability sets ensure that hello VMs you deploy on Azure are distributed across multiple isolated hardware clusters.</span></span> <span data-ttu-id="207d1-106">Questa operazione assicura che se si verifica un errore hardware o software all'interno di Azure, solo un sottoinsieme di macchine virtuali che verrà interessato e che la soluzione complessiva rimangono disponibili e operative dal punto di vista hello dei clienti di utilizzarlo.</span><span class="sxs-lookup"><span data-stu-id="207d1-106">Doing this ensures that if a hardware or software failure within Azure happens, only a sub-set of your VMs will be impacted and that your overall solution will remain available and operational from hello perspective of your customers using it.</span></span> 

<span data-ttu-id="207d1-107">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="207d1-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="207d1-108">Creare un set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="207d1-108">Create an availability set</span></span>
> * <span data-ttu-id="207d1-109">Creare una macchina virtuale in un set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="207d1-109">Create a VM in an availability set</span></span>
> * <span data-ttu-id="207d1-110">Controllare le dimensioni delle macchine virtuali disponibili</span><span class="sxs-lookup"><span data-stu-id="207d1-110">Check available VM sizes</span></span>

<span data-ttu-id="207d1-111">Questa esercitazione richiede hello Azure PowerShell versione 3.6 o versioni successive del modulo.</span><span class="sxs-lookup"><span data-stu-id="207d1-111">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="207d1-112">Eseguire ` Get-Module -ListAvailable AzureRM` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="207d1-112">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="207d1-113">Se è necessario tooupgrade, vedere [modulo installare Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="207d1-113">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="availability-set-overview"></a><span data-ttu-id="207d1-114">Informazioni generali sui set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="207d1-114">Availability set overview</span></span>

<span data-ttu-id="207d1-115">Un Set di disponibilità è una raggruppamento logico di funzionalità che è possibile utilizzare in Azure tooensure che le risorse VM hello posizionate all'interno di essa sono isolate tra loro quando vengono distribuiti all'interno di un Data Center Azure.</span><span class="sxs-lookup"><span data-stu-id="207d1-115">An Availability Set is a logical grouping capability that you can use in Azure tooensure that hello VM resources you place within it are isolated from each other when they are deployed within an Azure datacenter.</span></span> <span data-ttu-id="207d1-116">Azure garantisce che le macchine virtuali posizionate all'interno di un Set di disponibilità esegue tra più server fisici hello, calcolo rack, unità di archiviazione e commutatori di rete.</span><span class="sxs-lookup"><span data-stu-id="207d1-116">Azure ensures that hello VMs you place within an Availability Set run across multiple physical servers, compute racks, storage units, and network switches.</span></span> <span data-ttu-id="207d1-117">Ciò garantisce che nell'evento hello di un errore hardware o software di Azure, solo un subset delle macchine virtuali sarà interessato e in generale l'applicazione rimanere e continuare toobe tooyour disponibili clienti.</span><span class="sxs-lookup"><span data-stu-id="207d1-117">This ensures that in hello event of a hardware or Azure software failure, only a subset of your VMs will be impacted, and your overall application will stay up and continue toobe available tooyour customers.</span></span> <span data-ttu-id="207d1-118">Utilizzo di set di disponibilità è un tooleverage funzionalità essenziali quando si desidera che le soluzioni di cloud affidabile toobuild.</span><span class="sxs-lookup"><span data-stu-id="207d1-118">Using Availability Sets is an essential capability tooleverage when you want toobuild reliable cloud solutions.</span></span>

<span data-ttu-id="207d1-119">Si consideri una soluzione tipica basata su macchine virtuali, in cui si dispone di 4 server Web front-end e vengono usate 2 macchine virtuali di back-end che ospitano un database.</span><span class="sxs-lookup"><span data-stu-id="207d1-119">Let’s consider a typical VM-based solution where you might have 4 front-end web servers and use 2 back-end VMs that host a database.</span></span> <span data-ttu-id="207d1-120">Con Azure, si toodefine due set di disponibilità prima di distribuire le macchine virtuali: set di disponibilità di uno per il livello di "web" hello e un set di disponibilità per il livello di "database" hello.</span><span class="sxs-lookup"><span data-stu-id="207d1-120">With Azure, you’d want toodefine two availability sets before you deploy your VMs: one availability set for hello “web” tier and one availability set for hello “database” tier.</span></span> <span data-ttu-id="207d1-121">Quando si crea una nuova macchina virtuale, è possibile specificare la disponibilità di hello imposta come comando di creazione di una macchina virtuale az toohello di parametro e di Azure automaticamente verificare che le macchine virtuali create all'interno di hello disponibile hello set vengono isolati in più risorse hardware fisiche.</span><span class="sxs-lookup"><span data-stu-id="207d1-121">When you create a new VM you can then specify hello availability set as a parameter toohello az vm create command, and Azure will automatically ensure that hello VMs you create within hello available set are isolated across multiple physical hardware resources.</span></span> <span data-ttu-id="207d1-122">Ciò significa che se si è verificato un problema hardware fisico hello in esecuzione in uno dei Server Web o macchine virtuali del Server di Database, si conosce tale hello altre istanze del Server Web e macchine virtuali del Database rimarrà in esecuzione correttamente perché sono in un hardware diverso.</span><span class="sxs-lookup"><span data-stu-id="207d1-122">This means that if hello physical hardware that one of your Web Server or Database Server VMs is running on has a problem, you know that hello other instances of your Web Server and Database VMs will remain running fine because they are on different hardware.</span></span>

<span data-ttu-id="207d1-123">Quando si desidera toodeploy affidabili soluzioni di macchina virtuale in base all'interno di Azure, è necessario utilizzare sempre i set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="207d1-123">You should always use Availability Sets when you want toodeploy reliable VM based solutions within Azure.</span></span>

## <a name="create-an-availability-set"></a><span data-ttu-id="207d1-124">Creare un set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="207d1-124">Create an availability set</span></span>

<span data-ttu-id="207d1-125">È possibile creare un set di disponibilità con il comando [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="207d1-125">You can create an availability set using [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span> <span data-ttu-id="207d1-126">In questo esempio, è impostato sia il numero di domini di aggiornamento e di errore hello *2* per la disponibilità di hello set denominata *myAvailabilitySet* in hello *myResourceGroupAvailability*gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="207d1-126">In this example, we set both hello number of update and fault domains at *2* for hello availability set named *myAvailabilitySet* in hello *myResourceGroupAvailability* resource group.</span></span>

<span data-ttu-id="207d1-127">Creare un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="207d1-127">Create a resource group.</span></span>

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

## <a name="create-vms-inside-an-availability-set"></a><span data-ttu-id="207d1-128">Creare macchine virtuali in un set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="207d1-128">Create VMs inside an availability set</span></span>

<span data-ttu-id="207d1-129">Macchine virtuali devono toobe creati all'interno di hello toomake set di disponibilità che vengono distribuite correttamente su hardware hello.</span><span class="sxs-lookup"><span data-stu-id="207d1-129">VMs need toobe created within hello availability set toomake sure they are correctly distributed across hello hardware.</span></span> <span data-ttu-id="207d1-130">È possibile aggiungere un gruppo di disponibilità tooan VM impostato dopo la sua creazione.</span><span class="sxs-lookup"><span data-stu-id="207d1-130">You can't add an existing VM tooan availability set after it is created.</span></span> 

<span data-ttu-id="207d1-131">hardware Hello in un percorso è suddiviso in domini di aggiornamento toomultiple e domini di errore.</span><span class="sxs-lookup"><span data-stu-id="207d1-131">hello hardware in a location is divided in toomultiple update domains and fault domains.</span></span> <span data-ttu-id="207d1-132">Un **dominio di aggiornamento** è un gruppo di macchine virtuali e l'hardware fisico sottostante che può essere riavviata in hello contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="207d1-132">An **update domain** is a group of VMs and underlying physical hardware that can be rebooted at hello same time.</span></span> <span data-ttu-id="207d1-133">Macchine virtuali in hello stesso **dominio di errore** condividere archiviazione comune, nonché un commutatore power di origine e di rete comune.</span><span class="sxs-lookup"><span data-stu-id="207d1-133">VMs in hello same **fault domain** share common storage as well as a common power source and network switch.</span></span> 

<span data-ttu-id="207d1-134">Quando si crea una macchina virtuale utilizzando configurazione [New AzureRMVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) specificare hello set di disponibilità usando hello `-AvailabilitySetId` parametro toospecify hello ID hello del set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="207d1-134">When you create a VM using configuration using [New-AzureRMVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) you specify hello availability set using hello `-AvailabilitySetId` parameter toospecify hello ID of hello availability set.</span></span>

<span data-ttu-id="207d1-135">Creare 2 macchine virtuali con [New AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) nel set di disponibilità hello.</span><span class="sxs-lookup"><span data-stu-id="207d1-135">Create 2 VMs with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) in hello availability set.</span></span>

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

<span data-ttu-id="207d1-136">Accetta toocreate di pochi minuti e configurare entrambe le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="207d1-136">It takes a few minutes toocreate and configure both VMs.</span></span> <span data-ttu-id="207d1-137">Al termine, si avrà 2 macchine virtuali distribuite tra hello hardware sottostante.</span><span class="sxs-lookup"><span data-stu-id="207d1-137">When finished, you will have 2 virtual machines distributed across hello underlying hardware.</span></span> 

## <a name="check-for-available-vm-sizes"></a><span data-ttu-id="207d1-138">Controllare le dimensioni delle macchine virtuali disponibili</span><span class="sxs-lookup"><span data-stu-id="207d1-138">Check for available VM sizes</span></span> 

<span data-ttu-id="207d1-139">È possibile aggiungere ulteriori disponibilità toohello di macchine virtuali in un momento successivo, ma è necessario tooknow le dimensioni delle macchine Virtuali sono disponibili su hardware hello.</span><span class="sxs-lookup"><span data-stu-id="207d1-139">You can add more VMs toohello availability set later, but you need tooknow what VM sizes are available on hello hardware.</span></span> <span data-ttu-id="207d1-140">Utilizzare [Get AzureRMVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) toolist tutte le dimensioni disponibili hello hardware hello del cluster per il set di disponibilità hello.</span><span class="sxs-lookup"><span data-stu-id="207d1-140">Use [Get-AzureRMVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) toolist all hello available sizes on hello hardware cluster for hello availability set.</span></span>

```powershell
Get-AzureRmVMSize `
   -AvailabilitySetName myAvailabilitySet `
   -ResourceGroupName myResourceGroupAvailability  
```

## <a name="next-steps"></a><span data-ttu-id="207d1-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="207d1-141">Next steps</span></span>

<span data-ttu-id="207d1-142">In questa esercitazione si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="207d1-142">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="207d1-143">Creare un set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="207d1-143">Create an availability set</span></span>
> * <span data-ttu-id="207d1-144">Creare una macchina virtuale in un set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="207d1-144">Create a VM in an availability set</span></span>
> * <span data-ttu-id="207d1-145">Controllare le dimensioni delle macchine virtuali disponibili</span><span class="sxs-lookup"><span data-stu-id="207d1-145">Check available VM sizes</span></span>

<span data-ttu-id="207d1-146">Spostare toohello toolearn esercitazione successiva sui set di scalabilità di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="207d1-146">Advance toohello next tutorial toolearn about virtual machine scale sets.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="207d1-147">Creare un set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="207d1-147">Create a VM scale set</span></span>](tutorial-create-vmss.md)


