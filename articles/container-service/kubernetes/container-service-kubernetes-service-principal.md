---
title: "Entità servizio per cluster Azure Kubernetes | Documentazione Microsoft"
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
ms.openlocfilehash: 37171b4e69ad7d8c41ca8e7475c33ce70379f484
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="set-up-an-azure-ad-service-principal-for-a-kubernetes-cluster-in-container-service"></a><span data-ttu-id="f9a32-103">Configurare un'entità servizio di Azure AD per un cluster Kubernetes nel servizio contenitore</span><span class="sxs-lookup"><span data-stu-id="f9a32-103">Set up an Azure AD service principal for a Kubernetes cluster in Container Service</span></span>


<span data-ttu-id="f9a32-104">Un cluster Kubernetes richiede un'[entità servizio di Azure Active Directory](../../active-directory/develop/active-directory-application-objects.md) nel servizio contenitore di Azure per l'interazione con le API di Azure.</span><span class="sxs-lookup"><span data-stu-id="f9a32-104">In Azure Container Service, a Kubernetes cluster requires an [Azure Active Directory service principal](../../active-directory/develop/active-directory-application-objects.md) to interact with Azure APIs.</span></span> <span data-ttu-id="f9a32-105">L'entità servizio è necessaria per la gestione dinamica di risorse quali le [route definite dall'utente](../../virtual-network/virtual-networks-udr-overview.md) e [Azure Load Balancer di livello 4](../../load-balancer/load-balancer-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f9a32-105">The service principal is needed to dynamically manage resources such as [user-defined routes](../../virtual-network/virtual-networks-udr-overview.md) and the [Layer 4 Azure Load Balancer](../../load-balancer/load-balancer-overview.md).</span></span> 


<span data-ttu-id="f9a32-106">Questo articolo illustra le diverse opzioni disponibili per configurare un'entità servizio per il cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="f9a32-106">This article shows different options to set up a service principal for your Kubernetes cluster.</span></span> <span data-ttu-id="f9a32-107">Se, ad esempio, l'[interfaccia della riga di comando di Azure 2.0](/cli/azure/install-az-cli2) è già stata installata e configurata, è possibile eseguire il comando [`az acs create`](/cli/azure/acs#create) per creare il cluster Kubernetes e l'entità servizio contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="f9a32-107">For example, if you installed and set up the [Azure CLI 2.0](/cli/azure/install-az-cli2), you can run the [`az acs create`](/cli/azure/acs#create) command to create the Kubernetes cluster and the service principal at the same time.</span></span>


## <a name="requirements-for-the-service-principal"></a><span data-ttu-id="f9a32-108">Requisiti per l'entità servizio</span><span class="sxs-lookup"><span data-stu-id="f9a32-108">Requirements for the service principal</span></span>

<span data-ttu-id="f9a32-109">È possibile usare un'entità servizio di Azure AD esistente che soddisfi i requisiti seguenti oppure crearne una nuova.</span><span class="sxs-lookup"><span data-stu-id="f9a32-109">You can use an existing Azure AD service principal that meets the following requirements, or create a new one.</span></span>

* <span data-ttu-id="f9a32-110">**Ambito**: il gruppo di risorse nella sottoscrizione usato per distribuire il cluster Kubernetes o, in misura meno restrittiva, la sottoscrizione usata per distribuire il cluster.</span><span class="sxs-lookup"><span data-stu-id="f9a32-110">**Scope**: the resource group in the subscription used to deploy the Kubernetes cluster, or (less restrictively) the subscription used to deploy the cluster.</span></span>

* <span data-ttu-id="f9a32-111">**Ruolo**: **Collaboratore**.</span><span class="sxs-lookup"><span data-stu-id="f9a32-111">**Role**: **Contributor**</span></span>

* <span data-ttu-id="f9a32-112">**Segreto client**: deve essere una password.</span><span class="sxs-lookup"><span data-stu-id="f9a32-112">**Client secret**: must be a password.</span></span> <span data-ttu-id="f9a32-113">Non è attualmente possibile usare un'entità servizio configurata per l'autenticazione del certificato.</span><span class="sxs-lookup"><span data-stu-id="f9a32-113">Currently, you can't use a service principal set up for certificate authentication.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="f9a32-114">Per creare un'entità servizio sono necessarie autorizzazioni sufficienti per registrare un'applicazione con il tenant di Azure AD e assegnare l'applicazione a un ruolo nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="f9a32-114">To create a service principal, you must have permissions to register an application with your Azure AD tenant, and to assign the application to a role in your subscription.</span></span> <span data-ttu-id="f9a32-115">È possibile verificare se si hanno a disposizione le autorizzazioni necessarie [nel portale](../../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions).</span><span class="sxs-lookup"><span data-stu-id="f9a32-115">To see if you have the required permissions, [check in the Portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions).</span></span> 
>

## <a name="option-1-create-a-service-principal-in-azure-ad"></a><span data-ttu-id="f9a32-116">Opzione 1: creare un'entità servizio in Azure AD</span><span class="sxs-lookup"><span data-stu-id="f9a32-116">Option 1: Create a service principal in Azure AD</span></span>

<span data-ttu-id="f9a32-117">Azure mette a disposizione diversi metodi per creare un'entità servizio di Azure AD prima di distribuire il cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="f9a32-117">If you want to create an Azure AD service principal before you deploy your Kubernetes cluster, Azure provides several methods.</span></span> 

<span data-ttu-id="f9a32-118">I comandi di esempio seguenti illustrano come eseguire questa operazione con l'[interfaccia della riga di comando Azure 2.0](../../azure-resource-manager/resource-group-authenticate-service-principal-cli.md).</span><span class="sxs-lookup"><span data-stu-id="f9a32-118">The following example commands show you how to do this with the [Azure CLI 2.0](../../azure-resource-manager/resource-group-authenticate-service-principal-cli.md).</span></span> <span data-ttu-id="f9a32-119">In alternativa è possibile creare un'entità servizio usando [Azure PowerShell](../../azure-resource-manager/resource-group-authenticate-service-principal.md), il [portale](../../azure-resource-manager/resource-group-create-service-principal-portal.md) o altri metodi.</span><span class="sxs-lookup"><span data-stu-id="f9a32-119">You can alternatively create a service principal using [Azure PowerShell](../../azure-resource-manager/resource-group-authenticate-service-principal.md), the [portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md), or other methods.</span></span>

```azurecli
az login

az account set --subscription "mySubscriptionID"

az group create -n "myResourceGroupName" -l "westus"

az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/mySubscriptionID/resourceGroups/myResourceGroupName"
```

<span data-ttu-id="f9a32-120">L'output è simile al seguente (visualizzato con alcune modifiche):</span><span class="sxs-lookup"><span data-stu-id="f9a32-120">Output is similar to the following (shown here redacted):</span></span>

![Creare un’entità servizio](./media/container-service-kubernetes-service-principal/service-principal-creds.png)

<span data-ttu-id="f9a32-122">Sono evidenziati l'**ID client** (`appId`) e il **segreto client** (`password`) usati come parametri dell'entità servizio per la distribuzione del cluster.</span><span class="sxs-lookup"><span data-stu-id="f9a32-122">Highlighted are the **client ID** (`appId`) and the **client secret** (`password`) that you use as service principal parameters for cluster deployment.</span></span>


### <a name="specify-service-principal-when-creating-the-kubernetes-cluster"></a><span data-ttu-id="f9a32-123">Specificare l'entità servizio quando si crea il cluster Kubernetes</span><span class="sxs-lookup"><span data-stu-id="f9a32-123">Specify service principal when creating the Kubernetes cluster</span></span>

<span data-ttu-id="f9a32-124">Specificare l'**ID client**, anche chiamato `appId` ovvero ID applicazione, e il **segreto client** (`password`) di un'entità servizio esistente come parametri durante la creazione del cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="f9a32-124">Provide the **client ID** (also called the `appId`, for Application ID) and **client secret** (`password`) of an existing service principal as parameters when you create the Kubernetes cluster.</span></span> <span data-ttu-id="f9a32-125">Verificare che l'entità servizio soddisfi i requisiti illustrati all'inizio di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="f9a32-125">Make sure the service principal meets the requirements at the beginning this article.</span></span>

<span data-ttu-id="f9a32-126">È possibile specificare questi parametri durante la distribuzione del cluster Kubernetes usando l'[interfaccia della riga di comando di Azure 2.0](container-service-kubernetes-walkthrough.md), il [portale di Azure](../dcos-swarm/container-service-deployment.md) o altri metodi.</span><span class="sxs-lookup"><span data-stu-id="f9a32-126">You can specify these parameters when deploying the Kubernetes cluster using the [Azure Command-Line Interface (CLI) 2.0](container-service-kubernetes-walkthrough.md), [Azure portal](../dcos-swarm/container-service-deployment.md), or other methods.</span></span>

>[!TIP] 
><span data-ttu-id="f9a32-127">Quando si specifica l'**ID client**, assicurarsi di usare il valore `appId`, non `ObjectId`, dell'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="f9a32-127">When specifying the **client ID**, be sure to use the `appId`, not the `ObjectId`, of the service principal.</span></span>
>

<span data-ttu-id="f9a32-128">L'esempio seguente illustra un modo per passare i parametri con l'interfaccia della riga di comando di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="f9a32-128">The following example shows one way to pass the parameters with the Azure CLI 2.0.</span></span> <span data-ttu-id="f9a32-129">Questo esempio usa il [modello di avvio rapido di Kubernetes](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes).</span><span class="sxs-lookup"><span data-stu-id="f9a32-129">This example uses the [Kubernetes quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes).</span></span>

1. <span data-ttu-id="f9a32-130">[Scaricare](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.parameters.json) il file di parametri del modello `azuredeploy.parameters.json` da GitHub.</span><span class="sxs-lookup"><span data-stu-id="f9a32-130">[Download](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.parameters.json) the template parameters file `azuredeploy.parameters.json` from GitHub.</span></span>

2. <span data-ttu-id="f9a32-131">Per specificare l'entità servizio, immettere i valori per `servicePrincipalClientId` e `servicePrincipalClientSecret` nel file.</span><span class="sxs-lookup"><span data-stu-id="f9a32-131">To specify the service principal, enter values for `servicePrincipalClientId` and `servicePrincipalClientSecret` in the file.</span></span> <span data-ttu-id="f9a32-132">È anche necessario specificare valori personalizzati per `dnsNamePrefix` e `sshRSAPublicKey`,</span><span class="sxs-lookup"><span data-stu-id="f9a32-132">(You also need to provide your own values for `dnsNamePrefix` and `sshRSAPublicKey`.</span></span> <span data-ttu-id="f9a32-133">che indica la chiave pubblica SSH per l'accesso al cluster. Salvare il file.</span><span class="sxs-lookup"><span data-stu-id="f9a32-133">The latter is the SSH public key to access the cluster.) Save the file.</span></span>

    ![Passare i parametri dell'entità servizio](./media/container-service-kubernetes-service-principal/service-principal-params.png)

3. <span data-ttu-id="f9a32-135">Eseguire il comando seguente, usando `--parameters` per impostare il percorso per il file azuredeploy.parameters.json.</span><span class="sxs-lookup"><span data-stu-id="f9a32-135">Run the following command, using `--parameters` to set the path to the azuredeploy.parameters.json file.</span></span> <span data-ttu-id="f9a32-136">Questo comando distribuisce il cluster in un gruppo di risorse creato dall'utente e denominato `myResourceGroup` nell'area Stati Uniti occidentali.</span><span class="sxs-lookup"><span data-stu-id="f9a32-136">This command deploys the cluster in a resource group you create called `myResourceGroup` in the West US region.</span></span>

    ```azurecli
    az login

    az account set --subscription "mySubscriptionID"

    az group create --name "myResourceGroup" --location "westus" 
    
    az group deployment create -g "myResourceGroup" --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.json" --parameters @azuredeploy.parameters.json
    ```


## <a name="option-2-generate-a-service-principal-when-creating-the-cluster-with-az-acs-create"></a><span data-ttu-id="f9a32-137">Opzione 2: generare un'entità servizio durante la creazione del cluster con `az acs create`</span><span class="sxs-lookup"><span data-stu-id="f9a32-137">Option 2: Generate a service principal when creating the cluster with `az acs create`</span></span>

<span data-ttu-id="f9a32-138">Se si esegue il comando [`az acs create`](/cli/azure/acs#create) per creare il cluster Kubernetes, è possibile scegliere di generare automaticamente un'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="f9a32-138">If you run the [`az acs create`](/cli/azure/acs#create) command to create the Kubernetes cluster, you have the option to generate a service principal automatically.</span></span>

<span data-ttu-id="f9a32-139">Analogamente alle altre opzioni di creazione del cluster Kubernetes, è possibile specificare i parametri per un'entità servizio esistente quando si esegue `az acs create`.</span><span class="sxs-lookup"><span data-stu-id="f9a32-139">As with other Kubernetes cluster creation options, you can specify parameters for an existing service principal when you run `az acs create`.</span></span> <span data-ttu-id="f9a32-140">Quando tuttavia si omettono questi parametri, l'interfaccia della riga di comando di Azure crea automaticamente un'entità servizio da usare con il servizio contenitore.</span><span class="sxs-lookup"><span data-stu-id="f9a32-140">However, when you omit these parameters, the Azure CLI creates one automatically for use with Container Service.</span></span> <span data-ttu-id="f9a32-141">Questa operazione viene eseguita in modo trasparente durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="f9a32-141">This takes place transparently during the deployment.</span></span> 

<span data-ttu-id="f9a32-142">Il comando seguente crea un cluster Kubernetes e genera sia le chiavi SSH che le credenziali dell'entità servizio:</span><span class="sxs-lookup"><span data-stu-id="f9a32-142">The following command creates a Kubernetes cluster and generates both SSH keys and service principal credentials:</span></span>

```console
az acs create -n myClusterName -d myDNSPrefix -g myResourceGroup --generate-ssh-keys --orchestrator-type kubernetes
```

> [!IMPORTANT]
> <span data-ttu-id="f9a32-143">Se l'account non ha le autorizzazioni di Azure AD e della sottoscrizione necessarie per creare un'entità servizio, il comando genera un errore simile a `Insufficient privileges to complete the operation.`</span><span class="sxs-lookup"><span data-stu-id="f9a32-143">If your account doesn't have the Azure AD and subscription permissions to create a service principal, the command generates an error similar to `Insufficient privileges to complete the operation.`</span></span>
> 

## <a name="additional-considerations"></a><span data-ttu-id="f9a32-144">Ulteriori considerazioni</span><span class="sxs-lookup"><span data-stu-id="f9a32-144">Additional considerations</span></span>

* <span data-ttu-id="f9a32-145">Se non si hanno le autorizzazioni per creare un'entità servizio nella sottoscrizione, potrebbe essere necessario chiedere all'amministratore di Azure AD o della sottoscrizione di assegnare le autorizzazioni necessarie oppure chiedere che venga creata un'entità servizio da usare con il servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="f9a32-145">If you don't have permissions to create a service principal in your subscription, you might need to ask your Azure AD or subscription administrator to assign the necessary permissions, or ask them for a service principal to use with Azure Container Service.</span></span> 

* <span data-ttu-id="f9a32-146">L'entità servizio per Kubernetes fa parte della configurazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="f9a32-146">The service principal for Kubernetes is a part of the cluster configuration.</span></span> <span data-ttu-id="f9a32-147">Non usare tuttavia l'identità per distribuire il cluster.</span><span class="sxs-lookup"><span data-stu-id="f9a32-147">However, don't use the identity to deploy the cluster.</span></span>

* <span data-ttu-id="f9a32-148">Ogni entità servizio è associata a un'applicazione Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f9a32-148">Every service principal is associated with an Azure AD application.</span></span> <span data-ttu-id="f9a32-149">L'entità servizio per un cluster Kubernetes può essere associata a qualsiasi nome applicazione Azure AD valido, ad esempio `https://www.contoso.org/example`.</span><span class="sxs-lookup"><span data-stu-id="f9a32-149">The service principal for a Kubernetes cluster can be associated with any valid Azure AD application name (for example: `https://www.contoso.org/example`).</span></span> <span data-ttu-id="f9a32-150">L'URL per l'applicazione non deve essere necessariamente un endpoint reale.</span><span class="sxs-lookup"><span data-stu-id="f9a32-150">The URL for the application doesn't have to be a real endpoint.</span></span>

* <span data-ttu-id="f9a32-151">Quando si specifica l'**ID client** dell'entità servizio, è possibile usare il valore di `appId`, come illustrato in questo articolo, o il valore `name` corrispondente dell'entità servizio, ad esempio `https://www.contoso.org/example`.</span><span class="sxs-lookup"><span data-stu-id="f9a32-151">When specifying the service principal **Client ID**, you can use the value of the `appId` (as shown in this article) or the corresponding service principal `name` (for example,`https://www.contoso.org/example`).</span></span>

* <span data-ttu-id="f9a32-152">Nelle macchine virtuali master e dell'agente nel cluster Kubernetes, le credenziali dell'entità servizio vengono archiviate nel file /etc/kubernetes/azure.json.</span><span class="sxs-lookup"><span data-stu-id="f9a32-152">On the master and agent VMs in the Kubernetes cluster, the service principal credentials are stored in the file /etc/kubernetes/azure.json.</span></span>

* <span data-ttu-id="f9a32-153">Quando si usa il comando `az acs create` per generare automaticamente l'entità servizio, le credenziali dell'entità servizio vengono scritte nel file ~/.azure/acsServicePrincipal.json nel computer usato per eseguire il comando.</span><span class="sxs-lookup"><span data-stu-id="f9a32-153">When you use the `az acs create` command to generate the service principal automatically, the service principal credentials are written to the file ~/.azure/acsServicePrincipal.json on the machine used to run the command.</span></span> 

* <span data-ttu-id="f9a32-154">Quando si usa il comando `az acs create` per generare automaticamente l'entità servizio, questa può anche eseguire l'autenticazione con un [registro contenitori di Azure](../../container-registry/container-registry-intro.md) creato nella stessa sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="f9a32-154">When you use the `az acs create` command to generate the service principal automatically, the service principal can also authenticate with an [Azure container registry](../../container-registry/container-registry-intro.md) created in the same subscription.</span></span>




## <a name="next-steps"></a><span data-ttu-id="f9a32-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f9a32-155">Next steps</span></span>

* <span data-ttu-id="f9a32-156">[Introduzione a Kubernetes](container-service-kubernetes-walkthrough.md) nel cluster del servizio contenitore.</span><span class="sxs-lookup"><span data-stu-id="f9a32-156">[Get started with Kubernetes](container-service-kubernetes-walkthrough.md) in your container service cluster.</span></span>

* <span data-ttu-id="f9a32-157">Per risolvere i problemi dell'entità servizio per Kubernetes, vedere la [documentazione del motore ACS](https://github.com/Azure/acs-engine/blob/master/docs/kubernetes.md#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="f9a32-157">To troubleshoot the service principal for Kubernetes, see the [ACS Engine documentation](https://github.com/Azure/acs-engine/blob/master/docs/kubernetes.md#troubleshooting).</span></span>


