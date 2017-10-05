---
title: Convalidare la rete virtuale di Azure da usare con Azure RemoteApp | Documentazione Microsoft
description: "Informazioni su come assicurarsi che la rete virtuale di Azure sia pronta all’utilizzo con Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: b573ba02-4587-4be5-9821-27bd891a73b2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 05c8a0ff04293947cec391b6467cc4adddb6a7b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="validate-the-azure-vnet-to-use-with-azure-remoteapp"></a><span data-ttu-id="20c44-103">Convalidare la rete virtuale di Azure da usare con Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="20c44-103">Validate the Azure VNET to use with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="20c44-104">Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017.</span><span class="sxs-lookup"><span data-stu-id="20c44-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="20c44-105">Per i dettagli, vedere l' [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="20c44-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="20c44-106">Prima di utilizzare una rete virtuale di Azure con Azure RemoteApp, è possibile convalidare la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="20c44-106">Before you use an Azure VNET with Azure RemoteApp, you might want to validate the VNET.</span></span> <span data-ttu-id="20c44-107">Consente di evitare problemi con la connettività.</span><span class="sxs-lookup"><span data-stu-id="20c44-107">This helps prevent issues with connectivity.</span></span>

<span data-ttu-id="20c44-108">Per convalidare la rete virtuale di Azure, procedere come segue:</span><span class="sxs-lookup"><span data-stu-id="20c44-108">To validate your Azure VNET, do the following:</span></span>

1. <span data-ttu-id="20c44-109">Creare una macchina virtuale di Azure all'interno della subnet della rete virtuale di Azure da usare con Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="20c44-109">Create an Azure virtual machine inside the subnet of the Azure VNET you want to use with Azure RemoteApp.</span></span>
2. <span data-ttu-id="20c44-110">Connettersi a tale macchina virtuale usando l’opzione **Connetti** nel portale di gestione.</span><span class="sxs-lookup"><span data-stu-id="20c44-110">Connect to that VM by using the **Connect** option in the management portal.</span></span>
3. <span data-ttu-id="20c44-111">Aggiungere la macchina virtuale allo stesso dominio che si desidera usare con Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="20c44-111">Join the virtual machine to the same domain that you want to use with Azure RemoteApp.</span></span> <span data-ttu-id="20c44-112">Se si sta creando una raccolta ibrida che si connette alla rete locale, aggiungere la macchina virtuale al dominio locale.</span><span class="sxs-lookup"><span data-stu-id="20c44-112">If you are creating a hybrid collection that connects to your on-premises network, join the virtual machine to your local domain.</span></span>

<span data-ttu-id="20c44-113">Se l'operazione viene completata, la rete virtuale di Azure è pronta per l'utilizzo con RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="20c44-113">If this is successful, the Azure VNET is ready to use with RemoteApp.</span></span>

<span data-ttu-id="20c44-114">Per ulteriori informazioni sul flusso di lavoro della raccolta ibrida end-to-end, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="20c44-114">For more information about the end-to-end hybrid collection workflow, see the following articles:</span></span>

* [<span data-ttu-id="20c44-115">Come pianificare la rete virtuale per RemoteApp di Azure</span><span class="sxs-lookup"><span data-stu-id="20c44-115">How to plan your virtual network for Azure RemoteApp</span></span>](remoteapp-planvnet.md)
* [<span data-ttu-id="20c44-116">Creare una raccolta ibrida</span><span class="sxs-lookup"><span data-stu-id="20c44-116">Create a hybrid collection</span></span>](remoteapp-create-hybrid-deployment.md)
* [<span data-ttu-id="20c44-117">Distribuire la raccolta di Azure RemoteApp alla rete virtuale di Azure (con supporto per ExpressRoute)</span><span class="sxs-lookup"><span data-stu-id="20c44-117">Deploy Azure RemoteApp collection to your Azure Virtual Network (with support for ExpressRoute)</span></span>](http://blogs.msdn.com/b/rds/archive/2015/04/23/deploy-azure-remoteapp-collection-to-your-azure-virtual-network-with-support-for-expressroute.aspx)

