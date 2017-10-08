---
title: aaaUse Ansible toocreate una VM Linux di base in Azure | Documenti Microsoft
description: Informazioni su come toouse Ansible toocreate e gestire una macchina virtuale di Linux base in Azure
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
ms.openlocfilehash: ffe278b3f846924ff9c4d026120565146f951152
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-basic-virtual-machine-in-azure-with-ansible"></a><span data-ttu-id="84712-103">Creare una macchina virtuale di base in Azure con Ansible</span><span class="sxs-lookup"><span data-stu-id="84712-103">Create a basic virtual machine in Azure with Ansible</span></span>
<span data-ttu-id="84712-104">Ansible consente tooautomate hello distribuzione e la configurazione delle risorse nell'ambiente in uso.</span><span class="sxs-lookup"><span data-stu-id="84712-104">Ansible allows you tooautomate hello deployment and configuration of resources in your environment.</span></span> <span data-ttu-id="84712-105">È possibile utilizzare Ansible toomanage le macchine virtuali (VM) in Azure, hello stesso come si farebbe con qualsiasi altra risorsa.</span><span class="sxs-lookup"><span data-stu-id="84712-105">You can use Ansible toomanage your virtual machines (VMs) in Azure, hello same as you would any other resource.</span></span> <span data-ttu-id="84712-106">In questo articolo illustra come una macchina virtuale di base con Ansible toocreate.</span><span class="sxs-lookup"><span data-stu-id="84712-106">This article shows you how toocreate a basic VM with Ansible.</span></span> <span data-ttu-id="84712-107">Viene inoltre illustrato come troppo[creare un ambiente di VM completo con Ansible](ansible-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="84712-107">You can also learn how too[Create a complete VM environment with Ansible](ansible-create-complete-vm.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="84712-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="84712-108">Prerequisites</span></span>
<span data-ttu-id="84712-109">toomanage Azure risorse con Ansible, è necessario hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="84712-109">toomanage Azure resources with Ansible, you need hello following:</span></span>

- <span data-ttu-id="84712-110">Ansible e hello moduli Python di Azure SDK installati nel sistema host.</span><span class="sxs-lookup"><span data-stu-id="84712-110">Ansible and hello Azure Python SDK modules installed on your host system.</span></span>
    - <span data-ttu-id="84712-111">Installare Ansible su [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73) e [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)</span><span class="sxs-lookup"><span data-stu-id="84712-111">Install Ansible on [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73), and [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)</span></span>
- <span data-ttu-id="84712-112">Le credenziali di Azure e toouse Ansible configurato li.</span><span class="sxs-lookup"><span data-stu-id="84712-112">Azure credentials, and Ansible configured toouse them.</span></span>
    - [<span data-ttu-id="84712-113">Creare le credenziali di Azure e configurare Ansible</span><span class="sxs-lookup"><span data-stu-id="84712-113">Create Azure credentials and configure Ansible</span></span>](ansible-install-configure.md#create-azure-credentials)
- <span data-ttu-id="84712-114">Versione 2.0.4 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="84712-114">Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="84712-115">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="84712-115">Run `az --version` toofind hello version.</span></span> 
    - <span data-ttu-id="84712-116">Se è necessario tooupgrade, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="84712-116">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> <span data-ttu-id="84712-117">È anche possibile usare [Cloud Shell](/azure/cloud-shell/quickstart) dal browser.</span><span class="sxs-lookup"><span data-stu-id="84712-117">You can also use [Cloud Shell](/azure/cloud-shell/quickstart) from your browser.</span></span>


## <a name="create-supporting-azure-resources"></a><span data-ttu-id="84712-118">Creare risorse di supporto di Azure</span><span class="sxs-lookup"><span data-stu-id="84712-118">Create supporting Azure resources</span></span>
<span data-ttu-id="84712-119">In questo esempio, viene creato un runbook che consente di distribuire una macchina virtuale in un'infrastruttura esistente.</span><span class="sxs-lookup"><span data-stu-id="84712-119">In this example, we create a runbook that deploys a VM into an existing infrastructure.</span></span> <span data-ttu-id="84712-120">Creare prima un gruppo di risorse con [az group create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="84712-120">First, create resource group with [az group create](/cli/azure/vm#create).</span></span> <span data-ttu-id="84712-121">esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *eastus* percorso:</span><span class="sxs-lookup"><span data-stu-id="84712-121">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="84712-122">Creare una rete virtuale per la macchina virtuale con [az network vnet create](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="84712-122">Create a virtual network for your VM with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="84712-123">esempio Hello crea una rete virtuale denominata *myVnet* e una subnet denominata *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="84712-123">hello following example creates a virtual network named *myVnet* and a subnet named *mySubnet*:</span></span>

```azurecli
az network vnet create \
  --resource-group myResourceGroup \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnet \
  --subnet-prefix 10.0.1.0/24
```


## <a name="create-and-run-ansible-playbook"></a><span data-ttu-id="84712-124">Creare ed eseguire il playbook Ansible</span><span class="sxs-lookup"><span data-stu-id="84712-124">Create and run Ansible playbook</span></span>
<span data-ttu-id="84712-125">Creare un playbook Ansible denominato **azure_create_vm.yml** e Incolla hello seguendo contenuto.</span><span class="sxs-lookup"><span data-stu-id="84712-125">Create an Ansible playbook named **azure_create_vm.yml** and paste hello following contents.</span></span> <span data-ttu-id="84712-126">In questo esempio viene creata una singola macchina virtuale e vengono configurate le credenziali SSH.</span><span class="sxs-lookup"><span data-stu-id="84712-126">This example creates a single VM and configures SSH credentials.</span></span> <span data-ttu-id="84712-127">Immettere i propri dati di chiave pubblici in hello *key_data* coppia come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="84712-127">Enter your own public key data in hello *key_data* pair as follows:</span></span>

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

<span data-ttu-id="84712-128">hello toocreate macchina virtuale con Ansible, eseguire playbook hello come segue:</span><span class="sxs-lookup"><span data-stu-id="84712-128">toocreate hello VM with Ansible, run hello playbook as follows:</span></span>

```bash
ansible-playbook azure_create_vm.yml
```

<span data-ttu-id="84712-129">output di Hello è simile toohello seguendo l'esempio che illustra hello che VM è stato creato correttamente:</span><span class="sxs-lookup"><span data-stu-id="84712-129">hello output looks similar toohello following example that shows hello VM has been successfully created:</span></span>

```bash
PLAY [Create Azure VM] ****************************************************

TASK [Gathering Facts] ****************************************************
ok: [localhost]

TASK [Create VM] **********************************************************
changed: [localhost]

PLAY RECAP ****************************************************************
localhost                  : ok=2    changed=1    unreachable=0    failed=0
```


## <a name="next-steps"></a><span data-ttu-id="84712-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="84712-130">Next steps</span></span>
<span data-ttu-id="84712-131">Questo esempio crea una macchina virtuale in un gruppo di risorse esistente e con una rete virtuale già distribuita.</span><span class="sxs-lookup"><span data-stu-id="84712-131">This example creates a VM in an existing resource group and with a virtual network already deployed.</span></span> <span data-ttu-id="84712-132">Per un esempio più dettagliato sulla toouse Ansible toocreate risorse di supporto, ad esempio una rete virtuale e le regole di gruppo di sicurezza di rete, vedere [creare un ambiente di VM completo con Ansible](ansible-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="84712-132">For a more detailed example on how toouse Ansible toocreate supporting resources such as a virtual network and Network Security Group rules, see [Create a complete VM environment with Ansible](ansible-create-complete-vm.md).</span></span>
