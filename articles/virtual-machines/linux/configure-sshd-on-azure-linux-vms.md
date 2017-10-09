---
title: aaaConfigure SSHD nelle macchine virtuali Linux di Azure | Documenti Microsoft
description: Configurare SSHD per le procedure consigliate e toolockdown SSH tooAzure macchine virtuali Linux.
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/21/2016
ms.author: v-livech
ms.openlocfilehash: c2361be7199a24b129c06acfc899dd32f6e1d6fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-sshd-on-azure-linux-vms"></a><span data-ttu-id="56460-103">Configurare SSHD nelle macchine virtuali Linux di Azure</span><span class="sxs-lookup"><span data-stu-id="56460-103">Configure SSHD on Azure Linux VMs</span></span>

<span data-ttu-id="56460-104">Questo articolo illustra come toolockdown hello Server SSH in Linux, ottimizzare la sicurezza consigliate tooprovide e toospeed di processo di accesso SSH hello utilizzando le chiavi SSH anziché le password.</span><span class="sxs-lookup"><span data-stu-id="56460-104">This article shows how toolockdown hello SSH Server on Linux, tooprovide best practices security and also toospeed up hello SSH login process by using SSH keys instead of passwords.</span></span>  <span data-ttu-id="56460-105">blocco toofurther SSHD verrà utente root di hello toodisable siano in grado di toologin, limitare gli utenti di hello consentiti toologin tramite un elenco di gruppi approvati, la disabilitazione di versione 1 del protocollo SSH, impostare una chiave minima di bit e configurare auto-disconnessione degli utenti inattivi.</span><span class="sxs-lookup"><span data-stu-id="56460-105">toofurther lockdown SSHD we are going toodisable hello root user from being able toologin, limit hello users that are allowed toologin via an approved group list, disabling SSH protocol version 1, set a minimum key bit, and configure auto-logout of idle users.</span></span>  <span data-ttu-id="56460-106">requisiti di Hello per questo articolo sono: un account di Azure ([ottenere una versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/)) e [file chiavi SSH pubblica e privata](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="56460-106">hello requirements for this article are: an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)) and [SSH public and private key files](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="56460-107">Comandi rapidi</span><span class="sxs-lookup"><span data-stu-id="56460-107">Quick Commands</span></span>

<span data-ttu-id="56460-108">Configurare `/etc/ssh/sshd_config` con hello seguenti impostazioni:</span><span class="sxs-lookup"><span data-stu-id="56460-108">Configure `/etc/ssh/sshd_config` with hello following settings:</span></span>

### <a name="disable-password-logins"></a><span data-ttu-id="56460-109">Disabilitare gli accessi tramite password</span><span class="sxs-lookup"><span data-stu-id="56460-109">Disable password logins</span></span>

```bash
PasswordAuthentication no
```

### <a name="disable-login-by-hello-root-user"></a><span data-ttu-id="56460-110">Disabilitare l'account di accesso per l'utente root hello</span><span class="sxs-lookup"><span data-stu-id="56460-110">Disable login by hello root user</span></span>

```bash
PermitRootLogin no
```

### <a name="allowed-groups-list"></a><span data-ttu-id="56460-111">Elenco di gruppi consentiti</span><span class="sxs-lookup"><span data-stu-id="56460-111">Allowed groups list</span></span>

```bash
AllowGroups wheel
```

### <a name="allowed-users-list"></a><span data-ttu-id="56460-112">Elenco di utenti consentiti</span><span class="sxs-lookup"><span data-stu-id="56460-112">Allowed users list</span></span>

```bash
AllowUsers ahmet ralph
```

### <a name="disable-ssh-protocol-version-1"></a><span data-ttu-id="56460-113">Disabilitare la versione 1 del protocollo SSH</span><span class="sxs-lookup"><span data-stu-id="56460-113">Disable SSH protocol version 1</span></span>

```bash
Protocol 2
```

### <a name="minimum-key-bits"></a><span data-ttu-id="56460-114">Bit minimi della chiave</span><span class="sxs-lookup"><span data-stu-id="56460-114">Minimum key bits</span></span>

```bash
ServerKeyBits 2048
```

### <a name="disconnect-idle-users"></a><span data-ttu-id="56460-115">Disconnettere gli utenti inattivi</span><span class="sxs-lookup"><span data-stu-id="56460-115">Disconnect idle users</span></span>

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="56460-116">Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="56460-116">Detailed Walkthrough</span></span>

<span data-ttu-id="56460-117">SSHD è hello Server SSH in esecuzione su hello VM Linux.</span><span class="sxs-lookup"><span data-stu-id="56460-117">SSHD is hello SSH Server that runs on hello Linux VM.</span></span>  <span data-ttu-id="56460-118">SSH è un client eseguito da una shell nella workstation MacBook o Linux o tramite bash in Windows.</span><span class="sxs-lookup"><span data-stu-id="56460-118">SSH is a client that runs from a shell on your MacBook, Linux workstation, or from a Bash on Windows.</span></span>  <span data-ttu-id="56460-119">SSH è anche il protocollo di hello utilizzato toosecure e crittografare le comunicazioni hello tra la workstation e hello VM Linux effettua SSH anche una connessione VPN (Virtual Private Network).</span><span class="sxs-lookup"><span data-stu-id="56460-119">SSH is also hello protocol used toosecure and encrypt hello communication between your workstation and hello Linux VM making SSH also a VPN (Virtual Private Network).</span></span>

<span data-ttu-id="56460-120">Per questo articolo, è molto importante tookeep tooyour di un account di accesso VM Linux aprire per la procedura dettagliata intera hello.</span><span class="sxs-lookup"><span data-stu-id="56460-120">For this article, it is very important tookeep one login tooyour Linux VM open for hello entire walk-through.</span></span>  <span data-ttu-id="56460-121">Una volta stabilita una connessione SSH, rimane una sessione aperta fino a quando non viene chiusa la finestra hello.</span><span class="sxs-lookup"><span data-stu-id="56460-121">Once an SSH connection is established, it remains as an open session as long as hello window is not closed.</span></span>  <span data-ttu-id="56460-122">Con un unico terminale connesso, consente le modifiche apportate toobe toohello service SSHD senza essere bloccato se viene apportata una modifica di rilievo.</span><span class="sxs-lookup"><span data-stu-id="56460-122">Having one terminal logged in, allows for changes toobe made toohello SSHD service without being locked out if a breaking change is made.</span></span>  <span data-ttu-id="56460-123">Se restare bloccati senza accesso VM Linux con una configurazione SSHD interrotta, Azure offre una configurazione SSHD interrotta con hello hello possibilità tooreset [estensione accesso alle macchine Virtuali di Azure](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="56460-123">If you do get locked out of your Linux VM with a broken SSHD configuration, Azure offers hello ability tooreset a broken SSHD configuration with hello [Azure VM Access Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="56460-124">Per questo motivo è aprire due terminali e SSH toohello VM Linux da entrambi gli elementi.</span><span class="sxs-lookup"><span data-stu-id="56460-124">For this reason we open two terminals and SSH toohello Linux VM from both of them.</span></span>  <span data-ttu-id="56460-125">È utilizzare hello primo toomake terminal hello modifiche tooSSHDs file di configurazione e riavviare il servizio SSHD hello.</span><span class="sxs-lookup"><span data-stu-id="56460-125">We use hello first terminal toomake hello changes tooSSHDs configuration file and restart hello SSHD service.</span></span>  <span data-ttu-id="56460-126">Utilizziamo hello tootest terminal secondo le modifiche dopo aver riavviato il servizio di hello.</span><span class="sxs-lookup"><span data-stu-id="56460-126">We use hello second terminal tootest those changes once hello service is restarted.</span></span>  <span data-ttu-id="56460-127">Poiché ci stiamo disabilitazione password SSH e basarsi esclusivamente sulle chiavi SSH, se le chiavi SSH non sono corrette e si chiude hello connessione toohello VM, hello VM verrà definitivamente bloccato e non sarà in grado di toologin tooit richiederla toobe eliminato e ricreato.</span><span class="sxs-lookup"><span data-stu-id="56460-127">Because we are disabling SSH passwords and relying strictly on SSH keys, if your SSH keys are not correct and you close hello connection toohello VM, hello VM will be permanently locked and no one will be able toologin tooit requiring it toobe deleted and recreated.</span></span>

## <a name="disable-password-logins"></a><span data-ttu-id="56460-128">Disabilitare gli accessi tramite password</span><span class="sxs-lookup"><span data-stu-id="56460-128">Disable password logins</span></span>

<span data-ttu-id="56460-129">Hello toosecure modo più rapido è VM Linux sia gli account di accesso di toodisable password.</span><span class="sxs-lookup"><span data-stu-id="56460-129">hello quickest way toosecure you Linux VM is toodisable password logins.</span></span>  <span data-ttu-id="56460-130">Quando sono abilitati gli account di accesso di password, BOT eseguono la ricerca per indicizzazione web hello avvierà immediatamente il tentativo di toobrute imporre password hello ipotesi per le VM Linux con SSH.</span><span class="sxs-lookup"><span data-stu-id="56460-130">When password logins are enabled, bots crawling hello web will immediately start attempting toobrute force guess hello password for your Linux VM using SSH.</span></span>  <span data-ttu-id="56460-131">La disabilitazione di un account di accesso password completamente, Abilita hello SSH server tooignore tutti i tentativi di accesso di password.</span><span class="sxs-lookup"><span data-stu-id="56460-131">Disabling password logins completely, enables hello SSH server tooignore all password login attempts.</span></span>

```bash
PasswordAuthentication no
```

## <a name="disable-login-by-hello-root-user"></a><span data-ttu-id="56460-132">Disabilitare l'account di accesso per l'utente root hello</span><span class="sxs-lookup"><span data-stu-id="56460-132">Disable login by hello root user</span></span>

<span data-ttu-id="56460-133">Linux procedure consigliate seguenti, hello `root` utente non deve essere registrato in mai tramite SSH o utilizzando `sudo su`.</span><span class="sxs-lookup"><span data-stu-id="56460-133">Following Linux best practices, hello `root` user should never be logged into over SSH or using `sudo su`.</span></span>  <span data-ttu-id="56460-134">Tutti i comandi che richiedono autorizzazioni a livello di radice devono sempre essere eseguiti tramite hello `sudo` comando, che registra tutte le azioni di controllo futuro.</span><span class="sxs-lookup"><span data-stu-id="56460-134">All commands needing root level permissions should always be run through hello `sudo` command, which logs all actions for future auditing.</span></span>  <span data-ttu-id="56460-135">Disabilitazione hello `root` utente di accesso tramite SSH è un passaggio di procedure consigliate migliore sicurezza che assicura tooSSH può solo da utenti autorizzati.</span><span class="sxs-lookup"><span data-stu-id="56460-135">Disabling hello `root` user from logging in via SSH is a security best practices step that ensures only authorized users are allowed tooSSH.</span></span>

```bash
PermitRootLogin no
```

## <a name="allowed-groups-list"></a><span data-ttu-id="56460-136">Elenco di gruppi consentiti</span><span class="sxs-lookup"><span data-stu-id="56460-136">Allowed groups list</span></span>

<span data-ttu-id="56460-137">SSH offre un metodo per limitare gli utenti e i gruppi dotati o meno di autorizzazioni per l'accesso a SSH.</span><span class="sxs-lookup"><span data-stu-id="56460-137">SSH offers a method of restricting users and group that are allowed or disallowed from logging in over SSH.</span></span>  <span data-ttu-id="56460-138">Questa funzionalità utilizza tooapprove elenchi o deny per gli utenti e gruppi di accesso.</span><span class="sxs-lookup"><span data-stu-id="56460-138">This feature uses lists tooapprove or deny specific users and groups from logging in.</span></span>  <span data-ttu-id="56460-139">Impostazione hello rotellina gruppo toohello `AllowGroups` elenco limita gli account di accesso approvato su SSH toojust gli account utente nel gruppo rotellina hello.</span><span class="sxs-lookup"><span data-stu-id="56460-139">Setting hello wheel group toohello `AllowGroups` list restricts approved logins over SSH toojust user accounts that are in hello wheel group.</span></span>

```bash
AllowGroups wheel
```

## <a name="allowed-users-list"></a><span data-ttu-id="56460-140">Elenco di utenti consentiti</span><span class="sxs-lookup"><span data-stu-id="56460-140">Allowed users list</span></span>

<span data-ttu-id="56460-141">Limitare gli utenti di toojust gli account di accesso SSH è un modo più specifico tooaccomplish hello stessa attività `AllowGroups` è.</span><span class="sxs-lookup"><span data-stu-id="56460-141">Restricting SSH logins toojust users is a more specific way tooaccomplish hello same task that `AllowGroups` is.</span></span>  

```bash
AllowUsers ahmet ralph
```

## <a name="disable-ssh-protocol-version-1"></a><span data-ttu-id="56460-142">Disabilitare la versione 1 del protocollo SSH</span><span class="sxs-lookup"><span data-stu-id="56460-142">Disable SSH protocol version 1</span></span>

<span data-ttu-id="56460-143">La versione 1 del protocollo SSH non è sicura ed è consigliabile disabilitarla.</span><span class="sxs-lookup"><span data-stu-id="56460-143">SSH protocol version 1 is insecure and should be disabled.</span></span>  <span data-ttu-id="56460-144">Versione 2 del protocollo SSH è una versione corrente di hello che offre un server di tooyour tooSSH in modo sicuro.</span><span class="sxs-lookup"><span data-stu-id="56460-144">SSH protocol version 2 is hello current version that offers a secure way tooSSH tooyour server.</span></span>  <span data-ttu-id="56460-145">La disabilitazione di SSH versione 1 Nega qualsiasi client SSH che tentano di tooestablish una connessione con server SSH hello con SSH versione 1.</span><span class="sxs-lookup"><span data-stu-id="56460-145">Disabling SSH version 1 denies any SSH clients that are attempting tooestablish a connection with hello SSH server using SSH version 1.</span></span>  <span data-ttu-id="56460-146">Solo le connessioni di SSH versione 2 sono consentite toonegotiate una connessione con server SSH hello.</span><span class="sxs-lookup"><span data-stu-id="56460-146">Only SSH version 2 connections are allowed toonegotiate a connection with hello SSH server.</span></span>

```bash
Protocol 2
```

## <a name="minimum-key-bits"></a><span data-ttu-id="56460-147">Bit minimi della chiave</span><span class="sxs-lookup"><span data-stu-id="56460-147">Minimum key bits</span></span>

<span data-ttu-id="56460-148">Procedure ottimali di protezione, gli account di accesso di password SSH sono disabilitate e sono consentite solo le chiavi SSH toobe utilizzato tooauthenticate con server SSH hello.</span><span class="sxs-lookup"><span data-stu-id="56460-148">Following security best practices, password SSH logins are disabled and only SSH keys are allowed toobe used tooauthenticate with hello SSH server.</span></span>  <span data-ttu-id="56460-149">È possibile creare le chiavi SSH usando chiavi di lunghezza diversa misurate in bit.</span><span class="sxs-lookup"><span data-stu-id="56460-149">These SSH keys can be created using different length keys, measured in bits.</span></span>  <span data-ttu-id="56460-150">Procedure consigliate di stati che le chiavi di lunghezza pari a 2048 bit sono hello minimo accettabile livello di attendibilità.</span><span class="sxs-lookup"><span data-stu-id="56460-150">Best practices states that keys of 2048 bits in length are hello minimum acceptable key strength.</span></span>  <span data-ttu-id="56460-151">Chiavi inferiori a 2048 bit potrebbero teoricamente non funzionare.</span><span class="sxs-lookup"><span data-stu-id="56460-151">Keys of less than 2048 bits could theoretically be broken.</span></span>  <span data-ttu-id="56460-152">Hello impostazione `ServerKeyBits` troppo`2048` consente tutte le connessioni utilizzando le chiavi di 2048 bit o superiore e negare le connessioni di meno di 2048 bit.</span><span class="sxs-lookup"><span data-stu-id="56460-152">Setting hello `ServerKeyBits` too`2048` allows any connections using keys of 2048 bits or greater and deny connections of less than 2048 bits.</span></span>

```bash
ServerKeyBits 2048
```

## <a name="disconnect-idle-users"></a><span data-ttu-id="56460-153">Disconnettere gli utenti inattivi</span><span class="sxs-lookup"><span data-stu-id="56460-153">Disconnect idle users</span></span>

<span data-ttu-id="56460-154">SSH con gli utenti toodisconnect hello possibilità che le connessioni aperte che sono rimaste inattive per più di un determinato periodo di secondi.</span><span class="sxs-lookup"><span data-stu-id="56460-154">SSH has hello ability toodisconnect users that have open connections that have remained idle for more than a set period of seconds.</span></span>  <span data-ttu-id="56460-155">Mantenere sessioni aperte tooonly gli utenti che sono l'esposizione di hello active limiti di hello VM Linux.</span><span class="sxs-lookup"><span data-stu-id="56460-155">Keeping open sessions tooonly those users who are active limits hello exposure of hello Linux VM.</span></span>

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="restart-sshd"></a><span data-ttu-id="56460-156">Riavviare SSHD</span><span class="sxs-lookup"><span data-stu-id="56460-156">Restart SSHD</span></span>

<span data-ttu-id="56460-157">impostazioni hello tooenable `/etc/ssh/sshd_config` riavvio del processo SSHD hello che riavvia server SSH hello.</span><span class="sxs-lookup"><span data-stu-id="56460-157">tooenable hello settings in `/etc/ssh/sshd_config` restart hello SSHD process which restarts hello SSH server.</span></span>  <span data-ttu-id="56460-158">finestra terminale di Hello è utilizzare toorestart hello SSH server rimangono aperti senza perdere sessione SSH aperta hello.</span><span class="sxs-lookup"><span data-stu-id="56460-158">hello terminal window you use toorestart hello SSH server remain open without losing hello open SSH session.</span></span>  <span data-ttu-id="56460-159">tootest hello SSH impostazioni del nuovo server utilizzano una seconda finestra terminale o una scheda.  L'utilizzo di un connessione SSH di hello tootest terminal separato consente toogo indietro e apportare altre modifiche toohello `/etc/ssh/sshd_config` terminal prima di hello, senza essere bloccato da una modifica di rilievo SSHD.</span><span class="sxs-lookup"><span data-stu-id="56460-159">tootest hello new SSH server settings use a second terminal window or tab.  Using a separate terminal tootest hello SSH connection allows you toogo back and make additional changes toohello `/etc/ssh/sshd_config` in hello first terminal, without being locked out by a breaking SSHD change.</span></span>  

### <a name="on-redhat-centos-and-fedora"></a><span data-ttu-id="56460-160">Per Redhat, Centos e Fedora</span><span class="sxs-lookup"><span data-stu-id="56460-160">On Redhat, Centos and Fedora</span></span>

```bash
service sshd restart
```

### <a name="on-debian--ubuntu"></a><span data-ttu-id="56460-161">Per Debian e Ubuntu</span><span class="sxs-lookup"><span data-stu-id="56460-161">On Debian & Ubuntu</span></span>

```bash
service ssh restart
```

## <a name="reset-sshd-using-azure-reset-access"></a><span data-ttu-id="56460-162">Reimpostare SSHD usando il comando reset-access di Azure</span><span class="sxs-lookup"><span data-stu-id="56460-162">Reset SSHD using Azure reset-access</span></span>

<span data-ttu-id="56460-163">Se sono bloccati da una configurazione di rilievo modifica toohello SSHD hello estensione di macchina virtuale di Azure access tooreset hello SSHD configurazione toohello indietro originale configurazione consente.</span><span class="sxs-lookup"><span data-stu-id="56460-163">If you are locked out from a breaking change toohello SSHD configuration you can use hello Azure VM access-extension tooreset hello SSHD configuration back toohello original configuration.</span></span>

<span data-ttu-id="56460-164">Sostituire i nomi nell'esempio con quelli personalizzati.</span><span class="sxs-lookup"><span data-stu-id="56460-164">Replace any example names with your own.</span></span>

```azurecli
azure vm reset-access \
--resource-group myResourceGroup \
--name myVM \
--reset-ssh
```

## <a name="install-fail2ban"></a><span data-ttu-id="56460-165">Installare Fail2ban</span><span class="sxs-lookup"><span data-stu-id="56460-165">Install Fail2ban</span></span>

<span data-ttu-id="56460-166">È consigliabile tooinstall e il programma di installazione Apri origine app hello Fail2ban, quali blocchi ripetuti tentativi toologin tooyour VM Linux su SSH tramite forza bruta.</span><span class="sxs-lookup"><span data-stu-id="56460-166">It is strongly recommended tooinstall and setup hello open source app Fail2ban, which blocks repeated attempts toologin tooyour Linux VM over SSH using brute force.</span></span>  <span data-ttu-id="56460-167">I registri di Fail2ban ripetuti failover tentativi toologin SSH e quindi crea regole del firewall l'indirizzo IP di hello tooblock che hello tentativi provengano da.</span><span class="sxs-lookup"><span data-stu-id="56460-167">Fail2ban logs repeated failed attempts toologin over SSH and then creates firewall rules tooblock hello IP address that hello attempts are originating from.</span></span>

* [<span data-ttu-id="56460-168">Homepage di Fail2ban</span><span class="sxs-lookup"><span data-stu-id="56460-168">Fail2ban homepage</span></span>](http://www.fail2ban.org/wiki/index.php/Main_Page)

## <a name="next-steps"></a><span data-ttu-id="56460-169">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="56460-169">Next Steps</span></span>

<span data-ttu-id="56460-170">Dopo aver configurato e bloccati a server SSH hello nella VM Linux sono presenti procedure consigliate di sicurezza aggiuntive che è possibile seguire.</span><span class="sxs-lookup"><span data-stu-id="56460-170">Now that you have configured and locked down hello SSH server on your Linux VM there are additional security best practices you can follow.</span></span>  

* [<span data-ttu-id="56460-171">Gestire utenti, SSH e controllo o i dischi di ripristino di macchine virtuali Linux di Azure utilizzando hello estensione VMAccess</span><span class="sxs-lookup"><span data-stu-id="56460-171">Manage users, SSH, and check or repair disks on Azure Linux VMs using hello VMAccess Extension</span></span>](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [<span data-ttu-id="56460-172">Crittografare i dischi in una VM Linux utilizzando hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="56460-172">Encrypt disks on a Linux VM using hello Azure CLI</span></span>](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [<span data-ttu-id="56460-173">Accesso e sicurezza nei modelli di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="56460-173">Access and security in Azure Resource Manager templates</span></span>](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
