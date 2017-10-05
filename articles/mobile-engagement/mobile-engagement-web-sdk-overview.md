---
title: Panoramica di Azure Mobile Engagement SDK per Web | Documentazione Microsoft
description: Ultimi aggiornamenti e procedure relativi all'SDK per Web per Azure Mobile Engagement
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
ms.openlocfilehash: 770a83131a3e661771db50b22ce7de25b2d541cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-mobile-engagement-web-sdk"></a><span data-ttu-id="c60a0-103">Azure Mobile Engagement Web SDK</span><span class="sxs-lookup"><span data-stu-id="c60a0-103">Azure Mobile Engagement Web SDK</span></span>
<span data-ttu-id="c60a0-104">Da qui è possibile visualizzare tutti i dettagli su come integrare Azure Mobile Engagement in un'app Web.</span><span class="sxs-lookup"><span data-stu-id="c60a0-104">Start here for all the details about how to integrate Azure Mobile Engagement in a web app.</span></span> <span data-ttu-id="c60a0-105">Per fare una prova prima di iniziare con la propria app Web, vedere l' [esercitazione di 15 minuti](mobile-engagement-web-app-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c60a0-105">If you'd like to give it a try before getting started with your own web app, see our [15-minute tutorial](mobile-engagement-web-app-get-started.md).</span></span>

## <a name="integration-procedures"></a><span data-ttu-id="c60a0-106">Procedure di integrazione</span><span class="sxs-lookup"><span data-stu-id="c60a0-106">Integration procedures</span></span>
1. <span data-ttu-id="c60a0-107">Informazioni su [come integrare Mobile Engagement in un'app Web](mobile-engagement-web-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="c60a0-107">Learn [how to integrate Mobile Engagement in your web app](mobile-engagement-web-integrate-engagement.md).</span></span>
2. <span data-ttu-id="c60a0-108">Per l'implementazione del piano di tag, vedere [come usare l'API avanzata di assegnazione tag di Mobile Engagement nella propria app Web](mobile-engagement-web-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="c60a0-108">For tag plan implementation, learn [how to use the advanced Mobile Engagement tagging API in your web app](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="release-notes"></a><span data-ttu-id="c60a0-109">Note sulla versione</span><span class="sxs-lookup"><span data-stu-id="c60a0-109">Release notes</span></span>
### <a name="202-10182016"></a><span data-ttu-id="c60a0-110">2.0.2 (18/10/2016)</span><span class="sxs-lookup"><span data-stu-id="c60a0-110">2.0.2 (10/18/2016)</span></span>
* <span data-ttu-id="c60a0-111">Correzione di un problema di arresto anomalo nell'esplorazione privata (Safari).</span><span class="sxs-lookup"><span data-stu-id="c60a0-111">Fixed crash on private browsing (Safari).</span></span>
* <span data-ttu-id="c60a0-112">Correzione di un problema di arresto anomalo nei browser con cookie disabilitati.</span><span class="sxs-lookup"><span data-stu-id="c60a0-112">Fixed crash on browsers with cookies disabled.</span></span>

<span data-ttu-id="c60a0-113">Per tutte le versioni, vedere le [note sulla versione complete](mobile-engagement-web-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="c60a0-113">For all versions, please see the [complete release notes](mobile-engagement-web-release-notes.md).</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="c60a0-114">Procedure di aggiornamento</span><span class="sxs-lookup"><span data-stu-id="c60a0-114">Upgrade procedures</span></span>
### <a name="upgrade-from-121-to-200"></a><span data-ttu-id="c60a0-115">Aggiornamento da 1.2.1 a 2.0.0</span><span class="sxs-lookup"><span data-stu-id="c60a0-115">Upgrade from 1.2.1 to 2.0.0</span></span>
<span data-ttu-id="c60a0-116">Le sezioni seguenti illustrano come eseguire la migrazione di un'integrazione di Mobile Engagement Web SDK dal servizio Capptain offerto da Capptain SAS a un'app di Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="c60a0-116">The following sections describe how to migrate a Mobile Engagement Web SDK integration from the Capptain service, offered by Capptain SAS, to an Azure Mobile Engagement app.</span></span> <span data-ttu-id="c60a0-117">Se si esegue la migrazione da una versione precedente alla 1.2.1, visitare il sito Web di Capptain per eseguire prima la migrazione alla versione 1.2.1 e quindi applicare le procedure seguenti.</span><span class="sxs-lookup"><span data-stu-id="c60a0-117">If you are migrating from a version earlier than 1.2.1, please consult the Capptain website to migrate to 1.2.1 first, and then apply the following procedures.</span></span>

<span data-ttu-id="c60a0-118">Questa versione di Mobile Engagement SDK per Web non supporta Samsung Smart TV, OperaTV, webOS o la funzionalità Reach.</span><span class="sxs-lookup"><span data-stu-id="c60a0-118">This version of the Mobile Engagement Web SDK doesn't support Samsung Smart TV, Opera TV, webOS, or the Reach feature.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c60a0-119">Capptain e Azure Mobile Engagement sono servizi diversi e le procedure seguente illustrano solo come eseguire la migrazione dell'app client.</span><span class="sxs-lookup"><span data-stu-id="c60a0-119">Capptain and Azure Mobile Engagement are not the same service, and the following procedures highlight only how to migrate the client app.</span></span> <span data-ttu-id="c60a0-120">La migrazione di Mobile Engagement SDK per Web nell'app non comporta la migrazione dei dati dai server di Capptain a un server di Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="c60a0-120">Migrating the Mobile Engagement Web SDK in the app will not migrate your data from a Capptain server to a Mobile Engagement server.</span></span>
> 
> 

#### <a name="javascript-files"></a><span data-ttu-id="c60a0-121">File JavaScript</span><span class="sxs-lookup"><span data-stu-id="c60a0-121">JavaScript files</span></span>
<span data-ttu-id="c60a0-122">Sostituire il file capptain-sdk.js con il file azure-engagement.js e aggiornare di conseguenza le importazioni degli script.</span><span class="sxs-lookup"><span data-stu-id="c60a0-122">Replace the file capptain-sdk.js with the file azure-engagement.js, and then update your script imports accordingly.</span></span>

#### <a name="remove-capptain-reach"></a><span data-ttu-id="c60a0-123">Rimuovere Capptain Reach</span><span class="sxs-lookup"><span data-stu-id="c60a0-123">Remove Capptain Reach</span></span>
<span data-ttu-id="c60a0-124">Questa versione di Mobile Engagement SDK per Web non supporta la funzionalità Reach.</span><span class="sxs-lookup"><span data-stu-id="c60a0-124">This version of the Mobile Engagement Web SDK doesn't support the Reach feature.</span></span> <span data-ttu-id="c60a0-125">Se nell'applicazione è integrata la funzione Capptain Reach, rimuoverla.</span><span class="sxs-lookup"><span data-stu-id="c60a0-125">If you have integrated Capptain Reach into your application, you need to remove it.</span></span>

<span data-ttu-id="c60a0-126">Rimuovere l'importazione di CSS Reach dalla pagina ed eliminare il relativo file con estensione css (per impostazione predefinita, capptain-reach.css).</span><span class="sxs-lookup"><span data-stu-id="c60a0-126">Remove the Reach CSS import from your page and delete the related .css file (capptain-reach.css, by default).</span></span>

<span data-ttu-id="c60a0-127">Eliminare le risorse di Reach seguenti: l'immagine di chiusura (per impostazione predefinita, capptain-close.png) e l'icona del marchio (per impostazione predefinita, capptain-notification-icon).</span><span class="sxs-lookup"><span data-stu-id="c60a0-127">Delete the following Reach resources: the close image (capptain-close.png, by default) and the brand icon (capptain-notification-icon, by default).</span></span>

<span data-ttu-id="c60a0-128">Rimuovere l'interfaccia utente di Reach per le notifiche in-app.</span><span class="sxs-lookup"><span data-stu-id="c60a0-128">Remove the Reach UI for in-app notifications.</span></span> <span data-ttu-id="c60a0-129">Il layout predefinito è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="c60a0-129">The default layout looks like this:</span></span>

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

<span data-ttu-id="c60a0-130">Rimuovere l'interfaccia utente di Reach per gli annunci Web, per gli annunci di testo e per i sondaggi.</span><span class="sxs-lookup"><span data-stu-id="c60a0-130">Remove the Reach UI for text and web announcements and polls.</span></span> <span data-ttu-id="c60a0-131">Il layout predefinito è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="c60a0-131">The default layout looks like this:</span></span>

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

<span data-ttu-id="c60a0-132">Rimuovere l'oggetto `reach` dalla configurazione, se esiste.</span><span class="sxs-lookup"><span data-stu-id="c60a0-132">Remove the `reach` object from your configuration, if it exists.</span></span> <span data-ttu-id="c60a0-133">L'aspetto sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="c60a0-133">It looks like this:</span></span>

    window.capptain = {
      [...]
      reach: {
        [...]
      }
    }

<span data-ttu-id="c60a0-134">Rimuovere eventuali altre personalizzazioni di Reach, ad esempio le categorie.</span><span class="sxs-lookup"><span data-stu-id="c60a0-134">Remove any other Reach customization, such as categories.</span></span>

#### <a name="remove-deprecated-apis"></a><span data-ttu-id="c60a0-135">Rimuovere API deprecate</span><span class="sxs-lookup"><span data-stu-id="c60a0-135">Remove deprecated APIs</span></span>
<span data-ttu-id="c60a0-136">Alcune delle API da Capptain sono deprecate in Mobile Engagement SDK per Web.</span><span class="sxs-lookup"><span data-stu-id="c60a0-136">Some APIs from Capptain are deprecated in the Mobile Engagement Web SDK.</span></span>

<span data-ttu-id="c60a0-137">Rimuovere eventuali chiamate alle API seguenti: `agent.connect`, `agent.disconnect`, `agent.pause` e `agent.sendMessageToDevice`.</span><span class="sxs-lookup"><span data-stu-id="c60a0-137">Remove any calls to the following APIs: `agent.connect`, `agent.disconnect`, `agent.pause`, and `agent.sendMessageToDevice`.</span></span>

<span data-ttu-id="c60a0-138">Rimuovere i callback seguenti dalla configurazione di Capptain: `onConnected`, `onDisconnected`, `onDeviceMessageReceived` e `onPushMessageReceived`.</span><span class="sxs-lookup"><span data-stu-id="c60a0-138">Remove any of the following callbacks from your Capptain configuration: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, and `onPushMessageReceived`.</span></span>

#### <a name="configuration"></a><span data-ttu-id="c60a0-139">Configurazione</span><span class="sxs-lookup"><span data-stu-id="c60a0-139">Configuration</span></span>
<span data-ttu-id="c60a0-140">Mobile Engagement usa ora una stringa di connessione per configurare gli identificatori dell'SDK, ad esempio l'identificatore dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c60a0-140">Mobile Engagement uses a connection string to configure SDK identifiers, for example, the application identifier.</span></span>

<span data-ttu-id="c60a0-141">Sostituire l'ID dell'applicazione con la stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="c60a0-141">Replace the application ID with your connection string.</span></span> <span data-ttu-id="c60a0-142">Tenere presente che l'oggetto globale per le modifiche alla configurazione dell'SDK cambia da `capptain` a `azureEngagement`.</span><span class="sxs-lookup"><span data-stu-id="c60a0-142">Note that the global object for the SDK configuration changes from `capptain` to `azureEngagement`.</span></span>

<span data-ttu-id="c60a0-143">Prima della migrazione:</span><span class="sxs-lookup"><span data-stu-id="c60a0-143">Before migration:</span></span>

    window.capptain = {
      appId: ...,
      [...]
    };

<span data-ttu-id="c60a0-144">Dopo la migrazione:</span><span class="sxs-lookup"><span data-stu-id="c60a0-144">After migration:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      [...]
    };

<span data-ttu-id="c60a0-145">La stringa di connessione per l'applicazione viene visualizzata nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c60a0-145">The connection string for your application is displayed in the Azure portal.</span></span>

#### <a name="javascript-apis"></a><span data-ttu-id="c60a0-146">API JavaScript</span><span class="sxs-lookup"><span data-stu-id="c60a0-146">JavaScript APIs</span></span>
<span data-ttu-id="c60a0-147">L'oggetto JavaScript globale `window.capptain` è stato rinominato `window.azureEngagement`, ma è possibile usare l'alias `window.engagement` per le chiamate API.</span><span class="sxs-lookup"><span data-stu-id="c60a0-147">The global JavaScript object `window.capptain` has been renamed `window.azureEngagement`, but you can use the `window.engagement` alias for API calls.</span></span> <span data-ttu-id="c60a0-148">Non è possibile usare l'alias per definire la configurazione dell'SDK.</span><span class="sxs-lookup"><span data-stu-id="c60a0-148">You can't use this alias to define the SDK configuration.</span></span>

<span data-ttu-id="c60a0-149">Ad esempio, `capptain.deviceId` diventa `engagement.deviceId`, `capptain.agent.startActivity` diventa `engagement.agent.startActivity` e così via.</span><span class="sxs-lookup"><span data-stu-id="c60a0-149">For instance, `capptain.deviceId` becomes `engagement.deviceId`, `capptain.agent.startActivity` becomes `engagement.agent.startActivity`, and so on.</span></span>

<span data-ttu-id="c60a0-150">Se nell'applicazione Web è già stata integrata una versione precedente di Azure Mobile Engagement Web SDK, vedere le [procedure di aggiornamento](mobile-engagement-web-upgrade-procedure.md).</span><span class="sxs-lookup"><span data-stu-id="c60a0-150">If you have already integrated an earlier version of the Azure Mobile Engagement Web SDK into your application, please read about [upgrade procedures](mobile-engagement-web-upgrade-procedure.md).</span></span>

