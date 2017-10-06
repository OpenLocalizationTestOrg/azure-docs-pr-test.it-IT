---
title: aaaSet degli endpoint in una macchina virtuale Windows classica | Documenti Microsoft
description: Informazioni tooset degli endpoint per una macchina virtuale Windows hello Azure tooallow portale classico comunicazione con una macchina virtuale Windows in Azure.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 8afc21c2-d3fb-43a3-acce-aa06be448bb6
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: cynthn
ms.openlocfilehash: e817076f16d3a245a8d19add7b2f2cf5e3baa17e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-endpoints-on-a-classic-windows-virtual-machine-in-azure"></a><span data-ttu-id="58af6-103">Come tooset degli endpoint in una macchina virtuale di Windows classica in Azure</span><span class="sxs-lookup"><span data-stu-id="58af6-103">How tooset up endpoints on a classic Windows virtual machine in Azure</span></span>
<span data-ttu-id="58af6-104">Tutte le finestre di macchine virtuali create in Azure utilizzando il modello di distribuzione classica hello possono comunicare automaticamente tramite un canale di rete privata con altre macchine virtuali in hello nello stesso servizio cloud o rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="58af6-104">All Windows virtual machines that you create in Azure using hello classic deployment model can automatically communicate over a private network channel with other virtual machines in hello same cloud service or virtual network.</span></span> <span data-ttu-id="58af6-105">Tuttavia, i computer su Internet hello o altre reti virtuali richiedono endpoint toodirect hello rete in ingresso traffico tooa computer macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="58af6-105">However, computers on hello Internet or other virtual networks require endpoints toodirect hello inbound network traffic tooa virtual machine.</span></span> <span data-ttu-id="58af6-106">Questo articolo è disponibile anche per le [macchine virtuali Linux](../../linux/classic/setup-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="58af6-106">This article is also available for [Linux virtual machines](../../linux/classic/setup-endpoints.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="58af6-107">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="58af6-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="58af6-108">In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="58af6-108">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="58af6-109">Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="58af6-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="58af6-110">In hello **Gestione risorse** modello di distribuzione, gli endpoint vengono configurati tramite **rete sicurezza gruppi**.</span><span class="sxs-lookup"><span data-stu-id="58af6-110">In hello **Resource Manager** deployment model, endpoints are configured using **Network Security Groups (NSGs)**.</span></span> <span data-ttu-id="58af6-111">Per ulteriori informazioni, vedere [Consenti accesso esterno tooyour VM utilizzando hello Azure portal](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="58af6-111">For more information, see [Allow external access tooyour VM using hello Azure portal](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="58af6-112">Quando si crea una macchina virtuale Windows in hello portale di Azure, gli endpoint comuni come quelli per Desktop remoto e comunicazione remota di Windows PowerShell sono in genere creati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="58af6-112">When you create a Windows virtual machine in hello Azure portal, common endpoints like those for Remote Desktop and Windows PowerShell Remoting are typically created for you automatically.</span></span> <span data-ttu-id="58af6-113">È possibile configurare altri endpoint durante la creazione della macchina virtuale hello o in un secondo momento all'occorrenza.</span><span class="sxs-lookup"><span data-stu-id="58af6-113">You can configure additional endpoints while creating hello virtual machine or afterwards as needed.</span></span>

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a><span data-ttu-id="58af6-114">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="58af6-114">Next steps</span></span>
* <span data-ttu-id="58af6-115">toouse un tooset cmdlet PowerShell di Azure di un endpoint di macchina virtuale, vedere [Add-AzureEndpoint](https://msdn.microsoft.com/library/azure/dn495300.aspx).</span><span class="sxs-lookup"><span data-stu-id="58af6-115">toouse an Azure PowerShell cmdlet tooset up a VM endpoint, see [Add-AzureEndpoint](https://msdn.microsoft.com/library/azure/dn495300.aspx).</span></span>
* <span data-ttu-id="58af6-116">toouse un toomanage cmdlet PowerShell di Azure un ACL su un endpoint, vedere [il controllo di accesso di gestione elenchi (ACL) per gli endpoint tramite PowerShell](../../../virtual-network/virtual-networks-acl-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="58af6-116">toouse an Azure PowerShell cmdlet toomanage an ACL on an endpoint, see [Managing access control lists (ACLs) for endpoints by using PowerShell](../../../virtual-network/virtual-networks-acl-powershell.md).</span></span>
* <span data-ttu-id="58af6-117">Se una macchina virtuale è stato creato nel modello di distribuzione di gestione risorse di hello, è possibile usare Azure PowerShell troppo[creare gruppi di sicurezza di rete](../../../virtual-network/virtual-networks-create-nsg-arm-ps.md) toocontrol traffico toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="58af6-117">If you created a virtual machine in hello Resource Manager deployment model, you can use Azure PowerShell too[create network security groups](../../../virtual-network/virtual-networks-create-nsg-arm-ps.md) toocontrol traffic toohello VM.</span></span>
