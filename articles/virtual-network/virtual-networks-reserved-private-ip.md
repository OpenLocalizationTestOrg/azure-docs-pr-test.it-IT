---
title: Indirizzo IP privato interno statico - Macchina virtuale di Azure - Versione classica
description: Informazioni sugli indirizzi IP interni statici (DIP) e su come gestirli
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
ms.openlocfilehash: cf9ee59ca4e44ed01836c2efb1f4df5f073bf6e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-set-a-static-internal-private-ip-address-using-powershell-classic"></a><span data-ttu-id="e1bcc-103">Come impostare un indirizzo IP privato interno statico tramite PowerShell (classico)</span><span class="sxs-lookup"><span data-stu-id="e1bcc-103">How to set a static internal private IP address using PowerShell (Classic)</span></span>
<span data-ttu-id="e1bcc-104">Nella maggior parte dei casi non è necessario specificare un indirizzo IP interno statico per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e1bcc-104">In most cases, you won’t need to specify a static internal IP address for your virtual machine.</span></span> <span data-ttu-id="e1bcc-105">Le macchine virtuali in una rete virtuale infatti ricevono automaticamente un indirizzo IP interno da un intervallo specificato.</span><span class="sxs-lookup"><span data-stu-id="e1bcc-105">VMs in a virtual network will automatically receive an internal IP address from a range that you specify.</span></span> <span data-ttu-id="e1bcc-106">In alcuni casi è tuttavia opportuno specificare un indirizzo IP statico per una determinata macchina virtuale,</span><span class="sxs-lookup"><span data-stu-id="e1bcc-106">But in certain cases, specifying a static IP address for a particular VM makes sense.</span></span> <span data-ttu-id="e1bcc-107">ad esempio se questa eseguirà DNS o sarà un controller di dominio.</span><span class="sxs-lookup"><span data-stu-id="e1bcc-107">For example, if your VM is going to run DNS or will be a domain controller.</span></span> <span data-ttu-id="e1bcc-108">Un indirizzo IP interno statico resta associato alla macchina virtuale anche in caso di passaggio allo stato di arresto/deprovisioning.</span><span class="sxs-lookup"><span data-stu-id="e1bcc-108">A static internal IP address stays with the VM even through a stop/deprovision state.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="e1bcc-109">Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="e1bcc-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="e1bcc-110">Questo articolo illustra l'uso del modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="e1bcc-110">This article covers using the classic deployment model.</span></span> <span data-ttu-id="e1bcc-111">Microsoft consiglia di utilizzare il [modello di distribuzione di Resource Manager per le distribuzioni più recenti](virtual-networks-static-private-ip-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="e1bcc-111">Microsoft recommends that most new deployments use the [Resource Manager deployment model](virtual-networks-static-private-ip-arm-ps.md).</span></span>
> 
> 

## <a name="how-to-verify-if-a-specific-ip-address-is-available"></a><span data-ttu-id="e1bcc-112">Come verificare la disponibilità di uno specifico indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="e1bcc-112">How to verify if a specific IP address is available</span></span>
<span data-ttu-id="e1bcc-113">Per verificare se l'indirizzo IP *10.0.0.7* è disponibile in una rete virtuale denominata *TestVnet*, eseguire il comando PowerShell seguente e controllare il valore per *IsAvailable*:</span><span class="sxs-lookup"><span data-stu-id="e1bcc-113">To verify if the IP address *10.0.0.7* is available in a vnet named *TestVnet*, run the following PowerShell command and verify the value for *IsAvailable*:</span></span>

    Test-AzureStaticVNetIP –VNetName TestVNet –IPAddress 10.0.0.7 

    IsAvailable          : True
    AvailableAddresses   : {}
    OperationDescription : Test-AzureStaticVNetIP
    OperationId          : fd3097e1-5f4b-9cac-8afa-bba1e3492609
    OperationStatus      : Succeeded

> [!NOTE]
> <span data-ttu-id="e1bcc-114">Per testare il comando precedente in un ambiente sicuro, seguire le istruzioni in [Creare una rete virtuale (versione classica)](virtual-networks-create-vnet-classic-pportal.md) per creare una rete virtuale denominata *TestVnet* e assicurarsi che usi lo spazio degli indirizzi *10.0.0.0/8*.</span><span class="sxs-lookup"><span data-stu-id="e1bcc-114">If you want to test the command above in a safe environment follow the guidelines in [Create a virtual network (classic)](virtual-networks-create-vnet-classic-pportal.md) to create a vnet named *TestVnet* and ensure it uses the *10.0.0.0/8* address space.</span></span>
> 
> 

## <a name="how-to-specify-a-static-internal-ip-when-creating-a-vm"></a><span data-ttu-id="e1bcc-115">Come specificare un indirizzo IP interno statico durante la creazione di una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="e1bcc-115">How to specify a static internal IP when creating a VM</span></span>
<span data-ttu-id="e1bcc-116">Lo script di PowerShell seguente crea un nuovo servizio cloud denominato *TestService*, quindi recupera un'immagine da Azure, crea una macchina virtuale denominata *TestVM* nel nuovo servizio cloud tramite l'immagine recuperata, imposta la macchina virtuale in modo da trovarsi in una subnet denominata *Subnet-1* e imposta *10.0.0.7* come indirizzo IP interno statico per la macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="e1bcc-116">The PowerShell script below creates a new cloud service named *TestService*, then retrieves an image from Azure, then creates a VM named *TestVM* in the new cloud service using the retrieved image, sets the VM to be in a subnet named *Subnet-1*, and sets *10.0.0.7* as a static internal IP for the VM:</span></span>

    New-AzureService -ServiceName TestService -Location "Central US"
    $image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}
    New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
    | Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
    | Set-AzureSubnet –SubnetNames Subnet-1 `
    | Set-AzureStaticVNetIP -IPAddress 10.0.0.7 `
    | New-AzureVM -ServiceName "TestService" –VNetName TestVnet

## <a name="how-to-retrieve-static-internal-ip-information-for-a-vm"></a><span data-ttu-id="e1bcc-117">Come recuperare le informazioni relative all'indirizzo IP interno statico per una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="e1bcc-117">How to retrieve static internal IP information for a VM</span></span>
<span data-ttu-id="e1bcc-118">Per visualizzare le informazioni relative all'indirizzo IP interno statico per la macchina virtuale creata con lo script precedente, eseguire il comando PowerShell seguente e osservare i valori per *IpAddress*:</span><span class="sxs-lookup"><span data-stu-id="e1bcc-118">To view the static internal IP information for the VM created with the script above, run the following PowerShell command and observe the values for *IpAddress*:</span></span>

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

## <a name="how-to-remove-a-static-internal-ip-from-a-vm"></a><span data-ttu-id="e1bcc-119">Come rimuovere un indirizzo IP interno statico da una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="e1bcc-119">How to remove a static internal IP from a VM</span></span>
<span data-ttu-id="e1bcc-120">Per rimuovere l'indirizzo IP interno statico aggiunto alla macchina virtuale nello script precedente, eseguire il comando PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="e1bcc-120">To remove the static internal IP added to the VM in the script above, run the following PowerShell command:</span></span>

    Get-AzureVM -ServiceName TestService -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM

## <a name="how-to-add-a-static-internal-ip-to-an-existing-vm"></a><span data-ttu-id="e1bcc-121">Come aggiungere un indirizzo IP interno statico a una macchina virtuale esistente</span><span class="sxs-lookup"><span data-stu-id="e1bcc-121">How to add a static internal IP to an existing VM</span></span>
<span data-ttu-id="e1bcc-122">Per aggiungere un indirizzo IP interno statico alla macchina virtuale creata usando lo script precedente, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e1bcc-122">To add a static internal IP to the VM created using the script above, runt he following command:</span></span>

    Get-AzureVM -ServiceName TestService000 -Name TestVM `
    | Set-AzureStaticVNetIP -IPAddress 10.10.0.7 `
    | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="e1bcc-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e1bcc-123">Next steps</span></span>
[<span data-ttu-id="e1bcc-124">IP riservato</span><span class="sxs-lookup"><span data-stu-id="e1bcc-124">Reserved IP</span></span>](virtual-networks-reserved-public-ip.md)

[<span data-ttu-id="e1bcc-125">IP pubblico a livello di istanza (ILPIP)</span><span class="sxs-lookup"><span data-stu-id="e1bcc-125">Instance-Level Public IP (ILPIP)</span></span>](virtual-networks-instance-level-public-ip.md)

[<span data-ttu-id="e1bcc-126">API REST di IP riservati</span><span class="sxs-lookup"><span data-stu-id="e1bcc-126">Reserved IP REST APIs</span></span>](https://msdn.microsoft.com/library/azure/dn722420.aspx)

