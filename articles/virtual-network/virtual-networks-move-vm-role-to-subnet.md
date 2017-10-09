---
title: aaaMove una macchina virtuale (classico) o una subnet tooa diversi istanza ruolo Servizi Cloud - Azure PowerShell | Documenti Microsoft
description: Informazioni su come toomove macchine virtuali (classico) e istanze del ruolo di servizi Cloud tooa subnet diversa utilizzando PowerShell.
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
ms.openlocfilehash: c8d2de56f42a91be4a665414ea9641ffd46588fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-vm-classic-or-cloud-services-role-instance-tooa-different-subnet-using-powershell"></a><span data-ttu-id="40753-103">Spostare una macchina virtuale (classico) o i servizi Cloud ruolo istanza tooa subnet diversa utilizzando PowerShell</span><span class="sxs-lookup"><span data-stu-id="40753-103">Move a VM (Classic) or Cloud Services role instance tooa different subnet using PowerShell</span></span>
<span data-ttu-id="40753-104">È possibile utilizzare le macchine virtuali (classico) da una subnet tooanother toomove di PowerShell in hello stessa rete virtuale (VNet).</span><span class="sxs-lookup"><span data-stu-id="40753-104">You can use PowerShell toomove your VMs (Classic) from one subnet tooanother in hello same virtual network (VNet).</span></span> <span data-ttu-id="40753-105">Le istanze del ruolo possono essere spostate con la modifica di file CSCFG hello, anziché tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="40753-105">Role instances can be moved by editing hello CSCFG file, rather than using PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="40753-106">Questo articolo spiega come macchine virtuali toomove distribuito tramite solo modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="40753-106">This article explains how toomove VMs deployed through hello classic deployment model only.</span></span>
> 
> 

<span data-ttu-id="40753-107">Motivi per cui spostare le macchine virtuali tooanother subnet?</span><span class="sxs-lookup"><span data-stu-id="40753-107">Why move VMs tooanother subnet?</span></span> <span data-ttu-id="40753-108">La migrazione è utile quando la subnet meno recente hello è troppo piccola e non può essere espansa a causa di tooexisting macchine virtuali in esecuzione in quella subnet.</span><span class="sxs-lookup"><span data-stu-id="40753-108">Subnet migration is useful when hello older subnet is too small and cannot be expanded due tooexisting running VMs in that subnet.</span></span> <span data-ttu-id="40753-109">In tal caso, è possibile creare una nuova subnet più grande e la migrazione nuova subnet hello macchine virtuali toohello, quindi al termine della migrazione, è possibile eliminare vecchia subnet ormai vuota hello.</span><span class="sxs-lookup"><span data-stu-id="40753-109">In that case, you can create a new, larger subnet and migrate hello VMs toohello new subnet, then after migration is complete, you can delete hello old empty subnet.</span></span>

## <a name="how-toomove-a-vm-tooanother-subnet"></a><span data-ttu-id="40753-110">Come toomove tooanother subnet VM</span><span class="sxs-lookup"><span data-stu-id="40753-110">How toomove a VM tooanother subnet</span></span>
<span data-ttu-id="40753-111">toomove una macchina virtuale, eseguire i cmdlet di PowerShell Set-AzureSubnet hello, utilizzando l'esempio hello riportato di seguito come modello.</span><span class="sxs-lookup"><span data-stu-id="40753-111">toomove a VM, run hello Set-AzureSubnet PowerShell cmdlet, using hello example below as a template.</span></span> <span data-ttu-id="40753-112">Nell'esempio hello seguente, TestVM viene spostata dalla subnet corrente, tooSubnet-2.</span><span class="sxs-lookup"><span data-stu-id="40753-112">In hello example below, we are moving TestVM from its present subnet, tooSubnet-2.</span></span> <span data-ttu-id="40753-113">Essere tooreflect di esempio hello tooedit che l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="40753-113">Be sure tooedit hello example tooreflect your environment.</span></span> <span data-ttu-id="40753-114">Si noti che quando si esegue cmdlet Update-AzureVM hello come parte di una stored procedure, verrà riavviato la macchina virtuale come parte del processo di aggiornamento hello.</span><span class="sxs-lookup"><span data-stu-id="40753-114">Note that whenever you run hello Update-AzureVM cmdlet as part of a procedure, it will restart your VM as part of hello update process.</span></span>

    Get-AzureVM –ServiceName TestVMCloud –Name TestVM `
    | Set-AzureSubnet –SubnetNames Subnet-2 `
    | Update-AzureVM

<span data-ttu-id="40753-115">Se è stato specificato un indirizzo IP privato interno statico per la macchina virtuale, sarà necessario tooclear tale impostazione prima di poter spostare nuova subnet tooa VM hello.</span><span class="sxs-lookup"><span data-stu-id="40753-115">If you specified a static internal private IP for your VM, you'll have tooclear that setting before you can move hello VM tooa new subnet.</span></span> <span data-ttu-id="40753-116">In tal caso, utilizzare il seguente di hello:</span><span class="sxs-lookup"><span data-stu-id="40753-116">In that case, use hello following:</span></span>

    Get-AzureVM -ServiceName TestVMCloud -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM
    Get-AzureVM -ServiceName TestVMCloud -Name TestVM `
    | Set-AzureSubnet -SubnetNames Subnet-2 `
    | Update-AzureVM

## <a name="toomove-a-role-instance-tooanother-subnet"></a><span data-ttu-id="40753-117">toomove una subnet tooanother istanza di ruolo</span><span class="sxs-lookup"><span data-stu-id="40753-117">toomove a role instance tooanother subnet</span></span>
<span data-ttu-id="40753-118">toomove un'istanza del ruolo, modificare il file CSCFG hello.</span><span class="sxs-lookup"><span data-stu-id="40753-118">toomove a role instance, edit hello CSCFG file.</span></span> <span data-ttu-id="40753-119">Nell'esempio hello riportato di seguito "Role0" viene spostato nella rete virtuale *VNETName* dalla subnet corrente troppo*Subnet-2*.</span><span class="sxs-lookup"><span data-stu-id="40753-119">In hello example below, we are moving "Role0" in virtual network *VNETName* from its present subnet too*Subnet-2*.</span></span> <span data-ttu-id="40753-120">Poiché l'istanza del ruolo hello era già stata distribuita, sarà solo necessario impostare il nome di Subnet hello = Subnet-2.</span><span class="sxs-lookup"><span data-stu-id="40753-120">Because hello role instance was already deployed, you'll just change hello Subnet name = Subnet-2.</span></span> <span data-ttu-id="40753-121">Essere tooreflect di esempio hello tooedit che l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="40753-121">Be sure tooedit hello example tooreflect your environment.</span></span>

    <NetworkConfiguration>
        <VirtualNetworkSite name="VNETName" />
        <AddressAssignments>
           <InstanceAddress roleName="Role0">
                <Subnets><Subnet name="Subnet-2" /></Subnets>
           </InstanceAddress>
        </AddressAssignments>
    </NetworkConfiguration> 
