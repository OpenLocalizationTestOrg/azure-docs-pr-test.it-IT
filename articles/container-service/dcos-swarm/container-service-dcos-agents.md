---
title: Pool di agenti DC/OS per il servizio contenitore di Azure | Documentazione Microsoft
description: Informazioni sul funzionamento dei pool di agenti pubblici e privati con un cluster DC/OS del servizio contenitore di Azure
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
ms.openlocfilehash: da4a196b1a73c78dfff7d8310edcc349b8d10665
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="dcos-agent-pools-for-azure-container-service"></a><span data-ttu-id="d1518-104">Pool di agenti DC/OS per il servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="d1518-104">DC/OS agent pools for Azure Container Service</span></span>
<span data-ttu-id="d1518-105">I cluster DC/OS nel servizio contenitore di Azure contengono nodi di agenti in due pool, uno pubblico e uno privato.</span><span class="sxs-lookup"><span data-stu-id="d1518-105">DC/OS clusters in Azure Container Service contain agent nodes in two pools, a public pool and a private pool.</span></span> <span data-ttu-id="d1518-106">Un'applicazione può essere distribuita indifferentemente in uno dei due pool, ma ciò influisce sull'accessibilità tra i computer nel servizio contenitore.</span><span class="sxs-lookup"><span data-stu-id="d1518-106">An application can be deployed to either pool, affecting accessibility between machines in your container service.</span></span> <span data-ttu-id="d1518-107">I computer possono essere esposti a Internet (pubblico) o rimanere interni (privato).</span><span class="sxs-lookup"><span data-stu-id="d1518-107">The machines can be exposed to the internet (public) or kept internal (private).</span></span> <span data-ttu-id="d1518-108">Questo articolo descrive brevemente il motivo per cui esistono i pool pubblici e i pool privati.</span><span class="sxs-lookup"><span data-stu-id="d1518-108">This article gives a brief overview of why there are public and private pools.</span></span>


* <span data-ttu-id="d1518-109">**Agenti privati**: i nodi di agenti privati vengono eseguiti tramite una rete non instradabile,</span><span class="sxs-lookup"><span data-stu-id="d1518-109">**Private agents**: Private agent nodes run through a non-routable network.</span></span> <span data-ttu-id="d1518-110">accessibile unicamente dalla zona di amministrazione o attraverso il router perimetrale della zona pubblica.</span><span class="sxs-lookup"><span data-stu-id="d1518-110">This network is only accessible from the admin zone or through the public zone edge router.</span></span> <span data-ttu-id="d1518-111">Per impostazione predefinita, il DC/OS avvia le applicazioni in nodi di agenti privati.</span><span class="sxs-lookup"><span data-stu-id="d1518-111">By default, DC/OS launches apps on private agent nodes.</span></span> 

* <span data-ttu-id="d1518-112">**Agenti pubblici**: i nodi di agenti pubblici eseguono app e servizi DC/OS attraverso una rete accessibile pubblicamente.</span><span class="sxs-lookup"><span data-stu-id="d1518-112">**Public agents**: Public agent nodes run DC/OS apps and services through a publicly accessible network.</span></span> 

<span data-ttu-id="d1518-113">Per altre informazioni sulla sicurezza della rete DC/OS, vedere la [documentazione di DC/OS](https://dcos.io/docs/1.7/administration/securing-your-cluster/).</span><span class="sxs-lookup"><span data-stu-id="d1518-113">For more information about DC/OS network security, see the [DC/OS documentation](https://dcos.io/docs/1.7/administration/securing-your-cluster/).</span></span>

## <a name="deploy-agent-pools"></a><span data-ttu-id="d1518-114">Distribuire pool di agenti</span><span class="sxs-lookup"><span data-stu-id="d1518-114">Deploy agent pools</span></span>

<span data-ttu-id="d1518-115">I pool di agenti DC/OS del servizio contenitore di Azure vengono creati come segue:</span><span class="sxs-lookup"><span data-stu-id="d1518-115">The DC/OS agent pools In Azure Container Service are created as follows:</span></span>

* <span data-ttu-id="d1518-116">Il **pool privato** contiene il numero di nodi di agenti che si specifica quando si [distribuisce il cluster DC/OS](container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="d1518-116">The **private pool** contains the number of agent nodes that you specify when you [deploy the DC/OS cluster](container-service-deployment.md).</span></span> 

* <span data-ttu-id="d1518-117">Il **pool pubblico** contiene inizialmente un numero predeterminato di nodi di agenti.</span><span class="sxs-lookup"><span data-stu-id="d1518-117">The **public pool** initially contains a predetermined number of agent nodes.</span></span> <span data-ttu-id="d1518-118">Questo pool viene aggiunto automaticamente quando viene eseguito il provisioning del cluster DC/OS.</span><span class="sxs-lookup"><span data-stu-id="d1518-118">This pool is added automatically when the DC/OS cluster is provisioned.</span></span>

<span data-ttu-id="d1518-119">I pool pubblico e privato sono set di scalabilità di macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="d1518-119">The private pool and the public pool are Azure virtual machine scale sets.</span></span> <span data-ttu-id="d1518-120">È possibile ridimensionare questi pool dopo la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="d1518-120">You can resize these pools after deployment.</span></span>

## <a name="use-agent-pools"></a><span data-ttu-id="d1518-121">Uso dei pool di agenti</span><span class="sxs-lookup"><span data-stu-id="d1518-121">Use agent pools</span></span>
<span data-ttu-id="d1518-122">Per impostazione predefinita, **Marathon** distribuisce le nuove applicazioni in nodi di agenti *privati* .</span><span class="sxs-lookup"><span data-stu-id="d1518-122">By default, **Marathon** deploys any new application to the *private* agent nodes.</span></span> <span data-ttu-id="d1518-123">Per distribuire l'applicazione nei nodi *pubblici*, è necessario farlo in modo esplicito mentre la si crea.</span><span class="sxs-lookup"><span data-stu-id="d1518-123">You have to explicitly deploy the application to the *public* nodes during the creation of the application.</span></span> <span data-ttu-id="d1518-124">Selezionare la scheda **Optional** (Facoltativo) e immettere **slave_public** come valore di **Accepted Resource Roles** (Ruoli risorsa accettati).</span><span class="sxs-lookup"><span data-stu-id="d1518-124">Select the **Optional** tab and enter **slave_public** for the **Accepted Resource Roles** value.</span></span> <span data-ttu-id="d1518-125">Questo processo è documentato [qui](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) e nella documentazione di [DC\OS](https://dcos.io/docs/1.7/administration/installing/custom/create-public-agent/).</span><span class="sxs-lookup"><span data-stu-id="d1518-125">This process is documented [here](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) and in the [DC/OS](https://dcos.io/docs/1.7/administration/installing/custom/create-public-agent/) documentation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d1518-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d1518-126">Next steps</span></span>
* <span data-ttu-id="d1518-127">Sono disponibili altre informazioni sulla [gestione dei contenitori DC/OS](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="d1518-127">Read more about [managing your DC/OS containers](container-service-mesos-marathon-ui.md).</span></span>

* <span data-ttu-id="d1518-128">Informazioni su come [aprire il firewall](container-service-enable-public-access.md) fornito da Azure per consentire l'accesso pubblico ai contenitori DC/OS.</span><span class="sxs-lookup"><span data-stu-id="d1518-128">Learn how to [open the firewall](container-service-enable-public-access.md) provided by Azure to allow public access to your DC/OS containers.</span></span>

