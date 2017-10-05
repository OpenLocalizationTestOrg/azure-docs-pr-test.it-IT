---
title: "Gruppi di disponibilità di SQL Server: Macchine virtuali di Azure: panoramica | Documentazione Microsoft"
description: "Questo articolo offre una panoramica sui gruppi di disponibilità di SQL Server in macchine virtuali di Azure."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 601eebb1-fc2c-4f5b-9c05-0e6ffd0e5334
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/13/2017
ms.author: mikeray
ms.openlocfilehash: 2cbb9ff3b2d13996b1b8dc64aa833807c264c877
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="introducing-sql-server-always-on-availability-groups-on-azure-virtual-machines"></a><span data-ttu-id="b2852-103">Panoramica sui gruppi di disponibilità AlwaysOn di SQL Server in macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="b2852-103">Introducing SQL Server Always On availability groups on Azure virtual machines</span></span> #

<span data-ttu-id="b2852-104">Questo articolo offre una panoramica sui gruppi di disponibilità di SQL Server in macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="b2852-104">This article introduces SQL Server availability groups on Azure Virtual Machines.</span></span> 

<span data-ttu-id="b2852-105">I gruppi di disponibilità AlwaysOn in macchine virtuali di Azure sono simili ai gruppi di disponibilità AlwaysOn locali.</span><span class="sxs-lookup"><span data-stu-id="b2852-105">Always On availability groups on Azure Virtual Machines are similar to Always On availability groups on premises.</span></span> <span data-ttu-id="b2852-106">Per altre informazioni, vedere [Gruppi di disponibilità AlwaysOn (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx).</span><span class="sxs-lookup"><span data-stu-id="b2852-106">For more information, see [Always On Availability Groups (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx).</span></span> 

<span data-ttu-id="b2852-107">Il diagramma seguente illustra le parti di un gruppo di disponibilità di SQL Server completo in macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="b2852-107">The diagram illustrates the parts of a complete SQL Server Availability Group in Azure Virtual Machines.</span></span>

![Gruppo di disponibilità](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

<span data-ttu-id="b2852-109">La differenza principale per un gruppo di disponibilità in macchine virtuali Azure è che per queste ultime è necessario un [servizio di bilanciamento del carico](../../../load-balancer/load-balancer-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b2852-109">The key difference for an Availability Group in Azure Virtual Machines is that the Azure virtual machines, require a [load balancer](../../../load-balancer/load-balancer-overview.md).</span></span> <span data-ttu-id="b2852-110">Il servizio di bilanciamento del carico contiene gli indirizzi IP per il listener del gruppo di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="b2852-110">The load balancer holds the IP addresses for the availability group listener.</span></span> <span data-ttu-id="b2852-111">Se sono disponibili più gruppi di disponibilità, è necessario un listener per ogni gruppo.</span><span class="sxs-lookup"><span data-stu-id="b2852-111">If you have more than one availability group each group requires a listener.</span></span> <span data-ttu-id="b2852-112">Un servizio di bilanciamento del carico può supportare più listener.</span><span class="sxs-lookup"><span data-stu-id="b2852-112">One load balancer can support multiple listeners.</span></span>

<span data-ttu-id="b2852-113">Per compilare un gruppo di disponibilità di SQL Server in macchine virtuali di Azure, vedere le esercitazioni indicate di seguito.</span><span class="sxs-lookup"><span data-stu-id="b2852-113">When you are ready to build a SQL Server availability aroup on Azure Virtual Machines, refer to these tutorials.</span></span>

## <a name="automatically-create-an-availability-group-from-a-template"></a><span data-ttu-id="b2852-114">Creare automaticamente un gruppo di disponibilità da un modello</span><span class="sxs-lookup"><span data-stu-id="b2852-114">Automatically create an availability group from a template</span></span>

[<span data-ttu-id="b2852-115">Configurare automaticamente il gruppo di disponibilità AlwaysOn in macchine virtuali di Azure con Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b2852-115">Configure Always On availability group in Azure VM automatically - Resource Manager</span></span>](virtual-machines-windows-portal-sql-alwayson-availability-groups.md)

## <a name="manually-create-an-availability-group-in-azure-portal"></a><span data-ttu-id="b2852-116">Creare manualmente un gruppo di disponibilità nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="b2852-116">Manually create an availability group in Azure portal</span></span>

<span data-ttu-id="b2852-117">È anche possibile creare le macchine virtuali manualmente senza il modello.</span><span class="sxs-lookup"><span data-stu-id="b2852-117">You can also create the virtual machines yourself without the template.</span></span> <span data-ttu-id="b2852-118">A tale scopo, è necessario completare prima i prerequisiti e quindi creare il gruppo di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="b2852-118">First, complete the prerequisites, then create the availability group.</span></span> <span data-ttu-id="b2852-119">Vedere gli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="b2852-119">See the following topics:</span></span> 

- [<span data-ttu-id="b2852-120">Completare i prerequisiti per la creazione di gruppi di disponibilità AlwaysOn in macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="b2852-120">Configure prerequisites for SQL Server Always On availability groups on Azure Virtual Machines</span></span>](virtual-machines-windows-portal-sql-availability-group-prereq.md)

- [<span data-ttu-id="b2852-121">Creare un gruppo di disponibilità AlwaysOn per migliorare la disponibilità e il ripristino di emergenza</span><span class="sxs-lookup"><span data-stu-id="b2852-121">Create Always On Availability Group to improve availability and disaster recovery</span></span>](virtual-machines-windows-portal-sql-availability-group-tutorial.md)

## <a name="next-steps"></a><span data-ttu-id="b2852-122">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b2852-122">Next steps</span></span>

<span data-ttu-id="b2852-123">[Configurare un gruppo di disponibilità SQL Server AlwaysOn in Macchine virtuali di Azure](virtual-machines-windows-portal-sql-availability-group-dr.md).</span><span class="sxs-lookup"><span data-stu-id="b2852-123">[Configure a SQL Server Always On Availability Group on Azure Virtual Machines in Different Regions](virtual-machines-windows-portal-sql-availability-group-dr.md).</span></span>
