---
title: aaaHow gestire gli account utente in Gestione API di Azure | Documenti Microsoft
description: Informazioni su come toocreate o invita gli utenti in Gestione API di Azure
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 078abfa5-1e4f-4c9d-b9c7-a172bd19c1a2
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 3966f4454e29621d7c615beefee352ec91b48b2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-user-accounts-in-azure-api-management"></a><span data-ttu-id="50b03-103">La modalità di account utente di toomanage in Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="50b03-103">How toomanage user accounts in Azure API Management</span></span>
<span data-ttu-id="50b03-104">In Gestione API, gli sviluppatori sono utenti hello di hello API esposta tramite Gestione API.</span><span class="sxs-lookup"><span data-stu-id="50b03-104">In API Management, developers are hello users of hello APIs that you expose using API Management.</span></span> <span data-ttu-id="50b03-105">Questa guida Mostra toohow toocreate e invita gli sviluppatori toouse hello API e i prodotti che si apportano toothem disponibili con l'istanza di gestione API.</span><span class="sxs-lookup"><span data-stu-id="50b03-105">This guide shows toohow toocreate and invite developers toouse hello APIs and products that you make available toothem with your API Management instance.</span></span> <span data-ttu-id="50b03-106">Per informazioni sulla gestione degli account utente a livello di codice, vedere hello [entità utente](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentazione in hello [API REST di gestione](https://msdn.microsoft.com/library/azure/dn776326.aspx) riferimento.</span><span class="sxs-lookup"><span data-stu-id="50b03-106">For information on managing user accounts programmatically, see hello [User entity](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentation in hello [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) reference.</span></span>

## <span data-ttu-id="50b03-107"><a name="create-developer"> </a>Creare un nuovo sviluppatore</span><span class="sxs-lookup"><span data-stu-id="50b03-107"><a name="create-developer"> </a>Create a new developer</span></span>
<span data-ttu-id="50b03-108">toocreate uno sviluppatore di nuovo, fare clic su **portale di pubblicazione** in hello portale di Azure per il servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="50b03-108">toocreate a new developer, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="50b03-109">Consente di procedere toohello portale di pubblicazione di gestione API.</span><span class="sxs-lookup"><span data-stu-id="50b03-109">This takes you toohello API Management publisher portal.</span></span> <span data-ttu-id="50b03-110">Se non è ancora stato creato un'istanza del servizio Gestione API, vedere [creare un'istanza del servizio Gestione API] [ Create an API Management service instance] in hello [Introduzione a gestione API di Azure] [ Get started with Azure API Management] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="50b03-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

![Portale di pubblicazione][api-management-management-console]

<span data-ttu-id="50b03-112">Fare clic su **utenti** da hello **gestione API** menu hello a sinistra e quindi fare clic su **aggiungere utente**.</span><span class="sxs-lookup"><span data-stu-id="50b03-112">Click **Users** from hello **API Management** menu on hello left, and then click **add user**.</span></span>

![Create developer][api-management-create-developer]

<span data-ttu-id="50b03-114">Immettere hello **posta elettronica**, **Password**, e **nome** nuovo sviluppatore hello e fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="50b03-114">Enter hello **Email**, **Password**, and **Name** for hello new developer and click **Save**.</span></span>

![Create developer][api-management-add-new-user]

<span data-ttu-id="50b03-116">Per impostazione predefinita, gli account appena creato per sviluppatori sono **Active**e associati hello **sviluppatori** gruppo.</span><span class="sxs-lookup"><span data-stu-id="50b03-116">By default, newly created developer accounts are **Active**, and associated with hello **Developers** group.</span></span>

![New developer][api-management-new-developer]

<span data-ttu-id="50b03-118">Gli account sviluppatore in un **active** lo stato può essere utilizzato tooaccess tutte le API di hello per le quali sono le sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="50b03-118">Developer accounts that are in an **active** state can be used tooaccess all of hello APIs for which they have subscriptions.</span></span> <span data-ttu-id="50b03-119">sviluppatore di tooassociate hello appena creato con altri gruppi aggiuntivi, vedere [come i gruppi con gli sviluppatori tooassociate][How tooassociate groups with developers].</span><span class="sxs-lookup"><span data-stu-id="50b03-119">tooassociate hello newly created developer with additional groups, see [How tooassociate groups with developers][How tooassociate groups with developers].</span></span>

## <span data-ttu-id="50b03-120"><a name="invite-developer"> </a>Invitare uno sviluppatore</span><span class="sxs-lookup"><span data-stu-id="50b03-120"><a name="invite-developer"> </a>Invite a developer</span></span>
<span data-ttu-id="50b03-121">tooinvite uno sviluppatore, fare clic su **utenti** da hello **gestione API** menu hello a sinistra e quindi fare clic su **invitare utente**.</span><span class="sxs-lookup"><span data-stu-id="50b03-121">tooinvite a developer, click **Users** from hello **API Management** menu on hello left, and then click **Invite User**.</span></span>

![Invite developer][api-management-invite-developer]

<span data-ttu-id="50b03-123">Immettere l'indirizzo di posta elettronica e nome hello dello sviluppatore hello e fare clic su **invitare**.</span><span class="sxs-lookup"><span data-stu-id="50b03-123">Enter hello name and email address of hello developer, and click **Invite**.</span></span>

![Invite developer][api-management-invite-developer-window]

<span data-ttu-id="50b03-125">Viene visualizzato un messaggio di conferma, ma developer hello appena invito non è disponibile nell'elenco di hello fino a dopo aver accettato l'invito hello.</span><span class="sxs-lookup"><span data-stu-id="50b03-125">A confirmation message is displayed, but hello newly invited developer does not appear in hello list until after they accept hello invitation.</span></span> 

![Invite confirmation][api-management-invite-developer-confirmation]

<span data-ttu-id="50b03-127">Quando uno sviluppatore è visualizzato un messaggio, viene inviato un messaggio toohello developer.</span><span class="sxs-lookup"><span data-stu-id="50b03-127">When a developer is invited, an email is sent toohello developer.</span></span> <span data-ttu-id="50b03-128">generato con un modello e personalizzabile.</span><span class="sxs-lookup"><span data-stu-id="50b03-128">This email is generated using a template and is customizable.</span></span> <span data-ttu-id="50b03-129">Per altre informazioni, vedere [Configurare modelli di posta elettronica][Configure email templates].</span><span class="sxs-lookup"><span data-stu-id="50b03-129">For more information, see [Configure email templates][Configure email templates].</span></span>

<span data-ttu-id="50b03-130">Dopo aver accettato hello invito, account hello diventa attivo.</span><span class="sxs-lookup"><span data-stu-id="50b03-130">Once hello invitation is accepted, hello account becomes active.</span></span>

## <span data-ttu-id="50b03-131"><a name="block-developer"></a> Disattivare o riattivare un account sviluppatore</span><span class="sxs-lookup"><span data-stu-id="50b03-131"><a name="block-developer"> </a> Deactivate or reactivate a developer account</span></span>
<span data-ttu-id="50b03-132">Per impostazione predefinita, un nuovo account sviluppatore creato o invitato è **Attivo**.</span><span class="sxs-lookup"><span data-stu-id="50b03-132">By default, newly created or invited developer accounts are **Active**.</span></span> <span data-ttu-id="50b03-133">Fare clic su un account sviluppatore, toodeactivate **blocco**.</span><span class="sxs-lookup"><span data-stu-id="50b03-133">toodeactivate a developer account, click **Block**.</span></span> <span data-ttu-id="50b03-134">Fare clic su un account sviluppatore bloccati, tooreactivate **attiva**.</span><span class="sxs-lookup"><span data-stu-id="50b03-134">tooreactivate a blocked developer account, click **Activate**.</span></span> <span data-ttu-id="50b03-135">Un account sviluppatore bloccati non possa accedere al portale per sviluppatori hello o chiamare le API.</span><span class="sxs-lookup"><span data-stu-id="50b03-135">A blocked developer account can not access hello developer portal or call any APIs.</span></span> <span data-ttu-id="50b03-136">Fare clic su un account utente, toodelete **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="50b03-136">toodelete a user account, click **Delete**.</span></span>

![Block developer][api-management-new-developer]

## <a name="reset-a-user-password"></a><span data-ttu-id="50b03-138">Reimpostare la password di un utente</span><span class="sxs-lookup"><span data-stu-id="50b03-138">Reset a user password</span></span>
<span data-ttu-id="50b03-139">password di hello tooreset per un account utente, fare clic su nome hello dell'account di hello.</span><span class="sxs-lookup"><span data-stu-id="50b03-139">tooreset hello password for a user account, click hello name of hello account.</span></span>

![Reimpostazione delle password][api-management-view-developer]

<span data-ttu-id="50b03-141">Fare clic su **reimpostazione password** toosend tooreset di utente toohello un collegamento la propria password.</span><span class="sxs-lookup"><span data-stu-id="50b03-141">Click **Reset password** toosend a link toohello user tooreset their password.</span></span>

![Reimpostazione delle password][api-management-reset-password]

<span data-ttu-id="50b03-143">tooprogrammatically gestire account utente, vedere hello [entità utente](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentazione in hello [API REST di gestione](https://msdn.microsoft.com/library/azure/dn776326.aspx) riferimento.</span><span class="sxs-lookup"><span data-stu-id="50b03-143">tooprogrammatically work with user accounts, see hello [User entity](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentation in hello [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) reference.</span></span> <span data-ttu-id="50b03-144">un valore specifico utente account password tooa tooreset, è possibile utilizzare hello [aggiornare un utente](https://msdn.microsoft.com/library/azure/dn776330.aspx#UpdateUser) operazione e specificare la password desiderata hello.</span><span class="sxs-lookup"><span data-stu-id="50b03-144">tooreset a user account password tooa specific value, you can use hello [Update a user](https://msdn.microsoft.com/library/azure/dn776330.aspx#UpdateUser) operation and specify hello desired password.</span></span>

## <a name="pending-verification"></a><span data-ttu-id="50b03-145">Verifica in sospeso</span><span class="sxs-lookup"><span data-stu-id="50b03-145">Pending verification</span></span>
![Verifica in sospeso][api-management-pending-verification]

## <span data-ttu-id="50b03-147"><a name="next-steps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="50b03-147"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="50b03-148">Dopo aver creato un account sviluppatore, è possibile associarlo a ruoli ed effettuare la sottoscrizione tooproducts e API.</span><span class="sxs-lookup"><span data-stu-id="50b03-148">Once a developer account is created, you can associate it with roles and subscribe it tooproducts and APIs.</span></span> <span data-ttu-id="50b03-149">Per ulteriori informazioni, vedere [come toocreate e utilizzare gruppi][How toocreate and use groups].</span><span class="sxs-lookup"><span data-stu-id="50b03-149">For more information, see [How toocreate and use groups][How toocreate and use groups].</span></span>

[api-management-management-console]: ./media/api-management-howto-create-or-invite-developers/api-management-management-console.png
[api-management-add-new-user]: ./media/api-management-howto-create-or-invite-developers/api-management-add-new-user.png
[api-management-create-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-create-developer.png
[api-management-invite-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-invite-developer.png
[api-management-new-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-new-developer.png
[api-management-invite-developer-window]: ./media/api-management-howto-create-or-invite-developers/api-management-invite-developer-window.png
[api-management-invite-developer-confirmation]: ./media/api-management-howto-create-or-invite-developers/api-management-invite-developer-confirmation.png
[api-management-pending-verification]: ./media/api-management-howto-create-or-invite-developers/api-management-pending-verification.png
[api-management-view-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-view-developer.png
[api-management-reset-password]: ./media/api-management-howto-create-or-invite-developers/api-management-reset-password.png


[Create a new developer]: #create-developer
[Invite a developer]: #invite-developer
[Deactivate or reactivate a developer account]: #block-developer
[Next steps]: #next-steps
[How toocreate and use groups]: api-management-howto-create-groups.md
[How tooassociate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Configure email templates]: api-management-howto-configure-notifications.md#email-templates
