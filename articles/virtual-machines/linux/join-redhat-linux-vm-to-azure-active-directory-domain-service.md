---
title: aaaJoin tooan una VM Linux RedHat Azure Active Directory DS | Documenti Microsoft
description: Come toojoin un tooan Red Hat Enterprise Linux 7 VM esistente, il servizio di dominio Azure Active Directory.
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/14/2016
ms.author: v-livech
ms.openlocfilehash: f3ba3c764e253191753f1cc5fc8c3b85c53818af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-redhat-linux-vm-tooan-azure-active-directory-domain-service"></a><span data-ttu-id="8f0e1-103">Creare un join tooan una VM Linux RedHat servizi di dominio di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8f0e1-103">Join a RedHat Linux VM tooan Azure Active Directory Domain Service</span></span>

<span data-ttu-id="8f0e1-104">Questo articolo illustra la modalità di gestione dominio toojoin un tooan di macchina virtuale Red Hat Enterprise Linux (RHEL) 7 Azure Active Directory Domain Services (AADDS).</span><span class="sxs-lookup"><span data-stu-id="8f0e1-104">This article shows you how toojoin a Red Hat Enterprise Linux (RHEL) 7 virtual machine tooan Azure Active Directory Domain Services (AADDS) managed domain.</span></span>  <span data-ttu-id="8f0e1-105">requisiti di Hello sono:</span><span class="sxs-lookup"><span data-stu-id="8f0e1-105">hello requirements are:</span></span>

- [<span data-ttu-id="8f0e1-106">Un account di Azure</span><span class="sxs-lookup"><span data-stu-id="8f0e1-106">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)

- [<span data-ttu-id="8f0e1-107">File di chiavi SSH pubbliche e private</span><span class="sxs-lookup"><span data-stu-id="8f0e1-107">SSH public and private key files</span></span>](mac-create-ssh-keys.md)

- [<span data-ttu-id="8f0e1-108">Controller di dominio del servizio di dominio Active Directory di Azure</span><span class="sxs-lookup"><span data-stu-id="8f0e1-108">an Azure Active Directory Domain Services DC</span></span>](../../active-directory-domain-services/active-directory-ds-getting-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quick-commands"></a><span data-ttu-id="8f0e1-109">Comandi rapidi</span><span class="sxs-lookup"><span data-stu-id="8f0e1-109">Quick Commands</span></span>

<span data-ttu-id="8f0e1-110">_Sostituire gli esempi con le impostazioni desiderate._</span><span class="sxs-lookup"><span data-stu-id="8f0e1-110">_Replace any examples with your own settings._</span></span>

### <a name="switch-hello-azure-cli-tooclassic-deployment-mode"></a><span data-ttu-id="8f0e1-111">Modalità di distribuzione tooclassic commutatore hello cli di azure</span><span class="sxs-lookup"><span data-stu-id="8f0e1-111">Switch hello azure-cli tooclassic deployment mode</span></span>

```azurecli
azure config mode asm
```

### <a name="search-for-a-rhel-version-and-image"></a><span data-ttu-id="8f0e1-112">Cercare una versione e un'immagine di RHEL</span><span class="sxs-lookup"><span data-stu-id="8f0e1-112">Search for a RHEL version and image</span></span>

```azurecli
azure vm image list | grep "Red Hat"
```

### <a name="create-a-redhat-linux-vm"></a><span data-ttu-id="8f0e1-113">Creare una macchina virtuale Redhat Linux</span><span class="sxs-lookup"><span data-stu-id="8f0e1-113">Create a Redhat Linux VM</span></span>

```azurecli
azure vm create myVM \
-o a879bbefc56a43abb0ce65052aac09f3__RHEL_7_2_Standard_Azure_RHUI-20161026220742 \
-g ahmet \
-p myPassword \
-e 22 \
-t "~/.ssh/id_rsa.pub" \
-z "Small" \
-l "West US"
```

### <a name="ssh-toohello-vm"></a><span data-ttu-id="8f0e1-114">SSH toohello VM</span><span class="sxs-lookup"><span data-stu-id="8f0e1-114">SSH toohello VM</span></span>

```bash
ssh -i ~/.ssh/id_rsa ahmet@myVM
```

### <a name="update-yum-packages"></a><span data-ttu-id="8f0e1-115">Aggiornare i pacchetti YUM</span><span class="sxs-lookup"><span data-stu-id="8f0e1-115">Update YUM packages</span></span>

```bash
sudo yum update
```

### <a name="install-packages-needed"></a><span data-ttu-id="8f0e1-116">Installare i pacchetti necessari</span><span class="sxs-lookup"><span data-stu-id="8f0e1-116">Install packages needed</span></span>

```bash
sudo yum -y install realmd sssd krb5-workstation krb5-libs
```

<span data-ttu-id="8f0e1-117">Ora che i pacchetti hello necessario sono installati sulla macchina virtuale di Linux hello, hello è dominio gestito toohello toojoin hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="8f0e1-117">Now that hello required packages are installed on hello Linux virtual machine, hello next task is toojoin hello virtual machine toohello managed domain.</span></span>

### <a name="discover-hello-aad-domain-services-managed-domain"></a><span data-ttu-id="8f0e1-118">Individuare hello dominio gestito di servizi di dominio di Azure ad</span><span class="sxs-lookup"><span data-stu-id="8f0e1-118">Discover hello AAD Domain Services managed domain</span></span>

```bash
sudo realm discover mydomain.com
```

### <a name="initialize-kerberos"></a><span data-ttu-id="8f0e1-119">Inizializzare kerberos</span><span class="sxs-lookup"><span data-stu-id="8f0e1-119">Initialize kerberos</span></span>

<span data-ttu-id="8f0e1-120">Assicurarsi di specificare un utente appartenente al gruppo toohello 'AAD Administrators controller di dominio'.</span><span class="sxs-lookup"><span data-stu-id="8f0e1-120">Ensure that you specify a user who belongs toohello 'AAD DC Administrators' group.</span></span> <span data-ttu-id="8f0e1-121">Solo questi utenti è possono aggiungere domini gestiti toohello di computer.</span><span class="sxs-lookup"><span data-stu-id="8f0e1-121">Only these users can join computers toohello managed domain.</span></span>

```bash
kinit ahmet@mydomain.com
```

### <a name="join-hello-machine-toohello-domain"></a><span data-ttu-id="8f0e1-122">Dominio hello macchina toohello</span><span class="sxs-lookup"><span data-stu-id="8f0e1-122">Join hello machine toohello domain</span></span>

```bash
sudo realm join --verbose mydomain.com -U 'ahmet@mydomain.com'
```

### <a name="verify-hello-machine-is-joined-toohello-domain"></a><span data-ttu-id="8f0e1-123">Verificare macchina hello toohello aggiunti a un dominio</span><span class="sxs-lookup"><span data-stu-id="8f0e1-123">Verify hello machine is joined toohello domain</span></span>

```bash
ssh -l ahmet@mydomain.com mydomain.cloudapp.net
```

## <a name="next-steps"></a><span data-ttu-id="8f0e1-124">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8f0e1-124">Next Steps</span></span>

* [<span data-ttu-id="8f0e1-125">Red Hat Update Infrastructure (RHUI) per macchine virtuali Red Hat Enterprise Linux su richiesta in Azure</span><span class="sxs-lookup"><span data-stu-id="8f0e1-125">Red Hat Update Infrastructure (RHUI) for on-demand Red Hat Enterprise Linux VMs in Azure</span></span>](update-infrastructure-redhat.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="8f0e1-126">Configurare l'insieme di credenziali delle chiavi per le macchine virtuali in Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8f0e1-126">Set up Key Vault for virtual machines in Azure Resource Manager</span></span>](key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="8f0e1-127">Distribuire e gestire macchine virtuali utilizzando modelli di gestione risorse di Azure e hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="8f0e1-127">Deploy and manage virtual machines by using Azure Resource Manager templates and hello Azure CLI</span></span>](../linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
