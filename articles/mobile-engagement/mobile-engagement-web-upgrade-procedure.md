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
# <a name="azure-mobile-engagement-web-sdk-upgrade-procedures"></a><span data-ttu-id="de27f-103">Procedure di aggiornamento di Azure Mobile Engagement SDK per Web</span><span class="sxs-lookup"><span data-stu-id="de27f-103">Azure Mobile Engagement Web SDK upgrade procedures</span></span>
<span data-ttu-id="de27f-104">Se è già stata integrata una versione precedente di hello Azure Mobile Engagement Web SDK nell'applicazione web, è necessario hello tooconsider seguenti punti quando si aggiorna hello SDK.</span><span class="sxs-lookup"><span data-stu-id="de27f-104">If you have already integrated an earlier version of hello Azure Mobile Engagement Web SDK into your web application, you need tooconsider hello following points when you upgrade hello SDK.</span></span>

<span data-ttu-id="de27f-105">Se non si è eseguito più versioni di hello Mobile Engagement Web SDK, potrebbe essere toocomplete varie procedure durante il processo di aggiornamento hello.</span><span class="sxs-lookup"><span data-stu-id="de27f-105">If you skipped multiple versions of hello Mobile Engagement Web SDK, you might need toocomplete several procedures during hello upgrade process.</span></span> <span data-ttu-id="de27f-106">Ad esempio, se si esegue la migrazione da 1.4.0 too1.6.0, primo seguire hello procedure tooupgrade da 1.4.0 too1.5.0.</span><span class="sxs-lookup"><span data-stu-id="de27f-106">For example, if you migrate from 1.4.0 too1.6.0, first follow hello procedures tooupgrade from 1.4.0 too1.5.0.</span></span> <span data-ttu-id="de27f-107">Seguire quindi hello procedure tooupgrade da 1.5.0 too1.6.0.</span><span class="sxs-lookup"><span data-stu-id="de27f-107">Then, follow hello procedures tooupgrade from 1.5.0 too1.6.0.</span></span>

<span data-ttu-id="de27f-108">Qualsiasi versione di aggiornamento da, sostituire le versioni precedenti del file di hello azure-engagement.js con hello l'ultima versione del file hello.</span><span class="sxs-lookup"><span data-stu-id="de27f-108">Whichever version you upgrade from, replace any earlier version of hello file azure-engagement.js with hello latest version of hello file.</span></span>

## <a name="upgrade-from-121-too200"></a><span data-ttu-id="de27f-109">Eseguire l'aggiornamento da 1.2.1 too2.0.0</span><span class="sxs-lookup"><span data-stu-id="de27f-109">Upgrade from 1.2.1 too2.0.0</span></span>
<span data-ttu-id="de27f-110">In questa sezione viene descritto come toomigrate un'integrazione di Mobile Engagement Web SDK dal servizio Capptain hello, offerto Capptain SAS, app di Azure Mobile Engagement tooan.</span><span class="sxs-lookup"><span data-stu-id="de27f-110">This section describes how toomigrate a Mobile Engagement Web SDK integration from hello Capptain service, offered by Capptain SAS, tooan Azure Mobile Engagement app.</span></span> <span data-ttu-id="de27f-111">Se si esegue la migrazione da una versione precedente,. consultare hello Capptain sito Web toofirst too1.2.1 di eseguire la migrazione e quindi applicare hello seguire le procedure seguenti.</span><span class="sxs-lookup"><span data-stu-id="de27f-111">If you are migrating from an earlier version, please consult hello Capptain website toofirst migrate too1.2.1, and then apply hello following procedures.</span></span>

<span data-ttu-id="de27f-112">Questa versione di hello Mobile Engagement Web SDK non supporta TV Smart Samsung, Opera TV, webOS o funzionalità Reach hello.</span><span class="sxs-lookup"><span data-stu-id="de27f-112">This version of hello Mobile Engagement Web SDK doesn't support Samsung Smart TV, Opera TV, webOS, or hello Reach feature.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="de27f-113">Capptain e Azure Mobile Engagement non sono hello stesso servizio.</span><span class="sxs-lookup"><span data-stu-id="de27f-113">Capptain and Azure Mobile Engagement are not hello same service.</span></span> <span data-ttu-id="de27f-114">procedura Hello evidenzia solo come toomigrate hello app client.</span><span class="sxs-lookup"><span data-stu-id="de27f-114">hello following procedure highlights only how toomigrate hello client app.</span></span> <span data-ttu-id="de27f-115">Migrazione hello Mobile Engagement Web SDK nell'applicazione hello non eseguirà la migrazione dei dati da un server di Mobile Engagement Capptain tooa server.</span><span class="sxs-lookup"><span data-stu-id="de27f-115">Migrating hello Mobile Engagement Web SDK in hello app will not migrate your data from a Capptain server tooa Mobile Engagement server.</span></span>
> 
> 

### <a name="javascript-files"></a><span data-ttu-id="de27f-116">File JavaScript</span><span class="sxs-lookup"><span data-stu-id="de27f-116">JavaScript files</span></span>
<span data-ttu-id="de27f-117">Sostituisci hello file capptain-sdk.js con hello azure engagement.js di file e aggiornare di conseguenza le importazioni di script.</span><span class="sxs-lookup"><span data-stu-id="de27f-117">Replace hello file capptain-sdk.js with hello file azure-engagement.js, and then update your script imports accordingly.</span></span>

### <a name="remove-capptain-reach"></a><span data-ttu-id="de27f-118">Rimuovere Capptain Reach</span><span class="sxs-lookup"><span data-stu-id="de27f-118">Remove Capptain Reach</span></span>
<span data-ttu-id="de27f-119">Questa versione di hello Mobile Engagement Web SDK non supporta funzionalità di copertura hello.</span><span class="sxs-lookup"><span data-stu-id="de27f-119">This version of hello Mobile Engagement Web SDK doesn't support hello Reach feature.</span></span> <span data-ttu-id="de27f-120">Se Capptain Reach è integrato nell'applicazione, è necessario tooremove è.</span><span class="sxs-lookup"><span data-stu-id="de27f-120">If you integrated Capptain Reach into your application, you need tooremove it.</span></span>

<span data-ttu-id="de27f-121">Rimuovere hello raggiungere CSS importazione dalla pagina ed eliminare file con estensione CSS correlati hello (capptain-reach.css, per impostazione predefinita).</span><span class="sxs-lookup"><span data-stu-id="de27f-121">Remove hello Reach CSS import from your page and delete hello related .css file (capptain-reach.css, by default).</span></span>

<span data-ttu-id="de27f-122">Eliminare hello seguente di portata risorse: hello Chiudi immagine (capptain-close.png, per impostazione predefinita) e l'icona del marchio di hello (capptain--icona di notifica, per impostazione predefinita).</span><span class="sxs-lookup"><span data-stu-id="de27f-122">Delete hello following Reach resources: hello close image (capptain-close.png, by default) and hello brand icon (capptain-notification-icon, by default).</span></span>

<span data-ttu-id="de27f-123">Rimuovere hello raggiungere dell'interfaccia utente per le notifiche nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="de27f-123">Remove hello Reach UI for in-app notifications.</span></span> <span data-ttu-id="de27f-124">layout predefinito Hello è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="de27f-124">hello default layout looks like this:</span></span>

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

<span data-ttu-id="de27f-125">Rimuovere hello raggiungere dell'interfaccia utente per i sondaggi e gli annunci di testo e web.</span><span class="sxs-lookup"><span data-stu-id="de27f-125">Remove hello Reach UI for text and web announcements and polls.</span></span> <span data-ttu-id="de27f-126">layout predefinito Hello è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="de27f-126">hello default layout looks like this:</span></span>

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

<span data-ttu-id="de27f-127">Rimuovere hello `reach` oggetto dalla configurazione, se presente.</span><span class="sxs-lookup"><span data-stu-id="de27f-127">Remove hello `reach` object from your configuration, if it exists.</span></span> <span data-ttu-id="de27f-128">L'aspetto sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="de27f-128">It looks like this:</span></span>

    window.capptain = {
      [...]
      reach: {
        [...]
      }
    }

<span data-ttu-id="de27f-129">Rimuovere eventuali altre personalizzazioni di Reach, ad esempio le categorie.</span><span class="sxs-lookup"><span data-stu-id="de27f-129">Remove any other Reach customization, such as categories.</span></span>

### <a name="remove-deprecated-apis"></a><span data-ttu-id="de27f-130">Rimuovere API deprecate</span><span class="sxs-lookup"><span data-stu-id="de27f-130">Remove deprecated APIs</span></span>
<span data-ttu-id="de27f-131">Alcune API da Capptain sono deprecati in hello Web di Mobile Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="de27f-131">Some APIs from Capptain are deprecated in hello Mobile Engagement Web SDK.</span></span>

<span data-ttu-id="de27f-132">Rimuovere qualsiasi toohello chiamate API seguenti: `agent.connect`, `agent.disconnect`, `agent.pause`, e `agent.sendMessageToDevice`.</span><span class="sxs-lookup"><span data-stu-id="de27f-132">Remove any calls toohello following APIs: `agent.connect`, `agent.disconnect`, `agent.pause`, and `agent.sendMessageToDevice`.</span></span>

<span data-ttu-id="de27f-133">Rimuovere tutte le istanze di segue callback dalla configurazione Capptain hello: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, e `onPushMessageReceived`.</span><span class="sxs-lookup"><span data-stu-id="de27f-133">Remove any instances of hello following callbacks from your Capptain configuration: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, and `onPushMessageReceived`.</span></span>

### <a name="configuration"></a><span data-ttu-id="de27f-134">Configurazione</span><span class="sxs-lookup"><span data-stu-id="de27f-134">Configuration</span></span>
<span data-ttu-id="de27f-135">Engagement mobile Usa una connessione stringa tooconfigure SDK identificatori, ad esempio, identificatore dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="de27f-135">Mobile Engagement uses a connection string tooconfigure SDK identifiers, for example, hello application identifier.</span></span>

<span data-ttu-id="de27f-136">Sostituire l'ID dell'applicazione hello con la stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="de27f-136">Replace hello application ID with your connection string.</span></span> <span data-ttu-id="de27f-137">Si noti l'oggetto globale hello di hello configurazione SDK cambierà da `capptain` troppo`azureEngagement`.</span><span class="sxs-lookup"><span data-stu-id="de27f-137">Note that hello global object for hello SDK configuration changes from `capptain` too`azureEngagement`.</span></span>

<span data-ttu-id="de27f-138">Prima della migrazione:</span><span class="sxs-lookup"><span data-stu-id="de27f-138">Before migration:</span></span>

    window.capptain = {
      appId: ...,
      [...]
    };

<span data-ttu-id="de27f-139">Dopo la migrazione:</span><span class="sxs-lookup"><span data-stu-id="de27f-139">After migration:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      [...]
    };

<span data-ttu-id="de27f-140">stringa di connessione Hello per l'applicazione viene visualizzato nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="de27f-140">hello connection string for your application is displayed in hello Azure Portal.</span></span>

### <a name="javascript-apis"></a><span data-ttu-id="de27f-141">API JavaScript</span><span class="sxs-lookup"><span data-stu-id="de27f-141">JavaScript APIs</span></span>
<span data-ttu-id="de27f-142">oggetto JavaScript globale Hello `window.capptain` è stato rinominato `window.azureEngagement` ma è possibile utilizzare hello `window.engagement` alias per le chiamate API.</span><span class="sxs-lookup"><span data-stu-id="de27f-142">hello global JavaScript object `window.capptain` has been renamed `window.azureEngagement` but you can use hello `window.engagement` alias for API calls.</span></span> <span data-ttu-id="de27f-143">Non è possibile utilizzare configurazione di hello alias toodefine hello SDK.</span><span class="sxs-lookup"><span data-stu-id="de27f-143">You can't use hello alias toodefine hello SDK configuration.</span></span>

<span data-ttu-id="de27f-144">Ad esempio, `capptain.deviceId` diventa `engagement.deviceId`, `capptain.agent.startActivity` diventa `engagement.agent.startActivity` e così via.</span><span class="sxs-lookup"><span data-stu-id="de27f-144">For instance, `capptain.deviceId` becomes `engagement.deviceId`, `capptain.agent.startActivity` becomes `engagement.agent.startActivity`, and so on.</span></span>

