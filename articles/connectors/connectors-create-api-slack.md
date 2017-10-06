---
title: Ciao aaaUse Slack connettore App per la logica di Azure | Documenti Microsoft
description: Connettersi tooSlack nelle app di logica
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 234cad64-b13d-4494-ae78-18b17119ba24
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 6599d7b69d2147425c9fab978c5d0f93e5605f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-slack-connector"></a>Iniziare con connettore Slack hello
Slack è uno strumento di comunicazione del team, che riunisce tutte le comunicazioni del team in un'unica posizione immediatamente disponibile e individuabile in qualsiasi luogo. 

Creare prima di tutto un'app per la logica. Vedere [Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="create-a-connection-tooslack"></a>Creare una connessione tooSlack
connettore di Slack hello toouse, creare innanzitutto un **connessione** quindi fornire i dettagli di hello per queste proprietà: 

| Proprietà | Obbligatorio | Descrizione |
| --- | --- | --- |
| Token |Sì |Fornire le credenziali di Slack |

Seguire questi passaggi toosign in Slack e la configurazione completa hello di hello Slack **connessione** nell'app logica:

1. Selezionare **Ricorrenza**
2. Selezionare una **frequenza** e immettere un **intervallo**
3. Selezionare **Aggiungi un'azione**  
   ![Configurare Slack][1]  
4. Immettere il margine di flessibilità nella casella di ricerca hello e attendere hello ricerca tooreturn tutte le voci con Slack nel nome hello
5. Selezionare **Slack - Invia messaggio**
6. Selezionare **Accedi tooSlack**:  
   ![Configurare Slack][2]
7. Fornire il toosign Slack credenziali in un'applicazione hello tooauthorize    
   ![Configurare Slack][3]  
8. Sarà nella pagina di accesso reindirizzato tooyour dell'organizzazione. **Autorizzare** toointeract Slack con l'app logica:      
   ![Configurare Slack][5] 
9. Al termine dell'autorizzazione hello sarà reindirizzato tooyour logica app toocomplete, configurando hello **margine di flessibilità: ottenere tutti i messaggi** sezione. Aggiungere altri trigger e azioni necessari.  
   ![Configurare Slack][6]
10. Salvare il lavoro selezionando **salvare** sulla barra dei menu hello precedente.

## <a name="connector-specific-details"></a>Dettagli specifici del connettore

Visualizzare tutti i trigger e azioni definite in swagger hello e anche eventuali limiti di hello [dettagli connettore](/connectors/slack/).

## <a name="more-connectors"></a>Altri connettori
Tornare indietro toohello [elenco API](apis-list.md).

[1]: ./media/connectors-create-api-slack/connectionconfig1.png
[2]: ./media/connectors-create-api-slack/connectionconfig2.png 
[3]: ./media/connectors-create-api-slack/connectionconfig3.png
[4]: ./media/connectors-create-api-slack/connectionconfig4.png
[5]: ./media/connectors-create-api-slack/connectionconfig5.png
[6]: ./media/connectors-create-api-slack/connectionconfig6.png
