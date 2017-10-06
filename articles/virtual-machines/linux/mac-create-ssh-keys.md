---
title: aaaCreate e utilizzare un SSH coppia di chiavi per le macchine virtuali Linux in Azure | Documenti Microsoft
description: Come toocreate e utilizzare una coppia chiave SSH pubblica e privata per le macchine virtuali Linux in Azure tooimprove hello sicurezza del processo di autenticazione hello.
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 34ae9482-da3e-4b2d-9d0d-9d672aa42498
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/14/2017
ms.author: iainfou
ms.openlocfilehash: 7fb94841d34d5bc006f3134adf91102ddce5f174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-use-an-ssh-public-and-private-key-pair-for-linux-vms-in-azure"></a>Come toocreate e utilizzo chiave SSH pubblica e privata coppia per le macchine virtuali Linux in Azure
Con una coppia di chiavi sicuro shell (SSH), è possibile creare macchine virtuali (VM) in Azure che usano le chiavi SSH per l'autenticazione, eliminando la necessità hello per le password toolog in. Questo articolo illustra come tooquickly generare e utilizzare una coppia di file di chiave pubblica e privata RSA di SSH protocol versione 2 per le macchine virtuali Linux. Per ulteriori passaggi ed esempi aggiuntivi, vedere [dettagliate coppie di chiavi SSH toocreate passaggi e i certificati](create-ssh-keys-detailed.md).

## <a name="create-an-ssh-key-pair"></a>Creare una coppia di chiavi SSH
Hello utilizzare `ssh-keygen` comando toocreate SSH pubblici e privati file di chiave per impostazione predefinita creata in hello `~/.ssh` directory, ma è possibile specificare un percorso diverso e aggiuntiva passphrase (una password tooaccess hello file di chiave privata) quando richiesto. Eseguire hello comando seguente da una shell Bash, rispondere alle richieste hello con informazioni personali.

```bash
ssh-keygen -t rsa -b 2048
```

## <a name="use-hello-ssh-key-pair"></a>Utilizzare una coppia di chiavi SSH hello
chiave pubblica Hello inseriti nella VM Linux in Azure è archiviato per impostazione predefinita `~/.ssh/id_rsa.pub`, a meno che non è stato modificato di percorso di hello durante la creazione. Se si utilizza hello [CLI di Azure 2.0](/cli/azure) toocreate la macchina virtuale, specificare il percorso di hello di questa chiave pubblica quando si utilizza hello [creare vm az](/cli/azure/vm#create) con hello `--ssh-key-path` opzione. Se si copia e Incolla il contenuto di hello di hello toouse di file di chiave pubblica nel portale di Azure hello o un modello di gestione risorse, assicurarsi di non copiare eventuali spazi vuoti aggiuntivi. Ad esempio, se si utilizza OS X, è possibile inviare tramite pipe il file di chiave pubblica di hello (per impostazione predefinita, **~/.ssh/id_rsa.pub**) troppo**pbcopy** contenuto hello toocopy (sono presenti altri programmi di Linux che hello stessa operazione, ad esempio `xclip`).

Se non si ha familiarità con le chiavi pubbliche SSH, è possibile visualizzare la chiave pubblica eseguendo `cat` come segue, sostituendo `~/.ssh/id_rsa.pub` con il proprio percorso file della chiave pubblica:

```bash
cat ~/.ssh/id_rsa.pub
```

Con chiave pubblica di hello nella macchina virtuale di Azure, SSH tooyour VM utilizzando hello indirizzo IP o nome DNS della macchina virtuale (ricordare tooreplace `azureuser` e `myvm.westus.cloudapp.azure.com` seguito con nome utente amministratore hello e nome di dominio completo hello - o IP indirizzo):

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

Se si fornisce una passphrase al momento della creazione la coppia di chiavi, immettere passphrase hello quando richiesto durante il processo di accesso di hello. (server hello viene aggiunto tooyour `~/.ssh/known_hosts` cartella e non verranno più richieste tooconnect finché la chiave pubblica di hello nelle modifiche apportate alla macchina virtuale di Azure o il nome di server hello viene rimosso da `~/.ssh/known_hosts`.)

## <a name="next-steps"></a>Passaggi successivi

Macchine virtuali create utilizzando le chiavi SSH per impostazione predefinita configurata con le password disabilitate, toomake colpita indovinare tenta pertanto difficile e molto più costoso. Questo argomento descrive la creazione di una coppia di chiavi SSH semplice per un utilizzo rapido. Se si necessita di ulteriore assistenza per la creazione di coppia di chiavi SSH o richiedono certificati aggiuntivi, vedere [dettagliate coppie di chiavi SSH toocreate passaggi e i certificati](create-ssh-keys-detailed.md).

È possibile creare macchine virtuali che utilizzano la coppia di chiavi SSH utilizzando hello portale di Azure CLI e modelli:

* [Creare una VM Linux protette utilizzando hello portale di Azure](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Creare una VM Linux protette mediante Azure CLI 2.0 hello)](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Creare una VM Linux protetta usando un modello di Azure](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
