---
title: "Panoramica del log attività di Azure | Microsoft Docs"
description: "Informazioni sul log attività di Azure e su come usarlo per comprendere gli eventi che si verificano all'interno della sottoscrizione di Azure."
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
ms.date: 10/17/2017
ms.author: johnkem
ms.openlocfilehash: a101039b59eb1a4a3bcac25162c7f6373283e1b6
ms.sourcegitcommit: fa28ca091317eba4e55cef17766e72475bdd4c96
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="monitor-subscription-activity-with-the-azure-activity-log"></a>Monitorare l'attività di sottoscrizione con il log attività di Azure
Il **log attività di Azure** è un log delle sottoscrizioni che fornisce informazioni approfondite sugli eventi a livello di sottoscrizione che si sono verificati in Azure. Ciò include un intervallo di dati che vanno dai dati operativi di Azure Resource Manager agli aggiornamenti sugli eventi di integrità del servizio. Il log attività era noto in precedenza come "log di controllo" o "log operativo", perché la categoria amministrativa segnala eventi del piano di controllo per le sottoscrizioni. L'uso del log attività permette di acquisire informazioni dettagliate su qualsiasi operazione di scrittura (PUT, POST, DELETE) eseguita sulle risorse nella sottoscrizione. Consente inoltre di comprendere lo stato dell'operazione e altre proprietà specifiche. Il log attività non include le operazioni di lettura (GET) o quelle per le risorse che usano il modello classico/"RDFE".

![Log attività o altri tipi di log ](./media/monitoring-overview-activity-logs/Activity_Log_vs_other_logs_v5.png)

Figura 1: Log attività o altri tipi di log

Il log attività è diverso dal [log di diagnostica](monitoring-overview-of-diagnostic-logs.md). I log attività contengono dati relativi alle operazioni su una risorsa esterna (il "piano di controllo"). I log di diagnostica vengono generati da una risorsa e contengono informazioni sul funzionamento di tale risorsa (il "piano dati").

Per recuperare eventi dal log attività è possibile usare il portale di Azure, l'interfaccia della riga di comando, i cmdlet di PowerShell e l'API REST di Monitoraggio di Azure.


> [!WARNING]
> Il log attività di Azure è destinato principalmente alle attività che si verificano in Azure Resource Manager. Non tiene traccia delle risorse che usano il modello classico/RDFE. Alcuni tipi di risorse classiche dispongono di un provider di risorse proxy in Azure Resource Manager (ad esempio, Microsoft.ClassicCompute). Se un utente interagisce con un tipo di risorsa classica tramite Azure Resource Manager con questi provider di risorse di proxy, le operazioni verranno visualizzate nel log attività. Se si interagisce con un tipo di risorsa all'esterno dei proxy di gestione risorse di Azure classico, le azioni vengono registrate solo nel Log operazioni. È possibile esaminare il log delle operazioni in una sezione distinta del portale.
>
>

Guardare il video seguente di introduzione al log attività.
> [!VIDEO https://channel9.msdn.com/Blogs/Seth-Juarez/Logs-John-Kemnetz/player]
> 
>

## <a name="categories-in-the-activity-log"></a>Categorie nel log attività
Il log attività contiene diverse categorie di dati. Per informazioni dettagliate sugli schemi di queste categorie, [vedere questo articolo](monitoring-activity-log-schema.md). incluse le seguenti:
* **Amministrativa**: questa categoria contiene il record di tutte le operazioni di creazione, aggiornamento, eliminazione e azione eseguite tramite Resource Manager. Tra gli esempi dei tipi di eventi visualizzati in questa categoria sono inclusi "create virtual machine" e "delete network security group". Ogni azione eseguita da un utente o da un'applicazione usando Resource Manager viene modellata come operazione in un determinato tipo di risorsa. Se l'operazione è di tipo scrittura, eliminazione o azione, i record di avvio e riuscita o di non riuscita di tale operazione vengono registrati nella categoria amministrativa. La categoria amministrativa include anche eventuali modifiche al controllo degli accessi in base al ruolo in una sottoscrizione.
* **Integrità del servizio**: questa categoria contiene il record degli eventi imprevisti di integrità del servizio che si sono verificati in Azure. Un esempio del tipo di evento visualizzato in questa categoria è "SQL Azure in East US is experiencing downtime". Gli eventi di integrità del servizio sono di sei tipi: Action Required, Assisted Recovery, Incident, Maintenance, Information o Security, che vengono visualizzati solo se una risorsa della sottoscrizione è interessata dall'evento.
* **Avviso**: questa categoria contiene il record di tutte le attivazioni degli avvisi di Azure. Un esempio del tipo di evento visualizzato in questa categoria è "CPU % on myVM has been over 80 for the past 5 minutes". In diversi sistemi Azure il concetto di avviso prevede la possibilità di definire una regola di qualche tipo e di ricevere una notifica quando le condizioni corrispondono a tale regola. Ogni volta che un tipo di avviso di Azure supportato viene "attivato" o vengono soddisfatte le condizioni per generare una notifica, viene anche eseguito il push di un record dell'attivazione in questa categoria del log attività.
* **Ridimensionamento automatico**: questa categoria contiene il record degli eventi correlati all'operazione del motore di ridimensionamento automatico in base alle impostazioni di scalabilità automatica definite nella sottoscrizione. Un esempio del tipo di evento visualizzato in questa categoria è "Autoscale scale up action failed". Con il ridimensionamento automatico è possibile aumentare o ridurre automaticamente il numero di istanze in un tipo di risorsa supportato in base all'ora del giorno e/o ai dati di caricamento (metrica) usando un'impostazione di ridimensionamento automatico. Quando vengono soddisfatte le condizioni per aumentare o ridurre le prestazioni, gli eventi di avvio riusciti o quelli non riusciti vengono registrati in questa categoria.
* **Consiglio**: questa categoria include gli eventi di raccomandazione da determinati tipi di risorse, ad esempio siti web e server SQL. Questi eventi offrono indicazioni su come usare al meglio le risorse. Gli eventi di questo tipo si verificano solo se si hanno risorse che generano consigli.
* **Sicurezza**: questa categoria contiene il record degli avvisi generati dal Centro sicurezza di Azure. Un esempio del tipo di evento visualizzato in questa categoria è "Suspicious double extension file executed".
* **Criterio e Integrità risorse**: queste categorie non contengono eventi, ma sono riservate per usi futuri.

## <a name="event-schema-per-category"></a>Schema di eventi per categoria
[Vedere questo articolo per comprendere lo schema di eventi del log attività per categoria.](monitoring-activity-log-schema.md)

## <a name="what-you-can-do-with-the-activity-log"></a>Che cosa si può fare con il log attività
Ecco alcune delle attività che è possibile eseguire con il log attività:

![Log attività di Azure](./media/monitoring-overview-activity-logs/Activity_Log_Overview_v3.png)


* Eseguire query e visualizzarlo nel **portale di Azure**.
* [Creare un avviso per un evento del log attività](monitoring-activity-log-alerts.md)
* [Trasmetterlo a un **hub eventi**](monitoring-stream-activity-logs-event-hubs.md) per l'inserimento da parte di un servizio di terze parti o di una soluzione di analisi personalizzata come Power BI.
* Analizzarlo in Power BI usando il [**pacchetto di contenuto di Power BI**](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs/).
* [Salvarlo in un **account di archiviazione** per fini di archiviazione o di ispezione manuale](monitoring-archive-activity-log.md). È possibile specificare il tempo di conservazione in giorni usando il **profilo di log**.
* Eseguire query tramite l'API REST, i cmdlet di PowerShell o l'interfaccia della riga di comando.

## <a name="query-the-activity-log-in-the-azure-portal"></a>Eseguire query sul log attività nel portale di Azure
Nel portale di Azure è possibile visualizzare il log attività in diverse posizioni:
* Il **pannello Log attività**, a cui è possibile accedere cercando Log attività in "Altri servizi" nel riquadro di spostamento sinistro.
* Il **pannello Monitoraggio**, che per impostazione predefinita viene visualizzato nel riquadro di spostamento sinistro. Il log attività è una sezione di questo pannello Monitoraggio di Azure.
* Tutti i **pannelli delle risorse**, ad esempio il pannello di configurazione di una macchina virtuale. Il log attività è una delle sezioni nella maggior parte di questi pannelli delle risorse e, facendovi clic, vengono automaticamente filtrati gli eventi correlati alla risorsa specifica.

Nel portale di Azure è possibile filtrare il log attività in base a questi campi:
* Intervallo di tempo: ora di inizio e di fine degli eventi.
* Categoria: la categoria di eventi, come descritto sopra.
* Sottoscrizione: uno o più nomi di sottoscrizione di Azure.
* Gruppo di risorse: uno o più gruppi di risorse in tali sottoscrizioni.
* Risorsa (nome): nome di una risorsa specifica.
* Tipo di risorsa: tipo di risorsa, ad esempio Microsoft.Compute/virtualmachines.
* Nome operazione: nome di un'operazione di Azure Resource Manager, ad esempio Microsoft.SQL/servers/Write.
* Gravità: livello di gravità dell'evento (informativo, avviso, errore, critico).
* Evento avviato da: "chiamante" o utente che ha eseguito l'operazione.
* Apri ricerca: casella di ricerca di testo aperta che cerca tale stringa in tutti i campi di tutti gli eventi.

Dopo avere definito un set di filtri, è possibile salvarlo come query persistente nelle sessioni, in caso fosse necessario eseguire di nuovo la stessa query in futuro con tali filtri applicati. È anche possibile aggiungere una query al dashboard di Azure per avere sempre sotto controllo eventi specifici.

Fare clic su "Applica" per eseguire la query e visualizzare tutti gli eventi corrispondenti. Fare clic su un evento dell'elenco per visualizzare il riepilogo di tale evento, oltre al codice JSON non elaborato completo di tale evento.

Per eseguire operazioni più avanzate, è possibile fare clic sull'icona **Ricerca log**, che visualizza i dati del log attività nella [soluzione Analisi log attività di Log Analytics](../log-analytics/log-analytics-activity.md). Il pannello Log attività offre un'esperienza di filtro/esplorazione di base con i log, ma Log Analytics consente di trasformare tramite Pivot, eseguire query e visualizzare i dati in modo più dettagliato.

## <a name="export-the-activity-log-with-a-log-profile"></a>Esportare il log attività con un profilo di log
Un **profilo di log** controlla la modalità di esportazione del log attività. Un profilo di log permette di configurare quanto segue:

* Destinazione del log attività, ad esempio un account di archiviazione o un hub eventi.
* Categorie di eventi da inviare (scrittura, eliminazione o azione). *Il significato di "categoria" nei profili del log è diverso da quello negli eventi del log attività. Nel profilo del log, la "Categoria" rappresenta il tipo di operazione (scrittura, eliminazione, azione). In un evento del log attività, la proprietà "categoria" rappresenta l'origine o il tipo di evento (ad esempio, amministrazione, ServiceHealth, avviso e altro).*
* Aree o località da esportare. Assicurarsi di includere "global", perché molti eventi del log attività sono eventi globali.
* Per quanto tempo il log attività deve essere mantenuto nell'account di archiviazione.
    - Un periodo di conservazione di zero giorni significa che i log vengono conservati all'infinito. Se impostato su zero giorni, i log vengono conservati all'infinito.
    - Se i criteri di conservazione sono impostati, ma la memorizzazione dei log in un account di archiviazione è disabilitata, ad esempio se sono selezionate solo le opzioni Hub eventi o OMS, i criteri di conservazione non hanno alcun effetto.
    - I criteri di conservazione vengono applicati su base giornaliera. Al termine della giornata (UTC), i log relativi a tale giornata che non rientrano più nei criteri di conservazione verranno eliminati. Se, ad esempio, è presente un criterio di conservazione di un giorno, all'inizio della giornata vengono eliminati i log relativi al giorno precedente.

È possibile usare un account di archiviazione o un hub eventi dello spazio dei nomi che non si trovi nella stessa sottoscrizione di quello che crea i log. L'utente che configura l'impostazione deve disporre dell'accesso RBAC appropriato a entrambe le sottoscrizioni.

Queste impostazioni possono essere configurate tramite l'opzione "Esporta" nel pannello Log attività nel portale oppure a livello di codice tramite l'[API REST di Monitoraggio di Azure](https://msdn.microsoft.com/library/azure/dn931927.aspx), i cmdlet di PowerShell o l'interfaccia della riga di comando. Una sottoscrizione può avere un solo profilo di log.

### <a name="configure-log-profiles-using-the-azure-portal"></a>Configurare i profili di log tramite il portale di Azure
È possibile trasmettere il log attività a un hub eventi o memorizzarlo in un account di archiviazione usando l'opzione "Esporta" nel portale di Azure.

1. Passare al pannello **Log attività** usando il menu sul lato sinistro del portale.

    ![Passare al log attività nel portale](./media/monitoring-overview-activity-logs/activity-logs-portal-navigate.png)
2. Fare clic sul pulsante **Esporta** nella parte superiore del pannello.

    ![Pulsante Esporta nel portale](./media/monitoring-overview-activity-logs/activity-logs-portal-export.png)
3. Nel pannello visualizzato è possibile selezionare:  
  * aree per cui esportare gli eventi
  * account di archiviazione in cui salvare gli eventi
  * numero di giorni di conservazione degli eventi nella risorsa di archiviazione (se si impostano 0 giorni, i log vengono conservati all'infinito)
  * spazio dei nomi del bus di servizio in cui creare un hub eventi per la trasmissione di questi eventi.

     ![Pannello Esporta log di controllo](./media/monitoring-overview-activity-logs/activity-logs-portal-export-blade.png)
4. Fare clic su **Salva** per salvare le impostazioni. Le impostazioni vengono applicate immediatamente alla sottoscrizione.

### <a name="configure-log-profiles-using-the-azure-powershell-cmdlets"></a>Configurare i profili di log tramite i cmdlet di Azure PowerShell
#### <a name="get-existing-log-profile"></a>Ottenere un profilo di log esistente
```
Get-AzureRmLogProfile
```

#### <a name="add-a-log-profile"></a>Aggiungere un profilo di log
```
Add-AzureRmLogProfile -Name my_log_profile -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus -RetentionInDays 90 -Categories Write,Delete,Action
```

| Proprietà | Obbligatoria | DESCRIZIONE |
| --- | --- | --- |
| NOME |Sì |Nome del profilo di log. |
| StorageAccountId |No  |ID risorsa dell'account di archiviazione in cui salvare il log attività. |
| serviceBusRuleId |No  |ID regola del bus di servizio per lo spazio dei nomi del bus di servizio in cui creare gli hub eventi. Si tratta di una stringa nel formato seguente: `{service bus resource ID}/authorizationrules/{key name}`. |
| Località |Sì |Elenco delimitato da virgole di aree per cui raccogliere eventi del log attività. |
| RetentionInDays |Sì |Numero di giorni per cui gli eventi devono essere mantenuti, compreso tra 1 e 2147483647. Se il valore è zero, i log vengono mantenuti per un periodo illimitato. |
| Categorie |No  |Elenco delimitato da virgole di categorie di eventi che devono essere raccolti. I valori possibili sono Write, Delete e Action. |

#### <a name="remove-a-log-profile"></a>Rimozione di un profilo di log
```
Remove-AzureRmLogProfile -name my_log_profile
```

### <a name="configure-log-profiles-using-the-azure-cross-platform-cli"></a>Configurare i profili di log tramite l'interfaccia della riga di comando multipiattaforma di Azure
#### <a name="get-existing-log-profile"></a>Ottenere un profilo di log esistente
```
azure insights logprofile list
```
```
azure insights logprofile get --name my_log_profile
```
La proprietà `name` deve essere il nome del profilo di log.

#### <a name="add-a-log-profile"></a>Aggiungere un profilo di log
```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope --retentionInDays 90 –categories Write,Delete,Action
```

| Proprietà | Obbligatoria | DESCRIZIONE |
| --- | --- | --- |
| name |Sì |Nome del profilo di log. |
| storageId |No  |ID risorsa dell'account di archiviazione in cui salvare il log attività. |
| serviceBusRuleId |No  |ID regola del bus di servizio per lo spazio dei nomi del bus di servizio in cui creare gli hub eventi. Si tratta di una stringa nel formato seguente: `{service bus resource ID}/authorizationrules/{key name}`. |
| locations |Sì |Elenco delimitato da virgole di aree per cui raccogliere eventi del log attività. |
| RetentionInDays |Sì |Numero di giorni per cui gli eventi devono essere mantenuti, compreso tra 1 e 2147483647. Se il valore è zero, i log vengono mantenuti per un periodo illimitato. |
| Categorie |No  |Elenco delimitato da virgole di categorie di eventi che devono essere raccolti. I valori possibili sono Write, Delete e Action. |

#### <a name="remove-a-log-profile"></a>Rimozione di un profilo di log
```
azure insights logprofile delete --name my_log_profile
```

## <a name="next-steps"></a>Fasi successive
* [Altre informazioni sul log attività (in precedenza, log di controllo)](../azure-resource-manager/resource-group-audit.md)
* [Trasmettere il log attività di Azure a Hub eventi](monitoring-stream-activity-logs-event-hubs.md)
