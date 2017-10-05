---
title: Procedure di aggiornamento di Azure Mobile Engagement SDK per Web | Documentazione Microsoft
description: Ultimi aggiornamenti e procedure relativi all'SDK per Web per Azure Mobile Engagement
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
ms.openlocfilehash: afa8037dcb7a53042fa606e2c4014b442d4be326
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-mobile-engagement-web-sdk-upgrade-procedures"></a><span data-ttu-id="8e490-103">Procedure di aggiornamento di Azure Mobile Engagement SDK per Web</span><span class="sxs-lookup"><span data-stu-id="8e490-103">Azure Mobile Engagement Web SDK upgrade procedures</span></span>
<span data-ttu-id="8e490-104">Se nell'applicazione Web è già stata integrata una versione precedente di Azure Mobile Engagement SDK per Web, è necessario considerare i seguenti punti quando si aggiorna l'SDK.</span><span class="sxs-lookup"><span data-stu-id="8e490-104">If you have already integrated an earlier version of the Azure Mobile Engagement Web SDK into your web application, you need to consider the following points when you upgrade the SDK.</span></span>

<span data-ttu-id="8e490-105">Se si sono superate numerose versioni di Mobile Engagement SDK per Web, potrebbe essere necessario completare diverse procedure durante il processo di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="8e490-105">If you skipped multiple versions of the Mobile Engagement Web SDK, you might need to complete several procedures during the upgrade process.</span></span> <span data-ttu-id="8e490-106">Ad esempio, se si esegue la migrazione dalla versione 1.4.0 alla 1.6.0, seguire innanzitutto le procedure per l'aggiornamento dalla versione 1.4.0 alla 1.5.0.</span><span class="sxs-lookup"><span data-stu-id="8e490-106">For example, if you migrate from 1.4.0 to 1.6.0, first follow the procedures to upgrade from 1.4.0 to 1.5.0.</span></span> <span data-ttu-id="8e490-107">Seguire quindi le procedure per l'aggiornamento dalla versione 1.5.0 alla 1.6.0.</span><span class="sxs-lookup"><span data-stu-id="8e490-107">Then, follow the procedures to upgrade from 1.5.0 to 1.6.0.</span></span>

<span data-ttu-id="8e490-108">Indipendentemente dalla versione dell'aggiornamento, sostituire qualsiasi versione precedente del file azure-engagement.js con la versione più recente dello stesso file.</span><span class="sxs-lookup"><span data-stu-id="8e490-108">Whichever version you upgrade from, replace any earlier version of the file azure-engagement.js with the latest version of the file.</span></span>

## <a name="upgrade-from-121-to-200"></a><span data-ttu-id="8e490-109">Aggiornamento da 1.2.1 a 2.0.0</span><span class="sxs-lookup"><span data-stu-id="8e490-109">Upgrade from 1.2.1 to 2.0.0</span></span>
<span data-ttu-id="8e490-110">Questa sezione illustra come eseguire la migrazione di un'integrazione di Mobile Engagement SDK per Web dal servizio Capptain offerto da Capptain SAS a un'app di Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="8e490-110">This section describes how to migrate a Mobile Engagement Web SDK integration from the Capptain service, offered by Capptain SAS, to an Azure Mobile Engagement app.</span></span> <span data-ttu-id="8e490-111">Se si esegue la migrazione da una versione precedente, visitare il sito Web di Capptain per eseguire prima la migrazione alla versione 1.2.1 e quindi applicare la procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="8e490-111">If you are migrating from an earlier version, please consult the Capptain website to first migrate to 1.2.1, and then apply the following procedures.</span></span>

<span data-ttu-id="8e490-112">Questa versione di Mobile Engagement SDK per Web non supporta Samsung Smart TV, OperaTV, webOS o la funzionalità Reach.</span><span class="sxs-lookup"><span data-stu-id="8e490-112">This version of the Mobile Engagement Web SDK doesn't support Samsung Smart TV, Opera TV, webOS, or the Reach feature.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8e490-113">Capptain e Azure Mobile Engagement non costituiscono lo stesso servizio.</span><span class="sxs-lookup"><span data-stu-id="8e490-113">Capptain and Azure Mobile Engagement are not the same service.</span></span> <span data-ttu-id="8e490-114">La procedura seguente illustra solo come eseguire la migrazione dell'applicazione client.</span><span class="sxs-lookup"><span data-stu-id="8e490-114">The following procedure highlights only how to migrate the client app.</span></span> <span data-ttu-id="8e490-115">La migrazione di Mobile Engagement SDK per Web nell'app non comporta la migrazione dei dati dai server di Capptain a un server di Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="8e490-115">Migrating the Mobile Engagement Web SDK in the app will not migrate your data from a Capptain server to a Mobile Engagement server.</span></span>
> 
> 

### <a name="javascript-files"></a><span data-ttu-id="8e490-116">File JavaScript</span><span class="sxs-lookup"><span data-stu-id="8e490-116">JavaScript files</span></span>
<span data-ttu-id="8e490-117">Sostituire il file capptain-sdk.js con il file azure-engagement.js e aggiornare di conseguenza le importazioni degli script.</span><span class="sxs-lookup"><span data-stu-id="8e490-117">Replace the file capptain-sdk.js with the file azure-engagement.js, and then update your script imports accordingly.</span></span>

### <a name="remove-capptain-reach"></a><span data-ttu-id="8e490-118">Rimuovere Capptain Reach</span><span class="sxs-lookup"><span data-stu-id="8e490-118">Remove Capptain Reach</span></span>
<span data-ttu-id="8e490-119">Questa versione di Mobile Engagement SDK per Web non supporta la funzionalità Reach.</span><span class="sxs-lookup"><span data-stu-id="8e490-119">This version of the Mobile Engagement Web SDK doesn't support the Reach feature.</span></span> <span data-ttu-id="8e490-120">Se nell'applicazione è integrata la funzione Capptain Reach,rimuoverla.</span><span class="sxs-lookup"><span data-stu-id="8e490-120">If you integrated Capptain Reach into your application, you need to remove it.</span></span>

<span data-ttu-id="8e490-121">Rimuovere l'importazione di CSS Reach dalla pagina ed eliminare il relativo file con estensione css (per impostazione predefinita, capptain-reach.css).</span><span class="sxs-lookup"><span data-stu-id="8e490-121">Remove the Reach CSS import from your page and delete the related .css file (capptain-reach.css, by default).</span></span>

<span data-ttu-id="8e490-122">Eliminare le risorse di Reach seguenti: l'immagine di chiusura (per impostazione predefinita, capptain-close.png) e l'icona del marchio (per impostazione predefinita, capptain-notification-icon).</span><span class="sxs-lookup"><span data-stu-id="8e490-122">Delete the following Reach resources: the close image (capptain-close.png, by default) and the brand icon (capptain-notification-icon, by default).</span></span>

<span data-ttu-id="8e490-123">Rimuovere l'interfaccia utente di Reach per le notifiche in-app.</span><span class="sxs-lookup"><span data-stu-id="8e490-123">Remove the Reach UI for in-app notifications.</span></span> <span data-ttu-id="8e490-124">Il layout predefinito è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="8e490-124">The default layout looks like this:</span></span>

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

<span data-ttu-id="8e490-125">Rimuovere l'interfaccia utente di Reach per gli annunci Web, per gli annunci di testo e per i sondaggi.</span><span class="sxs-lookup"><span data-stu-id="8e490-125">Remove the Reach UI for text and web announcements and polls.</span></span> <span data-ttu-id="8e490-126">Il layout predefinito è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="8e490-126">The default layout looks like this:</span></span>

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

<span data-ttu-id="8e490-127">Rimuovere l'oggetto `reach` dalla configurazione, se esiste.</span><span class="sxs-lookup"><span data-stu-id="8e490-127">Remove the `reach` object from your configuration, if it exists.</span></span> <span data-ttu-id="8e490-128">L'aspetto sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="8e490-128">It looks like this:</span></span>

    window.capptain = {
      [...]
      reach: {
        [...]
      }
    }

<span data-ttu-id="8e490-129">Rimuovere eventuali altre personalizzazioni di Reach, ad esempio le categorie.</span><span class="sxs-lookup"><span data-stu-id="8e490-129">Remove any other Reach customization, such as categories.</span></span>

### <a name="remove-deprecated-apis"></a><span data-ttu-id="8e490-130">Rimuovere API deprecate</span><span class="sxs-lookup"><span data-stu-id="8e490-130">Remove deprecated APIs</span></span>
<span data-ttu-id="8e490-131">Alcune delle API da Capptain sono deprecate in Mobile Engagement SDK per Web.</span><span class="sxs-lookup"><span data-stu-id="8e490-131">Some APIs from Capptain are deprecated in the Mobile Engagement Web SDK.</span></span>

<span data-ttu-id="8e490-132">Rimuovere eventuali chiamate alle API seguenti: `agent.connect`, `agent.disconnect`, `agent.pause` e `agent.sendMessageToDevice`.</span><span class="sxs-lookup"><span data-stu-id="8e490-132">Remove any calls to the following APIs: `agent.connect`, `agent.disconnect`, `agent.pause`, and `agent.sendMessageToDevice`.</span></span>

<span data-ttu-id="8e490-133">Rimuovere qualsiasi istanza dei callback seguenti dalla configurazione di Capptain: `onConnected`, `onDisconnected`, `onDeviceMessageReceived` e `onPushMessageReceived`.</span><span class="sxs-lookup"><span data-stu-id="8e490-133">Remove any instances of the following callbacks from your Capptain configuration: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, and `onPushMessageReceived`.</span></span>

### <a name="configuration"></a><span data-ttu-id="8e490-134">Configurazione</span><span class="sxs-lookup"><span data-stu-id="8e490-134">Configuration</span></span>
<span data-ttu-id="8e490-135">Mobile Engagement usa ora una stringa di connessione per configurare gli identificatori dell'SDK, ad esempio l'identificatore dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8e490-135">Mobile Engagement uses a connection string to configure SDK identifiers, for example, the application identifier.</span></span>

<span data-ttu-id="8e490-136">Sostituire l'ID dell'applicazione con la stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="8e490-136">Replace the application ID with your connection string.</span></span> <span data-ttu-id="8e490-137">Tenere presente che l'oggetto globale per le modifiche alla configurazione dell'SDK cambia da `capptain` a `azureEngagement`.</span><span class="sxs-lookup"><span data-stu-id="8e490-137">Note that the global object for the SDK configuration changes from `capptain` to `azureEngagement`.</span></span>

<span data-ttu-id="8e490-138">Prima della migrazione:</span><span class="sxs-lookup"><span data-stu-id="8e490-138">Before migration:</span></span>

    window.capptain = {
      appId: ...,
      [...]
    };

<span data-ttu-id="8e490-139">Dopo la migrazione:</span><span class="sxs-lookup"><span data-stu-id="8e490-139">After migration:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      [...]
    };

<span data-ttu-id="8e490-140">La stringa di connessione per l'applicazione viene visualizzata nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8e490-140">The connection string for your application is displayed in the Azure Portal.</span></span>

### <a name="javascript-apis"></a><span data-ttu-id="8e490-141">API JavaScript</span><span class="sxs-lookup"><span data-stu-id="8e490-141">JavaScript APIs</span></span>
<span data-ttu-id="8e490-142">L'oggetto JavaScript globale `window.capptain` è stato rinominato `window.azureEngagement`, ma è possibile usare l'alias `window.engagement` per le chiamate API.</span><span class="sxs-lookup"><span data-stu-id="8e490-142">The global JavaScript object `window.capptain` has been renamed `window.azureEngagement` but you can use the `window.engagement` alias for API calls.</span></span> <span data-ttu-id="8e490-143">Non è possibile usare l'alias per definire la configurazione dell'SDK.</span><span class="sxs-lookup"><span data-stu-id="8e490-143">You can't use the alias to define the SDK configuration.</span></span>

<span data-ttu-id="8e490-144">Ad esempio, `capptain.deviceId` diventa `engagement.deviceId`, `capptain.agent.startActivity` diventa `engagement.agent.startActivity` e così via.</span><span class="sxs-lookup"><span data-stu-id="8e490-144">For instance, `capptain.deviceId` becomes `engagement.deviceId`, `capptain.agent.startActivity` becomes `engagement.agent.startActivity`, and so on.</span></span>

