---
title: Indirizzi VIP multipli per un servizio cloud
description: "Panoramica dell'uso di indirizzi VIP multipli e delle modalità di impostazione di più indirizzi VIP in un servizio cloud"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: 85f6d26a-3df5-4b8e-96a1-92b2793b5284
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: f40e0501eed8d5f296e7c79d8a35705a695ae6fd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="configure-multiple-vips-for-a-cloud-service"></a><span data-ttu-id="5e8d3-103">Configurare più indirizzi VIP per un servizio cloud</span><span class="sxs-lookup"><span data-stu-id="5e8d3-103">Configure multiple VIPs for a cloud service</span></span>

<span data-ttu-id="5e8d3-104">È possibile accedere ai servizi cloud di Azure tramite la rete Internet pubblica usando un indirizzo IP fornito da Azure.</span><span class="sxs-lookup"><span data-stu-id="5e8d3-104">You can access Azure cloud services over the public Internet by using an IP address provided by Azure.</span></span> <span data-ttu-id="5e8d3-105">Questo indirizzo IP pubblico è detto indirizzo VIP (Virtual IP, IP virtuale) poiché è collegato al bilanciamento del carico di Azure e non alle istanze di macchine virtuali (VM) nel servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="5e8d3-105">This public IP address is referred to as a VIP (virtual IP) since it is linked to the Azure load balancer, and not the Virtual Machine (VM) instances within the cloud service.</span></span> <span data-ttu-id="5e8d3-106">È possibile accedere a qualsiasi istanza di macchina virtuale in un servizio cloud usando un singolo indirizzo VIP.</span><span class="sxs-lookup"><span data-stu-id="5e8d3-106">You can access any VM instance within a cloud service by using a single VIP.</span></span>

<span data-ttu-id="5e8d3-107">Vi sono tuttavia scenari in cui potrebbe essere necessario più di un indirizzo VIP come punto di ingresso allo stesso servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="5e8d3-107">However, there are scenarios in which you may need more than one VIP as an entry point to the same cloud service.</span></span> <span data-ttu-id="5e8d3-108">Ad esempio, il servizio cloud può ospitare più siti Web che richiedono connettività SSL tramite la porta predefinita 443, poiché ogni sito è ospitato per un cliente o un tenant diverso.</span><span class="sxs-lookup"><span data-stu-id="5e8d3-108">For instance, your cloud service may host multiple websites that require SSL connectivity using the default port of 443, as each site is hosted for a different customer, or tenant.</span></span> <span data-ttu-id="5e8d3-109">In questo scenario è necessario disporre di un indirizzo IP pubblico diverso per ogni sito Web.</span><span class="sxs-lookup"><span data-stu-id="5e8d3-109">In this scenario, you need to have a different public facing IP address for each website.</span></span> <span data-ttu-id="5e8d3-110">Il diagramma seguente illustra un tipico caso di hosting Web multi-tenant che richiede più certificati SSL sulla stessa porta pubblica.</span><span class="sxs-lookup"><span data-stu-id="5e8d3-110">The diagram below illustrates a typical multi-tenant web hosting with a need for multiple SSL certificates on the same public port.</span></span>

![Scenario SSL con più indirizzi VIP](./media/load-balancer-multivip/Figure1.png)

<span data-ttu-id="5e8d3-112">Nell'esempio qui sopra tutti gli indirizzi VIP usano la stessa porta pubblica (443) e il traffico viene reindirizzato a una o più VM con carico bilanciato su una porta privata univoca per l'indirizzo IP interno del servizio cloud che ospita tutti i siti Web.</span><span class="sxs-lookup"><span data-stu-id="5e8d3-112">In the example above, all VIPs use the same public port (443) and traffic is redirected to one or more load balanced VMs on a unique private port for the internal IP address of the cloud service hosting all the websites.</span></span>

> [!NOTE]
> <span data-ttu-id="5e8d3-113">Un'altra situazione che richiede l'uso di più indirizzi VIP è costituito dall'hosting di più listener del gruppo di disponibilità SQL AlwaysOn nello stesso set di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="5e8d3-113">Another situation requiring the use the multiple VIPs is hosting multiple SQL AlwaysOn availability group listeners on the same set of Virtual Machines.</span></span>

<span data-ttu-id="5e8d3-114">Gli indirizzi VIP sono dinamici per impostazione predefinita e ciò significa che l'indirizzo IP effettivo assegnato al servizio cloud potrebbe cambiare nel tempo.</span><span class="sxs-lookup"><span data-stu-id="5e8d3-114">VIPs are dynamic by default, which means that the actual IP address assigned to the cloud service may change over time.</span></span> <span data-ttu-id="5e8d3-115">Per impedire che ciò accada, è possibile riservare un indirizzo VIP per il servizio.</span><span class="sxs-lookup"><span data-stu-id="5e8d3-115">To prevent that from happening, you can reserve a VIP for your service.</span></span> <span data-ttu-id="5e8d3-116">Per altre informazioni sugli indirizzi VIP riservati, vedere [IP pubblico riservato](../virtual-network/virtual-networks-reserved-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="5e8d3-116">To learn more about reserved VIPs, see [Reserved Public IP](../virtual-network/virtual-networks-reserved-public-ip.md).</span></span>

> [!NOTE]
> <span data-ttu-id="5e8d3-117">Per informazioni sui prezzi di indirizzi VIP e IP riservati, vedere [Prezzi per gli indirizzi IP](https://azure.microsoft.com/pricing/details/ip-addresses/) .</span><span class="sxs-lookup"><span data-stu-id="5e8d3-117">Please see [IP Address pricing](https://azure.microsoft.com/pricing/details/ip-addresses/) for information on pricing on VIPs and reserved IPs.</span></span>

<span data-ttu-id="5e8d3-118">È possibile usare PowerShell per verificare gli indirizzi VIP usati dai servizi cloud, nonché per aggiungere e rimuovere indirizzi VIP, associare un indirizzo VIP a un endpoint e configurare il bilanciamento del carico su un indirizzo VIP specifico.</span><span class="sxs-lookup"><span data-stu-id="5e8d3-118">You can use PowerShell to verify the VIPs used by your cloud services, as well as add and remove VIPs, associate a VIP to an endpoint, and configure load balancing on a specific VIP.</span></span>

## <a name="limitations"></a><span data-ttu-id="5e8d3-119">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="5e8d3-119">Limitations</span></span>

<span data-ttu-id="5e8d3-120">A questo punto, la funzionalità con più indirizzi VIP è limitata agli scenari seguenti:</span><span class="sxs-lookup"><span data-stu-id="5e8d3-120">At this time, Multi VIP functionality is limited to the following scenarios:</span></span>

* <span data-ttu-id="5e8d3-121">**Solo IaaS**.</span><span class="sxs-lookup"><span data-stu-id="5e8d3-121">**IaaS only**.</span></span> <span data-ttu-id="5e8d3-122">È possibile abilitare più indirizzi VIP per servizi cloud che contengono le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="5e8d3-122">You can only enable Multi VIP for cloud services that contain VMs.</span></span> <span data-ttu-id="5e8d3-123">Non è possibile usare più indirizzi VIP negli scenari PaaS con le istanze del ruolo.</span><span class="sxs-lookup"><span data-stu-id="5e8d3-123">You cannot use Multi VIP in PaaS scenarios with role instances.</span></span>
* <span data-ttu-id="5e8d3-124">**Solo PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="5e8d3-124">**PowerShell only**.</span></span> <span data-ttu-id="5e8d3-125">È possibile gestire più indirizzi VIP solo con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5e8d3-125">You can only manage Multi VIP by using PowerShell.</span></span>

<span data-ttu-id="5e8d3-126">Queste limitazioni sono temporanee e possono cambiare in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="5e8d3-126">These limitations are temporary, and may change at any time.</span></span> <span data-ttu-id="5e8d3-127">Assicurarsi di visualizzare nuovamente questa pagina per verificare le modifiche future.</span><span class="sxs-lookup"><span data-stu-id="5e8d3-127">Make sure to revisit this page to verify future changes.</span></span>

## <a name="how-to-add-a-vip-to-a-cloud-service"></a><span data-ttu-id="5e8d3-128">Come aggiungere un indirizzo VIP a un servizio cloud</span><span class="sxs-lookup"><span data-stu-id="5e8d3-128">How to add a VIP to a cloud service</span></span>
<span data-ttu-id="5e8d3-129">Per aggiungere un indirizzo VIP al servizio, eseguire il comando PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="5e8d3-129">To add a VIP to your service, run the following PowerShell command:</span></span>

```powershell
Add-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

<span data-ttu-id="5e8d3-130">Questo comando visualizza un risultato simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="5e8d3-130">This command displays a result similar to the following sample:</span></span>

    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    Add-AzureVirtualIP   4bd7b638-d2e7-216f-ba38-5221233d70ce Succeeded

## <a name="how-to-remove-a-vip-from-a-cloud-service"></a><span data-ttu-id="5e8d3-131">Come rimuovere un indirizzo VIP da un servizio cloud</span><span class="sxs-lookup"><span data-stu-id="5e8d3-131">How to remove a VIP from a cloud service</span></span>
<span data-ttu-id="5e8d3-132">Per rimuovere l'indirizzo VIP aggiunto al servizio nell'esempio precedente, eseguire il comando PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="5e8d3-132">To remove the VIP added to your service in the example above, run the following PowerShell command:</span></span>

```powershell
Remove-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

> [!IMPORTANT]
> <span data-ttu-id="5e8d3-133">È possibile rimuovere un indirizzo VIP solo se non dispone di alcun endpoint associato.</span><span class="sxs-lookup"><span data-stu-id="5e8d3-133">You can only remove a VIP if it has no endpoints associated to it.</span></span>


## <a name="how-to-retrieve-vip-information-from-a-cloud-service"></a><span data-ttu-id="5e8d3-134">Come recuperare informazioni sugli indirizzi VIP da un servizio cloud</span><span class="sxs-lookup"><span data-stu-id="5e8d3-134">How to retrieve VIP information from a Cloud Service</span></span>
<span data-ttu-id="5e8d3-135">Per recuperare gli indirizzi VIP associati a un servizio cloud, eseguire lo script di PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="5e8d3-135">To retrieve the VIPs associated with a cloud service, run the following PowerShell script:</span></span>

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

<span data-ttu-id="5e8d3-136">Lo script visualizza un risultato simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="5e8d3-136">The script displays a result similar to the following sample:</span></span>

    Address         : 191.238.74.148
    IsDnsProgrammed : True
    Name            : Vip1
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip2
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip3
    ReservedIPName  :
    ExtensionData   :

<span data-ttu-id="5e8d3-137">In questo esempio il servizio cloud dispone di 3 indirizzi VIP:</span><span class="sxs-lookup"><span data-stu-id="5e8d3-137">In this example, the cloud service has 3 VIPs:</span></span>

* <span data-ttu-id="5e8d3-138">**Vip1** è l'indirizzo VIP predefinito. Ciò è indicato dall'impostazione di IsDnsProgrammedName su true.</span><span class="sxs-lookup"><span data-stu-id="5e8d3-138">**Vip1** is the default VIP, you know that because the value for IsDnsProgrammedName is set to true.</span></span>
* <span data-ttu-id="5e8d3-139">**Vip2** e **Vip3** non sono in uso in quanto non dispongono di indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="5e8d3-139">**Vip2** and **Vip3** are not used as they do not have any IP addresses.</span></span> <span data-ttu-id="5e8d3-140">Verranno usati solo se si associa un endpoint all'indirizzo VIP.</span><span class="sxs-lookup"><span data-stu-id="5e8d3-140">They will only be used if you associate an endpoint to the VIP.</span></span>

> [!NOTE]
> <span data-ttu-id="5e8d3-141">Gli indirizzi VIP aggiuntivi verranno addebitati alla sottoscrizione solo dopo essere stati associati a un endpoint.</span><span class="sxs-lookup"><span data-stu-id="5e8d3-141">Your subscription will only be charged for extra VIPs once they are associated with an endpoint.</span></span> <span data-ttu-id="5e8d3-142">Per altre informazioni sui prezzi, vedere [Prezzi per gli indirizzi IP](https://azure.microsoft.com/pricing/details/ip-addresses/).</span><span class="sxs-lookup"><span data-stu-id="5e8d3-142">For more information on pricing, see [IP Address pricing](https://azure.microsoft.com/pricing/details/ip-addresses/).</span></span>

## <a name="how-to-associate-a-vip-to-an-endpoint"></a><span data-ttu-id="5e8d3-143">Come associare un indirizzo VIP a un endpoint</span><span class="sxs-lookup"><span data-stu-id="5e8d3-143">How to associate a VIP to an endpoint</span></span>

<span data-ttu-id="5e8d3-144">Per associare un indirizzo VIP in un servizio cloud a un endpoint, eseguire il comando PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="5e8d3-144">To associate a VIP on a cloud service to an endpoint, run the following PowerShell command:</span></span>

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -Protocol tcp -LocalPort 8080 -PublicPort 80 -VirtualIPName Vip2 |
    Update-AzureVM
```

<span data-ttu-id="5e8d3-145">Il comando crea un endpoint collegato all'indirizzo VIP denominato *Vip2* sulla porta *80* e lo collega alla VM denominata *myVM1* in un servizio cloud denominato *myService* usando il protocollo *TCP* sulla porta *8080*.</span><span class="sxs-lookup"><span data-stu-id="5e8d3-145">The command creates an endpoint linked to the VIP called *Vip2* on port *80*, and links it to the VM named *myVM1* in a cloud service named *myService* using *TCP* on port *8080*.</span></span>

<span data-ttu-id="5e8d3-146">Per verificare la configurazione, eseguire il comando PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="5e8d3-146">To verify the configuration, run the following PowerShell command:</span></span>

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

<span data-ttu-id="5e8d3-147">L'output è simile al seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="5e8d3-147">The output looks similar to the following example:</span></span>

    Address         : 191.238.74.148
    IsDnsProgrammed : True
    Name            : Vip1
    ReservedIPName  :
    ExtensionData   :

    Address         : 191.238.74.13
    IsDnsProgrammed :
    Name            : Vip2
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip3
    ReservedIPName  :
    ExtensionData   :

## <a name="how-to-enable-load-balancing-on-a-specific-vip"></a><span data-ttu-id="5e8d3-148">Come abilitare il bilanciamento del carico per un indirizzo VIP specifico</span><span class="sxs-lookup"><span data-stu-id="5e8d3-148">How to enable load balancing on a specific VIP</span></span>

<span data-ttu-id="5e8d3-149">È possibile associare un singolo indirizzo VIP a più macchine virtuali per scopi di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="5e8d3-149">You can associate a single VIP with multiple virtual machines for load balancing purposes.</span></span> <span data-ttu-id="5e8d3-150">Si supponga, ad esempio, di disporre di un servizio cloud denominato *myService* e di due macchine virtuali denominate *myVM1* e *myVM2*.</span><span class="sxs-lookup"><span data-stu-id="5e8d3-150">For example, you have a cloud service named *myService*, and two virtual machines named *myVM1* and *myVM2*.</span></span> <span data-ttu-id="5e8d3-151">Il servizio cloud dispone di più indirizzi VIP, uno dei quali è denominato *Vip2*.</span><span class="sxs-lookup"><span data-stu-id="5e8d3-151">And your cloud service has multiple VIPs, one of them named *Vip2*.</span></span> <span data-ttu-id="5e8d3-152">Se si desidera fare in modo che tutto il traffico verso la porta *81* su *Vip2* venga sottoposto a bilanciamento del carico tra *myVM1* e *myVM2* sulla porta *8181*, eseguire lo script di PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="5e8d3-152">If you want to ensure that all traffic to port *81* on *Vip2* is balanced between *myVM1* and *myVM2* on port *8181*, run the following PowerShell script:</span></span>

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2 -DefaultProbe |
    Update-AzureVM

Get-AzureVM -ServiceName myService -Name myVM2 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2  -DefaultProbe |
    Update-AzureVM
```

<span data-ttu-id="5e8d3-153">È anche possibile aggiornare il bilanciamento del carico per usare un indirizzo VIP diverso.</span><span class="sxs-lookup"><span data-stu-id="5e8d3-153">You can also update your load balancer to use a different VIP.</span></span> <span data-ttu-id="5e8d3-154">Ad esempio, se si esegue il comando PowerShell seguente, si modifica il set di bilanciamento del carico in modo che venga usato un indirizzo VIP denominato Vip1:</span><span class="sxs-lookup"><span data-stu-id="5e8d3-154">For example, if you run the PowerShell command below, you will change the load balancing set to use a VIP named Vip1:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName myService -LBSetName myLBSet -VirtualIPName Vip1
```

## <a name="next-steps"></a><span data-ttu-id="5e8d3-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5e8d3-155">Next Steps</span></span>

[<span data-ttu-id="5e8d3-156">Log Analytics per Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="5e8d3-156">Log analytics for Azure Load Balance</span></span>](load-balancer-monitor-log.md)

[<span data-ttu-id="5e8d3-157">Panoramica del bilanciamento del carico Internet</span><span class="sxs-lookup"><span data-stu-id="5e8d3-157">Internet facing load balancer overview</span></span>](load-balancer-internet-overview.md)

[<span data-ttu-id="5e8d3-158">Introduzione al bilanciamento del carico Internet</span><span class="sxs-lookup"><span data-stu-id="5e8d3-158">Get started on Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="5e8d3-159">Panoramica di Rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="5e8d3-159">Virtual Network Overview</span></span>](../virtual-network/virtual-networks-overview.md)

[<span data-ttu-id="5e8d3-160">API REST di IP riservati</span><span class="sxs-lookup"><span data-stu-id="5e8d3-160">Reserved IP REST APIs</span></span>](https://msdn.microsoft.com/library/azure/dn722420.aspx)
