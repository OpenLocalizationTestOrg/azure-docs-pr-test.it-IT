---
title: "Gruppi di disponibilità di SQL Server: Macchine virtuali di Azure: ripristino di emergenza | Documentazione Microsoft"
description: "Questo articolo illustra come configurare un gruppo di disponibilità SQL Server nelle macchine virtuali di Azure con una replica in un'area diversa."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 388c464e-a16e-4c9d-a0d5-bb7cf5974689
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/02/2017
ms.author: mikeray
ms.openlocfilehash: 1ce90cf4bae66bfd6387a2698fd9b1ba7fc64595
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="configure-an-always-on-availability-group-on-azure-virtual-machines-in-different-regions"></a><span data-ttu-id="37132-103">Configurare un gruppo di disponibilità AlwaysOn in macchine virtuali di Azure in aree diverse</span><span class="sxs-lookup"><span data-stu-id="37132-103">Configure an Always On availability group on Azure virtual machines in different regions</span></span>

<span data-ttu-id="37132-104">Questo articolo descrive come configurare la replica di un gruppo di disponibilità SQL Server AlwaysOn in macchine virtuali di Azure in una località di Azure remota.</span><span class="sxs-lookup"><span data-stu-id="37132-104">This article explains how to configure a SQL Server Always On availability group replica on Azure virtual machines in a remote Azure location.</span></span> <span data-ttu-id="37132-105">Usare questa configurazione per supportare il ripristino di emergenza.</span><span class="sxs-lookup"><span data-stu-id="37132-105">Use this configuration to support disaster recovery.</span></span>

<span data-ttu-id="37132-106">Questo articolo si applica a Macchine virtuali di Azure in modalità Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="37132-106">This article applies to Azure Virtual Machines in Resource Manager mode.</span></span>

<span data-ttu-id="37132-107">L'immagine seguente illustra una distribuzione comune di un gruppo di disponibilità nelle macchine virtuali di Azure:</span><span class="sxs-lookup"><span data-stu-id="37132-107">The following image shows a common deployment of an availability group on Azure virtual machines:</span></span>

   ![Gruppo di disponibilità](./media/virtual-machines-windows-portal-sql-availability-group-dr/00-availability-group-basic.png)

<span data-ttu-id="37132-109">In questa distribuzione tutte le macchine virtuali sono in un'unica area di Azure.</span><span class="sxs-lookup"><span data-stu-id="37132-109">In this deployment, all virtual machines are in one Azure region.</span></span> <span data-ttu-id="37132-110">Le repliche del gruppo di disponibilità possono avere il commit sincrono con failover automatico in SQL-1 e SQL-2.</span><span class="sxs-lookup"><span data-stu-id="37132-110">The availability group replicas can have synchronous commit with automatic failover on SQL-1 and SQL-2.</span></span> <span data-ttu-id="37132-111">Per creare questa architettura, vedere [Availability Group template or tutorial](virtual-machines-windows-portal-sql-availability-group-overview.md) (Modello o esercitazione per i gruppi di disponibilità).</span><span class="sxs-lookup"><span data-stu-id="37132-111">To build this architecture, see [Availability Group template or tutorial](virtual-machines-windows-portal-sql-availability-group-overview.md).</span></span>

<span data-ttu-id="37132-112">Questa architettura è soggetta a tempi di inattività se l'area di Azure diventa inaccessibile.</span><span class="sxs-lookup"><span data-stu-id="37132-112">This architecture is vulnerable to downtime if the Azure region becomes inaccessible.</span></span> <span data-ttu-id="37132-113">Per ovviare a questa vulnerabilità, aggiungere una replica in un'area di Azure diversa.</span><span class="sxs-lookup"><span data-stu-id="37132-113">To overcome this vulnerability, add a replica in a different Azure region.</span></span> <span data-ttu-id="37132-114">Il diagramma seguente illustra l'aspetto della nuova architettura:</span><span class="sxs-lookup"><span data-stu-id="37132-114">The following diagram shows how the new architecture would look:</span></span>

   ![Ripristino di emergenza del gruppo di disponibilità](./media/virtual-machines-windows-portal-sql-availability-group-dr/00-availability-group-basic-dr.png)

<span data-ttu-id="37132-116">Il diagramma precedente illustra una nuova macchina virtuale denominata SQL-3.</span><span class="sxs-lookup"><span data-stu-id="37132-116">The preceding diagram shows a new virtual machine called SQL-3.</span></span> <span data-ttu-id="37132-117">SQL-3 è in un'area di Azure diversa.</span><span class="sxs-lookup"><span data-stu-id="37132-117">SQL-3 is in a different Azure region.</span></span> <span data-ttu-id="37132-118">SQL-3 viene aggiunta al cluster di failover di Windows Server.</span><span class="sxs-lookup"><span data-stu-id="37132-118">SQL-3 is added to the Windows Server Failover Cluster.</span></span> <span data-ttu-id="37132-119">SQL-3 può ospitare una replica del gruppo di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="37132-119">SQL-3 can host an availability group replica.</span></span> <span data-ttu-id="37132-120">Si noti infine che l'area di Azure per SQL-3 ha un nuovo servizio di bilanciamento del carico di Azure.</span><span class="sxs-lookup"><span data-stu-id="37132-120">Finally, notice that the Azure region for SQL-3 has a new Azure load balancer.</span></span>

>[!NOTE]
> <span data-ttu-id="37132-121">Un set di disponibilità di Azure è necessario quando più macchine virtuali sono nella stessa area.</span><span class="sxs-lookup"><span data-stu-id="37132-121">An Azure availability set is required when more than one virtual machine is in the same region.</span></span> <span data-ttu-id="37132-122">Se una sola macchina virtuale è nell'area, il set di disponibilità non è necessario.</span><span class="sxs-lookup"><span data-stu-id="37132-122">If only one virtual machine is in the region, then the availability set is not required.</span></span> <span data-ttu-id="37132-123">È possibile inserire una macchina virtuale in un set di disponibilità solo al momento della creazione.</span><span class="sxs-lookup"><span data-stu-id="37132-123">You can only place a virtual machine in an availability set at creation time.</span></span> <span data-ttu-id="37132-124">Se la macchina virtuale è già in un set di disponibilità, è possibile aggiungere una macchina virtuale per un'altra replica in seguito.</span><span class="sxs-lookup"><span data-stu-id="37132-124">If the virtual machine is already in an availability set, you can add a virtual machine for an additional replica later.</span></span>

<span data-ttu-id="37132-125">In questa architettura la replica nell'area remota viene in genere configurata con la modalità di disponibilità commit asincrono e la modalità di failover manuale.</span><span class="sxs-lookup"><span data-stu-id="37132-125">In this architecture, the replica in the remote region is normally configured with asynchronous commit availability mode and manual failover mode.</span></span>

<span data-ttu-id="37132-126">Quando le repliche del gruppo di disponibilità sono nelle macchine virtuali di Azure in aree di Azure diverse, ogni area richiede:</span><span class="sxs-lookup"><span data-stu-id="37132-126">When availability group replicas are on Azure virtual machines in different Azure regions, each region requires:</span></span>

* <span data-ttu-id="37132-127">Un gateway di rete virtuale</span><span class="sxs-lookup"><span data-stu-id="37132-127">A virtual network gateway</span></span>
* <span data-ttu-id="37132-128">Una connessione gateway di rete virtuale</span><span class="sxs-lookup"><span data-stu-id="37132-128">A virtual network gateway connection</span></span>

<span data-ttu-id="37132-129">Il diagramma seguente illustra come le reti comunicano tra data center.</span><span class="sxs-lookup"><span data-stu-id="37132-129">The following diagram shows how the networks communicate between data centers.</span></span>

   ![Gruppo di disponibilità](./media/virtual-machines-windows-portal-sql-availability-group-dr/01-vpngateway-example.png)

>[!IMPORTANT]
><span data-ttu-id="37132-131">Questa architettura è soggetta a costi per i dati in uscita replicati tra le aree di Azure.</span><span class="sxs-lookup"><span data-stu-id="37132-131">This architecture incurs outbound data charges for data replicated between Azure regions.</span></span> <span data-ttu-id="37132-132">Vedere [Prezzi per la larghezza di banda](http://azure.microsoft.com/pricing/details/bandwidth/).</span><span class="sxs-lookup"><span data-stu-id="37132-132">See [Bandwidth Pricing](http://azure.microsoft.com/pricing/details/bandwidth/).</span></span>  

## <a name="create-remote-replica"></a><span data-ttu-id="37132-133">Creare una replica remota</span><span class="sxs-lookup"><span data-stu-id="37132-133">Create remote replica</span></span>

<span data-ttu-id="37132-134">Per creare una replica in un data center remoto, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="37132-134">To create a replica in a remote data center, do the following steps:</span></span>

1. <span data-ttu-id="37132-135">[Creare una rete virtuale nella nuova area](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="37132-135">[Create a virtual network in the new region](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>

1. <span data-ttu-id="37132-136">[Configurare una connessione da rete virtuale a rete virtuale con il portale di Azure](../../../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md).</span><span class="sxs-lookup"><span data-stu-id="37132-136">[Configure a VNet-to-VNet connection using the Azure portal](../../../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md).</span></span>

   >[!NOTE]
   ><span data-ttu-id="37132-137">In alcuni casi, potrebbe essere necessario usare PowerShell per creare la connessione da rete virtuale a rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="37132-137">In some cases, you may have to use PowerShell to create the VNet-to-VNet connection.</span></span> <span data-ttu-id="37132-138">Se, ad esempio, si usano account Azure diversi, non è possibile configurare la connessione nel portale.</span><span class="sxs-lookup"><span data-stu-id="37132-138">For example, if you use different Azure accounts you cannot configure the connection in the portal.</span></span> <span data-ttu-id="37132-139">In questi casi, vedere [Configurare una connessione da rete virtuale a rete virtuale con il portale di Azure](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="37132-139">In this case see, [Configure a VNet-to-VNet connection using the Azure portal](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span></span>

1. <span data-ttu-id="37132-140">[Creare un controller di dominio nella nuova area](../../../active-directory/active-directory-new-forest-virtual-machine.md).</span><span class="sxs-lookup"><span data-stu-id="37132-140">[Create a domain controller in the new region](../../../active-directory/active-directory-new-forest-virtual-machine.md).</span></span>

   <span data-ttu-id="37132-141">Questo controller di dominio fornisce l'autenticazione se il controller di dominio nel sito primario non è disponibile.</span><span class="sxs-lookup"><span data-stu-id="37132-141">This domain controller provides authentication if the domain controller in the primary site is not available.</span></span>

1. <span data-ttu-id="37132-142">[Creare una macchina virtuale SQL Server nella nuova area](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="37132-142">[Create a SQL Server virtual machine in the new region](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

1. <span data-ttu-id="37132-143">[Creare un servizio di bilanciamento del carico di Azure in rete nella nuova area](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span><span class="sxs-lookup"><span data-stu-id="37132-143">[Create an Azure load balancer in the network on the new region](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span></span>

   <span data-ttu-id="37132-144">Questo servizio di bilanciamento del carico deve:</span><span class="sxs-lookup"><span data-stu-id="37132-144">This load balancer must:</span></span>

   - <span data-ttu-id="37132-145">Essere nella stessa rete e subnet della nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="37132-145">Be in the same network and subnet as the new virtual machine.</span></span>
   - <span data-ttu-id="37132-146">Avere un indirizzo IP statico per il listener del gruppo di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="37132-146">Have a static IP address for the availability group listener.</span></span>
   - <span data-ttu-id="37132-147">Includere un pool back-end costituito solo dalle macchine virtuali nella stessa area del servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="37132-147">Include a backend pool consisting of only the virtual machines in the same region as the load balancer.</span></span>
   - <span data-ttu-id="37132-148">Usare il probe di una porta TCP specifico dell'indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="37132-148">Use a TCP port probe specific to the IP address.</span></span>
   - <span data-ttu-id="37132-149">Avere una regola di bilanciamento del carico specifica dell'istanza di SQL Server nella stessa area.</span><span class="sxs-lookup"><span data-stu-id="37132-149">Have a load balancing rule specific to the SQL Server in the same region.</span></span>  

1. <span data-ttu-id="37132-150">[Aggiungere la funzionalità di clustering di failover alla nuova istanza di SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span><span class="sxs-lookup"><span data-stu-id="37132-150">[Add Failover Clustering feature to the new SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span></span>

1. <span data-ttu-id="37132-151">[Aggiungere la nuova istanza di SQL Server al dominio](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span><span class="sxs-lookup"><span data-stu-id="37132-151">[Join the new SQL Server to the domain](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span></span>

1. <span data-ttu-id="37132-152">[Impostare il nuovo account del servizio SQL Server per l'uso di un account di dominio](virtual-machines-windows-portal-sql-availability-group-prereq.md#setServiceAccount).</span><span class="sxs-lookup"><span data-stu-id="37132-152">[Set the new SQL Server service account to use a domain account](virtual-machines-windows-portal-sql-availability-group-prereq.md#setServiceAccount).</span></span>

1. <span data-ttu-id="37132-153">[Aggiungere la nuova istanza di SQL Server al cluster di failover di Windows Server](virtual-machines-windows-portal-sql-availability-group-tutorial.md#addNode).</span><span class="sxs-lookup"><span data-stu-id="37132-153">[Add the new SQL Server to the Windows Server Failover Cluster](virtual-machines-windows-portal-sql-availability-group-tutorial.md#addNode).</span></span>

1. <span data-ttu-id="37132-154">Creare una risorsa indirizzo IP nel cluster.</span><span class="sxs-lookup"><span data-stu-id="37132-154">Create an IP address resource on the cluster.</span></span>

   <span data-ttu-id="37132-155">È possibile creare la risorsa indirizzo IP in Gestione cluster di failover.</span><span class="sxs-lookup"><span data-stu-id="37132-155">You can create the IP address resource in Failover Cluster Manager.</span></span> <span data-ttu-id="37132-156">Fare clic con il pulsante destro del mouse sul ruolo del gruppo di disponibilità, scegliere **Aggiungi risorsa**, **Altre risorse** e fare clic su **Indirizzo IP**.</span><span class="sxs-lookup"><span data-stu-id="37132-156">Right-click the availability group role, click **Add Resource**, **More Resources**, and click **IP Address**.</span></span>

   ![Creare un indirizzo IP](./media/virtual-machines-windows-portal-sql-availability-group-dr/20-add-ip-resource.png)

   <span data-ttu-id="37132-158">Configurare l'indirizzo IP come segue:</span><span class="sxs-lookup"><span data-stu-id="37132-158">Configure this IP address as follows:</span></span>

   - <span data-ttu-id="37132-159">Usare la rete dal data center remoto.</span><span class="sxs-lookup"><span data-stu-id="37132-159">Use the network from the remote data center.</span></span>
   - <span data-ttu-id="37132-160">Assegnare l'indirizzo IP dal nuovo servizio di bilanciamento del carico di Azure.</span><span class="sxs-lookup"><span data-stu-id="37132-160">Assign the IP address from the new Azure load balancer.</span></span> 

1. <span data-ttu-id="37132-161">Nella nuova istanza di SQL Server in Gestione configurazione SQL Server [abilitare i gruppi di disponibilità AlwaysOn](http://msdn.microsoft.com/library/ff878259.aspx).</span><span class="sxs-lookup"><span data-stu-id="37132-161">On the new SQL Server in SQL Server Configuration Manager, [enable Always On Availability Groups](http://msdn.microsoft.com/library/ff878259.aspx).</span></span>

1. <span data-ttu-id="37132-162">[Aprire le porte del firewall nella nuova istanza di SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span><span class="sxs-lookup"><span data-stu-id="37132-162">[Open firewall ports on the new SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span></span>

   <span data-ttu-id="37132-163">I numeri di porta che è necessario aprire dipendono dall'ambiente.</span><span class="sxs-lookup"><span data-stu-id="37132-163">The port numbers you need to open depend on your environment.</span></span> <span data-ttu-id="37132-164">Aprire le porte per l'endpoint del mirroring e il probe di integrità di bilanciamento del carico di Azure.</span><span class="sxs-lookup"><span data-stu-id="37132-164">Open ports for the mirroring endpoint and Azure load balancer health probe.</span></span>

1. <span data-ttu-id="37132-165">[Aggiungere una replica al gruppo di disponibilità nella nuova istanza di SQL Server](http://msdn.microsoft.com/library/hh213239.aspx).</span><span class="sxs-lookup"><span data-stu-id="37132-165">[Add a replica to the availability group on the new SQL Server](http://msdn.microsoft.com/library/hh213239.aspx).</span></span>

   <span data-ttu-id="37132-166">Per una replica in un'area di Azure remota, impostarla per la replica asincrona con il failover manuale.</span><span class="sxs-lookup"><span data-stu-id="37132-166">For a replica in a remote Azure region, set it for asynchronous replication with manual failover.</span></span>  

1. <span data-ttu-id="37132-167">Aggiungere la risorsa indirizzo IP come dipendenza per il cluster del punto di accesso client listener (nome della rete).</span><span class="sxs-lookup"><span data-stu-id="37132-167">Add the IP address resource as a dependency for the listener client access point (network name) cluster.</span></span>

   <span data-ttu-id="37132-168">Lo screenshot seguente illustra una risorsa cluster di tipo indirizzo IP configurata correttamente:</span><span class="sxs-lookup"><span data-stu-id="37132-168">The following screenshot shows a properly configured IP address cluster resource:</span></span>

   ![Gruppo di disponibilità](./media/virtual-machines-windows-portal-sql-availability-group-dr/50-configure-dependency-multiple-ip.png)

   >[!IMPORTANT]
   ><span data-ttu-id="37132-170">Il gruppo di risorse cluster include entrambi gli indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="37132-170">The cluster resource group includes both IP addresses.</span></span> <span data-ttu-id="37132-171">Entrambi gli indirizzi IP sono dipendenze per il punto di accesso client listener.</span><span class="sxs-lookup"><span data-stu-id="37132-171">Both IP addresses are dependencies for the listener client access point.</span></span> <span data-ttu-id="37132-172">Usare l'operatore **OR** nella configurazione delle dipendenze del cluster.</span><span class="sxs-lookup"><span data-stu-id="37132-172">Use the **OR** operator in the cluster dependency configuration.</span></span>

1. <span data-ttu-id="37132-173">[Impostare i parametri del cluster in PowerShell](virtual-machines-windows-portal-sql-availability-group-tutorial.md#setparam).</span><span class="sxs-lookup"><span data-stu-id="37132-173">[Set the cluster parameters in PowerShell](virtual-machines-windows-portal-sql-availability-group-tutorial.md#setparam).</span></span>

<span data-ttu-id="37132-174">Eseguire lo script PowerShell con il nome di rete cluster, l'indirizzo IP e la porta probe configurati nel servizio di bilanciamento del carico nella nuova area.</span><span class="sxs-lookup"><span data-stu-id="37132-174">Run the PowerShell script with the cluster network name, IP address, and probe port that you configured on the load balancer in the new region.</span></span>

   ```PowerShell
   $ClusterNetworkName = "<MyClusterNetworkName>" # The cluster name for the network in the new region (Use Get-ClusterNetwork on Windows Server 2012 of higher to find the name).
   $IPResourceName = "<IPResourceName>" # The cluster name for the new IP Address resource.
   $ILBIP = “<n.n.n.n>” # The IP Address of the Internal Load Balancer (ILB) in the new region. This is the static IP address for the load balancer you configured in the Azure portal.
   [int]$ProbePort = <nnnnn> # The probe port you set on the ILB.

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```

## <a name="set-connection-for-multiple-subnets"></a><span data-ttu-id="37132-175">Impostare la connessione per più subnet</span><span class="sxs-lookup"><span data-stu-id="37132-175">Set connection for multiple subnets</span></span>

<span data-ttu-id="37132-176">La replica nel data center remoto fa parte del gruppo di disponibilità, ma si trova in un'altra subnet.</span><span class="sxs-lookup"><span data-stu-id="37132-176">The replica in the remote data center is part of the availability group but it is in a different subnet.</span></span> <span data-ttu-id="37132-177">Se questa replica diventa quella primaria, possono verificarsi timeout della connessione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="37132-177">If this replica becomes the primary replica, application connection time-outs may occur.</span></span> <span data-ttu-id="37132-178">Questo comportamento è lo stesso di un gruppo di disponibilità locale in una distribuzione su più subnet.</span><span class="sxs-lookup"><span data-stu-id="37132-178">This behavior is the same as an on-premises availability group in a multi-subnet deployment.</span></span> <span data-ttu-id="37132-179">Per consentire le connessioni dalle applicazioni client, aggiornare la connessione client o configurare la memorizzazione nella cache della risoluzione dei nomi nella risorsa nome di rete del cluster.</span><span class="sxs-lookup"><span data-stu-id="37132-179">To allow connections from client applications, either update the client connection or configure name resolution caching on the cluster network name resource.</span></span>

<span data-ttu-id="37132-180">È preferibile aggiornare le stringhe di connessione client per impostare `MultiSubnetFailover=Yes`.</span><span class="sxs-lookup"><span data-stu-id="37132-180">Preferably, update the client connection strings to set `MultiSubnetFailover=Yes`.</span></span> <span data-ttu-id="37132-181">Vedere [Connessione con MultiSubnetFailover](http://msdn.microsoft.com/library/gg471494#Anchor_0).</span><span class="sxs-lookup"><span data-stu-id="37132-181">See [Connecting With MultiSubnetFailover](http://msdn.microsoft.com/library/gg471494#Anchor_0).</span></span>

<span data-ttu-id="37132-182">Se non è possibile modificare le stringhe di connessione, è possibile configurare la memorizzazione nella cache della risoluzione dei nomi.</span><span class="sxs-lookup"><span data-stu-id="37132-182">If you cannot modify the connection strings, you can configure name resolution caching.</span></span> <span data-ttu-id="37132-183">Vedere [Connection Timeouts in Multi-subnet Availability Group](http://blogs.msdn.microsoft.com/alwaysonpro/2014/06/03/connection-timeouts-in-multi-subnet-availability-group/) (Timeout connessione in un gruppo di disponibilità su più subnet).</span><span class="sxs-lookup"><span data-stu-id="37132-183">See [Connection Timeouts in Multi-subnet Availability Group](http://blogs.msdn.microsoft.com/alwaysonpro/2014/06/03/connection-timeouts-in-multi-subnet-availability-group/).</span></span>

## <a name="fail-over-to-remote-region"></a><span data-ttu-id="37132-184">Effettuare il failover in un'area remota</span><span class="sxs-lookup"><span data-stu-id="37132-184">Fail over to remote region</span></span>

<span data-ttu-id="37132-185">Per testare la connettività del listener all'area remota, è possibile effettuare il failover della replica nell'area remota.</span><span class="sxs-lookup"><span data-stu-id="37132-185">To test listener connectivity to the remote region, you can fail over the replica to the remote region.</span></span> <span data-ttu-id="37132-186">Mentre la replica è asincrona, il failover è soggetto a perdita potenziale di dati.</span><span class="sxs-lookup"><span data-stu-id="37132-186">While the replica is asynchronous, failover is vulnerable to potential data loss.</span></span> <span data-ttu-id="37132-187">Per effettuare il failover senza perdita di dati, impostare la modalità di disponibilità come sincrona e la modalità di failover come automatica.</span><span class="sxs-lookup"><span data-stu-id="37132-187">To fail over without data loss, change the availability mode to synchronous and set the failover mode to automatic.</span></span> <span data-ttu-id="37132-188">Seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="37132-188">Use the following steps:</span></span>

1. <span data-ttu-id="37132-189">In **Esplora oggetti** connettersi all'istanza di SQL Server che ospita la replica primaria.</span><span class="sxs-lookup"><span data-stu-id="37132-189">In **Object Explorer**, connect to the instance of SQL Server that hosts the primary replica.</span></span>
1. <span data-ttu-id="37132-190">In **Gruppi di disponibilità AlwaysOn**, **Gruppi di disponibilità** fare clic con il pulsante destro del mouse sul gruppo di disponibilità e scegliere **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="37132-190">Under **AlwaysOn Availability Groups**, **Availability Groups**, right-click your availability group and click **Properties**.</span></span>
1. <span data-ttu-id="37132-191">Nella pagina **Generale** in **Repliche di disponibilità** impostare la replica secondaria nel sito di ripristino di emergenza per l'uso della modalità di disponibilità **Commit sincrono** e della modalità di failover **Automatico**.</span><span class="sxs-lookup"><span data-stu-id="37132-191">On the **General** page, under **Availability Replicas**, set the secondary replica in the DR site to use **Synchronous Commit** availability mode and **Automatic** failover mode.</span></span>
1. <span data-ttu-id="37132-192">Se è presente una replica secondaria nello stesso sito della replica primaria per la disponibilità elevata, impostare questa replica su **Commit asincrono** e **Manuale**.</span><span class="sxs-lookup"><span data-stu-id="37132-192">If you have a secondary replica in same site as your primary replica for high availability, set this replica to **Asynchronous Commit** and **Manual**.</span></span>
1. <span data-ttu-id="37132-193">Fare clic su OK.</span><span class="sxs-lookup"><span data-stu-id="37132-193">Click OK.</span></span>
1. <span data-ttu-id="37132-194">In **Esplora oggetti** fare clic con il pulsante destro del mouse sul gruppo di disponibilità e scegliere **Mostra dashboard**.</span><span class="sxs-lookup"><span data-stu-id="37132-194">In **Object Explorer**, right-click the availability group, and click **Show Dashboard**.</span></span>
1. <span data-ttu-id="37132-195">Nel dashboard verificare che la replica nel sito di ripristino di emergenza sia sincronizzata.</span><span class="sxs-lookup"><span data-stu-id="37132-195">On the dashboard, verify that the replica on the DR site is synchronized.</span></span>
1. <span data-ttu-id="37132-196">In **Esplora oggetti** fare clic con il pulsante destro del mouse sul gruppo di disponibilità e scegliere **Failover**.</span><span class="sxs-lookup"><span data-stu-id="37132-196">In **Object Explorer**, right-click the availability group, and click **Failover...**.</span></span> <span data-ttu-id="37132-197">SQL Server Management Studio apre una procedura guidata per il failover di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="37132-197">SQL Server Management Studios opens a wizard to fail over SQL Server.</span></span>  
1. <span data-ttu-id="37132-198">Fare clic su **Avanti** e selezionare l'istanza di SQL Server nel sito del ripristino di emergenza.</span><span class="sxs-lookup"><span data-stu-id="37132-198">Click **Next**, and select the SQL Server instance in the DR site.</span></span> <span data-ttu-id="37132-199">Fare di nuovo clic su **Avanti** .</span><span class="sxs-lookup"><span data-stu-id="37132-199">Click **Next** again.</span></span>
1. <span data-ttu-id="37132-200">Connettersi all'istanza di SQL Server nel sito di ripristino di emergenza e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="37132-200">Connect to the SQL Server instance in the DR site and click **Next**.</span></span>
1. <span data-ttu-id="37132-201">Nella pagina **Riepilogo** verificare le impostazioni e fare clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="37132-201">On the **Summary** page, verify the settings and click **Finish**.</span></span>

<span data-ttu-id="37132-202">Dopo avere testato la connettività, spostare di nuovo la replica primaria nel data center primario e configurare di nuovo la modalità di disponibilità sulle normali impostazioni operative.</span><span class="sxs-lookup"><span data-stu-id="37132-202">After testing connectivity, move the primary replica back to your primary data center and set the availability mode back to their normal operating settings.</span></span> <span data-ttu-id="37132-203">La tabella seguente indica le normali impostazioni operative per l'architettura descritta in questo documento:</span><span class="sxs-lookup"><span data-stu-id="37132-203">The following table shows the normal operational settings for the architecture described in this document:</span></span>

| <span data-ttu-id="37132-204">Percorso</span><span class="sxs-lookup"><span data-stu-id="37132-204">Location</span></span> | <span data-ttu-id="37132-205">Istanza del server</span><span class="sxs-lookup"><span data-stu-id="37132-205">Server Instance</span></span> | <span data-ttu-id="37132-206">Ruolo</span><span class="sxs-lookup"><span data-stu-id="37132-206">Role</span></span> | <span data-ttu-id="37132-207">Modalità di disponibilità</span><span class="sxs-lookup"><span data-stu-id="37132-207">Availability Mode</span></span> | <span data-ttu-id="37132-208">Modalità di failover</span><span class="sxs-lookup"><span data-stu-id="37132-208">Failover Mode</span></span>
| ----- | ----- | ----- | ----- | -----
| <span data-ttu-id="37132-209">Data center primario</span><span class="sxs-lookup"><span data-stu-id="37132-209">Primary data center</span></span> | <span data-ttu-id="37132-210">SQL-1</span><span class="sxs-lookup"><span data-stu-id="37132-210">SQL-1</span></span> | <span data-ttu-id="37132-211">Primario</span><span class="sxs-lookup"><span data-stu-id="37132-211">Primary</span></span> | <span data-ttu-id="37132-212">Sincrono</span><span class="sxs-lookup"><span data-stu-id="37132-212">Synchronous</span></span> | <span data-ttu-id="37132-213">Automatico</span><span class="sxs-lookup"><span data-stu-id="37132-213">Automatic</span></span>
| <span data-ttu-id="37132-214">Data center primario</span><span class="sxs-lookup"><span data-stu-id="37132-214">Primary data center</span></span> | <span data-ttu-id="37132-215">SQL-2</span><span class="sxs-lookup"><span data-stu-id="37132-215">SQL-2</span></span> | <span data-ttu-id="37132-216">Secondario</span><span class="sxs-lookup"><span data-stu-id="37132-216">Secondary</span></span> | <span data-ttu-id="37132-217">Sincrono</span><span class="sxs-lookup"><span data-stu-id="37132-217">Synchronous</span></span> | <span data-ttu-id="37132-218">Automatico</span><span class="sxs-lookup"><span data-stu-id="37132-218">Automatic</span></span>
| <span data-ttu-id="37132-219">Data center secondario o remoto</span><span class="sxs-lookup"><span data-stu-id="37132-219">Secondary or remote data center</span></span> | <span data-ttu-id="37132-220">SQL-3</span><span class="sxs-lookup"><span data-stu-id="37132-220">SQL-3</span></span> | <span data-ttu-id="37132-221">Secondario</span><span class="sxs-lookup"><span data-stu-id="37132-221">Secondary</span></span> | <span data-ttu-id="37132-222">Asincrono</span><span class="sxs-lookup"><span data-stu-id="37132-222">Asynchronous</span></span> | <span data-ttu-id="37132-223">Manuale</span><span class="sxs-lookup"><span data-stu-id="37132-223">Manual</span></span>


### <a name="more-information-about-planned-and-forced-manual-failover"></a><span data-ttu-id="37132-224">Altre informazioni sul failover manuale forzato e pianificato</span><span class="sxs-lookup"><span data-stu-id="37132-224">More information about planned and forced manual failover</span></span>

<span data-ttu-id="37132-225">Per ulteriori informazioni, vedere gli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="37132-225">For more information, see the following topics:</span></span>

- [<span data-ttu-id="37132-226">Eseguire un failover manuale pianificato di un gruppo di disponibilità (SQL Server)</span><span class="sxs-lookup"><span data-stu-id="37132-226">Perform a Planned Manual Failover of an Availability Group (SQL Server)</span></span>](http://msdn.microsoft.com/library/hh231018.aspx)
- [<span data-ttu-id="37132-227">Eseguire un failover manuale forzato di un gruppo di disponibilità (SQL Server)</span><span class="sxs-lookup"><span data-stu-id="37132-227">Perform a Forced Manual Failover of an Availability Group (SQL Server)</span></span>](http://msdn.microsoft.com/library/ff877957.aspx)

## <a name="additional-links"></a><span data-ttu-id="37132-228">Altri collegamenti</span><span class="sxs-lookup"><span data-stu-id="37132-228">Additional Links</span></span>

* [<span data-ttu-id="37132-229">Gruppi di disponibilità AlwaysOn</span><span class="sxs-lookup"><span data-stu-id="37132-229">Always On Availability Groups</span></span>](http://msdn.microsoft.com/library/hh510230.aspx)
* [<span data-ttu-id="37132-230">Macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="37132-230">Azure Virtual Machines</span></span>](http://docs.microsoft.com/azure/virtual-machines/windows/)
* [<span data-ttu-id="37132-231">Servizi di bilanciamento del carico di Azure</span><span class="sxs-lookup"><span data-stu-id="37132-231">Azure Load Balancers</span></span>](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer)
* [<span data-ttu-id="37132-232">Set di disponibilità di Azure</span><span class="sxs-lookup"><span data-stu-id="37132-232">Azure Availability Sets</span></span>](../manage-availability.md)
