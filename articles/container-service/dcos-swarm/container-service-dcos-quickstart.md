---
title: aaaAzure avvio rapido del servizio contenitore - distribuire controller di dominio o del sistema operativo Cluster | Documenti Microsoft
description: Guida rapida al servizio contenitore di Azure - Distribuire un cluster DC/OS
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, contenitori, Micro-Service, Kubernetes, DC/OS, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: b961f15bd73deeafda5a3fc25ab53c839195219b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-dcos-cluster"></a><span data-ttu-id="92eaf-104">Distribuire un cluster DC/OS</span><span class="sxs-lookup"><span data-stu-id="92eaf-104">Deploy a DC/OS cluster</span></span>

<span data-ttu-id="92eaf-105">DC/OS fornisce una piattaforma distribuita per l'esecuzione di applicazioni in contenitori e moderne.</span><span class="sxs-lookup"><span data-stu-id="92eaf-105">DC/OS provides a distributed platform for running modern and containerized applications.</span></span> <span data-ttu-id="92eaf-106">Con il servizio contenitore di Azure, il provisioning di un cluster DC/OS pronto per la produzione è semplice e rapido.</span><span class="sxs-lookup"><span data-stu-id="92eaf-106">With Azure Container Service, provisioning of a production ready DC/OS cluster is simple and quick.</span></span> <span data-ttu-id="92eaf-107">Questo passaggi di base di avvio rapido dettagli hello necessari toodeploy un cluster di controller di dominio o del sistema operativo e un carico di lavoro di base esecuzione.</span><span class="sxs-lookup"><span data-stu-id="92eaf-107">This quick start details hello basic steps needed toodeploy a DC/OS cluster and run basic workload.</span></span>

<span data-ttu-id="92eaf-108">Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="92eaf-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="92eaf-109">Questa esercitazione richiede hello Azure CLI versione 2.0.4 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="92eaf-109">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="92eaf-110">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="92eaf-110">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="92eaf-111">Se è necessario tooupgrade, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="92eaf-111">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="log-in-tooazure"></a><span data-ttu-id="92eaf-112">Accedi tooAzure</span><span class="sxs-lookup"><span data-stu-id="92eaf-112">Log in tooAzure</span></span> 

<span data-ttu-id="92eaf-113">Accedere alla sottoscrizione di Azure con hello tooyour [accesso az](/cli/azure/#login) comando e seguire hello le direzioni.</span><span class="sxs-lookup"><span data-stu-id="92eaf-113">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span>

```azurecli
az login
```

## <a name="create-a-resource-group"></a><span data-ttu-id="92eaf-114">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="92eaf-114">Create a resource group</span></span>

<span data-ttu-id="92eaf-115">Creare un gruppo di risorse con hello [gruppo az creare](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="92eaf-115">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="92eaf-116">Un gruppo di risorse di Azure è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite.</span><span class="sxs-lookup"><span data-stu-id="92eaf-116">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="92eaf-117">esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *eastus* percorso.</span><span class="sxs-lookup"><span data-stu-id="92eaf-117">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-dcos-cluster"></a><span data-ttu-id="92eaf-118">Creare un cluster DC/OS</span><span class="sxs-lookup"><span data-stu-id="92eaf-118">Create DC/OS cluster</span></span>

<span data-ttu-id="92eaf-119">Creare un cluster di controller di dominio o del sistema operativo con hello [az acs creare](/cli/azure/acs#create) comando.</span><span class="sxs-lookup"><span data-stu-id="92eaf-119">Create a DC/OS cluster with hello [az acs create](/cli/azure/acs#create) command.</span></span>

<span data-ttu-id="92eaf-120">esempio Hello crea un cluster di controller di dominio o del sistema operativo denominato *myDCOSCluster* e crea le chiavi SSH se non esiste già.</span><span class="sxs-lookup"><span data-stu-id="92eaf-120">hello following example creates a DC/OS cluster named *myDCOSCluster* and creates SSH keys if they do not already exist.</span></span> <span data-ttu-id="92eaf-121">toouse uno specifico set di chiavi, utilizzare hello `--ssh-key-value` opzione.</span><span class="sxs-lookup"><span data-stu-id="92eaf-121">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

```azurecli
az acs create \
  --orchestrator-type dcos \
  --resource-group myResourceGroup \
  --name myDCOSCluster \
  --generate-ssh-keys
```

<span data-ttu-id="92eaf-122">Dopo alcuni minuti, comando hello completa e restituisce informazioni sulla distribuzione di hello.</span><span class="sxs-lookup"><span data-stu-id="92eaf-122">After several minutes, hello command completes, and returns information about hello deployment.</span></span>

## <a name="connect-toodcos-cluster"></a><span data-ttu-id="92eaf-123">Connettere il cluster tooDC/OS</span><span class="sxs-lookup"><span data-stu-id="92eaf-123">Connect tooDC/OS cluster</span></span>

<span data-ttu-id="92eaf-124">Dopo aver creato un cluster DC/OS, è possibile accedervi tramite un tunnel SSH.</span><span class="sxs-lookup"><span data-stu-id="92eaf-124">Once a DC/OS cluster has been created, it can be accesses through an SSH tunnel.</span></span> <span data-ttu-id="92eaf-125">Comando che segue di esecuzione hello tooreturn hello indirizzo IP pubblico del database master di controller di dominio/OS hello.</span><span class="sxs-lookup"><span data-stu-id="92eaf-125">Run hello following command tooreturn hello public IP address of hello DC/OS master.</span></span> <span data-ttu-id="92eaf-126">Questo indirizzo IP è archiviato in una variabile e usato nel passaggio successivo hello.</span><span class="sxs-lookup"><span data-stu-id="92eaf-126">This IP address is stored in a variable and used in hello next step.</span></span>

```azurecli
ip=$(az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-master')].[ipAddress]" -o tsv)
```

<span data-ttu-id="92eaf-127">toocreate hello tunnel SSH, eseguire hello comando seguente e istruzioni hello sullo schermo.</span><span class="sxs-lookup"><span data-stu-id="92eaf-127">toocreate hello SSH tunnel, run hello following command and follow hello on-screen instructions.</span></span> <span data-ttu-id="92eaf-128">Se la porta 80 è già in uso, il comando hello ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="92eaf-128">If port 80 is already in use, hello command fails.</span></span> <span data-ttu-id="92eaf-129">Hello aggiornamento tunneled tooone porta non è in uso, ad esempio `85:localhost:80`.</span><span class="sxs-lookup"><span data-stu-id="92eaf-129">Update hello tunneled port tooone not in use, such as `85:localhost:80`.</span></span> 

```azurecli
sudo ssh -i ~/.ssh/id_rsa -fNL 80:localhost:80 -p 2200 azureuser@$ip
```

<span data-ttu-id="92eaf-130">può essere testato tunnel SSH Hello esplorando troppo`http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="92eaf-130">hello SSH tunnel can be tested by browsing too`http://localhost`.</span></span> <span data-ttu-id="92eaf-131">Se una porta altro che è stata utilizzata 80, modificare toomatch percorso hello.</span><span class="sxs-lookup"><span data-stu-id="92eaf-131">If a port other that 80 has been used, adjust hello location toomatch.</span></span> 

<span data-ttu-id="92eaf-132">Se tunnel SSH hello è stato creato correttamente, viene restituito il portale di controller di dominio/OS hello.</span><span class="sxs-lookup"><span data-stu-id="92eaf-132">If hello SSH tunnel was successfully created, hello DC/OS portal is returned.</span></span>

![Interfaccia utente di DC/OS](./media/container-service-dcos-quickstart/dcos-ui.png)

## <a name="install-dcos-cli"></a><span data-ttu-id="92eaf-134">Installare l'interfaccia della riga di comando di DC/OS</span><span class="sxs-lookup"><span data-stu-id="92eaf-134">Install DC/OS CLI</span></span>

<span data-ttu-id="92eaf-135">interfaccia della riga di comando DC/OS Hello è toomanage usato un cluster di controller di dominio o del sistema operativo da hello della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="92eaf-135">hello DC/OS command line interface is used toomanage a DC/OS cluster from hello command-line.</span></span> <span data-ttu-id="92eaf-136">Installare hello cli di controller di dominio/OS utilizzando hello [az acs dcos install-cli](/azure/acs/dcos#install-cli) comando.</span><span class="sxs-lookup"><span data-stu-id="92eaf-136">Install hello DC/OS cli using hello [az acs dcos install-cli](/azure/acs/dcos#install-cli) command.</span></span> <span data-ttu-id="92eaf-137">Se si utilizza Azure CloudShell, hello CLI di controller di dominio o del sistema operativo è già installato.</span><span class="sxs-lookup"><span data-stu-id="92eaf-137">If you are using Azure CloudShell, hello DC/OS CLI is already installed.</span></span> 

<span data-ttu-id="92eaf-138">Se si esegue hello CLI di Azure in macOS o Linux, potrebbe essere comando hello toorun con sudo.</span><span class="sxs-lookup"><span data-stu-id="92eaf-138">If you are running hello Azure CLI on macOS or Linux, you might need toorun hello command with sudo.</span></span>

```azurecli
az acs dcos install-cli
```

<span data-ttu-id="92eaf-139">Prima di hello che CLI può essere utilizzato con i cluster di hello, deve essere tunnel SSH di hello toouse configurato.</span><span class="sxs-lookup"><span data-stu-id="92eaf-139">Before hello CLI can be used with hello cluster, it must be configured toouse hello SSH tunnel.</span></span> <span data-ttu-id="92eaf-140">toodo in tal caso, eseguire hello comando seguente, modificare la porta hello se necessario.</span><span class="sxs-lookup"><span data-stu-id="92eaf-140">toodo so, run hello following command, adjusting hello port if needed.</span></span>

```azurecli
dcos config set core.dcos_url http://localhost
```

## <a name="run-an-application"></a><span data-ttu-id="92eaf-141">Eseguire un'applicazione</span><span class="sxs-lookup"><span data-stu-id="92eaf-141">Run an application</span></span>

<span data-ttu-id="92eaf-142">valore predefinito di Hello meccanismo per un cluster ACS controller di dominio o del sistema operativo di pianificazione è maratona.</span><span class="sxs-lookup"><span data-stu-id="92eaf-142">hello default scheduling mechanism for an ACS DC/OS cluster is Marathon.</span></span> <span data-ttu-id="92eaf-143">Maratona toostart utilizzata un'applicazione e gestire lo stato di hello di un'applicazione hello nel cluster di controller di dominio/OS hello.</span><span class="sxs-lookup"><span data-stu-id="92eaf-143">Marathon is used toostart an application and manage hello state of hello application on hello DC/OS cluster.</span></span> <span data-ttu-id="92eaf-144">tooschedule un'applicazione tramite maratona, creare un file denominato *maratona app.json*, e hello copia seguendo contenuto al suo interno.</span><span class="sxs-lookup"><span data-stu-id="92eaf-144">tooschedule an application through Marathon, create a file named *marathon-app.json*, and copy hello following contents into it.</span></span> 

```json
{
  "id": "demo-app",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 1,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "hostPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  },
  "acceptedResourceRoles": [
    "slave_public"
  ]
}
```

<span data-ttu-id="92eaf-145">Eseguire hello successivo comando tooschedule hello applicazione toorun nel cluster di controller di dominio/OS hello.</span><span class="sxs-lookup"><span data-stu-id="92eaf-145">Run hello following command tooschedule hello application toorun on hello DC/OS cluster.</span></span>

```azurecli
dcos marathon app add marathon-app.json
```

<span data-ttu-id="92eaf-146">stato della distribuzione toosee hello per le app di hello, eseguire hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="92eaf-146">toosee hello deployment status for hello app, run hello following command.</span></span>

```azurecli
dcos marathon app list
```

<span data-ttu-id="92eaf-147">Quando hello **in attesa** passa il valore di colonna da *True* troppo*False*, la distribuzione di applicazioni è stata completata.</span><span class="sxs-lookup"><span data-stu-id="92eaf-147">When hello **WAITING** column value switches from *True* too*False*, application deployment has completed.</span></span>

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     1/1    ---       ---      False      DOCKER   None
```

<span data-ttu-id="92eaf-148">Ottenere l'indirizzo IP pubblico hello degli agenti di hello controller di dominio o del sistema operativo cluster.</span><span class="sxs-lookup"><span data-stu-id="92eaf-148">Get hello public IP address of hello DC/OS cluster agents.</span></span>

```azurecli
az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-agent')].[ipAddress]" -o tsv
```

<span data-ttu-id="92eaf-149">Esplorazione toothis indirizzo restituisce sito NGINX di hello predefinito.</span><span class="sxs-lookup"><span data-stu-id="92eaf-149">Browsing toothis address returns hello default NGINX site.</span></span>

![NGINX](./media/container-service-dcos-quickstart/nginx.png)

## <a name="delete-dcos-cluster"></a><span data-ttu-id="92eaf-151">Eliminare il cluster DC/OS</span><span class="sxs-lookup"><span data-stu-id="92eaf-151">Delete DC/OS cluster</span></span>

<span data-ttu-id="92eaf-152">Quando non è più necessario, è possibile utilizzare hello [eliminazione gruppo az](/cli/azure/group#delete) comandi tooremove gruppo di risorse hello, cluster/OS di controller di dominio e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="92eaf-152">When no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, DC/OS cluster, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --no-wait
```

## <a name="next-steps"></a><span data-ttu-id="92eaf-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="92eaf-153">Next steps</span></span>

<span data-ttu-id="92eaf-154">In questa Guida introduttiva, è stato distribuito un cluster di controller di dominio o del sistema operativo e l'esecuzione un semplice contenitore Docker in cluster hello.</span><span class="sxs-lookup"><span data-stu-id="92eaf-154">In this quick start, you’ve deployed a DC/OS cluster and have run a simple Docker container on hello cluster.</span></span> <span data-ttu-id="92eaf-155">toolearn ulteriori informazioni su servizio di contenitore di Azure, continuare esercitazioni toohello ACS.</span><span class="sxs-lookup"><span data-stu-id="92eaf-155">toolearn more about Azure Container Service, continue toohello ACS tutorials.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="92eaf-156">Gestire un cluster DC/OS del servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="92eaf-156">Manage an ACS DC/OS Cluster</span></span>](container-service-dcos-manage-tutorial.md)