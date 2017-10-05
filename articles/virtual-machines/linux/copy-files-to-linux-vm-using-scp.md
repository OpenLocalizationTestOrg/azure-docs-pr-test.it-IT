---
title: Spostare file da e verso macchine virtuali Linux di Azure usando SCP | Microsoft Docs
description: Spostare in sicurezza file da e verso una macchina virtuale Linux in Azure usando SCP e una coppia di chiavi SSH.
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
ms.openlocfilehash: 736f7c11ec3de04f1ad52ee29d0a4c952c9b0545
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="move-files-to-and-from-a-linux-vm-using-scp"></a><span data-ttu-id="e0f99-103">Spostare file da e verso una macchina virtuale Linux usando SCP</span><span class="sxs-lookup"><span data-stu-id="e0f99-103">Move files to and from a Linux VM using SCP</span></span>

<span data-ttu-id="e0f99-104">Questo articolo illustra come spostare file da una workstation a una macchina virtuale Linux di Azure, o viceversa, usando Secure Copy (SCP).</span><span class="sxs-lookup"><span data-stu-id="e0f99-104">This article shows how to move files from your workstation up to an Azure Linux VM, or from an Azure Linux VM down to your workstation, using Secure Copy (SCP).</span></span> <span data-ttu-id="e0f99-105">Il trasferimento di file tra una workstation e una macchina virtuale Linux in modo rapido e sicuro è un aspetto essenziale della gestione dell'infrastruttura di Azure.</span><span class="sxs-lookup"><span data-stu-id="e0f99-105">Moving files between your workstation and a Linux VM, quickly and securely, is critical for managing your Azure infrastructure.</span></span> 

<span data-ttu-id="e0f99-106">Per questo articolo è necessaria una macchina virtuale Linux distribuita in Azure tramite [file di chiavi SSH pubbliche e private](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e0f99-106">For this article, you need a Linux VM deployed in Azure using [SSH public and private key files](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="e0f99-107">È necessario anche un client SCP per il computer locale:</span><span class="sxs-lookup"><span data-stu-id="e0f99-107">You also need an SCP client for your local computer.</span></span> <span data-ttu-id="e0f99-108">uno strumento basato su SSH e incluso nella shell Bash predefinita della maggior parte dei computer Mac e Linux e in alcune shell di Windows.</span><span class="sxs-lookup"><span data-stu-id="e0f99-108">It is built on top of SSH and included in the default Bash shell of most Linux and Mac computers and some Windows shells.</span></span>

## <a name="quick-commands"></a><span data-ttu-id="e0f99-109">Comandi rapidi</span><span class="sxs-lookup"><span data-stu-id="e0f99-109">Quick commands</span></span>

<span data-ttu-id="e0f99-110">Copiare un file in una macchina virtuale Linux</span><span class="sxs-lookup"><span data-stu-id="e0f99-110">Copy a file up to the Linux VM</span></span>

```bash
scp file azureuser@azurehost:directory/targetfile
```

<span data-ttu-id="e0f99-111">Copiare un file da una macchina virtuale Linux</span><span class="sxs-lookup"><span data-stu-id="e0f99-111">Copy a file down from the Linux VM</span></span>

```bash
scp azureuser@azurehost:directory/file targetfile
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="e0f99-112">Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="e0f99-112">Detailed walkthrough</span></span>

<span data-ttu-id="e0f99-113">A titolo di esempio, si sposterà un file di configurazione di Azure in una macchina virtuale Linux e si scaricherà la directory di un file di log, usando in entrambi i casi SCP e chiavi SSH.</span><span class="sxs-lookup"><span data-stu-id="e0f99-113">As examples, we move an Azure configuration file up to a Linux VM and pull down a log file directory, both using SCP and SSH keys.</span></span>   

## <a name="ssh-key-pair-authentication"></a><span data-ttu-id="e0f99-114">Autenticazione della coppia di chiavi SSH</span><span class="sxs-lookup"><span data-stu-id="e0f99-114">SSH key pair authentication</span></span>

<span data-ttu-id="e0f99-115">SCP usa SSH per il livello di trasporto.</span><span class="sxs-lookup"><span data-stu-id="e0f99-115">SCP uses SSH for the transport layer.</span></span> <span data-ttu-id="e0f99-116">SSH gestisce l'autenticazione nell'host di destinazione e sposta il file in un tunnel crittografato fornito per impostazione predefinita con SSH.</span><span class="sxs-lookup"><span data-stu-id="e0f99-116">SSH handles the authentication on the destination host, and it moves the file in an encrypted tunnel provided by default with SSH.</span></span> <span data-ttu-id="e0f99-117">Per l'autenticazione SSH è possibile usare nomi utente e password.</span><span class="sxs-lookup"><span data-stu-id="e0f99-117">For SSH authentication, usernames and passwords can be used.</span></span> <span data-ttu-id="e0f99-118">Per una maggiore sicurezza, tuttavia, è consigliabile eseguire l'autenticazione tramite file di chiavi SSH pubbliche e private.</span><span class="sxs-lookup"><span data-stu-id="e0f99-118">However, SSH public and private key authentication are recommended as a security best practice.</span></span> <span data-ttu-id="e0f99-119">Dopo che SSH ha autenticato la connessione, SCP avvia il processo di copia del file.</span><span class="sxs-lookup"><span data-stu-id="e0f99-119">Once SSH has authenticated the connection, SCP then begins copying the file.</span></span> <span data-ttu-id="e0f99-120">Combinando un file `~/.ssh/config` correttamente configurato con chiavi SSH pubbliche e private, è possibile stabilire la connessione SCP usando solo un nome di server (o un indirizzo IP).</span><span class="sxs-lookup"><span data-stu-id="e0f99-120">Using a properly configured `~/.ssh/config` and SSH public and private keys, the SCP connection can be established by just using a server name (or IP address).</span></span> <span data-ttu-id="e0f99-121">Se si ha una sola chiave SSH, SCP la cerca nella directory `~/.ssh/` e, per impostazione predefinita, la usa per accedere alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e0f99-121">If you only have one SSH key, SCP looks for it in the `~/.ssh/` directory, and uses it by default to log in to the VM.</span></span>

<span data-ttu-id="e0f99-122">Per altre informazioni sulla configurazione del file `~/.ssh/config` e delle chiavi SSH pubbliche e private, vedere [Creare chiavi SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e0f99-122">For more information on configuring your `~/.ssh/config` and SSH public and private keys, see [Create SSH keys](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="scp-a-file-to-a-linux-vm"></a><span data-ttu-id="e0f99-123">Copia sicura di un file in una macchina virtuale Linux</span><span class="sxs-lookup"><span data-stu-id="e0f99-123">SCP a file to a Linux VM</span></span>

<span data-ttu-id="e0f99-124">Nel primo esempio si copia un file di configurazione di Azure in una macchina virtuale Linux usata per distribuire l'automazione.</span><span class="sxs-lookup"><span data-stu-id="e0f99-124">For the first example, we copy an Azure configuration file up to a Linux VM that is used to deploy automation.</span></span> <span data-ttu-id="e0f99-125">Poiché questo file contiene credenziali di API di Azure, che includono informazioni riservate, la sicurezza è particolarmente importante</span><span class="sxs-lookup"><span data-stu-id="e0f99-125">Because this file contains Azure API credentials, which include secrets, security is important.</span></span> <span data-ttu-id="e0f99-126">e il tunnel crittografato fornito con SSH assicura la protezione dei contenuti del file.</span><span class="sxs-lookup"><span data-stu-id="e0f99-126">The encrypted tunnel provided by SSH protects the contents of the file.</span></span>

<span data-ttu-id="e0f99-127">Il comando seguente consente di copiare il file *.azure/config* locale in una macchina virtuale di Azure con FQDN: *myserver.eastus.cloudapp.azure.com*. Il nome utente dell'amministratore nella macchina virtuale di Azure è *azureuser*.</span><span class="sxs-lookup"><span data-stu-id="e0f99-127">The following command copies the local *.azure/config* file to an Azure VM with FQDN *myserver.eastus.cloudapp.azure.com*. The admin user name on the Azure VM is *azureuser*.</span></span> <span data-ttu-id="e0f99-128">Il file è destinato ad essere inserito nella directory */home/azureuser/*.</span><span class="sxs-lookup"><span data-stu-id="e0f99-128">The file is targeted to the */home/azureuser/* directory.</span></span> <span data-ttu-id="e0f99-129">Nel comando sostituire i valori predefiniti con quelli personali.</span><span class="sxs-lookup"><span data-stu-id="e0f99-129">Substitute your own values in this command.</span></span>

```bash
scp ~/.azure/config azureuser@myserver.eastus.cloudapp.com:/home/azureuser/config
```

## <a name="scp-a-directory-from-a-linux-vm"></a><span data-ttu-id="e0f99-130">Copia sicura di una directory da una macchina virtuale Linux</span><span class="sxs-lookup"><span data-stu-id="e0f99-130">SCP a directory from a Linux VM</span></span>

<span data-ttu-id="e0f99-131">In questo esempio si copia una directory di file di log dalla macchina virtuale Linux in una workstation.</span><span class="sxs-lookup"><span data-stu-id="e0f99-131">For this example, we copy a directory of log files from the Linux VM down to your workstation.</span></span> <span data-ttu-id="e0f99-132">Poiché è possibile che un file di log contenga dati riservati,</span><span class="sxs-lookup"><span data-stu-id="e0f99-132">A log file may or may not contain sensitive or secret data.</span></span> <span data-ttu-id="e0f99-133">con SCP si ha la certezza che i contenuti dei file di log vengano crittografati.</span><span class="sxs-lookup"><span data-stu-id="e0f99-133">However, using SCP ensures the contents of the log files are encrypted.</span></span> <span data-ttu-id="e0f99-134">L'uso di SCP per il trasferimento dei file costituisce il modo più semplice per spostare in totale sicurezza file e directory di log in una workstation.</span><span class="sxs-lookup"><span data-stu-id="e0f99-134">Using SCP to transfer the files is the easiest way to get the log directory and files down to your workstation while also being secure.</span></span>

<span data-ttu-id="e0f99-135">Il comando seguente consente di copiare i file contenuti nella directory */home/azureuser/logs/* nella directory /tmp locale della macchina virtuale di Azure:</span><span class="sxs-lookup"><span data-stu-id="e0f99-135">The following command copies files in the */home/azureuser/logs/* directory on the Azure VM to the local /tmp directory:</span></span>

```bash
scp -r azureuser@myserver.eastus.cloudapp.com:/home/azureuser/logs/. /tmp/
```

<span data-ttu-id="e0f99-136">Il flag dell'interfaccia della riga di comando `-r` indica a SCP di copiare in modo ricorsivo i file e le directory dal punto della directory specificato nel comando.</span><span class="sxs-lookup"><span data-stu-id="e0f99-136">The `-r` cli flag instructs SCP to recursively copy the files and directories from the point of the directory listed in the command.</span></span>  <span data-ttu-id="e0f99-137">Osservare inoltre come la sintassi della riga di comando sia simile al comando di copia `cp`.</span><span class="sxs-lookup"><span data-stu-id="e0f99-137">Also notice that the command-line syntax is similar to a `cp` copy command.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0f99-138">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e0f99-138">Next steps</span></span>

* [<span data-ttu-id="e0f99-139">Gestire utenti, SSH e dischi di controllo o di ripristino in VM Linux di Azure tramite l'estensione VMAccess</span><span class="sxs-lookup"><span data-stu-id="e0f99-139">Manage users, SSH, and check or repair disks on Azure Linux VMs using the VMAccess Extension</span></span>](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)