---
title: Configurare notifiche e modelli di posta elettronica in Gestione API di Azure | Documentazione Microsoft
description: Informazioni su come configurare notifiche e modelli di posta elettronica in Gestione API di Azure.
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
ms.openlocfilehash: 3d8b74e32059cfc1a4c3a8fc7d3bd04676ee80c8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-configure-notifications-and-email-templates-in-azure-api-management"></a><span data-ttu-id="32d0a-103">Come configurare notifiche e modelli di posta elettronica in Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="32d0a-103">How to configure notifications and email templates in Azure API Management</span></span>
<span data-ttu-id="32d0a-104">Gestione API consente di configurare notifiche per eventi specifici nonché di configurare modelli di posta elettronica da usare per comunicare con gli amministratori e gli sviluppatori di un'istanza di Gestione API.</span><span class="sxs-lookup"><span data-stu-id="32d0a-104">API Management provides the ability to configure notifications for specific events, and to configure the email templates that are used to communicate with the administrators and developers of an API Management instance.</span></span> <span data-ttu-id="32d0a-105">In questo argomento viene illustrato come configurare notifiche per gli eventi disponibili e viene offerta una panoramica sulla configurazione di modelli di posta elettronica usati per tali eventi.</span><span class="sxs-lookup"><span data-stu-id="32d0a-105">This topic shows how to configure notifications for the available events, and provides an overview of configuring the email templates used for these events.</span></span>

## <span data-ttu-id="32d0a-106"><a name="publisher-notifications"> </a>Configurare le notifiche dell'editore</span><span class="sxs-lookup"><span data-stu-id="32d0a-106"><a name="publisher-notifications"> </a>Configure publisher notifications</span></span>
<span data-ttu-id="32d0a-107">Per configurare le notifiche, fare clic su **Portale di pubblicazione** nel portale di Azure per il servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="32d0a-107">To configure notifications, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="32d0a-108">Verrà visualizzato il portale di pubblicazione di Gestione API.</span><span class="sxs-lookup"><span data-stu-id="32d0a-108">This takes you to the API Management publisher portal.</span></span>

![Portale di pubblicazione][api-management-management-console]

> [!NOTE] 
> <span data-ttu-id="32d0a-110">Se non è stata creata un'istanza del servizio Gestione API, vedere [Creare un'istanza di Gestione API][Create an API Management service instance] nell'esercitazione [Introduzione a Gestione API di Azure][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="32d0a-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

<span data-ttu-id="32d0a-111">Fare clic su **Notifiche** dal menu **Gestione API** a sinistra per visualizzare le notifiche disponibili.</span><span class="sxs-lookup"><span data-stu-id="32d0a-111">Click **Notifications** from the **API Management** menu on the left to view the available notifications.</span></span>

![Notifiche dell'editore][api-management-publisher-notifications]

<span data-ttu-id="32d0a-113">L'elenco di eventi seguente può essere configurato per le notifiche.</span><span class="sxs-lookup"><span data-stu-id="32d0a-113">The following list of events can be configured for notifications.</span></span>

* <span data-ttu-id="32d0a-114">**Richieste di sottoscrizione (che richiedono approvazione)** - I destinatari e gli utenti di posta elettronica specificati riceveranno notifiche tramite posta elettronica sulle richieste di sottoscrizione per prodotti API che richiedono approvazione.</span><span class="sxs-lookup"><span data-stu-id="32d0a-114">**Subscription requests (requiring approval)** - The specified email recipients and users will receive email notifications about subscription requests for API products requiring approval.</span></span>
* <span data-ttu-id="32d0a-115">**Nuove sottoscrizioni** - I destinatari e gli utenti di posta elettronica specificati riceveranno notifiche tramite posta elettronica sulle nuove sottoscrizioni a prodotti API.</span><span class="sxs-lookup"><span data-stu-id="32d0a-115">**New subscriptions** - The specified email recipients and users will receive email notifications about new API product subscriptions.</span></span>
* <span data-ttu-id="32d0a-116">**Richieste relative alla raccolta di applicazioni** - I destinatari e gli utenti di posta elettronica specificati riceveranno notifiche tramite posta elettronica quando nuove applicazioni vengono inviate alla raccolta di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="32d0a-116">**Application gallery requests** - The specified email recipients and users will receive email notifications when new applications are submitted to the application gallery.</span></span>
* <span data-ttu-id="32d0a-117">**BCC** - I destinatari e gli utenti di posta elettronica specificati riceveranno copie per conoscenza nascosta di tutti i messaggi di posta elettronica inviati agli sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="32d0a-117">**BCC** - The specified email recipients and users will receive email blind carbon copies of all emails sent to developers.</span></span>
* <span data-ttu-id="32d0a-118">**Nuovo problema o commento** - I destinatari e gli utenti di posta elettronica specificati riceveranno notifiche tramite posta elettronica quando un nuovo problema o commento viene inviato al portale per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="32d0a-118">**New issue or comment** - The specified email recipients and users will receive email notifications when a new issue or comment is submitted on the developer portal.</span></span>
* <span data-ttu-id="32d0a-119">**Messaggio di chiusura account** - I destinatari e gli utenti di posta elettronica specificati riceveranno notifiche tramite posta elettronica quando un account viene chiuso.</span><span class="sxs-lookup"><span data-stu-id="32d0a-119">**Close account message** - The specified email recipients and users will receive email notifications when an account is closed.</span></span>
* <span data-ttu-id="32d0a-120">**Raggiungimento limite quota sottoscrizione** - I destinatari e gli utenti di posta elettronica specificati riceveranno notifiche tramite posta elettronica quando l'uso della sottoscrizione si avvicina al limite di quota di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="32d0a-120">**Approaching subscription quota limit** - The following email recipients and users will receive email notifications when subscription usage gets close to usage quota.</span></span>

<span data-ttu-id="32d0a-121">Per ogni evento, è possibile specificare i destinatari di posta elettronica usando la casella di testo per l'indirizzo di posta elettronica oppure è possibile selezionare gli utenti da un elenco.</span><span class="sxs-lookup"><span data-stu-id="32d0a-121">For each event, you can specify email recipients using the email address text box or you can select users from a list.</span></span>

<span data-ttu-id="32d0a-122">Per specificare gli indirizzi di posta elettronica a cui inviare le notifiche, immettere tali indirizzi nella casella di testo relativa all'indirizzo di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="32d0a-122">To specify the email addresses to be notified, enter them in the email address text box.</span></span> <span data-ttu-id="32d0a-123">Se ci sono più indirizzi di posta elettronica, separarli usando delle virgole.</span><span class="sxs-lookup"><span data-stu-id="32d0a-123">If you have multiple email addresses, separate them using commas.</span></span>

![Destinatari delle notifiche][api-management-email-addresses]

<span data-ttu-id="32d0a-125">Per specificare gli utenti a cui inviare le notifiche, fare clic su **Aggiungi destinatario**, selezionare la casella di controllo corrispondente all'utente desiderato, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="32d0a-125">To specify the users to be notified, click **add recipient**, check the box beside the users to be notified, and click **OK**.</span></span>

> [!NOTE] 
> <span data-ttu-id="32d0a-126">Solo gli amministratori vengono visualizzati nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="32d0a-126">Only administrators are displayed in the list.</span></span>


<span data-ttu-id="32d0a-127">Dopo avere configurato i destinatari delle notifiche, fare clic su **Salva** per rendere effettivi i destinatari delle notifiche aggiornati.</span><span class="sxs-lookup"><span data-stu-id="32d0a-127">After configuring the notification recipients, click **Save** to apply the updated notification recipients.</span></span>

> [!NOTE] 
> <span data-ttu-id="32d0a-128">Se si esce dalla scheda **Notifiche dell'editore** , il portale di pubblicazione visualizza un avviso in caso di modifiche non salvate.</span><span class="sxs-lookup"><span data-stu-id="32d0a-128">If you navigate away from the **Publisher Notifications** tab the publisher portal alerts you if there are unsaved changes.</span></span>


## <span data-ttu-id="32d0a-129"><a name="email-templates"> </a>Configurare modelli di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="32d0a-129"><a name="email-templates"> </a>Configure email templates</span></span>
<span data-ttu-id="32d0a-130">Gestione API fornisce modelli di posta elettronica per i messaggi che vengono inviati durante l'amministrazione e l'uso del servizio.</span><span class="sxs-lookup"><span data-stu-id="32d0a-130">API Management provides email templates for the email messages that are sent in the course of administering and using the service.</span></span> <span data-ttu-id="32d0a-131">Sono forniti i modelli di posta elettronica indicati di seguito.</span><span class="sxs-lookup"><span data-stu-id="32d0a-131">The following email templates are provided.</span></span>

* <span data-ttu-id="32d0a-132">Invio alla raccolta di applicazioni approvato</span><span class="sxs-lookup"><span data-stu-id="32d0a-132">Application gallery submission approved</span></span>
* <span data-ttu-id="32d0a-133">Lettera di commiato sviluppatore</span><span class="sxs-lookup"><span data-stu-id="32d0a-133">Developer farewell letter</span></span>
* <span data-ttu-id="32d0a-134">Notifica raggiungimento limite quota sviluppatore</span><span class="sxs-lookup"><span data-stu-id="32d0a-134">Developer quota limit approaching notification</span></span>
* <span data-ttu-id="32d0a-135">Invito utente</span><span class="sxs-lookup"><span data-stu-id="32d0a-135">Invite user</span></span>
* <span data-ttu-id="32d0a-136">Nuovo commento aggiunto a problema</span><span class="sxs-lookup"><span data-stu-id="32d0a-136">New comment added to an issue</span></span>
* <span data-ttu-id="32d0a-137">Nuovo problema ricevuto</span><span class="sxs-lookup"><span data-stu-id="32d0a-137">New issue received</span></span>
* <span data-ttu-id="32d0a-138">Nuova sottoscrizione attivata</span><span class="sxs-lookup"><span data-stu-id="32d0a-138">New subscription activated</span></span>
* <span data-ttu-id="32d0a-139">Conferma rinnovo sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="32d0a-139">Subscription renewed confirmation</span></span>
* <span data-ttu-id="32d0a-140">Richiesta sottoscrizione rifiutata</span><span class="sxs-lookup"><span data-stu-id="32d0a-140">Subscription request declines</span></span>
* <span data-ttu-id="32d0a-141">Richiesta sottoscrizione ricevuta</span><span class="sxs-lookup"><span data-stu-id="32d0a-141">Subscription request received</span></span>

<span data-ttu-id="32d0a-142">Questi modelli possono essere modificati a piacimento.</span><span class="sxs-lookup"><span data-stu-id="32d0a-142">These templates can be modified as desired.</span></span>

<span data-ttu-id="32d0a-143">Per visualizzare e configurare i modelli di posta elettronica per la propria istanza di Gestione API, fare clic su **Notifiche** dal menu **Gestione API** a sinistra, quindi selezionare la scheda **Modelli di posta elettronica**.</span><span class="sxs-lookup"><span data-stu-id="32d0a-143">To view and configure the email templates for your API Management instance, click **Notifications** from the **API Management** menu on the left, and select the **Email Templates** tab.</span></span>

![Modelli di posta elettronica][api-management-email-templates]

<span data-ttu-id="32d0a-145">Per visualizzare o modificare un modello specifico, selezionarlo dall'elenco a discesa **Modelli** .</span><span class="sxs-lookup"><span data-stu-id="32d0a-145">To view or modify a specific template, select it from the **Templates** drop-down list.</span></span>

![Elenco modelli di posta elettronica][api-management-email-templates-list]

<span data-ttu-id="32d0a-147">Ogni modello di posta elettronica ha un oggetto in testo normale e una definizione di corpo in formato HTML.</span><span class="sxs-lookup"><span data-stu-id="32d0a-147">Each email template has a subject in plain text, and a body definition in HTML format.</span></span> <span data-ttu-id="32d0a-148">Ogni elemento può essere personalizzato a piacimento.</span><span class="sxs-lookup"><span data-stu-id="32d0a-148">Each item can be customized as desired.</span></span>

![Editor dei modelli di posta elettronica][api-management-email-template]

<span data-ttu-id="32d0a-150">L'elenco **Parametri** contiene un elenco di parametri che, quando inserito nell'oggetto o nel corpo, verrà sostituito dal valore designato quando viene inviato il messaggio di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="32d0a-150">The **Parameters** list contains a list of parameters, which when inserted into the subject or body, will be replaced the designated value when the email is sent.</span></span> <span data-ttu-id="32d0a-151">Per inserire un parametro, posizionare il cursore dove si vuole inserire il parametro, quindi fare clic sulla freccia a sinistra del nome del parametro.</span><span class="sxs-lookup"><span data-stu-id="32d0a-151">To insert a parameter, place the cursor where you wish the parameter to go, and click the arrow to the left of the parameter name.</span></span>

<span data-ttu-id="32d0a-152">Fare clic su **Anteprima** o **Invia test** per verificare l'aspetto del messaggio o per inviare un messaggio di prova.</span><span class="sxs-lookup"><span data-stu-id="32d0a-152">Click **Preview** or **Send a test** to see how the email will look or send a test email.</span></span>

> [!NOTE] 
> <span data-ttu-id="32d0a-153">I parametri non vengono sostituiti con valori effettivi quando si visualizzano anteprime o si inviano messaggi di prova.</span><span class="sxs-lookup"><span data-stu-id="32d0a-153">The parameters are not replaced with actual values when previewing or sending a test.</span></span>

<span data-ttu-id="32d0a-154">Per salvare le modifiche al modello di posta elettronica, fare clic su **Salva** oppure, per annullare le modifiche, fare clic su **Annulla**.</span><span class="sxs-lookup"><span data-stu-id="32d0a-154">To save the changes to the email template, click **Save**, or to cancel the changes click **Cancel**.</span></span>
 

[api-management-management-console]: ./media/api-management-howto-configure-notifications/api-management-management-console.png
[api-management-publisher-notifications]: ./media/api-management-howto-configure-notifications/api-management-publisher-notifications.png
[api-management-email-addresses]: ./media/api-management-howto-configure-notifications/api-management-email-addresses.png


[api-management-email-templates]: ./media/api-management-howto-configure-notifications/api-management-email-templates.png
[api-management-email-templates-list]: ./media/api-management-howto-configure-notifications/api-management-email-templates-list.png
[api-management-email-template]: ./media/api-management-howto-configure-notifications/api-management-email-template.png


[Configure publisher notifications]: #publisher-notifications
[Configure email templates]: #email-templates

[How to create and use groups]: api-management-howto-create-groups.md
[How to associate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
