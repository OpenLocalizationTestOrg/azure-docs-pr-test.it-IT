---
title: le notifiche aaaConfigure e modelli in Gestione API di Azure di posta elettronica | Documenti Microsoft
description: Informazioni su come le notifiche tooconfigure e modelli in Gestione API di Azure di posta elettronica.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: ee25f26d-4752-433b-af9c-3817db38aed5
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: dc23289c25a1641992b73cb955099b3f207b6968
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-notifications-and-email-templates-in-azure-api-management"></a><span data-ttu-id="7b10d-103">Come le notifiche tooconfigure e modelli in Gestione API di Azure di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="7b10d-103">How tooconfigure notifications and email templates in Azure API Management</span></span>
<span data-ttu-id="7b10d-104">Gestione API consente hello tooconfigure notifiche per eventi specifici e i modelli di messaggio di posta elettronica hello tooconfigure che vengono utilizzati toocommunicate con hello amministratori e sviluppatori di un'istanza di gestione API.</span><span class="sxs-lookup"><span data-stu-id="7b10d-104">API Management provides hello ability tooconfigure notifications for specific events, and tooconfigure hello email templates that are used toocommunicate with hello administrators and developers of an API Management instance.</span></span> <span data-ttu-id="7b10d-105">Questo argomento viene illustrato come le notifiche di tooconfigure per hello eventi disponibili e viene fornita una panoramica della configurazione di modelli di messaggio di posta elettronica hello utilizzati per questi eventi.</span><span class="sxs-lookup"><span data-stu-id="7b10d-105">This topic shows how tooconfigure notifications for hello available events, and provides an overview of configuring hello email templates used for these events.</span></span>

## <span data-ttu-id="7b10d-106"><a name="publisher-notifications"></a>Configurare le notifiche dell'editore</span><span class="sxs-lookup"><span data-stu-id="7b10d-106"><a name="publisher-notifications"> </a>Configure publisher notifications</span></span>
<span data-ttu-id="7b10d-107">Fare clic su notifiche tooconfigure, **portale di pubblicazione** in hello portale di Azure per il servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="7b10d-107">tooconfigure notifications, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="7b10d-108">Consente di procedere toohello portale di pubblicazione di gestione API.</span><span class="sxs-lookup"><span data-stu-id="7b10d-108">This takes you toohello API Management publisher portal.</span></span>

![Portale di pubblicazione][api-management-management-console]

> [!NOTE] 
> <span data-ttu-id="7b10d-110">Se non è ancora stato creato un'istanza del servizio Gestione API, vedere [creare un'istanza del servizio Gestione API] [ Create an API Management service instance] in hello [Introduzione a gestione API di Azure] [ Get started with Azure API Management] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="7b10d-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

<span data-ttu-id="7b10d-111">Fare clic su **notifiche** da hello **gestione API** menu hello notifiche disponibili hello tooview a sinistra.</span><span class="sxs-lookup"><span data-stu-id="7b10d-111">Click **Notifications** from hello **API Management** menu on hello left tooview hello available notifications.</span></span>

![Notifiche dell'editore][api-management-publisher-notifications]

<span data-ttu-id="7b10d-113">Hello seguente elenco di eventi può essere configurato per le notifiche.</span><span class="sxs-lookup"><span data-stu-id="7b10d-113">hello following list of events can be configured for notifications.</span></span>

* <span data-ttu-id="7b10d-114">**Le richieste di sottoscrizione (che richiedono l'approvazione)** : hello destinatari di posta elettronica specificato e gli utenti riceveranno le notifiche di posta elettronica sulle richieste di sottoscrizione per i prodotti di API che richiedono l'approvazione.</span><span class="sxs-lookup"><span data-stu-id="7b10d-114">**Subscription requests (requiring approval)** - hello specified email recipients and users will receive email notifications about subscription requests for API products requiring approval.</span></span>
* <span data-ttu-id="7b10d-115">**Le nuove sottoscrizioni** : hello destinatari di posta elettronica specificato e gli utenti riceveranno le notifiche di posta elettronica su nuove sottoscrizioni di API del prodotto.</span><span class="sxs-lookup"><span data-stu-id="7b10d-115">**New subscriptions** - hello specified email recipients and users will receive email notifications about new API product subscriptions.</span></span>
* <span data-ttu-id="7b10d-116">**Le richieste dell'applicazione raccolta** : hello destinatari di posta elettronica specificato e gli utenti riceveranno le notifiche di posta elettronica quando la raccolta di applicazioni toohello inviato nuove applicazioni.</span><span class="sxs-lookup"><span data-stu-id="7b10d-116">**Application gallery requests** - hello specified email recipients and users will receive email notifications when new applications are submitted toohello application gallery.</span></span>
* <span data-ttu-id="7b10d-117">**Ccn** : hello destinatari di posta elettronica specificato e gli utenti riceveranno tramite posta elettronica in copia per conoscenza nascosta toodevelopers di tutti i messaggi di posta elettronica inviati.</span><span class="sxs-lookup"><span data-stu-id="7b10d-117">**BCC** - hello specified email recipients and users will receive email blind carbon copies of all emails sent toodevelopers.</span></span>
* <span data-ttu-id="7b10d-118">**Nuovo problema o un commento** : hello destinatari di posta elettronica specificato e gli utenti riceveranno le notifiche di posta elettronica quando un nuovo problema o commento viene presentato il portale per sviluppatori hello.</span><span class="sxs-lookup"><span data-stu-id="7b10d-118">**New issue or comment** - hello specified email recipients and users will receive email notifications when a new issue or comment is submitted on hello developer portal.</span></span>
* <span data-ttu-id="7b10d-119">**Messaggio Chiudi account** : hello destinatari di posta elettronica specificato e gli utenti riceveranno le notifiche di posta elettronica quando viene chiuso un account.</span><span class="sxs-lookup"><span data-stu-id="7b10d-119">**Close account message** - hello specified email recipients and users will receive email notifications when an account is closed.</span></span>
* <span data-ttu-id="7b10d-120">**Limite di quota di sottoscrizione vicine** : hello seguenti destinatari di posta elettronica e gli utenti riceveranno le notifiche di posta elettronica quando l'utilizzo della sottoscrizione Ottiene toousage Chiudi quota.</span><span class="sxs-lookup"><span data-stu-id="7b10d-120">**Approaching subscription quota limit** - hello following email recipients and users will receive email notifications when subscription usage gets close toousage quota.</span></span>

<span data-ttu-id="7b10d-121">Per ogni evento, è possibile specificare i destinatari di posta elettronica con casella di testo indirizzo di posta elettronica hello oppure è possibile selezionare gli utenti da un elenco.</span><span class="sxs-lookup"><span data-stu-id="7b10d-121">For each event, you can specify email recipients using hello email address text box or you can select users from a list.</span></span>

<span data-ttu-id="7b10d-122">gli indirizzi e-mail di toospecify hello toobe una notifica, immetterle nella casella di testo Indirizzo posta elettronica hello.</span><span class="sxs-lookup"><span data-stu-id="7b10d-122">toospecify hello email addresses toobe notified, enter them in hello email address text box.</span></span> <span data-ttu-id="7b10d-123">Se ci sono più indirizzi di posta elettronica, separarli usando delle virgole.</span><span class="sxs-lookup"><span data-stu-id="7b10d-123">If you have multiple email addresses, separate them using commas.</span></span>

![Destinatari delle notifiche][api-management-email-addresses]

<span data-ttu-id="7b10d-125">toospecify hello utenti toobe una notifica, fare clic su **aggiungere destinatario**hello casella accanto a hello utenti toobe una notifica di controllo e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="7b10d-125">toospecify hello users toobe notified, click **add recipient**, check hello box beside hello users toobe notified, and click **OK**.</span></span>

> [!NOTE] 
> <span data-ttu-id="7b10d-126">Solo gli amministratori vengono visualizzati nell'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="7b10d-126">Only administrators are displayed in hello list.</span></span>


<span data-ttu-id="7b10d-127">Dopo aver configurato i destinatari delle notifiche hello, fare clic su **salvare** hello tooapply aggiornata i destinatari delle notifiche.</span><span class="sxs-lookup"><span data-stu-id="7b10d-127">After configuring hello notification recipients, click **Save** tooapply hello updated notification recipients.</span></span>

> [!NOTE] 
> <span data-ttu-id="7b10d-128">Se si esce dalla hello **le notifiche di server di pubblicazione** portale di pubblicazione hello scheda genera avvisi se vi sono presenti modifiche non salvate.</span><span class="sxs-lookup"><span data-stu-id="7b10d-128">If you navigate away from hello **Publisher Notifications** tab hello publisher portal alerts you if there are unsaved changes.</span></span>


## <span data-ttu-id="7b10d-129"><a name="email-templates"> </a>Configurare modelli di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="7b10d-129"><a name="email-templates"> </a>Configure email templates</span></span>
<span data-ttu-id="7b10d-130">Gestione API fornisce modelli di posta elettronica per hello messaggi di posta elettronica vengono inviati in corso di hello di amministrazione e utilizzo di servizio hello.</span><span class="sxs-lookup"><span data-stu-id="7b10d-130">API Management provides email templates for hello email messages that are sent in hello course of administering and using hello service.</span></span> <span data-ttu-id="7b10d-131">viene fornito i seguenti modelli di posta elettronica Hello.</span><span class="sxs-lookup"><span data-stu-id="7b10d-131">hello following email templates are provided.</span></span>

* <span data-ttu-id="7b10d-132">Invio alla raccolta di applicazioni approvato</span><span class="sxs-lookup"><span data-stu-id="7b10d-132">Application gallery submission approved</span></span>
* <span data-ttu-id="7b10d-133">Lettera di commiato sviluppatore</span><span class="sxs-lookup"><span data-stu-id="7b10d-133">Developer farewell letter</span></span>
* <span data-ttu-id="7b10d-134">Notifica raggiungimento limite quota sviluppatore</span><span class="sxs-lookup"><span data-stu-id="7b10d-134">Developer quota limit approaching notification</span></span>
* <span data-ttu-id="7b10d-135">Invito utente</span><span class="sxs-lookup"><span data-stu-id="7b10d-135">Invite user</span></span>
* <span data-ttu-id="7b10d-136">Nuovo commento aggiunto tooan problema</span><span class="sxs-lookup"><span data-stu-id="7b10d-136">New comment added tooan issue</span></span>
* <span data-ttu-id="7b10d-137">Nuovo problema ricevuto</span><span class="sxs-lookup"><span data-stu-id="7b10d-137">New issue received</span></span>
* <span data-ttu-id="7b10d-138">Nuova sottoscrizione attivata</span><span class="sxs-lookup"><span data-stu-id="7b10d-138">New subscription activated</span></span>
* <span data-ttu-id="7b10d-139">Conferma rinnovo sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="7b10d-139">Subscription renewed confirmation</span></span>
* <span data-ttu-id="7b10d-140">Richiesta sottoscrizione rifiutata</span><span class="sxs-lookup"><span data-stu-id="7b10d-140">Subscription request declines</span></span>
* <span data-ttu-id="7b10d-141">Richiesta sottoscrizione ricevuta</span><span class="sxs-lookup"><span data-stu-id="7b10d-141">Subscription request received</span></span>

<span data-ttu-id="7b10d-142">Questi modelli possono essere modificati a piacimento.</span><span class="sxs-lookup"><span data-stu-id="7b10d-142">These templates can be modified as desired.</span></span>

<span data-ttu-id="7b10d-143">tooview e configurare i modelli di messaggio di posta elettronica hello per l'istanza di gestione API, fare clic su **notifiche** da hello **gestione API** menu hello a sinistra e seleziona hello **modelli di posta elettronica**  scheda.</span><span class="sxs-lookup"><span data-stu-id="7b10d-143">tooview and configure hello email templates for your API Management instance, click **Notifications** from hello **API Management** menu on hello left, and select hello **Email Templates** tab.</span></span>

![Modelli di posta elettronica][api-management-email-templates]

<span data-ttu-id="7b10d-145">tooview o modificare un modello specifico, selezionarlo hello **modelli** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="7b10d-145">tooview or modify a specific template, select it from hello **Templates** drop-down list.</span></span>

![Elenco modelli di posta elettronica][api-management-email-templates-list]

<span data-ttu-id="7b10d-147">Ogni modello di posta elettronica ha un oggetto in testo normale e una definizione di corpo in formato HTML.</span><span class="sxs-lookup"><span data-stu-id="7b10d-147">Each email template has a subject in plain text, and a body definition in HTML format.</span></span> <span data-ttu-id="7b10d-148">Ogni elemento può essere personalizzato a piacimento.</span><span class="sxs-lookup"><span data-stu-id="7b10d-148">Each item can be customized as desired.</span></span>

![Editor dei modelli di posta elettronica][api-management-email-template]

<span data-ttu-id="7b10d-150">Hello **parametri** elenco contiene un elenco di parametri, che, quando inserite nell'oggetto hello o il corpo, è sostituito hello designato valore quando viene inviato tramite posta elettronica hello.</span><span class="sxs-lookup"><span data-stu-id="7b10d-150">hello **Parameters** list contains a list of parameters, which when inserted into hello subject or body, will be replaced hello designated value when hello email is sent.</span></span> <span data-ttu-id="7b10d-151">tooinsert un parametro, inserire cursore hello in cui si desidera toogo parametro hello, quindi fare clic su hello freccia toohello sinistra del nome di parametro hello.</span><span class="sxs-lookup"><span data-stu-id="7b10d-151">tooinsert a parameter, place hello cursor where you wish hello parameter toogo, and click hello arrow toohello left of hello parameter name.</span></span>

<span data-ttu-id="7b10d-152">Fare clic su **anteprima** o **invio di un test** toosee come messaggio di posta elettronica hello verrà Cerca o inviare un messaggio di test.</span><span class="sxs-lookup"><span data-stu-id="7b10d-152">Click **Preview** or **Send a test** toosee how hello email will look or send a test email.</span></span>

> [!NOTE] 
> <span data-ttu-id="7b10d-153">parametri di Hello non vengono sostituiti con i valori effettivi durante l'anteprima o l'invio di un test.</span><span class="sxs-lookup"><span data-stu-id="7b10d-153">hello parameters are not replaced with actual values when previewing or sending a test.</span></span>

<span data-ttu-id="7b10d-154">modello di posta elettronica toohello modifiche hello toosave, fare clic su **salvare**, oppure fare clic su modifiche hello toocancel **Annulla**.</span><span class="sxs-lookup"><span data-stu-id="7b10d-154">toosave hello changes toohello email template, click **Save**, or toocancel hello changes click **Cancel**.</span></span>
 

[api-management-management-console]: ./media/api-management-howto-configure-notifications/api-management-management-console.png
[api-management-publisher-notifications]: ./media/api-management-howto-configure-notifications/api-management-publisher-notifications.png
[api-management-email-addresses]: ./media/api-management-howto-configure-notifications/api-management-email-addresses.png


[api-management-email-templates]: ./media/api-management-howto-configure-notifications/api-management-email-templates.png
[api-management-email-templates-list]: ./media/api-management-howto-configure-notifications/api-management-email-templates-list.png
[api-management-email-template]: ./media/api-management-howto-configure-notifications/api-management-email-template.png


[Configure publisher notifications]: #publisher-notifications
[Configure email templates]: #email-templates

[How toocreate and use groups]: api-management-howto-create-groups.md
[How tooassociate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
