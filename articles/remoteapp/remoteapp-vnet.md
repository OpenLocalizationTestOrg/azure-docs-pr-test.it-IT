---
title: aaaValidate hello rete virtuale di Azure toouse con Azure RemoteApp | Documenti Microsoft
description: "Informazioni su come toomake assicurarsi che la rete virtuale di Azure è pronta toouse con Azure RemoteApp"
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
ms.openlocfilehash: 5587556c264356e6ab6039b983a38cb2b95ed268
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="validate-hello-azure-vnet-toouse-with-azure-remoteapp"></a><span data-ttu-id="558d6-103">Convalidare hello toouse di rete virtuale di Azure con Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="558d6-103">Validate hello Azure VNET toouse with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="558d6-104">Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017.</span><span class="sxs-lookup"><span data-stu-id="558d6-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="558d6-105">Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="558d6-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="558d6-106">Prima di utilizzare una rete virtuale di Azure con Azure RemoteApp, è possibile toovalidate hello rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="558d6-106">Before you use an Azure VNET with Azure RemoteApp, you might want toovalidate hello VNET.</span></span> <span data-ttu-id="558d6-107">Consente di evitare problemi con la connettività.</span><span class="sxs-lookup"><span data-stu-id="558d6-107">This helps prevent issues with connectivity.</span></span>

<span data-ttu-id="558d6-108">toovalidate rete virtuale di Azure, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="558d6-108">toovalidate your Azure VNET, do hello following:</span></span>

1. <span data-ttu-id="558d6-109">Creare una macchina virtuale di Azure all'interno di hello subnet della rete virtuale di Azure, si desidera toouse con Azure RemoteApp hello.</span><span class="sxs-lookup"><span data-stu-id="558d6-109">Create an Azure virtual machine inside hello subnet of hello Azure VNET you want toouse with Azure RemoteApp.</span></span>
2. <span data-ttu-id="558d6-110">Connettersi con hello toothat VM **Connetti** opzione nel portale di gestione di hello.</span><span class="sxs-lookup"><span data-stu-id="558d6-110">Connect toothat VM by using hello **Connect** option in hello management portal.</span></span>
3. <span data-ttu-id="558d6-111">Join hello macchina virtuale toohello stesso dominio in cui si desidera toouse con Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="558d6-111">Join hello virtual machine toohello same domain that you want toouse with Azure RemoteApp.</span></span> <span data-ttu-id="558d6-112">Se si sta creando una raccolta ibrida che si connette rete locale tooyour, dominio locale tooyour join hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="558d6-112">If you are creating a hybrid collection that connects tooyour on-premises network, join hello virtual machine tooyour local domain.</span></span>

<span data-ttu-id="558d6-113">Se ha esito positivo, hello rete virtuale di Azure è pronta toouse con RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="558d6-113">If this is successful, hello Azure VNET is ready toouse with RemoteApp.</span></span>

<span data-ttu-id="558d6-114">Per ulteriori informazioni sul flusso di lavoro Raccolta hello ibrida end-to-end, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="558d6-114">For more information about hello end-to-end hybrid collection workflow, see hello following articles:</span></span>

* [<span data-ttu-id="558d6-115">Come tooplan la rete virtuale di Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="558d6-115">How tooplan your virtual network for Azure RemoteApp</span></span>](remoteapp-planvnet.md)
* [<span data-ttu-id="558d6-116">Creare una raccolta ibrida</span><span class="sxs-lookup"><span data-stu-id="558d6-116">Create a hybrid collection</span></span>](remoteapp-create-hybrid-deployment.md)
* [<span data-ttu-id="558d6-117">Distribuire Azure RemoteApp raccolta tooyour rete virtuale di Azure (con supporto per ExpressRoute)</span><span class="sxs-lookup"><span data-stu-id="558d6-117">Deploy Azure RemoteApp collection tooyour Azure Virtual Network (with support for ExpressRoute)</span></span>](http://blogs.msdn.com/b/rds/archive/2015/04/23/deploy-azure-remoteapp-collection-to-your-azure-virtual-network-with-support-for-expressroute.aspx)

