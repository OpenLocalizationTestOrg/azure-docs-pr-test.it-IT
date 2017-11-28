---
title: VM Linux aaaTroubleshooting errori di allocazione | Documenti Microsoft
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
ms.openlocfilehash: 502fbb406b0b4acf086c2586795f69a44cc1a004
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-allocation-failures-when-you-create-restart-or-resize-linux-vms-in-azure"></a><span data-ttu-id="2e351-103">Risolvere i problemi relativi a errori di allocazione quando si crea, riavvia o ridimensiona una macchina virtuale Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="2e351-103">Troubleshoot allocation failures when you create, restart, or resize Linux VMs in Azure</span></span>
<span data-ttu-id="2e351-104">Quando si crea una macchina virtuale, riavviare le macchine virtuali (deallocate) arrestate o ridimensiona una macchina virtuale, Microsoft Azure alloca le risorse di calcolo tooyour sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="2e351-104">When you create a VM, restart stopped (deallocated) VMs, or resize a VM, Microsoft Azure allocates compute resources tooyour subscription.</span></span> <span data-ttu-id="2e351-105">In alcuni casi, possono verificarsi errori durante l'esecuzione di queste operazioni, anche prima di raggiungere i limiti di hello sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="2e351-105">You may occasionally receive errors when performing these operations -- even before you reach hello Azure subscription limits.</span></span> <span data-ttu-id="2e351-106">In questo articolo vengono illustrate le cause di alcune delle comuni errori di allocazione hello hello e suggerisce una possibile risoluzione.</span><span class="sxs-lookup"><span data-stu-id="2e351-106">This article explains hello causes of some of hello common allocation failures and suggests possible remediation.</span></span> <span data-ttu-id="2e351-107">informazioni di Hello potrebbero essere utile anche quando si pianifica la distribuzione hello dei servizi.</span><span class="sxs-lookup"><span data-stu-id="2e351-107">hello information may also be useful when you plan hello deployment of your services.</span></span> <span data-ttu-id="2e351-108">È anche possibile [risolvere i problemi relativi agli errori di allocazione quando si crea, si riavvia o si ridimensiona una VM Windows in Azure](../windows/allocation-failure.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2e351-108">You can also [troubleshoot allocation failures when you create, restart, or resize Windows VMs in Azure](../windows/allocation-failure.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-allocation-failure](../../../includes/virtual-machines-common-allocation-failure.md)]

