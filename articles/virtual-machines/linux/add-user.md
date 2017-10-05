---
title: Aggiungere un utente a una macchina virtuale Linux in Azure | Microsoft Docs
description: Informazioni su come aggiungere un utente a una macchina virtuale Linux in Azure.
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f8aa633b-8b75-45d7-b61d-11ac112cedd5
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/18/2016
ms.author: v-livech
ms.openlocfilehash: a95157f57c0cbd1f2a9ed68a0fe83140d7c9ec40
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="add-a-user-to-an-azure-vm"></a><span data-ttu-id="1830d-103">Aggiungere un utente a una macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="1830d-103">Add a user to an Azure VM</span></span>
<span data-ttu-id="1830d-104">Una delle prime attività su qualsiasi VM Linux consiste nel creare un nuovo utente.</span><span class="sxs-lookup"><span data-stu-id="1830d-104">One of the first tasks on any new Linux VM is to create a new user.</span></span>  <span data-ttu-id="1830d-105">Questo articolo descrive la creazione di un account utente sudo, l'impostazione della password, l'aggiunta di chiavi pubbliche SSH e infine l'uso di `visudo` per consentire l'uso di sudo senza password.</span><span class="sxs-lookup"><span data-stu-id="1830d-105">In this article, we walk through creating a sudo user account, setting the password, adding SSH Public Keys, and finally use `visudo` to allow sudo without a password.</span></span>

<span data-ttu-id="1830d-106">Prerequisiti: un [account Azure](https://azure.microsoft.com/pricing/free-trial/), [chiavi pubbliche e private SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), un gruppo di risorse di Azure e l’interfaccia della riga di comando di Azure installata e con la modalità Azure Resource Manager attivata tramite `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="1830d-106">Prerequisites are: [an Azure account](https://azure.microsoft.com/pricing/free-trial/), [SSH public and private keys](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), an Azure resource group, and the Azure CLI installed and switched to Azure Resource Manager mode using `azure config mode arm`.</span></span>

## <a name="quick-commands"></a><span data-ttu-id="1830d-107">Comandi rapidi</span><span class="sxs-lookup"><span data-stu-id="1830d-107">Quick Commands</span></span>
```bash
# Add a new user on RedHat family distros
sudo useradd -G wheel exampleUser

# Add a new user on Debian family distros
sudo useradd -G sudo exampleUser

# Set a password
sudo passwd exampleUser
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully

# Copy the SSH Public Key to the new user
ssh-copy-id -i ~/.ssh/id_rsa exampleuser@exampleserver

# Change sudoers to allow no password
# Execute visudo as root to edit the /etc/sudoers file
visudo

# On RedHat family distros uncomment this line:
## Same thing without a password
# %wheel        ALL=(ALL)       NOPASSWD: ALL

# to this
## Same thing without a password
%wheel        ALL=(ALL)       NOPASSWD: ALL

# On Debian family distros change this line:
# Allow members of group sudo to execute any command
%sudo   ALL=(ALL:ALL) ALL

# to this
%sudo   ALL=(ALL) NOPASSWD:ALL

# Verify everything
# Verify the SSH keys & User account
bill@slackware$ ssh -i ~/.ssh/id_rsa exampleuser@exampleserver

# Verify sudo access
sudo top
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="1830d-108">Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="1830d-108">Detailed Walkthrough</span></span>
### <a name="introduction"></a><span data-ttu-id="1830d-109">Introduzione</span><span class="sxs-lookup"><span data-stu-id="1830d-109">Introduction</span></span>
<span data-ttu-id="1830d-110">Una delle prime e più comuni attività in un nuovo server consiste nell'aggiungere un account utente.</span><span class="sxs-lookup"><span data-stu-id="1830d-110">One of the first and most common task with a new server is to add a user account.</span></span>  <span data-ttu-id="1830d-111">Gli accessi radice devono essere disabilitati e l'account radice stesso non deve essere usato con il server Linux, solo sudo.</span><span class="sxs-lookup"><span data-stu-id="1830d-111">Root logins should be disabled and the root account itself should not be used with your Linux server, only sudo.</span></span>  <span data-ttu-id="1830d-112">L'assegnazione all'utente dei privilegi di escalation radice usando sudo rappresenta il metodo migliore per amministrare e usare Linux.</span><span class="sxs-lookup"><span data-stu-id="1830d-112">Giving a user root escalation privileges using sudo it the proper way to administer and use Linux.</span></span>

<span data-ttu-id="1830d-113">Usando il comando `useradd` vengono aggiunti gli account utente alla VM Linux.</span><span class="sxs-lookup"><span data-stu-id="1830d-113">Using the command `useradd` we are adding user accounts to the Linux VM.</span></span>  <span data-ttu-id="1830d-114">L'esecuzione di `useradd` modifica `/etc/passwd`, `/etc/shadow`, `/etc/group` e `/etc/gshadow`.</span><span class="sxs-lookup"><span data-stu-id="1830d-114">Running `useradd` modifies `/etc/passwd`, `/etc/shadow`, `/etc/group`, and `/etc/gshadow`.</span></span>  <span data-ttu-id="1830d-115">Viene aggiunto un flag di riga di comando al comando `useradd` per aggiungere anche il nuovo utente al gruppo sudo corretto in Linux.</span><span class="sxs-lookup"><span data-stu-id="1830d-115">We are adding a command-line flag to the `useradd` command to also add the new user to the proper sudo group on Linux.</span></span>  <span data-ttu-id="1830d-116">Sebbene `useradd` crei una voce in `/etc/passwd`, il comando non assegna una password al nuovo account utente.</span><span class="sxs-lookup"><span data-stu-id="1830d-116">Even thou `useradd` creates an entry into `/etc/passwd` it does not give the new user account a password.</span></span>  <span data-ttu-id="1830d-117">Viene creata una password iniziale per il nuovo utente usando il semplice comando `passwd` .</span><span class="sxs-lookup"><span data-stu-id="1830d-117">We are creating an initial password for the new user using the simple `passwd` command.</span></span>  <span data-ttu-id="1830d-118">L'ultimo passaggio è costituito dalla modifica delle regole di sudo per consentire all'utente di eseguire comandi con i privilegi sudo senza dover immettere una password per ogni comando.</span><span class="sxs-lookup"><span data-stu-id="1830d-118">The last step is to modify the sudo rules to allow that user to execute commands with sudo privileges without having to enter a password for every command.</span></span>  <span data-ttu-id="1830d-119">L'accesso con la chiave pubblica fa presupporre che l'account utente sia privo di attori pericolosi, quindi viene consentito l'accesso a sudo senza password.</span><span class="sxs-lookup"><span data-stu-id="1830d-119">Logging in using the Private key we are assuming that user account is safe from bad actors and are going to allow sudo access without a password.</span></span>  

### <a name="adding-a-single-sudo-user-to-an-azure-vm"></a><span data-ttu-id="1830d-120">Aggiunta di un singolo utente sudo a una macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="1830d-120">Adding a single sudo user to an Azure VM</span></span>
<span data-ttu-id="1830d-121">Accedere alla VM di Azure usando le chiavi SSH.</span><span class="sxs-lookup"><span data-stu-id="1830d-121">Log in to the Azure VM using SSH keys.</span></span>  <span data-ttu-id="1830d-122">Se non è stato configurato l'accesso con chiave pubblica SSH, eseguire prima i passaggi descritti in [Uso dell'autenticazione con chiave pubblica con Azure](http://link.to/article).</span><span class="sxs-lookup"><span data-stu-id="1830d-122">If you have not setup SSH public key access, complete this article first [Using Public Key Authentication with Azure](http://link.to/article).</span></span>  

<span data-ttu-id="1830d-123">Il comando `useradd` esegue le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="1830d-123">The `useradd` command completes the following tasks:</span></span>

* <span data-ttu-id="1830d-124">creazione di un nuovo account utente</span><span class="sxs-lookup"><span data-stu-id="1830d-124">create a new user account</span></span>
* <span data-ttu-id="1830d-125">creazione di un nuovo gruppo di utenti con lo stesso nome</span><span class="sxs-lookup"><span data-stu-id="1830d-125">create a new user group with the same name</span></span>
* <span data-ttu-id="1830d-126">aggiunta di una voce vuota in `/etc/passwd`</span><span class="sxs-lookup"><span data-stu-id="1830d-126">add a blank entry to `/etc/passwd`</span></span>
* <span data-ttu-id="1830d-127">aggiunta di una voce vuota in `/etc/gpasswd`</span><span class="sxs-lookup"><span data-stu-id="1830d-127">add a blank entry to `/etc/gpasswd`</span></span>

<span data-ttu-id="1830d-128">Il flag della riga di comando `-G` aggiunge il nuovo account utente al gruppo Linux corretto assegnando al nuovo account utente i privilegi di escalation radice.</span><span class="sxs-lookup"><span data-stu-id="1830d-128">The `-G` command-line flag adds the new user account to the proper Linux group giving the new user account root escalation privileges.</span></span>

#### <a name="add-the-user"></a><span data-ttu-id="1830d-129">Aggiungere l'utente</span><span class="sxs-lookup"><span data-stu-id="1830d-129">Add the user</span></span>
```bash
# On RedHat family distros
sudo useradd -G wheel exampleUser

# On Debian family distros
sudo useradd -G sudo exampleUser
```

#### <a name="set-a-password"></a><span data-ttu-id="1830d-130">Impostare una password</span><span class="sxs-lookup"><span data-stu-id="1830d-130">Set a password</span></span>
<span data-ttu-id="1830d-131">Il comando `useradd` crea l'utente e aggiunge una voce in `/etc/passwd` e `/etc/gpasswd` ma non imposta effettivamente la password.</span><span class="sxs-lookup"><span data-stu-id="1830d-131">The `useradd` command creates the user and adds an entry to both `/etc/passwd` and `/etc/gpasswd` but does not actually set the password.</span></span>  <span data-ttu-id="1830d-132">La password viene aggiunta alla voce usando il comando `passwd` .</span><span class="sxs-lookup"><span data-stu-id="1830d-132">The password is added to the entry using the `passwd` command.</span></span>

```bash
sudo passwd exampleUser
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
```

<span data-ttu-id="1830d-133">Un utente con privilegi sudo è ora disponibile nel server.</span><span class="sxs-lookup"><span data-stu-id="1830d-133">We now have a user with sudo privileges on the server.</span></span>

### <a name="add-your-ssh-public-key-to-the-new-user-account"></a><span data-ttu-id="1830d-134">Aggiungere la chiave pubblica SSH nel nuovo account utente</span><span class="sxs-lookup"><span data-stu-id="1830d-134">Add your SSH Public Key to the new user account</span></span>
<span data-ttu-id="1830d-135">Nel computer usare il comando `ssh-copy-id` con la nuova password.</span><span class="sxs-lookup"><span data-stu-id="1830d-135">From your machine, use the `ssh-copy-id` command with the new password.</span></span>

```bash
ssh-copy-id -i ~/.ssh/id_rsa exampleuser@exampleserver
```

### <a name="using-visudo-to-allow-sudo-usage-without-a-password"></a><span data-ttu-id="1830d-136">Uso di visudo per consentire l'utilizzo di sudo senza password</span><span class="sxs-lookup"><span data-stu-id="1830d-136">Using visudo to allow sudo usage without a password</span></span>
<span data-ttu-id="1830d-137">L'uso di `visudo` per la modifica del file `/etc/sudoers` aggiunge alcuni livelli di protezione dalla modifica non corretta di questo importante file.</span><span class="sxs-lookup"><span data-stu-id="1830d-137">Using `visudo` to edit the `/etc/sudoers` file adds a few layers of protection against incorrectly modifying this important file.</span></span>  <span data-ttu-id="1830d-138">Dopo l'esecuzione di `visudo` il file `/etc/sudoers` viene bloccato per impedire che altri utenti apportino modifiche mentre viene modificato.</span><span class="sxs-lookup"><span data-stu-id="1830d-138">Upon executing `visudo`, the `/etc/sudoers` file is locked to ensure no other user can make changes while it is actively being edited.</span></span>  <span data-ttu-id="1830d-139">Quando si tenta di salvare o uscire, `visudo` verifica anche che il file `/etc/sudoers` non contenga errori, quindi non è possibile salvare un file sudo corrotto.</span><span class="sxs-lookup"><span data-stu-id="1830d-139">The `/etc/sudoers` file is also checked for mistakes by `visudo` when you attempt to save or exit so you cannot save a broken sudoers file.</span></span>

<span data-ttu-id="1830d-140">Gli utenti sono già inseriti nel gruppo predefinito corretto per l'accesso a sudo.</span><span class="sxs-lookup"><span data-stu-id="1830d-140">We already have users in the correct default group for sudo access.</span></span>  <span data-ttu-id="1830d-141">I gruppi vengono ora abilitati per l'uso di sudo senza password.</span><span class="sxs-lookup"><span data-stu-id="1830d-141">Now we are going to enable those groups to use sudo with no password.</span></span>

```bash
# Execute visudo as root to edit the /etc/sudoers file
visudo

# On RedHat family distros uncomment this line:
## Same thing without a password
# %wheel        ALL=(ALL)       NOPASSWD: ALL

# to this
## Same thing without a password
%wheel        ALL=(ALL)       NOPASSWD: ALL

# On Debian family distros change this line:
# Allow members of group sudo to execute any command
%sudo   ALL=(ALL:ALL) ALL

# to this
%sudo   ALL=(ALL) NOPASSWD:ALL
```

### <a name="verify-the-user-ssh-keys-and-sudo"></a><span data-ttu-id="1830d-142">Verificare l'utente, le chiavi SSH e sudo</span><span class="sxs-lookup"><span data-stu-id="1830d-142">Verify the user, ssh keys, and sudo</span></span>
```bash
# Verify the SSH keys & User account
ssh -i ~/.ssh/id_rsa exampleuser@exampleserver

# Verify sudo access
sudo top
```
