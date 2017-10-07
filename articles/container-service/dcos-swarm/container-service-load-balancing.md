---
title: contenitori di saldo aaaLoad nel cluster di controller di dominio o sistema operativo di Azure | Documenti Microsoft
description: "Bilanciare il carico tra più contenitori in un cluster DC/OS del servizio contenitore di Azure."
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Contenitori, Micro-Service, controller di dominio/sistema operativo, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 2249cb06880cdb7e9a3aa94c0750c6a27316d349
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-containers-in-an-azure-container-service-dcos-cluster"></a><span data-ttu-id="013f0-104">Bilanciare il carico dei contenitori in un cluster DC/OS del servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="013f0-104">Load balance containers in an Azure Container Service DC/OS cluster</span></span>
<span data-ttu-id="013f0-105">In questo articolo esamineremo come il servizio di contenitore di Azure utilizzando maratona LB gestito toocreate un bilanciamento del carico interno in un controller di dominio o sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="013f0-105">In this article, we explore how toocreate an internal load balancer in a DC/OS managed Azure Container Service using Marathon-LB.</span></span> <span data-ttu-id="013f0-106">Questa configurazione consente di tooscale le applicazioni in senso orizzontale.</span><span class="sxs-lookup"><span data-stu-id="013f0-106">This configuration enables you tooscale your applications horizontally.</span></span> <span data-ttu-id="013f0-107">Consente inoltre tootake sfruttare cluster agente pubbliche e private hello inserendo i servizi di bilanciamento del carico sul cluster pubblica hello e i contenitori di applicazioni in cluster privata hello.</span><span class="sxs-lookup"><span data-stu-id="013f0-107">It also allows you tootake advantage of hello public and private agent clusters by placing your load balancers on hello public cluster and your application containers on hello private cluster.</span></span> <span data-ttu-id="013f0-108">In questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="013f0-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="013f0-109">Configurare un servizio di bilanciamento del carico Marathon</span><span class="sxs-lookup"><span data-stu-id="013f0-109">Configure a Marathon Load Balancer</span></span>
> * <span data-ttu-id="013f0-110">Distribuire un'applicazione con bilanciamento del carico hello</span><span class="sxs-lookup"><span data-stu-id="013f0-110">Deploy an application using hello load balancer</span></span>
> * <span data-ttu-id="013f0-111">Configurare Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="013f0-111">Configure and Azure load balancer</span></span>

<span data-ttu-id="013f0-112">È necessario un ACS controller di dominio o sistema operativo hello toocomplete cluster i passaggi in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="013f0-112">You need an ACS DC/OS cluster toocomplete hello steps in this tutorial.</span></span> <span data-ttu-id="013f0-113">Se necessario, questo [script di esempio](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) può crearne uno appositamente.</span><span class="sxs-lookup"><span data-stu-id="013f0-113">If needed, [this script sample](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) can create one for you.</span></span>

<span data-ttu-id="013f0-114">Questa esercitazione richiede hello Azure CLI versione 2.0.4 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="013f0-114">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="013f0-115">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="013f0-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="013f0-116">Se è necessario tooupgrade, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="013f0-116">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="load-balancing-overview"></a><span data-ttu-id="013f0-117">Panoramica del bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="013f0-117">Load balancing overview</span></span>

<span data-ttu-id="013f0-118">In un cluster DC/OS del servizio contenitore di Azure esistono due livelli di bilanciamento del carico:</span><span class="sxs-lookup"><span data-stu-id="013f0-118">There are two load-balancing layers in an Azure Container Service DC/OS cluster:</span></span> 

<span data-ttu-id="013f0-119">**Il bilanciamento del carico Azure** fornisce punti di ingresso pubblico (quelli che gli utenti finali accesso Buongiorno).</span><span class="sxs-lookup"><span data-stu-id="013f0-119">**Azure Load Balancer** provides public entry points (hello ones that end users access).</span></span> <span data-ttu-id="013f0-120">Un LB Azure viene fornito automaticamente dal servizio di contenitore di Azure ed è, per impostazione predefinita, tooexpose configurata la porta 80, 443 e 8080.</span><span class="sxs-lookup"><span data-stu-id="013f0-120">An Azure LB is provided automatically by Azure Container Service and is, by default, configured tooexpose port 80, 443 and 8080.</span></span>

<span data-ttu-id="013f0-121">**servizio di bilanciamento del carico maratona (maratona lb) Hello** route in ingresso istanze toocontainer le richieste che queste richieste.</span><span class="sxs-lookup"><span data-stu-id="013f0-121">**hello Marathon Load Balancer (marathon-lb)** routes inbound requests toocontainer instances that service these requests.</span></span> <span data-ttu-id="013f0-122">Come si scala contenitori hello che fornisce il servizio web, si adatta dinamicamente hello maratona kg.</span><span class="sxs-lookup"><span data-stu-id="013f0-122">As we scale hello containers providing our web service, hello marathon-lb dynamically adapts.</span></span> <span data-ttu-id="013f0-123">Impostazione predefinita nel servizio contenitore non è disponibile il bilanciamento del carico, ma è facile tooinstall.</span><span class="sxs-lookup"><span data-stu-id="013f0-123">This load balancer is not provided by default in your Container Service, but it is easy tooinstall.</span></span>

## <a name="configure-marathon-load-balancer"></a><span data-ttu-id="013f0-124">Configurare il servizio di bilanciamento del carico Marathon</span><span class="sxs-lookup"><span data-stu-id="013f0-124">Configure Marathon Load Balancer</span></span>

<span data-ttu-id="013f0-125">Servizio di bilanciamento del carico maratona dinamicamente riconfigura basato sui contenitori di hello che sono stati distribuiti.</span><span class="sxs-lookup"><span data-stu-id="013f0-125">Marathon Load Balancer dynamically reconfigures itself based on hello containers that you've deployed.</span></span> <span data-ttu-id="013f0-126">È inoltre toohello resilienti perdita di un contenitore o un agente - se questo errore si verifica, Mesos Apache riavvia altrove contenitore hello e maratona lb adatta.</span><span class="sxs-lookup"><span data-stu-id="013f0-126">It's also resilient toohello loss of a container or an agent - if this occurs, Apache Mesos restarts hello container elsewhere and marathon-lb adapts.</span></span>

<span data-ttu-id="013f0-127">Eseguire hello successivo comando tooinstall hello maratona bilanciamento del carico nel cluster dell'agente di hello pubblico.</span><span class="sxs-lookup"><span data-stu-id="013f0-127">Run hello following command tooinstall hello marathon load balancer on hello public agent's cluster.</span></span>

```azurecli-interactive
dcos package install marathon-lb
```

## <a name="deploy-load-balanced-application"></a><span data-ttu-id="013f0-128">Distribuire un'applicazione con bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="013f0-128">Deploy load balanced application</span></span>

<span data-ttu-id="013f0-129">Ora che abbiamo pacchetto maratona lb hello, è possibile distribuire un contenitore di applicazione che si desidera bilanciare tooload.</span><span class="sxs-lookup"><span data-stu-id="013f0-129">Now that we have hello marathon-lb package, we can deploy an application container that we wish tooload balance.</span></span> 

<span data-ttu-id="013f0-130">Innanzitutto, ottenere hello FQDN di agenti hello esposto pubblicamente.</span><span class="sxs-lookup"><span data-stu-id="013f0-130">First, get hello FQDN of hello publicly exposed agents.</span></span>

```azurecli-interactive
az acs list --resource-group myResourceGroup --query "[0].agentPoolProfiles[0].fqdn" --output tsv
```

<span data-ttu-id="013f0-131">Successivamente, creare un file denominato *hello web.json* e copia in hello seguendo contenuto.</span><span class="sxs-lookup"><span data-stu-id="013f0-131">Next, create a file named *hello-web.json* and copy in hello following contents.</span></span> <span data-ttu-id="013f0-132">Hello `HAPROXY_0_VHOST` etichetta deve toobe aggiornato con FQDN di agenti di controller di dominio/OS hello hello.</span><span class="sxs-lookup"><span data-stu-id="013f0-132">hello `HAPROXY_0_VHOST` label needs toobe updated with hello FQDN of hello DC/OS agents.</span></span> 

```json
{
  "id": "web",
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "yeasy/simple-web",
      "network": "BRIDGE",
      "portMappings": [
        { "hostPort": 0, "containerPort": 80, "servicePort": 10000 }
      ],
      "forcePullImage":true
    }
  },
  "instances": 3,
  "cpus": 0.1,
  "mem": 65,
  "healthChecks": [{
      "protocol": "HTTP",
      "path": "/",
      "portIndex": 0,
      "timeoutSeconds": 10,
      "gracePeriodSeconds": 10,
      "intervalSeconds": 2,
      "maxConsecutiveFailures": 10
  }],
  "labels":{
    "HAPROXY_GROUP":"external",
    "HAPROXY_0_VHOST":"YOUR FQDN",
    "HAPROXY_0_MODE":"http"
  }
}
```

<span data-ttu-id="013f0-133">Utilizzare un'applicazione hello toorun hello CLI di controller di dominio o del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="013f0-133">Use hello DC/OS CLI toorun hello application.</span></span> <span data-ttu-id="013f0-134">Per impostazione predefinita maratona distribuisce hello hello applicazione toohello privata del cluster.</span><span class="sxs-lookup"><span data-stu-id="013f0-134">By default Marathon deploys hello hello applicaton toohello private cluster.</span></span> <span data-ttu-id="013f0-135">Ciò significa che hello di sopra di distribuzione è accessibile solo tramite il servizio di bilanciamento del carico, che corrisponde in genere il comportamento di hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="013f0-135">This means that hello above deployment is only accessible via your load balancer, which is usually hello desired behavior.</span></span>

```azurecli-interactive
dcos marathon app add hello-web.json
```

<span data-ttu-id="013f0-136">Dopo la distribuzione di un'applicazione hello, esplorare toohello FQDN di un'applicazione hello agente cluster tooview con carico bilanciato.</span><span class="sxs-lookup"><span data-stu-id="013f0-136">Once hello application has been deployed, browse toohello FQDN of hello agent cluster tooview load balanced application.</span></span>

![Immagine dell'applicazione con bilanciamento del carico](./media/container-service-load-balancing/lb-app.png)

## <a name="configure-azure-load-balancer"></a><span data-ttu-id="013f0-138">Configurare Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="013f0-138">Configure Azure Load Balancer</span></span>

<span data-ttu-id="013f0-139">Per impostazione predefinita, Azure Load Balancer espone le porte 80, 8080 e 443.</span><span class="sxs-lookup"><span data-stu-id="013f0-139">By default, Azure Load Balancer exposes ports 80, 8080, and 443.</span></span> <span data-ttu-id="013f0-140">Se si utilizza uno di questi tre porte (come in hello esempio precedente), quindi non c'è niente che occorre toodo.</span><span class="sxs-lookup"><span data-stu-id="013f0-140">If you're using one of these three ports (as we do in hello above example), then there is nothing you need toodo.</span></span> <span data-ttu-id="013f0-141">Dovrebbe essere in grado di toohit FQDN del servizio di bilanciamento di carico dell'agente e ogni volta che si aggiorna, si verificherà uno dei server web di tre in uno schema round-robin.</span><span class="sxs-lookup"><span data-stu-id="013f0-141">You should be able toohit your agent load balancer's FQDN, and each time you refresh, you'll hit one of your three web servers in a round-robin fashion.</span></span> 

<span data-ttu-id="013f0-142">Se si utilizza una porta diversa, è necessario un round-robin tooadd regola e un probe di bilanciamento del carico hello per porta hello usata.</span><span class="sxs-lookup"><span data-stu-id="013f0-142">If you use a different port, you need tooadd a round-robin rule and a probe on hello load balancer for hello port that you used.</span></span> <span data-ttu-id="013f0-143">È possibile farlo da hello [CLI di Azure](../../azure-resource-manager/xplat-cli-azure-resource-manager.md), con i comandi di hello `azure network lb rule create` e `azure network lb probe create`.</span><span class="sxs-lookup"><span data-stu-id="013f0-143">You can do this from hello [Azure CLI](../../azure-resource-manager/xplat-cli-azure-resource-manager.md), with hello commands `azure network lb rule create` and `azure network lb probe create`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="013f0-144">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="013f0-144">Next steps</span></span>

<span data-ttu-id="013f0-145">In questa esercitazione, illustrando il bilanciamento del carico in ACS con hello maratona e carico di Azure tra cui bilanciamento hello seguenti azioni:</span><span class="sxs-lookup"><span data-stu-id="013f0-145">In this tutorial, you learned about load balancing in ACS with both hello Marathon and Azure load balancers including hello following actions:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="013f0-146">Configurare un servizio di bilanciamento del carico Marathon</span><span class="sxs-lookup"><span data-stu-id="013f0-146">Configure a Marathon Load Balancer</span></span>
> * <span data-ttu-id="013f0-147">Distribuire un'applicazione con bilanciamento del carico hello</span><span class="sxs-lookup"><span data-stu-id="013f0-147">Deploy an application using hello load balancer</span></span>
> * <span data-ttu-id="013f0-148">Configurare Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="013f0-148">Configure and Azure load balancer</span></span>

<span data-ttu-id="013f0-149">Spostare toohello Avanti toolearn esercitazione sull'integrazione di archiviazione di Azure con controller di dominio o del sistema operativo in Azure.</span><span class="sxs-lookup"><span data-stu-id="013f0-149">Advance toohello next tutorial toolearn about integrating Azure storage with DC/OS in Azure.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="013f0-150">Montare una condivisione file di Azure nel cluster DC/OS</span><span class="sxs-lookup"><span data-stu-id="013f0-150">Mount Azure File Share in DC/OS cluster</span></span>](container-service-dcos-fileshare.md)