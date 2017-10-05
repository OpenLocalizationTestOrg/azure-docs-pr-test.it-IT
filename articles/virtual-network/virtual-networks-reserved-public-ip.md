---
title: Gestire gli indirizzi IP riservati di Azure (versione classica) - PowerShell | Microsoft Docs
description: Comprendere gli indirizzi IP riservati (classica) e come gestirli tramite PowerShell.
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
ms.openlocfilehash: 5e9c83cebec96c6bc8afd53b0c637d7af899746f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="reserved-ip-addresses-classic"></a><span data-ttu-id="dcfff-103">Indirizzi IP riservati (classica)</span><span class="sxs-lookup"><span data-stu-id="dcfff-103">Reserved IP addresses (Classic)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="dcfff-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="dcfff-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="dcfff-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dcfff-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="dcfff-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="dcfff-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="dcfff-107">Modello</span><span class="sxs-lookup"><span data-stu-id="dcfff-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * <span data-ttu-id="dcfff-108">[PowerShell (Classic)](virtual-networks-reserved-public-ip.md) (PowerShell (classico))</span><span class="sxs-lookup"><span data-stu-id="dcfff-108">[PowerShell (Classic)](virtual-networks-reserved-public-ip.md)</span></span>

<span data-ttu-id="dcfff-109">Gli indirizzi IP in Azure rientrano in due categorie: indirizzi dinamici e indirizzi riservati.</span><span class="sxs-lookup"><span data-stu-id="dcfff-109">IP addresses in Azure fall into two categories: dynamic and reserved.</span></span> <span data-ttu-id="dcfff-110">Gli indirizzi IP pubblici gestiti da Azure sono dinamici per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="dcfff-110">Public IP addresses managed by Azure are dynamic by default.</span></span> <span data-ttu-id="dcfff-111">Questo significa che l'indirizzo IP usato per un determinato servizio cloud (VIP) oppure per accedere direttamente a una macchina virtuale o a un'istanza del ruolo (ILPIP) può essere arrestato o interrotto (deallocato).</span><span class="sxs-lookup"><span data-stu-id="dcfff-111">That means that the IP address used for a given cloud service (VIP) or to access a VM or role instance directly (ILPIP) can change from time to time, when resources are shut down or stopped (deallocated).</span></span>

<span data-ttu-id="dcfff-112">Per impedire che gli indirizzi IP cambino, è possibile riservarli.</span><span class="sxs-lookup"><span data-stu-id="dcfff-112">To prevent IP addresses from changing, you can reserve an IP address.</span></span> <span data-ttu-id="dcfff-113">Gli indirizzi IP riservati possono essere usati solo come indirizzi VIP, pertanto assicurano che l'indirizzo IP per il servizio cloud resti invariato anche se le risorse vengono arrestate o interrotte (deallocate).</span><span class="sxs-lookup"><span data-stu-id="dcfff-113">Reserved IPs can be used only as a VIP, ensuring that the IP address for the cloud service remains the same, even as resources are shut down or stopped (deallocated).</span></span> <span data-ttu-id="dcfff-114">È inoltre possibile convertire in indirizzo IP riservato gli indirizzi IP dinamici esistenti usati come indirizzi VIP.</span><span class="sxs-lookup"><span data-stu-id="dcfff-114">Furthermore, you can convert existing dynamic IPs used as a VIP to a reserved IP address.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dcfff-115">Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="dcfff-115">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="dcfff-116">Questo articolo illustra l'uso del modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="dcfff-116">This article covers using the classic deployment model.</span></span> <span data-ttu-id="dcfff-117">Microsoft consiglia di usare il modello di Gestione risorse per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="dcfff-117">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="dcfff-118">Informazioni su come riservare un indirizzo IP pubblico statico usando [il modello di distribuzione di Resource Manager](virtual-network-ip-addresses-overview-arm.md).</span><span class="sxs-lookup"><span data-stu-id="dcfff-118">Learn how to reserve a static public IP address using the [Resource Manager deployment model](virtual-network-ip-addresses-overview-arm.md).</span></span>

<span data-ttu-id="dcfff-119">Per altre informazioni sugli indirizzi IP in Azure, leggere l'articolo sugli [indirizzi IP](virtual-network-ip-addresses-overview-classic.md).</span><span class="sxs-lookup"><span data-stu-id="dcfff-119">To learn more about IP addresses in Azure, read the [IP addresses](virtual-network-ip-addresses-overview-classic.md) article.</span></span>

## <a name="when-do-i-need-a-reserved-ip"></a><span data-ttu-id="dcfff-120">Quando è necessario un indirizzo IP riservato?</span><span class="sxs-lookup"><span data-stu-id="dcfff-120">When do I need a reserved IP?</span></span>
* <span data-ttu-id="dcfff-121">**Si vuole essere certi che l'indirizzo IP sia riservato nella sottoscrizione**.</span><span class="sxs-lookup"><span data-stu-id="dcfff-121">**You want to ensure that the IP is reserved in your subscription**.</span></span> <span data-ttu-id="dcfff-122">Se si intende riservare un indirizzo IP in modo che non venga rilasciato dalla sottoscrizione in alcuna circostanza, è consigliabile usare un indirizzo IP pubblico riservato.</span><span class="sxs-lookup"><span data-stu-id="dcfff-122">If you want to reserve an IP address that is not released from your subscription under any circumstance, you should use a reserved public IP.</span></span>  
* <span data-ttu-id="dcfff-123">**Si vuole che l'indirizzo IP resti associato al servizio cloud anche se lo stato delle macchine virtuali è arrestato o deallocato**.</span><span class="sxs-lookup"><span data-stu-id="dcfff-123">**You want your IP to stay with your cloud service even across stopped or deallocated state (VMs)**.</span></span> <span data-ttu-id="dcfff-124">Se si vuole che il servizio cloud sia accessibile mediante l'uso di un indirizzo IP che non cambia, anche se le macchine virtuali nel servizio cloud vengono arrestate o interrotte (deallocate).</span><span class="sxs-lookup"><span data-stu-id="dcfff-124">If you want your service to be accessed by using an IP address that doesn't change, even when VMs in the cloud service are shut down or stop (deallocated).</span></span>
* <span data-ttu-id="dcfff-125">**Si vuole essere certi che il traffico in uscita da Azure usi un indirizzo IP prevedibile**.</span><span class="sxs-lookup"><span data-stu-id="dcfff-125">**You want to ensure that outbound traffic from Azure uses a predictable IP address**.</span></span> <span data-ttu-id="dcfff-126">È possibile che il firewall locale sia configurato per consentire solo il traffico proveniente da indirizzi IP specifici.</span><span class="sxs-lookup"><span data-stu-id="dcfff-126">You may have your on-premises firewall configured to allow only traffic from specific IP addresses.</span></span> <span data-ttu-id="dcfff-127">Riservando un indirizzo IP, si conoscerà l'indirizzo IP di origine e non sarà necessario aggiornare le regole del firewall a seguito del cambiamento di indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="dcfff-127">By reserving an IP, you know the source IP address, and don't need to update your firewall rules due to an IP change.</span></span>

## <a name="faq"></a><span data-ttu-id="dcfff-128">domande frequenti</span><span class="sxs-lookup"><span data-stu-id="dcfff-128">FAQ</span></span>
1. <span data-ttu-id="dcfff-129">È possibile usare un indirizzo IP riservato per tutti i servizi di Azure?</span><span class="sxs-lookup"><span data-stu-id="dcfff-129">Can I use a reserved IP for all Azure services?</span></span> <br>
    <span data-ttu-id="dcfff-130">No.</span><span class="sxs-lookup"><span data-stu-id="dcfff-130">No.</span></span> <span data-ttu-id="dcfff-131">Gli indirizzi IP riservati possono essere usati solo per le macchine virtuali e per i ruoli delle istanze del servizio cloud esposti mediante un indirizzo VIP.</span><span class="sxs-lookup"><span data-stu-id="dcfff-131">Reserved IPs can only be used for VMs and cloud service instance roles exposed through a VIP.</span></span>
2. <span data-ttu-id="dcfff-132">Di quanti indirizzi IP riservati è possibile disporre?</span><span class="sxs-lookup"><span data-stu-id="dcfff-132">How many reserved IPs can I have?</span></span> <br>
    <span data-ttu-id="dcfff-133">Per informazioni dettagliate, vedere il [Azure limita](../azure-subscription-service-limits.md#networking-limits) articolo.</span><span class="sxs-lookup"><span data-stu-id="dcfff-133">For details, see the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
3. <span data-ttu-id="dcfff-134">È previsto un addebito per gli indirizzi IP riservati?</span><span class="sxs-lookup"><span data-stu-id="dcfff-134">Is there a charge for reserved IPs?</span></span> <br>
    <span data-ttu-id="dcfff-135">In alcuni casi sì.</span><span class="sxs-lookup"><span data-stu-id="dcfff-135">Sometimes.</span></span> <span data-ttu-id="dcfff-136">Per informazioni dettagliate sui prezzi, consultare la pagina [Prezzi per gli indirizzi IP riservati](http://go.microsoft.com/fwlink/?LinkID=398482).</span><span class="sxs-lookup"><span data-stu-id="dcfff-136">For pricing details, see the [Reserved IP Address Pricing Details](http://go.microsoft.com/fwlink/?LinkID=398482) page.</span></span>
4. <span data-ttu-id="dcfff-137">Come è possibile riservare un indirizzo IP?</span><span class="sxs-lookup"><span data-stu-id="dcfff-137">How do I reserve an IP address?</span></span> <br>
    <span data-ttu-id="dcfff-138">È possibile usare PowerShell, la [API REST di gestione di Azure](https://msdn.microsoft.com/library/azure/dn722420.aspx), o [portale di Azure](https://portal.azure.com) per riservare un indirizzo IP in un'area di Azure.</span><span class="sxs-lookup"><span data-stu-id="dcfff-138">You can use PowerShell, the [Azure Management REST API](https://msdn.microsoft.com/library/azure/dn722420.aspx), or the [Azure portal](https://portal.azure.com) to reserve an IP address in an Azure region.</span></span> <span data-ttu-id="dcfff-139">Un indirizzo IP riservato è associato alla sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="dcfff-139">A reserved IP address is associated to your subscription.</span></span>
5. <span data-ttu-id="dcfff-140">È possibile usare gli indirizzi IP riservati con reti virtuali basate su gruppi di affinità?</span><span class="sxs-lookup"><span data-stu-id="dcfff-140">Can I use a reserved IP with affinity group-based VNets?</span></span> <br>
    <span data-ttu-id="dcfff-141">No.</span><span class="sxs-lookup"><span data-stu-id="dcfff-141">No.</span></span> <span data-ttu-id="dcfff-142">Gli indirizzi IP riservati sono supportati solo nelle reti virtuali di area.</span><span class="sxs-lookup"><span data-stu-id="dcfff-142">Reserved IPs are only supported in regional VNets.</span></span> <span data-ttu-id="dcfff-143">Gli indirizzi IP riservati non sono supportati per le reti virtuali associate a gruppi di affinità.</span><span class="sxs-lookup"><span data-stu-id="dcfff-143">Reserved IPs are not supported for VNets that are associated with affinity groups.</span></span> <span data-ttu-id="dcfff-144">Per altre informazioni sull'associazione di una rete virtuale a una regione o a un gruppo di affinità, vedere l'articolo sulle [reti virtuali dell'area e sui gruppi di affinità](virtual-networks-migrate-to-regional-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="dcfff-144">For more information about associating a VNet with a region or affinity group, see the [About Regional VNets and Affinity Groups](virtual-networks-migrate-to-regional-vnet.md) article.</span></span>

## <a name="manage-reserved-vips"></a><span data-ttu-id="dcfff-145">Gestire gli indirizzi VIP riservati</span><span class="sxs-lookup"><span data-stu-id="dcfff-145">Manage reserved VIPs</span></span>

<span data-ttu-id="dcfff-146">Verificare di aver installato e configurato Azure PowerShell eseguendo i passaggi descritti nell'articolo [Installare e configurare PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="dcfff-146">Ensure you have installed and configured PowerShell by completing the steps in the [Install and configure PowerShell](/powershell/azure/overview) article.</span></span> 

<span data-ttu-id="dcfff-147">Prima di poter usare gli indirizzi IP riservati, è necessario aggiungerli alla propria sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="dcfff-147">Before you can use reserved IPs, you must add it to your subscription.</span></span> <span data-ttu-id="dcfff-148">Per creare un indirizzo IP riservato dal pool di indirizzi IP pubblici disponibili nella posizione *Stati Uniti centrali*, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="dcfff-148">To create a reserved IP from the pool of public IP addresses available in the *Central US* location, run the following command:</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"
```

<span data-ttu-id="dcfff-149">Si noti tuttavia che non è possibile specificare quale indirizzo IP riservare.</span><span class="sxs-lookup"><span data-stu-id="dcfff-149">Notice, however, that you cannot specify what IP is being reserved.</span></span> <span data-ttu-id="dcfff-150">Per visualizzare gli indirizzi IP riservati nella propria sottoscrizione, eseguire il comando PowerShell seguente e osservare i valori per *ReservedIPName* e *Address*:</span><span class="sxs-lookup"><span data-stu-id="dcfff-150">To view what IP addresses are reserved in your subscription, run the following PowerShell command, and notice the values for *ReservedIPName* and *Address*:</span></span>

```powershell
Get-AzureReservedIP
```

<span data-ttu-id="dcfff-151">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="dcfff-151">Expected output:</span></span>

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
><span data-ttu-id="dcfff-152">Quando si crea un indirizzo IP riservato con PowerShell, non è possibile specificare un gruppo di risorse in cui creare l'indirizzo IP riservato.</span><span class="sxs-lookup"><span data-stu-id="dcfff-152">When you create a reserved IP address with PowerShell, you cannot specify a resource group to create the reserved IP in.</span></span> <span data-ttu-id="dcfff-153">Azure lo posiziona automaticamente in un gruppo di risorse denominato *Default-Networking*.</span><span class="sxs-lookup"><span data-stu-id="dcfff-153">Azure places it into a resource group named *Default-Networking* automatically.</span></span> <span data-ttu-id="dcfff-154">Se si crea l'indirizzo IP riservato usando il [portale Azure](http://portal.azure.com), è possibile specificare qualsiasi gruppo di risorse desiderato.</span><span class="sxs-lookup"><span data-stu-id="dcfff-154">If you create the reserved IP using the [Azure portal](http://portal.azure.com), you can specify any resource group you choose.</span></span> <span data-ttu-id="dcfff-155">Tuttavia, se si crea l'indirizzo IP riservato in un gruppo di risorse diverso da *Default-Networking*, quando si fa riferimento all'indirizzo IP riservato con comandi quali `Get-AzureReservedIP` e `Remove-AzureReservedIP`, è necessario fare riferimento al nome *Group resource-group-name reserved-ip-name*.</span><span class="sxs-lookup"><span data-stu-id="dcfff-155">If you create the reserved IP in a resource group other than *Default-Networking* however, whenever you reference the reserved IP with commands such as `Get-AzureReservedIP` and `Remove-AzureReservedIP`, you must reference the name *Group resource-group-name reserved-ip-name*.</span></span>  <span data-ttu-id="dcfff-156">Ad esempio, se si crea un indirizzo IP riservato denominato *myReservedIP* in un gruppo di risorse denominato *myResourceGroup*, è necessario fare riferimento al nome di un IP riservato come ad esempio *Group myResourceGroup myReservedIP*.</span><span class="sxs-lookup"><span data-stu-id="dcfff-156">For example, if you create a reserved IP named *myReservedIP* in a resource group named *myResourceGroup*, you must reference the name of the reserved IP as *Group myResourceGroup myReservedIP*.</span></span>   

<span data-ttu-id="dcfff-157">Dopo essere stato riservato, un indirizzo IP rimane associato alla sottoscrizione finché non viene eliminato.</span><span class="sxs-lookup"><span data-stu-id="dcfff-157">Once an IP is reserved, it remains associated to your subscription until you delete it.</span></span> <span data-ttu-id="dcfff-158">Per eliminare l'indirizzo IP riservato, eseguire il comando PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="dcfff-158">To delete a reserved IP, run the following PowerShell command:</span></span>

```powershell
Remove-AzureReservedIP -ReservedIPName "MyReservedIP"
```

## <a name="reserve-the-ip-address-of-an-existing-cloud-service"></a><span data-ttu-id="dcfff-159">Riservare l'indirizzo IP di un servizio cloud esistente</span><span class="sxs-lookup"><span data-stu-id="dcfff-159">Reserve the IP address of an existing cloud service</span></span>
<span data-ttu-id="dcfff-160">È possibile riservare l'indirizzo IP di un servizio cloud esistente aggiungendo il parametro `-ServiceName`.</span><span class="sxs-lookup"><span data-stu-id="dcfff-160">You can reserve the IP address of an existing cloud service by adding the `-ServiceName` parameter.</span></span> <span data-ttu-id="dcfff-161">Per riservare l'indirizzo IP di un servizio cloud *TestService* nella posizione *Stati Uniti centrali*, eseguire il comando PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="dcfff-161">To reserve the IP address of a cloud service *TestService* in the *Central US* location, run the following PowerShell command:</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US" -ServiceName TestService
```

## <a name="associate-a-reserved-ip-to-a-new-cloud-service"></a><span data-ttu-id="dcfff-162">Associare un indirizzo IP riservato a un nuovo servizio cloud</span><span class="sxs-lookup"><span data-stu-id="dcfff-162">Associate a reserved IP to a new cloud service</span></span>
<span data-ttu-id="dcfff-163">Lo script seguente crea un nuovo indirizzo IP riservato e quindi lo associa a un nuovo servizio cloud denominato *TestService*.</span><span class="sxs-lookup"><span data-stu-id="dcfff-163">The following script creates a new reserved IP, then associates it to a new cloud service named *TestService*.</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService -ReservedIPName MyReservedIP -Location "Central US"
```

> [!NOTE]
> <span data-ttu-id="dcfff-164">Quando si crea un indirizzo IP riservato da usare con un servizio cloud, è comunque necessario fare riferimento alla macchina virtuale tramite *VIP:&lt;numero porta>* per la comunicazione in ingresso.</span><span class="sxs-lookup"><span data-stu-id="dcfff-164">When you create a reserved IP to use with a cloud service, you still refer to the VM by using *VIP:&lt;port number>* for inbound communication.</span></span> <span data-ttu-id="dcfff-165">Il fatto di riservare un indirizzo IP non determina la possibilità di connettersi direttamente alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="dcfff-165">Reserving an IP does not mean you can connect to the VM directly.</span></span> <span data-ttu-id="dcfff-166">L'indirizzo IP riservato viene infatti assegnato al servizio cloud in cui è stata distribuita la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="dcfff-166">The reserved IP is assigned to the cloud service that the VM has been deployed to.</span></span> <span data-ttu-id="dcfff-167">Per connettersi direttamente a una macchina virtuale tramite indirizzo IP, è necessario configurare un indirizzo IP pubblico a livello di istanza.</span><span class="sxs-lookup"><span data-stu-id="dcfff-167">If you want to connect to a VM by IP directly, you have to configure an instance-level public IP.</span></span> <span data-ttu-id="dcfff-168">Si tratta di un tipo di indirizzo IP pubblico (denominato ILPIP) che viene assegnato direttamente alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="dcfff-168">An instance-level public IP is a type of public IP (called an ILPIP) that is assigned directly to your VM.</span></span> <span data-ttu-id="dcfff-169">Non può essere riservato.</span><span class="sxs-lookup"><span data-stu-id="dcfff-169">It cannot be reserved.</span></span> <span data-ttu-id="dcfff-170">Per altre informazioni, vedere l'articolo [IP pubblico a livello di istanza (ILPIP)](virtual-networks-instance-level-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="dcfff-170">For more information, read the [Instance-level Public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) article.</span></span>
> 

## <a name="remove-a-reserved-ip-from-a-running-deployment"></a><span data-ttu-id="dcfff-171">Rimuovere un indirizzo IP riservato da una distribuzione in esecuzione</span><span class="sxs-lookup"><span data-stu-id="dcfff-171">Remove a reserved IP from a running deployment</span></span>
<span data-ttu-id="dcfff-172">Per rimuovere un indirizzo IP riservato aggiunto a un nuovo servizio cloud, eseguire il comando PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="dcfff-172">To remove a reserved IP added to a new cloud service, run the following PowerShell command:</span></span>

```powershell
Remove-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService
```

> [!NOTE]
> <span data-ttu-id="dcfff-173">Rimuovendo un indirizzo IP riservato da una distribuzione in esecuzione, non si rimuove dalla sottoscrizione il fatto che sia riservato.</span><span class="sxs-lookup"><span data-stu-id="dcfff-173">Removing a reserved IP from a running deployment does not remove the reservation from your subscription.</span></span> <span data-ttu-id="dcfff-174">Si libera semplicemente l'indirizzo IP in modo che possa essere usato da un'altra risorsa nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="dcfff-174">It simply frees the IP to be used by another resource in your subscription.</span></span>
> 

## <a name="associate-a-reserved-ip-to-a-running-deployment"></a><span data-ttu-id="dcfff-175">Associare un indirizzo IP riservato a una distribuzione in esecuzione</span><span class="sxs-lookup"><span data-stu-id="dcfff-175">Associate a reserved IP to a running deployment</span></span>
<span data-ttu-id="dcfff-176">I seguenti comandi creano un servizio cloud denominato *TestService2* con una nuova macchina virtuale denominata *TestVM2*.</span><span class="sxs-lookup"><span data-stu-id="dcfff-176">The following commands create a cloud service named *TestService2* with a new VM named *TestVM2*.</span></span> <span data-ttu-id="dcfff-177">L'indirizzo IP riservato esistente denominato *MyReservedIP* viene quindi associato al servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="dcfff-177">The existing reserved IP named *MyReservedIP* is then associated to the cloud service.</span></span>

```powershell
$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM2 -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService2 -Location "Central US"

Set-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService2
```

## <a name="associate-a-reserved-ip-to-a-cloud-service-by-using-a-service-configuration-file"></a><span data-ttu-id="dcfff-178">Associare un indirizzo IP riservato a un servizio cloud usando un file cscfg</span><span class="sxs-lookup"><span data-stu-id="dcfff-178">Associate a reserved IP to a cloud service by using a service configuration file</span></span>
<span data-ttu-id="dcfff-179">È possibile anche associare un indirizzo IP riservato a un servizio cloud usando un file di configurazione del servizio (CSCFG).</span><span class="sxs-lookup"><span data-stu-id="dcfff-179">You can also associate a reserved IP to a cloud service by using a service configuration (CSCFG) file.</span></span> <span data-ttu-id="dcfff-180">Il file XML di esempio riportato di seguito illustra come configurare un servizio cloud per l'uso di un indirizzo VIP riservato denominato *MyReservedIP*:</span><span class="sxs-lookup"><span data-stu-id="dcfff-180">The following sample xml shows how to configure a cloud service to use a reserved VIP named *MyReservedIP*:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="dcfff-181">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dcfff-181">Next steps</span></span>
* <span data-ttu-id="dcfff-182">Informazioni sul funzionamento degli [indirizzi IP](virtual-network-ip-addresses-overview-classic.md) nel modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="dcfff-182">Understand how [IP addressing](virtual-network-ip-addresses-overview-classic.md) works in the classic deployment model.</span></span>
* <span data-ttu-id="dcfff-183">Informazioni su [indirizzi IP privati riservati](virtual-networks-reserved-private-ip.md).</span><span class="sxs-lookup"><span data-stu-id="dcfff-183">Learn about [reserved private IP addresses](virtual-networks-reserved-private-ip.md).</span></span>
* <span data-ttu-id="dcfff-184">Informazioni su [indirizzo IP pubblico a livello di istanza (ILPIP)](virtual-networks-instance-level-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="dcfff-184">Learn about [Instance Level Public IP (ILPIP) addresses](virtual-networks-instance-level-public-ip.md).</span></span>

