---
title: aggiunta di un'applicazione Azure AD raccolta aaaProblem | Documenti Microsoft
description: "Comprendere faccia persone problemi comuni di hello quando si aggiungono applicazioni della raccolta di Azure Active Directory e ciò che è possibile eseguire tooresolve li"
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
ms.openlocfilehash: 654f98116176d5590563c0471b92809f8763fbd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="problem-adding-an-azure-ad-gallery-application"></a><span data-ttu-id="9bf03-103">Errore durante l'aggiunta di un'applicazione della raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="9bf03-103">Problem adding an Azure AD Gallery application</span></span>

<span data-ttu-id="9bf03-104">Questo articolo è utile faccia di persone di toounderstand hello comuni problemi quando si aggiungono applicazioni della raccolta di Azure Active Directory e ciò che è possibile eseguire tooresolve li.</span><span class="sxs-lookup"><span data-stu-id="9bf03-104">This article help you toounderstand hello common problems people face when adding Azure AD Gallery applications and what you can do tooresolve them.</span></span>

## <a name="i-clicked-hello-add-button-and-my-application-took-a-long-time-tooappear"></a><span data-ttu-id="9bf03-105">Facendo clic su "Aggiungi" pulsante e l'applicazione ha richiesto un tempo tooappear hello</span><span class="sxs-lookup"><span data-stu-id="9bf03-105">I clicked hello “add” button and my application took a long time tooappear</span></span>

<span data-ttu-id="9bf03-106">In alcuni casi, può richiedere 1-2 minuti (o più) per un'applicazione tooappear dopo averlo aggiunto tooyour directory.</span><span class="sxs-lookup"><span data-stu-id="9bf03-106">Under some circumstances, it can take 1-2 minutes (and sometimes longer) for an application tooappear after adding it tooyour directory.</span></span> <span data-ttu-id="9bf03-107">Quando non si tratta di prestazioni previsto normali hello, è possibile visualizzare l'aggiunta dell'applicazione hello è in corso facendo clic su hello **notifiche** icona (campana hello) in alto a hello destra hello [il portale di Azure](https://portal.azure.com/)e cercando un **In corso** o **completato** notifica con l'etichetta **creare l'applicazione.**</span><span class="sxs-lookup"><span data-stu-id="9bf03-107">While this is not hello normal expected performance, you can see hello application addition is in progress by clicking on hello **Notifications** icon (hello bell) in hello upper right of hello [Azure Portal](https://portal.azure.com/) and looking for an **In Progress** or **Completed** notification labeled **Create application.**</span></span>

<span data-ttu-id="9bf03-108">Se l'applicazione non viene mai aggiunto o si verifica un errore quando si fa clic hello **Aggiungi** pulsante, verrà visualizzato un **notifica** in un **errore** stato.</span><span class="sxs-lookup"><span data-stu-id="9bf03-108">If your application is never added, or you encounter an error when clicking hello **Add** button, you’ll see a **Notification** in an **Error** state.</span></span> <span data-ttu-id="9bf03-109">Se si desidera visualizzare ulteriori dettagli su hello errore toolearn tooor più condividere con engingeer un supporto, è possibile visualizzare ulteriori informazioni sull'errore hello seguendo procedure hello hello [come dettagli di hello toosee di una notifica tramite il portale](#how-to-see-the-details-of-a-portal-notification) sezione.</span><span class="sxs-lookup"><span data-stu-id="9bf03-109">If you want more details about hello error toolearn more tooor share with a support engingeer, you can see more information about hello error by following hello steps in hello [How toosee hello details of a portal notification](#how-to-see-the-details-of-a-portal-notification) section.</span></span>

## <a name="i-clicked-hello-add-button-and-my-application-didnt-appear"></a><span data-ttu-id="9bf03-110">Fa clic sul pulsante "Aggiungi" hello e non è presente l'applicazione</span><span class="sxs-lookup"><span data-stu-id="9bf03-110">I clicked hello “add” button and my application didn’t appear</span></span>

<span data-ttu-id="9bf03-111">In alcuni casi, a causa di problemi di tootransient, problemi di rete o un bug, aggiunta di un errore di applicazione.</span><span class="sxs-lookup"><span data-stu-id="9bf03-111">Sometimes, due tootransient issues, networking problems, or a bug, adding an application fail.</span></span> <span data-ttu-id="9bf03-112">È possibile indicare ciò si verifica quando si fa clic su hello **notifiche** icona (campana hello) in alto a destra hello di hello portale di Azure e vedere un rosso (!) icona Avanti tooyour **creare applicazione** notifica.</span><span class="sxs-lookup"><span data-stu-id="9bf03-112">You can tell this happens when you click hello **Notifications** icon (hello bell) in hello upper right of hello Azure Portal and you see a red (!) icon next tooyour **Create application** notification.</span></span> <span data-ttu-id="9bf03-113">Ciò indica che si è verificato un errore durante la creazione di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="9bf03-113">This indicates there was an error when creating hello application.</span></span>

<span data-ttu-id="9bf03-114">Se si verifica un errore quando si fa clic hello **Aggiungi** pulsante, verrà visualizzato un **notifica** in un **errore** stato.</span><span class="sxs-lookup"><span data-stu-id="9bf03-114">If you encounter an error when clicking hello **Add** button, you’ll see a **Notification** in an **Error** state.</span></span> <span data-ttu-id="9bf03-115">Se si desidera visualizzare ulteriori dettagli su hello errore toolearn tooor più condividere con engingeer un supporto, è possibile visualizzare ulteriori informazioni sull'errore hello seguendo procedure hello hello [come dettagli di hello toosee di una notifica tramite il portale](#how-to-see-the-details-of-a-portal-notification) sezione.</span><span class="sxs-lookup"><span data-stu-id="9bf03-115">If you want more details about hello error toolearn more tooor share with a support engingeer, you can see more information about hello error by following hello steps in hello [How toosee hello details of a portal notification](#how-to-see-the-details-of-a-portal-notification) section.</span></span>

 ## <a name="i-dont-know-how-tooset-up-my-application-once-ive-added-it"></a><span data-ttu-id="9bf03-116">Non so come tooset backup una volta l'applicazione è stato aggiunto</span><span class="sxs-lookup"><span data-stu-id="9bf03-116">I don’t know how tooset up my application once I’ve added it</span></span>

<span data-ttu-id="9bf03-117">Se per ulteriori informazioni sulle applicazioni di apprendimento, hello [elenco di esercitazioni sulla procedura tooIntegrate App SaaS con Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list) articolo è un buon punto toostart.</span><span class="sxs-lookup"><span data-stu-id="9bf03-117">If you need help learning about applications, hello [List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list) article is a good place toostart.</span></span>

<span data-ttu-id="9bf03-118">In aggiunta toothis, hello [raccolta documenti di Azure AD applicazioni](https://docs.microsoft.com/azure/active-directory/active-directory-apps-index) consentono toolearn ulteriori informazioni su single sign-on con Azure AD e il relativo funzionamento.</span><span class="sxs-lookup"><span data-stu-id="9bf03-118">In addition toothis, hello [Azure AD Applications Document Library](https://docs.microsoft.com/azure/active-directory/active-directory-apps-index) help you toolearn more about single sign-on with Azure AD and how it works.</span></span>

## <a name="how-toosee-hello-details-of-a-portal-notification"></a><span data-ttu-id="9bf03-119">Modalità dettagli hello toosee di una notifica del portale</span><span class="sxs-lookup"><span data-stu-id="9bf03-119">How toosee hello details of a portal notification</span></span>

<span data-ttu-id="9bf03-120">È possibile visualizzare i dettagli di hello di qualsiasi notifica tramite il portale seguendo i passaggi di hello riportati di seguito:</span><span class="sxs-lookup"><span data-stu-id="9bf03-120">You can see hello details of any portal notification by following hello steps below:</span></span>

1.  <span data-ttu-id="9bf03-121">Fare clic su hello **notifiche** icona (campana hello) in alto a destra hello di hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="9bf03-121">click hello **Notifications** icon (hello bell) in hello upper right of hello Azure Portal</span></span>

2.  <span data-ttu-id="9bf03-122">Selezionare qualsiasi notifica in un **errore** stato (quelli con un toothem Avanti rosso (!)).</span><span class="sxs-lookup"><span data-stu-id="9bf03-122">Select any notification in an **Error** state (those with a red (!) next toothem).</span></span>

    >[!NOTE]
    ><span data-ttu-id="9bf03-123">Non è possibile fare clic sulle notifiche con stato **Operazione completata** o **In corso**.</span><span class="sxs-lookup"><span data-stu-id="9bf03-123">You cannot click notifications in a **Successful** or **In Progress** state.</span></span>
    >
    >

3.  <span data-ttu-id="9bf03-124">Questo hello aprire **i dettagli sulla notifica** blade.</span><span class="sxs-lookup"><span data-stu-id="9bf03-124">This open hello **Notification Details** blade.</span></span>

4.  <span data-ttu-id="9bf03-125">Utilizzare queste informazioni manualmente toounderstand ulteriori dettagli sul problema hello.</span><span class="sxs-lookup"><span data-stu-id="9bf03-125">Use this information yourself toounderstand more details about hello problem.</span></span>

5.  <span data-ttu-id="9bf03-126">Se è ancora necessario della Guida, è possibile condividere queste informazioni con il problema con un supporto tecnico o hello gruppo tooget Guida del prodotto.</span><span class="sxs-lookup"><span data-stu-id="9bf03-126">If you still need help, you can also share this information with a support engineer or hello product group tooget help with your problem.</span></span>

6.  <span data-ttu-id="9bf03-127">Fare clic su hello **copia** **icona** toohello diritto di hello **copiare errore** toocopy textbox tutti hello tooshare dettagli di notifica con un ingegnere del supporto o il prodotto gruppo</span><span class="sxs-lookup"><span data-stu-id="9bf03-127">Click hello **copy** **icon** toohello right of hello **Copy error** textbox toocopy all hello notification details tooshare with a support or product group engineer</span></span>

## <a name="how-tooget-help-by-sending-notification-details-tooa-support-engineer"></a><span data-ttu-id="9bf03-128">Informazioni tooget inviando al supporto tecnico tooa dettagli di notifica</span><span class="sxs-lookup"><span data-stu-id="9bf03-128">How tooget help by sending notification details tooa support engineer</span></span>

<span data-ttu-id="9bf03-129">È molto importante che si condivide **tutti hello dettagli riportati di seguito** con un supporto tecnico per assistenza, in modo che tali eventi consentono rapidamente.</span><span class="sxs-lookup"><span data-stu-id="9bf03-129">It is very important that you share **all hello details listed below** with a support engineer if you need help, so that they can help you quickly.</span></span> <span data-ttu-id="9bf03-130">Tale scopo, **acquisire uno screenshot,** o facendo clic su hello **sull'icona di errore di copia**, trovato toohello destra di hello **copiare errore** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="9bf03-130">You can do this easily by **taking a screenshot,** or by clicking hello **Copy error icon**, found toohello right of hello **Copy error** textbox.</span></span>

## <a name="notification-details-explained"></a><span data-ttu-id="9bf03-131">Spiegazione dei dettagli della notifica</span><span class="sxs-lookup"><span data-stu-id="9bf03-131">Notification Details Explained</span></span>

<span data-ttu-id="9bf03-132">Hello seguente illustra più quali tutti gli elementi hello notifica significa e fornisce esempi di ognuno di essi.</span><span class="sxs-lookup"><span data-stu-id="9bf03-132">hello below explains more what each of hello notification items means, and gives examples of each of them.</span></span>

### <a name="essential-notification-items"></a><span data-ttu-id="9bf03-133">Elementi essenziali della notifica</span><span class="sxs-lookup"><span data-stu-id="9bf03-133">Essential Notification Items</span></span>

-   <span data-ttu-id="9bf03-134">**Titolo** : hello titolo descrittivo della notifica hello</span><span class="sxs-lookup"><span data-stu-id="9bf03-134">**Title** – hello descriptive title of hello notification</span></span>

  * <span data-ttu-id="9bf03-135">Esempio: **Impostazioni proxy di applicazione**</span><span class="sxs-lookup"><span data-stu-id="9bf03-135">Example – **Application proxy settings**</span></span>

-   <span data-ttu-id="9bf03-136">**Descrizione** : hello descrizione di ciò che si è verificato in seguito a operazione hello</span><span class="sxs-lookup"><span data-stu-id="9bf03-136">**Description** – hello description of what occurred as a result of hello operation</span></span>

    -   <span data-ttu-id="9bf03-137">Esempio: **L'URL interno immesso è già usato da un'altra applicazione**</span><span class="sxs-lookup"><span data-stu-id="9bf03-137">Example – **Internal url entered is already being used by another application**</span></span>

-   <span data-ttu-id="9bf03-138">**Id di notifica** : id univoco di hello della notifica hello</span><span class="sxs-lookup"><span data-stu-id="9bf03-138">**Notification Id** – hello unique id of hello notification</span></span>

    -   <span data-ttu-id="9bf03-139">Esempio: **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span><span class="sxs-lookup"><span data-stu-id="9bf03-139">Example – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span></span>

-   <span data-ttu-id="9bf03-140">**Id richiesta client** : id richiesta specifico hello apportate dal browser</span><span class="sxs-lookup"><span data-stu-id="9bf03-140">**Client Request Id** – hello specific request id made by your browser</span></span>

    -   <span data-ttu-id="9bf03-141">Esempio: **302fd775-3329-4670-a9f3-bea37004f0bc**</span><span class="sxs-lookup"><span data-stu-id="9bf03-141">Example – **302fd775-3329-4670-a9f3-bea37004f0bc**</span></span>

-   <span data-ttu-id="9bf03-142">**Ora UTC timbro** : hello timestamp durante il quale la notifica hello si è verificato, in formato UTC</span><span class="sxs-lookup"><span data-stu-id="9bf03-142">**Time Stamp UTC** – hello timestamp during which hello notification occurred, in UTC</span></span>

    -   <span data-ttu-id="9bf03-143">Esempio: **2017-03-23T19:50:43.7583681Z**</span><span class="sxs-lookup"><span data-stu-id="9bf03-143">Example – **2017-03-23T19:50:43.7583681Z**</span></span>

-   <span data-ttu-id="9bf03-144">**Id della transazione interna** : hello ID interno, è possibile utilizzare l'errore hello toolook nei nostri sistemi</span><span class="sxs-lookup"><span data-stu-id="9bf03-144">**Internal Transaction Id** – hello internal ID we can use toolook hello error up in our systems</span></span>

    -   <span data-ttu-id="9bf03-145">Esempio: **71a2f329-ca29-402f-aa72-bc00a7aca603**</span><span class="sxs-lookup"><span data-stu-id="9bf03-145">Example – **71a2f329-ca29-402f-aa72-bc00a7aca603**</span></span>

-   <span data-ttu-id="9bf03-146">**UPN** – utente hello che ha eseguito l'operazione di hello</span><span class="sxs-lookup"><span data-stu-id="9bf03-146">**UPN** – hello user who performed hello operation</span></span>

    -   <span data-ttu-id="9bf03-147">Esempio: **tperkins@f128.info**</span><span class="sxs-lookup"><span data-stu-id="9bf03-147">Example – **tperkins@f128.info**</span></span>

-   <span data-ttu-id="9bf03-148">**Id tenant** : hello ID univoco del tenant hello che hello utente che ha eseguito l'operazione di hello è un membro di</span><span class="sxs-lookup"><span data-stu-id="9bf03-148">**Tenant Id** – hello unique ID of hello tenant that hello user who performed hello operation was a member of</span></span>

    -   <span data-ttu-id="9bf03-149">Esempio: **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span><span class="sxs-lookup"><span data-stu-id="9bf03-149">Example – **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span></span>

-   <span data-ttu-id="9bf03-150">**L'Id di oggetto utente** : hello ID univoco dell'utente di hello che ha eseguito l'operazione di hello</span><span class="sxs-lookup"><span data-stu-id="9bf03-150">**User object Id** – hello unique ID of hello user who performed hello operation</span></span>

    -   <span data-ttu-id="9bf03-151">Esempio: **17f84be4-51f8-483a-b533-383791227a99**</span><span class="sxs-lookup"><span data-stu-id="9bf03-151">Example – **17f84be4-51f8-483a-b533-383791227a99**</span></span>

### <a name="detailed-notification-items"></a><span data-ttu-id="9bf03-152">Elementi della notifica dettagliati</span><span class="sxs-lookup"><span data-stu-id="9bf03-152">Detailed Notification Items</span></span>

-   <span data-ttu-id="9bf03-153">**Nome visualizzato** – **(può essere vuoto)** un nome di visualizzazione più dettagliato per correggere l'errore hello</span><span class="sxs-lookup"><span data-stu-id="9bf03-153">**Display Name** – **(can be empty)** a more detailed display name for hello error</span></span>

    -   <span data-ttu-id="9bf03-154">Esempio: **Impostazioni proxy di applicazione**</span><span class="sxs-lookup"><span data-stu-id="9bf03-154">Example – **Application proxy settings**</span></span>

-   <span data-ttu-id="9bf03-155">**Stato** : hello specifico stato di notifica di hello</span><span class="sxs-lookup"><span data-stu-id="9bf03-155">**Status** – hello specific status of hello notification</span></span>

    -   <span data-ttu-id="9bf03-156">Esempio: **Operazione non riuscita**</span><span class="sxs-lookup"><span data-stu-id="9bf03-156">Example – **Failed**</span></span>

-   <span data-ttu-id="9bf03-157">**Id di oggetto** – **(può essere vuoto)** hello ID di oggetto su cui hello è stata eseguita l'operazione</span><span class="sxs-lookup"><span data-stu-id="9bf03-157">**Object Id** – **(can be empty)** hello object ID against which hello operation was performed</span></span>

    -   <span data-ttu-id="9bf03-158">Esempio: **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span><span class="sxs-lookup"><span data-stu-id="9bf03-158">Example – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span></span>

-   <span data-ttu-id="9bf03-159">**Dettagli** : hello descrizione dettagliata dell'accaduto come risultato di operazione hello</span><span class="sxs-lookup"><span data-stu-id="9bf03-159">**Details** – hello detailed description of what occurred as a result of hello operation</span></span>

    -   <span data-ttu-id="9bf03-160">Esempio: **L'URL interno "http://bing.com/" non è valido perché è già in uso**</span><span class="sxs-lookup"><span data-stu-id="9bf03-160">Example – **Internal url 'http://bing.com/' is invalid since it is already in use**</span></span>

-   <span data-ttu-id="9bf03-161">**Copiare l'errore** – fare clic su hello **sull'icona Copia** toohello diritto di hello **copiare errore** toocopy textbox tutti hello tooshare dettagli di notifica con un ingegnere del supporto o il prodotto gruppo</span><span class="sxs-lookup"><span data-stu-id="9bf03-161">**Copy error** – Click hello **copy icon** toohello right of hello **Copy error** textbox toocopy all hello notification details tooshare with a support or product group engineer</span></span>

    -   <span data-ttu-id="9bf03-162">Esempio```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span><span class="sxs-lookup"><span data-stu-id="9bf03-162">Example ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span></span>

## <a name="next-steps"></a><span data-ttu-id="9bf03-163">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9bf03-163">Next steps</span></span>
[<span data-ttu-id="9bf03-164">Gestione di applicazioni con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9bf03-164">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
