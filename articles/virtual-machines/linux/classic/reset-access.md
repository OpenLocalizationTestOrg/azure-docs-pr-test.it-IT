---
title: aaaReset password VM Linux e SSH chiave hello CLI | Documenti Microsoft
description: Come correggere configurazione SSH hello hello toouse estensione VMAccess da hello Azure interfaccia della riga di comando (CLI) tooreset una password di Linux VM o una chiave SSH e verificare la coerenza del disco
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: d975eb70-5ff1-40d1-a634-8dd2646dcd17
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: cynthn
ms.openlocfilehash: 1650ad64fb982627ae9f90b1a8209bb56bac7004
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-a-linux-vm-password-or-ssh-key-fix-hello-ssh-configuration-and-check-disk-consistency-using-hello-vmaccess-extension"></a>Come tooreset una password di Linux VM o una chiave SSH, correggere configurazione SSH hello e verificare la coerenza del disco tramite l'estensione VMAccess hello
Se non è possibile connettersi macchina virtuale di Linux tooa in Azure a causa di una password dimenticata, una chiave non corretta di Secure Shell (SSH) o un problema con la configurazione SSH hello, utilizzare l'estensione VMAccessForLinux hello con hello Azure CLI tooreset hello password o chiave SSH, correggere Hello configurazione SSH, quindi verificare la coerenza del disco. 

> [!IMPORTANT] 
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni. Informazioni su come troppo[eseguire questi passaggi tramite il modello di gestione risorse di hello](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).

Con hello CLI di Azure, utilizzare hello **set di estensioni di macchina virtuale di azure** comando dai comandi di tooaccess interfaccia della riga di comando (Bash, Terminal, prompt dei comandi). Per informazioni dettagliate sull'uso dell'estensione, eseguire **azure help vm extension set** .

Con hello CLI di Azure, è possibile eseguire hello quanto segue:

* [Reimpostare la password di hello](#pwresetcli)
* [Reimpostare la chiave SSH hello](#sshkeyresetcli)
* [Reimpostare la chiave SSH password e hello hello](#resetbothcli)
* [Creare un nuovo account utente sudo](#createnewsudocli)
* [Reimposta configurazione SSH hello](#sshconfigresetcli)
* [Eliminare un utente](#deletecli)
* [Visualizzare lo stato di hello di hello estensione VMAccess](#statuscli)
* [Verificare la coerenza dei dischi aggiunti](#checkdisk)
* [Ripristinare i dischi aggiunti nella VM Linux](#repairdisk)

## <a name="prerequisites"></a>Prerequisiti
È necessario seguente hello toodo:

* Sarà necessario troppo[installare hello Azure CLI](../../../cli-install-nodejs.md) e [connettere sottoscrizione tooyour](../../../xplat-cli-connect.md) toouse Azure le risorse associate all'account.
* Impostare la modalità corretta per il modello di distribuzione classica hello hello digitando hello segue al prompt dei comandi di hello:
    ``` 
        azure config mode asm
    ```
* Disporre di una nuova password o un set di chiavi SSH, se si desidera tooreset dei due. Questi non sono necessari se si desidera tooreset hello SSH configurazione.

## <a name="pwresetcli"></a>Reimpostare la password di hello
1. Creare un file denominato PrivateConf.json nel computer locale con queste righe. Sostituire **myUserName** e  **myP@ssW0rd**  con il proprio nome utente e password e impostare la data di scadenza.

    ```   
        {
        "username":"myUserName",
        "password":"myP@ssW0rd",
        "expiration":"2020-01-01"
        }
    ```
        
2. Eseguire questo comando, sostituendo il nome della macchina virtuale per hello **myVM**.

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* –-private-config-path PrivateConf.json
    ```

## <a name="sshkeyresetcli"></a>Reimpostare la chiave SSH hello
1. Creare un file denominato PrivateConf.json con questo contenuto. Sostituire hello **myUserName** e **mySSHKey** valori con le proprie informazioni.

    ```   
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey"
        }
    ```
2. Eseguire questo comando, sostituendo il nome della macchina virtuale per hello **myVM**.
   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json

## <a name="resetbothcli"></a>Reimpostare la chiave SSH hello e la password di hello
1. Creare un file denominato PrivateConf.json con questo contenuto. Sostituire hello **myUserName**, **mySSHKey** e  **myP@ssW0rd**  valori con le proprie informazioni.

    ``` 
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey",
        "password":"myP@ssW0rd"
        }
    ```

2. Eseguire questo comando, sostituendo il nome della macchina virtuale per hello **myVM**.

    ```   
        azure vm extension set MyVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <a name="createnewsudocli"></a>Creare un nuovo account utente sudo

Se si dimentica il nome utente, è possibile utilizzare uno nuovo con autorità sudo hello toocreate VMAccess. In questo caso, hello esistente nome utente e password non verranno modificate.

un nuovo utente sudo con accesso con password, utilizzare script hello toocreate [hello di reimpostazione password](#pwresetcli) e specificare nuovi nome utente di hello.

un nuovo utente sudo con accesso alla chiave SSH, utilizza script di hello in toocreate [la chiave SSH hello reimpostazione](#sshkeyresetcli) e specificare nuovi nome utente di hello.

È inoltre possibile utilizzare [reimpostare password hello e chiave SSH hello](#resetbothcli) toocreate un nuovo utente con accesso alla chiave SSH e la password.

## <a name="sshconfigresetcli"></a>Reimposta configurazione SSH hello
Se in uno stato indesiderato configurazione SSH hello, si potrebbe perdere anche l'accesso toohello macchina virtuale. È possibile utilizzare hello VMAccess estensione tooreset hello configurazione tooits stato predefinito. toodo in tal caso, è sufficiente chiave di "reset_ssh" hello tooset troppo "True". estensione Hello verrà riavviare i server SSH hello, aprire la porta SSH hello nella VM e reimpostare i valori hello SSH configurazione toodefault. account utente di Hello (nome, la password o le chiavi SSH) non verranno modificate.

> [!NOTE]
> file di configurazione di SSH Hello reimpostato si trova in /etc/ssh/sshd_config.
> 
> 

1. Creare un file denominato PrivateConf.json con questo contenuto.

    ```   
        {
        "reset_ssh":"True"
        }
    ```

2. Eseguire questo comando, sostituendo il nome della macchina virtuale per hello **myVM**. 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <a name="deletecli"></a>Eliminare un utente
Se si desidera toodelete un account utente senza registrazione direttamente toohello VM, è possibile utilizzare questo script.

1. Creare un file denominato PrivateConf.json con questo contenuto, sostituendo hello utente nome tooremove per **removeUserName**. 

    ```   
        {
        "remove_user":"removeUserName"
        }
    ```

2. Eseguire questo comando, sostituendo il nome della macchina virtuale per hello **myVM**. 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <a name="statuscli"></a>Visualizzare lo stato di hello di hello estensione VMAccess
stato hello toodisplay di hello estensione VMAccess, eseguire questo comando.

```
        azure vm extension get
```

## <a name='checkdisk'></a>Verificare la coerenza dei dischi aggiunti
sfck toorun su tutti i dischi nella macchina virtuale di Linux, è necessario seguente hello toodo:

1. Creare un file denominato PublicConf.json con questo contenuto. Controllo disco accetta un valore booleano per se toocheck dischi associato macchina virtuale tooyour o meno. 

    ```   
        {   
        "check_disk": "true"
        }
    ```

2. Eseguire tooexecute questo comando, sostituendo il nome della macchina virtuale per hello **myVM**.

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json 
    ```

## <a name='repairdisk'></a>Riparare i dischi
i dischi toorepair che non vengono montato o presentano errori di configurazione di montaggio, utilizzare configurazione di montaggio hello tooreset estensione VMAccess hello sulla macchina virtuale di Linux. Nome hello sostituendo del disco per **myDisk**.

1. Creare un file denominato PublicConf.json con questo contenuto. 

    ```   
        {
        "repair_disk":"true",
        "disk_name":"myDisk"
        }
    ```

2. Eseguire tooexecute questo comando, sostituendo il nome della macchina virtuale per hello **myVM**.

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json
    ```

## <a name="next-steps"></a>Passaggi successivi
* Se si desidera toouse cmdlet di Azure PowerShell o la password di Azure Resource Manager modelli tooreset hello o chiave SSH, correggere la configurazione SSH, hello e verificare la coerenza del disco, vedere hello [documentazione estensione VMAccess su GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess). 
* È inoltre possibile utilizzare hello [portale di Azure](https://portal.azure.com) tooreset hello password o una chiave SSH di una VM Linux distribuito nel modello di distribuzione classica hello. Non è possibile utilizzare hello portale toothis per una VM Linux distribuito nel modello di distribuzione di gestione risorse di hello.
* Per altre informazioni sull'uso di estensioni VM per macchine virtuali di Azure vedere [Informazioni sulle estensioni e sulle funzionalità delle macchine virtuali](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

