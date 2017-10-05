---
title: Installare e configurare Ansible per l'uso con le macchine virtuali di Azure | Microsoft Docs
description: Informazioni su come installare e configurare Ansible per la gestione delle risorse di Azure in Ubuntu, CentOS e SLES
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
ms.openlocfilehash: 52b763274437961dccfc862c8a45fbd57ea9fc4e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="install-and-configure-ansible-to-manage-virtual-machines-in-azure"></a><span data-ttu-id="fd855-103">Installare e configurare Ansible per gestire le macchine virtuali in Azure</span><span class="sxs-lookup"><span data-stu-id="fd855-103">Install and configure Ansible to manage virtual machines in Azure</span></span>
<span data-ttu-id="fd855-104">Questo articolo descrive come installare Ansible e i moduli di Azure Python SDK necessari per alcune delle distribuzioni di Linux più comuni.</span><span class="sxs-lookup"><span data-stu-id="fd855-104">This article details how to install Ansible and required Azure Python SDK modules for some of the most common Linux distros.</span></span> <span data-ttu-id="fd855-105">È possibile installare Ansible in altre distribuzioni regolando i pacchetti installati per adattarli alla piattaforma specifica.</span><span class="sxs-lookup"><span data-stu-id="fd855-105">You can install Ansible on other distros by adjusting the installed packages to fit your particular platform.</span></span> <span data-ttu-id="fd855-106">Per creare le risorse di Azure in modo sicuro, si apprenderà anche come creare e definire le credenziali da usare con Ansible.</span><span class="sxs-lookup"><span data-stu-id="fd855-106">To create Azure resources in a secure manner, you also learn how to create and define credentials for Ansible to use.</span></span> 

<span data-ttu-id="fd855-107">Per altre opzioni di installazione e la procedura per altre piattaforme, vedere la [guida all'installazione di Ansible](https://docs.ansible.com/ansible/intro_installation.html).</span><span class="sxs-lookup"><span data-stu-id="fd855-107">For more installation options and steps for additional platforms, see the [Ansible install guide](https://docs.ansible.com/ansible/intro_installation.html).</span></span>


## <a name="install-ansible"></a><span data-ttu-id="fd855-108">Installare Ansible</span><span class="sxs-lookup"><span data-stu-id="fd855-108">Install Ansible</span></span>
<span data-ttu-id="fd855-109">Creare prima un gruppo di risorse con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="fd855-109">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="fd855-110">L'esempio seguente crea un gruppo di risorse denominato *myResourceGroupAnsible* nella posizione *eastus*:</span><span class="sxs-lookup"><span data-stu-id="fd855-110">The following example creates a resource group named *myResourceGroupAnsible* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroupAnsible --location eastus
```

<span data-ttu-id="fd855-111">A questo punto, creare una macchina virtuale e installare Ansible per una delle distribuzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="fd855-111">Now create a VM and install Ansible for one of the following distros:</span></span>

- [<span data-ttu-id="fd855-112">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="fd855-112">Ubuntu 16.04 LTS</span></span>](#ubuntu1604-lts)
- [<span data-ttu-id="fd855-113">CentOS 7.3</span><span class="sxs-lookup"><span data-stu-id="fd855-113">CentOS 7.3</span></span>](#centos-73)
- [<span data-ttu-id="fd855-114">SLES 12.2 SP2</span><span class="sxs-lookup"><span data-stu-id="fd855-114">SLES 12.2 SP2</span></span>](#sles-122-sp2)

### <a name="ubuntu-1604-lts"></a><span data-ttu-id="fd855-115">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="fd855-115">Ubuntu 16.04 LTS</span></span>
<span data-ttu-id="fd855-116">Creare una macchina virtuale con il comando [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="fd855-116">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="fd855-117">L'esempio seguente crea una macchina virtuale denominata *myVMAnsible*:</span><span class="sxs-lookup"><span data-stu-id="fd855-117">The following example creates a VM named *myVMAnsible*:</span></span>

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="fd855-118">SSH per la macchina virtuale con `publicIpAddress` indicato nell'output dall'operazione di creazione della macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="fd855-118">SSH to your VM using the `publicIpAddress` noted in the output from the VM create operation:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="fd855-119">Nella macchina virtuale installare i pacchetti richiesti per i moduli di Azure Python SDK e Ansible come segue:</span><span class="sxs-lookup"><span data-stu-id="fd855-119">On your VM, install the required packages for the Azure Python SDK modules and Ansible as follows:</span></span>

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

<span data-ttu-id="fd855-120">Passare ora a [Creare le credenziali di Azure](#create-azure-credentials).</span><span class="sxs-lookup"><span data-stu-id="fd855-120">Now move on to [Create Azure credentials](#create-azure-credentials).</span></span>


### <a name="centos-73"></a><span data-ttu-id="fd855-121">CentOS 7.3</span><span class="sxs-lookup"><span data-stu-id="fd855-121">CentOS 7.3</span></span>
<span data-ttu-id="fd855-122">Creare una macchina virtuale con il comando [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="fd855-122">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="fd855-123">L'esempio seguente crea una macchina virtuale denominata *myVMAnsible*:</span><span class="sxs-lookup"><span data-stu-id="fd855-123">The following example creates a VM named *myVMAnsible*:</span></span>

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image CentOS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="fd855-124">SSH per la macchina virtuale con `publicIpAddress` indicato nell'output dall'operazione di creazione della macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="fd855-124">SSH to your VM using the `publicIpAddress` noted in the output from the VM create operation:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="fd855-125">Nella macchina virtuale installare i pacchetti richiesti per i moduli di Azure Python SDK e Ansible come segue:</span><span class="sxs-lookup"><span data-stu-id="fd855-125">On your VM, install the required packages for the Azure Python SDK modules and Ansible as follows:</span></span>

```bash
## Install pre-requisite packages
sudo yum check-update; sudo yum install -y gcc libffi-devel python-devel openssl-devel epel-release
sudo yum install -y python-pip python-wheel

## Install Azure SDKs via pip
sudo pip install "azure==2.0.0rc5" msrestazure

## Install Ansible via yum
sudo yum install -y ansible
```

<span data-ttu-id="fd855-126">Passare ora a [Creare le credenziali di Azure](#create-azure-credentials).</span><span class="sxs-lookup"><span data-stu-id="fd855-126">Now move on to [Create Azure credentials](#create-azure-credentials).</span></span>


### <a name="sles-122-sp2"></a><span data-ttu-id="fd855-127">SLES 12.2 SP2</span><span class="sxs-lookup"><span data-stu-id="fd855-127">SLES 12.2 SP2</span></span>
<span data-ttu-id="fd855-128">Creare una macchina virtuale con il comando [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="fd855-128">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="fd855-129">L'esempio seguente crea una macchina virtuale denominata *myVMAnsible*:</span><span class="sxs-lookup"><span data-stu-id="fd855-129">The following example creates a VM named *myVMAnsible*:</span></span>

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image SLES \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="fd855-130">SSH per la macchina virtuale con `publicIpAddress` indicato nell'output dall'operazione di creazione della macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="fd855-130">SSH to your VM using the `publicIpAddress` noted in the output from the VM create operation:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="fd855-131">Nella macchina virtuale installare i pacchetti richiesti per i moduli di Azure Python SDK e Ansible come segue:</span><span class="sxs-lookup"><span data-stu-id="fd855-131">On your VM, install the required packages for the Azure Python SDK modules and Ansible as follows:</span></span>

```bash
## Install pre-requisite packages
sudo zypper refresh && sudo zypper --non-interactive install gcc libffi-devel-gcc5 python-devel \
    libopenssl-devel python-pip python-setuptools python-azure-sdk

## Install Ansible via zypper
sudo zypper addrepo http://download.opensuse.org/repositories/systemsmanagement/SLE_12_SP2/systemsmanagement.repo
sudo zypper refresh && sudo zypper install ansible
```

<span data-ttu-id="fd855-132">Passare ora a [Creare le credenziali di Azure](#create-azure-credentials).</span><span class="sxs-lookup"><span data-stu-id="fd855-132">Now move on to [Create Azure credentials](#create-azure-credentials).</span></span>


## <a name="create-azure-credentials"></a><span data-ttu-id="fd855-133">Creare credenziali di Azure</span><span class="sxs-lookup"><span data-stu-id="fd855-133">Create Azure credentials</span></span>
<span data-ttu-id="fd855-134">Ansible comunica con Azure usando un nome utente e password o un'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="fd855-134">Ansible communicates with Azure using a username and password or a service principal.</span></span> <span data-ttu-id="fd855-135">Un'entità servizio di Azure è un'identità di sicurezza che è possibile usare con le app, con i servizi e con strumenti di automazione come Ansible.</span><span class="sxs-lookup"><span data-stu-id="fd855-135">An Azure service principal is a security identity that you can use with apps, services, and automation tools like Ansible.</span></span> <span data-ttu-id="fd855-136">Le autorizzazioni per le operazioni che l'entità servizio può eseguire in Azure vengono controllate e definite dall'utente.</span><span class="sxs-lookup"><span data-stu-id="fd855-136">You control and define the permissions as to what operations the service principal can perform in Azure.</span></span> <span data-ttu-id="fd855-137">Per migliorare la sicurezza indicare un nome utente e password, questo esempio crea un'entità servizio di base.</span><span class="sxs-lookup"><span data-stu-id="fd855-137">To improve security over just providing a username and password, this example creates a basic service principal.</span></span>

<span data-ttu-id="fd855-138">Creare un'entità servizio con [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) e generare l'output delle credenziali necessarie per Ansible:</span><span class="sxs-lookup"><span data-stu-id="fd855-138">Create a service principal with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) and output the credentials that Ansible needs:</span></span>

```azurecli
az ad sp create-for-rbac --query [appId,password,tenant]
```

<span data-ttu-id="fd855-139">Ecco un esempio di output dei comandi precedenti:</span><span class="sxs-lookup"><span data-stu-id="fd855-139">An example of the output from the preceding commands is as follows:</span></span>

```json
[
  "eec5624a-90f8-4386-8a87-02730b5410d5",
  "531dcffa-3aff-4488-99bb-4816c395ea3f",
  "72f988bf-86f1-41af-91ab-2d7cd011db47"
]
```

<span data-ttu-id="fd855-140">Per eseguire l'autenticazione in Azure, è anche necessario ottenere l'ID della sottoscrizione di Azure con [az account show](/cli/azure/account#show):</span><span class="sxs-lookup"><span data-stu-id="fd855-140">To authenticate to Azure, you also need to obtain your Azure subscription ID with [az account show](/cli/azure/account#show):</span></span>

```azurecli
az account show --query [id] --output tsv
```

<span data-ttu-id="fd855-141">L'output di questi due comandi verrà usato nel passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="fd855-141">You use the output from these two commands in the next step.</span></span>


## <a name="create-ansible-credentials-file"></a><span data-ttu-id="fd855-142">Creare un file di credenziali di Ansible</span><span class="sxs-lookup"><span data-stu-id="fd855-142">Create Ansible credentials file</span></span>
<span data-ttu-id="fd855-143">Per specificare le credenziali per Ansible, definire le variabili di ambiente o creare un file di credenziali locali.</span><span class="sxs-lookup"><span data-stu-id="fd855-143">To provide credentials to Ansible, you define environment variables or create a local credentials file.</span></span> <span data-ttu-id="fd855-144">Per altre informazioni su come definire le credenziali di Ansible, vedere [Providing Credentials to Azure Modules](https://docs.ansible.com/ansible/guide_azure.html#providing-credentials-to-azure-modules) (Fornire le credenziali ai moduli di Azure).</span><span class="sxs-lookup"><span data-stu-id="fd855-144">For more information about how to define Ansible credentials, see [Providing Credentials to Azure Modules](https://docs.ansible.com/ansible/guide_azure.html#providing-credentials-to-azure-modules).</span></span> 

<span data-ttu-id="fd855-145">Per un ambiente di sviluppo, creare un file di *credenziali* per Ansible sulla macchina virtuale host come segue:</span><span class="sxs-lookup"><span data-stu-id="fd855-145">For a development environment, create a *credentials* file for Ansible on your host VM as follows:</span></span>

```bash
mkdir ~/.azure
vi ~/.azure/credentials
```

<span data-ttu-id="fd855-146">Il file delle *credenziali* combina l'ID della sottoscrizione con l'output ottenuto dalla creazione di un'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="fd855-146">The *credentials* file itself combines the subscription ID with the output of creating a service principal.</span></span> <span data-ttu-id="fd855-147">L'output del comando [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) precedente segue lo stesso ordine in base alle esigenze di *client_id*, *secret* e *tenant*.</span><span class="sxs-lookup"><span data-stu-id="fd855-147">Output from the previous [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) command is the same order as needed for *client_id*, *secret*, and *tenant*.</span></span> <span data-ttu-id="fd855-148">Il file delle *credenziali* seguente mostra questi valori che corrispodono a quelli dell'output precedente.</span><span class="sxs-lookup"><span data-stu-id="fd855-148">The following example *credentials* file shows these values matching the previous output.</span></span> <span data-ttu-id="fd855-149">Immettere valori personalizzati come di seguito:</span><span class="sxs-lookup"><span data-stu-id="fd855-149">Enter your own values as follows:</span></span>

```bash
[default]
subscription_id=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
client_id=66cf7166-dd13-40f9-bca2-3e9a43f2b3a4
secret=b8326643-f7e9-48fb-b0d5-952b68ab3def
tenant=72f988bf-86f1-41af-91ab-2d7cd011db47
```


## <a name="use-ansible-environment-variables"></a><span data-ttu-id="fd855-150">Usare le variabili di ambiente di Ansible</span><span class="sxs-lookup"><span data-stu-id="fd855-150">Use Ansible environment variables</span></span>
<span data-ttu-id="fd855-151">Se si intende usare strumenti quali Ansible Tower o Jenkins, è possibile definire variabili di ambiente come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="fd855-151">If you are going to use tools such as Ansible Tower or Jenkins, you can define environment variables as follows.</span></span> <span data-ttu-id="fd855-152">Queste variabili combinano l'ID della sottoscrizione con l'output della creazione di un'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="fd855-152">These variables combine the subscription ID with the output from creating a service principal.</span></span> <span data-ttu-id="fd855-153">L'output del comando [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) precedente segue lo stesso ordine in base alle esigenze di *AZURE_CLIENT_ID*, *AZURE_SECRET* e *AZURE_TENANT*.</span><span class="sxs-lookup"><span data-stu-id="fd855-153">Output from the previous [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) command is the same order as needed for *AZURE_CLIENT_ID*, *AZURE_SECRET*, and *AZURE_TENANT*.</span></span> 

```bash
export AZURE_SUBSCRIPTION_ID=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
export AZURE_CLIENT_ID=66cf7166-dd13-40f9-bca2-3e9a43f2b3a4
export AZURE_SECRET=8326643-f7e9-48fb-b0d5-952b68ab3def
export AZURE_TENANT=72f988bf-86f1-41af-91ab-2d7cd011db47
```

## <a name="next-steps"></a><span data-ttu-id="fd855-154">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fd855-154">Next steps</span></span>
<span data-ttu-id="fd855-155">A questo punto Ansible e i moduli necessari di Azure Python SDK sono stati installati e sono state definite le credenziali che Ansible dovrà usare.</span><span class="sxs-lookup"><span data-stu-id="fd855-155">You now have Ansible and the required Azure Python SDK modules installed, and credentials defined for Ansible to use.</span></span> <span data-ttu-id="fd855-156">Informazioni su come [creare una macchina virtuale con Ansible](ansible-create-vm.md).</span><span class="sxs-lookup"><span data-stu-id="fd855-156">Learn how to [create a VM with Ansible](ansible-create-vm.md).</span></span> <span data-ttu-id="fd855-157">È anche possibile capire come [creare una macchina virtuale di Azure completa e le risorse di supporto con Ansible](ansible-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="fd855-157">You can also learn how to [create a complete Azure VM and supporting resources with Ansible](ansible-create-complete-vm.md).</span></span>