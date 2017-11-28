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
# <a name="azure-mobile-engagement-web-sdk"></a><span data-ttu-id="75ece-103">Azure Mobile Engagement Web SDK</span><span class="sxs-lookup"><span data-stu-id="75ece-103">Azure Mobile Engagement Web SDK</span></span>
<span data-ttu-id="75ece-104">Iniziare da qui per tutti hello informazioni dettagliate su come toointegrate Azure Mobile Engagement in un'app web.</span><span class="sxs-lookup"><span data-stu-id="75ece-104">Start here for all hello details about how toointegrate Azure Mobile Engagement in a web app.</span></span> <span data-ttu-id="75ece-105">Se si desidera toogive è un blocco try prima di iniziare con la propria app web, vedere il nostro [esercitazione di 15 minuti](mobile-engagement-web-app-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="75ece-105">If you'd like toogive it a try before getting started with your own web app, see our [15-minute tutorial](mobile-engagement-web-app-get-started.md).</span></span>

## <a name="integration-procedures"></a><span data-ttu-id="75ece-106">Procedure di integrazione</span><span class="sxs-lookup"><span data-stu-id="75ece-106">Integration procedures</span></span>
1. <span data-ttu-id="75ece-107">Informazioni su [come toointegrate Mobile Engagement in app web](mobile-engagement-web-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="75ece-107">Learn [how toointegrate Mobile Engagement in your web app](mobile-engagement-web-integrate-engagement.md).</span></span>
2. <span data-ttu-id="75ece-108">Per l'implementazione del piano di tag, informazioni su [come toouse hello avanzate tag API nelle applicazioni web di Mobile Engagement](mobile-engagement-web-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="75ece-108">For tag plan implementation, learn [how toouse hello advanced Mobile Engagement tagging API in your web app](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="release-notes"></a><span data-ttu-id="75ece-109">Note sulla versione</span><span class="sxs-lookup"><span data-stu-id="75ece-109">Release notes</span></span>
### <a name="202-10182016"></a><span data-ttu-id="75ece-110">2.0.2 (18/10/2016)</span><span class="sxs-lookup"><span data-stu-id="75ece-110">2.0.2 (10/18/2016)</span></span>
* <span data-ttu-id="75ece-111">Correzione di un problema di arresto anomalo nell'esplorazione privata (Safari).</span><span class="sxs-lookup"><span data-stu-id="75ece-111">Fixed crash on private browsing (Safari).</span></span>
* <span data-ttu-id="75ece-112">Correzione di un problema di arresto anomalo nei browser con cookie disabilitati.</span><span class="sxs-lookup"><span data-stu-id="75ece-112">Fixed crash on browsers with cookies disabled.</span></span>

<span data-ttu-id="75ece-113">Per tutte le versioni, vedere hello [completare note sulla versione](mobile-engagement-web-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="75ece-113">For all versions, please see hello [complete release notes](mobile-engagement-web-release-notes.md).</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="75ece-114">Procedure di aggiornamento</span><span class="sxs-lookup"><span data-stu-id="75ece-114">Upgrade procedures</span></span>
### <a name="upgrade-from-121-too200"></a><span data-ttu-id="75ece-115">Eseguire l'aggiornamento da 1.2.1 too2.0.0</span><span class="sxs-lookup"><span data-stu-id="75ece-115">Upgrade from 1.2.1 too2.0.0</span></span>
<span data-ttu-id="75ece-116">Hello nelle sezioni seguenti descrivono come toomigrate un'integrazione di Mobile Engagement Web SDK dal servizio Capptain hello, offerto Capptain SAS, app di Azure Mobile Engagement tooan.</span><span class="sxs-lookup"><span data-stu-id="75ece-116">hello following sections describe how toomigrate a Mobile Engagement Web SDK integration from hello Capptain service, offered by Capptain SAS, tooan Azure Mobile Engagement app.</span></span> <span data-ttu-id="75ece-117">Se si esegue la migrazione da una versione precedente di 1.2.1, consultare hello Capptain sito Web toomigrate too1.2.1 prima e quindi applicare hello seguire le procedure seguenti.</span><span class="sxs-lookup"><span data-stu-id="75ece-117">If you are migrating from a version earlier than 1.2.1, please consult hello Capptain website toomigrate too1.2.1 first, and then apply hello following procedures.</span></span>

<span data-ttu-id="75ece-118">Questa versione di hello Mobile Engagement Web SDK non supporta TV Smart Samsung, Opera TV, webOS o funzionalità Reach hello.</span><span class="sxs-lookup"><span data-stu-id="75ece-118">This version of hello Mobile Engagement Web SDK doesn't support Samsung Smart TV, Opera TV, webOS, or hello Reach feature.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="75ece-119">Capptain e Azure Mobile Engagement non sono hello stesso servizio e seguire le procedure seguenti hello evidenzia solo come toomigrate hello app client.</span><span class="sxs-lookup"><span data-stu-id="75ece-119">Capptain and Azure Mobile Engagement are not hello same service, and hello following procedures highlight only how toomigrate hello client app.</span></span> <span data-ttu-id="75ece-120">Migrazione hello Mobile Engagement Web SDK nell'applicazione hello non eseguirà la migrazione dei dati da un server di Mobile Engagement Capptain tooa server.</span><span class="sxs-lookup"><span data-stu-id="75ece-120">Migrating hello Mobile Engagement Web SDK in hello app will not migrate your data from a Capptain server tooa Mobile Engagement server.</span></span>
> 
> 

#### <a name="javascript-files"></a><span data-ttu-id="75ece-121">File JavaScript</span><span class="sxs-lookup"><span data-stu-id="75ece-121">JavaScript files</span></span>
<span data-ttu-id="75ece-122">Sostituisci hello file capptain-sdk.js con hello azure engagement.js di file e aggiornare di conseguenza le importazioni di script.</span><span class="sxs-lookup"><span data-stu-id="75ece-122">Replace hello file capptain-sdk.js with hello file azure-engagement.js, and then update your script imports accordingly.</span></span>

#### <a name="remove-capptain-reach"></a><span data-ttu-id="75ece-123">Rimuovere Capptain Reach</span><span class="sxs-lookup"><span data-stu-id="75ece-123">Remove Capptain Reach</span></span>
<span data-ttu-id="75ece-124">Questa versione di hello Mobile Engagement Web SDK non supporta funzionalità di copertura hello.</span><span class="sxs-lookup"><span data-stu-id="75ece-124">This version of hello Mobile Engagement Web SDK doesn't support hello Reach feature.</span></span> <span data-ttu-id="75ece-125">Se è stata integrata Capptain Reach nell'applicazione, è necessario tooremove è.</span><span class="sxs-lookup"><span data-stu-id="75ece-125">If you have integrated Capptain Reach into your application, you need tooremove it.</span></span>

<span data-ttu-id="75ece-126">Rimuovere hello raggiungere CSS importazione dalla pagina ed eliminare file con estensione CSS correlati hello (capptain-reach.css, per impostazione predefinita).</span><span class="sxs-lookup"><span data-stu-id="75ece-126">Remove hello Reach CSS import from your page and delete hello related .css file (capptain-reach.css, by default).</span></span>

<span data-ttu-id="75ece-127">Eliminare hello seguente di portata risorse: hello Chiudi immagine (capptain-close.png, per impostazione predefinita) e l'icona del marchio di hello (capptain--icona di notifica, per impostazione predefinita).</span><span class="sxs-lookup"><span data-stu-id="75ece-127">Delete hello following Reach resources: hello close image (capptain-close.png, by default) and hello brand icon (capptain-notification-icon, by default).</span></span>

<span data-ttu-id="75ece-128">Rimuovere hello raggiungere dell'interfaccia utente per le notifiche nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="75ece-128">Remove hello Reach UI for in-app notifications.</span></span> <span data-ttu-id="75ece-129">layout predefinito Hello è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="75ece-129">hello default layout looks like this:</span></span>

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

<span data-ttu-id="75ece-130">Rimuovere hello raggiungere dell'interfaccia utente per i sondaggi e gli annunci di testo e web.</span><span class="sxs-lookup"><span data-stu-id="75ece-130">Remove hello Reach UI for text and web announcements and polls.</span></span> <span data-ttu-id="75ece-131">layout predefinito Hello è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="75ece-131">hello default layout looks like this:</span></span>

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

<span data-ttu-id="75ece-132">Rimuovere hello `reach` oggetto dalla configurazione, se presente.</span><span class="sxs-lookup"><span data-stu-id="75ece-132">Remove hello `reach` object from your configuration, if it exists.</span></span> <span data-ttu-id="75ece-133">L'aspetto sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="75ece-133">It looks like this:</span></span>

    window.capptain = {
      [...]
      reach: {
        [...]
      }
    }

<span data-ttu-id="75ece-134">Rimuovere eventuali altre personalizzazioni di Reach, ad esempio le categorie.</span><span class="sxs-lookup"><span data-stu-id="75ece-134">Remove any other Reach customization, such as categories.</span></span>

#### <a name="remove-deprecated-apis"></a><span data-ttu-id="75ece-135">Rimuovere API deprecate</span><span class="sxs-lookup"><span data-stu-id="75ece-135">Remove deprecated APIs</span></span>
<span data-ttu-id="75ece-136">Alcune API da Capptain sono deprecati in hello Web di Mobile Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="75ece-136">Some APIs from Capptain are deprecated in hello Mobile Engagement Web SDK.</span></span>

<span data-ttu-id="75ece-137">Rimuovere qualsiasi toohello chiamate API seguenti: `agent.connect`, `agent.disconnect`, `agent.pause`, e `agent.sendMessageToDevice`.</span><span class="sxs-lookup"><span data-stu-id="75ece-137">Remove any calls toohello following APIs: `agent.connect`, `agent.disconnect`, `agent.pause`, and `agent.sendMessageToDevice`.</span></span>

<span data-ttu-id="75ece-138">Rimuovere uno dei seguenti callback dalla configurazione Capptain hello: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, e `onPushMessageReceived`.</span><span class="sxs-lookup"><span data-stu-id="75ece-138">Remove any of hello following callbacks from your Capptain configuration: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, and `onPushMessageReceived`.</span></span>

#### <a name="configuration"></a><span data-ttu-id="75ece-139">Configurazione</span><span class="sxs-lookup"><span data-stu-id="75ece-139">Configuration</span></span>
<span data-ttu-id="75ece-140">Engagement mobile Usa una connessione stringa tooconfigure SDK identificatori, ad esempio, identificatore dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="75ece-140">Mobile Engagement uses a connection string tooconfigure SDK identifiers, for example, hello application identifier.</span></span>

<span data-ttu-id="75ece-141">Sostituire l'ID dell'applicazione hello con la stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="75ece-141">Replace hello application ID with your connection string.</span></span> <span data-ttu-id="75ece-142">Si noti l'oggetto globale hello di hello configurazione SDK cambierà da `capptain` troppo`azureEngagement`.</span><span class="sxs-lookup"><span data-stu-id="75ece-142">Note that hello global object for hello SDK configuration changes from `capptain` too`azureEngagement`.</span></span>

<span data-ttu-id="75ece-143">Prima della migrazione:</span><span class="sxs-lookup"><span data-stu-id="75ece-143">Before migration:</span></span>

    window.capptain = {
      appId: ...,
      [...]
    };

<span data-ttu-id="75ece-144">Dopo la migrazione:</span><span class="sxs-lookup"><span data-stu-id="75ece-144">After migration:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      [...]
    };

<span data-ttu-id="75ece-145">stringa di connessione Hello per l'applicazione viene visualizzato nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="75ece-145">hello connection string for your application is displayed in hello Azure portal.</span></span>

#### <a name="javascript-apis"></a><span data-ttu-id="75ece-146">API JavaScript</span><span class="sxs-lookup"><span data-stu-id="75ece-146">JavaScript APIs</span></span>
<span data-ttu-id="75ece-147">oggetto JavaScript globale Hello `window.capptain` è stato rinominato `window.azureEngagement`, ma è possibile utilizzare hello `window.engagement` alias per le chiamate API.</span><span class="sxs-lookup"><span data-stu-id="75ece-147">hello global JavaScript object `window.capptain` has been renamed `window.azureEngagement`, but you can use hello `window.engagement` alias for API calls.</span></span> <span data-ttu-id="75ece-148">Non è possibile utilizzare questa configurazione di alias toodefine hello SDK.</span><span class="sxs-lookup"><span data-stu-id="75ece-148">You can't use this alias toodefine hello SDK configuration.</span></span>

<span data-ttu-id="75ece-149">Ad esempio, `capptain.deviceId` diventa `engagement.deviceId`, `capptain.agent.startActivity` diventa `engagement.agent.startActivity` e così via.</span><span class="sxs-lookup"><span data-stu-id="75ece-149">For instance, `capptain.deviceId` becomes `engagement.deviceId`, `capptain.agent.startActivity` becomes `engagement.agent.startActivity`, and so on.</span></span>

<span data-ttu-id="75ece-150">Se è già stata integrata una versione precedente di hello Azure Mobile Engagement Web SDK nell'applicazione, consultare l'articolo sulla [procedure aggiornamento](mobile-engagement-web-upgrade-procedure.md).</span><span class="sxs-lookup"><span data-stu-id="75ece-150">If you have already integrated an earlier version of hello Azure Mobile Engagement Web SDK into your application, please read about [upgrade procedures](mobile-engagement-web-upgrade-procedure.md).</span></span>

