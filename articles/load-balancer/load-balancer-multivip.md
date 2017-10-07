---
title: aaaMutiple VIP per un servizio cloud
description: "Panoramica di più indirizzi VIP e come tooset più indirizzi VIP in un servizio cloud"
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
ms.openlocfilehash: b3e0f2b24968cb75a7064484a09ffe94505bb70b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-multiple-vips-for-a-cloud-service"></a><span data-ttu-id="c7b05-103">Configurare più indirizzi VIP per un servizio cloud</span><span class="sxs-lookup"><span data-stu-id="c7b05-103">Configure multiple VIPs for a cloud service</span></span>

<span data-ttu-id="c7b05-104">È possibile accedere a servizi cloud di Azure su hello rete Internet pubblica utilizzando un indirizzo IP fornito da Azure.</span><span class="sxs-lookup"><span data-stu-id="c7b05-104">You can access Azure cloud services over hello public Internet by using an IP address provided by Azure.</span></span> <span data-ttu-id="c7b05-105">Questo indirizzo IP pubblico è tooas di cui si fa riferimento un indirizzo VIP (virtual IP) perché è collegata toohello Azure bilanciamento del carico e non hello istanze di macchina virtuale (VM) all'interno del servizio cloud hello.</span><span class="sxs-lookup"><span data-stu-id="c7b05-105">This public IP address is referred tooas a VIP (virtual IP) since it is linked toohello Azure load balancer, and not hello Virtual Machine (VM) instances within hello cloud service.</span></span> <span data-ttu-id="c7b05-106">È possibile accedere a qualsiasi istanza di macchina virtuale in un servizio cloud usando un singolo indirizzo VIP.</span><span class="sxs-lookup"><span data-stu-id="c7b05-106">You can access any VM instance within a cloud service by using a single VIP.</span></span>

<span data-ttu-id="c7b05-107">Tuttavia, esistono scenari in cui potrebbe essere necessario più di un indirizzo VIP come un toohello del punto di ingresso stesso servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="c7b05-107">However, there are scenarios in which you may need more than one VIP as an entry point toohello same cloud service.</span></span> <span data-ttu-id="c7b05-108">Ad esempio, il servizio cloud può ospitare più siti Web che richiedono una connettività SSL Usa hello porta predefinita 443, ogni sito è ospitato per un altro cliente o del tenant.</span><span class="sxs-lookup"><span data-stu-id="c7b05-108">For instance, your cloud service may host multiple websites that require SSL connectivity using hello default port of 443, as each site is hosted for a different customer, or tenant.</span></span> <span data-ttu-id="c7b05-109">In questo scenario, è necessario toohave un diverso indirizzo IP pubblico per ogni sito Web.</span><span class="sxs-lookup"><span data-stu-id="c7b05-109">In this scenario, you need toohave a different public facing IP address for each website.</span></span> <span data-ttu-id="c7b05-110">Hello diagramma seguente viene illustrato un tipico web multi-tenant che ospita con la necessità per certificati SSL multiple in hello stessa porta pubblica.</span><span class="sxs-lookup"><span data-stu-id="c7b05-110">hello diagram below illustrates a typical multi-tenant web hosting with a need for multiple SSL certificates on hello same public port.</span></span>

![Scenario SSL con più indirizzi VIP](./media/load-balancer-multivip/Figure1.png)

<span data-ttu-id="c7b05-112">Nell'esempio riportato sopra, tutti gli indirizzi VIP utilizzare hello hello stessa porta pubblica (443) e il traffico viene reindirizzato tooone o più carico bilanciate macchine virtuali su una porta privata univoca per l'indirizzo IP interno hello del servizio cloud hello hello tutti i siti Web di hosting.</span><span class="sxs-lookup"><span data-stu-id="c7b05-112">In hello example above, all VIPs use hello same public port (443) and traffic is redirected tooone or more load balanced VMs on a unique private port for hello internal IP address of hello cloud service hosting all hello websites.</span></span>

> [!NOTE]
> <span data-ttu-id="c7b05-113">Utilizzare hello di un'altra situazione che richiede hello più indirizzi VIP ospita più listener del gruppo di disponibilità AlwaysOn SQL in hello stesso insieme di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="c7b05-113">Another situation requiring hello use hello multiple VIPs is hosting multiple SQL AlwaysOn availability group listeners on hello same set of Virtual Machines.</span></span>

<span data-ttu-id="c7b05-114">Gli indirizzi VIP sono dinamici per impostazione predefinita, il che significa che l'indirizzo IP effettivo hello assegnato servizio cloud toohello potrebbe cambiare nel tempo.</span><span class="sxs-lookup"><span data-stu-id="c7b05-114">VIPs are dynamic by default, which means that hello actual IP address assigned toohello cloud service may change over time.</span></span> <span data-ttu-id="c7b05-115">tooprevent che accada, è possibile riservare un indirizzo VIP per il servizio.</span><span class="sxs-lookup"><span data-stu-id="c7b05-115">tooprevent that from happening, you can reserve a VIP for your service.</span></span> <span data-ttu-id="c7b05-116">toolearn ulteriori informazioni su indirizzi VIP riservati, vedere [indirizzo IP pubblico riservato](../virtual-network/virtual-networks-reserved-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="c7b05-116">toolearn more about reserved VIPs, see [Reserved Public IP](../virtual-network/virtual-networks-reserved-public-ip.md).</span></span>

> [!NOTE]
> <span data-ttu-id="c7b05-117">Per informazioni sui prezzi di indirizzi VIP e IP riservati, vedere [Prezzi per gli indirizzi IP](https://azure.microsoft.com/pricing/details/ip-addresses/) .</span><span class="sxs-lookup"><span data-stu-id="c7b05-117">Please see [IP Address pricing](https://azure.microsoft.com/pricing/details/ip-addresses/) for information on pricing on VIPs and reserved IPs.</span></span>

<span data-ttu-id="c7b05-118">È possibile utilizzare PowerShell tooverify hello VIP utilizzato dai servizi cloud, nonché aggiungere e rimuovere gli indirizzi VIP, associare un endpoint tooan VIP e configurare uno specifico VIP bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="c7b05-118">You can use PowerShell tooverify hello VIPs used by your cloud services, as well as add and remove VIPs, associate a VIP tooan endpoint, and configure load balancing on a specific VIP.</span></span>

## <a name="limitations"></a><span data-ttu-id="c7b05-119">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="c7b05-119">Limitations</span></span>

<span data-ttu-id="c7b05-120">A questo punto, funzionalità di più VIP è limitato toohello seguenti scenari:</span><span class="sxs-lookup"><span data-stu-id="c7b05-120">At this time, Multi VIP functionality is limited toohello following scenarios:</span></span>

* <span data-ttu-id="c7b05-121">**Solo IaaS**.</span><span class="sxs-lookup"><span data-stu-id="c7b05-121">**IaaS only**.</span></span> <span data-ttu-id="c7b05-122">È possibile abilitare più indirizzi VIP per servizi cloud che contengono le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="c7b05-122">You can only enable Multi VIP for cloud services that contain VMs.</span></span> <span data-ttu-id="c7b05-123">Non è possibile usare più indirizzi VIP negli scenari PaaS con le istanze del ruolo.</span><span class="sxs-lookup"><span data-stu-id="c7b05-123">You cannot use Multi VIP in PaaS scenarios with role instances.</span></span>
* <span data-ttu-id="c7b05-124">**Solo PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="c7b05-124">**PowerShell only**.</span></span> <span data-ttu-id="c7b05-125">È possibile gestire più indirizzi VIP solo con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c7b05-125">You can only manage Multi VIP by using PowerShell.</span></span>

<span data-ttu-id="c7b05-126">Queste limitazioni sono temporanee e possono cambiare in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="c7b05-126">These limitations are temporary, and may change at any time.</span></span> <span data-ttu-id="c7b05-127">Consentire toorevisit che questa pagina tooverify eventuali modifiche future.</span><span class="sxs-lookup"><span data-stu-id="c7b05-127">Make sure toorevisit this page tooverify future changes.</span></span>

## <a name="how-tooadd-a-vip-tooa-cloud-service"></a><span data-ttu-id="c7b05-128">Come servizio cloud tooa tooadd un indirizzo VIP</span><span class="sxs-lookup"><span data-stu-id="c7b05-128">How tooadd a VIP tooa cloud service</span></span>
<span data-ttu-id="c7b05-129">servizio tooyour tooadd un indirizzo VIP, eseguire il comando PowerShell seguente hello:</span><span class="sxs-lookup"><span data-stu-id="c7b05-129">tooadd a VIP tooyour service, run hello following PowerShell command:</span></span>

```powershell
Add-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

<span data-ttu-id="c7b05-130">Questo comando Visualizza un toohello simile di risultati seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="c7b05-130">This command displays a result similar toohello following sample:</span></span>

    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    Add-AzureVirtualIP   4bd7b638-d2e7-216f-ba38-5221233d70ce Succeeded

## <a name="how-tooremove-a-vip-from-a-cloud-service"></a><span data-ttu-id="c7b05-131">Come tooremove un indirizzo IP virtuale da un servizio cloud</span><span class="sxs-lookup"><span data-stu-id="c7b05-131">How tooremove a VIP from a cloud service</span></span>
<span data-ttu-id="c7b05-132">hello tooremove VIP aggiunto tooyour servizio nell'esempio hello sopra, hello esecuzione comando PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="c7b05-132">tooremove hello VIP added tooyour service in hello example above, run hello following PowerShell command:</span></span>

```powershell
Remove-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

> [!IMPORTANT]
> <span data-ttu-id="c7b05-133">È possibile rimuovere un indirizzo VIP solo se non dispone di alcun tooit endpoint associato.</span><span class="sxs-lookup"><span data-stu-id="c7b05-133">You can only remove a VIP if it has no endpoints associated tooit.</span></span>


## <a name="how-tooretrieve-vip-information-from-a-cloud-service"></a><span data-ttu-id="c7b05-134">Come tooretrieve VIP informazioni da un servizio Cloud</span><span class="sxs-lookup"><span data-stu-id="c7b05-134">How tooretrieve VIP information from a Cloud Service</span></span>
<span data-ttu-id="c7b05-135">hello tooretrieve VIP associata a un servizio cloud, eseguire lo script di PowerShell seguente hello:</span><span class="sxs-lookup"><span data-stu-id="c7b05-135">tooretrieve hello VIPs associated with a cloud service, run hello following PowerShell script:</span></span>

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

<span data-ttu-id="c7b05-136">script Hello Visualizza un toohello simile di risultati seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="c7b05-136">hello script displays a result similar toohello following sample:</span></span>

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

<span data-ttu-id="c7b05-137">In questo esempio, un servizio cloud hello è 3 VIP:</span><span class="sxs-lookup"><span data-stu-id="c7b05-137">In this example, hello cloud service has 3 VIPs:</span></span>

* <span data-ttu-id="c7b05-138">**Vip1** è hello VIP predefinito, si è certi che perché hello IsDnsProgrammedName è impostato tootrue.</span><span class="sxs-lookup"><span data-stu-id="c7b05-138">**Vip1** is hello default VIP, you know that because hello value for IsDnsProgrammedName is set tootrue.</span></span>
* <span data-ttu-id="c7b05-139">**Vip2** e **Vip3** non sono in uso in quanto non dispongono di indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="c7b05-139">**Vip2** and **Vip3** are not used as they do not have any IP addresses.</span></span> <span data-ttu-id="c7b05-140">Poter essere utilizzati solo se si associa un toohello endpoint VIP.</span><span class="sxs-lookup"><span data-stu-id="c7b05-140">They will only be used if you associate an endpoint toohello VIP.</span></span>

> [!NOTE]
> <span data-ttu-id="c7b05-141">Gli indirizzi VIP aggiuntivi verranno addebitati alla sottoscrizione solo dopo essere stati associati a un endpoint.</span><span class="sxs-lookup"><span data-stu-id="c7b05-141">Your subscription will only be charged for extra VIPs once they are associated with an endpoint.</span></span> <span data-ttu-id="c7b05-142">Per altre informazioni sui prezzi, vedere [Prezzi per gli indirizzi IP](https://azure.microsoft.com/pricing/details/ip-addresses/).</span><span class="sxs-lookup"><span data-stu-id="c7b05-142">For more information on pricing, see [IP Address pricing](https://azure.microsoft.com/pricing/details/ip-addresses/).</span></span>

## <a name="how-tooassociate-a-vip-tooan-endpoint"></a><span data-ttu-id="c7b05-143">Come endpoint tooan tooassociate un indirizzo VIP</span><span class="sxs-lookup"><span data-stu-id="c7b05-143">How tooassociate a VIP tooan endpoint</span></span>

<span data-ttu-id="c7b05-144">tooassociate un indirizzo IP virtuale nel cloud tooan endpoint del servizio eseguire hello comando PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="c7b05-144">tooassociate a VIP on a cloud service tooan endpoint, run hello following PowerShell command:</span></span>

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -Protocol tcp -LocalPort 8080 -PublicPort 80 -VirtualIPName Vip2 |
    Update-AzureVM
```

<span data-ttu-id="c7b05-145">comando Hello crea un endpoint denominato toohello collegato VIP *Vip2* sulla porta *80*e lo collega toohello macchina virtuale denominata *myVM1* in un servizio cloud denominato  *myService* utilizzando *TCP* sulla porta *8080*.</span><span class="sxs-lookup"><span data-stu-id="c7b05-145">hello command creates an endpoint linked toohello VIP called *Vip2* on port *80*, and links it toohello VM named *myVM1* in a cloud service named *myService* using *TCP* on port *8080*.</span></span>

<span data-ttu-id="c7b05-146">configurazione di hello tooverify, eseguire il comando PowerShell seguente hello:</span><span class="sxs-lookup"><span data-stu-id="c7b05-146">tooverify hello configuration, run hello following PowerShell command:</span></span>

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

<span data-ttu-id="c7b05-147">output di Hello è simile toohello esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="c7b05-147">hello output looks similar toohello following example:</span></span>

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

## <a name="how-tooenable-load-balancing-on-a-specific-vip"></a><span data-ttu-id="c7b05-148">Come tooenable il bilanciamento del carico in un indirizzo IP virtuale specifico</span><span class="sxs-lookup"><span data-stu-id="c7b05-148">How tooenable load balancing on a specific VIP</span></span>

<span data-ttu-id="c7b05-149">È possibile associare un singolo indirizzo VIP a più macchine virtuali per scopi di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="c7b05-149">You can associate a single VIP with multiple virtual machines for load balancing purposes.</span></span> <span data-ttu-id="c7b05-150">Si supponga, ad esempio, di disporre di un servizio cloud denominato *myService* e di due macchine virtuali denominate *myVM1* e *myVM2*.</span><span class="sxs-lookup"><span data-stu-id="c7b05-150">For example, you have a cloud service named *myService*, and two virtual machines named *myVM1* and *myVM2*.</span></span> <span data-ttu-id="c7b05-151">Il servizio cloud dispone di più indirizzi VIP, uno dei quali è denominato *Vip2*.</span><span class="sxs-lookup"><span data-stu-id="c7b05-151">And your cloud service has multiple VIPs, one of them named *Vip2*.</span></span> <span data-ttu-id="c7b05-152">Se si desidera che tutto il traffico tooport tooensure *81* su *Vip2* viene bilanciato tra *myVM1* e *myVM2* sulla porta *8181* eseguire hello seguente script di PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c7b05-152">If you want tooensure that all traffic tooport *81* on *Vip2* is balanced between *myVM1* and *myVM2* on port *8181*, run hello following PowerShell script:</span></span>

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2 -DefaultProbe |
    Update-AzureVM

Get-AzureVM -ServiceName myService -Name myVM2 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2  -DefaultProbe |
    Update-AzureVM
```

<span data-ttu-id="c7b05-153">È inoltre possibile aggiornare toouse di bilanciamento del carico un VIP diverso.</span><span class="sxs-lookup"><span data-stu-id="c7b05-153">You can also update your load balancer toouse a different VIP.</span></span> <span data-ttu-id="c7b05-154">Ad esempio, se si esegue hello comando PowerShell riportato di seguito, si modificherà set toouse un VIP denominato Vip1 di bilanciamento del carico di hello:</span><span class="sxs-lookup"><span data-stu-id="c7b05-154">For example, if you run hello PowerShell command below, you will change hello load balancing set toouse a VIP named Vip1:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName myService -LBSetName myLBSet -VirtualIPName Vip1
```

## <a name="next-steps"></a><span data-ttu-id="c7b05-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c7b05-155">Next Steps</span></span>

[<span data-ttu-id="c7b05-156">Log Analytics per Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="c7b05-156">Log analytics for Azure Load Balance</span></span>](load-balancer-monitor-log.md)

[<span data-ttu-id="c7b05-157">Panoramica del bilanciamento del carico Internet</span><span class="sxs-lookup"><span data-stu-id="c7b05-157">Internet facing load balancer overview</span></span>](load-balancer-internet-overview.md)

[<span data-ttu-id="c7b05-158">Introduzione al bilanciamento del carico Internet</span><span class="sxs-lookup"><span data-stu-id="c7b05-158">Get started on Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="c7b05-159">Panoramica di Rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="c7b05-159">Virtual Network Overview</span></span>](../virtual-network/virtual-networks-overview.md)

[<span data-ttu-id="c7b05-160">API REST di IP riservati</span><span class="sxs-lookup"><span data-stu-id="c7b05-160">Reserved IP REST APIs</span></span>](https://msdn.microsoft.com/library/azure/dn722420.aspx)
