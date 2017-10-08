---
title: aaaTroubleshooting istanze di contenitori di Azure
description: Informazioni su come tootroubleshoot problemi con le istanze di contenitore di Azure
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/03/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: dfec636a0a174c74a6f2e9d9c4da6e871f8d2fda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deployment-issues-with-azure-container-instances"></a><span data-ttu-id="57166-103">Risolvere i problemi di distribuzione in Istanze di contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="57166-103">Troubleshoot deployment issues with Azure Container Instances</span></span>

<span data-ttu-id="57166-104">Questo articolo illustra come tootroubleshoot problemi durante la distribuzione di contenitori tooAzure istanze di contenitori.</span><span class="sxs-lookup"><span data-stu-id="57166-104">This article shows how tootroubleshoot issues when deploying containers tooAzure Container Instances.</span></span> <span data-ttu-id="57166-105">Vengono inoltre descritti alcuni dei problemi comuni di hello che si verifichino.</span><span class="sxs-lookup"><span data-stu-id="57166-105">It also describes some of hello common issues you may run into.</span></span>

## <a name="getting-diagnostic-events"></a><span data-ttu-id="57166-106">Recupero degli eventi di diagnostica</span><span class="sxs-lookup"><span data-stu-id="57166-106">Getting diagnostic events</span></span>

<span data-ttu-id="57166-107">log tooview dal codice dell'applicazione in un contenitore, è possibile utilizzare hello [az contenitore registri](/cli/azure/container#logs) comando.</span><span class="sxs-lookup"><span data-stu-id="57166-107">tooview logs from your application code within a container, you can use hello [az container logs](/cli/azure/container#logs) command.</span></span> <span data-ttu-id="57166-108">Ma se il contenitore non viene distribuito correttamente, è necessario informazioni di diagnostica hello tooreview fornite dal provider di risorse hello istanze di contenitori di Azure.</span><span class="sxs-lookup"><span data-stu-id="57166-108">But if your container does not deploy successfully, you need tooreview hello diagnostic information provided by hello Azure Container Instances resource provider.</span></span> <span data-ttu-id="57166-109">eventi di hello tooview per il contenitore, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="57166-109">tooview hello events for your container, run hello following command:</span></span>

```azurecli-interactive
az container show -n mycontainername -g myresourcegroup
```

<span data-ttu-id="57166-110">output di Hello include proprietà principali hello del contenitore, insieme agli eventi di distribuzione:</span><span class="sxs-lookup"><span data-stu-id="57166-110">hello output includes hello core properties of your container, along with deployment events:</span></span>

```bash
{
  "containers": [
    {
      "command": null,
      "environmentVariables": [],
      "image": "microsoft/aci-helloworld",
      ...

      "events": [
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:52+00:00",
        "lastTimestamp": "2017-08-03T22:12:52+00:00",
        "message": "Pulling: pulling image \"microsoft/aci-helloworld\"",
        "type": "Normal"
      },
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:55+00:00",
        "lastTimestamp": "2017-08-03T22:12:55+00:00",
        "message": "Pulled: Successfully pulled image \"microsoft/aci-helloworld\"",
        "type": "Normal"
      },
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:55+00:00",
        "lastTimestamp": "2017-08-03T22:12:55+00:00",
        "message": "Created: Created container with id 61602059d6c31529c27609ef4ec0c858b0a96150177fa045cf944d7cf8fbab69",
        "type": "Normal"
      },
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:55+00:00",
        "lastTimestamp": "2017-08-03T22:12:55+00:00",
        "message": "Started: Started container with id 61602059d6c31529c27609ef4ec0c858b0a96150177fa045cf944d7cf8fbab69",
        "type": "Normal"
      }
    ],
    "name": "helloworld",
      "ports": [
        {
          "port": 80
        }
      ],
    ...
  ]
}
```

## <a name="common-deployment-issues"></a><span data-ttu-id="57166-111">Problemi di distribuzione comuni</span><span class="sxs-lookup"><span data-stu-id="57166-111">Common deployment issues</span></span>

<span data-ttu-id="57166-112">La maggior parte degli errori riscontrati durante la distribuzione è dovuta ad alcuni problemi comuni.</span><span class="sxs-lookup"><span data-stu-id="57166-112">There are a few common issues that account for most errors in deployment.</span></span>

### <a name="unable-toopull-image"></a><span data-ttu-id="57166-113">Non è possibile toopull immagine</span><span class="sxs-lookup"><span data-stu-id="57166-113">Unable toopull image</span></span>

<span data-ttu-id="57166-114">Se le istanze di contenitore di Azure è Impossibile toopull immagine inizialmente, eseguire un nuovo tentativo per un certo periodo prima che alla fine.</span><span class="sxs-lookup"><span data-stu-id="57166-114">If Azure Container Instances is unable toopull your image initially, it retries for some period before eventually failing.</span></span> <span data-ttu-id="57166-115">Se non è possibile effettuare il pull di immagine hello, vengono visualizzati gli eventi hello seguente:</span><span class="sxs-lookup"><span data-stu-id="57166-115">If hello image cannot be pulled, events like hello following are shown:</span></span>

```bash
"events": [
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:19:31+00:00",
    "lastTimestamp": "2017-08-03T22:19:31+00:00",
    "message": "Pulling: pulling image \"microsoft/aci-hellowrld\"",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:19:32+00:00",
    "lastTimestamp": "2017-08-03T22:19:32+00:00",
    "message": "Failed: Failed toopull image \"microsoft/aci-hellowrld\": rpc error: code 2 desc Error: image microsoft/aci-hellowrld:latest not found",
    "type": "Warning"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:19:33+00:00",
    "lastTimestamp": "2017-08-03T22:19:33+00:00",
    "message": "BackOff: Back-off pulling image \"microsoft/aci-hellowrld\"",
    "type": "Normal"
  }
]
```

<span data-ttu-id="57166-116">tooresolve, eliminare il contenitore di hello e ripetere la distribuzione, che sia stato digitato correttamente il nome di immagine hello pagante attenzione.</span><span class="sxs-lookup"><span data-stu-id="57166-116">tooresolve, delete hello container and retry your deployment, paying close attention that you have typed hello image name correctly.</span></span>

### <a name="container-continually-exits-and-restarts"></a><span data-ttu-id="57166-117">Il contenitore viene continuamente chiuso e riavviato</span><span class="sxs-lookup"><span data-stu-id="57166-117">Container continually exits and restarts</span></span>

<span data-ttu-id="57166-118">Istanze di contenitore di Azure supporta attualmente solo servizi a esecuzione prolungata.</span><span class="sxs-lookup"><span data-stu-id="57166-118">Currently, Azure Container Instances only supports long-running services.</span></span> <span data-ttu-id="57166-119">Se il contenitore esegue toocompletion e viene chiusa, viene automaticamente riavviata e viene eseguito di nuovo.</span><span class="sxs-lookup"><span data-stu-id="57166-119">If your container runs toocompletion and exits, it automatically restarts and runs again.</span></span> <span data-ttu-id="57166-120">In questo caso, vengono visualizzati eventi simili ai seguenti.</span><span class="sxs-lookup"><span data-stu-id="57166-120">If this happens, events like those following are shown.</span></span> <span data-ttu-id="57166-121">Nota che il contenitore hello si avvia, viene riavviato rapidamente.</span><span class="sxs-lookup"><span data-stu-id="57166-121">Note that hello container successfully starts, then quickly restarts.</span></span> <span data-ttu-id="57166-122">Hello contenitore istanze API include un `retryCount` proprietà che indica quante volte un determinato contenitore è stato riavviato.</span><span class="sxs-lookup"><span data-stu-id="57166-122">hello Container Instances API includes a `retryCount` property that shows how many times a particular container has restarted.</span></span>

```bash
"events": [
  {
    "count": 5,
    "firstTimestamp": "2017-08-03T22:21:55+00:00",
    "lastTimestamp": "2017-08-03T22:23:22+00:00",
    "message": "Pulling: pulling image \"alpine\"",
    "type": "Normal"
  },
  {
    "count": 5,
    "firstTimestamp": "2017-08-03T22:21:57+00:00",
    "lastTimestamp": "2017-08-03T22:23:23+00:00",
    "message": "Pulled: Successfully pulled image \"alpine\"",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:57+00:00",
    "lastTimestamp": "2017-08-03T22:21:57+00:00",
    "message": "Created: Created container with id ad2bf9bc51761c5f935260b4bab53b164d52d9cbc045b16afcb26fb4d14d0a70",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:57+00:00",
    "lastTimestamp": "2017-08-03T22:21:57+00:00",
    "message": "Started: Started container with id ad2bf9bc51761c5f935260b4bab53b164d52d9cbc045b16afcb26fb4d14d0a70",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:58+00:00",
    "lastTimestamp": "2017-08-03T22:21:58+00:00",
    "message": "Created: Created container with id 7687b9bd15dc01731fa66fc45f6f0241495600602dd03841e559453245e7f70b",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:58+00:00",
    "lastTimestamp": "2017-08-03T22:21:58+00:00",
    "message": "Started: Started container with id 7687b9bd15dc01731fa66fc45f6f0241495600602dd03841e559453245e7f70b",
    "type": "Normal"
  },
  {
    "count": 13,
    "firstTimestamp": "2017-08-03T22:21:59+00:00",
    "lastTimestamp": "2017-08-03T22:24:36+00:00",
    "message": "BackOff: Back-off restarting failed container",
    "type": "Warning"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:22:13+00:00",
    "lastTimestamp": "2017-08-03T22:22:13+00:00",
    "message": "Created: Created container with id 72e347e891290e238135e4a6b3078748ca25a1275dbbff30d8d214f026d89220",
    "type": "Normal"
  },
  ...
```

> [!NOTE]
> <span data-ttu-id="57166-123">La maggior parte delle immagini contenitore per le distribuzioni di Linux impostare una shell, come bash, come comando predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="57166-123">Most container images for Linux distributions set a shell, such as bash, as hello default command.</span></span> <span data-ttu-id="57166-124">Poiché una shell non è di per sé un servizio a esecuzione prolungata, questi contenitori vengono chiusi immediatamente e sono soggetti a un riavvio ciclico.</span><span class="sxs-lookup"><span data-stu-id="57166-124">Since a shell on its own is not a long-running service, these containers immediately exit and fall into a restart loop.</span></span>

### <a name="container-takes-a-long-time-toostart"></a><span data-ttu-id="57166-125">Contenitore accetta un toostart molto tempo</span><span class="sxs-lookup"><span data-stu-id="57166-125">Container takes a long time toostart</span></span>

<span data-ttu-id="57166-126">Se il contenitore richiede un toostart molto tempo, ma andrà a buon fine, iniziare esaminando dimensioni hello dell'immagine contenitore.</span><span class="sxs-lookup"><span data-stu-id="57166-126">If your container takes a long time toostart, but eventually succeeds, start by looking at hello size of your container image.</span></span> <span data-ttu-id="57166-127">Poiché le istanze di contenitore di Azure effettua il pull dell'immagine del contenitore su richiesta, si verificano tempi di avvio di hello sono tooits direttamente correlate, dimensioni.</span><span class="sxs-lookup"><span data-stu-id="57166-127">Because Azure Container Instances pulls your container image on demand, hello startup time you experience is directly related tooits size.</span></span>

<span data-ttu-id="57166-128">È possibile visualizzare dimensioni hello dell'immagine contenitore con Docker CLI hello:</span><span class="sxs-lookup"><span data-stu-id="57166-128">You can view hello size of your container image using hello Docker CLI:</span></span>

```bash
docker images
```

<span data-ttu-id="57166-129">Output:</span><span class="sxs-lookup"><span data-stu-id="57166-129">Output:</span></span>

```bash
REPOSITORY                             TAG                 IMAGE ID            CREATED             SIZE
microsoft/aci-helloworld               latest              7f78509b568e        13 days ago         68.1MB
```

<span data-ttu-id="57166-130">dimensioni dell'immagine di Hello tookeeping chiave piccole consiste nel garantire che l'immagine finale non può contenere dati che non è necessaria in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="57166-130">hello key tookeeping image sizes small is ensuring that your final image does not contain anything that is not required at runtime.</span></span> <span data-ttu-id="57166-131">Un modo toodo con [compilazioni a più fasi](https://docs.docker.com/engine/userguide/eng-image/multistage-build/).</span><span class="sxs-lookup"><span data-stu-id="57166-131">One way toodo this is with [multi-stage builds](https://docs.docker.com/engine/userguide/eng-image/multistage-build/).</span></span> <span data-ttu-id="57166-132">Le compilazioni a più fasi rendono tooensure semplice che immagine finale hello contenga solo elementi hello è necessario per l'applicazione e non hello aggiuntivo di contenuto che è stato richiesto al momento della compilazione.</span><span class="sxs-lookup"><span data-stu-id="57166-132">Multi-stage builds make it easy tooensure that hello final image contains only hello artifacts you need for your application, and not any of hello extra content that was required at build time.</span></span>

<span data-ttu-id="57166-133">altri effetti di hello tooreduce modo di hello immagine pull ora di avvio del contenitore Hello sono toohost hello contenitore immagine utilizzando Ciao del Registro di sistema di Azure contenitore hello stessa area in cui si intende toouse istanze di contenitori di Azure.</span><span class="sxs-lookup"><span data-stu-id="57166-133">hello other way tooreduce hello impact of hello image pull on your container's startup time is toohost hello container image using hello Azure Container Registry in hello same region where you intend toouse Azure Container Instances.</span></span> <span data-ttu-id="57166-134">Questo riduce percorso di rete hello hello tootravel di esigenze immagine contenitore, ridurre notevolmente i tempi di download hello.</span><span class="sxs-lookup"><span data-stu-id="57166-134">This shortens hello network path that hello container image needs tootravel, significantly shortening hello download time.</span></span>
