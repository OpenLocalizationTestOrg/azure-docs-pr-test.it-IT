---
title: coppia di chiavi aaaDetailed passaggi toocreate un SSH per le macchine virtuali Linux in Azure | Documenti Microsoft
description: Informazioni su ulteriori passaggi toocreate una coppia chiave SSH pubblica e privata per le macchine virtuali Linux in Azure, insieme a certificati specifici per diversi casi d'uso.
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
ms.openlocfilehash: 9ac52ef4dc87e73b9c07ccc323adc955829e2014
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="detailed-walk-through-toocreate-an-ssh-key-pair-and-additional-certificates-for-a-linux-vm-in-azure"></a><span data-ttu-id="d633f-103">Procedura dettagliata toocreate una coppia di chiavi SSH e certificati aggiuntivi per una VM Linux di Azure</span><span class="sxs-lookup"><span data-stu-id="d633f-103">Detailed walk through toocreate an SSH key pair and additional certificates for a Linux VM in Azure</span></span>
<span data-ttu-id="d633f-104">Con una coppia di chiavi SSH, è possibile creare macchine virtuali in Azure che utilizza l'impostazione predefinita le chiavi SSH toousing per l'autenticazione, eliminando la necessità hello per le password toolog in.</span><span class="sxs-lookup"><span data-stu-id="d633f-104">With an SSH key pair, you can create Virtual Machines on Azure that default toousing SSH keys for authentication, eliminating hello need for passwords toolog in.</span></span> <span data-ttu-id="d633f-105">Le password possono essere individuate e aprire le macchine virtuali di tooguess tentativi di attacchi di forza bruta toorelentless la password.</span><span class="sxs-lookup"><span data-stu-id="d633f-105">Passwords can be guessed, and open your VMs up toorelentless brute force attempts tooguess your password.</span></span> <span data-ttu-id="d633f-106">Macchine virtuali create con i modelli di hello CLI di Azure o di gestione delle risorse possono includere la chiave pubblica SSH come parte della distribuzione di hello, la rimozione di un passaggio di configurazione di distribuzione post della disabilitazione dell'account di accesso di password per SSH.</span><span class="sxs-lookup"><span data-stu-id="d633f-106">VMs created with hello Azure CLI or Resource Manager templates can include your SSH public key as part of hello deployment, removing a post deployment configuration step of disabling password logins for SSH.</span></span> <span data-ttu-id="d633f-107">Questo articolo illustra i passaggi dettagliati e offre esempi aggiuntivi per la generazione di certificati, ad esempio per l'uso con macchine virtuali di Linux.</span><span class="sxs-lookup"><span data-stu-id="d633f-107">This article provides detailed steps and additional examples of generating certificates, such as for use with Linux virtual machines.</span></span> <span data-ttu-id="d633f-108">Se si desidera tooquickly creare e utilizzare una coppia di chiavi SSH, vedere [come coppia di toocreate chiave SSH pubblica e privata per le macchine virtuali Linux in Azure](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="d633f-108">If you want tooquickly create and use an SSH key pair, see [How toocreate an SSH public and private key pair for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

## <a name="understanding-ssh-keys"></a><span data-ttu-id="d633f-109">Informazioni sulle chiavi SSH</span><span class="sxs-lookup"><span data-stu-id="d633f-109">Understanding SSH keys</span></span>

<span data-ttu-id="d633f-110">Utilizzo delle chiavi pubbliche e private SSH è toolog modo più semplice di hello in server Linux tooyour.</span><span class="sxs-lookup"><span data-stu-id="d633f-110">Using SSH public and private keys is hello easiest way toolog in tooyour Linux servers.</span></span> <span data-ttu-id="d633f-111">[Crittografia a chiave pubblica](https://en.wikipedia.org/wiki/Public-key_cryptography) fornisce un toolog modo molto più sicuro in tooyour Linux o BSD VM in Azure rispetto alle password, che possono essere colpita molto più semplice.</span><span class="sxs-lookup"><span data-stu-id="d633f-111">[Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) provides a much more secure way toolog in tooyour Linux or BSD VM in Azure than passwords, which can be brute-forced far more easily.</span></span>

<span data-ttu-id="d633f-112">La chiave pubblica può essere condivisa con chiunque, ma la chiave privata appartiene solo all'utente o all'infrastruttura di sicurezza locale.</span><span class="sxs-lookup"><span data-stu-id="d633f-112">Your public key can be shared with anyone; but only you (or your local security infrastructure) possess your private key.</span></span>  <span data-ttu-id="d633f-113">la chiave privata SSH Hello deve avere un [password molto sicura](https://www.xkcd.com/936/) (origine:[xkcd.com](https://xkcd.com)) toosafeguard è.</span><span class="sxs-lookup"><span data-stu-id="d633f-113">hello SSH private key should have a [very secure password](https://www.xkcd.com/936/) (source:[xkcd.com](https://xkcd.com)) toosafeguard it.</span></span>  <span data-ttu-id="d633f-114">Questa password è semplicemente tooaccess hello SSH file di chiave privata e **non** password dell'account utente hello.</span><span class="sxs-lookup"><span data-stu-id="d633f-114">This password is just tooaccess hello private SSH key file and **is not** hello user account password.</span></span>  <span data-ttu-id="d633f-115">Quando si aggiunge una chiave SSH tooyour, crittografa la chiave privata di hello tramite AES a 128 bit, in modo che hello chiave privata è inutile senza toodecrypt password hello è.</span><span class="sxs-lookup"><span data-stu-id="d633f-115">When you add a password tooyour SSH key, it encrypts hello private key using 128-bit AES, so that hello private key is useless without hello password toodecrypt it.</span></span>  <span data-ttu-id="d633f-116">Se un utente malintenzionato rubare la chiave privata e tale chiave non dispone di una password, saranno in grado di toouse che private key toolog nel server tooany che dispongono di chiave pubblica corrispondente hello.</span><span class="sxs-lookup"><span data-stu-id="d633f-116">If an attacker stole your private key and that key did not have a password, they would be able toouse that private key toolog in tooany servers that have hello corresponding public key.</span></span>  <span data-ttu-id="d633f-117">Una chiave privata protetta da password non può essere usata da utenti malintenzionati e rappresenta un livello di sicurezza aggiuntivo per l'infrastruttura in Azure.</span><span class="sxs-lookup"><span data-stu-id="d633f-117">If a private key is password protected it cannot be used by that attacker, providing an additional layer of security for your infrastructure on Azure.</span></span>

<span data-ttu-id="d633f-118">In questo articolo viene creata una versione del protocollo SSH 2 coppie di file di chiave pubblica e privata RSA (anche noto tooas "ssh-rsa" chiavi), che sono consigliate per le distribuzioni con Gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="d633f-118">This article creates an SSH protocol version 2 RSA public and private key file pair (also referred tooas "ssh-rsa" keys), which are recommended for deployments with Azure Resource Manager.</span></span> <span data-ttu-id="d633f-119">*SSH-rsa* le chiavi sono necessarie in hello [portale](https://portal.azure.com) per classica e le distribuzioni di gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="d633f-119">*ssh-rsa* keys are required on hello [portal](https://portal.azure.com) for both classic and Resource Manager deployments.</span></span>

## <a name="ssh-keys-use-and-benefits"></a><span data-ttu-id="d633f-120">Uso e vantaggi delle chiavi SSH</span><span class="sxs-lookup"><span data-stu-id="d633f-120">SSH keys use and benefits</span></span>

<span data-ttu-id="d633f-121">Azure richiede almeno 2048 bit, versione 2 RSA formato chiavi pubbliche e private; del protocollo SSH file di chiave pubblica Hello è hello `.pub` formato contenitore.</span><span class="sxs-lookup"><span data-stu-id="d633f-121">Azure requires at least 2048-bit, SSH protocol version 2 RSA format public and private keys; hello public key file has hello `.pub` container format.</span></span> <span data-ttu-id="d633f-122">Utilizzare tasti di hello toocreate `ssh-keygen`, che richiede una serie di domande e quindi scrive una chiave privata e una chiave pubblica corrispondente.</span><span class="sxs-lookup"><span data-stu-id="d633f-122">toocreate hello keys use `ssh-keygen`, which asks a series of questions and then writes a private key and a matching public key.</span></span> <span data-ttu-id="d633f-123">Quando viene creata una macchina virtuale di Azure, Azure copie hello toohello chiave pubblica `~/.ssh/authorized_keys` cartella hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d633f-123">When an Azure VM is created, Azure copies hello public key toohello `~/.ssh/authorized_keys` folder on hello VM.</span></span> <span data-ttu-id="d633f-124">Le chiavi SSH in `~/.ssh/authorized_keys` vengono utilizzati toochallenge hello toomatch hello corrispondente chiave privata del client su una connessione di accesso SSH.</span><span class="sxs-lookup"><span data-stu-id="d633f-124">SSH keys in `~/.ssh/authorized_keys` are used toochallenge hello client toomatch hello corresponding private key on an SSH login connection.</span></span>  <span data-ttu-id="d633f-125">Quando una macchina virtuale Linux di Azure viene creata utilizzando le chiavi SSH per l'autenticazione, Azure Configura hello SSHD toonot server consente l'accesso con password, solo le chiavi SSH.</span><span class="sxs-lookup"><span data-stu-id="d633f-125">When an Azure Linux VM is created using SSH keys for authentication, Azure configures hello SSHD server toonot allow password logins, only SSH keys.</span></span>  <span data-ttu-id="d633f-126">Di conseguenza, mediante la creazione di macchine virtuali Linux di Azure con le chiavi SSH, consentono di proteggere la distribuzione di macchine Virtuali hello e risparmiare passaggio di configurazione post-distribuzione tipica hello di disabilitazione di password in hello **sshd_config** file.</span><span class="sxs-lookup"><span data-stu-id="d633f-126">Therefore, by creating Azure Linux VMs with SSH keys, you can help secure hello VM deployment and save yourself hello typical post-deployment configuration step of disabling passwords in hello **sshd_config** file.</span></span>

## <a name="using-ssh-keygen"></a><span data-ttu-id="d633f-127">Uso di ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="d633f-127">Using ssh-keygen</span></span>

<span data-ttu-id="d633f-128">Questo comando crea una password protetta (crittografato) coppia di chiavi SSH tramite RSA a 2048 bit e si è impostata come commento tooeasily identificarlo.</span><span class="sxs-lookup"><span data-stu-id="d633f-128">This command creates a password secured (encrypted) SSH key pair using 2048-bit RSA and it is commented tooeasily identify it.</span></span>  

<span data-ttu-id="d633f-129">SSH chiavi per impostazione predefinita vengono mantenuta in hello `~/.ssh` directory.</span><span class="sxs-lookup"><span data-stu-id="d633f-129">SSH keys are by default kept in hello `~/.ssh` directory.</span></span>  <span data-ttu-id="d633f-130">Se non è un `~/.ssh` directory, hello `ssh-keygen` comando crea automaticamente con hello delle autorizzazioni corrette.</span><span class="sxs-lookup"><span data-stu-id="d633f-130">If you do not have a `~/.ssh` directory, hello `ssh-keygen` command creates it for you with hello correct permissions.</span></span>

```bash
ssh-keygen \
    -t rsa \
    -b 2048 \
    -C "azureuser@myserver" \
    -f ~/.ssh/id_rsa \
    -N mypassword
```

<span data-ttu-id="d633f-131">*Descrizione del comando*</span><span class="sxs-lookup"><span data-stu-id="d633f-131">*Command explained*</span></span>

<span data-ttu-id="d633f-132">`ssh-keygen`= hello programma utilizzato toocreate hello chiavi</span><span class="sxs-lookup"><span data-stu-id="d633f-132">`ssh-keygen` = hello program used toocreate hello keys</span></span>

<span data-ttu-id="d633f-133">`-t rsa`tipo di chiave toocreate hello RSA formato [wikipedia] =[parens alla fine](`https://en.wikipedia.org/wiki/RSA_(cryptosystem) `) 
 `-b 2048` = bit della chiave hello</span><span class="sxs-lookup"><span data-stu-id="d633f-133">`-t rsa` = type of key toocreate which is hello RSA format [wikipedia][parens at end](`https://en.wikipedia.org/wiki/RSA_(cryptosystem) `)
`-b 2048` = bits of hello key</span></span>

<span data-ttu-id="d633f-134">`-C "azureuser@myserver"`= un commento aggiunto toohello fine tooeasily file di chiave pubblica hello identificarlo.</span><span class="sxs-lookup"><span data-stu-id="d633f-134">`-C "azureuser@myserver"` = a comment appended toohello end of hello public key file tooeasily identify it.</span></span>  <span data-ttu-id="d633f-135">In genere un messaggio di posta elettronica viene utilizzato come commento hello ma è possibile utilizzare qualsiasi più adatto per l'infrastruttura.</span><span class="sxs-lookup"><span data-stu-id="d633f-135">Normally an email is used as hello comment but you can use whatever works best for your infrastructure.</span></span>

## <a name="classic-deploy-using-asm"></a><span data-ttu-id="d633f-136">Distribuzione classica tramite `asm`</span><span class="sxs-lookup"><span data-stu-id="d633f-136">Classic deploy using `asm`</span></span>

<span data-ttu-id="d633f-137">Se si utilizza il modello di distribuzione classica hello (`asm` modalità hello CLI), è possibile utilizzare una chiave pubblica SSH-RSA o formattato un RFC4716 chiave in un contenitore pem.</span><span class="sxs-lookup"><span data-stu-id="d633f-137">If you are using hello classic deployment model (`asm` mode in hello CLI), you can use an SSH-RSA public key or an RFC4716 formatted key in a pem container.</span></span>  <span data-ttu-id="d633f-138">chiave pubblica SSH-RSA Hello è ciò che è stato creato in precedenza in questo articolo utilizzando `ssh-keygen`.</span><span class="sxs-lookup"><span data-stu-id="d633f-138">hello SSH-RSA public key is what was created earlier in this article using `ssh-keygen`.</span></span>

<span data-ttu-id="d633f-139">toocreate un RFC4716 formato della chiave da una chiave pubblica SSH esistente:</span><span class="sxs-lookup"><span data-stu-id="d633f-139">toocreate a RFC4716 formatted key from an existing SSH public key:</span></span>

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a><span data-ttu-id="d633f-140">Esempio di ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="d633f-140">Example of ssh-keygen</span></span>

```bash
ssh-keygen -t rsa -b 2048 -C "azureuser@myserver"
Generating public/private rsa key pair.
Enter file in which toosave hello key (/home/azureuser/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/azureuser/.ssh/id_rsa.
Your public key has been saved in /home/azureuser/.ssh/id_rsa.pub.
hello key fingerprint is:
14:a3:cb:3e:78:ad:25:cc:55:e9:0c:08:e5:d1:a9:08 azureuser@myserver
hello keys randomart image is:
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

<span data-ttu-id="d633f-141">File delle chiavi salvati:</span><span class="sxs-lookup"><span data-stu-id="d633f-141">Saved key files:</span></span>

`Enter file in which toosave hello key (/home/azureuser/.ssh/id_rsa): ~/.ssh/id_rsa`

<span data-ttu-id="d633f-142">nome della coppia chiave Hello per questo articolo.</span><span class="sxs-lookup"><span data-stu-id="d633f-142">hello key pair name for this article.</span></span>  <span data-ttu-id="d633f-143">Con una coppia di chiavi denominata **id_rsa** hello predefinito e alcuni strumenti prevedibile hello **id_rsa** nome di file di chiave privata in modo che uno è una buona idea.</span><span class="sxs-lookup"><span data-stu-id="d633f-143">Having a key pair named **id_rsa** is hello default and some tools might expect hello **id_rsa** private key file name so having one is a good idea.</span></span> <span data-ttu-id="d633f-144">directory Hello `~/.ssh/` è il percorso predefinito hello per le coppie di chiavi SSH e file di configurazione di hello SSH.</span><span class="sxs-lookup"><span data-stu-id="d633f-144">hello directory `~/.ssh/` is hello default location for SSH key pairs and hello SSH config file.</span></span>  <span data-ttu-id="d633f-145">Se non è specificato con un percorso completo, `ssh-keygen` crea chiavi hello in hello directory di lavoro corrente, non il valore predefinito hello `~/.ssh`.</span><span class="sxs-lookup"><span data-stu-id="d633f-145">If not specified with a full path, `ssh-keygen` creates hello keys in hello current working directory, not hello default `~/.ssh`.</span></span>

<span data-ttu-id="d633f-146">Un elenco di hello `~/.ssh` directory.</span><span class="sxs-lookup"><span data-stu-id="d633f-146">A listing of hello `~/.ssh` directory.</span></span>

```bash
ls -al ~/.ssh
-rw------- 1 azureuser staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 azureuser staff   410 Aug 25 18:04 id_rsa.pub
```

<span data-ttu-id="d633f-147">Password della chiave:</span><span class="sxs-lookup"><span data-stu-id="d633f-147">Key Password:</span></span>

`Enter passphrase (empty for no passphrase):`

<span data-ttu-id="d633f-148">`ssh-keygen`fa riferimento tooa password per il file di chiave privata di hello come "una passphrase."</span><span class="sxs-lookup"><span data-stu-id="d633f-148">`ssh-keygen` refers tooa password for hello private key file as "a passphrase."</span></span>  <span data-ttu-id="d633f-149">È *fortemente* consigliato tooadd una chiave privata tooyour di password.</span><span class="sxs-lookup"><span data-stu-id="d633f-149">It is *strongly* recommended tooadd a password tooyour private key.</span></span> <span data-ttu-id="d633f-150">Senza un password protezione hello file di chiave, tutti gli utenti con file hello usarlo toolog tooany server dotato di chiave pubblica corrispondente hello.</span><span class="sxs-lookup"><span data-stu-id="d633f-150">Without a password protecting hello key file, anyone with hello file can use it toolog in tooany server that has hello corresponding public key.</span></span> <span data-ttu-id="d633f-151">Aggiunta di una password (passphrase) offre ulteriore protezione, nel caso in cui un utente è in grado di toogain accesso tooyour file di chiave privata, riceve chiavi hello toochange utilizzato tooauthenticate è.</span><span class="sxs-lookup"><span data-stu-id="d633f-151">Adding a password (passphrase) offers more protection in case someone is able toogain access tooyour private key file, given you time toochange hello keys used tooauthenticate you.</span></span>

## <a name="using-ssh-agent-toostore-your-private-key-password"></a><span data-ttu-id="d633f-152">Utilizzo di ssh agente toostore la password della chiave privata</span><span class="sxs-lookup"><span data-stu-id="d633f-152">Using ssh-agent toostore your private key password</span></span>

<span data-ttu-id="d633f-153">tooavoid digitare la password del file di chiave privata con ogni account di accesso SSH, è possibile utilizzare `ssh-agent` toocache la password del file di chiave privata.</span><span class="sxs-lookup"><span data-stu-id="d633f-153">tooavoid typing your private key file password with every SSH login, you can use `ssh-agent` toocache your private key file password.</span></span> <span data-ttu-id="d633f-154">Se si utilizza un computer Mac, hello OSX portachiavi Archivia password chiave privata hello in modo sicuro quando si richiama `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="d633f-154">If you are using a Mac, hello OSX Keychain securely stores hello private key passwords when you invoke `ssh-agent`.</span></span>

<span data-ttu-id="d633f-155">Verificare e utilizzare ssh agente ssh-Aggiungi tooinform hello SSH sistema sui file di chiave hello in modo che la passphrase hello non sarà necessario toobe utilizzati in modo interattivo.</span><span class="sxs-lookup"><span data-stu-id="d633f-155">Verify and use ssh-agent and ssh-add tooinform hello SSH system about hello key files so that hello passphrase will not need toobe used interactively.</span></span>

```bash
eval "$(ssh-agent -s)"
```

<span data-ttu-id="d633f-156">A questo punto aggiungere la chiave privata di hello troppo`ssh-agent` comando hello `ssh-add`.</span><span class="sxs-lookup"><span data-stu-id="d633f-156">Now add hello private key too`ssh-agent` using hello command `ssh-add`.</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

<span data-ttu-id="d633f-157">password della chiave privata Hello sono ora archiviate in `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="d633f-157">hello private key password is now stored in `ssh-agent`.</span></span>

## <a name="using-ssh-copy-id-toocopy-hello-key-tooan-existing-vm"></a><span data-ttu-id="d633f-158">Utilizzando `ssh-copy-id` toocopy hello tooan chiave macchina virtuale esistente</span><span class="sxs-lookup"><span data-stu-id="d633f-158">Using `ssh-copy-id` toocopy hello key tooan existing VM</span></span>
<span data-ttu-id="d633f-159">Se è stato già creato una macchina virtuale è possibile installare hello nuovo SSH pubblica chiave tooyour VM Linux con:</span><span class="sxs-lookup"><span data-stu-id="d633f-159">If you have already created a VM you can install hello new SSH public key tooyour Linux VM with:</span></span>

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a><span data-ttu-id="d633f-160">Creare e configurare un file config SSH</span><span class="sxs-lookup"><span data-stu-id="d633f-160">Create and configure an SSH config file</span></span>

<span data-ttu-id="d633f-161">È un consigliato toocreate prassi migliori e configurare un `~/.ssh/config` toospeed file di log aggiuntivi e per l'ottimizzazione del comportamento del client SSH.</span><span class="sxs-lookup"><span data-stu-id="d633f-161">It is a recommended best practice toocreate and configure an `~/.ssh/config` file toospeed up log ins and for optimizing your SSH client behavior.</span></span>

<span data-ttu-id="d633f-162">Hello di esempio seguente viene illustrata una configurazione standard.</span><span class="sxs-lookup"><span data-stu-id="d633f-162">hello following example shows a standard configuration.</span></span>

### <a name="create-hello-file"></a><span data-ttu-id="d633f-163">Creare file hello</span><span class="sxs-lookup"><span data-stu-id="d633f-163">Create hello file</span></span>

```bash
touch ~/.ssh/config
```

### <a name="edit-hello-file-tooadd-hello-new-ssh-configuration"></a><span data-ttu-id="d633f-164">Modificare hello file tooadd hello nuova configurazione SSH:</span><span class="sxs-lookup"><span data-stu-id="d633f-164">Edit hello file tooadd hello new SSH configuration:</span></span>

```bash
vim ~/.ssh/config
```

### <a name="example-sshconfig-file"></a><span data-ttu-id="d633f-165">File `~/.ssh/config` di esempio:</span><span class="sxs-lookup"><span data-stu-id="d633f-165">Example `~/.ssh/config` file:</span></span>

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

<span data-ttu-id="d633f-166">In questo modo di configurazione SSH sezioni per ogni server tooenable ogni toohave propria dedicata coppia di chiavi.</span><span class="sxs-lookup"><span data-stu-id="d633f-166">This SSH config gives you sections for each server tooenable each toohave its own dedicated key pair.</span></span> <span data-ttu-id="d633f-167">le impostazioni predefinite di Hello (`Host *`) sono per tutti gli host che non corrispondono a uno degli host hello specifico livello più alto nel file di configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="d633f-167">hello default settings (`Host *`) are for any hosts that do not match any of hello specific hosts higher up in hello config file.</span></span>

### <a name="config-file-explained"></a><span data-ttu-id="d633f-168">Descrizione del file config</span><span class="sxs-lookup"><span data-stu-id="d633f-168">Config file explained</span></span>

<span data-ttu-id="d633f-169">`Host`= nome hello dell'host di hello viene chiamato il metodo hello terminal.</span><span class="sxs-lookup"><span data-stu-id="d633f-169">`Host` = hello name of hello host being called on hello terminal.</span></span>  <span data-ttu-id="d633f-170">`ssh fedora22`indica `SSH` valori hello toouse in blocco settings hello etichettata `Host fedora22` Nota: Host può essere qualsiasi etichetta logico per l'utilizzo e non rappresenta hello nome host effettivo di qualsiasi server.</span><span class="sxs-lookup"><span data-stu-id="d633f-170">`ssh fedora22` tells `SSH` toouse hello values in hello settings block labeled `Host fedora22`  NOTE: Host can be any label that is logical for your usage and does not represent hello actual hostname of any server.</span></span>

<span data-ttu-id="d633f-171">`Hostname 102.160.203.241`= indirizzo hello o un nome DNS per il server di hello cui si accede.</span><span class="sxs-lookup"><span data-stu-id="d633f-171">`Hostname 102.160.203.241` = hello IP address or DNS name for hello server being accessed.</span></span>

<span data-ttu-id="d633f-172">`User ahmet`= toouse di account utente remoto hello durante l'accesso toohello server.</span><span class="sxs-lookup"><span data-stu-id="d633f-172">`User ahmet` = hello remote user account toouse when logging in toohello server.</span></span>

<span data-ttu-id="d633f-173">`PubKeyAuthentication yes`= indica SSH desiderato toouse un toolog chiave SSH.</span><span class="sxs-lookup"><span data-stu-id="d633f-173">`PubKeyAuthentication yes` = tells SSH you want toouse an SSH key toolog in.</span></span>

<span data-ttu-id="d633f-174">`IdentityFile /home/ahmet/.ssh/id_id_rsa`= la chiave privata SSH hello e toouse di chiave pubblica corrispondente per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="d633f-174">`IdentityFile /home/ahmet/.ssh/id_id_rsa` = hello SSH private key and corresponding public key toouse for authentication.</span></span>

## <a name="ssh-into-linux-without-a-password"></a><span data-ttu-id="d633f-175">Usare SSH per accedere a Linux senza password</span><span class="sxs-lookup"><span data-stu-id="d633f-175">SSH into Linux without a password</span></span>

<span data-ttu-id="d633f-176">Dopo aver creato una coppia di chiavi SSH e un file di configurazione SSH configurato, sono in grado di toolog in tooyour VM Linux rapidamente e in modo sicuro.</span><span class="sxs-lookup"><span data-stu-id="d633f-176">Now that you have an SSH key pair and a configured SSH config file, you are able toolog in tooyour Linux VM quickly and securely.</span></span> <span data-ttu-id="d633f-177">Hello al primo accesso nel server di tooa tramite un prompt dei comandi hello chiave SSH è per la passphrase hello per tale file di chiave.</span><span class="sxs-lookup"><span data-stu-id="d633f-177">hello first time you log in tooa server using an SSH key hello command prompts you for hello passphrase for that key file.</span></span>

```bash
ssh fedora22
```

### <a name="command-explained"></a><span data-ttu-id="d633f-178">Descrizione del comando</span><span class="sxs-lookup"><span data-stu-id="d633f-178">Command explained</span></span>

<span data-ttu-id="d633f-179">Quando `ssh fedora22` viene eseguita SSH prima individua e carica le impostazioni da hello `Host fedora22` blocco e quindi carica tutti hello rimanenti impostazioni dall'ultimo blocco, hello `Host *`.</span><span class="sxs-lookup"><span data-stu-id="d633f-179">When `ssh fedora22` is executed SSH first locates and loads any settings from hello `Host fedora22` block, and then loads all hello remaining settings from hello last block, `Host *`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d633f-180">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d633f-180">Next Steps</span></span>

<span data-ttu-id="d633f-181">Successivamente backup toocreate macchine virtuali Linux di Azure Usa hello nuovo la chiave pubblica SSH.</span><span class="sxs-lookup"><span data-stu-id="d633f-181">Next up is toocreate Azure Linux VMs using hello new SSH public key.</span></span>  <span data-ttu-id="d633f-182">Macchine virtuali di Azure che vengono create con una chiave pubblica SSH come account di accesso hello sono più protette rispetto a macchine virtuali create con metodo di accesso predefinito hello, le password.</span><span class="sxs-lookup"><span data-stu-id="d633f-182">Azure VMs that are created with an SSH public key as hello login are better secured than VMs created with hello default login method, passwords.</span></span>  <span data-ttu-id="d633f-183">Per impostazione predefinita, le VM di Azure create con le chiavi SSH vengono configurate con le password disabilitate, evitando tentativi di attacco basati su forza bruta per scoprire le password.</span><span class="sxs-lookup"><span data-stu-id="d633f-183">Azure VMs created using SSH keys are by default configured with passwords disabled, avoiding brute-forced guessing attempts.</span></span>

* [<span data-ttu-id="d633f-184">Creare una VM Linux protetta usando un modello di Azure</span><span class="sxs-lookup"><span data-stu-id="d633f-184">Create a secure Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="d633f-185">Creare una VM Linux protette utilizzando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="d633f-185">Create a secure Linux VM using hello Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="d633f-186">Creare una VM Linux protette utilizzando hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="d633f-186">Create a secure Linux VM using hello Azure CLI</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
