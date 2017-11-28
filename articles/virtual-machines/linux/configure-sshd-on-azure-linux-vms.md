---
title: Configurare SSHD nelle macchine virtuali Linux di Azure | Documentazione Microsoft
description: Configurare SSHD per le procedure di sicurezza consigliate e per bloccare SSH nelle macchine virtuali Linux di Azure.
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
ms.openlocfilehash: 0195c385b00ab92b2b92ce8ff00983a0d91bf3a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="configure-sshd-on-azure-linux-vms"></a><span data-ttu-id="73b05-103">Configurare SSHD nelle macchine virtuali Linux di Azure</span><span class="sxs-lookup"><span data-stu-id="73b05-103">Configure SSHD on Azure Linux VMs</span></span>

<span data-ttu-id="73b05-104">Questo articolo illustra come bloccare il server SSH in Linux, come fornire procedure di sicurezza consigliate e come accelerare l'accesso al server SSH con chiavi SSH anziché password.</span><span class="sxs-lookup"><span data-stu-id="73b05-104">This article shows how to lockdown the SSH Server on Linux, to provide best practices security and also to speed up the SSH login process by using SSH keys instead of passwords.</span></span>  <span data-ttu-id="73b05-105">Per bloccare SSHD viene disabilitata la capacità di accesso dell'utente root, vengono limitati gli utenti autorizzati ad accedere tramite l'elenco di gruppi approvati, viene disabilitata la versione 1 del protocollo SSH, viene impostato un numero minimo di bit per la chiave e infine configurata la disconnessione automatica degli utenti inattivi.</span><span class="sxs-lookup"><span data-stu-id="73b05-105">To further lockdown SSHD we are going to disable the root user from being able to login, limit the users that are allowed to login via an approved group list, disabling SSH protocol version 1, set a minimum key bit, and configure auto-logout of idle users.</span></span>  <span data-ttu-id="73b05-106">Prerequisiti necessari: un account Azure (è possibile [ottenere una versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/)) e i [file delle chiavi SSH pubbliche e private](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="73b05-106">The requirements for this article are: an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)) and [SSH public and private key files](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="73b05-107">Comandi rapidi</span><span class="sxs-lookup"><span data-stu-id="73b05-107">Quick Commands</span></span>

<span data-ttu-id="73b05-108">Configurare `/etc/ssh/sshd_config` con le seguenti impostazioni:</span><span class="sxs-lookup"><span data-stu-id="73b05-108">Configure `/etc/ssh/sshd_config` with the following settings:</span></span>

### <a name="disable-password-logins"></a><span data-ttu-id="73b05-109">Disabilitare gli accessi tramite password</span><span class="sxs-lookup"><span data-stu-id="73b05-109">Disable password logins</span></span>

```bash
PasswordAuthentication no
```

### <a name="disable-login-by-the-root-user"></a><span data-ttu-id="73b05-110">Disabilitare l'accesso per l'utente root</span><span class="sxs-lookup"><span data-stu-id="73b05-110">Disable login by the root user</span></span>

```bash
PermitRootLogin no
```

### <a name="allowed-groups-list"></a><span data-ttu-id="73b05-111">Elenco di gruppi consentiti</span><span class="sxs-lookup"><span data-stu-id="73b05-111">Allowed groups list</span></span>

```bash
AllowGroups wheel
```

### <a name="allowed-users-list"></a><span data-ttu-id="73b05-112">Elenco di utenti consentiti</span><span class="sxs-lookup"><span data-stu-id="73b05-112">Allowed users list</span></span>

```bash
AllowUsers ahmet ralph
```

### <a name="disable-ssh-protocol-version-1"></a><span data-ttu-id="73b05-113">Disabilitare la versione 1 del protocollo SSH</span><span class="sxs-lookup"><span data-stu-id="73b05-113">Disable SSH protocol version 1</span></span>

```bash
Protocol 2
```

### <a name="minimum-key-bits"></a><span data-ttu-id="73b05-114">Bit minimi della chiave</span><span class="sxs-lookup"><span data-stu-id="73b05-114">Minimum key bits</span></span>

```bash
ServerKeyBits 2048
```

### <a name="disconnect-idle-users"></a><span data-ttu-id="73b05-115">Disconnettere gli utenti inattivi</span><span class="sxs-lookup"><span data-stu-id="73b05-115">Disconnect idle users</span></span>

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="73b05-116">Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="73b05-116">Detailed Walkthrough</span></span>

<span data-ttu-id="73b05-117">SSHD è il server SSH eseguito nella VM Linux.</span><span class="sxs-lookup"><span data-stu-id="73b05-117">SSHD is the SSH Server that runs on the Linux VM.</span></span>  <span data-ttu-id="73b05-118">SSH è un client eseguito da una shell nella workstation MacBook o Linux o tramite bash in Windows.</span><span class="sxs-lookup"><span data-stu-id="73b05-118">SSH is a client that runs from a shell on your MacBook, Linux workstation, or from a Bash on Windows.</span></span>  <span data-ttu-id="73b05-119">SSH è anche il protocollo usato per proteggere e crittografare le comunicazioni tra la workstation e la VM Linux, ed è pertanto anche una rete privata virtuale (VPN, Virtual Private Network).</span><span class="sxs-lookup"><span data-stu-id="73b05-119">SSH is also the protocol used to secure and encrypt the communication between your workstation and the Linux VM making SSH also a VPN (Virtual Private Network).</span></span>

<span data-ttu-id="73b05-120">Ai fini di questo articolo è molto importante mantenere aperto un accesso alla VM Linux per l'intera procedura.</span><span class="sxs-lookup"><span data-stu-id="73b05-120">For this article, it is very important to keep one login to your Linux VM open for the entire walk-through.</span></span>  <span data-ttu-id="73b05-121">Dopo aver stabilito la connessione SSH, la sessione rimane aperta fino a quando la finestra non viene chiusa.</span><span class="sxs-lookup"><span data-stu-id="73b05-121">Once an SSH connection is established, it remains as an open session as long as the window is not closed.</span></span>  <span data-ttu-id="73b05-122">La connessione di un terminale consente di apportare le modifiche al servizio SSHD senza rimanere bloccati se viene apportata una modifica di rilievo.</span><span class="sxs-lookup"><span data-stu-id="73b05-122">Having one terminal logged in, allows for changes to be made to the SSHD service without being locked out if a breaking change is made.</span></span>  <span data-ttu-id="73b05-123">Se la VM Linux viene bloccata da una configurazione SSHD interrotta, Azure consente di reimpostare la configurazione SSHD interrotta con l'[estensione dell'accesso alle macchine virtuali di Azure](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="73b05-123">If you do get locked out of your Linux VM with a broken SSHD configuration, Azure offers the ability to reset a broken SSHD configuration with the [Azure VM Access Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="73b05-124">Per questo motivo vengono aperti due terminali che usano entrambi SSH per comunicare con la VM Linux.</span><span class="sxs-lookup"><span data-stu-id="73b05-124">For this reason we open two terminals and SSH to the Linux VM from both of them.</span></span>  <span data-ttu-id="73b05-125">Il primo terminale viene usato per apportare modifiche al file di configurazione SSHD e per riavviare il servizio SSHD.</span><span class="sxs-lookup"><span data-stu-id="73b05-125">We use the first terminal to make the changes to SSHDs configuration file and restart the SSHD service.</span></span>  <span data-ttu-id="73b05-126">Il secondo terminale viene usato per testare le modifiche apportate dopo il riavvio del servizio.</span><span class="sxs-lookup"><span data-stu-id="73b05-126">We use the second terminal to test those changes once the service is restarted.</span></span>  <span data-ttu-id="73b05-127">Poiché si eseguirà la disabilitazione delle password SSH e ci si affiderà esclusivamente alle chiavi SSH, se le chiavi SSH non sono corrette e si chiude la connessione alla VM, quest'ultima verrà definitivamente bloccata. Nessuno sarà più in grado di accedervi e la macchina virtuale dovrà essere eliminata e ricreata.</span><span class="sxs-lookup"><span data-stu-id="73b05-127">Because we are disabling SSH passwords and relying strictly on SSH keys, if your SSH keys are not correct and you close the connection to the VM, the VM will be permanently locked and no one will be able to login to it requiring it to be deleted and recreated.</span></span>

## <a name="disable-password-logins"></a><span data-ttu-id="73b05-128">Disabilitare gli accessi tramite password</span><span class="sxs-lookup"><span data-stu-id="73b05-128">Disable password logins</span></span>

<span data-ttu-id="73b05-129">Il modo più rapido per proteggere la VM Linux è la disabilitazione degli accessi tramite password.</span><span class="sxs-lookup"><span data-stu-id="73b05-129">The quickest way to secure you Linux VM is to disable password logins.</span></span>  <span data-ttu-id="73b05-130">Quando gli accessi tramite password sono abilitati, i robot che circolano in rete tentano immediatamente di indovinare la password della VM Linux che usa SSH.</span><span class="sxs-lookup"><span data-stu-id="73b05-130">When password logins are enabled, bots crawling the web will immediately start attempting to brute force guess the password for your Linux VM using SSH.</span></span>  <span data-ttu-id="73b05-131">Disabilitando completamente l'accesso tramite password, il server SSH ignora tutti i tentativi di accesso di questo tipo.</span><span class="sxs-lookup"><span data-stu-id="73b05-131">Disabling password logins completely, enables the SSH server to ignore all password login attempts.</span></span>

```bash
PasswordAuthentication no
```

## <a name="disable-login-by-the-root-user"></a><span data-ttu-id="73b05-132">Disabilitare l'accesso per l'utente root</span><span class="sxs-lookup"><span data-stu-id="73b05-132">Disable login by the root user</span></span>

<span data-ttu-id="73b05-133">In base alle procedure Linux consigliate, l'`root`utente non dovrebbe mai accedere tramite SSH o con `sudo su`.</span><span class="sxs-lookup"><span data-stu-id="73b05-133">Following Linux best practices, the `root` user should never be logged into over SSH or using `sudo su`.</span></span>  <span data-ttu-id="73b05-134">Tutti i comandi che richiedono autorizzazioni root devono sempre essere eseguiti tramite il comando `sudo`, che registra ogni azione per eventuali controlli successivi.</span><span class="sxs-lookup"><span data-stu-id="73b05-134">All commands needing root level permissions should always be run through the `sudo` command, which logs all actions for future auditing.</span></span>  <span data-ttu-id="73b05-135">La disabilitazione dell'accesso dell'utente `root` a SSH è una procedura di sicurezza consigliata che garantisce l'accesso a SSH ai soli utenti autorizzati.</span><span class="sxs-lookup"><span data-stu-id="73b05-135">Disabling the `root` user from logging in via SSH is a security best practices step that ensures only authorized users are allowed to SSH.</span></span>

```bash
PermitRootLogin no
```

## <a name="allowed-groups-list"></a><span data-ttu-id="73b05-136">Elenco di gruppi consentiti</span><span class="sxs-lookup"><span data-stu-id="73b05-136">Allowed groups list</span></span>

<span data-ttu-id="73b05-137">SSH offre un metodo per limitare gli utenti e i gruppi dotati o meno di autorizzazioni per l'accesso a SSH.</span><span class="sxs-lookup"><span data-stu-id="73b05-137">SSH offers a method of restricting users and group that are allowed or disallowed from logging in over SSH.</span></span>  <span data-ttu-id="73b05-138">Questa funzionalità usa gli elenchi per concedere o negare l'accesso a utenti e gruppi specifici.</span><span class="sxs-lookup"><span data-stu-id="73b05-138">This feature uses lists to approve or deny specific users and groups from logging in.</span></span>  <span data-ttu-id="73b05-139">Inserendo il gruppo wheel nell'elenco `AllowGroups` si limitano gli accessi a SSH solo agli account utente presenti in tale gruppo.</span><span class="sxs-lookup"><span data-stu-id="73b05-139">Setting the wheel group to the `AllowGroups` list restricts approved logins over SSH to just user accounts that are in the wheel group.</span></span>

```bash
AllowGroups wheel
```

## <a name="allowed-users-list"></a><span data-ttu-id="73b05-140">Elenco di utenti consentiti</span><span class="sxs-lookup"><span data-stu-id="73b05-140">Allowed users list</span></span>

<span data-ttu-id="73b05-141">Limitare gli accessi a SSH solo agli utenti è un metodo più specifico rispetto ad `AllowGroups` per ottenere lo stesso risultato.</span><span class="sxs-lookup"><span data-stu-id="73b05-141">Restricting SSH logins to just users is a more specific way to accomplish the same task that `AllowGroups` is.</span></span>  

```bash
AllowUsers ahmet ralph
```

## <a name="disable-ssh-protocol-version-1"></a><span data-ttu-id="73b05-142">Disabilitare la versione 1 del protocollo SSH</span><span class="sxs-lookup"><span data-stu-id="73b05-142">Disable SSH protocol version 1</span></span>

<span data-ttu-id="73b05-143">La versione 1 del protocollo SSH non è sicura ed è consigliabile disabilitarla.</span><span class="sxs-lookup"><span data-stu-id="73b05-143">SSH protocol version 1 is insecure and should be disabled.</span></span>  <span data-ttu-id="73b05-144">La versione 2 è la versione corrente, e offre una modalità di connessione SSH sicura al server.</span><span class="sxs-lookup"><span data-stu-id="73b05-144">SSH protocol version 2 is the current version that offers a secure way to SSH to your server.</span></span>  <span data-ttu-id="73b05-145">Disabilitando la versione 1 di SSH si impedisce ai client SSH che tentano di connettersi al server SSH di usare la versione 1.</span><span class="sxs-lookup"><span data-stu-id="73b05-145">Disabling SSH version 1 denies any SSH clients that are attempting to establish a connection with the SSH server using SSH version 1.</span></span>  <span data-ttu-id="73b05-146">Solo le connessioni che avvengono tramite la versione 2 di SSH possono così negoziare la connessione al server SSH.</span><span class="sxs-lookup"><span data-stu-id="73b05-146">Only SSH version 2 connections are allowed to negotiate a connection with the SSH server.</span></span>

```bash
Protocol 2
```

## <a name="minimum-key-bits"></a><span data-ttu-id="73b05-147">Bit minimi della chiave</span><span class="sxs-lookup"><span data-stu-id="73b05-147">Minimum key bits</span></span>

<span data-ttu-id="73b05-148">Secondo le procedure di sicurezza consigliate, gli accessi tramite password SSH sono disattivati e l'autenticazione al server SSH è consentita solo tramite l'uso delle chiavi SSH.</span><span class="sxs-lookup"><span data-stu-id="73b05-148">Following security best practices, password SSH logins are disabled and only SSH keys are allowed to be used to authenticate with the SSH server.</span></span>  <span data-ttu-id="73b05-149">È possibile creare le chiavi SSH usando chiavi di lunghezza diversa misurate in bit.</span><span class="sxs-lookup"><span data-stu-id="73b05-149">These SSH keys can be created using different length keys, measured in bits.</span></span>  <span data-ttu-id="73b05-150">Le procedure di sicurezza consigliate indicano che la lunghezza minima per ottenere una complessità accettabile della chiave è di 2048 bit.</span><span class="sxs-lookup"><span data-stu-id="73b05-150">Best practices states that keys of 2048 bits in length are the minimum acceptable key strength.</span></span>  <span data-ttu-id="73b05-151">Chiavi inferiori a 2048 bit potrebbero teoricamente non funzionare.</span><span class="sxs-lookup"><span data-stu-id="73b05-151">Keys of less than 2048 bits could theoretically be broken.</span></span>  <span data-ttu-id="73b05-152">Impostare `ServerKeyBits` su `2048` consente qualsiasi connessione che utilizza chiavi pari o superiori a 2048 bit e impedisce quelle con un numero di bit inferiori a 2048.</span><span class="sxs-lookup"><span data-stu-id="73b05-152">Setting the `ServerKeyBits` to `2048` allows any connections using keys of 2048 bits or greater and deny connections of less than 2048 bits.</span></span>

```bash
ServerKeyBits 2048
```

## <a name="disconnect-idle-users"></a><span data-ttu-id="73b05-153">Disconnettere gli utenti inattivi</span><span class="sxs-lookup"><span data-stu-id="73b05-153">Disconnect idle users</span></span>

<span data-ttu-id="73b05-154">SSH consente di disconnettere gli utenti con connessioni aperte che restano inattivi per un numero di secondi superiore rispetto a quello stabilito.</span><span class="sxs-lookup"><span data-stu-id="73b05-154">SSH has the ability to disconnect users that have open connections that have remained idle for more than a set period of seconds.</span></span>  <span data-ttu-id="73b05-155">Mantenere aperte le sessioni ai soli utenti attivi limita l'esposizione delle VM Linux.</span><span class="sxs-lookup"><span data-stu-id="73b05-155">Keeping open sessions to only those users who are active limits the exposure of the Linux VM.</span></span>

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="restart-sshd"></a><span data-ttu-id="73b05-156">Riavviare SSHD</span><span class="sxs-lookup"><span data-stu-id="73b05-156">Restart SSHD</span></span>

<span data-ttu-id="73b05-157">Per abilitare le impostazioni in `/etc/ssh/sshd_config`, riavviare il processo SSHD, che a sua volta riavvia il server SSH.</span><span class="sxs-lookup"><span data-stu-id="73b05-157">To enable the settings in `/etc/ssh/sshd_config` restart the SSHD process which restarts the SSH server.</span></span>  <span data-ttu-id="73b05-158">La finestra del terminale usata per riavviare il server SSH resta aperta, senza perdere la sessione SSH aperta.</span><span class="sxs-lookup"><span data-stu-id="73b05-158">The terminal window you use to restart the SSH server remain open without losing the open SSH session.</span></span>  <span data-ttu-id="73b05-159">Per testare le nuove impostazioni del server SSH, usare una seconda finestra o scheda del terminale.</span><span class="sxs-lookup"><span data-stu-id="73b05-159">To test the new SSH server settings use a second terminal window or tab.</span></span>  <span data-ttu-id="73b05-160">L'utilizzo di un terminale distinto per testare la connessione SSH consente di tornare indietro e apportare modifiche aggiuntive a `/etc/ssh/sshd_config`, senza rimanere bloccati se viene apportata una modifica di rilievo a SSHD.</span><span class="sxs-lookup"><span data-stu-id="73b05-160">Using a separate terminal to test the SSH connection allows you to go back and make additional changes to the `/etc/ssh/sshd_config` in the first terminal, without being locked out by a breaking SSHD change.</span></span>  

### <a name="on-redhat-centos-and-fedora"></a><span data-ttu-id="73b05-161">Per Redhat, Centos e Fedora</span><span class="sxs-lookup"><span data-stu-id="73b05-161">On Redhat, Centos and Fedora</span></span>

```bash
service sshd restart
```

### <a name="on-debian--ubuntu"></a><span data-ttu-id="73b05-162">Per Debian e Ubuntu</span><span class="sxs-lookup"><span data-stu-id="73b05-162">On Debian & Ubuntu</span></span>

```bash
service ssh restart
```

## <a name="reset-sshd-using-azure-reset-access"></a><span data-ttu-id="73b05-163">Reimpostare SSHD usando il comando reset-access di Azure</span><span class="sxs-lookup"><span data-stu-id="73b05-163">Reset SSHD using Azure reset-access</span></span>

<span data-ttu-id="73b05-164">Se si viene bloccati da una modifica di rilievo alla configurazione SSHD è possibile usare l'estensione di accesso della macchina virtuale di Azure per ripristinare la configurazione SSHD a quella originale.</span><span class="sxs-lookup"><span data-stu-id="73b05-164">If you are locked out from a breaking change to the SSHD configuration you can use the Azure VM access-extension to reset the SSHD configuration back to the original configuration.</span></span>

<span data-ttu-id="73b05-165">Sostituire i nomi nell'esempio con quelli personalizzati.</span><span class="sxs-lookup"><span data-stu-id="73b05-165">Replace any example names with your own.</span></span>

```azurecli
azure vm reset-access \
--resource-group myResourceGroup \
--name myVM \
--reset-ssh
```

## <a name="install-fail2ban"></a><span data-ttu-id="73b05-166">Installare Fail2ban</span><span class="sxs-lookup"><span data-stu-id="73b05-166">Install Fail2ban</span></span>

<span data-ttu-id="73b05-167">È consigliabile installare e configurare l'applicazione open source Fail2ban, che blocca i tentativi ripetuti di accesso alla VM Linux tramite SSH con l'uso della forza bruta.</span><span class="sxs-lookup"><span data-stu-id="73b05-167">It is strongly recommended to install and setup the open source app Fail2ban, which blocks repeated attempts to login to your Linux VM over SSH using brute force.</span></span>  <span data-ttu-id="73b05-168">Fail2ban registra i ripetuti tentativi non riusciti di accedere tramite SSH e quindi crea regole firewall per bloccare l'indirizzo IP dal quale hanno origine gli attacchi.</span><span class="sxs-lookup"><span data-stu-id="73b05-168">Fail2ban logs repeated failed attempts to login over SSH and then creates firewall rules to block the IP address that the attempts are originating from.</span></span>

* [<span data-ttu-id="73b05-169">Homepage di Fail2ban</span><span class="sxs-lookup"><span data-stu-id="73b05-169">Fail2ban homepage</span></span>](http://www.fail2ban.org/wiki/index.php/Main_Page)

## <a name="next-steps"></a><span data-ttu-id="73b05-170">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="73b05-170">Next Steps</span></span>

<span data-ttu-id="73b05-171">Dopo aver configurato e bloccato il server SSH nella VM Linux, è possibile eseguire alcune procedure di sicurezza aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="73b05-171">Now that you have configured and locked down the SSH server on your Linux VM there are additional security best practices you can follow.</span></span>  

* [<span data-ttu-id="73b05-172">Gestire utenti, SSH e dischi di controllo o di ripristino in VM Linux di Azure tramite l'estensione VMAccess</span><span class="sxs-lookup"><span data-stu-id="73b05-172">Manage users, SSH, and check or repair disks on Azure Linux VMs using the VMAccess Extension</span></span>](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [<span data-ttu-id="73b05-173">Crittografare i dischi di una VM Linux usando l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="73b05-173">Encrypt disks on a Linux VM using the Azure CLI</span></span>](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [<span data-ttu-id="73b05-174">Accesso e sicurezza nei modelli di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="73b05-174">Access and security in Azure Resource Manager templates</span></span>](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
