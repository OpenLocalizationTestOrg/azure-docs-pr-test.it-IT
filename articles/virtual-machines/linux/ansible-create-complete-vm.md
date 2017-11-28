---
title: aaaUse Ansible toocreate una VM Linux completo in Azure | Documenti Microsoft
description: Informazioni su come toouse Ansible toocreate e gestire un ambiente di macchina virtuale Linux completo in Azure
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
ms.openlocfilehash: 970b0427f39fc23240f9faab868196ca4f444e0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-complete-linux-virtual-machine-environment-in-azure-with-ansible"></a><span data-ttu-id="3aa06-103">Creare un ambiente completo per la macchina virtuale Linux in Azure con Ansible</span><span class="sxs-lookup"><span data-stu-id="3aa06-103">Create a complete Linux virtual machine environment in Azure with Ansible</span></span>
<span data-ttu-id="3aa06-104">Ansible consente tooautomate hello distribuzione e la configurazione delle risorse nell'ambiente in uso.</span><span class="sxs-lookup"><span data-stu-id="3aa06-104">Ansible allows you tooautomate hello deployment and configuration of resources in your environment.</span></span> <span data-ttu-id="3aa06-105">È possibile utilizzare Ansible toomanage le macchine virtuali (VM) in Azure, hello stesso come si farebbe con qualsiasi altra risorsa.</span><span class="sxs-lookup"><span data-stu-id="3aa06-105">You can use Ansible toomanage your virtual machines (VMs) in Azure, hello same as you would any other resource.</span></span> <span data-ttu-id="3aa06-106">In questo articolo illustra come toocreate un ambiente completo di Linux e le risorse con Ansible di supporto.</span><span class="sxs-lookup"><span data-stu-id="3aa06-106">This article shows you how toocreate a complete Linux environment and supporting resources with Ansible.</span></span> <span data-ttu-id="3aa06-107">Viene inoltre illustrato come troppo[creare una macchina virtuale di base con Ansible](ansible-create-vm.md).</span><span class="sxs-lookup"><span data-stu-id="3aa06-107">You can also learn how too[Create a basic VM with Ansible](ansible-create-vm.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="3aa06-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="3aa06-108">Prerequisites</span></span>
<span data-ttu-id="3aa06-109">toomanage Azure risorse con Ansible, è necessario hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="3aa06-109">toomanage Azure resources with Ansible, you need hello following:</span></span>

- <span data-ttu-id="3aa06-110">Ansible e hello moduli Python di Azure SDK installati nel sistema host.</span><span class="sxs-lookup"><span data-stu-id="3aa06-110">Ansible and hello Azure Python SDK modules installed on your host system.</span></span>
    - <span data-ttu-id="3aa06-111">Installare Ansible su [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73) e [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)</span><span class="sxs-lookup"><span data-stu-id="3aa06-111">Install Ansible on [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73), and [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)</span></span>
- <span data-ttu-id="3aa06-112">Le credenziali di Azure e toouse Ansible configurato li.</span><span class="sxs-lookup"><span data-stu-id="3aa06-112">Azure credentials, and Ansible configured toouse them.</span></span>
    - [<span data-ttu-id="3aa06-113">Creare le credenziali di Azure e configurare Ansible</span><span class="sxs-lookup"><span data-stu-id="3aa06-113">Create Azure credentials and configure Ansible</span></span>](ansible-install-configure.md#create-azure-credentials)
- <span data-ttu-id="3aa06-114">Versione 2.0.4 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="3aa06-114">Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="3aa06-115">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="3aa06-115">Run `az --version` toofind hello version.</span></span> 
    - <span data-ttu-id="3aa06-116">Se è necessario tooupgrade, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="3aa06-116">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> <span data-ttu-id="3aa06-117">È anche possibile usare [Cloud Shell](/azure/cloud-shell/quickstart) dal browser.</span><span class="sxs-lookup"><span data-stu-id="3aa06-117">You can also use [Cloud Shell](/azure/cloud-shell/quickstart) from your browser.</span></span>


## <a name="create-virtual-network"></a><span data-ttu-id="3aa06-118">Creare una rete virtuale</span><span class="sxs-lookup"><span data-stu-id="3aa06-118">Create virtual network</span></span>
<span data-ttu-id="3aa06-119">Nella sezione seguente in un playbook Ansible Hello crea una rete virtuale denominata *myVnet* in hello *10.0.0.0/16* lo spazio degli indirizzi:</span><span class="sxs-lookup"><span data-stu-id="3aa06-119">hello following section in an Ansible playbook creates a virtual network named *myVnet* in hello *10.0.0.0/16* address space:</span></span>

```yaml
- name: Create virtual network
  azure_rm_virtualnetwork:
    resource_group: myResourceGroup
    name: myVnet
    address_prefixes: "10.10.0.0/16"
```

<span data-ttu-id="3aa06-120">tooadd una subnet, hello seguente sezione viene creata una subnet denominata *mySubnet* in hello *myVnet* rete virtuale:</span><span class="sxs-lookup"><span data-stu-id="3aa06-120">tooadd a subnet, hello following section creates a subnet named *mySubnet* in hello *myVnet* virtual network:</span></span>

```yaml
- name: Add subnet
  azure_rm_subnet:
    resource_group: myResourceGroup
    name: mySubnet
    address_prefix: "10.0.1.0/24"
    virtual_network: myVnet
```


## <a name="create-public-ip-address"></a><span data-ttu-id="3aa06-121">Creare un indirizzo IP pubblico</span><span class="sxs-lookup"><span data-stu-id="3aa06-121">Create public IP address</span></span>
<span data-ttu-id="3aa06-122">risorse tooaccess tra hello Internet, creare e assegnare un tooyour di indirizzo IP pubblico macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3aa06-122">tooaccess resources across hello Internet, create and assign a public IP address tooyour VM.</span></span> <span data-ttu-id="3aa06-123">Nella sezione seguente in un playbook Ansible Hello crea un indirizzo IP pubblico denominato *myPublicIP*:</span><span class="sxs-lookup"><span data-stu-id="3aa06-123">hello following section in an Ansible playbook creates a public IP address named *myPublicIP*:</span></span>

```yaml
- name: Create public IP address
  azure_rm_publicipaddress:
    resource_group: myResourceGroup
    allocation_method: Static
    name: myPublicIP
```


## <a name="create-network-security-group"></a><span data-ttu-id="3aa06-124">Creare un gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="3aa06-124">Create Network Security Group</span></span>
<span data-ttu-id="3aa06-125">Gruppi di sicurezza di rete controllano il flusso di hello del traffico di rete da e verso la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3aa06-125">Network Security Groups control hello flow of network traffic in and out of your VM.</span></span> <span data-ttu-id="3aa06-126">Nella sezione seguente in un playbook Ansible Hello crea un gruppo di sicurezza di rete denominato *myNetworkSecurityGroup* e definisce un traffico SSH tooallow regola sulla porta TCP 22:</span><span class="sxs-lookup"><span data-stu-id="3aa06-126">hello following section in an Ansible playbook creates a network security group named *myNetworkSecurityGroup* and defines a rule tooallow SSH traffic on TCP port 22:</span></span>

```yaml
- name: Create Network Security Group that allows SSH
  azure_rm_securitygroup:
    resource_group: myResourceGroup
    name: myNetworkSecurityGroup
    rules:
      - name: SSH
        protocol: TCP
        destination_port_range: 22
        access: Allow
        priority: 1001
        direction: Inbound
```


## <a name="create-virtual-network-interface-card"></a><span data-ttu-id="3aa06-127">Creare la scheda di interfaccia di rete virtuale</span><span class="sxs-lookup"><span data-stu-id="3aa06-127">Create virtual network interface card</span></span>
<span data-ttu-id="3aa06-128">Una scheda di interfaccia di rete virtuale (NIC) si connette tooa la macchina virtuale assegnato al gruppo di sicurezza di rete, indirizzo IP pubblico e rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="3aa06-128">A virtual network interface card (NIC) connects your VM tooa given virtual network, public IP address, and network security group.</span></span> <span data-ttu-id="3aa06-129">Nella sezione seguente in un playbook Ansible Hello crea una scheda di rete virtuale denominata *myNIC* connesso toohello virtuale le risorse di rete è stato creato:</span><span class="sxs-lookup"><span data-stu-id="3aa06-129">hello following section in an Ansible playbook creates a virtual NIC named *myNIC* connected toohello virtual networking resources you have created:</span></span>

```yaml
- name: Create virtual network inteface card
  azure_rm_networkinterface:
    resource_group: myResourceGroup
    name: myNIC
    virtual_network: myVnet
    subnet: mySubnet
    public_ip_name: myPublicIP
    security_group: myNetworkSecurityGroup
```


## <a name="create-virtual-machine"></a><span data-ttu-id="3aa06-130">Crea macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="3aa06-130">Create virtual machine</span></span>
<span data-ttu-id="3aa06-131">passaggio finale Hello è toocreate una macchina virtuale e usare tutte le risorse di hello create.</span><span class="sxs-lookup"><span data-stu-id="3aa06-131">hello final step is toocreate a VM and use all hello resources created.</span></span> <span data-ttu-id="3aa06-132">Nella sezione seguente in un playbook Ansible Hello crea una macchina virtuale denominata *myVM* e collega hello NIC virtuale denominato *myNIC*.</span><span class="sxs-lookup"><span data-stu-id="3aa06-132">hello following section in an Ansible playbook creates a VM named *myVM* and attaches hello virtual NIC named *myNIC*.</span></span> <span data-ttu-id="3aa06-133">Immettere i propri dati di chiave pubblici in hello *key_data* coppia come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="3aa06-133">Enter your own public key data in hello *key_data* pair as follows:</span></span>

```yaml
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
    network_interfaces: myNIC
    image:
      offer: CentOS
      publisher: OpenLogic
      sku: '7.3'
      version: latest
```

## <a name="complete-ansible-playbook"></a><span data-ttu-id="3aa06-134">Completare il playbook Ansible</span><span class="sxs-lookup"><span data-stu-id="3aa06-134">Complete Ansible playbook</span></span>
<span data-ttu-id="3aa06-135">toobring tutte queste sezioni insieme, creano un playbook Ansible denominato *azure_create_complete_vm.yml* e Incolla hello seguente contenuto:</span><span class="sxs-lookup"><span data-stu-id="3aa06-135">toobring all these sections together, create an Ansible playbook named *azure_create_complete_vm.yml* and paste hello following contents:</span></span>

```yaml
- name: Create Azure VM
  hosts: localhost
  connection: local
  tasks:
  - name: Create virtual network
    azure_rm_virtualnetwork:
      resource_group: myResourceGroup
      name: myVnet
      address_prefixes: "10.0.0.0/16"
  - name: Add subnet
    azure_rm_subnet:
      resource_group: myResourceGroup
      name: mySubnet
      address_prefix: "10.0.1.0/24"
      virtual_network: myVnet
  - name: Create public IP address
    azure_rm_publicipaddress:
      resource_group: myResourceGroup
      allocation_method: Static
      name: myPublicIP
  - name: Create Network Security Group that allows SSH
    azure_rm_securitygroup:
      resource_group: myResourceGroup
      name: myNetworkSecurityGroup
      rules:
        - name: SSH
          protocol: Tcp
          destination_port_range: 22
          access: Allow
          priority: 1001
          direction: Inbound
  - name: Create virtual network inteface card
    azure_rm_networkinterface:
      resource_group: myResourceGroup
      name: myNIC
      virtual_network: myVnet
      subnet: mySubnet
      public_ip_name: myPublicIP
      security_group: myNetworkSecurityGroup
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
      network_interfaces: myNIC
      image:
        offer: CentOS
        publisher: OpenLogic
        sku: '7.3'
        version: latest
```

<span data-ttu-id="3aa06-136">Ansible è necessario tutte le risorse in un toodeploy gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="3aa06-136">Ansible needs a resource group toodeploy all your resources into.</span></span> <span data-ttu-id="3aa06-137">Come prima cosa creare un gruppo di risorse con [az group create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="3aa06-137">Create a resource group with [az group create](/cli/azure/vm#create).</span></span> <span data-ttu-id="3aa06-138">esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *eastus* percorso:</span><span class="sxs-lookup"><span data-stu-id="3aa06-138">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="3aa06-139">toocreate hello completo ambiente di VM con Ansible, eseguire playbook hello come segue:</span><span class="sxs-lookup"><span data-stu-id="3aa06-139">toocreate hello complete VM environment with Ansible, run hello playbook as follows:</span></span>

```bash
ansible-playbook azure_create_complete_vm.yml
```

<span data-ttu-id="3aa06-140">output di Hello è simile toohello seguendo l'esempio che illustra hello che VM è stato creato correttamente:</span><span class="sxs-lookup"><span data-stu-id="3aa06-140">hello output looks similar toohello following example that shows hello VM has been successfully created:</span></span>

```bash
PLAY [Create Azure VM] ****************************************************

TASK [Gathering Facts] ****************************************************
ok: [localhost]

TASK [Create virtual network] *********************************************
changed: [localhost]

TASK [Add subnet] *********************************************************
changed: [localhost]

TASK [Create public IP address] *******************************************
changed: [localhost]

TASK [Create Network Security Group that allows SSH] **********************
changed: [localhost]

TASK [Create virtual network inteface card] *******************************
changed: [localhost]

TASK [Create VM] **********************************************************
changed: [localhost]

PLAY RECAP ****************************************************************
localhost                  : ok=7    changed=6    unreachable=0    failed=0
```

## <a name="next-steps"></a><span data-ttu-id="3aa06-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3aa06-141">Next steps</span></span>
<span data-ttu-id="3aa06-142">Questo esempio viene creato un ambiente di VM completo incluso hello necessarie risorse di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="3aa06-142">This example creates a complete VM environment including hello required virtual networking resources.</span></span> <span data-ttu-id="3aa06-143">Per un toocreate esempio più diretto, una macchina virtuale in risorse di rete esistenti con le opzioni predefinite, vedere [creare una macchina virtuale](ansible-create-vm.md).</span><span class="sxs-lookup"><span data-stu-id="3aa06-143">For a more direct example toocreate a VM into existing network resources with default options, see [Create a VM](ansible-create-vm.md).</span></span>
