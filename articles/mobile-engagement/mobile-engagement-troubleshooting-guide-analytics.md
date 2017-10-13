---
title: Guida alla risoluzione dei problemi di Azure Mobile Engagement - Analytics
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
ms.openlocfilehash: e30c9ac0a8421ffcf4fc3e2548cfd7ac49701900
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="troubleshooting-guide-for-analytics-monitoring-segmentation-and-dashboard-issues"></a>Guida alla risoluzione dei problemi relativi ad analisi, monitoraggio, segmentazione e dashboard
Di seguito sono indicati possibili problemi che relativi al modo in cui Azure Mobile Engagement raccoglie informazioni su applicazioni, dispositivi e utenti.

## <a name="missingdelayed-information"></a>Informazioni mancanti o in ritardo
### <a name="issue"></a>Problema
* Informazioni visualizzate in ritardo nell'analisi, nella segmentazione o nel dashboard.
* Informazioni mancanti nel monitoraggio.
* Informazioni mancanti nell'analisi, nella segmentazione o nel dashboard.
* Raggiungimento dei limiti di segmentazione.

### <a name="causes"></a>Cause
* È possibile usare le API Analytics, Monitor e Segments per verificare se i dati che non vengono visualizzati nell'interfaccia utente sono visibili tramite le API.
* Se Azure Mobile Engagement SDK non è stato integrato correttamente nell'app, non sarà possibile visualizzare le informazioni nell'analisi, nella segmentazione, nel monitoraggio o nei dashboard.
* Una volta creati, i segmenti possono essere soltanto "clonati" (copiati) o "distrutti" (eliminati). I segmenti possono contenere solo 10 criteri.
* Il modo migliore per verificare le informazioni non visualizzate nel monitoraggio consiste nel configurare un dispositivo di test, disinstallare l'app dal dispositivo e/o reinstallarla.
* Le informazioni vengono aggiornate ogni 24 ore per l'analisi, la segmentazione o i dashboard.
* È possibile che le informazioni nei nuovi segmenti vengano visualizzate solo dopo 24 ore dal momento della creazione, anche se il segmento si basa su informazioni precedenti.
* Se i dati di analisi presenti nell'interfaccia utente vengono filtrati, è possibile visualizzare tutti gli esempi di questo tipo, indipendentemente dalla versione dell'app. Ad esempio, se si filtrano gli "arresti anomali" in base al nome, verranno visualizzati quelli delle versioni 1 e 2 dell'app.
* Il periodo per l'analisi si basa sulla data presente nelle impostazioni del dispositivo dell'utente. Pertanto, se nel telefono di un utente la data è impostata in modo errato, è possibile che venga visualizzato il periodo errato.
* Non vengono registrati dati sul lato server quando si usa il pulsante per "testare" i push, vengono registrati solo i dati per le campagne di push reali.

## <a name="cant-locate-items-in-ui"></a>Impossibile individuare elementi nell'interfaccia utente
### <a name="issue"></a>Problema
* Impossibile creare segmenti in base a determinati criteri di tag sulle informazioni dell'app integrati o personalizzati.
* Impossibile trovare criteri di tag sulle informazioni dell'app integrati o personalizzati nell'analisi, nel monitoraggio o nei dashboard.
* Impossibile interpretare i dati presenti nell'analisi, nel monitoraggio, nella segmentazione o nei dashboard.

### <a name="causes"></a>Cause
* Alcuni elementi integrati e tag sulle informazioni dell'app sono disponibili soltanto come criteri di inserimento, ma non possono essere aggiunti a un segmento o essere visibili nell'analisi, nel monitoraggio o nel dashboard. 
* Nel caso di elementi integrati e tag sulle informazioni dell'app che non possono essere aggiunti a un segmento, sarà necessario impostare un elenco di criteri di destinazione per ogni campagna, in modo che eseguano la stessa funzione di selezione della destinazione basata su un segmento.
* Visualizzare i menu di scelta rapida nelle sezioni di analisi, monitoraggio e dashboard dell'interfaccia utente di Azure Mobile Engagement per altre informazioni di supporto e procedure.

## <a name="crash-troubleshooting"></a>Risoluzione dei problemi di arresto anomalo
### <a name="issue"></a>Problema
* Gli arresti anomali dell'applicazione vengono visualizzati nelle sezioni di analisi, monitoraggio o dashboard.

### <a name="causes"></a>Cause
* Per risolvere i problemi di arresto anomalo dell'applicazione visualizzati nelle sezioni di analisi, monitoraggio o dashboard, controllare le note sulla versione e verificare la presenza di problemi noti nelle versioni precedenti dell'SDK.
* Per risolvere altri problemi di arresto anomalo dell'app, eseguire un evento da un dispositivo di test su cui è installata l'app, quindi cercare l'ID dispositivo nella sezione "Monitor - Eventi" dell'interfaccia utente di Azure Mobile Engagement. Quindi, eseguire l'evento che causa l'arresto anomalo dell'applicazione e cercare altre informazioni nella sezione "Monitor - Arresto anomalo" dell'interfaccia utente di Azure Mobile Engagement. 

