---
title: aaaGet Introduzione a monitoraggio di Azure | Documenti Microsoft
description: Introduzione all'uso di operazione hello delle risorse approfondite toogain Monitor di Azure ed esegue azioni in base ai dati.
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: ce2930aa-fc41-4b81-b0cb-e7ea922467e1
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/19/2016
ms.author: johnkem
ms.openlocfilehash: 49e7105621a9e60c9fa14c4911c4fe45e0d197a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-monitor"></a>Introduzione al monitoraggio di Azure
Monitoraggio di Azure è servizio di piattaforma hello che fornisce un'unica origine per il monitoraggio delle risorse di Azure. Con il monitoraggio di Azure, è possibile visualizzare, richiedere, route, archiviare e intraprendere un'azione in metriche hello e log provenienti dalle risorse in Azure. È possibile utilizzare questo dati pannello portale monitoraggio di hello, con [i cmdlet PowerShell di monitoraggio](insights-powershell-samples.md), [CLI multipiattaforma](insights-cli-samples.md), o [API REST di Azure monitoraggio](https://msdn.microsoft.com/library/dn931943.aspx). In questo articolo vengono illustrate le alcuni dei componenti principali di hello di monitoraggio di Azure, tramite il portale di hello dimostrativo.

1. Nel portale di hello passare troppo**più servizi** e trovare hello **monitoraggio** opzione. Fare clic su hello tooadd di icona a stella Preferiti di tooyour questa opzione in modo che sia sempre facilmente accessibile dalla barra di navigazione a sinistra di hello.
   
    ![Monitorare nell'elenco di servizi di hello](./media/monitoring-get-started/monitor-more-services.png)
2. Fare clic su hello **monitoraggio** tooopen opzione backup hello **monitoraggio** blade. che riunisce tutte le impostazioni e i dati di monitoraggio in un'unica vista consolidata. Viene aperto prima toohello **log attività** sezione.
   
    ![Esplorazione del pannello Monitoraggio](./media/monitoring-get-started/monitor-blade-nav.png)
   
    Monitoraggio di Azure ha tre categorie di dati di monitoraggio di base: hello **log attività**, **metriche**, e **i log di diagnostica**.
3. Fare clic su **log attività** tooensure che hello sezione log attività viene visualizzato.
   
    ![Pannello Log di attività](./media/monitoring-get-started/monitor-act-log-blade.png)
   
    Hello [ **log attività** ](monitoring-overview-activity-logs.md) descrive tutte le operazioni eseguite sulle risorse nella sottoscrizione. Hello registro attività, consentono di determinare hello ' cosa, chi e quando ' per le operazioni di creazione, aggiornamento o eliminazione di operazioni sulle risorse nella sottoscrizione. Ad esempio, hello Log attività indica quando un'app web è stata arrestata e che ha interrotto. Eventi del registro attività vengono archiviati nella piattaforma hello e tooquery disponibili per 90 giorni.
   
    È possibile creare e salvare le query per filtri comuni, quindi pin hello più importanti query tooa dashboard del portale in modo si saprà sempre se si sono verificati gli eventi che soddisfano i criteri specificati.
4. Filtrare hello vista tooa determinato gruppo di risorse su hello ultima settimana, quindi fare clic su hello **salvare** pulsante.
   
    ![Salvare la query del Log di attività](./media/monitoring-get-started/monitor-act-log-save.png)
5. A questo punto, fare clic su hello **Pin** pulsante.
   
    ![Fare clic su Aggiungi per Log di attività](./media/monitoring-get-started/monitor-act-log-pin.png)
   
    La maggior parte delle viste hello in questa procedura dettagliata può essere bloccato tooa dashboard. Ciò consente di creare un'unica origine di informazioni sui dati operativi nei propri servizi. 
6. Dashboard tooyour restituito. È possibile ora query hello (e numero di risultati) è visualizzato nel dashboard. Ciò è utile se si desidera vedere tooquickly eventuali azioni di alto profilo che si sono verificati recente nella sottoscrizione, ad esempio. l'assegnazione di un nuovo ruolo o l'eliminazione di una macchina virtuale.
   
    ![Attività bloccato log toodashboard](./media/monitoring-get-started/monitor-act-log-db.png)
7. Restituire toohello **monitoraggio** riquadro e fare clic su hello **metriche** sezione. È necessario innanzitutto tooselect una risorsa di applicazione di filtri e selezionando utilizzando hello opzioni a discesa nella parte superiore di hello del pannello hello.
   
    ![Filtrare le risorse per le metriche](./media/monitoring-get-started/monitor-met-filter.png)
   
    Tutte le risorse di Azure generano [**metriche**](monitoring-overview-metrics.md). Questa visualizzazione riunisce tutte le metriche in un unico pannello in modo da comprendere facilmente le prestazioni delle risorse.
8. Dopo aver selezionato una risorsa, tutte le metriche disponibili vengono visualizzati sul lato sinistro di blade hello hello. È possibile grafico contemporaneamente diverse metriche selezionando le metriche e modificare l'intervallo di tempo e di tipo di grafico hello. È inoltre possibile visualizzare tutti gli avvisi relativi alle metriche impostati su questa risorsa.
   
    ![Blade delle metriche](./media/monitoring-get-started/monitor-metric-blade.png)
   
   > [!NOTE]
   > Alcune metriche sono disponibili solo abilitando [Application Insights](../application-insights/app-insights-overview.md) e/o Diagnostica di Azure per Windows o Linux sulla risorsa.
   > 
   > 
9. Quando si è soddisfatti con il grafico, è possibile utilizzare hello **Pin** pulsante toopin è tooyour dashboard.
10. Restituire toohello **monitoraggio** pannello e fare clic su **log di diagnostica**.
    
    ![Pannello Log di diagnostica](./media/monitoring-get-started/monitor-diaglogs-blade.png)
    
    [**I log di diagnostica** ](monitoring-overview-of-diagnostic-logs.md) sono registri generati *da* una risorsa che forniscono dati sull'operazione di hello di tale particolare risorsa. Ad esempio, i numeri di regole del gruppo di sicurezza di rete e i log del flusso di lavoro delle app per la logica sono due tipologie di log di diagnostica. Questi registri possono essere archiviati in un account di archiviazione, flusso tooan Hub eventi, e/o inviati troppo[Analitica Log](../log-analytics/log-analytics-overview.md). Log Analytics è il prodotto di intelligence operativa di Microsoft per eseguire operazioni avanzate di ricerca e avviso.
    
    Nel portale di hello è possibile visualizzare e filtrare un elenco di tutte le risorse in tooidentify la sottoscrizione se dispongono di log di diagnostica abilitato.
11. Fare clic su una risorsa nel Pannello di log di diagnostica hello. Se i log di diagnostica vengono archiviati in un account di archiviazione, l'utente visualizzerà un elenco di log orari scaricabile.
    
    ![Log di diagnostica per una risorsa](./media/monitoring-get-started/monitor-diaglogs-detail.png)
    
    È anche possibile fare clic su **le impostazioni di diagnostica**, che consente tooset backup o modificare le impostazioni per l'account di archiviazione dell'archivio tooa, streaming tooEvent hub o l'invio dell'area di lavoro di tooa Analitica di Log.
    
    ![Abilitare i log di diagnostica](./media/monitoring-get-started/monitor-diaglogs-enable.png)
    
    Se configuri i log di diagnostica tooLog Analitica, è possibile quindi cercare li hello **ricerca nei Log** sezione del portale hello.
12. Passare toohello **avvisi** sezione del pannello monitoraggio hello.
    
    ![pannello avvisi pubblici](./media/monitoring-get-started/monitor-alerts-nopp.png)
    
    Qui è possibile gestire tutti gli [**avvisi**](monitoring-overview-alerts.md) delle risorse di Azure, compresi gli avvisi sulle metriche, sugli eventi di log attività, sui test Web di Application Insights (posizioni) e sulla diagnostica proattiva di Application Insights. Gli avvisi possono attivare toobe un messaggio di posta elettronica inviato o un URL del webhook tooa HTTP POST.
13. Fare clic su **Aggiungi avviso metrica** toocreate un avviso.
    
    ![Aggiungi avviso sulla metrica](./media/monitoring-get-started/monitor-alerts-add.png)
    
    È possibile quindi pin un tooeasily dashboard tooyour avviso vedere lo stato in qualsiasi momento.
14. la sezione monitoraggio Hello include anche collegamenti troppo[Application Insights](../application-insights/app-insights-overview.md) applicazioni e [Log Analitica](../log-analytics/log-analytics-overview.md) soluzioni di gestione. Questi altri prodotti Microsoft si integrano pienamente con il monitoraggio di Azure.
15. Se Application Insights o Log Analytics non vengono usati, ci sono possibilità che il monitoraggio di Azure funzioni in collaborazione con le soluzioni di monitoraggio, registrazione e avviso attualmente in uso. Vedere il nostro [pagina partner](monitoring-partners.md) per un elenco completo e istruzioni su come toointegrate.

La procedura seguente e tutti i dashboard tooa sezioni pertinenti di blocco, è possibile creare visualizzazioni complete dell'applicazione e dell'infrastruttura come questa:

![Dashboard del monitoraggio di Azure](./media/monitoring-get-started/monitor-final-dash.png)

## <a name="next-steps"></a>Passaggi successivi
* Hello lettura [Panoramica di monitoraggio di Azure](monitoring-overview.md)

