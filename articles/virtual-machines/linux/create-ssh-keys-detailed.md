---
title: Procedura dettagliata per creare una coppia di chiavi SSH per le macchine virtuali Linux in Azure | Microsoft Docs
description: Passaggi aggiuntivi per creare una coppia di chiavi SSH pubblica e privata per le VM Linux in Azure, con certificati specifici per i diversi casi d'uso.
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 6/28/2017
ms.author: danlep
ms.openlocfilehash: d4548c6f21d04effd57ea36e4fc0d15f77568903
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="detailed-walk-through-to-create-an-ssh-key-pair-and-additional-certificates-for-a-linux-vm-in-azure"></a><span data-ttu-id="ca226-103">Procedura dettagliata per creare una coppia di chiavi SSH e certificati aggiuntivi per una VM Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="ca226-103">Detailed walk through to create an SSH key pair and additional certificates for a Linux VM in Azure</span></span>
<span data-ttu-id="ca226-104">Con una coppia di chiavi SSH è possibile creare macchine virtuali in Azure che per impostazione predefinita usano le chiavi SSH per l'autenticazione, eliminando la necessità di password per l'accesso.</span><span class="sxs-lookup"><span data-stu-id="ca226-104">With an SSH key pair, you can create Virtual Machines on Azure that default to using SSH keys for authentication, eliminating the need for passwords to log in.</span></span> <span data-ttu-id="ca226-105">Le password sono intuibili e le macchine virtuali sono esposte a inesorabili tentativi di attacchi massicci per scoprire la password.</span><span class="sxs-lookup"><span data-stu-id="ca226-105">Passwords can be guessed, and open your VMs up to relentless brute force attempts to guess your password.</span></span> <span data-ttu-id="ca226-106">Le macchine virtuali create con l'interfaccia della riga di comando di Azure o i modelli di Resource Manager possono includere la chiave pubblica SSH durante la distribuzione, rimuovendo il passaggio della configurazione post-distribuzione di disattivazione degli account di accesso con password per SSH.</span><span class="sxs-lookup"><span data-stu-id="ca226-106">VMs created with the Azure CLI or Resource Manager templates can include your SSH public key as part of the deployment, removing a post deployment configuration step of disabling password logins for SSH.</span></span> <span data-ttu-id="ca226-107">Questo articolo illustra i passaggi dettagliati e offre esempi aggiuntivi per la generazione di certificati, ad esempio per l'uso con macchine virtuali di Linux.</span><span class="sxs-lookup"><span data-stu-id="ca226-107">This article provides detailed steps and additional examples of generating certificates, such as for use with Linux virtual machines.</span></span> <span data-ttu-id="ca226-108">Per creare rapidamente e usare una coppia di chiavi SSH, vedere [Come creare una coppia di chiavi SSH pubblica e privata per le macchine virtuali Linux in Azure](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="ca226-108">If you want to quickly create and use an SSH key pair, see [How to create an SSH public and private key pair for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

## <a name="understanding-ssh-keys"></a><span data-ttu-id="ca226-109">Informazioni sulle chiavi SSH</span><span class="sxs-lookup"><span data-stu-id="ca226-109">Understanding SSH keys</span></span>

<span data-ttu-id="ca226-110">L'uso di chiavi SSH pubbliche e private è il modo più semplice di accedere ai server Linux.</span><span class="sxs-lookup"><span data-stu-id="ca226-110">Using SSH public and private keys is the easiest way to log in to your Linux servers.</span></span> <span data-ttu-id="ca226-111">[crittografia a chiave pubblica](https://en.wikipedia.org/wiki/Public-key_cryptography) fornisce un modo molto più sicuro per accedere a una VM Linux o BSD in Azure rispetto all'uso di password, che possono essere molto più facilmente soggette ad attacchi di forza bruta.</span><span class="sxs-lookup"><span data-stu-id="ca226-111">[Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) provides a much more secure way to log in to your Linux or BSD VM in Azure than passwords, which can be brute-forced far more easily.</span></span>

<span data-ttu-id="ca226-112">La chiave pubblica può essere condivisa con chiunque, ma la chiave privata appartiene solo all'utente o all'infrastruttura di sicurezza locale.</span><span class="sxs-lookup"><span data-stu-id="ca226-112">Your public key can be shared with anyone; but only you (or your local security infrastructure) possess your private key.</span></span>  <span data-ttu-id="ca226-113">La chiave privata SSH deve essere protetta da una [password molto sicura](https://www.xkcd.com/936/) (origine: [xkcd.com](https://xkcd.com)).</span><span class="sxs-lookup"><span data-stu-id="ca226-113">The SSH private key should have a [very secure password](https://www.xkcd.com/936/) (source:[xkcd.com](https://xkcd.com)) to safeguard it.</span></span>  <span data-ttu-id="ca226-114">Questa password serve solo per accedere al file della chiave SSH privata e **non è** la password dell'account utente.</span><span class="sxs-lookup"><span data-stu-id="ca226-114">This password is just to access the private SSH key file and **is not** the user account password.</span></span>  <span data-ttu-id="ca226-115">Quando si aggiunge una password alla chiave SSH, la chiave privata viene crittografata usando AES a 128 bit, in modo che non sia possibile usarla senza la password per decrittografarla.</span><span class="sxs-lookup"><span data-stu-id="ca226-115">When you add a password to your SSH key, it encrypts the private key using 128-bit AES, so that the private key is useless without the password to decrypt it.</span></span>  <span data-ttu-id="ca226-116">Se un utente malintenzionato ruba una chiave privata priva di password, può usarla per accedere ai server che hanno la chiave pubblica corrispondente.</span><span class="sxs-lookup"><span data-stu-id="ca226-116">If an attacker stole your private key and that key did not have a password, they would be able to use that private key to log in to any servers that have the corresponding public key.</span></span>  <span data-ttu-id="ca226-117">Una chiave privata protetta da password non può essere usata da utenti malintenzionati e rappresenta un livello di sicurezza aggiuntivo per l'infrastruttura in Azure.</span><span class="sxs-lookup"><span data-stu-id="ca226-117">If a private key is password protected it cannot be used by that attacker, providing an additional layer of security for your infrastructure on Azure.</span></span>

<span data-ttu-id="ca226-118">Questo articolo crea una coppia di file di chiavi pubblica e privata RSA protocollo SSH versione 2 (definite anche chiavi "ssh-rsa"), consigliate per le distribuzioni con Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ca226-118">This article creates an SSH protocol version 2 RSA public and private key file pair (also referred to as "ssh-rsa" keys), which are recommended for deployments with Azure Resource Manager.</span></span> <span data-ttu-id="ca226-119">*ssh-rsa* sono necessarie nel [portale](https://portal.azure.com) per le distribuzioni sia classica che Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ca226-119">*ssh-rsa* keys are required on the [portal](https://portal.azure.com) for both classic and Resource Manager deployments.</span></span>

## <a name="ssh-keys-use-and-benefits"></a><span data-ttu-id="ca226-120">Uso e vantaggi delle chiavi SSH</span><span class="sxs-lookup"><span data-stu-id="ca226-120">SSH keys use and benefits</span></span>

<span data-ttu-id="ca226-121">Azure richiede almeno chiavi pubbliche e private in formato RSA protocollo SSH versione 2 a 2048 bit. Il file di chiave pubblica ha il formato di contenitore `.pub`.</span><span class="sxs-lookup"><span data-stu-id="ca226-121">Azure requires at least 2048-bit, SSH protocol version 2 RSA format public and private keys; the public key file has the `.pub` container format.</span></span> <span data-ttu-id="ca226-122">Per creare le chiavi, usare `ssh-keygen`, che presenta una serie di domande e quindi scrive una chiave privata e una pubblica corrispondente.</span><span class="sxs-lookup"><span data-stu-id="ca226-122">To create the keys use `ssh-keygen`, which asks a series of questions and then writes a private key and a matching public key.</span></span> <span data-ttu-id="ca226-123">Quando viene creata una VM di Azure, Azure copia la chiave pubblica nella cartella `~/.ssh/authorized_keys` sulla VM.</span><span class="sxs-lookup"><span data-stu-id="ca226-123">When an Azure VM is created, Azure copies the public key to the `~/.ssh/authorized_keys` folder on the VM.</span></span> <span data-ttu-id="ca226-124">Le chiavi SSH in `~/.ssh/authorized_keys` vengono usate per fare in modo che il client trovi la chiave privata corrispondente in una connessione di accesso SSH.</span><span class="sxs-lookup"><span data-stu-id="ca226-124">SSH keys in `~/.ssh/authorized_keys` are used to challenge the client to match the corresponding private key on an SSH login connection.</span></span>  <span data-ttu-id="ca226-125">Quando viene creata una macchina virtuale Linux di Azure usando le chiavi SSH per l'autenticazione, Azure configura il server SSHD per non consentire l'accesso con password, ma solo con le chiavi SSH.</span><span class="sxs-lookup"><span data-stu-id="ca226-125">When an Azure Linux VM is created using SSH keys for authentication, Azure configures the SSHD server to not allow password logins, only SSH keys.</span></span>  <span data-ttu-id="ca226-126">La creazione di macchine virtuali Linux in Azure con chiavi SSH consente di proteggere la distribuzione delle VM e di evitare l'esecuzione del passaggio di post-distribuzione tipico relativo alla disabilitazione delle password nel file **sshd_config**.</span><span class="sxs-lookup"><span data-stu-id="ca226-126">Therefore, by creating Azure Linux VMs with SSH keys, you can help secure the VM deployment and save yourself the typical post-deployment configuration step of disabling passwords in the **sshd_config** file.</span></span>

## <a name="using-ssh-keygen"></a><span data-ttu-id="ca226-127">Uso di ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="ca226-127">Using ssh-keygen</span></span>

<span data-ttu-id="ca226-128">Questo comando crea una coppia di chiavi SSH protette da password (crittografate) usando RSA a 2048 bit impostata come commento per identificarla facilmente.</span><span class="sxs-lookup"><span data-stu-id="ca226-128">This command creates a password secured (encrypted) SSH key pair using 2048-bit RSA and it is commented to easily identify it.</span></span>  

<span data-ttu-id="ca226-129">Per impostazione predefinita, le chiavi SSH vengono conservate nella directory `~/.ssh`.</span><span class="sxs-lookup"><span data-stu-id="ca226-129">SSH keys are by default kept in the `~/.ssh` directory.</span></span>  <span data-ttu-id="ca226-130">Se non si dispone di una directory `~/.ssh`, questa viene creata automaticamente dal comando `ssh-keygen` con le autorizzazioni corrette.</span><span class="sxs-lookup"><span data-stu-id="ca226-130">If you do not have a `~/.ssh` directory, the `ssh-keygen` command creates it for you with the correct permissions.</span></span>

```bash
ssh-keygen \
    -t rsa \
    -b 2048 \
    -C "azureuser@myserver" \
    -f ~/.ssh/id_rsa \
    -N mypassword
```

<span data-ttu-id="ca226-131">*Descrizione del comando*</span><span class="sxs-lookup"><span data-stu-id="ca226-131">*Command explained*</span></span>

<span data-ttu-id="ca226-132">`ssh-keygen`: programma usato per creare le chiavi.</span><span class="sxs-lookup"><span data-stu-id="ca226-132">`ssh-keygen` = the program used to create the keys</span></span>

<span data-ttu-id="ca226-133">`-t rsa` = tipo di chiave da creare, in formato RSA [wikipedia][parens at end](`https://en.wikipedia.org/wiki/RSA_(cryptosystem) `)
`-b 2048` = bit della chiave</span><span class="sxs-lookup"><span data-stu-id="ca226-133">`-t rsa` = type of key to create which is the RSA format [wikipedia][parens at end](`https://en.wikipedia.org/wiki/RSA_(cryptosystem) `)
`-b 2048` = bits of the key</span></span>

<span data-ttu-id="ca226-134">`-C "azureuser@myserver"`: commento aggiunto alla fine del file della chiave pubblica per identificarla facilmente.</span><span class="sxs-lookup"><span data-stu-id="ca226-134">`-C "azureuser@myserver"` = a comment appended to the end of the public key file to easily identify it.</span></span>  <span data-ttu-id="ca226-135">In genere come commento viene usato un indirizzo di posta elettronica, ma è possibile usare qualsiasi elemento, in base alle esigenze dell'infrastruttura.</span><span class="sxs-lookup"><span data-stu-id="ca226-135">Normally an email is used as the comment but you can use whatever works best for your infrastructure.</span></span>

## <a name="classic-deploy-using-asm"></a><span data-ttu-id="ca226-136">Distribuzione classica tramite `asm`</span><span class="sxs-lookup"><span data-stu-id="ca226-136">Classic deploy using `asm`</span></span>

<span data-ttu-id="ca226-137">Se si usa il modello di distribuzione classica (modalità `asm` nell'interfaccia della riga di comando), è possibile usare una chiave pubblica SSH-RSA o una chiave formattata RFC4716 in un contenitore PEM.</span><span class="sxs-lookup"><span data-stu-id="ca226-137">If you are using the classic deployment model (`asm` mode in the CLI), you can use an SSH-RSA public key or an RFC4716 formatted key in a pem container.</span></span>  <span data-ttu-id="ca226-138">La chiave pubblica SSH-RSA corrisponde a quella creata in precedenza in questo articolo tramite `ssh-keygen`.</span><span class="sxs-lookup"><span data-stu-id="ca226-138">The SSH-RSA public key is what was created earlier in this article using `ssh-keygen`.</span></span>

<span data-ttu-id="ca226-139">Per creare una chiave in formato RFC4716 da una chiave pubblica SSH esistente:</span><span class="sxs-lookup"><span data-stu-id="ca226-139">To create a RFC4716 formatted key from an existing SSH public key:</span></span>

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a><span data-ttu-id="ca226-140">Esempio di ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="ca226-140">Example of ssh-keygen</span></span>

```bash
ssh-keygen -t rsa -b 2048 -C "azureuser@myserver"
Generating public/private rsa key pair.
Enter file in which to save the key (/home/azureuser/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/azureuser/.ssh/id_rsa.
Your public key has been saved in /home/azureuser/.ssh/id_rsa.pub.
The key fingerprint is:
14:a3:cb:3e:78:ad:25:cc:55:e9:0c:08:e5:d1:a9:08 azureuser@myserver
The keys randomart image is:
+--[ RSA 2048]----+
|        o o. .   |
|      E. = .o    |
|      ..o...     |
|     . o....     |
|      o S =      |
|     . + O       |
|      + = =      |
|       o +       |
|        .        |
+-----------------+
```

<span data-ttu-id="ca226-141">File delle chiavi salvati:</span><span class="sxs-lookup"><span data-stu-id="ca226-141">Saved key files:</span></span>

`Enter file in which to save the key (/home/azureuser/.ssh/id_rsa): ~/.ssh/id_rsa`

<span data-ttu-id="ca226-142">Nome della coppia di chiavi per questo articolo.</span><span class="sxs-lookup"><span data-stu-id="ca226-142">The key pair name for this article.</span></span>  <span data-ttu-id="ca226-143">Una coppia di chiavi denominata **id_rsa** è disponibile per impostazione predefinita e alcuni strumenti potrebbero prevedere un file della chiave privata con nome **id_rsa**, quindi è opportuno averne uno.</span><span class="sxs-lookup"><span data-stu-id="ca226-143">Having a key pair named **id_rsa** is the default and some tools might expect the **id_rsa** private key file name so having one is a good idea.</span></span> <span data-ttu-id="ca226-144">La directory `~/.ssh/` è la posizione predefinita per le coppie di chiavi SSH e il file config SSH.</span><span class="sxs-lookup"><span data-stu-id="ca226-144">The directory `~/.ssh/` is the default location for SSH key pairs and the SSH config file.</span></span>  <span data-ttu-id="ca226-145">Se non viene specificato con un percorso completo, `ssh-keygen` crea le chiavi nella directory di lavoro corrente, non nel percorso `~/.ssh` predefinito.</span><span class="sxs-lookup"><span data-stu-id="ca226-145">If not specified with a full path, `ssh-keygen` creates the keys in the current working directory, not the default `~/.ssh`.</span></span>

<span data-ttu-id="ca226-146">Un listato della directory `~/.ssh` .</span><span class="sxs-lookup"><span data-stu-id="ca226-146">A listing of the `~/.ssh` directory.</span></span>

```bash
ls -al ~/.ssh
-rw------- 1 azureuser staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 azureuser staff   410 Aug 25 18:04 id_rsa.pub
```

<span data-ttu-id="ca226-147">Password della chiave:</span><span class="sxs-lookup"><span data-stu-id="ca226-147">Key Password:</span></span>

`Enter passphrase (empty for no passphrase):`

<span data-ttu-id="ca226-148">`ssh-keygen` indica una password per il file di chiave privata come "passphrase".</span><span class="sxs-lookup"><span data-stu-id="ca226-148">`ssh-keygen` refers to a password for the private key file as "a passphrase."</span></span>  <span data-ttu-id="ca226-149">È *vivamente* consigliabile aggiungere una password alla chiave privata.</span><span class="sxs-lookup"><span data-stu-id="ca226-149">It is *strongly* recommended to add a password to your private key.</span></span> <span data-ttu-id="ca226-150">Senza una password che protegge il file di chiave, chiunque abbia il file può usarlo per accedere a qualsiasi server che ha la chiave pubblica corrispondente.</span><span class="sxs-lookup"><span data-stu-id="ca226-150">Without a password protecting the key file, anyone with the file can use it to log in to any server that has the corresponding public key.</span></span> <span data-ttu-id="ca226-151">L'aggiunta di una password (passphrase) offre protezione nel caso in cui qualcuno riesca ad accedere al file della chiave privata, consentendo all'utente il tempo necessario per modificare le chiavi usate per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="ca226-151">Adding a password (passphrase) offers more protection in case someone is able to gain access to your private key file, given you time to change the keys used to authenticate you.</span></span>

## <a name="using-ssh-agent-to-store-your-private-key-password"></a><span data-ttu-id="ca226-152">Uso di ssh-agent per archiviare la password della chiave privata</span><span class="sxs-lookup"><span data-stu-id="ca226-152">Using ssh-agent to store your private key password</span></span>

<span data-ttu-id="ca226-153">Per evitare di digitare la password del file della chiave privata a ogni accesso SSH, è possibile usare `ssh-agent` per memorizzare nella cache la password del file della chiave privata.</span><span class="sxs-lookup"><span data-stu-id="ca226-153">To avoid typing your private key file password with every SSH login, you can use `ssh-agent` to cache your private key file password.</span></span> <span data-ttu-id="ca226-154">Se si usa un Mac, il portachiavi OSX archivia in modo sicuro le password delle chiavi private quando si richiama `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="ca226-154">If you are using a Mac, the OSX Keychain securely stores the private key passwords when you invoke `ssh-agent`.</span></span>

<span data-ttu-id="ca226-155">Verificare e usare ssh-agent e ssh-add per fornire informazioni al sistema SSH sui file delle chiavi, in modo che non sia necessario usare la passphrase in modo interattivo.</span><span class="sxs-lookup"><span data-stu-id="ca226-155">Verify and use ssh-agent and ssh-add to inform the SSH system about the key files so that the passphrase will not need to be used interactively.</span></span>

```bash
eval "$(ssh-agent -s)"
```

<span data-ttu-id="ca226-156">Ora aggiungere la chiave privata a `ssh-agent` usando il comando `ssh-add`.</span><span class="sxs-lookup"><span data-stu-id="ca226-156">Now add the private key to `ssh-agent` using the command `ssh-add`.</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

<span data-ttu-id="ca226-157">La password della chiave privata viene ora archiviata in `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="ca226-157">The private key password is now stored in `ssh-agent`.</span></span>

## <a name="using-ssh-copy-id-to-copy-the-key-to-an-existing-vm"></a><span data-ttu-id="ca226-158">Uso di `ssh-copy-id` per copiare la chiave in una VM esistente</span><span class="sxs-lookup"><span data-stu-id="ca226-158">Using `ssh-copy-id` to copy the key to an existing VM</span></span>
<span data-ttu-id="ca226-159">Se è già stata creata una macchina virtuale, è possibile installare la nuova chiave SSH pubblica nella VM Linux con:</span><span class="sxs-lookup"><span data-stu-id="ca226-159">If you have already created a VM you can install the new SSH public key to your Linux VM with:</span></span>

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a><span data-ttu-id="ca226-160">Creare e configurare un file config SSH</span><span class="sxs-lookup"><span data-stu-id="ca226-160">Create and configure an SSH config file</span></span>

<span data-ttu-id="ca226-161">È una procedura consigliata creare e configurare un file `~/.ssh/config` per velocizzare gli accessi e ottimizzare il comportamento del client SSH.</span><span class="sxs-lookup"><span data-stu-id="ca226-161">It is a recommended best practice to create and configure an `~/.ssh/config` file to speed up log ins and for optimizing your SSH client behavior.</span></span>

<span data-ttu-id="ca226-162">L'esempio seguente illustra una configurazione standard.</span><span class="sxs-lookup"><span data-stu-id="ca226-162">The following example shows a standard configuration.</span></span>

### <a name="create-the-file"></a><span data-ttu-id="ca226-163">Creare il file</span><span class="sxs-lookup"><span data-stu-id="ca226-163">Create the file</span></span>

```bash
touch ~/.ssh/config
```

### <a name="edit-the-file-to-add-the-new-ssh-configuration"></a><span data-ttu-id="ca226-164">Modificare il file aggiungendo la nuova configurazione SSH:</span><span class="sxs-lookup"><span data-stu-id="ca226-164">Edit the file to add the new SSH configuration:</span></span>

```bash
vim ~/.ssh/config
```

### <a name="example-sshconfig-file"></a><span data-ttu-id="ca226-165">File `~/.ssh/config` di esempio:</span><span class="sxs-lookup"><span data-stu-id="ca226-165">Example `~/.ssh/config` file:</span></span>

```bash
# Azure Keys
Host fedora22
  Hostname 102.160.203.241
  User ahmet
# ./Azure Keys
# Default Settings
Host *
  PubkeyAuthentication=yes
  IdentitiesOnly=yes
  ServerAliveInterval=60
  ServerAliveCountMax=30
  ControlMaster auto
  ControlPath ~/.ssh/SSHConnections/ssh-%r@%h:%p
  ControlPersist 4h
  IdentityFile ~/.ssh/id_rsa
```

<span data-ttu-id="ca226-166">Questo file config SSH include sezioni per ogni server, per consentire a ognuno di essi di avere una coppia di chiavi dedicata.</span><span class="sxs-lookup"><span data-stu-id="ca226-166">This SSH config gives you sections for each server to enable each to have its own dedicated key pair.</span></span> <span data-ttu-id="ca226-167">Le impostazioni predefinite (`Host *`) sono valide per tutti gli host che non corrispondono ad alcuno degli host specifici indicati sopra nel file config.</span><span class="sxs-lookup"><span data-stu-id="ca226-167">The default settings (`Host *`) are for any hosts that do not match any of the specific hosts higher up in the config file.</span></span>

### <a name="config-file-explained"></a><span data-ttu-id="ca226-168">Descrizione del file config</span><span class="sxs-lookup"><span data-stu-id="ca226-168">Config file explained</span></span>

<span data-ttu-id="ca226-169">`Host` : nome dell'host chiamato sul terminale.</span><span class="sxs-lookup"><span data-stu-id="ca226-169">`Host` = the name of the host being called on the terminal.</span></span>  <span data-ttu-id="ca226-170">`ssh fedora22` indica a `SSH` di usare i valori nel blocco di impostazioni con l'etichetta `Host fedora22`. NOTA: l'Host può essere qualsiasi etichetta logica per il proprio uso e non rappresenta il nome host effettivo di un server.</span><span class="sxs-lookup"><span data-stu-id="ca226-170">`ssh fedora22` tells `SSH` to use the values in the settings block labeled `Host fedora22`  NOTE: Host can be any label that is logical for your usage and does not represent the actual hostname of any server.</span></span>

<span data-ttu-id="ca226-171">`Hostname 102.160.203.241`: indirizzo IP o nome DNS del server a cui si accede.</span><span class="sxs-lookup"><span data-stu-id="ca226-171">`Hostname 102.160.203.241` = the IP address or DNS name for the server being accessed.</span></span>

<span data-ttu-id="ca226-172">`User ahmet` = account utente remoto da usare quando si accede al server.</span><span class="sxs-lookup"><span data-stu-id="ca226-172">`User ahmet` = the remote user account to use when logging in to the server.</span></span>

<span data-ttu-id="ca226-173">`PubKeyAuthentication yes`: indica a SSH che si vuole usare una chiave SSH per l'accesso.</span><span class="sxs-lookup"><span data-stu-id="ca226-173">`PubKeyAuthentication yes` = tells SSH you want to use an SSH key to log in.</span></span>

<span data-ttu-id="ca226-174">`IdentityFile /home/ahmet/.ssh/id_id_rsa`: chiave privata SSH e chiave pubblica corrispondente da usare per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="ca226-174">`IdentityFile /home/ahmet/.ssh/id_id_rsa` = the SSH private key and corresponding public key to use for authentication.</span></span>

## <a name="ssh-into-linux-without-a-password"></a><span data-ttu-id="ca226-175">Usare SSH per accedere a Linux senza password</span><span class="sxs-lookup"><span data-stu-id="ca226-175">SSH into Linux without a password</span></span>

<span data-ttu-id="ca226-176">Con una coppia di chiavi SSH e un file config SSH configurato è ora possibile accedere alla VM Linux in modo rapido e sicuro.</span><span class="sxs-lookup"><span data-stu-id="ca226-176">Now that you have an SSH key pair and a configured SSH config file, you are able to log in to your Linux VM quickly and securely.</span></span> <span data-ttu-id="ca226-177">La prima volta che si accede a un server con una chiave SSH, il comando richiede la passphrase per il file della chiave.</span><span class="sxs-lookup"><span data-stu-id="ca226-177">The first time you log in to a server using an SSH key the command prompts you for the passphrase for that key file.</span></span>

```bash
ssh fedora22
```

### <a name="command-explained"></a><span data-ttu-id="ca226-178">Descrizione del comando</span><span class="sxs-lookup"><span data-stu-id="ca226-178">Command explained</span></span>

<span data-ttu-id="ca226-179">Quando si esegue `ssh fedora22`, SSH trova e carica prima di tutto le impostazioni dal blocco `Host fedora22` e quindi carica tutte le impostazioni rimanenti dell'ultimo blocco `Host *`.</span><span class="sxs-lookup"><span data-stu-id="ca226-179">When `ssh fedora22` is executed SSH first locates and loads any settings from the `Host fedora22` block, and then loads all the remaining settings from the last block, `Host *`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ca226-180">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ca226-180">Next Steps</span></span>

<span data-ttu-id="ca226-181">Il prossimo passaggio consiste nel creare VM Linux di Azure usando la nuova chiave pubblica SSH.</span><span class="sxs-lookup"><span data-stu-id="ca226-181">Next up is to create Azure Linux VMs using the new SSH public key.</span></span>  <span data-ttu-id="ca226-182">Le VM di Azure create con una chiave pubblica SSH come account di accesso sono più protette rispetto alle VM create con il metodo di accesso predefinito basato su password.</span><span class="sxs-lookup"><span data-stu-id="ca226-182">Azure VMs that are created with an SSH public key as the login are better secured than VMs created with the default login method, passwords.</span></span>  <span data-ttu-id="ca226-183">Per impostazione predefinita, le VM di Azure create con le chiavi SSH vengono configurate con le password disabilitate, evitando tentativi di attacco basati su forza bruta per scoprire le password.</span><span class="sxs-lookup"><span data-stu-id="ca226-183">Azure VMs created using SSH keys are by default configured with passwords disabled, avoiding brute-forced guessing attempts.</span></span>

* [<span data-ttu-id="ca226-184">Creare una VM Linux protetta usando un modello di Azure</span><span class="sxs-lookup"><span data-stu-id="ca226-184">Create a secure Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="ca226-185">Creare una VM Linux protetta usando il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="ca226-185">Create a secure Linux VM using the Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="ca226-186">Creare una VM Linux protetta usando l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="ca226-186">Create a secure Linux VM using the Azure CLI</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
