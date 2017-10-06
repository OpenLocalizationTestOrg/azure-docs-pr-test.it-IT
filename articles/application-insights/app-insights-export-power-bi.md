---
title: aaaExport tooPower BI da Application Insights | Documenti Microsoft
description: Le query di Analisi possono essere visualizzate in Power BI.
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 7f13ea66-09dc-450f-b8f9-f40fdad239f2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: bwren
ms.openlocfilehash: 6668cd7f4e0fbf41695972617f5f8ec207356659
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="feed-power-bi-from-application-insights"></a>Feed di Power BI da Application Insights
[Power BI](http://www.powerbi.com/) è una suite di strumenti di analisi business che consente di analizzare i dati e condividere informazioni dettagliate. Dashboard completi sono disponibili in tutti i dispositivi. È possibile combinare dati provenienti da diverse origini, incluse le query di Analytics di [Azure Application Insights](app-insights-overview.md).

Esistono tre metodi consigliati per l'esportazione di dati di Application Insights tooPower BI. Possono essere usati insieme o separatamente.

* [**Adattatore Power BI**](#power-pi-adapter): consente di impostare un dashboard di dati di telemetria completo dall'app. set di grafici di Hello è predefinita, ma è possibile aggiungere query personalizzate da tutte le altre origini.
* [**Esportazione delle query Analitica** ](#export-analytics-queries) -scrivere una query tramite Analitica ed esportarlo tooPower BI. È possibile inserire questa query in un dashboard insieme a tutti gli altri dati.
* [**L'esportazione continua e Analitica flusso** ](app-insights-export-stream-analytics.md) -questa operazione richiede più lavoro tooset backup. È utile se si desidera tookeep i dati per lunghi periodi di tempo. In caso contrario, hello altri metodi sono consigliati.

## <a name="power-bi-adapter"></a>Adattatore Power BI
Con questo metodo si crea un dashboard di dati di telemetria completo per l'utente. set di dati iniziale Hello è predefinita, ma è possibile aggiungere ulteriori dati tooit.

### <a name="get-hello-adapter"></a>Ottenere hello scheda
1. Accedi troppo[Power BI](https://app.powerbi.com/).
2. Aprire **Get Data** (Ottieni dati), **Servizi**, **Application Insights**
   
    ![Scaricare da un'origine dati di Application Insights](./media/app-insights-export-power-bi/power-bi-adapter.png)
3. Fornire dettagli hello della risorsa di Application Insights.
   
    ![Scaricare da un'origine dati di Application Insights](./media/app-insights-export-power-bi/azure-subscription-resource-group-name.png)
4. Attendere un minuto o due per hello toobe di dati importati.
   
    ![Adattatore Power BI](./media/app-insights-export-power-bi/010.png)

È possibile modificare il dashboard di hello, la combinazione di grafici di Application Insights hello con quelli di altre origini e con query Analitica. È disponibile una raccolta di visualizzazioni nella quale è possibile ottenere più grafici e ogni grafico include parametri che possono essere impostati.

Dopo l'importazione iniziale hello, dashboard hello e report hello continuare tooupdate ogni giorno. È possibile controllare pianificazione dell'aggiornamento hello hello set di dati.

## <a name="export-analytics-queries"></a>Esportare query di Analisi
La route consente toowrite qualsiasi Analitica si desidera eseguire una query e quindi esportare i dashboard di Power BI tooa. (È possibile aggiungere dashboard toohello creato dall'adapter hello).

### <a name="one-time-install-power-bi-desktop"></a>Operazione da eseguire una sola volta: installazione di Power BI Desktop
tooimport della query di Application Insights, si utilizza hello versione desktop di Power BI. Ma è possibile pubblicarla, web toohello o tooyour dell'area di lavoro di Power BI cloud. 

Installare [Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/).

### <a name="export-an-analytics-query"></a>Esportare una query di Analisi
1. [Aprire Analisi e scrivere la query](app-insights-analytics-tour.md).
2. Testare e perfezionare query hello finché non si è soddisfatti dei risultati di hello.

   **Verificare che tale query hello viene eseguito correttamente in Analitica prima di esportarlo.**
3. In hello **esportare** menu, scegliere **Power BI (M)**. Salvare il file di testo hello.
   
    ![Esportare la query di Power BI](./media/app-insights-export-power-bi/analytics-export-power-bi.png)
4. In Power BI Desktop selezionare **recupera dati, Query vuota** e quindi in hello editor di query, in **vista** selezionare **Editor avanzato Query di**.

    Incollare lo script di linguaggio M hello esportata nella hello avanzate dell'Editor di Query.

    ![Editor query avanzata](./media/app-insights-export-power-bi/power-bi-import-analytics-query.png)

1. Potrebbe essere tooprovide credenziali tooallow Power BI tooaccess Azure. Utilizzare toosign 'account aziendale' con l'account Microsoft.
   
    ![Fornire le credenziali di Azure tooenable Power BI toorun query Application Insights](./media/app-insights-export-power-bi/power-bi-import-sign-in.png)

    (Se sono necessarie le credenziali di hello tooverify, utilizzare hello impostazioni dell'origine dati menu comando hello Editor di Query. Prestare attenzione credenziali di hello toospecify utilizzate per Azure, potrebbe essere diverso dalle credenziali per Power BI.)
2. Scegliere una visualizzazione per la query e selezionare i campi di hello per l'asse x, y e segmentazione dimensione.
   
    ![Selezionare la visualizzazione](./media/app-insights-export-power-bi/power-bi-analytics-visualize.png)
3. Pubblicare report tooyour Power BI cloud area di lavoro. Da qui è possibile incorporare una versione sincronizzata in altre pagine Web.
   
    ![Selezionare la visualizzazione](./media/app-insights-export-power-bi/publish-power-bi.png)
4. Aggiornare manualmente i report hello a intervalli o di impostare un aggiornamento pianificato nella pagina di opzioni di hello.

## <a name="troubleshooting"></a>Risoluzione dei problemi

### <a name="401-or-403-unauthorized"></a>401 o 403 - Non autorizzato 
Questo errore può verificarsi se il token di aggiornamento non è stato aggiornato. Provare a tooensure questi passaggi sarà comunque possibile accedere. Se si dispone dell'accesso e le credenziali di aggiornamento hello non funziona, aprire un ticket di supporto.

1. Accedere al portale di Azure hello e assicurarsi che sia possibile accedere a risorse hello
2. Provare a specificare credenziali hello toorefresh per hello Dashboard

### <a name="502-bad-gateway"></a>502 - Gateway non valido
Questo errore è in genere causato da una query di Analisi che restituisce troppi dati. È consigliabile provare con un intervallo di tempo inferiore o utilizzando hello [fa](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#ago) o [startofweek/startofmonth](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#startofweek) solo funzioni [progetto](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#project-operator) hello campi necessari.

Se la riduzione di hello set di dati provenienti da query Analitica hello non soddisfa i requisiti, è consigliabile utilizzare hello [API](https://dev.applicationinsights.io/documentation/overview) toopull un set di dati più grande. Di seguito sono istruzioni sulla procedura di esportazione toouse hello API tooconvert hello M-Query.

1. Creare una [chiave API](https://dev.applicationinsights.io/documentation/Authorization/API-key-and-App-ID)
2. Hello aggiornamento dello script di Power BI M esportato da Analitica sostituendo hello URL ARM con API AI (vedere l'esempio riportato di seguito)
   * Sostituire **https://management.azure.com/subscriptions/...**
   * con **https://api.applicationinsights.io/beta/apps/...**
3. Infine, aggiornare le credenziali toobasic e utilizzare la chiave API
  

**Script esistente**
 ```
 Source = Json.Document(Web.Contents("https://management.azure.com/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups//providers/microsoft.insights/components//api/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```
**Script aggiornato**
 ```
 Source = Json.Document(Web.Contents("https://api.applicationinsights.io/beta/apps/<APPLICATION_ID>/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```

## <a name="about-sampling"></a>Informazioni sul campionamento
Se l'applicazione invia una grande quantità di dati, funzionalità di campionamento adattivo hello possono operare e inviare solo una percentuale dei dati di telemetria. Hello che stesso vale se manualmente impostate campionamento in hello SDK o in un inserimento. [Altre informazioni sul campionamento.](app-insights-sampling.md)


## <a name="next-steps"></a>Passaggi successivi
* [Power BI - Informazioni](http://www.powerbi.com/learning/)
* [Esercitazione su Analisi](app-insights-analytics-tour.md)

