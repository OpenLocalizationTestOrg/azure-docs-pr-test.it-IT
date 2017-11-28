---
title: aaaUse bozza con il servizio contenitore di Azure e del Registro di sistema di Azure contenitore | Documenti Microsoft
description: Creare un cluster ACS Kubernetes e un toocreate del Registro di sistema di Azure contenitore della prima applicazione in Azure con bozza.
services: container-service
documentationcenter: 
author: squillace
manager: gamonroy
editor: 
tags: draft, helm, acs, azure-container-service
keywords: Docker, contenitori, microservizi, Kubernetes, Draft, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: rasquill
ms.custom: mvc
ms.openlocfilehash: f5e21cda01e5e8452bf86a5c8fa458904d89f451
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-draft-with-azure-container-service-and-azure-container-registry-toobuild-and-deploy-an-application-tookubernetes"></a><span data-ttu-id="cdc16-104">Utilizzare bozza con il servizio contenitore di Azure e del Registro di sistema di Azure contenitore toobuild e distribuire un'applicazione tooKubernetes</span><span class="sxs-lookup"><span data-stu-id="cdc16-104">Use Draft with Azure Container Service and Azure Container Registry toobuild and deploy an application tooKubernetes</span></span>

<span data-ttu-id="cdc16-105">[Bozza](https://aka.ms/draft) è un nuovo strumento open source che rende le applicazioni basate sul contenitore toodevelop semplice e distribuirli tooKubernetes cluster senza conoscere molto di Docker e Kubernetes - o anche l'installazione.</span><span class="sxs-lookup"><span data-stu-id="cdc16-105">[Draft](https://aka.ms/draft) is a new open-source tool that makes it easy toodevelop container-based applications and deploy them tooKubernetes clusters without knowing much about Docker and Kubernetes -- or even installing them.</span></span> <span data-ttu-id="cdc16-106">Usando strumenti come bozza consentono lo stato attivo del team compilazione di un'applicazione hello con Kubernetes, non sostenere il maggior numero tooinfrastructure attenzione.</span><span class="sxs-lookup"><span data-stu-id="cdc16-106">Using tools like Draft let you and your teams focus on building hello application with Kubernetes, not paying as much attention tooinfrastructure.</span></span>

<span data-ttu-id="cdc16-107">È possibile usare Draft con qualsiasi registro di immagini Docker e cluster Kubernetes, anche in locale.</span><span class="sxs-lookup"><span data-stu-id="cdc16-107">You can use Draft with any Docker image registry and any Kubernetes cluster, including locally.</span></span> <span data-ttu-id="cdc16-108">Questa esercitazione viene illustrato come toouse ACS con toocreate Kubernetes e record DNS di Azure uno sviluppatore CI/CD-ROM in tempo reale di pipeline utilizzando bozza.</span><span class="sxs-lookup"><span data-stu-id="cdc16-108">This tutorial shows how toouse ACS with Kubernetes, ACR, and Azure DNS toocreate a live CI/CD developer pipeline using Draft.</span></span>


## <a name="create-an-azure-container-registry"></a><span data-ttu-id="cdc16-109">Creare un Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="cdc16-109">Create an Azure Container Registry</span></span>
<span data-ttu-id="cdc16-110">È possibile [creare un nuovo registro contenitore Azure](../../container-registry/container-registry-get-started-azure-cli.md), ma hello passaggi sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="cdc16-110">You can easily [create a new Azure Container Registry](../../container-registry/container-registry-get-started-azure-cli.md), but hello steps are as follows:</span></span>

1. <span data-ttu-id="cdc16-111">Creare un toomanage gruppo di risorse di Azure del cluster Kubernetes record del Registro di sistema e hello in ACS.</span><span class="sxs-lookup"><span data-stu-id="cdc16-111">Create a Azure resource group toomanage your ACR registry and hello Kubernetes cluster in ACS.</span></span>
      ```azurecli
      az group create --name draft --location eastus
      ```

2. <span data-ttu-id="cdc16-112">Creare un registro di immagini del Registro contenitori di Azure usando [az acr create](/cli/azure/acr#create)</span><span class="sxs-lookup"><span data-stu-id="cdc16-112">Create an ACR image registry using [az acr create](/cli/azure/acr#create)</span></span>
      ```azurecli
      az acr create -g draft -n draftacs --sku Basic --admin-enabled true -l eastus
      ```


## <a name="create-an-azure-container-service-with-kubernetes"></a><span data-ttu-id="cdc16-113">Creare un servizio contenitore di Azure con Kubernetes</span><span class="sxs-lookup"><span data-stu-id="cdc16-113">Create an Azure Container Service with Kubernetes</span></span>

<span data-ttu-id="cdc16-114">A questo punto è pronti toouse [az acs creare](/cli/azure/acs#create) cluster toocreate un ACS utilizzando Kubernetes come hello `--orchestrator-type` valore.</span><span class="sxs-lookup"><span data-stu-id="cdc16-114">Now you're ready toouse [az acs create](/cli/azure/acs#create) toocreate an ACS cluster using Kubernetes as hello `--orchestrator-type` value.</span></span>
```azurecli
az acs create --resource-group draft --name draft-kube-acs --dns-prefix draft-cluster --orchestrator-type kubernetes
```

> [!NOTE]
> <span data-ttu-id="cdc16-115">Poiché Kubernetes non è di tipo di orchestrator hello predefinito, assicurarsi di utilizzare hello `--orchestrator-type kubernetes` passare.</span><span class="sxs-lookup"><span data-stu-id="cdc16-115">Because Kubernetes is not hello default orchestrator type, be sure you use hello `--orchestrator-type kubernetes` switch.</span></span>

<span data-ttu-id="cdc16-116">output di Hello quando ha esito positivo sarà simile toohello seguente.</span><span class="sxs-lookup"><span data-stu-id="cdc16-116">hello output when successful looks similar toohello following.</span></span>

```json
waiting for AAD role toopropagate.done
{
  "id": "/subscriptions/<guid>/resourceGroups/draft/providers/Microsoft.Resources/deployments/azurecli14904.93snip09",
  "name": "azurecli1496227204.9323909",
  "properties": {
    "correlationId": "<guid>",
    "debugSetting": null,
    "dependencies": [],
    "mode": "Incremental",
    "outputs": null,
    "parameters": {
      "clientSecret": {
        "type": "SecureString"
      }
    },
    "parametersLink": null,
    "providers": [
      {
        "id": null,
        "namespace": "Microsoft.ContainerService",
        "registrationState": null,
        "resourceTypes": [
          {
            "aliases": null,
            "apiVersions": null,
            "locations": [
              "westus"
            ],
            "properties": null,
            "resourceType": "containerServices"
          }
        ]
      }
    ],
    "provisioningState": "Succeeded",
    "template": null,
    "templateLink": null,
    "timestamp": "2017-05-31T10:46:29.434095+00:00"
  },
  "resourceGroup": "draft"
}
```

<span data-ttu-id="cdc16-117">Dopo aver creato un cluster, è possibile importare le credenziali di hello utilizzando hello [az acs kubernetes get-credenziali](/cli/azure/acs/kubernetes#get-credentials) comando.</span><span class="sxs-lookup"><span data-stu-id="cdc16-117">Now that you have a cluster, you can import hello credentials by using hello [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span> <span data-ttu-id="cdc16-118">Ora è un file di configurazione locale per il cluster, ovvero quali Helm e bozza necessario tooget proprio lavoro.</span><span class="sxs-lookup"><span data-stu-id="cdc16-118">Now you have a local configuration file for your cluster, which is what Helm and Draft need tooget their work done.</span></span>

## <a name="install-and-configure-draft"></a><span data-ttu-id="cdc16-119">Installare e configurare Draft</span><span class="sxs-lookup"><span data-stu-id="cdc16-119">Install and configure draft</span></span>
<span data-ttu-id="cdc16-120">istruzioni di installazione di Hello per bozza presenti hello [repository bozza](https://github.com/Azure/draft/blob/master/docs/install.md).</span><span class="sxs-lookup"><span data-stu-id="cdc16-120">hello installation instructions for Draft are in hello [Draft repository](https://github.com/Azure/draft/blob/master/docs/install.md).</span></span> <span data-ttu-id="cdc16-121">Sono relativamente semplici, ma richiedono operazioni di configurazione, come dipende [Helm](https://aka.ms/helm) toocreate e distribuire un grafico Helm in cluster Kubernetes hello.</span><span class="sxs-lookup"><span data-stu-id="cdc16-121">They are relatively simple, but do require some configuration, as it depends on [Helm](https://aka.ms/helm) toocreate and deploy a Helm chart into hello Kubernetes cluster.</span></span>

1. <span data-ttu-id="cdc16-122">[Scaricare e installare Helm](https://aka.ms/helm#install).</span><span class="sxs-lookup"><span data-stu-id="cdc16-122">[Download and install Helm](https://aka.ms/helm#install).</span></span>
2. <span data-ttu-id="cdc16-123">Utilizzare toosearch Helm per e installa `stable/traefik`e in ingresso controller tooenable le richieste per le compilazioni in ingresso.</span><span class="sxs-lookup"><span data-stu-id="cdc16-123">Use Helm toosearch for and install `stable/traefik`, and ingress controller tooenable inbound requests for your builds.</span></span>
    ```bash
    $ helm search traefik
    NAME            VERSION DESCRIPTION
    stable/traefik  1.3.0   A Traefik based Kubernetes ingress controller w...

    $ helm install stable/traefik --name ingress
    ```
    <span data-ttu-id="cdc16-124">Ora impostare un'espressione di controllo su hello `ingress` controller toocapture hello IP valore esterno quando viene distribuito.</span><span class="sxs-lookup"><span data-stu-id="cdc16-124">Now set a watch on hello `ingress` controller toocapture hello external IP value when it is deployed.</span></span> <span data-ttu-id="cdc16-125">Questo indirizzo IP sarà hello uno [mappata dominio distribuzione tooyour](#wire-up-deployment-domain) nella sezione successiva hello.</span><span class="sxs-lookup"><span data-stu-id="cdc16-125">This IP address will be hello one [mapped tooyour deployment domain](#wire-up-deployment-domain) in hello next section.</span></span>

    ```bash
    kubectl get svc -w
    NAME                          CLUSTER-IP     EXTERNAL-IP     PORT(S)                      AGE
    ingress-traefik               10.0.248.104   13.64.108.240   80:31046/TCP,443:32556/TCP   1h
    kubernetes                    10.0.0.1       <none>          443/TCP                      7h
    ```

    <span data-ttu-id="cdc16-126">In questo caso, hello indirizzo IP esterno per il dominio di distribuzione hello è `13.64.108.240`.</span><span class="sxs-lookup"><span data-stu-id="cdc16-126">In this case, hello external IP for hello deployment domain is `13.64.108.240`.</span></span> <span data-ttu-id="cdc16-127">Ora è possibile mappare i IP toothat di dominio.</span><span class="sxs-lookup"><span data-stu-id="cdc16-127">Now you can map your domain toothat IP.</span></span>

## <a name="wire-up-deployment-domain"></a><span data-ttu-id="cdc16-128">Collegare il dominio di distribuzione</span><span class="sxs-lookup"><span data-stu-id="cdc16-128">Wire up deployment domain</span></span>

<span data-ttu-id="cdc16-129">Draft crea una versione per ogni grafico Helm creato, ovvero ogni applicazione a cui si sta lavorando.</span><span class="sxs-lookup"><span data-stu-id="cdc16-129">Draft creates a release for each Helm chart it creates -- each application you are working on.</span></span> <span data-ttu-id="cdc16-130">Ognuno di essi Ottiene un nome generato utilizzato dal progetto come un _sottodominio_ sopra radice hello _dominio distribuzione_ controllate dall'utente.</span><span class="sxs-lookup"><span data-stu-id="cdc16-130">Each one gets a generated name that is used by draft as a _subdomain_ on top of hello root _deployment domain_ that you control.</span></span> <span data-ttu-id="cdc16-131">(In questo esempio, si usa `squillace.io` come dominio distribuzione hello.) tooenable questo comportamento di sottodominio, è necessario creare un record A per `'*'` le voci DNS per il dominio di distribuzione, in modo che ogni generato sottodominio è indirizzato toohello Kubernetes controller di ingresso del cluster.</span><span class="sxs-lookup"><span data-stu-id="cdc16-131">(In this example, we use `squillace.io` as hello deployment domain.) tooenable this subdomain behavior, you must create an A record for `'*'` in your DNS entries for your deployment domain, so that each generated subdomain is routed toohello Kubernetes cluster's ingress controller.</span></span>

<span data-ttu-id="cdc16-132">Un provider di dominio ha i propri server DNS di vie tooassign; troppo[delegare il tooAzure nameservers di dominio DNS](../../dns/dns-delegate-domain-azure-dns.md), si accettano hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="cdc16-132">Your own domain provider has their own way tooassign DNS servers; too[delegate your domain nameservers tooAzure DNS](../../dns/dns-delegate-domain-azure-dns.md), you take hello following steps:</span></span>

1. <span data-ttu-id="cdc16-133">Creare un gruppo di risorse per la propria zona.</span><span class="sxs-lookup"><span data-stu-id="cdc16-133">Create a resource group for your zone.</span></span>
    ```azurecli
    az group create --name squillace.io --location eastus
    {
      "id": "/subscriptions/<guid>/resourceGroups/squillace.io",
      "location": "eastus",
      "managedBy": null,
      "name": "zones",
      "properties": {
        "provisioningState": "Succeeded"
      },
      "tags": null
    }
    ```

2. <span data-ttu-id="cdc16-134">Creare una zona DNS per il proprio dominio.</span><span class="sxs-lookup"><span data-stu-id="cdc16-134">Create a DNS zone for your domain.</span></span>
<span data-ttu-id="cdc16-135">Hello utilizzare [zona dns di rete az creare](/cli/azure/network/dns/zone#create) comando tooobtain hello nameservers toodelegate DNS controllare tooAzure DNS per il dominio.</span><span class="sxs-lookup"><span data-stu-id="cdc16-135">Use hello [az network dns zone create](/cli/azure/network/dns/zone#create) command tooobtain hello nameservers toodelegate DNS control tooAzure DNS for your domain.</span></span>
    ```azurecli
    az network dns zone create --resource-group squillace.io --name squillace.io
    {
      "etag": "<guid>",
      "id": "/subscriptions/<guid>/resourceGroups/zones/providers/Microsoft.Network/dnszones/squillace.io",
      "location": "global",
      "maxNumberOfRecordSets": 5000,
      "name": "squillace.io",
      "nameServers": [
        "ns1-09.azure-dns.com.",
        "ns2-09.azure-dns.net.",
        "ns3-09.azure-dns.org.",
        "ns4-09.azure-dns.info."
      ],
      "numberOfRecordSets": 2,
      "resourceGroup": "squillace.io",
      "tags": {},
      "type": "Microsoft.Network/dnszones"
    }
    ```
3. <span data-ttu-id="cdc16-136">Aggiungere i server DNS di hello che è toohello provider del dominio per il dominio di distribuzione, che consente il dominio è toouse DNS di Azure toorepoint desiderato.</span><span class="sxs-lookup"><span data-stu-id="cdc16-136">Add hello DNS servers you are given toohello domain provider for your deployment domain, which enables you toouse Azure DNS toorepoint your domain as you want.</span></span>
4. <span data-ttu-id="cdc16-137">Creare una voce di set di record A per il toohello di mapping dominio distribuzione `ingress` IP dal passaggio 2 della sezione precedente hello.</span><span class="sxs-lookup"><span data-stu-id="cdc16-137">Create an A record-set entry for your deployment domain mapping toohello `ingress` IP from step 2 of hello previous section.</span></span>
    ```azurecli
    az network dns record-set a add-record --ipv4-address 13.64.108.240 --record-set-name '*' -g squillace.io -z squillace.io
    ```
<span data-ttu-id="cdc16-138">output di Hello simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="cdc16-138">hello output looks something like:</span></span>
    ```json
    {
      "arecords": [
        {
          "ipv4Address": "13.64.108.240"
        }
      ],
      "etag": "<guid>",
      "id": "/subscriptions/<guid>/resourceGroups/squillace.io/providers/Microsoft.Network/dnszones/squillace.io/A/*",
      "metadata": null,
      "name": "*",
      "resourceGroup": "squillace.io",
      "ttl": 3600,
      "type": "Microsoft.Network/dnszones/A"
    }
    ```

5. <span data-ttu-id="cdc16-139">Configurare toouse bozza del Registro di sistema e creare i sottodomini per ogni grafico Helm che viene creato.</span><span class="sxs-lookup"><span data-stu-id="cdc16-139">Configure Draft toouse your registry and create subdomains for each Helm chart it creates.</span></span> <span data-ttu-id="cdc16-140">tooconfigure bozza, è necessario:</span><span class="sxs-lookup"><span data-stu-id="cdc16-140">tooconfigure Draft, you need:</span></span>
  - <span data-ttu-id="cdc16-141">Il nome del Registro contenitori di Azure (in questo esempio, `draft`)</span><span class="sxs-lookup"><span data-stu-id="cdc16-141">your Azure Container Registry name (in this example, `draft`)</span></span>
  - <span data-ttu-id="cdc16-142">La chiave, o password, del registro da `az acr credential show -n <registry name> --output tsv --query "passwords[0].value"`.</span><span class="sxs-lookup"><span data-stu-id="cdc16-142">your registry key, or password, from `az acr credential show -n <registry name> --output tsv --query "passwords[0].value"`.</span></span>
  - <span data-ttu-id="cdc16-143">dominio di distribuzione principale di Hello di aver configurato toomap toohello Kubernetes in ingresso l'indirizzo IP esterno (in questo caso, `squillace.io`)</span><span class="sxs-lookup"><span data-stu-id="cdc16-143">hello root deployment domain that you have configured toomap toohello Kubernetes ingress external IP address (here, `squillace.io`)</span></span>

  <span data-ttu-id="cdc16-144">Chiamare `draft init` e il processo di configurazione di hello viene chiesto di immettere i valori hello precedenti.</span><span class="sxs-lookup"><span data-stu-id="cdc16-144">Call `draft init` and hello configuration process prompts you for hello values above.</span></span> <span data-ttu-id="cdc16-145">processo Hello sembra qualcosa seguente hello hello prima di eseguirla.</span><span class="sxs-lookup"><span data-stu-id="cdc16-145">hello process looks something like hello following hello first time you run it.</span></span>
 ```bash
    $ draft init
    Creating pack ruby...
    Creating pack node...
    Creating pack gradle...
    Creating pack maven...
    Creating pack php...
    Creating pack python...
    Creating pack dotnetcore...
    Creating pack golang...
    $DRAFT_HOME has been configured at /Users/ralphsquillace/.draft.

    In order tooinstall Draft, we need a bit more information...

    1. Enter your Docker registry URL (e.g. docker.io, quay.io, myregistry.azurecr.io): draft.azurecr.io
    2. Enter your username: draft
    3. Enter your password:
    4. Enter your org where Draft will push images [draft]: draft
    5. Enter your top-level domain for ingress (e.g. draft.example.com): squillace.io
    Draft has been installed into your Kubernetes Cluster.
    Happy Sailing!
    ```

<span data-ttu-id="cdc16-146">Ora si è pronti toodeploy un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cdc16-146">Now you're ready toodeploy an application.</span></span>


## <a name="build-and-deploy-an-application"></a><span data-ttu-id="cdc16-147">Compilare e distribuire un'applicazione</span><span class="sxs-lookup"><span data-stu-id="cdc16-147">Build and deploy an application</span></span>

<span data-ttu-id="cdc16-148">Nel repository di bozza hello sono [sei applicazioni di esempio semplice](https://github.com/Azure/draft/tree/master/examples).</span><span class="sxs-lookup"><span data-stu-id="cdc16-148">In hello Draft repo are [six simple example applications](https://github.com/Azure/draft/tree/master/examples).</span></span> <span data-ttu-id="cdc16-149">Clonare il repository hello e utilizziamo hello [esempio Python](https://github.com/Azure/draft/tree/master/examples/python).</span><span class="sxs-lookup"><span data-stu-id="cdc16-149">Clone hello repo and let's use hello [Python example](https://github.com/Azure/draft/tree/master/examples/python).</span></span> <span data-ttu-id="cdc16-150">Modificare in directory esempi/Python hello e digitare `draft create` toobuild un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="cdc16-150">Change into hello examples/Python directory, and type `draft create` toobuild hello application.</span></span> <span data-ttu-id="cdc16-151">Dovrebbe essere simile hello di esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="cdc16-151">It should look like hello following example.</span></span>
```bash
$ draft create
--> Python app detected
--> Ready toosail
```

<span data-ttu-id="cdc16-152">output di Hello include un Dockerfile e un grafico Helm.</span><span class="sxs-lookup"><span data-stu-id="cdc16-152">hello output includes a Dockerfile and a Helm chart.</span></span> <span data-ttu-id="cdc16-153">toobuild e la distribuzione, è sufficiente digitare `draft up`.</span><span class="sxs-lookup"><span data-stu-id="cdc16-153">toobuild and deploy, you just type `draft up`.</span></span> <span data-ttu-id="cdc16-154">output di Hello è vasto, ma inizia come hello di esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="cdc16-154">hello output is extensive, but begins like hello following example.</span></span>
```bash
$ draft up
--> Building Dockerfile
Step 1 : FROM python:onbuild
onbuild: Pulling from library/python
10a267c67f42: Pulling fs layer
fb5937da9414: Pulling fs layer
9021b2326a1e: Pulling fs layer
dbed9b09434e: Pulling fs layer
ea8a37f15161: Pulling fs layer
<snip>
```

<span data-ttu-id="cdc16-155">e quando ha esito positivo termina con un codice simile toohello esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="cdc16-155">and when successful ends with something similar toohello following example.</span></span>
```bash
ab68189731eb: Pushed
53c0ab0341bee12d01be3d3c192fbd63562af7f1: digest: sha256:bb0450ec37acf67ed461c1512ef21f58a500ff9326ce3ec623ce1e4427df9765 size: 2841
--> Deploying tooKubernetes
--> Status: DEPLOYED
--> Notes:

  http://gangly-bronco.squillace.io tooaccess your application

Watching local files for changes...
```

<span data-ttu-id="cdc16-156">L'elemento è il nome del grafico, è ora possibile `curl http://gangly-bronco.squillace.io` risposta hello tooreceive, `Hello World!`.</span><span class="sxs-lookup"><span data-stu-id="cdc16-156">Whatever your chart's name is, you can now `curl http://gangly-bronco.squillace.io` tooreceive hello reply, `Hello World!`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cdc16-157">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cdc16-157">Next steps</span></span>

<span data-ttu-id="cdc16-158">Dopo aver creato un cluster ACS Kubernetes, è possibile provare a utilizzare [Registro di sistema di Azure contenitore](../../container-registry/container-registry-intro.md) toocreate altre e diverse distribuzioni di questo scenario.</span><span class="sxs-lookup"><span data-stu-id="cdc16-158">Now that you have an ACS Kubernetes cluster, you can investigate using [Azure Container Registry](../../container-registry/container-registry-intro.md) toocreate more and different deployments of this scenario.</span></span> <span data-ttu-id="cdc16-159">È ad esempio possibile creare un recordset DNS di dominio draft._basedomain.toplevel_ che controlla le attività all'esterno di un sottodominio più profondo per distribuzioni specifiche del servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="cdc16-159">For example, you can create a draft._basedomain.toplevel_ domain DNS record-set that controls things off of a deeper subdomain for specific ACS deployments.</span></span>






