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
# <a name="install-and-configure-ansible-toomanage-virtual-machines-in-azure"></a>Installare e configurare le macchine virtuali toomanage Ansible in Azure
In questo articolo illustra in dettaglio come tooinstall Ansible e i moduli di Azure SDK Python necessari per alcune delle hello le distribuzioni di Linux più comuni. È possibile installare Ansible in altre distribuzioni regolando toofit pacchetti hello installato la piattaforma specifica. toocreate Azure le risorse in modo sicuro, verrà inoltre descritto come toocreate e definire le credenziali per Ansible toouse. 

Per altre opzioni di installazione e i passaggi per altre piattaforme, vedere hello [Ansible Guida all'installazione](https://docs.ansible.com/ansible/intro_installation.html).


## <a name="install-ansible"></a>Installare Ansible
Creare prima un gruppo di risorse con [az group create](/cli/azure/group#create). esempio Hello crea un gruppo di risorse denominato *myResourceGroupAnsible* in hello *eastus* percorso:

```azurecli
az group create --name myResourceGroupAnsible --location eastus
```

Ora di creare una macchina virtuale e installare Ansible per uno dei seguenti distribuzioni hello:

- [Ubuntu 16.04 LTS](#ubuntu1604-lts)
- [CentOS 7.3](#centos-73)
- [SLES 12.2 SP2](#sles-122-sp2)

### <a name="ubuntu-1604-lts"></a>Ubuntu 16.04 LTS
Creare una VM con il comando [az vm create](/cli/azure/vm#create). esempio Hello crea una macchina virtuale denominata *myVMAnsible*:

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

SSH tramite VM tooyour hello `publicIpAddress` indicato nel hello operazione di creazione dell'output di hello VM:

```bash
ssh azureuser@<publicIpAddress>
```

Nella macchina virtuale, installare i pacchetti hello necessario per i moduli di Azure SDK Python hello e Ansible come indicato di seguito:

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

Procedere con troppo[le credenziali di Azure creare](#create-azure-credentials).


### <a name="centos-73"></a>CentOS 7.3
Creare una VM con il comando [az vm create](/cli/azure/vm#create). esempio Hello crea una macchina virtuale denominata *myVMAnsible*:

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image CentOS \
    --admin-username azureuser \
    --generate-ssh-keys
```

SSH tramite VM tooyour hello `publicIpAddress` indicato nel hello operazione di creazione dell'output di hello VM:

```bash
ssh azureuser@<publicIpAddress>
```

Nella macchina virtuale, installare i pacchetti hello necessario per i moduli di Azure SDK Python hello e Ansible come indicato di seguito:

```bash
## Install pre-requisite packages
sudo yum check-update; sudo yum install -y gcc libffi-devel python-devel openssl-devel epel-release
sudo yum install -y python-pip python-wheel

## Install Azure SDKs via pip
sudo pip install "azure==2.0.0rc5" msrestazure

## Install Ansible via yum
sudo yum install -y ansible
```

Procedere con troppo[le credenziali di Azure creare](#create-azure-credentials).


### <a name="sles-122-sp2"></a>SLES 12.2 SP2
Creare una VM con il comando [az vm create](/cli/azure/vm#create). esempio Hello crea una macchina virtuale denominata *myVMAnsible*:

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image SLES \
    --admin-username azureuser \
    --generate-ssh-keys
```

SSH tramite VM tooyour hello `publicIpAddress` indicato nel hello operazione di creazione dell'output di hello VM:

```bash
ssh azureuser@<publicIpAddress>
```

Nella macchina virtuale, installare i pacchetti hello necessario per i moduli di Azure SDK Python hello e Ansible come indicato di seguito:

```bash
## Install pre-requisite packages
sudo zypper refresh && sudo zypper --non-interactive install gcc libffi-devel-gcc5 python-devel \
    libopenssl-devel python-pip python-setuptools python-azure-sdk

## Install Ansible via zypper
sudo zypper addrepo http://download.opensuse.org/repositories/systemsmanagement/SLE_12_SP2/systemsmanagement.repo
sudo zypper refresh && sudo zypper install ansible
```

Procedere con troppo[le credenziali di Azure creare](#create-azure-credentials).


## <a name="create-azure-credentials"></a>Creare credenziali di Azure
Ansible comunica con Azure usando un nome utente e password o un'entità servizio. Un'entità servizio di Azure è un'identità di sicurezza che è possibile usare con le app, con i servizi e con strumenti di automazione come Ansible. È controllare e definire le autorizzazioni di hello come entità di servizio toowhat operazioni hello è possibile eseguire in Azure. sicurezza tooimprove su per fornire un nome utente e una password, questo esempio crea un servizio di base dell'entità.

Creare un servizio principale con [az ad sp creare-per-rbac](/cli/azure/ad/sp#create-for-rbac) e le credenziali di hello output Ansible deve:

```azurecli
az ad sp create-for-rbac --query [appId,password,tenant]
```

Un esempio di output di hello da hello precedenti comandi è la seguente:

```json
[
  "eec5624a-90f8-4386-8a87-02730b5410d5",
  "531dcffa-3aff-4488-99bb-4816c395ea3f",
  "72f988bf-86f1-41af-91ab-2d7cd011db47"
]
```

tooAzure tooauthenticate, è necessario anche con l'ID sottoscrizione Azure tooobtain [mostra account az](/cli/azure/account#show):

```azurecli
az account show --query [id] --output tsv
```

Utilizzare l'output di hello di questi due comandi nel passaggio successivo hello.


## <a name="create-ansible-credentials-file"></a>Creare un file di credenziali di Ansible
tooprovide credenziali tooAnsible, definire le variabili di ambiente o creare un file di credenziali locali. Per ulteriori informazioni su come toodefine Ansible credenziali, vedere [tooAzure fornendo credenziali moduli](https://docs.ansible.com/ansible/guide_azure.html#providing-credentials-to-azure-modules). 

Per un ambiente di sviluppo, creare un file di *credenziali* per Ansible sulla macchina virtuale host come segue:

```bash
mkdir ~/.azure
vi ~/.azure/credentials
```

Hello *credenziali* file combina l'ID sottoscrizione hello con l'output di hello di creazione di un'entità servizio. L'output di hello precedente [az ad sp creare-per-rbac](/cli/azure/ad/sp#create-for-rbac) comando è hello stesso ordine in base alle esigenze per *client_id*, *secret*, e *tenant* . Hello seguente esempio *credenziali* file Mostra questi valori di output di hello precedente corrispondente. Immettere valori personalizzati come di seguito:

```bash
[default]
subscription_id=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
client_id=66cf7166-dd13-40f9-bca2-3e9a43f2b3a4
secret=b8326643-f7e9-48fb-b0d5-952b68ab3def
tenant=72f988bf-86f1-41af-91ab-2d7cd011db47
```


## <a name="use-ansible-environment-variables"></a>Usare le variabili di ambiente di Ansible
Se si intende toouse strumenti, ad esempio Ansible Tower o Jenkins, è possibile definire variabili di ambiente come indicato di seguito. Queste variabili combinano l'ID sottoscrizione hello output di hello di creazione di un servizio principale. L'output di hello precedente [az ad sp creare-per-rbac](/cli/azure/ad/sp#create-for-rbac) comando è hello stesso ordine in base alle esigenze per *AZURE_CLIENT_ID*, *AZURE_SECRET*, e *AZURE_ TENANT*. 

```bash
export AZURE_SUBSCRIPTION_ID=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
export AZURE_CLIENT_ID=66cf7166-dd13-40f9-bca2-3e9a43f2b3a4
export AZURE_SECRET=8326643-f7e9-48fb-b0d5-952b68ab3def
export AZURE_TENANT=72f988bf-86f1-41af-91ab-2d7cd011db47
```

## <a name="next-steps"></a>Passaggi successivi
È ora Ansible e hello obbligatorio i moduli Python di Azure SDK installati e le credenziali definite per Ansible toouse. Informazioni su come troppo[creare una macchina virtuale con Ansible](ansible-create-vm.md). Viene inoltre illustrato come troppo[creare una macchina virtuale di Azure completo e il supporto di risorse con Ansible](ansible-create-complete-vm.md).
