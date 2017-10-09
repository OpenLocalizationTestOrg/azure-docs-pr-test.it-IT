---
title: integrazione di aaaSCOM con Application Insights | Documenti Microsoft
description: Gli utenti di SCOM possono monitorare le prestazioni e diagnosticare i problemi con Application Insights. Dashboard completi, avvisi intelligenti, potenti strumenti di diagnostica e query di analisi.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 606e9d03-c0e6-4a77-80e8-61b75efacde0
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/12/2016
ms.author: bwren
ms.openlocfilehash: ee9ad462610fd916098a0e292c5bd44f2a873c10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="application-performance-monitoring-using-application-insights-for-scom"></a>Application Performance Monitoring con Application Insights per SCOM
Se si utilizzano System Center Operations Manager (SCOM) toomanage i server, è possibile monitorare le prestazioni e diagnosticare i problemi di prestazioni con l'aiuto di hello di [Azure Application Insights](app-insights-asp-net.md). Application Insights monitora le richieste in ingresso dell'applicazione Web, le chiamate REST e SQL in uscita, le eccezioni e le tracce dei log. Fornisce i dashboard con grafici delle metriche e avvisi intelligenti, nonché funzionalità di ricerca diagnostica avanzate e query analitiche di questi dati di telemetria. 

È possibile attivare il monitoraggio di Application Insights tramite un Management Pack di SCOM.

## <a name="before-you-start"></a>Prima di iniziare
Si presuppone quanto segue:

* Si ha familiarità con SCOM e usare SCOM 2012 R2 o 2016 toomanage di IIS server web.
* Già installati nei server di un'applicazione web che si desidera toomonitor con Application Insights.
* La versione de framework applicazione è .NET 4.5 o versione successiva.
* Si dispone di accesso tooa sottoscrizione [Microsoft Azure](https://azure.com) e può firmare in toohello [portale di Azure](https://portal.azure.com). L'organizzazione dispone di una sottoscrizione e può aggiungere la tooit account Microsoft.

(il team di sviluppo hello venga compilato hello [Application Insights SDK](app-insights-asp-net.md) in hello web app. La strumentazione in fase di compilazione offre una maggiore flessibilità per la scrittura di dati di telemetria personalizzati. Tuttavia, non è importante: è possibile seguire i passaggi di hello descritti qui, con o senza hello SDK incorporata.)

## <a name="one-time-install-application-insights-management-pack"></a>(Una sola volta) Installare Management Pack per Application Insights
Nel computer di hello in cui si esegue Operations Manager:

1. Disinstallare qualsiasi versione precedente del management pack di hello:
   1. In Operations Manager aprire Amministrazione, Management Pack. 
   2. Eliminare la versione precedente di hello.
2. Scaricare e installare hello management pack dal catalogo hello.
3. Riavviare Operations Manager.

## <a name="create-a-management-pack"></a>Creare un management pack
1. In Operations Manager aprire **Creazione**, **.NET... con Application Insights**, **Aggiunta guidata monitoraggio** e scegliere nuovamente **.NET... con Application Insights**.
   
    ![](./media/app-insights-scom/020.png)
2. Configurazione del nome hello dopo l'applicazione. (Hai tooinstrument un'app alla volta.)
   
    ![](./media/app-insights-scom/030.png)
3. Hello nella stessa pagina della procedura guidata, creare un nuovo management pack o selezionare un pacchetto creato in precedenza per Application Insights.
   
     (hello Application Insights [management pack di](https://technet.microsoft.com/library/cc974491.aspx) è un modello, da cui si crea un'istanza. È possibile riutilizzare hello stessa istanza in un secondo momento.)

    ![Nella scheda proprietà generali di hello, digitare il nome di hello dell'applicazione hello. Fare clic su Nuovo e digitare un nome per un management pack. Fare clic su OK e quindi su Avanti.](./media/app-insights-scom/040.png)

1. Scegliere un'app che si desidera toomonitor. funzionalità di ricerca Hello Cerca tra le app installate nel server.
   
    ![Nella scheda da tooMonitor, fare clic su Aggiungi, digitare parte del nome dell'applicazione hello, fare clic su Cerca, scegliere OK hello app, quindi scegliere Aggiungi,](./media/app-insights-scom/050.png)
   
    Hello facoltativo monitoraggio ambito campo può essere utilizzato toospecify un sottoinsieme di server, se non si desidera app hello toomonitor in tutti i server.
2. Nella pagina della procedura guidata Avanti hello, è necessario specificare innanzitutto toosign le credenziali in tooMicrosoft Azure.
   
    In questa pagina è scegliere una risorsa di Application Insights hello in cui si desidera hello toobe dati di telemetria analizzati e visualizzati. 
   
   * Se un'applicazione hello è stata configurata per Application Insights durante lo sviluppo, selezionare la risorsa esistente.
   * In caso contrario, creare una nuova risorsa denominata per l'applicazione hello. Se sono presenti altre applicazioni che sono componenti di hello sistema stesso, inserirli in hello stesso gruppo di risorse, toomake accesso toohello telemetria più facile toomanage.
     
     Queste impostazioni possono essere modificate in seguito.
     
     ![Nella scheda Impostazioni di Application Insights fare clic su 'accedi' e fornire le credenziali dell'account Microsoft per Azure. Quindi scegliere una sottoscrizione, gruppo di risorse e una risorse.](./media/app-insights-scom/060.png)
3. Creazione guidata hello completo.
   
    ![Fare clic su Crea](./media/app-insights-scom/070.png)

Ripetere questa procedura per ogni app che si desidera toomonitor.

Se è necessario toochange impostazioni in un secondo momento, è necessario aprire nuovamente proprietà hello del monitoraggio di hello dalla finestra di creazione e modifica di hello.

![Nella finestra di creazione selezionare Monitoraggio delle prestazioni delle applicazioni .NET con Application Insights, selezionare la funzionalità di monitoraggio e fare clic su Proprietà.](./media/app-insights-scom/080.png)

## <a name="verify-monitoring"></a>Verificare il monitoraggio
monitoraggio di Hello di avere installato Cerca l'app in ogni server. In cui trova app hello, configura Application Insights Status Monitor toomonitor hello app. Se necessario, innanzitutto Status Monitor viene installato nel server di hello.

È possibile verificare quali istanze di applicazione hello che è stato individuato:

![In Monitoraggio aprire Application Insights](./media/app-insights-scom/100.png)

## <a name="view-telemetry-in-application-insights"></a>Visualizzare i dati di telemetria in Application Insights
In hello [portale di Azure](https://portal.azure.com), Sfoglia risorsa toohello per l'app. Nell'app è possibile [visualizzare grafici che mostrano i dati di telemetria](app-insights-dashboards.md) . (Se non vengono visualizzate nella pagina principale di hello ancora, fare clic su flusso di metriche in tempo reale).

## <a name="next-steps"></a>Passaggi successivi
* [Impostare un dashboard](app-insights-dashboards.md) grafici più importanti insieme hello toobring monitoraggio questa e altre app.
* [Informazioni sulle metriche](app-insights-metrics-explorer.md)
* [Impostare gli avvisi in Application Insights](app-insights-alerts.md)
* [Rilevare, valutare e diagnosticare con Application Insights](app-insights-detect-triage-diagnose.md)
* [Query di Analisi avanzate](app-insights-analytics.md)
* [Test Web di disponibilità](app-insights-monitor-web-app-availability.md)

