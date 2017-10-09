---
title: l'agente di Backup aaaAzure domande frequenti | Documenti Microsoft
description: 'Risposte alle domande toocommon sul: hello come agente Azure backup funziona, backup e conservazione dei limiti.'
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
keywords: backup e ripristino di emergenza; servizio Backup
ms.assetid: 778c6ccf-3e57-4103-a022-367cc60c411a
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/18/2017
ms.author: trinadhk;pullabhk;
ms.openlocfilehash: bdefb4efb39301f38cdf692bdc93c841a2bbb441
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="questions-about-hello-azure-backup-agent"></a>Domande sull'agente di Backup di Azure hello
In questo articolo ha risposte toocommon domande toohelp comprendere rapidamente i componenti di hello Azure Backup agent. In alcune delle risposte hello, sono disponibili articoli toohello collegamenti con informazioni complete. È anche possibile pubblicare domande sul servizio Azure Backup hello in hello [forum di discussione](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup).

## <a name="configure-backup"></a>Configurare il backup
### <a name="where-can-i-download-hello-latest-azure-backup-agent-br"></a>In cui è possibile scaricare l'agente Azure Backup più recente di hello? <br/>
È possibile scaricare l'ultima versione dell'agente hello per il backup dei client di Windows, Windows Server o System Center DPM da [qui](http://aka.ms/azurebackup_agent). Se si desidera tooback rapidamente una macchina virtuale, utilizzare hello agente della macchina virtuale (che viene installata automaticamente interno corretto hello). Hello agente VM è già presente nelle macchine virtuali create da hello raccolta di Azure.

### <a name="when-configuring-hello-azure-backup-agent-i-am-prompted-tooenter-hello-vault-credentials-do-vault-credentials-expire"></a>Quando si configura l'agente Azure Backup hello, sono richieste tooenter hello insieme di credenziali. Le credenziali dell'insieme di credenziali scadono?
Sì, l'insieme di credenziali hello scada dopo 48 ore. Se il file hello scade, file di log in toohello Azure portal e scaricare hello insieme di credenziali le credenziali dall'insieme di credenziali.

### <a name="what-types-of-drives-can-i-back-up-files-and-folders-from-br"></a>Da quali tipi di unità è possibile eseguire il backup di file e cartelle? <br/>
Non è possibile effettuare hello unità o volumi seguenti:

* Supporto rimovibile: tutte le origini degli elementi di backup devono essere segnalate come corrette.
* Volumi di sola lettura: volume hello deve essere accessibile in scrittura per hello volume shadow copia service (VSS) toofunction.
* Volumi offline: volume hello deve essere online per toofunction VSS.
* Condivisione di rete: volume hello deve essere locale toohello server toobe sottoposti a backup tramite backup in linea.
* Volumi protetti da BitLocker: hello volume deve essere sbloccata prima di poter eseguire il backup di hello.
* Identificazione di file System: NTFS è hello solo file system supportato.

### <a name="what-file-and-folder-types-can-i-back-up-from-my-serverbr"></a>Di quali tipi di file e cartelle è possibile eseguire il backup dal server?<br/>
è supportato i seguenti tipi di Hello:

* Crittografato
* Compresso
* Sparse
* Compresso + Sparse
* Collegamenti reali: non supportato, ignorato
* Punto di analisi: non supportato, ignorato
* Crittografato + Sparse: non supportato, ignorato
* Flusso compresso: non supportato, ignorato
* Flusso di tipo sparse: non supportato, ignorato

### <a name="can-i-install-hello-azure-backup-agent-on-an-azure-vm-already-backed-by-hello-azure-backup-service-using-hello-vm-extension-br"></a>È possibile installare l'agente Azure Backup hello in una macchina virtuale di Azure già eseguito dal servizio di Backup di Azure hello utilizzando hello estensione della macchina virtuale? <br/>
Certo. Backup di Azure fornisce backup a livello di macchina virtuale per le macchine virtuali di Azure utilizzando l'estensione della macchina virtuale hello. tooprotect file e cartelle nel guest hello del sistema operativo Windows, installare l'agente Azure Backup hello in guest hello del sistema operativo Windows.

### <a name="can-i-install-hello-azure-backup-agent-on-an-azure-vm-tooback-up-files-and-folders-present-on-temporary-storage-provided-by-hello-azure-vm-br"></a>È possibile installare l'agente Azure Backup hello in tooback una macchina virtuale di Azure backup di file e cartelle presenti in archiviazione temporanea fornita da Azure VM hello? <br/>
Sì. Installare l'agente Azure Backup hello in guest hello del sistema operativo Windows e il backup di file e cartelle archiviazione tootemporary. Dopo la cancellazione dei dati nell'archivio temporaneo, i processi di backup hanno esito negativo. Inoltre, se i dati di archiviazione temporanea hello sono stati eliminati, è possibile ripristinare solo archiviazione toonon volatile.

### <a name="whats-hello-minimum-size-requirement-for-hello-cache-folder-br"></a>Che cos'è requisito delle dimensioni minime per la cartella della cache di hello hello? <br/>
dimensione di Hello della cartella cache di hello determina la quantità hello di dati che esegue il backup. La cartella della cache deve essere di 5% di spazio hello necessaria per l'archiviazione dei dati.

### <a name="how-do-i-register-my-server-tooanother-datacenterbr"></a>Come è possibile registrare il Data Center tooanother server?<br/>
Dati di backup viene inviati toohello Data Center di hello toowhich di insieme di credenziali che è registrato. Hello più semplice modo toochange hello datacenter toouninstall hello agente e reinstallare l'agente di hello e registrare tooa nuovo insieme di credenziali che appartiene toodesired datacenter.

### <a name="does-hello-azure-backup-agent-work-on-a-server-that-uses-windows-server-2012-deduplication-br"></a>Non hello Azure Backup agent funziona in un server che utilizza la deduplicazione di Windows Server 2012? <br/>
Sì. servizio agente Hello converte hello deduplicato dati toonormal dati quando prepara l'operazione di backup hello. Quindi Ottimizza hello dati per il backup, crittografa i dati di hello e invia quindi crittografato hello dati toohello servizio di backup online.

## <a name="backup"></a>Backup
### <a name="how-do-i-change-hello-cache-location-specified-for-hello-azure-backup-agentbr"></a>Come è possibile modificare il percorso di cache hello specificato per l'agente di Backup di Azure hello?<br/>
Utilizzare hello seguente percorso della cache di hello toochange elenco.

1. Arrestare il motore di Backup hello eseguendo hello seguente comando in un prompt dei comandi con privilegi elevati:

    ```PS C:\> Net stop obengine``` 
  
2. Non spostare i file hello. Copiare invece hello cache spazio cartella tooa diverse unità con spazio sufficiente. lo spazio su cache originale Hello può essere rimossa dopo la conferma hello i backup funzionino con il nuovo spazio di cache hello.
3. Aggiornare hello seguenti voci del registro con hello percorso toohello nuova cartella della cache dello spazio.<br/>

    | Percorso del Registro | Chiave del Registro | Valore |
    | --- | --- | --- |
    | `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config` |ScratchLocation |*Nuovo percorso della cartella della cache* |
    | `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider` |ScratchLocation |*Nuovo percorso della cartella della cache* |

4. Riavviare il motore di Backup hello eseguendo hello seguente comando in un prompt dei comandi con privilegi elevati:

    ```PS C:\> Net start obengine```

Dopo la creazione di backup hello è stata completata nel nuovo percorso della cache di hello, è possibile rimuovere una cartella della cache di hello originale.


### <a name="where-can-i-put-hello-cache-folder-for-hello-azure-backup-agent-toowork-as-expectedbr"></a>In cui si desidera inserire la cartella cache di hello hello Azure Backup Agent toowork come previsto?<br/>
Hello percorsi seguenti per la cartella della cache di hello non sono consigliate:

* Condivisione di rete supporti rimovibili: la cartella della cache di hello deve essere locale toohello server necessarie per il backup tramite backup online. I percorsi di rete o i supporti rimovibili, ad esempio le unità USB, non sono supportati.
* Volumi offline: la cartella della cache di hello deve essere online per il backup previsto con Azure Backup Agent.

### <a name="are-there-any-attributes-of-hello-cache-folder-that-are-not-supportedbr"></a>Sono presenti tutti gli attributi di cartella della cache di hello non sono supportati?<br/>
Hello seguenti attributi o le relative combinazioni non sono supportati per la cartella della cache di hello:

* Crittografato
* De-duplicated
* Compresso
* Sparse
* Reparse-Point

cartella della cache di Hello e metadati hello VHD non ha gli attributi necessari hello per l'agente Azure Backup hello.

### <a name="is-there-a-way-tooadjust-hello-amount-of-bandwidth-used-by-hello-backup-servicebr"></a>È disponibile una quantità di hello tooadjust modalità della larghezza di banda utilizzata dal servizio di Backup hello?<br/>
  Sì, usare hello **Modifica proprietà** opzione larghezza di banda tooadjust hello agente di Backup. È possibile regolare la quantità hello di larghezza di banda e hello volte quando si utilizza la larghezza di banda. Per istruzioni dettagliate, vedere **[Abilitare la limitazione della larghezza di banda](backup-configure-vault.md#enable-network-throttling)**.

## <a name="manage-backups"></a>Gestire i backup
### <a name="what-happens-if-i-rename-a-windows-server-that-is-backing-up-data-tooazurebr"></a>Cosa succede se si rinomina un server di Windows che esegue il backup dei dati tooAzure?<br/>
Quando si rinomina un server, tutti i backup attualmente configurati vengono arrestati.
Registrare hello nuovo nome del server hello insieme di credenziali di Backup hello. Quando si registra nuovo nome hello con insieme di credenziali hello, hello prima operazione di backup è un *completo* backup. Se è necessario dati toorecover sottoposti a backup insieme di credenziali toohello con nome hello del server precedente, utilizzare hello [ **un altro server** ](backup-azure-restore-windows-server.md#use-instant-restore-to-restore-data-to-an-alternate-machine) opzione hello **Ripristina dati** procedura guidata.

### <a name="what-is-hello-maximum-file-path-length-that-can-be-specified-in-backup-policy-using-azure-backup-agent-br"></a>Che cos'è hello lunghezza massima percorso del file che può essere specificato nei criteri di Backup utilizzando l'agente Azure Backup? <br/>
L'agente di Backup di Azure si basa su NTFS. Hello [specifica della lunghezza di filepath è limitata dalle API di Windows hello](https://msdn.microsoft.com/library/aa365247.aspx#fully_qualified_vs._relative_paths). Se il file hello da tooprotect dispone di una lunghezza di percorso del file supera il valore consentito dall'API di Windows hello, eseguire il backup cartella padre hello o unità disco hello.  

### <a name="what-characters-are-allowed-in-file-path-of-azure-backup-policy-using-azure-backup-agent-br"></a>Quali caratteri sono consentiti nel percorso file dei criteri di Backup di Azure che usano l'agente di Backup di Azure? <br>
 L'agente di Backup di Azure si basa su NTFS. Consente i [caratteri supportati da NTFS](https://msdn.microsoft.com/library/aa365247.aspx#naming_conventions) come parte della specifica file. 
 
### <a name="i-receive-hello-warning-azure-backups-have-not-been-configured-for-this-server-even-though-i-configured-a-backup-policy-br"></a>Viene visualizzato l'avviso "Backup di Azure non sono stati configurati per il server di" hello, anche se è configurato un criterio di backup <br/>
Questo avviso si verifica quando le impostazioni di pianificazione del backup hello archiviate nel server locale hello hello identico hello impostazioni archiviate nell'insieme di credenziali backup hello. Quando il server hello o impostazioni hello sono stato ripristinato tooa stato funzionante, pianificazioni di backup hello possono perdere la sincronizzazione. Se viene visualizzato questo avviso, [riconfigurare i criteri di backup hello](backup-azure-manage-windows-server.md) e quindi **eseguire backup immediato** server locale di hello tooresynchronize con Azure.
