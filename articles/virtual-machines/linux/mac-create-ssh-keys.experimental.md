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
# <a name="create-an-ssh-public-and-private-key-pair-for-linux-vms"></a>Creare una coppia di chiavi SSH pubblica e privata per le macchine virtuali di Linux

Questo articolo illustra come toogenerate protocol versione 2 RSA pubblica e privata chiave SSH file coppia toouse con le macchine virtuali Linux.  Con una coppia di chiavi SSH, è possibile creare macchine virtuali in Azure che utilizza l'impostazione predefinita le chiavi SSH toousing per l'autenticazione, eliminando la necessità hello per le password toolog in.  Le password possono essere individuate e aprire le macchine virtuali di tooguess tentativi di attacchi di forza bruta toorelentless la password. Macchine virtuali create con modelli di Azure o hello `azure-cli` possono includere la chiave pubblica SSH come parte della distribuzione di hello, la rimozione di un passaggio di configurazione di distribuzione post della disabilitazione dell'account di accesso di password per SSH.

## <a name="quick-commands"></a>Comandi rapidi

Eseguire hello seguendo i comandi da una shell Bash, sostituendo esempi hello con le proprie scelte.

Per impostazione predefinita, il file di chiave pubblica SSH viene creato in `~/.ssh/id_rsa.pub`. Quando viene richiesto tramite hello comando seguente, è necessario creare un toosecure "passphrase" con la chiave privata. (hello passphrase è utilizzata una password tooencrypt con la chiave privata).

```bash
ssh-keygen -t rsa -b 2048 
```

Aggiungere la chiave di hello appena creato troppo`ssh-agent`:

```bash
ssh-add ~/.ssh/id_rsa
```

> [!IMPORTANT] 
> Hello sopra lavoro comandi su sistemi operativi Linux di quasi tutte le distribuzioni, ma non necessariamente all'interno di contenitori, come ambiente hello può essere vincolato radicalmente. 

## <a name="detailed-walkthrough"></a>Procedura dettagliata

Utilizzo delle chiavi pubbliche e private SSH è toolog modo più semplice di hello in server Linux tooyour. [Crittografia a chiave pubblica](https://en.wikipedia.org/wiki/Public-key_cryptography) fornisce un toolog modo molto più sicuro in tooyour Linux o BSD VM in Azure rispetto alle password, che possono essere colpita molto più semplice.

> [!IMPORTANT]
> La chiave pubblica può essere condivisa con chiunque, ma la chiave privata appartiene solo all'utente o all'infrastruttura di sicurezza locale.  la chiave privata SSH Hello deve avere un [password molto sicura](https://www.xkcd.com/936/) (origine:[xkcd.com](https://xkcd.com)) toosafeguard è.  Questa password è una chiave privata SSH di tooaccess solo hello e **non** password dell'account utente hello.  Quando si aggiunge una chiave SSH tooyour, crittografa la chiave privata di hello tramite AES a 128 bit, in modo che hello chiave privata è inutile senza toodecrypt password hello è.  Se un utente malintenzionato rubare la chiave privata e tale chiave non dispone di una password, saranno in grado di toouse che private key toolog nel server tooany che dispongono di chiave pubblica corrispondente hello.  Una chiave privata protetta da password non può essere usata da utenti malintenzionati e rappresenta un livello di sicurezza aggiuntivo per l'infrastruttura in Azure.

In questo articolo Crea versione del protocollo SSH 2 RSA pubblici e privati file di chiave, che sono consigliati per le distribuzioni di hello Gestione risorse.  *SSH-rsa* le chiavi sono necessarie in hello [portale](https://portal.azure.com) per classica e le distribuzioni di gestione risorse.

## <a name="disable-ssh-passwords-by-using-ssh-keys"></a>Disabilitare le password SSH usando le chiavi SSH

Azure richiede chiavi pubbliche e private nel formato ssh-rsa almeno a 2048 bit. Utilizzare tasti di hello toocreate `ssh-keygen`, che richiede una serie di domande e quindi scrive una chiave privata e una chiave pubblica corrispondente. Quando viene creata una macchina virtuale di Azure, la chiave pubblica di hello viene copiata troppo`~/.ssh/authorized_keys`.  Le chiavi SSH in `~/.ssh/authorized_keys` vengono utilizzati toochallenge hello toomatch hello corrispondente chiave privata del client su una connessione di accesso SSH.  Quando una macchina virtuale Linux di Azure viene creata utilizzando le chiavi SSH per l'autenticazione, Azure Configura hello SSHD toonot server consente l'accesso con password, solo le chiavi SSH.  Pertanto, tramite la creazione di macchine virtuali Linux di Azure con le chiavi SSH, è possibile consentono la distribuzione di macchina virtuale protetta hello e risparmiare passaggio di configurazione post-distribuzione tipica hello della disabilitazione delle password nel file di configurazione sshd_config hello.

## <a name="using-ssh-keygen"></a>Uso di ssh-keygen

Questo comando crea una password protetta (crittografato) coppia di chiavi SSH tramite RSA a 2048 bit e si è impostata come commento tooeasily identificarlo.  

SSH chiavi per impostazione predefinita vengono mantenuta in hello `~/.ssh` directory.  Se non è un `~/.ssh` directory, hello `ssh-keygen` comando crea automaticamente con hello delle autorizzazioni corrette.

```bash
ssh-keygen \
-t rsa \
-b 2048 
```

*Descrizione del comando*

`ssh-keygen`= hello programma utilizzato toocreate hello chiavi

`-t rsa`tipo di chiave toocreate hello RSA formato = [wikipedia](https://en.wikipedia.org/wiki/RSA_(cryptosystem)

`-b 2048`= bit della chiave hello


## <a name="classic-portal-and-x509-certs"></a>Portale classico e certificati X.509

Se si utilizza hello Azure [portale classico](https://manage.windowsazure.com/), richiede i certificati x. 509 per le chiavi SSH hello.  Non sono consentite altre chiavi pubbliche SSH, *devono* essere certificati X.509.

toocreate un certificato x. 509 dalla chiave privata SSH-RSA esistente:

```bash
openssl req -x509 \
-key ~/.ssh/id_rsa \
-nodes \
-days 365 \
-newkey rsa:2048 \
-out ~/.ssh/id_rsa.pem
```

## <a name="classic-deploy-using-asm"></a>Distribuzione classica tramite `asm`

Se si utilizza classica hello distribuire modello (gestione dei servizi Azure CLI `asm`), è possibile utilizzare una chiave pubblica SSH-RSA o formattato un RFC4716 chiave in un **PEM** contenitore.  chiave pubblica SSH-RSA Hello è ciò che è stato creato in precedenza in questo articolo utilizzando `ssh-keygen`.

toocreate un RFC4716 formato della chiave da una chiave pubblica SSH esistente:

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a>Esempio di ssh-keygen

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

File delle chiavi salvati:

`Enter file in which toosave hello key (/home/ahmet/.ssh/id_rsa): ~/.ssh/id_rsa`

nome della coppia chiave Hello per questo articolo.  Con una coppia di chiavi denominata **id_rsa** hello predefinito e alcuni strumenti prevedibile hello **id_rsa** nome di file di chiave privata in modo che uno è una buona idea. directory Hello `~/.ssh/` è il percorso predefinito hello per le coppie di chiavi SSH e file di configurazione di hello SSH.  Se non è specificato con un percorso completo, `ssh-keygen` dovrà creare chiavi hello nella directory di lavoro corrente hello, hello non predefinito `~/.ssh`.

Un elenco di hello `~/.ssh` directory.

```bash
ls -al ~/.ssh
-rw------- 1 ahmet staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 ahmet staff   410 Aug 25 18:04 rsa.pub
```

Password della chiave:

`Enter passphrase (empty for no passphrase):`

`ssh-keygen`fa riferimento di chiave privata hello tooencrypt password utilizzata tooa come "una passphrase."  È *fortemente* consigliato tooadd coppie di chiavi di tooyour una passphrase. Senza una passphrase protezione hello chiave privata, tutti gli utenti con i file di chiave hello usarlo toolog tooany server dotato di chiave pubblica corrispondente hello. Aggiunta di una passphrase offre ulteriore protezione, nel caso in cui un utente è in grado di toogain accesso tooyour file di chiave privata, offrendo chiavi hello toochange utilizzato tooauthenticate è.

## <a name="using-ssh-agent-toostore-your-private-key-password"></a>Utilizzo di ssh agente toostore la password della chiave privata

Digitare la chiave privata tooavoid file passphrase con ogni account di accesso SSH, è possibile utilizzare `ssh-agent` toocache la password del file di chiave privata. Se si utilizza un computer Mac, hello OSX portachiavi Archivia password chiave privata hello in modo sicuro quando si richiama `ssh-agent`.

Verificare e utilizzare `ssh-agent` e `ssh-add` tooinform hello sistema SSH sui file di chiave hello in modo che la passphrase hello non sarà necessario toobe utilizzati in modo interattivo.

```bash
eval "$(ssh-agent -s)"
```

A questo punto aggiungere la chiave privata di hello troppo`ssh-agent` comando hello `ssh-add`.

```bash
ssh-add ~/.ssh/id_rsa
```

password della chiave privata Hello sono ora archiviate in `ssh-agent`.

## <a name="using-ssh-copy-id-tooinstall-hello-new-key"></a>Utilizzando `ssh-copy-id` nuova chiave di tooinstall hello
Se è stato già creato una macchina virtuale è possibile installare hello nuovo SSH pubblica chiave tooyour VM Linux con hello comando seguente, sostituendo il nome utente VM hello e l'indirizzo di server hello con valori personalizzati:

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a>Creare e configurare un file config SSH

Un migliore toocreate pratica e configurare un `~/.ssh/config` toospeed file di log aggiuntivi e per l'ottimizzazione del comportamento del client SSH.

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

Successivamente backup toocreate macchine virtuali Linux di Azure Usa hello nuovo la chiave pubblica SSH.  Macchine virtuali di Azure che vengono create con una chiave pubblica SSH come account di accesso hello sono più protette rispetto a macchine virtuali create con metodo di accesso predefinito hello, le password.  Per impostazione predefinita, le VM di Azure create con le chiavi SSH vengono configurate con le password disabilitate, evitando tentativi di attacco basati su forza bruta per scoprire le password. Se si necessita di ulteriore assistenza per la creazione di coppia di chiavi SSH o richiedono certificati aggiuntivi, ad esempio per l'utilizzo con portale classico hello, vedere [dettagliate coppie di chiavi SSH toocreate passaggi e i certificati](create-ssh-keys-detailed.md).

* [Creare una VM Linux protetta usando un modello di Azure](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Creare una VM Linux protette utilizzando hello portale di Azure](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Creare una VM Linux protette utilizzando hello CLI di Azure](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
