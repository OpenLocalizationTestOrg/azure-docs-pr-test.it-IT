---
title: aaaApplication o servizio maratona specifiche dell'utente | Documenti Microsoft
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
ms.openlocfilehash: 1e6f69ed64e113a3a059788a71ddb57b6d3ad8da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-or-user-specific-marathon-service"></a><span data-ttu-id="f0f21-104">Creare un servizio Marathon specifico per un'applicazione o un'utente</span><span class="sxs-lookup"><span data-stu-id="f0f21-104">Create an application or user-specific Marathon service</span></span>
<span data-ttu-id="f0f21-105">Il servizio contenitore di Azure fornisce un set di server master in cui vengono preconfigurati Apache Mesos e Marathon.</span><span class="sxs-lookup"><span data-stu-id="f0f21-105">Azure Container Service provides a set of master servers on which we preconfigure Apache Mesos and Marathon.</span></span> <span data-ttu-id="f0f21-106">Possono essere utilizzati tooorchestrate le applicazioni in cluster hello, ma ottimale non toouse hello server master a questo scopo.</span><span class="sxs-lookup"><span data-stu-id="f0f21-106">These can be used tooorchestrate your applications on hello cluster, but it's best not toouse hello master servers for this purpose.</span></span> <span data-ttu-id="f0f21-107">Ad esempio, modifiche di configurazione hello di maratona richiede accesso al server master di hello stessi e per apportare modifiche, questa incoraggia univoco server master che sono leggermente diversi hello standard e toobe necessità di e gestito in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="f0f21-107">For example, tweaking hello configuration of Marathon requires logging into hello master servers themselves and making changes--this encourages unique master servers that are a little different from hello standard and need toobe cared for and managed independently.</span></span> <span data-ttu-id="f0f21-108">Inoltre, configurazione hello richiesto da un team potrebbe non essere ottimale hello per un altro team.</span><span class="sxs-lookup"><span data-stu-id="f0f21-108">Additionally, hello configuration required by one team might not be hello optimal configuration for another team.</span></span>

<span data-ttu-id="f0f21-109">In questo articolo verrà illustrato come tooadd un servizio maratona specifico dell'utente o applicazione.</span><span class="sxs-lookup"><span data-stu-id="f0f21-109">In this article, we'll explain how tooadd an application or user-specific Marathon service.</span></span>

<span data-ttu-id="f0f21-110">Poiché questo servizio apparterrà tooa singolo utente o del team, sono tooconfigure disponibile in alcun modo che lo desiderano.</span><span class="sxs-lookup"><span data-stu-id="f0f21-110">Because this service will belong tooa single user or team, they are free tooconfigure it in any way that they desire.</span></span> <span data-ttu-id="f0f21-111">Inoltre, il servizio contenitore di Azure verrà garantire il funzionamento di un servizio hello toorun.</span><span class="sxs-lookup"><span data-stu-id="f0f21-111">Also, Azure Container Service will ensure that hello service continues toorun.</span></span> <span data-ttu-id="f0f21-112">Se il servizio di hello non riesce, il servizio contenitore di Azure verrà viene riavviato.</span><span class="sxs-lookup"><span data-stu-id="f0f21-112">If hello service fails, Azure Container Service will restart it for you.</span></span> <span data-ttu-id="f0f21-113">La maggior parte del tempo di hello non anche noterai che aveva i tempi di inattività.</span><span class="sxs-lookup"><span data-stu-id="f0f21-113">Most of hello time you won't even notice it had downtime.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f0f21-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f0f21-114">Prerequisites</span></span>
<span data-ttu-id="f0f21-115">[Distribuire un'istanza del servizio di contenitore di Azure di](container-service-deployment.md) con orchestrator digitare DC/OS e [assicurarsi che i client possano connettersi cluster tooyour](../container-service-connect.md).</span><span class="sxs-lookup"><span data-stu-id="f0f21-115">[Deploy an instance of Azure Container Service](container-service-deployment.md) with orchestrator type DC/OS and  [ensure that your client can connect tooyour cluster](../container-service-connect.md).</span></span> <span data-ttu-id="f0f21-116">Inoltre, hello i passaggi seguenti.</span><span class="sxs-lookup"><span data-stu-id="f0f21-116">Also, do hello following steps.</span></span>

[!INCLUDE [install hello DC/OS CLI](../../../includes/container-service-install-dcos-cli-include.md)]

## <a name="create-an-application-or-user-specific-marathon-service"></a><span data-ttu-id="f0f21-117">Creare un servizio Marathon specifico per un'applicazione o un'utente</span><span class="sxs-lookup"><span data-stu-id="f0f21-117">Create an application or user-specific Marathon service</span></span>
<span data-ttu-id="f0f21-118">Iniziare creando un file di configurazione JSON che definisce il nome di hello del servizio di applicazione hello che si desidera toocreate.</span><span class="sxs-lookup"><span data-stu-id="f0f21-118">Begin by creating a JSON configuration file that defines hello name of hello application service that you want toocreate.</span></span> <span data-ttu-id="f0f21-119">Nell'esempio si utilizza `marathon-alice` come nome di framework hello.</span><span class="sxs-lookup"><span data-stu-id="f0f21-119">Here we use `marathon-alice` as hello framework name.</span></span> <span data-ttu-id="f0f21-120">Salvare il file di hello come `marathon-alice.json`:</span><span class="sxs-lookup"><span data-stu-id="f0f21-120">Save hello file as something like `marathon-alice.json`:</span></span>

```json
{"marathon": {"framework-name": "marathon-alice" }}
```

<span data-ttu-id="f0f21-121">Successivamente, utilizzare l'istanza maratona di hello DC/OS CLI tooinstall hello con le opzioni hello impostate nel file di configurazione:</span><span class="sxs-lookup"><span data-stu-id="f0f21-121">Next, use hello DC/OS CLI tooinstall hello Marathon instance with hello options that are set in your configuration file:</span></span>

```bash
dcos package install --options=marathon-alice.json marathon
```

<span data-ttu-id="f0f21-122">Verrà visualizzato il `marathon-alice` servizio in esecuzione nella scheda Servizi hello dell'interfaccia utente controller di dominio o del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="f0f21-122">You should now see your `marathon-alice` service running in hello Services tab of your DC/OS UI.</span></span> <span data-ttu-id="f0f21-123">Hello dell'interfaccia utente sarà `http://<hostname>/service/marathon-alice/` se si desidera tooaccess è direttamente.</span><span class="sxs-lookup"><span data-stu-id="f0f21-123">hello UI will be `http://<hostname>/service/marathon-alice/` if you want tooaccess it directly.</span></span>

## <a name="set-hello-dcos-cli-tooaccess-hello-service"></a><span data-ttu-id="f0f21-124">Impostare hello DC/OS CLI tooaccess servizio hello</span><span class="sxs-lookup"><span data-stu-id="f0f21-124">Set hello DC/OS CLI tooaccess hello service</span></span>
<span data-ttu-id="f0f21-125">È possibile facoltativamente configurare tooaccess il controller di dominio/OS CLI questo nuovo servizio impostazione hello `marathon.url` proprietà toopoint toohello `marathon-alice` istanza come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="f0f21-125">You can optionally configure your DC/OS CLI tooaccess this new service by setting hello `marathon.url` property toopoint toohello `marathon-alice` instance as follows:</span></span>

```bash
dcos config set marathon.url http://<hostname>/service/marathon-alice/
```

<span data-ttu-id="f0f21-126">È possibile verificare quale istanza di maratona in cui viene usata l'interfaccia CLI con hello `dcos config show` comando.</span><span class="sxs-lookup"><span data-stu-id="f0f21-126">You can verify which instance of Marathon that your CLI is working against with hello `dcos config show` command.</span></span> <span data-ttu-id="f0f21-127">È possibile ripristinare il master del servizio maratona con il comando hello toousing `dcos config unset marathon.url`.</span><span class="sxs-lookup"><span data-stu-id="f0f21-127">You can revert toousing your master Marathon service with hello command `dcos config unset marathon.url`.</span></span>

