---
title: risoluzione dei problemi SSH aaaDetailed per una macchina virtuale di Azure | Documenti Microsoft
description: Ulteriori SSH risoluzione di problemi di connessione tooan macchina virtuale di Azure
keywords: connessione SSH rifiutata,errore SSH,SSH Azure,connessione SSH non riuscita
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: b8e8be5f-e8a6-489d-9922-9df8de32e839
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: support-article
ms.date: 07/06/2017
ms.author: iainfou
ms.openlocfilehash: 3f711e53a8251f8c06dbb589a258222566a4ae1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="detailed-ssh-troubleshooting-steps-for-issues-connecting-tooa-linux-vm-in-azure"></a>SSH dettagliate risoluzione di problemi di connessione tooa VM Linux di Azure
Vi sono molti i motivi possibili che client SSH hello potrebbe non essere tooreach in grado di servizio SSH hello in hello VM. Se sono state eseguite tramite hello più [generale SSH risoluzione](troubleshoot-ssh-connection.md), è necessario toofurther risolvere il problema di connessione hello. In questo articolo in modo semplificato dettagliate sulla risoluzione dei problemi toodetermine di passaggi in cui non è possibile eseguire la connessione SSH hello e come tooresolve è.

## <a name="take-preliminary-steps"></a>Operazioni preliminari
Hello diagramma seguente mostra i componenti di hello coinvolti.

![Diagramma che mostra i componenti del servizio SSH](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot1.png)

Hello passaggi seguenti consentono di isolare origine hello dell'errore hello e scoprire le soluzioni.

1. Controllare lo stato di hello di hello VM nel portale di hello.
   In hello [portale di Azure](https://portal.azure.com)selezionare **macchine virtuali** > *nome della macchina virtuale*.

   Hello riquadro di stato per hello VM mostreranno **esecuzione**. Scorrere verso il basso tooshow attività recente calcolo, archiviazione e risorse di rete.

2. Selezionare **impostazioni** tooexamine endpoint, gli indirizzi IP, gruppi di sicurezza di rete e altre impostazioni.

   Hello macchina virtuale deve disporre di un endpoint definito per il traffico SSH che è possibile visualizzare in **endpoint** o  **[il gruppo di sicurezza di rete](../../virtual-network/virtual-networks-nsg.md)**. Gli endpoint nelle VM create tramite Resource Manager vengono archiviati in un gruppo di sicurezza di rete. Inoltre, verificare che le regole di hello siano stati applicati toohello gruppo di sicurezza di rete e che sta viene fatto riferimento nella subnet hello.

connettività di rete tooverify endpoint hello configurato e controllare se è possibile raggiungere hello VM tramite un altro protocollo, ad esempio HTTP o un altro servizio.

Dopo questi passaggi, riprovare hello connessione SSH.

## <a name="find-hello-source-of-hello-issue"></a>Trovare hello origine del problema hello
client di Hello SSH nel computer in uso potrebbe non riuscire il servizio SSH hello tooreach su hello Azure VM scadenza tooissues o errori di configurazione in hello seguenti aree:

* [Computer client SSH](#source-1-ssh-client-computer)
* [Dispositivo periferico dell'organizzazione](#source-2-organization-edge-device)
* [Endpoint del servizio cloud ed elenco di controllo di accesso (ACL)](#source-3-cloud-service-endpoint-and-acl)
* [Gruppi di sicurezza di rete](#source-4-network-security-groups)
* [VM di Azure basata su Linux](#source-5-linux-based-azure-virtual-machine)

## <a name="source-1-ssh-client-computer"></a>Origine 1: computer client SSH
tooeliminate computer come origine di hello di errore hello, verificare che è possibile rendere SSH connessioni tooanother locale, i computer basati su Linux.

![Diagramma che evidenzia i componenti del computer client SSH](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot2.png)

Se la connessione hello non riesce, verificare la presenza hello seguenti problemi nel computer in uso:

* Un'impostazione locale del firewall che blocca il traffico SSH in ingresso o in uscita (TCP 22)
* Software proxy client installato localmente che impedisce le connessioni SSH
* Software di monitoraggio della rete installato localmente che impedisce le connessioni SSH
* Altri tipi di software di sicurezza che eseguono il monitoraggio del traffico o consentono/non consentono tipi di traffico specifici

Se una di queste condizioni si applica, temporaneamente disattivare software hello e provare un toofind SSH connessione tooan locale computer out motivo hello connessione hello è stato bloccato nel computer in uso. Quindi utilizzare connessioni di rete amministratore toocorrect hello software impostazioni tooallow SSH.

Se si utilizza l'autenticazione del certificato, verificare di disporre queste autorizzazioni toohello .ssh cartella nella home directory:

* Chmod 700 ~/.ssh
* Chmod 644 ~/.ssh/\*.pub
* Chmod 600 ~/.ssh/id_rsa (o qualsiasi altro file in cui siano archiviate le chiavi private)
* Chmod 644 ~/.ssh/known_hosts (contiene host che si è connessi toovia SSH)

## <a name="source-2-organization-edge-device"></a>Origine 2: dispositivo periferico dell'organizzazione
tooeliminate il dispositivo perimetrale dell'organizzazione come origine di hello di errore hello, verificare che un computer che è direttamente connesso toohello Internet può rendere tooyour connessioni SSH macchina virtuale di Azure. Se si accede tramite una VPN da sito a sito o una connessione Azure ExpressRoute hello macchina virtuale, andare troppo[origine 4: gruppi di sicurezza di rete](#nsg).

![Diagramma che evidenzia il dispositivo periferico dell'organizzazione](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot3.png)

Se non si dispone di un computer che è direttamente connesso toohello Internet, creare una nuova macchina virtuale di Azure nel proprio risorse gruppo o un servizio cloud e utilizzarlo. Per altre informazioni, vedere [Creare una macchina virtuale che esegue Linux in Azure](quick-create-cli.md). Al termine con i test, eliminare hello risorse gruppo o macchina virtuale e il servizio cloud.

Se è possibile creare una connessione SSH con un computer che è direttamente connesso toohello Internet, controllare il dispositivo perimetrale dell'organizzazione per:

* Un firewall interno che sta bloccando il traffico SSH con hello Internet
* Un server proxy impedisce le connessioni SSH
* Un software per il rilevamento di intrusioni o il monitoraggio della rete in esecuzione sui dispositivi presenti nella rete perimetrale impedisce le connessioni SSH

Funziona con le impostazioni di rete amministratore toocorrect hello del traffico organizzazione edge dispositivi tooallow SSH con hello Internet.

## <a name="source-3-cloud-service-endpoint-and-acl"></a>Origine 3: endpoint del servizio cloud e ACL
> [!NOTE]
> L'origine si applica solo tooVMs che sono state create tramite il modello di distribuzione classica hello. Per le macchine virtuali che sono state create usando Gestione risorse, ignorare troppo[origine 4: gruppi di sicurezza di rete](#nsg).

endpoint del servizio cloud hello tooeliminate e ACL come origine di hello di errore hello, verificare che un'altra macchina virtuale di Azure in hello stessa rete virtuale è possibile apportare tooyour connessioni SSH macchina virtuale.

![Diagramma che evidenzia l'endpoint del servizio cloud e l'elenco di controllo di accesso](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot4.png)

Se non si dispone di un'altra macchina virtuale in hello stessa rete virtuale, è possibile creare facilmente uno. Per ulteriori informazioni, vedere [creare una VM Linux in Azure utilizzando hello CLI](quick-create-cli.md). Eliminare hello VM aggiuntive al termine con i test.

Se è possibile creare una connessione SSH con una macchina virtuale in hello virtuale stessa rete, controllare hello seguenti aree:

* **configurazione dell'endpoint Hello del traffico SSH sulla destinazione hello macchina virtuale.** porta TCP privata Hello dell'endpoint hello deve corrispondere la porta TCP hello su quale hello SSH servizio su hello macchina virtuale è in ascolto. (porta predefinita hello è 22). Verifica del numero di porta SSH TCP hello nel portale di Azure hello selezionando **macchine virtuali** > *nome della macchina virtuale* > **impostazioni**  >  **Endpoint**.
* **Hello ACL per l'endpoint di traffico hello SSH nella macchina virtuale di destinazione hello.** Un ACL consente toospecify consentito o negato il traffico in ingresso da hello Internet, in base al relativo indirizzo IP di origine. ACL configurato in modo errato può impedire l'endpoint di toohello traffico SSH in ingresso. Controllare il tooensure ACL che è consentito il traffico in ingresso da indirizzi IP pubblici hello del proxy o un altro server edge. Per altre informazioni, vedere [Informazioni sugli elenchi di controllo di accesso (ACL) di rete](../../virtual-network/virtual-networks-acl.md).

endpoint di hello tooeliminate come origine del problema hello, rimuovere l'endpoint corrente di hello, creare un altro endpoint e specificare il nome SSH hello (porta TCP 22 per il numero di porta pubblica e privata hello). Per altre informazioni, vedere [Configurare endpoint in una macchina virtuale in Azure](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

<a id="nsg"></a>

## <a name="source-4-network-security-groups"></a>Origine 4: gruppi di sicurezza di rete
Gruppi di sicurezza di rete consentono di toohave un controllo più granulare del traffico consentito in ingresso e in uscita. È possibile creare regole che si estendono alle subnet e ai servizi cloud in una rete virtuale di Azure. Controllare il tooensure di regole gruppo di sicurezza rete tale tooand traffico SSH da hello che Internet è consentita.
Per altre informazioni, vedere [Informazioni sui gruppi di sicurezza di rete](../../virtual-network/virtual-networks-nsg.md).

È inoltre possibile utilizzare IP verificare la configurazione di NSG hello toovalidate. Per altre informazioni, vedere [Panoramica del monitoraggio della rete in Azure](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-monitoring-overview). 

## <a name="source-5-linux-based-azure-virtual-machine"></a>Origine 5: macchina virtuale di Azure basata su Linux
origine di ultima Hello di possibili problemi è hello Azure macchina virtuale stessa.

![Diagramma che evidenzia la macchina virtuale di Azure basata su Linux](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot5.png)

Se non è già fatto, seguire le istruzioni di hello [tooreset una password o SSH per le macchine virtuali basate su Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

Provare nuovamente la connessione dal computer. Se il problema persiste, hello Ecco alcune delle possibili problemi di hello:

* Hello servizio SSH non è in esecuzione nella macchina virtuale di destinazione hello.
* Hello servizio SSH non è in ascolto sulla porta TCP 22. tootest, installare un client telnet nel computer locale ed eseguire "telnet *Nomeserviziocloud*. cloudapp.net 22". Questo passaggio determina se macchina virtuale hello consente a endpoint di comunicazione in entrata e in uscita toohello SSH.
* firewall locale di Hello nella macchina virtuale di destinazione hello dispone di regole che impediscono il traffico in ingresso o in uscita SSH.
* Rilevamento delle intrusioni o software che è in esecuzione nella macchina virtuale di Azure hello di monitoraggio della rete impedisce le connessioni SSH.

## <a name="additional-resources"></a>Risorse aggiuntive
Per ulteriori informazioni sulla risoluzione dei problemi di accesso all'applicazione, vedere [applicazione tooan accesso di risoluzione dei problemi in esecuzione in una macchina virtuale di Azure](troubleshoot-app-connection.md)
