---
title: "Creare una configurazione di SAP a più SID in Azure| Documentazione Microsoft"
description: "Guida alla configurazione di SAP NetWeaver a più SID a disponibilità elevata nelle macchine virtuali Windows"
services: virtual-machines-windows, virtual-network, storage
documentationcenter: saponazure
author: goraco
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 0b89b4f8-6d6c-45d7-8d20-fe93430217ca
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/05/2017
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b48df78df9f53ac7bf0804f55a8d36a2fe2f86b4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-sap-netweaver-multi-sid-configuration"></a><span data-ttu-id="b41ed-103">Creare una configurazione di SAP NetWeaver a più SID</span><span class="sxs-lookup"><span data-stu-id="b41ed-103">Create an SAP NetWeaver multi-SID configuration</span></span>

[load-balancer-multivip-overview]:../../../load-balancer/load-balancer-multivip-overview.md
[sap-ha-guide]:sap-high-availability-guide.md 
[sap-ha-guide-figure-6001]:./media/virtual-machines-shared-sap-high-availability-guide/6001-sap-multi-sid-ascs-scs-sid1.png
[sap-ha-guide-figure-6002]:./media/virtual-machines-shared-sap-high-availability-guide/6002-sap-multi-sid-ascs-scs.png
[sap-ha-guide-figure-6003]:./media/virtual-machines-shared-sap-high-availability-guide/6003-sap-multi-sid-full-landscape.png
[sap-ha-guide-figure-6004]:./media/virtual-machines-shared-sap-high-availability-guide/6004-sap-multi-sid-dns.png
[sap-ha-guide-figure-6005]:./media/virtual-machines-shared-sap-high-availability-guide/6005-sap-multi-sid-azure-portal.png
[sap-ha-guide-figure-6006]:./media/virtual-machines-shared-sap-high-availability-guide/6006-sap-multi-sid-sios-replication.png
[networking-limits-azure-resource-manager]:../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits
[sap-ha-guide-9.1.1]:sap-high-availability-guide.md#a97ad604-9094-44fe-a364-f89cb39bf097 
[sap-ha-guide-8.8]:sap-high-availability-guide.md#f19bd997-154d-4583-a46e-7f5a69d0153c
[sap-ha-guide-8.12.3.3]:sap-high-availability-guide.md#d9c1fc8e-8710-4dff-bec2-1f535db7b006 
[sap-ha-guide-9]:sap-high-availability-guide.md#a06f0b49-8a7a-42bf-8b0d-c12026c5746b
[sap-ha-guide-9.1]:sap-high-availability-guide.md#31c6bd4f-51df-4057-9fdf-3fcbc619c170 
[sap-ha-guide-9.1.2]:sap-high-availability-guide.md#eb5af918-b42f-4803-bb50-eff41f84b0b0 
[sap-ha-guide-9.1.3]:sap-high-availability-guide.md#e4caaab2-e90f-4f2c-bc84-2cd2e12a9556 
[sap-ha-guide-9.1.4]:sap-high-availability-guide.md#10822f4f-32e7-4871-b63a-9b86c76ce761 
[sap-ha-guide-9.4]:sap-high-availability-guide.md#094bc895-31d4-4471-91cc-1513b64e406a 
[sap-ha-guide-9.5]:sap-high-availability-guide.md#2477e58f-c5a7-4a5d-9ae3-7b91022cafb5 
[sap-ha-guide-9.6]:sap-high-availability-guide.md#0ba4a6c1-cc37-4bcf-a8dc-025de4263772 
[sap-ha-guide-10]:sap-high-availability-guide.md#18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9

<span data-ttu-id="b41ed-104">A settembre 2016 Microsoft ha rilasciato una funzionalità con cui è possibile gestire più indirizzi IP virtuali usando un servizio di bilanciamento del carico interno di Azure.</span><span class="sxs-lookup"><span data-stu-id="b41ed-104">In September 2016, Microsoft released a feature where you can manage multiple virtual IP addresses by using an Azure internal load balancer.</span></span> <span data-ttu-id="b41ed-105">Questa funzionalità esiste già nel servizio di bilanciamento del carico esterno di Azure.</span><span class="sxs-lookup"><span data-stu-id="b41ed-105">This functionality already exists in the Azure external load balancer.</span></span>

<span data-ttu-id="b41ed-106">Se si dispone di una distribuzione di SAP, è possibile usare un bilanciamento del carico interno Azure per creare una configurazione del cluster Windows per SAP ASCS/SCS come documentato in [SAP NetWeaver in macchine virtuali Windows: guida alle funzionalità di disponibilità elevata][sap-ha-guide].</span><span class="sxs-lookup"><span data-stu-id="b41ed-106">If you have an SAP deployment, you can use an internal load balancer to create a Windows cluster configuration for SAP ASCS/SCS, as documented in the [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide].</span></span>

<span data-ttu-id="b41ed-107">Questo articolo si concentra sul passaggio da un'installazione di ASCS/SCS singola a una configurazione di SAP a più SID tramite l'installazione di istanze aggiuntive nel cluster ASCS/SCS di SAP in un cluster di Windows Server Failover Clustering (WSFC).</span><span class="sxs-lookup"><span data-stu-id="b41ed-107">This article focuses on how to move from a single ASCS/SCS installation to an SAP multi-SID configuration by installing additional SAP ASCS/SCS clustered instances into an existing Windows Server Failover Clustering (WSFC) cluster.</span></span> <span data-ttu-id="b41ed-108">Al termine di questo processo, verrà configurato un cluster a più SID di SAP.</span><span class="sxs-lookup"><span data-stu-id="b41ed-108">When this process is completed, you will have configured an SAP multi-SID cluster.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="b41ed-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b41ed-109">Prerequisites</span></span>
<span data-ttu-id="b41ed-110">È già stato configurato un cluster WSFC che viene usato per un'istanza di SAP ASCS/SCS, come descritto in [SAP NetWeaver in macchine virtuali Windows: guida alle funzionalità di disponibilità elevata][sap-ha-guide] e come illustrato nella figura seguente.</span><span class="sxs-lookup"><span data-stu-id="b41ed-110">You have already configured a WSFC cluster that is used for one SAP ASCS/SCS instance, as discussed in the [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide] and as shown in this diagram.</span></span>

![Istanza di SAP ASCS/SCS a disponibilità elevata][sap-ha-guide-figure-6001]

## <a name="target-architecture"></a><span data-ttu-id="b41ed-112">Architettura di destinazione</span><span class="sxs-lookup"><span data-stu-id="b41ed-112">Target architecture</span></span>

<span data-ttu-id="b41ed-113">L'obiettivo è l'installazione di più istanze cluster di SAP ABAP ASCS o SAP Java SCS nello stesso cluster WSFC, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="b41ed-113">The goal is to install multiple SAP ABAP ASCS or SAP Java SCS clustered instances in the same WSFC cluster, as illustrated here:</span></span>

![Più istanze in cluster di SAP ASCS/SCS in Azure][sap-ha-guide-figure-6002]

> [!NOTE]
><span data-ttu-id="b41ed-115">È previsto un limite di indirizzi IP front-end privati per ogni servizio di bilanciamento del carico interno di Azure.</span><span class="sxs-lookup"><span data-stu-id="b41ed-115">There is a limit to the number of private front-end IPs for each Azure internal load balancer.</span></span>
>
><span data-ttu-id="b41ed-116">Il numero massimo di istanze di SAP ASCS/SCS in un cluster WSFC è uguale al numero massimo di indirizzi IP front-end privati per ogni servizio di bilanciamento del carico interno di Azure.</span><span class="sxs-lookup"><span data-stu-id="b41ed-116">The maximum number of SAP ASCS/SCS instances in one WSFC cluster is equal to the maximum number of private front-end IPs for each Azure internal load balancer.</span></span>
>

<span data-ttu-id="b41ed-117">Per informazioni sui limiti del servizio di bilanciamento del carico vedere "IP front-end privato per ogni servizio di bilanciamento del carico" in [Limiti relativi alle reti - Azure Resource Manager][networking-limits-azure-resource-manager].</span><span class="sxs-lookup"><span data-stu-id="b41ed-117">For more information about load-balancer limits, see "Private front end IP per load balancer" in [Networking limits: Azure Resource Manager][networking-limits-azure-resource-manager].</span></span>

<span data-ttu-id="b41ed-118">Il panorama generale con due sistemi SAP a disponibilità elevata si presenta come segue:</span><span class="sxs-lookup"><span data-stu-id="b41ed-118">The complete landscape with two high-availability SAP systems would look like this:</span></span>

![Configurazione a più SID di SAP a disponibilità elevata con due SID di sistema SAP][sap-ha-guide-figure-6003]

> [!IMPORTANT]
> <span data-ttu-id="b41ed-120">Il programma di installazione deve soddisfare le condizioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="b41ed-120">The setup must meet the following conditions:</span></span>
> - <span data-ttu-id="b41ed-121">Le istanze di SAP ASCS/SCS devono condividere lo stesso cluster WSFC.</span><span class="sxs-lookup"><span data-stu-id="b41ed-121">The SAP ASCS/SCS instances must share the same WSFC cluster.</span></span>
> - <span data-ttu-id="b41ed-122">Ogni SID DBMS deve avere un cluster WSFC dedicato.</span><span class="sxs-lookup"><span data-stu-id="b41ed-122">Each DBMS SID must have its own dedicated WSFC cluster.</span></span>
> - <span data-ttu-id="b41ed-123">I server applicazioni SAP che fanno parte di un SID del sistema SAP devono avere proprie VM dedicate.</span><span class="sxs-lookup"><span data-stu-id="b41ed-123">SAP application servers that belong to one SAP system SID must have their own dedicated VMs.</span></span>


## <a name="prepare-the-infrastructure"></a><span data-ttu-id="b41ed-124">Preparare l'infrastruttura</span><span class="sxs-lookup"><span data-stu-id="b41ed-124">Prepare the infrastructure</span></span>
<span data-ttu-id="b41ed-125">Per preparare l'infrastruttura, è possibile installare un'istanza aggiuntiva di SAP ASCS/SCS con i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="b41ed-125">To prepare your infrastructure, you can install an additional SAP ASCS/SCS instance with the following parameters:</span></span>

| <span data-ttu-id="b41ed-126">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="b41ed-126">Parameter name</span></span> | <span data-ttu-id="b41ed-127">Valore</span><span class="sxs-lookup"><span data-stu-id="b41ed-127">Value</span></span> |
| --- | --- |
| <span data-ttu-id="b41ed-128">SID di SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="b41ed-128">SAP ASCS/SCS SID</span></span> |<span data-ttu-id="b41ed-129">pr1-lb-ascs</span><span class="sxs-lookup"><span data-stu-id="b41ed-129">pr1-lb-ascs</span></span> |
| <span data-ttu-id="b41ed-130">Servizio di bilanciamento del carico interno di SAP DBMS</span><span class="sxs-lookup"><span data-stu-id="b41ed-130">SAP DBMS internal load balancer</span></span> | <span data-ttu-id="b41ed-131">PR5</span><span class="sxs-lookup"><span data-stu-id="b41ed-131">PR5</span></span> |
| <span data-ttu-id="b41ed-132">Nome host virtuale SAP</span><span class="sxs-lookup"><span data-stu-id="b41ed-132">SAP virtual host name</span></span> | <span data-ttu-id="b41ed-133">pr5-sap-cl</span><span class="sxs-lookup"><span data-stu-id="b41ed-133">pr5-sap-cl</span></span> |
| <span data-ttu-id="b41ed-134">Indirizzo IP dell'host virtuale di SAP ASCS/SCS (indirizzo IP aggiuntivo del servizio di bilanciamento del carico di Azure)</span><span class="sxs-lookup"><span data-stu-id="b41ed-134">SAP ASCS/SCS virtual host IP address (additional Azure load balancer IP address)</span></span> | <span data-ttu-id="b41ed-135">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="b41ed-135">10.0.0.50</span></span> |
| <span data-ttu-id="b41ed-136">Numero di istanza di SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="b41ed-136">SAP ASCS/SCS instance number</span></span> | <span data-ttu-id="b41ed-137">50</span><span class="sxs-lookup"><span data-stu-id="b41ed-137">50</span></span> |
| <span data-ttu-id="b41ed-138">Porta di probe del servizio di bilanciamento del carico interno per l'istanza aggiuntiva di SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="b41ed-138">ILB probe port for additional SAP ASCS/SCS instance</span></span> | <span data-ttu-id="b41ed-139">62350</span><span class="sxs-lookup"><span data-stu-id="b41ed-139">62350</span></span> |

> [!NOTE]
> <span data-ttu-id="b41ed-140">Per le istanze nel cluster di SAP ASCS/SCS, ogni indirizzo IP richiede una porta probe univoca.</span><span class="sxs-lookup"><span data-stu-id="b41ed-140">For SAP ASCS/SCS cluster instances, each IP address requires a unique probe port.</span></span> <span data-ttu-id="b41ed-141">Ad esempio, se un indirizzo IP su un servizio di bilanciamento del carico interno di Azure usa la porta probe 62300, nessun altro indirizzo IP in tale servizio di bilanciamento del carico può usare la porta probe 62300.</span><span class="sxs-lookup"><span data-stu-id="b41ed-141">For example, if one IP address on an Azure internal load balancer uses probe port 62300, no other IP address on that load balancer can use probe port 62300.</span></span>
>
><span data-ttu-id="b41ed-142">Per gli scopi prefissati viene usata la porta probe 62350 perché la porta probe 62300 è già stata riservata.</span><span class="sxs-lookup"><span data-stu-id="b41ed-142">For our purposes, because probe port 62300 is already reserved, we are using probe port 62350.</span></span>

<span data-ttu-id="b41ed-143">È possibile installare le istanze aggiuntive di SAP ASCS/SCS nel cluster WSFC esistente con due nodi:</span><span class="sxs-lookup"><span data-stu-id="b41ed-143">You can install additional SAP ASCS/SCS instances in the existing WSFC cluster with two nodes:</span></span>

| <span data-ttu-id="b41ed-144">Ruolo macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="b41ed-144">Virtual machine role</span></span> | <span data-ttu-id="b41ed-145">Nome host macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="b41ed-145">Virtual machine host name</span></span> | <span data-ttu-id="b41ed-146">Indirizzo IP statico</span><span class="sxs-lookup"><span data-stu-id="b41ed-146">Static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b41ed-147">1° nodo del cluster per l'istanza di ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="b41ed-147">1st cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="b41ed-148">pr1-ascs-0</span><span class="sxs-lookup"><span data-stu-id="b41ed-148">pr1-ascs-0</span></span> |<span data-ttu-id="b41ed-149">10.0.0.10</span><span class="sxs-lookup"><span data-stu-id="b41ed-149">10.0.0.10</span></span> |
| <span data-ttu-id="b41ed-150">2° nodo del cluster per l'istanza di ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="b41ed-150">2nd cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="b41ed-151">pr1-ascs-1</span><span class="sxs-lookup"><span data-stu-id="b41ed-151">pr1-ascs-1</span></span> |<span data-ttu-id="b41ed-152">10.0.0.9</span><span class="sxs-lookup"><span data-stu-id="b41ed-152">10.0.0.9</span></span> |

### <a name="create-a-virtual-host-name-for-the-clustered-sap-ascsscs-instance-on-the-dns-server"></a><span data-ttu-id="b41ed-153">Creare un nome host virtuale per l'istanza di SAP ASCS/SCS in cluster sul server DNS</span><span class="sxs-lookup"><span data-stu-id="b41ed-153">Create a virtual host name for the clustered SAP ASCS/SCS instance on the DNS server</span></span>

<span data-ttu-id="b41ed-154">È possibile creare una voce DNS per il nome host virtuale dell'istanza di ASCS/SCS usando i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="b41ed-154">You can create a DNS entry for the virtual host name of the ASCS/SCS instance by using the following parameters:</span></span>

| <span data-ttu-id="b41ed-155">Nuovo nome host virtuale di SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="b41ed-155">New SAP ASCS/SCS virtual host name</span></span> | <span data-ttu-id="b41ed-156">Indirizzo IP associato</span><span class="sxs-lookup"><span data-stu-id="b41ed-156">Associated IP address</span></span> |
| --- | --- | --- |
|<span data-ttu-id="b41ed-157">pr5-sap-cl</span><span class="sxs-lookup"><span data-stu-id="b41ed-157">pr5-sap-cl</span></span> |<span data-ttu-id="b41ed-158">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="b41ed-158">10.0.0.50</span></span> |

<span data-ttu-id="b41ed-159">Il nuovo nome host e l'indirizzo IP vengono visualizzati in Gestore DNS, come illustrato nello screenshot seguente:</span><span class="sxs-lookup"><span data-stu-id="b41ed-159">The new host name and IP address are displayed in the DNS Manager, as shown in the following screenshot:</span></span>

![Elenco di Gestore DNS che evidenzia la voce DNS definita per il nuovo nome virtuale e indirizzo TCP/IP del cluster SAP ASCS/SCS][sap-ha-guide-figure-6004]

<span data-ttu-id="b41ed-161">La procedura per la creazione di una voce DNS è descritta in dettaglio in [Disponibilità elevata in Macchine virtuali di Azure per SAP NetWeaver][sap-ha-guide-9.1.1].</span><span class="sxs-lookup"><span data-stu-id="b41ed-161">The procedure for creating a DNS entry is also described in detail in the main [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-9.1.1].</span></span>

> [!NOTE]
> <span data-ttu-id="b41ed-162">Il nuovo indirizzo IP assegnato al nome host virtuale dell'istanza di ASCS/SCS aggiuntiva deve essere lo stesso nuovo indirizzo IP assegnato ad Azure Load Balancer SAP.</span><span class="sxs-lookup"><span data-stu-id="b41ed-162">The new IP address that you assign to the virtual host name of the additional ASCS/SCS instance must be the same as the new IP address that you assigned to the SAP Azure load balancer.</span></span>
>
><span data-ttu-id="b41ed-163">In questo scenario, l'indirizzo IP è 10.0.0.50.</span><span class="sxs-lookup"><span data-stu-id="b41ed-163">In our scenario, the IP address is 10.0.0.50.</span></span>

### <a name="add-an-ip-address-to-an-existing-azure-internal-load-balancer-by-using-powershell"></a><span data-ttu-id="b41ed-164">Aggiungere un indirizzo IP a un servizio di bilanciamento del carico interno di Azure esistente usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="b41ed-164">Add an IP address to an existing Azure internal load balancer by using PowerShell</span></span>

<span data-ttu-id="b41ed-165">Per creare più istanze di SAP ASCS/SCS nello stesso cluster WSFC, usare PowerShell per aggiungere un indirizzo IP a un servizio di bilanciamento del carico interno di Azure esistente.</span><span class="sxs-lookup"><span data-stu-id="b41ed-165">To create more than one SAP ASCS/SCS instance in the same WSFC cluster, use PowerShell to add an IP address to an existing Azure internal load balancer.</span></span> <span data-ttu-id="b41ed-166">Ogni indirizzo IP richiede regole di bilanciamento del carico, una porta probe, un pool di indirizzi IP front-end e un pool back-end propri.</span><span class="sxs-lookup"><span data-stu-id="b41ed-166">Each IP address requires its own load-balancing rules, probe port, front-end IP pool, and back-end pool.</span></span>

<span data-ttu-id="b41ed-167">Lo script seguente aggiunge un nuovo indirizzo IP a un servizio di bilanciamento del carico esistente.</span><span class="sxs-lookup"><span data-stu-id="b41ed-167">The following script adds a new IP address to an existing load balancer.</span></span> <span data-ttu-id="b41ed-168">Aggiornare le variabili PowerShell per l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="b41ed-168">Update the PowerShell variables for your environment.</span></span> <span data-ttu-id="b41ed-169">Lo script creerà tutte le regole di bilanciamento del carico necessarie per tutte le porte SAP ASCS /SCS.</span><span class="sxs-lookup"><span data-stu-id="b41ed-169">The script will create all needed load-balancing rules for all SAP ASCS/SCS ports.</span></span>

```powershell

# Select-AzureRmSubscription -SubscriptionId <xxxxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx>
Clear-Host
$ResourceGroupName = "SAP-MULTI-SID-Landscape"      # Existing resource group name
$VNetName = "pr2-vnet"                        # Existing virtual network name
$SubnetName = "Subnet"                        # Existing subnet name
$ILBName = "pr2-lb-ascs"                      # Existing ILB name                      
$ILBIP = "10.0.0.50"                          # New IP address
$VMNames = "pr2-ascs-0","pr2-ascs-1"          # Existing cluster virtual machine names
$SAPInstanceNumber = 50                       # SAP ASCS/SCS instance number: must be a unique value for each cluster
[int]$ProbePort = "623$SAPInstanceNumber"     # Probe port: must be a unique value for each IP and load balancer

$ILB = Get-AzureRmLoadBalancer -Name $ILBName -ResourceGroupName $ResourceGroupName

$count = $ILB.FrontendIpConfigurations.Count + 1
$FrontEndConfigurationName ="lbFrontendASCS$count"
$LBProbeName = "lbProbeASCS$count"

# Get the Azure VNet and subnet
$VNet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName
$Subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $VNet -Name $SubnetName

# Add second front-end and probe configuration
Write-Host "Adding new front end IP Pool '$FrontEndConfigurationName' ..." -ForegroundColor Green
$ILB | Add-AzureRmLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -PrivateIpAddress $ILBIP -SubnetId $Subnet.Id
$ILB | Add-AzureRmLoadBalancerProbeConfig -Name $LBProbeName  -Protocol Tcp -Port $Probeport -ProbeCount 2 -IntervalInSeconds 10  | Set-AzureRmLoadBalancer

# Get new updated configuration
$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName
# Get new updated LP FrontendIP COnfig
$FEConfig = Get-AzureRmLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -LoadBalancer $ILB
$HealthProbe  = Get-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -LoadBalancer $ILB

# Add new back-end configuration into existing ILB
$BackEndConfigurationName  = "backendPoolASCS$count"
Write-Host "Adding new backend Pool '$BackEndConfigurationName' ..." -ForegroundColor Green
$BEConfig = Add-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB | Set-AzureRmLoadBalancer

# Get new updated config
$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName

# Assign VM NICs to backend pool
$BEPool = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB
foreach($VMName in $VMNames){
        $VM = Get-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VMName
        $NICName = ($VM.NetworkInterfaceIDs[0].Split('/') | select -last 1)        
        $NIC = Get-AzureRmNetworkInterface -name $NICName -ResourceGroupName $ResourceGroupName                
        $NIC.IpConfigurations[0].LoadBalancerBackendAddressPools += $BEPool
        Write-Host "Assigning network card '$NICName' of the '$VMName' VM to the backend pool '$BackEndConfigurationName' ..." -ForegroundColor Green
        Set-AzureRmNetworkInterface -NetworkInterface $NIC
        #start-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VM.Name
}


# Create load-balancing rules
$Ports = "445","32$SAPInstanceNumber","33$SAPInstanceNumber","36$SAPInstanceNumber","39$SAPInstanceNumber","5985","81$SAPInstanceNumber","5$SAPInstanceNumber`13","5$SAPInstanceNumber`14","5$SAPInstanceNumber`16"
$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName
$FEConfig = get-AzureRMLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -LoadBalancer $ILB
$BEConfig = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB
$HealthProbe  = Get-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -LoadBalancer $ILB

Write-Host "Creating load balancing rules for the ports: '$Ports' ... " -ForegroundColor Green

foreach ($Port in $Ports) {

        $LBConfigrulename = "lbrule$Port" + "_$count"
        Write-Host "Creating load balancing rule '$LBConfigrulename' for the port '$Port' ..." -ForegroundColor Green

        $ILB | Add-AzureRmLoadBalancerRuleConfig -Name $LBConfigRuleName -FrontendIpConfiguration $FEConfig  -BackendAddressPool $BEConfig -Probe $HealthProbe -Protocol tcp -FrontendPort  $Port -BackendPort $Port -IdleTimeoutInMinutes 30 -LoadDistribution Default -EnableFloatingIP   
}

$ILB | Set-AzureRmLoadBalancer

Write-Host "Succesfully added new IP '$ILBIP' to the internal load balancer '$ILBName'!" -ForegroundColor Green

```
<span data-ttu-id="b41ed-170">Dopo l'esecuzione dello script, i risultati vengono visualizzati nel portale di Azure, come illustrato nello screenshot seguente:</span><span class="sxs-lookup"><span data-stu-id="b41ed-170">After the script has run, the results are displayed in the Azure portal, as shown in the following screenshot:</span></span>

![Nuovo pool di indirizzi IP front-end nel portale di Azure][sap-ha-guide-figure-6005]

### <a name="add-disks-to-cluster-machines-and-configure-the-sios-cluster-share-disk"></a><span data-ttu-id="b41ed-172">Aggiungere dischi ai computer del cluster e configurare il disco cluster condiviso SIOS</span><span class="sxs-lookup"><span data-stu-id="b41ed-172">Add disks to cluster machines, and configure the SIOS cluster share disk</span></span>

<span data-ttu-id="b41ed-173">È necessario aggiungere un nuovo disco cluster condiviso per ogni istanza di SAP ASCS/SCS aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="b41ed-173">You must add a new cluster share disk for each additional SAP ASCS/SCS instance.</span></span> <span data-ttu-id="b41ed-174">Attualmente, il disco cluster condiviso Windows Server 2012 R2 WSFC viene usato dalla soluzione software SIOS DataKeeper.</span><span class="sxs-lookup"><span data-stu-id="b41ed-174">For Windows Server 2012 R2, the WSFC cluster share disk currently in use is the SIOS DataKeeper software solution.</span></span>

<span data-ttu-id="b41ed-175">Eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="b41ed-175">Do the following:</span></span>
1. <span data-ttu-id="b41ed-176">Aggiungere un altro disco o più dischi con la stessa dimensione (da sottoporre a striping) su ciascuno dei nodi del cluster e formattarli.</span><span class="sxs-lookup"><span data-stu-id="b41ed-176">Add an additional disk or disks of the same size (which you need to stripe) to each of the cluster nodes, and format them.</span></span>
2. <span data-ttu-id="b41ed-177">Configurare la replica di archiviazione con SIOS DataKeeper.</span><span class="sxs-lookup"><span data-stu-id="b41ed-177">Configure storage replication with SIOS DataKeeper.</span></span>

<span data-ttu-id="b41ed-178">Questa procedura presuppone che SIOS DataKeeper sia già stato installato nei computer del cluster WSFC.</span><span class="sxs-lookup"><span data-stu-id="b41ed-178">This procedure assumes that you have already installed SIOS DataKeeper on the WSFC cluster machines.</span></span> <span data-ttu-id="b41ed-179">Se è stato installato, è ora necessario configurare la replica tra le macchine.</span><span class="sxs-lookup"><span data-stu-id="b41ed-179">If you have installed it, you must now configure replication between the machines.</span></span> <span data-ttu-id="b41ed-180">La procedura è descritta in dettaglio in [Disponibilità elevata in Macchine virtuali di Azure per SAP NetWeaver][sap-ha-guide-8.12.3.3].</span><span class="sxs-lookup"><span data-stu-id="b41ed-180">The process is described in detail in the main [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-8.12.3.3].</span></span>  

![Mirroring sincrono di DataKeeper per il nuovo disco condiviso di SAP ASCS/SCS è attivo][sap-ha-guide-figure-6006]

### <a name="deploy-vms-for-sap-application-servers-and-dbms-cluster"></a><span data-ttu-id="b41ed-182">Distribuire le VM per i server applicazioni SAP e il cluster DBMS</span><span class="sxs-lookup"><span data-stu-id="b41ed-182">Deploy VMs for SAP application servers and DBMS cluster</span></span>

<span data-ttu-id="b41ed-183">Per completare la preparazione dell'infrastruttura per il secondo sistema SAP, procedere come segue:</span><span class="sxs-lookup"><span data-stu-id="b41ed-183">To complete the infrastructure preparation for the second SAP system, do the following:</span></span>

1. <span data-ttu-id="b41ed-184">Distribuire VM dedicate per i server applicazioni SAP e inserirle nel proprio gruppo di disponibilità dedicato.</span><span class="sxs-lookup"><span data-stu-id="b41ed-184">Deploy dedicated VMs for SAP application servers and put them in their own dedicated availability group.</span></span>
2. <span data-ttu-id="b41ed-185">Distribuire VM dedicate per il cluster DBMS e inserirle nel proprio gruppo di disponibilità dedicato.</span><span class="sxs-lookup"><span data-stu-id="b41ed-185">Deploy dedicated VMs for DBMS cluster and put them in their own dedicated availability group.</span></span>


## <a name="install-the-second-sap-sid2-netweaver-system"></a><span data-ttu-id="b41ed-186">Installare il secondo sistema SAP NetWeaver SID2</span><span class="sxs-lookup"><span data-stu-id="b41ed-186">Install the second SAP SID2 NetWeaver system</span></span>

<span data-ttu-id="b41ed-187">Il processo completo di installazione di un secondo sistema SAP SID2 è descritto in [Disponibilità elevata in Macchine virtuali di Azure per SAP NetWeaver][sap-ha-guide-9].</span><span class="sxs-lookup"><span data-stu-id="b41ed-187">The complete process of installing a second SAP SID2 system is described in the main [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-9].</span></span>

<span data-ttu-id="b41ed-188">La procedura di alto livello è la seguente:</span><span class="sxs-lookup"><span data-stu-id="b41ed-188">The high-level procedure is as follows:</span></span>

1. <span data-ttu-id="b41ed-189">[Installare il primo nodo del cluster SAP][sap-ha-guide-9.1.2].</span><span class="sxs-lookup"><span data-stu-id="b41ed-189">[Install the SAP first cluster node][sap-ha-guide-9.1.2].</span></span>  
 <span data-ttu-id="b41ed-190">In questo passaggio si sta installando SAP con un'istanza di ASCS/SCS a disponibilità elevata nel **nodo 1 del cluster WSFC ESISTENTE**.</span><span class="sxs-lookup"><span data-stu-id="b41ed-190">In this step, you are installing SAP with a high-availability ASCS/SCS instance on the **EXISTING WSFC cluster node 1**.</span></span>

2. <span data-ttu-id="b41ed-191">[Modificare il profilo SAP dell'istanza di ASCS/SCS][sap-ha-guide-9.1.3].</span><span class="sxs-lookup"><span data-stu-id="b41ed-191">[Modify the SAP profile of the ASCS/SCS instance][sap-ha-guide-9.1.3].</span></span>

3. <span data-ttu-id="b41ed-192">[Configurare una porta probe][sap-ha-guide-9.1.4].</span><span class="sxs-lookup"><span data-stu-id="b41ed-192">[Configure a probe port][sap-ha-guide-9.1.4].</span></span>  
 <span data-ttu-id="b41ed-193">In questo passaggio si sta configurando una porta probe SAP-SID2-IP della risorsa nel cluster SAP tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b41ed-193">In this step, you are configuring an SAP cluster resource SAP-SID2-IP probe port by using PowerShell.</span></span> <span data-ttu-id="b41ed-194">Eseguire questa configurazione in uno dei nodi del cluster SAP ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="b41ed-194">Execute this configuration on one of the SAP ASCS/SCS cluster nodes.</span></span>

4. <span data-ttu-id="b41ed-195">[Installare l'istanza di database][sap-ha-guide-9.2].</span><span class="sxs-lookup"><span data-stu-id="b41ed-195">[Install the database instance][sap-ha-guide-9.2].</span></span>  
 <span data-ttu-id="b41ed-196">In questo passaggio si sta installando DBMS in un cluster WSFC dedicato.</span><span class="sxs-lookup"><span data-stu-id="b41ed-196">In this step, you are installing DBMS on a dedicated WSFC cluster.</span></span>

5. <span data-ttu-id="b41ed-197">[Installare il secondo nodo del cluster][sap-ha-guide-9.3].</span><span class="sxs-lookup"><span data-stu-id="b41ed-197">[Install the second cluster node][sap-ha-guide-9.3].</span></span>  
 <span data-ttu-id="b41ed-198">In questo passaggio si sta installando SAP con un'istanza di ASCS/SCS a disponibilità elevata nel nodo 2 del cluster WSFC esistente.</span><span class="sxs-lookup"><span data-stu-id="b41ed-198">In this step, you are installing SAP with a high-availability ASCS/SCS instance on the existing WSFC cluster node 2.</span></span>

6. <span data-ttu-id="b41ed-199">Aprire le porte di Windows Firewall per l'istanza di SAP ASCS/SCS e ProbePort.</span><span class="sxs-lookup"><span data-stu-id="b41ed-199">Open Windows Firewall ports for the SAP ASCS/SCS instance and ProbePort.</span></span>  
 <span data-ttu-id="b41ed-200">In entrambi i nodi del cluster usati per le istanze di SAP ASCS/SCS si stanno aprendo tutte le porte di Windows Firewall usate da SAP ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="b41ed-200">On both cluster nodes that are used for SAP ASCS/SCS instances, you are opening all Windows Firewall ports that are used by SAP ASCS/SCS.</span></span> <span data-ttu-id="b41ed-201">Queste porte sono elencate in [Disponibilità elevata in Macchine virtuali di Azure per SAP NetWeaver][sap-ha-guide-8.8].</span><span class="sxs-lookup"><span data-stu-id="b41ed-201">These ports are listed in the [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-8.8].</span></span>  
 <span data-ttu-id="b41ed-202">Aprire anche la porta probe del servizio di bilanciamento del carico interno di Azure, ovvero 62350, in questo scenario.</span><span class="sxs-lookup"><span data-stu-id="b41ed-202">Also open the Azure internal load balancer probe port, which is 62350 in our scenario.</span></span>

7. <span data-ttu-id="b41ed-203">[Cambiare il tipo di avvio dell'istanza del servizio Windows SAP ERS][sap-ha-guide-9.4].</span><span class="sxs-lookup"><span data-stu-id="b41ed-203">[Change the start type of the SAP ERS Windows service instance][sap-ha-guide-9.4].</span></span>

8. <span data-ttu-id="b41ed-204">[Installare Primary Application Server (PAS) SAP][sap-ha-guide-9.5] nella nuova VM dedicata.</span><span class="sxs-lookup"><span data-stu-id="b41ed-204">[Install the SAP primary application server][sap-ha-guide-9.5] on the new dedicated VM.</span></span>

9. <span data-ttu-id="b41ed-205">[Installare il server applicazione SAP aggiuntivo][sap-ha-guide-9.6] nella nuova VM dedicata.</span><span class="sxs-lookup"><span data-stu-id="b41ed-205">[Install the SAP additional application server][sap-ha-guide-9.6] on the new dedicated VM.</span></span>

10. <span data-ttu-id="b41ed-206">[Testare il failover e la replica SIOS dell'istanza di SAP ASCS/SCS][sap-ha-guide-10].</span><span class="sxs-lookup"><span data-stu-id="b41ed-206">[Test the SAP ASCS/SCS instance failover and SIOS replication][sap-ha-guide-10].</span></span>

## <a name="next-steps"></a><span data-ttu-id="b41ed-207">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b41ed-207">Next steps</span></span>

- <span data-ttu-id="b41ed-208">[Limiti relativi alle reti: Azure Resource Manager][networking-limits-azure-resource-manager]</span><span class="sxs-lookup"><span data-stu-id="b41ed-208">[Networking limits: Azure Resource Manager][networking-limits-azure-resource-manager]</span></span>
- <span data-ttu-id="b41ed-209">[Più indirizzi VIP per Azure Load Balancer][load-balancer-multivip-overview]</span><span class="sxs-lookup"><span data-stu-id="b41ed-209">[Multiple VIPs for Azure Load Balancer][load-balancer-multivip-overview]</span></span>
- <span data-ttu-id="b41ed-210">[SAP NetWeaver in macchine virtuali Windows: guida alle funzionalità di disponibilità elevata][sap-ha-guide]</span><span class="sxs-lookup"><span data-stu-id="b41ed-210">[Guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide]</span></span>
