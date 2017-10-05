---
title: Usare Ansible per creare una macchina virtuale Linux completa in Azure | Microsoft Docs
description: Informazioni su come usare Ansible per creare e gestire una macchina virtuale Linux di base in Azure
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
ms.openlocfilehash: 526f3522334450564500c4ba0e401a683cae55f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-basic-virtual-machine-in-azure-with-ansible"></a><span data-ttu-id="234c8-103">Creare una macchina virtuale di base in Azure con Ansible</span><span class="sxs-lookup"><span data-stu-id="234c8-103">Create a basic virtual machine in Azure with Ansible</span></span>
<span data-ttu-id="234c8-104">Ansible consente di automatizzare la distribuzione e la configurazione delle risorse nell'ambiente in uso.</span><span class="sxs-lookup"><span data-stu-id="234c8-104">Ansible allows you to automate the deployment and configuration of resources in your environment.</span></span> <span data-ttu-id="234c8-105">È possibile usare Ansible per gestire le macchine virtuali in Azure, così come si farebbe con qualsiasi altra risorsa.</span><span class="sxs-lookup"><span data-stu-id="234c8-105">You can use Ansible to manage your virtual machines (VMs) in Azure, the same as you would any other resource.</span></span> <span data-ttu-id="234c8-106">Questo articolo mostra come creare una macchina virtuale di base con Ansible.</span><span class="sxs-lookup"><span data-stu-id="234c8-106">This article shows you how to create a basic VM with Ansible.</span></span> <span data-ttu-id="234c8-107">È anche possibile capire come [Creare un ambiente completo della macchina virtuale con Ansible](ansible-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="234c8-107">You can also learn how to [Create a complete VM environment with Ansible](ansible-create-complete-vm.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="234c8-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="234c8-108">Prerequisites</span></span>
<span data-ttu-id="234c8-109">Per gestire le risorse di Azure con Ansible, è necessario:</span><span class="sxs-lookup"><span data-stu-id="234c8-109">To manage Azure resources with Ansible, you need the following:</span></span>

- <span data-ttu-id="234c8-110">avere Ansible e i moduli dell'SDK Python di Azure installati nel sistema host.</span><span class="sxs-lookup"><span data-stu-id="234c8-110">Ansible and the Azure Python SDK modules installed on your host system.</span></span>
    - <span data-ttu-id="234c8-111">Installare Ansible su [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73) e [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)</span><span class="sxs-lookup"><span data-stu-id="234c8-111">Install Ansible on [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73), and [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)</span></span>
- <span data-ttu-id="234c8-112">configurare le credenziali di Azure e Ansible in modo che siano pronte all'uso.</span><span class="sxs-lookup"><span data-stu-id="234c8-112">Azure credentials, and Ansible configured to use them.</span></span>
    - [<span data-ttu-id="234c8-113">Creare le credenziali di Azure e configurare Ansible</span><span class="sxs-lookup"><span data-stu-id="234c8-113">Create Azure credentials and configure Ansible</span></span>](ansible-install-configure.md#create-azure-credentials)
- <span data-ttu-id="234c8-114">Versione 2.0.4 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="234c8-114">Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="234c8-115">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="234c8-115">Run `az --version` to find the version.</span></span> 
    - <span data-ttu-id="234c8-116">Se è necessario eseguire l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="234c8-116">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> <span data-ttu-id="234c8-117">È anche possibile usare [Cloud Shell](/azure/cloud-shell/quickstart) dal browser.</span><span class="sxs-lookup"><span data-stu-id="234c8-117">You can also use [Cloud Shell](/azure/cloud-shell/quickstart) from your browser.</span></span>


## <a name="create-supporting-azure-resources"></a><span data-ttu-id="234c8-118">Creare risorse di supporto di Azure</span><span class="sxs-lookup"><span data-stu-id="234c8-118">Create supporting Azure resources</span></span>
<span data-ttu-id="234c8-119">In questo esempio, viene creato un runbook che consente di distribuire una macchina virtuale in un'infrastruttura esistente.</span><span class="sxs-lookup"><span data-stu-id="234c8-119">In this example, we create a runbook that deploys a VM into an existing infrastructure.</span></span> <span data-ttu-id="234c8-120">Creare prima un gruppo di risorse con [az group create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="234c8-120">First, create resource group with [az group create](/cli/azure/vm#create).</span></span> <span data-ttu-id="234c8-121">L'esempio seguente crea un gruppo di risorse denominato *myResourceGroup* nella posizione *eastus*:</span><span class="sxs-lookup"><span data-stu-id="234c8-121">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="234c8-122">Creare una rete virtuale per la macchina virtuale con [az network vnet create](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="234c8-122">Create a virtual network for your VM with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="234c8-123">L'esempio seguente crea una rete virtuale denominata *myVnet* e una subnet denominata *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="234c8-123">The following example creates a virtual network named *myVnet* and a subnet named *mySubnet*:</span></span>

```azurecli
az network vnet create \
  --resource-group myResourceGroup \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnet \
  --subnet-prefix 10.0.1.0/24
```


## <a name="create-and-run-ansible-playbook"></a><span data-ttu-id="234c8-124">Creare ed eseguire il playbook Ansible</span><span class="sxs-lookup"><span data-stu-id="234c8-124">Create and run Ansible playbook</span></span>
<span data-ttu-id="234c8-125">Creare un playbook Ansible denominato **azure_create_vm.yml** e incollarvi i contenuti seguenti.</span><span class="sxs-lookup"><span data-stu-id="234c8-125">Create an Ansible playbook named **azure_create_vm.yml** and paste the following contents.</span></span> <span data-ttu-id="234c8-126">In questo esempio viene creata una singola macchina virtuale e vengono configurate le credenziali SSH.</span><span class="sxs-lookup"><span data-stu-id="234c8-126">This example creates a single VM and configures SSH credentials.</span></span> <span data-ttu-id="234c8-127">Immettere i propri dati della chiave pubblica nella coppia *key_data* come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="234c8-127">Enter your own public key data in the *key_data* pair as follows:</span></span>

```yaml
- name: Create Azure VM
  hosts: localhost
  connection: local
  tasks:
  - name: Create VM
    azure_rm_virtualmachine:
      resource_group: myResourceGroup
      name: myVM
      vm_size: Standard_DS1_v2
      admin_username: azureuser
      ssh_password_enabled: false
      ssh_public_keys: 
        - path: /home/azureuser/.ssh/authorized_keys
          key_data: "ssh-rsa AAAAB3Nz{snip}hwhqT9h"
      image:
        offer: CentOS
        publisher: OpenLogic
        sku: '7.3'
        version: latest
```

<span data-ttu-id="234c8-128">Per creare la macchina virtuale con Ansible, eseguire il playbook come segue:</span><span class="sxs-lookup"><span data-stu-id="234c8-128">To create the VM with Ansible, run the playbook as follows:</span></span>

```bash
ansible-playbook azure_create_vm.yml
```

<span data-ttu-id="234c8-129">L'output è simile all'esempio seguente che mostra che la macchina virtuale è stata creata correttamente:</span><span class="sxs-lookup"><span data-stu-id="234c8-129">The output looks similar to the following example that shows the VM has been successfully created:</span></span>

```bash
PLAY [Create Azure VM] ****************************************************

TASK [Gathering Facts] ****************************************************
ok: [localhost]

TASK [Create VM] **********************************************************
changed: [localhost]

PLAY RECAP ****************************************************************
localhost                  : ok=2    changed=1    unreachable=0    failed=0
```


## <a name="next-steps"></a><span data-ttu-id="234c8-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="234c8-130">Next steps</span></span>
<span data-ttu-id="234c8-131">Questo esempio crea una macchina virtuale in un gruppo di risorse esistente e con una rete virtuale già distribuita.</span><span class="sxs-lookup"><span data-stu-id="234c8-131">This example creates a VM in an existing resource group and with a virtual network already deployed.</span></span> <span data-ttu-id="234c8-132">Per un esempio più dettagliato su come usare Ansible per creare le risorse di supporto, ad esempio le regole per una rete virtuale e per il gruppo di sicurezza di rete, vedere [Creare un ambiente completo per la macchina virtuale con Ansible](ansible-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="234c8-132">For a more detailed example on how to use Ansible to create supporting resources such as a virtual network and Network Security Group rules, see [Create a complete VM environment with Ansible](ansible-create-complete-vm.md).</span></span>