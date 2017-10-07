---
title: procedure di aggiornamento di Mobile Engagement Web SDK aaaAzure | Documenti Microsoft
description: "Hello procedure per hello Web SDK e gli aggiornamenti più recenti per Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a20529b4-ec8d-4503-8ae9-09b5f0846d5b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 06/07/2016
ms.author: piyushjo
ms.openlocfilehash: a2df65904c6b56584ce6588ed26a9b79f3aa27ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-web-sdk-upgrade-procedures"></a>Procedure di aggiornamento di Azure Mobile Engagement SDK per Web
Se è già stata integrata una versione precedente di hello Azure Mobile Engagement Web SDK nell'applicazione web, è necessario hello tooconsider seguenti punti quando si aggiorna hello SDK.

Se non si è eseguito più versioni di hello Mobile Engagement Web SDK, potrebbe essere toocomplete varie procedure durante il processo di aggiornamento hello. Ad esempio, se si esegue la migrazione da 1.4.0 too1.6.0, primo seguire hello procedure tooupgrade da 1.4.0 too1.5.0. Seguire quindi hello procedure tooupgrade da 1.5.0 too1.6.0.

Qualsiasi versione di aggiornamento da, sostituire le versioni precedenti del file di hello azure-engagement.js con hello l'ultima versione del file hello.

## <a name="upgrade-from-121-too200"></a>Eseguire l'aggiornamento da 1.2.1 too2.0.0
In questa sezione viene descritto come toomigrate un'integrazione di Mobile Engagement Web SDK dal servizio Capptain hello, offerto Capptain SAS, app di Azure Mobile Engagement tooan. Se si esegue la migrazione da una versione precedente,. consultare hello Capptain sito Web toofirst too1.2.1 di eseguire la migrazione e quindi applicare hello seguire le procedure seguenti.

Questa versione di hello Mobile Engagement Web SDK non supporta TV Smart Samsung, Opera TV, webOS o funzionalità Reach hello.

> [!IMPORTANT]
> Capptain e Azure Mobile Engagement non sono hello stesso servizio. procedura Hello evidenzia solo come toomigrate hello app client. Migrazione hello Mobile Engagement Web SDK nell'applicazione hello non eseguirà la migrazione dei dati da un server di Mobile Engagement Capptain tooa server.
> 
> 

### <a name="javascript-files"></a>File JavaScript
Sostituisci hello file capptain-sdk.js con hello azure engagement.js di file e aggiornare di conseguenza le importazioni di script.

### <a name="remove-capptain-reach"></a>Rimuovere Capptain Reach
Questa versione di hello Mobile Engagement Web SDK non supporta funzionalità di copertura hello. Se Capptain Reach è integrato nell'applicazione, è necessario tooremove è.

Rimuovere hello raggiungere CSS importazione dalla pagina ed eliminare file con estensione CSS correlati hello (capptain-reach.css, per impostazione predefinita).

Eliminare hello seguente di portata risorse: hello Chiudi immagine (capptain-close.png, per impostazione predefinita) e l'icona del marchio di hello (capptain--icona di notifica, per impostazione predefinita).

Rimuovere hello raggiungere dell'interfaccia utente per le notifiche nell'applicazione. layout predefinito Hello è simile al seguente:

    <!-- capptain notification -->
    <div id="capptain_notification_area" class="capptain_category_default">
      <div class="icon">
        <img src="capptain-notification-icon.png" alt="icon" />
      </div>
      <div class="content">
        <div class="title" id="capptain_notification_title"></div>
        <div class="message" id="capptain_notification_message"></div>
      </div>
      <div id="capptain_notification_image"></div>
      <div>
        <button id="capptain_notification_close">Close</button>
      </div>
    </div>

Rimuovere hello raggiungere dell'interfaccia utente per i sondaggi e gli annunci di testo e web. layout predefinito Hello è simile al seguente:

    <div id="capptain_overlay" class="capptain_category_default">
      <button id="capptain_overlay_close">x</button>
      <div id="capptain_overlay_title"></div>
      <div id="capptain_overlay_body"></div>
      <div id="capptain_overlay_poll"></div>
      <div id="capptain_overlay_buttons">
        <button id="capptain_overlay_exit"></button>
        <button id="capptain_overlay_action"></button>
      </div>
    </div>

Rimuovere hello `reach` oggetto dalla configurazione, se presente. L'aspetto sarà simile al seguente:

    window.capptain = {
      [...]
      reach: {
        [...]
      }
    }

Rimuovere eventuali altre personalizzazioni di Reach, ad esempio le categorie.

### <a name="remove-deprecated-apis"></a>Rimuovere API deprecate
Alcune API da Capptain sono deprecati in hello Web di Mobile Engagement SDK.

Rimuovere qualsiasi toohello chiamate API seguenti: `agent.connect`, `agent.disconnect`, `agent.pause`, e `agent.sendMessageToDevice`.

Rimuovere tutte le istanze di segue callback dalla configurazione Capptain hello: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, e `onPushMessageReceived`.

### <a name="configuration"></a>Configurazione
Engagement mobile Usa una connessione stringa tooconfigure SDK identificatori, ad esempio, identificatore dell'applicazione hello.

Sostituire l'ID dell'applicazione hello con la stringa di connessione. Si noti l'oggetto globale hello di hello configurazione SDK cambierà da `capptain` troppo`azureEngagement`.

Prima della migrazione:

    window.capptain = {
      appId: ...,
      [...]
    };

Dopo la migrazione:

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      [...]
    };

stringa di connessione Hello per l'applicazione viene visualizzato nel portale di Azure hello.

### <a name="javascript-apis"></a>API JavaScript
oggetto JavaScript globale Hello `window.capptain` è stato rinominato `window.azureEngagement` ma è possibile utilizzare hello `window.engagement` alias per le chiamate API. Non è possibile utilizzare configurazione di hello alias toodefine hello SDK.

Ad esempio, `capptain.deviceId` diventa `engagement.deviceId`, `capptain.agent.startActivity` diventa `engagement.agent.startActivity` e così via.

