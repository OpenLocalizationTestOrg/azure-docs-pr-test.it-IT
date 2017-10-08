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
# <a name="disable-ssh-passwords-on-your-linux-vm-by-configuring-sshd"></a>Disabilitare le password SSH nella VM Linux configurando SSHD
Questo articolo è incentrato sulla toolock verso il basso la sicurezza degli accessi hello della VM Linux.  Non appena viene aperta la porta SSH 22 hello toohello world Bot avviare durante il tentativo toologin cercando di indovinare le password.  In questo articolo si disabiliteranno gli accessi tramite password mediante SSH.  Per rimuovere completamente il possibilità hello attacco di forza password toouse Proteggiamo hello VM Linux da questo tipo di bruta.  Hello aggiunto bonus si configurerà Linux SSHD tooonly consentire gli account di accesso tramite chiavi SSH pubbliche e private di gran lunga hello tooLinux di toologin modo più sicuro.  le possibili combinazioni Hello di esso richiederebbe la chiave privata tooguess hello è enorme e sconsiglia pertanto Bot dall'intervento tootry toobrute force le chiavi SSH.

## <a name="goals"></a>Obiettivi
* Configurare SSHD toodisallow:
  * Accessi tramite password
  * Accesso dell'utente ROOT
  * Autenticazione In attesa/Risposta
* Configurare SSHD tooallow:
  * solo accessi tramite chiave SSH
* Riavviare SSHD durante la connessione
* Configurazione di test hello nuovo SSHD

## <a name="introduction"></a>Introduzione
[Definizione di SSH](https://en.wikipedia.org/wiki/Secure_Shell)

SSHD è hello Server SSH in esecuzione su hello VM Linux.  SSH è un client eseguito da una shell nella workstation MacBook o Linux.  SSH è anche il protocollo hello utilizzato toosecure e crittografare le comunicazioni tra la workstation e hello VM Linux hello.

Per questo articolo è molto importante tookeep un account di accesso tooyour VM Linux aperto per l'intera hello scorrere.  Per questo motivo verrà aperta due terminali e SSH toohello VM Linux da entrambi gli elementi.  Verrà utilizzare hello primo toomake terminal hello modifiche tooSSHDs file di configurazione e riavviare il servizio SSHD hello.  Si utilizzerà hello tootest terminal secondo le modifiche dopo aver riavviato il servizio di hello.  Poiché ci stiamo disabilitazione password SSH e basarsi esclusivamente sulle chiavi SSH, se le chiavi SSH non sono corrette e si chiude hello connessione toohello VM, hello VM verrà definitivamente bloccato e non sarà in grado di toologin tooit richiederla toobe eliminato e ricreato.

## <a name="prerequisites"></a>Prerequisiti
* [Creare chiavi SSH in Linux e Mac per le VM Linux in Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* Account Azure
  * [Versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/)
  * [Portale di Azure](http://portal.azure.com)
* VM Linux in esecuzione in Azure
* Coppia di chiavi SSH pubblica e privata in `~/.ssh/`
* La chiave pubblica SSH in `~/.ssh/authorized_keys` su hello VM Linux
* Diritti di Sudo su hello VM
* Porta 22 aperta

## <a name="quick-commands"></a>Comandi rapidi
*Gli amministratori di Linux esperti che si desidera versione TLDR hello iniziare da qui.  Per tutti gli utenti che desidera hello dettagliate e procedura per ignorare questa sezione.*

```bash
sudo vim /etc/ssh/sshd_config
```

Modificare il file di configurazione di hello come indicato di seguito:

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

Riavviare il servizio SSHD hello. Nelle distribuzioni basate su Debian:

```bash
sudo service ssh restart
```

Nelle distribuzioni basate su Red Hat:

```bash
sudo service sshd restart
```

## <a name="detailed-walk-through"></a>Procedura dettagliata
Account di accesso toohello VM Linux su terminal 1 (T1).  Account di accesso toohello VM Linux su terminal 2 (T2).

Nella tabella T2 verrà file di configurazione tooedit hello SSHD.  

```bash
sudo vim /etc/ssh/sshd_config
```

Da qui la modifica appena hello impostazioni toodisable le password e abilitare gli account di accesso chiave SSH.  Esistono molte impostazioni in questo file che è consigliabile ricercare e modificare toomake Linux & SSH come protette in base alle esigenze.

#### <a name="disable-password-logins"></a>Disabilitare gli accessi tramite password

```sh
# Change PasswordAuthentication toothis:
PasswordAuthentication no
```

#### <a name="enable-public-key-authentication"></a>Abilitare l'autenticazione con chiave pubblica

```sh
# Change PubkeyAuthentication toothis:
PubkeyAuthentication yes
```

#### <a name="disable-root-login"></a>Disabilitare l'accesso root

```sh
# Change PermitRootLogin toothis:
PermitRootLogin no
```

#### <a name="disable-challenge-response-authentication"></a>Disabilitare l'autenticazione In attesa/Risposta
```sh
# Change ChallengeResponseAuthentication toothis:
ChallengeResponseAuthentication no
```

### <a name="restart-sshd"></a>Riavviare SSHD
Verificare che si è ancora connessi da shell hello T1.  Questo è fondamentale per non rimanere esclusi dalla VM nel caso in cui le chiavi SSH non siano corrette, dato che ora le password sono disabilitate.  Se tutte le impostazioni sono corrette nella VM Linux è possibile utilizzare T1 toofix sshd_config come verrà comunque eseguito e SSH verrà mantenere attiva la connessione hello durante hello service SSHD riavviare.

Da T2 eseguire:

##### <a name="on-hello-debian-family"></a>Nella famiglia Debian hello
```bash
sudo service ssh restart
```

##### <a name="on-hello-redhat-family"></a>Nella famiglia RedHat hello
```bash
sudo service sshd restart
```

Le password sono ora disabilitate nella VM, che a questo punto è protetta dai tentativi di accesso tramite password da parte di attacchi di forza bruta.  Con solo SSH chiavi consentito sarà in grado di toologin molto più rapido e sicuro.

