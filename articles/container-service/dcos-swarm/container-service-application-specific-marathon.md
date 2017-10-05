---
title: Servizio Marathon specifico per un'applicazione o un'utente | Documentazione Microsoft
description: Creare un servizio Marathon specifico per un'applicazione o un'utente
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Contenitori, Marathon, Micro-Service, controller di dominio/sistema operativo, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/12/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: b265763fb5dad240edd710cd8d0fb1079e3a7b51
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-application-or-user-specific-marathon-service"></a><span data-ttu-id="2b7ed-104">Creare un servizio Marathon specifico per un'applicazione o un'utente</span><span class="sxs-lookup"><span data-stu-id="2b7ed-104">Create an application or user-specific Marathon service</span></span>
<span data-ttu-id="2b7ed-105">Il servizio contenitore di Azure fornisce un set di server master in cui vengono preconfigurati Apache Mesos e Marathon.</span><span class="sxs-lookup"><span data-stu-id="2b7ed-105">Azure Container Service provides a set of master servers on which we preconfigure Apache Mesos and Marathon.</span></span> <span data-ttu-id="2b7ed-106">È possibile usarli per orchestrare le applicazioni nel cluster, ma è consigliabile non usare i server master a questo scopo.</span><span class="sxs-lookup"><span data-stu-id="2b7ed-106">These can be used to orchestrate your applications on the cluster, but it's best not to use the master servers for this purpose.</span></span> <span data-ttu-id="2b7ed-107">La modifica della configurazione di Marathon richiede ad esempio l'accesso ai server master stessi per apportare modifiche. Per questa operazione sono consigliabili server master univoci, che risultano leggermente diversi dai server standard e devono essere gestiti in modo specifico e indipendente.</span><span class="sxs-lookup"><span data-stu-id="2b7ed-107">For example, tweaking the configuration of Marathon requires logging into the master servers themselves and making changes--this encourages unique master servers that are a little different from the standard and need to be cared for and managed independently.</span></span> <span data-ttu-id="2b7ed-108">La configurazione necessaria per un team potrebbe non essere ottimale per un altro team.</span><span class="sxs-lookup"><span data-stu-id="2b7ed-108">Additionally, the configuration required by one team might not be the optimal configuration for another team.</span></span>

<span data-ttu-id="2b7ed-109">Questo articolo illustra come aggiungere un servizio Marathon specifico per un'applicazione o un'utente.</span><span class="sxs-lookup"><span data-stu-id="2b7ed-109">In this article, we'll explain how to add an application or user-specific Marathon service.</span></span>

<span data-ttu-id="2b7ed-110">Dato che il servizio apparterrà a un singolo utente o team, sarà possibile configurarlo in base alle esigenze specifiche dell'utente o del team.</span><span class="sxs-lookup"><span data-stu-id="2b7ed-110">Because this service will belong to a single user or team, they are free to configure it in any way that they desire.</span></span> <span data-ttu-id="2b7ed-111">Il servizio contenitore di Azure assicurerà la continuazione dell'esecuzione del servizio.</span><span class="sxs-lookup"><span data-stu-id="2b7ed-111">Also, Azure Container Service will ensure that the service continues to run.</span></span> <span data-ttu-id="2b7ed-112">In caso di errore, il servizio verrà riavviato dal servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="2b7ed-112">If the service fails, Azure Container Service will restart it for you.</span></span> <span data-ttu-id="2b7ed-113">Nella maggior parte dei casi il tempo di inattività non verrà percepito dall'utente.</span><span class="sxs-lookup"><span data-stu-id="2b7ed-113">Most of the time you won't even notice it had downtime.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2b7ed-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2b7ed-114">Prerequisites</span></span>
<span data-ttu-id="2b7ed-115">[Distribuire un'istanza del servizio contenitore di Azure](container-service-deployment.md) con un agente di orchestrazione di tipo DC/OS e [assicurarsi che il client possa connettersi al cluster](../container-service-connect.md).</span><span class="sxs-lookup"><span data-stu-id="2b7ed-115">[Deploy an instance of Azure Container Service](container-service-deployment.md) with orchestrator type DC/OS and  [ensure that your client can connect to your cluster](../container-service-connect.md).</span></span> <span data-ttu-id="2b7ed-116">Seguire anche questa procedura.</span><span class="sxs-lookup"><span data-stu-id="2b7ed-116">Also, do the following steps.</span></span>

[!INCLUDE [install the DC/OS CLI](../../../includes/container-service-install-dcos-cli-include.md)]

## <a name="create-an-application-or-user-specific-marathon-service"></a><span data-ttu-id="2b7ed-117">Creare un servizio Marathon specifico per un'applicazione o un'utente</span><span class="sxs-lookup"><span data-stu-id="2b7ed-117">Create an application or user-specific Marathon service</span></span>
<span data-ttu-id="2b7ed-118">Creare prima di tutto un file di configurazione JSON che definisce il nome del servizio dell'applicazione da creare.</span><span class="sxs-lookup"><span data-stu-id="2b7ed-118">Begin by creating a JSON configuration file that defines the name of the application service that you want to create.</span></span> <span data-ttu-id="2b7ed-119">In questo caso viene usato `marathon-alice` come nome del framework.</span><span class="sxs-lookup"><span data-stu-id="2b7ed-119">Here we use `marathon-alice` as the framework name.</span></span> <span data-ttu-id="2b7ed-120">Salvare il file con un nome analogo a `marathon-alice.json`:</span><span class="sxs-lookup"><span data-stu-id="2b7ed-120">Save the file as something like `marathon-alice.json`:</span></span>

```json
{"marathon": {"framework-name": "marathon-alice" }}
```

<span data-ttu-id="2b7ed-121">Usare quindi l'interfaccia della riga di comando del controller di dominio/sistema operativo per installare l'istanza di Marathon con le opzioni impostate nel file di configurazione:</span><span class="sxs-lookup"><span data-stu-id="2b7ed-121">Next, use the DC/OS CLI to install the Marathon instance with the options that are set in your configuration file:</span></span>

```bash
dcos package install --options=marathon-alice.json marathon
```

<span data-ttu-id="2b7ed-122">Dovrebbe essere visualizzato il servizio `marathon-alice` in esecuzione nella scheda dei servizi dell'interfaccia della riga di comando del controller di dominio/sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="2b7ed-122">You should now see your `marathon-alice` service running in the Services tab of your DC/OS UI.</span></span> <span data-ttu-id="2b7ed-123">L'interfaccia utente sarà `http://<hostname>/service/marathon-alice/` , se si vuole accedere direttamente.</span><span class="sxs-lookup"><span data-stu-id="2b7ed-123">The UI will be `http://<hostname>/service/marathon-alice/` if you want to access it directly.</span></span>

## <a name="set-the-dcos-cli-to-access-the-service"></a><span data-ttu-id="2b7ed-124">Impostare l'interfaccia della riga di comando di DC/OS per accedere al servizio</span><span class="sxs-lookup"><span data-stu-id="2b7ed-124">Set the DC/OS CLI to access the service</span></span>
<span data-ttu-id="2b7ed-125">Facoltativamente è possibile configurare l'interfaccia della riga di comando del controller di dominio/sistema operativo per accedere a questo nuovo servizio. A tale scopo, impostare la proprietà `marathon.url` in modo che punti all'istanza `marathon-alice`, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="2b7ed-125">You can optionally configure your DC/OS CLI to access this new service by setting the `marathon.url` property to point to the `marathon-alice` instance as follows:</span></span>

```bash
dcos config set marathon.url http://<hostname>/service/marathon-alice/
```

<span data-ttu-id="2b7ed-126">Per verificare quale istanza di Marathon stia usando l'interfaccia della riga di comando, è possibile usare il comando `dcos config show` .</span><span class="sxs-lookup"><span data-stu-id="2b7ed-126">You can verify which instance of Marathon that your CLI is working against with the `dcos config show` command.</span></span> <span data-ttu-id="2b7ed-127">Per ripristinare l'uso del servizio Marathon master, è possibile usare il comando `dcos config unset marathon.url`.</span><span class="sxs-lookup"><span data-stu-id="2b7ed-127">You can revert to using your master Marathon service with the command `dcos config unset marathon.url`.</span></span>

