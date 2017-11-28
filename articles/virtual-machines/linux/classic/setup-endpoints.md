---
title: aaaSet degli endpoint in una VM Linux classico | Documenti Microsoft
description: Informazioni su tooset degli endpoint per una VM Linux di hello Azure tooallow portale classico comunicazione con una macchina virtuale di Linux in Azure
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: f3749738-1109-4a1d-8635-40e4bd220e91
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: cynthn
ms.openlocfilehash: 1c959d10dd1e20228fa4a20e1cc0205c1d12f185
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-endpoints-on-a-linux-classic-virtual-machine-in-azure"></a><span data-ttu-id="25c59-103">Come tooset degli endpoint in una macchina virtuale di Linux classica in Azure</span><span class="sxs-lookup"><span data-stu-id="25c59-103">How tooset up endpoints on a Linux classic virtual machine in Azure</span></span>
<span data-ttu-id="25c59-104">Tutte le macchine virtuali Linux create in Azure utilizzando il modello di distribuzione classica hello possono comunicare automaticamente tramite un canale di rete privata con altre macchine virtuali in hello che stesso servizio o della rete virtuale del cloud.</span><span class="sxs-lookup"><span data-stu-id="25c59-104">All Linux virtual machines that you create in Azure using hello classic deployment model can automatically communicate over a private network channel with other virtual machines in hello same cloud service or virtual network.</span></span> <span data-ttu-id="25c59-105">Tuttavia, i computer su Internet hello o altre reti virtuali richiedono endpoint toodirect hello rete in ingresso traffico tooa computer macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="25c59-105">However, computers on hello Internet or other virtual networks require endpoints toodirect hello inbound network traffic tooa virtual machine.</span></span> <span data-ttu-id="25c59-106">Questo articolo è disponibile anche per le [macchine virtuali Windows](../../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="25c59-106">This article is also available for [Windows virtual machines](../../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="25c59-107">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="25c59-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="25c59-108">In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="25c59-108">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="25c59-109">Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="25c59-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="25c59-110">In hello **Gestione risorse** modello di distribuzione, gli endpoint vengono configurati tramite **rete sicurezza gruppi**.</span><span class="sxs-lookup"><span data-stu-id="25c59-110">In hello **Resource Manager** deployment model, endpoints are configured using **Network Security Groups (NSGs)**.</span></span> <span data-ttu-id="25c59-111">Per altre informazioni, vedere [Apertura di porte e di endpoint](../nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="25c59-111">For more information, see [Opening ports and endpoints](../nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="25c59-112">Quando si crea una macchina virtuale Linux nel portale di Azure hello, un endpoint per SSH (Secure Shell) è in genere creato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="25c59-112">When you create a Linux virtual machine in hello Azure portal, an endpoint for Secure Shell (SSH) is typically created for you automatically.</span></span> <span data-ttu-id="25c59-113">È possibile configurare altri endpoint durante la creazione della macchina virtuale hello o in un secondo momento all'occorrenza.</span><span class="sxs-lookup"><span data-stu-id="25c59-113">You can configure additional endpoints while creating hello virtual machine or afterwards as needed.</span></span>

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a><span data-ttu-id="25c59-114">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="25c59-114">Next steps</span></span>
* <span data-ttu-id="25c59-115">È anche possibile creare un endpoint della macchina virtuale utilizzando hello [interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="25c59-115">You can also create a VM endpoint by using hello [Azure Command-Line Interface](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span> <span data-ttu-id="25c59-116">Eseguire hello **creare endpoint di macchina virtuale di azure** comando.</span><span class="sxs-lookup"><span data-stu-id="25c59-116">Run hello **azure vm endpoint create** command.</span></span>
* <span data-ttu-id="25c59-117">Se una macchina virtuale è stato creato nel modello di distribuzione di gestione risorse di hello, è possibile utilizzare anche hello CLI di Azure in modalità di gestione risorse[creare gruppi di sicurezza di rete](../../../virtual-network/virtual-networks-create-nsg-arm-cli.md) toocontrol traffico toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="25c59-117">If you created a virtual machine in hello Resource Manager deployment model, you can use hello Azure CLI in Resource Manager mode too[create network security groups](../../../virtual-network/virtual-networks-create-nsg-arm-cli.md) toocontrol traffic toohello VM.</span></span>
