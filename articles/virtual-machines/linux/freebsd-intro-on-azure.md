---
title: Introduzione a FreeBSD in Azure | Microsoft Docs
description: Informazioni sull'uso delle macchine virtuali FreeBSD in Azure
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 32b87a5f-d024-4da0-8bf0-77e233d1422b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: kyliel
ms.openlocfilehash: 7ada9fddd7ffccc3dcbfe3eac05d99b710b67cbc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="introduction-to-freebsd-on-azure"></a><span data-ttu-id="7c708-103">Introduzione a FreeBSD in Azure</span><span class="sxs-lookup"><span data-stu-id="7c708-103">Introduction to FreeBSD on Azure</span></span>
<span data-ttu-id="7c708-104">Questo argomento offre una panoramica dell'esecuzione di una macchina virtuale FreeBSD in Azure.</span><span class="sxs-lookup"><span data-stu-id="7c708-104">This topic provides an overview of running a FreeBSD virtual machine in Azure.</span></span>

## <a name="overview"></a><span data-ttu-id="7c708-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="7c708-105">Overview</span></span>
<span data-ttu-id="7c708-106">FreeBSD per Microsoft Azure è un avanzato sistema operativo impiegato per potenziare moderne piattaforme incorporate, server e desktop.</span><span class="sxs-lookup"><span data-stu-id="7c708-106">FreeBSD for Microsoft Azure is an advanced computer operating system used to power modern servers, desktops, and embedded platforms.</span></span>

<span data-ttu-id="7c708-107">Microsoft Corporation sta creando immagini di FreeBSD disponibili in Azure con l'[agente guest della macchina virtuale di Azure](https://github.com/Azure/WALinuxAgent/) preconfigurato.</span><span class="sxs-lookup"><span data-stu-id="7c708-107">Microsoft Corporation is making images of FreeBSD available on Azure with the [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) pre-configured.</span></span> <span data-ttu-id="7c708-108">Attualmente, sono disponibili come immagini le seguenti versioni di FreeBSD:</span><span class="sxs-lookup"><span data-stu-id="7c708-108">Currently, the following FreeBSD versions are offered as images by Microsoft:</span></span>

- <span data-ttu-id="7c708-109">FreeBSD 10.3-RELEASE</span><span class="sxs-lookup"><span data-stu-id="7c708-109">FreeBSD 10.3-RELEASE</span></span>
- <span data-ttu-id="7c708-110">FreeBSD 11.0-RELEASE</span><span class="sxs-lookup"><span data-stu-id="7c708-110">FreeBSD 11.0-RELEASE</span></span>

<span data-ttu-id="7c708-111">L'agente è responsabile della comunicazione tra la VM FreeBSD e l'infrastruttura di Azure per operazioni quali il provisioning della VM al primo uso (nome utente, password o chiave SSH, nome host e così via) e l'abilitazione di funzionalità per estensioni di VM selettive.</span><span class="sxs-lookup"><span data-stu-id="7c708-111">The agent is responsible for communication between the FreeBSD VM and the Azure fabric for operations such as provisioning the VM on first use (user name, password or SSH key, host name, etc.) and enabling functionality for selective VM extensions.</span></span>

<span data-ttu-id="7c708-112">Per quanto riguarda le versioni future di FreeBSD, la strategia consiste nel rimanere aggiornati e rendere disponibili le versioni più recenti subito dopo la pubblicazione da parte del team di progettazione di FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="7c708-112">As for future versions of FreeBSD, the strategy is to stay current and make the latest releases available shortly after they are published by the FreeBSD release engineering team.</span></span>

## <a name="deploying-a-freebsd-virtual-machine"></a><span data-ttu-id="7c708-113">Distribuzione di una macchina virtuale FreeBSD</span><span class="sxs-lookup"><span data-stu-id="7c708-113">Deploying a FreeBSD virtual machine</span></span>
<span data-ttu-id="7c708-114">Il processo di distribuzione di una macchina virtuale FreeBSD è semplice e rapido se si usa un'immagine di Azure Marketplace dal portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="7c708-114">Deploying a FreeBSD virtual machine is a straightforward process using an image from the Azure Marketplace from the Azure portal:</span></span>

- [<span data-ttu-id="7c708-115">FreeBSD 10.3 in Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="7c708-115">FreeBSD 10.3 on the Azure Marketplace</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd103/)
- [<span data-ttu-id="7c708-116">FreeBSD 11.0 in Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="7c708-116">FreeBSD 11.0 on the Azure Marketplace</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/)

### <a name="create-a-freebsd-vm-through-azure-cli-20-on-freebsd"></a><span data-ttu-id="7c708-117">Creare una VM FreeBSD tramite l'interfaccia della riga di comando di Azure 2.0 su FreeBSD</span><span class="sxs-lookup"><span data-stu-id="7c708-117">Create a FreeBSD VM through Azure CLI 2.0 on FreeBSD</span></span>
<span data-ttu-id="7c708-118">Prima di tutto è necessario installare l'[interfaccia della riga di comando di Azure 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) in un computer FreeBSD con il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="7c708-118">First you need to install [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) though following command on a FreeBSD machine.</span></span>

```bash 
curl -L https://aka.ms/InstallAzureCli | bash
```

<span data-ttu-id="7c708-119">Se bash non è installato nel computer FreeBSD, eseguire il seguente comando prima dell'installazione.</span><span class="sxs-lookup"><span data-stu-id="7c708-119">If bash is not installed on your FreeBSD machine, run following command before the installation.</span></span> 

```bash
sudo pkg install bash
```

<span data-ttu-id="7c708-120">Se python non è installato nel computer FreeBSD, eseguire i seguenti comandi prima dell'installazione.</span><span class="sxs-lookup"><span data-stu-id="7c708-120">If python is not installed on your FreeBSD machine, run following commands before the installation.</span></span> 

```bash
sudo pkg install python35
cd /usr/local/bin 
sudo rm /usr/local/bin/python 
sudo ln -s /usr/local/bin/python3.5 /usr/local/bin/python
```

<span data-ttu-id="7c708-121">Durante l'installazione, viene visualizzata la seguente richiesta: `Modify profile to update your $PATH and enable shell/tab completion now? (Y/n)`.</span><span class="sxs-lookup"><span data-stu-id="7c708-121">During the installation, you are asked `Modify profile to update your $PATH and enable shell/tab completion now? (Y/n)`.</span></span> <span data-ttu-id="7c708-122">Se si risponde `y` e si immette `/etc/rc.conf` come `a path to an rc file to update`, può verificarsi il problema `ERROR: [Errno 13] Permission denied`.</span><span class="sxs-lookup"><span data-stu-id="7c708-122">If you answer `y` and enter `/etc/rc.conf` as `a path to an rc file to update`, you may meet the problem `ERROR: [Errno 13] Permission denied`.</span></span> <span data-ttu-id="7c708-123">Per risolvere questo problema assegnare i diritti di scrittura all'utente corrente per il file `etc/rc.conf`.</span><span class="sxs-lookup"><span data-stu-id="7c708-123">To resolve this problem, you should grant the write right to current user against the file `etc/rc.conf`.</span></span>

<span data-ttu-id="7c708-124">A questo punto è possibile accedere ad Azure e creare la VM FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="7c708-124">Now you can log in Azure and create your FreeBSD VM.</span></span> <span data-ttu-id="7c708-125">Di seguito è riportato un esempio di creazione di una VM FreeBSD 11.0.</span><span class="sxs-lookup"><span data-stu-id="7c708-125">Below is an example to create a FreeBSD 11.0 VM.</span></span> <span data-ttu-id="7c708-126">È anche possibile aggiungere il parametro `--public-ip-address-dns-name` con un nome DNS univoco globale per un indirizzo IP pubblico appena creato.</span><span class="sxs-lookup"><span data-stu-id="7c708-126">You can also add the parameter `--public-ip-address-dns-name` with a globally unique DNS name for a newly created Public IP.</span></span> 

```azurecli
az login 
az group create --name myResourceGroup --location eastus
az vm create --name myFreeBSD11 \
    --resource-group myResourceGroup \
    --image MicrosoftOSTC:FreeBSD:11.0:latest \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="7c708-127">Quindi è possibile accedere alla VM FreeBSD mediante l'indirizzo IP visualizzato nell'output della distribuzione mostrata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="7c708-127">Then you can log in to your FreeBSD VM through the ip address that printed in the output of above deployment.</span></span> 

```bash
ssh azureuser@xx.xx.xx.xx -i /etc/ssh/ssh_host_rsa_key
```   

## <a name="vm-extensions-for-freebsd"></a><span data-ttu-id="7c708-128">Estensioni di VM per FreeBSD</span><span class="sxs-lookup"><span data-stu-id="7c708-128">VM extensions for FreeBSD</span></span>
<span data-ttu-id="7c708-129">Di seguito sono descritte le estensioni di VM supportate in FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="7c708-129">Following are supported VM extensions in FreeBSD.</span></span>

### <a name="vmaccess"></a><span data-ttu-id="7c708-130">VMAccess</span><span class="sxs-lookup"><span data-stu-id="7c708-130">VMAccess</span></span>
<span data-ttu-id="7c708-131">Con l'estensione [VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) è possibile:</span><span class="sxs-lookup"><span data-stu-id="7c708-131">The [VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) extension can:</span></span>

* <span data-ttu-id="7c708-132">Reimpostare la password dell'utente sudo originale.</span><span class="sxs-lookup"><span data-stu-id="7c708-132">Reset the password of the original sudo user.</span></span>
* <span data-ttu-id="7c708-133">Creare un nuovo utente sudo con la password specificata.</span><span class="sxs-lookup"><span data-stu-id="7c708-133">Create a new sudo user with the password specified.</span></span>
* <span data-ttu-id="7c708-134">Impostare la chiave host pubblica con la chiave specificata.</span><span class="sxs-lookup"><span data-stu-id="7c708-134">Set the public host key with the key given.</span></span>
* <span data-ttu-id="7c708-135">Reimpostare la chiave host pubblica specificata durante il provisioning di VM se non è stata indicata la chiave host.</span><span class="sxs-lookup"><span data-stu-id="7c708-135">Reset the public host key provided during VM provisioning if the host key is not provided.</span></span>
* <span data-ttu-id="7c708-136">Aprire la porta SSH (22) e ripristinare sshd_config se reset_ssh è impostato su true.</span><span class="sxs-lookup"><span data-stu-id="7c708-136">Open the SSH port (22) and restore the sshd_config if reset_ssh is set to true.</span></span>
* <span data-ttu-id="7c708-137">Rimuovere l'utente esistente.</span><span class="sxs-lookup"><span data-stu-id="7c708-137">Remove the existing user.</span></span>
* <span data-ttu-id="7c708-138">Controllare i dischi.</span><span class="sxs-lookup"><span data-stu-id="7c708-138">Check disks.</span></span>
* <span data-ttu-id="7c708-139">Riparare un disco aggiunto.</span><span class="sxs-lookup"><span data-stu-id="7c708-139">Repair an added disk.</span></span>

### <a name="customscript"></a><span data-ttu-id="7c708-140">CustomScript</span><span class="sxs-lookup"><span data-stu-id="7c708-140">CustomScript</span></span>
<span data-ttu-id="7c708-141">Con l'estensione [CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript) è possibile:</span><span class="sxs-lookup"><span data-stu-id="7c708-141">The [CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript) extension can:</span></span>

* <span data-ttu-id="7c708-142">Se disponibili, scaricare gli script personalizzati dall'archivio di Azure o dall'archivio pubblico esterno, ad esempio GitHub.</span><span class="sxs-lookup"><span data-stu-id="7c708-142">If provided, download the customized scripts from Azure Storage or external public storage (for example, GitHub).</span></span>
* <span data-ttu-id="7c708-143">Eseguire lo script di punto di ingresso.</span><span class="sxs-lookup"><span data-stu-id="7c708-143">Run the entry point script.</span></span>
* <span data-ttu-id="7c708-144">Supportare comandi inline.</span><span class="sxs-lookup"><span data-stu-id="7c708-144">Support inline commands.</span></span>
* <span data-ttu-id="7c708-145">Convertire automaticamente la nuova riga stile Windows in script della shell e Python.</span><span class="sxs-lookup"><span data-stu-id="7c708-145">Convert Windows-style newline in shell and Python scripts automatically.</span></span>
* <span data-ttu-id="7c708-146">Rimuovere automaticamente un carattere BOM negli script della shell e Python.</span><span class="sxs-lookup"><span data-stu-id="7c708-146">Remove BOM in shell and Python scripts automatically.</span></span>
* <span data-ttu-id="7c708-147">Proteggere i dati sensibili in CommandToExecute.</span><span class="sxs-lookup"><span data-stu-id="7c708-147">Protect sensitive data in CommandToExecute.</span></span>

> [!NOTE]
> <span data-ttu-id="7c708-148">FreeBSD VM supporta solo CustomScript versione 1. x per adesso.</span><span class="sxs-lookup"><span data-stu-id="7c708-148">FreeBSD VM only supports CustomScript version 1.x by now.</span></span>  

## <a name="authentication-user-names-passwords-and-ssh-keys"></a><span data-ttu-id="7c708-149">Autenticazione: nomi utente, password e chiavi SSH</span><span class="sxs-lookup"><span data-stu-id="7c708-149">Authentication: user names, passwords, and SSH keys</span></span>
<span data-ttu-id="7c708-150">Quando si crea una macchina virtuale FreeBSD usando il portale di Azure, è necessario immettere un nome utente, una password o una chiave pubblica SSH.</span><span class="sxs-lookup"><span data-stu-id="7c708-150">When you're creating a FreeBSD virtual machine by using the Azure portal, you must provide a user name, password, or SSH public key.</span></span>
<span data-ttu-id="7c708-151">I nomi utente per la distribuzione di una macchina virtuale FreeBSD in Azure non devono corrispondere ai nomi degli account di sistema (UID <100) già presenti nella macchina virtuale, ad esempio "root".</span><span class="sxs-lookup"><span data-stu-id="7c708-151">User names for deploying a FreeBSD virtual machine on Azure must not match names of system accounts (UID <100) already present in the virtual machine ("root", for example).</span></span>
<span data-ttu-id="7c708-152">È attualmente supportata solo la chiave RSA SSH.</span><span class="sxs-lookup"><span data-stu-id="7c708-152">Currently, only the RSA SSH key is supported.</span></span> <span data-ttu-id="7c708-153">Una chiave SSH su più righe deve iniziare con `---- BEGIN SSH2 PUBLIC KEY ----` e terminare con `---- END SSH2 PUBLIC KEY ----`.</span><span class="sxs-lookup"><span data-stu-id="7c708-153">A multiline SSH key must begin with `---- BEGIN SSH2 PUBLIC KEY ----` and end with `---- END SSH2 PUBLIC KEY ----`.</span></span>

## <a name="obtaining-superuser-privileges"></a><span data-ttu-id="7c708-154">Ottenere privilegi utente avanzati</span><span class="sxs-lookup"><span data-stu-id="7c708-154">Obtaining superuser privileges</span></span>
<span data-ttu-id="7c708-155">L'account utente specificato durante la distribuzione di istanze di macchine virtuali in Azure è un account con privilegi.</span><span class="sxs-lookup"><span data-stu-id="7c708-155">The user account that is specified during virtual machine instance deployment on Azure is a privileged account.</span></span> <span data-ttu-id="7c708-156">Il pacchetto di sudo è stato installato nell'immagine FreeBSD pubblicata.</span><span class="sxs-lookup"><span data-stu-id="7c708-156">The package of sudo was installed in the published FreeBSD image.</span></span>
<span data-ttu-id="7c708-157">Dopo aver eseguito l'accesso usando questo account utente, è possibile eseguire comandi come utente ROOT usando la sintassi del comando.</span><span class="sxs-lookup"><span data-stu-id="7c708-157">After you're logged in through this user account, you can run commands as root by using the command syntax.</span></span>

```
$ sudo <COMMAND>
```

<span data-ttu-id="7c708-158">Facoltativamente, è possibile ottenere una shell radice usando `sudo -s`.</span><span class="sxs-lookup"><span data-stu-id="7c708-158">You can optionally obtain a root shell by using `sudo -s`.</span></span>

## <a name="known-issues"></a><span data-ttu-id="7c708-159">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="7c708-159">Known issues</span></span>
<span data-ttu-id="7c708-160">[Agente guest per macchine virtuali di Azure](https://github.com/Azure/WALinuxAgent/) versione 2.2.2 presenta un [problema noto] (https://github.com/Azure/WALinuxAgent/pull/517) che impedisce il provisioning di una VM FreeBSD in Azure.</span><span class="sxs-lookup"><span data-stu-id="7c708-160">The [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) version 2.2.2 has a [known issue] (https://github.com/Azure/WALinuxAgent/pull/517) that causes the provision failure for FreeBSD VM on Azure.</span></span> <span data-ttu-id="7c708-161">La correzione è stata acquisita da [Agente guest di macchine virtuali di Azure](https://github.com/Azure/WALinuxAgent/) versione 2.2.3 e successive.</span><span class="sxs-lookup"><span data-stu-id="7c708-161">The fix was captured by [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) version 2.2.3 and later releases.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="7c708-162">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7c708-162">Next steps</span></span>
* <span data-ttu-id="7c708-163">Passare ad [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) per creare una VM FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="7c708-163">Go to [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) to create a FreeBSD VM.</span></span>
* <span data-ttu-id="7c708-164">Se si desidera trasferire il proprio sistema operativo FreeBSD in Azure, fare riferimento a [Creare e caricare un disco rigido virtuale con FreeBSD in Azure](classic/freebsd-create-upload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="7c708-164">If you want to bring your own FreeBSD to Azure, refer to [Create and upload a FreeBSD VHD to Azure](classic/freebsd-create-upload-vhd.md).</span></span>
