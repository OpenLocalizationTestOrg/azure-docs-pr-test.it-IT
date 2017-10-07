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
# <a name="detailed-walk-through-toocreate-an-ssh-key-pair-and-additional-certificates-for-a-linux-vm-in-azure"></a>Procedura dettagliata toocreate una coppia di chiavi SSH e certificati aggiuntivi per una VM Linux di Azure
Con una coppia di chiavi SSH, è possibile creare macchine virtuali in Azure che utilizza l'impostazione predefinita le chiavi SSH toousing per l'autenticazione, eliminando la necessità hello per le password toolog in. Le password possono essere individuate e aprire le macchine virtuali di tooguess tentativi di attacchi di forza bruta toorelentless la password. Macchine virtuali create con i modelli di hello CLI di Azure o di gestione delle risorse possono includere la chiave pubblica SSH come parte della distribuzione di hello, la rimozione di un passaggio di configurazione di distribuzione post della disabilitazione dell'account di accesso di password per SSH. Questo articolo illustra i passaggi dettagliati e offre esempi aggiuntivi per la generazione di certificati, ad esempio per l'uso con macchine virtuali di Linux. Se si desidera tooquickly creare e utilizzare una coppia di chiavi SSH, vedere [come coppia di toocreate chiave SSH pubblica e privata per le macchine virtuali Linux in Azure](mac-create-ssh-keys.md).

## <a name="understanding-ssh-keys"></a>Informazioni sulle chiavi SSH

Utilizzo delle chiavi pubbliche e private SSH è toolog modo più semplice di hello in server Linux tooyour. [Crittografia a chiave pubblica](https://en.wikipedia.org/wiki/Public-key_cryptography) fornisce un toolog modo molto più sicuro in tooyour Linux o BSD VM in Azure rispetto alle password, che possono essere colpita molto più semplice.

La chiave pubblica può essere condivisa con chiunque, ma la chiave privata appartiene solo all'utente o all'infrastruttura di sicurezza locale.  la chiave privata SSH Hello deve avere un [password molto sicura](https://www.xkcd.com/936/) (origine:[xkcd.com](https://xkcd.com)) toosafeguard è.  Questa password è semplicemente tooaccess hello SSH file di chiave privata e **non** password dell'account utente hello.  Quando si aggiunge una chiave SSH tooyour, crittografa la chiave privata di hello tramite AES a 128 bit, in modo che hello chiave privata è inutile senza toodecrypt password hello è.  Se un utente malintenzionato rubare la chiave privata e tale chiave non dispone di una password, saranno in grado di toouse che private key toolog nel server tooany che dispongono di chiave pubblica corrispondente hello.  Una chiave privata protetta da password non può essere usata da utenti malintenzionati e rappresenta un livello di sicurezza aggiuntivo per l'infrastruttura in Azure.

In questo articolo viene creata una versione del protocollo SSH 2 coppie di file di chiave pubblica e privata RSA (anche noto tooas "ssh-rsa" chiavi), che sono consigliate per le distribuzioni con Gestione risorse di Azure. *SSH-rsa* le chiavi sono necessarie in hello [portale](https://portal.azure.com) per classica e le distribuzioni di gestione risorse.

## <a name="ssh-keys-use-and-benefits"></a>Uso e vantaggi delle chiavi SSH

Azure richiede almeno 2048 bit, versione 2 RSA formato chiavi pubbliche e private; del protocollo SSH file di chiave pubblica Hello è hello `.pub` formato contenitore. Utilizzare tasti di hello toocreate `ssh-keygen`, che richiede una serie di domande e quindi scrive una chiave privata e una chiave pubblica corrispondente. Quando viene creata una macchina virtuale di Azure, Azure copie hello toohello chiave pubblica `~/.ssh/authorized_keys` cartella hello macchina virtuale. Le chiavi SSH in `~/.ssh/authorized_keys` vengono utilizzati toochallenge hello toomatch hello corrispondente chiave privata del client su una connessione di accesso SSH.  Quando una macchina virtuale Linux di Azure viene creata utilizzando le chiavi SSH per l'autenticazione, Azure Configura hello SSHD toonot server consente l'accesso con password, solo le chiavi SSH.  Di conseguenza, mediante la creazione di macchine virtuali Linux di Azure con le chiavi SSH, consentono di proteggere la distribuzione di macchine Virtuali hello e risparmiare passaggio di configurazione post-distribuzione tipica hello di disabilitazione di password in hello **sshd_config** file.

## <a name="using-ssh-keygen"></a>Uso di ssh-keygen

Questo comando crea una password protetta (crittografato) coppia di chiavi SSH tramite RSA a 2048 bit e si è impostata come commento tooeasily identificarlo.  

SSH chiavi per impostazione predefinita vengono mantenuta in hello `~/.ssh` directory.  Se non è un `~/.ssh` directory, hello `ssh-keygen` comando crea automaticamente con hello delle autorizzazioni corrette.

```bash
ssh-keygen \
    -t rsa \
    -b 2048 \
    -C "azureuser@myserver" \
    -f ~/.ssh/id_rsa \
    -N mypassword
```

*Descrizione del comando*

`ssh-keygen`= hello programma utilizzato toocreate hello chiavi

`-t rsa`tipo di chiave toocreate hello RSA formato [wikipedia] =[parens alla fine](`https://en.wikipedia.org/wiki/RSA_(cryptosystem) `) 
 `-b 2048` = bit della chiave hello

`-C "azureuser@myserver"`= un commento aggiunto toohello fine tooeasily file di chiave pubblica hello identificarlo.  In genere un messaggio di posta elettronica viene utilizzato come commento hello ma è possibile utilizzare qualsiasi più adatto per l'infrastruttura.

## <a name="classic-deploy-using-asm"></a>Distribuzione classica tramite `asm`

Se si utilizza il modello di distribuzione classica hello (`asm` modalità hello CLI), è possibile utilizzare una chiave pubblica SSH-RSA o formattato un RFC4716 chiave in un contenitore pem.  chiave pubblica SSH-RSA Hello è ciò che è stato creato in precedenza in questo articolo utilizzando `ssh-keygen`.

toocreate un RFC4716 formato della chiave da una chiave pubblica SSH esistente:

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a>Esempio di ssh-keygen

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

File delle chiavi salvati:

`Enter file in which toosave hello key (/home/azureuser/.ssh/id_rsa): ~/.ssh/id_rsa`

nome della coppia chiave Hello per questo articolo.  Con una coppia di chiavi denominata **id_rsa** hello predefinito e alcuni strumenti prevedibile hello **id_rsa** nome di file di chiave privata in modo che uno è una buona idea. directory Hello `~/.ssh/` è il percorso predefinito hello per le coppie di chiavi SSH e file di configurazione di hello SSH.  Se non è specificato con un percorso completo, `ssh-keygen` crea chiavi hello in hello directory di lavoro corrente, non il valore predefinito hello `~/.ssh`.

Un elenco di hello `~/.ssh` directory.

```bash
ls -al ~/.ssh
-rw------- 1 azureuser staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 azureuser staff   410 Aug 25 18:04 id_rsa.pub
```

Password della chiave:

`Enter passphrase (empty for no passphrase):`

`ssh-keygen`fa riferimento tooa password per il file di chiave privata di hello come "una passphrase."  È *fortemente* consigliato tooadd una chiave privata tooyour di password. Senza un password protezione hello file di chiave, tutti gli utenti con file hello usarlo toolog tooany server dotato di chiave pubblica corrispondente hello. Aggiunta di una password (passphrase) offre ulteriore protezione, nel caso in cui un utente è in grado di toogain accesso tooyour file di chiave privata, riceve chiavi hello toochange utilizzato tooauthenticate è.

## <a name="using-ssh-agent-toostore-your-private-key-password"></a>Utilizzo di ssh agente toostore la password della chiave privata

tooavoid digitare la password del file di chiave privata con ogni account di accesso SSH, è possibile utilizzare `ssh-agent` toocache la password del file di chiave privata. Se si utilizza un computer Mac, hello OSX portachiavi Archivia password chiave privata hello in modo sicuro quando si richiama `ssh-agent`.

Verificare e utilizzare ssh agente ssh-Aggiungi tooinform hello SSH sistema sui file di chiave hello in modo che la passphrase hello non sarà necessario toobe utilizzati in modo interattivo.

```bash
eval "$(ssh-agent -s)"
```

A questo punto aggiungere la chiave privata di hello troppo`ssh-agent` comando hello `ssh-add`.

```bash
ssh-add ~/.ssh/id_rsa
```

password della chiave privata Hello sono ora archiviate in `ssh-agent`.

## <a name="using-ssh-copy-id-toocopy-hello-key-tooan-existing-vm"></a>Utilizzando `ssh-copy-id` toocopy hello tooan chiave macchina virtuale esistente
Se è stato già creato una macchina virtuale è possibile installare hello nuovo SSH pubblica chiave tooyour VM Linux con:

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a>Creare e configurare un file config SSH

È un consigliato toocreate prassi migliori e configurare un `~/.ssh/config` toospeed file di log aggiuntivi e per l'ottimizzazione del comportamento del client SSH.

Hello di esempio seguente viene illustrata una configurazione standard.

### <a name="create-hello-file"></a>Creare file hello

```bash
touch ~/.ssh/config
```

### <a name="edit-hello-file-tooadd-hello-new-ssh-configuration"></a>Modificare hello file tooadd hello nuova configurazione SSH:

```bash
vim ~/.ssh/config
```

### <a name="example-sshconfig-file"></a>File `~/.ssh/config` di esempio:

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

In questo modo di configurazione SSH sezioni per ogni server tooenable ogni toohave propria dedicata coppia di chiavi. le impostazioni predefinite di Hello (`Host *`) sono per tutti gli host che non corrispondono a uno degli host hello specifico livello più alto nel file di configurazione hello.

### <a name="config-file-explained"></a>Descrizione del file config

`Host`= nome hello dell'host di hello viene chiamato il metodo hello terminal.  `ssh fedora22`indica `SSH` valori hello toouse in blocco settings hello etichettata `Host fedora22` Nota: Host può essere qualsiasi etichetta logico per l'utilizzo e non rappresenta hello nome host effettivo di qualsiasi server.

`Hostname 102.160.203.241`= indirizzo hello o un nome DNS per il server di hello cui si accede.

`User ahmet`= toouse di account utente remoto hello durante l'accesso toohello server.

`PubKeyAuthentication yes`= indica SSH desiderato toouse un toolog chiave SSH.

`IdentityFile /home/ahmet/.ssh/id_id_rsa`= la chiave privata SSH hello e toouse di chiave pubblica corrispondente per l'autenticazione.

## <a name="ssh-into-linux-without-a-password"></a>Usare SSH per accedere a Linux senza password

Dopo aver creato una coppia di chiavi SSH e un file di configurazione SSH configurato, sono in grado di toolog in tooyour VM Linux rapidamente e in modo sicuro. Hello al primo accesso nel server di tooa tramite un prompt dei comandi hello chiave SSH è per la passphrase hello per tale file di chiave.

```bash
ssh fedora22
```

### <a name="command-explained"></a>Descrizione del comando

Quando `ssh fedora22` viene eseguita SSH prima individua e carica le impostazioni da hello `Host fedora22` blocco e quindi carica tutti hello rimanenti impostazioni dall'ultimo blocco, hello `Host *`.

## <a name="next-steps"></a>Passaggi successivi

Successivamente backup toocreate macchine virtuali Linux di Azure Usa hello nuovo la chiave pubblica SSH.  Macchine virtuali di Azure che vengono create con una chiave pubblica SSH come account di accesso hello sono più protette rispetto a macchine virtuali create con metodo di accesso predefinito hello, le password.  Per impostazione predefinita, le VM di Azure create con le chiavi SSH vengono configurate con le password disabilitate, evitando tentativi di attacco basati su forza bruta per scoprire le password.

* [Creare una VM Linux protetta usando un modello di Azure](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Creare una VM Linux protette utilizzando hello portale di Azure](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Creare una VM Linux protette utilizzando hello CLI di Azure](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
