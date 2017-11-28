---
title: aaaManage Azure riservato di indirizzi IP (classico) - finestra di PowerShell | Documenti Microsoft
description: Comprendere gli indirizzi IP riservati (classico) e in che modo toomanage loro tramite PowerShell.
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 34652a55-3ab8-4c2d-8fb2-43684033b191
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2016
ms.author: jdial
ms.openlocfilehash: c0a77b2ab8b1ab9bef6015c903eb735ea4358a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="reserved-ip-addresses-classic"></a><span data-ttu-id="ce7e6-103">Indirizzi IP riservati (classica)</span><span class="sxs-lookup"><span data-stu-id="ce7e6-103">Reserved IP addresses (Classic)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ce7e6-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="ce7e6-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="ce7e6-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ce7e6-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="ce7e6-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="ce7e6-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="ce7e6-107">Modello</span><span class="sxs-lookup"><span data-stu-id="ce7e6-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * <span data-ttu-id="ce7e6-108">[PowerShell (Classic)](virtual-networks-reserved-public-ip.md) (PowerShell (classico))</span><span class="sxs-lookup"><span data-stu-id="ce7e6-108">[PowerShell (Classic)](virtual-networks-reserved-public-ip.md)</span></span>

<span data-ttu-id="ce7e6-109">Gli indirizzi IP in Azure rientrano in due categorie: indirizzi dinamici e indirizzi riservati.</span><span class="sxs-lookup"><span data-stu-id="ce7e6-109">IP addresses in Azure fall into two categories: dynamic and reserved.</span></span> <span data-ttu-id="ce7e6-110">Gli indirizzi IP pubblici gestiti da Azure sono dinamici per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="ce7e6-110">Public IP addresses managed by Azure are dynamic by default.</span></span> <span data-ttu-id="ce7e6-111">Che indica che l'indirizzo IP di hello utilizzato per un determinato servizio cloud (VIP) o tooaccess una macchina virtuale o istanza del ruolo direttamente (ILPIP) è possibile modificare da tootime ora, quando le risorse arrestare o arrestate (deallocate).</span><span class="sxs-lookup"><span data-stu-id="ce7e6-111">That means that hello IP address used for a given cloud service (VIP) or tooaccess a VM or role instance directly (ILPIP) can change from time tootime, when resources are shut down or stopped (deallocated).</span></span>

<span data-ttu-id="ce7e6-112">tooprevent da indirizzi IP di modifica, è possibile riservare un indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="ce7e6-112">tooprevent IP addresses from changing, you can reserve an IP address.</span></span> <span data-ttu-id="ce7e6-113">Gli indirizzi IP riservati possono essere utilizzato solo come un indirizzo VIP, assicurandosi di tale indirizzo IP di hello per il servizio cloud hello rimane hello stesso, anche se le risorse vengono arrestate o arrestate (deallocate).</span><span class="sxs-lookup"><span data-stu-id="ce7e6-113">Reserved IPs can be used only as a VIP, ensuring that hello IP address for hello cloud service remains hello same, even as resources are shut down or stopped (deallocated).</span></span> <span data-ttu-id="ce7e6-114">Inoltre, è possibile convertire utilizzato come indirizzo IP riservato tooa VIP gli indirizzi IP dinamici esistente.</span><span class="sxs-lookup"><span data-stu-id="ce7e6-114">Furthermore, you can convert existing dynamic IPs used as a VIP tooa reserved IP address.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ce7e6-115">Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ce7e6-115">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ce7e6-116">In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="ce7e6-116">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="ce7e6-117">Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="ce7e6-117">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="ce7e6-118">Informazioni su come un indirizzo pubblico IP statico usando tooreserve hello [il modello di distribuzione di gestione risorse](virtual-network-ip-addresses-overview-arm.md).</span><span class="sxs-lookup"><span data-stu-id="ce7e6-118">Learn how tooreserve a static public IP address using hello [Resource Manager deployment model](virtual-network-ip-addresses-overview-arm.md).</span></span>

<span data-ttu-id="ce7e6-119">gli indirizzi toolearn più sull'indirizzo IP in Azure, leggere hello [gli indirizzi IP](virtual-network-ip-addresses-overview-classic.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="ce7e6-119">toolearn more about IP addresses in Azure, read hello [IP addresses](virtual-network-ip-addresses-overview-classic.md) article.</span></span>

## <a name="when-do-i-need-a-reserved-ip"></a><span data-ttu-id="ce7e6-120">Quando è necessario un indirizzo IP riservato?</span><span class="sxs-lookup"><span data-stu-id="ce7e6-120">When do I need a reserved IP?</span></span>
* <span data-ttu-id="ce7e6-121">**Si desidera tooensure che hello IP riservato nella sottoscrizione**.</span><span class="sxs-lookup"><span data-stu-id="ce7e6-121">**You want tooensure that hello IP is reserved in your subscription**.</span></span> <span data-ttu-id="ce7e6-122">Se si desidera tooreserve un indirizzo IP che non viene rilasciato dalla sottoscrizione in nessuna circostanza, è necessario utilizzare un indirizzo IP pubblico riservato.</span><span class="sxs-lookup"><span data-stu-id="ce7e6-122">If you want tooreserve an IP address that is not released from your subscription under any circumstance, you should use a reserved public IP.</span></span>  
* <span data-ttu-id="ce7e6-123">**Si desidera che il toostay IP con il servizio cloud anche attraverso arrestato o DEALLOCATE (VM) di stato**.</span><span class="sxs-lookup"><span data-stu-id="ce7e6-123">**You want your IP toostay with your cloud service even across stopped or deallocated state (VMs)**.</span></span> <span data-ttu-id="ce7e6-124">Se si desidera toobe il servizio a cui accede utilizzando un indirizzo IP che non cambia, anche quando le macchine virtuali in hello cloud servizio vengono arrestate o arrestare (deallocato).</span><span class="sxs-lookup"><span data-stu-id="ce7e6-124">If you want your service toobe accessed by using an IP address that doesn't change, even when VMs in hello cloud service are shut down or stop (deallocated).</span></span>
* <span data-ttu-id="ce7e6-125">**Si desidera che il traffico in uscita da Azure usi un indirizzo IP prevedibile tooensure**.</span><span class="sxs-lookup"><span data-stu-id="ce7e6-125">**You want tooensure that outbound traffic from Azure uses a predictable IP address**.</span></span> <span data-ttu-id="ce7e6-126">È possibile il locale firewall configurato tooallow solo il traffico da indirizzi IP specifici.</span><span class="sxs-lookup"><span data-stu-id="ce7e6-126">You may have your on-premises firewall configured tooallow only traffic from specific IP addresses.</span></span> <span data-ttu-id="ce7e6-127">Riserva un indirizzo IP, si conosce l'indirizzo IP di origine hello indirizzo e non sono necessarie regole firewall a causa di modifiche IP tooan tooupdate.</span><span class="sxs-lookup"><span data-stu-id="ce7e6-127">By reserving an IP, you know hello source IP address, and don't need tooupdate your firewall rules due tooan IP change.</span></span>

## <a name="faq"></a><span data-ttu-id="ce7e6-128">domande frequenti</span><span class="sxs-lookup"><span data-stu-id="ce7e6-128">FAQ</span></span>
1. <span data-ttu-id="ce7e6-129">È possibile usare un indirizzo IP riservato per tutti i servizi di Azure?</span><span class="sxs-lookup"><span data-stu-id="ce7e6-129">Can I use a reserved IP for all Azure services?</span></span> <br>
    <span data-ttu-id="ce7e6-130">No.</span><span class="sxs-lookup"><span data-stu-id="ce7e6-130">No.</span></span> <span data-ttu-id="ce7e6-131">Gli indirizzi IP riservati possono essere usati solo per le macchine virtuali e per i ruoli delle istanze del servizio cloud esposti mediante un indirizzo VIP.</span><span class="sxs-lookup"><span data-stu-id="ce7e6-131">Reserved IPs can only be used for VMs and cloud service instance roles exposed through a VIP.</span></span>
2. <span data-ttu-id="ce7e6-132">Di quanti indirizzi IP riservati è possibile disporre?</span><span class="sxs-lookup"><span data-stu-id="ce7e6-132">How many reserved IPs can I have?</span></span> <br>
    <span data-ttu-id="ce7e6-133">Per informazioni dettagliate, vedere hello [Azure limita](../azure-subscription-service-limits.md#networking-limits) articolo.</span><span class="sxs-lookup"><span data-stu-id="ce7e6-133">For details, see hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
3. <span data-ttu-id="ce7e6-134">È previsto un addebito per gli indirizzi IP riservati?</span><span class="sxs-lookup"><span data-stu-id="ce7e6-134">Is there a charge for reserved IPs?</span></span> <br>
    <span data-ttu-id="ce7e6-135">In alcuni casi sì.</span><span class="sxs-lookup"><span data-stu-id="ce7e6-135">Sometimes.</span></span> <span data-ttu-id="ce7e6-136">Per informazioni sui prezzi, vedere hello [dettagli prezzi di indirizzi IP riservati](http://go.microsoft.com/fwlink/?LinkID=398482) pagina.</span><span class="sxs-lookup"><span data-stu-id="ce7e6-136">For pricing details, see hello [Reserved IP Address Pricing Details](http://go.microsoft.com/fwlink/?LinkID=398482) page.</span></span>
4. <span data-ttu-id="ce7e6-137">Come è possibile riservare un indirizzo IP?</span><span class="sxs-lookup"><span data-stu-id="ce7e6-137">How do I reserve an IP address?</span></span> <br>
    <span data-ttu-id="ce7e6-138">È possibile usare PowerShell, hello [API REST di gestione di Azure](https://msdn.microsoft.com/library/azure/dn722420.aspx), o hello [portale di Azure](https://portal.azure.com) tooreserve un indirizzo IP in un'area di Azure.</span><span class="sxs-lookup"><span data-stu-id="ce7e6-138">You can use PowerShell, hello [Azure Management REST API](https://msdn.microsoft.com/library/azure/dn722420.aspx), or hello [Azure portal](https://portal.azure.com) tooreserve an IP address in an Azure region.</span></span> <span data-ttu-id="ce7e6-139">Un indirizzo IP riservato è sottoscrizione tooyour associato.</span><span class="sxs-lookup"><span data-stu-id="ce7e6-139">A reserved IP address is associated tooyour subscription.</span></span>
5. <span data-ttu-id="ce7e6-140">È possibile usare gli indirizzi IP riservati con reti virtuali basate su gruppi di affinità?</span><span class="sxs-lookup"><span data-stu-id="ce7e6-140">Can I use a reserved IP with affinity group-based VNets?</span></span> <br>
    <span data-ttu-id="ce7e6-141">No.</span><span class="sxs-lookup"><span data-stu-id="ce7e6-141">No.</span></span> <span data-ttu-id="ce7e6-142">Gli indirizzi IP riservati sono supportati solo nelle reti virtuali di area.</span><span class="sxs-lookup"><span data-stu-id="ce7e6-142">Reserved IPs are only supported in regional VNets.</span></span> <span data-ttu-id="ce7e6-143">Gli indirizzi IP riservati non sono supportati per le reti virtuali associate a gruppi di affinità.</span><span class="sxs-lookup"><span data-stu-id="ce7e6-143">Reserved IPs are not supported for VNets that are associated with affinity groups.</span></span> <span data-ttu-id="ce7e6-144">Per ulteriori informazioni sull'associazione di una rete virtuale con un'area o un gruppo di affinità, vedere hello [sulle reti e i gruppi di affinità](virtual-networks-migrate-to-regional-vnet.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="ce7e6-144">For more information about associating a VNet with a region or affinity group, see hello [About Regional VNets and Affinity Groups](virtual-networks-migrate-to-regional-vnet.md) article.</span></span>

## <a name="manage-reserved-vips"></a><span data-ttu-id="ce7e6-145">Gestire gli indirizzi VIP riservati</span><span class="sxs-lookup"><span data-stu-id="ce7e6-145">Manage reserved VIPs</span></span>

<span data-ttu-id="ce7e6-146">Assicurarsi di aver installato e configurato PowerShell completando i passaggi hello hello [installare e configurare PowerShell](/powershell/azure/overview) articolo.</span><span class="sxs-lookup"><span data-stu-id="ce7e6-146">Ensure you have installed and configured PowerShell by completing hello steps in hello [Install and configure PowerShell](/powershell/azure/overview) article.</span></span> 

<span data-ttu-id="ce7e6-147">Prima di poter utilizzare gli indirizzi IP riservati, è necessario aggiungere tooyour sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="ce7e6-147">Before you can use reserved IPs, you must add it tooyour subscription.</span></span> <span data-ttu-id="ce7e6-148">un indirizzo IP dal pool hello dell'indirizzo IP pubblico riservato toocreate indirizzi disponibili in hello *centrale Usa* percorso, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="ce7e6-148">toocreate a reserved IP from hello pool of public IP addresses available in hello *Central US* location, run hello following command:</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"
```

<span data-ttu-id="ce7e6-149">Si noti tuttavia che non è possibile specificare quale indirizzo IP riservare.</span><span class="sxs-lookup"><span data-stu-id="ce7e6-149">Notice, however, that you cannot specify what IP is being reserved.</span></span> <span data-ttu-id="ce7e6-150">tooview quali indirizzi IP sono riservati nella sottoscrizione, eseguire dopo il comando di PowerShell, hello e osservare i valori hello per *ReservedIPName* e *indirizzo*:</span><span class="sxs-lookup"><span data-stu-id="ce7e6-150">tooview what IP addresses are reserved in your subscription, run hello following PowerShell command, and notice hello values for *ReservedIPName* and *Address*:</span></span>

```powershell
Get-AzureReservedIP
```

<span data-ttu-id="ce7e6-151">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="ce7e6-151">Expected output:</span></span>

    ReservedIPName       : MyReservedIP
    Address              : 23.101.114.211
    Id                   : d73be9dd-db12-4b5e-98c8-bc62e7c42041
    Label                :
    Location             : Central US
    State                : Created
    InUse                : False
    ServiceName          :
    DeploymentName       :
    OperationDescription : Get-AzureReservedIP
    OperationId          : 55e4f245-82e4-9c66-9bd8-273e815ce30a
    OperationStatus      : Succeeded

>[!NOTE]
><span data-ttu-id="ce7e6-152">Quando si crea un indirizzo IP riservato con PowerShell, è possibile specificare un indirizzo IP risorsa gruppo toocreate hello riservato in.</span><span class="sxs-lookup"><span data-stu-id="ce7e6-152">When you create a reserved IP address with PowerShell, you cannot specify a resource group toocreate hello reserved IP in.</span></span> <span data-ttu-id="ce7e6-153">Azure lo posiziona automaticamente in un gruppo di risorse denominato *Default-Networking*.</span><span class="sxs-lookup"><span data-stu-id="ce7e6-153">Azure places it into a resource group named *Default-Networking* automatically.</span></span> <span data-ttu-id="ce7e6-154">Se si crea l'IP riservato hello utilizzando hello [portale di Azure](http://portal.azure.com), è possibile specificare qualsiasi gruppo di risorse desiderato.</span><span class="sxs-lookup"><span data-stu-id="ce7e6-154">If you create hello reserved IP using hello [Azure portal](http://portal.azure.com), you can specify any resource group you choose.</span></span> <span data-ttu-id="ce7e6-155">Se si crea IP hello riservato in un gruppo di risorse diverso da *predefinito rete* , tuttavia, ogni volta che si fa riferimento hello IP riservato con i comandi, ad esempio `Get-AzureReservedIP` e `Remove-AzureReservedIP`, è necessario fare riferimento a nome hello *Resource-group-name riservato-ip-nome del gruppo*.</span><span class="sxs-lookup"><span data-stu-id="ce7e6-155">If you create hello reserved IP in a resource group other than *Default-Networking* however, whenever you reference hello reserved IP with commands such as `Get-AzureReservedIP` and `Remove-AzureReservedIP`, you must reference hello name *Group resource-group-name reserved-ip-name*.</span></span>  <span data-ttu-id="ce7e6-156">Ad esempio, se si crea un indirizzo IP riservato denominato *myReservedIP* in un gruppo di risorse denominato *myResourceGroup*, è necessario fare riferimento a nome hello dell'IP riservato hello come *myResourceGroup gruppo myReservedIP*.</span><span class="sxs-lookup"><span data-stu-id="ce7e6-156">For example, if you create a reserved IP named *myReservedIP* in a resource group named *myResourceGroup*, you must reference hello name of hello reserved IP as *Group myResourceGroup myReservedIP*.</span></span>   

<span data-ttu-id="ce7e6-157">Una volta che un indirizzo IP riservato, rimane associato tooyour sottoscrizione fino a quando non viene eliminato.</span><span class="sxs-lookup"><span data-stu-id="ce7e6-157">Once an IP is reserved, it remains associated tooyour subscription until you delete it.</span></span> <span data-ttu-id="ce7e6-158">toodelete un indirizzo IP riservato, hello esecuzione comando PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="ce7e6-158">toodelete a reserved IP, run hello following PowerShell command:</span></span>

```powershell
Remove-AzureReservedIP -ReservedIPName "MyReservedIP"
```

## <a name="reserve-hello-ip-address-of-an-existing-cloud-service"></a><span data-ttu-id="ce7e6-159">Riservare hello di indirizzo IP di un servizio cloud esistente</span><span class="sxs-lookup"><span data-stu-id="ce7e6-159">Reserve hello IP address of an existing cloud service</span></span>
<span data-ttu-id="ce7e6-160">È possibile riservare un indirizzo IP hello di un servizio cloud esistente aggiungendo hello `-ServiceName` parametro.</span><span class="sxs-lookup"><span data-stu-id="ce7e6-160">You can reserve hello IP address of an existing cloud service by adding hello `-ServiceName` parameter.</span></span> <span data-ttu-id="ce7e6-161">indirizzo IP di hello tooreserve di un servizio cloud *TestService* in hello *centrale Usa* percorso, eseguire il comando PowerShell seguente hello:</span><span class="sxs-lookup"><span data-stu-id="ce7e6-161">tooreserve hello IP address of a cloud service *TestService* in hello *Central US* location, run hello following PowerShell command:</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US" -ServiceName TestService
```

## <a name="associate-a-reserved-ip-tooa-new-cloud-service"></a><span data-ttu-id="ce7e6-162">Associare un riservato IP tooa nuovo servizio cloud</span><span class="sxs-lookup"><span data-stu-id="ce7e6-162">Associate a reserved IP tooa new cloud service</span></span>
<span data-ttu-id="ce7e6-163">Hello lo script seguente crea un indirizzo IP riservato nuovo, quindi associa tooa nuovo servizio cloud denominato *TestService*.</span><span class="sxs-lookup"><span data-stu-id="ce7e6-163">hello following script creates a new reserved IP, then associates it tooa new cloud service named *TestService*.</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService -ReservedIPName MyReservedIP -Location "Central US"
```

> [!NOTE]
> <span data-ttu-id="ce7e6-164">Quando si crea un toouse IP riservato con un servizio cloud, si continuerà a fare riferimento toohello VM utilizzando *VIP:&lt;il numero di porta >* per le comunicazioni in ingresso.</span><span class="sxs-lookup"><span data-stu-id="ce7e6-164">When you create a reserved IP toouse with a cloud service, you still refer toohello VM by using *VIP:&lt;port number>* for inbound communication.</span></span> <span data-ttu-id="ce7e6-165">Riservare un indirizzo IP non significa che è possibile connettersi direttamente toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ce7e6-165">Reserving an IP does not mean you can connect toohello VM directly.</span></span> <span data-ttu-id="ce7e6-166">Hello IP riservato viene assegnato toohello cloud servizio che hello macchina virtuale è stata distribuita.</span><span class="sxs-lookup"><span data-stu-id="ce7e6-166">hello reserved IP is assigned toohello cloud service that hello VM has been deployed to.</span></span> <span data-ttu-id="ce7e6-167">Se si desidera tooconnect tooa macchina virtuale con l'IP direttamente, è necessario tooconfigure un indirizzo IP pubblico a livello di istanza.</span><span class="sxs-lookup"><span data-stu-id="ce7e6-167">If you want tooconnect tooa VM by IP directly, you have tooconfigure an instance-level public IP.</span></span> <span data-ttu-id="ce7e6-168">Un indirizzo IP pubblico a livello di istanza è un tipo di indirizzo IP pubblico (chiamato un ILPIP) assegnato direttamente tooyour macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ce7e6-168">An instance-level public IP is a type of public IP (called an ILPIP) that is assigned directly tooyour VM.</span></span> <span data-ttu-id="ce7e6-169">Non può essere riservato.</span><span class="sxs-lookup"><span data-stu-id="ce7e6-169">It cannot be reserved.</span></span> <span data-ttu-id="ce7e6-170">Per altre informazioni, vedere hello [IP pubblico a livello di istanza (ILPIP)](virtual-networks-instance-level-public-ip.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="ce7e6-170">For more information, read hello [Instance-level Public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) article.</span></span>
> 

## <a name="remove-a-reserved-ip-from-a-running-deployment"></a><span data-ttu-id="ce7e6-171">Rimuovere un indirizzo IP riservato da una distribuzione in esecuzione</span><span class="sxs-lookup"><span data-stu-id="ce7e6-171">Remove a reserved IP from a running deployment</span></span>
<span data-ttu-id="ce7e6-172">un indirizzo IP riservato tooremove aggiunto tooa nuovo servizio cloud, eseguire il comando PowerShell seguente hello:</span><span class="sxs-lookup"><span data-stu-id="ce7e6-172">tooremove a reserved IP added tooa new cloud service, run hello following PowerShell command:</span></span>

```powershell
Remove-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService
```

> [!NOTE]
> <span data-ttu-id="ce7e6-173">Rimozione di un indirizzo IP riservato da una distribuzione in esecuzione non rimuovere la prenotazione hello dalla sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="ce7e6-173">Removing a reserved IP from a running deployment does not remove hello reservation from your subscription.</span></span> <span data-ttu-id="ce7e6-174">Libera semplicemente hello IP toobe utilizzato da un'altra risorsa nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="ce7e6-174">It simply frees hello IP toobe used by another resource in your subscription.</span></span>
> 

## <a name="associate-a-reserved-ip-tooa-running-deployment"></a><span data-ttu-id="ce7e6-175">Associare un tooa IP riservato in esecuzione la distribuzione</span><span class="sxs-lookup"><span data-stu-id="ce7e6-175">Associate a reserved IP tooa running deployment</span></span>
<span data-ttu-id="ce7e6-176">i comandi seguenti Hello creano un servizio cloud denominato *TestService2* con una nuova macchina virtuale denominata *TestVM2*.</span><span class="sxs-lookup"><span data-stu-id="ce7e6-176">hello following commands create a cloud service named *TestService2* with a new VM named *TestVM2*.</span></span> <span data-ttu-id="ce7e6-177">Hello esistente riservato IP denominato *MyReservedIP* viene quindi associato toohello servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="ce7e6-177">hello existing reserved IP named *MyReservedIP* is then associated toohello cloud service.</span></span>

```powershell
$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM2 -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService2 -Location "Central US"

Set-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService2
```

## <a name="associate-a-reserved-ip-tooa-cloud-service-by-using-a-service-configuration-file"></a><span data-ttu-id="ce7e6-178">Associare un servizio cloud di tooa IP riservato con un file di configurazione del servizio</span><span class="sxs-lookup"><span data-stu-id="ce7e6-178">Associate a reserved IP tooa cloud service by using a service configuration file</span></span>
<span data-ttu-id="ce7e6-179">È anche possibile associare un servizio cloud di tooa IP riservato usando un file di configurazione (CSCFG) del servizio.</span><span class="sxs-lookup"><span data-stu-id="ce7e6-179">You can also associate a reserved IP tooa cloud service by using a service configuration (CSCFG) file.</span></span> <span data-ttu-id="ce7e6-180">Hello xml di esempio seguente viene illustrato come tooconfigure un toouse servizio cloud un VIP riservato denominati *MyReservedIP*:</span><span class="sxs-lookup"><span data-stu-id="ce7e6-180">hello following sample xml shows how tooconfigure a cloud service toouse a reserved VIP named *MyReservedIP*:</span></span>

    <?xml version="1.0" encoding="utf-8"?>
    <ServiceConfiguration serviceName="ReservedIPSample" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="4" osVersion="*" schemaVersion="2014-01.2.3">
      <Role name="WebRole1">
        <Instances count="1" />
        <ConfigurationSettings>
          <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
        </ConfigurationSettings>
      </Role>
      <NetworkConfiguration>
        <AddressAssignments>
          <ReservedIPs>
           <ReservedIP name="MyReservedIP"/>
          </ReservedIPs>
        </AddressAssignments>
      </NetworkConfiguration>
    </ServiceConfiguration>

## <a name="next-steps"></a><span data-ttu-id="ce7e6-181">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ce7e6-181">Next steps</span></span>
* <span data-ttu-id="ce7e6-182">Comprendere come [gli indirizzi IP](virtual-network-ip-addresses-overview-classic.md) funziona nel modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="ce7e6-182">Understand how [IP addressing](virtual-network-ip-addresses-overview-classic.md) works in hello classic deployment model.</span></span>
* <span data-ttu-id="ce7e6-183">Informazioni su [indirizzi IP privati riservati](virtual-networks-reserved-private-ip.md).</span><span class="sxs-lookup"><span data-stu-id="ce7e6-183">Learn about [reserved private IP addresses](virtual-networks-reserved-private-ip.md).</span></span>
* <span data-ttu-id="ce7e6-184">Informazioni su [indirizzo IP pubblico a livello di istanza (ILPIP)](virtual-networks-instance-level-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="ce7e6-184">Learn about [Instance Level Public IP (ILPIP) addresses](virtual-networks-instance-level-public-ip.md).</span></span>

