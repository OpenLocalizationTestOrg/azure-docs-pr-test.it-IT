---
title: "aaaSecurity toohelp di funzionalità di protezione dei backup di ibrido che usano i Backup di Azure | Documenti Microsoft"
description: "Informazioni su come funzionalità di sicurezza toouse nei backup toomake Azure Backup più sicure"
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: 47bc8423-0a08-4191-826d-3f52de0b4cb8
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: pajosh
ms.openlocfilehash: 17a0f5e877f84af53c15062ec4a8df480383125e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="security-features-toohelp-protect-hybrid-backups-that-use-azure-backup"></a>Toohelp funzionalità di sicurezza di protezione dei backup di ibride che utilizzano i Backup di Azure
Le preoccupazioni riguardo ai problemi di sicurezza, come malware, ransomware e intrusioni, aumentano continuamente. Questi problemi di sicurezza possono essere costosi in termini di denaro e di dati. tooguard da tali attacchi, Backup di Azure ora fornisce sicurezza toohelp funzionalità di protezione dei backup di ibrida. Questo articolo descrive come tooenable e utilizzare queste funzionalità, utilizzando un agente di servizi di ripristino di Azure e i Server di Backup di Azure. Queste funzionalità includono:

- **Prevenzione**. Ogni volta che viene eseguita un'operazione critica, come la modifica di una passphrase, viene aggiunto un ulteriore livello di autenticazione. La convalida è tooensure che tali operazioni possono essere eseguite solo da utenti che dispongono di credenziali di Azure valide.
- **Invio di avvisi**. Verrà inviata una notifica di posta elettronica toohello amministratore della sottoscrizione ogni volta che un'operazione critica, ad esempio l'eliminazione di dati di backup viene eseguita. Questo messaggio di posta elettronica garantisce che l'utente hello notifica rapidamente su tali azioni.
- **Ripristino**. Dati di backup eliminati vengono mantenuti per un ulteriore 14 giorni dalla data di hello di eliminazione hello. In questo modo si garantisce la recuperabilità dei dati hello all'interno di un determinato periodo di tempo, pertanto non c'è alcuna perdita di dati, anche se si verifica un attacco. Inoltre, un numero maggiore di punti di recupero con registrazione minima viene mantenuto tooguard contro dati danneggiati.

> [!NOTE]
> Le funzionalità di sicurezza non devono essere abilitate se si usa il backup di VM IaaS (Infrastructure as a Service, infrastruttura distribuita come servizio). Poiché queste funzionalità non sono ancora disponibili per il backup di VM IaaS, la loro abilitazione non avrà alcun impatto. Le funzionalità di sicurezza devono essere abilitate solo se si usa: <br/>
>  * **Agente di Backup di Azure**. Versione minima dell'agente: 2.0.9052. Dopo avere abilitato queste funzionalità, è consigliabile aggiornare operazioni critiche tooperform versione agente toothis. <br/>
>  * **Server di Backup di Azure**. Versione minima dell'agente di Backup di Azure: 2.0.9052, con l'aggiornamento 1 del server di Backup di Azure. <br/>
>  * **System Center Data Protection Manager**. Versione minima dell'agente di Backup di Azure: 2.0.9052, con Data Protection Manager 2012 R2 UR12 o Data Protection Manager 2016 UR2. <br/> 


> [!NOTE]
> Queste funzionalità sono disponibili solo per l'insieme di credenziali dei Servizi di ripristino. Hello tutti i nuovi insiemi di credenziali di servizi di ripristino hanno le funzionalità abilitate per impostazione predefinita. Per gli archivi di servizi di ripristino esistenti, gli utenti abilitano queste funzionalità tramite i passaggi di hello indicati nella seguente sezione hello. Dopo aver hello funzionalità sono abilitate, si applicano i computer agente di servizi di ripristino hello tooall, le istanze del Server di Backup di Azure e registrati con l'insieme di credenziali hello server Data Protection Manager. L'abilitazione di questa impostazione è un'azione eseguibile una volta sola e in seguito non sarà più possibile disabilitare le funzionalità.
>

## <a name="enable-security-features"></a>Abilitare le funzionalità di sicurezza
Se si sta creando un insieme di credenziali di servizi di ripristino, è possibile utilizzare tutte le funzionalità di sicurezza hello. Se si usa un insieme di credenziali esistente, abilitare le funzionalità di sicurezza eseguendo questa procedura:

1. Accedi toohello portale di Azure utilizzando le credenziali di Azure.
2. Selezionare **Sfoglia** e quindi digitare **Servizi di ripristino**.

    ![Screenshot dell'opzione Sfoglia del portale di Azure](./media/backup-azure-security-feature/browse-to-rs-vaults.png) <br/>

    viene visualizzato l'elenco di Hello degli archivi di servizi di ripristino. Selezionare un insieme di credenziali dall'elenco. Apre il dashboard di Hello insieme di credenziali selezionato.
3. Elenco di hello di elementi visualizzato in insieme di credenziali, hello in **impostazioni**, fare clic su **proprietà**.

    ![Screenshot delle opzioni per l'insieme di credenziali di Servizi di ripristino](./media/backup-azure-security-feature/vault-list-properties.png)
4. Fare clic su **Aggiorna** in **Impostazioni di sicurezza**.

    ![Screenshot delle proprietà dell'insieme di credenziali di Servizi di ripristino](./media/backup-azure-security-feature/security-settings-update.png)

    aggiornare il collegamento Hello apre hello **le impostazioni di sicurezza** pannello, che fornisce un riepilogo delle funzionalità di hello e consente di abilitarle.
5. Dall'elenco a discesa hello **sono state configurate Azure multi-Factor Authentication?**, selezionare un valore tooconfirm se è stata abilitata [Azure multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md). Se è abilitato, viene richiesto durante la firma nel portale di Azure toohello tooauthenticate da un altro dispositivo (ad esempio, un telefono cellulare).

   Quando si eseguono operazioni critiche nel Backup, è possibile tooenter un PIN, disponibile nel portale di Azure hello di sicurezza. L'abilitazione di Azure Multi-Factor Authentication aggiunge un livello di sicurezza. Solo gli utenti con le credenziali di Azure valide autorizzati e autenticati da un secondo dispositivo, è possibile accedere hello portale di Azure.
6. Selezionare le impostazioni di sicurezza, toosave **abilitare** e fare clic su **salvare**. È possibile selezionare **abilitare** solo dopo aver selezionato un valore in hello **sono state configurate Azure multi-Factor Authentication?** elenco nel passaggio precedente hello.

    ![Screenshot delle impostazioni di sicurezza](./media/backup-azure-security-feature/enable-security-settings-dpm-update.png)

## <a name="recover-deleted-backup-data"></a>Ripristino dei dati di backup eliminati
Mantiene i dati di backup eliminati per 14 giorni, backup e non viene eliminata immediatamente se hello **Interrompi backup con dati di backup delete** viene eseguita l'operazione. toorestore questi dati in hello 14 giorni, richiedere hello alla procedura seguente, a seconda di ciò che si utilizza:

Per utenti dell'**agente di Servizi di ripristino di Azure**:

1. Se il computer di hello backup sono stati in cui il problema è ancora disponibile, utilizzare [ripristinare dati toohello nello stesso computer](backup-azure-restore-windows-server.md#use-instant-restore-to-recover-data-to-the-same-machine) in servizi di ripristino di Azure, toorecover da tutti i punti di ripristino precedente hello.
2. Se il computer non è disponibile, utilizzare [ripristino tooan alternativo macchina](backup-azure-restore-windows-server.md#use-instant-restore-to-restore-data-to-an-alternate-machine) toouse un'altra tooget di computer Servizi di ripristino di Azure questi dati.

Per gli utenti che usano il **server di Backup di Azure**:

1. Se il server di hello backup sono stati in cui il problema è ancora disponibile, riproteggere hello eliminato le origini dati e utilizzare hello **Ripristina dati** funzionalità toorecover da tutti i punti di ripristino precedente hello.
2. Se il server non è disponibile, utilizzare [ripristinare i dati da un altro Server di Backup di Azure](backup-azure-alternate-dpm-server.md) toouse un altro Server di Backup di Azure istanza tooget questi dati.

Per gli utenti di **Data Protection Manager**:

1. Se il server di hello backup sono stati in cui il problema è ancora disponibile, riproteggere hello eliminato le origini dati e utilizzare hello **Ripristina dati** funzionalità toorecover da tutti i punti di ripristino precedente hello.
2. Se il server non è disponibile, utilizzare [Aggiungi DPM esterno](backup-azure-alternate-dpm-server.md) toouse un'altra Data Protection Manager server tooget questi dati.

## <a name="prevent-attacks"></a>Prevenire gli attacchi
Controlli sono stati aggiunti toomake che solo gli utenti validi è possono eseguire diverse operazioni. Questi controlli includono l'aggiunta di un ulteriore livello di autenticazione e il mantenimento di un intervallo minimo di conservazione per scopi di ripristino.

### <a name="authentication-tooperform-critical-operations"></a>Operazioni di autenticazione tooperform critiche
Come parte dell'aggiunta di un ulteriore livello di autenticazione per le operazioni critiche, sono richieste tooenter un PIN di sicurezza quando si eseguono **Arresta protezione dati con dati di eliminazione** e **modifica Passphrase** operazioni .

tooreceive questo PIN:

1. Accedi toohello portale di Azure.
2. Sfoglia troppo**insieme di credenziali di servizi di ripristino** > **impostazioni** > **proprietà**.
3. Fare clic su **Genera** in **PIN di sicurezza**. Verrà aperto un pannello che contiene toobe PIN hello immesso nell'interfaccia utente dell'agente di servizi di ripristino di Azure hello.
    Questo PIN è valido solo per cinque minuti e viene generato automaticamente dopo questo periodo.

### <a name="maintain-a-minimum-retention-range"></a>Mantenimento di un intervallo minimo di conservazione
punti disponibili tooensure vengono sempre un numero di ripristino valido, hello seguenti controlli è stati aggiunti:

- Per la conservazione giornaliera, è necessario garantire almeno **sette** giorni.
- Per la conservazione settimanale, è necessario garantire almeno **quattro** settimane.
- Per la conservazione mensile, è necessario garantire almeno **tre** mesi.
- Per la conservazione annuale, è necessario garantire almeno **un** anno.

## <a name="notifications-for-critical-operations"></a>Notifiche relative alle operazioni critiche
In genere, quando viene eseguita un'operazione critica, salve sottoscrizione viene inviata una notifica di posta elettronica con i dettagli sull'operazione hello. È possibile configurare i destinatari di posta elettronica aggiuntivi per queste notifiche utilizzando hello portale di Azure.

funzionalità di sicurezza Hello indicate in questo articolo forniscono meccanismi di difesa contro gli attacchi di destinazione. Ancora più importante, se si verifica un attacco, queste funzionalità consentono di hello toorecover capacità dei dati.

## <a name="troubleshooting-errors"></a>Risoluzione dei problemi
| Operazione | Dettagli errore | Risoluzione |
| --- | --- | --- |
| Modifica dei criteri |Impossibile modificare i criteri di backup Hello. Errore: hello corrente non riuscita a causa di errore interno del servizio tooan [0x29834]. Ripetere l'operazione di hello dopo qualche minuto. Se hello problema persiste, contattare il supporto tecnico Microsoft. |**Causa:**<br/>Questo errore si verifica quando sono abilitate le impostazioni di sicurezza, si tenta di mantenimento dati tooreduce sotto valori minimi di hello specificato in precedenza e si è nella versione non supportata (le versioni supportate sono specificate nella nota prima di questo articolo). <br/>**Azione consigliata:**<br/> In questo caso, è necessario impostare il periodo di memorizzazione sopra hello memorizzazione minimo periodo indicato (sette giorni per ogni giorno, quattro settimane per ogni settimana, tre settimane per mese o anno per la frequenza annuale) tooproceed con i criteri relativi aggiornamenti. Facoltativamente, approccio consigliato sarebbe tooupdate l'agente di backup, gli aggiornamenti della sicurezza di hello tutti i Server di Backup di Azure e/o DPM UR tooleverage. |
| Modificare la passphrase |Il PIN di sicurezza immesso non è corretto. (ID: 100130) Fornire toocomplete PIN di sicurezza corretto hello questa operazione. |**Causa:**<br/> Questo errore si verifica quando si immette un PIN di sicurezza non valido o scaduto durante l'esecuzione di operazioni critiche, ad esempio la modifica della passphrase. <br/>**Azione consigliata:**<br/> operazione di hello toocomplete, è necessario immettere il PIN di sicurezza valido. tooget hello PIN, accedere nel portale tooAzure e passare l'insieme di credenziali di servizi tooRecovery > Impostazioni > Proprietà > Genera PIN di sicurezza. Utilizzare questa passphrase toochange PIN. |
| Modificare la passphrase |Operazione non riuscita. ID: 120002 |**Causa:**<br/>Questo errore si verifica quando si abilitano le impostazioni di sicurezza, si tenta di passphrase toochange e si è nella versione non supportata (versioni valide specificate nella prima nota di questo articolo).<br/>**Azione consigliata:**<br/> passphrase toochange, è necessario aggiornare prima versione dell'agente di backup toominimum 2.0.9052 minimo, Azure Backup server toominimum update 1 e/o DPM toominimum UR12 di DPM 2012 R2 o DPM 2016 UR2 (download collegamenti riportati di seguito), quindi immettere il PIN di sicurezza valido. tooget hello PIN, accedere nel portale tooAzure e passare l'insieme di credenziali di servizi tooRecovery > Impostazioni > Proprietà > Genera PIN di sicurezza. Utilizzare questa passphrase toochange PIN. |

## <a name="next-steps"></a>Passaggi successivi
* [Introduzione a servizi di ripristino di Azure dell'insieme di credenziali](backup-azure-vms-first-look-arm.md) tooenable queste funzionalità.
* [Scaricare l'agente di servizi di ripristino di Azure più recenti hello](http://aka.ms/azurebackup_agent) toohelp proteggere i computer Windows e proteggersi da attacchi ai dati di backup.
* [Download hello Server di Backup più recente di Azure](https://aka.ms/latest_azurebackupserver) toohelp proteggere carichi di lavoro e i dati di backup da attacchi di protezione.
* [Scaricare UR12 per System Center 2012 R2 Data Protection Manager](https://support.microsoft.com/help/3209592/update-rollup-12-for-system-center-2012-r2-data-protection-manager) o [scaricare UR2 per System Center 2016 Data Protection Manager](https://support.microsoft.com/help/3209593/update-rollup-2-for-system-center-2016-data-protection-manager) toohelp proteggere carichi di lavoro e i dati di backup da attacchi di protezione.
