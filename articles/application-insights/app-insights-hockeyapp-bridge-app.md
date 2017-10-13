---
title: Esplorazione dei dati HockeyApp in Application Insights | Microsoft Docs
description: Analizzare l'utilizzo e le prestazioni dell'app Azure con Application Insights.
services: application-insights
documentationcenter: windows
author: CFreemanwa
manager: carmonm
ms.assetid: 97783cc6-67d6-465f-9926-cb9821f4176e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: bwren
ms.openlocfilehash: 450ca10613d137393090578619f3766734d1d493
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="exploring-hockeyapp-data-in-application-insights"></a>Esplorazione dei dati HockeyApp in Application Insights
[HockeyApp](https://azure.microsoft.com/services/hockeyapp/) è la piattaforma consigliata per il monitoraggio di live app per desktop e per dispositivi mobili. Da HockeyApp è possibile inviare dati di telemetria di traccia e personalizzata per monitorare l'utilizzo e facilitare la diagnosi, oltre a ottenere dati di arresto anomalo. È possibile effettuare una query di questo flusso di dati di telemetria con la funzionalità [Analytics](app-insights-analytics.md) di [Azure Application Insights](app-insights-overview.md). È anche possibile [esportare i dati di telemetria di traccia e personalizzata](app-insights-export-telemetry.md). Per abilitare queste funzionalità, configurare un bridge che inoltra i dati HockeyApp personalizzati ad Application Insights.

## <a name="the-hockeyapp-bridge-app"></a>App bridge HockeyApp
L'app bridge HockeyApp è la funzionalità di base che consente di accedere ai dati di telemetria di traccia e personalizzata HockeyApp in Application Insights tramite le funzionalità Analisi ed Esportazione continua. Gli eventi di traccia e personalizzati raccolti da HockeyApp dopo la creazione dell'app bridge HockeyApp saranno accessibili da queste funzionalità. Ora verrà descritto come configurare una di queste app bridge.

In HockeyApp aprire Account Settings (Impostazioni account), [API Tokens](https://rink.hockeyapp.net/manage/auth_tokens)(Token API). Creare un token oppure usarne uno esistente. I diritti minimi necessari sono "Read Only" (Sola lettura). Eseguire una copia del token API.

![Ottenere un token API HockeyApp](./media/app-insights-hockeyapp-bridge-app/01.png)

Accedere al portale di Microsoft Azure e [creare una risorsa di Application Insights](app-insights-create-new-resource.md). Impostare il tipo di applicazione su "Applicazione bridge HockeyApp":

![Nuova risorsa di Application Insights](./media/app-insights-hockeyapp-bridge-app/02.png)

Non è necessario impostare un nome, verrà impostato automaticamente dal nome HockeyApp.

Verranno visualizzati i campi dell'applicazione bridge HockeyApp. 

![Immettere i campi dell'app bridge](./media/app-insights-hockeyapp-bridge-app/03.png)

Immettere il token HockeyApp annotato in precedenza. Questa azione consente di popolare il menu a discesa "Applicazione HockeyApp" con tutte le applicazioni HockeyApp. Selezionare l'applicazione da usare e compilare gli altri campi. 

Aprire la nuova risorsa. 

Si noti che l'avvio del flusso di dati richiede del tempo.

![Risorsa di Application Insights in attesa dei dati](./media/app-insights-hockeyapp-bridge-app/04.png)

La procedura è terminata. Da questo momento, i dati di traccia e personalizzati raccolti nell'app instrumentata HockeyApp saranno disponibili anche nelle funzionalità Analisi ed Esportazione continua di Application Insights.

Verranno brevemente esaminate queste funzionalità ora disponibili.

## <a name="analytics"></a>Analytics
Analisi è uno strumento avanzato per query ad hoc che consente di diagnosticare e analizzare i dati di telemetria e di individuare rapidamente cause radice e modelli.

![Analytics](./media/app-insights-hockeyapp-bridge-app/05.png)

* [Altre informazioni su Analisi](app-insights-analytics-tour.md)

## <a name="continuous-export"></a>Esportazione continua
Esportazione continua consente di esportare i dati in un contenitore dell'archivio BLOB di Azure. Ciò è molto utile se è necessario mantenere i dati per un tempo maggiore rispetto al periodo di conservazione attualmente offerto da Application Insights. È possibile conservare i dati nell'archivio BLOB ed elaborarli in un database SQL o nella soluzione di data warehousing scelta.

[Altre informazioni su Esportazione continua](app-insights-export-telemetry.md)

## <a name="next-steps"></a>Passaggi successivi
* [Applicare Analisi ai dati](app-insights-analytics-tour.md)

