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
# <a name="how-toocreate-and-use-an-ssh-public-and-private-key-pair-for-linux-vms-in-azure"></a><span data-ttu-id="bfca6-103">Come toocreate e utilizzo chiave SSH pubblica e privata coppia per le macchine virtuali Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="bfca6-103">How toocreate and use an SSH public and private key pair for Linux VMs in Azure</span></span>
<span data-ttu-id="bfca6-104">Con una coppia di chiavi sicuro shell (SSH), è possibile creare macchine virtuali (VM) in Azure che usano le chiavi SSH per l'autenticazione, eliminando la necessità hello per le password toolog in.</span><span class="sxs-lookup"><span data-stu-id="bfca6-104">With a secure shell (SSH) key pair, you can create virtual machines (VMs) in Azure that use SSH keys for authentication, eliminating hello need for passwords toolog in.</span></span> <span data-ttu-id="bfca6-105">Questo articolo illustra come tooquickly generare e utilizzare una coppia di file di chiave pubblica e privata RSA di SSH protocol versione 2 per le macchine virtuali Linux.</span><span class="sxs-lookup"><span data-stu-id="bfca6-105">This article shows you how tooquickly generate and use an SSH protocol version 2 RSA public and private key file pair for Linux VMs.</span></span> <span data-ttu-id="bfca6-106">Per ulteriori passaggi ed esempi aggiuntivi, vedere [dettagliate coppie di chiavi SSH toocreate passaggi e i certificati](create-ssh-keys-detailed.md).</span><span class="sxs-lookup"><span data-stu-id="bfca6-106">For more detailed steps and additional examples, see [detailed steps toocreate SSH key pairs and certificates](create-ssh-keys-detailed.md).</span></span>

## <a name="create-an-ssh-key-pair"></a><span data-ttu-id="bfca6-107">Creare una coppia di chiavi SSH</span><span class="sxs-lookup"><span data-stu-id="bfca6-107">Create an SSH key pair</span></span>
<span data-ttu-id="bfca6-108">Hello utilizzare `ssh-keygen` comando toocreate SSH pubblici e privati file di chiave per impostazione predefinita creata in hello `~/.ssh` directory, ma è possibile specificare un percorso diverso e aggiuntiva passphrase (una password tooaccess hello file di chiave privata) quando richiesto.</span><span class="sxs-lookup"><span data-stu-id="bfca6-108">Use hello `ssh-keygen` command toocreate SSH public and private key files that are by default created in hello `~/.ssh` directory, but you can specify a different location and additional passphrase (a password tooaccess hello private key file) when prompted.</span></span> <span data-ttu-id="bfca6-109">Eseguire hello comando seguente da una shell Bash, rispondere alle richieste hello con informazioni personali.</span><span class="sxs-lookup"><span data-stu-id="bfca6-109">Run hello following command from a Bash shell, answering hello prompts with your own information.</span></span>

```bash
ssh-keygen -t rsa -b 2048
```

## <a name="use-hello-ssh-key-pair"></a><span data-ttu-id="bfca6-110">Utilizzare una coppia di chiavi SSH hello</span><span class="sxs-lookup"><span data-stu-id="bfca6-110">Use hello SSH key pair</span></span>
<span data-ttu-id="bfca6-111">chiave pubblica Hello inseriti nella VM Linux in Azure è archiviato per impostazione predefinita `~/.ssh/id_rsa.pub`, a meno che non è stato modificato di percorso di hello durante la creazione.</span><span class="sxs-lookup"><span data-stu-id="bfca6-111">hello public key that you place on your Linux VM in Azure is by default stored in `~/.ssh/id_rsa.pub`, unless you changed hello location when you created them.</span></span> <span data-ttu-id="bfca6-112">Se si utilizza hello [CLI di Azure 2.0](/cli/azure) toocreate la macchina virtuale, specificare il percorso di hello di questa chiave pubblica quando si utilizza hello [creare vm az](/cli/azure/vm#create) con hello `--ssh-key-path` opzione.</span><span class="sxs-lookup"><span data-stu-id="bfca6-112">If you use hello [Azure CLI 2.0](/cli/azure) toocreate your VM, specify hello location of this public key when you use hello [az vm create](/cli/azure/vm#create) with hello `--ssh-key-path` option.</span></span> <span data-ttu-id="bfca6-113">Se si copia e Incolla il contenuto di hello di hello toouse di file di chiave pubblica nel portale di Azure hello o un modello di gestione risorse, assicurarsi di non copiare eventuali spazi vuoti aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="bfca6-113">If you copy and paste hello contents of hello public key file toouse in hello Azure portal or a Resource Manager template, make sure you don't copy any additional whitespace.</span></span> <span data-ttu-id="bfca6-114">Ad esempio, se si utilizza OS X, è possibile inviare tramite pipe il file di chiave pubblica di hello (per impostazione predefinita, **~/.ssh/id_rsa.pub**) troppo**pbcopy** contenuto hello toocopy (sono presenti altri programmi di Linux che hello stessa operazione, ad esempio `xclip`).</span><span class="sxs-lookup"><span data-stu-id="bfca6-114">For example, if you use OS X, you can pipe hello public key file (by default, **~/.ssh/id_rsa.pub**) too**pbcopy** toocopy hello contents (there are other Linux programs that do hello same thing, such as `xclip`).</span></span>

<span data-ttu-id="bfca6-115">Se non si ha familiarità con le chiavi pubbliche SSH, è possibile visualizzare la chiave pubblica eseguendo `cat` come segue, sostituendo `~/.ssh/id_rsa.pub` con il proprio percorso file della chiave pubblica:</span><span class="sxs-lookup"><span data-stu-id="bfca6-115">If you're not familiar with SSH public keys, you can see your public key by running `cat` as follows, replacing `~/.ssh/id_rsa.pub` with your own public key file location:</span></span>

```bash
cat ~/.ssh/id_rsa.pub
```

<span data-ttu-id="bfca6-116">Con chiave pubblica di hello nella macchina virtuale di Azure, SSH tooyour VM utilizzando hello indirizzo IP o nome DNS della macchina virtuale (ricordare tooreplace `azureuser` e `myvm.westus.cloudapp.azure.com` seguito con nome utente amministratore hello e nome di dominio completo hello - o IP indirizzo):</span><span class="sxs-lookup"><span data-stu-id="bfca6-116">With hello public key on your Azure VM, SSH tooyour VM using hello IP address or DNS name of your VM (remember tooreplace `azureuser` and `myvm.westus.cloudapp.azure.com` below with hello admin username and hello fully qualified domain name -- or IP address):</span></span>

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

<span data-ttu-id="bfca6-117">Se si fornisce una passphrase al momento della creazione la coppia di chiavi, immettere passphrase hello quando richiesto durante il processo di accesso di hello.</span><span class="sxs-lookup"><span data-stu-id="bfca6-117">If you provided a passphrase when you created your key pair, enter hello passphrase when prompted during hello login process.</span></span> <span data-ttu-id="bfca6-118">(server hello viene aggiunto tooyour `~/.ssh/known_hosts` cartella e non verranno più richieste tooconnect finché la chiave pubblica di hello nelle modifiche apportate alla macchina virtuale di Azure o il nome di server hello viene rimosso da `~/.ssh/known_hosts`.)</span><span class="sxs-lookup"><span data-stu-id="bfca6-118">(hello server is added tooyour `~/.ssh/known_hosts` folder, and you won't be asked tooconnect again until hello public key on your Azure VM changes or hello server name is removed from `~/.ssh/known_hosts`.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="bfca6-119">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bfca6-119">Next steps</span></span>

<span data-ttu-id="bfca6-120">Macchine virtuali create utilizzando le chiavi SSH per impostazione predefinita configurata con le password disabilitate, toomake colpita indovinare tenta pertanto difficile e molto più costoso.</span><span class="sxs-lookup"><span data-stu-id="bfca6-120">VMs created using SSH keys are by default configured with passwords disabled, toomake brute-forced guessing attempts vastly more expensive and therefore difficult.</span></span> <span data-ttu-id="bfca6-121">Questo argomento descrive la creazione di una coppia di chiavi SSH semplice per un utilizzo rapido.</span><span class="sxs-lookup"><span data-stu-id="bfca6-121">This topic describes creating a simple SSH key pair for quick usage.</span></span> <span data-ttu-id="bfca6-122">Se si necessita di ulteriore assistenza per la creazione di coppia di chiavi SSH o richiedono certificati aggiuntivi, vedere [dettagliate coppie di chiavi SSH toocreate passaggi e i certificati](create-ssh-keys-detailed.md).</span><span class="sxs-lookup"><span data-stu-id="bfca6-122">If you need more assistance in creating your SSH key pair or require additional certificates, see [Detailed steps toocreate SSH key pairs and certificates](create-ssh-keys-detailed.md).</span></span>

<span data-ttu-id="bfca6-123">È possibile creare macchine virtuali che utilizzano la coppia di chiavi SSH utilizzando hello portale di Azure CLI e modelli:</span><span class="sxs-lookup"><span data-stu-id="bfca6-123">You can create VMs that use your SSH key pair using hello Azure portal, CLI, and templates:</span></span>

* [<span data-ttu-id="bfca6-124">Creare una VM Linux protette utilizzando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="bfca6-124">Create a secure Linux VM using hello Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="bfca6-125">Creare una VM Linux protette mediante Azure CLI 2.0 hello)</span><span class="sxs-lookup"><span data-stu-id="bfca6-125">Create a secure Linux VM using hello Azure CLI 2.0)</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="bfca6-126">Creare una VM Linux protetta usando un modello di Azure</span><span class="sxs-lookup"><span data-stu-id="bfca6-126">Create a secure Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
