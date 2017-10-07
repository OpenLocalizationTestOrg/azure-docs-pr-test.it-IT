---
title: 'Risolvere un problema di Backup di Azure: stato dell''agente guest non disponibile | Microsoft Docs'
description: 'Sintomi, cause e risoluzioni di tooerror correlati gli errori di Backup di Azure: Impossibile comunicare con l''agente VM hello'
services: backup
documentationcenter: 
author: genlin
manager: cshepard
editor: 
keywords: "Backup di Azure; agente di macchine virtuali; connettività di rete;"
ms.assetid: 4b02ffa4-c48e-45f6-8363-73d536be4639
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: genli;markgal;
ms.openlocfilehash: 724c61ba80d0a9ef91a5f8543ae72bb86968881b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-backup-failure-issues-with-agent-andor-extension"></a>Risolvere i problemi di Backup di Azure relativi all'agente e/o all'estensione

Questo articolo fornisce la risoluzione dei problemi toohelp passaggi risolvere gli errori di Backup relative tooproblems nella comunicazione con l'agente di macchine Virtuali e l'estensione.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="vm-agent-unable-toocommunicate-with-azure-backup"></a>Agente VM toocommunicate Impossibile con Backup di Azure
Dopo che è necessario registrarla e pianificare una macchina virtuale per hello servizio Azure Backup, Backup avvia il processo di hello comunicando con hello tootake agente VM uno snapshot del punto nel tempo. Una delle seguenti condizioni hello potrebbe impedire snapshot hello da viene attivata, che a sua volta può causare un errore tooBackup. Di seguito sono riportati i passaggi in hello dato ordine di risoluzione dei problemi e ripetere l'operazione.
##### <a name="cause-1-hello-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>Causa 1: [hello VM non è accesso a Internet](#the-vm-has-no-internet-access)
##### <a name="cause-2-hello-agent-is-installed-in-hello-vm-but-is-unresponsive-for-windows-vmsthe-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>Causa 2: [hello agente viene installato nella macchina virtuale hello, ma non risponde (per le macchine virtuali di Windows)](#the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms)
##### <a name="cause-3-hello-agent-installed-in-hello-vm-is-out-of-date-for-linux-vmsthe-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>Causa 3: [agente hello installato nella macchina virtuale hello è scaduto (per le macchine virtuali Linux)](#the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms)
##### <a name="cause-4-hello-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-takenthe-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>Causa 4: [. Impossibile recuperare lo stato dello snapshot hello o non può essere eseguito uno snapshot](#the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken)
##### <a name="cause-5-hello-backup-extension-fails-tooupdate-or-loadthe-backup-extension-fails-to-update-or-load"></a>Causa 5: [estensione backup hello ha esito negativo tooupdate o carico](#the-backup-extension-fails-to-update-or-load)

## <a name="snapshot-operation-failed-due-toono-network-connectivity-on-hello-virtual-machine"></a>Snapshot non riuscita a causa di toono la connettività di rete nella macchina virtuale hello
Dopo che è necessario registrarla e pianificare una macchina virtuale per hello servizio Azure Backup, Backup avvia il processo di hello comunicando con snapshot di un punto nel tempo tootake hello VM estensione del backup. Una delle seguenti condizioni hello potrebbe impedire snapshot hello da viene attivata, che a sua volta può causare un errore tooBackup. Di seguito sono riportati i passaggi in hello dato ordine di risoluzione dei problemi e ripetere l'operazione.
##### <a name="cause-1-hello-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>Causa 1: [hello VM non è accesso a Internet](#the-vm-has-no-internet-access)
##### <a name="cause-2-hello-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-takenthe-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>Causa 2: [. Impossibile recuperare lo stato dello snapshot hello o non può essere eseguito uno snapshot](#the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken)
##### <a name="cause-3-hello-backup-extension-fails-tooupdate-or-loadthe-backup-extension-fails-to-update-or-load"></a>Causa 3: [estensione backup hello ha esito negativo tooupdate o carico](#the-backup-extension-fails-to-update-or-load)

## <a name="vmsnapshot-extension-operation-failed"></a>Operazione dell'estensione VMSnapshot non riuscita

Dopo che è necessario registrarla e pianificare una macchina virtuale per hello servizio Azure Backup, Backup avvia il processo di hello comunicando con snapshot di un punto nel tempo tootake hello VM estensione del backup. Una delle seguenti condizioni hello potrebbe impedire snapshot hello da viene attivata, che a sua volta può causare un errore tooBackup. Di seguito sono riportati i passaggi in hello dato ordine di risoluzione dei problemi e ripetere l'operazione.
##### <a name="cause-1-hello-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-takenthe-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>Causa 1: [. Impossibile recuperare lo stato dello snapshot hello o non può essere eseguito uno snapshot](#the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken)
##### <a name="cause-2-hello-backup-extension-fails-tooupdate-or-loadthe-backup-extension-fails-to-update-or-load"></a>Causa 2: [estensione backup hello ha esito negativo tooupdate o carico](#the-backup-extension-fails-to-update-or-load)
##### <a name="cause-3-hello-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>Causa 3: [hello VM non è accesso a Internet](#the-vm-has-no-internet-access)
##### <a name="cause-4-hello-agent-is-installed-in-hello-vm-but-is-unresponsive-for-windows-vmsthe-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>Causa 4: [hello agente viene installato nella macchina virtuale hello, ma non risponde (per le macchine virtuali di Windows)](#the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms)
##### <a name="cause-5-hello-agent-installed-in-hello-vm-is-out-of-date-for-linux-vmsthe-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>Causa 5: [agente hello installato nella macchina virtuale hello è scaduto (per le macchine virtuali Linux)](#the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms)

## <a name="unable-tooperform-hello-operation-as-hello-vm-agent-is-not-responsive"></a>Operazione hello tooperform Impossibile come hello agente della macchina virtuale non è reattiva

Dopo che è necessario registrarla e pianificare una macchina virtuale per hello servizio Azure Backup, Backup avvia il processo di hello comunicando con snapshot di un punto nel tempo tootake hello VM estensione del backup. Una delle seguenti condizioni hello potrebbe impedire snapshot hello da viene attivata, che a sua volta può causare un errore tooBackup. Di seguito sono riportati i passaggi in hello dato ordine di risoluzione dei problemi e ripetere l'operazione.
##### <a name="cause-1-hello-agent-is-installed-in-hello-vm-but-is-unresponsive-for-windows-vmsthe-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>Causa 1: [hello agente viene installato nella macchina virtuale hello, ma non risponde (per le macchine virtuali di Windows)](#the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms)
##### <a name="cause-2-hello-agent-installed-in-hello-vm-is-out-of-date-for-linux-vmsthe-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>Causa 2: [agente hello installato nella macchina virtuale hello è scaduto (per le macchine virtuali Linux)](#the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms)
##### <a name="cause-3-hello-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>Causa 3: [hello VM non è accesso a Internet](#the-vm-has-no-internet-access)

## <a name="backup-failed-with-an-internal-error---please-retry-hello-operation-in-a-few-minutes"></a>Backup non riuscito con errore interno: ripetere l'operazione di hello in pochi minuti

Dopo che è necessario registrarla e pianificare una macchina virtuale per hello servizio Azure Backup, Backup avvia il processo di hello comunicando con snapshot di un punto nel tempo tootake hello VM estensione del backup. Una delle seguenti condizioni hello potrebbe impedire snapshot hello da viene attivata, che a sua volta può causare un errore tooBackup. Di seguito sono riportati i passaggi in hello dato ordine di risoluzione dei problemi e ripetere l'operazione.
##### <a name="cause-1-hello-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>Causa 1: [hello VM non è accesso a Internet](#the-vm-has-no-internet-access)
##### <a name="cause-2-hello-agent-installed-in-hello-vm-but-unresponsive-for-windows-vmsthe-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>Causa 2: [agente hello installato nella macchina virtuale di hello ma che non risponde (per macchine virtuali di Windows)](#the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms)
##### <a name="cause-3-hello-agent-installed-in-hello-vm-is-out-of-date-for-linux-vmsthe-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>Causa 3: [agente hello installato nella macchina virtuale hello è scaduto (per le macchine virtuali Linux)](#the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms)
##### <a name="cause-4-hello-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-takenthe-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>Causa 4: [. Impossibile recuperare lo stato dello snapshot hello o non può essere eseguito uno snapshot](#the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken)
##### <a name="cause-5-hello-backup-extension-fails-tooupdate-or-loadthe-backup-extension-fails-to-update-or-load"></a>Causa 5: [estensione backup hello ha esito negativo tooupdate o carico](#the-backup-extension-fails-to-update-or-load)


## <a name="causes-and-solutions"></a>Cause e soluzioni

### <a name="hello-vm-has-no-internet-access"></a>Hello VM non è accesso a Internet
Per ogni requisito di distribuzione hello, hello VM non è accesso a Internet o ha restrizioni che impediscono l'accesso toohello dell'infrastruttura di Azure.

toofunction correttamente, hello backup estensione richiede indirizzi IP pubblico di Azure toohello di connettività. estensione Hello invia comandi snapshot tooan di archiviazione di Azure endpoint (URL HTTP) toomanage hello di hello macchina virtuale. Se l'estensione hello non è toohello alcun accesso che Internet pubblico, alla fine di Backup non riesce.

####  <a name="solution"></a>Soluzione
problema di hello tooresolve, procedere in uno dei metodi di hello elencati di seguito.
##### <a name="allow-access-toohello-azure-datacenter-ip-ranges"></a>Consentire l'accesso gli intervalli di IP toohello Data Center di Azure

1. Ottenere hello [elenco di indirizzi IP Data Center di Azure](https://www.microsoft.com/download/details.aspx?id=41653) tooallow accedervi.
2. Sbloccare hello IP eseguendo hello **New-NetRoute** cmdlet in hello macchina virtuale di Azure in una finestra di PowerShell con privilegi elevata. Eseguire i cmdlet di hello come amministratore.
3. tooallow accesso toohello indirizzi IP, aggiungere il gruppo di sicurezza rete toohello regole, se si dispone di uno.

##### <a name="create-a-path-for-http-traffic-tooflow"></a>Creare un percorso per tooflow il traffico HTTP

1. Se si dispone di restrizioni di rete (ad esempio, un gruppo di rete), è possibile distribuire un proxy server tooroute hello il traffico HTTP.
2. tooallow accesso toohello Internet dal server proxy HTTP di hello, aggiungere il gruppo di sicurezza rete toohello regole, se si dispone di uno.

toolearn tooset di un proxy HTTP per i backup di macchine Virtuali, vedere [preparare tooback l'ambiente di macchine virtuali di Azure](backup-azure-vms-prepare.md#using-an-http-proxy-for-vm-backups).

Nel caso in cui si utilizzano dischi gestiti, potrebbe essere necessario un ulteriore porta (8443) aprendo nei firewall hello.

### <a name="hello-agent-installed-in-hello-vm-but-unresponsive-for-windows-vms"></a>agente di Hello installato nella macchina virtuale di hello ma che non risponde (per le macchine virtuali di Windows)

#### <a name="solution"></a>Soluzione
Hello agente della macchina virtuale potrebbe essere danneggiato o potrebbe essere stato arrestato il servizio di hello. Agente di macchine Virtuali hello nuovamente l'installazione consente di ottenere la versione più recente di hello e riavviare la comunicazione hello.

1. Verificare se il servizio dell'agente Guest di Windows in esecuzione in servizi (services.msc) di hello macchina virtuale. Provare a riavviare il servizio di agente Guest di Windows hello e avviare hello Backup<br>
2. Se non è visibile tra i servizi, verificare in Programmi e funzionalità che il servizio agente guest di Windows sia installato.
4. Se si è in grado di tooview in programmi e funzionalità hello disinstallazione dell'agente Guest di Windows.
5. Scaricare e installare hello [versione più recente del file msi](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). È necessario installazione hello toocomplete privilegi di amministratore.
6. Quindi dovrebbe essere in grado di tooview servizi di agente Guest di Windows in servizi
7. Provare a eseguire un backup su richiesta/adhoc facendo clic su "Esegui Backup ora" nel portale di hello.

Verificare inoltre la macchina virtuale disponga ** [.NET 4.5 installato nel sistema hello](https://docs.microsoft.com/en-us/dotnet/framework/migration-guide/how-to-determine-which-versions-are-installed)**. È necessario per toocommunicate agente VM di hello con servizio hello

### <a name="hello-agent-installed-in-hello-vm-is-out-of-date-for-linux-vms"></a>agente Hello installato nella macchina virtuale hello è scaduto (per le macchine virtuali Linux)

#### <a name="solution"></a>Soluzione
La maggior parte degli errori relativi ad agenti o estensioni nelle macchine virtuali Linux è dovuta a problemi correlati ad agenti di macchine virtuali non aggiornati. tootroubleshoot questo problema, seguire queste linee guida generali:

1. Seguire le istruzioni di hello per [aggiornamento hello agente VM Linux](../virtual-machines/linux/update-agent.md).

 >[!NOTE]
 >Abbiamo *consigliabile* aggiornamento agente hello solo tramite un repository di distribuzione. Non è consigliabile scaricare codice agente hello direttamente da GitHub e aggiornarla. Se non è disponibili per la distribuzione più recenti dell'agente hello, contattare il supporto di distribuzione per istruzioni su come tooinstall è. toocheck per hello più recente dell'agente, passa toohello [agente Linux di Windows Azure](https://github.com/Azure/WALinuxAgent/releases) pagina nel repository GitHub hello.

2. Verificare che tale hello agente di Azure è in esecuzione nella macchina virtuale hello eseguendo hello comando seguente:`ps -e`

 Se il processo di hello non è in esecuzione, riavviarlo utilizzando hello seguenti comandi:

 * Per Ubuntu: `service walinuxagent start`
 * Per altre distribuzioni: `service waagent start`

3. [Configurare l'agente di riavvio automatico di hello](https://github.com/Azure/WALinuxAgent/wiki/Known-Issues#mitigate_agent_crash).
4. Eseguire un nuovo backup di prova. Se l'errore hello persiste, raccogliere hello seguendo i registri dalla macchina virtuale del cliente hello:

   * /var/lib/waagent/*.xml
   * /var/log/waagent.log
   * /var/log/azure/*

Se è necessaria una registrazione dettagliata per waagent, seguire questa procedura:

1. Nel file /etc/waagent.conf hello individuare hello seguente riga: **abilitare la registrazione dettagliata (y | n)**
2. Hello modifica **Logs.Verbose** valore * n * troppo*y*.
3. Salvare la modifica hello e quindi riavviare waagent seguendo i passaggi precedenti di hello in questa sezione.

### <a name="hello-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>Impossibile recuperare lo stato dello snapshot Hello o non può essere eseguito uno snapshot
backup di VM Hello si basa sul rilascio di un account di archiviazione sottostante snapshot comando toohello. Backup può non riuscire poiché non dispone di alcun account di archiviazione toohello di accesso o esecuzione hello dell'attività di snapshot di hello viene posticipata.

#### <a name="solution"></a>Soluzione
Hello le condizioni seguenti può causare errori di attività di snapshot:

| Causa | Soluzione |
| --- | --- |
| Hello VM è configurato il backup di SQL Server. | Per impostazione predefinita, il backup di VM hello viene eseguito un backup completo di VSS nelle macchine virtuali di Windows. Nelle macchine virtuali che eseguono server basati su SQL Server e in cui è configurato il backup di SQL Server possono verificarsi ritardi nell'esecuzione di snapshot.<br><br>Se si verifica un errore di Backup a causa di un problema di snapshot, impostare hello seguente chiave del Registro di sistema:<br><br>**[HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\BCDRAGENT] "USEVSSCOPYBACKUP"="TRUE"** |
| stato della macchina virtuale Hello viene segnalato in modo non corretto perché hello VM è stato arrestato in RDP. | Se si arresta hello VM in Remote Desktop Protocol (RDP), controllare toodetermine portale hello se hello stato della macchina virtuale sia corretto. Se non è corretto, arrestare hello VM nel portale di hello tramite hello **arresto** opzione nel dashboard della macchina virtuale hello. |
| Più macchine virtuali da hello sono nello stesso servizio cloud configurato tooback backup hello contemporaneamente. | È una migliore toospread pratica le pianificazioni di backup di hello per le macchine virtuali da hello stesso servizio cloud. |
| Hello macchina virtuale è in esecuzione in un utilizzo elevato della CPU o memoria. | Se hello macchina virtuale è in esecuzione a utilizzo elevato della CPU (oltre il 90%) o a utilizzo elevato della memoria, hello snapshot attività in coda e ritardato e viene infine interrotta per timeout. In una situazione di questo tipo, provare a eseguire un backup su richiesta. |
| Hello VM non è possibile ottenere l'indirizzo di host o dell'infrastruttura di hello da DHCP. | DHCP deve essere abilitato all'interno di hello guest per hello toowork backup VM IaaS.  Se hello VM non è possibile ottenere hello/infrastruttura host indirizzo dalla risposta DHCP 245, non può scaricare o eseguire tutte le estensioni. Se è necessario un indirizzo IP privato statico, è necessario configurarlo mediante platform hello. Hello opzione DHCP all'interno di hello VM deve essere lasciato abilitato. Per altre informazioni, vedere [Impostazione di un indirizzo IP privato interno statico](../virtual-network/virtual-networks-reserved-private-ip.md). |

### <a name="hello-backup-extension-fails-tooupdate-or-load"></a>estensione del backup Hello ha esito negativo tooupdate o carico
Se non è possibile caricare le estensioni, Backup ha esito negativo perché non è possibile acquisire uno snapshot.

#### <a name="solution"></a>Soluzione

**Per gli utenti guest Windows:** verificare che il servizio di iaasvmprovider hello è abilitato ed è un tipo di avvio *automatica*. Se il servizio di hello non è configurato in questo modo, abilitarla toodetermine se hello successivo backup ha esito positivo.

**Per i Guest Linux:** verificare hello versione VMSnapshot per Linux (estensione hello utilizzato dal Backup) è 1.0.91.0.<br>


Se l'estensione del backup hello persistono tooupdate o carico, è possibile forzare hello VMSnapshot estensione toobe ricaricato disinstallando estensione hello. tentativo di backup successivo Hello ricaricherà estensione hello.

toouninstall hello estensione, hello seguenti:

1. Passare toohello [portale di Azure](https://portal.azure.com/).
2. Individuare hello macchina virtuale che presenta problemi di backup.
3. Fare clic su **Impostazioni**.
4. Fare clic su **Estensioni**.
5. Fare clic su **Estensione Vmsnapshot**.
6. Fare clic su **Disinstalla**.

Questa procedura consente di hello estensione toobe reinstallato durante il backup successivo hello.

