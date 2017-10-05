---
title: Panoramica di uno scenario di ripristino di emergenza di Oracle nell'ambiente Azure | Microsoft Docs
description: Scenario di ripristino di emergenza per un'istanza di Database Oracle 12c nell'ambiente Azure
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 6/2/2017
ms.author: rclaus
ms.openlocfilehash: f17ebb2b74cd7ad872f88483ed7cdb4f239ee069
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="disaster-recovery-for-an-oracle-database-12c-database-in-an-azure-environment"></a><span data-ttu-id="53a9c-103">Ripristino di emergenza per un'istanza di Database Oracle 12c in un ambiente Azure</span><span class="sxs-lookup"><span data-stu-id="53a9c-103">Disaster recovery for an Oracle Database 12c database in an Azure environment</span></span>

## <a name="assumptions"></a><span data-ttu-id="53a9c-104">Presupposti</span><span class="sxs-lookup"><span data-stu-id="53a9c-104">Assumptions</span></span>

- <span data-ttu-id="53a9c-105">Conoscenza degli ambienti Azure e della progettazione di Oracle Data Guard.</span><span class="sxs-lookup"><span data-stu-id="53a9c-105">You have an understanding of Oracle Data Guard design and Azure environments.</span></span>


## <a name="goals"></a><span data-ttu-id="53a9c-106">Obiettivi</span><span class="sxs-lookup"><span data-stu-id="53a9c-106">Goals</span></span>
- <span data-ttu-id="53a9c-107">Progettare la topologia e la configurazione che soddisfano i requisiti di ripristino di emergenza.</span><span class="sxs-lookup"><span data-stu-id="53a9c-107">Design the topology and configuration that meet your disaster recovery (DR) requirements.</span></span>

## <a name="scenario-1-primary-and-dr-sites-on-azure"></a><span data-ttu-id="53a9c-108">Scenario 1: Siti primari e di ripristino di emergenza in Azure</span><span class="sxs-lookup"><span data-stu-id="53a9c-108">Scenario 1: Primary and DR sites on Azure</span></span>

<span data-ttu-id="53a9c-109">Un cliente ha un database Oracle configurato nel sito primario.</span><span class="sxs-lookup"><span data-stu-id="53a9c-109">A customer has an Oracle database set up on the primary site.</span></span> <span data-ttu-id="53a9c-110">Un sito di ripristino di emergenza si trova in un'area diversa.</span><span class="sxs-lookup"><span data-stu-id="53a9c-110">A DR site is in a different region.</span></span> <span data-ttu-id="53a9c-111">Il cliente usa Oracle Data Guard per eseguire un ripristino rapido tra questi siti.</span><span class="sxs-lookup"><span data-stu-id="53a9c-111">The customer uses Oracle Data Guard for quick recovery between these sites.</span></span> <span data-ttu-id="53a9c-112">Il sito primario ha anche un database secondario per la creazione di report e altri usi.</span><span class="sxs-lookup"><span data-stu-id="53a9c-112">The primary site also has a secondary database for reporting and other uses.</span></span> 

### <a name="topology"></a><span data-ttu-id="53a9c-113">Topologia</span><span class="sxs-lookup"><span data-stu-id="53a9c-113">Topology</span></span>

<span data-ttu-id="53a9c-114">Ecco un riepilogo della configurazione di Azure:</span><span class="sxs-lookup"><span data-stu-id="53a9c-114">Here is a summary of the Azure setup:</span></span>

- <span data-ttu-id="53a9c-115">Due siti (un sito primario e un sito di ripristino di emergenza)</span><span class="sxs-lookup"><span data-stu-id="53a9c-115">Two sites (a primary site and a DR site)</span></span>
- <span data-ttu-id="53a9c-116">Due reti virtuali</span><span class="sxs-lookup"><span data-stu-id="53a9c-116">Two virtual networks</span></span>
- <span data-ttu-id="53a9c-117">Due database Oracle con Data Guard (primario e standby)</span><span class="sxs-lookup"><span data-stu-id="53a9c-117">Two Oracle databases with Data Guard (primary and standby)</span></span>
- <span data-ttu-id="53a9c-118">Due database Oracle con Golden Gate o Data Guard (solo sito primario)</span><span class="sxs-lookup"><span data-stu-id="53a9c-118">Two Oracle databases with Golden Gate or Data Guard (primary site only)</span></span>
- <span data-ttu-id="53a9c-119">Due servizi dell'applicazione, uno primario e uno nel sito di ripristino di emergenza</span><span class="sxs-lookup"><span data-stu-id="53a9c-119">Two application services, one primary and one on the DR site</span></span>
- <span data-ttu-id="53a9c-120">Un *set di disponibilità*, usato per il servizio dell'applicazione e il database nel sito primario</span><span class="sxs-lookup"><span data-stu-id="53a9c-120">An *availability set,* which is used for database and application service on the primary site</span></span>
- <span data-ttu-id="53a9c-121">Un jumpbox in ogni sito, che limita l'accesso alla rete privata e consente l'accesso solo a un amministratore</span><span class="sxs-lookup"><span data-stu-id="53a9c-121">One jumpbox on each site, which restricts access to the private network and only allows sign-in by an administrator</span></span>
- <span data-ttu-id="53a9c-122">Un jumpbox, un servizio dell'applicazione, un database e un gateway VPN in subnet separate</span><span class="sxs-lookup"><span data-stu-id="53a9c-122">A jumpbox, application service, database, and VPN gateway on separate subnets</span></span>
- <span data-ttu-id="53a9c-123">Gruppo di sicurezza di rete applicato nelle subnet dell'applicazione e del database</span><span class="sxs-lookup"><span data-stu-id="53a9c-123">NSG enforced on application and database subnets</span></span>

![Schermata della pagina di topologia del ripristino di emergenza](./media/oracle-disaster-recovery/oracle_topology_01.png)

## <a name="scenario-2-primary-site-on-premises-and-dr-site-on-azure"></a><span data-ttu-id="53a9c-125">Scenario 2: Sito primario locale e sito di ripristino di emergenza in Azure</span><span class="sxs-lookup"><span data-stu-id="53a9c-125">Scenario 2: Primary site on-premises and DR site on Azure</span></span>

<span data-ttu-id="53a9c-126">Il cliente ha una configurazione del database Oracle locale nel sito primario.</span><span class="sxs-lookup"><span data-stu-id="53a9c-126">A customer has an on-premises Oracle database setup (primary site).</span></span> <span data-ttu-id="53a9c-127">Il sito di un ripristino di emergenza è in Azure.</span><span class="sxs-lookup"><span data-stu-id="53a9c-127">A DR site is on Azure.</span></span> <span data-ttu-id="53a9c-128">Oracle Data Guard viene usato per eseguire un ripristino rapido tra questi siti.</span><span class="sxs-lookup"><span data-stu-id="53a9c-128">Oracle Data Guard is used for quick recovery between these sites.</span></span> <span data-ttu-id="53a9c-129">Il sito primario ha anche un database secondario per la creazione di report e altri usi.</span><span class="sxs-lookup"><span data-stu-id="53a9c-129">The primary site also has a secondary database for reporting and other uses.</span></span> 

<span data-ttu-id="53a9c-130">Per questo tipo di configurazione esistono due approcci.</span><span class="sxs-lookup"><span data-stu-id="53a9c-130">There are two approaches for this setup.</span></span>

### <a name="approach-1-direct-connections-between-on-premises-and-azure-requiring-open-tcp-ports-on-the-firewall"></a><span data-ttu-id="53a9c-131">Approccio 1: Connessioni dirette tra siti locali e Azure, che richiedono porte TCP aperte sul firewall</span><span class="sxs-lookup"><span data-stu-id="53a9c-131">Approach 1: Direct connections between on-premises and Azure, requiring open TCP ports on the firewall</span></span> 

<span data-ttu-id="53a9c-132">Le connessioni dirette non sono consigliate perché espongono le porte TCP al mondo esterno.</span><span class="sxs-lookup"><span data-stu-id="53a9c-132">We don't recommend direct connections because they expose the TCP ports to the outside world.</span></span>

#### <a name="topology"></a><span data-ttu-id="53a9c-133">Topologia</span><span class="sxs-lookup"><span data-stu-id="53a9c-133">Topology</span></span>

<span data-ttu-id="53a9c-134">Il seguente è un riepilogo della configurazione di Azure:</span><span class="sxs-lookup"><span data-stu-id="53a9c-134">Following is a summary of the Azure setup:</span></span>

- <span data-ttu-id="53a9c-135">Un sito di ripristino di emergenza</span><span class="sxs-lookup"><span data-stu-id="53a9c-135">One DR site</span></span> 
- <span data-ttu-id="53a9c-136">Una rete virtuale</span><span class="sxs-lookup"><span data-stu-id="53a9c-136">One virtual network</span></span>
- <span data-ttu-id="53a9c-137">Un database Oracle con Data Guard (attivo)</span><span class="sxs-lookup"><span data-stu-id="53a9c-137">One Oracle database with Data Guard (active)</span></span>
- <span data-ttu-id="53a9c-138">Un servizio dell'applicazione nel sito di ripristino di emergenza</span><span class="sxs-lookup"><span data-stu-id="53a9c-138">One application service on the DR site</span></span>
- <span data-ttu-id="53a9c-139">Un jumpbox, che limita l'accesso alla rete privata e consente l'accesso solo a un amministratore</span><span class="sxs-lookup"><span data-stu-id="53a9c-139">One jumpbox, which restricts access to the private network and only allows sign-in by an administrator</span></span>
- <span data-ttu-id="53a9c-140">Un jumpbox, un servizio dell'applicazione, un database e un gateway VPN in subnet separate</span><span class="sxs-lookup"><span data-stu-id="53a9c-140">A jumpbox, application service, database, and VPN gateway on separate subnets</span></span>
- <span data-ttu-id="53a9c-141">Gruppo di sicurezza di rete applicato nelle subnet dell'applicazione e del database</span><span class="sxs-lookup"><span data-stu-id="53a9c-141">NSG enforced on application and database subnets</span></span>
- <span data-ttu-id="53a9c-142">Un criterio o una regola del gruppo di sicurezza di rete per consentire la porta TCP 1521 in ingresso (o una porta definita dall'utente)</span><span class="sxs-lookup"><span data-stu-id="53a9c-142">An NSG policy/rule to allow inbound TCP port 1521 (or a user-defined port)</span></span>
- <span data-ttu-id="53a9c-143">Un criterio o una regola del gruppo di sicurezza di rete per limitare l'accesso alla rete virtuale solo all'indirizzo IP o agli indirizzi locali (database o applicazione)</span><span class="sxs-lookup"><span data-stu-id="53a9c-143">An NSG policy/rule to restrict only the IP address/addresses on-premises (DB or application) to access the virtual network</span></span>

![Schermata della pagina di topologia del ripristino di emergenza](./media/oracle-disaster-recovery/oracle_topology_02.png)

### <a name="approach-2-site-to-site-vpn"></a><span data-ttu-id="53a9c-145">Approccio 2: VPN da sito a sito</span><span class="sxs-lookup"><span data-stu-id="53a9c-145">Approach 2: Site-to-site VPN</span></span>
<span data-ttu-id="53a9c-146">La VPN da sito a sito è un approccio migliore.</span><span class="sxs-lookup"><span data-stu-id="53a9c-146">Site-to-site VPN is a better approach.</span></span> <span data-ttu-id="53a9c-147">Per altre informazioni sulla configurazione di una VPN, vedere [Creare una rete virtuale con una connessione VPN da sito a sito usando l'interfaccia della riga di comando](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span><span class="sxs-lookup"><span data-stu-id="53a9c-147">For more information about setting up a VPN, see [Create a virtual network with a Site-to-Site VPN connection using CLI](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span></span>

#### <a name="topology"></a><span data-ttu-id="53a9c-148">Topologia</span><span class="sxs-lookup"><span data-stu-id="53a9c-148">Topology</span></span>

<span data-ttu-id="53a9c-149">Il seguente è un riepilogo della configurazione di Azure:</span><span class="sxs-lookup"><span data-stu-id="53a9c-149">Following is a summary of the Azure setup:</span></span>

- <span data-ttu-id="53a9c-150">Un sito di ripristino di emergenza</span><span class="sxs-lookup"><span data-stu-id="53a9c-150">One DR site</span></span> 
- <span data-ttu-id="53a9c-151">Una rete virtuale</span><span class="sxs-lookup"><span data-stu-id="53a9c-151">One virtual network</span></span> 
- <span data-ttu-id="53a9c-152">Un database Oracle con Data Guard (attivo)</span><span class="sxs-lookup"><span data-stu-id="53a9c-152">One Oracle database with Data Guard (active)</span></span>
- <span data-ttu-id="53a9c-153">Un servizio dell'applicazione nel sito di ripristino di emergenza</span><span class="sxs-lookup"><span data-stu-id="53a9c-153">One application service on the DR site</span></span>
- <span data-ttu-id="53a9c-154">Un jumpbox, che limita l'accesso alla rete privata e consente l'accesso solo a un amministratore</span><span class="sxs-lookup"><span data-stu-id="53a9c-154">One jumpbox, which restricts access to the private network and only allows sign-in by an administrator</span></span>
- <span data-ttu-id="53a9c-155">Un jumpbox, un servizio dell'applicazione, un database e un gateway VPN in subnet separate</span><span class="sxs-lookup"><span data-stu-id="53a9c-155">A jumpbox, application service, database, and VPN gateway are on separate subnets</span></span>
- <span data-ttu-id="53a9c-156">Gruppo di sicurezza di rete applicato nelle subnet dell'applicazione e del database</span><span class="sxs-lookup"><span data-stu-id="53a9c-156">NSG enforced on application and database subnets</span></span>
- <span data-ttu-id="53a9c-157">Connessione VPN da sito a sito tra rete locale e Azure</span><span class="sxs-lookup"><span data-stu-id="53a9c-157">Site-to-site VPN connection between on-premises and Azure</span></span>

![Schermata della pagina di topologia del ripristino di emergenza](./media/oracle-disaster-recovery/oracle_topology_03.png)

## <a name="additional-reading"></a><span data-ttu-id="53a9c-159">Informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="53a9c-159">Additional reading</span></span>

- [<span data-ttu-id="53a9c-160">Progettare e implementare un database Oracle in Azure</span><span class="sxs-lookup"><span data-stu-id="53a9c-160">Design and implement an Oracle database on Azure</span></span>](oracle-design.md)
- [<span data-ttu-id="53a9c-161">Configurare Oracle Data Guard</span><span class="sxs-lookup"><span data-stu-id="53a9c-161">Configure Oracle Data Guard</span></span>](configure-oracle-dataguard.md)
- [<span data-ttu-id="53a9c-162">Configurare Oracle Golden Gate</span><span class="sxs-lookup"><span data-stu-id="53a9c-162">Configure Oracle Golden Gate</span></span>](configure-oracle-golden-gate.md)
- [<span data-ttu-id="53a9c-163">Backup e ripristino di Oracle</span><span class="sxs-lookup"><span data-stu-id="53a9c-163">Oracle backup and recovery</span></span>](oracle-backup-recovery.md)


## <a name="next-steps"></a><span data-ttu-id="53a9c-164">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="53a9c-164">Next steps</span></span>

- [<span data-ttu-id="53a9c-165">Esercitazione: Creare VM a disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="53a9c-165">Tutorial: Create highly available VMs</span></span>](../../linux/create-cli-complete.md)
- [<span data-ttu-id="53a9c-166">Esplorare gli esempi dell'interfaccia della riga di comando di Azure per la distribuzione della VM</span><span class="sxs-lookup"><span data-stu-id="53a9c-166">Explore VM deployment Azure CLI samples</span></span>](../../linux/cli-samples.md)
