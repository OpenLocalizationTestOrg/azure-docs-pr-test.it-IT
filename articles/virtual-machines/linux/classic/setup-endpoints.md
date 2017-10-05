---
title: Configurare gli endpoint in una VM Linux classica | Microsoft Docs
description: Informazioni su come configurare gli endpoint per una macchina virtuale Linux nel portale di Azure classico per consentire la comunicazione con una VM Linux in Azure
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
ms.openlocfilehash: 4fd8b847b0f60648d1661ce5a8667c641e616ed4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-set-up-endpoints-on-a-linux-classic-virtual-machine-in-azure"></a><span data-ttu-id="9c3d0-103">Come configurare gli endpoint in una macchina virtuale Linux classica in Azure</span><span class="sxs-lookup"><span data-stu-id="9c3d0-103">How to set up endpoints on a Linux classic virtual machine in Azure</span></span>
<span data-ttu-id="9c3d0-104">Tutte le macchine virtuali Linux create in Azure con il modello di distribuzione classico possono comunicare automaticamente mediante un canale di rete privato con altre macchine virtuali dello stesso servizio cloud o nella stessa rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="9c3d0-104">All Linux virtual machines that you create in Azure using the classic deployment model can automatically communicate over a private network channel with other virtual machines in the same cloud service or virtual network.</span></span> <span data-ttu-id="9c3d0-105">Tuttavia, i computer in Internet o altre reti virtuali richiedono gli endpoint per indirizzare il traffico di rete in ingresso a una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="9c3d0-105">However, computers on the Internet or other virtual networks require endpoints to direct the inbound network traffic to a virtual machine.</span></span> <span data-ttu-id="9c3d0-106">Questo articolo è disponibile anche per le [macchine virtuali Windows](../../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9c3d0-106">This article is also available for [Windows virtual machines](../../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9c3d0-107">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="9c3d0-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="9c3d0-108">Questo articolo illustra l'uso del modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="9c3d0-108">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="9c3d0-109">Microsoft consiglia di usare il modello di Gestione risorse per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="9c3d0-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="9c3d0-110">Nel modello di distribuzione **Resource Manager** gli endpoint vengono configurati tramite **Gruppi di sicurezza di rete**.</span><span class="sxs-lookup"><span data-stu-id="9c3d0-110">In the **Resource Manager** deployment model, endpoints are configured using **Network Security Groups (NSGs)**.</span></span> <span data-ttu-id="9c3d0-111">Per altre informazioni, vedere [Apertura di porte e di endpoint](../nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9c3d0-111">For more information, see [Opening ports and endpoints](../nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="9c3d0-112">Quando si crea una macchina virtuale Linux nel portale di Azure, viene in genere creato automaticamente un endpoint per Secure Shell (SSH).</span><span class="sxs-lookup"><span data-stu-id="9c3d0-112">When you create a Linux virtual machine in the Azure portal, an endpoint for Secure Shell (SSH) is typically created for you automatically.</span></span> <span data-ttu-id="9c3d0-113">È possibile configurare altri endpoint durante la creazione della macchina virtuale o successivamente all'occorrenza.</span><span class="sxs-lookup"><span data-stu-id="9c3d0-113">You can configure additional endpoints while creating the virtual machine or afterwards as needed.</span></span>

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a><span data-ttu-id="9c3d0-114">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9c3d0-114">Next steps</span></span>
* <span data-ttu-id="9c3d0-115">È anche possibile creare un endpoint di VM con l' [interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="9c3d0-115">You can also create a VM endpoint by using the [Azure Command-Line Interface](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span> <span data-ttu-id="9c3d0-116">Eseguire il comando **azure vm endpoint create** .</span><span class="sxs-lookup"><span data-stu-id="9c3d0-116">Run the **azure vm endpoint create** command.</span></span>
* <span data-ttu-id="9c3d0-117">Se una macchina virtuale è stata creata nel modello di distribuzione Resource Manager, è possibile usare l'interfaccia della riga di comando di Azure in modalità Resource Manager per [creare gruppi di sicurezza di rete](../../../virtual-network/virtual-networks-create-nsg-arm-cli.md) per controllare il traffico verso la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="9c3d0-117">If you created a virtual machine in the Resource Manager deployment model, you can use the Azure CLI in Resource Manager mode to [create network security groups](../../../virtual-network/virtual-networks-create-nsg-arm-cli.md) to control traffic to the VM.</span></span>
