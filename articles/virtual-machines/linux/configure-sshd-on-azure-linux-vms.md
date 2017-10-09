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
# <a name="configure-sshd-on-azure-linux-vms"></a>Configurare SSHD nelle macchine virtuali Linux di Azure

Questo articolo illustra come toolockdown hello Server SSH in Linux, ottimizzare la sicurezza consigliate tooprovide e toospeed di processo di accesso SSH hello utilizzando le chiavi SSH anziché le password.  blocco toofurther SSHD verrà utente root di hello toodisable siano in grado di toologin, limitare gli utenti di hello consentiti toologin tramite un elenco di gruppi approvati, la disabilitazione di versione 1 del protocollo SSH, impostare una chiave minima di bit e configurare auto-disconnessione degli utenti inattivi.  requisiti di Hello per questo articolo sono: un account di Azure ([ottenere una versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/)) e [file chiavi SSH pubblica e privata](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="quick-commands"></a>Comandi rapidi

Configurare `/etc/ssh/sshd_config` con hello seguenti impostazioni:

### <a name="disable-password-logins"></a>Disabilitare gli accessi tramite password

```bash
PasswordAuthentication no
```

### <a name="disable-login-by-hello-root-user"></a>Disabilitare l'account di accesso per l'utente root hello

```bash
PermitRootLogin no
```

### <a name="allowed-groups-list"></a>Elenco di gruppi consentiti

```bash
AllowGroups wheel
```

### <a name="allowed-users-list"></a>Elenco di utenti consentiti

```bash
AllowUsers ahmet ralph
```

### <a name="disable-ssh-protocol-version-1"></a>Disabilitare la versione 1 del protocollo SSH

```bash
Protocol 2
```

### <a name="minimum-key-bits"></a>Bit minimi della chiave

```bash
ServerKeyBits 2048
```

### <a name="disconnect-idle-users"></a>Disconnettere gli utenti inattivi

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="detailed-walkthrough"></a>Procedura dettagliata

SSHD è hello Server SSH in esecuzione su hello VM Linux.  SSH è un client eseguito da una shell nella workstation MacBook o Linux o tramite bash in Windows.  SSH è anche il protocollo di hello utilizzato toosecure e crittografare le comunicazioni hello tra la workstation e hello VM Linux effettua SSH anche una connessione VPN (Virtual Private Network).

Per questo articolo, è molto importante tookeep tooyour di un account di accesso VM Linux aprire per la procedura dettagliata intera hello.  Una volta stabilita una connessione SSH, rimane una sessione aperta fino a quando non viene chiusa la finestra hello.  Con un unico terminale connesso, consente le modifiche apportate toobe toohello service SSHD senza essere bloccato se viene apportata una modifica di rilievo.  Se restare bloccati senza accesso VM Linux con una configurazione SSHD interrotta, Azure offre una configurazione SSHD interrotta con hello hello possibilità tooreset [estensione accesso alle macchine Virtuali di Azure](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Per questo motivo è aprire due terminali e SSH toohello VM Linux da entrambi gli elementi.  È utilizzare hello primo toomake terminal hello modifiche tooSSHDs file di configurazione e riavviare il servizio SSHD hello.  Utilizziamo hello tootest terminal secondo le modifiche dopo aver riavviato il servizio di hello.  Poiché ci stiamo disabilitazione password SSH e basarsi esclusivamente sulle chiavi SSH, se le chiavi SSH non sono corrette e si chiude hello connessione toohello VM, hello VM verrà definitivamente bloccato e non sarà in grado di toologin tooit richiederla toobe eliminato e ricreato.

## <a name="disable-password-logins"></a>Disabilitare gli accessi tramite password

Hello toosecure modo più rapido è VM Linux sia gli account di accesso di toodisable password.  Quando sono abilitati gli account di accesso di password, BOT eseguono la ricerca per indicizzazione web hello avvierà immediatamente il tentativo di toobrute imporre password hello ipotesi per le VM Linux con SSH.  La disabilitazione di un account di accesso password completamente, Abilita hello SSH server tooignore tutti i tentativi di accesso di password.

```bash
PasswordAuthentication no
```

## <a name="disable-login-by-hello-root-user"></a>Disabilitare l'account di accesso per l'utente root hello

Linux procedure consigliate seguenti, hello `root` utente non deve essere registrato in mai tramite SSH o utilizzando `sudo su`.  Tutti i comandi che richiedono autorizzazioni a livello di radice devono sempre essere eseguiti tramite hello `sudo` comando, che registra tutte le azioni di controllo futuro.  Disabilitazione hello `root` utente di accesso tramite SSH è un passaggio di procedure consigliate migliore sicurezza che assicura tooSSH può solo da utenti autorizzati.

```bash
PermitRootLogin no
```

## <a name="allowed-groups-list"></a>Elenco di gruppi consentiti

SSH offre un metodo per limitare gli utenti e i gruppi dotati o meno di autorizzazioni per l'accesso a SSH.  Questa funzionalità utilizza tooapprove elenchi o deny per gli utenti e gruppi di accesso.  Impostazione hello rotellina gruppo toohello `AllowGroups` elenco limita gli account di accesso approvato su SSH toojust gli account utente nel gruppo rotellina hello.

```bash
AllowGroups wheel
```

## <a name="allowed-users-list"></a>Elenco di utenti consentiti

Limitare gli utenti di toojust gli account di accesso SSH è un modo più specifico tooaccomplish hello stessa attività `AllowGroups` è.  

```bash
AllowUsers ahmet ralph
```

## <a name="disable-ssh-protocol-version-1"></a>Disabilitare la versione 1 del protocollo SSH

La versione 1 del protocollo SSH non è sicura ed è consigliabile disabilitarla.  Versione 2 del protocollo SSH è una versione corrente di hello che offre un server di tooyour tooSSH in modo sicuro.  La disabilitazione di SSH versione 1 Nega qualsiasi client SSH che tentano di tooestablish una connessione con server SSH hello con SSH versione 1.  Solo le connessioni di SSH versione 2 sono consentite toonegotiate una connessione con server SSH hello.

```bash
Protocol 2
```

## <a name="minimum-key-bits"></a>Bit minimi della chiave

Procedure ottimali di protezione, gli account di accesso di password SSH sono disabilitate e sono consentite solo le chiavi SSH toobe utilizzato tooauthenticate con server SSH hello.  È possibile creare le chiavi SSH usando chiavi di lunghezza diversa misurate in bit.  Procedure consigliate di stati che le chiavi di lunghezza pari a 2048 bit sono hello minimo accettabile livello di attendibilità.  Chiavi inferiori a 2048 bit potrebbero teoricamente non funzionare.  Hello impostazione `ServerKeyBits` troppo`2048` consente tutte le connessioni utilizzando le chiavi di 2048 bit o superiore e negare le connessioni di meno di 2048 bit.

```bash
ServerKeyBits 2048
```

## <a name="disconnect-idle-users"></a>Disconnettere gli utenti inattivi

SSH con gli utenti toodisconnect hello possibilità che le connessioni aperte che sono rimaste inattive per più di un determinato periodo di secondi.  Mantenere sessioni aperte tooonly gli utenti che sono l'esposizione di hello active limiti di hello VM Linux.

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="restart-sshd"></a>Riavviare SSHD

impostazioni hello tooenable `/etc/ssh/sshd_config` riavvio del processo SSHD hello che riavvia server SSH hello.  finestra terminale di Hello è utilizzare toorestart hello SSH server rimangono aperti senza perdere sessione SSH aperta hello.  tootest hello SSH impostazioni del nuovo server utilizzano una seconda finestra terminale o una scheda.  L'utilizzo di un connessione SSH di hello tootest terminal separato consente toogo indietro e apportare altre modifiche toohello `/etc/ssh/sshd_config` terminal prima di hello, senza essere bloccato da una modifica di rilievo SSHD.  

### <a name="on-redhat-centos-and-fedora"></a>Per Redhat, Centos e Fedora

```bash
service sshd restart
```

### <a name="on-debian--ubuntu"></a>Per Debian e Ubuntu

```bash
service ssh restart
```

## <a name="reset-sshd-using-azure-reset-access"></a>Reimpostare SSHD usando il comando reset-access di Azure

Se sono bloccati da una configurazione di rilievo modifica toohello SSHD hello estensione di macchina virtuale di Azure access tooreset hello SSHD configurazione toohello indietro originale configurazione consente.

Sostituire i nomi nell'esempio con quelli personalizzati.

```azurecli
azure vm reset-access \
--resource-group myResourceGroup \
--name myVM \
--reset-ssh
```

## <a name="install-fail2ban"></a>Installare Fail2ban

È consigliabile tooinstall e il programma di installazione Apri origine app hello Fail2ban, quali blocchi ripetuti tentativi toologin tooyour VM Linux su SSH tramite forza bruta.  I registri di Fail2ban ripetuti failover tentativi toologin SSH e quindi crea regole del firewall l'indirizzo IP di hello tooblock che hello tentativi provengano da.

* [Homepage di Fail2ban](http://www.fail2ban.org/wiki/index.php/Main_Page)

## <a name="next-steps"></a>Passaggi successivi

Dopo aver configurato e bloccati a server SSH hello nella VM Linux sono presenti procedure consigliate di sicurezza aggiuntive che è possibile seguire.  

* [Gestire utenti, SSH e controllo o i dischi di ripristino di macchine virtuali Linux di Azure utilizzando hello estensione VMAccess](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [Crittografare i dischi in una VM Linux utilizzando hello CLI di Azure](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [Accesso e sicurezza nei modelli di Azure Resource Manager](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
