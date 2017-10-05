---
title: Distribuire OpenShift Origin in Azure| Microsoft Docs
description: Informazioni su come distribuire OpenShift Origin in macchine virtuali di Azure.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: jbinder
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 
ms.author: jbinder
ms.openlocfilehash: e03da05625e440eab29ccc28a2343d3433fc7607
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-openshift-origin-to-azure-virtual-machines"></a><span data-ttu-id="895df-103">Distribuire OpenShift Origin in macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="895df-103">Deploy OpenShift Origin to Azure Virtual Machines</span></span> 

<span data-ttu-id="895df-104">[ OpenShift Origin](https://www.openshift.org/) è una piattaforma contenitore open source basata su [Kubernetes](https://kubernetes.io/).</span><span class="sxs-lookup"><span data-stu-id="895df-104">[OpenShift Origin](https://www.openshift.org/) is an open source container platform built on [Kubernetes](https://kubernetes.io/).</span></span> <span data-ttu-id="895df-105">Semplifica distribuzione, ridimensionamento e uso delle applicazioni multi-tenant.</span><span class="sxs-lookup"><span data-stu-id="895df-105">It simplifies the process of deploying, scaling, and operating multi-tenant applications.</span></span> 

<span data-ttu-id="895df-106">Questa guida descrive come distribuire OpenShift Origin in macchine virtuali di Azure tramite la CLI di Azure e i modelli di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="895df-106">This guide describes how to deploy OpenShift Origin on Azure Virtual Machines using the Azure CLI and Azure Resource Manager Templates.</span></span> <span data-ttu-id="895df-107">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="895df-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="895df-108">Creare un insieme di credenziali delle chiavi per gestire le chiavi SSH per il cluster OpenShift.</span><span class="sxs-lookup"><span data-stu-id="895df-108">Create a KeyVault to manage SSH keys for the OpenShift cluster.</span></span>
> * <span data-ttu-id="895df-109">Distribuire un cluster OpenShift in macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="895df-109">Deploy an OpenShift cluster on Azure VMs.</span></span> 
> * <span data-ttu-id="895df-110">Installare e configurare la [CLI di OpenShift](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) per gestire il cluster.</span><span class="sxs-lookup"><span data-stu-id="895df-110">Install and configure the [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) to manage the cluster.</span></span>
> * <span data-ttu-id="895df-111">Personalizzare la distribuzione di OpenShift.</span><span class="sxs-lookup"><span data-stu-id="895df-111">Customize the OpenShift deployment.</span></span>

<span data-ttu-id="895df-112">Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="895df-112">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="895df-113">Questa guida introduttiva richiede l'interfaccia della riga di comando di Azure 2.0.8 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="895df-113">This quick start requires the Azure CLI version 2.0.8 or later.</span></span> <span data-ttu-id="895df-114">Per trovare la versione, eseguire `az --version`.</span><span class="sxs-lookup"><span data-stu-id="895df-114">To find the version, run `az --version`.</span></span> <span data-ttu-id="895df-115">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="895df-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="log-in-to-azure"></a><span data-ttu-id="895df-116">Accedere ad Azure</span><span class="sxs-lookup"><span data-stu-id="895df-116">Log in to Azure</span></span> 
<span data-ttu-id="895df-117">Accedere alla sottoscrizione di Azure con il comando [az login](/cli/azure/#login) e seguire le istruzioni visualizzate oppure fare clic su **Prova** per usare Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="895df-117">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions or click **Try it** to use Cloud Shell.</span></span>

```azurecli 
az login
```
## <a name="create-a-resource-group"></a><span data-ttu-id="895df-118">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="895df-118">Create a resource group</span></span>

<span data-ttu-id="895df-119">Creare un gruppo di risorse con il comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="895df-119">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="895df-120">Un gruppo di risorse di Azure è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite.</span><span class="sxs-lookup"><span data-stu-id="895df-120">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="895df-121">L'esempio seguente crea un gruppo di risorse denominato *myResourceGroup* nella località *stati uniti orientali*.</span><span class="sxs-lookup"><span data-stu-id="895df-121">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-key-vault"></a><span data-ttu-id="895df-122">Creare un insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="895df-122">Create a Key Vault</span></span>
<span data-ttu-id="895df-123">Creare un insieme di credenziali delle chiavi per archiviare le chiavi SSH per il cluster con il comando [az keyvault create](/cli/azure/keyvault#create).</span><span class="sxs-lookup"><span data-stu-id="895df-123">Create a KeyVault to store the SSH keys for the cluster with the [az keyvault create](/cli/azure/keyvault#create) command.</span></span>  

```azurecli 
az keyvault create --resource-group myResourceGroup --name myKeyVault \
       --enabled-for-template-deployment true \
       --location eastus
```

## <a name="create-an-ssh-key"></a><span data-ttu-id="895df-124">Creare una chiave SSH</span><span class="sxs-lookup"><span data-stu-id="895df-124">Create an SSH key</span></span> 
<span data-ttu-id="895df-125">La chiave SSH è necessaria per proteggere l'accesso al cluster di OpenShift Origin.</span><span class="sxs-lookup"><span data-stu-id="895df-125">An SSH key is needed to secure access to the OpenShift Origin cluster.</span></span> <span data-ttu-id="895df-126">Creare una coppia di chiavi SSH usando il comando `ssh-keygen`.</span><span class="sxs-lookup"><span data-stu-id="895df-126">Create an SSH key-pair using the `ssh-keygen` command.</span></span> 
 
 ```bash
ssh-keygen -f ~/.ssh/openshift_rsa -t rsa -N ''
```

> [!NOTE]
> <span data-ttu-id="895df-127">La coppia di chiavi SSH che viene creata non deve avere una passphrase.</span><span class="sxs-lookup"><span data-stu-id="895df-127">The SSH key pair you create must not have a passphrase.</span></span>

<span data-ttu-id="895df-128">Per altre informazioni sulle chiavi SSH in Windows, vedere [Come usare le chiavi SSH con Windows in Azure](/azure/virtual-machines/linux/ssh-from-windows).</span><span class="sxs-lookup"><span data-stu-id="895df-128">For more information on SSH keys on Windows, [How to create SSH keys on Windows](/azure/virtual-machines/linux/ssh-from-windows).</span></span>

## <a name="store-ssh-private-key-in-key-vault"></a><span data-ttu-id="895df-129">Archiviare la chiave privata SSH nell'insieme di credenziali per le chiavi</span><span class="sxs-lookup"><span data-stu-id="895df-129">Store SSH private key in Key Vault</span></span>
<span data-ttu-id="895df-130">La distribuzione di OpenShift usa la chiave SSH che è stata creata per proteggere l'accesso al master di OpenShift.</span><span class="sxs-lookup"><span data-stu-id="895df-130">The OpenShift deployment uses the SSH key you created to secure access to the OpenShift master.</span></span> <span data-ttu-id="895df-131">Per abilitare la distribuzione per recuperare in modo sicuro la chiave SSH, archiviare la chiave nell'insieme di credenziali per le chiavi usando il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="895df-131">To enable the deployment to securely retrieve the SSH key, store the key in Key Vault using the following command.</span></span>

# <a name="enabled-for-template-deployment"></a><span data-ttu-id="895df-132">Distribuzione abilitata per modello</span><span class="sxs-lookup"><span data-stu-id="895df-132">Enabled for template deployment</span></span>
```azurecli
az keyvault secret set --vault-name KeyVaultName --name OpenShiftKey --file ~/.ssh/openshift.rsa
```

## <a name="create-a-service-principal"></a><span data-ttu-id="895df-133">Creare un'entità servizio</span><span class="sxs-lookup"><span data-stu-id="895df-133">Create a service principal</span></span> 
<span data-ttu-id="895df-134">OpenShift comunica con Azure usando un nome utente e una password o un'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="895df-134">OpenShift communicates with Azure using a username and password or a service principal.</span></span> <span data-ttu-id="895df-135">Un'entità servizio di Azure è un'identità di sicurezza che è possibile usare con le app, con i servizi e con strumenti di automazione come OpenShift.</span><span class="sxs-lookup"><span data-stu-id="895df-135">An Azure service principal is a security identity that you can use with apps, services, and automation tools like OpenShift.</span></span> <span data-ttu-id="895df-136">Le autorizzazioni per le operazioni che l'entità servizio può eseguire in Azure vengono controllate e definite dall'utente.</span><span class="sxs-lookup"><span data-stu-id="895df-136">You control and define the permissions as to what operations the service principal can perform in Azure.</span></span> <span data-ttu-id="895df-137">Per migliorare la sicurezza rispetto alla semplice immissione di nome utente e password, questo esempio crea un'entità servizio di base.</span><span class="sxs-lookup"><span data-stu-id="895df-137">To improve security over just providing a username and password, this example creates a basic service principal.</span></span>

<span data-ttu-id="895df-138">Creare un'entità servizio con [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) e generare l'output delle credenziali necessarie per OpenShift:</span><span class="sxs-lookup"><span data-stu-id="895df-138">Create a service principal with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) and output the credentials that OpenShift needs:</span></span>

```azurecli
az ad sp create-for-rbac --name openshiftsp \
          --role Contributor --password {strong password} \
          --scopes $(az group show --name myResourceGroup --query id)
```
<span data-ttu-id="895df-139">Prendere nota della proprietà appId restituita dal comando.</span><span class="sxs-lookup"><span data-stu-id="895df-139">Take note of the appId property returned from the command.</span></span>
```json
{
  "appId": "a487e0c1-82af-47d9-9a0b-af184eb87646d",
  "displayName": "openshiftsp",
  "name": "http://openshiftsp",
  "password": {strong password},
  "tenant": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX"
}
```
 > [!WARNING] 
 > <span data-ttu-id="895df-140">Non creare una password non sicura.</span><span class="sxs-lookup"><span data-stu-id="895df-140">Don't create an insecure password.</span></span>  <span data-ttu-id="895df-141">Attenersi alle istruzioni relative a [regole e limitazioni sulle password di Azure AD](/azure/active-directory/active-directory-passwords-policy).</span><span class="sxs-lookup"><span data-stu-id="895df-141">Follow the [Azure AD password rules and restrictions](/azure/active-directory/active-directory-passwords-policy) guidance.</span></span>

<span data-ttu-id="895df-142">Per altre informazioni sulle entità servizio, vedere [Creare un'entità servizio di Azure con l'interfaccia della riga di comando di Azure 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)</span><span class="sxs-lookup"><span data-stu-id="895df-142">For more information on service principals, see [Create an Azure service principal with Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)</span></span>

## <a name="deploy-the-openshift-origin-template"></a><span data-ttu-id="895df-143">Distribuire il modello di OpenShift Origin</span><span class="sxs-lookup"><span data-stu-id="895df-143">Deploy the OpenShift Origin template</span></span>
<span data-ttu-id="895df-144">A questo punto distribuire OpenShift Origin usando un modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="895df-144">Next deploy OpenShift Origin using an Azure Resource Manager template.</span></span> 

> [!NOTE] 
> <span data-ttu-id="895df-145">Il comando seguente richiede l'interfaccia della riga di comando di Azure 2.0.8 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="895df-145">The following command requires az CLI 2.0.8 or later.</span></span> <span data-ttu-id="895df-146">È possibile verificare la versione della CLI di Azure con il comando `az --version`.</span><span class="sxs-lookup"><span data-stu-id="895df-146">You can verify the az CLI version with the `az --version` command.</span></span> <span data-ttu-id="895df-147">Per aggiornare la versione della CLI, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="895df-147">To update the CLI version, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="895df-148">Usare il valore `appId` dall'entità servizio creata in precedenza per il parametro `aadClientId`.</span><span class="sxs-lookup"><span data-stu-id="895df-148">Use the `appId` value from the service principal you created earlier for the `aadClientId` parameter.</span></span>

```azurecli 
az group deployment create --name myOpenShiftCluster \
      --template-uri https://raw.githubusercontent.com/Microsoft/openshift-origin/master/azuredeploy.json \
      --params \ 
        openshiftMasterPublicIpDnsLabel=myopenshiftmaster \
        infraLbPublicIpDnsLabel=myopenshiftlb \
        openshiftPassword=Pass@word!
        sshPublicKey=~/.ssh/openshift_rsa.pub \
        keyVaultResourceGroup=myResourceGroup \
        keyVaultName=myKeyVault \
        keyVaultSecret=OpenShiftKey \
        aadClientId={appId} \
        aadClientSecret={strong password} 
```
<span data-ttu-id="895df-149">Il completamento della distribuzione richiede fino a 20 minuti.</span><span class="sxs-lookup"><span data-stu-id="895df-149">The deployment may take up to 20 minutes to complete.</span></span> <span data-ttu-id="895df-150">Al termine della distribuzione, l'URL della console di OpenShift e il nome DNS del master di OpenShift vengono visualizzati sul terminale.</span><span class="sxs-lookup"><span data-stu-id="895df-150">The URL of the OpenShift console and DNS name of the OpenShift master is printed to the terminal when the deployment completes.</span></span>

```json
{
  "OpenShift Console Uri": "http://openshiftlb.cloudapp.azure.com:8443/console",
  "OpenShift Master SSH": "ocpadmin@myopenshiftmaster.cloudapp.azure.com"
}
```
## <a name="connect-to-the-openshift-cluster"></a><span data-ttu-id="895df-151">Eseguire la connessione al cluster OpenShift</span><span class="sxs-lookup"><span data-stu-id="895df-151">Connect to the OpenShift cluster</span></span>
<span data-ttu-id="895df-152">Al termine della distribuzione, eseguire la connessione alla console di OpenShift tramite il browser immettendo `OpenShift Console Uri`.</span><span class="sxs-lookup"><span data-stu-id="895df-152">When the deployment completes, connect to the OpenShift console using the browser using the `OpenShift Console Uri`.</span></span> <span data-ttu-id="895df-153">In alternativa, è possibile connettersi al master di OpenShift usando il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="895df-153">Alternatively, you can connect to the OpenShift master using the following command.</span></span>

```bash
$ ssh ocpadmin@myopenshiftmaster.cloudapp.azure.com
```

## <a name="clean-up-resources"></a><span data-ttu-id="895df-154">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="895df-154">Clean up resources</span></span>
<span data-ttu-id="895df-155">Quando non servono più, è possibile rimuovere il gruppo di risorse, il cluster OpenShift e tutte le risorse correlate tramite il comando [az group delete](/cli/azure/group#delete).</span><span class="sxs-lookup"><span data-stu-id="895df-155">When no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, OpenShift cluster, and all related resources.</span></span>

```azurecli 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="895df-156">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="895df-156">Next steps</span></span>

<span data-ttu-id="895df-157">Questa esercitazione ha illustrato come:</span><span class="sxs-lookup"><span data-stu-id="895df-157">In this tutorial, learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="895df-158">Creare un insieme di credenziali delle chiavi per gestire le chiavi SSH per il cluster OpenShift.</span><span class="sxs-lookup"><span data-stu-id="895df-158">Create a KeyVault to manage SSH keys for the OpenShift cluster.</span></span>
> * <span data-ttu-id="895df-159">Distribuire un cluster OpenShift in macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="895df-159">Deploy an OpenShift cluster on Azure VMs.</span></span> 
> * <span data-ttu-id="895df-160">Installare e configurare la [CLI di OpenShift](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) per gestire il cluster.</span><span class="sxs-lookup"><span data-stu-id="895df-160">Install and configure the [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) to manage the cluster.</span></span>

<span data-ttu-id="895df-161">A questo punto il cluster OpenShift Origin è stato distribuito.</span><span class="sxs-lookup"><span data-stu-id="895df-161">Now that OpenShift Origin cluster is deployed.</span></span> <span data-ttu-id="895df-162">È possibile seguire le esercitazioni di OpenShift per imparare a distribuire la prima applicazione e a usare gli strumenti di OpenShift.</span><span class="sxs-lookup"><span data-stu-id="895df-162">You can follow OpenShift tutorials to learn how to deploy your first application and use the OpenShift tools.</span></span> <span data-ttu-id="895df-163">Per una panoramica iniziale, vedere [Getting Started with OpenShift Origin](https://docs.openshift.org/latest/getting_started/index.html) (Introduzione a OpenShift Origin).</span><span class="sxs-lookup"><span data-stu-id="895df-163">See [Getting Started with OpenShift Origin](https://docs.openshift.org/latest/getting_started/index.html) to get started.</span></span> 
