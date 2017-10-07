---
title: aaaInstall e configurare Ansible per l'utilizzo con macchine virtuali di Azure | Documenti Microsoft
description: Informazioni su come tooinstall e configurare Ansible per la gestione delle risorse di Azure in Ubuntu, in CentOS e SLES
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: na
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/25/2017
ms.author: iainfou
ms.openlocfilehash: b33d1893909b6134a5474617c9af2d6e4f627c05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-ansible-toomanage-virtual-machines-in-azure"></a><span data-ttu-id="2a70d-103">Installare e configurare le macchine virtuali toomanage Ansible in Azure</span><span class="sxs-lookup"><span data-stu-id="2a70d-103">Install and configure Ansible toomanage virtual machines in Azure</span></span>
<span data-ttu-id="2a70d-104">In questo articolo illustra in dettaglio come tooinstall Ansible e i moduli di Azure SDK Python necessari per alcune delle hello le distribuzioni di Linux più comuni.</span><span class="sxs-lookup"><span data-stu-id="2a70d-104">This article details how tooinstall Ansible and required Azure Python SDK modules for some of hello most common Linux distros.</span></span> <span data-ttu-id="2a70d-105">È possibile installare Ansible in altre distribuzioni regolando toofit pacchetti hello installato la piattaforma specifica.</span><span class="sxs-lookup"><span data-stu-id="2a70d-105">You can install Ansible on other distros by adjusting hello installed packages toofit your particular platform.</span></span> <span data-ttu-id="2a70d-106">toocreate Azure le risorse in modo sicuro, verrà inoltre descritto come toocreate e definire le credenziali per Ansible toouse.</span><span class="sxs-lookup"><span data-stu-id="2a70d-106">toocreate Azure resources in a secure manner, you also learn how toocreate and define credentials for Ansible toouse.</span></span> 

<span data-ttu-id="2a70d-107">Per altre opzioni di installazione e i passaggi per altre piattaforme, vedere hello [Ansible Guida all'installazione](https://docs.ansible.com/ansible/intro_installation.html).</span><span class="sxs-lookup"><span data-stu-id="2a70d-107">For more installation options and steps for additional platforms, see hello [Ansible install guide](https://docs.ansible.com/ansible/intro_installation.html).</span></span>


## <a name="install-ansible"></a><span data-ttu-id="2a70d-108">Installare Ansible</span><span class="sxs-lookup"><span data-stu-id="2a70d-108">Install Ansible</span></span>
<span data-ttu-id="2a70d-109">Creare prima un gruppo di risorse con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="2a70d-109">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="2a70d-110">esempio Hello crea un gruppo di risorse denominato *myResourceGroupAnsible* in hello *eastus* percorso:</span><span class="sxs-lookup"><span data-stu-id="2a70d-110">hello following example creates a resource group named *myResourceGroupAnsible* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroupAnsible --location eastus
```

<span data-ttu-id="2a70d-111">Ora di creare una macchina virtuale e installare Ansible per uno dei seguenti distribuzioni hello:</span><span class="sxs-lookup"><span data-stu-id="2a70d-111">Now create a VM and install Ansible for one of hello following distros:</span></span>

- [<span data-ttu-id="2a70d-112">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="2a70d-112">Ubuntu 16.04 LTS</span></span>](#ubuntu1604-lts)
- [<span data-ttu-id="2a70d-113">CentOS 7.3</span><span class="sxs-lookup"><span data-stu-id="2a70d-113">CentOS 7.3</span></span>](#centos-73)
- [<span data-ttu-id="2a70d-114">SLES 12.2 SP2</span><span class="sxs-lookup"><span data-stu-id="2a70d-114">SLES 12.2 SP2</span></span>](#sles-122-sp2)

### <a name="ubuntu-1604-lts"></a><span data-ttu-id="2a70d-115">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="2a70d-115">Ubuntu 16.04 LTS</span></span>
<span data-ttu-id="2a70d-116">Creare una VM con il comando [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="2a70d-116">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="2a70d-117">esempio Hello crea una macchina virtuale denominata *myVMAnsible*:</span><span class="sxs-lookup"><span data-stu-id="2a70d-117">hello following example creates a VM named *myVMAnsible*:</span></span>

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="2a70d-118">SSH tramite VM tooyour hello `publicIpAddress` indicato nel hello operazione di creazione dell'output di hello VM:</span><span class="sxs-lookup"><span data-stu-id="2a70d-118">SSH tooyour VM using hello `publicIpAddress` noted in hello output from hello VM create operation:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="2a70d-119">Nella macchina virtuale, installare i pacchetti hello necessario per i moduli di Azure SDK Python hello e Ansible come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="2a70d-119">On your VM, install hello required packages for hello Azure Python SDK modules and Ansible as follows:</span></span>

```bash
## Install pre-requisite packages
sudo apt-get update && sudo apt-get install -y libssl-dev libffi-dev python-dev python-pip

## Install Azure SDKs via pip
pip install "azure==2.0.0rc5" msrestazure

## Install Ansible via apt
sudo apt-get install -y software-properties-common
sudo apt-add-repository -y ppa:ansible/ansible
sudo apt-get update && sudo apt-get install -y ansible
```

<span data-ttu-id="2a70d-120">Procedere con troppo[le credenziali di Azure creare](#create-azure-credentials).</span><span class="sxs-lookup"><span data-stu-id="2a70d-120">Now move on too[Create Azure credentials](#create-azure-credentials).</span></span>


### <a name="centos-73"></a><span data-ttu-id="2a70d-121">CentOS 7.3</span><span class="sxs-lookup"><span data-stu-id="2a70d-121">CentOS 7.3</span></span>
<span data-ttu-id="2a70d-122">Creare una VM con il comando [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="2a70d-122">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="2a70d-123">esempio Hello crea una macchina virtuale denominata *myVMAnsible*:</span><span class="sxs-lookup"><span data-stu-id="2a70d-123">hello following example creates a VM named *myVMAnsible*:</span></span>

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image CentOS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="2a70d-124">SSH tramite VM tooyour hello `publicIpAddress` indicato nel hello operazione di creazione dell'output di hello VM:</span><span class="sxs-lookup"><span data-stu-id="2a70d-124">SSH tooyour VM using hello `publicIpAddress` noted in hello output from hello VM create operation:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="2a70d-125">Nella macchina virtuale, installare i pacchetti hello necessario per i moduli di Azure SDK Python hello e Ansible come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="2a70d-125">On your VM, install hello required packages for hello Azure Python SDK modules and Ansible as follows:</span></span>

```bash
## Install pre-requisite packages
sudo yum check-update; sudo yum install -y gcc libffi-devel python-devel openssl-devel epel-release
sudo yum install -y python-pip python-wheel

## Install Azure SDKs via pip
sudo pip install "azure==2.0.0rc5" msrestazure

## Install Ansible via yum
sudo yum install -y ansible
```

<span data-ttu-id="2a70d-126">Procedere con troppo[le credenziali di Azure creare](#create-azure-credentials).</span><span class="sxs-lookup"><span data-stu-id="2a70d-126">Now move on too[Create Azure credentials](#create-azure-credentials).</span></span>


### <a name="sles-122-sp2"></a><span data-ttu-id="2a70d-127">SLES 12.2 SP2</span><span class="sxs-lookup"><span data-stu-id="2a70d-127">SLES 12.2 SP2</span></span>
<span data-ttu-id="2a70d-128">Creare una VM con il comando [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="2a70d-128">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="2a70d-129">esempio Hello crea una macchina virtuale denominata *myVMAnsible*:</span><span class="sxs-lookup"><span data-stu-id="2a70d-129">hello following example creates a VM named *myVMAnsible*:</span></span>

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image SLES \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="2a70d-130">SSH tramite VM tooyour hello `publicIpAddress` indicato nel hello operazione di creazione dell'output di hello VM:</span><span class="sxs-lookup"><span data-stu-id="2a70d-130">SSH tooyour VM using hello `publicIpAddress` noted in hello output from hello VM create operation:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="2a70d-131">Nella macchina virtuale, installare i pacchetti hello necessario per i moduli di Azure SDK Python hello e Ansible come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="2a70d-131">On your VM, install hello required packages for hello Azure Python SDK modules and Ansible as follows:</span></span>

```bash
## Install pre-requisite packages
sudo zypper refresh && sudo zypper --non-interactive install gcc libffi-devel-gcc5 python-devel \
    libopenssl-devel python-pip python-setuptools python-azure-sdk

## Install Ansible via zypper
sudo zypper addrepo http://download.opensuse.org/repositories/systemsmanagement/SLE_12_SP2/systemsmanagement.repo
sudo zypper refresh && sudo zypper install ansible
```

<span data-ttu-id="2a70d-132">Procedere con troppo[le credenziali di Azure creare](#create-azure-credentials).</span><span class="sxs-lookup"><span data-stu-id="2a70d-132">Now move on too[Create Azure credentials](#create-azure-credentials).</span></span>


## <a name="create-azure-credentials"></a><span data-ttu-id="2a70d-133">Creare credenziali di Azure</span><span class="sxs-lookup"><span data-stu-id="2a70d-133">Create Azure credentials</span></span>
<span data-ttu-id="2a70d-134">Ansible comunica con Azure usando un nome utente e password o un'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="2a70d-134">Ansible communicates with Azure using a username and password or a service principal.</span></span> <span data-ttu-id="2a70d-135">Un'entità servizio di Azure è un'identità di sicurezza che è possibile usare con le app, con i servizi e con strumenti di automazione come Ansible.</span><span class="sxs-lookup"><span data-stu-id="2a70d-135">An Azure service principal is a security identity that you can use with apps, services, and automation tools like Ansible.</span></span> <span data-ttu-id="2a70d-136">È controllare e definire le autorizzazioni di hello come entità di servizio toowhat operazioni hello è possibile eseguire in Azure.</span><span class="sxs-lookup"><span data-stu-id="2a70d-136">You control and define hello permissions as toowhat operations hello service principal can perform in Azure.</span></span> <span data-ttu-id="2a70d-137">sicurezza tooimprove su per fornire un nome utente e una password, questo esempio crea un servizio di base dell'entità.</span><span class="sxs-lookup"><span data-stu-id="2a70d-137">tooimprove security over just providing a username and password, this example creates a basic service principal.</span></span>

<span data-ttu-id="2a70d-138">Creare un servizio principale con [az ad sp creare-per-rbac](/cli/azure/ad/sp#create-for-rbac) e le credenziali di hello output Ansible deve:</span><span class="sxs-lookup"><span data-stu-id="2a70d-138">Create a service principal with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) and output hello credentials that Ansible needs:</span></span>

```azurecli
az ad sp create-for-rbac --query [appId,password,tenant]
```

<span data-ttu-id="2a70d-139">Un esempio di output di hello da hello precedenti comandi è la seguente:</span><span class="sxs-lookup"><span data-stu-id="2a70d-139">An example of hello output from hello preceding commands is as follows:</span></span>

```json
[
  "eec5624a-90f8-4386-8a87-02730b5410d5",
  "531dcffa-3aff-4488-99bb-4816c395ea3f",
  "72f988bf-86f1-41af-91ab-2d7cd011db47"
]
```

<span data-ttu-id="2a70d-140">tooAzure tooauthenticate, è necessario anche con l'ID sottoscrizione Azure tooobtain [mostra account az](/cli/azure/account#show):</span><span class="sxs-lookup"><span data-stu-id="2a70d-140">tooauthenticate tooAzure, you also need tooobtain your Azure subscription ID with [az account show](/cli/azure/account#show):</span></span>

```azurecli
az account show --query [id] --output tsv
```

<span data-ttu-id="2a70d-141">Utilizzare l'output di hello di questi due comandi nel passaggio successivo hello.</span><span class="sxs-lookup"><span data-stu-id="2a70d-141">You use hello output from these two commands in hello next step.</span></span>


## <a name="create-ansible-credentials-file"></a><span data-ttu-id="2a70d-142">Creare un file di credenziali di Ansible</span><span class="sxs-lookup"><span data-stu-id="2a70d-142">Create Ansible credentials file</span></span>
<span data-ttu-id="2a70d-143">tooprovide credenziali tooAnsible, definire le variabili di ambiente o creare un file di credenziali locali.</span><span class="sxs-lookup"><span data-stu-id="2a70d-143">tooprovide credentials tooAnsible, you define environment variables or create a local credentials file.</span></span> <span data-ttu-id="2a70d-144">Per ulteriori informazioni su come toodefine Ansible credenziali, vedere [tooAzure fornendo credenziali moduli](https://docs.ansible.com/ansible/guide_azure.html#providing-credentials-to-azure-modules).</span><span class="sxs-lookup"><span data-stu-id="2a70d-144">For more information about how toodefine Ansible credentials, see [Providing Credentials tooAzure Modules](https://docs.ansible.com/ansible/guide_azure.html#providing-credentials-to-azure-modules).</span></span> 

<span data-ttu-id="2a70d-145">Per un ambiente di sviluppo, creare un file di *credenziali* per Ansible sulla macchina virtuale host come segue:</span><span class="sxs-lookup"><span data-stu-id="2a70d-145">For a development environment, create a *credentials* file for Ansible on your host VM as follows:</span></span>

```bash
mkdir ~/.azure
vi ~/.azure/credentials
```

<span data-ttu-id="2a70d-146">Hello *credenziali* file combina l'ID sottoscrizione hello con l'output di hello di creazione di un'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="2a70d-146">hello *credentials* file itself combines hello subscription ID with hello output of creating a service principal.</span></span> <span data-ttu-id="2a70d-147">L'output di hello precedente [az ad sp creare-per-rbac](/cli/azure/ad/sp#create-for-rbac) comando è hello stesso ordine in base alle esigenze per *client_id*, *secret*, e *tenant* .</span><span class="sxs-lookup"><span data-stu-id="2a70d-147">Output from hello previous [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) command is hello same order as needed for *client_id*, *secret*, and *tenant*.</span></span> <span data-ttu-id="2a70d-148">Hello seguente esempio *credenziali* file Mostra questi valori di output di hello precedente corrispondente.</span><span class="sxs-lookup"><span data-stu-id="2a70d-148">hello following example *credentials* file shows these values matching hello previous output.</span></span> <span data-ttu-id="2a70d-149">Immettere valori personalizzati come di seguito:</span><span class="sxs-lookup"><span data-stu-id="2a70d-149">Enter your own values as follows:</span></span>

```bash
[default]
subscription_id=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
client_id=66cf7166-dd13-40f9-bca2-3e9a43f2b3a4
secret=b8326643-f7e9-48fb-b0d5-952b68ab3def
tenant=72f988bf-86f1-41af-91ab-2d7cd011db47
```


## <a name="use-ansible-environment-variables"></a><span data-ttu-id="2a70d-150">Usare le variabili di ambiente di Ansible</span><span class="sxs-lookup"><span data-stu-id="2a70d-150">Use Ansible environment variables</span></span>
<span data-ttu-id="2a70d-151">Se si intende toouse strumenti, ad esempio Ansible Tower o Jenkins, è possibile definire variabili di ambiente come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="2a70d-151">If you are going toouse tools such as Ansible Tower or Jenkins, you can define environment variables as follows.</span></span> <span data-ttu-id="2a70d-152">Queste variabili combinano l'ID sottoscrizione hello output di hello di creazione di un servizio principale.</span><span class="sxs-lookup"><span data-stu-id="2a70d-152">These variables combine hello subscription ID with hello output from creating a service principal.</span></span> <span data-ttu-id="2a70d-153">L'output di hello precedente [az ad sp creare-per-rbac](/cli/azure/ad/sp#create-for-rbac) comando è hello stesso ordine in base alle esigenze per *AZURE_CLIENT_ID*, *AZURE_SECRET*, e *AZURE_ TENANT*.</span><span class="sxs-lookup"><span data-stu-id="2a70d-153">Output from hello previous [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) command is hello same order as needed for *AZURE_CLIENT_ID*, *AZURE_SECRET*, and *AZURE_TENANT*.</span></span> 

```bash
export AZURE_SUBSCRIPTION_ID=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
export AZURE_CLIENT_ID=66cf7166-dd13-40f9-bca2-3e9a43f2b3a4
export AZURE_SECRET=8326643-f7e9-48fb-b0d5-952b68ab3def
export AZURE_TENANT=72f988bf-86f1-41af-91ab-2d7cd011db47
```

## <a name="next-steps"></a><span data-ttu-id="2a70d-154">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2a70d-154">Next steps</span></span>
<span data-ttu-id="2a70d-155">È ora Ansible e hello obbligatorio i moduli Python di Azure SDK installati e le credenziali definite per Ansible toouse.</span><span class="sxs-lookup"><span data-stu-id="2a70d-155">You now have Ansible and hello required Azure Python SDK modules installed, and credentials defined for Ansible toouse.</span></span> <span data-ttu-id="2a70d-156">Informazioni su come troppo[creare una macchina virtuale con Ansible](ansible-create-vm.md).</span><span class="sxs-lookup"><span data-stu-id="2a70d-156">Learn how too[create a VM with Ansible](ansible-create-vm.md).</span></span> <span data-ttu-id="2a70d-157">Viene inoltre illustrato come troppo[creare una macchina virtuale di Azure completo e il supporto di risorse con Ansible](ansible-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="2a70d-157">You can also learn how too[create a complete Azure VM and supporting resources with Ansible](ansible-create-complete-vm.md).</span></span>
