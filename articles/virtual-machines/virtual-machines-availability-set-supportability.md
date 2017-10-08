---
title: "aaaSupportability di aggiunta di set di disponibilità esistente tooan di macchine virtuali di Azure | Documenti Microsoft"
description: "Supporto di aggiunta di macchine virtuali di Azure tooan set di disponibilità esistente."
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
ms.openlocfilehash: dc2bd86b916f1d1a0a0d4c9e870df829434c96b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="supportability-of-adding-azure-vms-tooan-existing-availability-set"></a><span data-ttu-id="cc1be-103">Supporto di aggiunta di macchine virtuali di Azure tooan set di disponibilità esistente</span><span class="sxs-lookup"><span data-stu-id="cc1be-103">Supportability of adding Azure VMs tooan existing availability set</span></span>

<span data-ttu-id="cc1be-104">In alcuni casi, è possibile riscontrare limitazioni quando si aggiungono nuove macchine virtuali (VM) tooan set di disponibilità esistente.</span><span class="sxs-lookup"><span data-stu-id="cc1be-104">You may occasionally encounter limitations when you add new virtual machines (VMs) tooan existing availability set.</span></span> <span data-ttu-id="cc1be-105">Hello seguenti dettagli grafico le serie di macchina virtuale in cui è possibile combinare hello stesso set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="cc1be-105">hello following chart details which VM series you can mix in hello same availability set.</span></span>

<span data-ttu-id="cc1be-106">Ecco hello supportabilità matrice toomix diversi tipi di macchine virtuali:</span><span class="sxs-lookup"><span data-stu-id="cc1be-106">Here is hello supportability matrix toomix different types of VMs:</span></span>

<span data-ttu-id="cc1be-107">Serie e set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="cc1be-107">Series & Availability Set</span></span>|<span data-ttu-id="cc1be-108">Seconda macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="cc1be-108">Second VM</span></span>|<span data-ttu-id="cc1be-109">Una </span><span class="sxs-lookup"><span data-stu-id="cc1be-109">A</span></span>|<span data-ttu-id="cc1be-110">Av2</span><span class="sxs-lookup"><span data-stu-id="cc1be-110">Av2</span></span>|<span data-ttu-id="cc1be-111">D</span><span class="sxs-lookup"><span data-stu-id="cc1be-111">D</span></span>|<span data-ttu-id="cc1be-112">Dv2</span><span class="sxs-lookup"><span data-stu-id="cc1be-112">Dv2</span></span>|<span data-ttu-id="cc1be-113">Dv3</span><span class="sxs-lookup"><span data-stu-id="cc1be-113">Dv3</span></span>|
|---|---|---|---|---|---|---|
|<span data-ttu-id="cc1be-114">Prima macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="cc1be-114">First VM</span></span>|||||||
|<span data-ttu-id="cc1be-115">Una </span><span class="sxs-lookup"><span data-stu-id="cc1be-115">A</span></span>||<span data-ttu-id="cc1be-116">OK</span><span class="sxs-lookup"><span data-stu-id="cc1be-116">OK</span></span>|<span data-ttu-id="cc1be-117">OK</span><span class="sxs-lookup"><span data-stu-id="cc1be-117">OK</span></span>|<span data-ttu-id="cc1be-118">OK</span><span class="sxs-lookup"><span data-stu-id="cc1be-118">OK</span></span>|<span data-ttu-id="cc1be-119">OK</span><span class="sxs-lookup"><span data-stu-id="cc1be-119">OK</span></span>|<span data-ttu-id="cc1be-120">OK</span><span class="sxs-lookup"><span data-stu-id="cc1be-120">OK</span></span>|
|<span data-ttu-id="cc1be-121">Av2</span><span class="sxs-lookup"><span data-stu-id="cc1be-121">Av2</span></span>||<span data-ttu-id="cc1be-122">OK</span><span class="sxs-lookup"><span data-stu-id="cc1be-122">OK</span></span>|<span data-ttu-id="cc1be-123">OK</span><span class="sxs-lookup"><span data-stu-id="cc1be-123">OK</span></span>|<span data-ttu-id="cc1be-124">OK</span><span class="sxs-lookup"><span data-stu-id="cc1be-124">OK</span></span>|<span data-ttu-id="cc1be-125">OK</span><span class="sxs-lookup"><span data-stu-id="cc1be-125">OK</span></span>|<span data-ttu-id="cc1be-126">OK</span><span class="sxs-lookup"><span data-stu-id="cc1be-126">OK</span></span>|
|<span data-ttu-id="cc1be-127">D</span><span class="sxs-lookup"><span data-stu-id="cc1be-127">D</span></span>||<span data-ttu-id="cc1be-128">OK</span><span class="sxs-lookup"><span data-stu-id="cc1be-128">OK</span></span>|<span data-ttu-id="cc1be-129">OK</span><span class="sxs-lookup"><span data-stu-id="cc1be-129">OK</span></span>|<span data-ttu-id="cc1be-130">OK</span><span class="sxs-lookup"><span data-stu-id="cc1be-130">OK</span></span>|<span data-ttu-id="cc1be-131">OK</span><span class="sxs-lookup"><span data-stu-id="cc1be-131">OK</span></span>|<span data-ttu-id="cc1be-132">OK</span><span class="sxs-lookup"><span data-stu-id="cc1be-132">OK</span></span>|
|<span data-ttu-id="cc1be-133">Dv2</span><span class="sxs-lookup"><span data-stu-id="cc1be-133">Dv2</span></span>||<span data-ttu-id="cc1be-134">OK</span><span class="sxs-lookup"><span data-stu-id="cc1be-134">OK</span></span>|<span data-ttu-id="cc1be-135">OK</span><span class="sxs-lookup"><span data-stu-id="cc1be-135">OK</span></span>|<span data-ttu-id="cc1be-136">OK</span><span class="sxs-lookup"><span data-stu-id="cc1be-136">OK</span></span>|<span data-ttu-id="cc1be-137">OK</span><span class="sxs-lookup"><span data-stu-id="cc1be-137">OK</span></span>|<span data-ttu-id="cc1be-138">OK</span><span class="sxs-lookup"><span data-stu-id="cc1be-138">OK</span></span>|
|<span data-ttu-id="cc1be-139">Dv3</span><span class="sxs-lookup"><span data-stu-id="cc1be-139">Dv3</span></span>||<span data-ttu-id="cc1be-140">OK</span><span class="sxs-lookup"><span data-stu-id="cc1be-140">OK</span></span>|<span data-ttu-id="cc1be-141">OK</span><span class="sxs-lookup"><span data-stu-id="cc1be-141">OK</span></span>|<span data-ttu-id="cc1be-142">OK</span><span class="sxs-lookup"><span data-stu-id="cc1be-142">OK</span></span>|<span data-ttu-id="cc1be-143">OK</span><span class="sxs-lookup"><span data-stu-id="cc1be-143">OK</span></span>|<span data-ttu-id="cc1be-144">OK</span><span class="sxs-lookup"><span data-stu-id="cc1be-144">OK</span></span>|

<span data-ttu-id="cc1be-145">Tutte le altre serie non è stato in hello stesso disponibilità impostata perché richiedono un hardware specifico.</span><span class="sxs-lookup"><span data-stu-id="cc1be-145">All other series could not be in hello same availability set because they require a specific hardware.</span></span>
