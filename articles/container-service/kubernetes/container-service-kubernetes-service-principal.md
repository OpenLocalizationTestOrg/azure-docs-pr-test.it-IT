---
title: "entità aaaService per cluster di Azure Kubernetes | Documenti Microsoft"
description: "Creare e gestire un'entità servizio di Azure Active Directory per un cluster Kubernetes nel servizio contenitore di Azure"
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/08/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 7a01624c5ac3fa717dbcbd570e05ceb4d917c53a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-an-azure-ad-service-principal-for-a-kubernetes-cluster-in-container-service"></a><span data-ttu-id="d4641-103">Configurare un'entità servizio di Azure AD per un cluster Kubernetes nel servizio contenitore</span><span class="sxs-lookup"><span data-stu-id="d4641-103">Set up an Azure AD service principal for a Kubernetes cluster in Container Service</span></span>


<span data-ttu-id="d4641-104">Nel servizio contenitore di Azure, è necessario un cluster Kubernetes un [dell'entità servizio di Azure Active Directory](../../active-directory/develop/active-directory-application-objects.md) toointeract con le API di Azure.</span><span class="sxs-lookup"><span data-stu-id="d4641-104">In Azure Container Service, a Kubernetes cluster requires an [Azure Active Directory service principal](../../active-directory/develop/active-directory-application-objects.md) toointeract with Azure APIs.</span></span> <span data-ttu-id="d4641-105">Hello dell'entità servizio è necessario toodynamically gestire le risorse, ad esempio [le route definite dall'utente](../../virtual-network/virtual-networks-udr-overview.md) hello e [servizio di bilanciamento del carico di Azure di livello 4](../../load-balancer/load-balancer-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d4641-105">hello service principal is needed toodynamically manage resources such as [user-defined routes](../../virtual-network/virtual-networks-udr-overview.md) and hello [Layer 4 Azure Load Balancer](../../load-balancer/load-balancer-overview.md).</span></span> 


<span data-ttu-id="d4641-106">Questo articolo illustra tooset diverse opzioni di un servizio principale per il cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="d4641-106">This article shows different options tooset up a service principal for your Kubernetes cluster.</span></span> <span data-ttu-id="d4641-107">Ad esempio, se è installato e configurato hello [CLI di Azure 2.0](/cli/azure/install-az-cli2), è possibile eseguire hello [ `az acs create` ](/cli/azure/acs#create) comando toocreate hello Kubernetes cluster e hello entità servizio in hello contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="d4641-107">For example, if you installed and set up hello [Azure CLI 2.0](/cli/azure/install-az-cli2), you can run hello [`az acs create`](/cli/azure/acs#create) command toocreate hello Kubernetes cluster and hello service principal at hello same time.</span></span>


## <a name="requirements-for-hello-service-principal"></a><span data-ttu-id="d4641-108">Requisiti per l'entità servizio hello</span><span class="sxs-lookup"><span data-stu-id="d4641-108">Requirements for hello service principal</span></span>

<span data-ttu-id="d4641-109">È possibile utilizzare un'entità servizio di Azure AD esistente, che soddisfa hello seguenti requisiti o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="d4641-109">You can use an existing Azure AD service principal that meets hello following requirements, or create a new one.</span></span>

* <span data-ttu-id="d4641-110">**Ambito**: gruppo di risorse hello nella sottoscrizione hello utilizzato cluster Kubernetes di hello toodeploy, o (meno correggono) sottoscrizione hello cluster hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="d4641-110">**Scope**: hello resource group in hello subscription used toodeploy hello Kubernetes cluster, or (less restrictively) hello subscription used toodeploy hello cluster.</span></span>

* <span data-ttu-id="d4641-111">**Ruolo**: **Collaboratore**.</span><span class="sxs-lookup"><span data-stu-id="d4641-111">**Role**: **Contributor**</span></span>

* <span data-ttu-id="d4641-112">**Segreto client**: deve essere una password.</span><span class="sxs-lookup"><span data-stu-id="d4641-112">**Client secret**: must be a password.</span></span> <span data-ttu-id="d4641-113">Non è attualmente possibile usare un'entità servizio configurata per l'autenticazione del certificato.</span><span class="sxs-lookup"><span data-stu-id="d4641-113">Currently, you can't use a service principal set up for certificate authentication.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="d4641-114">toocreate un'entità servizio, è necessario disporre delle autorizzazioni tooregister un'applicazione con il tenant di Azure AD e ruolo di tooa applicazione hello tooassign nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="d4641-114">toocreate a service principal, you must have permissions tooregister an application with your Azure AD tenant, and tooassign hello application tooa role in your subscription.</span></span> <span data-ttu-id="d4641-115">toosee se si dispone delle autorizzazioni necessarie hello, [archivia hello portale](../../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions).</span><span class="sxs-lookup"><span data-stu-id="d4641-115">toosee if you have hello required permissions, [check in hello Portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions).</span></span> 
>

## <a name="option-1-create-a-service-principal-in-azure-ad"></a><span data-ttu-id="d4641-116">Opzione 1: creare un'entità servizio in Azure AD</span><span class="sxs-lookup"><span data-stu-id="d4641-116">Option 1: Create a service principal in Azure AD</span></span>

<span data-ttu-id="d4641-117">Se si desidera toocreate un'entità servizio di Azure AD prima di distribuire il cluster Kubernetes, Azure fornisce diversi metodi.</span><span class="sxs-lookup"><span data-stu-id="d4641-117">If you want toocreate an Azure AD service principal before you deploy your Kubernetes cluster, Azure provides several methods.</span></span> 

<span data-ttu-id="d4641-118">Hello comandi di esempio seguenti illustrano come toodo con hello [CLI di Azure 2.0](../../azure-resource-manager/resource-group-authenticate-service-principal-cli.md).</span><span class="sxs-lookup"><span data-stu-id="d4641-118">hello following example commands show you how toodo this with hello [Azure CLI 2.0](../../azure-resource-manager/resource-group-authenticate-service-principal-cli.md).</span></span> <span data-ttu-id="d4641-119">In alternativa creare un servizio principale utilizzando [Azure PowerShell](../../azure-resource-manager/resource-group-authenticate-service-principal.md), hello [portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md), o altri metodi.</span><span class="sxs-lookup"><span data-stu-id="d4641-119">You can alternatively create a service principal using [Azure PowerShell](../../azure-resource-manager/resource-group-authenticate-service-principal.md), hello [portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md), or other methods.</span></span>

```azurecli
az login

az account set --subscription "mySubscriptionID"

az group create -n "myResourceGroupName" -l "westus"

az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/mySubscriptionID/resourceGroups/myResourceGroupName"
```

<span data-ttu-id="d4641-120">L'output è simile seguente toohello (illustrato di seguito redatta):</span><span class="sxs-lookup"><span data-stu-id="d4641-120">Output is similar toohello following (shown here redacted):</span></span>

![Creare un’entità servizio](./media/container-service-kubernetes-service-principal/service-principal-creds.png)

<span data-ttu-id="d4641-122">Sono hello **ID client** (`appId`) e hello **segreto client** (`password`) utilizzati come parametri dell'entità servizio per la distribuzione di cluster.</span><span class="sxs-lookup"><span data-stu-id="d4641-122">Highlighted are hello **client ID** (`appId`) and hello **client secret** (`password`) that you use as service principal parameters for cluster deployment.</span></span>


### <a name="specify-service-principal-when-creating-hello-kubernetes-cluster"></a><span data-ttu-id="d4641-123">Specificare l'entità servizio durante la creazione di cluster Kubernetes hello</span><span class="sxs-lookup"><span data-stu-id="d4641-123">Specify service principal when creating hello Kubernetes cluster</span></span>

<span data-ttu-id="d4641-124">Fornire hello **ID client** (detto anche hello `appId`, per l'ID applicazione) e **segreto client** (`password`) di un'entità come parametri quando si crea hello servizio esistente Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="d4641-124">Provide hello **client ID** (also called hello `appId`, for Application ID) and **client secret** (`password`) of an existing service principal as parameters when you create hello Kubernetes cluster.</span></span> <span data-ttu-id="d4641-125">Assicurarsi che un'entità servizio hello soddisfi i requisiti di hello in hello a partire da questo articolo.</span><span class="sxs-lookup"><span data-stu-id="d4641-125">Make sure hello service principal meets hello requirements at hello beginning this article.</span></span>

<span data-ttu-id="d4641-126">È possibile specificare questi parametri quando si distribuiscono cluster Kubernetes hello utilizzando hello [Azure interfaccia della riga di comando (CLI) 2.0](container-service-kubernetes-walkthrough.md), [portale di Azure](../dcos-swarm/container-service-deployment.md), o altri metodi.</span><span class="sxs-lookup"><span data-stu-id="d4641-126">You can specify these parameters when deploying hello Kubernetes cluster using hello [Azure Command-Line Interface (CLI) 2.0](container-service-kubernetes-walkthrough.md), [Azure portal](../dcos-swarm/container-service-deployment.md), or other methods.</span></span>

>[!TIP] 
><span data-ttu-id="d4641-127">Quando si specifica hello **ID client**, hello toouse assicurarsi di essere `appId`, non hello `ObjectId`, dell'entità servizio hello.</span><span class="sxs-lookup"><span data-stu-id="d4641-127">When specifying hello **client ID**, be sure toouse hello `appId`, not hello `ObjectId`, of hello service principal.</span></span>
>

<span data-ttu-id="d4641-128">Hello esempio seguente viene illustrato un modo toopass parametri hello con hello CLI di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="d4641-128">hello following example shows one way toopass hello parameters with hello Azure CLI 2.0.</span></span> <span data-ttu-id="d4641-129">Questo esempio viene utilizzato hello [Kubernetes delle Guide rapide modello](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes).</span><span class="sxs-lookup"><span data-stu-id="d4641-129">This example uses hello [Kubernetes quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes).</span></span>

1. <span data-ttu-id="d4641-130">[Scaricare](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.parameters.json) file dei parametri di modello hello `azuredeploy.parameters.json` da GitHub.</span><span class="sxs-lookup"><span data-stu-id="d4641-130">[Download](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.parameters.json) hello template parameters file `azuredeploy.parameters.json` from GitHub.</span></span>

2. <span data-ttu-id="d4641-131">servizio hello toospecify principale, immettere i valori per `servicePrincipalClientId` e `servicePrincipalClientSecret` nel file hello.</span><span class="sxs-lookup"><span data-stu-id="d4641-131">toospecify hello service principal, enter values for `servicePrincipalClientId` and `servicePrincipalClientSecret` in hello file.</span></span> <span data-ttu-id="d4641-132">(È anche necessario tooprovide i propri valori per `dnsNamePrefix` e `sshRSAPublicKey`.</span><span class="sxs-lookup"><span data-stu-id="d4641-132">(You also need tooprovide your own values for `dnsNamePrefix` and `sshRSAPublicKey`.</span></span> <span data-ttu-id="d4641-133">Hello quest'ultimo è cluster hello tooaccess chiave pubblica SSH di hello). Salvare il file hello.</span><span class="sxs-lookup"><span data-stu-id="d4641-133">hello latter is hello SSH public key tooaccess hello cluster.) Save hello file.</span></span>

    ![Passare i parametri dell'entità servizio](./media/container-service-kubernetes-service-principal/service-principal-params.png)

3. <span data-ttu-id="d4641-135">Hello esecuzione comando seguente, usando `--parameters` tooset hello percorso toohello azuredeploy.parameters.json file.</span><span class="sxs-lookup"><span data-stu-id="d4641-135">Run hello following command, using `--parameters` tooset hello path toohello azuredeploy.parameters.json file.</span></span> <span data-ttu-id="d4641-136">Questo comando consente di distribuire cluster hello in un gruppo di risorse creato chiamato `myResourceGroup` nell'area Stati Uniti occidentali hello.</span><span class="sxs-lookup"><span data-stu-id="d4641-136">This command deploys hello cluster in a resource group you create called `myResourceGroup` in hello West US region.</span></span>

    ```azurecli
    az login

    az account set --subscription "mySubscriptionID"

    az group create --name "myResourceGroup" --location "westus" 
    
    az group deployment create -g "myResourceGroup" --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.json" --parameters @azuredeploy.parameters.json
    ```


## <a name="option-2-generate-a-service-principal-when-creating-hello-cluster-with-az-acs-create"></a><span data-ttu-id="d4641-137">Opzione 2: Generare un'entità servizio durante la creazione di cluster hello con`az acs create`</span><span class="sxs-lookup"><span data-stu-id="d4641-137">Option 2: Generate a service principal when creating hello cluster with `az acs create`</span></span>

<span data-ttu-id="d4641-138">Se si esegue hello [ `az acs create` ](/cli/azure/acs#create) toocreate comando hello Kubernetes cluster, è necessario hello opzione toogenerate un'entità servizio automaticamente.</span><span class="sxs-lookup"><span data-stu-id="d4641-138">If you run hello [`az acs create`](/cli/azure/acs#create) command toocreate hello Kubernetes cluster, you have hello option toogenerate a service principal automatically.</span></span>

<span data-ttu-id="d4641-139">Analogamente alle altre opzioni di creazione del cluster Kubernetes, è possibile specificare i parametri per un'entità servizio esistente quando si esegue `az acs create`.</span><span class="sxs-lookup"><span data-stu-id="d4641-139">As with other Kubernetes cluster creation options, you can specify parameters for an existing service principal when you run `az acs create`.</span></span> <span data-ttu-id="d4641-140">Tuttavia, quando si omettono i parametri, hello CLI di Azure viene creata una automaticamente per l'utilizzo con il servizio di contenitore.</span><span class="sxs-lookup"><span data-stu-id="d4641-140">However, when you omit these parameters, hello Azure CLI creates one automatically for use with Container Service.</span></span> <span data-ttu-id="d4641-141">Questo avviene in modo trasparente durante la distribuzione di hello.</span><span class="sxs-lookup"><span data-stu-id="d4641-141">This takes place transparently during hello deployment.</span></span> 

<span data-ttu-id="d4641-142">Hello seguente comando crea un cluster Kubernetes e genera le chiavi SSH e le credenziali dell'entità servizio:</span><span class="sxs-lookup"><span data-stu-id="d4641-142">hello following command creates a Kubernetes cluster and generates both SSH keys and service principal credentials:</span></span>

```console
az acs create -n myClusterName -d myDNSPrefix -g myResourceGroup --generate-ssh-keys --orchestrator-type kubernetes
```

> [!IMPORTANT]
> <span data-ttu-id="d4641-143">Se l'account non dispone di hello Azure AD e sottoscrizione autorizzazioni toocreate un'entità servizio, il comando hello genera un errore simile troppo`Insufficient privileges toocomplete hello operation.`</span><span class="sxs-lookup"><span data-stu-id="d4641-143">If your account doesn't have hello Azure AD and subscription permissions toocreate a service principal, hello command generates an error similar too`Insufficient privileges toocomplete hello operation.`</span></span>
> 

## <a name="additional-considerations"></a><span data-ttu-id="d4641-144">Considerazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="d4641-144">Additional considerations</span></span>

* <span data-ttu-id="d4641-145">Se non si dispone delle autorizzazioni toocreate un'entità servizio nella sottoscrizione, potrebbe essere necessario tooask Azure AD o sottoscrizione amministratore tooassign hello delle autorizzazioni necessarie o chiedere un toouse dell'entità servizio con il servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="d4641-145">If you don't have permissions toocreate a service principal in your subscription, you might need tooask your Azure AD or subscription administrator tooassign hello necessary permissions, or ask them for a service principal toouse with Azure Container Service.</span></span> 

* <span data-ttu-id="d4641-146">entità servizio Hello per Kubernetes è una parte hello della configurazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="d4641-146">hello service principal for Kubernetes is a part of hello cluster configuration.</span></span> <span data-ttu-id="d4641-147">Tuttavia, non utilizzare cluster di hello identità toodeploy hello.</span><span class="sxs-lookup"><span data-stu-id="d4641-147">However, don't use hello identity toodeploy hello cluster.</span></span>

* <span data-ttu-id="d4641-148">Ogni entità servizio è associata a un'applicazione Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d4641-148">Every service principal is associated with an Azure AD application.</span></span> <span data-ttu-id="d4641-149">Hello dell'entità servizio per un cluster Kubernetes può essere associata a qualsiasi valido di Azure nome applicazione Active Directory (ad esempio: `https://www.contoso.org/example`).</span><span class="sxs-lookup"><span data-stu-id="d4641-149">hello service principal for a Kubernetes cluster can be associated with any valid Azure AD application name (for example: `https://www.contoso.org/example`).</span></span> <span data-ttu-id="d4641-150">Hello URL per un'applicazione hello privo di toobe un endpoint di tipo real.</span><span class="sxs-lookup"><span data-stu-id="d4641-150">hello URL for hello application doesn't have toobe a real endpoint.</span></span>

* <span data-ttu-id="d4641-151">Quando si specifica un'entità servizio hello **ID Client**, è possibile utilizzare il valore di hello di hello `appId` (come illustrato in questo articolo) o entità servizio corrispondente hello `name` (ad esempio,`https://www.contoso.org/example`).</span><span class="sxs-lookup"><span data-stu-id="d4641-151">When specifying hello service principal **Client ID**, you can use hello value of hello `appId` (as shown in this article) or hello corresponding service principal `name` (for example,`https://www.contoso.org/example`).</span></span>

* <span data-ttu-id="d4641-152">Nel master hello e agente di macchine virtuali in cluster Kubernetes hello, vengono archiviate le credenziali dell'entità servizio di hello in /etc/kubernetes/azure.json file hello.</span><span class="sxs-lookup"><span data-stu-id="d4641-152">On hello master and agent VMs in hello Kubernetes cluster, hello service principal credentials are stored in hello file /etc/kubernetes/azure.json.</span></span>

* <span data-ttu-id="d4641-153">Quando si utilizza hello `az acs create` comando dell'entità servizio di hello toogenerate automaticamente, le credenziali dell'entità servizio di hello vengono scritti toohello file ~/.azure/acsServicePrincipal.json computer hello utilizzato comando hello toorun.</span><span class="sxs-lookup"><span data-stu-id="d4641-153">When you use hello `az acs create` command toogenerate hello service principal automatically, hello service principal credentials are written toohello file ~/.azure/acsServicePrincipal.json on hello machine used toorun hello command.</span></span> 

* <span data-ttu-id="d4641-154">Quando si utilizza hello `az acs create` comando dell'entità servizio di hello toogenerate automaticamente, entità servizio hello possono anche eseguire l'autenticazione con un [Registro di sistema di contenitore di Azure](../../container-registry/container-registry-intro.md) creato in hello stessa sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="d4641-154">When you use hello `az acs create` command toogenerate hello service principal automatically, hello service principal can also authenticate with an [Azure container registry](../../container-registry/container-registry-intro.md) created in hello same subscription.</span></span>




## <a name="next-steps"></a><span data-ttu-id="d4641-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d4641-155">Next steps</span></span>

* <span data-ttu-id="d4641-156">[Introduzione a Kubernetes](container-service-kubernetes-walkthrough.md) nel cluster del servizio contenitore.</span><span class="sxs-lookup"><span data-stu-id="d4641-156">[Get started with Kubernetes](container-service-kubernetes-walkthrough.md) in your container service cluster.</span></span>

* <span data-ttu-id="d4641-157">tootroubleshoot hello entità servizio per Kubernetes, vedere hello [documentazione del motore di ACS](https://github.com/Azure/acs-engine/blob/master/docs/kubernetes.md#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="d4641-157">tootroubleshoot hello service principal for Kubernetes, see hello [ACS Engine documentation](https://github.com/Azure/acs-engine/blob/master/docs/kubernetes.md#troubleshooting).</span></span>


