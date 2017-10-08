---
title: aaaMove file tooand da macchine virtuali Linux di Azure con SCP | Documenti Microsoft
description: Spostare in modo sicuro i file tooand da una VM Linux di Azure tramite SCP e una coppia di chiavi SSH.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: danlep
ms.openlocfilehash: 9e4dce667aa581df74aec3d45a6ba5e52f777d1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-files-tooand-from-a-linux-vm-using-scp"></a>Spostare i file tooand da una VM Linux tramite SCP

Questo articolo illustra come toomove file dalla propria workstation backup tooan VM Linux di Azure o da una VM Linux di Azure verso il basso tooyour workstation, utilizzando Secure copia (SCP). Il trasferimento di file tra una workstation e una macchina virtuale Linux in modo rapido e sicuro è un aspetto essenziale della gestione dell'infrastruttura di Azure. 

Per questo articolo è necessaria una macchina virtuale Linux distribuita in Azure tramite [file di chiavi SSH pubbliche e private](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). È necessario anche un client SCP per il computer locale: È basato su SSH e della shell Bash predefinita di hello della maggior parte dei computer Mac e Linux e alcuni shell di Windows.

## <a name="quick-commands"></a>Comandi rapidi

Copiare un file di backup toohello VM Linux

```bash
scp file azureuser@azurehost:directory/targetfile
```

Copia un file verso il basso da hello VM Linux

```bash
scp azureuser@azurehost:directory/file targetfile
```

## <a name="detailed-walkthrough"></a>Procedura dettagliata

Ad esempio spostare un file di configurazione di Azure backup tooa VM Linux e acquisisce una directory di file di log, sia utilizzando chiavi SCP e SSH.   

## <a name="ssh-key-pair-authentication"></a>Autenticazione della coppia di chiavi SSH

SCP utilizza SSH per il livello di trasporto hello. Handle SSH hello autenticazione sull'host di destinazione hello e sposta il file hello in un tunnel crittografato fornito per impostazione predefinita con SSH. Per l'autenticazione SSH è possibile usare nomi utente e password. Per una maggiore sicurezza, tuttavia, è consigliabile eseguire l'autenticazione tramite file di chiavi SSH pubbliche e private. Una volta SSH è autenticato connessione hello, SCP, viene avviata la copia di file hello. Utilizzando un correttamente configurato `~/.ssh/config` e SSH chiavi pubbliche e private, connessione hello SCP possono essere stabilite utilizzando solo un nome server (o indirizzo IP). Se si dispone solo di una chiave SSH, SCP Cerca in hello `~/.ssh/` directory che viene utilizzato da toolog predefinito in toohello macchina virtuale.

Per altre informazioni sulla configurazione del file `~/.ssh/config` e delle chiavi SSH pubbliche e private, vedere [Creare chiavi SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="scp-a-file-tooa-linux-vm"></a>SCP tooa un file VM Linux

Ad esempio primo hello copiamo un file di configurazione di Azure backup tooa VM Linux automazione toodeploy utilizzato. Poiché questo file contiene credenziali di API di Azure, che includono informazioni riservate, la sicurezza è particolarmente importante tunnel di crittografato Hello fornito da SSH protegge il contenuto di hello del file hello.

Hello seguenti comando copie hello locale *.azure/config* tooan macchina virtuale di Azure con nome di dominio completo del file *myserver.eastus.cloudapp.azure.com*. nome utente amministratore di hello nella macchina virtuale di Azure hello è *azureuser* . file Hello è toohello destinazione */home/azureuser/* directory. Nel comando sostituire i valori predefiniti con quelli personali.

```bash
scp ~/.azure/config azureuser@myserver.eastus.cloudapp.com:/home/azureuser/config
```

## <a name="scp-a-directory-from-a-linux-vm"></a>Copia sicura di una directory da una macchina virtuale Linux

In questo esempio è copiare una directory di file di log da hello VM Linux verso il basso tooyour workstation. Poiché è possibile che un file di log contenga dati riservati, Tuttavia, tramite SCP garantisce la crittografia contenuto hello hello dei file di log. Utilizzo dei file di hello tootransfer SCP è tooget modo più semplice hello hello directory di log e file verso il basso workstation tooyour pur sicura.

Hello comando seguente copia i file in hello */home/azureuser/log/* directory nella directory /tmp locale toohello di hello macchina virtuale di Azure:

```bash
scp -r azureuser@myserver.eastus.cloudapp.com:/home/azureuser/logs/. /tmp/
```

Hello `-r` flag cli indica SCP toorecursively copia hello file e directory dal punto di hello della directory hello elencati nel comando hello.  Si noti che la sintassi della riga di comando hello sono anche simile tooa `cp` comando copia.

## <a name="next-steps"></a>Passaggi successivi

* [Gestire utenti, SSH e controllo o i dischi di ripristino di macchine virtuali Linux di Azure utilizzando hello estensione VMAccess](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
