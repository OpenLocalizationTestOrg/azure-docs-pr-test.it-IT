---
title: aaaTroubleshoot Azure backup errori nel portale classico | Documenti Microsoft
description: Risolvere i problemi di Backup e ripristino di macchine virtuali di Azure nel portale classico hello Azure.
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: 117201fb-c0cd-4be4-b47f-abd88fe914cf
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 1/23/2017
ms.author: trinadhk;markgal;
ms.openlocfilehash: b9907f6fa57c631f5446c4d00f946a57c4efd72b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-virtual-machine-backup"></a>Risolvere i problemi relativi al backup delle macchine virtuali di Azure
> [!div class="op_single_selector"]
> * [Insieme di credenziali dei servizi di ripristino](backup-azure-vms-troubleshoot.md)
> * [Insieme di credenziali per il backup](backup-azure-vms-troubleshoot-classic.md)
>
>

È possibile risolvere gli errori rilevati durante tramite Backup di Azure con le informazioni elencate nella tabella hello riportato di seguito.

## <a name="discovery"></a>Individuazione
| Operazione di backup | Dettagli errore | Soluzione alternativa |
| --- | --- | --- |
| Individuazione |Non è stato possibile toodiscover nuovi elementi - Backup di Microsoft Azure ha rilevato e di errore interno. Attendere qualche minuto e quindi riprovare hello. |Ripetere il processo di individuazione hello dopo 15 minuti. |
| Individuazione |Non è stato possibile toodiscover nuovi elementi: individuazione di un'altra operazione è già in corso. Attendere finché non viene completata l'operazione di individuazione corrente hello. |Nessuno |

## <a name="register"></a>Registra
| Operazione di backup | Dettagli errore | Soluzione alternativa |
| --- | --- | --- |
| Registra |Numero di dischi dati collegati limite di hello supportata della macchina virtuale superato toohello - scollegare alcuni dischi dati in questa operazione hello macchina virtuale e riprovare. Azure supporta backup di dischi dati too16 associata tooan macchina virtuale per il backup di Azure |Nessuno |
| Registra |Backup di Microsoft Azure ha rilevato un errore interno - attendere qualche minuto, quindi riprovare hello. Se hello problema persiste, contattare il supporto Microsoft. |È possibile ottenere questo errore a causa di tooone di hello seguente non supportato di configurazione della macchina virtuale in archiviazione con ridondanza locale Premium. <br> Il backup delle macchine virtuali di Archiviazione Premium può essere eseguito usando l'insieme di credenziali di Servizi di ripristino. [Altre informazioni](backup-introduction-to-azure-backup.md#using-premium-storage-vms-with-azure-backup) |
| Registra |Registrazione non riuscita con timeout dell'operazione dell'agente di installazione |Controllare se la versione di hello del sistema operativo della macchina virtuale hello è supportata. |
| Registra |L'esecuzione del comando non è riuscita. In questo elemento è già in corso un'altra operazione. Attendere il completamento dell'operazione precedente hello |Nessuno |
| Registra |Le macchine virtuali con dischi rigidi virtuali archiviati nel servizio di archiviazione Premium non sono supportate per il backup |None |
| Registra |Agente della macchina virtuale non è presente nella macchina virtuale hello: installare hello necessari prerequisiti, agente di macchine Virtuali e riavviare l'operazione di hello. |[Ulteriori](#vm-agent) sull'installazione dell'agente VM e come toovalidate hello installazione dell'agente VM. |

## <a name="backup"></a>Backup
| Operazione di backup | Dettagli errore | Soluzione alternativa |
| --- | --- | --- |
| Backup |Impossibile comunicare con l'agente VM hello per lo stato dello snapshot. Timeout della sottoattività di snapshot macchina virtuale. -Vedere risoluzione dei problemi di hello Guida su come tooresolve questo. |Questo errore viene generato se si è verificato un problema con hello agente della macchina virtuale o toohello di accesso di rete dell'infrastruttura di Azure è bloccata in qualche modo. Vedere altre informazioni sul [debug dei problemi di snapshot della macchina virtuale](backup-azure-troubleshoot-vm-backup-fails-snapshot-timeout.md). <br> Se l'agente VM hello non causa problemi, quindi riavviare hello macchina virtuale. In alcuni casi uno stato macchina virtuale non corretto può causare problemi e il riavvio di hello VM Reimposta questo stato"non valido" |
| Backup |Backup non riuscito con errore interno: ripetere hello operazione tra qualche minuto. Se hello problema persiste, contattare il supporto Microsoft |Verificare se esiste un problema temporaneo durante l'accesso alla risorsa di archiviazione della macchina virtuale. Verificare [stato Azure](https://azure.microsoft.com/en-us/status/) toosee se è presente un problema correlato toocompute / / rete di archiviazione nell'area di hello in corso. . Riprova hello post backup problema viene ridotta. |
| Backup |Impossibile eseguire l'operazione di hello come macchina virtuale non esiste più. |Impossibile eseguire il backup perché hello macchina virtuale configurata per il backup è stato eliminato. Per passare visualizzazione degli elementi tooProtected arrestare altri backup, selezionare l'elemento protetto e fare clic su Arresta protezione dati. È possibile conservare i dati selezionando l'opzione Conserva i dati di backup. Sarà successivamente possibile riprendere la protezione per questa macchina virtuale facendo clic su Configura protezione dalla vista Elementi registrati |
| Backup |Non riuscito tooinstall hello estensione di servizi di ripristino di Azure nell'elemento selezionato hello - agente VM è un prerequisito per l'estensione di servizi di ripristino di Azure. Installare l'agente VM di Azure hello e riavviare l'operazione di registrazione hello |<ol> <li>Controllare se l'agente VM hello è stato installato correttamente. <li>Verificare che hello flag di configurazione della macchina hello sia impostata correttamente.</ol> [Ulteriori](#validating-vm-agent-installation) sull'installazione dell'agente VM e come toovalidate hello installazione dell'agente VM. |
| Backup |L'esecuzione del comando non è riuscita. In questo elemento è attualmente in corso un'altra operazione. Attendere il completamento dell'operazione precedente hello e quindi riprovare. |È in esecuzione un processo di backup o ripristino esistente per hello VM e non può avviare un nuovo processo durante l'esecuzione di processo esistente hello. |
| Backup |L'installazione dell'estensione non è riuscita con errore hello "COM+ non è stato Impossibile tootalk toohello Microsoft Distributed Transaction Coordinator |In genere, ciò significa che servizio hello COM+ non è in esecuzione. Per informazioni su come correggere l'errore, contattare il supporto tecnico Microsoft. |
| Backup |Snapshot non riuscita con hello errore operazione VSS "questa unità è bloccata da crittografia unità BitLocker. Sbloccare l'unità dal Pannello di controllo. |Disattivare BitLocker per tutte le unità hello VM e osservare se hello VSS viene risolto |
| Backup |Le macchine virtuali con dischi rigidi virtuali archiviati nel servizio di archiviazione Premium non sono supportate per il backup |None |
| Backup |La macchina virtuale di Azure non è stata trovata. |Ciò accade quando hello VM primaria viene eliminata, ma i criteri di backup hello continua toolook per un backup tooperform macchina virtuale. toofix questo errore: <ol><li>Ricreare la macchina virtuale hello con hello stesso nome e nome gruppo di risorse stesso [nome] del servizio cloud, <br>OPPURE <li> Disabilitare la protezione per questa macchina virtuale in modo che non vengano attivati backup successivi. </ol> |
| Backup |Agente della macchina virtuale non è presente nella macchina virtuale hello: installare hello necessari prerequisiti, agente di macchine Virtuali e riavviare l'operazione di hello. |[Ulteriori](#vm-agent) sull'installazione dell'agente VM e come toovalidate hello installazione dell'agente VM. |

## <a name="jobs"></a>Processi
| Operazione | Dettagli errore | Soluzione alternativa |
| --- | --- | --- |
| Annulla processo |Annullamento non è supportata per questo tipo di processo, attendere fino al completamento del processo di hello. |Nessuno |
| Annulla processo |Hello processo non è in uno stato annullabile: attendere il completamento del processo di hello. <br>OPPURE<br> processo di Hello selezionato non è in uno stato annullabile - attendere toocomplete processo hello. |È molto probabile processo hello quasi completata. Attendere il completamento del processo di hello |
| Annulla processo |Impossibile annullare il processo di hello perché non è in corso: annullamento è supportato solo per i processi che sono in corso. Tentare l'annullamento solo per un processo in corso. |Ciò si verifica a causa dello stato transitorio tooa. Attendere alcuni minuti e ripetere l'operazione di annullamento hello |
| Annulla processo |Errore toocancel hello processo - attendere fino al completamento del processo. |Nessuno |

## <a name="restore"></a>Ripristino
| Operazione | Dettagli errore | Soluzione alternativa |
| --- | --- | --- |
| Ripristino |Ripristino non riuscito con errore interno del cloud |<ol><li>Toowhich servizio cloud che si sta tentando di toorestore è configurato con le impostazioni DNS. Verificare  <br>$deployment = Get-AzureDeployment -ServiceName "ServiceName" -Slot "Production"     Get-AzureDns -DnsSettings $deployment.DnsSettings<br>Se è presente un indirizzo configurato, significa che le impostazioni DNS sono configurate.<br> <li>Sta tentando di cloud service toowhich tooyou toorestore è configurata con l'IP riservato e macchine virtuali esistenti nel servizio cloud sono in stato di arresto.<br>È possibile controllare che il servizio cloud disponga di IP riservato tramite i cmdlet di PowerShell seguenti:<br>$deployment = Get-AzureDeployment -ServiceName "servicename" -Slot "Production" $dep.ReservedIPName <br><li>Si sta tentando di una macchina virtuale con configurazioni di rete speciali seguenti nel servizio cloud toosame toorestore. <br>- Macchine virtuali con configurazione del servizio di bilanciamento del carico (interno ed esterno)<br>- Macchine virtuali con più indirizzi IP riservati<br>- Macchine virtuali con più schede di rete<br>Selezionare un nuovo servizio cloud in hello dell'interfaccia utente o consultare troppo[ripristinare considerazioni](backup-azure-restore-vms.md#restoring-vms-with-special-network-configurations) per le macchine virtuali con configurazioni di rete speciali</ol> |
| Ripristino |nome DNS Hello selezionato è già in uso:. specificare un nome DNS diverso e riprovare. |Hello qui il nome DNS fa riferimento toohello nome del servizio cloud (in genere terminano con. n e t). Questa operazione deve toobe univoco. Se si verifica questo errore, è necessario toochoose un diverso nome della macchina virtuale durante il ripristino. <br><br> Questo errore viene visualizzato solo toousers di hello portale di Azure. Hello operazione di ripristino tramite PowerShell ha esito positivo perché solo Ripristina dischi hello e non è possibile creare hello macchina virtuale. Errore Hello verrà affligge hello macchina virtuale viene creata in modo esplicito dall'utente dopo un'operazione di ripristino disco hello. |
| Ripristino |configurazione di rete virtuale specificata Hello non è corretta - specificare una configurazione di rete virtuale diverso e riprovare. |Nessuno |
| Ripristino |Hello specificata utilizza un IP riservato che non corrisponde alla configurazione di hello della macchina virtuale hello in fase di ripristino -. specificare un altro servizio cloud che non utilizzi un indirizzo IP riservato o scegliere un altro toorestore di punto di ripristino dal servizio cloud. |Nessuno |
| Ripristino |Servizio cloud ha raggiunto limite sul numero di endpoint di input - operazione di hello riprovare specificando un altro servizio cloud o tramite un endpoint esistente. |Nessuno |
| Ripristino |Account di archiviazione di destinazione e di insieme di credenziali di backup sono in due aree diverse, verificare che l'account di archiviazione hello specificato nell'operazione di ripristino sia in hello stessa area di Azure come archivio di backup hello. |Nessuno |
| Ripristino |Account di archiviazione specificato per l'operazione di ripristino hello non è supportata - gli account di archiviazione solo Basic/Standard con ridondanza locale o le impostazioni di replica con ridondanza geografica sono supportate. Selezionare un account di archiviazione supportato |None |
| Ripristino |Tipo di Account di archiviazione specificato per l'operazione di ripristino non è online, verificare che l'account di archiviazione hello specificato nell'operazione di ripristino sia online |Questa situazione può verificarsi a causa di un errore temporaneo in archiviazione di Azure o a causa di un'interruzione di tooan. Scegliere un altro account di archiviazione. |
| Ripristino |È stata raggiunta la Quota di gruppo di risorse, eliminare alcuni gruppi di risorse dal portale Azure oppure contattare il supporto tecnico di Azure tooincrease hello limiti. |Nessuno |
| Ripristino |La subnet selezionata non esiste. Selezionare una subnet esistente |None |

## <a name="policy"></a>Criterio
| Operazione | Dettagli errore | Soluzione alternativa |
| --- | --- | --- |
| Crea criteri |Criteri di hello toocreate - non ridurre toocontinue scelte di conservazione hello con la configurazione dei criteri. |Nessuno |

## <a name="vm-agent"></a>Agente di macchine virtuali
### <a name="setting-up-hello-vm-agent"></a>Impostazione di hello agente della macchina virtuale
In genere, hello agente VM è già presente nelle macchine virtuali create da hello raccolta di Azure. Tuttavia, le macchine virtuali vengono migrate da Data Center locale non avrebbero hello agente VM installato. Per tali macchine virtuali, hello agente VM deve toobe installato in modo esplicito. Altre informazioni sui [l'installazione dell'agente VM hello in una macchina virtuale esistente](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx).

Per VM di Windows:

* Scaricare e installare hello [agente MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Sarà necessario installazione hello toocomplete privilegi di amministratore.
* [Aggiorna proprietà macchina virtuale hello](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) tooindicate che hello agente è installato.

Per le macchine virtuali Linux:

* Installare l' [agente Linux](https://github.com/Azure/WALinuxAgent) più recente da Github.
* [Aggiorna proprietà macchina virtuale hello](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) tooindicate che hello agente è installato.

### <a name="updating-hello-vm-agent"></a>Aggiornamento agente VM hello
Per VM di Windows:

* Aggiornamento hello agente della macchina virtuale è semplice come reinstallare hello [binari agente VM](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Tuttavia, è necessario tooensure in esecuzione alcuna operazione di backup durante hello che agente VM viene aggiornata.

Per le macchine virtuali Linux:

* Seguire le istruzioni di hello [aggiornamento agente VM Linux](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

### <a name="validating-vm-agent-installation"></a>Convalida dell'installazione dell'agente di VM
Toocheck per hello come versione di agente di macchine Virtuali in macchine virtuali Windows:

1. Accedere toohello macchina virtuale di Azure e passare la cartella toohello *C:\WindowsAzure\Packages*. È necessario trovare un file WaAppAgent.exe hello presentano.
2. Fare clic sul file hello, andare troppo**proprietà**, quindi selezionare hello **dettagli** campo versione prodotto di hello scheda deve essere 2.6.1198.718 o versione successiva
