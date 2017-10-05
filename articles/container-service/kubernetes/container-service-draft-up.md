---
title: Usare Draft con il servizio contenitore di Azure e il Registro contenitori di Azure | Microsoft Docs
description: Creare un cluster Kubernetes ACS e un Registro contenitori di Azure per creare la prima applicazione in Azure con Draft.
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
ms.openlocfilehash: e7e3ea461145571753a1a6d768b52118dcbfb507
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="use-draft-with-azure-container-service-and-azure-container-registry-to-build-and-deploy-an-application-to-kubernetes"></a><span data-ttu-id="e6e91-104">Usare Draft con il servizio contenitore di Azure e il Registro contenitori di Azure per compilare e distribuire un'applicazione in Kubernetes</span><span class="sxs-lookup"><span data-stu-id="e6e91-104">Use Draft with Azure Container Service and Azure Container Registry to build and deploy an application to Kubernetes</span></span>

<span data-ttu-id="e6e91-105">[Draft](https://aka.ms/draft) è un nuovo strumento open source che semplifica lo sviluppo di applicazioni basate su contenitori e la loro distribuzione in cluster Kubernetes senza necessità di conoscere a fondo Docker e Kubernetes, né di installarli.</span><span class="sxs-lookup"><span data-stu-id="e6e91-105">[Draft](https://aka.ms/draft) is a new open-source tool that makes it easy to develop container-based applications and deploy them to Kubernetes clusters without knowing much about Docker and Kubernetes -- or even installing them.</span></span> <span data-ttu-id="e6e91-106">Con strumenti come Draft, gli sviluppatori e i loro team possono concentrarsi sulla compilazione dell'applicazione con Kubernetes, senza fare molta attenzione all'infrastruttura.</span><span class="sxs-lookup"><span data-stu-id="e6e91-106">Using tools like Draft let you and your teams focus on building the application with Kubernetes, not paying as much attention to infrastructure.</span></span>

<span data-ttu-id="e6e91-107">È possibile usare Draft con qualsiasi registro di immagini Docker e cluster Kubernetes, anche in locale.</span><span class="sxs-lookup"><span data-stu-id="e6e91-107">You can use Draft with any Docker image registry and any Kubernetes cluster, including locally.</span></span> <span data-ttu-id="e6e91-108">Questa esercitazione mostra come usare il servizio contenitore di Azure con Kubernetes, il Registro contenitori di Azure e il servizio DNS di Azure per creare una pipeline di sviluppo CI/CD (integrazione continua/distribuzione continua) live con Draft.</span><span class="sxs-lookup"><span data-stu-id="e6e91-108">This tutorial shows how to use ACS with Kubernetes, ACR, and Azure DNS to create a live CI/CD developer pipeline using Draft.</span></span>


## <a name="create-an-azure-container-registry"></a><span data-ttu-id="e6e91-109">Creare un Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="e6e91-109">Create an Azure Container Registry</span></span>
<span data-ttu-id="e6e91-110">È possibile [creare un nuovo Registro contenitori di Azure](../../container-registry/container-registry-get-started-azure-cli.md) facilmente, ma i passaggi sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="e6e91-110">You can easily [create a new Azure Container Registry](../../container-registry/container-registry-get-started-azure-cli.md), but the steps are as follows:</span></span>

1. <span data-ttu-id="e6e91-111">Creare un gruppo di risorse di Azure per gestire il Registro contenitori di Azure e il cluster Kubernetes nel servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="e6e91-111">Create a Azure resource group to manage your ACR registry and the Kubernetes cluster in ACS.</span></span>
      ```azurecli
      az group create --name draft --location eastus
      ```

2. <span data-ttu-id="e6e91-112">Creare un registro di immagini del Registro contenitori di Azure usando [az acr create](/cli/azure/acr#create)</span><span class="sxs-lookup"><span data-stu-id="e6e91-112">Create an ACR image registry using [az acr create](/cli/azure/acr#create)</span></span>
      ```azurecli
      az acr create -g draft -n draftacs --sku Basic --admin-enabled true -l eastus
      ```


## <a name="create-an-azure-container-service-with-kubernetes"></a><span data-ttu-id="e6e91-113">Creare un servizio contenitore di Azure con Kubernetes</span><span class="sxs-lookup"><span data-stu-id="e6e91-113">Create an Azure Container Service with Kubernetes</span></span>

<span data-ttu-id="e6e91-114">A questo punto, è possibile usare [az acs create](/cli/azure/acs#create) per creare un cluster ACS usando Kubernetes come valore `--orchestrator-type`.</span><span class="sxs-lookup"><span data-stu-id="e6e91-114">Now you're ready to use [az acs create](/cli/azure/acs#create) to create an ACS cluster using Kubernetes as the `--orchestrator-type` value.</span></span>
```azurecli
az acs create --resource-group draft --name draft-kube-acs --dns-prefix draft-cluster --orchestrator-type kubernetes
```

> [!NOTE]
> <span data-ttu-id="e6e91-115">Poiché Kubernetes non è il tipo di agente di orchestrazione predefinito, assicurarsi di usare l'opzione `--orchestrator-type kubernetes`.</span><span class="sxs-lookup"><span data-stu-id="e6e91-115">Because Kubernetes is not the default orchestrator type, be sure you use the `--orchestrator-type kubernetes` switch.</span></span>

<span data-ttu-id="e6e91-116">L'output, in caso di esito positivo, è simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="e6e91-116">The output when successful looks similar to the following.</span></span>

```json
waiting for AAD role to propagate.done
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

<span data-ttu-id="e6e91-117">Dopo aver creato un cluster, è possibile importare le credenziali usando il comando [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials).</span><span class="sxs-lookup"><span data-stu-id="e6e91-117">Now that you have a cluster, you can import the credentials by using the [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span> <span data-ttu-id="e6e91-118">A questo punto, si ha un file di configurazione locale per il cluster, necessario per Helm e Draft.</span><span class="sxs-lookup"><span data-stu-id="e6e91-118">Now you have a local configuration file for your cluster, which is what Helm and Draft need to get their work done.</span></span>

## <a name="install-and-configure-draft"></a><span data-ttu-id="e6e91-119">Installare e configurare Draft</span><span class="sxs-lookup"><span data-stu-id="e6e91-119">Install and configure draft</span></span>
<span data-ttu-id="e6e91-120">Le istruzioni di installazione di Draft sono disponibili nel [repository di Draft](https://github.com/Azure/draft/blob/master/docs/install.md).</span><span class="sxs-lookup"><span data-stu-id="e6e91-120">The installation instructions for Draft are in the [Draft repository](https://github.com/Azure/draft/blob/master/docs/install.md).</span></span> <span data-ttu-id="e6e91-121">La procedura è relativamente semplice, ma richiede alcune operazioni di configurazione, in quanto dipende da [Helm](https://aka.ms/helm) per la creazione e la distribuzione di un grafico Helm nel cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="e6e91-121">They are relatively simple, but do require some configuration, as it depends on [Helm](https://aka.ms/helm) to create and deploy a Helm chart into the Kubernetes cluster.</span></span>

1. <span data-ttu-id="e6e91-122">[Scaricare e installare Helm](https://aka.ms/helm#install).</span><span class="sxs-lookup"><span data-stu-id="e6e91-122">[Download and install Helm](https://aka.ms/helm#install).</span></span>
2. <span data-ttu-id="e6e91-123">Usare Helm per cercare e installare `stable/traefik` e il controller di ingresso per abilitare le richieste in ingresso per le compilazioni.</span><span class="sxs-lookup"><span data-stu-id="e6e91-123">Use Helm to search for and install `stable/traefik`, and ingress controller to enable inbound requests for your builds.</span></span>
    ```bash
    $ helm search traefik
    NAME            VERSION DESCRIPTION
    stable/traefik  1.3.0   A Traefik based Kubernetes ingress controller w...

    $ helm install stable/traefik --name ingress
    ```
    <span data-ttu-id="e6e91-124">Impostare quindi un'espressione di controllo sul controller `ingress` per acquisire il valore IP esterno quando viene distribuito.</span><span class="sxs-lookup"><span data-stu-id="e6e91-124">Now set a watch on the `ingress` controller to capture the external IP value when it is deployed.</span></span> <span data-ttu-id="e6e91-125">Questo indirizzo IP sarà quello [mappato al dominio di distribuzione](#wire-up-deployment-domain) nella sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="e6e91-125">This IP address will be the one [mapped to your deployment domain](#wire-up-deployment-domain) in the next section.</span></span>

    ```bash
    kubectl get svc -w
    NAME                          CLUSTER-IP     EXTERNAL-IP     PORT(S)                      AGE
    ingress-traefik               10.0.248.104   13.64.108.240   80:31046/TCP,443:32556/TCP   1h
    kubernetes                    10.0.0.1       <none>          443/TCP                      7h
    ```

    <span data-ttu-id="e6e91-126">In questo caso, l'IP esterno per il dominio di distribuzione è `13.64.108.240`.</span><span class="sxs-lookup"><span data-stu-id="e6e91-126">In this case, the external IP for the deployment domain is `13.64.108.240`.</span></span> <span data-ttu-id="e6e91-127">È ora possibile mappare il dominio a tale IP.</span><span class="sxs-lookup"><span data-stu-id="e6e91-127">Now you can map your domain to that IP.</span></span>

## <a name="wire-up-deployment-domain"></a><span data-ttu-id="e6e91-128">Collegare il dominio di distribuzione</span><span class="sxs-lookup"><span data-stu-id="e6e91-128">Wire up deployment domain</span></span>

<span data-ttu-id="e6e91-129">Draft crea una versione per ogni grafico Helm creato, ovvero ogni applicazione a cui si sta lavorando.</span><span class="sxs-lookup"><span data-stu-id="e6e91-129">Draft creates a release for each Helm chart it creates -- each application you are working on.</span></span> <span data-ttu-id="e6e91-130">Ogni versione ottiene un nome generato, usato da Draft come _sottodominio_ del _dominio di distribuzione_ radice controllato dall'utente.</span><span class="sxs-lookup"><span data-stu-id="e6e91-130">Each one gets a generated name that is used by draft as a _subdomain_ on top of the root _deployment domain_ that you control.</span></span> <span data-ttu-id="e6e91-131">In questo esempio viene usato `squillace.io` come dominio di distribuzione. Per abilitare questo comportamento del sottodominio, è necessario creare un record A per `'*'` nelle voci DNS per il dominio di distribuzione, in modo che venga eseguito il routing di ogni sottodominio generato al controller di ingresso del cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="e6e91-131">(In this example, we use `squillace.io` as the deployment domain.) To enable this subdomain behavior, you must create an A record for `'*'` in your DNS entries for your deployment domain, so that each generated subdomain is routed to the Kubernetes cluster's ingress controller.</span></span>

<span data-ttu-id="e6e91-132">Ogni provider di dominio assegna i server DNS in un modo specifico. Per [delegare i server dei nomi di dominio al servizio DNS di Azure](../../dns/dns-delegate-domain-azure-dns.md), seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="e6e91-132">Your own domain provider has their own way to assign DNS servers; to [delegate your domain nameservers to Azure DNS](../../dns/dns-delegate-domain-azure-dns.md), you take the following steps:</span></span>

1. <span data-ttu-id="e6e91-133">Creare un gruppo di risorse per la propria zona.</span><span class="sxs-lookup"><span data-stu-id="e6e91-133">Create a resource group for your zone.</span></span>
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

2. <span data-ttu-id="e6e91-134">Creare una zona DNS per il proprio dominio.</span><span class="sxs-lookup"><span data-stu-id="e6e91-134">Create a DNS zone for your domain.</span></span>
<span data-ttu-id="e6e91-135">Usare il comando [az network dns zone create](/cli/azure/network/dns/zone#create) per ottenere i server dei nomi per delegare il controllo DNS al servizio DNS di Azure per il dominio.</span><span class="sxs-lookup"><span data-stu-id="e6e91-135">Use the [az network dns zone create](/cli/azure/network/dns/zone#create) command to obtain the nameservers to delegate DNS control to Azure DNS for your domain.</span></span>
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
3. <span data-ttu-id="e6e91-136">Aggiungere i server DNS ottenuti al provider di dominio per il dominio di distribuzione, per poter usare il servizio DNS di Azure per modificare il puntamento del dominio come desiderato.</span><span class="sxs-lookup"><span data-stu-id="e6e91-136">Add the DNS servers you are given to the domain provider for your deployment domain, which enables you to use Azure DNS to repoint your domain as you want.</span></span>
4. <span data-ttu-id="e6e91-137">Creare una voce di recordset A per il mapping del dominio di distribuzione all'IP `ingress` del passaggio 2 della sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="e6e91-137">Create an A record-set entry for your deployment domain mapping to the `ingress` IP from step 2 of the previous section.</span></span>
    ```azurecli
    az network dns record-set a add-record --ipv4-address 13.64.108.240 --record-set-name '*' -g squillace.io -z squillace.io
    ```
<span data-ttu-id="e6e91-138">L'output è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="e6e91-138">The output looks something like:</span></span>
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

5. <span data-ttu-id="e6e91-139">Configurare Draft per usare il registro e creare sottodomini per ogni grafico Helm creato.</span><span class="sxs-lookup"><span data-stu-id="e6e91-139">Configure Draft to use your registry and create subdomains for each Helm chart it creates.</span></span> <span data-ttu-id="e6e91-140">Per configurare Draft sono necessari:</span><span class="sxs-lookup"><span data-stu-id="e6e91-140">To configure Draft, you need:</span></span>
  - <span data-ttu-id="e6e91-141">Il nome del Registro contenitori di Azure (in questo esempio, `draft`)</span><span class="sxs-lookup"><span data-stu-id="e6e91-141">your Azure Container Registry name (in this example, `draft`)</span></span>
  - <span data-ttu-id="e6e91-142">La chiave, o password, del registro da `az acr credential show -n <registry name> --output tsv --query "passwords[0].value"`.</span><span class="sxs-lookup"><span data-stu-id="e6e91-142">your registry key, or password, from `az acr credential show -n <registry name> --output tsv --query "passwords[0].value"`.</span></span>
  - <span data-ttu-id="e6e91-143">Il dominio di distribuzione radice configurato per il mapping all'indirizzo IP esterno di ingresso di Kubernetes (in questo caso, `squillace.io`)</span><span class="sxs-lookup"><span data-stu-id="e6e91-143">the root deployment domain that you have configured to map to the Kubernetes ingress external IP address (here, `squillace.io`)</span></span>

  <span data-ttu-id="e6e91-144">Chiamare `draft init`. Il processo di configurazione chiederà i valori indicati sopra.</span><span class="sxs-lookup"><span data-stu-id="e6e91-144">Call `draft init` and the configuration process prompts you for the values above.</span></span> <span data-ttu-id="e6e91-145">Alla prima esecuzione, il processo è simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="e6e91-145">The process looks something like the following the first time you run it.</span></span>
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

    In order to install Draft, we need a bit more information...

    1. Enter your Docker registry URL (e.g. docker.io, quay.io, myregistry.azurecr.io): draft.azurecr.io
    2. Enter your username: draft
    3. Enter your password:
    4. Enter your org where Draft will push images [draft]: draft
    5. Enter your top-level domain for ingress (e.g. draft.example.com): squillace.io
    Draft has been installed into your Kubernetes Cluster.
    Happy Sailing!
    ```

<span data-ttu-id="e6e91-146">A questo punto, è possibile distribuire un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e6e91-146">Now you're ready to deploy an application.</span></span>


## <a name="build-and-deploy-an-application"></a><span data-ttu-id="e6e91-147">Compilare e distribuire un'applicazione</span><span class="sxs-lookup"><span data-stu-id="e6e91-147">Build and deploy an application</span></span>

<span data-ttu-id="e6e91-148">Nel repository di Draft ci sono [sei semplici applicazioni di esempio](https://github.com/Azure/draft/tree/master/examples).</span><span class="sxs-lookup"><span data-stu-id="e6e91-148">In the Draft repo are [six simple example applications](https://github.com/Azure/draft/tree/master/examples).</span></span> <span data-ttu-id="e6e91-149">Clonare il repository e usare l'[esempio Python](https://github.com/Azure/draft/tree/master/examples/python).</span><span class="sxs-lookup"><span data-stu-id="e6e91-149">Clone the repo and let's use the [Python example](https://github.com/Azure/draft/tree/master/examples/python).</span></span> <span data-ttu-id="e6e91-150">Passare alla directory examples/Python e digitare `draft create` per compilare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e6e91-150">Change into the examples/Python directory, and type `draft create` to build the application.</span></span> <span data-ttu-id="e6e91-151">Il risultato dovrebbe essere simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="e6e91-151">It should look like the following example.</span></span>
```bash
$ draft create
--> Python app detected
--> Ready to sail
```

<span data-ttu-id="e6e91-152">L'output include un Dockerfile e un grafico Helm.</span><span class="sxs-lookup"><span data-stu-id="e6e91-152">The output includes a Dockerfile and a Helm chart.</span></span> <span data-ttu-id="e6e91-153">Per la compilazione e la distribuzione è sufficiente digitare `draft up`.</span><span class="sxs-lookup"><span data-stu-id="e6e91-153">To build and deploy, you just type `draft up`.</span></span> <span data-ttu-id="e6e91-154">L'output è vasto, ma inizia in modo analogo all'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="e6e91-154">The output is extensive, but begins like the following example.</span></span>
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

<span data-ttu-id="e6e91-155">E, in caso di esito positivo, termina in modo analogo all'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="e6e91-155">and when successful ends with something similar to the following example.</span></span>
```bash
ab68189731eb: Pushed
53c0ab0341bee12d01be3d3c192fbd63562af7f1: digest: sha256:bb0450ec37acf67ed461c1512ef21f58a500ff9326ce3ec623ce1e4427df9765 size: 2841
--> Deploying to Kubernetes
--> Status: DEPLOYED
--> Notes:

  http://gangly-bronco.squillace.io to access your application

Watching local files for changes...
```

<span data-ttu-id="e6e91-156">Qualunque sia il nome del grafico, è ora possibile usare il comando `curl http://gangly-bronco.squillace.io` per ricevere la risposta `Hello World!`.</span><span class="sxs-lookup"><span data-stu-id="e6e91-156">Whatever your chart's name is, you can now `curl http://gangly-bronco.squillace.io` to receive the reply, `Hello World!`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e6e91-157">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e6e91-157">Next steps</span></span>

<span data-ttu-id="e6e91-158">Ora che è stato creato un cluster Kubernetes ACS, è possibile provare a usare il [Registro contenitori di Azure](../../container-registry/container-registry-intro.md) per creare altre distribuzioni diverse di questo scenario.</span><span class="sxs-lookup"><span data-stu-id="e6e91-158">Now that you have an ACS Kubernetes cluster, you can investigate using [Azure Container Registry](../../container-registry/container-registry-intro.md) to create more and different deployments of this scenario.</span></span> <span data-ttu-id="e6e91-159">È ad esempio possibile creare un recordset DNS di dominio draft._basedomain.toplevel_ che controlla le attività all'esterno di un sottodominio più profondo per distribuzioni specifiche del servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="e6e91-159">For example, you can create a draft._basedomain.toplevel_ domain DNS record-set that controls things off of a deeper subdomain for specific ACS deployments.</span></span>






