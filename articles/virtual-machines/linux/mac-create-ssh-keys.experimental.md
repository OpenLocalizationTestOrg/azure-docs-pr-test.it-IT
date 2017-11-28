---
title: coppia di chiavi aaaCreate un SSH per le macchine virtuali Linux in Azure | Documenti Microsoft
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
ms.openlocfilehash: c4c7cec77c9b48295f2a28c8179b30a4dc38a555
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-ssh-public-and-private-key-pair-for-linux-vms"></a><span data-ttu-id="3c920-103">Creare una coppia di chiavi SSH pubblica e privata per le macchine virtuali di Linux</span><span class="sxs-lookup"><span data-stu-id="3c920-103">Create an SSH public and private key pair for Linux VMs</span></span>

<span data-ttu-id="3c920-104">Questo articolo illustra come toogenerate protocol versione 2 RSA pubblica e privata chiave SSH file coppia toouse con le macchine virtuali Linux.</span><span class="sxs-lookup"><span data-stu-id="3c920-104">This article shows you how toogenerate an SSH protocol version 2 RSA public and private key file pair toouse with Linux VMs.</span></span>  <span data-ttu-id="3c920-105">Con una coppia di chiavi SSH, è possibile creare macchine virtuali in Azure che utilizza l'impostazione predefinita le chiavi SSH toousing per l'autenticazione, eliminando la necessità hello per le password toolog in.</span><span class="sxs-lookup"><span data-stu-id="3c920-105">With an SSH key pair, you can create Virtual Machines on Azure that default toousing SSH keys for authentication, eliminating hello need for passwords toolog in.</span></span>  <span data-ttu-id="3c920-106">Le password possono essere individuate e aprire le macchine virtuali di tooguess tentativi di attacchi di forza bruta toorelentless la password.</span><span class="sxs-lookup"><span data-stu-id="3c920-106">Passwords can be guessed, and open your VMs up toorelentless brute force attempts tooguess your password.</span></span> <span data-ttu-id="3c920-107">Macchine virtuali create con modelli di Azure o hello `azure-cli` possono includere la chiave pubblica SSH come parte della distribuzione di hello, la rimozione di un passaggio di configurazione di distribuzione post della disabilitazione dell'account di accesso di password per SSH.</span><span class="sxs-lookup"><span data-stu-id="3c920-107">VMs created with Azure Templates or hello `azure-cli` can include your SSH public key as part of hello deployment, removing a post deployment configuration step of disabling password logins for SSH.</span></span>

## <a name="quick-commands"></a><span data-ttu-id="3c920-108">Comandi rapidi</span><span class="sxs-lookup"><span data-stu-id="3c920-108">Quick Commands</span></span>

<span data-ttu-id="3c920-109">Eseguire hello seguendo i comandi da una shell Bash, sostituendo esempi hello con le proprie scelte.</span><span class="sxs-lookup"><span data-stu-id="3c920-109">Run hello following commands from a Bash shell, replacing hello examples with your own choices.</span></span>

<span data-ttu-id="3c920-110">Per impostazione predefinita, il file di chiave pubblica SSH viene creato in `~/.ssh/id_rsa.pub`.</span><span class="sxs-lookup"><span data-stu-id="3c920-110">Your SSH public key file is by default created at `~/.ssh/id_rsa.pub`.</span></span> <span data-ttu-id="3c920-111">Quando viene richiesto tramite hello comando seguente, è necessario creare un toosecure "passphrase" con la chiave privata.</span><span class="sxs-lookup"><span data-stu-id="3c920-111">When prompted using hello following command, you should create a "passphrase" toosecure your private key.</span></span> <span data-ttu-id="3c920-112">(hello passphrase è utilizzata una password tooencrypt con la chiave privata).</span><span class="sxs-lookup"><span data-stu-id="3c920-112">(hello passphrase is a password used tooencrypt your private key.)</span></span>

```bash
ssh-keygen -t rsa -b 2048 
```

<span data-ttu-id="3c920-113">Aggiungere la chiave di hello appena creato troppo`ssh-agent`:</span><span class="sxs-lookup"><span data-stu-id="3c920-113">Add hello newly created key too`ssh-agent`:</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

> [!IMPORTANT] 
> <span data-ttu-id="3c920-114">Hello sopra lavoro comandi su sistemi operativi Linux di quasi tutte le distribuzioni, ma non necessariamente all'interno di contenitori, come ambiente hello può essere vincolato radicalmente.</span><span class="sxs-lookup"><span data-stu-id="3c920-114">hello above commands work on Linux operating systems of almost all distributions, but do not necessarily work in containers, as hello environment can be radically constrained.</span></span> 

## <a name="detailed-walkthrough"></a><span data-ttu-id="3c920-115">Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="3c920-115">Detailed Walkthrough</span></span>

<span data-ttu-id="3c920-116">Utilizzo delle chiavi pubbliche e private SSH è toolog modo più semplice di hello in server Linux tooyour.</span><span class="sxs-lookup"><span data-stu-id="3c920-116">Using SSH public and private keys is hello easiest way toolog in tooyour Linux servers.</span></span> <span data-ttu-id="3c920-117">[Crittografia a chiave pubblica](https://en.wikipedia.org/wiki/Public-key_cryptography) fornisce un toolog modo molto più sicuro in tooyour Linux o BSD VM in Azure rispetto alle password, che possono essere colpita molto più semplice.</span><span class="sxs-lookup"><span data-stu-id="3c920-117">[Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) provides a much more secure way toolog in tooyour Linux or BSD VM in Azure than passwords, which can be brute-forced far more easily.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3c920-118">La chiave pubblica può essere condivisa con chiunque, ma la chiave privata appartiene solo all'utente o all'infrastruttura di sicurezza locale.</span><span class="sxs-lookup"><span data-stu-id="3c920-118">Your public key can be shared with anyone; but only you (or your local security infrastructure) possess your private key.</span></span>  <span data-ttu-id="3c920-119">la chiave privata SSH Hello deve avere un [password molto sicura](https://www.xkcd.com/936/) (origine:[xkcd.com](https://xkcd.com)) toosafeguard è.</span><span class="sxs-lookup"><span data-stu-id="3c920-119">hello SSH private key should have a [very secure password](https://www.xkcd.com/936/) (source:[xkcd.com](https://xkcd.com)) toosafeguard it.</span></span>  <span data-ttu-id="3c920-120">Questa password è una chiave privata SSH di tooaccess solo hello e **non** password dell'account utente hello.</span><span class="sxs-lookup"><span data-stu-id="3c920-120">This password is just tooaccess hello private SSH key and **is not** hello user account password.</span></span>  <span data-ttu-id="3c920-121">Quando si aggiunge una chiave SSH tooyour, crittografa la chiave privata di hello tramite AES a 128 bit, in modo che hello chiave privata è inutile senza toodecrypt password hello è.</span><span class="sxs-lookup"><span data-stu-id="3c920-121">When you add a password tooyour SSH key, it encrypts hello private key using 128-bit AES, so that hello private key is useless without hello password toodecrypt it.</span></span>  <span data-ttu-id="3c920-122">Se un utente malintenzionato rubare la chiave privata e tale chiave non dispone di una password, saranno in grado di toouse che private key toolog nel server tooany che dispongono di chiave pubblica corrispondente hello.</span><span class="sxs-lookup"><span data-stu-id="3c920-122">If an attacker stole your private key and that key did not have a password, they would be able toouse that private key toolog in tooany servers that have hello corresponding public key.</span></span>  <span data-ttu-id="3c920-123">Una chiave privata protetta da password non può essere usata da utenti malintenzionati e rappresenta un livello di sicurezza aggiuntivo per l'infrastruttura in Azure.</span><span class="sxs-lookup"><span data-stu-id="3c920-123">If a private key is password protected it cannot be used by that attacker, providing an additional layer of security for your infrastructure on Azure.</span></span>

<span data-ttu-id="3c920-124">In questo articolo Crea versione del protocollo SSH 2 RSA pubblici e privati file di chiave, che sono consigliati per le distribuzioni di hello Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="3c920-124">This article creates SSH protocol version 2 RSA public and private key files, which are recommended for deployments on hello Resource Manager.</span></span>  <span data-ttu-id="3c920-125">*SSH-rsa* le chiavi sono necessarie in hello [portale](https://portal.azure.com) per classica e le distribuzioni di gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="3c920-125">*ssh-rsa* keys are required on hello [portal](https://portal.azure.com) for both classic and Resource Manager deployments.</span></span>

## <a name="disable-ssh-passwords-by-using-ssh-keys"></a><span data-ttu-id="3c920-126">Disabilitare le password SSH usando le chiavi SSH</span><span class="sxs-lookup"><span data-stu-id="3c920-126">Disable SSH passwords by using SSH keys</span></span>

<span data-ttu-id="3c920-127">Azure richiede chiavi pubbliche e private nel formato ssh-rsa almeno a 2048 bit.</span><span class="sxs-lookup"><span data-stu-id="3c920-127">Azure requires at least 2048-bit, ssh-rsa format public and private keys.</span></span> <span data-ttu-id="3c920-128">Utilizzare tasti di hello toocreate `ssh-keygen`, che richiede una serie di domande e quindi scrive una chiave privata e una chiave pubblica corrispondente.</span><span class="sxs-lookup"><span data-stu-id="3c920-128">toocreate hello keys use `ssh-keygen`, which asks a series of questions and then writes a private key and a matching public key.</span></span> <span data-ttu-id="3c920-129">Quando viene creata una macchina virtuale di Azure, la chiave pubblica di hello viene copiata troppo`~/.ssh/authorized_keys`.</span><span class="sxs-lookup"><span data-stu-id="3c920-129">When an Azure VM is created, hello public key is copied too`~/.ssh/authorized_keys`.</span></span>  <span data-ttu-id="3c920-130">Le chiavi SSH in `~/.ssh/authorized_keys` vengono utilizzati toochallenge hello toomatch hello corrispondente chiave privata del client su una connessione di accesso SSH.</span><span class="sxs-lookup"><span data-stu-id="3c920-130">SSH keys in `~/.ssh/authorized_keys` are used toochallenge hello client toomatch hello corresponding private key on an SSH login connection.</span></span>  <span data-ttu-id="3c920-131">Quando una macchina virtuale Linux di Azure viene creata utilizzando le chiavi SSH per l'autenticazione, Azure Configura hello SSHD toonot server consente l'accesso con password, solo le chiavi SSH.</span><span class="sxs-lookup"><span data-stu-id="3c920-131">When an Azure Linux VM is created using SSH keys for authentication, Azure configures hello SSHD server toonot allow password logins, only SSH keys.</span></span>  <span data-ttu-id="3c920-132">Pertanto, tramite la creazione di macchine virtuali Linux di Azure con le chiavi SSH, è possibile consentono la distribuzione di macchina virtuale protetta hello e risparmiare passaggio di configurazione post-distribuzione tipica hello della disabilitazione delle password nel file di configurazione sshd_config hello.</span><span class="sxs-lookup"><span data-stu-id="3c920-132">Therefore, by creating Azure Linux VMs with SSH keys, you can help secure hello VM deployment and save yourself hello typical post-deployment configuration step of disabling passwords in hello sshd_config config file.</span></span>

## <a name="using-ssh-keygen"></a><span data-ttu-id="3c920-133">Uso di ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="3c920-133">Using ssh-keygen</span></span>

<span data-ttu-id="3c920-134">Questo comando crea una password protetta (crittografato) coppia di chiavi SSH tramite RSA a 2048 bit e si è impostata come commento tooeasily identificarlo.</span><span class="sxs-lookup"><span data-stu-id="3c920-134">This command creates a password secured (encrypted) SSH key pair using 2048-bit RSA and it is commented tooeasily identify it.</span></span>  

<span data-ttu-id="3c920-135">SSH chiavi per impostazione predefinita vengono mantenuta in hello `~/.ssh` directory.</span><span class="sxs-lookup"><span data-stu-id="3c920-135">SSH keys are by default kept in hello `~/.ssh` directory.</span></span>  <span data-ttu-id="3c920-136">Se non è un `~/.ssh` directory, hello `ssh-keygen` comando crea automaticamente con hello delle autorizzazioni corrette.</span><span class="sxs-lookup"><span data-stu-id="3c920-136">If you do not have a `~/.ssh` directory, hello `ssh-keygen` command creates it for you with hello correct permissions.</span></span>

```bash
ssh-keygen \
-t rsa \
-b 2048 
```

<span data-ttu-id="3c920-137">*Descrizione del comando*</span><span class="sxs-lookup"><span data-stu-id="3c920-137">*Command explained*</span></span>

<span data-ttu-id="3c920-138">`ssh-keygen`= hello programma utilizzato toocreate hello chiavi</span><span class="sxs-lookup"><span data-stu-id="3c920-138">`ssh-keygen` = hello program used toocreate hello keys</span></span>

<span data-ttu-id="3c920-139">`-t rsa`tipo di chiave toocreate hello RSA formato = [wikipedia](https://en.wikipedia.org/wiki/RSA_(cryptosystem)</span><span class="sxs-lookup"><span data-stu-id="3c920-139">`-t rsa` = type of key toocreate which is hello RSA format [wikipedia](https://en.wikipedia.org/wiki/RSA_(cryptosystem)</span></span>

<span data-ttu-id="3c920-140">`-b 2048`= bit della chiave hello</span><span class="sxs-lookup"><span data-stu-id="3c920-140">`-b 2048` = bits of hello key</span></span>


## <a name="classic-portal-and-x509-certs"></a><span data-ttu-id="3c920-141">Portale classico e certificati X.509</span><span class="sxs-lookup"><span data-stu-id="3c920-141">Classic portal and X.509 certs</span></span>

<span data-ttu-id="3c920-142">Se si utilizza hello Azure [portale classico](https://manage.windowsazure.com/), richiede i certificati x. 509 per le chiavi SSH hello.</span><span class="sxs-lookup"><span data-stu-id="3c920-142">If you are using hello Azure [classic portal](https://manage.windowsazure.com/), it requires X.509 certs for hello SSH keys.</span></span>  <span data-ttu-id="3c920-143">Non sono consentite altre chiavi pubbliche SSH, *devono* essere certificati X.509.</span><span class="sxs-lookup"><span data-stu-id="3c920-143">No other types of SSH public keys are allowed, they *must* be X.509 certs.</span></span>

<span data-ttu-id="3c920-144">toocreate un certificato x. 509 dalla chiave privata SSH-RSA esistente:</span><span class="sxs-lookup"><span data-stu-id="3c920-144">toocreate an X.509 cert from your existing SSH-RSA private key:</span></span>

```bash
openssl req -x509 \
-key ~/.ssh/id_rsa \
-nodes \
-days 365 \
-newkey rsa:2048 \
-out ~/.ssh/id_rsa.pem
```

## <a name="classic-deploy-using-asm"></a><span data-ttu-id="3c920-145">Distribuzione classica tramite `asm`</span><span class="sxs-lookup"><span data-stu-id="3c920-145">Classic deploy using `asm`</span></span>

<span data-ttu-id="3c920-146">Se si utilizza classica hello distribuire modello (gestione dei servizi Azure CLI `asm`), è possibile utilizzare una chiave pubblica SSH-RSA o formattato un RFC4716 chiave in un **PEM** contenitore.</span><span class="sxs-lookup"><span data-stu-id="3c920-146">If you are using hello classic deploy model (Azure service management CLI `asm`), you can use an SSH-RSA public key or an RFC4716 formatted key in a **.pem** container.</span></span>  <span data-ttu-id="3c920-147">chiave pubblica SSH-RSA Hello è ciò che è stato creato in precedenza in questo articolo utilizzando `ssh-keygen`.</span><span class="sxs-lookup"><span data-stu-id="3c920-147">hello SSH-RSA public key is what was created earlier in this article using `ssh-keygen`.</span></span>

<span data-ttu-id="3c920-148">toocreate un RFC4716 formato della chiave da una chiave pubblica SSH esistente:</span><span class="sxs-lookup"><span data-stu-id="3c920-148">toocreate a RFC4716 formatted key from an existing SSH public key:</span></span>

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a><span data-ttu-id="3c920-149">Esempio di ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="3c920-149">Example of ssh-keygen</span></span>

```bash
ssh-keygen -t rsa -b 2048 -C "ahmet@myserver"
Generating public/private rsa key pair.
Enter file in which toosave hello key (/home/ahmet/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/ahmet/.ssh/id_rsa.
Your public key has been saved in /home/ahmet/.ssh/id_rsa.pub.
hello key fingerprint is:
14:a3:cb:3e:78:ad:25:cc:55:e9:0c:08:e5:d1:a9:08 ahmet@myserver
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

<span data-ttu-id="3c920-150">File delle chiavi salvati:</span><span class="sxs-lookup"><span data-stu-id="3c920-150">Saved key files:</span></span>

`Enter file in which toosave hello key (/home/ahmet/.ssh/id_rsa): ~/.ssh/id_rsa`

<span data-ttu-id="3c920-151">nome della coppia chiave Hello per questo articolo.</span><span class="sxs-lookup"><span data-stu-id="3c920-151">hello key pair name for this article.</span></span>  <span data-ttu-id="3c920-152">Con una coppia di chiavi denominata **id_rsa** hello predefinito e alcuni strumenti prevedibile hello **id_rsa** nome di file di chiave privata in modo che uno è una buona idea.</span><span class="sxs-lookup"><span data-stu-id="3c920-152">Having a key pair named **id_rsa** is hello default and some tools might expect hello **id_rsa** private key file name so having one is a good idea.</span></span> <span data-ttu-id="3c920-153">directory Hello `~/.ssh/` è il percorso predefinito hello per le coppie di chiavi SSH e file di configurazione di hello SSH.</span><span class="sxs-lookup"><span data-stu-id="3c920-153">hello directory `~/.ssh/` is hello default location for SSH key pairs and hello SSH config file.</span></span>  <span data-ttu-id="3c920-154">Se non è specificato con un percorso completo, `ssh-keygen` dovrà creare chiavi hello nella directory di lavoro corrente hello, hello non predefinito `~/.ssh`.</span><span class="sxs-lookup"><span data-stu-id="3c920-154">If not specified with a full path, `ssh-keygen` will create hello keys in hello current working directory, not hello default `~/.ssh`.</span></span>

<span data-ttu-id="3c920-155">Un elenco di hello `~/.ssh` directory.</span><span class="sxs-lookup"><span data-stu-id="3c920-155">A listing of hello `~/.ssh` directory.</span></span>

```bash
ls -al ~/.ssh
-rw------- 1 ahmet staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 ahmet staff   410 Aug 25 18:04 rsa.pub
```

<span data-ttu-id="3c920-156">Password della chiave:</span><span class="sxs-lookup"><span data-stu-id="3c920-156">Key Password:</span></span>

`Enter passphrase (empty for no passphrase):`

<span data-ttu-id="3c920-157">`ssh-keygen`fa riferimento di chiave privata hello tooencrypt password utilizzata tooa come "una passphrase."</span><span class="sxs-lookup"><span data-stu-id="3c920-157">`ssh-keygen` refers tooa password used tooencrypt hello private key as "a passphrase."</span></span>  <span data-ttu-id="3c920-158">È *fortemente* consigliato tooadd coppie di chiavi di tooyour una passphrase.</span><span class="sxs-lookup"><span data-stu-id="3c920-158">It is *strongly* recommended tooadd a passphrase tooyour key pairs.</span></span> <span data-ttu-id="3c920-159">Senza una passphrase protezione hello chiave privata, tutti gli utenti con i file di chiave hello usarlo toolog tooany server dotato di chiave pubblica corrispondente hello.</span><span class="sxs-lookup"><span data-stu-id="3c920-159">Without a passphrase protecting hello private key, anyone with hello key file can use it toolog in tooany server that has hello corresponding public key.</span></span> <span data-ttu-id="3c920-160">Aggiunta di una passphrase offre ulteriore protezione, nel caso in cui un utente è in grado di toogain accesso tooyour file di chiave privata, offrendo chiavi hello toochange utilizzato tooauthenticate è.</span><span class="sxs-lookup"><span data-stu-id="3c920-160">Adding a passphrase offers more protection in case someone is able toogain access tooyour private key file, giving you time toochange hello keys used tooauthenticate you.</span></span>

## <a name="using-ssh-agent-toostore-your-private-key-password"></a><span data-ttu-id="3c920-161">Utilizzo di ssh agente toostore la password della chiave privata</span><span class="sxs-lookup"><span data-stu-id="3c920-161">Using ssh-agent toostore your private key password</span></span>

<span data-ttu-id="3c920-162">Digitare la chiave privata tooavoid file passphrase con ogni account di accesso SSH, è possibile utilizzare `ssh-agent` toocache la password del file di chiave privata.</span><span class="sxs-lookup"><span data-stu-id="3c920-162">tooavoid typing your private key file passphrase with every SSH login, you can use `ssh-agent` toocache your private key file password.</span></span> <span data-ttu-id="3c920-163">Se si utilizza un computer Mac, hello OSX portachiavi Archivia password chiave privata hello in modo sicuro quando si richiama `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="3c920-163">If you are using a Mac, hello OSX Keychain securely stores hello private key passwords when you invoke `ssh-agent`.</span></span>

<span data-ttu-id="3c920-164">Verificare e utilizzare `ssh-agent` e `ssh-add` tooinform hello sistema SSH sui file di chiave hello in modo che la passphrase hello non sarà necessario toobe utilizzati in modo interattivo.</span><span class="sxs-lookup"><span data-stu-id="3c920-164">Verify and use `ssh-agent` and `ssh-add` tooinform hello SSH system about hello key files so that hello passphrase will not need toobe used interactively.</span></span>

```bash
eval "$(ssh-agent -s)"
```

<span data-ttu-id="3c920-165">A questo punto aggiungere la chiave privata di hello troppo`ssh-agent` comando hello `ssh-add`.</span><span class="sxs-lookup"><span data-stu-id="3c920-165">Now add hello private key too`ssh-agent` using hello command `ssh-add`.</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

<span data-ttu-id="3c920-166">password della chiave privata Hello sono ora archiviate in `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="3c920-166">hello private key password is now stored in `ssh-agent`.</span></span>

## <a name="using-ssh-copy-id-tooinstall-hello-new-key"></a><span data-ttu-id="3c920-167">Utilizzando `ssh-copy-id` nuova chiave di tooinstall hello</span><span class="sxs-lookup"><span data-stu-id="3c920-167">Using `ssh-copy-id` tooinstall hello new key</span></span>
<span data-ttu-id="3c920-168">Se è stato già creato una macchina virtuale è possibile installare hello nuovo SSH pubblica chiave tooyour VM Linux con hello comando seguente, sostituendo il nome utente VM hello e l'indirizzo di server hello con valori personalizzati:</span><span class="sxs-lookup"><span data-stu-id="3c920-168">If you have already created a VM you can install hello new SSH public key tooyour Linux VM with hello following command, replacing hello VM username and hello server address with your own values:</span></span>

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a><span data-ttu-id="3c920-169">Creare e configurare un file config SSH</span><span class="sxs-lookup"><span data-stu-id="3c920-169">Create and configure an SSH config file</span></span>

<span data-ttu-id="3c920-170">Un migliore toocreate pratica e configurare un `~/.ssh/config` toospeed file di log aggiuntivi e per l'ottimizzazione del comportamento del client SSH.</span><span class="sxs-lookup"><span data-stu-id="3c920-170">It is a best practice toocreate and configure an `~/.ssh/config` file toospeed up log ins and for optimizing your SSH client behavior.</span></span>

<span data-ttu-id="3c920-171">Hello di esempio seguente viene illustrata una configurazione standard.</span><span class="sxs-lookup"><span data-stu-id="3c920-171">hello following example shows a standard configuration.</span></span>

### <a name="create-hello-file"></a><span data-ttu-id="3c920-172">Creare file hello</span><span class="sxs-lookup"><span data-stu-id="3c920-172">Create hello file</span></span>

```bash
touch ~/.ssh/config
```

### <a name="edit-hello-file-tooadd-hello-new-ssh-configuration"></a><span data-ttu-id="3c920-173">Modificare hello file tooadd hello nuova configurazione SSH:</span><span class="sxs-lookup"><span data-stu-id="3c920-173">Edit hello file tooadd hello new SSH configuration:</span></span>

```bash
vim ~/.ssh/config
```

### <a name="example-sshconfig-file"></a><span data-ttu-id="3c920-174">File `~/.ssh/config` di esempio:</span><span class="sxs-lookup"><span data-stu-id="3c920-174">Example `~/.ssh/config` file:</span></span>

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

<span data-ttu-id="3c920-175">In questo modo di configurazione SSH sezioni per ogni server tooenable ogni toohave propria dedicata coppia di chiavi.</span><span class="sxs-lookup"><span data-stu-id="3c920-175">This SSH config gives you sections for each server tooenable each toohave its own dedicated key pair.</span></span> <span data-ttu-id="3c920-176">le impostazioni predefinite di Hello (`Host *`) sono per tutti gli host che non corrispondono a uno degli host hello specifico livello più alto nel file di configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="3c920-176">hello default settings (`Host *`) are for any hosts that do not match any of hello specific hosts higher up in hello config file.</span></span>

### <a name="config-file-explained"></a><span data-ttu-id="3c920-177">Descrizione del file config</span><span class="sxs-lookup"><span data-stu-id="3c920-177">Config file explained</span></span>

<span data-ttu-id="3c920-178">`Host`= nome hello dell'host di hello viene chiamato il metodo hello terminal.</span><span class="sxs-lookup"><span data-stu-id="3c920-178">`Host` = hello name of hello host being called on hello terminal.</span></span>  <span data-ttu-id="3c920-179">`ssh fedora22`indica `SSH` valori hello toouse in blocco settings hello etichettata `Host fedora22` Nota: Host può essere qualsiasi etichetta logico per l'utilizzo e non rappresenta hello nome host effettivo di qualsiasi server.</span><span class="sxs-lookup"><span data-stu-id="3c920-179">`ssh fedora22` tells `SSH` toouse hello values in hello settings block labeled `Host fedora22`  NOTE: Host can be any label that is logical for your usage and does not represent hello actual hostname of any server.</span></span>

<span data-ttu-id="3c920-180">`Hostname 102.160.203.241`= indirizzo hello o un nome DNS per il server di hello cui si accede.</span><span class="sxs-lookup"><span data-stu-id="3c920-180">`Hostname 102.160.203.241` = hello IP address or DNS name for hello server being accessed.</span></span>

<span data-ttu-id="3c920-181">`User ahmet`= toouse di account utente remoto hello durante l'accesso toohello server.</span><span class="sxs-lookup"><span data-stu-id="3c920-181">`User ahmet` = hello remote user account toouse when logging in toohello server.</span></span>

<span data-ttu-id="3c920-182">`PubKeyAuthentication yes`= indica SSH desiderato toouse un toolog chiave SSH.</span><span class="sxs-lookup"><span data-stu-id="3c920-182">`PubKeyAuthentication yes` = tells SSH you want toouse an SSH key toolog in.</span></span>

<span data-ttu-id="3c920-183">`IdentityFile /home/ahmet/.ssh/id_id_rsa`= la chiave privata SSH hello e toouse di chiave pubblica corrispondente per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="3c920-183">`IdentityFile /home/ahmet/.ssh/id_id_rsa` = hello SSH private key and corresponding public key toouse for authentication.</span></span>

## <a name="ssh-into-linux-without-a-password"></a><span data-ttu-id="3c920-184">Usare SSH per accedere a Linux senza password</span><span class="sxs-lookup"><span data-stu-id="3c920-184">SSH into Linux without a password</span></span>

<span data-ttu-id="3c920-185">Dopo aver creato una coppia di chiavi SSH e un file di configurazione SSH configurato, sono in grado di toolog in tooyour VM Linux rapidamente e in modo sicuro.</span><span class="sxs-lookup"><span data-stu-id="3c920-185">Now that you have an SSH key pair and a configured SSH config file, you are able toolog in tooyour Linux VM quickly and securely.</span></span> <span data-ttu-id="3c920-186">Hello al primo accesso nel server di tooa tramite un prompt dei comandi hello chiave SSH è per la passphrase hello per tale file di chiave.</span><span class="sxs-lookup"><span data-stu-id="3c920-186">hello first time you log in tooa server using an SSH key hello command prompts you for hello passphrase for that key file.</span></span>

```bash
ssh fedora22
```

### <a name="command-explained"></a><span data-ttu-id="3c920-187">Descrizione del comando</span><span class="sxs-lookup"><span data-stu-id="3c920-187">Command explained</span></span>

<span data-ttu-id="3c920-188">Quando `ssh fedora22` viene eseguita SSH prima individua e carica le impostazioni da hello `Host fedora22` blocco e quindi carica tutti hello rimanenti impostazioni dall'ultimo blocco, hello `Host *`.</span><span class="sxs-lookup"><span data-stu-id="3c920-188">When `ssh fedora22` is executed SSH first locates and loads any settings from hello `Host fedora22` block, and then loads all hello remaining settings from hello last block, `Host *`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c920-189">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3c920-189">Next Steps</span></span>

<span data-ttu-id="3c920-190">Successivamente backup toocreate macchine virtuali Linux di Azure Usa hello nuovo la chiave pubblica SSH.</span><span class="sxs-lookup"><span data-stu-id="3c920-190">Next up is toocreate Azure Linux VMs using hello new SSH public key.</span></span>  <span data-ttu-id="3c920-191">Macchine virtuali di Azure che vengono create con una chiave pubblica SSH come account di accesso hello sono più protette rispetto a macchine virtuali create con metodo di accesso predefinito hello, le password.</span><span class="sxs-lookup"><span data-stu-id="3c920-191">Azure VMs that are created with an SSH public key as hello login are better secured than VMs created with hello default login method, passwords.</span></span>  <span data-ttu-id="3c920-192">Per impostazione predefinita, le VM di Azure create con le chiavi SSH vengono configurate con le password disabilitate, evitando tentativi di attacco basati su forza bruta per scoprire le password.</span><span class="sxs-lookup"><span data-stu-id="3c920-192">Azure VMs created using SSH keys are by default configured with passwords disabled, avoiding brute-forced guessing attempts.</span></span> <span data-ttu-id="3c920-193">Se si necessita di ulteriore assistenza per la creazione di coppia di chiavi SSH o richiedono certificati aggiuntivi, ad esempio per l'utilizzo con portale classico hello, vedere [dettagliate coppie di chiavi SSH toocreate passaggi e i certificati](create-ssh-keys-detailed.md).</span><span class="sxs-lookup"><span data-stu-id="3c920-193">If you need more assistance in creating your SSH key pair or require additional certificates, such as for use with hello classic portal, see [Detailed steps toocreate SSH key pairs and certificates](create-ssh-keys-detailed.md).</span></span>

* [<span data-ttu-id="3c920-194">Creare una VM Linux protetta usando un modello di Azure</span><span class="sxs-lookup"><span data-stu-id="3c920-194">Create a secure Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="3c920-195">Creare una VM Linux protette utilizzando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="3c920-195">Create a secure Linux VM using hello Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="3c920-196">Creare una VM Linux protette utilizzando hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="3c920-196">Create a secure Linux VM using hello Azure CLI</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
