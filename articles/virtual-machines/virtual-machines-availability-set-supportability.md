---
title: "Supporto dell'aggiunta di macchine virtuali di Azure a un set di disponibilità esistente | Microsoft Docs"
description: "Supporto dell'aggiunta di macchine virtuali di Azure a un set di disponibilità esistente."
services: virtual-machines-linux
documentationcenter: 
author: Deland-Han
manager: cshepard
editor: 
ms.assetid: 
ms.service: virtual-machines
ms.workload: virtual-machines
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/15/2017
ms.author: delhan
ms.openlocfilehash: 3ce9b8a79108cb9e57df14bcb3354cc637193233
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/29/2017
---
# <a name="supportability-of-adding-azure-vms-to-an-existing-availability-set"></a><span data-ttu-id="a71b0-103">Supporto dell'aggiunta di macchine virtuali di Azure a un set di disponibilità esistente</span><span class="sxs-lookup"><span data-stu-id="a71b0-103">Supportability of adding Azure VMs to an existing availability set</span></span>

<span data-ttu-id="a71b0-104">È possibile riscontrare occasionalmente limitazioni quando si aggiungono nuove macchine virtuali (VM) in un set di disponibilità esistente.</span><span class="sxs-lookup"><span data-stu-id="a71b0-104">You may occasionally encounter limitations when you add new virtual machines (VMs) to an existing availability set.</span></span> <span data-ttu-id="a71b0-105">Il grafico seguente illustra in dettaglio quali serie di macchine virtuali è possibile combinare nello stesso set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="a71b0-105">The following chart details which VM series you can mix in the same availability set.</span></span>

<span data-ttu-id="a71b0-106">Di seguito si riporta la matrice di supporto per combinare diversi tipi di macchine virtuali:</span><span class="sxs-lookup"><span data-stu-id="a71b0-106">Here is the supportability matrix to mix different types of VMs:</span></span>

<span data-ttu-id="a71b0-107">Serie e set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="a71b0-107">Series & Availability Set</span></span>|<span data-ttu-id="a71b0-108">Seconda macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="a71b0-108">Second VM</span></span>|<span data-ttu-id="a71b0-109">Una </span><span class="sxs-lookup"><span data-stu-id="a71b0-109">A</span></span>|<span data-ttu-id="a71b0-110">Av2</span><span class="sxs-lookup"><span data-stu-id="a71b0-110">Av2</span></span>|<span data-ttu-id="a71b0-111">D</span><span class="sxs-lookup"><span data-stu-id="a71b0-111">D</span></span>|<span data-ttu-id="a71b0-112">Dv2</span><span class="sxs-lookup"><span data-stu-id="a71b0-112">Dv2</span></span>|<span data-ttu-id="a71b0-113">Dv3</span><span class="sxs-lookup"><span data-stu-id="a71b0-113">Dv3</span></span>|
|---|---|---|---|---|---|---|
|<span data-ttu-id="a71b0-114">Prima macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="a71b0-114">First VM</span></span>|||||||
|<span data-ttu-id="a71b0-115">Una </span><span class="sxs-lookup"><span data-stu-id="a71b0-115">A</span></span>||<span data-ttu-id="a71b0-116">OK</span><span class="sxs-lookup"><span data-stu-id="a71b0-116">OK</span></span>|<span data-ttu-id="a71b0-117">OK</span><span class="sxs-lookup"><span data-stu-id="a71b0-117">OK</span></span>|<span data-ttu-id="a71b0-118">OK</span><span class="sxs-lookup"><span data-stu-id="a71b0-118">OK</span></span>|<span data-ttu-id="a71b0-119">OK</span><span class="sxs-lookup"><span data-stu-id="a71b0-119">OK</span></span>|<span data-ttu-id="a71b0-120">OK</span><span class="sxs-lookup"><span data-stu-id="a71b0-120">OK</span></span>|
|<span data-ttu-id="a71b0-121">Av2</span><span class="sxs-lookup"><span data-stu-id="a71b0-121">Av2</span></span>||<span data-ttu-id="a71b0-122">OK</span><span class="sxs-lookup"><span data-stu-id="a71b0-122">OK</span></span>|<span data-ttu-id="a71b0-123">OK</span><span class="sxs-lookup"><span data-stu-id="a71b0-123">OK</span></span>|<span data-ttu-id="a71b0-124">OK</span><span class="sxs-lookup"><span data-stu-id="a71b0-124">OK</span></span>|<span data-ttu-id="a71b0-125">OK</span><span class="sxs-lookup"><span data-stu-id="a71b0-125">OK</span></span>|<span data-ttu-id="a71b0-126">OK</span><span class="sxs-lookup"><span data-stu-id="a71b0-126">OK</span></span>|
|<span data-ttu-id="a71b0-127">D</span><span class="sxs-lookup"><span data-stu-id="a71b0-127">D</span></span>||<span data-ttu-id="a71b0-128">OK</span><span class="sxs-lookup"><span data-stu-id="a71b0-128">OK</span></span>|<span data-ttu-id="a71b0-129">OK</span><span class="sxs-lookup"><span data-stu-id="a71b0-129">OK</span></span>|<span data-ttu-id="a71b0-130">OK</span><span class="sxs-lookup"><span data-stu-id="a71b0-130">OK</span></span>|<span data-ttu-id="a71b0-131">OK</span><span class="sxs-lookup"><span data-stu-id="a71b0-131">OK</span></span>|<span data-ttu-id="a71b0-132">OK</span><span class="sxs-lookup"><span data-stu-id="a71b0-132">OK</span></span>|
|<span data-ttu-id="a71b0-133">Dv2</span><span class="sxs-lookup"><span data-stu-id="a71b0-133">Dv2</span></span>||<span data-ttu-id="a71b0-134">OK</span><span class="sxs-lookup"><span data-stu-id="a71b0-134">OK</span></span>|<span data-ttu-id="a71b0-135">OK</span><span class="sxs-lookup"><span data-stu-id="a71b0-135">OK</span></span>|<span data-ttu-id="a71b0-136">OK</span><span class="sxs-lookup"><span data-stu-id="a71b0-136">OK</span></span>|<span data-ttu-id="a71b0-137">OK</span><span class="sxs-lookup"><span data-stu-id="a71b0-137">OK</span></span>|<span data-ttu-id="a71b0-138">OK</span><span class="sxs-lookup"><span data-stu-id="a71b0-138">OK</span></span>|
|<span data-ttu-id="a71b0-139">Dv3</span><span class="sxs-lookup"><span data-stu-id="a71b0-139">Dv3</span></span>||<span data-ttu-id="a71b0-140">OK</span><span class="sxs-lookup"><span data-stu-id="a71b0-140">OK</span></span>|<span data-ttu-id="a71b0-141">OK</span><span class="sxs-lookup"><span data-stu-id="a71b0-141">OK</span></span>|<span data-ttu-id="a71b0-142">OK</span><span class="sxs-lookup"><span data-stu-id="a71b0-142">OK</span></span>|<span data-ttu-id="a71b0-143">OK</span><span class="sxs-lookup"><span data-stu-id="a71b0-143">OK</span></span>|<span data-ttu-id="a71b0-144">OK</span><span class="sxs-lookup"><span data-stu-id="a71b0-144">OK</span></span>|

<span data-ttu-id="a71b0-145">Tutte le altre serie potrebbero non trovarsi nello stesso set di disponibilità perché richiedono un hardware specifico.</span><span class="sxs-lookup"><span data-stu-id="a71b0-145">All other series could not be in the same availability set because they require a specific hardware.</span></span>