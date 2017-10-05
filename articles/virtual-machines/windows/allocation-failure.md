---
title: Risolvere i problemi relativi a errori di allocazione delle VM Windows | Microsoft Docs
description: Risolvere i problemi relativi a errori di allocazione quando si crea, riavvia o ridimensiona una macchina virtuale Windows in Azure
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue,azure-resource-manager,azure-service-management
ms.assetid: bb939e23-77fc-4948-96f7-5037761c30e8
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: cjiang
ms.openlocfilehash: 57925b5a75fd8bcf2a9450025b5dc51eb552353f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-allocation-failures-when-you-create-restart-or-resize-windows-vms-in-azure"></a><span data-ttu-id="bd339-103">Risolvere i problemi relativi a errori di allocazione quando si crea, riavvia o ridimensiona una macchina virtuale Windows in Azure</span><span class="sxs-lookup"><span data-stu-id="bd339-103">Troubleshoot allocation failures when you create, restart, or resize Windows VMs in Azure</span></span>
<span data-ttu-id="bd339-104">Quando si crea una VM, si riavviano VM arrestate (deallocate) o si ridimensiona una VM, Microsoft Azure alloca risorse di calcolo alla sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="bd339-104">When you create a VM, restart stopped (deallocated) VMs, or resize a VM, Microsoft Azure allocates compute resources to your subscription.</span></span> <span data-ttu-id="bd339-105">In alcuni casi possono verificarsi errori quando si eseguono queste operazioni, anche prima di raggiungere i limiti della sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="bd339-105">You may occasionally receive errors when performing these operations -- even before you reach the Azure subscription limits.</span></span> <span data-ttu-id="bd339-106">Questo articolo illustra le cause di alcuni dei più comuni errori di allocazione e suggerisce una possibile correzione.</span><span class="sxs-lookup"><span data-stu-id="bd339-106">This article explains the causes of some of the common allocation failures and suggests possible remediation.</span></span> <span data-ttu-id="bd339-107">Queste informazioni potrebbero risultare utili anche quando si pianifica la distribuzione dei servizi.</span><span class="sxs-lookup"><span data-stu-id="bd339-107">The information may also be useful when you plan the deployment of your services.</span></span> <span data-ttu-id="bd339-108">È anche possibile [risolvere i problemi relativi agli errori di allocazione quando si crea, si riavvia o si ridimensiona una VM Linux in Azure](../linux/allocation-failure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bd339-108">You can also [troubleshoot allocation failures when you create, restart, or resize Linux VMs in Azure](../linux/allocation-failure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-allocation-failure](../../../includes/virtual-machines-common-allocation-failure.md)]

