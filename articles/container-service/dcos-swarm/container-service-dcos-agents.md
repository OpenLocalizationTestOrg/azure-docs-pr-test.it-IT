---
title: pool di agenti aaaDC/del sistema operativo per il servizio contenitore di Azure | Documenti Microsoft
description: Funzionamento dei pool di agenti pubbliche e private di hello con un cluster di Azure contenitore del servizio controller di dominio o del sistema operativo
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, Contenitori, Micro-servizi, Mesos, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: c7d3889db07cb9908e8b68b668bd8a14ef3c2552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="dcos-agent-pools-for-azure-container-service"></a><span data-ttu-id="2baea-104">Pool di agenti DC/OS per il servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="2baea-104">DC/OS agent pools for Azure Container Service</span></span>
<span data-ttu-id="2baea-105">I cluster DC/OS nel servizio contenitore di Azure contengono nodi di agenti in due pool, uno pubblico e uno privato.</span><span class="sxs-lookup"><span data-stu-id="2baea-105">DC/OS clusters in Azure Container Service contain agent nodes in two pools, a public pool and a private pool.</span></span> <span data-ttu-id="2baea-106">Un'applicazione può essere distribuita tooeither pool, avere effetto sull'accessibilità tra i computer nel servizio contenitore.</span><span class="sxs-lookup"><span data-stu-id="2baea-106">An application can be deployed tooeither pool, affecting accessibility between machines in your container service.</span></span> <span data-ttu-id="2baea-107">Hello macchine possono essere esposto toohello internet (pubblica) o interno (privato).</span><span class="sxs-lookup"><span data-stu-id="2baea-107">hello machines can be exposed toohello internet (public) or kept internal (private).</span></span> <span data-ttu-id="2baea-108">Questo articolo descrive brevemente il motivo per cui esistono i pool pubblici e i pool privati.</span><span class="sxs-lookup"><span data-stu-id="2baea-108">This article gives a brief overview of why there are public and private pools.</span></span>


* <span data-ttu-id="2baea-109">**Agenti privati**: i nodi di agenti privati vengono eseguiti tramite una rete non instradabile,</span><span class="sxs-lookup"><span data-stu-id="2baea-109">**Private agents**: Private agent nodes run through a non-routable network.</span></span> <span data-ttu-id="2baea-110">Questa rete è accessibile solo dall'area di amministrazione di hello o tramite router perimetrale di hello zona pubblico.</span><span class="sxs-lookup"><span data-stu-id="2baea-110">This network is only accessible from hello admin zone or through hello public zone edge router.</span></span> <span data-ttu-id="2baea-111">Per impostazione predefinita, il DC/OS avvia le applicazioni in nodi di agenti privati.</span><span class="sxs-lookup"><span data-stu-id="2baea-111">By default, DC/OS launches apps on private agent nodes.</span></span> 

* <span data-ttu-id="2baea-112">**Agenti pubblici**: i nodi di agenti pubblici eseguono app e servizi DC/OS attraverso una rete accessibile pubblicamente.</span><span class="sxs-lookup"><span data-stu-id="2baea-112">**Public agents**: Public agent nodes run DC/OS apps and services through a publicly accessible network.</span></span> 

<span data-ttu-id="2baea-113">Per ulteriori informazioni sulla sicurezza di rete di controller di dominio o del sistema operativo, vedere hello [documentazione DC/OS](https://dcos.io/docs/1.7/administration/securing-your-cluster/).</span><span class="sxs-lookup"><span data-stu-id="2baea-113">For more information about DC/OS network security, see hello [DC/OS documentation](https://dcos.io/docs/1.7/administration/securing-your-cluster/).</span></span>

## <a name="deploy-agent-pools"></a><span data-ttu-id="2baea-114">Distribuire pool di agenti</span><span class="sxs-lookup"><span data-stu-id="2baea-114">Deploy agent pools</span></span>

<span data-ttu-id="2baea-115">pool di agenti Hello controller di dominio o del sistema operativo del servizio di contenitore di Azure vengono creati come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="2baea-115">hello DC/OS agent pools In Azure Container Service are created as follows:</span></span>

* <span data-ttu-id="2baea-116">Hello **pool privata** contiene il numero di hello di nodi di agente che si specifica quando si [distribuire cluster di controller di dominio/OS hello](container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="2baea-116">hello **private pool** contains hello number of agent nodes that you specify when you [deploy hello DC/OS cluster](container-service-deployment.md).</span></span> 

* <span data-ttu-id="2baea-117">Hello **pool pubblica** inizialmente contiene un numero predeterminato di nodi dell'agente.</span><span class="sxs-lookup"><span data-stu-id="2baea-117">hello **public pool** initially contains a predetermined number of agent nodes.</span></span> <span data-ttu-id="2baea-118">Il pool viene aggiunto automaticamente quando viene eseguito il provisioning di cluster di controller di dominio/OS hello.</span><span class="sxs-lookup"><span data-stu-id="2baea-118">This pool is added automatically when hello DC/OS cluster is provisioned.</span></span>

<span data-ttu-id="2baea-119">pool privata Hello e pool pubblica hello sono set di scalabilità di macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="2baea-119">hello private pool and hello public pool are Azure virtual machine scale sets.</span></span> <span data-ttu-id="2baea-120">È possibile ridimensionare questi pool dopo la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="2baea-120">You can resize these pools after deployment.</span></span>

## <a name="use-agent-pools"></a><span data-ttu-id="2baea-121">Uso dei pool di agenti</span><span class="sxs-lookup"><span data-stu-id="2baea-121">Use agent pools</span></span>
<span data-ttu-id="2baea-122">Per impostazione predefinita, **maratona** consente di distribuire qualsiasi nuova toohello applicazione *privata* nodi agente.</span><span class="sxs-lookup"><span data-stu-id="2baea-122">By default, **Marathon** deploys any new application toohello *private* agent nodes.</span></span> <span data-ttu-id="2baea-123">Si dispone di tooexplicitly distribuire toohello applicazione hello *pubblica* nodi durante la creazione di un'applicazione hello hello.</span><span class="sxs-lookup"><span data-stu-id="2baea-123">You have tooexplicitly deploy hello application toohello *public* nodes during hello creation of hello application.</span></span> <span data-ttu-id="2baea-124">Seleziona hello **facoltativo** scheda e immettere **slave_public** per hello **accettato ruoli risorse** valore.</span><span class="sxs-lookup"><span data-stu-id="2baea-124">Select hello **Optional** tab and enter **slave_public** for hello **Accepted Resource Roles** value.</span></span> <span data-ttu-id="2baea-125">Questo processo è documentato [qui](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) e hello [DC/OS](https://dcos.io/docs/1.7/administration/installing/custom/create-public-agent/) documentazione.</span><span class="sxs-lookup"><span data-stu-id="2baea-125">This process is documented [here](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) and in hello [DC/OS](https://dcos.io/docs/1.7/administration/installing/custom/create-public-agent/) documentation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2baea-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2baea-126">Next steps</span></span>
* <span data-ttu-id="2baea-127">Sono disponibili altre informazioni sulla [gestione dei contenitori DC/OS](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="2baea-127">Read more about [managing your DC/OS containers](container-service-mesos-marathon-ui.md).</span></span>

* <span data-ttu-id="2baea-128">Informazioni su come troppo[aprire hello firewall](container-service-enable-public-access.md) fornito dai contenitori di Azure tooallow accesso pubblico tooyour controller di dominio o del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="2baea-128">Learn how too[open hello firewall](container-service-enable-public-access.md) provided by Azure tooallow public access tooyour DC/OS containers.</span></span>

