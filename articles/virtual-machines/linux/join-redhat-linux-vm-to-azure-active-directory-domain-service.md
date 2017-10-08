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
# <a name="join-a-redhat-linux-vm-tooan-azure-active-directory-domain-service"></a>Creare un join tooan una VM Linux RedHat servizi di dominio di Azure Active Directory

Questo articolo illustra la modalità di gestione dominio toojoin un tooan di macchina virtuale Red Hat Enterprise Linux (RHEL) 7 Azure Active Directory Domain Services (AADDS).  requisiti di Hello sono:

- [Un account di Azure](https://azure.microsoft.com/pricing/free-trial/)

- [File di chiavi SSH pubbliche e private](mac-create-ssh-keys.md)

- [Controller di dominio del servizio di dominio Active Directory di Azure](../../active-directory-domain-services/active-directory-ds-getting-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quick-commands"></a>Comandi rapidi

_Sostituire gli esempi con le impostazioni desiderate._

### <a name="switch-hello-azure-cli-tooclassic-deployment-mode"></a>Modalità di distribuzione tooclassic commutatore hello cli di azure

```azurecli
azure config mode asm
```

### <a name="search-for-a-rhel-version-and-image"></a>Cercare una versione e un'immagine di RHEL

```azurecli
azure vm image list | grep "Red Hat"
```

### <a name="create-a-redhat-linux-vm"></a>Creare una macchina virtuale Redhat Linux

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

### <a name="ssh-toohello-vm"></a>SSH toohello VM

```bash
ssh -i ~/.ssh/id_rsa ahmet@myVM
```

### <a name="update-yum-packages"></a>Aggiornare i pacchetti YUM

```bash
sudo yum update
```

### <a name="install-packages-needed"></a>Installare i pacchetti necessari

```bash
sudo yum -y install realmd sssd krb5-workstation krb5-libs
```

Ora che i pacchetti hello necessario sono installati sulla macchina virtuale di Linux hello, hello è dominio gestito toohello toojoin hello macchina virtuale.

### <a name="discover-hello-aad-domain-services-managed-domain"></a>Individuare hello dominio gestito di servizi di dominio di Azure ad

```bash
sudo realm discover mydomain.com
```

### <a name="initialize-kerberos"></a>Inizializzare kerberos

Assicurarsi di specificare un utente appartenente al gruppo toohello 'AAD Administrators controller di dominio'. Solo questi utenti è possono aggiungere domini gestiti toohello di computer.

```bash
kinit ahmet@mydomain.com
```

### <a name="join-hello-machine-toohello-domain"></a>Dominio hello macchina toohello

```bash
sudo realm join --verbose mydomain.com -U 'ahmet@mydomain.com'
```

### <a name="verify-hello-machine-is-joined-toohello-domain"></a>Verificare macchina hello toohello aggiunti a un dominio

```bash
ssh -l ahmet@mydomain.com mydomain.cloudapp.net
```

## <a name="next-steps"></a>Passaggi successivi

* [Red Hat Update Infrastructure (RHUI) per macchine virtuali Red Hat Enterprise Linux su richiesta in Azure](update-infrastructure-redhat.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Configurare l'insieme di credenziali delle chiavi per le macchine virtuali in Azure Resource Manager](key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Distribuire e gestire macchine virtuali utilizzando modelli di gestione risorse di Azure e hello CLI di Azure](../linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
