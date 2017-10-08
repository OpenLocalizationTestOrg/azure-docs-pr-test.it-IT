---
title: Origine OpenShift tooAzure aaaDeploy | Documenti Microsoft
description: Informazioni su origine OpenShift toodeploy tooAzure le macchine virtuali.
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
ms.openlocfilehash: a67450c46da41134a5f6c669a9e54e14773ac5b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-openshift-origin-tooazure-virtual-machines"></a><span data-ttu-id="f9c07-103">Distribuzione di origine OpenShift tooAzure macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="f9c07-103">Deploy OpenShift Origin tooAzure Virtual Machines</span></span> 

<span data-ttu-id="f9c07-104">[ OpenShift Origin](https://www.openshift.org/) è una piattaforma contenitore open source basata su [Kubernetes](https://kubernetes.io/).</span><span class="sxs-lookup"><span data-stu-id="f9c07-104">[OpenShift Origin](https://www.openshift.org/) is an open source container platform built on [Kubernetes](https://kubernetes.io/).</span></span> <span data-ttu-id="f9c07-105">Semplifica il processo di hello di distribuzione, scalabilità e gestione di applicazioni multi-tenant.</span><span class="sxs-lookup"><span data-stu-id="f9c07-105">It simplifies hello process of deploying, scaling, and operating multi-tenant applications.</span></span> 

<span data-ttu-id="f9c07-106">Questa guida descrive come toodeploy OpenShift origine sull'uso di macchine virtuali di Azure hello Azure CLI e modelli di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="f9c07-106">This guide describes how toodeploy OpenShift Origin on Azure Virtual Machines using hello Azure CLI and Azure Resource Manager Templates.</span></span> <span data-ttu-id="f9c07-107">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="f9c07-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f9c07-108">Creare un toomanage KeyVault chiavi SSH per cluster OpenShift hello.</span><span class="sxs-lookup"><span data-stu-id="f9c07-108">Create a KeyVault toomanage SSH keys for hello OpenShift cluster.</span></span>
> * <span data-ttu-id="f9c07-109">Distribuire un cluster OpenShift in macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="f9c07-109">Deploy an OpenShift cluster on Azure VMs.</span></span> 
> * <span data-ttu-id="f9c07-110">Installare e configurare hello [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) cluster hello toomanage.</span><span class="sxs-lookup"><span data-stu-id="f9c07-110">Install and configure hello [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) toomanage hello cluster.</span></span>
> * <span data-ttu-id="f9c07-111">Personalizzare la distribuzione OpenShift hello.</span><span class="sxs-lookup"><span data-stu-id="f9c07-111">Customize hello OpenShift deployment.</span></span>

<span data-ttu-id="f9c07-112">Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="f9c07-112">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="f9c07-113">Questa Guida introduttiva richiede hello Azure CLI versione 2.0.8 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="f9c07-113">This quick start requires hello Azure CLI version 2.0.8 or later.</span></span> <span data-ttu-id="f9c07-114">versione di hello toofind, eseguire `az --version`.</span><span class="sxs-lookup"><span data-stu-id="f9c07-114">toofind hello version, run `az --version`.</span></span> <span data-ttu-id="f9c07-115">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f9c07-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="log-in-tooazure"></a><span data-ttu-id="f9c07-116">Accedi tooAzure</span><span class="sxs-lookup"><span data-stu-id="f9c07-116">Log in tooAzure</span></span> 
<span data-ttu-id="f9c07-117">Accedere alla sottoscrizione di Azure con hello tooyour [accesso az](/cli/azure/#login) comando e seguire hello direzioni o fare clic su **provarla** toouse Shell Cloud.</span><span class="sxs-lookup"><span data-stu-id="f9c07-117">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions or click **Try it** toouse Cloud Shell.</span></span>

```azurecli 
az login
```
## <a name="create-a-resource-group"></a><span data-ttu-id="f9c07-118">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="f9c07-118">Create a resource group</span></span>

<span data-ttu-id="f9c07-119">Creare un gruppo di risorse con hello [gruppo az creare](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="f9c07-119">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="f9c07-120">Un gruppo di risorse di Azure è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite.</span><span class="sxs-lookup"><span data-stu-id="f9c07-120">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="f9c07-121">esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *eastus* percorso.</span><span class="sxs-lookup"><span data-stu-id="f9c07-121">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-key-vault"></a><span data-ttu-id="f9c07-122">Creare un insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="f9c07-122">Create a Key Vault</span></span>
<span data-ttu-id="f9c07-123">Creare un hello toostore KeyVault chiavi SSH per il cluster hello con hello [keyvault az creare](/cli/azure/keyvault#create) comando.</span><span class="sxs-lookup"><span data-stu-id="f9c07-123">Create a KeyVault toostore hello SSH keys for hello cluster with hello [az keyvault create](/cli/azure/keyvault#create) command.</span></span>  

```azurecli 
az keyvault create --resource-group myResourceGroup --name myKeyVault \
       --enabled-for-template-deployment true \
       --location eastus
```

## <a name="create-an-ssh-key"></a><span data-ttu-id="f9c07-124">Creare una chiave SSH</span><span class="sxs-lookup"><span data-stu-id="f9c07-124">Create an SSH key</span></span> 
<span data-ttu-id="f9c07-125">Una chiave SSH è necessario toosecure accesso toohello cluster OpenShift origine.</span><span class="sxs-lookup"><span data-stu-id="f9c07-125">An SSH key is needed toosecure access toohello OpenShift Origin cluster.</span></span> <span data-ttu-id="f9c07-126">Creare una coppia di chiavi SSH utilizzando hello `ssh-keygen` comando.</span><span class="sxs-lookup"><span data-stu-id="f9c07-126">Create an SSH key-pair using hello `ssh-keygen` command.</span></span> 
 
 ```bash
ssh-keygen -f ~/.ssh/openshift_rsa -t rsa -N ''
```

> [!NOTE]
> <span data-ttu-id="f9c07-127">coppia di chiavi SSH crei Hello non deve avere una passphrase.</span><span class="sxs-lookup"><span data-stu-id="f9c07-127">hello SSH key pair you create must not have a passphrase.</span></span>

<span data-ttu-id="f9c07-128">Per ulteriori informazioni sulle chiavi SSH in Windows, [come toocreate SSH chiavi in Windows](/azure/virtual-machines/linux/ssh-from-windows).</span><span class="sxs-lookup"><span data-stu-id="f9c07-128">For more information on SSH keys on Windows, [How toocreate SSH keys on Windows](/azure/virtual-machines/linux/ssh-from-windows).</span></span>

## <a name="store-ssh-private-key-in-key-vault"></a><span data-ttu-id="f9c07-129">Archiviare la chiave privata SSH nell'insieme di credenziali per le chiavi</span><span class="sxs-lookup"><span data-stu-id="f9c07-129">Store SSH private key in Key Vault</span></span>
<span data-ttu-id="f9c07-130">Hello OpenShift distribuzione utilizza la chiave SSH hello creato accesso toosecure toohello OpenShift master.</span><span class="sxs-lookup"><span data-stu-id="f9c07-130">hello OpenShift deployment uses hello SSH key you created toosecure access toohello OpenShift master.</span></span> <span data-ttu-id="f9c07-131">tooenable hello distribuzione toosecurely recuperare la chiave SSH hello, archivia la chiave di hello nell'insieme di credenziali chiave usando hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="f9c07-131">tooenable hello deployment toosecurely retrieve hello SSH key, store hello key in Key Vault using hello following command.</span></span>

# <a name="enabled-for-template-deployment"></a><span data-ttu-id="f9c07-132">Distribuzione abilitata per modello</span><span class="sxs-lookup"><span data-stu-id="f9c07-132">Enabled for template deployment</span></span>
```azurecli
az keyvault secret set --vault-name KeyVaultName --name OpenShiftKey --file ~/.ssh/openshift.rsa
```

## <a name="create-a-service-principal"></a><span data-ttu-id="f9c07-133">Creare un'entità servizio</span><span class="sxs-lookup"><span data-stu-id="f9c07-133">Create a service principal</span></span> 
<span data-ttu-id="f9c07-134">OpenShift comunica con Azure usando un nome utente e una password o un'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="f9c07-134">OpenShift communicates with Azure using a username and password or a service principal.</span></span> <span data-ttu-id="f9c07-135">Un'entità servizio di Azure è un'identità di sicurezza che è possibile usare con le app, con i servizi e con strumenti di automazione come OpenShift.</span><span class="sxs-lookup"><span data-stu-id="f9c07-135">An Azure service principal is a security identity that you can use with apps, services, and automation tools like OpenShift.</span></span> <span data-ttu-id="f9c07-136">È controllare e definire le autorizzazioni di hello come entità di servizio toowhat operazioni hello è possibile eseguire in Azure.</span><span class="sxs-lookup"><span data-stu-id="f9c07-136">You control and define hello permissions as toowhat operations hello service principal can perform in Azure.</span></span> <span data-ttu-id="f9c07-137">sicurezza tooimprove su per fornire un nome utente e una password, questo esempio crea un servizio di base dell'entità.</span><span class="sxs-lookup"><span data-stu-id="f9c07-137">tooimprove security over just providing a username and password, this example creates a basic service principal.</span></span>

<span data-ttu-id="f9c07-138">Creare un servizio principale con [az ad sp creare-per-rbac](/cli/azure/ad/sp#create-for-rbac) e le credenziali di hello output OpenShift deve:</span><span class="sxs-lookup"><span data-stu-id="f9c07-138">Create a service principal with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) and output hello credentials that OpenShift needs:</span></span>

```azurecli
az ad sp create-for-rbac --name openshiftsp \
          --role Contributor --password {strong password} \
          --scopes $(az group show --name myResourceGroup --query id)
```
<span data-ttu-id="f9c07-139">Prendere nota della proprietà appId hello restituito dal comando hello.</span><span class="sxs-lookup"><span data-stu-id="f9c07-139">Take note of hello appId property returned from hello command.</span></span>
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
 > <span data-ttu-id="f9c07-140">Non creare una password non sicura.</span><span class="sxs-lookup"><span data-stu-id="f9c07-140">Don't create an insecure password.</span></span>  <span data-ttu-id="f9c07-141">Attenersi alle istruzioni relative a [regole e limitazioni sulle password di Azure AD](/azure/active-directory/active-directory-passwords-policy).</span><span class="sxs-lookup"><span data-stu-id="f9c07-141">Follow the [Azure AD password rules and restrictions](/azure/active-directory/active-directory-passwords-policy) guidance.</span></span>

<span data-ttu-id="f9c07-142">Per altre informazioni sulle entità servizio, vedere [Creare un'entità servizio di Azure con l'interfaccia della riga di comando di Azure 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)</span><span class="sxs-lookup"><span data-stu-id="f9c07-142">For more information on service principals, see [Create an Azure service principal with Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)</span></span>

## <a name="deploy-hello-openshift-origin-template"></a><span data-ttu-id="f9c07-143">Distribuire il modello di origine OpenShift hello</span><span class="sxs-lookup"><span data-stu-id="f9c07-143">Deploy hello OpenShift Origin template</span></span>
<span data-ttu-id="f9c07-144">A questo punto distribuire OpenShift Origin usando un modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f9c07-144">Next deploy OpenShift Origin using an Azure Resource Manager template.</span></span> 

> [!NOTE] 
> <span data-ttu-id="f9c07-145">il comando seguente Hello richiede az CLI 2.0.8 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="f9c07-145">hello following command requires az CLI 2.0.8 or later.</span></span> <span data-ttu-id="f9c07-146">È possibile verificare hello az CLI versione con hello `az --version` comando.</span><span class="sxs-lookup"><span data-stu-id="f9c07-146">You can verify hello az CLI version with hello `az --version` command.</span></span> <span data-ttu-id="f9c07-147">hello tooupdate versione CLI, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f9c07-147">tooupdate hello CLI version, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="f9c07-148">Hello utilizzare `appId` valore dall'entità servizio hello creato in precedenza per hello `aadClientId` parametro.</span><span class="sxs-lookup"><span data-stu-id="f9c07-148">Use hello `appId` value from hello service principal you created earlier for hello `aadClientId` parameter.</span></span>

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
<span data-ttu-id="f9c07-149">distribuzione di Hello potrebbe richiedere too20 minuti toocomplete.</span><span class="sxs-lookup"><span data-stu-id="f9c07-149">hello deployment may take up too20 minutes toocomplete.</span></span> <span data-ttu-id="f9c07-150">Hello URL della console OpenShift hello e il nome DNS di hello OpenShift master viene stampato toohello terminal al completamento distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="f9c07-150">hello URL of hello OpenShift console and DNS name of hello OpenShift master is printed toohello terminal when hello deployment completes.</span></span>

```json
{
  "OpenShift Console Uri": "http://openshiftlb.cloudapp.azure.com:8443/console",
  "OpenShift Master SSH": "ocpadmin@myopenshiftmaster.cloudapp.azure.com"
}
```
## <a name="connect-toohello-openshift-cluster"></a><span data-ttu-id="f9c07-151">Connettere il cluster di OpenShift toohello</span><span class="sxs-lookup"><span data-stu-id="f9c07-151">Connect toohello OpenShift cluster</span></span>
<span data-ttu-id="f9c07-152">Al termine della distribuzione di hello, connettersi toohello OpenShift console tramite browser hello utilizzando hello `OpenShift Console Uri`.</span><span class="sxs-lookup"><span data-stu-id="f9c07-152">When hello deployment completes, connect toohello OpenShift console using hello browser using hello `OpenShift Console Uri`.</span></span> <span data-ttu-id="f9c07-153">In alternativa, è possibile connettersi toohello OpenShift master utilizzando hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="f9c07-153">Alternatively, you can connect toohello OpenShift master using hello following command.</span></span>

```bash
$ ssh ocpadmin@myopenshiftmaster.cloudapp.azure.com
```

## <a name="clean-up-resources"></a><span data-ttu-id="f9c07-154">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="f9c07-154">Clean up resources</span></span>
<span data-ttu-id="f9c07-155">Quando non è più necessario, è possibile utilizzare hello [eliminazione gruppo az](/cli/azure/group#delete) comando gruppo di risorse hello tooremove OpenShift cluster e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="f9c07-155">When no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, OpenShift cluster, and all related resources.</span></span>

```azurecli 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="f9c07-156">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f9c07-156">Next steps</span></span>

<span data-ttu-id="f9c07-157">Questa esercitazione ha illustrato come:</span><span class="sxs-lookup"><span data-stu-id="f9c07-157">In this tutorial, learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="f9c07-158">Creare un toomanage KeyVault chiavi SSH per cluster OpenShift hello.</span><span class="sxs-lookup"><span data-stu-id="f9c07-158">Create a KeyVault toomanage SSH keys for hello OpenShift cluster.</span></span>
> * <span data-ttu-id="f9c07-159">Distribuire un cluster OpenShift in macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="f9c07-159">Deploy an OpenShift cluster on Azure VMs.</span></span> 
> * <span data-ttu-id="f9c07-160">Installare e configurare hello [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) cluster hello toomanage.</span><span class="sxs-lookup"><span data-stu-id="f9c07-160">Install and configure hello [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) toomanage hello cluster.</span></span>

<span data-ttu-id="f9c07-161">A questo punto il cluster OpenShift Origin è stato distribuito.</span><span class="sxs-lookup"><span data-stu-id="f9c07-161">Now that OpenShift Origin cluster is deployed.</span></span> <span data-ttu-id="f9c07-162">È possibile seguire OpenShift esercitazioni toolearn come toodeploy la prima applicazione e usare hello OpenShift strumenti.</span><span class="sxs-lookup"><span data-stu-id="f9c07-162">You can follow OpenShift tutorials toolearn how toodeploy your first application and use hello OpenShift tools.</span></span> <span data-ttu-id="f9c07-163">Vedere [Guida introduttiva a origine OpenShift](https://docs.openshift.org/latest/getting_started/index.html) tooget avviato.</span><span class="sxs-lookup"><span data-stu-id="f9c07-163">See [Getting Started with OpenShift Origin](https://docs.openshift.org/latest/getting_started/index.html) tooget started.</span></span> 
