---
title: aaaAdd tooa un utente Linux VM in Azure | Documenti Microsoft
description: Aggiungere un tooa utente Linux VM in Azure.
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
ms.openlocfilehash: eed050154adf0cbed2c168e7aa675bd3ded85fcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-user-tooan-azure-vm"></a><span data-ttu-id="5dc2e-103">Aggiungere un tooan utente macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="5dc2e-103">Add a user tooan Azure VM</span></span>
<span data-ttu-id="5dc2e-104">Una delle prime attività in qualsiasi nuova VM Linux di hello è toocreate un nuovo utente.</span><span class="sxs-lookup"><span data-stu-id="5dc2e-104">One of hello first tasks on any new Linux VM is toocreate a new user.</span></span>  <span data-ttu-id="5dc2e-105">In questo articolo è illustrata la creazione di un account utente di sudo, l'impostazione password hello, aggiunta di chiavi pubbliche SSH e infine utilizzare `visudo` sudo tooallow senza una password.</span><span class="sxs-lookup"><span data-stu-id="5dc2e-105">In this article, we walk through creating a sudo user account, setting hello password, adding SSH Public Keys, and finally use `visudo` tooallow sudo without a password.</span></span>

<span data-ttu-id="5dc2e-106">Prerequisiti: [un account Azure](https://azure.microsoft.com/pricing/free-trial/), [chiavi pubbliche e private SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), un gruppo di risorse di Azure e hello Azure CLI installato e passa in modalità di gestione risorse tooAzure utilizzando `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="5dc2e-106">Prerequisites are: [an Azure account](https://azure.microsoft.com/pricing/free-trial/), [SSH public and private keys](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), an Azure resource group, and hello Azure CLI installed and switched tooAzure Resource Manager mode using `azure config mode arm`.</span></span>

## <a name="quick-commands"></a><span data-ttu-id="5dc2e-107">Comandi rapidi</span><span class="sxs-lookup"><span data-stu-id="5dc2e-107">Quick Commands</span></span>
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

# Copy hello SSH Public Key toohello new user
ssh-copy-id -i ~/.ssh/id_rsa exampleuser@exampleserver

# Change sudoers tooallow no password
# Execute visudo as root tooedit hello /etc/sudoers file
visudo

# On RedHat family distros uncomment this line:
## Same thing without a password
# %wheel        ALL=(ALL)       NOPASSWD: ALL

# toothis
## Same thing without a password
%wheel        ALL=(ALL)       NOPASSWD: ALL

# On Debian family distros change this line:
# Allow members of group sudo tooexecute any command
%sudo   ALL=(ALL:ALL) ALL

# toothis
%sudo   ALL=(ALL) NOPASSWD:ALL

# Verify everything
# Verify hello SSH keys & User account
bill@slackware$ ssh -i ~/.ssh/id_rsa exampleuser@exampleserver

# Verify sudo access
sudo top
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="5dc2e-108">Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="5dc2e-108">Detailed Walkthrough</span></span>
### <a name="introduction"></a><span data-ttu-id="5dc2e-109">Introduzione</span><span class="sxs-lookup"><span data-stu-id="5dc2e-109">Introduction</span></span>
<span data-ttu-id="5dc2e-110">Una delle attività di primo e più comune di hello con un nuovo server è tooadd un account utente.</span><span class="sxs-lookup"><span data-stu-id="5dc2e-110">One of hello first and most common task with a new server is tooadd a user account.</span></span>  <span data-ttu-id="5dc2e-111">Account di accesso radice deve essere disabilitata e account radice hello stessa non deve essere utilizzato con i server Linux e solo sudo.</span><span class="sxs-lookup"><span data-stu-id="5dc2e-111">Root logins should be disabled and hello root account itself should not be used with your Linux server, only sudo.</span></span>  <span data-ttu-id="5dc2e-112">Concedere i privilegi utilizzando "Sudo" hello tooadminister modo corretto e utilizzare Linux di escalation dei blocchi una radice di utente.</span><span class="sxs-lookup"><span data-stu-id="5dc2e-112">Giving a user root escalation privileges using sudo it hello proper way tooadminister and use Linux.</span></span>

<span data-ttu-id="5dc2e-113">Comando hello `useradd` aggiungiamo toohello gli account utente Linux VM.</span><span class="sxs-lookup"><span data-stu-id="5dc2e-113">Using hello command `useradd` we are adding user accounts toohello Linux VM.</span></span>  <span data-ttu-id="5dc2e-114">L'esecuzione di `useradd` modifica `/etc/passwd`, `/etc/shadow`, `/etc/group` e `/etc/gshadow`.</span><span class="sxs-lookup"><span data-stu-id="5dc2e-114">Running `useradd` modifies `/etc/passwd`, `/etc/shadow`, `/etc/group`, and `/etc/gshadow`.</span></span>  <span data-ttu-id="5dc2e-115">Si sta aggiungendo un flag della riga di comando di toohello `useradd` comando tooalso aggiungere hello nuovo toohello sudo corretto gruppo di utenti in Linux.</span><span class="sxs-lookup"><span data-stu-id="5dc2e-115">We are adding a command-line flag toohello `useradd` command tooalso add hello new user toohello proper sudo group on Linux.</span></span>  <span data-ttu-id="5dc2e-116">Anche viaggi `useradd` viene creata una voce in `/etc/passwd` non viene nuovo account utente di hello una password.</span><span class="sxs-lookup"><span data-stu-id="5dc2e-116">Even thou `useradd` creates an entry into `/etc/passwd` it does not give hello new user account a password.</span></span>  <span data-ttu-id="5dc2e-117">Si sta creando una password iniziale per hello nuovo utente con il semplice hello `passwd` comando.</span><span class="sxs-lookup"><span data-stu-id="5dc2e-117">We are creating an initial password for hello new user using hello simple `passwd` command.</span></span>  <span data-ttu-id="5dc2e-118">ultimo passaggio Hello è toomodify hello sudo regole tooallow che i comandi tooexecute utente con privilegi sudo senza tooenter una password per ogni comando.</span><span class="sxs-lookup"><span data-stu-id="5dc2e-118">hello last step is toomodify hello sudo rules tooallow that user tooexecute commands with sudo privileges without having tooenter a password for every command.</span></span>  <span data-ttu-id="5dc2e-119">La registrazione con la chiave privata hello si suppone che l'account utente è protetta da cattivi attori e prevede l'accesso a sudo tooallow senza una password.</span><span class="sxs-lookup"><span data-stu-id="5dc2e-119">Logging in using hello Private key we are assuming that user account is safe from bad actors and are going tooallow sudo access without a password.</span></span>  

### <a name="adding-a-single-sudo-user-tooan-azure-vm"></a><span data-ttu-id="5dc2e-120">Aggiunta di un tooan utente sudo singola macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="5dc2e-120">Adding a single sudo user tooan Azure VM</span></span>
<span data-ttu-id="5dc2e-121">Accedi toohello macchina virtuale di Azure utilizzando le chiavi SSH.</span><span class="sxs-lookup"><span data-stu-id="5dc2e-121">Log in toohello Azure VM using SSH keys.</span></span>  <span data-ttu-id="5dc2e-122">Se non è stato configurato l'accesso con chiave pubblica SSH, eseguire prima i passaggi descritti in [Uso dell'autenticazione con chiave pubblica con Azure](http://link.to/article).</span><span class="sxs-lookup"><span data-stu-id="5dc2e-122">If you have not setup SSH public key access, complete this article first [Using Public Key Authentication with Azure](http://link.to/article).</span></span>  

<span data-ttu-id="5dc2e-123">Hello `useradd` hello seguenti attività di completamento del comando:</span><span class="sxs-lookup"><span data-stu-id="5dc2e-123">hello `useradd` command completes hello following tasks:</span></span>

* <span data-ttu-id="5dc2e-124">creazione di un nuovo account utente</span><span class="sxs-lookup"><span data-stu-id="5dc2e-124">create a new user account</span></span>
* <span data-ttu-id="5dc2e-125">creare un nuovo gruppo di utenti con hello stesso nome</span><span class="sxs-lookup"><span data-stu-id="5dc2e-125">create a new user group with hello same name</span></span>
* <span data-ttu-id="5dc2e-126">aggiungere una voce vuota troppo`/etc/passwd`</span><span class="sxs-lookup"><span data-stu-id="5dc2e-126">add a blank entry too`/etc/passwd`</span></span>
* <span data-ttu-id="5dc2e-127">aggiungere una voce vuota troppo`/etc/gpasswd`</span><span class="sxs-lookup"><span data-stu-id="5dc2e-127">add a blank entry too`/etc/gpasswd`</span></span>

<span data-ttu-id="5dc2e-128">Hello `-G` flag della riga di comando aggiunge hello nuovo utente account toohello corretto gruppo Linux concedere i privilegi di escalation dei blocchi di radice nuovo account utente di hello.</span><span class="sxs-lookup"><span data-stu-id="5dc2e-128">hello `-G` command-line flag adds hello new user account toohello proper Linux group giving hello new user account root escalation privileges.</span></span>

#### <a name="add-hello-user"></a><span data-ttu-id="5dc2e-129">Aggiungere l'utente hello</span><span class="sxs-lookup"><span data-stu-id="5dc2e-129">Add hello user</span></span>
```bash
# On RedHat family distros
sudo useradd -G wheel exampleUser

# On Debian family distros
sudo useradd -G sudo exampleUser
```

#### <a name="set-a-password"></a><span data-ttu-id="5dc2e-130">Impostare una password</span><span class="sxs-lookup"><span data-stu-id="5dc2e-130">Set a password</span></span>
<span data-ttu-id="5dc2e-131">Hello `useradd` comando Crea hello e aggiunge una voce tooboth `/etc/passwd` e `/etc/gpasswd` ma non vengono effettivamente impostate password hello.</span><span class="sxs-lookup"><span data-stu-id="5dc2e-131">hello `useradd` command creates hello user and adds an entry tooboth `/etc/passwd` and `/etc/gpasswd` but does not actually set hello password.</span></span>  <span data-ttu-id="5dc2e-132">Hello password viene aggiunta voce toohello utilizzando hello `passwd` comando.</span><span class="sxs-lookup"><span data-stu-id="5dc2e-132">hello password is added toohello entry using hello `passwd` command.</span></span>

```bash
sudo passwd exampleUser
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
```

<span data-ttu-id="5dc2e-133">Un utente con privilegi sudo è ora disponibile nel server di hello.</span><span class="sxs-lookup"><span data-stu-id="5dc2e-133">We now have a user with sudo privileges on hello server.</span></span>

### <a name="add-your-ssh-public-key-toohello-new-user-account"></a><span data-ttu-id="5dc2e-134">Aggiungere il chiave pubblica SSH toohello nuovo account utente</span><span class="sxs-lookup"><span data-stu-id="5dc2e-134">Add your SSH Public Key toohello new user account</span></span>
<span data-ttu-id="5dc2e-135">Dal computer, utilizzare hello `ssh-copy-id` comando con una nuova password hello.</span><span class="sxs-lookup"><span data-stu-id="5dc2e-135">From your machine, use hello `ssh-copy-id` command with hello new password.</span></span>

```bash
ssh-copy-id -i ~/.ssh/id_rsa exampleuser@exampleserver
```

### <a name="using-visudo-tooallow-sudo-usage-without-a-password"></a><span data-ttu-id="5dc2e-136">Utilizzo visudo tooallow sudo senza una password</span><span class="sxs-lookup"><span data-stu-id="5dc2e-136">Using visudo tooallow sudo usage without a password</span></span>
<span data-ttu-id="5dc2e-137">Utilizzando `visudo` tooedit hello `/etc/sudoers` file consente di aggiungere alcuni livelli di protezione per la modifica in modo non corretto di questo file importanti.</span><span class="sxs-lookup"><span data-stu-id="5dc2e-137">Using `visudo` tooedit hello `/etc/sudoers` file adds a few layers of protection against incorrectly modifying this important file.</span></span>  <span data-ttu-id="5dc2e-138">Durante l'esecuzione `visudo`, hello `/etc/sudoers` file è bloccato tooensure nessun altro utente può apportare modifiche mentre attivamente viene modificato.</span><span class="sxs-lookup"><span data-stu-id="5dc2e-138">Upon executing `visudo`, hello `/etc/sudoers` file is locked tooensure no other user can make changes while it is actively being edited.</span></span>  <span data-ttu-id="5dc2e-139">Hello `/etc/sudoers` file viene archiviato anche per individuare errori da `visudo` quando si tenta di toosave o uscire in modo non è possibile salvare un file di file interrotto.</span><span class="sxs-lookup"><span data-stu-id="5dc2e-139">hello `/etc/sudoers` file is also checked for mistakes by `visudo` when you attempt toosave or exit so you cannot save a broken sudoers file.</span></span>

<span data-ttu-id="5dc2e-140">Gli utenti è già presente nel gruppo di hello predefiniti corretti per l'accesso a sudo.</span><span class="sxs-lookup"><span data-stu-id="5dc2e-140">We already have users in hello correct default group for sudo access.</span></span>  <span data-ttu-id="5dc2e-141">A questo punto verrà tooenable tali sudo toouse gruppi senza password.</span><span class="sxs-lookup"><span data-stu-id="5dc2e-141">Now we are going tooenable those groups toouse sudo with no password.</span></span>

```bash
# Execute visudo as root tooedit hello /etc/sudoers file
visudo

# On RedHat family distros uncomment this line:
## Same thing without a password
# %wheel        ALL=(ALL)       NOPASSWD: ALL

# toothis
## Same thing without a password
%wheel        ALL=(ALL)       NOPASSWD: ALL

# On Debian family distros change this line:
# Allow members of group sudo tooexecute any command
%sudo   ALL=(ALL:ALL) ALL

# toothis
%sudo   ALL=(ALL) NOPASSWD:ALL
```

### <a name="verify-hello-user-ssh-keys-and-sudo"></a><span data-ttu-id="5dc2e-142">Verificare utente hello, ssh chiavi e sudo</span><span class="sxs-lookup"><span data-stu-id="5dc2e-142">Verify hello user, ssh keys, and sudo</span></span>
```bash
# Verify hello SSH keys & User account
ssh -i ~/.ssh/id_rsa exampleuser@exampleserver

# Verify sudo access
sudo top
```
