---
title: Creare un servizio di bilanciamento del carico interno di Azure - Distribuzione classica con PowerShell | Documentazione Microsoft
description: Informazioni su come creare un servizio di bilanciamento del carico interno usando PowerShell nel modello di distribuzione classica
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 3be93168-3787-45a5-a194-9124fe386493
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: f701fb3564c62cf8088cc4362a10c5e2c2301ae6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-using-powershell"></a><span data-ttu-id="886b4-103">Introduzione alla creazione di un servizio di bilanciamento del carico interno (classico) tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="886b4-103">Get started creating an internal load balancer (classic) using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="886b4-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="886b4-104">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [<span data-ttu-id="886b4-105">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="886b4-105">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [<span data-ttu-id="886b4-106">Servizi cloud</span><span class="sxs-lookup"><span data-stu-id="886b4-106">Cloud services</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="886b4-107">Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="886b4-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="886b4-108">Questo articolo illustra l'uso del modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="886b4-108">This article covers using the classic deployment model.</span></span> <span data-ttu-id="886b4-109">Microsoft consiglia di usare il modello di Gestione risorse per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="886b4-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="886b4-110">Informazioni su come [eseguire questa procedura con il modello di Resource Manager](load-balancer-get-started-ilb-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="886b4-110">Learn how to [perform these steps using the Resource Manager model](load-balancer-get-started-ilb-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-internal-load-balancer-set-for-virtual-machines"></a><span data-ttu-id="886b4-111">Creare un set con servizio di bilanciamento del carico interno per le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="886b4-111">Create an internal load balancer set for virtual machines</span></span>

<span data-ttu-id="886b4-112">Per creare un set con servizio di bilanciamento del carico e i server che invieranno il traffico a esso, è necessario eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="886b4-112">To create an internal load balancer set and the servers that will send their traffic to it, you have to do the following:</span></span>

1. <span data-ttu-id="886b4-113">Creare un'istanza della funzionalità di bilanciamento del carico interno che sarà l'endpoint del traffico in ingresso da configurare con carico bilanciato tra i server di un set con carico bilanciato.</span><span class="sxs-lookup"><span data-stu-id="886b4-113">Create an instance of Internal Load Balancing that will be the endpoint of incoming traffic to be load balanced across the servers of a load-balanced set.</span></span>
2. <span data-ttu-id="886b4-114">Aggiungere gli endpoint corrispondenti alle macchine virtuali che riceveranno il traffico in ingresso.</span><span class="sxs-lookup"><span data-stu-id="886b4-114">Add endpoints corresponding to the virtual machines that will be receiving the incoming traffic.</span></span>
3. <span data-ttu-id="886b4-115">Configurare i server che invieranno il traffico con carico bilanciato all'indirizzo IP virtuale (indirizzo VIP) dell'istanza del bilanciamento del carico interno.</span><span class="sxs-lookup"><span data-stu-id="886b4-115">Configure the servers that will be sending the traffic to be load balanced to send their traffic to the virtual IP (VIP) address of the Internal Load Balancing instance.</span></span>

### <a name="step-1-create-an-internal-load-balancing-instance"></a><span data-ttu-id="886b4-116">Passaggio 1: Creare un'istanza del bilanciamento del carico interno</span><span class="sxs-lookup"><span data-stu-id="886b4-116">Step 1: Create an Internal Load Balancing instance</span></span>

<span data-ttu-id="886b4-117">Per un servizio cloud esistente o un servizio cloud distribuito in una rete virtuale dell'area, è possibile creare un'istanza del bilanciamento del carico interno con i comandi di Windows PowerShell seguenti:</span><span class="sxs-lookup"><span data-stu-id="886b4-117">For an existing cloud service or a cloud service deployed under a regional virtual network, you can create an Internal Load Balancing instance with the following Windows PowerShell commands:</span></span>

```powershell
$svc="<Cloud Service Name>"
$ilb="<Name of your ILB instance>"
$subnet="<Name of the subnet within your virtual network>"
$IP="<The IPv4 address to use on the subnet-optional>"

Add-AzureInternalLoadBalancer -ServiceName $svc -InternalLoadBalancerName $ilb –SubnetName $subnet –StaticVNetIPAddress $IP
```

<span data-ttu-id="886b4-118">Si noti che questo uso del cmdlet di Windows PowerShell [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx) richiede il set di parametri DefaultProbe.</span><span class="sxs-lookup"><span data-stu-id="886b4-118">Note that this use of the [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx) Windows PowerShell cmdlet uses the DefaultProbe parameter set.</span></span> <span data-ttu-id="886b4-119">Per altre informazioni sui set di parametri aggiuntivi, vedere [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx).</span><span class="sxs-lookup"><span data-stu-id="886b4-119">For more information on additional parameter sets, see [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx).</span></span>

### <a name="step-2-add-endpoints-to-the-internal-load-balancing-instance"></a><span data-ttu-id="886b4-120">Passaggio 2: Aggiungere endpoint all'istanza del bilanciamento del carico interno</span><span class="sxs-lookup"><span data-stu-id="886b4-120">Step 2: Add endpoints to the Internal Load Balancing instance</span></span>

<span data-ttu-id="886b4-121">Di seguito è fornito un esempio:</span><span class="sxs-lookup"><span data-stu-id="886b4-121">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
$vmname="DB1"
$epname="TCP-1433-1433"
$lbsetname="lbset"
$prot="tcp"
$locport=1433
$pubport=1433
$ilb="ilbset"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -Lbset $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM
```

### <a name="step-3-configure-your-servers-to-send-their-traffic-to-the-new-internal-load-balancing-endpoint"></a><span data-ttu-id="886b4-122">Passaggio 3: Configurare i server per l'invio del traffico al nuovo endpoint del bilanciamento del carico interno</span><span class="sxs-lookup"><span data-stu-id="886b4-122">Step 3: Configure your servers to send their traffic to the new Internal Load Balancing endpoint</span></span>

<span data-ttu-id="886b4-123">Per poter usare il nuovo indirizzo IP (indirizzo VIP) dell'istanza del bilanciamento del carico interno, è necessario configurare i server il cui traffico verrà configurato con carico bilanciato.</span><span class="sxs-lookup"><span data-stu-id="886b4-123">You have to  configure the servers whose traffic is going to be load balanced to use the new IP address (the VIP) of the Internal Load Balancing instance.</span></span> <span data-ttu-id="886b4-124">Si tratta dell'indirizzo su cui è in ascolto l'istanza del bilanciamento del carico interno.</span><span class="sxs-lookup"><span data-stu-id="886b4-124">This is the address on which the Internal Load Balancing instance is listening.</span></span> <span data-ttu-id="886b4-125">Nella maggior parte dei casi, è sufficiente aggiungere o modificare un record DNS per l'indirizzo VIP dell'istanza del bilanciamento del carico interno.</span><span class="sxs-lookup"><span data-stu-id="886b4-125">In most cases, you need to just add or modify a DNS record for the VIP of the Internal Load Balancing instance.</span></span>

<span data-ttu-id="886b4-126">Se l'indirizzo IP è stato specificato durante la creazione dell'istanza del bilanciamento del carico interno, si ha già l'indirizzo VIP.</span><span class="sxs-lookup"><span data-stu-id="886b4-126">If you specified the IP address during the creation of the Internal Load Balancing instance, you already have the VIP.</span></span> <span data-ttu-id="886b4-127">In caso contrario, è possibile visualizzare l'indirizzo VIP eseguendo i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="886b4-127">Otherwise, you can see the VIP from the following commands:</span></span>

```powershell
$svc="<Cloud Service Name>"
Get-AzureService -ServiceName $svc | Get-AzureInternalLoadBalancer
```

<span data-ttu-id="886b4-128">Per usare questi comandi, inserire i valori e rimuovere < and >.</span><span class="sxs-lookup"><span data-stu-id="886b4-128">To use these commands, fill in the values and remove the < and >.</span></span> <span data-ttu-id="886b4-129">Di seguito è fornito un esempio:</span><span class="sxs-lookup"><span data-stu-id="886b4-129">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
Get-AzureService -ServiceName $svc | Get-AzureInternalLoadBalancer
```

<span data-ttu-id="886b4-130">Dalla visualizzazione del comando Get-AzureInternalLoadBalancer prendere nota dell'indirizzo IP e apportare le modifiche necessarie ai server o ai record DNS per assicurarsi che il traffico venga inviato all'indirizzo VIP.</span><span class="sxs-lookup"><span data-stu-id="886b4-130">From the display of the Get-AzureInternalLoadBalancer command, note the IP address and make the necessary changes to your servers or DNS records to ensure that traffic gets sent to the VIP.</span></span>

> [!NOTE]
> <span data-ttu-id="886b4-131">La piattaforma Microsoft Azure usa un indirizzo IPv4 statico e instradabile pubblicamente per un'ampia gamma di scenari di amministrazione.</span><span class="sxs-lookup"><span data-stu-id="886b4-131">The Microsoft Azure platform uses a static, publicly routable IPv4 address for a variety of administrative scenarios.</span></span> <span data-ttu-id="886b4-132">L'indirizzo IP è 168.63.129.16.</span><span class="sxs-lookup"><span data-stu-id="886b4-132">The IP address is 168.63.129.16.</span></span> <span data-ttu-id="886b4-133">Questo indirizzo IP non deve essere bloccato da alcun firewall, perché potrebbe causare un comportamento imprevisto.</span><span class="sxs-lookup"><span data-stu-id="886b4-133">This IP address should not be blocked by any firewalls, because it can cause unexpected behavior.</span></span>
> <span data-ttu-id="886b4-134">Per quanto riguarda il bilanciamento del carico interno di Azure, questo indirizzo IP viene usato da probe di monitoraggio del servizio di bilanciamento del carico per determinare lo stato di integrità delle macchine virtuali in un set con carico bilanciato.</span><span class="sxs-lookup"><span data-stu-id="886b4-134">With respect to Azure Internal Load Balancing, this IP address is used by monitoring probes from the load balancer to determine the health state for virtual machines in a load balanced set.</span></span> <span data-ttu-id="886b4-135">Se si usa un gruppo di sicurezza di rete per limitare il traffico alle macchine virtuali di Azure in un set con carico bilanciato internamente o lo si applica a una subnet di rete virtuale, assicurarsi di aggiungere una regola di sicurezza di rete per consentire il traffico dall'indirizzo 168.63.129.16.</span><span class="sxs-lookup"><span data-stu-id="886b4-135">If a Network Security Group is used to restrict traffic to Azure virtual machines in an internally load-balanced set or is applied to a Virtual Network Subnet, ensure that a Network Security Rule is added to allow traffic from 168.63.129.16.</span></span>

## <a name="example-of-internal-load-balancing"></a><span data-ttu-id="886b4-136">Esempio di bilanciamento del carico interno</span><span class="sxs-lookup"><span data-stu-id="886b4-136">Example of internal load balancing</span></span>

<span data-ttu-id="886b4-137">Per una descrizione del processo end-to-end di creazione di un set con carico bilanciato per due configurazioni di esempio, vedere le sezioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="886b4-137">To step you through the end-to end process of creating a load-balanced set for two example configurations, see the following sections.</span></span>

### <a name="an-internet-facing-multi-tier-application"></a><span data-ttu-id="886b4-138">Applicazione multilivello con connessione Internet</span><span class="sxs-lookup"><span data-stu-id="886b4-138">An Internet facing, multi-tier application</span></span>

<span data-ttu-id="886b4-139">Si vuole offrire un servizio di database con carico bilanciato per un gruppo di server Web con connessione Internet.</span><span class="sxs-lookup"><span data-stu-id="886b4-139">You want to provide a load balanced database service for  a set of Internet-facing web servers.</span></span> <span data-ttu-id="886b4-140">Entrambi i set di server sono ospitati in un unico servizio cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="886b4-140">Both sets of servers are hosted in a single Azure cloud service.</span></span> <span data-ttu-id="886b4-141">Il traffico dei server Web verso la porta TCP 1433 deve essere distribuito tra due macchine virtuali nel livello database.</span><span class="sxs-lookup"><span data-stu-id="886b4-141">Web server traffic to TCP port 1433 must be distributed among two virtual machines in the database tier.</span></span> <span data-ttu-id="886b4-142">La figura 1 illustra la configurazione.</span><span class="sxs-lookup"><span data-stu-id="886b4-142">Figure 1 shows the configuration.</span></span>

![Set con carico bilanciato interno per il livello database](./media/load-balancer-internal-getstarted/IC736321.png)

<span data-ttu-id="886b4-144">La configurazione è costituita dai seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="886b4-144">The configuration consists of the following:</span></span>

* <span data-ttu-id="886b4-145">Il servizio cloud esistente che ospita le macchine virtuali è denominato mytestcloud.</span><span class="sxs-lookup"><span data-stu-id="886b4-145">The existing cloud service hosting the virtual machines is named mytestcloud.</span></span>
* <span data-ttu-id="886b4-146">I due server di database esistenti sono denominati DB1, DB2.</span><span class="sxs-lookup"><span data-stu-id="886b4-146">The two existing database servers are named DB1, DB2.</span></span>
* <span data-ttu-id="886b4-147">I server Web nel livello Web si connettono ai server di database nel livello database usando l’indirizzo IP privato.</span><span class="sxs-lookup"><span data-stu-id="886b4-147">Web servers in the web tier connect to the database servers in the database tier by using the private IP address.</span></span> <span data-ttu-id="886b4-148">Un'altra opzione consiste nell'utilizzare il proprio DNS per la rete virtuale e registrare manualmente un record A per il set di bilanciamento del carico interno.</span><span class="sxs-lookup"><span data-stu-id="886b4-148">Another option is to use your own DNS for the virtual network and manually register an A record for the internal load balancer set.</span></span>

<span data-ttu-id="886b4-149">I comandi seguenti configurano una nuova istanza del bilanciamento del carico interno denominata **ILBset** e aggiungono endpoint alle macchine virtuali corrispondenti ai due server di database:</span><span class="sxs-lookup"><span data-stu-id="886b4-149">The following commands configure a new Internal Load Balancing instance named **ILBset** and add endpoints to the virtual machines corresponding to the two database servers:</span></span>

```powershell
$svc="mytestcloud"
$ilb="ilbset"
Add-AzureInternalLoadBalancer -ServiceName $svc -InternalLoadBalancerName $ilb
$prot="tcp"
$locport=1433
$pubport=1433
$epname="TCP-1433-1433"
$lbsetname="lbset"
$vmname="DB1"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -LbSetName $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM

$epname="TCP-1433-1433-2"
$vmname="DB2"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -LbSetName $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM
```

## <a name="remove-an-internal-load-balancing-configuration"></a><span data-ttu-id="886b4-150">Rimuovere una configurazione del bilanciamento del carico interno</span><span class="sxs-lookup"><span data-stu-id="886b4-150">Remove an Internal Load Balancing configuration</span></span>

<span data-ttu-id="886b4-151">Per rimuovere una macchina virtuale come endpoint da un'istanza del servizio di bilanciamento del carico interno, usare i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="886b4-151">To remove a virtual machine as an endpoint from an internal load balancer instance, use the following commands:</span></span>

```powershell
$svc="<Cloud service name>"
$vmname="<Name of the VM>"
$epname="<Name of the endpoint>"
Get-AzureVM -ServiceName $svc -Name $vmname | Remove-AzureEndpoint -Name $epname | Update-AzureVM
```

<span data-ttu-id="886b4-152">Per usare questi comandi, inserire i valori rimuovendo < and >.</span><span class="sxs-lookup"><span data-stu-id="886b4-152">To use these commands, fill in the values, removing the < and >.</span></span>

<span data-ttu-id="886b4-153">Di seguito è fornito un esempio:</span><span class="sxs-lookup"><span data-stu-id="886b4-153">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
$vmname="DB1"
$epname="TCP-1433-1433"
Get-AzureVM -ServiceName $svc -Name $vmname | Remove-AzureEndpoint -Name $epname | Update-AzureVM
```

<span data-ttu-id="886b4-154">Per rimuovere un'istanza del servizio di bilanciamento del carico interno da un servizio cloud, usare i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="886b4-154">To remove an internal load balancer instance from a cloud service, use the following commands:</span></span>

```powershell
$svc="<Cloud service name>"
Remove-AzureInternalLoadBalancer -ServiceName $svc
```

<span data-ttu-id="886b4-155">Per usare questi comandi, inserire il valore e rimuovere < and >.</span><span class="sxs-lookup"><span data-stu-id="886b4-155">To use these commands, fill in the value and remove the < and >.</span></span>

<span data-ttu-id="886b4-156">Di seguito è fornito un esempio:</span><span class="sxs-lookup"><span data-stu-id="886b4-156">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
Remove-AzureInternalLoadBalancer -ServiceName $svc
```

## <a name="additional-information-about-internal-load-balancer-cmdlets"></a><span data-ttu-id="886b4-157">Altre informazioni sui cmdlet per servizio di bilanciamento del carico interno</span><span class="sxs-lookup"><span data-stu-id="886b4-157">Additional information about internal load balancer cmdlets</span></span>

<span data-ttu-id="886b4-158">Per ottenere altre informazioni sui cmdlet per il bilanciamento del carico interno, eseguire i comandi seguenti da un prompt di Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="886b4-158">To obtain additional information about Internal Load Balancing cmdlets, run the following commands at a Windows PowerShell prompt:</span></span>

```powershell
Get-Help New-AzureInternalLoadBalancerConfig -full
Get-Help Add-AzureInternalLoadBalancer -full
Get-Help Get-AzureInternalLoadbalancer -full
Get-Help Remove-AzureInternalLoadBalancer -full
```

## <a name="next-steps"></a><span data-ttu-id="886b4-159">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="886b4-159">Next steps</span></span>

[<span data-ttu-id="886b4-160">Configurare una modalità di distribuzione del servizio di bilanciamento del carico utilizzando l’affinità dell’IP di origine</span><span class="sxs-lookup"><span data-stu-id="886b4-160">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="886b4-161">Configurare le impostazioni del timeout di inattività TCP per il bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="886b4-161">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

