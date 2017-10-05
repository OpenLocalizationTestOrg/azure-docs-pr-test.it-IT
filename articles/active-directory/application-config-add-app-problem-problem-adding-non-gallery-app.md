---
title: Errore durante l'aggiunta di un'applicazione non inclusa nella raccolta | Microsoft Docs
description: Comprendere i problemi frequenti che si riscontrano durante l'aggiunta di applicazioni personalizzate non incluse nella raccolta
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: bb3fc7877f4e7cafc3904fc67abd87b897874d8a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="problem-adding-a-non-gallery-application"></a><span data-ttu-id="04994-103">Errore durante l'aggiunta di un'applicazione non inclusa nella raccolta</span><span class="sxs-lookup"><span data-stu-id="04994-103">Problem adding a non-gallery application</span></span>

<span data-ttu-id="04994-104">Questo articolo consente di comprendere i problemi frequenti che si riscontrano durante l'aggiunta di **applicazioni personalizzate non incluse nella raccolta** e presenta le azioni da intraprendere per risolverli.</span><span class="sxs-lookup"><span data-stu-id="04994-104">This article help you to understand the common problems people face when adding **custom non-gallery applications** and what you can do to resolve them.</span></span> 

## <a name="i-clicked-the-add-button-and-my-application-took-a-long-time-to-appear"></a><span data-ttu-id="04994-105">Dopo avere fatto clic sul pulsante "Aggiungi", l'applicazione ha impiegato molto tempo per essere visualizzata</span><span class="sxs-lookup"><span data-stu-id="04994-105">I clicked the “add” button and my application took a long time to appear</span></span>

<span data-ttu-id="04994-106">In alcuni casi, dopo essere stata aggiunta alla directory, un'applicazione può impiegare 1-2 minuti per essere visualizzata. Talvolta, possono essere richiesti tempi ancora più lunghi.</span><span class="sxs-lookup"><span data-stu-id="04994-106">Under some circumstances, it can take 1-2 minutes (and sometimes longer) for an application to appear after adding it to your directory.</span></span> <span data-ttu-id="04994-107">Sebbene non si tratti delle normali prestazioni previste, è possibile vedere che è in corso l'aggiunta dell'applicazione facendo clic sull'icona **Notifiche** (la campanella) nella parte superiore destra del [Portale di Azure](https://portal.azure.com/) e cercando una notifica che indica **In corso** o **Completata** con l'etichetta **Crea applicazione**.</span><span class="sxs-lookup"><span data-stu-id="04994-107">While this is not the normal expected performance, you can see the application addition is in progress by clicking on the **Notifications** icon (the bell) in the upper right of the [Azure Portal](https://portal.azure.com/) and looking for an **In Progress** or **Completed** notification labeled **Create application**.</span></span>

<span data-ttu-id="04994-108">Se l'applicazione non viene mai aggiunta o si verifica un errore quando si fa clic sul pulsante **Aggiungi**, verrà visualizzata una **Notifica** in uno stato di **Errore**.</span><span class="sxs-lookup"><span data-stu-id="04994-108">If your application is never added, or you encounter an error when clicking the **Add** button, you’ll see a **Notification** in an **Error** state.</span></span> <span data-ttu-id="04994-109">Se si desidera visualizzare altri dettagli sull'errore per saperne di più o per effettuarne la condivisione con un tecnico del supporto, è possibile visualizzare altre informazioni sull'errore seguendo i passaggi illustrati nella sezione [Come visualizzare i dettagli di una notifica del portale](#how-to-see-the-details-of-a-portal-notification).</span><span class="sxs-lookup"><span data-stu-id="04994-109">If you want more details about the error to learn more to or share with a support engingeer, you can see more information about the error by following the steps in the [How to see the details of a portal notification](#how-to-see-the-details-of-a-portal-notification) section.</span></span>

## <a name="i-clicked-the-add-button-and-my-application-didnt-appear"></a><span data-ttu-id="04994-110">Quando si fa clic sul pulsante "Aggiungi" l'applicazione non viene visualizzata</span><span class="sxs-lookup"><span data-stu-id="04994-110">I clicked the “add” button and my application didn’t appear</span></span>

<span data-ttu-id="04994-111">In alcuni casi, a causa di problemi temporanei, problemi di rete o un bug, l'aggiunta di un'applicazione ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="04994-111">Sometimes, due to transient issues, networking problems, or a bug, adding an application fail.</span></span> <span data-ttu-id="04994-112">È possibile verificare il problema facendo clic sull'icona **Notifiche** (la campanella) nella parte superiore destra del portale di Azure. Un punto esclamativo (!) rosso viene visualizzato accanto alla notifica **Crea applicazione**.</span><span class="sxs-lookup"><span data-stu-id="04994-112">You can tell this happens when you click the **Notifications** icon (the bell) in the upper right of the Azure Portal and you see a red (!) icon next to your **Create application** notification.</span></span> <span data-ttu-id="04994-113">Questa icona indica che si è verificato un errore durante la creazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="04994-113">This indicates there was an error when creating the application.</span></span>

<span data-ttu-id="04994-114">Se si verifica un errore quando si fa clic sul pulsante **Aggiungi**, viene visualizzata una **Notifica** con stato **Errore**.</span><span class="sxs-lookup"><span data-stu-id="04994-114">If you encounter an error when clicking the **Add** button, you’ll see a **Notification** in an **Error** state.</span></span> <span data-ttu-id="04994-115">Se si desidera visualizzare altri dettagli sull'errore per saperne di più o per effettuarne la condivisione con un tecnico del supporto, è possibile visualizzare altre informazioni sull'errore seguendo i passaggi illustrati nella sezione [Come visualizzare i dettagli di una notifica del portale](#how-to-see-the-details-of-a-portal-notification).</span><span class="sxs-lookup"><span data-stu-id="04994-115">If you want more details about the error to learn more to or share with a support engingeer, you can see more information about the error by following the steps in the [How to see the details of a portal notification](#how-to-see-the-details-of-a-portal-notification) section.</span></span>

## <a name="i-dont-know-how-to-set-up-my-application-once-ive-added-it"></a><span data-ttu-id="04994-116">Come configurare l'applicazione dopo averla aggiunta</span><span class="sxs-lookup"><span data-stu-id="04994-116">I don’t know how to set up my application once I’ve added it</span></span>

<span data-ttu-id="04994-117">Se sono necessarie altre informazioni sulle applicazioni personalizzate, la [Raccolta documenti sulle applicazioni Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-apps-index) consente di acquisire familiarità con Single sign-on con Azure AD e il relativo funzionamento.</span><span class="sxs-lookup"><span data-stu-id="04994-117">If you need help learning about custom applications, the [Azure AD Applications Document Library](https://docs.microsoft.com/azure/active-directory/active-directory-apps-index) help you to learn more about single sign-on with Azure AD and how it works.</span></span>

## <a name="how-to-see-the-details-of-a-portal-notification"></a><span data-ttu-id="04994-118">Come visualizzare i dettagli di una notifica del portale</span><span class="sxs-lookup"><span data-stu-id="04994-118">How to see the details of a portal notification</span></span>

<span data-ttu-id="04994-119">È possibile visualizzare i dettagli di qualsiasi notifica del portale seguendo questa procedura:</span><span class="sxs-lookup"><span data-stu-id="04994-119">You can see the details of any portal notification by following the steps below:</span></span>

1.  <span data-ttu-id="04994-120">Fare clic sull'icona **Notifiche** (la campanella) nella parte superiore destra del portale di Azure</span><span class="sxs-lookup"><span data-stu-id="04994-120">click the **Notifications** icon (the bell) in the upper right of the Azure Portal</span></span>

2.  <span data-ttu-id="04994-121">Selezionare una notifica con stato **Errore** contrassegnata con un punto esclamativo (!) rosso.</span><span class="sxs-lookup"><span data-stu-id="04994-121">Select any notification in an **Error** state (those with a red (!) next to them).</span></span>

   >[!NOTE]
   ><span data-ttu-id="04994-122">Non è possibile fare clic sulle notifiche con stato **Operazione completata** o **In corso**.</span><span class="sxs-lookup"><span data-stu-id="04994-122">You cannot click notifications in a **Successful** or **In Progress** state.</span></span>
   >
   >

3.  <span data-ttu-id="04994-123">Viene aperto il pannello **Dettagli notifica**.</span><span class="sxs-lookup"><span data-stu-id="04994-123">This open the **Notification Details** blade.</span></span>

4.  <span data-ttu-id="04994-124">Usare queste informazioni per ottenere più dettagli sul problema.</span><span class="sxs-lookup"><span data-stu-id="04994-124">Use this information yourself to understand more details about the problem.</span></span>

5.  <span data-ttu-id="04994-125">In caso sia necessaria ulteriore assistenza, è anche possibile condividere queste informazioni con un tecnico del supporto o il gruppo di prodotto per ottenere assistenza con il problema.</span><span class="sxs-lookup"><span data-stu-id="04994-125">If you still need help, you can also share this information with a support engineer or the product group to get help with your problem.</span></span>

6.  <span data-ttu-id="04994-126">Fare clic sull'**icona Copia** a destra della casella di testo **Copia errore** per copiare tutti i dettagli di notifica da condividere con un tecnico del supporto o del gruppo di prodotto.</span><span class="sxs-lookup"><span data-stu-id="04994-126">Click the **copy icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group engineer.</span></span>

## <a name="how-to-get-help-by-sending-notification-details-to-a-support-engineer"></a><span data-ttu-id="04994-127">Come ottenere assistenza inviando i dettagli di notifica a un tecnico del supporto</span><span class="sxs-lookup"><span data-stu-id="04994-127">How to get help by sending notification details to a support engineer</span></span>

<span data-ttu-id="04994-128">È molto importante condividere **tutti i dettagli elencati di seguito** con un tecnico del supporto per poter ricevere assistenza immediata.</span><span class="sxs-lookup"><span data-stu-id="04994-128">It is very important that you share **all the details listed below** with a support engineer if you need help, so that they can help you quickly.</span></span> <span data-ttu-id="04994-129">A tale scopo, è possibile **acquisire uno screenshot** o fare clic sull'**icona Copia errore** che si trova a destra della casella di testo **Copia errore**.</span><span class="sxs-lookup"><span data-stu-id="04994-129">You can do this easily by **taking a screenshot,** or by clicking the **Copy error icon**, found to the right of the **Copy error** textbox.</span></span>

## <a name="notification-details-explained"></a><span data-ttu-id="04994-130">Spiegazione dei dettagli della notifica</span><span class="sxs-lookup"><span data-stu-id="04994-130">Notification Details Explained</span></span>

<span data-ttu-id="04994-131">La sezione seguente illustra in dettaglio il significato degli elementi della notifica e offre esempi per ognuno di essi.</span><span class="sxs-lookup"><span data-stu-id="04994-131">The below explains more what each of the notification items means, and gives examples of each of them.</span></span>

### <a name="essential-notification-items"></a><span data-ttu-id="04994-132">Elementi essenziali della notifica</span><span class="sxs-lookup"><span data-stu-id="04994-132">Essential Notification Items</span></span>

-   <span data-ttu-id="04994-133">**Titolo**: il titolo descrittivo della notifica</span><span class="sxs-lookup"><span data-stu-id="04994-133">**Title** – the descriptive title of the notification</span></span>
   *  <span data-ttu-id="04994-134">Esempio: **Impostazioni proxy di applicazione**</span><span class="sxs-lookup"><span data-stu-id="04994-134">Example – **Application proxy settings**</span></span>

-   <span data-ttu-id="04994-135">**Descrizione**: la descrizione di ciò che si è verificato a seguito dell'operazione</span><span class="sxs-lookup"><span data-stu-id="04994-135">**Description** – the description of what occurred as a result of the operation</span></span>

   *  <span data-ttu-id="04994-136">Esempio: **L'URL interno immesso è già usato da un'altra applicazione**</span><span class="sxs-lookup"><span data-stu-id="04994-136">Example – **Internal url entered is already being used by another application**</span></span>

-   <span data-ttu-id="04994-137">**ID notifica**: l'ID univoco della notifica</span><span class="sxs-lookup"><span data-stu-id="04994-137">**Notification Id** – the unique id of the notification</span></span>

   *  <span data-ttu-id="04994-138">Esempio: **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span><span class="sxs-lookup"><span data-stu-id="04994-138">Example – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span></span>

-   <span data-ttu-id="04994-139">**ID richiesta client**: l'ID specifico della richiesta creato dal browser</span><span class="sxs-lookup"><span data-stu-id="04994-139">**Client Request Id** – the specific request id made by your browser</span></span>

   *  <span data-ttu-id="04994-140">Esempio: **302fd775-3329-4670-a9f3-bea37004f0bc**</span><span class="sxs-lookup"><span data-stu-id="04994-140">Example – **302fd775-3329-4670-a9f3-bea37004f0bc**</span></span>

-   <span data-ttu-id="04994-141">**Timestamp (UTC)**: il timestamp in cui si è verificata la notifica, basato sul sistema UTC</span><span class="sxs-lookup"><span data-stu-id="04994-141">**Time Stamp UTC** – the timestamp during which the notification occurred, in UTC</span></span>

   *  <span data-ttu-id="04994-142">Esempio: **2017-03-23T19:50:43.7583681Z**</span><span class="sxs-lookup"><span data-stu-id="04994-142">Example – **2017-03-23T19:50:43.7583681Z**</span></span>

-   <span data-ttu-id="04994-143">**ID transazione interna**: l'ID interno che è possibile usare per cercare l'errore nei sistemi</span><span class="sxs-lookup"><span data-stu-id="04994-143">**Internal Transaction Id** – the internal ID we can use to look the error up in our systems</span></span>

   *  <span data-ttu-id="04994-144">Esempio: **71a2f329-ca29-402f-aa72-bc00a7aca603**</span><span class="sxs-lookup"><span data-stu-id="04994-144">Example – **71a2f329-ca29-402f-aa72-bc00a7aca603**</span></span>

-   <span data-ttu-id="04994-145">**UPN** : l'utente che ha eseguito l'operazione</span><span class="sxs-lookup"><span data-stu-id="04994-145">**UPN** – the user who performed the operation</span></span>

   *  <span data-ttu-id="04994-146">Esempio: **tperkins@f128.info**</span><span class="sxs-lookup"><span data-stu-id="04994-146">Example – **tperkins@f128.info**</span></span>

-   <span data-ttu-id="04994-147">**ID tenant**: l'ID univoco del tenant di cui è membro l'utente che ha eseguito l'operazione</span><span class="sxs-lookup"><span data-stu-id="04994-147">**Tenant Id** – the unique ID of the tenant that the user who performed the operation was a member of</span></span>

   *  <span data-ttu-id="04994-148">Esempio: **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span><span class="sxs-lookup"><span data-stu-id="04994-148">Example – **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span></span>

-   <span data-ttu-id="04994-149">**ID oggetto utente**: l'ID univoco dell'utente che ha eseguito l'operazione</span><span class="sxs-lookup"><span data-stu-id="04994-149">**User object Id** – the unique ID of the user who performed the operation</span></span>

 *  <span data-ttu-id="04994-150">Esempio: **17f84be4-51f8-483a-b533-383791227a99**</span><span class="sxs-lookup"><span data-stu-id="04994-150">Example – **17f84be4-51f8-483a-b533-383791227a99**</span></span>

### <a name="detailed-notification-items"></a><span data-ttu-id="04994-151">Elementi della notifica dettagliati</span><span class="sxs-lookup"><span data-stu-id="04994-151">Detailed Notification Items</span></span>

-   <span data-ttu-id="04994-152">**Nome visualizzato**: **(può essere vuoto)** un nome visualizzato più dettagliato per l'errore</span><span class="sxs-lookup"><span data-stu-id="04994-152">**Display Name** – **(can be empty)** a more detailed display name for the error</span></span>

  *  <span data-ttu-id="04994-153">Esempio: **Impostazioni proxy di applicazione**</span><span class="sxs-lookup"><span data-stu-id="04994-153">Example – **Application proxy settings**</span></span>

-   <span data-ttu-id="04994-154">**Stato**: lo stato specifico della notifica</span><span class="sxs-lookup"><span data-stu-id="04994-154">**Status** – the specific status of the notification</span></span>

   *  <span data-ttu-id="04994-155">Esempio: **Operazione non riuscita**</span><span class="sxs-lookup"><span data-stu-id="04994-155">Example – **Failed**</span></span>

-   <span data-ttu-id="04994-156">**ID oggetto**: **(può essere vuoto)** l'ID dell'oggetto su cui è stata eseguita l'operazione</span><span class="sxs-lookup"><span data-stu-id="04994-156">**Object Id** – **(can be empty)** the object ID against which the operation was performed</span></span>

   *  <span data-ttu-id="04994-157">Esempio: **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span><span class="sxs-lookup"><span data-stu-id="04994-157">Example – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span></span>

-   <span data-ttu-id="04994-158">**Dettagli**: la descrizione dettagliata di ciò che si è verificato come conseguenza dell'operazione</span><span class="sxs-lookup"><span data-stu-id="04994-158">**Details** – the detailed description of what occurred as a result of the operation</span></span>

   *  <span data-ttu-id="04994-159">Esempio: **L'URL interno "http://bing.com/" non è valido perché è già in uso**</span><span class="sxs-lookup"><span data-stu-id="04994-159">Example – **Internal url 'http://bing.com/' is invalid since it is already in use**</span></span>

-   <span data-ttu-id="04994-160">**Copia errore**: fare clic sull'**icona Copia** a destra della casella di testo **Copia errore** per copiare tutti i dettagli della notifica da condividere con un tecnico di supporto o del gruppo di prodotti</span><span class="sxs-lookup"><span data-stu-id="04994-160">**Copy error** – Click the **copy icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group engineer</span></span>

   *  <span data-ttu-id="04994-161">Esempio```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span><span class="sxs-lookup"><span data-stu-id="04994-161">Example ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span></span>

## <a name="next-steps"></a><span data-ttu-id="04994-162">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="04994-162">Next steps</span></span>
[<span data-ttu-id="04994-163">Gestione di applicazioni con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="04994-163">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)



