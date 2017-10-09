---
title: Azure interna aaaCreate bilanciamento del carico - PowerShell classico | Documenti Microsoft
description: Informazioni su come toocreate un interno bilanciamento del carico con PowerShell nel modello di distribuzione classica hello
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
ms.openlocfilehash: 382db80c42ffab09905513019b72e85a4f9dfeff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-using-powershell"></a><span data-ttu-id="d3b75-103">Introduzione alla creazione di un servizio di bilanciamento del carico interno (classico) tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="d3b75-103">Get started creating an internal load balancer (classic) using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d3b75-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d3b75-104">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [<span data-ttu-id="d3b75-105">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="d3b75-105">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [<span data-ttu-id="d3b75-106">Servizi cloud</span><span class="sxs-lookup"><span data-stu-id="d3b75-106">Cloud services</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="d3b75-107">Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="d3b75-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="d3b75-108">In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="d3b75-108">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="d3b75-109">Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="d3b75-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="d3b75-110">Informazioni su come troppo[eseguire questi passaggi tramite il modello di gestione risorse di hello](load-balancer-get-started-ilb-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="d3b75-110">Learn how too[perform these steps using hello Resource Manager model](load-balancer-get-started-ilb-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-internal-load-balancer-set-for-virtual-machines"></a><span data-ttu-id="d3b75-111">Creare un set con servizio di bilanciamento del carico interno per le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="d3b75-111">Create an internal load balancer set for virtual machines</span></span>

<span data-ttu-id="d3b75-112">toocreate un bilanciamento del carico interno impostato e hello server che invierà i tooit di traffico, è necessario seguente hello toodo:</span><span class="sxs-lookup"><span data-stu-id="d3b75-112">toocreate an internal load balancer set and hello servers that will send their traffic tooit, you have toodo hello following:</span></span>

1. <span data-ttu-id="d3b75-113">Creare un'istanza interna il bilanciamento del carico che fungerà da endpoint hello in arrivo traffico toobe con bilanciato del carico tra i server hello di un set con carico bilanciato.</span><span class="sxs-lookup"><span data-stu-id="d3b75-113">Create an instance of Internal Load Balancing that will be hello endpoint of incoming traffic toobe load balanced across hello servers of a load-balanced set.</span></span>
2. <span data-ttu-id="d3b75-114">Aggiungere gli endpoint corrispondenti toohello le macchine virtuali che riceveranno il traffico in ingresso hello.</span><span class="sxs-lookup"><span data-stu-id="d3b75-114">Add endpoints corresponding toohello virtual machines that will be receiving hello incoming traffic.</span></span>
3. <span data-ttu-id="d3b75-115">Configurare i server hello che invieranno hello traffico toobe con bilanciamento del carico toosend loro traffico toohello indirizzo IP virtuale (VIP) dell'istanza di hello interno il bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="d3b75-115">Configure hello servers that will be sending hello traffic toobe load balanced toosend their traffic toohello virtual IP (VIP) address of hello Internal Load Balancing instance.</span></span>

### <a name="step-1-create-an-internal-load-balancing-instance"></a><span data-ttu-id="d3b75-116">Passaggio 1: Creare un'istanza del bilanciamento del carico interno</span><span class="sxs-lookup"><span data-stu-id="d3b75-116">Step 1: Create an Internal Load Balancing instance</span></span>

<span data-ttu-id="d3b75-117">Per un servizio cloud esistente o un servizio cloud distribuito in una rete virtuale regionale, è possibile creare un'istanza di bilanciamento del carico interno con hello seguenti comandi di Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="d3b75-117">For an existing cloud service or a cloud service deployed under a regional virtual network, you can create an Internal Load Balancing instance with hello following Windows PowerShell commands:</span></span>

```powershell
$svc="<Cloud Service Name>"
$ilb="<Name of your ILB instance>"
$subnet="<Name of hello subnet within your virtual network>"
$IP="<hello IPv4 address toouse on hello subnet-optional>"

Add-AzureInternalLoadBalancer -ServiceName $svc -InternalLoadBalancerName $ilb –SubnetName $subnet –StaticVNetIPAddress $IP
```

<span data-ttu-id="d3b75-118">Si noti che questo utilizzo di hello [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx) cmdlet di Windows PowerShell Usa hello di parametri defaultprobe.</span><span class="sxs-lookup"><span data-stu-id="d3b75-118">Note that this use of hello [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx) Windows PowerShell cmdlet uses hello DefaultProbe parameter set.</span></span> <span data-ttu-id="d3b75-119">Per altre informazioni sui set di parametri aggiuntivi, vedere [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx).</span><span class="sxs-lookup"><span data-stu-id="d3b75-119">For more information on additional parameter sets, see [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx).</span></span>

### <a name="step-2-add-endpoints-toohello-internal-load-balancing-instance"></a><span data-ttu-id="d3b75-120">Passaggio 2: Aggiungere l'istanza di bilanciamento del carico interno toohello endpoint</span><span class="sxs-lookup"><span data-stu-id="d3b75-120">Step 2: Add endpoints toohello Internal Load Balancing instance</span></span>

<span data-ttu-id="d3b75-121">Di seguito è fornito un esempio:</span><span class="sxs-lookup"><span data-stu-id="d3b75-121">Here is an example:</span></span>

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

### <a name="step-3-configure-your-servers-toosend-their-traffic-toohello-new-internal-load-balancing-endpoint"></a><span data-ttu-id="d3b75-122">Passaggio 3: Configurare il server toosend i relativi endpoint di bilanciamento del carico interno nuovo traffico toohello</span><span class="sxs-lookup"><span data-stu-id="d3b75-122">Step 3: Configure your servers toosend their traffic toohello new Internal Load Balancing endpoint</span></span>

<span data-ttu-id="d3b75-123">Configurare hello server il cui traffico corso toobe con carico bilanciato toouse hello nuovo indirizzo IP (Buongiorno VIP) del hello istanza interno il bilanciamento del carico eccessivo.</span><span class="sxs-lookup"><span data-stu-id="d3b75-123">You have too configure hello servers whose traffic is going toobe load balanced toouse hello new IP address (hello VIP) of hello Internal Load Balancing instance.</span></span> <span data-ttu-id="d3b75-124">Questo è hello indirizzo sul quale hello bilanciamento del carico interno è in ascolto l'istanza.</span><span class="sxs-lookup"><span data-stu-id="d3b75-124">This is hello address on which hello Internal Load Balancing instance is listening.</span></span> <span data-ttu-id="d3b75-125">Nella maggior parte dei casi, è necessario toojust aggiungere o modificare un record DNS per hello VIP dell'istanza di bilanciamento del carico interno hello.</span><span class="sxs-lookup"><span data-stu-id="d3b75-125">In most cases, you need toojust add or modify a DNS record for hello VIP of hello Internal Load Balancing instance.</span></span>

<span data-ttu-id="d3b75-126">Se si specifica l'indirizzo IP hello durante la creazione dell'istanza di bilanciamento del carico interno hello hello, si dispone già di hello VIP.</span><span class="sxs-lookup"><span data-stu-id="d3b75-126">If you specified hello IP address during hello creation of hello Internal Load Balancing instance, you already have hello VIP.</span></span> <span data-ttu-id="d3b75-127">In caso contrario, è possibile visualizzare il VIP hello da hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="d3b75-127">Otherwise, you can see hello VIP from hello following commands:</span></span>

```powershell
$svc="<Cloud Service Name>"
Get-AzureService -ServiceName $svc | Get-AzureInternalLoadBalancer
```

<span data-ttu-id="d3b75-128">toouse questi comandi, immettere i valori hello e Rimuovi hello < e >.</span><span class="sxs-lookup"><span data-stu-id="d3b75-128">toouse these commands, fill in hello values and remove hello < and >.</span></span> <span data-ttu-id="d3b75-129">Di seguito è fornito un esempio:</span><span class="sxs-lookup"><span data-stu-id="d3b75-129">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
Get-AzureService -ServiceName $svc | Get-AzureInternalLoadBalancer
```

<span data-ttu-id="d3b75-130">Dalla visualizzazione hello di hello comando Get-AzureInternalLoadBalancer, prendere nota indirizzo IP hello e rendere server tooyour di hello le modifiche necessarie o tooensure i record DNS che il traffico venga inviato toohello VIP.</span><span class="sxs-lookup"><span data-stu-id="d3b75-130">From hello display of hello Get-AzureInternalLoadBalancer command, note hello IP address and make hello necessary changes tooyour servers or DNS records tooensure that traffic gets sent toohello VIP.</span></span>

> [!NOTE]
> <span data-ttu-id="d3b75-131">piattaforma Microsoft Azure Hello utilizza un indirizzo IPv4 statico, instradabile pubblicamente per un'ampia gamma di scenari di amministrazione.</span><span class="sxs-lookup"><span data-stu-id="d3b75-131">hello Microsoft Azure platform uses a static, publicly routable IPv4 address for a variety of administrative scenarios.</span></span> <span data-ttu-id="d3b75-132">indirizzo IP Hello è 168.63.129.16.</span><span class="sxs-lookup"><span data-stu-id="d3b75-132">hello IP address is 168.63.129.16.</span></span> <span data-ttu-id="d3b75-133">Questo indirizzo IP non deve essere bloccato da alcun firewall, perché potrebbe causare un comportamento imprevisto.</span><span class="sxs-lookup"><span data-stu-id="d3b75-133">This IP address should not be blocked by any firewalls, because it can cause unexpected behavior.</span></span>
> <span data-ttu-id="d3b75-134">Con tooAzure riguardo interno il bilanciamento del carico, viene utilizzato questo indirizzo IP dal monitoraggio probe di stato di integrità hello toodetermine bilanciamento del carico hello per le macchine virtuali in un set con carico bilanciato.</span><span class="sxs-lookup"><span data-stu-id="d3b75-134">With respect tooAzure Internal Load Balancing, this IP address is used by monitoring probes from hello load balancer toodetermine hello health state for virtual machines in a load balanced set.</span></span> <span data-ttu-id="d3b75-135">Se un gruppo di sicurezza di rete è utilizzata toorestrict traffico tooAzure le macchine virtuali in un set di internamente con bilanciamento del carico o applicato tooa Subnet rete virtuale, assicurarsi che una regola di sicurezza di rete viene aggiunto il traffico tooallow 168.63.129.16.</span><span class="sxs-lookup"><span data-stu-id="d3b75-135">If a Network Security Group is used toorestrict traffic tooAzure virtual machines in an internally load-balanced set or is applied tooa Virtual Network Subnet, ensure that a Network Security Rule is added tooallow traffic from 168.63.129.16.</span></span>

## <a name="example-of-internal-load-balancing"></a><span data-ttu-id="d3b75-136">Esempio di bilanciamento del carico interno</span><span class="sxs-lookup"><span data-stu-id="d3b75-136">Example of internal load balancing</span></span>

<span data-ttu-id="d3b75-137">toostep illustra il processo di fine tooend hello di creazione di un set con carico bilanciato per due configurazioni di esempio, vedere hello seguenti sezioni.</span><span class="sxs-lookup"><span data-stu-id="d3b75-137">toostep you through hello end-tooend process of creating a load-balanced set for two example configurations, see hello following sections.</span></span>

### <a name="an-internet-facing-multi-tier-application"></a><span data-ttu-id="d3b75-138">Applicazione multilivello con connessione Internet</span><span class="sxs-lookup"><span data-stu-id="d3b75-138">An Internet facing, multi-tier application</span></span>

<span data-ttu-id="d3b75-139">Si desidera tooprovide un servizio di database con carico bilanciato per un set di server web con connessione Internet.</span><span class="sxs-lookup"><span data-stu-id="d3b75-139">You want tooprovide a load balanced database service for  a set of Internet-facing web servers.</span></span> <span data-ttu-id="d3b75-140">Entrambi i set di server sono ospitati in un unico servizio cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="d3b75-140">Both sets of servers are hosted in a single Azure cloud service.</span></span> <span data-ttu-id="d3b75-141">La porta Web server traffico tooTCP 1433 deve essere distribuita tra due macchine virtuali nel livello di database hello.</span><span class="sxs-lookup"><span data-stu-id="d3b75-141">Web server traffic tooTCP port 1433 must be distributed among two virtual machines in hello database tier.</span></span> <span data-ttu-id="d3b75-142">Figura 1 mostra la configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="d3b75-142">Figure 1 shows hello configuration.</span></span>

![Set con carico bilanciato interno per il livello di database hello](./media/load-balancer-internal-getstarted/IC736321.png)

<span data-ttu-id="d3b75-144">configurazione di Hello è costituita dai seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="d3b75-144">hello configuration consists of hello following:</span></span>

* <span data-ttu-id="d3b75-145">Hello servizio cloud che ospita macchine virtuali hello è denominato mytestcloud.</span><span class="sxs-lookup"><span data-stu-id="d3b75-145">hello existing cloud service hosting hello virtual machines is named mytestcloud.</span></span>
* <span data-ttu-id="d3b75-146">il server di database di Hello due esistenti sono denominati DB1, DB2.</span><span class="sxs-lookup"><span data-stu-id="d3b75-146">hello two existing database servers are named DB1, DB2.</span></span>
* <span data-ttu-id="d3b75-147">I server Web nel livello web hello connettono i server di database toohello nel livello di database hello utilizzando l'indirizzo IP privato hello.</span><span class="sxs-lookup"><span data-stu-id="d3b75-147">Web servers in hello web tier connect toohello database servers in hello database tier by using hello private IP address.</span></span> <span data-ttu-id="d3b75-148">Un'altra opzione è toouse DNS per la rete virtuale hello e registrare manualmente un record A per il set di bilanciamento del carico interno con carico hello.</span><span class="sxs-lookup"><span data-stu-id="d3b75-148">Another option is toouse your own DNS for hello virtual network and manually register an A record for hello internal load balancer set.</span></span>

<span data-ttu-id="d3b75-149">i comandi seguenti Hello configurano una nuova istanza di bilanciamento del carico interno denominata **ILBset** e aggiungere le macchine virtuali endpoint toohello corrispondente toohello due server di database:</span><span class="sxs-lookup"><span data-stu-id="d3b75-149">hello following commands configure a new Internal Load Balancing instance named **ILBset** and add endpoints toohello virtual machines corresponding toohello two database servers:</span></span>

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

## <a name="remove-an-internal-load-balancing-configuration"></a><span data-ttu-id="d3b75-150">Rimuovere una configurazione del bilanciamento del carico interno</span><span class="sxs-lookup"><span data-stu-id="d3b75-150">Remove an Internal Load Balancing configuration</span></span>

<span data-ttu-id="d3b75-151">tooremove una macchina virtuale come un endpoint da un'istanza di servizio di bilanciamento del carico interno, hello di utilizzare i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d3b75-151">tooremove a virtual machine as an endpoint from an internal load balancer instance, use hello following commands:</span></span>

```powershell
$svc="<Cloud service name>"
$vmname="<Name of hello VM>"
$epname="<Name of hello endpoint>"
Get-AzureVM -ServiceName $svc -Name $vmname | Remove-AzureEndpoint -Name $epname | Update-AzureVM
```

<span data-ttu-id="d3b75-152">toouse questi comandi, inserire i valori hello, rimozione hello < e >.</span><span class="sxs-lookup"><span data-stu-id="d3b75-152">toouse these commands, fill in hello values, removing hello < and >.</span></span>

<span data-ttu-id="d3b75-153">Di seguito è fornito un esempio:</span><span class="sxs-lookup"><span data-stu-id="d3b75-153">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
$vmname="DB1"
$epname="TCP-1433-1433"
Get-AzureVM -ServiceName $svc -Name $vmname | Remove-AzureEndpoint -Name $epname | Update-AzureVM
```

<span data-ttu-id="d3b75-154">tooremove un'istanza di servizio di bilanciamento del carico interno da un servizio cloud, hello di utilizzare i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d3b75-154">tooremove an internal load balancer instance from a cloud service, use hello following commands:</span></span>

```powershell
$svc="<Cloud service name>"
Remove-AzureInternalLoadBalancer -ServiceName $svc
```

<span data-ttu-id="d3b75-155">toouse questi comandi, inserire il valore di hello e rimuovere hello < e >.</span><span class="sxs-lookup"><span data-stu-id="d3b75-155">toouse these commands, fill in hello value and remove hello < and >.</span></span>

<span data-ttu-id="d3b75-156">Di seguito è fornito un esempio:</span><span class="sxs-lookup"><span data-stu-id="d3b75-156">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
Remove-AzureInternalLoadBalancer -ServiceName $svc
```

## <a name="additional-information-about-internal-load-balancer-cmdlets"></a><span data-ttu-id="d3b75-157">Altre informazioni sui cmdlet per servizio di bilanciamento del carico interno</span><span class="sxs-lookup"><span data-stu-id="d3b75-157">Additional information about internal load balancer cmdlets</span></span>

<span data-ttu-id="d3b75-158">tooobtain ulteriori informazioni sui cmdlet di bilanciamento del carico interno, eseguire hello comandi al prompt di Windows PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="d3b75-158">tooobtain additional information about Internal Load Balancing cmdlets, run hello following commands at a Windows PowerShell prompt:</span></span>

```powershell
Get-Help New-AzureInternalLoadBalancerConfig -full
Get-Help Add-AzureInternalLoadBalancer -full
Get-Help Get-AzureInternalLoadbalancer -full
Get-Help Remove-AzureInternalLoadBalancer -full
```

## <a name="next-steps"></a><span data-ttu-id="d3b75-159">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d3b75-159">Next steps</span></span>

[<span data-ttu-id="d3b75-160">Configurare una modalità di distribuzione del servizio di bilanciamento del carico utilizzando l’affinità dell’IP di origine</span><span class="sxs-lookup"><span data-stu-id="d3b75-160">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="d3b75-161">Configurare le impostazioni del timeout di inattività TCP per il bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="d3b75-161">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

