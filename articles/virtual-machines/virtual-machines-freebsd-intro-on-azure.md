---
title: tooFreeBSD aaaIntroduction in Azure | Documenti Microsoft
description: Informazioni sull'uso delle macchine virtuali FreeBSD in Azure
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 32b87a5f-d024-4da0-8bf0-77e233d1422b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: kyliel
ms.openlocfilehash: eab7aeda7f7ef893740b39c0250aacc29d6fd71b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toofreebsd-on-azure"></a><span data-ttu-id="58212-103">Introduzione tooFreeBSD in Azure</span><span class="sxs-lookup"><span data-stu-id="58212-103">Introduction tooFreeBSD on Azure</span></span>
<span data-ttu-id="58212-104">Questo argomento offre una panoramica dell'esecuzione di una macchina virtuale FreeBSD in Azure.</span><span class="sxs-lookup"><span data-stu-id="58212-104">This topic provides an overview of running a FreeBSD virtual machine in Azure.</span></span>

## <a name="overview"></a><span data-ttu-id="58212-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="58212-105">Overview</span></span>
<span data-ttu-id="58212-106">FreeBSD per Microsoft Azure è un sistema operativo avanzate toopower moderna server, desktop e piattaforme incorporate.</span><span class="sxs-lookup"><span data-stu-id="58212-106">FreeBSD for Microsoft Azure is an advanced computer operating system used toopower modern servers, desktops, and embedded platforms.</span></span>

<span data-ttu-id="58212-107">Microsoft Corporation rende le immagini di FreeBSD disponibile in Azure con hello [agente Guest della macchina virtuale Azure](https://github.com/Azure/WALinuxAgent/) preconfigurato.</span><span class="sxs-lookup"><span data-stu-id="58212-107">Microsoft Corporation is making images of FreeBSD available on Azure with hello [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) pre-configured.</span></span> <span data-ttu-id="58212-108">Attualmente, hello versioni FreeBSD seguenti sono disponibili come immagini da Microsoft:</span><span class="sxs-lookup"><span data-stu-id="58212-108">Currently, hello following FreeBSD versions are offered as images by Microsoft:</span></span>

- <span data-ttu-id="58212-109">FreeBSD 10.3-RELEASE</span><span class="sxs-lookup"><span data-stu-id="58212-109">FreeBSD 10.3-RELEASE</span></span>
- <span data-ttu-id="58212-110">FreeBSD 11.0-RELEASE</span><span class="sxs-lookup"><span data-stu-id="58212-110">FreeBSD 11.0-RELEASE</span></span>

<span data-ttu-id="58212-111">Hello agente è responsabile per la comunicazione tra hello FreeBSD VM e l'infrastruttura di Azure per operazioni quali il provisioning di hello hello VM al primo utilizzo (nome utente, password o chiave SSH, nome host e così via) e le funzionalità di attivazione per selettive estensioni della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="58212-111">hello agent is responsible for communication between hello FreeBSD VM and hello Azure fabric for operations such as provisioning hello VM on first use (user name, password or SSH key, host name, etc.) and enabling functionality for selective VM extensions.</span></span>

<span data-ttu-id="58212-112">Come per le versioni future di FreeBSD, strategia hello è toostay corrente e rendere hello versioni più recenti disponibili subito dopo la pubblicazione dal team di progettazione di hello FreeBSD versione.</span><span class="sxs-lookup"><span data-stu-id="58212-112">As for future versions of FreeBSD, hello strategy is toostay current and make hello latest releases available shortly after they are published by hello FreeBSD release engineering team.</span></span>

## <a name="deploying-a-freebsd-virtual-machine"></a><span data-ttu-id="58212-113">Distribuzione di una macchina virtuale FreeBSD</span><span class="sxs-lookup"><span data-stu-id="58212-113">Deploying a FreeBSD virtual machine</span></span>
<span data-ttu-id="58212-114">Distribuisce una macchina virtuale FreeBSD è un processo semplice utilizzando un'immagine da hello Azure Marketplace da hello portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="58212-114">Deploying a FreeBSD virtual machine is a straightforward process using an image from hello Azure Marketplace from hello Azure portal:</span></span>

- [<span data-ttu-id="58212-115">10.3 FreeBSD in hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="58212-115">FreeBSD 10.3 on hello Azure Marketplace</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd103/)
- [<span data-ttu-id="58212-116">11.0 FreeBSD in hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="58212-116">FreeBSD 11.0 on hello Azure Marketplace</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/)

### <a name="create-a-freebsd-vm-through-azure-cli-20-on-freebsd"></a><span data-ttu-id="58212-117">Creare una VM FreeBSD tramite l'interfaccia della riga di comando di Azure 2.0 su FreeBSD</span><span class="sxs-lookup"><span data-stu-id="58212-117">Create a FreeBSD VM through Azure CLI 2.0 on FreeBSD</span></span>
<span data-ttu-id="58212-118">È necessario innanzitutto tooinstall [CLI di Azure 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) se il comando seguente in un computer di FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="58212-118">First you need tooinstall [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) though following command on a FreeBSD machine.</span></span>

```bash 
    curl -L https://aka.ms/InstallAzureCli | bash
```

<span data-ttu-id="58212-119">Se bash non è installato nel computer FreeBSD, eseguire il comando prima dell'installazione di hello seguente.</span><span class="sxs-lookup"><span data-stu-id="58212-119">If bash is not installed on your FreeBSD machine, run following command before hello installation.</span></span> 

```
    sudo pkg install bash
```

<span data-ttu-id="58212-120">Se nel computer FreeBSD, python non è installato, eseguire seguenti comandi prima dell'installazione di hello.</span><span class="sxs-lookup"><span data-stu-id="58212-120">If python is not installed on your FreeBSD machine, run following commands before hello installation.</span></span> 

```
    sudo pkg install python35
    cd /usr/local/bin 
    sudo rm /usr/local/bin/python 
    sudo ln -s /usr/local/bin/python3.5 /usr/local/bin/python
```

<span data-ttu-id="58212-121">Durante l'installazione di hello, viene chiesto `Modify profile tooupdate your $PATH and enable shell/tab completion now? (Y/n)`.</span><span class="sxs-lookup"><span data-stu-id="58212-121">During hello installation, you are asked `Modify profile tooupdate your $PATH and enable shell/tab completion now? (Y/n)`.</span></span> <span data-ttu-id="58212-122">Se si risponde `y` e immettere `/etc/rc.conf` come `a path tooan rc file tooupdate`, si potrebbe soddisfare problema hello `ERROR: [Errno 13] Permission denied`.</span><span class="sxs-lookup"><span data-stu-id="58212-122">If you answer `y` and enter `/etc/rc.conf` as `a path tooan rc file tooupdate`, you may meet hello problem `ERROR: [Errno 13] Permission denied`.</span></span> <span data-ttu-id="58212-123">tooresolve questo problema, è necessario concedere hello scrittura toocurrent diritto utente file hello `etc/rc.conf`.</span><span class="sxs-lookup"><span data-stu-id="58212-123">tooresolve this problem, you should grant hello write right toocurrent user against hello file `etc/rc.conf`.</span></span>

<span data-ttu-id="58212-124">A questo punto è possibile accedere ad Azure e creare la VM FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="58212-124">Now you can log in Azure and create your FreeBSD VM.</span></span> <span data-ttu-id="58212-125">Di seguito è un esempio toocreate una macchina virtuale 11.0 FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="58212-125">Below is an example toocreate a FreeBSD 11.0 VM.</span></span> <span data-ttu-id="58212-126">È inoltre possibile aggiungere il parametro hello `--public-ip-address-dns-name` con un nome DNS univoco globale per un indirizzo IP pubblico appena creato.</span><span class="sxs-lookup"><span data-stu-id="58212-126">You can also add hello parameter `--public-ip-address-dns-name` with a globally unique DNS name for a newly created Public IP.</span></span> 

```azurecli
    az login 
    az group create -n myResourceGroup -l westus az vm create -n myFreeBSD11 -g myResourceGroup --image MicrosoftOSTC:FreeBSD:11.0:latest --admin-username azureuser --ssh-key-value /etc/ssh/ssh_host_rsa_key.pub 
```

<span data-ttu-id="58212-127">È quindi possibile accedere tooyour FreeBSD VM tramite indirizzo ip hello stampato un output di hello di sopra di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="58212-127">Then you can log in tooyour FreeBSD VM through hello ip address that printed in hello output of above deployment.</span></span> 

```bash
    ssh azureuser@xx.xx.xx.xx -i /etc/ssh/ssh_host_rsa_key
```   

## <a name="vm-extensions-for-freebsd"></a><span data-ttu-id="58212-128">Estensioni di VM per FreeBSD</span><span class="sxs-lookup"><span data-stu-id="58212-128">VM extensions for FreeBSD</span></span>
<span data-ttu-id="58212-129">Di seguito sono descritte le estensioni di VM supportate in FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="58212-129">Following are supported VM extensions in FreeBSD.</span></span>

### <a name="vmaccess"></a><span data-ttu-id="58212-130">VMAccess</span><span class="sxs-lookup"><span data-stu-id="58212-130">VMAccess</span></span>
<span data-ttu-id="58212-131">Hello [VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) estensione possibile:</span><span class="sxs-lookup"><span data-stu-id="58212-131">hello [VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) extension can:</span></span>

* <span data-ttu-id="58212-132">Reimpostare la password di hello dell'utente sudo originale hello.</span><span class="sxs-lookup"><span data-stu-id="58212-132">Reset hello password of hello original sudo user.</span></span>
* <span data-ttu-id="58212-133">Creare un nuovo utente sudo con password hello specificata.</span><span class="sxs-lookup"><span data-stu-id="58212-133">Create a new sudo user with hello password specified.</span></span>
* <span data-ttu-id="58212-134">Impostare la chiave host pubblica hello con chiave hello specificata.</span><span class="sxs-lookup"><span data-stu-id="58212-134">Set hello public host key with hello key given.</span></span>
* <span data-ttu-id="58212-135">Reimposta chiave host pubblica hello fornita durante il provisioning se non viene fornito codice Product key host hello VM.</span><span class="sxs-lookup"><span data-stu-id="58212-135">Reset hello public host key provided during VM provisioning if hello host key is not provided.</span></span>
* <span data-ttu-id="58212-136">Aprire la porta SSH hello (22) e il ripristino hello sshd_config se reset_ssh è impostato tootrue.</span><span class="sxs-lookup"><span data-stu-id="58212-136">Open hello SSH port (22) and restore hello sshd_config if reset_ssh is set tootrue.</span></span>
* <span data-ttu-id="58212-137">Rimuovere l'utente esistente hello.</span><span class="sxs-lookup"><span data-stu-id="58212-137">Remove hello existing user.</span></span>
* <span data-ttu-id="58212-138">Controllare i dischi.</span><span class="sxs-lookup"><span data-stu-id="58212-138">Check disks.</span></span>
* <span data-ttu-id="58212-139">Riparare un disco aggiunto.</span><span class="sxs-lookup"><span data-stu-id="58212-139">Repair an added disk.</span></span>

### <a name="customscript"></a><span data-ttu-id="58212-140">CustomScript</span><span class="sxs-lookup"><span data-stu-id="58212-140">CustomScript</span></span>
<span data-ttu-id="58212-141">Hello [CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript) estensione possibile:</span><span class="sxs-lookup"><span data-stu-id="58212-141">hello [CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript) extension can:</span></span>

* <span data-ttu-id="58212-142">Se fornito, è possibile scaricare gli script personalizzato hello da Azure o l'archiviazione esterna pubblico (ad esempio, GitHub).</span><span class="sxs-lookup"><span data-stu-id="58212-142">If provided, download hello customized scripts from Azure Storage or external public storage (for example, GitHub).</span></span>
* <span data-ttu-id="58212-143">Eseguire script di punto di ingresso hello.</span><span class="sxs-lookup"><span data-stu-id="58212-143">Run hello entry point script.</span></span>
* <span data-ttu-id="58212-144">Supportare comandi inline.</span><span class="sxs-lookup"><span data-stu-id="58212-144">Support inline commands.</span></span>
* <span data-ttu-id="58212-145">Convertire automaticamente la nuova riga stile Windows in script della shell e Python.</span><span class="sxs-lookup"><span data-stu-id="58212-145">Convert Windows-style newline in shell and Python scripts automatically.</span></span>
* <span data-ttu-id="58212-146">Rimuovere automaticamente un carattere BOM negli script della shell e Python.</span><span class="sxs-lookup"><span data-stu-id="58212-146">Remove BOM in shell and Python scripts automatically.</span></span>
* <span data-ttu-id="58212-147">Proteggere i dati sensibili in CommandToExecute.</span><span class="sxs-lookup"><span data-stu-id="58212-147">Protect sensitive data in CommandToExecute.</span></span>

> [!NOTE]
> <span data-ttu-id="58212-148">FreeBSD VM supporta solo CustomScript versione 1. x per adesso.</span><span class="sxs-lookup"><span data-stu-id="58212-148">FreeBSD VM only supports CustomScript version 1.x by now.</span></span>  

## <a name="authentication-user-names-passwords-and-ssh-keys"></a><span data-ttu-id="58212-149">Autenticazione: nomi utente, password e chiavi SSH</span><span class="sxs-lookup"><span data-stu-id="58212-149">Authentication: user names, passwords, and SSH keys</span></span>
<span data-ttu-id="58212-150">Quando si crea una macchina virtuale FreeBSD utilizzando hello portale di Azure, è necessario fornire un nome utente, password o chiave pubblica SSH.</span><span class="sxs-lookup"><span data-stu-id="58212-150">When you're creating a FreeBSD virtual machine by using hello Azure portal, you must provide a user name, password, or SSH public key.</span></span>
<span data-ttu-id="58212-151">I nomi utente per la distribuzione di una macchina virtuale di FreeBSD in Azure non devono corrispondere i nomi degli account di sistema (UID < 100) è già presente nella macchina virtuale hello ("root", ad esempio).</span><span class="sxs-lookup"><span data-stu-id="58212-151">User names for deploying a FreeBSD virtual machine on Azure must not match names of system accounts (UID <100) already present in hello virtual machine ("root", for example).</span></span>
<span data-ttu-id="58212-152">Attualmente è supportata solo hello RSA chiave SSH.</span><span class="sxs-lookup"><span data-stu-id="58212-152">Currently, only hello RSA SSH key is supported.</span></span> <span data-ttu-id="58212-153">Una chiave SSH su più righe deve iniziare con `---- BEGIN SSH2 PUBLIC KEY ----` e terminare con `---- END SSH2 PUBLIC KEY ----`.</span><span class="sxs-lookup"><span data-stu-id="58212-153">A multiline SSH key must begin with `---- BEGIN SSH2 PUBLIC KEY ----` and end with `---- END SSH2 PUBLIC KEY ----`.</span></span>

## <a name="obtaining-superuser-privileges"></a><span data-ttu-id="58212-154">Ottenere privilegi utente avanzati</span><span class="sxs-lookup"><span data-stu-id="58212-154">Obtaining superuser privileges</span></span>
<span data-ttu-id="58212-155">account utente di Hello specificato durante la distribuzione di istanza di macchina virtuale in Azure è un account con privilegi.</span><span class="sxs-lookup"><span data-stu-id="58212-155">hello user account that is specified during virtual machine instance deployment on Azure is a privileged account.</span></span> <span data-ttu-id="58212-156">Hello pacchetto di sudo sia stato installato nella hello pubblicati FreeBSD immagine.</span><span class="sxs-lookup"><span data-stu-id="58212-156">hello package of sudo was installed in hello published FreeBSD image.</span></span>
<span data-ttu-id="58212-157">Dopo che si è connessi tramite l'account utente, è possibile eseguire i comandi come radice utilizzando la sintassi del comando hello.</span><span class="sxs-lookup"><span data-stu-id="58212-157">After you're logged in through this user account, you can run commands as root by using hello command syntax.</span></span>

```
    $ sudo <COMMAND>
```

<span data-ttu-id="58212-158">Facoltativamente, è possibile ottenere una shell radice usando `sudo -s`.</span><span class="sxs-lookup"><span data-stu-id="58212-158">You can optionally obtain a root shell by using `sudo -s`.</span></span>

## <a name="known-issues"></a><span data-ttu-id="58212-159">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="58212-159">Known issues</span></span>
<span data-ttu-id="58212-160">Hello [agente Guest della macchina virtuale Azure](https://github.com/Azure/WALinuxAgent/) versione 2.2.2 dispone di un [problema noto] (https://github.com/Azure/WALinuxAgent/pull/517) che causa un errore di effettuare il provisioning di hello per FreeBSD VM in Azure.</span><span class="sxs-lookup"><span data-stu-id="58212-160">hello [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) version 2.2.2 has a [known issue] (https://github.com/Azure/WALinuxAgent/pull/517) that causes hello provision failure for FreeBSD VM on Azure.</span></span> <span data-ttu-id="58212-161">Hello correzione è stata acquisita da [agente Guest della macchina virtuale Azure](https://github.com/Azure/WALinuxAgent/) versione 2.2.3 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="58212-161">hello fix was captured by [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) version 2.2.3 and later releases.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="58212-162">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="58212-162">Next steps</span></span>
* <span data-ttu-id="58212-163">Andare troppo[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) toocreate una VM FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="58212-163">Go too[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) toocreate a FreeBSD VM.</span></span>
* <span data-ttu-id="58212-164">Se si desidera toobring proprio tooAzure FreeBSD, fare riferimento troppo[creazione e caricamento di un tooAzure FreeBSD VHD](linux/classic/freebsd-create-upload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="58212-164">If you want toobring your own FreeBSD tooAzure, refer too[Create and upload a FreeBSD VHD tooAzure](linux/classic/freebsd-create-upload-vhd.md).</span></span>
