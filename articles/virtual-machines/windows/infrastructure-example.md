---
title: procedura dettagliata dell'infrastruttura di Azure aaaExample | Documenti Microsoft
description: Informazioni su hello progettazione e implementazione di linee guida fondamentali per la distribuzione di un'infrastruttura di esempio in Azure.
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7032b586-e4e5-4954-952f-fdfc03fc1980
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bd6b6e904404bea0b5be37dfce6d60039daae636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="example-azure-infrastructure-walkthrough-for-windows-vms"></a><span data-ttu-id="82551-103">Procedura dettagliata per un'infrastruttura di esempio di Azure per macchine virtuali Windows</span><span class="sxs-lookup"><span data-stu-id="82551-103">Example Azure infrastructure walkthrough for Windows VMs</span></span>

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

<span data-ttu-id="82551-104">Questo articolo illustra le modalità di compilazione di un'infrastruttura di applicazione di esempio.</span><span class="sxs-lookup"><span data-stu-id="82551-104">This article walks through building out an example application infrastructure.</span></span> <span data-ttu-id="82551-105">Si illustra in dettaglio la progettazione di un'infrastruttura per un negozio online semplice che raggruppa tutte le linee guida hello e decisioni sulla convenzioni di denominazione, i set di disponibilità, le reti virtuali e servizi di bilanciamento del carico e riguarda la distribuzione delle macchine virtuali (VM).</span><span class="sxs-lookup"><span data-stu-id="82551-105">We detail designing an infrastructure for a simple on-line store that brings together all hello guidelines and decisions around naming conventions, availability sets, virtual networks and load balancers, and actually deploying your virtual machines (VMs).</span></span>

## <a name="example-workload"></a><span data-ttu-id="82551-106">Carico di lavoro di esempio</span><span class="sxs-lookup"><span data-stu-id="82551-106">Example workload</span></span>
<span data-ttu-id="82551-107">Adventure Works Cycles desidera toobuild un'applicazione di negozio online in Azure che è costituito da:</span><span class="sxs-lookup"><span data-stu-id="82551-107">Adventure Works Cycles wants toobuild an on-line store application in Azure that consists of:</span></span>

* <span data-ttu-id="82551-108">Due server IIS che eseguono client hello front-end in un livello web</span><span class="sxs-lookup"><span data-stu-id="82551-108">Two IIS servers running hello client front-end in a web tier</span></span>
* <span data-ttu-id="82551-109">Due server IIS che elaborano i dati e gli ordini in un livello applicazione</span><span class="sxs-lookup"><span data-stu-id="82551-109">Two IIS servers processing data and orders in an application tier</span></span>
* <span data-ttu-id="82551-110">Due istanze di Microsoft SQL Server con gruppi di disponibilità AlwaysOn (due SQL Server e un server di controllo del nodo di maggioranza) per archiviare dati sui prodotti e ordini in un livello di database</span><span class="sxs-lookup"><span data-stu-id="82551-110">Two Microsoft SQL Server instances with AlwaysOn availability groups (two SQL Servers and a majority node witness) for storing product data and orders in a database tier</span></span>
* <span data-ttu-id="82551-111">Due controller di dominio di Active Directory per gli account dei clienti e dei fornitori in un livello di autenticazione</span><span class="sxs-lookup"><span data-stu-id="82551-111">Two Active Directory domain controllers for customer accounts and suppliers in an authentication tier</span></span>
* <span data-ttu-id="82551-112">Tutti i server hello si trovano in due subnet:</span><span class="sxs-lookup"><span data-stu-id="82551-112">All hello servers are located in two subnets:</span></span>
  * <span data-ttu-id="82551-113">una subnet front-end per i server web hello</span><span class="sxs-lookup"><span data-stu-id="82551-113">a front-end subnet for hello web servers</span></span> 
  * <span data-ttu-id="82551-114">una subnet di back-end per i server applicazioni hello, cluster di SQL e i controller di dominio</span><span class="sxs-lookup"><span data-stu-id="82551-114">a back-end subnet for hello application servers, SQL cluster, and domain controllers</span></span>

![Diagramma dei diversi livelli di infrastruttura dell'applicazione](./media/infrastructure-example/example-tiers.png)

<span data-ttu-id="82551-116">In ingresso sicuro il traffico web deve essere con carico bilanciato tra i server web hello negozio online hello per esaminare i clienti.</span><span class="sxs-lookup"><span data-stu-id="82551-116">Incoming secure web traffic must be load-balanced among hello web servers as customers browse hello on-line store.</span></span> <span data-ttu-id="82551-117">Ordine del traffico di elaborazione nel modulo hello di richieste HTTP effettuate dal web hello server devono essere bilanciati tra i server applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="82551-117">Order processing traffic in hello form of HTTP requests from hello web servers must be balanced among hello application servers.</span></span> <span data-ttu-id="82551-118">Inoltre, l'infrastruttura hello deve essere progettata per la disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="82551-118">Additionally, hello infrastructure must be designed for high availability.</span></span>

<span data-ttu-id="82551-119">progettazione di Hello risultante deve includere:</span><span class="sxs-lookup"><span data-stu-id="82551-119">hello resulting design must incorporate:</span></span>

* <span data-ttu-id="82551-120">Una sottoscrizione e un account di Azure</span><span class="sxs-lookup"><span data-stu-id="82551-120">An Azure subscription and account</span></span>
* <span data-ttu-id="82551-121">Un unico gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="82551-121">A single resource group</span></span>
* <span data-ttu-id="82551-122">Azure Managed Disks</span><span class="sxs-lookup"><span data-stu-id="82551-122">Azure Managed Disks</span></span>
* <span data-ttu-id="82551-123">Una rete virtuale con due subnet</span><span class="sxs-lookup"><span data-stu-id="82551-123">A virtual network with two subnets</span></span>
* <span data-ttu-id="82551-124">Set di disponibilità per hello macchine virtuali con un ruolo simile</span><span class="sxs-lookup"><span data-stu-id="82551-124">Availability sets for hello VMs with a similar role</span></span>
* <span data-ttu-id="82551-125">Macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="82551-125">Virtual machines</span></span>

<span data-ttu-id="82551-126">Hello tutti precedente queste convenzioni di denominazione:</span><span class="sxs-lookup"><span data-stu-id="82551-126">All hello above follow these naming conventions:</span></span>

* <span data-ttu-id="82551-127">Adventure Works Cycles usa come prefisso **[carico di lavoro IT]-[località]-[risorsa di Azure]**</span><span class="sxs-lookup"><span data-stu-id="82551-127">Adventure Works Cycles uses **[IT workload]-[location]-[Azure resource]** as a prefix</span></span>
  * <span data-ttu-id="82551-128">Per questo esempio, "**azos**" (archivio online di Azure) è hello il nome del carico di lavoro IT e "**utilizzare**" (Stati Uniti orientali 2) è il percorso di hello</span><span class="sxs-lookup"><span data-stu-id="82551-128">For this example, "**azos**" (Azure On-line Store) is hello IT workload name and "**use**" (East US 2) is hello location</span></span>
* <span data-ttu-id="82551-129">Le reti virtuali usano AZOS-USE-VN**[numero]**</span><span class="sxs-lookup"><span data-stu-id="82551-129">Virtual networks use AZOS-USE-VN**[number]**</span></span>
* <span data-ttu-id="82551-130">I set di disponibilità usano azos-use-as-**[ruolo]**</span><span class="sxs-lookup"><span data-stu-id="82551-130">Availability sets use azos-use-as-**[role]**</span></span>
* <span data-ttu-id="82551-131">I nomi delle macchine virtuali usano azos-use-vm-**[nomevm]**</span><span class="sxs-lookup"><span data-stu-id="82551-131">Virtual machine names use azos-use-vm-**[vmname]**</span></span>

## <a name="azure-subscriptions-and-accounts"></a><span data-ttu-id="82551-132">Sottoscrizioni e account di Azure</span><span class="sxs-lookup"><span data-stu-id="82551-132">Azure subscriptions and accounts</span></span>
<span data-ttu-id="82551-133">Adventure Works Cycles è tramite la sottoscrizione dell'organizzazione, denominata Adventure Works Enterprise sottoscrizione, tooprovide fatturazione per il carico di lavoro IT.</span><span class="sxs-lookup"><span data-stu-id="82551-133">Adventure Works Cycles is using their Enterprise subscription, named Adventure Works Enterprise Subscription, tooprovide billing for this IT workload.</span></span>

## <a name="storage"></a><span data-ttu-id="82551-134">Archiviazione</span><span class="sxs-lookup"><span data-stu-id="82551-134">Storage</span></span>
<span data-ttu-id="82551-135">Adventure Works Cycles ha determinato che è necessario usare Managed Disks di Azure.</span><span class="sxs-lookup"><span data-stu-id="82551-135">Adventure Works Cycles determined that they should use Azure Managed Disks.</span></span> <span data-ttu-id="82551-136">Durante la creazione di macchine virtuali, vengono usati entrambi i livelli di archiviazione disponibili:</span><span class="sxs-lookup"><span data-stu-id="82551-136">When creating VMs, both storage available storage tiers are used:</span></span>

* <span data-ttu-id="82551-137">**Archiviazione standard** per server web hello, server applicazioni e i controller di dominio e i relativi dischi dati.</span><span class="sxs-lookup"><span data-stu-id="82551-137">**Standard storage** for hello web servers, application servers, and domain controllers and their data disks.</span></span>
* <span data-ttu-id="82551-138">**Archiviazione Premium** per macchine virtuali di hello SQL Server e dei dischi dati.</span><span class="sxs-lookup"><span data-stu-id="82551-138">**Premium storage** for hello SQL Server VMs and their data disks.</span></span>

## <a name="virtual-network-and-subnets"></a><span data-ttu-id="82551-139">Rete virtuale e subnet</span><span class="sxs-lookup"><span data-stu-id="82551-139">Virtual network and subnets</span></span>
<span data-ttu-id="82551-140">Poiché la rete virtuale hello non necessita di rete locale di connettività in corso toohello Adventure lavoro cicli, essi deciso in una rete virtuale solo cloud.</span><span class="sxs-lookup"><span data-stu-id="82551-140">Because hello virtual network does not need ongoing connectivity toohello Adventure Work Cycles on-premises network, they decided on a cloud-only virtual network.</span></span>

<span data-ttu-id="82551-141">Una rete virtuale solo cloud sono creati con hello seguendo le impostazioni utilizzando hello portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="82551-141">They created a cloud-only virtual network with hello following settings using hello Azure portal:</span></span>

* <span data-ttu-id="82551-142">Nome: AZOS-USE-VN01</span><span class="sxs-lookup"><span data-stu-id="82551-142">Name: AZOS-USE-VN01</span></span>
* <span data-ttu-id="82551-143">Sede: Stati Uniti orientali 2</span><span class="sxs-lookup"><span data-stu-id="82551-143">Location: East US 2</span></span>
* <span data-ttu-id="82551-144">Spazio degli indirizzi della rete virtuale: 10.0.0.0/8</span><span class="sxs-lookup"><span data-stu-id="82551-144">Virtual network address space: 10.0.0.0/8</span></span>
* <span data-ttu-id="82551-145">Prima subnet:</span><span class="sxs-lookup"><span data-stu-id="82551-145">First subnet:</span></span>
  * <span data-ttu-id="82551-146">Nome: FrontEnd</span><span class="sxs-lookup"><span data-stu-id="82551-146">Name: FrontEnd</span></span>
  * <span data-ttu-id="82551-147">Spazio degli indirizzi: 10.0.1.0/24</span><span class="sxs-lookup"><span data-stu-id="82551-147">Address space: 10.0.1.0/24</span></span>
* <span data-ttu-id="82551-148">Seconda subnet:</span><span class="sxs-lookup"><span data-stu-id="82551-148">Second subnet:</span></span>
  * <span data-ttu-id="82551-149">Nome: BackEnd</span><span class="sxs-lookup"><span data-stu-id="82551-149">Name: BackEnd</span></span>
  * <span data-ttu-id="82551-150">Spazio degli indirizzi: 10.0.2.0/24</span><span class="sxs-lookup"><span data-stu-id="82551-150">Address space: 10.0.2.0/24</span></span>

## <a name="availability-sets"></a><span data-ttu-id="82551-151">Set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="82551-151">Availability sets</span></span>
<span data-ttu-id="82551-152">disponibilità elevata di toomaintain di tutti i quattro livelli di relativo archivio online, Adventure Works Cycles decidere su quattro set di disponibilità:</span><span class="sxs-lookup"><span data-stu-id="82551-152">toomaintain high availability of all four tiers of their on-line store, Adventure Works Cycles decided on four availability sets:</span></span>

* <span data-ttu-id="82551-153">**Utilizzare azos come web** per i server web hello</span><span class="sxs-lookup"><span data-stu-id="82551-153">**azos-use-as-web** for hello web servers</span></span>
* <span data-ttu-id="82551-154">**Utilizzare azos come app** per i server applicazioni hello</span><span class="sxs-lookup"><span data-stu-id="82551-154">**azos-use-as-app** for hello application servers</span></span>
* <span data-ttu-id="82551-155">**Utilizzare azos come sql** per hello istanze di SQL Server</span><span class="sxs-lookup"><span data-stu-id="82551-155">**azos-use-as-sql** for hello SQL Servers</span></span>
* <span data-ttu-id="82551-156">**azos utilizzare come controller di dominio** hello ai controller di dominio</span><span class="sxs-lookup"><span data-stu-id="82551-156">**azos-use-as-dc** for hello domain controllers</span></span>

## <a name="virtual-machines"></a><span data-ttu-id="82551-157">Macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="82551-157">Virtual machines</span></span>
<span data-ttu-id="82551-158">Adventure Works Cycles scelto hello seguenti nomi per le proprie macchine virtuali di Azure:</span><span class="sxs-lookup"><span data-stu-id="82551-158">Adventure Works Cycles decided on hello following names for their Azure VMs:</span></span>

* <span data-ttu-id="82551-159">**azos-utilizzo-vm-web01** per il server web prima di hello</span><span class="sxs-lookup"><span data-stu-id="82551-159">**azos-use-vm-web01** for hello first web server</span></span>
* <span data-ttu-id="82551-160">**azos-utilizzo-vm-web02** per server web secondo hello</span><span class="sxs-lookup"><span data-stu-id="82551-160">**azos-use-vm-web02** for hello second web server</span></span>
* <span data-ttu-id="82551-161">**azos-utilizzo-vm-il server app01** per il primo server di applicazione hello</span><span class="sxs-lookup"><span data-stu-id="82551-161">**azos-use-vm-app01** for hello first application server</span></span>
* <span data-ttu-id="82551-162">**azos-utilizzo-vm-app02** per il server applicazioni secondo hello</span><span class="sxs-lookup"><span data-stu-id="82551-162">**azos-use-vm-app02** for hello second application server</span></span>
* <span data-ttu-id="82551-163">**azos-utilizzo-vm-sql01** per hello primo Server di SQL server in cluster hello</span><span class="sxs-lookup"><span data-stu-id="82551-163">**azos-use-vm-sql01** for hello first SQL Server server in hello cluster</span></span>
* <span data-ttu-id="82551-164">**azos-utilizzo-vm-sql02** per hello secondo Server di SQL server in cluster hello</span><span class="sxs-lookup"><span data-stu-id="82551-164">**azos-use-vm-sql02** for hello second SQL Server server in hello cluster</span></span>
* <span data-ttu-id="82551-165">**azos-utilizzo-vm-dc01** per il primo controller di dominio hello</span><span class="sxs-lookup"><span data-stu-id="82551-165">**azos-use-vm-dc01** for hello first domain controller</span></span>
* <span data-ttu-id="82551-166">**azos-utilizzo-vm-dc02** per il secondo controller di dominio hello</span><span class="sxs-lookup"><span data-stu-id="82551-166">**azos-use-vm-dc02** for hello second domain controller</span></span>

<span data-ttu-id="82551-167">Di seguito è riportata la configurazione risultante hello.</span><span class="sxs-lookup"><span data-stu-id="82551-167">Here is hello resulting configuration.</span></span>

![Infrastruttura dell'applicazione finale distribuita in Azure](./media/infrastructure-example/example-config.png)

<span data-ttu-id="82551-169">Questa configurazione include:</span><span class="sxs-lookup"><span data-stu-id="82551-169">This configuration incorporates:</span></span>

* <span data-ttu-id="82551-170">Una rete virtuale solo cloud con due subnet (front-end e back-end)</span><span class="sxs-lookup"><span data-stu-id="82551-170">A cloud-only virtual network with two subnets (FrontEnd and BackEnd)</span></span>
* <span data-ttu-id="82551-171">Managed Disks di Azure con dischi Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="82551-171">Azure Managed Disks with both Standard and Premium disks</span></span>
* <span data-ttu-id="82551-172">Quattro set di disponibilità, uno per ogni livello di negozio online hello</span><span class="sxs-lookup"><span data-stu-id="82551-172">Four availability sets, one for each tier of hello on-line store</span></span>
* <span data-ttu-id="82551-173">macchine virtuali Hello per i livelli di hello quattro</span><span class="sxs-lookup"><span data-stu-id="82551-173">hello virtual machines for hello four tiers</span></span>
* <span data-ttu-id="82551-174">Un set esterno con carico bilanciato per il traffico web basato su HTTPS dai server web di hello Internet toohello</span><span class="sxs-lookup"><span data-stu-id="82551-174">An external load balanced set for HTTPS-based web traffic from hello Internet toohello web servers</span></span>
* <span data-ttu-id="82551-175">Set per il traffico web crittografato dal server di applicazioni toohello hello web server con un interno carico bilanciato</span><span class="sxs-lookup"><span data-stu-id="82551-175">An internal load balanced set for unencrypted web traffic from hello web servers toohello application servers</span></span>
* <span data-ttu-id="82551-176">Un unico gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="82551-176">A single resource group</span></span>