---
title: errori di allocazione macchina virtuale Windows aaaTroubleshooting | Documenti Microsoft
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
ms.openlocfilehash: d0cc75ac60d952d8e4310cebc37654dc4f80857f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-allocation-failures-when-you-create-restart-or-resize-windows-vms-in-azure"></a><span data-ttu-id="af8d0-103">Risolvere i problemi relativi a errori di allocazione quando si crea, riavvia o ridimensiona una macchina virtuale Windows in Azure</span><span class="sxs-lookup"><span data-stu-id="af8d0-103">Troubleshoot allocation failures when you create, restart, or resize Windows VMs in Azure</span></span>
<span data-ttu-id="af8d0-104">Quando si crea una macchina virtuale, riavviare le macchine virtuali (deallocate) arrestate o ridimensiona una macchina virtuale, Microsoft Azure alloca le risorse di calcolo tooyour sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="af8d0-104">When you create a VM, restart stopped (deallocated) VMs, or resize a VM, Microsoft Azure allocates compute resources tooyour subscription.</span></span> <span data-ttu-id="af8d0-105">In alcuni casi, possono verificarsi errori durante l'esecuzione di queste operazioni, anche prima di raggiungere i limiti di hello sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="af8d0-105">You may occasionally receive errors when performing these operations -- even before you reach hello Azure subscription limits.</span></span> <span data-ttu-id="af8d0-106">In questo articolo vengono illustrate le cause di alcune delle comuni errori di allocazione hello hello e suggerisce una possibile risoluzione.</span><span class="sxs-lookup"><span data-stu-id="af8d0-106">This article explains hello causes of some of hello common allocation failures and suggests possible remediation.</span></span> <span data-ttu-id="af8d0-107">informazioni di Hello potrebbero essere utile anche quando si pianifica la distribuzione hello dei servizi.</span><span class="sxs-lookup"><span data-stu-id="af8d0-107">hello information may also be useful when you plan hello deployment of your services.</span></span> <span data-ttu-id="af8d0-108">È anche possibile [risolvere i problemi relativi agli errori di allocazione quando si crea, si riavvia o si ridimensiona una VM Linux in Azure](../linux/allocation-failure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="af8d0-108">You can also [troubleshoot allocation failures when you create, restart, or resize Linux VMs in Azure](../linux/allocation-failure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-allocation-failure](../../../includes/virtual-machines-common-allocation-failure.md)]

