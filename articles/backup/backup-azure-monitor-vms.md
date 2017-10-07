---
title: i backup di distribuzione di gestione risorse di macchina virtuale aaaMonitor | Documenti Microsoft
description: Monitorare gli eventi e gli avvisi dei backup delle macchine virtuali distribuite con Resource Manager. Inviare messaggi di posta elettronica in base agli avvisi.
services: backup
documentationcenter: dev-center-name
author: markgalioto
manager: carmonm
editor: 
ms.assetid: fed32015-2db2-44f8-b204-d89f6fd1bea2
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/21/2016
ms.author: markgal;trinadhk;giridham;
ms.openlocfilehash: bf45cbaa05621b2365c26bafa1bd8223a444c1fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-alerts-for-azure-virtual-machine-backups"></a>Monitorare gli avvisi per i backup della macchina virtuale di Azure
Gli avvisi sono le risposte dal servizio hello che una soglia di evento è stato soddisfatta o superata. Sapere quando si avvia problemi può essere tookeeping critici i costi di business. In genere non si verificano avvisi in base alla pianificazione ed è utile tooknow appena possibile dopo gli avvisi vengono generati. Ad esempio, quando un processo di backup o ripristino non riesce, viene generato un avviso di errore hello cinque minuti. Dashboard dell'insieme di credenziali hello hello riquadro avvisi di Backup consente di visualizzare gli eventi critici e a livello di avviso. Nelle impostazioni di hello gli avvisi di Backup, è possibile visualizzare tutti gli eventi. Ma cosa fare se un avviso viene generato mentre si lavora a un problema diverso? Se non si conosce in caso di avviso hello, potrebbe essere un inconveniente secondario o potrebbe compromettere i dati. Quando si verifica, toomake coloro hello che è a conoscenza di un avviso - configurare hello servizio toosend notifiche di avviso tramite posta elettronica. Per informazioni dettagliate sulla configurazione di notifiche di posta elettronica, vedere [Configurare le notifiche](backup-azure-monitor-vms.md#configure-notifications).

## <a name="how-do-i-find-information-about-hello-alerts"></a>Ricerca di informazioni sugli avvisi hello
tooview informazioni sull'evento hello che ha generato un avviso, è necessario aprire il pannello di avvisi di Backup hello. Esistono due Pannello di avvisi di Backup dall'hello tooopen modi: dal riquadro avvisi di Backup nel dashboard dell'insieme di credenziali hello hello o dal Pannello di hello avvisi ed eventi.

riquadro blade di avvisi di Backup tooopen hello dagli avvisi di Backup:

* In hello **gli avvisi di Backup** riquadro nel dashboard dell'insieme di credenziali hello, fare clic su **critico** o **avviso** tooview hello gli eventi operativi per tale livello di gravità.

    ![Riquadro Avvisi di backup](./media/backup-azure-monitor-vms/backup-alerts-tile.png)

Pannello di avvisi di Backup tooopen hello dal Pannello di avvisi ed eventi hello:

1. Dashboard dell'insieme di credenziali hello fare clic su **tutte le impostazioni**. ![Pulsante Tutte le impostazioni](./media/backup-azure-monitor-vms/all-settings-button.png)
2. In hello **impostazioni** pannello, fare clic su **avvisi ed eventi**. ![Pulsante Avvisi ed eventi](./media/backup-azure-monitor-vms/alerts-and-events-button.png)
3. In hello **avvisi ed eventi** pannello, fare clic su **gli avvisi di Backup**. ![Pulsante Avvisi di backup](./media/backup-azure-monitor-vms/backup-alerts.png)

    Hello **gli avvisi di Backup** pannello apre e Visualizza hello avvisi filtrati.

    ![Riquadro Avvisi di backup](./media/backup-azure-monitor-vms/backup-alerts-critical.png)
4. tooview informazioni dettagliate su un avviso specifico, dall'elenco di hello degli eventi, fare clic su tooopen avviso hello relativo **dettagli** blade.

    ![Dettagli dell'evento](./media/backup-azure-monitor-vms/audit-logs-event-detail.png)

    gli attributi di hello toocustomize visualizzati nell'elenco di hello, vedere [consente di visualizzare gli attributi dell'evento aggiuntive](backup-azure-monitor-vms.md#view-additional-event-attributes)

## <a name="configure-notifications"></a>Configurare le notifiche
 È possibile configurare notifiche tramite posta elettronica di hello servizio toosend per gli avvisi di hello che si è verificato su hello passati ora o quando si verificano particolari tipi di eventi.

tooset di notifiche di posta elettronica per gli avvisi

1. Scegliere dal menu degli avvisi di Backup hello **configurare le notifiche**

    ![Menu Avvisi di backup](./media/backup-azure-monitor-vms/backup-alerts-menu.png)

    Pannello di Hello configura notifiche viene visualizzata.

    ![Pannello Configura notifiche](./media/backup-azure-monitor-vms/configure-notifications.png)
2. Nel Pannello di notifiche Configura hello, per le notifiche di posta elettronica, fare clic su **su**.

    Hello destinatari e le finestre di dialogo di gravità hanno una stella toothem Avanti perché tali informazioni sono necessarie. Specificare almeno un indirizzo di posta elettronica e selezionare almeno un valore per Gravità.
3. In hello **destinatari (posta elettronica)** finestra di dialogo, indirizzi di posta elettronica di tipo hello per che ricevono notifiche hello. Utilizzare il formato hello: username@domainname.com. Separare più indirizzi di posta elettronica con un punto e virgola (;).
4. In hello **notifica** area scegliere **per ogni avviso** toosend notifica quando hello specificato viene generato l'avviso, o **Digest oraria** toosend un riepilogo per hello ora precedente.
5. In hello **gravità** finestra di dialogo, scegliere uno o più livelli che si desidera tootrigger notifica tramite posta elettronica.
6. Fare clic su **Salva**.

   ### <a name="what-alert-types-are-available-for-azure-iaas-vm-backup"></a>Quali tipi di avviso sono disponibili per il backup di VM IaaS di Azure?
   | Livello avviso | Avvisi inviati |
   | --- | --- |
   | Critico |Errore di backup, errore di ripristino |
   | Avviso |None |
   | Informazioni |None |

### <a name="are-there-situations-where-email-isnt-sent-even-if-notifications-are-configured"></a>Esistono situazioni in cui il messaggio e-mail non viene inviato anche se sono configurate le notifiche?
Ci sono casi in cui non viene inviato un avviso, anche se le notifiche di hello sono state configurate correttamente. Hello notifiche di posta elettronica situazioni seguenti non vengono inviate tooavoid frequenza degli avvisi:

* Se le notifiche sono configurate tooHourly Digest e un avviso viene generato e risolto entro ora hello.
* Hello processi vengono annullati.
* Viene attivato un processo di backup che non riesce ed è in corso un altro processo di backup.
* Avvia un processo di backup pianificato per una macchina virtuale abilitata alla gestione delle risorse, ma hello VM non esiste più.

## <a name="customize-your-view-of-events"></a>Personalizzare la visualizzazione degli eventi
Hello **log di controllo** impostazione include un set predefinito di filtri e colonne contenenti informazioni sugli eventi operativi. È possibile personalizzare la visualizzazione hello in modo che quando hello **eventi** pannello viene aperto, viene visualizzata hello informazioni desiderate.

1. In hello [dashboard dell'insieme di credenziali](backup-azure-manage-vms.md#open-a-recovery-services-vault-in-the-dashboard), fare clic su tooand Sfoglia **i log di controllo** tooopen hello **eventi** blade.

    ![Log di controllo](./media/backup-azure-monitor-vms/audit-logs-1606-1.png)

    Hello **eventi** pannello apre gli eventi operativi di toohello filtrati solo per l'insieme di credenziali hello corrente.

    ![Filtro di Log di controllo](./media/backup-azure-monitor-vms/audit-logs-filter.png)

    Pannello Hello Mostra elenco hello di critico, errore, avviso e informativi che si sono verificati in hello settimana precedente. intervallo di tempo Hello è un valore predefinito impostato in hello **filtro**. Hello **eventi** pannello mostra anche la registrazione quando si sono verificati eventi hello un grafico a barre. Se non si desidera toosee hello grafico a barre, hello **eventi** menu, fare clic su **Nascondi grafico** tootoggle off grafico hello. Hello predefinito di eventi visualizza le informazioni di operazione, livello, stato, risorse e ora. Per informazioni sull'esposizione ulteriori attributi dell'evento, vedere la sezione hello [espansione informazioni sull'evento](backup-azure-monitor-vms.md#view-additional-event-attributes).
2. Per ulteriori informazioni su un evento operativo, in hello **operazione** colonna, fare clic su un tooopen eventi operativi relativo pannello. Pannello Hello contiene informazioni dettagliate sugli eventi hello. Gli eventi vengono raggruppati per il loro ID di correlazione e un elenco di eventi di hello che si sono verificati nell'intervallo di tempo hello.

    ![Dettagli operazione](./media/backup-azure-monitor-vms/audit-logs-details-window.png)
3. tooview informazioni dettagliate su un determinato evento, dall'elenco di hello degli eventi, fare clic su hello evento tooopen relativo **dettagli** blade.

    ![Dettagli dell'evento](./media/backup-azure-monitor-vms/audit-logs-details-window-deep.png)

    informazioni a livello di evento Hello sono come hello Ottiene informazioni dettagliate. Se si desidera visualizzare questo quantità di informazioni relative a ogni evento e si desidera tooadd questo dettaglio molto toohello **eventi** pannello, vedere la sezione hello [espansione informazioni sull'evento](backup-azure-monitor-vms.md#view-additional-event-attributes).

## <a name="customize-hello-event-filter"></a>Personalizzare il filtro di eventi hello
Hello utilizzare **filtro** tooadjust o scegliere le informazioni di hello che viene visualizzato in un pannello specifico. informazioni sull'evento toofilter hello:

1. In hello [dashboard dell'insieme di credenziali](backup-azure-manage-vms.md#open-a-recovery-services-vault-in-the-dashboard), fare clic su tooand Sfoglia **i log di controllo** tooopen hello **eventi** blade.

    ![Log di controllo](./media/backup-azure-monitor-vms/audit-logs-1606-1.png)

    Hello **eventi** pannello apre gli eventi operativi di toohello filtrati solo per l'insieme di credenziali hello corrente.

    ![Filtro di Log di controllo](./media/backup-azure-monitor-vms/audit-logs-filter.png)
2. In hello **eventi** menu, fare clic su **filtro** tooopen tale pannello.

    ![Aprire il pannello del filtro](./media/backup-azure-monitor-vms/audit-logs-filter-button.png)
3. In hello **filtro** pannello regolare hello **livello**, **intervallo di tempo**, e **chiamante** filtri. Hello altri filtri non sono disponibili poiché le informazioni correnti di hello tooprovide fossero impostati per l'insieme di credenziali di servizi di ripristino hello.

    ![Dettagli della query sui Log di controllo](./media/backup-azure-monitor-vms/filter-blade.png)

    È possibile specificare hello **livello** dell'evento: critico, errore, avviso o informativo. È possibile scegliere qualsiasi combinazione di livelli dell'evento, ma è necessario avere selezionato almeno un livello. Attiva o disattiva hello livello o disattivare. Hello **intervallo di tempo** filtro consente di toospecify hello durata per l'acquisizione degli eventi. Se si utilizza un intervallo di tempo personalizzato, è possibile impostare l'avvio di hello e ora di fine.
4. Una volta pronto tooquery hello operazioni log utilizzando il filtro, fare clic su **aggiornamento**. visualizzano i risultati di Hello in hello **eventi** blade.

    ![Dettagli operazione](./media/backup-azure-monitor-vms/edited-list-of-events.png)

### <a name="view-additional-event-attributes"></a>Visualizzare altri attributi degli eventi
Utilizzando hello **colonne** pulsante, è possibile abilitare eventi ulteriori attributi tooappear nell'elenco hello hello **eventi** blade. elenco predefinito di Hello di eventi visualizza le informazioni per l'operazione, livello, stato, risorse e ora. tooenable attributi aggiuntivi:

1. In hello **eventi** pannello, fare clic su **colonne**.

    ![Aprire le colonne](./media/backup-azure-monitor-vms/audi-logs-column-button.png)

    Hello **scegliere le colonne** apre blade.

    ![Pannello delle colonne](./media/backup-azure-monitor-vms/columns-blade.png)
2. hello tooselect attributo, fare clic sulla casella di controllo hello. casella di controllo di Hello attributo attiva o disattiva.
3. Fare clic su **reimpostare** tooreset hello elenco di attributi hello **eventi** blade. Dopo l'aggiunta o rimozione di attributi dall'elenco di hello, utilizzare **reimpostare** tooview hello nuovo elenco di attributi evento.
4. Fare clic su **aggiornamento** dati hello tooupdate negli attributi evento hello. Hello nella tabella seguente fornisce informazioni su ogni attributo.

| Nome colonna | Descrizione |
| --- | --- |
| Operazione |nome Hello dell'operazione di hello |
| Level |Salve a livello di operazione hello, i possibili valori sono: informativo, avviso, errore o critico |
| Stato |Descrittivo dello stato dell'operazione hello |
| Risorsa |URL che identifica la risorsa hello. noto anche come ID di risorsa hello |
| Tempo |Tempo, misurato dal hello ora corrente, in cui si è verificato l'evento hello |
| Chiamante |Chi o cosa chiamato o attivato l'evento hello. può essere sistema hello o un utente |
| Timestamp |ora di Hello evento hello stato attivazione |
| Gruppo di risorse |gruppo di risorse associato Hello |
| Tipo di risorsa |tipo di risorsa interno Hello usato da Gestione risorse |
| ID sottoscrizione |Hello associato all'ID di sottoscrizione |
| Categoria |Categoria di eventi hello |
| ID correlazione |ID comune per gli eventi correlati. |

## <a name="use-powershell-toocustomize-alerts"></a>Utilizzare PowerShell toocustomize avvisi
È possibile ottenere le notifiche di avviso personalizzate per i processi di hello nel portale di hello. Questi processi, tooget definire avviso basata su PowerShell regole hello operativo registra gli eventi. Usare *PowerShell versione 1.3.0 o successiva*.

toodefine tooalert una notifica personalizzata per gli errori di backup, usare un comando simile hello lo script seguente:

```
PS C:\> $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail contoso@microsoft.com
PS C:\> Add-AzureRmLogAlertRule -Name backupFailedAlert -Location "East US" -ResourceGroup RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US -OperationName Microsoft.RecoveryServices/recoveryServicesVault/Backup -Status Failed -TargetResourceId /subscriptions/86eeac34-eth9a-4de3-84db-7a27d121967e/resourceGroups/RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US/providers/Microsoft.RecoveryServices/vaults/trinadhVault -Actions $actionEmail
```

**ResourceId** : È possibile ottenere ResourceId da hello i log di controllo. Hello ResourceId è un URL fornito nella colonna risorsa hello del log delle operazioni hello.

**OperationName** : OperationName è nel formato hello "Microsoft.RecoveryServices/recoveryServicesVault/*EventName*" in cui *EventName* può essere:<br/>

* Registra <br/>
* Unregister  <br/>
* ConfigureProtection  <br/>
* Backup  <br/>
* Restore  <br/>
* StopProtection  <br/>
* DeleteBackupData  <br/>
* CreateProtectionPolicy  <br/>
* DeleteProtectionPolicy  <br/>
* UpdateProtectionPolicy  <br/>

**Status** : i valori supportati sono Started, Succeeded o Failed.

**Gruppo di risorse** : si tratta di hello appartiene toowhich hello risorsa gruppo di risorse. È possibile aggiungere hello gruppo di risorse colonna toohello generato log. Gruppo di risorse è uno dei tipi di informazioni sugli eventi disponibili hello.

**Nome** : nome della regola di avviso hello.

**CustomEmail** : specificare toowhich indirizzo di posta elettronica personalizzati hello desiderato toosend una notifica di avviso

**SendToServiceOwners** : questa opzione consente di inviare amministratori tooall notifiche di avviso e i coamministratori della sottoscrizione hello. Può essere usata nel cmdlet **New AzureRmAlertRuleEmail** .

### <a name="limitations-on-alerts"></a>Limitazioni per gli avvisi
Avvisi basati su eventi sono soggetto toohello limitazioni seguenti:

1. Gli avvisi vengono attivati in tutte le macchine virtuali in hello che insieme di credenziali di servizi di ripristino. Non è possibile personalizzare l'avviso hello per un sottoinsieme di macchine virtuali in un insieme di credenziali di servizi di ripristino.
2. Questa funzionalità è in anteprima. [Altre informazioni](../monitoring-and-diagnostics/insights-powershell-samples.md#create-metric-alerts)
3. Gli avvisi vengono inviati da "alerts-noreply@mail.windowsazure.com". Attualmente non è possibile modificare il mittente di posta elettronica hello.

## <a name="next-steps"></a>Passaggi successivi
I registri eventi abilitare grande finale e il supporto per operazioni di backup hello di controllo. viene registrato Hello seguenti operazioni:

* Registra
* Unregister 
* Configura protezione
* Backup (sia backup pianificato che su richiesta )
* Restore 
* Arresta protezione
* Elimina dati di backup
* Aggiungi criteri
* Elimina criteri
* Aggiorna criteri
* Annulla processo

Per una spiegazione di eventi, le operazioni e i log di controllo tra hello ampia servizi di Azure, vedere l'articolo hello [visualizzare eventi e log di controllo](../monitoring-and-diagnostics/insights-debugging-with-events.md).

Per informazioni su come ricreare una macchina virtuale da un punto di ripristino, vedere [Ripristinare macchine virtuali in Azure](backup-azure-restore-vms.md). Per ulteriori informazioni sulla protezione di macchine virtuali, vedere [innanzitutto: eseguire il backup di macchine virtuali tooa insieme di credenziali di servizi di ripristino](backup-azure-vms-first-look-arm.md). Informazioni sulle attività di gestione di hello per i backup VM in articolo hello [backup di macchine virtuali di Azure gestire](backup-azure-manage-vms.md).
