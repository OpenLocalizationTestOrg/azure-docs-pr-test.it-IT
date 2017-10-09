---
title: domande frequenti sulla ricerca di log nuovo aaaLog Analitica | Documenti Microsoft
description: Questo articolo fornisce le domande frequenti relative hello aggiornamento del Log Analitica toohello nuovo linguaggio di query.
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/27/2017
ms.author: bwren
ms.openlocfilehash: b8664c8329fab0547f270793fa13e8cdd06ba637
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-new-log-search-faq-and-known-issues"></a>Nuova ricerca log in Log Analytics - domande frequenti e problemi noti

In questo articolo include domande frequenti e problemi noti relativi hello aggiornamento di [toohello Log Analitica nuovo linguaggio di query](log-analytics-log-search-upgrade.md).  È necessario leggere l'intero articolo prima di apportare hello decisione tooupgrade l'area di lavoro.


## <a name="alerts"></a>Avvisi

### <a name="question-i-have-a-lot-of-alert-rules-do-i-need-toocreate-them-again-in-hello-new-language-after-i-upgrade"></a>Domanda: Sono presenti molte regole di avviso. Necessario toocreate nuovamente nel hello nuovo linguaggio dopo l'aggiornamento?  
No, le regole di avviso vengono automaticamente convertiti toohello nuovo linguaggio di ricerca durante l'aggiornamento.  


## <a name="computer-groups"></a>Gruppi di computer

### <a name="question-im-getting-errors-when-trying-toouse-computer-groups--has-their-syntax-changed"></a>Domanda: taccia errori durante il tentativo di gruppi di computer toouse.  La sintassi è stata modificata?
Sì, sintassi hello per l'utilizzo di computer Raggruppa le modifiche quando si aggiorna l'area di lavoro.  Per informazioni dettagliate, vedere [Gruppi di computer nelle ricerche nei log in Log Analytics](log-analytics-computer-groups.md).

### <a name="known-issue-groups-imported-from-active-directory"></a>Problema noto: Gruppi importati da Active Directory
Attualmente, è possibile creare una query che usi un gruppo di computer importato da Active Directory.  In alternativa finché non viene risolto questo problema, creare un nuovo gruppo di computer utilizzando il gruppo di Active Directory hello importato e quindi utilizzare tale nuovo gruppo nella query.

Un toocreate di query di esempio un nuovo gruppo di computer che include un gruppo di Active Directory importato è indicato di seguito:

    ComputerGroup | where GroupSource == "ActiveDirectory" and Group == "AD Group Name" and TimeGenerated >= ago(24h) | distinct Computer


## <a name="dashboards"></a>Dashboard

### <a name="question-can-i-still-use-dashboards-in-an-upgraded-workspace"></a>Domanda: È sempre possibile usare i dashboard in un'area di lavoro aggiornata?
È possibile continuare a toouse qualsiasi riquadri aggiunti troppo**My Dashboard** prima che l'area di lavoro è stato aggiornato, ma è possibile modificare tali riquadri o aggiungerne di nuovi.  È possibile continuare toocreate e modificare le viste con [Visualizza finestra di progettazione](log-analytics-view-designer.md) e anche creare dashboard in hello portale di Azure.


## <a name="log-searches"></a>Ricerche log

### <a name="question-i-have-saved-searches-outside-of-my-upgraded-workspace-can-i-convert-them-toohello-new-search-language-automatically"></a>Domanda: Le ricerche salvate all'esterno dell'area di lavoro aggiornata È possibile convertire in nuovo linguaggio di ricerca toohello automaticamente?
È possibile utilizzare strumento di conversione language hello in hello Registro ricerca pagina tooconvert ciascuno di essi.  Non è non convertire tooautomatically metodo più ricerche senza effettuare l'aggiornamento dell'area di lavoro di hello.

### <a name="question-why-are-my-query-results-not-sorted"></a>Domanda: Perché i risultati della query non sono ordinati?
Risultati non sono ordinati per impostazione predefinita nel nuovo linguaggio di query hello.  Hello utilizzare [operatore sort](https://go.microsoft.com/fwlink/?linkid=856079) toosort i risultati tramite una o più proprietà.

### <a name="known-issue-search-results-in-a-list-may-include-properties-with-no-data"></a>Problema noto: I risultati della ricerca in un elenco possono includere proprietà senza dati
I risultati della ricerca log in un elenco possono includere proprietà senza dati.  Tooupgrade precedenti, queste proprietà non può essere incluse.  Questo problema verrà corretto in modo che le proprietà vuote non vengano visualizzate.

### <a name="known-issue-selecting-a-value-in-a-chart-doesnt-display-detailed-results"></a>Problema noto: La selezione di un valore in un grafico non visualizza risultati dettagliati
Tooupgrade precedente, quando si seleziona un valore in un grafico, restituisce un elenco dettagliato dei record corrispondenti al valore selezionato hello.  Dopo l'aggiornamento, viene restituito solo hello riepilogati riga.  Questo problema è attualmente in fase di analisi.

## <a name="log-search-api"></a>API di ricerca nei log

### <a name="question-does-hello-log-search-api-get-updated-after-i-upgrade"></a>Domanda: Hello API di ricerca Log viene aggiornato dopo l'aggiornamento?
Hello [API di ricerca Log](log-analytics-log-search-api.md) non è ancora stato aggiornato toohello nuovo linguaggio di ricerca.  Continuare il linguaggio di query legacy hello toouse con questa API, anche dopo l'aggiornamento dell'area di lavoro.  Quando viene aggiornato, verrà rese disponibile per l'API di ricerca Log hello documentazione aggiornata.


## <a name="portals"></a>Portali

### <a name="question-should-i-use-hello-new-advanced-analytics-portal-or-keep-using-hello-log-search-portal"></a>Domanda: È consigliabile usare il nuovo portale di Advanced Analitica hello o continuare a utilizzare il portale di ricerca nei Log hello?
È possibile visualizzare un confronto dei portali hello due in [portali per la creazione e modifica delle query di log in Azure Log Analitica](log-analytics-log-search-portals.md).  Ognuno presenta vantaggi distinti in cui è possibile scegliere hello più adatto alle proprie esigenze.  È una query toowrite comuni nel portale avanzate Analitica hello e incollarli in altre posizioni, ad esempio Progettazione viste.  È necessario essere a conoscenza [problemi tooconsider](log-analytics-log-search-portals.md#advanced-analytics-portal) quando questa operazione.


## <a name="power-bi"></a>Power BI

### <a name="question-does-anything-change-with-powerbi-integration"></a>Domanda: L'aggiornamento implica modifiche per l'integrazione con Power BI?
Sì.  Dopo che l'area di lavoro è stato aggiornato quindi processo hello per l'esportazione di dati di Log Analitica tooPower BI non funzionerà più.  Le pianificazioni esistenti create prima dell'aggiornamento verranno disabilitate.  Dopo l'aggiornamento, viene utilizzato Azure Log Analitica hello stessa piattaforma come Application Insights e si utilizza hello stessa procedura adottata tooexport Analitica Log query tooPower BI come [tooexport processo hello Application Insights query tooPower BI](../application-insights/app-insights-export-power-bi.md#export-analytics-queries).

### <a name="known-issue-power-bi-request-size-limit"></a>Problema noto: Limite di dimensioni richiesta in Power BI
È attualmente una dimensione massima di 8 MB per una query Log Analitica che può essere esportati tooPower BI.  Questo limite verrà presto incrementato.


##<a name="powershell-cmdlets"></a>Cmdlet PowerShell

### <a name="question-does-hello-log-search-powershell-cmdlet-get-updated-after-i-upgrade"></a>Domanda: Cmdlet PowerShell di ricerca Log hello viene aggiornato dopo l'aggiornamento?
Hello [Get AzureRmOperationalInsightsSearchResults](https://docs.microsoft.com/powershell/module/azurerm.operationalinsights/Get-AzureRmOperationalInsightsSearchResults) non è ancora stato aggiornato toohello nuovo linguaggio di ricerca.  Continuare il linguaggio di query legacy hello toouse con questo cmdlet, anche dopo l'aggiornamento dell'area di lavoro.  Quando viene aggiornato, verrà rese disponibile per cmdlet hello documentazione aggiornata.


## <a name="resource-manager-templates"></a>Modelli di Gestione risorse

### <a name="question-can-i-create-an-upgraded-workspace-with-a-resource-manager-template"></a>Domanda: È possibile creare un'area di lavoro aggiornata con un modello di Resource Manager?
Sì.  È necessario utilizzare la versione dell'API di 2017-03-15-preview e include un **funzionalità** sezione nel modello come hello di esempio seguente.

    "resources": [
        {
            "type": "Microsoft.OperationalInsights/workspaces",
            "apiVersion": "2017-03-15-preview",
            "name": "[parameters('workspaceName')]",
            "location": "[parameters('workspaceRegion')]",
            "properties": {
                "sku": {
                    "name": "Free"
                },
                "features": {
                    "legacy": 0,
                    "searchVersion": 1
                }
            }
        }
    ],



## <a name="solutions"></a>Soluzioni

### <a name="question-will-my-solutions-continue-toowork"></a>Domanda: My soluzioni continuerà toowork?
Tutte le soluzioni continuerà toowork in un'area di lavoro aggiornata, anche se le prestazioni miglioreranno se sono toohello convertito di nuovo linguaggio di query.  Esistono alcuni problemi noti con alcune soluzioni esistenti che sono descritte in questa sezione.

### <a name="known-issue-capacity-and-performance-solution"></a>Problema noto: Soluzione Capacità e prestazioni
Alcune delle parti di hello hello [capacità e prestazioni](log-analytics-capacity.md) vista può essere vuota.  Un problema di correzione toothis è disponibile a breve.

### <a name="known-issue-device-health-solution"></a>Problema noto: Soluzione Integrità del dispositivo
Hello [soluzione di integrità del dispositivo](https://docs.microsoft.com/windows/deployment/update/device-health-monitor) non raccoglierà i dati in un'area di lavoro aggiornato.  Un problema di correzione toothis è disponibile a breve.

### <a name="known-issue-application-insights-connector"></a>Problema noto: Connettore di Application Insights
Le prospettive nella [soluzione Connettore di Application Insights](log-analytics-app-insights-connector.md) non sono attualmente supportate in un'area di lavoro aggiornata.  Un problema di correzione toothis è attualmente sottoposta ad analisi.

## <a name="upgrade-process"></a>Processo di aggiornamento

### <a name="question-i-have-several-workspaces-can-i-upgrade-all-workspaces-at-hello-same-time"></a>Domanda: Sono disponibili diverse aree di lavoro. È possibile aggiornare tutte le aree di lavoro in hello contemporaneamente?  
No.  L'aggiornamento si applica tooa singola area di lavoro ogni volta. Non è attualmente disponibile alcun modo per aggiornare contemporaneamente molte aree di lavoro. Si noti che saranno interessate anche altri utenti dell'area di lavoro hello aggiornato.  

### <a name="question-will-existing-log-data-collected-in-my-workspace-be-modified-if-i-upgrade"></a>Domanda: I dati di log esistenti raccolti in un'area di lavoro verranno modificati in seguito all'aggiornamento?  
No. ricerche di Hello log dati tooyour disponibile dell'area di lavoro non è interessata dall'aggiornamento hello. Ricerche salvate, avvisi e alle visualizzazioni verrà convertito toohello nuovo linguaggio di ricerca automaticamente.  

### <a name="question-what-happens-if-i-dont-upgrade-my-workspace"></a>Domanda: Cosa accade se non si aggiorna l'area di lavoro?  
ricerca nei log legacy Hello verrà deprecata in hello in arrivo mesi. Le aree di lavoro non aggiornate verranno in seguito aggiornate automaticamente.

### <a name="question-i-didnt-choose-tooupgrade-but-my-workspace-has-been-upgraded-anyway-what-happened"></a>Domanda: non è stata scegliere tooupgrade, ma l'area di lavoro è stato aggiornato comunque! Che cosa è successo?  
Area di lavoro hello Impossibile sono aggiornati da un altro amministratore dell'area di lavoro. Si noti che tutte le aree di lavoro verrà automaticamente aggiornati quando raggiunge il nuovo linguaggio hello disponibilità generale.  

### <a name="question-i-have-upgraded-by-mistake-and-now-need-toocancel-it-and-restore-everything-back-what-should-i-do"></a>Domanda: sono stati aggiornati per errore e necessario toocancel insieme a tutti gli elementi cui eseguire il ripristino. ripristinare tutto?  
Non c'è problema.  Prima dell'aggiornamento dell'area di lavoro viene creato uno snapshot ed è quindi possibile ripristinarlo. Tenere presente che per la ricerca, gli avvisi o è stato salvato dopo l'aggiornamento di hello andranno persi anche se le viste.  toorestore l'ambiente dell'area di lavoro, seguire hello procedura [posso accedere nuovamente dopo l'aggiornamento?](log-analytics-log-search-upgrade.md#can-i-go-back-after-i-upgrade)


## <a name="views"></a>Visualizzazioni

### <a name="question-how-do-i-create-a-new-view-with-view-designer"></a>Domanda: Come si crea una nuova vista con Progettazione viste?
Tooupgrade precedente, è possibile creare una nuova vista con progettazione vista da un riquadro nel dashboard principale hello.  Quando l'area di lavoro viene aggiornata, questo riquadro viene rimosso.  È possibile creare una nuova vista con progettazione vista nel portale OMS hello facendo clic sul pulsante di menu a sinistra di hello + hello verde.

### <a name="known-issue-see-all-option-for-line-charts-in-views-doesnt-result-in-a-line-chart"></a>Problema noto: L'opzione Tutti per i grafici a linee in Viste non dà origine a un grafico a linee
Quando fa clic su hello *tutti* opzione nella parte inferiore di hello di una parte del grafico di riga in una vista, viene visualizzata una tabella.  Tooupgrade precedente, verrà visualizzata con un grafico a linee.  Questo problema è attualmente in fase di analisi per una modifica potenziale.


## <a name="next-steps"></a>Passaggi successivi

- Altre informazioni, vedere [toohello l'area di lavoro di aggiornamento il linguaggio di query nuovo Log Analitica](log-analytics-log-search-upgrade.md).
