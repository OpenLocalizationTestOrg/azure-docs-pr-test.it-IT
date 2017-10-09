---
title: aaaExploring HockeyApp dati in Azure Application Insights | Documenti Microsoft
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
ms.openlocfilehash: ed7cf99b48f5ec78d6b401bb954cfcd014b9d1f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="exploring-hockeyapp-data-in-application-insights"></a>Esplorazione dei dati HockeyApp in Application Insights
[HockeyApp](https://azure.microsoft.com/services/hockeyapp/) hello consiglia di piattaforma per il monitoraggio in tempo reale App desktop e mobile. Da HockeyApp, è possibile inviare personalizzato e di traccia dell'utilizzo di dati di telemetria toomonitor e facilitare la diagnosi (nei dati di arresto anomalo di addizione toogetting). Questo flusso di dati di telemetria è possibile eseguire query tramite hello avanzato [Analitica](app-insights-analytics.md) funzionalità di [Azure Application Insights](app-insights-overview.md). È inoltre possibile [esportare hello personalizzato e i dati di telemetria di traccia](app-insights-export-telemetry.md). tooenable queste funzionalità, è possibile impostare un bridge che inoltra i dati personalizzati di HockeyApp tooApplication Insights.

## <a name="hello-hockeyapp-bridge-app"></a>app HockeyApp Bridge Hello
Hello HockeyApp Bridge App è una funzionalità principale hello che consente di tooaccess la telemetria di traccia in Application Insights tramite hello Analitica HockeyApp personalizzati e le funzionalità di esportazione continua. Eventi personalizzati e di traccia raccolti da HockeyApp dopo la creazione di hello di hello HockeyApp Bridge App sarà accessibili da queste funzionalità. Di seguito viene illustrato come tooset di una di queste App Bridge.

In HockeyApp aprire Account Settings (Impostazioni account), [API Tokens](https://rink.hockeyapp.net/manage/auth_tokens)(Token API). Creare un token oppure usarne uno esistente. diritti minimi Hello necessarie sono "di sola lettura". Eseguire una copia di hello API token.

![Ottenere un token API HockeyApp](./media/app-insights-hockeyapp-bridge-app/01.png)

Portale di Microsoft Azure aprire hello e [creare una risorsa di Application Insights](app-insights-create-new-resource.md). Impostare il tipo di applicazione troppo "Applicazione bridge HockeyApp":

![Nuova risorsa di Application Insights](./media/app-insights-hockeyapp-bridge-app/02.png)

Non devi tooset un nome, questo verrà impostato automaticamente dal nome HockeyApp hello.

Hello HockeyApp bridge campi vengono visualizzati. 

![Immettere i campi dell'app bridge](./media/app-insights-hockeyapp-bridge-app/03.png)

Immettere il token di HockeyApp hello annotati in precedenza. Questa azione consente di popolare menu a discesa di "HockeyApp applicazione" hello con tutte le applicazioni HockeyApp. Selezionare hello uno desiderata toouse e resto hello completo di campi di hello. 

Aprire una nuova risorsa hello. 

Si noti che i dati di hello richiede un po' di tempo toostart propagazione.

![Risorsa di Application Insights in attesa dei dati](./media/app-insights-hockeyapp-bridge-app/04.png)

La procedura è terminata. Dati personalizzati e di traccia raccolti nell'applicazione instrumentata HockeyApp da questo punto in avanti sono anche disponibile tooyou in hello Analitica e funzionalità esportazione continua di Application Insights.

Brevemente esaminare ognuno di questi tooyou ora disponibili le funzionalità.

## <a name="analytics"></a>Analytics
Analitica è uno strumento potente per ad hoc l'esecuzione di query dei dati, consentendo toodiagnose e analizza i dati di telemetria e individua rapidamente le cause principali e modelli.

![Analytics](./media/app-insights-hockeyapp-bridge-app/05.png)

* [Altre informazioni su Analisi](app-insights-analytics-tour.md)

## <a name="continuous-export"></a>Esportazione continua
Tooexport consente l'esportazione continua dei dati in un contenitore di archiviazione Blob di Azure. È molto utile se occorre tookeep i dati per più di periodo di memorizzazione hello attualmente offerto da Application Insights. È possibile mantenere i dati di hello nell'archiviazione blob, convertirlo in un Database SQL o i preferito soluzione di data warehousing.

[Altre informazioni su Esportazione continua](app-insights-export-telemetry.md)

## <a name="next-steps"></a>Passaggi successivi
* [Applicare tooyour Analitica dei dati](app-insights-analytics-tour.md)

