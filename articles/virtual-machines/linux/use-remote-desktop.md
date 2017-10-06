---
title: Desktop remoto di aaaUse tooa VM Linux di Azure | Documenti Microsoft
description: Informazioni su come tooinstall e configurare Desktop remoto (xrdp) tooconnect tooa VM Linux in Azure tramite strumenti grafici
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: iainfou
ms.openlocfilehash: 64d30be101ceeb49fc05bb10293ad63db358efe3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-remote-desktop-tooconnect-tooa-linux-vm-in-azure"></a>Installare e configurare Desktop remoto tooconnect tooa VM Linux in Azure
Le macchine virtuali Linux (VM) in Azure vengono solitamente gestite dalla riga di comando hello utilizzando una connessione sicura shell (SSH). Quando tooLinux nuovo, o per gli scenari di risoluzione dei problemi veloci, può risultare più semplice utilizzare hello di desktop remoto. Questo articolo come dettagli tooinstall e configurare un ambiente desktop ([xfce](https://www.xfce.org)) e desktop remoto ([xrdp](http://www.xrdp.org)) per le VM Linux con modello di distribuzione di gestione risorse di hello.


## <a name="prerequisites"></a>Prerequisiti
Questo articolo richiede l'esistenza di una VM Linux di Azure. Se è necessario toocreate una macchina virtuale, utilizzare uno dei seguenti metodi hello:

- Hello [CLI di Azure 2.0](quick-create-cli.md)
- Hello [portale di Azure](quick-create-portal.md)


## <a name="install-a-desktop-environment-on-your-linux-vm"></a>Installare un ambiente desktop nella VM Linux
La maggior parte delle macchine virtuali Linux di Azure non presenta un ambiente desktop installato per impostazione predefinita. Le macchine virtuali Linux in genere vengono gestite usando connessioni SSH piuttosto che un ambiente desktop. In Linux esistono diversi ambienti desktop tra i quali è possibile scegliere. A seconda della scelta effettuata dell'ambiente desktop, potrebbe utilizzi uno too2 GB di spazio su disco, richiedere 5 too10 minuti tooinstall e configurare tutti i pacchetti hello necessario.

esempio Hello installa lightweight hello [xfce4](https://www.xfce.org/) ambiente desktop in una VM Ubuntu. I comandi per altre distribuzioni variano leggermente (utilizzare `yum` tooinstall su Red Hat Enterprise Linux e configurare appropriato `selinux` regole o utilizzare `zypper` tooinstall in SUSE, ad esempio).

Prima di tutto, SSH tooyour macchina virtuale. esempio Hello connette toohello macchina virtuale denominata *myvm.westus.cloudapp.azure.com* con il nome utente hello di *azureuser*:

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

Se si utilizza Windows e altre informazioni sull'uso di SSH, vedere [come chiavi, toouse SSH tramite Windows](ssh-from-windows.md).

Successivamente, installare xfce usando `apt` come indicato di seguito:

```bash
sudo apt-get update
sudo apt-get install xfce4
```

## <a name="install-and-configure-a-remote-desktop-server"></a>Installare e configurare un server di desktop remoto
Dopo aver creato un ambiente desktop installato, è possibile configurare un toolisten di servizi desktop remoto per le connessioni in ingresso. [xrdp](http://xrdp.org) è un server Remote Desktop Protocol (RDP) open source che è disponibile nella maggior parte delle distribuzioni Linux e funziona bene con xfce. Installare xrdp nella VM Ubuntu come indicato di seguito:

```bash
sudo apt-get install xrdp
```

Indicare xrdp quali toouse ambiente desktop quando si avvia la sessione. Configurare xrdp toouse xfce come ambiente di desktop come indicato di seguito:

```bash
echo xfce4-session >~/.xsession
```

Riavviare servizio xrdp hello per effetto di hello modifiche tootake come indicato di seguito:

```bash
sudo service xrdp restart
```


## <a name="set-a-local-user-account-password"></a>Impostare una password per l'account utente locale
Se la password dell'account utente è stata impostata al momento della creazione della macchina virtuale, ignorare questo passaggio. Se solo di utilizzare l'autenticazione con chiave SSH e password di un account locale non è impostato, specificare una password prima di utilizzare xrdp toolog tooyour VM. xrdp non può accettare chiavi SSH per l'autenticazione. esempio Hello specifica una password per l'account utente di hello *azureuser*:

```bash
sudo passwd azureuser
```

> [!NOTE]
> Specificare una password non aggiorna gli account di accesso delle password SSHD configurazione toopermit se attualmente non. Da una prospettiva di sicurezza, è possibile desidera tooconnect tooyour macchina virtuale con un tunnel SSH utilizzando l'autenticazione basata su chiavi e quindi connettersi tooxrdp. In questo caso, ignorare hello successivo passaggio nella creazione di un protezione gruppo regola tooallow remote desktop il traffico di rete.


## <a name="create-a-network-security-group-rule-for-remote-desktop-traffic"></a>Creare una regola del gruppo di sicurezza di rete per il traffico di Desktop remoto
tooallow Desktop remoto traffico tooreach VM Linux, una regola gruppo di sicurezza di rete deve toobe creato che consenta il traffico TCP nella porta 3389 tooreach la macchina virtuale. Per altre informazioni sulle regole dei gruppi di sicurezza di rete, vedere [Che cos'è un gruppo di sicurezza di rete](../../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). È anche possibile [utilizzare una regola gruppo di sicurezza di rete di Azure toocreate portale hello](../windows/nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Negli esempi seguenti Hello creano una regola gruppo di sicurezza di rete con [creare una regola gruppo rete az](/cli/azure/network/nsg/rule#create) denominato *myNetworkSecurityGroupRule* troppo*consentire* traffico su *tcp* porta *3389*.

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1010 \
    --destination-port-range 3389
```


## <a name="connect-your-linux-vm-with-a-remote-desktop-client"></a>Connettere la macchina virtuale Linux con un client di Desktop remoto
Aprire il client desktop remoto locale e connettersi toohello l'indirizzo IP o nome DNS della VM Linux. Immettere hello nome utente e password per account utente di hello nella VM come indicato di seguito:

![Connettersi tooxrdp utilizzando il client Desktop remoto](./media/use-remote-desktop/remote-desktop-client.png)

Dopo l'autenticazione, ambiente di desktop xfce hello verrà caricate ed esaminare toohello simile esempio seguente:

![ambiente desktop xfce tramite xrdp](./media/use-remote-desktop/xfce-desktop-environment.png)


## <a name="troubleshoot"></a>Risoluzione dei problemi
Se non è possibile connettersi tooyour VM Linux utilizzando un client Desktop remoto, utilizzare `netstat` sul tooverify VM Linux che la macchina virtuale è in attesa come indicato di seguito per le connessioni RDP:

```bash
sudo netstat -plnt | grep rdp
```

Hello seguendo l'esempio hello macchina virtuale è in ascolto sulla porta TCP 3389 come previsto:

```bash
tcp     0     0      127.0.0.1:3350     0.0.0.0:*     LISTEN     53192/xrdp-sesman
tcp     0     0      0.0.0.0:3389       0.0.0.0:*     LISTEN     53188/xrdp
```

Se non è in ascolto il servizio di xrdp hello, in una VM Ubuntu riavviare servizio hello come indicato di seguito:

```bash
sudo service xrdp restart
```

Revisione accede *var/log*Thug nella VM Ubuntu per indicazioni come servizio hello toowhy non risponde. È anche possibile monitorare hello syslog durante un tooview tentativo di connessione desktop remoto gli eventuali errori:

```bash
tail -f /var/log/syslog
```

Altre distribuzioni Linux, ad esempio Red Hat Enterprise Linux e SUSE possono avere servizi toorestart modi diversi e tooreview percorsi di file alternativo per il log.

Se si non riceve alcuna risposta il client desktop remoto e non viene visualizzato alcun evento nel Registro di sistema hello, ciò indica che il traffico di desktop remoto non riesce a raggiungere hello VM. Esaminare il tooensure di regole gruppo di sicurezza di rete di disporre di un toopermit regola TCP sulla porta 3389. Per altre informazioni, vedere [Risolvere i problemi di connettività delle applicazioni in una macchina virtuale di Azure per Linux](../windows/troubleshoot-app-connection.md).


## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni sulla creazione e l'uso di chiavi SSH con macchine virtuali Linux, vedere [Creare una coppia di chiavi SSH pubblica e privata per le macchine virtuali di Linux](mac-create-ssh-keys.md).

Per informazioni sull'utilizzo di SSH da Windows, vedere [come chiavi, toouse SSH tramite Windows](ssh-from-windows.md).

