---
title: un ritardo nell'App per la logica aaaAdd | Documenti Microsoft
description: Panoramica di hello ritardo e il ritardo-fino a quando le azioni e come toouse con un'app per la logica di Azure.
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 915f48bf-3bd8-4656-be73-91a941d0afcd
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: e5bc9d639adbddc01ee0f6a4c68716f586d4344a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-delay-and-delay-until-actions"></a>Introduzione a hello ritardo e il ritardo-fino a quando le azioni
Tramite il ritardo di hello e "ritardo-fino a quando non" azioni, è possibile completare gli scenari di flusso di lavoro.

Ad esempio, è possibile:

* Attendere l'aggiornamento toosend un giorno della settimana lo stato tramite posta elettronica.
* Ritardo del flusso di lavoro hello fino a quando una chiamata HTTP è ora toofinish prima di ripresa e recuperare i risultati di hello.

tooget avviato utilizzando l'azione di ritardo hello in un'app di logica, vedere [creare un'app di logica](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-hello-delay-actions"></a>Utilizzare le azioni di ritardo hello
Un'azione è un'operazione che viene eseguita dal flusso di lavoro hello è definito in un'app di logica. [Altre informazioni sulle azioni](connectors-overview.md).

Di seguito è riportata una sequenza di esempio della modalità di passaggio toouse un ritardo in un'app di logica:

1. Dopo l'aggiunta di un trigger, fare clic su **nuovo passaggio** tooadd un'azione.
2. Cercare **ritardo** toobring le azioni di ritardo hello. In questo esempio si selezionerà **Ritarda**.
   
    ![Azioni di ritardo](./media/connectors-native-delay/using-action-1.png)
3. Completa eventuali di ritardo di hello azione proprietà tooconfigure hello.
   
    ![Configurazione del ritardo](./media/connectors-native-delay/using-action-2.png)
4. Fare clic su **salvare** toopublish e attivare hello logica app.

## <a name="action-details"></a>Informazioni dettagliate sulle azioni
i trigger di ricorrenza Hello è hello seguenti proprietà che possono essere configurate.

### <a name="delay-action"></a>Azione Ritarda
Questo hello ritardi azione eseguita per un determinato intervallo di tempo.
Un asterisco (*) indica che è un campo obbligatorio.

| Nome visualizzato | Nome proprietà | Descrizione |
| --- | --- | --- |
| Conteggio* |count |numero di Hello di toodelay unità di tempo |
| Unità* |unit |unità di Hello di tempo: `Second`, `Minute`, `Hour`, o`Day` |

<br>

### <a name="delay-until-action"></a>Azione Ritarda fino a
Questa azione consente di ritardare hello eseguito fino a quando una data/ora specificata.
Un asterisco (*) indica che è un campo obbligatorio.

| Nome visualizzato | Nome proprietà | Descrizione |
| --- | --- | --- |
| Anno* |timestamp |Hello anno toodelay finché (GMT) |
| Mese* |timestamp |Hello mese toodelay finché (GMT) |
| Giorno* |timestamp |Hello toodelay giorno finché (GMT) |

<br>

## <a name="next-steps"></a>Passaggi successivi
A questo punto, provare a piattaforma hello e [creare un'app di logica](../logic-apps/logic-apps-create-a-logic-app.md). È possibile esplorare altri connettori disponibile in App per la logica di hello esaminando il nostro [elenco API](apis-list.md).

