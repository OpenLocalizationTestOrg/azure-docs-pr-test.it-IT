---
title: Configurare gli endpoint su una VM Windows classica | Microsoft Docs
description: Informazioni su come configurare gli endpoint per una macchina virtuale Windows nel portale di Azure classico per consentire la comunicazione con una macchina virtuale Windows in Azure.
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
ms.openlocfilehash: 60861819a7e437bb715b14c0e8eaf74f13b33ebf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-set-up-endpoints-on-a-classic-windows-virtual-machine-in-azure"></a><span data-ttu-id="bd9fe-103">Come configurare gli endpoint in una macchina virtuale Windows classica in Azure</span><span class="sxs-lookup"><span data-stu-id="bd9fe-103">How to set up endpoints on a classic Windows virtual machine in Azure</span></span>
<span data-ttu-id="bd9fe-104">Tutte le macchine virtuali Windows create in Azure con il modello di distribuzione classico possono comunicare automaticamente mediante un canale di rete privato con altre macchine virtuali dello stesso servizio cloud o nella stessa rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="bd9fe-104">All Windows virtual machines that you create in Azure using the classic deployment model can automatically communicate over a private network channel with other virtual machines in the same cloud service or virtual network.</span></span> <span data-ttu-id="bd9fe-105">Tuttavia, i computer in Internet o altre reti virtuali richiedono gli endpoint per indirizzare il traffico di rete in ingresso a una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="bd9fe-105">However, computers on the Internet or other virtual networks require endpoints to direct the inbound network traffic to a virtual machine.</span></span> <span data-ttu-id="bd9fe-106">Questo articolo è disponibile anche per le [macchine virtuali Linux](../../linux/classic/setup-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="bd9fe-106">This article is also available for [Linux virtual machines](../../linux/classic/setup-endpoints.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bd9fe-107">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="bd9fe-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="bd9fe-108">Questo articolo illustra l'uso del modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="bd9fe-108">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="bd9fe-109">Microsoft consiglia di usare il modello di Gestione risorse per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="bd9fe-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="bd9fe-110">Nel modello di distribuzione **Resource Manager** gli endpoint vengono configurati tramite **Gruppi di sicurezza di rete**.</span><span class="sxs-lookup"><span data-stu-id="bd9fe-110">In the **Resource Manager** deployment model, endpoints are configured using **Network Security Groups (NSGs)**.</span></span> <span data-ttu-id="bd9fe-111">Per altre informazioni, vedere [Consentire l'accesso esterno alla VM mediante il portale di Azure](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bd9fe-111">For more information, see [Allow external access to your VM using the Azure portal](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="bd9fe-112">Quando si crea una macchina virtuale Windows nel portale di Azure, gli endpoint comuni, ad esempio quelli di Desktop remoto e Comunicazione remota di Windows PowerShell, sono in genere creati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="bd9fe-112">When you create a Windows virtual machine in the Azure portal, common endpoints like those for Remote Desktop and Windows PowerShell Remoting are typically created for you automatically.</span></span> <span data-ttu-id="bd9fe-113">È possibile configurare altri endpoint durante la creazione della macchina virtuale o successivamente all'occorrenza.</span><span class="sxs-lookup"><span data-stu-id="bd9fe-113">You can configure additional endpoints while creating the virtual machine or afterwards as needed.</span></span>

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a><span data-ttu-id="bd9fe-114">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bd9fe-114">Next steps</span></span>
* <span data-ttu-id="bd9fe-115">Per usare un cmdlet di Azure PowerShell per impostare un endpoint di VM, vedere [Add-AzureEndpoint](https://msdn.microsoft.com/library/azure/dn495300.aspx).</span><span class="sxs-lookup"><span data-stu-id="bd9fe-115">To use an Azure PowerShell cmdlet to set up a VM endpoint, see [Add-AzureEndpoint](https://msdn.microsoft.com/library/azure/dn495300.aspx).</span></span>
* <span data-ttu-id="bd9fe-116">Per usare un cmdlet di Azure PowerShell per gestire un ACL in un endpoint, vedere [Come gestire gli elenchi di controllo di accesso per gli endpoint tramite PowerShell](../../../virtual-network/virtual-networks-acl-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="bd9fe-116">To use an Azure PowerShell cmdlet to manage an ACL on an endpoint, see [Managing access control lists (ACLs) for endpoints by using PowerShell](../../../virtual-network/virtual-networks-acl-powershell.md).</span></span>
* <span data-ttu-id="bd9fe-117">Se una macchina virtuale è stata creata nel modello di distribuzione Resource Manager, è possibile usare Azure PowerShell per [creare gruppi di sicurezza di rete](../../../virtual-network/virtual-networks-create-nsg-arm-ps.md) per controllare il traffico verso la VM.</span><span class="sxs-lookup"><span data-stu-id="bd9fe-117">If you created a virtual machine in the Resource Manager deployment model, you can use Azure PowerShell to [create network security groups](../../../virtual-network/virtual-networks-create-nsg-arm-ps.md) to control traffic to the VM.</span></span>
