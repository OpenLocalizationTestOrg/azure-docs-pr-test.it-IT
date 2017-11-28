---
title: aaaStatic interno classica - VM di Azure - IP privato
description: Informazioni IP interno statico (DIP) e in che modo toomanage li
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 93444c6f-af1b-41f8-a035-77f5c0302bf0
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2016
ms.author: jdial
ms.openlocfilehash: 5abe1c59f2f3ed19bcf56c269dfe57ac32d4f601
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-a-static-internal-private-ip-address-using-powershell-classic"></a><span data-ttu-id="e5107-103">Come un indirizzo IP privato interno statico tooset indirizzo tramite PowerShell (versione classica)</span><span class="sxs-lookup"><span data-stu-id="e5107-103">How tooset a static internal private IP address using PowerShell (Classic)</span></span>
<span data-ttu-id="e5107-104">Nella maggior parte dei casi, non è necessario toospecify un indirizzo IP interno statico per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e5107-104">In most cases, you won’t need toospecify a static internal IP address for your virtual machine.</span></span> <span data-ttu-id="e5107-105">Le macchine virtuali in una rete virtuale infatti ricevono automaticamente un indirizzo IP interno da un intervallo specificato.</span><span class="sxs-lookup"><span data-stu-id="e5107-105">VMs in a virtual network will automatically receive an internal IP address from a range that you specify.</span></span> <span data-ttu-id="e5107-106">In alcuni casi è tuttavia opportuno specificare un indirizzo IP statico per una determinata macchina virtuale,</span><span class="sxs-lookup"><span data-stu-id="e5107-106">But in certain cases, specifying a static IP address for a particular VM makes sense.</span></span> <span data-ttu-id="e5107-107">Ad esempio, se la macchina virtuale è corso toorun DNS o sarà un controller di dominio.</span><span class="sxs-lookup"><span data-stu-id="e5107-107">For example, if your VM is going toorun DNS or will be a domain controller.</span></span> <span data-ttu-id="e5107-108">Un indirizzo IP interno statico rimane associato hello VM anche attraverso un arresto o deprovisioning.</span><span class="sxs-lookup"><span data-stu-id="e5107-108">A static internal IP address stays with hello VM even through a stop/deprovision state.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="e5107-109">Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="e5107-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="e5107-110">In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="e5107-110">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="e5107-111">Microsoft consiglia di utilizzano hello più nuove distribuzioni [il modello di distribuzione di gestione risorse](virtual-networks-static-private-ip-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="e5107-111">Microsoft recommends that most new deployments use hello [Resource Manager deployment model](virtual-networks-static-private-ip-arm-ps.md).</span></span>
> 
> 

## <a name="how-tooverify-if-a-specific-ip-address-is-available"></a><span data-ttu-id="e5107-112">Come tooverify se è disponibile un indirizzo IP specifico</span><span class="sxs-lookup"><span data-stu-id="e5107-112">How tooverify if a specific IP address is available</span></span>
<span data-ttu-id="e5107-113">tooverify se hello indirizzo IP *10.0.0.7* è disponibile in una rete virtuale denominata *TestVnet*, eseguire il comando PowerShell seguente hello e verificare il valore di hello per *IsAvailable*:</span><span class="sxs-lookup"><span data-stu-id="e5107-113">tooverify if hello IP address *10.0.0.7* is available in a vnet named *TestVnet*, run hello following PowerShell command and verify hello value for *IsAvailable*:</span></span>

    Test-AzureStaticVNetIP –VNetName TestVNet –IPAddress 10.0.0.7 

    IsAvailable          : True
    AvailableAddresses   : {}
    OperationDescription : Test-AzureStaticVNetIP
    OperationId          : fd3097e1-5f4b-9cac-8afa-bba1e3492609
    OperationStatus      : Succeeded

> [!NOTE]
> <span data-ttu-id="e5107-114">Se si desidera tootest un comando di hello in precedenza in un ambiente sicuro, seguire le linee guida hello in [creare una rete virtuale (classico)](virtual-networks-create-vnet-classic-pportal.md) toocreate una rete virtuale denominata *TestVnet* e verificare che venga utilizzato hello  *10.0.0.0/8* lo spazio degli indirizzi.</span><span class="sxs-lookup"><span data-stu-id="e5107-114">If you want tootest hello command above in a safe environment follow hello guidelines in [Create a virtual network (classic)](virtual-networks-create-vnet-classic-pportal.md) toocreate a vnet named *TestVnet* and ensure it uses hello *10.0.0.0/8* address space.</span></span>
> 
> 

## <a name="how-toospecify-a-static-internal-ip-when-creating-a-vm"></a><span data-ttu-id="e5107-115">Come toospecify un indirizzo IP interno statico durante la creazione di una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="e5107-115">How toospecify a static internal IP when creating a VM</span></span>
<span data-ttu-id="e5107-116">Hello script di PowerShell riportato di seguito crea un nuovo servizio cloud denominato *TestService*, quindi recupera un'immagine da Azure, quindi crea una macchina virtuale denominata *TestVM* in hello nuovo servizio cloud usando hello recuperato immagine, set di hello toobe macchina virtuale in una subnet denominata *Subnet-1*e imposta *10.0.0.7* come un indirizzo IP interno statico per hello VM:</span><span class="sxs-lookup"><span data-stu-id="e5107-116">hello PowerShell script below creates a new cloud service named *TestService*, then retrieves an image from Azure, then creates a VM named *TestVM* in hello new cloud service using hello retrieved image, sets hello VM toobe in a subnet named *Subnet-1*, and sets *10.0.0.7* as a static internal IP for hello VM:</span></span>

    New-AzureService -ServiceName TestService -Location "Central US"
    $image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}
    New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
    | Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
    | Set-AzureSubnet –SubnetNames Subnet-1 `
    | Set-AzureStaticVNetIP -IPAddress 10.0.0.7 `
    | New-AzureVM -ServiceName "TestService" –VNetName TestVnet

## <a name="how-tooretrieve-static-internal-ip-information-for-a-vm"></a><span data-ttu-id="e5107-117">Come tooretrieve interne informazioni IP statici per una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="e5107-117">How tooretrieve static internal IP information for a VM</span></span>
<span data-ttu-id="e5107-118">tooview hello interne informazioni IP statici per hello macchina virtuale creata con lo script hello precedente, eseguire il comando PowerShell seguente hello e osservare i valori hello per *IpAddress*:</span><span class="sxs-lookup"><span data-stu-id="e5107-118">tooview hello static internal IP information for hello VM created with hello script above, run hello following PowerShell command and observe hello values for *IpAddress*:</span></span>

    Get-AzureVM -Name TestVM -ServiceName TestService

    DeploymentName              : TestService
    Name                        : TestVM
    Label                       : 
    VM                          : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.PersistentVM
    InstanceStatus              : Provisioning
    IpAddress                   : 10.0.0.7
    InstanceStateDetails        : Windows is preparing your computer for first use...
    PowerState                  : Started
    InstanceErrorCode           : 
    InstanceFaultDomain         : 0
    InstanceName                : TestVM
    InstanceUpgradeDomain       : 0
    InstanceSize                : Small
    HostName                    : rsR2-797
    AvailabilitySetName         : 
    DNSName                     : http://testservice000.cloudapp.net/
    Status                      : Provisioning
    GuestAgentStatus            : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.GuestAgentStatus
    ResourceExtensionStatusList : {Microsoft.Compute.BGInfo}
    PublicIPAddress             : 
    PublicIPName                : 
    NetworkInterfaces           : {}
    ServiceName                 : TestService
    OperationDescription        : Get-AzureVM
    OperationId                 : 34c1560a62f0901ab75cde4fed8e8bd1
    OperationStatus             : OK

## <a name="how-tooremove-a-static-internal-ip-from-a-vm"></a><span data-ttu-id="e5107-119">Come tooremove un indirizzo IP interno statico da una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="e5107-119">How tooremove a static internal IP from a VM</span></span>
<span data-ttu-id="e5107-120">tooremove hello indirizzo IP interno statico aggiunta toohello VM hello allo script precedente, eseguire il comando PowerShell seguente hello:</span><span class="sxs-lookup"><span data-stu-id="e5107-120">tooremove hello static internal IP added toohello VM in hello script above, run hello following PowerShell command:</span></span>

    Get-AzureVM -ServiceName TestService -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM

## <a name="how-tooadd-a-static-internal-ip-tooan-existing-vm"></a><span data-ttu-id="e5107-121">Come tooadd un tooan IP interno statico macchina virtuale esistente</span><span class="sxs-lookup"><span data-stu-id="e5107-121">How tooadd a static internal IP tooan existing VM</span></span>
<span data-ttu-id="e5107-122">tooadd un toohello IP interno statico macchina virtuale creata utilizzando lo script hello sopra, Run il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="e5107-122">tooadd a static internal IP toohello VM created using hello script above, runt he following command:</span></span>

    Get-AzureVM -ServiceName TestService000 -Name TestVM `
    | Set-AzureStaticVNetIP -IPAddress 10.10.0.7 `
    | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="e5107-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e5107-123">Next steps</span></span>
[<span data-ttu-id="e5107-124">IP riservato</span><span class="sxs-lookup"><span data-stu-id="e5107-124">Reserved IP</span></span>](virtual-networks-reserved-public-ip.md)

[<span data-ttu-id="e5107-125">IP pubblico a livello di istanza (ILPIP)</span><span class="sxs-lookup"><span data-stu-id="e5107-125">Instance-Level Public IP (ILPIP)</span></span>](virtual-networks-instance-level-public-ip.md)

[<span data-ttu-id="e5107-126">API REST di IP riservati</span><span class="sxs-lookup"><span data-stu-id="e5107-126">Reserved IP REST APIs</span></span>](https://msdn.microsoft.com/library/azure/dn722420.aspx)

