---
title: tooFreeBSD aaaIntroduction in Azure | Documenti Microsoft
description: Informazioni sull'uso delle macchine virtuali FreeBSD in Azure
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 32b87a5f-d024-4da0-8bf0-77e233d1422b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: kyliel
ms.openlocfilehash: eab7aeda7f7ef893740b39c0250aacc29d6fd71b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toofreebsd-on-azure"></a>Introduzione tooFreeBSD in Azure
Questo argomento offre una panoramica dell'esecuzione di una macchina virtuale FreeBSD in Azure.

## <a name="overview"></a>Panoramica
FreeBSD per Microsoft Azure è un sistema operativo avanzate toopower moderna server, desktop e piattaforme incorporate.

Microsoft Corporation rende le immagini di FreeBSD disponibile in Azure con hello [agente Guest della macchina virtuale Azure](https://github.com/Azure/WALinuxAgent/) preconfigurato. Attualmente, hello versioni FreeBSD seguenti sono disponibili come immagini da Microsoft:

- FreeBSD 10.3-RELEASE
- FreeBSD 11.0-RELEASE

Hello agente è responsabile per la comunicazione tra hello FreeBSD VM e l'infrastruttura di Azure per operazioni quali il provisioning di hello hello VM al primo utilizzo (nome utente, password o chiave SSH, nome host e così via) e le funzionalità di attivazione per selettive estensioni della macchina virtuale.

Come per le versioni future di FreeBSD, strategia hello è toostay corrente e rendere hello versioni più recenti disponibili subito dopo la pubblicazione dal team di progettazione di hello FreeBSD versione.

## <a name="deploying-a-freebsd-virtual-machine"></a>Distribuzione di una macchina virtuale FreeBSD
Distribuisce una macchina virtuale FreeBSD è un processo semplice utilizzando un'immagine da hello Azure Marketplace da hello portale di Azure:

- [10.3 FreeBSD in hello Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd103/)
- [11.0 FreeBSD in hello Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/)

### <a name="create-a-freebsd-vm-through-azure-cli-20-on-freebsd"></a>Creare una VM FreeBSD tramite l'interfaccia della riga di comando di Azure 2.0 su FreeBSD
È necessario innanzitutto tooinstall [CLI di Azure 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) se il comando seguente in un computer di FreeBSD.

```bash 
    curl -L https://aka.ms/InstallAzureCli | bash
```

Se bash non è installato nel computer FreeBSD, eseguire il comando prima dell'installazione di hello seguente. 

```
    sudo pkg install bash
```

Se nel computer FreeBSD, python non è installato, eseguire seguenti comandi prima dell'installazione di hello. 

```
    sudo pkg install python35
    cd /usr/local/bin 
    sudo rm /usr/local/bin/python 
    sudo ln -s /usr/local/bin/python3.5 /usr/local/bin/python
```

Durante l'installazione di hello, viene chiesto `Modify profile tooupdate your $PATH and enable shell/tab completion now? (Y/n)`. Se si risponde `y` e immettere `/etc/rc.conf` come `a path tooan rc file tooupdate`, si potrebbe soddisfare problema hello `ERROR: [Errno 13] Permission denied`. tooresolve questo problema, è necessario concedere hello scrittura toocurrent diritto utente file hello `etc/rc.conf`.

A questo punto è possibile accedere ad Azure e creare la VM FreeBSD. Di seguito è un esempio toocreate una macchina virtuale 11.0 FreeBSD. È inoltre possibile aggiungere il parametro hello `--public-ip-address-dns-name` con un nome DNS univoco globale per un indirizzo IP pubblico appena creato. 

```azurecli
    az login 
    az group create -n myResourceGroup -l westus az vm create -n myFreeBSD11 -g myResourceGroup --image MicrosoftOSTC:FreeBSD:11.0:latest --admin-username azureuser --ssh-key-value /etc/ssh/ssh_host_rsa_key.pub 
```

È quindi possibile accedere tooyour FreeBSD VM tramite indirizzo ip hello stampato un output di hello di sopra di distribuzione. 

```bash
    ssh azureuser@xx.xx.xx.xx -i /etc/ssh/ssh_host_rsa_key
```   

## <a name="vm-extensions-for-freebsd"></a>Estensioni di VM per FreeBSD
Di seguito sono descritte le estensioni di VM supportate in FreeBSD.

### <a name="vmaccess"></a>VMAccess
Hello [VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) estensione possibile:

* Reimpostare la password di hello dell'utente sudo originale hello.
* Creare un nuovo utente sudo con password hello specificata.
* Impostare la chiave host pubblica hello con chiave hello specificata.
* Reimposta chiave host pubblica hello fornita durante il provisioning se non viene fornito codice Product key host hello VM.
* Aprire la porta SSH hello (22) e il ripristino hello sshd_config se reset_ssh è impostato tootrue.
* Rimuovere l'utente esistente hello.
* Controllare i dischi.
* Riparare un disco aggiunto.

### <a name="customscript"></a>CustomScript
Hello [CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript) estensione possibile:

* Se fornito, è possibile scaricare gli script personalizzato hello da Azure o l'archiviazione esterna pubblico (ad esempio, GitHub).
* Eseguire script di punto di ingresso hello.
* Supportare comandi inline.
* Convertire automaticamente la nuova riga stile Windows in script della shell e Python.
* Rimuovere automaticamente un carattere BOM negli script della shell e Python.
* Proteggere i dati sensibili in CommandToExecute.

> [!NOTE]
> FreeBSD VM supporta solo CustomScript versione 1. x per adesso.  

## <a name="authentication-user-names-passwords-and-ssh-keys"></a>Autenticazione: nomi utente, password e chiavi SSH
Quando si crea una macchina virtuale FreeBSD utilizzando hello portale di Azure, è necessario fornire un nome utente, password o chiave pubblica SSH.
I nomi utente per la distribuzione di una macchina virtuale di FreeBSD in Azure non devono corrispondere i nomi degli account di sistema (UID < 100) è già presente nella macchina virtuale hello ("root", ad esempio).
Attualmente è supportata solo hello RSA chiave SSH. Una chiave SSH su più righe deve iniziare con `---- BEGIN SSH2 PUBLIC KEY ----` e terminare con `---- END SSH2 PUBLIC KEY ----`.

## <a name="obtaining-superuser-privileges"></a>Ottenere privilegi utente avanzati
account utente di Hello specificato durante la distribuzione di istanza di macchina virtuale in Azure è un account con privilegi. Hello pacchetto di sudo sia stato installato nella hello pubblicati FreeBSD immagine.
Dopo che si è connessi tramite l'account utente, è possibile eseguire i comandi come radice utilizzando la sintassi del comando hello.

```
    $ sudo <COMMAND>
```

Facoltativamente, è possibile ottenere una shell radice usando `sudo -s`.

## <a name="known-issues"></a>Problemi noti
Hello [agente Guest della macchina virtuale Azure](https://github.com/Azure/WALinuxAgent/) versione 2.2.2 dispone di un [problema noto] (https://github.com/Azure/WALinuxAgent/pull/517) che causa un errore di effettuare il provisioning di hello per FreeBSD VM in Azure. Hello correzione è stata acquisita da [agente Guest della macchina virtuale Azure](https://github.com/Azure/WALinuxAgent/) versione 2.2.3 e versioni successive. 

## <a name="next-steps"></a>Passaggi successivi
* Andare troppo[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) toocreate una VM FreeBSD.
* Se si desidera toobring proprio tooAzure FreeBSD, fare riferimento troppo[creazione e caricamento di un tooAzure FreeBSD VHD](linux/classic/freebsd-create-upload-vhd.md).
