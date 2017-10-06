---
title: "aaaOverview di hello Log attività di Azure | Documenti Microsoft"
description: "Informazioni su quali hello è Log attività di Azure e come è possibile usarlo toounderstand eventi che si verificano nella sottoscrizione di Azure."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: c274782f-039d-4c28-9ddb-f89ce21052c7
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: johnkem
ms.openlocfilehash: cba79b7f6dc0833ef588382e763761fd77d43307
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-subscription-activity-with-hello-azure-activity-log"></a>Monitorare l'attività di sottoscrizione con hello Log attività di Azure
Hello **Log attività Azure** è un log di sottoscrizione che consente di comprendere gli eventi a livello di sottoscrizione che si sono verificati in Azure. Sono inclusi un intervallo di dati, da Gestione risorse di Azure sui dati operativi tooupdates sugli eventi di integrità del servizio. Log attività Hello era noto in precedenza come "Registri di controllo" o "I registri operativi", poiché hello categoria amministrativa report Pannello di controllo degli eventi per le sottoscrizioni. Hello registro attività, consentono di determinare hello ' cosa, chi e quando ' per le operazioni (PUT, POST, DELETE) eseguite su risorse hello nella sottoscrizione di scrittura. È anche possibile comprendere lo stato di hello dell'operazione di hello e altre proprietà pertinenti. Log attività Hello non include operazioni di lettura (GET) o per le risorse che utilizzano hello Classic / modello "RDFE".

![Log attività o altri tipi di log ](./media/monitoring-overview-activity-logs/Activity_Log_vs_other_logs_v5.png)

Figura 1: Log attività o altri tipi di log

Hello Log attività è diverso da [i log di diagnostica](monitoring-overview-of-diagnostic-logs.md). Log attività forniscono dati relativi alle operazioni di hello su una risorsa da hello esterno (Buongiorno "piano di controllo"). I log di diagnostica vengono emessi da una risorsa e forniscono informazioni sull'operazione di hello di tale risorsa (Buongiorno "piano di dati").

È possibile recuperare gli eventi dal registro attività utilizzando hello portale di Azure CLI, i cmdlet di PowerShell e API REST di monitoraggio di Azure.


> [!WARNING]
> Hello Log attività di Azure viene utilizzata principalmente per le attività che si verificano in Gestione risorse di Azure. Non rileva le risorse utilizzando hello Classic/RDFE modello. Alcuni tipi di risorse classiche dispongono di un provider di risorse proxy in Azure Resource Manager (ad esempio, Microsoft.ClassicCompute). Se si interagisce con un tipo di risorsa classica tramite Azure Resource Manager utilizzando questi provider di risorse di proxy, operazioni hello visualizzati nel Log attività hello. Se si interagisce con una risorsa classica digitare nel portale classico hello o in caso contrario all'esterno di proxy di gestione risorse di Azure hello, le azioni vengono registrate solo in hello Log operazioni. Hello Log operazioni è accessibile solo nel portale classico di hello.
>
>

Hello visualizzazione seguente hello introduzione video Log attività.
> [!VIDEO https://channel9.msdn.com/Blogs/Seth-Juarez/Logs-John-Kemnetz/player]
> 
>

## <a name="categories-in-hello-activity-log"></a>Categorie di hello Log attività
Log attività Hello contiene diverse categorie di dati. Per informazioni dettagliate su schemi hello di queste categorie, [, vedere l'articolo](monitoring-activity-log-schema.md). incluse le seguenti:
* **Amministrazione** -questa categoria include i record di hello di tutti create, update, delete e azione di operazioni eseguite tramite Gestione risorse. Esempi di tipi di eventi visualizzati in questa categoria includono hello "Crea macchina virtuale" e "gruppo di sicurezza di rete delete" ogni azione eseguita da un utente o applicazione usando Gestione risorse viene modellato come un'operazione su un determinato tipo di risorsa. Se il tipo di operazione hello è scrivere, Delete o azione, i record di hello inizio hello sia esito positivo o esito negativo dell'operazione vengono registrati nella categoria amministrativa hello. categoria amministrativa Hello include anche qualsiasi controllo di accesso basato su toorole modifiche in una sottoscrizione.
* **Stato servizio** -questa categoria include i record di hello di eventuali problemi di integrità servizio che si sono verificati in Azure. Un esempio di hello tipo di evento che verrà visualizzato in questa categoria è "SQL Azure negli Stati Uniti orientali si è verificati i tempi di inattività". Eventi di integrità del servizio sono disponibili in cinque tipi: azione richiesta, del recupero assistito, evento imprevisto, manutenzione, informazioni o sicurezza e vengono visualizzate solo se si dispone di una risorsa nella sottoscrizione hello che potrebbe essere interessata dall'evento hello.
* **Avviso** -questa categoria include i record di hello di tutte le attivazioni di avvisi di Azure. Un esempio di hello tipo di evento che verrà visualizzato in questa categoria è "% della CPU nella macchina virtuale myVM è stato superato l'80 per hello negli ultimi 5 minuti." In diversi sistemi Azure il concetto di avviso prevede la possibilità di definire una regola di qualche tipo e di ricevere una notifica quando le condizioni corrispondono a tale regola. Ogni volta che un tipo di avviso Azure supportato 'attiva,' o condizioni hello sono soddisfatto toogenerate una notifica, un record di attivazione hello viene inoltre inserito toothis categoria di hello Log attività.
* **Scalabilità automatica** -questa categoria include i record di hello di qualsiasi operazione toohello correlati gli eventi del motore di scalabilità automatica hello in base alle impostazioni di scalabilità automatica è stato definito nella sottoscrizione. Un esempio di hello tipo di evento che verrà visualizzato in questa categoria è "Scalabilità automatica scalabilità verticale azione non riuscita". Utilizza la scalabilità automatica, è possibile automaticamente scalare in orizzontale o ridimensionare in hello numero di istanze in un tipo di risorsa supportati è basato sull'ora del giorno e/o caricamento dati (metrici) utilizzando un'impostazione di scalabilità automatica. Quando vengono soddisfatte le condizioni di hello tooscale verso l'alto o verso il basso, inizio hello e gli eventi di riuscite o non riusciti vengono registrati in questa categoria.
* **Consiglio**: questa categoria include gli eventi di raccomandazione da determinati tipi di risorse, ad esempio siti web e server SQL. Questi eventi forniti consigli per la modalità toobetter utilizzano le risorse. Gli eventi di questo tipo si verificano solo se si hanno risorse che generano consigli.
* **Criterio, sicurezza e integrità delle risorse**: queste categorie non contengono eventi, ma sono riservate per usi futuri.

## <a name="event-schema-per-category"></a>Schema di eventi per categoria
[Vedere questo schema di eventi articolo toounderstand hello Log attività per categoria.](monitoring-activity-log-schema.md)

## <a name="what-you-can-do-with-hello-activity-log"></a>Operazioni eseguibili con hello Log attività
Ecco alcune delle operazioni di hello che è possibile eseguire con hello Log attività:

![Log attività di Azure](./media/monitoring-overview-activity-logs/Activity_Log_Overview_v3.png)


* Eseguire una query e visualizzarlo in hello **portale di Azure**.
* [Creare un avviso per un evento del log attività](monitoring-activity-log-alerts.md)
* [Flusso di tooan **Hub eventi** ](monitoring-stream-activity-logs-event-hubs.md) per l'inserimento di un servizio di terze parti o di una soluzione analitica personalizzato, ad esempio Power BI.
* Analizzare in Power BI usando hello [ **pacchetto di contenuto Power BI**](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs/).
* [Salvarlo tooa **Account di archiviazione** per l'ispezione dell'archivio o manuale](monitoring-archive-activity-log.md). È possibile specificare hello memorizzazione tempo (in giorni) utilizzando hello **profilo Log**.
* Eseguire query tramite l'API REST, i cmdlet di PowerShell o l'interfaccia della riga di comando.

## <a name="query-hello-activity-log-in-hello-azure-portal"></a>Ciao query Log attività hello portale di Azure
All'interno di hello portale di Azure è possibile visualizzare il Log di attività in diverse posizioni:
* Hello **pannello Log attività**, che è possibile accedere eseguendo una ricerca di hello registro attività "Più servizi" nel riquadro di navigazione a sinistra di hello.
* Hello **pannello monitoraggio**, che viene visualizzato per impostazione predefinita nel riquadro di navigazione a sinistra di hello. Log attività Hello è una sezione di questo pannello monitoraggio di Azure.
* Qualsiasi risorsa **pannello della risorsa**, ad esempio, il pannello di configurazione hello per una macchina virtuale. Log attività Hello è sia una delle sezioni hello nella maggior parte dei pannelli risorse, e facendo clic su di esso automaticamente Filtra gli eventi di hello toothose correlati toothat di risorse.

Nel portale di Azure hello, è possibile filtrare il registro attività per questi campi:
* TimeSpan - hello iniziale e finale di tempo per gli eventi.
* Categoria - categoria di eventi hello come descritto in precedenza.
* Sottoscrizione: uno o più nomi di sottoscrizione di Azure.
* Gruppo di risorse: uno o più gruppi di risorse in tali sottoscrizioni.
* Risorsa (nome) - nome hello di una risorsa specifica.
* Tipo di risorsa - tipo hello di risorsa, ad esempio, Microsoft.Compute/virtualmachines.
* Nome dell'operazione - nome hello di un'operazione di gestione risorse di Azure, ad esempio, Microsoft.SQL/servers/Write.
* Gravità - livello di gravità hello dell'evento hello (informativo, avviso, errore critico).
* Evento avviato da - chiamante"hello", o l'utente che ha eseguito l'operazione di hello.
* Apri ricerca: casella di ricerca di testo aperta che cerca tale stringa in tutti i campi di tutti gli eventi.

Dopo aver definito un set di filtri, è possibile salvarlo come una query che viene mantenuta tra le sessioni se avrai bisogno di tooperform hello stessa query con i filtri applicati nuovamente in futuro hello. È anche possibile aggiungere keep query tooyour dashboard di Azure tooalways d'occhio su eventi specifici.

Fare clic su "Applica" per eseguire la query e visualizzare tutti gli eventi corrispondenti. Facendo clic su qualsiasi evento nel Mostra elenco hello hello riepilogo dell'evento nonché hello raw completa JSON dell'evento in questione.

Per una potenza ancora maggiore, è possibile fare clic su hello **ricerca nei Log** icona, che visualizza i dati dei Log di attività in hello [soluzione Analitica di Log attività Analitica Log](../log-analytics/log-analytics-activity.md). Pannello Log attività Hello offre un'esperienza di operazioni di filtro/visualizzazione nel log, ma consente di Log Analitica è toopivot, eseguire una query e visualizzare i dati in modo più efficiente.

## <a name="export-hello-activity-log-with-a-log-profile"></a>Esportazione hello Log attività con un profilo di Log
Un **profilo di log** controlla la modalità di esportazione del log attività. Un profilo di log permette di configurare quanto segue:

* Dove hello Log attività deve essere inviato (Account di archiviazione o hub eventi)
* Categorie di eventi da inviare (scrittura, eliminazione o azione). *il significato di Hello di "categoria" nei profili di registro e gli eventi del registro attività è diverso. Nel profilo Log hello, "Categoria" rappresenta il tipo di operazione hello (azione di scrittura, eliminazione). In un evento di registro attività, proprietà di "categoria" hello rappresenta origine hello o un tipo di evento (ad esempio, amministrazione, ServiceHealth, avviso e informazioni).*
* Aree o località da esportare. Rendere tooinclude che "globali", molti eventi nel registro attività hello sono globali.
* Quanto tempo hello Log attività deve essere mantenuto in un Account di archiviazione.
    - Un periodo di conservazione di zero giorni significa che i log vengono conservati all'infinito. In caso contrario, il valore di hello può essere qualsiasi numero di giorni compreso tra 1 e 2147483647.
    - Se i criteri di conservazione sono impostati, ma l'archiviazione dei log in un Account di archiviazione è disabilitata (ad esempio, se solo le opzioni di hub eventi o OMS sono selezionate), i criteri di conservazione hello non hanno alcun effetto.
    - Criteri di conservazione vengono applicati al giorno, vengono eliminati in modo a hello fine di un giorno (UTC), i log da giorno hello che si trova ora oltre i criteri di conservazione hello. Ad esempio, se si dispone di un criterio di conservazione di un giorno, all'inizio di hello del giorno hello oggi hello registri hello ieri dovrebbero essere eliminati.

È possibile utilizzare un account di archiviazione o spazio dei nomi hub di eventi che non si trova in hello stessa sottoscrizione come hello una creazione di log. utente di Hello che configura l'impostazione di hello deve disporre di sottoscrizioni di hello appropriate RBAC accesso tooboth.

Queste impostazioni possono essere configurate tramite l'opzione "Esporta" hello nel pannello Log attività hello nel portale di hello. Possono anche essere configurate a livello di programmazione [utilizzando hello API REST di Azure monitoraggio](https://msdn.microsoft.com/library/azure/dn931927.aspx), i cmdlet di PowerShell o CLI. Una sottoscrizione può avere un solo profilo di log.

### <a name="configure-log-profiles-using-hello-azure-portal"></a>Configurare i profili di log utilizzando hello portale di Azure
È possibile trasmettere hello Log attività tooan Hub eventi o archiviarli in un Account di archiviazione utilizzando l'opzione "Esporta" hello in hello portale di Azure.

1. Passare toohello **Log attività** pannello utilizzando il menu di hello hello il lato sinistro di portale hello.

    ![Passare tooActivity Log nel portale](./media/monitoring-overview-activity-logs/activity-logs-portal-navigate.png)
2. Fare clic su hello **esportare** pulsante nella parte superiore di hello del pannello hello.

    ![Pulsante Esporta nel portale](./media/monitoring-overview-activity-logs/activity-logs-portal-export.png)
3. Nel pannello hello che viene visualizzata, è possibile selezionare:  
  * aree per cui si desidera tooexport eventi
  * Hello toowhich Account di archiviazione desiderato toosave eventi
  * numero di Hello di giorni che si desidera tooretain questi eventi nel servizio di archiviazione. Un'impostazione di 0 giorni conserva per sempre registri hello.
  * Hello Service Bus Namespace nel quale si desidera toobe un Hub eventi creato per lo streaming di questi eventi.

     ![Pannello Esporta log di controllo](./media/monitoring-overview-activity-logs/activity-logs-portal-export-blade.png)
4. Fare clic su **salvare** toosave queste impostazioni. le impostazioni di Hello sono immediatamente di essere applicati tooyour sottoscrizione.

### <a name="configure-log-profiles-using-hello-azure-powershell-cmdlets"></a>Configurare i profili di log utilizzando hello cmdlet PowerShell di Azure
#### <a name="get-existing-log-profile"></a>Ottenere un profilo di log esistente
```
Get-AzureRmLogProfile
```

#### <a name="add-a-log-profile"></a>Aggiungere un profilo di log
```
Add-AzureRmLogProfile -Name my_log_profile -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus -RetentionInDays 90 -Categories Write,Delete,Action
```

| Proprietà | Obbligatorio | Description |
| --- | --- | --- |
| Name |Sì |Nome del profilo di log. |
| StorageAccountId |No |ID di risorsa di hello toowhich tramite Account di archiviazione hello Log attività deve essere salvato. |
| serviceBusRuleId |No |ID regola Bus di servizio per spazio dei nomi Service Bus hello sarebbe hub di eventi toohave creato in. Si tratta di una stringa nel formato seguente: `{service bus resource ID}/authorizationrules/{key name}`. |
| Località |Sì |Elenco delimitato da virgole delle aree per cui si desidera toocollect attività registra eventi. |
| RetentionInDays |Sì |Numero di giorni per cui gli eventi devono essere mantenuti, compreso tra 1 e 2147483647. Un valore pari a zero vengono archiviati i log di hello illimitata (sempre). |
| Categorie |No |Elenco delimitato da virgole di categorie di eventi che devono essere raccolti. I valori possibili sono Write, Delete e Action. |

#### <a name="remove-a-log-profile"></a>Rimozione di un profilo di log
```
Remove-AzureRmLogProfile -name my_log_profile
```

### <a name="configure-log-profiles-using-hello-azure-cross-platform-cli"></a>Configurare i profili di log tramite hello CLI multipiattaforma di Azure
#### <a name="get-existing-log-profile"></a>Ottenere un profilo di log esistente
```
azure insights logprofile list
```
```
azure insights logprofile get --name my_log_profile
```
Hello `name` della proprietà deve essere il nome di hello del profilo di log.

#### <a name="add-a-log-profile"></a>Aggiungere un profilo di log
```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope --retentionInDays 90 –categories Write,Delete,Action
```

| Proprietà | Obbligatorio | Description |
| --- | --- | --- |
| name |Sì |Nome del profilo di log. |
| storageId |No |ID di risorsa di hello toowhich tramite Account di archiviazione hello Log attività deve essere salvato. |
| serviceBusRuleId |No |ID regola Bus di servizio per spazio dei nomi Service Bus hello sarebbe hub di eventi toohave creato in. Si tratta di una stringa nel formato seguente: `{service bus resource ID}/authorizationrules/{key name}`. |
| locations |Sì |Elenco delimitato da virgole delle aree per cui si desidera toocollect attività registra eventi. |
| RetentionInDays |Sì |Numero di giorni per cui gli eventi devono essere mantenuti, compreso tra 1 e 2147483647. Un valore pari a zero vengono archiviati i log di hello illimitata (sempre). |
| Categorie |No |Elenco delimitato da virgole di categorie di eventi che devono essere raccolti. I valori possibili sono Write, Delete e Action. |

#### <a name="remove-a-log-profile"></a>Rimozione di un profilo di log
```
azure insights logprofile delete --name my_log_profile
```

## <a name="next-steps"></a>Passaggi successivi
* [Altre informazioni su hello Log attività (in precedenza i log di controllo)](../azure-resource-manager/resource-group-audit.md)
* [Flusso hello Log attività Azure tooEvent hub](monitoring-stream-activity-logs-event-hubs.md)
