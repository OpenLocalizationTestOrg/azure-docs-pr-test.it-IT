---
title: "Bilanciamento del carico in più configurazioni IP in Azure | Microsoft Docs"
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
ms.openlocfilehash: a8550519f094ca7afcd868a14b313337627f97d3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="load-balancing-on-multiple-ip-configurations-using-powershell"></a><span data-ttu-id="49e7b-103">Bilanciamento del carico in più configurazioni IP tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="49e7b-103">Load balancing on multiple IP configurations using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="49e7b-104">Portale</span><span class="sxs-lookup"><span data-stu-id="49e7b-104">Portal</span></span>](load-balancer-multiple-ip.md)
> * [<span data-ttu-id="49e7b-105">CLI</span><span class="sxs-lookup"><span data-stu-id="49e7b-105">CLI</span></span>](load-balancer-multiple-ip-cli.md)
> * [<span data-ttu-id="49e7b-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="49e7b-106">PowerShell</span></span>](load-balancer-multiple-ip-powershell.md)

<span data-ttu-id="49e7b-107">Questo articolo descrive come usare Azure Load Balancer con più indirizzi IP su una scheda di interfaccia di rete secondaria.</span><span class="sxs-lookup"><span data-stu-id="49e7b-107">This article describes how to use Azure Load Balancer with multiple IP addresses on a secondary network interface (NIC).</span></span> <span data-ttu-id="49e7b-108">Per questo scenario sono disponibili due VM con Windows, ognuna con una scheda di interfaccia di rete primaria e secondaria.</span><span class="sxs-lookup"><span data-stu-id="49e7b-108">For this scenario, we have two VMs running Windows, each with a primary and a secondary NIC.</span></span> <span data-ttu-id="49e7b-109">Ogni scheda di interfaccia di rete secondaria dispone di due configurazioni di IP.</span><span class="sxs-lookup"><span data-stu-id="49e7b-109">Each of the secondary NICs have two IP configurations.</span></span> <span data-ttu-id="49e7b-110">Ogni macchina virtuale ospita entrambi i siti Web: contoso.com e fabrikam.com. Ogni sito Web è associato a una delle configurazioni IP della scheda di interfaccia di rete secondaria.</span><span class="sxs-lookup"><span data-stu-id="49e7b-110">Each VM hosts both websites contoso.com and fabrikam.com. Each website is bound to one of the IP configurations on the secondary NIC.</span></span> <span data-ttu-id="49e7b-111">Azure Load Balancer viene usato per esporre due indirizzi IP front-end, uno per ogni sito Web, per distribuire il traffico alla rispettiva configurazione IP per il sito Web.</span><span class="sxs-lookup"><span data-stu-id="49e7b-111">We use Azure Load Balancer to expose two frontend IP addresses, one for each website, to distribute traffic to the respective IP configuration for the website.</span></span> <span data-ttu-id="49e7b-112">Questo scenario usa lo stesso numero di porta per entrambi i front-end, nonché per entrambi gli indirizzi IP del pool back-end.</span><span class="sxs-lookup"><span data-stu-id="49e7b-112">This scenario uses the same port number across both frontends, as well as both backend pool IP addresses.</span></span>

![Immagine dello scenario LB](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

## <a name="steps-to-load-balance-on-multiple-ip-configurations"></a><span data-ttu-id="49e7b-114">Procedura per il bilanciamento del carico in più configurazioni IP</span><span class="sxs-lookup"><span data-stu-id="49e7b-114">Steps to load balance on multiple IP configurations</span></span>

<span data-ttu-id="49e7b-115">Per ottenere lo scenario descritto in questo articolo, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="49e7b-115">Follow the steps below to achieve the scenario outlined in this article:</span></span>

1. <span data-ttu-id="49e7b-116">Installare Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="49e7b-116">Install Azure PowerShell.</span></span> <span data-ttu-id="49e7b-117">Per informazioni su come installare la versione più recente di Azure PowerShell, selezionare la sottoscrizione e accedere all'account, vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="49e7b-117">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for information about installing the latest version of Azure PowerShell, selecting your subscription, and signing in to your account.</span></span>
2. <span data-ttu-id="49e7b-118">Creare un gruppo di risorse usando le impostazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="49e7b-118">Create a resource group using the following settings:</span></span>

    ```powershell
    $location = "westcentralus".
    $myResourceGroup = "contosofabrikam"
    ```

    <span data-ttu-id="49e7b-119">Per altre informazioni, vedere il passaggio 2 dell'articolo relativo alla [creazione di un gruppo di risorse](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="49e7b-119">For more information, see Step 2 of [Create a Resource Group](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span></span>

3. <span data-ttu-id="49e7b-120">[Creare un set di disponibilità](../virtual-machines/windows/tutorial-availability-sets.md?toc=%2fazure%2fload-balancer%2ftoc.json) che dovrà contenere le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="49e7b-120">[Create an Availability Set](../virtual-machines/windows/tutorial-availability-sets.md?toc=%2fazure%2fload-balancer%2ftoc.json) to contain your VMs.</span></span> <span data-ttu-id="49e7b-121">Per questo scenario, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="49e7b-121">For this scenario, use the following command:</span></span>

    ```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "contosofabrikam" -Name "myAvailset" -Location "West Central US"
    ```

4. <span data-ttu-id="49e7b-122">Seguire le istruzioni contenute nei passaggi da 3 a 5 dell'articolo [Creare una VM Windows](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) per preparare la creazione di una macchina virtuale con una scheda di interfaccia di rete singola.</span><span class="sxs-lookup"><span data-stu-id="49e7b-122">Follow instructions steps 3 through 5 in [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) article to prepare the creation of a VM with a single NIC.</span></span> <span data-ttu-id="49e7b-123">Eseguire il passaggio 6.1 e sostituire il comando del passaggio 6.2 con quanto segue:</span><span class="sxs-lookup"><span data-stu-id="49e7b-123">Execute step 6.1, and use the following instead of step 6.2:</span></span>

    ```powershell
    $availset = Get-AzureRmAvailabilitySet -ResourceGroupName "contosofabrikam" -Name "myAvailset"
    New-AzureRmVMConfig -VMName "VM1" -VMSize "Standard_DS1_v2" -AvailabilitySetId $availset.Id
    ```

    <span data-ttu-id="49e7b-124">Completare quindi i passaggi da 6.3 a 6.8 dell'articolo [Creare una VM Windows](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="49e7b-124">Then complete [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) steps 6.3 through 6.8.</span></span>

5. <span data-ttu-id="49e7b-125">Aggiungere una seconda configurazione IP a ognuna delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="49e7b-125">Add a second IP configuration to each of the VMs.</span></span> <span data-ttu-id="49e7b-126">Seguire le istruzioni contenute nell'articolo [Assegnare più indirizzi IP alle macchine virtuali](../virtual-network/virtual-network-multiple-ip-addresses-powershell.md#add).</span><span class="sxs-lookup"><span data-stu-id="49e7b-126">Follow the instructions in [Assign multiple IP addresses to virtual machines](../virtual-network/virtual-network-multiple-ip-addresses-powershell.md#add) article.</span></span> <span data-ttu-id="49e7b-127">Usare le impostazioni di configurazione seguenti:</span><span class="sxs-lookup"><span data-stu-id="49e7b-127">Use the following configuration settings:</span></span>

    ```powershell
    $NicName = "VM1-NIC2"
    $RgName = "contosofabrikam"
    $NicLocation = "West Central US"
    $IPConfigName4 = "VM1-ipconfig2"
    $Subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "mySubnet" -VirtualNetwork $myVnet
    ```

    <span data-ttu-id="49e7b-128">Ai fini di questa esercitazione, non è necessario associare le configurazioni IP secondarie agli indirizzi IP pubblici.</span><span class="sxs-lookup"><span data-stu-id="49e7b-128">You do not need to associate the secondary IP configurations with public IPs for the purpose of this tutorial.</span></span> <span data-ttu-id="49e7b-129">Modificare il comando per rimuovere la parte relativa all'associazione dell'indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="49e7b-129">Edit the command to remove the public IP association part.</span></span>

6. <span data-ttu-id="49e7b-130">Completare nuovamente i passaggi da 4 a 6 di questo articolo per VM2.</span><span class="sxs-lookup"><span data-stu-id="49e7b-130">Complete steps 4 through 6 of this article again for VM2.</span></span> <span data-ttu-id="49e7b-131">In questo caso assicurarsi di sostituire il nome della macchina virtuale con VM2.</span><span class="sxs-lookup"><span data-stu-id="49e7b-131">Be sure to replace the VM name to VM2 when doing this.</span></span> <span data-ttu-id="49e7b-132">Si noti che non è necessario creare una rete virtuale per la seconda macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="49e7b-132">Note that you do not need to create a virtual network for the second VM.</span></span> <span data-ttu-id="49e7b-133">È possibile scegliere se creare o meno una nuova subnet in base al caso d'uso.</span><span class="sxs-lookup"><span data-stu-id="49e7b-133">You may or may not create a new subnet based on your use case.</span></span>

7. <span data-ttu-id="49e7b-134">Creare due indirizzi IP pubblici e archiviarli in variabili appropriate, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="49e7b-134">Create two public IP addresses and store them in the appropriate variables as shown:</span></span>

    ```powershell
    $publicIP1 = New-AzureRmPublicIpAddress -Name PublicIp1 -ResourceGroupName contosofabrikam -Location 'West Central US' -AllocationMethod Dynamic -DomainNameLabel contoso
    $publicIP2 = New-AzureRmPublicIpAddress -Name PublicIp2 -ResourceGroupName contosofabrikam -Location 'West Central US' -AllocationMethod Dynamic -DomainNameLabel fabrikam

    $publicIP1 = Get-AzureRmPublicIpAddress -Name PublicIp1 -ResourceGroupName contosofabrikam
    $publicIP2 = Get-AzureRmPublicIpAddress -Name PublicIp2 -ResourceGroupName contosofabrikam
    ```

8. <span data-ttu-id="49e7b-135">Creare due configurazioni IP front-end:</span><span class="sxs-lookup"><span data-stu-id="49e7b-135">Create two frontend IP configurations:</span></span>

    ```powershell
    $frontendIP1 = New-AzureRmLoadBalancerFrontendIpConfig -Name contosofe -PublicIpAddress $publicIP1
    $frontendIP2 = New-AzureRmLoadBalancerFrontendIpConfig -Name fabrikamfe -PublicIpAddress $publicIP2
    ```

9. <span data-ttu-id="49e7b-136">Creare i pool di indirizzi back-end, un probe e regole di bilanciamento del carico:</span><span class="sxs-lookup"><span data-stu-id="49e7b-136">Create your backend address pools, a probe, and your load balancing rules:</span></span>

    ```powershell
    $beaddresspool1 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name contosopool
    $beaddresspool2 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name fabrikampool

    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HTTP -RequestPath 'index.html' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

    $lbrule1 = New-AzureRmLoadBalancerRuleConfig -Name HTTPc -FrontendIpConfiguration $frontendIP1 -BackendAddressPool $beaddresspool1 -Probe $healthprobe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    $lbrule2 = New-AzureRmLoadBalancerRuleConfig -Name HTTPf -FrontendIpConfiguration $frontendIP2 -BackendAddressPool $beaddresspool2 -Probe $healthprobe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    ```

10. <span data-ttu-id="49e7b-137">Dopo aver creato queste risorse, creare il servizio di bilanciamento del carico:</span><span class="sxs-lookup"><span data-stu-id="49e7b-137">Once you have these resources created, create your load balancer:</span></span>

    ```powershell
    $mylb = New-AzureRmLoadBalancer -ResourceGroupName contosofabrikam -Name mylb -Location 'West Central US' -FrontendIpConfiguration $frontendIP1 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
    ```

11. <span data-ttu-id="49e7b-138">Aggiungere il secondo pool di indirizzi back-end e la configurazione IP front-end per il servizio di bilanciamento del carico appena creato:</span><span class="sxs-lookup"><span data-stu-id="49e7b-138">Add the second backend address pool and frontend IP configuration to your newly created load balancer:</span></span>

    ```powershell
    $mylb = Get-AzureRmLoadBalancer -Name "mylb" -ResourceGroupName $myResourceGroup | Add-AzureRmLoadBalancerBackendAddressPoolConfig -Name fabrikampool | Set-AzureRmLoadBalancer

    $mylb | Add-AzureRmLoadBalancerFrontendIpConfig -Name fabrikamfe -PublicIpAddress $publicIP2 | Set-AzureRmLoadBalancer
    
    Add-AzureRmLoadBalancerRuleConfig -Name HTTP -LoadBalancer $mylb -FrontendIpConfiguration $frontendIP2 -BackendAddressPool $beaddresspool2 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80 | Set-AzureRmLoadBalancer
    ```

12. <span data-ttu-id="49e7b-139">I comandi seguenti permettono di ottenere le schede di interfaccia di rete e aggiungono entrambe le configurazioni IP di ogni scheda di interfaccia di rete secondaria al pool di indirizzi back-end del servizio di bilanciamento del carico:</span><span class="sxs-lookup"><span data-stu-id="49e7b-139">The commands below get the NICs and then add both IP configurations of each secondary NIC to the backend address pool of the load balancer:</span></span>

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

13. <span data-ttu-id="49e7b-140">Infine, è necessario configurare i record risorsa DNS in modo che puntino all'indirizzo IP front-end corrispondente di Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="49e7b-140">Finally, you must configure DNS resource records to point to the respective frontend IP address of the Load Balancer.</span></span> <span data-ttu-id="49e7b-141">È possibile ospitare i domini nel servizio DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="49e7b-141">You may host your domains in Azure DNS.</span></span> <span data-ttu-id="49e7b-142">Per altre informazioni sull'uso del servizio DNS di Azure con Azure Load Balancer, vedere [Uso del servizio DNS di Azure con altri servizi di Azure](../dns/dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="49e7b-142">For more information about using Azure DNS with Load Balancer, see [Using Azure DNS with other Azure services](../dns/dns-for-azure-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="49e7b-143">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="49e7b-143">Next steps</span></span>
- <span data-ttu-id="49e7b-144">Altre informazioni su come combinare i servizi di bilanciamento del carico di Azure sono disponibili in [Uso dei servizi di bilanciamento del carico in Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span><span class="sxs-lookup"><span data-stu-id="49e7b-144">Learn more about how to combine load balancing services in Azure in [Using load-balancing services in Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span></span>
- <span data-ttu-id="49e7b-145">Informazioni su come è possibile usare diversi tipi di log in Azure per gestire e risolvere i problemi di bilanciamento del carico sono disponibili in [Analisi dei log per Azure Load Balancer](../load-balancer/load-balancer-monitor-log.md).</span><span class="sxs-lookup"><span data-stu-id="49e7b-145">Learn how you can use different types of logs in Azure to manage and troubleshoot load balancer in [Log analytics for Azure Load Balancer](../load-balancer/load-balancer-monitor-log.md).</span></span>
