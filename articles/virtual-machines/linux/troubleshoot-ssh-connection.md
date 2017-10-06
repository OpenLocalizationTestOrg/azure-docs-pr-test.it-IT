---
title: problemi di connessione SSH aaaTroubleshoot tooan macchina virtuale di Azure | Documenti Microsoft
description: Come tootroubleshoot problemi, ad esempio 'Connessione SSH non riuscito' o 'Connessione SSH rifiutata' per una macchina virtuale di Azure che eseguono Linux.
keywords: connessione SSH rifiutata, errore SSH, SSH Azure, connessione SSH non riuscita
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: dcb82e19-29b2-47bb-99f2-900d4cfb5bbb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: iainfou
ms.openlocfilehash: dfb4e75e571c8306edf5f300c4e0f07a5fe7750a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-ssh-connections-tooan-azure-linux-vm-that-fails-errors-out-or-is-refused"></a>Risoluzione dei problemi tooan connessioni SSH VM Linux di Azure non riesce, gli errori, che è stata rifiutata
Esistono vari motivi che si verificano errori di Secure Shell (SSH), gli errori di connessione SSH o SSH viene rifiutato quando si tenta di macchina virtuale di Linux tooa tooconnect (VM). In questo articolo consente di trovare e problemi di hello corretto. È possibile utilizzare hello portale di Azure CLI di Azure o estensione accesso della macchina virtuale per Linux tootroubleshoot e risolvere i problemi di connessione.

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Se è necessario ulteriore assistenza in qualsiasi punto in questo articolo, è possibile contattare hello Azure esperti in [hello forum MSDN di Azure e di Overflow dello Stack](http://azure.microsoft.com/support/forums/). In alternativa, è possibile archiviare un evento imprevisto di supporto tecnico di Azure. Passare toohello [sito del supporto tecnico di Azure](http://azure.microsoft.com/support/options/) e selezionare **ottenere supporto**. Per informazioni sull'utilizzo di supporto di Azure, leggere hello [supporto tecnico di Microsoft Azure domande frequenti su](http://azure.microsoft.com/support/faq/).

## <a name="quick-troubleshooting-steps"></a>Passaggi rapidi per la risoluzione dei problemi
Dopo ogni passaggio della risoluzione dei problemi, provare a riconnettersi toohello macchina virtuale.

1. Reimposta configurazione SSH hello.
2. Reimpostare le credenziali di hello per utente hello.
3. Verificare hello [Network Security Group](../../virtual-network/virtual-networks-nsg.md) regole consentono il traffico SSH.
   * Verificare che una regola del gruppo di sicurezza di rete esista traffico SSH toopermit (per impostazione predefinita, la porta TCP 22).
   * Non è possibile usare il reindirizzamento o mapping delle porte senza usare Azure Load Balancer.
4. Controllare hello [integrità delle risorse di VM](../../resource-health/resource-health-overview.md). 
   * Verificare che hello VM report come integro.
   * Se è abilitata la diagnostica di avvio, verificare gli errori di avvio nei registri hello hello VM non è in corso.
5. Riavviare hello macchina virtuale.
6. Ridistribuire hello macchina virtuale.

Continuare la lettura per la procedura di risoluzione dei problemi e spiegazioni più dettagliate.

## <a name="available-methods-tootroubleshoot-ssh-connection-issues"></a>Problemi di connessione SSH tootroubleshoot metodi disponibili
È possibile reimpostare le credenziali o la configurazione SSH utilizzando uno dei seguenti metodi hello:

* [Portale di Azure](#use-the-azure-portal) : eccellente se è necessario tooquickly Reimposta configurazione SSH hello o chiave SSH e non avere hello installati gli strumenti di Azure.
* [Azure CLI 2.0](#use-the-azure-cli-20) : se sono già nella riga di comando hello rapidamente la reimpostazione della configurazione di SSH hello o le credenziali. È inoltre possibile utilizzare hello [1.0 CLI di Azure](#use-the-azure-cli-10)
* [L'estensione VMAccessForLinux Azure](#use-the-vmaccess-extension) : creare e riutilizzare json definizione file tooreset hello SSH configurazione o credenziali dell'utente.

Dopo ogni passaggio della risoluzione dei problemi, provare a riconnettersi tooyour macchina virtuale. Se non è possibile connettersi, provare a passaggio successivo hello.

## <a name="use-hello-azure-portal"></a>Utilizzare hello portale di Azure
Hello portale di Azure fornisce un hello tooreset rapidamente le credenziali utente o di configurazione di SSH senza installare gli strumenti nel computer locale.

Selezionare la macchina virtuale nel portale di Azure hello. Scorrere verso il basso toohello **supporto + Troubleshooting** sezione e selezionare **reimpostazione password** come hello di esempio seguente:

![Configurazione SSH per la reimpostazione o credenziali nel portale di Azure hello](./media/troubleshoot-ssh-connection/reset-credentials-using-portal.png)

### <a name="reset-hello-ssh-configuration"></a>Reimposta configurazione SSH hello
Come primo passaggio, selezionare `Reset configuration only` da hello **modalità** dal menu a discesa in hello precedente schermata, quindi fare clic su hello **reimpostare** pulsante. Una volta completata questa azione, riprovare tooaccess la macchina virtuale.

### <a name="reset-ssh-credentials-for-a-user"></a>Reimpostare le credenziali SSH di un utente
le credenziali di hello tooreset di un utente esistente, selezionare l'opzione `Reset SSH public key` o `Reset password` da hello **modalità** dal menu a discesa come hello precedente schermata. Specificare nome utente di hello e una chiave SSH o nuova password, quindi fare clic su hello **reimpostare** pulsante.

È anche possibile creare un utente con privilegi sudo su hello VM da questo menu. Immettere un nuovo nome utente e password associata o una chiave SSH e quindi fare clic su hello **reimpostare** pulsante.

## <a name="use-hello-azure-cli-20"></a>Utilizzare hello Azure CLI 2.0
Se hai già fatto, installare più recente hello [CLI di Azure 2.0](/cli/azure/install-az-cli2) e accedere con un account Azure tooan [accesso az](/cli/azure/#login).

Se è stato creato e caricato un'immagine del disco Linux personalizzata, verificare che hello [agente Linux di Microsoft Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) versione 2.0.5 o versione successiva è installato. Per le macchine virtuali create tramite le immagini della raccolta, questa estensione dell'accesso è già installata e configurata automaticamente.

### <a name="reset-ssh-configuration"></a>Reimpostare la configurazione SSH
È possibile inizialmente try reimpostazione hello SSH toodefault i valori di configurazione e il riavvio server SSH hello hello macchina virtuale. Si noti che ciò non modifica il nome di account utente di hello, password o le chiavi SSH.
Hello seguente utilizza [az vm utente reset-ssh](/cli/azure/vm/user#reset-ssh) tooreset hello SSH configurazione macchina virtuale denominata hello `myVM` in `myResourceGroup`. Usare i valori personalizzati come di seguito:

```azurecli
az vm user reset-ssh --resource-group myResourceGroup --name myVM
```

### <a name="reset-ssh-credentials-for-a-user"></a>Reimpostare le credenziali SSH di un utente
Hello seguente utilizza [aggiornamento dell'utente vm az](/cli/azure/vm/user#update) tooreset hello le credenziali per `myUsername` toohello valore specificato in `myPassword`, nella macchina virtuale denominata hello `myVM` in `myResourceGroup`. Usare i valori personalizzati come di seguito:

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
     --username myUsername --password myPassword
```

Se si utilizza l'autenticazione con chiave SSH, è possibile reimpostare la chiave SSH hello per un determinato utente. Hello seguente utilizza **az vm accesso utente di linux set** tooupdate hello SSH chiave archiviata in `~/.ssh/id_rsa.pub` per utente hello denominato `myUsername`, nella macchina virtuale denominata hello `myVM` in `myResourceGroup`. Usare i valori personalizzati come di seguito:

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
    --username myUsername --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="use-hello-vmaccess-extension"></a>Utilizzare l'estensione VMAccess hello
legge un file json che definisce le azioni toocarry out Hello estensione accesso della macchina virtuale per Linux. Queste azioni includono la reimpostazione SSHD, la reimpostazione di una chiave SSH o l'aggiunta di un utente. È comunque usare hello toocall di hello Azure CLI estensione VMAccess, ma è possibile riutilizzare i file json hello in più macchine virtuali se lo si desidera. Questo approccio consente toocreate un archivio di file json che può essere chiamato per specificato scenari.

### <a name="reset-sshd"></a>Reimpostare un disco SSHD
Creare un file denominato `settings.json` con hello seguente contenuto:

```json
{  
    "reset_ssh":"True"
}
```

Utilizzando hello CLI di Azure, è possibile quindi chiamare hello `VMAccessForLinux` estensione tooreset connessione SSHD specificando il file json. Hello seguente utilizza [az vm estensione set](/cli/azure/vm/extension#set) tooreset SSHD nella macchina virtuale denominata hello `myVM` in `myResourceGroup`. Usare i valori personalizzati come di seguito:

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

### <a name="reset-ssh-credentials-for-a-user"></a>Reimpostare le credenziali SSH di un utente
Se SSHD toofunction venga visualizzato correttamente, è possibile reimpostare le credenziali di hello per un utente donatore. password di hello tooreset per un utente, creare un file denominato `settings.json`. esempio Hello Reimposta credenziali hello per `myUsername` toohello valore specificato in `myPassword`. Immettere hello righe in seguito il `settings.json` file, utilizzando i valori personalizzati:

```json
{
    "username":"myUsername", "password":"myPassword"
}
```

O tooreset hello chiave SSH per un utente, creare innanzitutto un file denominato `settings.json`. esempio Hello Reimposta credenziali hello per `myUsername` toohello valore specificato in `myPassword`, nella macchina virtuale denominata hello `myVM` in `myResourceGroup`. Immettere hello righe in seguito il `settings.json` file, utilizzando i valori personalizzati:

```json
{
    "username":"myUsername", "ssh_key":"mySSHKey"
}
```

Dopo avere creato il file json, utilizzare hello toocall CLI di Azure di hello `VMAccessForLinux` tooreset estensione le credenziali dell'utente SSH specificando il file json. esempio Hello Reimposta credenziali sulla macchina virtuale denominata hello `myVM` in `myResourceGroup`. Usare i valori personalizzati come di seguito:

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

## <a name="use-hello-azure-cli-10"></a>Utilizzare hello Azure CLI 1.0
Se hai già fatto, [installare hello Azure CLI 1.0 e connettere tooyour sottoscrizione di Azure](../../cli-install-nodejs.md). Verificare di usare la modalità di Resource Manager come indicato di seguito:

```azurecli
azure config mode arm
```

Se è stato creato e caricato un'immagine del disco Linux personalizzata, verificare che hello [agente Linux di Microsoft Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) versione 2.0.5 o versione successiva è installato. Per le macchine virtuali create tramite le immagini della raccolta, questa estensione dell'accesso è già installata e configurata automaticamente.

### <a name="reset-ssh-configuration"></a>Reimpostare la configurazione SSH
configurazione di SSHD Hello stessa sia configurato correttamente o hello servizio ha rilevato un errore. È possibile reimpostare toomake SSHD che configurazione SSH hello stesso sia valido. Reimpostazione SSHD deve essere hello sulla risoluzione dei problemi innanzitutto che eseguire.

esempio Hello Reimposta SSHD in una macchina virtuale denominata `myVM` nel gruppo di risorse hello denominato `myResourceGroup`. Usare i nomi della macchina virtuale e del gruppo di risorse personalizzati come segue:

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --reset-ssh
```

### <a name="reset-ssh-credentials-for-a-user"></a>Reimpostare le credenziali SSH di un utente
Se SSHD toofunction venga visualizzato correttamente, è possibile reimpostare la password di hello per un utente donatore. esempio Hello Reimposta credenziali hello per `myUsername` toohello valore specificato in `myPassword`, nella macchina virtuale denominata hello `myVM` in `myResourceGroup`. Usare i valori personalizzati come di seguito:

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
     --user-name myUsername --password myPassword
```

Se si utilizza l'autenticazione con chiave SSH, è possibile reimpostare la chiave SSH hello per un determinato utente. dopo gli aggiornamenti di esempio Hello hello chiave SSH archiviata in `~/.ssh/id_rsa.pub` per utente hello denominato `myUsername`, nella macchina virtuale denominata hello `myVM` in `myResourceGroup`. Usare i valori personalizzati come di seguito:

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --user-name myUsername --ssh-key-file ~/.ssh/id_rsa.pub
```


## <a name="restart-a-vm"></a>Riavviare una macchina virtuale
Se si hanno reimpostare le credenziali di configurazione e dell'utente SSH hello o ha rilevato un errore in tal modo, è possibile provare a riavviare hello VM tooaddress sottostanti i problemi di calcolo.

### <a name="azure-portal"></a>Portale di Azure
toorestart una macchina virtuale utilizzando hello Azure selezionare portale, hello la macchina virtuale e fare clic su **riavviare** pulsante come hello di esempio seguente:

![Riavviare una macchina virtuale nel portale di Azure hello](./media/troubleshoot-ssh-connection/restart-vm-using-portal.png)

### <a name="azure-cli-10"></a>Interfaccia della riga di comando di Azure 1.0
Dopo il riavvio di esempio Hello hello macchina virtuale denominata `myVM` nel gruppo di risorse hello denominato `myResourceGroup`. Usare i valori personalizzati come di seguito:

```azurecli
azure vm restart --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a>Interfaccia della riga di comando di Azure 2.0
Hello seguente utilizza [riavvio vm az](/cli/azure/vm#restart) toorestart hello macchina virtuale denominata `myVM` nel gruppo di risorse hello denominato `myResourceGroup`. Usare i valori personalizzati come di seguito:

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```


## <a name="redeploy-a-vm"></a>Ridistribuire una VM
È possibile ridistribuire un nodo tooanother della macchina virtuale in Azure, che può correggere eventuali problemi di rete sottostante. Per informazioni sulla ridistribuzione di una macchina virtuale, vedere [ridistribuire toonew macchina virtuale Azure nodo](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

> [!NOTE]
> Al termine di questa operazione, dati su disco temporaneo andranno persi e verranno aggiornati gli indirizzi IP dinamici che sono associati a macchina virtuale hello.
> 
> 

### <a name="azure-portal"></a>Portale di Azure
tooredeploy una macchina virtuale utilizzando hello Azure selezionare portale, la macchina virtuale e scorrere verso il basso toohello **supporto + Troubleshooting** sezione. Fare clic su hello **ridistribuire** pulsante come hello di esempio seguente:

![Ridistribuire una macchina virtuale in hello portale di Azure](./media/troubleshoot-ssh-connection/redeploy-vm-using-portal.png)

### <a name="azure-cli-10"></a>Interfaccia della riga di comando di Azure 1.0
Hello seguenti distribuzioni di esempio hello macchina virtuale denominata `myVM` nel gruppo di risorse hello denominato `myResourceGroup`. Usare i valori personalizzati come di seguito:

```azurecli
azure vm redeploy --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a>Interfaccia della riga di comando di Azure 2.0
Hello in seguito ad esempio [Ridistribuisci vm az](/cli/azure/vm#redeploy) tooredeploy hello macchina virtuale denominata `myVM` nel gruppo di risorse hello denominato `myResourceGroup`. Usare i valori personalizzati come di seguito:

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM
```

## <a name="vms-created-by-using-hello-classic-deployment-model"></a>Macchine virtuali create con modello di distribuzione classica hello
Ripetere questi passaggi tooresolve hello più comuni SSH errori di connessione per le macchine virtuali che sono state create tramite il modello di distribuzione classica hello. Dopo ogni passaggio, provare a riconnettersi toohello macchina virtuale.

* Reimpostare l'accesso remoto da hello [portale di Azure](https://portal.azure.com). Hello portale di Azure, selezionare la macchina virtuale e fare clic su hello **Reimposta accesso remoto...**  pulsante.
* Riavviare hello macchina virtuale. In hello [portale di Azure](https://portal.azure.com), selezionare la macchina virtuale e fare clic su hello **riavviare** pulsante.
    
* Ridistribuire hello VM tooa nuovo nodo di Azure. Per informazioni su come tooredeploy una macchina virtuale, vedere [ridistribuire toonew macchina virtuale Azure nodo](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
  
    Al termine di questa operazione, dati su disco temporaneo andranno persi e verranno aggiornati gli indirizzi IP dinamici che sono associati a macchina virtuale hello.
* Seguire le istruzioni hello [come tooreset una password o SSH per le macchine virtuali basate su Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) per:
  
  * Hello di reimpostazione password o chiave SSH.
  * Creare un account utente *sudo*.
  * Reimposta configurazione SSH hello.
* Controllare l'integrità delle risorse della macchina virtuale di hello per eventuali problemi della piattaforma.<br>
     Selezionare la macchina virtuale e scorrere verso il basso fino a **Impostazioni** > **Controlla integrità**.

## <a name="additional-resources"></a>Risorse aggiuntive
* Se si riesce ancora tooSSH tooyour VM dopo seguente hello dopo i passaggi, vedere [ulteriori passaggi di risoluzione dei problemi](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooreview ulteriori passaggi tooresolve il problema.
* Per ulteriori informazioni sulla risoluzione dei problemi di accesso all'applicazione, vedere [applicazione tooan accesso di risoluzione dei problemi in esecuzione in una macchina virtuale di Azure](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* Per ulteriori informazioni sulla risoluzione dei problemi delle macchine virtuali che sono state create tramite il modello di distribuzione classica hello, vedere [come tooreset una password o SSH per le macchine virtuali basate su Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

