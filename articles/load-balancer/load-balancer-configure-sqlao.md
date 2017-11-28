---
title: bilanciamento del carico aaaConfigure per SQL AlwaysOn | Documenti Microsoft
description: Configurare toowork bilanciamento di carico con SQL sempre e come tooleverage powershell toocreate bilanciamento del carico per implementazione SQL hello
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: d7bc3790-47d3-4e95-887c-c533011e4afd
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: ac6200b18f725dadee2555b80055327d379417d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-load-balancer-for-sql-always-on"></a><span data-ttu-id="c2e02-103">Configurare il bilanciamento del carico per SQL AlwaysOn</span><span class="sxs-lookup"><span data-stu-id="c2e02-103">Configure load balancer for SQL always on</span></span>

<span data-ttu-id="c2e02-104">I gruppi di disponibilità AlwaysOn di SQL Server ora possono essere eseguiti con ILB.</span><span class="sxs-lookup"><span data-stu-id="c2e02-104">SQL Server AlwaysOn Availability Groups can now be run with ILB.</span></span> <span data-ttu-id="c2e02-105">Un gruppo di disponibilità è la soluzione principale di SQL Server per il ripristino di emergenza e la disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="c2e02-105">Availability Group is SQL Server's flagship solution for high availability and disaster recovery.</span></span> <span data-ttu-id="c2e02-106">Hello listener del gruppo di disponibilità consente alle applicazioni client tooseamlessly connettersi toohello la replica primaria, indipendentemente dal numero di hello di repliche hello nella configurazione di hello.</span><span class="sxs-lookup"><span data-stu-id="c2e02-106">hello Availability Group Listener allows client applications tooseamlessly connect toohello primary replica, irrespective of hello number of hello replicas in hello configuration.</span></span>

<span data-ttu-id="c2e02-107">nome del listener (DNS) di Hello è l'indirizzo IP mappato tooa con bilanciata del carico e bilanciamento del carico di Azure indirizza il server primario di hello in arrivo traffico tooonly hello nel set di repliche hello.</span><span class="sxs-lookup"><span data-stu-id="c2e02-107">hello listener (DNS) name is mapped tooa load-balanced IP address and Azure's load balancer directs hello incoming traffic tooonly hello primary server in hello replica set.</span></span>

<span data-ttu-id="c2e02-108">È possibile usare il supporto ILB per gli endpoint di SQL Server AlwaysOn (listener).</span><span class="sxs-lookup"><span data-stu-id="c2e02-108">You can use ILB support for SQL Server AlwaysOn (listener) endpoints.</span></span> <span data-ttu-id="c2e02-109">È ora possibile controllare accessibilità hello del listener hello e scegliere l'indirizzo IP con bilanciamento del carico hello da una subnet specifica nella rete virtuale (VNet).</span><span class="sxs-lookup"><span data-stu-id="c2e02-109">You now have control over hello accessibility of hello listener and can choose hello load-balanced IP address from a specific subnet in your Virtual Network (VNet).</span></span>

<span data-ttu-id="c2e02-110">Con bilanciamento del carico interno listener hello, hello endpoint SQL server (ad esempio Server = tcp:ListenerName, 1433; Database = DatabaseName) è accessibile solo da:</span><span class="sxs-lookup"><span data-stu-id="c2e02-110">By using ILB on hello listener, hello SQL server endpoint (e.g. Server=tcp:ListenerName,1433;Database=DatabaseName) is accessible only by:</span></span>

* <span data-ttu-id="c2e02-111">Servizi e macchine virtuali nella stessa rete virtuale di hello</span><span class="sxs-lookup"><span data-stu-id="c2e02-111">Services and VMs in hello same Virtual network</span></span>
* <span data-ttu-id="c2e02-112">Servizi e VM dalla rete locale connessa</span><span class="sxs-lookup"><span data-stu-id="c2e02-112">Services and VMs from connected on-premises network</span></span>
* <span data-ttu-id="c2e02-113">Servizi e VM da reti virtuali interconnesse</span><span class="sxs-lookup"><span data-stu-id="c2e02-113">Services and VMs from interconnected VNets</span></span>

![ILB_SQLAO_NewPic](./media/load-balancer-configure-sqlao/sqlao1.png)

<span data-ttu-id="c2e02-115">Figura 1 - SQL AlwaysOn configurato con bilanciamento del carico con connessione Internet</span><span class="sxs-lookup"><span data-stu-id="c2e02-115">Figure 1 - SQL AlwaysOn configured with Internet-facing load balancer</span></span>

## <a name="add-internal-load-balancer-toohello-service"></a><span data-ttu-id="c2e02-116">Aggiungere il servizio di bilanciamento del carico interno toohello</span><span class="sxs-lookup"><span data-stu-id="c2e02-116">Add Internal Load Balancer toohello service</span></span>

1. <span data-ttu-id="c2e02-117">Nel seguente esempio di hello, è possibile configurare una rete virtuale che contiene una subnet denominata "Subnet-1":</span><span class="sxs-lookup"><span data-stu-id="c2e02-117">In hello following example, we will configure a Virtual network that contains a subnet  called 'Subnet-1':</span></span>

    ```powershell
    Add-AzureInternalLoadBalancer -InternalLoadBalancerName ILB_SQL_AO -SubnetName Subnet-1 -ServiceName SqlSvc
    ```
2. <span data-ttu-id="c2e02-118">Aggiungere gli endpoint con carico bilanciato per ILB in ogni macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="c2e02-118">Add load balanced endpoints for ILB on each VM</span></span>

    ```powershell
    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc1 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -
    DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM

    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc2 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM
    ```

    <span data-ttu-id="c2e02-119">Nell'esempio hello sopra, si dispone di 2 VM chiamato "sqlsvc1" e "sqlsvc2" esecuzione del servizio nel cloud hello "Sqlsvc".</span><span class="sxs-lookup"><span data-stu-id="c2e02-119">In hello example above, you have 2 VM's called "sqlsvc1" and "sqlsvc2" running in hello cloud service "Sqlsvc".</span></span> <span data-ttu-id="c2e02-120">Dopo la creazione di hello ILB con `DirectServerReturn` passa, si aggiungono carico bilanciato endpoint toohello ILB tooallow SQL tooconfigure hello listener per gruppi di disponibilità hello.</span><span class="sxs-lookup"><span data-stu-id="c2e02-120">After creating hello ILB with `DirectServerReturn` switch, you add load balanced endpoints toohello ILB tooallow SQL tooconfigure hello listeners for hello availability groups.</span></span>

<span data-ttu-id="c2e02-121">Per altre informazioni su SQL AlwaysOn, vedere [Configurare un servizio di bilanciamento del carico interno per un gruppo di disponibilità AlwaysOn in Azure](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span><span class="sxs-lookup"><span data-stu-id="c2e02-121">For more information about SQL AlwaysOn, see [Configure an internal load balancer for an AlwaysOn availability group in Azure](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="c2e02-122">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c2e02-122">See Also</span></span>
[<span data-ttu-id="c2e02-123">Introduzione alla configurazione del bilanciamento del carico Internet</span><span class="sxs-lookup"><span data-stu-id="c2e02-123">Get started configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="c2e02-124">Introduzione alla configurazione del bilanciamento del carico interno</span><span class="sxs-lookup"><span data-stu-id="c2e02-124">Get started configuring an Internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="c2e02-125">Configurare una modalità di distribuzione del bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="c2e02-125">Configure a Load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="c2e02-126">Configurare le impostazioni del timeout di inattività TCP per il bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="c2e02-126">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
