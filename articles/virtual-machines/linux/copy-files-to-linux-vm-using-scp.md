---
title: aaaMove file tooand da macchine virtuali Linux di Azure con SCP | Documenti Microsoft
description: Spostare in modo sicuro i file tooand da una VM Linux di Azure tramite SCP e una coppia di chiavi SSH.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: danlep
ms.openlocfilehash: 9e4dce667aa581df74aec3d45a6ba5e52f777d1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-files-tooand-from-a-linux-vm-using-scp"></a><span data-ttu-id="467aa-103">Spostare i file tooand da una VM Linux tramite SCP</span><span class="sxs-lookup"><span data-stu-id="467aa-103">Move files tooand from a Linux VM using SCP</span></span>

<span data-ttu-id="467aa-104">Questo articolo illustra come toomove file dalla propria workstation backup tooan VM Linux di Azure o da una VM Linux di Azure verso il basso tooyour workstation, utilizzando Secure copia (SCP).</span><span class="sxs-lookup"><span data-stu-id="467aa-104">This article shows how toomove files from your workstation up tooan Azure Linux VM, or from an Azure Linux VM down tooyour workstation, using Secure Copy (SCP).</span></span> <span data-ttu-id="467aa-105">Il trasferimento di file tra una workstation e una macchina virtuale Linux in modo rapido e sicuro è un aspetto essenziale della gestione dell'infrastruttura di Azure.</span><span class="sxs-lookup"><span data-stu-id="467aa-105">Moving files between your workstation and a Linux VM, quickly and securely, is critical for managing your Azure infrastructure.</span></span> 

<span data-ttu-id="467aa-106">Per questo articolo è necessaria una macchina virtuale Linux distribuita in Azure tramite [file di chiavi SSH pubbliche e private](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="467aa-106">For this article, you need a Linux VM deployed in Azure using [SSH public and private key files](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="467aa-107">È necessario anche un client SCP per il computer locale:</span><span class="sxs-lookup"><span data-stu-id="467aa-107">You also need an SCP client for your local computer.</span></span> <span data-ttu-id="467aa-108">È basato su SSH e della shell Bash predefinita di hello della maggior parte dei computer Mac e Linux e alcuni shell di Windows.</span><span class="sxs-lookup"><span data-stu-id="467aa-108">It is built on top of SSH and included in hello default Bash shell of most Linux and Mac computers and some Windows shells.</span></span>

## <a name="quick-commands"></a><span data-ttu-id="467aa-109">Comandi rapidi</span><span class="sxs-lookup"><span data-stu-id="467aa-109">Quick commands</span></span>

<span data-ttu-id="467aa-110">Copiare un file di backup toohello VM Linux</span><span class="sxs-lookup"><span data-stu-id="467aa-110">Copy a file up toohello Linux VM</span></span>

```bash
scp file azureuser@azurehost:directory/targetfile
```

<span data-ttu-id="467aa-111">Copia un file verso il basso da hello VM Linux</span><span class="sxs-lookup"><span data-stu-id="467aa-111">Copy a file down from hello Linux VM</span></span>

```bash
scp azureuser@azurehost:directory/file targetfile
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="467aa-112">Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="467aa-112">Detailed walkthrough</span></span>

<span data-ttu-id="467aa-113">Ad esempio spostare un file di configurazione di Azure backup tooa VM Linux e acquisisce una directory di file di log, sia utilizzando chiavi SCP e SSH.</span><span class="sxs-lookup"><span data-stu-id="467aa-113">As examples, we move an Azure configuration file up tooa Linux VM and pull down a log file directory, both using SCP and SSH keys.</span></span>   

## <a name="ssh-key-pair-authentication"></a><span data-ttu-id="467aa-114">Autenticazione della coppia di chiavi SSH</span><span class="sxs-lookup"><span data-stu-id="467aa-114">SSH key pair authentication</span></span>

<span data-ttu-id="467aa-115">SCP utilizza SSH per il livello di trasporto hello.</span><span class="sxs-lookup"><span data-stu-id="467aa-115">SCP uses SSH for hello transport layer.</span></span> <span data-ttu-id="467aa-116">Handle SSH hello autenticazione sull'host di destinazione hello e sposta il file hello in un tunnel crittografato fornito per impostazione predefinita con SSH.</span><span class="sxs-lookup"><span data-stu-id="467aa-116">SSH handles hello authentication on hello destination host, and it moves hello file in an encrypted tunnel provided by default with SSH.</span></span> <span data-ttu-id="467aa-117">Per l'autenticazione SSH è possibile usare nomi utente e password.</span><span class="sxs-lookup"><span data-stu-id="467aa-117">For SSH authentication, usernames and passwords can be used.</span></span> <span data-ttu-id="467aa-118">Per una maggiore sicurezza, tuttavia, è consigliabile eseguire l'autenticazione tramite file di chiavi SSH pubbliche e private.</span><span class="sxs-lookup"><span data-stu-id="467aa-118">However, SSH public and private key authentication are recommended as a security best practice.</span></span> <span data-ttu-id="467aa-119">Una volta SSH è autenticato connessione hello, SCP, viene avviata la copia di file hello.</span><span class="sxs-lookup"><span data-stu-id="467aa-119">Once SSH has authenticated hello connection, SCP then begins copying hello file.</span></span> <span data-ttu-id="467aa-120">Utilizzando un correttamente configurato `~/.ssh/config` e SSH chiavi pubbliche e private, connessione hello SCP possono essere stabilite utilizzando solo un nome server (o indirizzo IP).</span><span class="sxs-lookup"><span data-stu-id="467aa-120">Using a properly configured `~/.ssh/config` and SSH public and private keys, hello SCP connection can be established by just using a server name (or IP address).</span></span> <span data-ttu-id="467aa-121">Se si dispone solo di una chiave SSH, SCP Cerca in hello `~/.ssh/` directory che viene utilizzato da toolog predefinito in toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="467aa-121">If you only have one SSH key, SCP looks for it in hello `~/.ssh/` directory, and uses it by default toolog in toohello VM.</span></span>

<span data-ttu-id="467aa-122">Per altre informazioni sulla configurazione del file `~/.ssh/config` e delle chiavi SSH pubbliche e private, vedere [Creare chiavi SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="467aa-122">For more information on configuring your `~/.ssh/config` and SSH public and private keys, see [Create SSH keys](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="scp-a-file-tooa-linux-vm"></a><span data-ttu-id="467aa-123">SCP tooa un file VM Linux</span><span class="sxs-lookup"><span data-stu-id="467aa-123">SCP a file tooa Linux VM</span></span>

<span data-ttu-id="467aa-124">Ad esempio primo hello copiamo un file di configurazione di Azure backup tooa VM Linux automazione toodeploy utilizzato.</span><span class="sxs-lookup"><span data-stu-id="467aa-124">For hello first example, we copy an Azure configuration file up tooa Linux VM that is used toodeploy automation.</span></span> <span data-ttu-id="467aa-125">Poiché questo file contiene credenziali di API di Azure, che includono informazioni riservate, la sicurezza è particolarmente importante</span><span class="sxs-lookup"><span data-stu-id="467aa-125">Because this file contains Azure API credentials, which include secrets, security is important.</span></span> <span data-ttu-id="467aa-126">tunnel di crittografato Hello fornito da SSH protegge il contenuto di hello del file hello.</span><span class="sxs-lookup"><span data-stu-id="467aa-126">hello encrypted tunnel provided by SSH protects hello contents of hello file.</span></span>

<span data-ttu-id="467aa-127">Hello seguenti comando copie hello locale *.azure/config* tooan macchina virtuale di Azure con nome di dominio completo del file *myserver.eastus.cloudapp.azure.com*. nome utente amministratore di hello nella macchina virtuale di Azure hello è *azureuser* .</span><span class="sxs-lookup"><span data-stu-id="467aa-127">hello following command copies hello local *.azure/config* file tooan Azure VM with FQDN *myserver.eastus.cloudapp.azure.com*. hello admin user name on hello Azure VM is *azureuser*.</span></span> <span data-ttu-id="467aa-128">file Hello è toohello destinazione */home/azureuser/* directory.</span><span class="sxs-lookup"><span data-stu-id="467aa-128">hello file is targeted toohello */home/azureuser/* directory.</span></span> <span data-ttu-id="467aa-129">Nel comando sostituire i valori predefiniti con quelli personali.</span><span class="sxs-lookup"><span data-stu-id="467aa-129">Substitute your own values in this command.</span></span>

```bash
scp ~/.azure/config azureuser@myserver.eastus.cloudapp.com:/home/azureuser/config
```

## <a name="scp-a-directory-from-a-linux-vm"></a><span data-ttu-id="467aa-130">Copia sicura di una directory da una macchina virtuale Linux</span><span class="sxs-lookup"><span data-stu-id="467aa-130">SCP a directory from a Linux VM</span></span>

<span data-ttu-id="467aa-131">In questo esempio è copiare una directory di file di log da hello VM Linux verso il basso tooyour workstation.</span><span class="sxs-lookup"><span data-stu-id="467aa-131">For this example, we copy a directory of log files from hello Linux VM down tooyour workstation.</span></span> <span data-ttu-id="467aa-132">Poiché è possibile che un file di log contenga dati riservati,</span><span class="sxs-lookup"><span data-stu-id="467aa-132">A log file may or may not contain sensitive or secret data.</span></span> <span data-ttu-id="467aa-133">Tuttavia, tramite SCP garantisce la crittografia contenuto hello hello dei file di log.</span><span class="sxs-lookup"><span data-stu-id="467aa-133">However, using SCP ensures hello contents of hello log files are encrypted.</span></span> <span data-ttu-id="467aa-134">Utilizzo dei file di hello tootransfer SCP è tooget modo più semplice hello hello directory di log e file verso il basso workstation tooyour pur sicura.</span><span class="sxs-lookup"><span data-stu-id="467aa-134">Using SCP tootransfer hello files is hello easiest way tooget hello log directory and files down tooyour workstation while also being secure.</span></span>

<span data-ttu-id="467aa-135">Hello comando seguente copia i file in hello */home/azureuser/log/* directory nella directory /tmp locale toohello di hello macchina virtuale di Azure:</span><span class="sxs-lookup"><span data-stu-id="467aa-135">hello following command copies files in hello */home/azureuser/logs/* directory on hello Azure VM toohello local /tmp directory:</span></span>

```bash
scp -r azureuser@myserver.eastus.cloudapp.com:/home/azureuser/logs/. /tmp/
```

<span data-ttu-id="467aa-136">Hello `-r` flag cli indica SCP toorecursively copia hello file e directory dal punto di hello della directory hello elencati nel comando hello.</span><span class="sxs-lookup"><span data-stu-id="467aa-136">hello `-r` cli flag instructs SCP toorecursively copy hello files and directories from hello point of hello directory listed in hello command.</span></span>  <span data-ttu-id="467aa-137">Si noti che la sintassi della riga di comando hello sono anche simile tooa `cp` comando copia.</span><span class="sxs-lookup"><span data-stu-id="467aa-137">Also notice that hello command-line syntax is similar tooa `cp` copy command.</span></span>

## <a name="next-steps"></a><span data-ttu-id="467aa-138">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="467aa-138">Next steps</span></span>

* [<span data-ttu-id="467aa-139">Gestire utenti, SSH e controllo o i dischi di ripristino di macchine virtuali Linux di Azure utilizzando hello estensione VMAccess</span><span class="sxs-lookup"><span data-stu-id="467aa-139">Manage users, SSH, and check or repair disks on Azure Linux VMs using hello VMAccess Extension</span></span>](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
