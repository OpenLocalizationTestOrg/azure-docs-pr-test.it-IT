---
title: Mappa in Azure Application Insights aaaApplication | Documenti Microsoft
description: Rappresentazione grafica delle dipendenze di hello tra i componenti dell'app, etichettata con avvisi e gli indicatori KPI.
services: application-insights
documentationcenter: 
author: SoubhagyaDash
manager: carmonm
ms.assetid: 3bf37fe9-70d7-4229-98d6-4f624d256c36
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 96ab753a100ea53ec7d367e3559b6622ab6fd182
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="application-map-in-application-insights"></a>Mappa delle applicazioni in Application Insights
In [Azure Application Insights](app-insights-overview.md), mapping di applicazioni è un layout visivo hello relazioni di dipendenza dei componenti di applicazione. Ogni componente mostra gli indicatori KPI, ad esempio toohelp carico, prestazioni, errori e avvisi, che si scopre di qualsiasi componente che causa un errore o un problema di prestazioni. È possibile fare clic su tramite toomore qualsiasi componente dettagliate di diagnostica, ad esempio gli eventi di Application Insights. Se l'app Usa i servizi di Azure, è anche possibile fare clic tramite diagnostica tooAzure, ad esempio indicazioni guidata Database SQL.

Come altri tipi di grafico, è possibile aggiungere un toohello mappa applicazione dashboard di Azure, in cui è completamente funzionale. 

## <a name="open-hello-application-map"></a>Mappa delle applicazioni hello aperto
Mappa di hello aperto dal pannello della panoramica hello per l'applicazione:

![aprire la mappa delle app](./media/app-insights-app-map/01.png)

![mappa delle app](./media/app-insights-app-map/02.png)

Mostra mappa Hello:

* Test della disponibilità
* Componente lato client (controllato con hello SDK per JavaScript)
* Componente lato server
* Dipendenze dei componenti client e server hello

È possibile espandere e comprimere i gruppi di collegamento di dipendenza:

![comprimere](./media/app-insights-app-map/03.png)

Se si dispone di numerose dipendenze di un tipo (SQL, HTTP e così via), possono essere visualizzate raggruppate. 

![dipendenze raggruppate](./media/app-insights-app-map/03-2.png)

## <a name="spot-problems"></a>Individuazione di problemi
Ogni nodo dispone di indicatori di prestazioni rilevanti, ad esempio tassi hello di carico, prestazioni ed errori per il componente. 

Le icone di avviso evidenziano possibili problemi. Un avviso di colore arancione indica che si verificano errori nelle richieste, visualizzazioni di pagina o chiamate di dipendenza. Il rosso indica una percentuale di errore superiore al 5%. Se si desidera tooadjust queste soglie, aprire Opzioni.

![icone di errore](./media/app-insights-app-map/04.png)

Vengono visualizzati anche avvisi attivi: 

![avvisi attivi](./media/app-insights-app-map/05.png)

Se si usa SQL Azure, è presente un'icona che indica quando sono disponibili consigli su come è possibile migliorare le prestazioni. 

![Suggerimento di Azure](./media/app-insights-app-map/06.png)

Fare clic su qualsiasi icona tooget ulteriori dettagli:

![Suggerimento di Azure](./media/app-insights-app-map/07.png)

## <a name="diagnostic-click-through"></a>Diagnostica tramite clic
Ogni nodo hello nella mappa hello offre destinazione click-through per la diagnostica. opzioni di Hello variano a seconda di tipo hello del nodo hello.

![opzioni server](./media/app-insights-app-map/09.png)

Per i componenti sono ospitati in Azure, le opzioni di hello includono toothem collegamenti diretti.

## <a name="filters-and-time-range"></a>Filtri e intervallo di tempo
Per impostazione predefinita, la mappa hello riepiloga i dati di hello tutti disponibili per l'intervallo di tempo scelto hello. Ma è possibile filtrare i nomi delle operazioni solo a specifici di tooinclude o dipendenze.

* Nome dell'operazione: include sia le visualizzazioni pagina che i tipi di richiesta lato server. Con questa opzione, hello mappa Mostra hello KPI nel nodo di hello client/server-side per le operazioni di hello selezionato solo. Mostra dipendenze hello chiamate nel contesto di hello di tali operazioni specifiche.
* Nome di base della dipendenza: sono incluse le dipendenze di browser AJAX hello e le dipendenze sul lato server. Se si segnala telemetria dipendenza personalizzata con hello TrackDependency API, verranno visualizzate anche qui. È possibile selezionare hello dipendenze tooshow nella mappa hello. Attualmente questa selezione non filtra richieste sul lato server hello o visualizzazioni di pagina sul lato client hello.

![impostare i filtri](./media/app-insights-app-map/11.png)

## <a name="save-filters"></a>Salvare i filtri
toosave hello i filtri applicati, hello pin filtrati visualizzazione su un [dashboard](app-insights-dashboards.md).

![PIN toodashboard](./media/app-insights-app-map/12.png)

## <a name="error-pane"></a>Riquadro dell'errore
Quando si fa clic su un nodo nella mappa hello, un riquadro di errore viene visualizzato sul lato destro di hello Riepilogo errori relativi a tale nodo. Gli errori vengono prima raggruppati per ID operazione e quindi per ID del problema.

![Riquadro dell'errore](./media/app-insights-app-map/error-pane.png)

Facendo clic su un errore accetta toohello istanza più recente di questo tipo di errore.

## <a name="resource-health"></a>Integrità delle risorse
Per alcuni tipi di risorsa, l'integrità delle risorse viene visualizzato nella parte superiore di hello del riquadro errore hello. Ad esempio, facendo clic su un nodo SQL verranno visualizzati integrità database hello e eventuali avvisi che sono stati attivati.

![Integrità delle risorse](./media/app-insights-app-map/resource-health.png)

È possibile scegliere le metriche hello risorsa nome tooview Panoramica standard per tale risorsa.

## <a name="end-to-end-system-app-maps"></a>Mappe delle app del sistema end-to-end

*È necessaria la versione 2.3 o successive di SDK*

Se l'applicazione dispone di diversi componenti, ad esempio, un servizio back-end inoltre toohello web app, quindi si può visualizzare tutte nel mapping di un'applicazione integrata.

![impostare i filtri](./media/app-insights-app-map/multi-component-app-map.png)

mappa app Hello consente di trovare i nodi del server seguendo le chiamate di dipendenza HTTP inviate tra i server con hello che Application Insights SDK installato. Ogni risorsa di Application Insights presuppone toocontain un server.

### <a name="multi-role-app-map-preview"></a>Mappa con app multi-ruolo (anteprima)

Hello anteprima app Multiruolo mappa consente toouse hello app mappa con più server, l'invio di dati toohello stessa risorsa di Application Insights / chiave di strumentazione. I server nella mappa hello sono segmentati per proprietà cloud_RoleName hello sugli elementi di dati di telemetria. Impostare *con più ruoli applicazione mappa* troppo*su* da hello anteprime pannello tooenable questa configurazione.

Questo approccio è preferibile in un'applicazione di micro-services o in altri scenari in cui si desidera che gli eventi toocorrelate tra più server all'interno di una singola risorsa di Application Insights.

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="feedback"></a>Commenti e suggerimenti
Fornire commenti e suggerimenti tramite l'opzione commenti e suggerimenti portale hello.

![Immagine MapLink-1](./media/app-insights-app-map/13.png)


## <a name="next-steps"></a>Passaggi successivi

* [Portale di Azure](https://portal.azure.com)
