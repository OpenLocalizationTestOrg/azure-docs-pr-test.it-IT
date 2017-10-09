---
title: una configurazione di multi-SID di SAP in Azure aaaCreate | Documenti Microsoft
description: "Configurazione di multi-SID Guida toohigh disponibilità SAP NetWeaver in macchine virtuali Windows"
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
ms.openlocfilehash: e2a4b12928231743c59af86dab72595ad38d364b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-sap-netweaver-multi-sid-configuration"></a><span data-ttu-id="7e1cb-103">Creare una configurazione di SAP NetWeaver a più SID</span><span class="sxs-lookup"><span data-stu-id="7e1cb-103">Create an SAP NetWeaver multi-SID configuration</span></span>

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

<span data-ttu-id="7e1cb-104">A settembre 2016 Microsoft ha rilasciato una funzionalità con cui è possibile gestire più indirizzi IP virtuali usando un servizio di bilanciamento del carico interno di Azure.</span><span class="sxs-lookup"><span data-stu-id="7e1cb-104">In September 2016, Microsoft released a feature where you can manage multiple virtual IP addresses by using an Azure internal load balancer.</span></span> <span data-ttu-id="7e1cb-105">Questa funzionalità esiste già nel servizio di bilanciamento del carico esterno Azure hello.</span><span class="sxs-lookup"><span data-stu-id="7e1cb-105">This functionality already exists in hello Azure external load balancer.</span></span>

<span data-ttu-id="7e1cb-106">Se si dispone di una distribuzione di SAP, è possibile utilizzare un toocreate bilanciamento di carico interno una configurazione cluster di Windows per SAP ASCS/SCS, come documentato in hello [Guida per la disponibilità elevata di SAP NetWeaver in macchine virtuali Windows] [ sap-ha-guide].</span><span class="sxs-lookup"><span data-stu-id="7e1cb-106">If you have an SAP deployment, you can use an internal load balancer toocreate a Windows cluster configuration for SAP ASCS/SCS, as documented in hello [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide].</span></span>

<span data-ttu-id="7e1cb-107">Questo articolo illustra come toomove da una singola ASCS/SCS installazione tooan SAP più SID configurazione installando aggiuntive SAP ASCS/SCS istanze del cluster in un cluster di Windows Server Failover Clustering (WSFC) esistente.</span><span class="sxs-lookup"><span data-stu-id="7e1cb-107">This article focuses on how toomove from a single ASCS/SCS installation tooan SAP multi-SID configuration by installing additional SAP ASCS/SCS clustered instances into an existing Windows Server Failover Clustering (WSFC) cluster.</span></span> <span data-ttu-id="7e1cb-108">Al termine di questo processo, verrà configurato un cluster a più SID di SAP.</span><span class="sxs-lookup"><span data-stu-id="7e1cb-108">When this process is completed, you will have configured an SAP multi-SID cluster.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="7e1cb-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7e1cb-109">Prerequisites</span></span>
<span data-ttu-id="7e1cb-110">È già stato configurato un cluster WSFC in cui viene utilizzato per un'istanza di SAP ASCS/SCS, come descritto in hello [Guida per la disponibilità elevata di SAP NetWeaver in macchine virtuali Windows] [ sap-ha-guide] e come illustrato nella figura seguente.</span><span class="sxs-lookup"><span data-stu-id="7e1cb-110">You have already configured a WSFC cluster that is used for one SAP ASCS/SCS instance, as discussed in hello [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide] and as shown in this diagram.</span></span>

![Istanza di SAP ASCS/SCS a disponibilità elevata][sap-ha-guide-figure-6001]

## <a name="target-architecture"></a><span data-ttu-id="7e1cb-112">Architettura di destinazione</span><span class="sxs-lookup"><span data-stu-id="7e1cb-112">Target architecture</span></span>

<span data-ttu-id="7e1cb-113">Hello obiettivo è tooinstall più ABAP di SAP ASCS o SCS Java di SAP in cluster le istanze in hello stesso cluster WSFC, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="7e1cb-113">hello goal is tooinstall multiple SAP ABAP ASCS or SAP Java SCS clustered instances in hello same WSFC cluster, as illustrated here:</span></span>

![Più istanze in cluster di SAP ASCS/SCS in Azure][sap-ha-guide-figure-6002]

> [!NOTE]
><span data-ttu-id="7e1cb-115">È un toohello limita il numero di indirizzi IP privati di front-end per ogni servizio di bilanciamento del carico interno di Azure.</span><span class="sxs-lookup"><span data-stu-id="7e1cb-115">There is a limit toohello number of private front-end IPs for each Azure internal load balancer.</span></span>
>
><span data-ttu-id="7e1cb-116">numero massimo di Hello di istanze di SAP ASCS/SCS in un cluster WSFC è uguale toohello il numero massimo di indirizzi IP privati di front-end per ogni servizio di bilanciamento del carico interno di Azure.</span><span class="sxs-lookup"><span data-stu-id="7e1cb-116">hello maximum number of SAP ASCS/SCS instances in one WSFC cluster is equal toohello maximum number of private front-end IPs for each Azure internal load balancer.</span></span>
>

<span data-ttu-id="7e1cb-117">Per informazioni sui limiti del servizio di bilanciamento del carico vedere "IP front-end privato per ogni servizio di bilanciamento del carico" in [Limiti relativi alle reti - Azure Resource Manager][networking-limits-azure-resource-manager].</span><span class="sxs-lookup"><span data-stu-id="7e1cb-117">For more information about load-balancer limits, see "Private front end IP per load balancer" in [Networking limits: Azure Resource Manager][networking-limits-azure-resource-manager].</span></span>

<span data-ttu-id="7e1cb-118">Panoramica di completa Hello con due sistemi SAP a disponibilità elevata è analogo al seguente:</span><span class="sxs-lookup"><span data-stu-id="7e1cb-118">hello complete landscape with two high-availability SAP systems would look like this:</span></span>

![Configurazione a più SID di SAP a disponibilità elevata con due SID di sistema SAP][sap-ha-guide-figure-6003]

> [!IMPORTANT]
> <span data-ttu-id="7e1cb-120">il programma di installazione di Hello deve soddisfare hello seguenti condizioni:</span><span class="sxs-lookup"><span data-stu-id="7e1cb-120">hello setup must meet hello following conditions:</span></span>
> - <span data-ttu-id="7e1cb-121">Hello devono condividere le istanze SAP ASCS/SCS hello stesso cluster WSFC.</span><span class="sxs-lookup"><span data-stu-id="7e1cb-121">hello SAP ASCS/SCS instances must share hello same WSFC cluster.</span></span>
> - <span data-ttu-id="7e1cb-122">Ogni SID DBMS deve avere un cluster WSFC dedicato.</span><span class="sxs-lookup"><span data-stu-id="7e1cb-122">Each DBMS SID must have its own dedicated WSFC cluster.</span></span>
> - <span data-ttu-id="7e1cb-123">I server applicazioni SAP che appartengono a sistema SAP tooone SID devono avere le proprie macchine virtuali di dedicato.</span><span class="sxs-lookup"><span data-stu-id="7e1cb-123">SAP application servers that belong tooone SAP system SID must have their own dedicated VMs.</span></span>


## <a name="prepare-hello-infrastructure"></a><span data-ttu-id="7e1cb-124">Preparare l'infrastruttura di hello</span><span class="sxs-lookup"><span data-stu-id="7e1cb-124">Prepare hello infrastructure</span></span>
<span data-ttu-id="7e1cb-125">tooprepare dell'infrastruttura, è possibile installare un'altra istanza di SAP ASCS/SCS con hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="7e1cb-125">tooprepare your infrastructure, you can install an additional SAP ASCS/SCS instance with hello following parameters:</span></span>

| <span data-ttu-id="7e1cb-126">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="7e1cb-126">Parameter name</span></span> | <span data-ttu-id="7e1cb-127">Valore</span><span class="sxs-lookup"><span data-stu-id="7e1cb-127">Value</span></span> |
| --- | --- |
| <span data-ttu-id="7e1cb-128">SID di SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="7e1cb-128">SAP ASCS/SCS SID</span></span> |<span data-ttu-id="7e1cb-129">pr1-lb-ascs</span><span class="sxs-lookup"><span data-stu-id="7e1cb-129">pr1-lb-ascs</span></span> |
| <span data-ttu-id="7e1cb-130">Servizio di bilanciamento del carico interno di SAP DBMS</span><span class="sxs-lookup"><span data-stu-id="7e1cb-130">SAP DBMS internal load balancer</span></span> | <span data-ttu-id="7e1cb-131">PR5</span><span class="sxs-lookup"><span data-stu-id="7e1cb-131">PR5</span></span> |
| <span data-ttu-id="7e1cb-132">Nome host virtuale SAP</span><span class="sxs-lookup"><span data-stu-id="7e1cb-132">SAP virtual host name</span></span> | <span data-ttu-id="7e1cb-133">pr5-sap-cl</span><span class="sxs-lookup"><span data-stu-id="7e1cb-133">pr5-sap-cl</span></span> |
| <span data-ttu-id="7e1cb-134">Indirizzo IP dell'host virtuale di SAP ASCS/SCS (indirizzo IP aggiuntivo del servizio di bilanciamento del carico di Azure)</span><span class="sxs-lookup"><span data-stu-id="7e1cb-134">SAP ASCS/SCS virtual host IP address (additional Azure load balancer IP address)</span></span> | <span data-ttu-id="7e1cb-135">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="7e1cb-135">10.0.0.50</span></span> |
| <span data-ttu-id="7e1cb-136">Numero di istanza di SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="7e1cb-136">SAP ASCS/SCS instance number</span></span> | <span data-ttu-id="7e1cb-137">50</span><span class="sxs-lookup"><span data-stu-id="7e1cb-137">50</span></span> |
| <span data-ttu-id="7e1cb-138">Porta di probe del servizio di bilanciamento del carico interno per l'istanza aggiuntiva di SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="7e1cb-138">ILB probe port for additional SAP ASCS/SCS instance</span></span> | <span data-ttu-id="7e1cb-139">62350</span><span class="sxs-lookup"><span data-stu-id="7e1cb-139">62350</span></span> |

> [!NOTE]
> <span data-ttu-id="7e1cb-140">Per le istanze nel cluster di SAP ASCS/SCS, ogni indirizzo IP richiede una porta probe univoca.</span><span class="sxs-lookup"><span data-stu-id="7e1cb-140">For SAP ASCS/SCS cluster instances, each IP address requires a unique probe port.</span></span> <span data-ttu-id="7e1cb-141">Ad esempio, se un indirizzo IP su un servizio di bilanciamento del carico interno di Azure usa la porta probe 62300, nessun altro indirizzo IP in tale servizio di bilanciamento del carico può usare la porta probe 62300.</span><span class="sxs-lookup"><span data-stu-id="7e1cb-141">For example, if one IP address on an Azure internal load balancer uses probe port 62300, no other IP address on that load balancer can use probe port 62300.</span></span>
>
><span data-ttu-id="7e1cb-142">Per gli scopi prefissati viene usata la porta probe 62350 perché la porta probe 62300 è già stata riservata.</span><span class="sxs-lookup"><span data-stu-id="7e1cb-142">For our purposes, because probe port 62300 is already reserved, we are using probe port 62350.</span></span>

<span data-ttu-id="7e1cb-143">È possibile installare altre istanze di SAP ASCS/SCS nel cluster WSFC esistente hello con due nodi:</span><span class="sxs-lookup"><span data-stu-id="7e1cb-143">You can install additional SAP ASCS/SCS instances in hello existing WSFC cluster with two nodes:</span></span>

| <span data-ttu-id="7e1cb-144">Ruolo macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="7e1cb-144">Virtual machine role</span></span> | <span data-ttu-id="7e1cb-145">Nome host macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="7e1cb-145">Virtual machine host name</span></span> | <span data-ttu-id="7e1cb-146">Indirizzo IP statico</span><span class="sxs-lookup"><span data-stu-id="7e1cb-146">Static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7e1cb-147">1° nodo del cluster per l'istanza di ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="7e1cb-147">1st cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="7e1cb-148">pr1-ascs-0</span><span class="sxs-lookup"><span data-stu-id="7e1cb-148">pr1-ascs-0</span></span> |<span data-ttu-id="7e1cb-149">10.0.0.10</span><span class="sxs-lookup"><span data-stu-id="7e1cb-149">10.0.0.10</span></span> |
| <span data-ttu-id="7e1cb-150">2° nodo del cluster per l'istanza di ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="7e1cb-150">2nd cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="7e1cb-151">pr1-ascs-1</span><span class="sxs-lookup"><span data-stu-id="7e1cb-151">pr1-ascs-1</span></span> |<span data-ttu-id="7e1cb-152">10.0.0.9</span><span class="sxs-lookup"><span data-stu-id="7e1cb-152">10.0.0.9</span></span> |

### <a name="create-a-virtual-host-name-for-hello-clustered-sap-ascsscs-instance-on-hello-dns-server"></a><span data-ttu-id="7e1cb-153">Creare un nome host virtuale per l'istanza di SAP ASCS/SCS hello cluster sul server DNS hello</span><span class="sxs-lookup"><span data-stu-id="7e1cb-153">Create a virtual host name for hello clustered SAP ASCS/SCS instance on hello DNS server</span></span>

<span data-ttu-id="7e1cb-154">È possibile creare una voce DNS per il nome host virtuale hello dell'istanza di hello ASCS/SCS tramite hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="7e1cb-154">You can create a DNS entry for hello virtual host name of hello ASCS/SCS instance by using hello following parameters:</span></span>

| <span data-ttu-id="7e1cb-155">Nuovo nome host virtuale di SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="7e1cb-155">New SAP ASCS/SCS virtual host name</span></span> | <span data-ttu-id="7e1cb-156">Indirizzo IP associato</span><span class="sxs-lookup"><span data-stu-id="7e1cb-156">Associated IP address</span></span> |
| --- | --- | --- |
|<span data-ttu-id="7e1cb-157">pr5-sap-cl</span><span class="sxs-lookup"><span data-stu-id="7e1cb-157">pr5-sap-cl</span></span> |<span data-ttu-id="7e1cb-158">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="7e1cb-158">10.0.0.50</span></span> |

<span data-ttu-id="7e1cb-159">nuovo nome host di Hello e indirizzo IP vengono visualizzate nella hello gestore DNS, come illustrato nella seguente schermata hello:</span><span class="sxs-lookup"><span data-stu-id="7e1cb-159">hello new host name and IP address are displayed in hello DNS Manager, as shown in hello following screenshot:</span></span>

![Elenco di gestore DNS evidenziazione hello definito voce DNS per hello nuovo SAP ASCS/SCS virtuale nome cluster e indirizzo TCP/IP][sap-ha-guide-figure-6004]

<span data-ttu-id="7e1cb-161">Hello per la creazione di una voce DNS anche descritta in dettaglio in hello principale [Guida per la disponibilità elevata di SAP NetWeaver in macchine virtuali Windows][sap-ha-guide-9.1.1].</span><span class="sxs-lookup"><span data-stu-id="7e1cb-161">hello procedure for creating a DNS entry is also described in detail in hello main [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-9.1.1].</span></span>

> [!NOTE]
> <span data-ttu-id="7e1cb-162">Hello nuovo indirizzo IP che si assegna il nome host virtuale toohello di hello aggiuntive ASCS/SCS dell'istanza deve essere hello come hello nuovo indirizzo IP di bilanciamento del carico di Azure SAP toohello assegnato.</span><span class="sxs-lookup"><span data-stu-id="7e1cb-162">hello new IP address that you assign toohello virtual host name of hello additional ASCS/SCS instance must be hello same as hello new IP address that you assigned toohello SAP Azure load balancer.</span></span>
>
><span data-ttu-id="7e1cb-163">In questo scenario, l'indirizzo IP hello è 10.0.0.50.</span><span class="sxs-lookup"><span data-stu-id="7e1cb-163">In our scenario, hello IP address is 10.0.0.50.</span></span>

### <a name="add-an-ip-address-tooan-existing-azure-internal-load-balancer-by-using-powershell"></a><span data-ttu-id="7e1cb-164">Aggiungere un IP indirizzo tooan esistente Azure bilanciamento del carico interno tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="7e1cb-164">Add an IP address tooan existing Azure internal load balancer by using PowerShell</span></span>

<span data-ttu-id="7e1cb-165">toocreate più di un'istanza di SAP ASCS/SCS in hello WSFC stesso cluster, utilizzare PowerShell tooadd un tooan di indirizzo IP del bilanciamento del carico interno di Azure esistente.</span><span class="sxs-lookup"><span data-stu-id="7e1cb-165">toocreate more than one SAP ASCS/SCS instance in hello same WSFC cluster, use PowerShell tooadd an IP address tooan existing Azure internal load balancer.</span></span> <span data-ttu-id="7e1cb-166">Ogni indirizzo IP richiede regole di bilanciamento del carico, una porta probe, un pool di indirizzi IP front-end e un pool back-end propri.</span><span class="sxs-lookup"><span data-stu-id="7e1cb-166">Each IP address requires its own load-balancing rules, probe port, front-end IP pool, and back-end pool.</span></span>

<span data-ttu-id="7e1cb-167">Hello script seguente aggiunge un nuovo IP indirizzo tooan bilanciamento del carico esistente.</span><span class="sxs-lookup"><span data-stu-id="7e1cb-167">hello following script adds a new IP address tooan existing load balancer.</span></span> <span data-ttu-id="7e1cb-168">Aggiornare le variabili di PowerShell hello per l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="7e1cb-168">Update hello PowerShell variables for your environment.</span></span> <span data-ttu-id="7e1cb-169">script Hello creerà necessarie tutte le regole di bilanciamento del carico per tutte le porte di SAP ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="7e1cb-169">hello script will create all needed load-balancing rules for all SAP ASCS/SCS ports.</span></span>

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

# Get hello Azure VNet and subnet
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

# Assign VM NICs toobackend pool
$BEPool = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB
foreach($VMName in $VMNames){
        $VM = Get-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VMName
        $NICName = ($VM.NetworkInterfaceIDs[0].Split('/') | select -last 1)        
        $NIC = Get-AzureRmNetworkInterface -name $NICName -ResourceGroupName $ResourceGroupName                
        $NIC.IpConfigurations[0].LoadBalancerBackendAddressPools += $BEPool
        Write-Host "Assigning network card '$NICName' of hello '$VMName' VM toohello backend pool '$BackEndConfigurationName' ..." -ForegroundColor Green
        Set-AzureRmNetworkInterface -NetworkInterface $NIC
        #start-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VM.Name
}


# Create load-balancing rules
$Ports = "445","32$SAPInstanceNumber","33$SAPInstanceNumber","36$SAPInstanceNumber","39$SAPInstanceNumber","5985","81$SAPInstanceNumber","5$SAPInstanceNumber`13","5$SAPInstanceNumber`14","5$SAPInstanceNumber`16"
$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName
$FEConfig = get-AzureRMLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -LoadBalancer $ILB
$BEConfig = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB
$HealthProbe  = Get-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -LoadBalancer $ILB

Write-Host "Creating load balancing rules for hello ports: '$Ports' ... " -ForegroundColor Green

foreach ($Port in $Ports) {

        $LBConfigrulename = "lbrule$Port" + "_$count"
        Write-Host "Creating load balancing rule '$LBConfigrulename' for hello port '$Port' ..." -ForegroundColor Green

        $ILB | Add-AzureRmLoadBalancerRuleConfig -Name $LBConfigRuleName -FrontendIpConfiguration $FEConfig  -BackendAddressPool $BEConfig -Probe $HealthProbe -Protocol tcp -FrontendPort  $Port -BackendPort $Port -IdleTimeoutInMinutes 30 -LoadDistribution Default -EnableFloatingIP   
}

$ILB | Set-AzureRmLoadBalancer

Write-Host "Succesfully added new IP '$ILBIP' toohello internal load balancer '$ILBName'!" -ForegroundColor Green

```
<span data-ttu-id="7e1cb-170">Dopo l'esecuzione di script hello, hello risultati vengono visualizzati in hello portale di Azure, come illustrato nella seguente schermata hello:</span><span class="sxs-lookup"><span data-stu-id="7e1cb-170">After hello script has run, hello results are displayed in hello Azure portal, as shown in hello following screenshot:</span></span>

![Nuovo pool IP front-end di hello portale di Azure][sap-ha-guide-figure-6005]

### <a name="add-disks-toocluster-machines-and-configure-hello-sios-cluster-share-disk"></a><span data-ttu-id="7e1cb-172">Aggiungere dischi toocluster macchine e configurare hello SIOS cluster quota disco</span><span class="sxs-lookup"><span data-stu-id="7e1cb-172">Add disks toocluster machines, and configure hello SIOS cluster share disk</span></span>

<span data-ttu-id="7e1cb-173">È necessario aggiungere un nuovo disco cluster condiviso per ogni istanza di SAP ASCS/SCS aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="7e1cb-173">You must add a new cluster share disk for each additional SAP ASCS/SCS instance.</span></span> <span data-ttu-id="7e1cb-174">Per Windows Server 2012 R2, disco condivisione del cluster WSFC hello attualmente in uso è una soluzione software SIOS DataKeeper di hello.</span><span class="sxs-lookup"><span data-stu-id="7e1cb-174">For Windows Server 2012 R2, hello WSFC cluster share disk currently in use is hello SIOS DataKeeper software solution.</span></span>

<span data-ttu-id="7e1cb-175">Hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="7e1cb-175">Do hello following:</span></span>
1. <span data-ttu-id="7e1cb-176">Aggiungere un altro disco o i dischi di hello stessa dimensione (che è necessario toostripe) tooeach di hello nodi del cluster e formattare il testo.</span><span class="sxs-lookup"><span data-stu-id="7e1cb-176">Add an additional disk or disks of hello same size (which you need toostripe) tooeach of hello cluster nodes, and format them.</span></span>
2. <span data-ttu-id="7e1cb-177">Configurare la replica di archiviazione con SIOS DataKeeper.</span><span class="sxs-lookup"><span data-stu-id="7e1cb-177">Configure storage replication with SIOS DataKeeper.</span></span>

<span data-ttu-id="7e1cb-178">Questa procedura si presuppone che SIOS DataKeeper già stato installato nel computer del cluster WSFC hello.</span><span class="sxs-lookup"><span data-stu-id="7e1cb-178">This procedure assumes that you have already installed SIOS DataKeeper on hello WSFC cluster machines.</span></span> <span data-ttu-id="7e1cb-179">Se è stato installato, è ora necessario configurare la replica tra computer hello.</span><span class="sxs-lookup"><span data-stu-id="7e1cb-179">If you have installed it, you must now configure replication between hello machines.</span></span> <span data-ttu-id="7e1cb-180">il processo di Hello è descritto dettagliatamente in hello principale [Guida per la disponibilità elevata di SAP NetWeaver in macchine virtuali Windows][sap-ha-guide-8.12.3.3].</span><span class="sxs-lookup"><span data-stu-id="7e1cb-180">hello process is described in detail in hello main [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-8.12.3.3].</span></span>  

![Il mirroring per il nuovo disco di condivisione di SAP ASCS/SCS di hello sincrono DataKeeper][sap-ha-guide-figure-6006]

### <a name="deploy-vms-for-sap-application-servers-and-dbms-cluster"></a><span data-ttu-id="7e1cb-182">Distribuire le VM per i server applicazioni SAP e il cluster DBMS</span><span class="sxs-lookup"><span data-stu-id="7e1cb-182">Deploy VMs for SAP application servers and DBMS cluster</span></span>

<span data-ttu-id="7e1cb-183">Preparazione dell'infrastruttura di hello toocomplete per secondo sistema SAP di hello, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="7e1cb-183">toocomplete hello infrastructure preparation for hello second SAP system, do hello following:</span></span>

1. <span data-ttu-id="7e1cb-184">Distribuire VM dedicate per i server applicazioni SAP e inserirle nel proprio gruppo di disponibilità dedicato.</span><span class="sxs-lookup"><span data-stu-id="7e1cb-184">Deploy dedicated VMs for SAP application servers and put them in their own dedicated availability group.</span></span>
2. <span data-ttu-id="7e1cb-185">Distribuire VM dedicate per il cluster DBMS e inserirle nel proprio gruppo di disponibilità dedicato.</span><span class="sxs-lookup"><span data-stu-id="7e1cb-185">Deploy dedicated VMs for DBMS cluster and put them in their own dedicated availability group.</span></span>


## <a name="install-hello-second-sap-sid2-netweaver-system"></a><span data-ttu-id="7e1cb-186">Installare il sistema SAP NetWeaver SID2 secondo di hello</span><span class="sxs-lookup"><span data-stu-id="7e1cb-186">Install hello second SAP SID2 NetWeaver system</span></span>

<span data-ttu-id="7e1cb-187">processo completo di Hello di installazione di un sistema SAP SID2 secondo è descritto in hello principale [Guida per la disponibilità elevata di SAP NetWeaver in macchine virtuali Windows][sap-ha-guide-9].</span><span class="sxs-lookup"><span data-stu-id="7e1cb-187">hello complete process of installing a second SAP SID2 system is described in hello main [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-9].</span></span>

<span data-ttu-id="7e1cb-188">procedura Hello è come segue:</span><span class="sxs-lookup"><span data-stu-id="7e1cb-188">hello high-level procedure is as follows:</span></span>

1. <span data-ttu-id="7e1cb-189">[Installare hello SAP primo nodo del cluster][sap-ha-guide-9.1.2].</span><span class="sxs-lookup"><span data-stu-id="7e1cb-189">[Install hello SAP first cluster node][sap-ha-guide-9.1.2].</span></span>  
 <span data-ttu-id="7e1cb-190">In questo passaggio si installa SAP con un'istanza ASCS/SCS a disponibilità elevata in hello **nodo del cluster WSFC esistente 1**.</span><span class="sxs-lookup"><span data-stu-id="7e1cb-190">In this step, you are installing SAP with a high-availability ASCS/SCS instance on hello **EXISTING WSFC cluster node 1**.</span></span>

2. <span data-ttu-id="7e1cb-191">[Modificare il profilo di SAP hello dell'istanza ASCS/SCS hello][sap-ha-guide-9.1.3].</span><span class="sxs-lookup"><span data-stu-id="7e1cb-191">[Modify hello SAP profile of hello ASCS/SCS instance][sap-ha-guide-9.1.3].</span></span>

3. <span data-ttu-id="7e1cb-192">[Configurare una porta probe][sap-ha-guide-9.1.4].</span><span class="sxs-lookup"><span data-stu-id="7e1cb-192">[Configure a probe port][sap-ha-guide-9.1.4].</span></span>  
 <span data-ttu-id="7e1cb-193">In questo passaggio si sta configurando una porta probe SAP-SID2-IP della risorsa nel cluster SAP tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7e1cb-193">In this step, you are configuring an SAP cluster resource SAP-SID2-IP probe port by using PowerShell.</span></span> <span data-ttu-id="7e1cb-194">Eseguire questa configurazione su uno dei nodi del cluster di SAP ASCS/SCS hello.</span><span class="sxs-lookup"><span data-stu-id="7e1cb-194">Execute this configuration on one of hello SAP ASCS/SCS cluster nodes.</span></span>

4. <span data-ttu-id="7e1cb-195">[Installare l'istanza del database hello] [sap a disponibilità elevata-Guida-9.2].</span><span class="sxs-lookup"><span data-stu-id="7e1cb-195">[Install hello database instance][sap-ha-guide-9.2].</span></span>  
 <span data-ttu-id="7e1cb-196">In questo passaggio si sta installando DBMS in un cluster WSFC dedicato.</span><span class="sxs-lookup"><span data-stu-id="7e1cb-196">In this step, you are installing DBMS on a dedicated WSFC cluster.</span></span>

5. <span data-ttu-id="7e1cb-197">[Installare secondo nodo del cluster hello] [sap a disponibilità elevata-Guida-9.3].</span><span class="sxs-lookup"><span data-stu-id="7e1cb-197">[Install hello second cluster node][sap-ha-guide-9.3].</span></span>  
 <span data-ttu-id="7e1cb-198">In questo passaggio, si sta installando SAP con un'istanza ASCS/SCS a disponibilità elevata nel nodo del cluster esistente WSFC hello 2.</span><span class="sxs-lookup"><span data-stu-id="7e1cb-198">In this step, you are installing SAP with a high-availability ASCS/SCS instance on hello existing WSFC cluster node 2.</span></span>

6. <span data-ttu-id="7e1cb-199">Aprire le porte del Firewall di Windows per l'istanza di SAP ASCS/SCS hello e ProbePort.</span><span class="sxs-lookup"><span data-stu-id="7e1cb-199">Open Windows Firewall ports for hello SAP ASCS/SCS instance and ProbePort.</span></span>  
 <span data-ttu-id="7e1cb-200">In entrambi i nodi del cluster usati per le istanze di SAP ASCS/SCS si stanno aprendo tutte le porte di Windows Firewall usate da SAP ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="7e1cb-200">On both cluster nodes that are used for SAP ASCS/SCS instances, you are opening all Windows Firewall ports that are used by SAP ASCS/SCS.</span></span> <span data-ttu-id="7e1cb-201">Queste porte sono elencate in hello [Guida per la disponibilità elevata di SAP NetWeaver in macchine virtuali Windows][sap-ha-guide-8.8].</span><span class="sxs-lookup"><span data-stu-id="7e1cb-201">These ports are listed in hello [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-8.8].</span></span>  
 <span data-ttu-id="7e1cb-202">Inoltre aprire hello Azure carico interno del servizio di bilanciamento porta probe, ovvero 62350 in questo scenario.</span><span class="sxs-lookup"><span data-stu-id="7e1cb-202">Also open hello Azure internal load balancer probe port, which is 62350 in our scenario.</span></span>

7. <span data-ttu-id="7e1cb-203">[Modificare il tipo di avvio dell'istanza di servizio SAP Hiamanti Windows hello hello][sap-ha-guide-9.4].</span><span class="sxs-lookup"><span data-stu-id="7e1cb-203">[Change hello start type of hello SAP ERS Windows service instance][sap-ha-guide-9.4].</span></span>

8. <span data-ttu-id="7e1cb-204">[Installare server primario applicazioni SAP hello] [ sap-ha-guide-9.5] sul nuovo hello dedicato macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="7e1cb-204">[Install hello SAP primary application server][sap-ha-guide-9.5] on hello new dedicated VM.</span></span>

9. <span data-ttu-id="7e1cb-205">[Installare server aggiuntivi di applicazioni SAP hello] [ sap-ha-guide-9.6] sul nuovo hello dedicato macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="7e1cb-205">[Install hello SAP additional application server][sap-ha-guide-9.6] on hello new dedicated VM.</span></span>

10. <span data-ttu-id="7e1cb-206">[Test di failover di istanza di SAP ASCS/SCS hello e la replica di SIOS][sap-ha-guide-10].</span><span class="sxs-lookup"><span data-stu-id="7e1cb-206">[Test hello SAP ASCS/SCS instance failover and SIOS replication][sap-ha-guide-10].</span></span>

## <a name="next-steps"></a><span data-ttu-id="7e1cb-207">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7e1cb-207">Next steps</span></span>

- <span data-ttu-id="7e1cb-208">[Limiti relativi alle reti: Azure Resource Manager][networking-limits-azure-resource-manager]</span><span class="sxs-lookup"><span data-stu-id="7e1cb-208">[Networking limits: Azure Resource Manager][networking-limits-azure-resource-manager]</span></span>
- <span data-ttu-id="7e1cb-209">[Più indirizzi VIP per Azure Load Balancer][load-balancer-multivip-overview]</span><span class="sxs-lookup"><span data-stu-id="7e1cb-209">[Multiple VIPs for Azure Load Balancer][load-balancer-multivip-overview]</span></span>
- <span data-ttu-id="7e1cb-210">[SAP NetWeaver in macchine virtuali Windows: guida alle funzionalità di disponibilità elevata][sap-ha-guide]</span><span class="sxs-lookup"><span data-stu-id="7e1cb-210">[Guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide]</span></span>
