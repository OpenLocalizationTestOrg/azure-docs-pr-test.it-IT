---
title: Spostare una VM (classica) o un'istanza del ruolo di Servizi cloud in un'altra subnet - Azure PowerShell | Documentazione Microsoft
description: Informazioni su come spostare le VM (classiche) e le istanze del ruolo di Servizi cloud in un'altra subnet mediante PowerShell.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: de4135c7-dc5b-4ffa-84cc-1b8364b7b427
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b094f8338394ef2e84cad3070936d715411326a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="move-a-vm-classic-or-cloud-services-role-instance-to-a-different-subnet-using-powershell"></a><span data-ttu-id="b40e5-103">Spostare una VM (classica) o un'istanza del ruolo di Servizi cloud in un'altra subnet mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="b40e5-103">Move a VM (Classic) or Cloud Services role instance to a different subnet using PowerShell</span></span>
<span data-ttu-id="b40e5-104">È possibile usare PowerShell per spostare le proprie VM (classiche) da una subnet a un'altra nella stessa rete virtuale (VNet).</span><span class="sxs-lookup"><span data-stu-id="b40e5-104">You can use PowerShell to move your VMs (Classic) from one subnet to another in the same virtual network (VNet).</span></span> <span data-ttu-id="b40e5-105">Le istanze del ruolo possono essere spostate modificando il file CSCFG invece di usare PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b40e5-105">Role instances can be moved by editing the CSCFG file, rather than using PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="b40e5-106">Questo articolo spiega come spostare solo le VM distribuite tramite il modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="b40e5-106">This article explains how to move VMs deployed through the classic deployment model only.</span></span>
> 
> 

<span data-ttu-id="b40e5-107">Perché spostare le macchine virtuali in un'altra subnet?</span><span class="sxs-lookup"><span data-stu-id="b40e5-107">Why move VMs to another subnet?</span></span> <span data-ttu-id="b40e5-108">La migrazione in un'altra subnet è utile quando la subnet corrente è troppo piccola e non può essere espansa a causa delle macchine virtuali in esecuzione al suo interno.</span><span class="sxs-lookup"><span data-stu-id="b40e5-108">Subnet migration is useful when the older subnet is too small and cannot be expanded due to existing running VMs in that subnet.</span></span> <span data-ttu-id="b40e5-109">In tal caso, è possibile creare una nuova subnet più grande, migrarvi le macchine virtuali e al termine eliminare la precedente subnet ormai vuota.</span><span class="sxs-lookup"><span data-stu-id="b40e5-109">In that case, you can create a new, larger subnet and migrate the VMs to the new subnet, then after migration is complete, you can delete the old empty subnet.</span></span>

## <a name="how-to-move-a-vm-to-another-subnet"></a><span data-ttu-id="b40e5-110">Come spostare una macchina virtuale in un'altra subnet</span><span class="sxs-lookup"><span data-stu-id="b40e5-110">How to move a VM to another subnet</span></span>
<span data-ttu-id="b40e5-111">Per spostare una macchina virtuale, eseguire il cmdlet di PowerShell Set-AzureSubnet usando l'esempio seguente come modello.</span><span class="sxs-lookup"><span data-stu-id="b40e5-111">To move a VM, run the Set-AzureSubnet PowerShell cmdlet, using the example below as a template.</span></span> <span data-ttu-id="b40e5-112">In tale esempio TestVM viene spostata dalla subnet corrente a Subnet-2.</span><span class="sxs-lookup"><span data-stu-id="b40e5-112">In the example below, we are moving TestVM from its present subnet, to Subnet-2.</span></span> <span data-ttu-id="b40e5-113">Ricordarsi di modificare l'esempio in base all'ambiente in uso.</span><span class="sxs-lookup"><span data-stu-id="b40e5-113">Be sure to edit the example to reflect your environment.</span></span> <span data-ttu-id="b40e5-114">Si noti che, ogni volta che il cmdlet Update-AzureVM viene eseguito in una procedura, riavvierà la macchina virtuale come parte del processo di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="b40e5-114">Note that whenever you run the Update-AzureVM cmdlet as part of a procedure, it will restart your VM as part of the update process.</span></span>

    Get-AzureVM –ServiceName TestVMCloud –Name TestVM `
    | Set-AzureSubnet –SubnetNames Subnet-2 `
    | Update-AzureVM

<span data-ttu-id="b40e5-115">Se è stato specificato un indirizzo IP privato interno statico per la macchina virtuale, sarà necessario cancellare tale impostazione prima di poter spostare la macchina virtuale in una nuova subnet.</span><span class="sxs-lookup"><span data-stu-id="b40e5-115">If you specified a static internal private IP for your VM, you'll have to clear that setting before you can move the VM to a new subnet.</span></span> <span data-ttu-id="b40e5-116">In questo caso, usare quanto segue:</span><span class="sxs-lookup"><span data-stu-id="b40e5-116">In that case, use the following:</span></span>

    Get-AzureVM -ServiceName TestVMCloud -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM
    Get-AzureVM -ServiceName TestVMCloud -Name TestVM `
    | Set-AzureSubnet -SubnetNames Subnet-2 `
    | Update-AzureVM

## <a name="to-move-a-role-instance-to-another-subnet"></a><span data-ttu-id="b40e5-117">Per spostare un'istanza del ruolo in un'altra subnet</span><span class="sxs-lookup"><span data-stu-id="b40e5-117">To move a role instance to another subnet</span></span>
<span data-ttu-id="b40e5-118">Per spostare un'istanza del ruolo, modificare il file CSCFG.</span><span class="sxs-lookup"><span data-stu-id="b40e5-118">To move a role instance, edit the CSCFG file.</span></span> <span data-ttu-id="b40e5-119">Nell'esempio seguente "Role0" nella rete virtuale *VNETName* viene spostato dalla subnet corrente a *Subnet-2*.</span><span class="sxs-lookup"><span data-stu-id="b40e5-119">In the example below, we are moving "Role0" in virtual network *VNETName* from its present subnet to *Subnet-2*.</span></span> <span data-ttu-id="b40e5-120">Poiché l'istanza del ruolo è già stata distribuita, sarà necessario solo modificare Subnet name = Subnet-2.</span><span class="sxs-lookup"><span data-stu-id="b40e5-120">Because the role instance was already deployed, you'll just change the Subnet name = Subnet-2.</span></span> <span data-ttu-id="b40e5-121">Ricordarsi di modificare l'esempio in base all'ambiente in uso.</span><span class="sxs-lookup"><span data-stu-id="b40e5-121">Be sure to edit the example to reflect your environment.</span></span>

    <NetworkConfiguration>
        <VirtualNetworkSite name="VNETName" />
        <AddressAssignments>
           <InstanceAddress roleName="Role0">
                <Subnets><Subnet name="Subnet-2" /></Subnets>
           </InstanceAddress>
        </AddressAssignments>
    </NetworkConfiguration> 
