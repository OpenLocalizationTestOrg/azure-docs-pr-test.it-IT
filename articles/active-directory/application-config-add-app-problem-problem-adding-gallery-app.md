---
title: Errore durante l'aggiunta di un'applicazione della raccolta di Azure AD| Microsoft Docs
description: Informazioni sui problemi frequenti che si riscontrano quando si aggiungono applicazioni della raccolta di Azure AD e sulle azioni da eseguire per risolverli
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
ms.openlocfilehash: b3ae472d52208d3c76424d29192c1eb982639572
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="problem-adding-an-azure-ad-gallery-application"></a><span data-ttu-id="eb64e-103">Errore durante l'aggiunta di un'applicazione della raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb64e-103">Problem adding an Azure AD Gallery application</span></span>

<span data-ttu-id="eb64e-104">Questo articolo illustra i problemi frequenti che si riscontrano durante l'aggiunta di applicazioni della raccolta di Azure AD e le operazioni da eseguire per risolverli.</span><span class="sxs-lookup"><span data-stu-id="eb64e-104">This article help you to understand the common problems people face when adding Azure AD Gallery applications and what you can do to resolve them.</span></span>

## <a name="i-clicked-the-add-button-and-my-application-took-a-long-time-to-appear"></a><span data-ttu-id="eb64e-105">Quando si fa clic sul pulsante "Aggiungi" trascorre molto tempo prima che l'applicazione venga visualizzata</span><span class="sxs-lookup"><span data-stu-id="eb64e-105">I clicked the “add” button and my application took a long time to appear</span></span>

<span data-ttu-id="eb64e-106">In alcuni casi, potrebbero trascorrere uno o due minuti e a volte di più prima che l'applicazione venga visualizzata dopo essere stata aggiunta alla directory.</span><span class="sxs-lookup"><span data-stu-id="eb64e-106">Under some circumstances, it can take 1-2 minutes (and sometimes longer) for an application to appear after adding it to your directory.</span></span> <span data-ttu-id="eb64e-107">Sebbene non si tratti delle normali prestazioni previste, è possibile visualizzare l'aggiunta dell'applicazione in corso facendo clic sull'icona **Notifiche** (la campanella) nella parte superiore destra del [portale di Azure](https://portal.azure.com/) e cercando una notifica con stato **In corso** o **Completato** con l'etichetta **Crea applicazione**.</span><span class="sxs-lookup"><span data-stu-id="eb64e-107">While this is not the normal expected performance, you can see the application addition is in progress by clicking on the **Notifications** icon (the bell) in the upper right of the [Azure Portal](https://portal.azure.com/) and looking for an **In Progress** or **Completed** notification labeled **Create application.**</span></span>

<span data-ttu-id="eb64e-108">Se l'applicazione non viene mai aggiunta o si verifica un errore quando si fa clic sul pulsante **Aggiungi**, viene visualizzata una **Notifica** con stato **Errore**.</span><span class="sxs-lookup"><span data-stu-id="eb64e-108">If your application is never added, or you encounter an error when clicking the **Add** button, you’ll see a **Notification** in an **Error** state.</span></span> <span data-ttu-id="eb64e-109">Se si desidera visualizzare altri dettagli sull'errore per saperne di più o per effettuarne la condivisione con un tecnico del supporto, è possibile visualizzare altre informazioni sull'errore seguendo i passaggi illustrati nella sezione [Come visualizzare i dettagli di una notifica del portale](#how-to-see-the-details-of-a-portal-notification).</span><span class="sxs-lookup"><span data-stu-id="eb64e-109">If you want more details about the error to learn more to or share with a support engingeer, you can see more information about the error by following the steps in the [How to see the details of a portal notification](#how-to-see-the-details-of-a-portal-notification) section.</span></span>

## <a name="i-clicked-the-add-button-and-my-application-didnt-appear"></a><span data-ttu-id="eb64e-110">Quando si fa clic sul pulsante "Aggiungi" l'applicazione non viene visualizzata</span><span class="sxs-lookup"><span data-stu-id="eb64e-110">I clicked the “add” button and my application didn’t appear</span></span>

<span data-ttu-id="eb64e-111">In alcuni casi, a causa di problemi temporanei, problemi di rete o un bug, l'aggiunta di un'applicazione ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="eb64e-111">Sometimes, due to transient issues, networking problems, or a bug, adding an application fail.</span></span> <span data-ttu-id="eb64e-112">È possibile verificare il problema facendo clic sull'icona **Notifiche** (la campanella) nella parte superiore destra del portale di Azure. Un punto esclamativo (!) rosso viene visualizzato accanto alla notifica **Crea applicazione**.</span><span class="sxs-lookup"><span data-stu-id="eb64e-112">You can tell this happens when you click the **Notifications** icon (the bell) in the upper right of the Azure Portal and you see a red (!) icon next to your **Create application** notification.</span></span> <span data-ttu-id="eb64e-113">Questa icona indica che si è verificato un errore durante la creazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="eb64e-113">This indicates there was an error when creating the application.</span></span>

<span data-ttu-id="eb64e-114">Se si verifica un errore quando si fa clic sul pulsante **Aggiungi**, viene visualizzata una **Notifica** con stato **Errore**.</span><span class="sxs-lookup"><span data-stu-id="eb64e-114">If you encounter an error when clicking the **Add** button, you’ll see a **Notification** in an **Error** state.</span></span> <span data-ttu-id="eb64e-115">Se si desidera visualizzare altri dettagli sull'errore per saperne di più o per effettuarne la condivisione con un tecnico del supporto, è possibile visualizzare altre informazioni sull'errore seguendo i passaggi illustrati nella sezione [Come visualizzare i dettagli di una notifica del portale](#how-to-see-the-details-of-a-portal-notification).</span><span class="sxs-lookup"><span data-stu-id="eb64e-115">If you want more details about the error to learn more to or share with a support engingeer, you can see more information about the error by following the steps in the [How to see the details of a portal notification](#how-to-see-the-details-of-a-portal-notification) section.</span></span>

 ## <a name="i-dont-know-how-to-set-up-my-application-once-ive-added-it"></a><span data-ttu-id="eb64e-116">Non si sa come configurare l'applicazione dopo averla aggiunta</span><span class="sxs-lookup"><span data-stu-id="eb64e-116">I don’t know how to set up my application once I’ve added it</span></span>

<span data-ttu-id="eb64e-117">Per informazioni su come configurare le applicazioni, vedere l'articolo [Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list).</span><span class="sxs-lookup"><span data-stu-id="eb64e-117">If you need help learning about applications, the [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list) article is a good place to start.</span></span>

<span data-ttu-id="eb64e-118">Vedere anche l'articolo [Azure AD Applications Document Library](https://docs.microsoft.com/azure/active-directory/active-directory-apps-index) (Raccolta di documenti sulle applicazioni di Azure AD) che include informazioni sull'accesso Single Sign-On e ne illustra il funzionamento.</span><span class="sxs-lookup"><span data-stu-id="eb64e-118">In addition to this, the [Azure AD Applications Document Library](https://docs.microsoft.com/azure/active-directory/active-directory-apps-index) help you to learn more about single sign-on with Azure AD and how it works.</span></span>

## <a name="how-to-see-the-details-of-a-portal-notification"></a><span data-ttu-id="eb64e-119">Come visualizzare i dettagli di una notifica del portale</span><span class="sxs-lookup"><span data-stu-id="eb64e-119">How to see the details of a portal notification</span></span>

<span data-ttu-id="eb64e-120">È possibile visualizzare i dettagli di qualsiasi notifica del portale seguendo questa procedura:</span><span class="sxs-lookup"><span data-stu-id="eb64e-120">You can see the details of any portal notification by following the steps below:</span></span>

1.  <span data-ttu-id="eb64e-121">Fare clic sull'icona **Notifiche** (la campanella) nella parte superiore destra del portale di Azure</span><span class="sxs-lookup"><span data-stu-id="eb64e-121">click the **Notifications** icon (the bell) in the upper right of the Azure Portal</span></span>

2.  <span data-ttu-id="eb64e-122">Selezionare una notifica con stato **Errore** contrassegnata con un punto esclamativo (!) rosso.</span><span class="sxs-lookup"><span data-stu-id="eb64e-122">Select any notification in an **Error** state (those with a red (!) next to them).</span></span>

    >[!NOTE]
    ><span data-ttu-id="eb64e-123">Non è possibile fare clic sulle notifiche con stato **Operazione completata** o **In corso**.</span><span class="sxs-lookup"><span data-stu-id="eb64e-123">You cannot click notifications in a **Successful** or **In Progress** state.</span></span>
    >
    >

3.  <span data-ttu-id="eb64e-124">Viene aperto il pannello **Dettagli notifica**.</span><span class="sxs-lookup"><span data-stu-id="eb64e-124">This open the **Notification Details** blade.</span></span>

4.  <span data-ttu-id="eb64e-125">Usare queste informazioni per ottenere più dettagli sul problema.</span><span class="sxs-lookup"><span data-stu-id="eb64e-125">Use this information yourself to understand more details about the problem.</span></span>

5.  <span data-ttu-id="eb64e-126">In caso sia ancora necessaria assistenza sul problema, è possibile condividere queste informazioni con un tecnico di supporto o con il gruppo del prodotto.</span><span class="sxs-lookup"><span data-stu-id="eb64e-126">If you still need help, you can also share this information with a support engineer or the product group to get help with your problem.</span></span>

6.  <span data-ttu-id="eb64e-127">Fare clic sull'**icona** **Copia** a destra della casella di testo **Copia errore** per copiare tutti i dettagli della notifica da condividere con un tecnico del supporto o con il gruppo del prodotto.</span><span class="sxs-lookup"><span data-stu-id="eb64e-127">Click the **copy** **icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group engineer</span></span>

## <a name="how-to-get-help-by-sending-notification-details-to-a-support-engineer"></a><span data-ttu-id="eb64e-128">Come ottenere assistenza inviando i dettagli della notifica a un tecnico di supporto</span><span class="sxs-lookup"><span data-stu-id="eb64e-128">How to get help by sending notification details to a support engineer</span></span>

<span data-ttu-id="eb64e-129">È molto importante condividere **tutti i dettagli elencati di seguito** con un tecnico del supporto per poter ricevere assistenza immediata.</span><span class="sxs-lookup"><span data-stu-id="eb64e-129">It is very important that you share **all the details listed below** with a support engineer if you need help, so that they can help you quickly.</span></span> <span data-ttu-id="eb64e-130">A tale scopo, è possibile **acquisire uno screenshot** o fare clic sull'**icona Copia errore** che si trova a destra della casella di testo **Copia errore**.</span><span class="sxs-lookup"><span data-stu-id="eb64e-130">You can do this easily by **taking a screenshot,** or by clicking the **Copy error icon**, found to the right of the **Copy error** textbox.</span></span>

## <a name="notification-details-explained"></a><span data-ttu-id="eb64e-131">Spiegazione dei dettagli della notifica</span><span class="sxs-lookup"><span data-stu-id="eb64e-131">Notification Details Explained</span></span>

<span data-ttu-id="eb64e-132">La sezione seguente illustra in dettaglio il significato degli elementi della notifica e offre esempi per ognuno di essi.</span><span class="sxs-lookup"><span data-stu-id="eb64e-132">The below explains more what each of the notification items means, and gives examples of each of them.</span></span>

### <a name="essential-notification-items"></a><span data-ttu-id="eb64e-133">Elementi essenziali della notifica</span><span class="sxs-lookup"><span data-stu-id="eb64e-133">Essential Notification Items</span></span>

-   <span data-ttu-id="eb64e-134">**Titolo**: il titolo descrittivo della notifica</span><span class="sxs-lookup"><span data-stu-id="eb64e-134">**Title** – the descriptive title of the notification</span></span>

  * <span data-ttu-id="eb64e-135">Esempio: **Impostazioni proxy di applicazione**</span><span class="sxs-lookup"><span data-stu-id="eb64e-135">Example – **Application proxy settings**</span></span>

-   <span data-ttu-id="eb64e-136">**Descrizione**: la descrizione di ciò che si è verificato a seguito dell'operazione</span><span class="sxs-lookup"><span data-stu-id="eb64e-136">**Description** – the description of what occurred as a result of the operation</span></span>

    -   <span data-ttu-id="eb64e-137">Esempio: **L'URL interno immesso è già usato da un'altra applicazione**</span><span class="sxs-lookup"><span data-stu-id="eb64e-137">Example – **Internal url entered is already being used by another application**</span></span>

-   <span data-ttu-id="eb64e-138">**ID notifica**: l'ID univoco della notifica</span><span class="sxs-lookup"><span data-stu-id="eb64e-138">**Notification Id** – the unique id of the notification</span></span>

    -   <span data-ttu-id="eb64e-139">Esempio: **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span><span class="sxs-lookup"><span data-stu-id="eb64e-139">Example – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span></span>

-   <span data-ttu-id="eb64e-140">**ID richiesta client**: l'ID specifico della richiesta creato dal browser</span><span class="sxs-lookup"><span data-stu-id="eb64e-140">**Client Request Id** – the specific request id made by your browser</span></span>

    -   <span data-ttu-id="eb64e-141">Esempio: **302fd775-3329-4670-a9f3-bea37004f0bc**</span><span class="sxs-lookup"><span data-stu-id="eb64e-141">Example – **302fd775-3329-4670-a9f3-bea37004f0bc**</span></span>

-   <span data-ttu-id="eb64e-142">**Timestamp (UTC)**: il timestamp in cui si è verificata la notifica, basato sul sistema UTC</span><span class="sxs-lookup"><span data-stu-id="eb64e-142">**Time Stamp UTC** – the timestamp during which the notification occurred, in UTC</span></span>

    -   <span data-ttu-id="eb64e-143">Esempio: **2017-03-23T19:50:43.7583681Z**</span><span class="sxs-lookup"><span data-stu-id="eb64e-143">Example – **2017-03-23T19:50:43.7583681Z**</span></span>

-   <span data-ttu-id="eb64e-144">**ID transazione interna**: l'ID interno che è possibile usare per cercare l'errore nei sistemi</span><span class="sxs-lookup"><span data-stu-id="eb64e-144">**Internal Transaction Id** – the internal ID we can use to look the error up in our systems</span></span>

    -   <span data-ttu-id="eb64e-145">Esempio: **71a2f329-ca29-402f-aa72-bc00a7aca603**</span><span class="sxs-lookup"><span data-stu-id="eb64e-145">Example – **71a2f329-ca29-402f-aa72-bc00a7aca603**</span></span>

-   <span data-ttu-id="eb64e-146">**UPN** : l'utente che ha eseguito l'operazione</span><span class="sxs-lookup"><span data-stu-id="eb64e-146">**UPN** – the user who performed the operation</span></span>

    -   <span data-ttu-id="eb64e-147">Esempio: **tperkins@f128.info**</span><span class="sxs-lookup"><span data-stu-id="eb64e-147">Example – **tperkins@f128.info**</span></span>

-   <span data-ttu-id="eb64e-148">**ID tenant**: l'ID univoco del tenant di cui è membro l'utente che ha eseguito l'operazione</span><span class="sxs-lookup"><span data-stu-id="eb64e-148">**Tenant Id** – the unique ID of the tenant that the user who performed the operation was a member of</span></span>

    -   <span data-ttu-id="eb64e-149">Esempio: **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span><span class="sxs-lookup"><span data-stu-id="eb64e-149">Example – **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span></span>

-   <span data-ttu-id="eb64e-150">**ID oggetto utente**: l'ID univoco dell'utente che ha eseguito l'operazione</span><span class="sxs-lookup"><span data-stu-id="eb64e-150">**User object Id** – the unique ID of the user who performed the operation</span></span>

    -   <span data-ttu-id="eb64e-151">Esempio: **17f84be4-51f8-483a-b533-383791227a99**</span><span class="sxs-lookup"><span data-stu-id="eb64e-151">Example – **17f84be4-51f8-483a-b533-383791227a99**</span></span>

### <a name="detailed-notification-items"></a><span data-ttu-id="eb64e-152">Elementi della notifica dettagliati</span><span class="sxs-lookup"><span data-stu-id="eb64e-152">Detailed Notification Items</span></span>

-   <span data-ttu-id="eb64e-153">**Nome visualizzato**: **(può essere vuoto)** un nome visualizzato più dettagliato per l'errore</span><span class="sxs-lookup"><span data-stu-id="eb64e-153">**Display Name** – **(can be empty)** a more detailed display name for the error</span></span>

    -   <span data-ttu-id="eb64e-154">Esempio: **Impostazioni proxy di applicazione**</span><span class="sxs-lookup"><span data-stu-id="eb64e-154">Example – **Application proxy settings**</span></span>

-   <span data-ttu-id="eb64e-155">**Stato**: lo stato specifico della notifica</span><span class="sxs-lookup"><span data-stu-id="eb64e-155">**Status** – the specific status of the notification</span></span>

    -   <span data-ttu-id="eb64e-156">Esempio: **Operazione non riuscita**</span><span class="sxs-lookup"><span data-stu-id="eb64e-156">Example – **Failed**</span></span>

-   <span data-ttu-id="eb64e-157">**ID oggetto**: **(può essere vuoto)** l'ID dell'oggetto su cui è stata eseguita l'operazione</span><span class="sxs-lookup"><span data-stu-id="eb64e-157">**Object Id** – **(can be empty)** the object ID against which the operation was performed</span></span>

    -   <span data-ttu-id="eb64e-158">Esempio: **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span><span class="sxs-lookup"><span data-stu-id="eb64e-158">Example – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span></span>

-   <span data-ttu-id="eb64e-159">**Dettagli**: la descrizione dettagliata di ciò che si è verificato come conseguenza dell'operazione</span><span class="sxs-lookup"><span data-stu-id="eb64e-159">**Details** – the detailed description of what occurred as a result of the operation</span></span>

    -   <span data-ttu-id="eb64e-160">Esempio: **L'URL interno "http://bing.com/" non è valido perché è già in uso**</span><span class="sxs-lookup"><span data-stu-id="eb64e-160">Example – **Internal url 'http://bing.com/' is invalid since it is already in use**</span></span>

-   <span data-ttu-id="eb64e-161">**Copia errore**: fare clic sull'**icona Copia** a destra della casella di testo **Copia errore** per copiare tutti i dettagli della notifica da condividere con un tecnico di supporto o del gruppo di prodotti</span><span class="sxs-lookup"><span data-stu-id="eb64e-161">**Copy error** – Click the **copy icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group engineer</span></span>

    -   <span data-ttu-id="eb64e-162">Esempio```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span><span class="sxs-lookup"><span data-stu-id="eb64e-162">Example ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span></span>

## <a name="next-steps"></a><span data-ttu-id="eb64e-163">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="eb64e-163">Next steps</span></span>
[<span data-ttu-id="eb64e-164">Gestione di applicazioni con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="eb64e-164">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
