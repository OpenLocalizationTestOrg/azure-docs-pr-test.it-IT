---
title: Risolvere i problemi relativi al backup di una macchina virtuale di Azure | Microsoft Docs
description: Risolvere i problemi relativi al backup e al ripristino delle macchine virtuali di Azure
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: 73214212-57a4-4b57-a2e2-eaf9d7fde67f
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: trinadhk;markgal;jpallavi;
ms.openlocfilehash: 096c97f4cb41ff8df2e646f59dbc0bf845721ac7
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="troubleshoot-azure-virtual-machine-backup"></a>Risolvere i problemi relativi al backup delle macchine virtuali di Azure
> [!div class="op_single_selector"]
> * [Insieme di credenziali dei servizi di ripristino](backup-azure-vms-troubleshoot.md)
> * [Insieme di credenziali per il backup](backup-azure-vms-troubleshoot-classic.md)
>
>

È possibile risolvere gli errori rilevati durante l'uso di Backup di Azure con le informazioni elencate nella tabella seguente.

## <a name="backup"></a>Backup

### <a name="error-the-specified-disk-configuration-is-not-supported"></a>Errore: la configurazione di disco specificata non è supportata

Attualmente Backup di Azure non supporta dischi di dimensioni [maggiori di 1023 GB](https://docs.microsoft.com/azure/backup/backup-azure-arm-vms-prepare#limitations-when-backing-up-and-restoring-a-vm). 
- Se la dimensione dei dischi è maggiore di 1 TB, [collegare nuovi dischi](https://docs.microsoft.com/azure/virtual-machines/windows/attach-managed-disk-portal) di dimensione inferiore a 1 TB <br>
- Copiare quindi i dati dal disco di dimensione superiore a 1 TB nei dischi appena creati di dimensione inferiore a 1 TB. <br>
- Verificare che tutti i dati siano stati copiati e rimuovere i dischi di dimensione superiore a 1 TB
- Avviare il backup.

| Dettagli errore | Soluzione alternativa |
| --- | --- |
| Impossibile eseguire l'operazione perché la VM non esiste più. Arrestare la protezione della macchina virtuale senza eliminare i dati del backup. Per altre informazioni visitare la pagina Web http://go.microsoft.com/fwlink/?LinkId=808124 |Questo si verifica quando la macchina virtuale primaria viene eliminata, ma i criteri di backup continuano a cercare una macchina virtuale per il backup. Per correggere l'errore:  <ol><li> Ricreare la macchina virtuale con lo stesso nome e lo stesso nome del gruppo di risorse [nome del servizio cloud],<br>OPPURE</li><li> Interrompere la protezione della macchina virtuale cancellando o senza eliminare i dati del backup. [Altre informazioni](http://go.microsoft.com/fwlink/?LinkId=808124)</li></ol> |
| Operazione di creazione snapshot non riuscita a causa dell'assenza della connettività di rete nella macchina virtuale. Assicurarsi che la VM abbia accesso alla rete. Per la corretta creazione dello snapshot, aggiungere all'elenco elementi consentiti gli intervalli IP del data center di Azure oppure configurare un server proxy per l'accesso di rete. Per altri dettagli, vedere http://go.microsoft.com/fwlink/?LinkId=800034. Se si usa già il server proxy, assicurarsi che le impostazioni del server proxy siano configurate correttamente. | Questo errore viene generato quando si nega la connettività Internet in uscita nella macchina virtuale. La connettività Internet è necessaria per consentire all'estensione snapshot della VM di creare uno snapshot dei dischi sottostanti della macchina virtuale. [Altre informazioni](backup-azure-troubleshoot-vm-backup-fails-snapshot-timeout.md#snapshot-operation-failed-due-to-no-network-connectivity-on-the-virtual-machine) su come risolvere gli errori degli snapshot dovuti all'accesso di rete bloccato. |
| L'agente di macchine virtuali non riesce a comunicare con il servizio Backup di Azure. Verificare la connettività di rete della macchina virtuale e che l'agente di macchine virtuali sia in esecuzione con la versione più recente. Per altre informazioni, vedere http://go.microsoft.com/fwlink/?LinkId=800034. |Questo errore viene generato se si verifica un problema con l'agente di VM o se l'accesso di rete all'infrastruttura di Azure è bloccato in qualche modo. Vedere [altre informazioni](backup-azure-troubleshoot-vm-backup-fails-snapshot-timeout.md#vm-agent-unable-to-communicate-with-azure-backup) sul debug dei problemi di snapshot della VM.<br> Se l'agente VM non causa alcun problema, riavviare la VM. Talvolta, uno stato della macchina virtuale non corretto genera problemi che vengono corretti riavviando la macchina virtuale. |
| Lo stato di provisioning della macchina virtuale è Non riuscito. Riavviare la macchina virtuale e assicurarsi che lo stato della macchina virtuale sia In esecuzione o Arresto per il backup. | Questo errore si verifica quando gli errori di una delle estensioni provocano lo stato non riuscito del provisioning della VM. Passare all'elenco di estensioni e verificare se è presente un'estensione con errore, rimuoverla e provare a riavviare la macchina virtuale. Se tutte le estensioni sono in stato di esecuzione, verificare se è in esecuzione il servizio agente di macchine virtuali. In caso contrario, riavviare il servizio agente di macchine virtuali. | 
| L'operazione dell'estensione VMSnapshot non è riuscita per i dischi gestiti. Ripetere l'operazione di backup. Se il problema si ripete, seguire le istruzioni illustrate nell'articolo 'http://go.microsoft.com/fwlink/?LinkId=800034'. Se il problema continua a persistere, contattare il supporto tecnico Microsoft. | Questo errore viene visualizzato quando il servizio Backup di Azure non riesce ad attivare uno snapshot. [Altre informazioni](backup-azure-troubleshoot-vm-backup-fails-snapshot-timeout.md#vmsnapshot-extension-operation-failed) sul debug dei problemi delle VM relativi agli snapshot. |
| Non è stato possibile copiare lo snapshot della macchina virtuale a causa dello spazio disponibile insufficiente nell'account di archiviazione. Assicurarsi che lo spazio disponibile nell'account di archiviazione sia equivalente ai dati presenti nei dischi di archiviazione Premium collegati alla macchina virtuale. | Nel caso delle VM Premium, lo snapshot deve essere copiato nell'account di archiviazione, in modo da assicurare che il traffico di gestione dei backup, che funziona sullo snapshot, non limiti il numero di IOPS disponibili all'applicazione che usa i dischi Premium. Microsoft consiglia di allocare solo il 50% dello spazio totale dell'account di archiviazione, in modo che il servizio Backup di Azure possa copiare lo snapshot nell'account di archiviazione e trasferire i dati da questa posizione copiata nell'account di archiviazione all'insieme di credenziali. | 
| Non è possibile eseguire l'operazione perché l'agente di macchine virtuali non risponde |Questo errore viene generato se si verifica un problema con l'agente di VM o se l'accesso di rete all'infrastruttura di Azure è bloccato in qualche modo. Per le macchine virtuali di Windows, controllare lo stato del servizio agente di macchine virtuali nella sezione dei servizi e verificare che l'agente venga visualizzato tra i programmi nel pannello di controllo. Provare a rimuovere il programma dal pannello di controllo e a reinstallare l'agente come indicato di [seguito](#vm-agent). Dopo aver reinstallato l'agente, attivare un backup adhoc per verificare. |
| Operazione di estensione dei servizi di ripristino non riuscita. Assicurarsi che nella macchina virtuale sia presente l'agente di macchine virtuali più recente e che il servizio agente sia in esecuzione. Ripetere l'operazione di backup e, in caso di esito negativo, contattare il supporto tecnico Microsoft. |Questo errore viene generato quando l'agente VM non è aggiornato. Per aggiornare l'agente VM, fare riferimento alla sezione "Aggiornamento dell'agente VM" riportata di seguito. |
| La macchina virtuale non esiste. Verificare che la macchina virtuale sia presente o selezionarne un'altra. |Questo errore si verifica quando viene rilevata la macchina virtuale primaria ma i criteri di backup continuano a cercare una macchina virtuale per il backup. Per correggere l'errore:  <ol><li> Ricreare la macchina virtuale con lo stesso nome e lo stesso nome del gruppo di risorse [nome del servizio cloud],<br>OPPURE<br></li><li>Interrompere la protezione della macchina virtuale senza eliminare i dati del backup. [Altre informazioni](http://go.microsoft.com/fwlink/?LinkId=808124)</li></ol> |
| L'esecuzione del comando non è riuscita. In questo elemento è attualmente in corso un'altra operazione. Attendere il completamento dell'operazione precedente, quindi riprovare. |È in esecuzione un processo di backup esistente per la VM e non è possibile avviare un nuovo processo mentre è in esecuzione il processo esistente. |
| Si è verificato il timeout della copia dei dischi rigidi virtuali dall'insieme di credenziali per il backup. Attendere qualche minuto prima di ripetere l'operazione. Se il problema persiste, contattare il supporto tecnico Microsoft. | Questo problema si verifica in caso di errore temporaneo sul lato della risorsa di archiviazione o se il servizio di backup non riceve IOPS sufficienti dall'account di archiviazione che ospita la macchina virtuale per trasferire i dati all'insieme di credenziali entro il periodo di timeout. Assicurarsi di seguire le [Procedure consigliate](backup-azure-vms-introduction.md#best-practices) durante la configurazione del backup. Provare a spostare la macchina virtuale in un account di archiviazione diverso, non caricato, quindi provare a eseguire di nuovo il backup.|
| Il backup non è riuscito e si è verificato un errore interno. Attendere qualche minuto prima di ripetere l'operazione. Se il problema persiste, contattare il supporto tecnico Microsoft. |Questo problema può verificarsi per 2 ragioni:  <ol><li> È stato riscontrato un problema temporaneo nell'accesso all'archiviazione della macchina virtuale. Controllare lo [stato di Azure](https://azure.microsoft.com/en-us/status/) per verificare la presenza di un eventuale problema in corso relativo alle operazioni di calcolo/archiviazione/rete nell'area. Dopo aver risolto il problema, riprovare a eseguire il backup. <li>La macchina virtuale originale è stata eliminata, pertanto non è possibile ricorrere al punto di ripristino. Per mantenere i dati di backup per una macchina virtuale eliminata, evitando gli errori di backup, interrompere la protezione della macchina virtuale e selezionare l'opzione di conservazione dei dati. Questa operazione interrompe il processo di backup pianificato e i messaggi di errore ricorrenti. |
| Non è stato possibile installare l'estensione Servizi di ripristino di Azure nell'elemento selezionato. L'agente VM è un prerequisito dell'estensione Servizi di ripristino di Azure. Installare l'agente VM di Azure e riavviare l'operazione di registrazione |<ol> <li>Controllare se l'agente di VM è stato installato correttamente. <li>Assicurarsi che il flag sul file di configurazione della macchina virtuale sia impostato correttamente.</ol> [Altre informazioni](#validating-vm-agent-installation) sull'installazione dell'agente VM e su come convalidarla. |
| L'installazione dell'estensione non è riuscita con un errore che indica che il servizio COM+ non può comunicare con Microsoft Distributed Transaction Coordinator |Questo errore in genere indica che il servizio COM+ non è in esecuzione. Per informazioni su come correggere l'errore, contattare il supporto tecnico Microsoft. |
| L'operazione di snapshot non è riuscita con un errore dell'operazione del Servizio Copia Shadow del volume che indica che l'unità è bloccata da Crittografia unità BitLocker. È necessario sbloccare l'unità dal Pannello di controllo. |Disattivare BitLocker per tutte le unità della macchina virtuale e verificare se il problema relativo al Servizio Copia Shadow del volume è stato risolto |
| Lo stato della macchina virtuale non consente i backup. |<ul><li>Verificare se la macchina virtuale ha uno stato temporaneo intermedio tra In esecuzione e Arresto. In questo caso, attendere che lo stato della macchina virtuale corrisponda a uno dei due stati indicati e riattivare il backup. <li> Se la macchina virtuale è Linux e usa il modulo del kernel [Security Enhanced Linux], è necessario escludere il percorso dell'agente Linux (_/var/lib/waagent_) dai criteri di sicurezza per assicurare l'installazione dell'estensione di backup.  |
| La macchina virtuale di Azure non è stata trovata. |Questo errore si verifica quando viene rilevata la macchina virtuale primaria ma i criteri di backup continuano a cercare una macchina virtuale per il backup. Per correggere l'errore:  <ol><li>Ricreare la macchina virtuale con lo stesso nome e lo stesso nome del gruppo di risorse [nome del servizio cloud], <br>OPPURE <li> Disabilitare la protezione per questa macchina virtuale affinché i processi di backup non vengano creati. </ol> |
| L'agente di macchine virtuali non è presente nella macchina virtuale. Installare i prerequisiti necessari, l'agente VM, quindi ripetere l'operazione. |[Altre informazioni](#vm-agent) sull'installazione dell'agente di VM e su come convalidare l'installazione dell'agente di VM. |
| L'operazione di snapshot non è riuscita a causa dello stato non corretto dei VSS writer |È necessario riavviare i VSS (servizio Copia Shadow del volume) writer con stato non corretto. A questo scopo, da un prompt dei comandi con privilegi elevati eseguire _vssadmin list writers_. L'output contiene tutti i VSS writer con lo stato. Riavviare ogni VSS writer con stato diverso da "[1] Stable" usando i comandi seguenti da un prompt dei comandi con privilegi elevati:<br> _net stop serviceName_ <br> _net start serviceName_|
| L'operazione di snapshot non è riuscita a causa di un errore di analisi della configurazione |Questo problema si verifica a causa della modifica delle autorizzazioni nella directory MachineKeys: _%systemdrive%\programdata\microsoft\crypto\rsa\machinekeys_ <br>Eseguire il comando sotto e verificare che le autorizzazioni per la directory MachineKeys siano quelle predefinite:<br>_icacls %systemdrive%\programdata\microsoft\crypto\rsa\machinekeys_ <br><br> Le autorizzazioni predefinite sono:<br>Everyone:(R,W) <br>BUILTIN\Administrators:(F)<br><br>Se vengono visualizzate autorizzazioni per la directory MachineKeys diverse da quelle predefinite, seguire i passaggi sotto per correggere le autorizzazioni, eliminare il certificato e attivare il backup.<ol><li>Correggere le autorizzazioni per la directory MachineKeys.<br>Usando le impostazioni di sicurezza avanzate e le proprietà di sicurezza di Explorer per la directory, reimpostare le autorizzazioni sui valori predefiniti, rimuovere eventuali oggetti utente aggiuntivi (diversi da quelli predefiniti) dalla directory e assicurarsi che le autorizzazioni "Everyone" abbiano l'accesso speciale per:<br>-Elencare cartelle/leggere dati <br>-Leggere attributi <br>-Leggere attributi estesi <br>-Creare file/scrivere dati <br>-Creare cartelle/aggiungere dati<br>-Scrivere attributi<br>-Scrivere attributi estesi<br>-Leggere autorizzazioni<br><br><li>Eliminare tutti i certificati con il campo "Rilasciato a" = "Windows Azure Service Management for Extensions" (Microsoft Azure Service Management per le estensioni) o "Windows Azure CRP Certificate Generator" (Generatore certificati CRP Microsoft Azure).<ul><li>[Aprire la console certificati (computer locale)](https://msdn.microsoft.com/library/ms788967(v=vs.110).aspx)<li>Eliminare tutti i certificati (in Personale -> Certificati) con il campo "Rilasciato a" = "Windows Azure Service Management for Extensions" (Microsoft Azure Service Management per le estensioni) o "Windows Azure CRP Certificate Generator" (Generatore certificati CRP Microsoft Azure).</ul><li>Attivare il backup della VM. </ol>|
| Convalida non riuscita perché la macchina virtuale è crittografata con il solo BEK. I backup possono essere abilitati solo per le macchine virtuali crittografate con BEK e KEK. |La macchina virtuale deve essere crittografata mediante la chiave di crittografia BitLocker e la chiave di crittografia delle chiavi. In seguito, il backup deve essere abilitato. |
| Il servizio backup di Azure non possiede autorizzazioni sufficienti nel Key Vault per il backup di macchine virtuali crittografate. |Il servizio di backup deve ricevere queste autorizzazioni in PowerShell tramite la procedura indicata nella sezione **Abilitazione del backup** della [Documentazione di PowerShell](backup-azure-vms-automation.md). |
|L'installazione dell'estensione dello snapshot non è riuscita con un errore che indica che il servizio COM+ non può comunicare con Microsoft Distributed Transaction Coordinator | Provare ad avviare il servizio di Windows "Applicazione di sistema COM+" (da un prompt dei comandi con privilegi elevati - _net start COMSysApp_). <br>In caso di errore durante l'avvio, seguire questa procedura:<ol><li> Verificare che l'account di accesso del servizio "Distributed Transaction Coordinator" sia "Servizio di rete". In caso contrario, modificarlo in "Servizio di rete", riavviare il servizio e quindi provare ad avviare il servizio "Applicazione di sistema COM+".<li>Se il problema persiste, disinstallare/installare il servizio "Distributed Transaction Coordinator" seguendo questa procedura:<br> - Arrestare il servizio MSDTC<br> - Aprire un prompt dei comandi (cmd) <br> - Eseguire il comando "msdtc -uninstall" <br> - Eseguire il comando "msdtc -install" <br> - Avviare il servizio MSDTC<li>Avviare il servizio di Windows "Applicazione di sistema COM+" e quindi attivare il backup dal portale.</ol> |
|  L'operazione di creazione snapshot non è riuscita a causa di un errore COM+ | L'azione consigliata è di riavviare il servizio di Windows "Applicazione di sistema COM+" (da un prompt dei comandi con privilegi elevati - _net start COMSysApp_). Se il problema persiste, riavviare la macchina virtuale. Se anche il riavvio della macchina virtuale non consente di risolvere il problema, provare a [rimuovere l'estensione VMSnapshot](https://docs.microsoft.com/en-us/azure/backup/backup-azure-troubleshoot-vm-backup-fails-snapshot-timeout#cause-3-the-backup-extension-fails-to-update-or-load) e ad attivare il backup manualmente. |
| Impossibile bloccare uno o più punti di montaggio della macchina virtuale per creare uno snapshot coerente con il file system | Seguire questa procedura: <ol><li>Controllare lo stato del file system di tutti i dispositivi montati tramite il comando _'tune2fs'_.<br> Ad esempio: tune2fs -l /dev/sdb1 \| grep "Filesystem state" <li>Smontare i dispositivi il cui stato del file system non è pulito tramite il comando _'umount'_. <li> Eseguire il controllo FileSystemConsistency su tali dispositivi tramite il comando _'fsck'_. <li> Montare di nuovo i dispositivi e provare a eseguire il backup.</ol> |
| L'operazione di snapshot non è riuscita a causa di un errore durante la creazione del canale di comunicazione di rete protetta | <ol><Li> Aprire l'editor del Registro di sistema eseguendo regedit.exe con privilegi elevati. <li> Identificare tutte le versioni di .NetFramework presenti nel sistema, disponibili nella gerarchia della chiave del Registro di sistema "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft" <li> Per ogni versione di .NetFramework presente nella chiave del Registro di sistema, aggiungere la seguente chiave: <br> "SchUseStrongCrypto"=dword:00000001 </ol>|
| L'operazione di snapshot non è riuscita a causa di un errore durante l'installazione di Visual C++ Redistributable per Visual Studio 2012 | Andare a C:\Packages\Plugins\Microsoft.Azure.RecoveryServices.VMSnapshot\agentVersion e installare vcredist2012_x64. Assicurarsi che il valore della chiave del Registro di sistema per consentire l'installazione del servizio sia impostato correttamente: il valore della chiave del Registro di sistema _HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Msiserver_ deve essere impostato su 3, non su 4. Se i problemi di installazione persistono, riavviare il servizio di installazione eseguendo _MSIEXEC /UNREGISTER_ e quindi _MSIEXEC /REGISTER_ da un prompt dei comandi con privilegi elevati.  |


## <a name="jobs"></a>Processi
| Dettagli errore | Soluzione alternativa |
| --- | --- |
| L'annullamento non è supportato per questo tipo di processo. Attendere il completamento del processo. |None |
| Il processo non si trova in uno stato annullabile. Attendere il completamento del processo. <br>OPPURE<br> Il processo selezionato non si trova in uno stato annullabile. Attendere il completamento del processo. |Con tutta probabilità, il processo è quasi completo. Attendere che il processo venga completato.|
| Non è possibile annullare il processo perché non è in corso. L'annullamento è supportato solo per i processi in corso. Tentare l'annullamento solo per un processo in corso. |Questo errore è causato da uno stato temporaneo. Attendere un minuto e ripetere l'operazione di annullamento. |
| Non è stato possibile annullare il processo. Attendere il completamento del processo. |None |

## <a name="restore"></a>Ripristino
| Dettagli errore | Soluzione alternativa |
| --- | --- |
| Ripristino non riuscito con errore interno del cloud |<ol><li>Il servizio cloud in cui si sta tentando di eseguire il ripristino è configurato con le impostazioni DNS. Verificare  <br>$deployment = Get-AzureDeployment -ServiceName "ServiceName" -Slot "Production"     Get-AzureDns -DnsSettings $deployment.DnsSettings<br>Se è presente un indirizzo configurato, significa che le impostazioni DNS sono configurate.<br> <li>Il servizio cloud che si sta tentando di ripristinare è configurato con ReservedIP e le macchine virtuali esistenti nel servizio cloud sono in stato di arresto.<br>È possibile controllare che il servizio cloud disponga di IP riservato tramite i cmdlet di PowerShell seguenti:<br>$deployment = Get-AzureDeployment -ServiceName "servicename" -Slot "Production" $dep.ReservedIPName <br><li>Si sta tentando di ripristinare una macchina virtuale con le configurazioni di rete speciali seguenti nello stesso servizio cloud. <br>- Macchine virtuali con configurazione del servizio di bilanciamento del carico (interno ed esterno)<br>- Macchine virtuali con più indirizzi IP riservati<br>- Macchine virtuali con più schede di rete<br>Selezionare un nuovo servizio cloud nell'interfaccia utente o consultare le [considerazioni sul ripristino](backup-azure-arm-restore-vms.md#restore-vms-with-special-network-configurations) per le macchine virtuali con configurazioni di rete speciali.</ol> |
| Il nome DNS selezionato è già in uso. Specificare un nome DNS diverso e riprovare. |Il nome DNS fa riferimento al nome del servizio cloud, che in genere termina con .cloudapp.net. Questo nome deve essere univoco. Se si verifica questo errore, è necessario scegliere un altro nome di macchina virtuale durante il ripristino. <br><br> Questo errore viene visualizzato solo dagli utenti del portale di Azure. L'operazione di ripristino tramite PowerShell riuscirà perché ripristina solo i dischi e non crea la macchina virtuale. L'errore viene restituito quando la macchina virtuale viene creata in modo esplicito dall'utente dopo l'operazione di ripristino dei dischi. |
| La configurazione di rete virtuale specificata non è corretta. Specificare un'altra configurazione di rete virtuale e riprovare. |None |
| Il servizio cloud specificato usa un indirizzo IP riservato che non corrisponde alla configurazione della macchina virtuale in fase di ripristino. Specificare un altro servizio cloud che non usa un indirizzo IP riservato o scegliere un altro punto di ripristino da cui eseguire l'operazione. |None |
| Il servizio cloud ha raggiunto il limite consentito per il numero di endpoint di input. Ripetere l'operazione specificando un altro servizio cloud o usando un endpoint esistente. |None |
| L'insieme di credenziali di backup e l'account di archiviazione di destinazione si trovano in due aree diverse. Assicurarsi che l'account di archiviazione specificato nell'operazione di ripristino si trovi nella stessa area di Azure dell'insieme di credenziali di backup. |None |
| L'account di archiviazione specificato per l'operazione di ripristino non è supportato. Sono supportati solo gli account di archiviazione dei piani Basic/Standard con le impostazioni di replica con ridondanza locale o ridondanza geografica. Selezionare un account di archiviazione supportato |None |
| Il tipo di account di archiviazione specificato per l'operazione di ripristino non è online. Assicurarsi che l'account di archiviazione specificato nell'operazione di ripristino sia online |Questo problema può essere provocato da un errore temporaneo nel servizio di archiviazione di Azure o da un'interruzione del servizio. Scegliere un altro account di archiviazione. |
| È stata raggiunta la quota del gruppo di risorse. Eliminare alcuni gruppi di risorse dal portale di Azure o contattare il supporto tecnico di Azure per richiedere un aumento dei limiti. |None |
| La subnet selezionata non esiste. Selezionare una subnet esistente |Nessuno |
| Il servizio Backup non ha l'autorizzazione per accedere alle risorse nella sottoscrizione. |Per risolvere questo problema, ripristinare prima di tutto i dischi seguendo la procedura illustrata nella sezione **Ripristino dei dischi sottoposti a backup** in [Scelta di una configurazione di ripristino per la macchina virtuale](backup-azure-arm-restore-vms.md#choose-a-vm-restore-configuration). Seguire quindi la procedura di PowerShell illustrata in [Creare una macchina virtuale da dischi ripristinati](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) per creare una macchina virtuale completa dai dischi ripristinati. |

## <a name="backup-or-restore-taking-time"></a>Il backup o il ripristino richiede del tempo
In caso di eccessivo allungamento del tempo di backup (> 12 ore) o di ripristino (> 6 ore):
* Comprendere i [fattori che incidono sul tempo di backup](backup-azure-vms-introduction.md#total-vm-backup-time) e i [fattori che incidono sul tempo di ripristino](backup-azure-vms-introduction.md#total-restore-time).
* Assicurarsi di seguire le [Procedure consigliate per il backup](backup-azure-vms-introduction.md#best-practices). 

## <a name="vm-agent"></a>Agente di macchine virtuali
### <a name="setting-up-the-vm-agent"></a>Configurazione dell'agente di VM
L'agente di VM è in genere già presente nelle VM create dalla raccolta di Azure. Nelle macchine virtuali di cui viene eseguita la migrazione da data center locali non è installato l'agente di VM. Per queste VM è necessario installare esplicitamente l'agente di VM.

Per VM di Windows:

* Scaricare e installare il file [MSI per l'agente](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Per completare l'installazione sono necessari privilegi di amministratore.
* Per le macchine virtuali classiche, [aggiornare le proprietà della macchina virtuale](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) per indicare che l'agente è stato installato. Questo passaggio non è necessario per le macchine virtuali di Resource Manager.

Per le macchine virtuali Linux:

* Installare l'archivio di distribuzione più recente. È **fortemente consigliato** installare l'agente solo tramite l'archivio di distribuzione. Per informazioni dettagliate sul nome del pacchetto, vedere [archivio agente Linux](https://github.com/Azure/WALinuxAgent) 
* Per le macchine virtuali classiche, [aggiornare le proprietà della macchina virtuale](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) per indicare che l'agente è stato installato. Questo passaggio non è necessario per le macchine virtuali di Resource Manager.

### <a name="updating-the-vm-agent"></a>Aggiornamento dell'agente di VM
Per VM di Windows:

* L'aggiornamento dell'agente di VM è semplice quanto la reinstallazione dei [file binari dell'agente di VM](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). È tuttavia necessario assicurarsi che non siano in esecuzione operazioni di backup durante l'aggiornamento dell'agente di VM.

Per le macchine virtuali Linux:

* Seguire le istruzioni in [Come aggiornare l'agente Linux di Azure su una macchina virtuale per la versione più recente da GitHub](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
È **fortemente consigliato** aggiornare l'agente solo tramite il repository di distribuzione. Non è consigliabile scaricare il codice dell'agente direttamente da GitHub e aggiornarlo. Se l'agente più recente non è disponibile per la distribuzione, contattare il supporto per la distribuzione per istruzioni su come installare l'agente più recente. È possibile trovare le informazioni più recenti sull'[agente Linux di Microsoft Azure](https://github.com/Azure/WALinuxAgent/releases) nel repository GitHub.

### <a name="validating-vm-agent-installation"></a>Convalida dell'installazione dell'agente di VM
Come controllare la versione dell'agente di VM nelle macchine virtuali di Windows:

1. Accedere alla macchina virtuale di Azure e passare alla cartella *C:\WindowsAzure\Packages*. che dovrebbe includere il file WaAppAgent.exe.
2. Fare clic con il pulsante destro del mouse sul file, scegliere **Proprietà** e quindi selezionare la scheda **Dettagli**. Il campo Versione prodotto deve essere 2.6.1198.718 o superiore.

## <a name="troubleshoot-vm-snapshot-issues"></a>Risoluzione dei problemi relativi allo snapshot della macchina virtuale
Il backup delle macchine virtuali si basa sull'esecuzione dei comandi di snapshot sull'archiviazione sottostante. Non disporre dell'accesso all'archiviazione o il ritardo nell'esecuzione dell'attività dello snapshot può causare il fallimento del processo di backup. I seguenti elementi possono causare il fallimento dell'attività di backup.

1. L'accesso alla rete per l'archiviazione è bloccato mediante NSG<br>
    Vedere altre informazioni su come [abilitare l'accesso alla rete](backup-azure-vms-prepare.md#network-connectivity) per l'archiviazione tramite gli elenchi di indirizzi IP consentiti o il server proxy.
2. Le VM con il backup di SQL Server configurato possono causare ritardi nelle attività di snapshot  <br>
   Per impostazione predefinita, il backup delle VM genera un backup VSS completo sulle VM Windows. In VM che eseguono SQL Server e se è configurato il backup di SQL Server, potrebbero verificarsi ritardi nell'esecuzione di snapshot. Impostare la seguente chiave del Registro di sistema se si verificano errori di backup a causa di problemi di snapshot.

   ```
   [HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\BCDRAGENT]
   "USEVSSCOPYBACKUP"="TRUE"
   ```
3. Stato della VM segnalato in modo non corretto perché la VM viene arrestata in RDP.  <br>
   Se la macchina virtuale si è fermata in RDP, verificare nel portale che lo stato della VM venga indicato correttamente. In caso contrario, arrestare la VM nel portale usando l'opzione ''Arresta'' nel dashboard della VM.
4. Se più di quattro VM condividono lo stesso servizio cloud, configurare criteri di backup multipli per organizzare i tempi di backup in modo che non vengano eseguiti più di quattro backup delle VM allo stesso tempo. Provare a distribuire i tempi di avvio del backup ogni ora tra i criteri.
5. La VM è in esecuzione con un uso elevato di CPU/memoria.<br>
   Se la macchina virtuale è in esecuzione con un uso elevato della CPU (&gt; 90%) o della memoria, l'attività di snapshot viene messa in coda, ritardata e infine messa in timeout. In tali situazioni, provare a eseguire un backup su richiesta.

<br>

## <a name="networking"></a>Rete
Analogamente a tutte le estensioni, per il funzionamento delle estensioni di Backup è necessario l'accesso a Internet pubblico. L'assenza di accesso a Internet pubblico può manifestarsi in diversi modi:

* Possono verificarsi errori di installazione dell'estensione.
* Possono verificarsi errori delle operazioni di backup, ad esempio lo snapshot del disco.
* Possono verificarsi errori di visualizzazione dello stato dell'operazione di backup.

La necessità di risolvere gli indirizzi Internet pubblici è stata illustrata [qui](http://blogs.msdn.com/b/mast/archive/2014/06/18/azure-vm-provisioning-stuck-on-quot-installing-extensions-on-virtual-machine-quot.aspx). È necessario controllare le configurazioni DNS per la rete virtuale e assicurarsi che sia possibile risolvere gli URI di Azure.

Dopo la corretta risoluzione dei nomi, sarà necessario fornire anche l'accesso agli IP di Azure. Per sbloccare l'accesso all'infrastruttura di Azure, eseguire la procedura seguente:

1. Aggiungere all'elenco elementi consentiti gli intervalli IP dei data center di Azure.
   * Ottenere l'elenco di [IP dei data center di Azure](https://www.microsoft.com/download/details.aspx?id=41653) da aggiungere all'elenco di IP consentiti.
   * Sbloccare gli IP mediante il cmdlet [New-NetRoute](https://technet.microsoft.com/library/hh826148.aspx) . Eseguire questo cmdlet all’interno della macchina virtuale di Azure, in una finestra di PowerShell con privilegi elevati, eseguita come amministratore.
   * Aggiungere regole al gruppo di sicurezza di rete (se esistente) per consentire l'accesso agli indirizzi IP.
2. Creare un percorso per il flusso del traffico HTTP
   * Se si dispone di alcune limitazioni di rete (un gruppo di sicurezza di rete, ad esempio) distribuire un server proxy HTTP per indirizzare il traffico. I passaggi per distribuire un server proxy HTTP sono reperibili [qui](backup-azure-vms-prepare.md#network-connectivity).
   * Aggiungere regole al gruppo di sicurezza di rete (se esistente) per consentire l'accesso a INTERNET dal proxy HTTP.

> [!NOTE]
> DHCP deve essere abilitato nel computer guest per consentire il funzionamento del backup delle VM IaaS.  Se è necessario un indirizzo IP privato statico, è necessario configurarlo tramite la piattaforma. L'opzione DHCP all'interno della VM deve essere abilitata.
> Vedere altre informazioni sull' [impostazione di un indirizzo IP privato interno statico](../virtual-network/virtual-networks-reserved-private-ip.md).
>
>
