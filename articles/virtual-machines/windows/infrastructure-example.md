---
title: Procedura dettagliata per un'infrastruttura di esempio di Azure | Microsoft Docs
description: Informazioni sulle principali linee guida di progettazione e implementazione per la distribuzione di un'infrastruttura di esempio in Azure.
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
ms.openlocfilehash: 84cefcdb85f1a3c753027e827abde010b461cda7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="example-azure-infrastructure-walkthrough-for-windows-vms"></a><span data-ttu-id="e9ede-103">Procedura dettagliata per un'infrastruttura di esempio di Azure per macchine virtuali Windows</span><span class="sxs-lookup"><span data-stu-id="e9ede-103">Example Azure infrastructure walkthrough for Windows VMs</span></span>

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

<span data-ttu-id="e9ede-104">Questo articolo illustra le modalità di compilazione di un'infrastruttura di applicazione di esempio.</span><span class="sxs-lookup"><span data-stu-id="e9ede-104">This article walks through building out an example application infrastructure.</span></span> <span data-ttu-id="e9ede-105">Sarà trattata la progettazione di un'infrastruttura per un semplice negozio online che riunisce tutte le linee guida e le decisioni sulle convenzioni di denominazione, i set di disponibilità, le reti virtuali e i servizi di bilanciamento del carico e l'effettiva distribuzione delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="e9ede-105">We detail designing an infrastructure for a simple on-line store that brings together all the guidelines and decisions around naming conventions, availability sets, virtual networks and load balancers, and actually deploying your virtual machines (VMs).</span></span>

## <a name="example-workload"></a><span data-ttu-id="e9ede-106">Carico di lavoro di esempio</span><span class="sxs-lookup"><span data-stu-id="e9ede-106">Example workload</span></span>
<span data-ttu-id="e9ede-107">Adventure Works Cycles desidera compilare un'applicazione per un negozio online in Azure, che è costituita da:</span><span class="sxs-lookup"><span data-stu-id="e9ede-107">Adventure Works Cycles wants to build an on-line store application in Azure that consists of:</span></span>

* <span data-ttu-id="e9ede-108">Due server IIS che eseguono il client front-end in un livello Web</span><span class="sxs-lookup"><span data-stu-id="e9ede-108">Two IIS servers running the client front-end in a web tier</span></span>
* <span data-ttu-id="e9ede-109">Due server IIS che elaborano i dati e gli ordini in un livello applicazione</span><span class="sxs-lookup"><span data-stu-id="e9ede-109">Two IIS servers processing data and orders in an application tier</span></span>
* <span data-ttu-id="e9ede-110">Due istanze di Microsoft SQL Server con gruppi di disponibilità AlwaysOn (due SQL Server e un server di controllo del nodo di maggioranza) per archiviare dati sui prodotti e ordini in un livello di database</span><span class="sxs-lookup"><span data-stu-id="e9ede-110">Two Microsoft SQL Server instances with AlwaysOn availability groups (two SQL Servers and a majority node witness) for storing product data and orders in a database tier</span></span>
* <span data-ttu-id="e9ede-111">Due controller di dominio di Active Directory per gli account dei clienti e dei fornitori in un livello di autenticazione</span><span class="sxs-lookup"><span data-stu-id="e9ede-111">Two Active Directory domain controllers for customer accounts and suppliers in an authentication tier</span></span>
* <span data-ttu-id="e9ede-112">Tutti i server si trovano in due subnet:</span><span class="sxs-lookup"><span data-stu-id="e9ede-112">All the servers are located in two subnets:</span></span>
  * <span data-ttu-id="e9ede-113">una subnet front-end per i server Web</span><span class="sxs-lookup"><span data-stu-id="e9ede-113">a front-end subnet for the web servers</span></span> 
  * <span data-ttu-id="e9ede-114">una subnet back-end per i server applicazioni, i cluster SQL e i controller di dominio</span><span class="sxs-lookup"><span data-stu-id="e9ede-114">a back-end subnet for the application servers, SQL cluster, and domain controllers</span></span>

![Diagramma dei diversi livelli di infrastruttura dell'applicazione](./media/infrastructure-example/example-tiers.png)

<span data-ttu-id="e9ede-116">Il traffico Web protetto in ingresso deve essere sottoposto al bilanciamento del carico tra i server Web mentre i clienti visitano il negozio online.</span><span class="sxs-lookup"><span data-stu-id="e9ede-116">Incoming secure web traffic must be load-balanced among the web servers as customers browse the on-line store.</span></span> <span data-ttu-id="e9ede-117">Il traffico di elaborazione degli ordini sotto forma di richieste HTTP provenienti dai server Web deve essere bilanciato tra i server applicazioni.</span><span class="sxs-lookup"><span data-stu-id="e9ede-117">Order processing traffic in the form of HTTP requests from the web servers must be balanced among the application servers.</span></span> <span data-ttu-id="e9ede-118">Inoltre, l'infrastruttura deve essere progettata per l'elevata disponibilità.</span><span class="sxs-lookup"><span data-stu-id="e9ede-118">Additionally, the infrastructure must be designed for high availability.</span></span>

<span data-ttu-id="e9ede-119">La progettazione risultante deve includere:</span><span class="sxs-lookup"><span data-stu-id="e9ede-119">The resulting design must incorporate:</span></span>

* <span data-ttu-id="e9ede-120">Una sottoscrizione e un account di Azure</span><span class="sxs-lookup"><span data-stu-id="e9ede-120">An Azure subscription and account</span></span>
* <span data-ttu-id="e9ede-121">Un unico gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="e9ede-121">A single resource group</span></span>
* <span data-ttu-id="e9ede-122">Azure Managed Disks</span><span class="sxs-lookup"><span data-stu-id="e9ede-122">Azure Managed Disks</span></span>
* <span data-ttu-id="e9ede-123">Una rete virtuale con due subnet</span><span class="sxs-lookup"><span data-stu-id="e9ede-123">A virtual network with two subnets</span></span>
* <span data-ttu-id="e9ede-124">Set di disponibilità per le macchine virtuali con ruoli simili</span><span class="sxs-lookup"><span data-stu-id="e9ede-124">Availability sets for the VMs with a similar role</span></span>
* <span data-ttu-id="e9ede-125">Macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="e9ede-125">Virtual machines</span></span>

<span data-ttu-id="e9ede-126">Tutti gli elementi devono rispettare le convenzioni di denominazione seguenti:</span><span class="sxs-lookup"><span data-stu-id="e9ede-126">All the above follow these naming conventions:</span></span>

* <span data-ttu-id="e9ede-127">Adventure Works Cycles usa come prefisso **[carico di lavoro IT]-[località]-[risorsa di Azure]**</span><span class="sxs-lookup"><span data-stu-id="e9ede-127">Adventure Works Cycles uses **[IT workload]-[location]-[Azure resource]** as a prefix</span></span>
  * <span data-ttu-id="e9ede-128">In questo esempio, "**azos**" (Azure online Store) è il nome del carico di lavoro IT e "**use**" (Stati Uniti orientali 2) è la località</span><span class="sxs-lookup"><span data-stu-id="e9ede-128">For this example, "**azos**" (Azure On-line Store) is the IT workload name and "**use**" (East US 2) is the location</span></span>
* <span data-ttu-id="e9ede-129">Le reti virtuali usano AZOS-USE-VN**[numero]**</span><span class="sxs-lookup"><span data-stu-id="e9ede-129">Virtual networks use AZOS-USE-VN**[number]**</span></span>
* <span data-ttu-id="e9ede-130">I set di disponibilità usano azos-use-as-**[ruolo]**</span><span class="sxs-lookup"><span data-stu-id="e9ede-130">Availability sets use azos-use-as-**[role]**</span></span>
* <span data-ttu-id="e9ede-131">I nomi delle macchine virtuali usano azos-use-vm-**[nomevm]**</span><span class="sxs-lookup"><span data-stu-id="e9ede-131">Virtual machine names use azos-use-vm-**[vmname]**</span></span>

## <a name="azure-subscriptions-and-accounts"></a><span data-ttu-id="e9ede-132">Sottoscrizioni e account di Azure</span><span class="sxs-lookup"><span data-stu-id="e9ede-132">Azure subscriptions and accounts</span></span>
<span data-ttu-id="e9ede-133">Adventure Works Cycles usa la propria sottoscrizione aziendale, denominata Adventure Works Enterprise Subscription, per fornire la fatturazione per questo carico di lavoro IT.</span><span class="sxs-lookup"><span data-stu-id="e9ede-133">Adventure Works Cycles is using their Enterprise subscription, named Adventure Works Enterprise Subscription, to provide billing for this IT workload.</span></span>

## <a name="storage"></a><span data-ttu-id="e9ede-134">Archiviazione</span><span class="sxs-lookup"><span data-stu-id="e9ede-134">Storage</span></span>
<span data-ttu-id="e9ede-135">Adventure Works Cycles ha determinato che è necessario usare Managed Disks di Azure.</span><span class="sxs-lookup"><span data-stu-id="e9ede-135">Adventure Works Cycles determined that they should use Azure Managed Disks.</span></span> <span data-ttu-id="e9ede-136">Durante la creazione di macchine virtuali, vengono usati entrambi i livelli di archiviazione disponibili:</span><span class="sxs-lookup"><span data-stu-id="e9ede-136">When creating VMs, both storage available storage tiers are used:</span></span>

* <span data-ttu-id="e9ede-137">**Archiviazione Standard** per i server Web, i server applicazioni e i controller di dominio e relativi dischi dati.</span><span class="sxs-lookup"><span data-stu-id="e9ede-137">**Standard storage** for the web servers, application servers, and domain controllers and their data disks.</span></span>
* <span data-ttu-id="e9ede-138">**Archiviazione Premium** per le VM SQL Server e relativi dischi dati.</span><span class="sxs-lookup"><span data-stu-id="e9ede-138">**Premium storage** for the SQL Server VMs and their data disks.</span></span>

## <a name="virtual-network-and-subnets"></a><span data-ttu-id="e9ede-139">Rete virtuale e subnet</span><span class="sxs-lookup"><span data-stu-id="e9ede-139">Virtual network and subnets</span></span>
<span data-ttu-id="e9ede-140">Poiché la rete virtuale non necessita di connettività costante alla rete locale Adventure Work Cycles, l’azienda ha optato per una rete virtuale solo cloud.</span><span class="sxs-lookup"><span data-stu-id="e9ede-140">Because the virtual network does not need ongoing connectivity to the Adventure Work Cycles on-premises network, they decided on a cloud-only virtual network.</span></span>

<span data-ttu-id="e9ede-141">Contoso ha creato una rete virtuale solo cloud con le impostazioni seguenti tramite il portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="e9ede-141">They created a cloud-only virtual network with the following settings using the Azure portal:</span></span>

* <span data-ttu-id="e9ede-142">Nome: AZOS-USE-VN01</span><span class="sxs-lookup"><span data-stu-id="e9ede-142">Name: AZOS-USE-VN01</span></span>
* <span data-ttu-id="e9ede-143">Sede: Stati Uniti orientali 2</span><span class="sxs-lookup"><span data-stu-id="e9ede-143">Location: East US 2</span></span>
* <span data-ttu-id="e9ede-144">Spazio degli indirizzi della rete virtuale: 10.0.0.0/8</span><span class="sxs-lookup"><span data-stu-id="e9ede-144">Virtual network address space: 10.0.0.0/8</span></span>
* <span data-ttu-id="e9ede-145">Prima subnet:</span><span class="sxs-lookup"><span data-stu-id="e9ede-145">First subnet:</span></span>
  * <span data-ttu-id="e9ede-146">Nome: FrontEnd</span><span class="sxs-lookup"><span data-stu-id="e9ede-146">Name: FrontEnd</span></span>
  * <span data-ttu-id="e9ede-147">Spazio degli indirizzi: 10.0.1.0/24</span><span class="sxs-lookup"><span data-stu-id="e9ede-147">Address space: 10.0.1.0/24</span></span>
* <span data-ttu-id="e9ede-148">Seconda subnet:</span><span class="sxs-lookup"><span data-stu-id="e9ede-148">Second subnet:</span></span>
  * <span data-ttu-id="e9ede-149">Nome: BackEnd</span><span class="sxs-lookup"><span data-stu-id="e9ede-149">Name: BackEnd</span></span>
  * <span data-ttu-id="e9ede-150">Spazio degli indirizzi: 10.0.2.0/24</span><span class="sxs-lookup"><span data-stu-id="e9ede-150">Address space: 10.0.2.0/24</span></span>

## <a name="availability-sets"></a><span data-ttu-id="e9ede-151">Set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="e9ede-151">Availability sets</span></span>
<span data-ttu-id="e9ede-152">Per mantenere elevata la disponibilità di tutti i quattro i livelli del negozio online, Adventure Works Cycles ha optato per quattro set di disponibilità:</span><span class="sxs-lookup"><span data-stu-id="e9ede-152">To maintain high availability of all four tiers of their on-line store, Adventure Works Cycles decided on four availability sets:</span></span>

* <span data-ttu-id="e9ede-153">**azos-use-as-web** per i server Web</span><span class="sxs-lookup"><span data-stu-id="e9ede-153">**azos-use-as-web** for the web servers</span></span>
* <span data-ttu-id="e9ede-154">**azos-use-as-app** per i server applicazioni</span><span class="sxs-lookup"><span data-stu-id="e9ede-154">**azos-use-as-app** for the application servers</span></span>
* <span data-ttu-id="e9ede-155">**azos-use-as-sql** per SQL Server</span><span class="sxs-lookup"><span data-stu-id="e9ede-155">**azos-use-as-sql** for the SQL Servers</span></span>
* <span data-ttu-id="e9ede-156">**azos-use-as-dc** per i controller di dominio</span><span class="sxs-lookup"><span data-stu-id="e9ede-156">**azos-use-as-dc** for the domain controllers</span></span>

## <a name="virtual-machines"></a><span data-ttu-id="e9ede-157">Macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="e9ede-157">Virtual machines</span></span>
<span data-ttu-id="e9ede-158">Adventure Works Cycles ha optato per i seguenti nomi per le macchine virtuali di Azure:</span><span class="sxs-lookup"><span data-stu-id="e9ede-158">Adventure Works Cycles decided on the following names for their Azure VMs:</span></span>

* <span data-ttu-id="e9ede-159">**azos-use-vm-web01** per il primo server Web</span><span class="sxs-lookup"><span data-stu-id="e9ede-159">**azos-use-vm-web01** for the first web server</span></span>
* <span data-ttu-id="e9ede-160">**azos-use-vm-web02** per il secondo server Web</span><span class="sxs-lookup"><span data-stu-id="e9ede-160">**azos-use-vm-web02** for the second web server</span></span>
* <span data-ttu-id="e9ede-161">**azos-use-vm-app01** per il primo server applicazioni</span><span class="sxs-lookup"><span data-stu-id="e9ede-161">**azos-use-vm-app01** for the first application server</span></span>
* <span data-ttu-id="e9ede-162">**azos-use-vm-app02** , per il secondo server applicazioni</span><span class="sxs-lookup"><span data-stu-id="e9ede-162">**azos-use-vm-app02** for the second application server</span></span>
* <span data-ttu-id="e9ede-163">**azos-use-vm-sql01** per il primo SQL Server del cluster</span><span class="sxs-lookup"><span data-stu-id="e9ede-163">**azos-use-vm-sql01** for the first SQL Server server in the cluster</span></span>
* <span data-ttu-id="e9ede-164">**azos-use-vm-sql02** per il secondo SQL Server del cluster</span><span class="sxs-lookup"><span data-stu-id="e9ede-164">**azos-use-vm-sql02** for the second SQL Server server in the cluster</span></span>
* <span data-ttu-id="e9ede-165">**azos-use-vm-dc01** per il primo controller di dominio</span><span class="sxs-lookup"><span data-stu-id="e9ede-165">**azos-use-vm-dc01** for the first domain controller</span></span>
* <span data-ttu-id="e9ede-166">**azos-use-vm-dc02** per il secondo controller di dominio</span><span class="sxs-lookup"><span data-stu-id="e9ede-166">**azos-use-vm-dc02** for the second domain controller</span></span>

<span data-ttu-id="e9ede-167">Di seguito è riportata la configurazione risultante.</span><span class="sxs-lookup"><span data-stu-id="e9ede-167">Here is the resulting configuration.</span></span>

![Infrastruttura dell'applicazione finale distribuita in Azure](./media/infrastructure-example/example-config.png)

<span data-ttu-id="e9ede-169">Questa configurazione include:</span><span class="sxs-lookup"><span data-stu-id="e9ede-169">This configuration incorporates:</span></span>

* <span data-ttu-id="e9ede-170">Una rete virtuale solo cloud con due subnet (front-end e back-end)</span><span class="sxs-lookup"><span data-stu-id="e9ede-170">A cloud-only virtual network with two subnets (FrontEnd and BackEnd)</span></span>
* <span data-ttu-id="e9ede-171">Managed Disks di Azure con dischi Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="e9ede-171">Azure Managed Disks with both Standard and Premium disks</span></span>
* <span data-ttu-id="e9ede-172">Quattro set di disponibilità, uno per ciascun livello del negozio online</span><span class="sxs-lookup"><span data-stu-id="e9ede-172">Four availability sets, one for each tier of the on-line store</span></span>
* <span data-ttu-id="e9ede-173">Le macchine virtuali per i quattro livelli</span><span class="sxs-lookup"><span data-stu-id="e9ede-173">The virtual machines for the four tiers</span></span>
* <span data-ttu-id="e9ede-174">Un set esterno con bilanciamento del carico per il traffico Web basato su HTTPS da Internet ai server Web</span><span class="sxs-lookup"><span data-stu-id="e9ede-174">An external load balanced set for HTTPS-based web traffic from the Internet to the web servers</span></span>
* <span data-ttu-id="e9ede-175">Un set interno con bilanciamento del carico per il traffico Web crittografato dai server Web ai server applicazioni</span><span class="sxs-lookup"><span data-stu-id="e9ede-175">An internal load balanced set for unencrypted web traffic from the web servers to the application servers</span></span>
* <span data-ttu-id="e9ede-176">Un unico gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="e9ede-176">A single resource group</span></span>