---
title: le password SSH aaaDisable nella VM Linux configurando SSHD | Documenti Microsoft
description: Proteggere la VM Linux in Azure disabilitando l'accesso tramite password per SSH.
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: 
ms.assetid: 46137640-a7d2-40e5-a1e9-9effef7eb190
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/26/2016
ms.author: v-livech
ms.openlocfilehash: fb67b2f5b8b3bf2ba214858940b04f2ea9013fb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="disable-ssh-passwords-on-your-linux-vm-by-configuring-sshd"></a><span data-ttu-id="894f7-103">Disabilitare le password SSH nella VM Linux configurando SSHD</span><span class="sxs-lookup"><span data-stu-id="894f7-103">Disable SSH passwords on your Linux VM by configuring SSHD</span></span>
<span data-ttu-id="894f7-104">Questo articolo è incentrato sulla toolock verso il basso la sicurezza degli accessi hello della VM Linux.</span><span class="sxs-lookup"><span data-stu-id="894f7-104">This article focuses on how toolock down hello login security of your Linux VM.</span></span>  <span data-ttu-id="894f7-105">Non appena viene aperta la porta SSH 22 hello toohello world Bot avviare durante il tentativo toologin cercando di indovinare le password.</span><span class="sxs-lookup"><span data-stu-id="894f7-105">As soon as hello SSH port 22 is opened toohello world bots start trying toologin by guessing passwords.</span></span>  <span data-ttu-id="894f7-106">In questo articolo si disabiliteranno gli accessi tramite password mediante SSH.</span><span class="sxs-lookup"><span data-stu-id="894f7-106">What we will do in this article is disable password logins over SSH.</span></span>  <span data-ttu-id="894f7-107">Per rimuovere completamente il possibilità hello attacco di forza password toouse Proteggiamo hello VM Linux da questo tipo di bruta.</span><span class="sxs-lookup"><span data-stu-id="894f7-107">By completely removing hello ability toouse passwords we protect hello Linux VM from this type of brute force attack.</span></span>  <span data-ttu-id="894f7-108">Hello aggiunto bonus si configurerà Linux SSHD tooonly consentire gli account di accesso tramite chiavi SSH pubbliche e private di gran lunga hello tooLinux di toologin modo più sicuro.</span><span class="sxs-lookup"><span data-stu-id="894f7-108">hello added bonus is we will configure Linux SSHD tooonly allow logins via SSH public & private keys, by far hello most secure way toologin tooLinux.</span></span>  <span data-ttu-id="894f7-109">le possibili combinazioni Hello di esso richiederebbe la chiave privata tooguess hello è enorme e sconsiglia pertanto Bot dall'intervento tootry toobrute force le chiavi SSH.</span><span class="sxs-lookup"><span data-stu-id="894f7-109">hello possible combinations of it would require tooguess hello private key is immense and therefore discourages bots from even bothering tootry toobrute force SSH keys.</span></span>

## <a name="goals"></a><span data-ttu-id="894f7-110">Obiettivi</span><span class="sxs-lookup"><span data-stu-id="894f7-110">Goals</span></span>
* <span data-ttu-id="894f7-111">Configurare SSHD toodisallow:</span><span class="sxs-lookup"><span data-stu-id="894f7-111">Configure SSHD toodisallow:</span></span>
  * <span data-ttu-id="894f7-112">Accessi tramite password</span><span class="sxs-lookup"><span data-stu-id="894f7-112">Password logins</span></span>
  * <span data-ttu-id="894f7-113">Accesso dell'utente ROOT</span><span class="sxs-lookup"><span data-stu-id="894f7-113">Root user login</span></span>
  * <span data-ttu-id="894f7-114">Autenticazione In attesa/Risposta</span><span class="sxs-lookup"><span data-stu-id="894f7-114">Challenge-response authentication</span></span>
* <span data-ttu-id="894f7-115">Configurare SSHD tooallow:</span><span class="sxs-lookup"><span data-stu-id="894f7-115">Configure SSHD tooallow:</span></span>
  * <span data-ttu-id="894f7-116">solo accessi tramite chiave SSH</span><span class="sxs-lookup"><span data-stu-id="894f7-116">only SSH key logins</span></span>
* <span data-ttu-id="894f7-117">Riavviare SSHD durante la connessione</span><span class="sxs-lookup"><span data-stu-id="894f7-117">Restart SSHD while still logged in</span></span>
* <span data-ttu-id="894f7-118">Configurazione di test hello nuovo SSHD</span><span class="sxs-lookup"><span data-stu-id="894f7-118">Test hello new SSHD configuration</span></span>

## <a name="introduction"></a><span data-ttu-id="894f7-119">Introduzione</span><span class="sxs-lookup"><span data-stu-id="894f7-119">Introduction</span></span>
[<span data-ttu-id="894f7-120">Definizione di SSH</span><span class="sxs-lookup"><span data-stu-id="894f7-120">SSH defined</span></span>](https://en.wikipedia.org/wiki/Secure_Shell)

<span data-ttu-id="894f7-121">SSHD è hello Server SSH in esecuzione su hello VM Linux.</span><span class="sxs-lookup"><span data-stu-id="894f7-121">SSHD is hello SSH Server that runs on hello Linux VM.</span></span>  <span data-ttu-id="894f7-122">SSH è un client eseguito da una shell nella workstation MacBook o Linux.</span><span class="sxs-lookup"><span data-stu-id="894f7-122">SSH is a client that runs from a shell on your MacBook or Linux workstation.</span></span>  <span data-ttu-id="894f7-123">SSH è anche il protocollo hello utilizzato toosecure e crittografare le comunicazioni tra la workstation e hello VM Linux hello.</span><span class="sxs-lookup"><span data-stu-id="894f7-123">SSH is also hello protocol used toosecure and encrypt hello communication between your workstation and hello Linux VM.</span></span>

<span data-ttu-id="894f7-124">Per questo articolo è molto importante tookeep un account di accesso tooyour VM Linux aperto per l'intera hello scorrere.</span><span class="sxs-lookup"><span data-stu-id="894f7-124">For this article it is very important tookeep one login tooyour Linux VM open for hello entire walk through.</span></span>  <span data-ttu-id="894f7-125">Per questo motivo verrà aperta due terminali e SSH toohello VM Linux da entrambi gli elementi.</span><span class="sxs-lookup"><span data-stu-id="894f7-125">For this reason we will open two terminals and SSH toohello Linux VM from both of them.</span></span>  <span data-ttu-id="894f7-126">Verrà utilizzare hello primo toomake terminal hello modifiche tooSSHDs file di configurazione e riavviare il servizio SSHD hello.</span><span class="sxs-lookup"><span data-stu-id="894f7-126">We will use hello first terminal toomake hello changes tooSSHDs configuration file and restart hello SSHD service.</span></span>  <span data-ttu-id="894f7-127">Si utilizzerà hello tootest terminal secondo le modifiche dopo aver riavviato il servizio di hello.</span><span class="sxs-lookup"><span data-stu-id="894f7-127">We will use hello second terminal tootest those changes once hello service is restarted.</span></span>  <span data-ttu-id="894f7-128">Poiché ci stiamo disabilitazione password SSH e basarsi esclusivamente sulle chiavi SSH, se le chiavi SSH non sono corrette e si chiude hello connessione toohello VM, hello VM verrà definitivamente bloccato e non sarà in grado di toologin tooit richiederla toobe eliminato e ricreato.</span><span class="sxs-lookup"><span data-stu-id="894f7-128">Because we are disabling SSH passwords and relying strictly on SSH keys, if your SSH keys are not correct and you close hello connection toohello VM, hello VM will be permanently locked and no one will be able toologin tooit requiring it toobe deleted and recreated.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="894f7-129">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="894f7-129">Prerequisites</span></span>
* [<span data-ttu-id="894f7-130">Creare chiavi SSH in Linux e Mac per le VM Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="894f7-130">Create SSH keys on Linux and Mac for Linux VMs in Azure</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* <span data-ttu-id="894f7-131">Account Azure</span><span class="sxs-lookup"><span data-stu-id="894f7-131">Azure account</span></span>
  * [<span data-ttu-id="894f7-132">Versione di valutazione gratuita</span><span class="sxs-lookup"><span data-stu-id="894f7-132">free trial signup</span></span>](https://azure.microsoft.com/pricing/free-trial/)
  * [<span data-ttu-id="894f7-133">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="894f7-133">Azure portal</span></span>](http://portal.azure.com)
* <span data-ttu-id="894f7-134">VM Linux in esecuzione in Azure</span><span class="sxs-lookup"><span data-stu-id="894f7-134">Linux VM running on azure</span></span>
* <span data-ttu-id="894f7-135">Coppia di chiavi SSH pubblica e privata in `~/.ssh/`</span><span class="sxs-lookup"><span data-stu-id="894f7-135">SSH public & private key pair in `~/.ssh/`</span></span>
* <span data-ttu-id="894f7-136">La chiave pubblica SSH in `~/.ssh/authorized_keys` su hello VM Linux</span><span class="sxs-lookup"><span data-stu-id="894f7-136">SSH public key in `~/.ssh/authorized_keys` on hello Linux VM</span></span>
* <span data-ttu-id="894f7-137">Diritti di Sudo su hello VM</span><span class="sxs-lookup"><span data-stu-id="894f7-137">Sudo rights on hello VM</span></span>
* <span data-ttu-id="894f7-138">Porta 22 aperta</span><span class="sxs-lookup"><span data-stu-id="894f7-138">Port 22 open</span></span>

## <a name="quick-commands"></a><span data-ttu-id="894f7-139">Comandi rapidi</span><span class="sxs-lookup"><span data-stu-id="894f7-139">Quick Commands</span></span>
<span data-ttu-id="894f7-140">*Gli amministratori di Linux esperti che si desidera versione TLDR hello iniziare da qui.  Per tutti gli utenti che desidera hello dettagliate e procedura per ignorare questa sezione.*</span><span class="sxs-lookup"><span data-stu-id="894f7-140">*Seasoned Linux Admins who just want hello TLDR version start here.  For everyone else that wants hello detailed explanation and walk through skip this section.*</span></span>

```bash
sudo vim /etc/ssh/sshd_config
```

<span data-ttu-id="894f7-141">Modificare il file di configurazione di hello come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="894f7-141">Edit hello config file as follows:</span></span>

```sh
# Change PasswordAuthentication toothis:
PasswordAuthentication no

# Change PubkeyAuthentication toothis:
PubkeyAuthentication yes

# Change PermitRootLogin toothis:
PermitRootLogin no

# Change ChallengeResponseAuthentication toothis:
ChallengeResponseAuthentication no
```

<span data-ttu-id="894f7-142">Riavviare il servizio SSHD hello.</span><span class="sxs-lookup"><span data-stu-id="894f7-142">Restart hello SSHD service.</span></span> <span data-ttu-id="894f7-143">Nelle distribuzioni basate su Debian:</span><span class="sxs-lookup"><span data-stu-id="894f7-143">On Debian-based distros:</span></span>

```bash
sudo service ssh restart
```

<span data-ttu-id="894f7-144">Nelle distribuzioni basate su Red Hat:</span><span class="sxs-lookup"><span data-stu-id="894f7-144">On Red Hat-based distros:</span></span>

```bash
sudo service sshd restart
```

## <a name="detailed-walk-through"></a><span data-ttu-id="894f7-145">Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="894f7-145">Detailed Walk Through</span></span>
<span data-ttu-id="894f7-146">Account di accesso toohello VM Linux su terminal 1 (T1).</span><span class="sxs-lookup"><span data-stu-id="894f7-146">Login toohello Linux VM on terminal 1 (T1).</span></span>  <span data-ttu-id="894f7-147">Account di accesso toohello VM Linux su terminal 2 (T2).</span><span class="sxs-lookup"><span data-stu-id="894f7-147">Login toohello Linux VM on terminal 2 (T2).</span></span>

<span data-ttu-id="894f7-148">Nella tabella T2 verrà file di configurazione tooedit hello SSHD.</span><span class="sxs-lookup"><span data-stu-id="894f7-148">On T2 we are going tooedit hello SSHD configuration file.</span></span>  

```bash
sudo vim /etc/ssh/sshd_config
```

<span data-ttu-id="894f7-149">Da qui la modifica appena hello impostazioni toodisable le password e abilitare gli account di accesso chiave SSH.</span><span class="sxs-lookup"><span data-stu-id="894f7-149">From here we will edit just hello settings toodisable passwords and enable SSH key logins.</span></span>  <span data-ttu-id="894f7-150">Esistono molte impostazioni in questo file che è consigliabile ricercare e modificare toomake Linux & SSH come protette in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="894f7-150">There are many settings in this file that you should research and change toomake Linux & SSH as secure as you need.</span></span>

#### <a name="disable-password-logins"></a><span data-ttu-id="894f7-151">Disabilitare gli accessi tramite password</span><span class="sxs-lookup"><span data-stu-id="894f7-151">Disable Password logins</span></span>

```sh
# Change PasswordAuthentication toothis:
PasswordAuthentication no
```

#### <a name="enable-public-key-authentication"></a><span data-ttu-id="894f7-152">Abilitare l'autenticazione con chiave pubblica</span><span class="sxs-lookup"><span data-stu-id="894f7-152">Enable Public Key Authentication</span></span>

```sh
# Change PubkeyAuthentication toothis:
PubkeyAuthentication yes
```

#### <a name="disable-root-login"></a><span data-ttu-id="894f7-153">Disabilitare l'accesso root</span><span class="sxs-lookup"><span data-stu-id="894f7-153">Disable Root Login</span></span>

```sh
# Change PermitRootLogin toothis:
PermitRootLogin no
```

#### <a name="disable-challenge-response-authentication"></a><span data-ttu-id="894f7-154">Disabilitare l'autenticazione In attesa/Risposta</span><span class="sxs-lookup"><span data-stu-id="894f7-154">Disable Challenge-response Authentication</span></span>
```sh
# Change ChallengeResponseAuthentication toothis:
ChallengeResponseAuthentication no
```

### <a name="restart-sshd"></a><span data-ttu-id="894f7-155">Riavviare SSHD</span><span class="sxs-lookup"><span data-stu-id="894f7-155">Restart SSHD</span></span>
<span data-ttu-id="894f7-156">Verificare che si è ancora connessi da shell hello T1.</span><span class="sxs-lookup"><span data-stu-id="894f7-156">From hello T1 shell verify that you are still logged in.</span></span>  <span data-ttu-id="894f7-157">Questo è fondamentale per non rimanere esclusi dalla VM nel caso in cui le chiavi SSH non siano corrette, dato che ora le password sono disabilitate.</span><span class="sxs-lookup"><span data-stu-id="894f7-157">This is critical so you do not get locked out of your VM if your SSH keys are not correct since passwords are now disabled.</span></span>  <span data-ttu-id="894f7-158">Se tutte le impostazioni sono corrette nella VM Linux è possibile utilizzare T1 toofix sshd_config come verrà comunque eseguito e SSH verrà mantenere attiva la connessione hello durante hello service SSHD riavviare.</span><span class="sxs-lookup"><span data-stu-id="894f7-158">If any setting are incorrect on your Linux VM you can use T1 toofix sshd_config as you will still be logged in and SSH will keep hello connection alive during hello SSHD service restart.</span></span>

<span data-ttu-id="894f7-159">Da T2 eseguire:</span><span class="sxs-lookup"><span data-stu-id="894f7-159">From T2 run:</span></span>

##### <a name="on-hello-debian-family"></a><span data-ttu-id="894f7-160">Nella famiglia Debian hello</span><span class="sxs-lookup"><span data-stu-id="894f7-160">On hello Debian Family</span></span>
```bash
sudo service ssh restart
```

##### <a name="on-hello-redhat-family"></a><span data-ttu-id="894f7-161">Nella famiglia RedHat hello</span><span class="sxs-lookup"><span data-stu-id="894f7-161">On hello RedHat Family</span></span>
```bash
sudo service sshd restart
```

<span data-ttu-id="894f7-162">Le password sono ora disabilitate nella VM, che a questo punto è protetta dai tentativi di accesso tramite password da parte di attacchi di forza bruta.</span><span class="sxs-lookup"><span data-stu-id="894f7-162">Passwords are now disabled on your VM protecting it from brute force password login attempts.</span></span>  <span data-ttu-id="894f7-163">Con solo SSH chiavi consentito sarà in grado di toologin molto più rapido e sicuro.</span><span class="sxs-lookup"><span data-stu-id="894f7-163">With only SSH Keys allowed you will be able toologin faster and much more secure.</span></span>

