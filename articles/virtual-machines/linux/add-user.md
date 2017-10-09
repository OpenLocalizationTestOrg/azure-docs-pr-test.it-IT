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
# <a name="add-a-user-tooan-azure-vm"></a>Aggiungere un tooan utente macchina virtuale di Azure
Una delle prime attività in qualsiasi nuova VM Linux di hello è toocreate un nuovo utente.  In questo articolo è illustrata la creazione di un account utente di sudo, l'impostazione password hello, aggiunta di chiavi pubbliche SSH e infine utilizzare `visudo` sudo tooallow senza una password.

Prerequisiti: [un account Azure](https://azure.microsoft.com/pricing/free-trial/), [chiavi pubbliche e private SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), un gruppo di risorse di Azure e hello Azure CLI installato e passa in modalità di gestione risorse tooAzure utilizzando `azure config mode arm`.

## <a name="quick-commands"></a>Comandi rapidi
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

## <a name="detailed-walkthrough"></a>Procedura dettagliata
### <a name="introduction"></a>Introduzione
Una delle attività di primo e più comune di hello con un nuovo server è tooadd un account utente.  Account di accesso radice deve essere disabilitata e account radice hello stessa non deve essere utilizzato con i server Linux e solo sudo.  Concedere i privilegi utilizzando "Sudo" hello tooadminister modo corretto e utilizzare Linux di escalation dei blocchi una radice di utente.

Comando hello `useradd` aggiungiamo toohello gli account utente Linux VM.  L'esecuzione di `useradd` modifica `/etc/passwd`, `/etc/shadow`, `/etc/group` e `/etc/gshadow`.  Si sta aggiungendo un flag della riga di comando di toohello `useradd` comando tooalso aggiungere hello nuovo toohello sudo corretto gruppo di utenti in Linux.  Anche viaggi `useradd` viene creata una voce in `/etc/passwd` non viene nuovo account utente di hello una password.  Si sta creando una password iniziale per hello nuovo utente con il semplice hello `passwd` comando.  ultimo passaggio Hello è toomodify hello sudo regole tooallow che i comandi tooexecute utente con privilegi sudo senza tooenter una password per ogni comando.  La registrazione con la chiave privata hello si suppone che l'account utente è protetta da cattivi attori e prevede l'accesso a sudo tooallow senza una password.  

### <a name="adding-a-single-sudo-user-tooan-azure-vm"></a>Aggiunta di un tooan utente sudo singola macchina virtuale di Azure
Accedi toohello macchina virtuale di Azure utilizzando le chiavi SSH.  Se non è stato configurato l'accesso con chiave pubblica SSH, eseguire prima i passaggi descritti in [Uso dell'autenticazione con chiave pubblica con Azure](http://link.to/article).  

Hello `useradd` hello seguenti attività di completamento del comando:

* creazione di un nuovo account utente
* creare un nuovo gruppo di utenti con hello stesso nome
* aggiungere una voce vuota troppo`/etc/passwd`
* aggiungere una voce vuota troppo`/etc/gpasswd`

Hello `-G` flag della riga di comando aggiunge hello nuovo utente account toohello corretto gruppo Linux concedere i privilegi di escalation dei blocchi di radice nuovo account utente di hello.

#### <a name="add-hello-user"></a>Aggiungere l'utente hello
```bash
# On RedHat family distros
sudo useradd -G wheel exampleUser

# On Debian family distros
sudo useradd -G sudo exampleUser
```

#### <a name="set-a-password"></a>Impostare una password
Hello `useradd` comando Crea hello e aggiunge una voce tooboth `/etc/passwd` e `/etc/gpasswd` ma non vengono effettivamente impostate password hello.  Hello password viene aggiunta voce toohello utilizzando hello `passwd` comando.

```bash
sudo passwd exampleUser
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
```

Un utente con privilegi sudo è ora disponibile nel server di hello.

### <a name="add-your-ssh-public-key-toohello-new-user-account"></a>Aggiungere il chiave pubblica SSH toohello nuovo account utente
Dal computer, utilizzare hello `ssh-copy-id` comando con una nuova password hello.

```bash
ssh-copy-id -i ~/.ssh/id_rsa exampleuser@exampleserver
```

### <a name="using-visudo-tooallow-sudo-usage-without-a-password"></a>Utilizzo visudo tooallow sudo senza una password
Utilizzando `visudo` tooedit hello `/etc/sudoers` file consente di aggiungere alcuni livelli di protezione per la modifica in modo non corretto di questo file importanti.  Durante l'esecuzione `visudo`, hello `/etc/sudoers` file è bloccato tooensure nessun altro utente può apportare modifiche mentre attivamente viene modificato.  Hello `/etc/sudoers` file viene archiviato anche per individuare errori da `visudo` quando si tenta di toosave o uscire in modo non è possibile salvare un file di file interrotto.

Gli utenti è già presente nel gruppo di hello predefiniti corretti per l'accesso a sudo.  A questo punto verrà tooenable tali sudo toouse gruppi senza password.

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

### <a name="verify-hello-user-ssh-keys-and-sudo"></a>Verificare utente hello, ssh chiavi e sudo
```bash
# Verify hello SSH keys & User account
ssh -i ~/.ssh/id_rsa exampleuser@exampleserver

# Verify sudo access
sudo top
```
