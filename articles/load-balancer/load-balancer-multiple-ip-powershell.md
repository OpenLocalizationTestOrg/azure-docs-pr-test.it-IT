---
title: "bilanciamento del carico su più configurazioni IP in Azure aaaLoad | Documenti Microsoft"
description: Bilanciamento del carico tra configurazioni IP primarie e secondarie.
services: load-balancer
documentationcenter: na
author: anavinahar
manager: narayan
editor: na
ms.assetid: 244907cd-b275-4494-aaf7-dcfc4d93edfe
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: annahar
ms.openlocfilehash: fe1cdb317350942ff759229491c2025e98dd24a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="load-balancing-on-multiple-ip-configurations-using-powershell"></a><span data-ttu-id="3ddf0-103">Bilanciamento del carico in più configurazioni IP tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="3ddf0-103">Load balancing on multiple IP configurations using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="3ddf0-104">Portale</span><span class="sxs-lookup"><span data-stu-id="3ddf0-104">Portal</span></span>](load-balancer-multiple-ip.md)
> * [<span data-ttu-id="3ddf0-105">CLI</span><span class="sxs-lookup"><span data-stu-id="3ddf0-105">CLI</span></span>](load-balancer-multiple-ip-cli.md)
> * [<span data-ttu-id="3ddf0-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3ddf0-106">PowerShell</span></span>](load-balancer-multiple-ip-powershell.md)

<span data-ttu-id="3ddf0-107">In questo articolo viene descritto come indirizzi di bilanciamento del carico di Azure con più IP toouse su un'interfaccia di rete secondaria (NIC).</span><span class="sxs-lookup"><span data-stu-id="3ddf0-107">This article describes how toouse Azure Load Balancer with multiple IP addresses on a secondary network interface (NIC).</span></span> <span data-ttu-id="3ddf0-108">Per questo scenario sono disponibili due VM con Windows, ognuna con una scheda di interfaccia di rete primaria e secondaria.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-108">For this scenario, we have two VMs running Windows, each with a primary and a secondary NIC.</span></span> <span data-ttu-id="3ddf0-109">Ognuno di hello secondario schede di rete dispone di due configurazioni IP.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-109">Each of hello secondary NICs have two IP configurations.</span></span> <span data-ttu-id="3ddf0-110">Ogni macchina virtuale ospita entrambi i siti Web: contoso.com e fabrikam.com. Ogni sito Web è associato tooone delle configurazioni IP hello sulla hello di rete secondaria.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-110">Each VM hosts both websites contoso.com and fabrikam.com. Each website is bound tooone of hello IP configurations on hello secondary NIC.</span></span> <span data-ttu-id="3ddf0-111">Utilizziamo bilanciamento del carico di Azure tooexpose due front-end indirizzi IP, una per ogni sito Web, toodistribute traffico toohello rispettiva configurazione IP per il sito Web di hello.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-111">We use Azure Load Balancer tooexpose two frontend IP addresses, one for each website, toodistribute traffic toohello respective IP configuration for hello website.</span></span> <span data-ttu-id="3ddf0-112">Questo scenario utilizza hello stesso numero di porta tra i server front-end, così come entrambi indirizzi IP del pool back-end.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-112">This scenario uses hello same port number across both frontends, as well as both backend pool IP addresses.</span></span>

![Immagine dello scenario LB](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

## <a name="steps-tooload-balance-on-multiple-ip-configurations"></a><span data-ttu-id="3ddf0-114">Saldo tooload passaggi su più configurazioni IP</span><span class="sxs-lookup"><span data-stu-id="3ddf0-114">Steps tooload balance on multiple IP configurations</span></span>

<span data-ttu-id="3ddf0-115">Attenersi alla procedura hello seguente scenario hello tooachieve descritta in questo articolo:</span><span class="sxs-lookup"><span data-stu-id="3ddf0-115">Follow hello steps below tooachieve hello scenario outlined in this article:</span></span>

1. <span data-ttu-id="3ddf0-116">Installare Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-116">Install Azure PowerShell.</span></span> <span data-ttu-id="3ddf0-117">Vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) per informazioni sull'installazione hello la versione più recente di Azure PowerShell, selezionando la sottoscrizione e la firma nell'account tooyour.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-117">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for information about installing hello latest version of Azure PowerShell, selecting your subscription, and signing in tooyour account.</span></span>
2. <span data-ttu-id="3ddf0-118">Creare un gruppo di risorse utilizzando hello seguenti impostazioni:</span><span class="sxs-lookup"><span data-stu-id="3ddf0-118">Create a resource group using hello following settings:</span></span>

    ```powershell
    $location = "westcentralus".
    $myResourceGroup = "contosofabrikam"
    ```

    <span data-ttu-id="3ddf0-119">Per altre informazioni, vedere il passaggio 2 dell'articolo relativo alla [creazione di un gruppo di risorse](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3ddf0-119">For more information, see Step 2 of [Create a Resource Group](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span></span>

3. <span data-ttu-id="3ddf0-120">[Creare un Set di disponibilità](../virtual-machines/windows/tutorial-availability-sets.md?toc=%2fazure%2fload-balancer%2ftoc.json) toocontain le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-120">[Create an Availability Set](../virtual-machines/windows/tutorial-availability-sets.md?toc=%2fazure%2fload-balancer%2ftoc.json) toocontain your VMs.</span></span> <span data-ttu-id="3ddf0-121">Per questo scenario, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="3ddf0-121">For this scenario, use hello following command:</span></span>

    ```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "contosofabrikam" -Name "myAvailset" -Location "West Central US"
    ```

4. <span data-ttu-id="3ddf0-122">Seguire i passaggi da istruzioni 3 a 5 [creare una macchina virtuale Windows](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) articolo Creazione hello tooprepare di una macchina virtuale con una singola scheda di rete.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-122">Follow instructions steps 3 through 5 in [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) article tooprepare hello creation of a VM with a single NIC.</span></span> <span data-ttu-id="3ddf0-123">Eseguire passaggio 6.1 e utilizzare i seguenti hello anziché passaggio 6.2:</span><span class="sxs-lookup"><span data-stu-id="3ddf0-123">Execute step 6.1, and use hello following instead of step 6.2:</span></span>

    ```powershell
    $availset = Get-AzureRmAvailabilitySet -ResourceGroupName "contosofabrikam" -Name "myAvailset"
    New-AzureRmVMConfig -VMName "VM1" -VMSize "Standard_DS1_v2" -AvailabilitySetId $availset.Id
    ```

    <span data-ttu-id="3ddf0-124">Completare quindi i passaggi da 6.3 a 6.8 dell'articolo [Creare una VM Windows](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3ddf0-124">Then complete [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) steps 6.3 through 6.8.</span></span>

5. <span data-ttu-id="3ddf0-125">Aggiungere un secondo tooeach di configurazione IP di hello macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-125">Add a second IP configuration tooeach of hello VMs.</span></span> <span data-ttu-id="3ddf0-126">Seguire le istruzioni hello [assegnare più indirizzi IP macchine toovirtual](../virtual-network/virtual-network-multiple-ip-addresses-powershell.md#add) articolo.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-126">Follow hello instructions in [Assign multiple IP addresses toovirtual machines](../virtual-network/virtual-network-multiple-ip-addresses-powershell.md#add) article.</span></span> <span data-ttu-id="3ddf0-127">Utilizzare hello le impostazioni di configurazione seguente:</span><span class="sxs-lookup"><span data-stu-id="3ddf0-127">Use hello following configuration settings:</span></span>

    ```powershell
    $NicName = "VM1-NIC2"
    $RgName = "contosofabrikam"
    $NicLocation = "West Central US"
    $IPConfigName4 = "VM1-ipconfig2"
    $Subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "mySubnet" -VirtualNetwork $myVnet
    ```

    <span data-ttu-id="3ddf0-128">Non è necessario tooassociate hello secondaria le configurazioni IP con indirizzi IP pubblici a scopo di hello di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-128">You do not need tooassociate hello secondary IP configurations with public IPs for hello purpose of this tutorial.</span></span> <span data-ttu-id="3ddf0-129">Modificare hello comando tooremove hello pubblica IP associazione parte.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-129">Edit hello command tooremove hello public IP association part.</span></span>

6. <span data-ttu-id="3ddf0-130">Completare nuovamente i passaggi da 4 a 6 di questo articolo per VM2.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-130">Complete steps 4 through 6 of this article again for VM2.</span></span> <span data-ttu-id="3ddf0-131">In tal caso, essere tooreplace che hello VM nome tooVM2.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-131">Be sure tooreplace hello VM name tooVM2 when doing this.</span></span> <span data-ttu-id="3ddf0-132">Si noti che non è necessaria una rete virtuale toocreate per hello seconda macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-132">Note that you do not need toocreate a virtual network for hello second VM.</span></span> <span data-ttu-id="3ddf0-133">È possibile scegliere se creare o meno una nuova subnet in base al caso d'uso.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-133">You may or may not create a new subnet based on your use case.</span></span>

7. <span data-ttu-id="3ddf0-134">Creare due indirizzi IP pubblici e memorizzarli in variabili appropriate hello, come illustrato:</span><span class="sxs-lookup"><span data-stu-id="3ddf0-134">Create two public IP addresses and store them in hello appropriate variables as shown:</span></span>

    ```powershell
    $publicIP1 = New-AzureRmPublicIpAddress -Name PublicIp1 -ResourceGroupName contosofabrikam -Location 'West Central US' -AllocationMethod Dynamic -DomainNameLabel contoso
    $publicIP2 = New-AzureRmPublicIpAddress -Name PublicIp2 -ResourceGroupName contosofabrikam -Location 'West Central US' -AllocationMethod Dynamic -DomainNameLabel fabrikam

    $publicIP1 = Get-AzureRmPublicIpAddress -Name PublicIp1 -ResourceGroupName contosofabrikam
    $publicIP2 = Get-AzureRmPublicIpAddress -Name PublicIp2 -ResourceGroupName contosofabrikam
    ```

8. <span data-ttu-id="3ddf0-135">Creare due configurazioni IP front-end:</span><span class="sxs-lookup"><span data-stu-id="3ddf0-135">Create two frontend IP configurations:</span></span>

    ```powershell
    $frontendIP1 = New-AzureRmLoadBalancerFrontendIpConfig -Name contosofe -PublicIpAddress $publicIP1
    $frontendIP2 = New-AzureRmLoadBalancerFrontendIpConfig -Name fabrikamfe -PublicIpAddress $publicIP2
    ```

9. <span data-ttu-id="3ddf0-136">Creare i pool di indirizzi back-end, un probe e regole di bilanciamento del carico:</span><span class="sxs-lookup"><span data-stu-id="3ddf0-136">Create your backend address pools, a probe, and your load balancing rules:</span></span>

    ```powershell
    $beaddresspool1 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name contosopool
    $beaddresspool2 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name fabrikampool

    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HTTP -RequestPath 'index.html' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

    $lbrule1 = New-AzureRmLoadBalancerRuleConfig -Name HTTPc -FrontendIpConfiguration $frontendIP1 -BackendAddressPool $beaddresspool1 -Probe $healthprobe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    $lbrule2 = New-AzureRmLoadBalancerRuleConfig -Name HTTPf -FrontendIpConfiguration $frontendIP2 -BackendAddressPool $beaddresspool2 -Probe $healthprobe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    ```

10. <span data-ttu-id="3ddf0-137">Dopo aver creato queste risorse, creare il servizio di bilanciamento del carico:</span><span class="sxs-lookup"><span data-stu-id="3ddf0-137">Once you have these resources created, create your load balancer:</span></span>

    ```powershell
    $mylb = New-AzureRmLoadBalancer -ResourceGroupName contosofabrikam -Name mylb -Location 'West Central US' -FrontendIpConfiguration $frontendIP1 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
    ```

11. <span data-ttu-id="3ddf0-138">Aggiungere hello secondo back-end indirizzo front-end e pool IP configurazione appena creato tooyour bilanciamento del carico:</span><span class="sxs-lookup"><span data-stu-id="3ddf0-138">Add hello second backend address pool and frontend IP configuration tooyour newly created load balancer:</span></span>

    ```powershell
    $mylb = Get-AzureRmLoadBalancer -Name "mylb" -ResourceGroupName $myResourceGroup | Add-AzureRmLoadBalancerBackendAddressPoolConfig -Name fabrikampool | Set-AzureRmLoadBalancer

    $mylb | Add-AzureRmLoadBalancerFrontendIpConfig -Name fabrikamfe -PublicIpAddress $publicIP2 | Set-AzureRmLoadBalancer
    
    Add-AzureRmLoadBalancerRuleConfig -Name HTTP -LoadBalancer $mylb -FrontendIpConfiguration $frontendIP2 -BackendAddressPool $beaddresspool2 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80 | Set-AzureRmLoadBalancer
    ```

12. <span data-ttu-id="3ddf0-139">comandi Hello seguenti ottenere hello NIC e quindi aggiungere che entrambe le configurazioni IP ogni secondario NIC toohello back-end del pool di indirizzi di hello bilanciamento del carico:</span><span class="sxs-lookup"><span data-stu-id="3ddf0-139">hello commands below get hello NICs and then add both IP configurations of each secondary NIC toohello backend address pool of hello load balancer:</span></span>

    ```powershell
    $nic1 = Get-AzureRmNetworkInterface -Name "VM1-NIC2" -ResourceGroupName "MyResourcegroup";
    $nic2 = Get-AzureRmNetworkInterface -Name "VM2-NIC2" -ResourceGroupName "MyResourcegroup";

    $nic1.IpConfigurations[0].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[0]);
    $nic1.IpConfigurations[1].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[1]);
    $nic2.IpConfigurations[0].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[0]);
    $nic2.IpConfigurations[1].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[1]);

    $mylb = $mylb | Set-AzureRmLoadBalancer

    $nic1 | Set-AzureRmNetworkInterface
    $nic2 | Set-AzureRmNetworkInterface
    ```

13. <span data-ttu-id="3ddf0-140">Infine, è necessario configurare resource record toopoint toohello front-end rispettivi indirizzo IP del DNS hello bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-140">Finally, you must configure DNS resource records toopoint toohello respective frontend IP address of hello Load Balancer.</span></span> <span data-ttu-id="3ddf0-141">È possibile ospitare i domini nel servizio DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="3ddf0-141">You may host your domains in Azure DNS.</span></span> <span data-ttu-id="3ddf0-142">Per altre informazioni sull'uso del servizio DNS di Azure con Azure Load Balancer, vedere [Uso del servizio DNS di Azure con altri servizi di Azure](../dns/dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="3ddf0-142">For more information about using Azure DNS with Load Balancer, see [Using Azure DNS with other Azure services](../dns/dns-for-azure-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3ddf0-143">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3ddf0-143">Next steps</span></span>
- <span data-ttu-id="3ddf0-144">Altre informazioni su come il bilanciamento del carico toocombine servizi in Azure in [utilizzando servizi di bilanciamento del carico in Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span><span class="sxs-lookup"><span data-stu-id="3ddf0-144">Learn more about how toocombine load balancing services in Azure in [Using load-balancing services in Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span></span>
- <span data-ttu-id="3ddf0-145">Informazioni su come è possibile utilizzare diversi tipi di registri in Azure toomanage e risolvere i problemi di bilanciamento del carico in [Log analitica per il bilanciamento del carico di Azure](../load-balancer/load-balancer-monitor-log.md).</span><span class="sxs-lookup"><span data-stu-id="3ddf0-145">Learn how you can use different types of logs in Azure toomanage and troubleshoot load balancer in [Log analytics for Azure Load Balancer](../load-balancer/load-balancer-monitor-log.md).</span></span>
