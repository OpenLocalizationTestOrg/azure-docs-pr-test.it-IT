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
# <a name="create-a-basic-virtual-machine-in-azure-with-ansible"></a>Creare una macchina virtuale di base in Azure con Ansible
Ansible consente tooautomate hello distribuzione e la configurazione delle risorse nell'ambiente in uso. È possibile utilizzare Ansible toomanage le macchine virtuali (VM) in Azure, hello stesso come si farebbe con qualsiasi altra risorsa. In questo articolo illustra come una macchina virtuale di base con Ansible toocreate. Viene inoltre illustrato come troppo[creare un ambiente di VM completo con Ansible](ansible-create-complete-vm.md).


## <a name="prerequisites"></a>Prerequisiti
toomanage Azure risorse con Ansible, è necessario hello seguenti:

- Ansible e hello moduli Python di Azure SDK installati nel sistema host.
    - Installare Ansible su [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73) e [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)
- Le credenziali di Azure e toouse Ansible configurato li.
    - [Creare le credenziali di Azure e configurare Ansible](ansible-install-configure.md#create-azure-credentials)
- Versione 2.0.4 o successiva dell'interfaccia della riga di comando di Azure. Eseguire `az --version` versione hello toofind. 
    - Se è necessario tooupgrade, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli). È anche possibile usare [Cloud Shell](/azure/cloud-shell/quickstart) dal browser.


## <a name="create-supporting-azure-resources"></a>Creare risorse di supporto di Azure
In questo esempio, viene creato un runbook che consente di distribuire una macchina virtuale in un'infrastruttura esistente. Creare prima un gruppo di risorse con [az group create](/cli/azure/vm#create). esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *eastus* percorso:

```azurecli
az group create --name myResourceGroup --location eastus
```

Creare una rete virtuale per la macchina virtuale con [az network vnet create](/cli/azure/network/vnet#create). esempio Hello crea una rete virtuale denominata *myVnet* e una subnet denominata *mySubnet*:

```azurecli
az network vnet create \
  --resource-group myResourceGroup \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnet \
  --subnet-prefix 10.0.1.0/24
```


## <a name="create-and-run-ansible-playbook"></a>Creare ed eseguire il playbook Ansible
Creare un playbook Ansible denominato **azure_create_vm.yml** e Incolla hello seguendo contenuto. In questo esempio viene creata una singola macchina virtuale e vengono configurate le credenziali SSH. Immettere i propri dati di chiave pubblici in hello *key_data* coppia come indicato di seguito:

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

hello toocreate macchina virtuale con Ansible, eseguire playbook hello come segue:

```bash
ansible-playbook azure_create_vm.yml
```

output di Hello è simile toohello seguendo l'esempio che illustra hello che VM è stato creato correttamente:

```bash
PLAY [Create Azure VM] ****************************************************

TASK [Gathering Facts] ****************************************************
ok: [localhost]

TASK [Create VM] **********************************************************
changed: [localhost]

PLAY RECAP ****************************************************************
localhost                  : ok=2    changed=1    unreachable=0    failed=0
```


## <a name="next-steps"></a>Passaggi successivi
Questo esempio crea una macchina virtuale in un gruppo di risorse esistente e con una rete virtuale già distribuita. Per un esempio più dettagliato sulla toouse Ansible toocreate risorse di supporto, ad esempio una rete virtuale e le regole di gruppo di sicurezza di rete, vedere [creare un ambiente di VM completo con Ansible](ansible-create-complete-vm.md).
