---
title: aaaAzure Mobile Engagement Troubleshooting Guide - Analitica
description: Risoluzione dei problemi relativi ad analisi, monitoraggio, segmentazione e dashboard in Azure Mobile Engagement
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 04a7020a-ad74-4491-be69-0bd574890029
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 69c6ff8f5c8540f8ba8b85b9ffec55acc59329fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-analytics-monitoring-segmentation-and-dashboard-issues"></a>Guida alla risoluzione dei problemi relativi ad analisi, monitoraggio, segmentazione e dashboard
di seguito Hello sono possibili problemi che possono verificarsi con Azure Mobile Engagement come raccoglie le informazioni sulle applicazioni e dispositivi e utenti.

## <a name="missingdelayed-information"></a>Informazioni mancanti o in ritardo
### <a name="issue"></a>Problema
* Informazioni visualizzate in ritardo nell'analisi, nella segmentazione o nel dashboard.
* Informazioni mancanti nel monitoraggio.
* Informazioni mancanti nell'analisi, nella segmentazione o nel dashboard.
* Raggiungimento dei limiti di segmentazione.

### <a name="causes"></a>Cause
* È possibile utilizzare hello API Analitica, API di monitoraggio, e API segmenti toosee se tutti i dati mancano hello dell'interfaccia utente è visibile attraverso le API di hello.
* Se correttamente hello Azure Mobile Engagement SDK non è integrato nell'app quindi non sarà in grado di toosee informazioni in hello Analitica, segmentazione, monitoraggio o dashboard.
* Una volta creati, i segmenti possono essere soltanto "clonati" (copiati) o "distrutti" (eliminati). I segmenti possono contenere solo 10 criteri.
* tootest modo migliore di Hello mancano le informazioni di monitoraggio è un dispositivo di test toosetup, disinstallare e/o reinstallare hello app sul dispositivo di test hello.
* Le informazioni vengono aggiornate ogni 24 ore per l'analisi, la segmentazione o i dashboard.
* Informazioni contenute in nuovi segmenti potrebbe non essere visualizzati fino a 24 ore dopo averli creati, anche se il segmento hello è in base alle informazioni precedenti.
* Filtrare i dati analitica in hello dell'interfaccia utente visualizzerà tutti gli esempi di questo tipo, indipendentemente dalla versione di hello dell'app (ad esempio Ad esempio, se si filtrano gli "arresti anomali" in base al nome, verranno visualizzati quelli delle versioni 1 e 2 dell'app.
* Hello periodo di tempo per Analitica è basato sulla data hello dalle impostazioni del dispositivo degli utenti hello, pertanto un utente il cui telefono è data hello impostato in modo errato può visualizzati nella hello errato periodo di tempo.
* Inserisce alcun lato server vengono registrati i dati quando si utilizza il pulsante hello troppo "non test", i dati vengono registrati solo per le campagne push reale.

## <a name="cant-locate-items-in-ui"></a>Impossibile individuare elementi nell'interfaccia utente
### <a name="issue"></a>Problema
* Impossibile creare segmenti in base a determinati criteri di tag sulle informazioni dell'app integrati o personalizzati.
* Impossibile trovare criteri di tag sulle informazioni dell'app integrati o personalizzati nell'analisi, nel monitoraggio o nei dashboard.
* Impossibile interpretare i dati di hello in Analitica, il monitoraggio, segmentazione o dashboard.

### <a name="causes"></a>Cause
* Alcuni compilati negli elementi e informazioni sull'app tag sono disponibili solo come criteri di push, ma non possono essere aggiunti tooa segmento o visibili da Analitica, monitoraggio o Dashboard. 
* Per incorporate negli elementi e informazioni sull'app tag che non può essere aggiunto tooa segmento, sarà necessario toosetup elenco di criteri di ogni hello tooperform campagna stessa funzione come destinazione in base a un segmento di destinazione.
* Vedere i menu di scelta rapida hello nelle sezioni Analitica, monitoraggio, segmentazione e i dashboard di hello di hello dell'interfaccia utente di Azure Mobile Engagement per ulteriori informazioni e come tooinformation.

## <a name="crash-troubleshooting"></a>Risoluzione dei problemi di arresto anomalo
### <a name="issue"></a>Problema
* Gli arresti anomali dell'applicazione vengono visualizzati nelle sezioni di analisi, monitoraggio o dashboard.

### <a name="causes"></a>Cause
* Blocchi applicazione tootroubleshoot visualizzati nel Dashboard, monitoraggio o Analitica rendere note sulla versione di hello toocheck che per i problemi noti con le versioni precedenti di hello SDK.
* toofurther di risolvere i problemi applicazione arresti anomali del sistema esegue un evento da un dispositivo di test con l'applicazione installata e cercare l'ID dispositivo nella sezione hello "eventi – monitoraggio" hello dell'interfaccia utente di Azure Mobile Engagement. Quindi eseguire hello evento che causa l'applicazione toocrash e cercare informazioni aggiuntive in hello "Monitoraggio – Crash" sezione di hello dell'interfaccia utente di Azure Mobile Engagement. 

