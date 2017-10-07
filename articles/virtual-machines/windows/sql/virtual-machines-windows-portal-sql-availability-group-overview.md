---
title: "Panoramica di gruppi di disponibilità Server - macchine virtuali di Azure - aaaSQL | Documenti Microsoft"
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
ms.openlocfilehash: ecac8b8c5073021af2aa22a05490bb8c4c20ed17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-sql-server-always-on-availability-groups-on-azure-virtual-machines"></a><span data-ttu-id="bdd72-103">Panoramica sui gruppi di disponibilità AlwaysOn di SQL Server in macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="bdd72-103">Introducing SQL Server Always On availability groups on Azure virtual machines</span></span> #

<span data-ttu-id="bdd72-104">Questo articolo offre una panoramica sui gruppi di disponibilità di SQL Server in macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="bdd72-104">This article introduces SQL Server availability groups on Azure Virtual Machines.</span></span> 

<span data-ttu-id="bdd72-105">Sempre in gruppi di disponibilità nelle macchine virtuali Azure sono simili tooAlways gruppi di disponibilità in locale.</span><span class="sxs-lookup"><span data-stu-id="bdd72-105">Always On availability groups on Azure Virtual Machines are similar tooAlways On availability groups on premises.</span></span> <span data-ttu-id="bdd72-106">Per altre informazioni, vedere [Gruppi di disponibilità AlwaysOn (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx).</span><span class="sxs-lookup"><span data-stu-id="bdd72-106">For more information, see [Always On Availability Groups (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx).</span></span> 

<span data-ttu-id="bdd72-107">diagramma di Hello sono illustrate hello parti di un gruppo di disponibilità Server nelle macchine virtuali di Azure SQL completo.</span><span class="sxs-lookup"><span data-stu-id="bdd72-107">hello diagram illustrates hello parts of a complete SQL Server Availability Group in Azure Virtual Machines.</span></span>

![Gruppo di disponibilità](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

<span data-ttu-id="bdd72-109">Hello differenza fondamentale per un gruppo di disponibilità in macchine virtuali di Azure è che hello macchine virtuali di Azure, richiedono un [bilanciamento del carico](../../../load-balancer/load-balancer-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bdd72-109">hello key difference for an Availability Group in Azure Virtual Machines is that hello Azure virtual machines, require a [load balancer](../../../load-balancer/load-balancer-overview.md).</span></span> <span data-ttu-id="bdd72-110">servizio di bilanciamento del carico Hello contiene indirizzi IP hello per listener del gruppo di disponibilità hello.</span><span class="sxs-lookup"><span data-stu-id="bdd72-110">hello load balancer holds hello IP addresses for hello availability group listener.</span></span> <span data-ttu-id="bdd72-111">Se sono disponibili più gruppi di disponibilità, è necessario un listener per ogni gruppo.</span><span class="sxs-lookup"><span data-stu-id="bdd72-111">If you have more than one availability group each group requires a listener.</span></span> <span data-ttu-id="bdd72-112">Un servizio di bilanciamento del carico può supportare più listener.</span><span class="sxs-lookup"><span data-stu-id="bdd72-112">One load balancer can support multiple listeners.</span></span>

<span data-ttu-id="bdd72-113">Quando si è pronti toobuild un aroup di disponibilità di SQL Server in macchine virtuali di Azure, vedere le esercitazioni toothese.</span><span class="sxs-lookup"><span data-stu-id="bdd72-113">When you are ready toobuild a SQL Server availability aroup on Azure Virtual Machines, refer toothese tutorials.</span></span>

## <a name="automatically-create-an-availability-group-from-a-template"></a><span data-ttu-id="bdd72-114">Creare automaticamente un gruppo di disponibilità da un modello</span><span class="sxs-lookup"><span data-stu-id="bdd72-114">Automatically create an availability group from a template</span></span>

[<span data-ttu-id="bdd72-115">Configurare automaticamente il gruppo di disponibilità AlwaysOn in macchine virtuali di Azure con Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bdd72-115">Configure Always On availability group in Azure VM automatically - Resource Manager</span></span>](virtual-machines-windows-portal-sql-alwayson-availability-groups.md)

## <a name="manually-create-an-availability-group-in-azure-portal"></a><span data-ttu-id="bdd72-116">Creare manualmente un gruppo di disponibilità nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="bdd72-116">Manually create an availability group in Azure portal</span></span>

<span data-ttu-id="bdd72-117">È possibile inoltre creare macchine virtuali hello manualmente senza modello hello.</span><span class="sxs-lookup"><span data-stu-id="bdd72-117">You can also create hello virtual machines yourself without hello template.</span></span> <span data-ttu-id="bdd72-118">Innanzitutto, completare i prerequisiti di hello, quindi creare il gruppo di disponibilità hello.</span><span class="sxs-lookup"><span data-stu-id="bdd72-118">First, complete hello prerequisites, then create hello availability group.</span></span> <span data-ttu-id="bdd72-119">Vedere hello seguenti argomenti:</span><span class="sxs-lookup"><span data-stu-id="bdd72-119">See hello following topics:</span></span> 

- [<span data-ttu-id="bdd72-120">Completare i prerequisiti per la creazione di gruppi di disponibilità AlwaysOn in macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="bdd72-120">Configure prerequisites for SQL Server Always On availability groups on Azure Virtual Machines</span></span>](virtual-machines-windows-portal-sql-availability-group-prereq.md)

- [<span data-ttu-id="bdd72-121">Ripristino di emergenza e disponibilità tooimprove Crea gruppo di disponibilità AlwaysOn</span><span class="sxs-lookup"><span data-stu-id="bdd72-121">Create Always On Availability Group tooimprove availability and disaster recovery</span></span>](virtual-machines-windows-portal-sql-availability-group-tutorial.md)

## <a name="next-steps"></a><span data-ttu-id="bdd72-122">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bdd72-122">Next steps</span></span>

<span data-ttu-id="bdd72-123">[Configurare un gruppo di disponibilità SQL Server AlwaysOn in Macchine virtuali di Azure](virtual-machines-windows-portal-sql-availability-group-dr.md).</span><span class="sxs-lookup"><span data-stu-id="bdd72-123">[Configure a SQL Server Always On Availability Group on Azure Virtual Machines in Different Regions](virtual-machines-windows-portal-sql-availability-group-dr.md).</span></span>
