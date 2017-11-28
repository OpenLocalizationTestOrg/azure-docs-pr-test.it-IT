---
title: aaaOverview di uno scenario di ripristino di emergenza Oracle nell'ambiente Azure | Documenti Microsoft
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
ms.openlocfilehash: 1fa69e1ba044b46b27695fec92fd9ca82df796f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="disaster-recovery-for-an-oracle-database-12c-database-in-an-azure-environment"></a><span data-ttu-id="6b0ea-103">Ripristino di emergenza per un'istanza di Database Oracle 12c in un ambiente Azure</span><span class="sxs-lookup"><span data-stu-id="6b0ea-103">Disaster recovery for an Oracle Database 12c database in an Azure environment</span></span>

## <a name="assumptions"></a><span data-ttu-id="6b0ea-104">Presupposti</span><span class="sxs-lookup"><span data-stu-id="6b0ea-104">Assumptions</span></span>

- <span data-ttu-id="6b0ea-105">Conoscenza degli ambienti Azure e della progettazione di Oracle Data Guard.</span><span class="sxs-lookup"><span data-stu-id="6b0ea-105">You have an understanding of Oracle Data Guard design and Azure environments.</span></span>


## <a name="goals"></a><span data-ttu-id="6b0ea-106">Obiettivi</span><span class="sxs-lookup"><span data-stu-id="6b0ea-106">Goals</span></span>
- <span data-ttu-id="6b0ea-107">Progettare hello topologia e configurazione che soddisfano i requisiti di ripristino di emergenza di emergenza.</span><span class="sxs-lookup"><span data-stu-id="6b0ea-107">Design hello topology and configuration that meet your disaster recovery (DR) requirements.</span></span>

## <a name="scenario-1-primary-and-dr-sites-on-azure"></a><span data-ttu-id="6b0ea-108">Scenario 1: Siti primari e di ripristino di emergenza in Azure</span><span class="sxs-lookup"><span data-stu-id="6b0ea-108">Scenario 1: Primary and DR sites on Azure</span></span>

<span data-ttu-id="6b0ea-109">Un cliente ha Oracle database set di backup nel sito primario di hello.</span><span class="sxs-lookup"><span data-stu-id="6b0ea-109">A customer has an Oracle database set up on hello primary site.</span></span> <span data-ttu-id="6b0ea-110">Un sito di ripristino di emergenza si trova in un'area diversa.</span><span class="sxs-lookup"><span data-stu-id="6b0ea-110">A DR site is in a different region.</span></span> <span data-ttu-id="6b0ea-111">il cliente di Hello utilizza Oracle Data Guard per il ripristino rapido tra questi siti.</span><span class="sxs-lookup"><span data-stu-id="6b0ea-111">hello customer uses Oracle Data Guard for quick recovery between these sites.</span></span> <span data-ttu-id="6b0ea-112">sito primario di Hello dispone di un database secondario per la creazione di report e altri utilizzi.</span><span class="sxs-lookup"><span data-stu-id="6b0ea-112">hello primary site also has a secondary database for reporting and other uses.</span></span> 

### <a name="topology"></a><span data-ttu-id="6b0ea-113">Topologia</span><span class="sxs-lookup"><span data-stu-id="6b0ea-113">Topology</span></span>

<span data-ttu-id="6b0ea-114">Di seguito è riportato un riepilogo di hello installazione di Azure:</span><span class="sxs-lookup"><span data-stu-id="6b0ea-114">Here is a summary of hello Azure setup:</span></span>

- <span data-ttu-id="6b0ea-115">Due siti (un sito primario e un sito di ripristino di emergenza)</span><span class="sxs-lookup"><span data-stu-id="6b0ea-115">Two sites (a primary site and a DR site)</span></span>
- <span data-ttu-id="6b0ea-116">Due reti virtuali</span><span class="sxs-lookup"><span data-stu-id="6b0ea-116">Two virtual networks</span></span>
- <span data-ttu-id="6b0ea-117">Due database Oracle con Data Guard (primario e standby)</span><span class="sxs-lookup"><span data-stu-id="6b0ea-117">Two Oracle databases with Data Guard (primary and standby)</span></span>
- <span data-ttu-id="6b0ea-118">Due database Oracle con Golden Gate o Data Guard (solo sito primario)</span><span class="sxs-lookup"><span data-stu-id="6b0ea-118">Two Oracle databases with Golden Gate or Data Guard (primary site only)</span></span>
- <span data-ttu-id="6b0ea-119">Due servizi delle applicazioni, uno primario e uno nel sito di ripristino di emergenza hello</span><span class="sxs-lookup"><span data-stu-id="6b0ea-119">Two application services, one primary and one on hello DR site</span></span>
- <span data-ttu-id="6b0ea-120">Un *set di disponibilità,* utilizzato per il servizio di database e dell'applicazione nel sito primario di hello</span><span class="sxs-lookup"><span data-stu-id="6b0ea-120">An *availability set,* which is used for database and application service on hello primary site</span></span>
- <span data-ttu-id="6b0ea-121">Uno jumpbox in ogni sito, che limita l'accesso di rete privata toohello e consente solo accesso in ingresso da un amministratore</span><span class="sxs-lookup"><span data-stu-id="6b0ea-121">One jumpbox on each site, which restricts access toohello private network and only allows sign-in by an administrator</span></span>
- <span data-ttu-id="6b0ea-122">Un jumpbox, un servizio dell'applicazione, un database e un gateway VPN in subnet separate</span><span class="sxs-lookup"><span data-stu-id="6b0ea-122">A jumpbox, application service, database, and VPN gateway on separate subnets</span></span>
- <span data-ttu-id="6b0ea-123">Gruppo di sicurezza di rete applicato nelle subnet dell'applicazione e del database</span><span class="sxs-lookup"><span data-stu-id="6b0ea-123">NSG enforced on application and database subnets</span></span>

![Schermata della pagina di topologia hello ripristino di emergenza](./media/oracle-disaster-recovery/oracle_topology_01.png)

## <a name="scenario-2-primary-site-on-premises-and-dr-site-on-azure"></a><span data-ttu-id="6b0ea-125">Scenario 2: Sito primario locale e sito di ripristino di emergenza in Azure</span><span class="sxs-lookup"><span data-stu-id="6b0ea-125">Scenario 2: Primary site on-premises and DR site on Azure</span></span>

<span data-ttu-id="6b0ea-126">Il cliente ha una configurazione del database Oracle locale nel sito primario.</span><span class="sxs-lookup"><span data-stu-id="6b0ea-126">A customer has an on-premises Oracle database setup (primary site).</span></span> <span data-ttu-id="6b0ea-127">Il sito di un ripristino di emergenza è in Azure.</span><span class="sxs-lookup"><span data-stu-id="6b0ea-127">A DR site is on Azure.</span></span> <span data-ttu-id="6b0ea-128">Oracle Data Guard viene usato per eseguire un ripristino rapido tra questi siti.</span><span class="sxs-lookup"><span data-stu-id="6b0ea-128">Oracle Data Guard is used for quick recovery between these sites.</span></span> <span data-ttu-id="6b0ea-129">sito primario di Hello dispone di un database secondario per la creazione di report e altri utilizzi.</span><span class="sxs-lookup"><span data-stu-id="6b0ea-129">hello primary site also has a secondary database for reporting and other uses.</span></span> 

<span data-ttu-id="6b0ea-130">Per questo tipo di configurazione esistono due approcci.</span><span class="sxs-lookup"><span data-stu-id="6b0ea-130">There are two approaches for this setup.</span></span>

### <a name="approach-1-direct-connections-between-on-premises-and-azure-requiring-open-tcp-ports-on-hello-firewall"></a><span data-ttu-id="6b0ea-131">Approccio 1: Connessioni dirette tra sedi locali e Azure, che richiedono porte TCP aperte nel firewall hello</span><span class="sxs-lookup"><span data-stu-id="6b0ea-131">Approach 1: Direct connections between on-premises and Azure, requiring open TCP ports on hello firewall</span></span> 

<span data-ttu-id="6b0ea-132">Connessioni dirette non è consigliabile in quanto espongono toohello porte TCP di hello world di fuori.</span><span class="sxs-lookup"><span data-stu-id="6b0ea-132">We don't recommend direct connections because they expose hello TCP ports toohello outside world.</span></span>

#### <a name="topology"></a><span data-ttu-id="6b0ea-133">Topologia</span><span class="sxs-lookup"><span data-stu-id="6b0ea-133">Topology</span></span>

<span data-ttu-id="6b0ea-134">Ecco un riepilogo di hello installazione di Azure:</span><span class="sxs-lookup"><span data-stu-id="6b0ea-134">Following is a summary of hello Azure setup:</span></span>

- <span data-ttu-id="6b0ea-135">Un sito di ripristino di emergenza</span><span class="sxs-lookup"><span data-stu-id="6b0ea-135">One DR site</span></span> 
- <span data-ttu-id="6b0ea-136">Una rete virtuale</span><span class="sxs-lookup"><span data-stu-id="6b0ea-136">One virtual network</span></span>
- <span data-ttu-id="6b0ea-137">Un database Oracle con Data Guard (attivo)</span><span class="sxs-lookup"><span data-stu-id="6b0ea-137">One Oracle database with Data Guard (active)</span></span>
- <span data-ttu-id="6b0ea-138">Servizio di un'applicazione nel sito di ripristino di emergenza hello</span><span class="sxs-lookup"><span data-stu-id="6b0ea-138">One application service on hello DR site</span></span>
- <span data-ttu-id="6b0ea-139">Uno jumpbox, che limita l'accesso di rete privata toohello e consente solo accesso in ingresso da un amministratore</span><span class="sxs-lookup"><span data-stu-id="6b0ea-139">One jumpbox, which restricts access toohello private network and only allows sign-in by an administrator</span></span>
- <span data-ttu-id="6b0ea-140">Un jumpbox, un servizio dell'applicazione, un database e un gateway VPN in subnet separate</span><span class="sxs-lookup"><span data-stu-id="6b0ea-140">A jumpbox, application service, database, and VPN gateway on separate subnets</span></span>
- <span data-ttu-id="6b0ea-141">Gruppo di sicurezza di rete applicato nelle subnet dell'applicazione e del database</span><span class="sxs-lookup"><span data-stu-id="6b0ea-141">NSG enforced on application and database subnets</span></span>
- <span data-ttu-id="6b0ea-142">Un tooallow/regola dei criteri di gruppo in ingresso porta 1521 (o una porta definita dall'utente)</span><span class="sxs-lookup"><span data-stu-id="6b0ea-142">An NSG policy/rule tooallow inbound TCP port 1521 (or a user-defined port)</span></span>
- <span data-ttu-id="6b0ea-143">Una gruppo/regola dei criteri toorestrict solo hello IP indirizzo o gli indirizzi locali (database o applicazione) tooaccess hello rete virtuale</span><span class="sxs-lookup"><span data-stu-id="6b0ea-143">An NSG policy/rule toorestrict only hello IP address/addresses on-premises (DB or application) tooaccess hello virtual network</span></span>

![Schermata della pagina di topologia hello ripristino di emergenza](./media/oracle-disaster-recovery/oracle_topology_02.png)

### <a name="approach-2-site-to-site-vpn"></a><span data-ttu-id="6b0ea-145">Approccio 2: VPN da sito a sito</span><span class="sxs-lookup"><span data-stu-id="6b0ea-145">Approach 2: Site-to-site VPN</span></span>
<span data-ttu-id="6b0ea-146">La VPN da sito a sito è un approccio migliore.</span><span class="sxs-lookup"><span data-stu-id="6b0ea-146">Site-to-site VPN is a better approach.</span></span> <span data-ttu-id="6b0ea-147">Per altre informazioni sulla configurazione di una VPN, vedere [Creare una rete virtuale con una connessione VPN da sito a sito usando l'interfaccia della riga di comando](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span><span class="sxs-lookup"><span data-stu-id="6b0ea-147">For more information about setting up a VPN, see [Create a virtual network with a Site-to-Site VPN connection using CLI](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span></span>

#### <a name="topology"></a><span data-ttu-id="6b0ea-148">Topologia</span><span class="sxs-lookup"><span data-stu-id="6b0ea-148">Topology</span></span>

<span data-ttu-id="6b0ea-149">Ecco un riepilogo di hello installazione di Azure:</span><span class="sxs-lookup"><span data-stu-id="6b0ea-149">Following is a summary of hello Azure setup:</span></span>

- <span data-ttu-id="6b0ea-150">Un sito di ripristino di emergenza</span><span class="sxs-lookup"><span data-stu-id="6b0ea-150">One DR site</span></span> 
- <span data-ttu-id="6b0ea-151">Una rete virtuale</span><span class="sxs-lookup"><span data-stu-id="6b0ea-151">One virtual network</span></span> 
- <span data-ttu-id="6b0ea-152">Un database Oracle con Data Guard (attivo)</span><span class="sxs-lookup"><span data-stu-id="6b0ea-152">One Oracle database with Data Guard (active)</span></span>
- <span data-ttu-id="6b0ea-153">Servizio di un'applicazione nel sito di ripristino di emergenza hello</span><span class="sxs-lookup"><span data-stu-id="6b0ea-153">One application service on hello DR site</span></span>
- <span data-ttu-id="6b0ea-154">Uno jumpbox, che limita l'accesso di rete privata toohello e consente solo accesso in ingresso da un amministratore</span><span class="sxs-lookup"><span data-stu-id="6b0ea-154">One jumpbox, which restricts access toohello private network and only allows sign-in by an administrator</span></span>
- <span data-ttu-id="6b0ea-155">Un jumpbox, un servizio dell'applicazione, un database e un gateway VPN in subnet separate</span><span class="sxs-lookup"><span data-stu-id="6b0ea-155">A jumpbox, application service, database, and VPN gateway are on separate subnets</span></span>
- <span data-ttu-id="6b0ea-156">Gruppo di sicurezza di rete applicato nelle subnet dell'applicazione e del database</span><span class="sxs-lookup"><span data-stu-id="6b0ea-156">NSG enforced on application and database subnets</span></span>
- <span data-ttu-id="6b0ea-157">Connessione VPN da sito a sito tra rete locale e Azure</span><span class="sxs-lookup"><span data-stu-id="6b0ea-157">Site-to-site VPN connection between on-premises and Azure</span></span>

![Schermata della pagina di topologia hello ripristino di emergenza](./media/oracle-disaster-recovery/oracle_topology_03.png)

## <a name="additional-reading"></a><span data-ttu-id="6b0ea-159">Informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="6b0ea-159">Additional reading</span></span>

- [<span data-ttu-id="6b0ea-160">Progettare e implementare un database Oracle in Azure</span><span class="sxs-lookup"><span data-stu-id="6b0ea-160">Design and implement an Oracle database on Azure</span></span>](oracle-design.md)
- [<span data-ttu-id="6b0ea-161">Configurare Oracle Data Guard</span><span class="sxs-lookup"><span data-stu-id="6b0ea-161">Configure Oracle Data Guard</span></span>](configure-oracle-dataguard.md)
- [<span data-ttu-id="6b0ea-162">Configurare Oracle Golden Gate</span><span class="sxs-lookup"><span data-stu-id="6b0ea-162">Configure Oracle Golden Gate</span></span>](configure-oracle-golden-gate.md)
- [<span data-ttu-id="6b0ea-163">Backup e ripristino di Oracle</span><span class="sxs-lookup"><span data-stu-id="6b0ea-163">Oracle backup and recovery</span></span>](oracle-backup-recovery.md)


## <a name="next-steps"></a><span data-ttu-id="6b0ea-164">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6b0ea-164">Next steps</span></span>

- [<span data-ttu-id="6b0ea-165">Esercitazione: Creare VM a disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="6b0ea-165">Tutorial: Create highly available VMs</span></span>](../../linux/create-cli-complete.md)
- [<span data-ttu-id="6b0ea-166">Esplorare gli esempi dell'interfaccia della riga di comando di Azure per la distribuzione della VM</span><span class="sxs-lookup"><span data-stu-id="6b0ea-166">Explore VM deployment Azure CLI samples</span></span>](../../linux/cli-samples.md)
