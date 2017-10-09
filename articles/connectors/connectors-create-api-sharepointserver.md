---
title: hello aaaUse connettore Server SharePoint nelle App logica | Documenti Microsoft
description: Introduzione all'uso hello hello connettore Server SharePoint in App per la logica
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 0238a060-d592-4719-b7a2-26064c437a1a
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 3b814f42611e4971ff5c94ae3b021829217911dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-sharepoint-connector"></a>Iniziare con il connettore di SharePoint hello
Hello connettore di SharePoint fornisce un modo toowork con gli elenchi in SharePoint.

Creare prima di tutto un'app per la logica. Vedere [Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="create-a-connection-toosharepoint"></a>Creare una connessione tooSharePoint
toouse hello connettore di SharePoint, creare innanzitutto un **connessione** quindi fornire i dettagli di hello per queste proprietà: 

| Proprietà | Obbligatorio | Descrizione |
| --- | --- | --- |
| Token |Sì |Fornire le credenziali di SharePoint |

tooconnect troppo**SharePoint**, immettere il tooSharePoint identità (nome utente e password, le credenziali della smart card e così via). Una volta che si è stati autenticati, è possibile procedere connettore di SharePoint hello toouse nell'app logica. 

Mentre nella finestra di progettazione di hello dell'app logica, seguire questi toosign passaggi in connessioni di SharePoint toocreate hello **connessione** per l'utilizzo nell'app logica:

1. Immettere SharePoint nella casella di ricerca hello e attendere che tutte le voci con SharePoint nel nome hello tooreturn ricerca hello:   
   ![Configurare SharePoint][1]  
2. Selezionare **SharePoint - Quando un file viene creato**   
3. Selezionare **Accedi tooSharePoint**:   
   ![Configurare SharePoint][2]    
4. Fornire il toosign le credenziali di SharePoint in tooauthenticate con SharePoint   
   ![Configurare SharePoint][3]     
5. Al termine dell'autenticazione hello sarà reindirizzato tooyour logica app toocomplete, tramite la configurazione di SharePoint **quando viene creato un file** finestra di dialogo.          
   ![Configurare SharePoint][4]  
6. È quindi possibile aggiungere altre azioni che è necessario toocomplete app logica e i trigger.   
7. Salvare il lavoro selezionando **salvare** sulla barra dei menu hello precedente.  

## <a name="connector-specific-details"></a>Dettagli specifici del connettore

Visualizzare tutti i trigger e azioni definite in swagger hello e anche eventuali limiti di hello [dettagli connettore](/connectors/sharepoint/).

## <a name="more-connectors"></a>Altri connettori
Tornare indietro toohello [elenco API](apis-list.md).

[1]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig1.png  
[2]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig2.png 
[3]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig3.png
[4]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig4.png
[5]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig5.png
