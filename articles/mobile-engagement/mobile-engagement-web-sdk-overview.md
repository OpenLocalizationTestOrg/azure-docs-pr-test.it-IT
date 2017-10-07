---
title: Panoramica di Mobile Engagement Web SDK aaaAzure | Documenti Microsoft
description: "Hello procedure per hello Web SDK e gli aggiornamenti più recenti per Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 5bbc2fda-0f3f-43d0-a73d-0f2c0f8dc25b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 10/18/2016
ms.author: piyushjo
ms.openlocfilehash: 9e60a232b5eb2c41c405041a88e09d7137563513
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-web-sdk"></a>Azure Mobile Engagement Web SDK
Iniziare da qui per tutti hello informazioni dettagliate su come toointegrate Azure Mobile Engagement in un'app web. Se si desidera toogive è un blocco try prima di iniziare con la propria app web, vedere il nostro [esercitazione di 15 minuti](mobile-engagement-web-app-get-started.md).

## <a name="integration-procedures"></a>Procedure di integrazione
1. Informazioni su [come toointegrate Mobile Engagement in app web](mobile-engagement-web-integrate-engagement.md).
2. Per l'implementazione del piano di tag, informazioni su [come toouse hello avanzate tag API nelle applicazioni web di Mobile Engagement](mobile-engagement-web-use-engagement-api.md).

## <a name="release-notes"></a>Note sulla versione
### <a name="202-10182016"></a>2.0.2 (18/10/2016)
* Correzione di un problema di arresto anomalo nell'esplorazione privata (Safari).
* Correzione di un problema di arresto anomalo nei browser con cookie disabilitati.

Per tutte le versioni, vedere hello [completare note sulla versione](mobile-engagement-web-release-notes.md).

## <a name="upgrade-procedures"></a>Procedure di aggiornamento
### <a name="upgrade-from-121-too200"></a>Eseguire l'aggiornamento da 1.2.1 too2.0.0
Hello nelle sezioni seguenti descrivono come toomigrate un'integrazione di Mobile Engagement Web SDK dal servizio Capptain hello, offerto Capptain SAS, app di Azure Mobile Engagement tooan. Se si esegue la migrazione da una versione precedente di 1.2.1, consultare hello Capptain sito Web toomigrate too1.2.1 prima e quindi applicare hello seguire le procedure seguenti.

Questa versione di hello Mobile Engagement Web SDK non supporta TV Smart Samsung, Opera TV, webOS o funzionalità Reach hello.

> [!IMPORTANT]
> Capptain e Azure Mobile Engagement non sono hello stesso servizio e seguire le procedure seguenti hello evidenzia solo come toomigrate hello app client. Migrazione hello Mobile Engagement Web SDK nell'applicazione hello non eseguirà la migrazione dei dati da un server di Mobile Engagement Capptain tooa server.
> 
> 

#### <a name="javascript-files"></a>File JavaScript
Sostituisci hello file capptain-sdk.js con hello azure engagement.js di file e aggiornare di conseguenza le importazioni di script.

#### <a name="remove-capptain-reach"></a>Rimuovere Capptain Reach
Questa versione di hello Mobile Engagement Web SDK non supporta funzionalità di copertura hello. Se è stata integrata Capptain Reach nell'applicazione, è necessario tooremove è.

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

#### <a name="remove-deprecated-apis"></a>Rimuovere API deprecate
Alcune API da Capptain sono deprecati in hello Web di Mobile Engagement SDK.

Rimuovere qualsiasi toohello chiamate API seguenti: `agent.connect`, `agent.disconnect`, `agent.pause`, e `agent.sendMessageToDevice`.

Rimuovere uno dei seguenti callback dalla configurazione Capptain hello: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, e `onPushMessageReceived`.

#### <a name="configuration"></a>Configurazione
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

#### <a name="javascript-apis"></a>API JavaScript
oggetto JavaScript globale Hello `window.capptain` è stato rinominato `window.azureEngagement`, ma è possibile utilizzare hello `window.engagement` alias per le chiamate API. Non è possibile utilizzare questa configurazione di alias toodefine hello SDK.

Ad esempio, `capptain.deviceId` diventa `engagement.deviceId`, `capptain.agent.startActivity` diventa `engagement.agent.startActivity` e così via.

Se è già stata integrata una versione precedente di hello Azure Mobile Engagement Web SDK nell'applicazione, consultare l'articolo sulla [procedure aggiornamento](mobile-engagement-web-upgrade-procedure.md).

