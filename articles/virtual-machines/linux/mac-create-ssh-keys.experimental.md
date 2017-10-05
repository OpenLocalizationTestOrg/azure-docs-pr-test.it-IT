---
title: Creare una coppia di chiavi SSH per le macchine virtuali Linux in Azure | Documentazione Microsoft
description: Creare in modo sicuro una coppia di chiavi SSH pubblica e privata per le macchine virtuali di Linux in Azure.
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: 
ms.assetid: 34ae9482-da3e-4b2d-9d0d-9d672aa42498
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/08/2017
ms.author: rasquill
ms.openlocfilehash: 19acd4efca7ef043f31b436b96f9129caee9591b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-ssh-public-and-private-key-pair-for-linux-vms"></a><span data-ttu-id="dd86d-103">Creare una coppia di chiavi SSH pubblica e privata per le macchine virtuali di Linux</span><span class="sxs-lookup"><span data-stu-id="dd86d-103">Create an SSH public and private key pair for Linux VMs</span></span>

<span data-ttu-id="dd86d-104">Questo articolo illustra come generare una coppia di file di chiavi pubblica e privata RSA protocollo SSH versione 2 da usare con le VM Linux.</span><span class="sxs-lookup"><span data-stu-id="dd86d-104">This article shows you how to generate an SSH protocol version 2 RSA public and private key file pair to use with Linux VMs.</span></span>  <span data-ttu-id="dd86d-105">Con una coppia di chiavi SSH è possibile creare macchine virtuali in Azure che per impostazione predefinita usano le chiavi SSH per l'autenticazione, eliminando la necessità di password per l'accesso.</span><span class="sxs-lookup"><span data-stu-id="dd86d-105">With an SSH key pair, you can create Virtual Machines on Azure that default to using SSH keys for authentication, eliminating the need for passwords to log in.</span></span>  <span data-ttu-id="dd86d-106">Le password sono intuibili e le macchine virtuali sono esposte a inesorabili tentativi di attacchi massicci per scoprire la password.</span><span class="sxs-lookup"><span data-stu-id="dd86d-106">Passwords can be guessed, and open your VMs up to relentless brute force attempts to guess your password.</span></span> <span data-ttu-id="dd86d-107">Le macchine virtuali create con i modelli di Azure o con `azure-cli` possono includere la chiave pubblica SSH durante la distribuzione, rimuovendo il passaggio della configurazione post-distribuzione di disattivazione degli account di accesso con password per SSH.</span><span class="sxs-lookup"><span data-stu-id="dd86d-107">VMs created with Azure Templates or the `azure-cli` can include your SSH public key as part of the deployment, removing a post deployment configuration step of disabling password logins for SSH.</span></span>

## <a name="quick-commands"></a><span data-ttu-id="dd86d-108">Comandi rapidi</span><span class="sxs-lookup"><span data-stu-id="dd86d-108">Quick Commands</span></span>

<span data-ttu-id="dd86d-109">Eseguire i comandi seguenti da un bash shell, sostituendo gli esempi con le proprie scelte.</span><span class="sxs-lookup"><span data-stu-id="dd86d-109">Run the following commands from a Bash shell, replacing the examples with your own choices.</span></span>

<span data-ttu-id="dd86d-110">Per impostazione predefinita, il file di chiave pubblica SSH viene creato in `~/.ssh/id_rsa.pub`.</span><span class="sxs-lookup"><span data-stu-id="dd86d-110">Your SSH public key file is by default created at `~/.ssh/id_rsa.pub`.</span></span> <span data-ttu-id="dd86d-111">Quando viene richiesto di usare il comando seguente, è consigliabile creare una "passphrase" per proteggere la chiave privata.</span><span class="sxs-lookup"><span data-stu-id="dd86d-111">When prompted using the following command, you should create a "passphrase" to secure your private key.</span></span> <span data-ttu-id="dd86d-112">La passphrase è una password usata per crittografare la chiave privata.</span><span class="sxs-lookup"><span data-stu-id="dd86d-112">(The passphrase is a password used to encrypt your private key.)</span></span>

```bash
ssh-keygen -t rsa -b 2048 
```

<span data-ttu-id="dd86d-113">Aggiungere la chiave appena creata per `ssh-agent`:</span><span class="sxs-lookup"><span data-stu-id="dd86d-113">Add the newly created key to `ssh-agent`:</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

> [!IMPORTANT] 
> <span data-ttu-id="dd86d-114">I comandi precedenti funzionano nei sistemi operativi di Linux di quasi tutte le distribuzioni, ma non necessariamente in contenitori, perché l'ambiente può essere sottoposto a vincoli radicali.</span><span class="sxs-lookup"><span data-stu-id="dd86d-114">The above commands work on Linux operating systems of almost all distributions, but do not necessarily work in containers, as the environment can be radically constrained.</span></span> 

## <a name="detailed-walkthrough"></a><span data-ttu-id="dd86d-115">Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="dd86d-115">Detailed Walkthrough</span></span>

<span data-ttu-id="dd86d-116">L'uso di chiavi SSH pubbliche e private è il modo più semplice di accedere ai server Linux.</span><span class="sxs-lookup"><span data-stu-id="dd86d-116">Using SSH public and private keys is the easiest way to log in to your Linux servers.</span></span> <span data-ttu-id="dd86d-117">[crittografia a chiave pubblica](https://en.wikipedia.org/wiki/Public-key_cryptography) fornisce un modo molto più sicuro per accedere a una VM Linux o BSD in Azure rispetto all'uso di password, che possono essere molto più facilmente soggette ad attacchi di forza bruta.</span><span class="sxs-lookup"><span data-stu-id="dd86d-117">[Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) provides a much more secure way to log in to your Linux or BSD VM in Azure than passwords, which can be brute-forced far more easily.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dd86d-118">La chiave pubblica può essere condivisa con chiunque, ma la chiave privata appartiene solo all'utente o all'infrastruttura di sicurezza locale.</span><span class="sxs-lookup"><span data-stu-id="dd86d-118">Your public key can be shared with anyone; but only you (or your local security infrastructure) possess your private key.</span></span>  <span data-ttu-id="dd86d-119">La chiave privata SSH deve essere protetta da una [password molto sicura](https://www.xkcd.com/936/) (origine: [xkcd.com](https://xkcd.com)).</span><span class="sxs-lookup"><span data-stu-id="dd86d-119">The SSH private key should have a [very secure password](https://www.xkcd.com/936/) (source:[xkcd.com](https://xkcd.com)) to safeguard it.</span></span>  <span data-ttu-id="dd86d-120">Questa password serve solo per accedere alla chiave SSH privata e **non è** la password dell'account utente.</span><span class="sxs-lookup"><span data-stu-id="dd86d-120">This password is just to access the private SSH key and **is not** the user account password.</span></span>  <span data-ttu-id="dd86d-121">Quando si aggiunge una password alla chiave SSH, la chiave privata viene crittografata usando AES a 128 bit, in modo che non sia possibile usarla senza la password per decrittografarla.</span><span class="sxs-lookup"><span data-stu-id="dd86d-121">When you add a password to your SSH key, it encrypts the private key using 128-bit AES, so that the private key is useless without the password to decrypt it.</span></span>  <span data-ttu-id="dd86d-122">Se un utente malintenzionato ruba una chiave privata priva di password, può usarla per accedere ai server che hanno la chiave pubblica corrispondente.</span><span class="sxs-lookup"><span data-stu-id="dd86d-122">If an attacker stole your private key and that key did not have a password, they would be able to use that private key to log in to any servers that have the corresponding public key.</span></span>  <span data-ttu-id="dd86d-123">Una chiave privata protetta da password non può essere usata da utenti malintenzionati e rappresenta un livello di sicurezza aggiuntivo per l'infrastruttura in Azure.</span><span class="sxs-lookup"><span data-stu-id="dd86d-123">If a private key is password protected it cannot be used by that attacker, providing an additional layer of security for your infrastructure on Azure.</span></span>

<span data-ttu-id="dd86d-124">Questo articolo consente di creare file di chiave pubblica e privata RSA protocollo SSH versione 2, consigliati per le distribuzioni in Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="dd86d-124">This article creates SSH protocol version 2 RSA public and private key files, which are recommended for deployments on the Resource Manager.</span></span>  <span data-ttu-id="dd86d-125">*ssh-rsa* sono necessarie nel [portale](https://portal.azure.com) per le distribuzioni sia classica che Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="dd86d-125">*ssh-rsa* keys are required on the [portal](https://portal.azure.com) for both classic and Resource Manager deployments.</span></span>

## <a name="disable-ssh-passwords-by-using-ssh-keys"></a><span data-ttu-id="dd86d-126">Disabilitare le password SSH usando le chiavi SSH</span><span class="sxs-lookup"><span data-stu-id="dd86d-126">Disable SSH passwords by using SSH keys</span></span>

<span data-ttu-id="dd86d-127">Azure richiede chiavi pubbliche e private nel formato ssh-rsa almeno a 2048 bit.</span><span class="sxs-lookup"><span data-stu-id="dd86d-127">Azure requires at least 2048-bit, ssh-rsa format public and private keys.</span></span> <span data-ttu-id="dd86d-128">Per creare le chiavi, usare `ssh-keygen`, che presenta una serie di domande e quindi scrive una chiave privata e una pubblica corrispondente.</span><span class="sxs-lookup"><span data-stu-id="dd86d-128">To create the keys use `ssh-keygen`, which asks a series of questions and then writes a private key and a matching public key.</span></span> <span data-ttu-id="dd86d-129">Quando viene creata una VM di Azure, la chiave pubblica viene copiata in `~/.ssh/authorized_keys`.</span><span class="sxs-lookup"><span data-stu-id="dd86d-129">When an Azure VM is created, the public key is copied to `~/.ssh/authorized_keys`.</span></span>  <span data-ttu-id="dd86d-130">Le chiavi SSH in `~/.ssh/authorized_keys` vengono usate per fare in modo che il client trovi la chiave privata corrispondente in una connessione di accesso SSH.</span><span class="sxs-lookup"><span data-stu-id="dd86d-130">SSH keys in `~/.ssh/authorized_keys` are used to challenge the client to match the corresponding private key on an SSH login connection.</span></span>  <span data-ttu-id="dd86d-131">Quando viene creata una macchina virtuale Linux di Azure usando le chiavi SSH per l'autenticazione, Azure configura il server SSHD per non consentire l'accesso con password, ma solo con le chiavi SSH.</span><span class="sxs-lookup"><span data-stu-id="dd86d-131">When an Azure Linux VM is created using SSH keys for authentication, Azure configures the SSHD server to not allow password logins, only SSH keys.</span></span>  <span data-ttu-id="dd86d-132">La creazione di macchine virtuali Linux in Azure con chiavi SSH consente di proteggere la distribuzione delle VM e di evitare l'esecuzione del passaggio di post-distribuzione tipico relativo alla disabilitazione delle password nel file di configurazione sshd_config.</span><span class="sxs-lookup"><span data-stu-id="dd86d-132">Therefore, by creating Azure Linux VMs with SSH keys, you can help secure the VM deployment and save yourself the typical post-deployment configuration step of disabling passwords in the sshd_config config file.</span></span>

## <a name="using-ssh-keygen"></a><span data-ttu-id="dd86d-133">Uso di ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="dd86d-133">Using ssh-keygen</span></span>

<span data-ttu-id="dd86d-134">Questo comando crea una coppia di chiavi SSH protette da password (crittografate) usando RSA a 2048 bit impostata come commento per identificarla facilmente.</span><span class="sxs-lookup"><span data-stu-id="dd86d-134">This command creates a password secured (encrypted) SSH key pair using 2048-bit RSA and it is commented to easily identify it.</span></span>  

<span data-ttu-id="dd86d-135">Per impostazione predefinita, le chiavi SSH vengono conservate nella directory `~/.ssh`.</span><span class="sxs-lookup"><span data-stu-id="dd86d-135">SSH keys are by default kept in the `~/.ssh` directory.</span></span>  <span data-ttu-id="dd86d-136">Se non si dispone di una directory `~/.ssh`, questa viene creata automaticamente dal comando `ssh-keygen` con le autorizzazioni corrette.</span><span class="sxs-lookup"><span data-stu-id="dd86d-136">If you do not have a `~/.ssh` directory, the `ssh-keygen` command creates it for you with the correct permissions.</span></span>

```bash
ssh-keygen \
-t rsa \
-b 2048 
```

<span data-ttu-id="dd86d-137">*Descrizione del comando*</span><span class="sxs-lookup"><span data-stu-id="dd86d-137">*Command explained*</span></span>

<span data-ttu-id="dd86d-138">`ssh-keygen`: programma usato per creare le chiavi.</span><span class="sxs-lookup"><span data-stu-id="dd86d-138">`ssh-keygen` = the program used to create the keys</span></span>

<span data-ttu-id="dd86d-139">`-t rsa` = tipo di chiave da creare, corrispondente al formato RSA [wikipedia](https://en.wikipedia.org/wiki/RSA_(cryptosystem)</span><span class="sxs-lookup"><span data-stu-id="dd86d-139">`-t rsa` = type of key to create which is the RSA format [wikipedia](https://en.wikipedia.org/wiki/RSA_(cryptosystem)</span></span>

<span data-ttu-id="dd86d-140">`-b 2048`: bit della chiave.</span><span class="sxs-lookup"><span data-stu-id="dd86d-140">`-b 2048` = bits of the key</span></span>


## <a name="classic-portal-and-x509-certs"></a><span data-ttu-id="dd86d-141">Portale classico e certificati X.509</span><span class="sxs-lookup"><span data-stu-id="dd86d-141">Classic portal and X.509 certs</span></span>

<span data-ttu-id="dd86d-142">Se si usa il [portale classico](https://manage.windowsazure.com/) di Azure, sono necessari certificati X.509 per le chiavi SSH.</span><span class="sxs-lookup"><span data-stu-id="dd86d-142">If you are using the Azure [classic portal](https://manage.windowsazure.com/), it requires X.509 certs for the SSH keys.</span></span>  <span data-ttu-id="dd86d-143">Non sono consentite altre chiavi pubbliche SSH, *devono* essere certificati X.509.</span><span class="sxs-lookup"><span data-stu-id="dd86d-143">No other types of SSH public keys are allowed, they *must* be X.509 certs.</span></span>

<span data-ttu-id="dd86d-144">Per creare un certificato X.509 dalla chiave privata SSH-RSA:</span><span class="sxs-lookup"><span data-stu-id="dd86d-144">To create an X.509 cert from your existing SSH-RSA private key:</span></span>

```bash
openssl req -x509 \
-key ~/.ssh/id_rsa \
-nodes \
-days 365 \
-newkey rsa:2048 \
-out ~/.ssh/id_rsa.pem
```

## <a name="classic-deploy-using-asm"></a><span data-ttu-id="dd86d-145">Distribuzione classica tramite `asm`</span><span class="sxs-lookup"><span data-stu-id="dd86d-145">Classic deploy using `asm`</span></span>

<span data-ttu-id="dd86d-146">Se si usa il modello di distribuzione classica (comando `asm` dell'interfaccia della riga di comando di gestione dei servizi di Azure), è possibile usare una chiave pubblica SSH-RSA o una chiave formattata RFC4716 in un contenitore **PEM**.</span><span class="sxs-lookup"><span data-stu-id="dd86d-146">If you are using the classic deploy model (Azure service management CLI `asm`), you can use an SSH-RSA public key or an RFC4716 formatted key in a **.pem** container.</span></span>  <span data-ttu-id="dd86d-147">La chiave pubblica SSH-RSA corrisponde a quella creata in precedenza in questo articolo tramite `ssh-keygen`.</span><span class="sxs-lookup"><span data-stu-id="dd86d-147">The SSH-RSA public key is what was created earlier in this article using `ssh-keygen`.</span></span>

<span data-ttu-id="dd86d-148">Per creare una chiave in formato RFC4716 da una chiave pubblica SSH esistente:</span><span class="sxs-lookup"><span data-stu-id="dd86d-148">To create a RFC4716 formatted key from an existing SSH public key:</span></span>

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a><span data-ttu-id="dd86d-149">Esempio di ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="dd86d-149">Example of ssh-keygen</span></span>

```bash
ssh-keygen -t rsa -b 2048 -C "ahmet@myserver"
Generating public/private rsa key pair.
Enter file in which to save the key (/home/ahmet/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/ahmet/.ssh/id_rsa.
Your public key has been saved in /home/ahmet/.ssh/id_rsa.pub.
The key fingerprint is:
14:a3:cb:3e:78:ad:25:cc:55:e9:0c:08:e5:d1:a9:08 ahmet@myserver
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

<span data-ttu-id="dd86d-150">File delle chiavi salvati:</span><span class="sxs-lookup"><span data-stu-id="dd86d-150">Saved key files:</span></span>

`Enter file in which to save the key (/home/ahmet/.ssh/id_rsa): ~/.ssh/id_rsa`

<span data-ttu-id="dd86d-151">Nome della coppia di chiavi per questo articolo.</span><span class="sxs-lookup"><span data-stu-id="dd86d-151">The key pair name for this article.</span></span>  <span data-ttu-id="dd86d-152">Una coppia di chiavi denominata **id_rsa** è disponibile per impostazione predefinita e alcuni strumenti potrebbero prevedere un file della chiave privata con nome **id_rsa**, quindi è opportuno averne uno.</span><span class="sxs-lookup"><span data-stu-id="dd86d-152">Having a key pair named **id_rsa** is the default and some tools might expect the **id_rsa** private key file name so having one is a good idea.</span></span> <span data-ttu-id="dd86d-153">La directory `~/.ssh/` è la posizione predefinita per le coppie di chiavi SSH e il file config SSH.</span><span class="sxs-lookup"><span data-stu-id="dd86d-153">The directory `~/.ssh/` is the default location for SSH key pairs and the SSH config file.</span></span>  <span data-ttu-id="dd86d-154">Se non viene specificato con un percorso completo, `ssh-keygen` creerà le chiavi nella directory di lavoro corrente, non nel percorso `~/.ssh` predefinito.</span><span class="sxs-lookup"><span data-stu-id="dd86d-154">If not specified with a full path, `ssh-keygen` will create the keys in the current working directory, not the default `~/.ssh`.</span></span>

<span data-ttu-id="dd86d-155">Un listato della directory `~/.ssh` .</span><span class="sxs-lookup"><span data-stu-id="dd86d-155">A listing of the `~/.ssh` directory.</span></span>

```bash
ls -al ~/.ssh
-rw------- 1 ahmet staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 ahmet staff   410 Aug 25 18:04 rsa.pub
```

<span data-ttu-id="dd86d-156">Password della chiave:</span><span class="sxs-lookup"><span data-stu-id="dd86d-156">Key Password:</span></span>

`Enter passphrase (empty for no passphrase):`

<span data-ttu-id="dd86d-157">`ssh-keygen` indica una password usata per crittografare la chiave privata come "passphrase".</span><span class="sxs-lookup"><span data-stu-id="dd86d-157">`ssh-keygen` refers to a password used to encrypt the private key as "a passphrase."</span></span>  <span data-ttu-id="dd86d-158">È *vivamente* consigliabile aggiungere una passphrase alle coppie di chiavi.</span><span class="sxs-lookup"><span data-stu-id="dd86d-158">It is *strongly* recommended to add a passphrase to your key pairs.</span></span> <span data-ttu-id="dd86d-159">Senza una passphrase che protegge la chiave privata, chiunque abbia il file della chiave può usarlo per accedere a qualsiasi server che ha la chiave pubblica corrispondente.</span><span class="sxs-lookup"><span data-stu-id="dd86d-159">Without a passphrase protecting the private key, anyone with the key file can use it to log in to any server that has the corresponding public key.</span></span> <span data-ttu-id="dd86d-160">L'aggiunta di una passphrase offre protezione nel caso in cui qualcuno riesca ad accedere al file della chiave privata, consentendo all'utente il tempo necessario per modificare le chiavi usate per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="dd86d-160">Adding a passphrase offers more protection in case someone is able to gain access to your private key file, giving you time to change the keys used to authenticate you.</span></span>

## <a name="using-ssh-agent-to-store-your-private-key-password"></a><span data-ttu-id="dd86d-161">Uso di ssh-agent per archiviare la password della chiave privata</span><span class="sxs-lookup"><span data-stu-id="dd86d-161">Using ssh-agent to store your private key password</span></span>

<span data-ttu-id="dd86d-162">Per evitare di digitare la passphrase del file della chiave privata a ogni accesso SSH, è possibile usare `ssh-agent` per memorizzare nella cache la password del file della chiave privata.</span><span class="sxs-lookup"><span data-stu-id="dd86d-162">To avoid typing your private key file passphrase with every SSH login, you can use `ssh-agent` to cache your private key file password.</span></span> <span data-ttu-id="dd86d-163">Se si usa un Mac, il portachiavi OSX archivia in modo sicuro le password delle chiavi private quando si richiama `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="dd86d-163">If you are using a Mac, the OSX Keychain securely stores the private key passwords when you invoke `ssh-agent`.</span></span>

<span data-ttu-id="dd86d-164">Verificare e usare `ssh-agent` e `ssh-add` per fornire informazioni al sistema SSH sui file delle chiavi, in modo che non sia necessario usare la passphrase in modo interattivo.</span><span class="sxs-lookup"><span data-stu-id="dd86d-164">Verify and use `ssh-agent` and `ssh-add` to inform the SSH system about the key files so that the passphrase will not need to be used interactively.</span></span>

```bash
eval "$(ssh-agent -s)"
```

<span data-ttu-id="dd86d-165">Ora aggiungere la chiave privata a `ssh-agent` usando il comando `ssh-add`.</span><span class="sxs-lookup"><span data-stu-id="dd86d-165">Now add the private key to `ssh-agent` using the command `ssh-add`.</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

<span data-ttu-id="dd86d-166">La password della chiave privata viene ora archiviata in `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="dd86d-166">The private key password is now stored in `ssh-agent`.</span></span>

## <a name="using-ssh-copy-id-to-install-the-new-key"></a><span data-ttu-id="dd86d-167">Uso di `ssh-copy-id` per installare la nuova chiave</span><span class="sxs-lookup"><span data-stu-id="dd86d-167">Using `ssh-copy-id` to install the new key</span></span>
<span data-ttu-id="dd86d-168">Se si è già creata una VM, è possibile installare la nuova chiave pubblica SSH nella VM Linux con il comando seguente, sostituendo il nome utente della VM e l'indirizzo del server con i propri valori:</span><span class="sxs-lookup"><span data-stu-id="dd86d-168">If you have already created a VM you can install the new SSH public key to your Linux VM with the following command, replacing the VM username and the server address with your own values:</span></span>

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a><span data-ttu-id="dd86d-169">Creare e configurare un file config SSH</span><span class="sxs-lookup"><span data-stu-id="dd86d-169">Create and configure an SSH config file</span></span>

<span data-ttu-id="dd86d-170">È una procedura consigliata creare e configurare un file `~/.ssh/config` per velocizzare gli accessi e ottimizzare il comportamento del client SSH.</span><span class="sxs-lookup"><span data-stu-id="dd86d-170">It is a best practice to create and configure an `~/.ssh/config` file to speed up log ins and for optimizing your SSH client behavior.</span></span>

<span data-ttu-id="dd86d-171">L'esempio seguente illustra una configurazione standard.</span><span class="sxs-lookup"><span data-stu-id="dd86d-171">The following example shows a standard configuration.</span></span>

### <a name="create-the-file"></a><span data-ttu-id="dd86d-172">Creare il file</span><span class="sxs-lookup"><span data-stu-id="dd86d-172">Create the file</span></span>

```bash
touch ~/.ssh/config
```

### <a name="edit-the-file-to-add-the-new-ssh-configuration"></a><span data-ttu-id="dd86d-173">Modificare il file aggiungendo la nuova configurazione SSH:</span><span class="sxs-lookup"><span data-stu-id="dd86d-173">Edit the file to add the new SSH configuration:</span></span>

```bash
vim ~/.ssh/config
```

### <a name="example-sshconfig-file"></a><span data-ttu-id="dd86d-174">File `~/.ssh/config` di esempio:</span><span class="sxs-lookup"><span data-stu-id="dd86d-174">Example `~/.ssh/config` file:</span></span>

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

<span data-ttu-id="dd86d-175">Questo file config SSH include sezioni per ogni server, per consentire a ognuno di essi di avere una coppia di chiavi dedicata.</span><span class="sxs-lookup"><span data-stu-id="dd86d-175">This SSH config gives you sections for each server to enable each to have its own dedicated key pair.</span></span> <span data-ttu-id="dd86d-176">Le impostazioni predefinite (`Host *`) sono valide per tutti gli host che non corrispondono ad alcuno degli host specifici indicati sopra nel file config.</span><span class="sxs-lookup"><span data-stu-id="dd86d-176">The default settings (`Host *`) are for any hosts that do not match any of the specific hosts higher up in the config file.</span></span>

### <a name="config-file-explained"></a><span data-ttu-id="dd86d-177">Descrizione del file config</span><span class="sxs-lookup"><span data-stu-id="dd86d-177">Config file explained</span></span>

<span data-ttu-id="dd86d-178">`Host` : nome dell'host chiamato sul terminale.</span><span class="sxs-lookup"><span data-stu-id="dd86d-178">`Host` = the name of the host being called on the terminal.</span></span>  <span data-ttu-id="dd86d-179">`ssh fedora22` indica a `SSH` di usare i valori nel blocco di impostazioni con l'etichetta `Host fedora22`. NOTA: l'Host può essere qualsiasi etichetta logica per il proprio uso e non rappresenta il nome host effettivo di un server.</span><span class="sxs-lookup"><span data-stu-id="dd86d-179">`ssh fedora22` tells `SSH` to use the values in the settings block labeled `Host fedora22`  NOTE: Host can be any label that is logical for your usage and does not represent the actual hostname of any server.</span></span>

<span data-ttu-id="dd86d-180">`Hostname 102.160.203.241`: indirizzo IP o nome DNS del server a cui si accede.</span><span class="sxs-lookup"><span data-stu-id="dd86d-180">`Hostname 102.160.203.241` = the IP address or DNS name for the server being accessed.</span></span>

<span data-ttu-id="dd86d-181">`User ahmet` = account utente remoto da usare quando si accede al server.</span><span class="sxs-lookup"><span data-stu-id="dd86d-181">`User ahmet` = the remote user account to use when logging in to the server.</span></span>

<span data-ttu-id="dd86d-182">`PubKeyAuthentication yes`: indica a SSH che si vuole usare una chiave SSH per l'accesso.</span><span class="sxs-lookup"><span data-stu-id="dd86d-182">`PubKeyAuthentication yes` = tells SSH you want to use an SSH key to log in.</span></span>

<span data-ttu-id="dd86d-183">`IdentityFile /home/ahmet/.ssh/id_id_rsa`: chiave privata SSH e chiave pubblica corrispondente da usare per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="dd86d-183">`IdentityFile /home/ahmet/.ssh/id_id_rsa` = the SSH private key and corresponding public key to use for authentication.</span></span>

## <a name="ssh-into-linux-without-a-password"></a><span data-ttu-id="dd86d-184">Usare SSH per accedere a Linux senza password</span><span class="sxs-lookup"><span data-stu-id="dd86d-184">SSH into Linux without a password</span></span>

<span data-ttu-id="dd86d-185">Con una coppia di chiavi SSH e un file config SSH configurato è ora possibile accedere alla VM Linux in modo rapido e sicuro.</span><span class="sxs-lookup"><span data-stu-id="dd86d-185">Now that you have an SSH key pair and a configured SSH config file, you are able to log in to your Linux VM quickly and securely.</span></span> <span data-ttu-id="dd86d-186">La prima volta che si accede a un server con una chiave SSH, il comando richiede la passphrase per il file della chiave.</span><span class="sxs-lookup"><span data-stu-id="dd86d-186">The first time you log in to a server using an SSH key the command prompts you for the passphrase for that key file.</span></span>

```bash
ssh fedora22
```

### <a name="command-explained"></a><span data-ttu-id="dd86d-187">Descrizione del comando</span><span class="sxs-lookup"><span data-stu-id="dd86d-187">Command explained</span></span>

<span data-ttu-id="dd86d-188">Quando si esegue `ssh fedora22`, SSH trova e carica prima di tutto le impostazioni dal blocco `Host fedora22` e quindi carica tutte le impostazioni rimanenti dell'ultimo blocco `Host *`.</span><span class="sxs-lookup"><span data-stu-id="dd86d-188">When `ssh fedora22` is executed SSH first locates and loads any settings from the `Host fedora22` block, and then loads all the remaining settings from the last block, `Host *`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dd86d-189">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dd86d-189">Next Steps</span></span>

<span data-ttu-id="dd86d-190">Il prossimo passaggio consiste nel creare VM Linux di Azure usando la nuova chiave pubblica SSH.</span><span class="sxs-lookup"><span data-stu-id="dd86d-190">Next up is to create Azure Linux VMs using the new SSH public key.</span></span>  <span data-ttu-id="dd86d-191">Le VM di Azure create con una chiave pubblica SSH come account di accesso sono più protette rispetto alle VM create con il metodo di accesso predefinito basato su password.</span><span class="sxs-lookup"><span data-stu-id="dd86d-191">Azure VMs that are created with an SSH public key as the login are better secured than VMs created with the default login method, passwords.</span></span>  <span data-ttu-id="dd86d-192">Per impostazione predefinita, le VM di Azure create con le chiavi SSH vengono configurate con le password disabilitate, evitando tentativi di attacco basati su forza bruta per scoprire le password.</span><span class="sxs-lookup"><span data-stu-id="dd86d-192">Azure VMs created using SSH keys are by default configured with passwords disabled, avoiding brute-forced guessing attempts.</span></span> <span data-ttu-id="dd86d-193">Se serve maggiore assistenza durante la creazione della coppia di chiavi SSH o sono necessari certificati aggiuntivi, ad esempio per l'uso con il portale classico, vedere [Detailed steps to create SSH key pairs and certificates](create-ssh-keys-detailed.md) (Procedura dettagliata per creare coppie di chiavi SSH e certificati).</span><span class="sxs-lookup"><span data-stu-id="dd86d-193">If you need more assistance in creating your SSH key pair or require additional certificates, such as for use with the classic portal, see [Detailed steps to create SSH key pairs and certificates](create-ssh-keys-detailed.md).</span></span>

* [<span data-ttu-id="dd86d-194">Creare una VM Linux protetta usando un modello di Azure</span><span class="sxs-lookup"><span data-stu-id="dd86d-194">Create a secure Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="dd86d-195">Creare una VM Linux protetta usando il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="dd86d-195">Create a secure Linux VM using the Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="dd86d-196">Creare una VM Linux protetta usando l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="dd86d-196">Create a secure Linux VM using the Azure CLI</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
