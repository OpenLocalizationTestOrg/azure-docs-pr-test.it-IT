---
title: Risolvere i problemi relativi a errori di allocazione delle VM Linux | Microsoft Docs
description: Risolvere i problemi relativi a errori di allocazione quando si crea, riavvia o ridimensiona una macchina virtuale Linux in Azure
services: virtual-machines-linux, azure-resource-manager
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue,azure-resourece-manager,azure-service-management
ms.assetid: 1ef41144-6dd6-4a56-b180-9d8b3d05eae7
ms.service: virtual-machines-linux
ms.workload: na
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2016
ms.author: cjiang
ms.openlocfilehash: c65ede134971c034006781e058c05a82ffb68a19
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-allocation-failures-when-you-create-restart-or-resize-linux-vms-in-azure"></a><span data-ttu-id="7abb9-103">Risolvere i problemi relativi a errori di allocazione quando si crea, riavvia o ridimensiona una macchina virtuale Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="7abb9-103">Troubleshoot allocation failures when you create, restart, or resize Linux VMs in Azure</span></span>
<span data-ttu-id="7abb9-104">Quando si crea una VM, si riavviano VM arrestate (deallocate) o si ridimensiona una VM, Microsoft Azure alloca risorse di calcolo alla sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="7abb9-104">When you create a VM, restart stopped (deallocated) VMs, or resize a VM, Microsoft Azure allocates compute resources to your subscription.</span></span> <span data-ttu-id="7abb9-105">In alcuni casi possono verificarsi errori quando si eseguono queste operazioni, anche prima di raggiungere i limiti della sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7abb9-105">You may occasionally receive errors when performing these operations -- even before you reach the Azure subscription limits.</span></span> <span data-ttu-id="7abb9-106">Questo articolo illustra le cause di alcuni dei più comuni errori di allocazione e suggerisce una possibile correzione.</span><span class="sxs-lookup"><span data-stu-id="7abb9-106">This article explains the causes of some of the common allocation failures and suggests possible remediation.</span></span> <span data-ttu-id="7abb9-107">Queste informazioni potrebbero risultare utili anche quando si pianifica la distribuzione dei servizi.</span><span class="sxs-lookup"><span data-stu-id="7abb9-107">The information may also be useful when you plan the deployment of your services.</span></span> <span data-ttu-id="7abb9-108">È anche possibile [risolvere i problemi relativi agli errori di allocazione quando si crea, si riavvia o si ridimensiona una VM Windows in Azure](../windows/allocation-failure.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7abb9-108">You can also [troubleshoot allocation failures when you create, restart, or resize Windows VMs in Azure](../windows/allocation-failure.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-allocation-failure](../../../includes/virtual-machines-common-allocation-failure.md)]

