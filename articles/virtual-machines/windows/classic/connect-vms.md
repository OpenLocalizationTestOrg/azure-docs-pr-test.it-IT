---
title: Connettere le macchine virtuali Windows in un servizio cloud | Microsoft Docs
description: Connettere le macchine virtuali Windows create con il modello di distribuzione classica a un servizio cloud di Azure o a una rete virtuale.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: c1cbc802-4352-4d2e-9e49-4ccbd955324b
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: cynthn
ms.openlocfilehash: 0c7a21461e5bb111c4359df8e949d48382b591c1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="connect-windows-virtual-machines-created-with-the-classic-deployment-model-with-a-virtual-network-or-cloud-service"></a><span data-ttu-id="6503e-103">Connettere le macchine virtuali Windows create con il modello di distribuzione classica con un servizio cloud o rete virtuale</span><span class="sxs-lookup"><span data-stu-id="6503e-103">Connect Windows virtual machines created with the classic deployment model with a virtual network or cloud service</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6503e-104">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="6503e-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="6503e-105">Questo articolo illustra l'uso del modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="6503e-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="6503e-106">Microsoft consiglia di usare il modello di Gestione risorse per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="6503e-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="6503e-107">Le macchine virtuali Windows create con il modello di distribuzione classica vengono sempre inserite in un servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="6503e-107">Windows virtual machines created with the classic deployment model are always placed in a cloud service.</span></span> <span data-ttu-id="6503e-108">Il servizio cloud funge da contenitore e fornisce un nome DNS pubblico univoco, un indirizzo IP pubblico e un set di endpoint per accedere alla macchina virtuale su Internet.</span><span class="sxs-lookup"><span data-stu-id="6503e-108">The cloud service acts as a container and provides a unique public DNS name, a public IP address, and a set of endpoints to access the virtual machine over the Internet.</span></span> <span data-ttu-id="6503e-109">Il servizio cloud può essere in una rete virtuale, ma questo non è un requisito.</span><span class="sxs-lookup"><span data-stu-id="6503e-109">The cloud service can be in a virtual network, but that's not a requirement.</span></span> <span data-ttu-id="6503e-110">È inoltre possibile [connettere le macchine virtuali Linux con una rete virtuale o un servizio cloud](../../linux/classic/connect-vms.md).</span><span class="sxs-lookup"><span data-stu-id="6503e-110">You can also [connect Linux virtual machines with a virtual network or cloud service](../../linux/classic/connect-vms.md).</span></span>

<span data-ttu-id="6503e-111">Se un servizio cloud non si trova in una rete virtuale, è detto servizio cloud *autonomo* .</span><span class="sxs-lookup"><span data-stu-id="6503e-111">If a cloud service isn't in a virtual network, it's called a *standalone* cloud service.</span></span> <span data-ttu-id="6503e-112">Le macchine virtuali in un servizio cloud autonomo comunicano con altre macchine virtuali usando i nomi DNS pubblici delle altre macchine virtuali e il traffico viene trasmesso attraverso Internet.</span><span class="sxs-lookup"><span data-stu-id="6503e-112">The virtual machines in a standalone cloud service communicate with other virtual machines by using the other virtual machines’ public DNS names, and the traffic travels over the Internet.</span></span> <span data-ttu-id="6503e-113">Se un servizio cloud si trova in una rete virtuale, le macchine virtuali in tale servizio cloud possono comunicare con tutte le altre macchine virtuali nella rete virtuale senza inviare traffico su Internet.</span><span class="sxs-lookup"><span data-stu-id="6503e-113">If a cloud service is in a virtual network, the virtual machines in that cloud service can communicate with all other virtual machines in the virtual network without sending any traffic over the Internet.</span></span>

<span data-ttu-id="6503e-114">Se si inseriscono le macchine virtuali nello stesso servizio cloud autonomo, si potranno continuare a usare il bilanciamento del carico e i set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="6503e-114">If you place your virtual machines in the same standalone cloud service, you can still use load balancing and availability sets.</span></span> <span data-ttu-id="6503e-115">Per altre informazioni, vedere gli articoli relativi a [bilanciamento del carico delle macchine virtuali](../../virtual-machines-windows-load-balance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) e [gestione della disponibilità delle macchine virtuali](../../virtual-machines-windows-manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6503e-115">For details, see [Load balancing virtual machines](../../virtual-machines-windows-load-balance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Manage the availability of virtual machines](../../virtual-machines-windows-manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="6503e-116">Tuttavia, non è possibile organizzare le macchine virtuali nelle subnet o connettere un servizio cloud autonomo alla rete locale.</span><span class="sxs-lookup"><span data-stu-id="6503e-116">However, you can't organize the virtual machines on subnets or connect a standalone cloud service to your on-premises network.</span></span> <span data-ttu-id="6503e-117">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="6503e-117">Here's an example:</span></span>

[!INCLUDE [virtual-machines-common-classic-connect-vms](../../../../includes/virtual-machines-common-classic-connect-vms.md)]

## <a name="next-steps"></a><span data-ttu-id="6503e-118">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6503e-118">Next steps</span></span>
<span data-ttu-id="6503e-119">Dopo avere creato una macchina virtuale, è consigliabile [aggiungere un disco dati](attach-disk.md) , in modo che i servizi e i carichi di lavoro possano usarlo per archiviare i dati.</span><span class="sxs-lookup"><span data-stu-id="6503e-119">After you create a virtual machine, it's a good idea to [add a data disk](attach-disk.md) so your services and workloads have a location to store data.</span></span>
