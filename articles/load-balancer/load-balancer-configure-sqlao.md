---
title: Configurare il bilanciamento del carico per SQL AlwaysOn | Documentazione Microsoft
description: Configurare il bilanciamento del carico per usare sempre SQL AlwaysOn e sfruttare PowerShell per creare il bilanciamento del carico per l'implementazione SQL
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
ms.openlocfilehash: 68aad6253f185d53fdd7f11c8660c7287ef12655
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="configure-load-balancer-for-sql-always-on"></a><span data-ttu-id="d5ba4-103">Configurare il bilanciamento del carico per SQL AlwaysOn</span><span class="sxs-lookup"><span data-stu-id="d5ba4-103">Configure load balancer for SQL always on</span></span>

<span data-ttu-id="d5ba4-104">I gruppi di disponibilità AlwaysOn di SQL Server ora possono essere eseguiti con ILB.</span><span class="sxs-lookup"><span data-stu-id="d5ba4-104">SQL Server AlwaysOn Availability Groups can now be run with ILB.</span></span> <span data-ttu-id="d5ba4-105">Un gruppo di disponibilità è la soluzione principale di SQL Server per il ripristino di emergenza e la disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="d5ba4-105">Availability Group is SQL Server's flagship solution for high availability and disaster recovery.</span></span> <span data-ttu-id="d5ba4-106">Il listener del gruppo di disponibilità consente alle applicazioni client di connettersi facilmente alla replica primaria, indipendentemente dal numero di repliche nella configurazione.</span><span class="sxs-lookup"><span data-stu-id="d5ba4-106">The Availability Group Listener allows client applications to seamlessly connect to the primary replica, irrespective of the number of the replicas in the configuration.</span></span>

<span data-ttu-id="d5ba4-107">Il nome del listener (DNS) viene associato a un indirizzo IP con carico bilanciato e il bilanciamento del carico di Azure indirizza il traffico in ingresso solo al server primario nel set di repliche.</span><span class="sxs-lookup"><span data-stu-id="d5ba4-107">The listener (DNS) name is mapped to a load-balanced IP address and Azure's load balancer directs the incoming traffic to only the primary server in the replica set.</span></span>

<span data-ttu-id="d5ba4-108">È possibile usare il supporto ILB per gli endpoint di SQL Server AlwaysOn (listener).</span><span class="sxs-lookup"><span data-stu-id="d5ba4-108">You can use ILB support for SQL Server AlwaysOn (listener) endpoints.</span></span> <span data-ttu-id="d5ba4-109">Ora si ha il controllo dell'accessibilità del listener e si può scegliere l'indirizzo IP con carico bilanciato da una subnet specifica nella rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="d5ba4-109">You now have control over the accessibility of the listener and can choose the load-balanced IP address from a specific subnet in your Virtual Network (VNet).</span></span>

<span data-ttu-id="d5ba4-110">Usando ILB sul listener, l'endpoint SQL Server (ad esempio, Server=tcp:ListenerName,1433;Database=DatabaseName) è accessibile solo per:</span><span class="sxs-lookup"><span data-stu-id="d5ba4-110">By using ILB on the listener, the SQL server endpoint (e.g. Server=tcp:ListenerName,1433;Database=DatabaseName) is accessible only by:</span></span>

* <span data-ttu-id="d5ba4-111">Servizi e VM nella stessa rete virtuale</span><span class="sxs-lookup"><span data-stu-id="d5ba4-111">Services and VMs in the same Virtual network</span></span>
* <span data-ttu-id="d5ba4-112">Servizi e VM dalla rete locale connessa</span><span class="sxs-lookup"><span data-stu-id="d5ba4-112">Services and VMs from connected on-premises network</span></span>
* <span data-ttu-id="d5ba4-113">Servizi e VM da reti virtuali interconnesse</span><span class="sxs-lookup"><span data-stu-id="d5ba4-113">Services and VMs from interconnected VNets</span></span>

![ILB_SQLAO_NewPic](./media/load-balancer-configure-sqlao/sqlao1.png)

<span data-ttu-id="d5ba4-115">Figura 1 - SQL AlwaysOn configurato con bilanciamento del carico con connessione Internet</span><span class="sxs-lookup"><span data-stu-id="d5ba4-115">Figure 1 - SQL AlwaysOn configured with Internet-facing load balancer</span></span>

## <a name="add-internal-load-balancer-to-the-service"></a><span data-ttu-id="d5ba4-116">Aggiungere al servizio il bilanciamento del carico interno</span><span class="sxs-lookup"><span data-stu-id="d5ba4-116">Add Internal Load Balancer to the service</span></span>

1. <span data-ttu-id="d5ba4-117">Nell'esempio seguente verrà configurata una rete virtuale che contiene una subnet denominata "Subnet-1":</span><span class="sxs-lookup"><span data-stu-id="d5ba4-117">In the following example, we will configure a Virtual network that contains a subnet  called 'Subnet-1':</span></span>

    ```powershell
    Add-AzureInternalLoadBalancer -InternalLoadBalancerName ILB_SQL_AO -SubnetName Subnet-1 -ServiceName SqlSvc
    ```
2. <span data-ttu-id="d5ba4-118">Aggiungere gli endpoint con carico bilanciato per ILB in ogni macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="d5ba4-118">Add load balanced endpoints for ILB on each VM</span></span>

    ```powershell
    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc1 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -
    DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM

    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc2 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM
    ```

    <span data-ttu-id="d5ba4-119">Nell'esempio precedente, si dispone di 2 macchine virtuali denominate "sqlsvc1" e "sqlsvc2" in esecuzione nel servizio cloud "Sqlsvc".</span><span class="sxs-lookup"><span data-stu-id="d5ba4-119">In the example above, you have 2 VM's called "sqlsvc1" and "sqlsvc2" running in the cloud service "Sqlsvc".</span></span> <span data-ttu-id="d5ba4-120">Dopo la creazione di ILB con l'opzione `DirectServerReturn` vengono aggiunti gli endpoint con carico bilanciato all’ILB per consentire a SQL di configurare i listener per i gruppi di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="d5ba4-120">After creating the ILB with `DirectServerReturn` switch, you add load balanced endpoints to the ILB to allow SQL to configure the listeners for the availability groups.</span></span>

<span data-ttu-id="d5ba4-121">Per altre informazioni su SQL AlwaysOn, vedere [Configurare un servizio di bilanciamento del carico interno per un gruppo di disponibilità AlwaysOn in Azure](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span><span class="sxs-lookup"><span data-stu-id="d5ba4-121">For more information about SQL AlwaysOn, see [Configure an internal load balancer for an AlwaysOn availability group in Azure](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="d5ba4-122">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="d5ba4-122">See Also</span></span>
[<span data-ttu-id="d5ba4-123">Introduzione alla configurazione del bilanciamento del carico Internet</span><span class="sxs-lookup"><span data-stu-id="d5ba4-123">Get started configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="d5ba4-124">Introduzione alla configurazione del bilanciamento del carico interno</span><span class="sxs-lookup"><span data-stu-id="d5ba4-124">Get started configuring an Internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="d5ba4-125">Configurare una modalità di distribuzione del bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="d5ba4-125">Configure a Load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="d5ba4-126">Configurare le impostazioni del timeout di inattività TCP per il bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="d5ba4-126">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
