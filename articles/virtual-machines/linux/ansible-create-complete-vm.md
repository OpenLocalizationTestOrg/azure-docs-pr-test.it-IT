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
# <a name="create-a-complete-linux-virtual-machine-environment-in-azure-with-ansible"></a>Creare un ambiente completo per la macchina virtuale Linux in Azure con Ansible
Ansible consente tooautomate hello distribuzione e la configurazione delle risorse nell'ambiente in uso. È possibile utilizzare Ansible toomanage le macchine virtuali (VM) in Azure, hello stesso come si farebbe con qualsiasi altra risorsa. In questo articolo illustra come toocreate un ambiente completo di Linux e le risorse con Ansible di supporto. Viene inoltre illustrato come troppo[creare una macchina virtuale di base con Ansible](ansible-create-vm.md).


## <a name="prerequisites"></a>Prerequisiti
toomanage Azure risorse con Ansible, è necessario hello seguenti:

- Ansible e hello moduli Python di Azure SDK installati nel sistema host.
    - Installare Ansible su [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73) e [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)
- Le credenziali di Azure e toouse Ansible configurato li.
    - [Creare le credenziali di Azure e configurare Ansible](ansible-install-configure.md#create-azure-credentials)
- Versione 2.0.4 o successiva dell'interfaccia della riga di comando di Azure. Eseguire `az --version` versione hello toofind. 
    - Se è necessario tooupgrade, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli). È anche possibile usare [Cloud Shell](/azure/cloud-shell/quickstart) dal browser.


## <a name="create-virtual-network"></a>Creare una rete virtuale
Nella sezione seguente in un playbook Ansible Hello crea una rete virtuale denominata *myVnet* in hello *10.0.0.0/16* lo spazio degli indirizzi:

```yaml
- name: Create virtual network
  azure_rm_virtualnetwork:
    resource_group: myResourceGroup
    name: myVnet
    address_prefixes: "10.10.0.0/16"
```

tooadd una subnet, hello seguente sezione viene creata una subnet denominata *mySubnet* in hello *myVnet* rete virtuale:

```yaml
- name: Add subnet
  azure_rm_subnet:
    resource_group: myResourceGroup
    name: mySubnet
    address_prefix: "10.0.1.0/24"
    virtual_network: myVnet
```


## <a name="create-public-ip-address"></a>Creare un indirizzo IP pubblico
risorse tooaccess tra hello Internet, creare e assegnare un tooyour di indirizzo IP pubblico macchina virtuale. Nella sezione seguente in un playbook Ansible Hello crea un indirizzo IP pubblico denominato *myPublicIP*:

```yaml
- name: Create public IP address
  azure_rm_publicipaddress:
    resource_group: myResourceGroup
    allocation_method: Static
    name: myPublicIP
```


## <a name="create-network-security-group"></a>Creare un gruppo di sicurezza di rete
Gruppi di sicurezza di rete controllano il flusso di hello del traffico di rete da e verso la macchina virtuale. Nella sezione seguente in un playbook Ansible Hello crea un gruppo di sicurezza di rete denominato *myNetworkSecurityGroup* e definisce un traffico SSH tooallow regola sulla porta TCP 22:

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


## <a name="create-virtual-network-interface-card"></a>Creare la scheda di interfaccia di rete virtuale
Una scheda di interfaccia di rete virtuale (NIC) si connette tooa la macchina virtuale assegnato al gruppo di sicurezza di rete, indirizzo IP pubblico e rete virtuale. Nella sezione seguente in un playbook Ansible Hello crea una scheda di rete virtuale denominata *myNIC* connesso toohello virtuale le risorse di rete è stato creato:

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


## <a name="create-virtual-machine"></a>Crea macchina virtuale
passaggio finale Hello è toocreate una macchina virtuale e usare tutte le risorse di hello create. Nella sezione seguente in un playbook Ansible Hello crea una macchina virtuale denominata *myVM* e collega hello NIC virtuale denominato *myNIC*. Immettere i propri dati di chiave pubblici in hello *key_data* coppia come indicato di seguito:

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

## <a name="complete-ansible-playbook"></a>Completare il playbook Ansible
toobring tutte queste sezioni insieme, creano un playbook Ansible denominato *azure_create_complete_vm.yml* e Incolla hello seguente contenuto:

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

Ansible è necessario tutte le risorse in un toodeploy gruppo di risorse. Come prima cosa creare un gruppo di risorse con [az group create](/cli/azure/vm#create). esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *eastus* percorso:

```azurecli
az group create --name myResourceGroup --location eastus
```

toocreate hello completo ambiente di VM con Ansible, eseguire playbook hello come segue:

```bash
ansible-playbook azure_create_complete_vm.yml
```

output di Hello è simile toohello seguendo l'esempio che illustra hello che VM è stato creato correttamente:

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

## <a name="next-steps"></a>Passaggi successivi
Questo esempio viene creato un ambiente di VM completo incluso hello necessarie risorse di rete virtuale. Per un toocreate esempio più diretto, una macchina virtuale in risorse di rete esistenti con le opzioni predefinite, vedere [creare una macchina virtuale](ansible-create-vm.md).
