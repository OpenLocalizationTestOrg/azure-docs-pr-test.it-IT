---
title: "Servizio di sincronizzazione Azure AD Connect: utilità di pianificazione | Documentazione Microsoft"
description: "In questo argomento vengono descritte funzionalità hello predefinite dell'utilità di pianificazione di sincronizzazione di Azure AD Connect."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 6b1a598f-89c0-4244-9b20-f4aaad5233cf
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: c587039cc68d305862a07beff364894b6f74cd2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-scheduler"></a>Servizio di sincronizzazione Azure AD Connect: utilità di pianificazione
In questo argomento descrive hello predefinite dell'utilità di pianificazione della sincronizzazione di Azure AD Connect (anche noto come motore di sincronizzazione.

Questa funzionalità è stata introdotta nella build 1.1.105.0 rilasciata nel mese di febbraio 2016.

## <a name="overview"></a>Panoramica
Il servizio di sincronizzazione Azure AD Connect sincronizza le modifiche rilevate nella directory locale usando un'utilità di pianificazione. Sono disponibili due processi dell'utilità di pianificazione, uno per la sincronizzazione delle password e uno per la sincronizzazione di oggetti/attributi e per le attività di manutenzione. Questo argomento illustra hello quest'ultimo.

Nelle versioni precedenti, utilità di pianificazione di hello per oggetti e gli attributi è il motore di sincronizzazione toohello esterno. Consente di utilità di pianificazione di Windows o un processo di sincronizzazione hello separato del tootrigger servizio Windows. utilità di pianificazione Hello è con hello motore di sincronizzazione predefinite toohello versioni 1.1 e consentire alcune personalizzazioni. frequenza di sincronizzazione Hello nuovo valore predefinito è 30 minuti.

utilità di pianificazione Hello è responsabile di due attività:

* **Ciclo di sincronizzazione**. Hello processo tooimport, sincronizzazione e le modifiche di esportazione.
* **Attività di manutenzione**. rinnovo di chiavi e certificati per la reimpostazione delle password e per il servizio Registrazione dispositivo. Eliminare le voci precedenti nel log operazioni hello.

utilità di pianificazione di Hello stesso è sempre in esecuzione, ma può essere configurato tooonly eseguire una o nessuna di queste attività. Ad esempio, se è necessario toohave proprio processo del ciclo di sincronizzazione, è possibile disabilitare questa attività nell'utilità di pianificazione hello ma l'attività di manutenzione hello ancora esecuzione.

## <a name="scheduler-configuration"></a>Configurazione dell'utilità di pianificazione
toosee le impostazioni di configurazione correnti, passare tooPowerShell ed eseguire `Get-ADSyncScheduler`. Il risultato visualizzato è simile al seguente:

![GetSyncScheduler](./media/active-directory-aadconnectsync-feature-scheduler/getsynccyclesettings2016.png)

Se viene visualizzato **comando Sincronizza hello o un cmdlet non è disponibile** quando si esegue questo cmdlet, quindi hello modulo di PowerShell non è caricato. Questo problema può verificarsi se si esegue Azure AD Connect in un controller di dominio o in un server con i livelli di restrizione di PowerShell più elevati rispetto a impostazioni predefinite di hello. Se viene visualizzato questo errore, quindi eseguire `Import-Module ADSync` toomake hello cmdlet disponibili.

* **AllowedSyncCycleInterval**. Hello più breve intervallo di tempo tra i cicli di sincronizzazione consentito da Azure AD. La sincronizzazione con una frequenza superiore a quella di questa impostazione non è supportata.
* **CurrentlyEffectiveSyncCycleInterval**. Hello pianificazione attualmente attivo. Ha lo stesso valore CustomizedSyncInterval hello (se impostato) se non è più frequente AllowedSyncInterval. Se si usa una build precedente alla 1.1.281 e si modifica il valore di CustomizedSyncCycleInterval, la modifica viene applicata dopo il ciclo di sincronizzazione successivo. Da compilazione 1.1.281 hello modifica ha effetto immediato.
* **CustomizedSyncCycleInterval**. Se si desidera hello dell'utilità di pianificazione toorun a qualsiasi altra frequenza rispetto al valore predefinito di hello 30 minuti, si configura questa impostazione. Nella figura hello precedente, utilità di pianificazione hello è stata impostata toorun ogni ora invece. Se si imposta questo valore di impostazione tooa inferiore AllowedSyncInterval, hello quest'ultimo viene utilizzato.
* **NextSyncCyclePolicyType**. differenziale o iniziale. Definisce se hello prossima esecuzione deve solo le modifiche delta di processo, o se hello prossima esecuzione deve eseguire una procedura completa di importare e sincronizzare. Hello quest'ultimo potrebbe inoltre rielaborare regole nuove o modificate.
* **NextSyncCycleStartTimeInUTC**. Successivo avvio dell'utilità di pianificazione di hello hello successivo ciclo di sincronizzazione.
* **PurgeRunHistoryInterval**. Hello operazione ora devono essere conservati i log. Questi registri possono essere esaminati in Gestione servizio di sincronizzazione hello. Hello predefinito è tookeep questi registri per 7 giorni.
* **SyncCycleEnabled**. Indica se dell'utilità di pianificazione di hello è in esecuzione processi di esportazione, sincronizzazione e importazione hello come parte dell'operazione del.
* **MaintenanceEnabled**. Indica se il processo di manutenzione hello è abilitato. Aggiorna i certificati o chiavi hello ed Elimina hello log operazioni.
* **StagingModeEnabled**. Indica se la [modalità di gestione temporanea](active-directory-aadconnectsync-operations.md#staging-mode) è abilitata. Se questa impostazione è abilitata, esso Elimina esportazioni hello esecuzione ma comunque eseguire l'importazione e la sincronizzazione.
* **SchedulerSuspended**. L'impostazione Connetti un'utilità di pianificazione aggiornamento tootemporarily hello blocco durante l'esecuzione.

Alcune di queste impostazioni possono essere modificate con `Set-ADSyncScheduler`. è possibile modificare Hello seguenti parametri:

* CustomizedSyncCycleInterval
* NextSyncCyclePolicyType
* PurgeRunHistoryInterval
* SyncCycleEnabled
* MaintenanceEnabled

Nelle versioni precedenti di Azure AD Connect, **isStagingModeEnabled** era esposto in Set-ADSyncScheduler. È **non supportato** tooset questa proprietà. proprietà Hello **SchedulerSuspended** deve essere modificata solo da Connect. È **non supportato** tooset con PowerShell direttamente.

configurazione dell'utilità di pianificazione di Hello viene archiviata in Azure AD. Se si dispone di un server di gestione temporanea, qualsiasi modifica nel server primario hello interesserà anche hello server (ad eccezione di IsStagingModeEnabled) di gestione temporanea.

### <a name="customizedsynccycleinterval"></a>CustomizedSyncCycleInterval
Sintassi: `Set-ADSyncScheduler -CustomizedSyncCycleInterval d.HH:mm:ss`  
d - giorni, HH - ore, mm - minuti, ss - secondi

Esempio: `Set-ADSyncScheduler -CustomizedSyncCycleInterval 03:00:00`  
Le modifiche hello toorun dell'utilità di pianificazione ogni 3 ore.

Esempio: `Set-ADSyncScheduler -CustomizedSyncCycleInterval 1.0:0:0`  
Le modifiche hello dell'utilità di pianificazione toorun ogni giorno.

### <a name="disable-hello-scheduler"></a>Disabilitare l'utilità di pianificazione hello  
Se è necessario toomake modifiche di configurazione, si desidera dell'utilità di pianificazione di toodisable hello. Ad esempio, quando si [configurare il filtro](active-directory-aadconnectsync-configure-filtering.md) o [apportare modifiche regole toosynchronization](active-directory-aadconnectsync-change-the-configuration.md).

toodisable hello dell'utilità di pianificazione, eseguire `Set-ADSyncScheduler -SyncCycleEnabled $false`.

![Disabilitare l'utilità di pianificazione hello](./media/active-directory-aadconnectsync-change-the-configuration/schedulerdisable.png)

Quando sono state apportate le modifiche, non dimenticare di utilità di pianificazione hello tooenable con `Set-ADSyncScheduler -SyncCycleEnabled $true`.

## <a name="start-hello-scheduler"></a>Avviare l'utilità di pianificazione hello
utilità di pianificazione Hello è eseguiti ogni 30 minuti per impostazione predefinita. In alcuni casi, potrebbe essere toorun tra hello del ciclo di sincronizzazione pianificato cicli o se è necessario toorun un tipo diverso.

**Ciclo di sincronizzazione differenziale**  
Un ciclo di sincronizzazione delta include hello alla procedura seguente:

* Importazione differenziale su tutti i connettori
* Sincronizzazione differenziale su tutti i connettori
* Esportazione su tutti i connettori

È possibile che si dispone di un urgente modifiche che deve essere sincronizzati immediatamente, è necessario toomanually eseguire un ciclo. Se è necessario toomanually eseguire un ciclo, quindi dall'esecuzione di PowerShell `Start-ADSyncSyncCycle -PolicyType Delta`.

**Ciclo di sincronizzazione completo**  
Se sono state apportate a una delle seguenti modifiche di configurazione hello, è necessario (anche noto come toorun un ciclo di sincronizzazione completa Iniziale:

* Aggiunta di ulteriori toobe di attributi o oggetti importati da una directory di origine
* Modifiche delle regole di sincronizzazione toohello
* Modifica dei [filtri](active-directory-aadconnectsync-configure-filtering.md) in modo che venga incluso un numero diverso di oggetti

Se sono state apportate a una di queste modifiche, è necessario toorun una sincronizzazione completa del ciclo in modo spazi connettore di hello opportunità tooreconsolidate hello è il motore di sincronizzazione hello. Un ciclo di sincronizzazione completa include hello alla procedura seguente:

* Importazione completa su tutti i connettori
* Sincronizzazione completa su tutti i connettori
* Esportazione su tutti i connettori

tooinitiate un ciclo di sincronizzazione completa, eseguire `Start-ADSyncSyncCycle -PolicyType Initial` da un prompt dei comandi di PowerShell. Questo comando avvia un ciclo di sincronizzazione completo.

## <a name="stop-hello-scheduler"></a>Arrestare il pianificatore di hello
Utilità di pianificazione hello è attualmente in esecuzione un ciclo di sincronizzazione, potrebbe essere necessario toostop è. Se si avvia l'installazione guidata di hello e questo errore si verifica ad esempio:

![SyncCycleRunningError](./media/active-directory-aadconnectsync-feature-scheduler/synccyclerunningerror.png)

Quando un ciclo di sincronizzazione è in esecuzione, non è possibile modificare la configurazione. È possibile attendere che l'utilità di pianificazione hello ha completato il processo di hello, ma è anche possibile arrestare, pertanto è possibile apportare le modifiche immediatamente. Arresto hello ciclo corrente non è dannoso e vengono elaborate le modifiche in sospeso e quindi eseguire.

1. Inizio indicando hello toostop di utilità di pianificazione corrente del ciclo con i cmdlet di PowerShell hello `Stop-ADSyncSyncCycle`.
2. Se si usa una compilazione prima di 1.1.281, eseguire l'arresto dell'utilità di pianificazione di hello non arresta hello corrente connettore dalla relativa attività corrente. tooforce hello toostop connettore, richiedere hello seguenti azioni: ![StopAConnector](./media/active-directory-aadconnectsync-feature-scheduler/stopaconnector.png)
   * Avviare **servizio di sincronizzazione** dal menu di avvio hello. Andare troppo**connettori**, evidenziare hello connettore con stato hello **esecuzione**e selezionare **arrestare** da hello azioni.

utilità di pianificazione Hello è ancora attiva e avvia nuovamente nella successiva opportunità.

## <a name="custom-scheduler"></a>Utilità di pianificazione personalizzata
Hello cmdlet documentati in questa sezione sono disponibili solo nella build [1.1.130.0](active-directory-aadconnect-version-history.md#111300) e versioni successive.

Se l'utilità di pianificazione integrata hello non soddisfa i requisiti, è possibile pianificare i connettori di hello con PowerShell.

### <a name="invoke-adsyncrunprofile"></a>Invoke-ADSyncRunProfile
È possibile avviare un profilo per un connettore in questo modo:

```
Invoke-ADSyncRunProfile -ConnectorName "name of connector" -RunProfileName "name of profile"
```

Hello nomi toouse per [i nomi dei connettori](active-directory-aadconnectsync-service-manager-ui-connectors.md) e [i nomi dei profili di esecuzione](active-directory-aadconnectsync-service-manager-ui-connectors.md#configure-run-profiles) è reperibile in hello [UI Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md).

![Richiamare il profilo di esecuzione](./media/active-directory-aadconnectsync-feature-scheduler/invokerunprofile.png)  

Hello `Invoke-ADSyncRunProfile` cmdlet è sincrona, vale a dire non restituisce il controllo fino al completamento operazione hello, hello connettore correttamente o con un errore.

Quando si pianificano i connettori, indicazione hello è tooschedule nel seguente ordine hello:

1. (Completa/differenziale) Importazione da directory locali, ad esempio Active Directory
2. (Completa/differenziale) Importazione da Azure AD
3. (Completa/differenziale) Sincronizzazione da directory locali, ad esempio Active Directory
4. (Completa/differenziale) Sincronizzazione da Azure AD
5. Esportazione tooAzure AD
6. Esportare directory tooon locali, ad esempio Active Directory

Questo ordine è la modalità di esecuzione connettori hello in utilità di pianificazione integrata hello.

### <a name="get-adsyncconnectorrunstatus"></a>Get-ADSyncConnectorRunStatus
È inoltre possibile monitorare toosee motore di sincronizzazione hello se è inattivo o meno. Questo cmdlet restituisce un risultato vuoto se il motore di sincronizzazione hello è inattivo e non è in esecuzione un connettore. Se è in esecuzione un connettore, restituisce il nome di hello di hello connettore.

```
Get-ADSyncConnectorRunStatus
```

![Stato di esecuzione del connettore](./media/active-directory-aadconnectsync-feature-scheduler/getconnectorrunstatus.png)  
Immagine di hello precedente, hello prima riga è da uno stato in cui il motore di sincronizzazione hello è inattivo. seconda riga Hello da quando è in esecuzione hello Azure Active Directory Connector.

## <a name="scheduler-and-installation-wizard"></a>Utilità di pianificazione e installazione guidata
Se si avvia l'installazione guidata di hello, utilità di pianificazione hello è temporaneamente sospeso. Questo comportamento è perché vengono apportate modifiche alla configurazione e non è possibile applicare queste impostazioni se è in esecuzione il motore di sincronizzazione di hello. Per questo motivo, non lasciare installazione guidata di hello aperto poiché si arresta il motore di sincronizzazione hello da eseguire alcuna azione di sincronizzazione.

## <a name="next-steps"></a>Passaggi successivi
Altre informazioni su hello [sincronizzazione di Azure AD Connect](active-directory-aadconnectsync-whatis.md) configurazione.

Altre informazioni su [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).
