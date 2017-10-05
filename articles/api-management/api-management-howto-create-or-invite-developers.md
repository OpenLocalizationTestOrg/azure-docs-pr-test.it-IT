---
title: Come gestire gli account utente in Gestione API di Azure | Microsoft Docs
description: Informazioni su come creare o invitare gli utenti in Gestione API di Azure.
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
ms.openlocfilehash: d3a50f6d22cbf1797f580078bc0d2cc9cefe5064
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-user-accounts-in-azure-api-management"></a><span data-ttu-id="f0e0b-103">Come gestire gli account utente in Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="f0e0b-103">How to manage user accounts in Azure API Management</span></span>
<span data-ttu-id="f0e0b-104">In Gestione API gli sviluppatori sono gli utenti delle API esposte con Gestione API.</span><span class="sxs-lookup"><span data-stu-id="f0e0b-104">In API Management, developers are the users of the APIs that you expose using API Management.</span></span> <span data-ttu-id="f0e0b-105">In questa guida viene illustrato come creare e invitare gli sviluppatori a usare le API e i prodotti resi disponibili con l'istanza di Gestione API.</span><span class="sxs-lookup"><span data-stu-id="f0e0b-105">This guide shows to how to create and invite developers to use the APIs and products that you make available to them with your API Management instance.</span></span> <span data-ttu-id="f0e0b-106">Per informazioni sulla gestione degli account utente a livello di codice, vedere la documentazione [Entità utente](https://msdn.microsoft.com/library/azure/dn776330.aspx) nel riferimento [API Management REST (REST di gestione API)](https://msdn.microsoft.com/library/azure/dn776326.aspx).</span><span class="sxs-lookup"><span data-stu-id="f0e0b-106">For information on managing user accounts programmatically, see the [User entity](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentation in the [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) reference.</span></span>

## <span data-ttu-id="f0e0b-107"><a name="create-developer"> </a>Creare un nuovo sviluppatore</span><span class="sxs-lookup"><span data-stu-id="f0e0b-107"><a name="create-developer"> </a>Create a new developer</span></span>
<span data-ttu-id="f0e0b-108">Per creare un nuovo sviluppatore, fare clic su **Portale di pubblicazione** nel portale di Azure per il servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="f0e0b-108">To create a new developer, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="f0e0b-109">Verrà visualizzato il portale di pubblicazione di Gestione API.</span><span class="sxs-lookup"><span data-stu-id="f0e0b-109">This takes you to the API Management publisher portal.</span></span> <span data-ttu-id="f0e0b-110">Se non è stata creata un'istanza del servizio Gestione API, vedere [Creare un'istanza di Gestione API][Create an API Management service instance] nell'esercitazione [Introduzione a Gestione API di Azure][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="f0e0b-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

![Portale di pubblicazione][api-management-management-console]

<span data-ttu-id="f0e0b-112">Fare clic su **Utenti** dal menu **Gestione API** sulla sinistra, quindi scegliere **aggiungi utente**.</span><span class="sxs-lookup"><span data-stu-id="f0e0b-112">Click **Users** from the **API Management** menu on the left, and then click **add user**.</span></span>

![Create developer][api-management-create-developer]

<span data-ttu-id="f0e0b-114">Immettere **Indirizzo e-mail**, **Password** e **Nome** per il nuovo sviluppatore, quindi fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="f0e0b-114">Enter the **Email**, **Password**, and **Name** for the new developer and click **Save**.</span></span>

![Create developer][api-management-add-new-user]

<span data-ttu-id="f0e0b-116">Per impostazione predefinita, i nuovi account sviluppatore creati sono **attivi** e associati al gruppo **Sviluppatori**.</span><span class="sxs-lookup"><span data-stu-id="f0e0b-116">By default, newly created developer accounts are **Active**, and associated with the **Developers** group.</span></span>

![New developer][api-management-new-developer]

<span data-ttu-id="f0e0b-118">Gli account sviluppatore con stato **attivo** possono essere usati per accedere a tutte le API per cui dispongono di sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="f0e0b-118">Developer accounts that are in an **active** state can be used to access all of the APIs for which they have subscriptions.</span></span> <span data-ttu-id="f0e0b-119">Per associare il nuovo sviluppatore creato ad altri gruppi, vedere [Come associare gruppi a sviluppatori][How to associate groups with developers].</span><span class="sxs-lookup"><span data-stu-id="f0e0b-119">To associate the newly created developer with additional groups, see [How to associate groups with developers][How to associate groups with developers].</span></span>

## <span data-ttu-id="f0e0b-120"><a name="invite-developer"> </a>Invitare uno sviluppatore</span><span class="sxs-lookup"><span data-stu-id="f0e0b-120"><a name="invite-developer"> </a>Invite a developer</span></span>
<span data-ttu-id="f0e0b-121">Per invitare uno sviluppatore, fare clic su **Utenti** dal menu **Gestione API** sulla sinistra, quindi scegliere **Invita utente**.</span><span class="sxs-lookup"><span data-stu-id="f0e0b-121">To invite a developer, click **Users** from the **API Management** menu on the left, and then click **Invite User**.</span></span>

![Invite developer][api-management-invite-developer]

<span data-ttu-id="f0e0b-123">Immettere il nome e l'indirizzo di posta elettronica e fare clic su **Invita**.</span><span class="sxs-lookup"><span data-stu-id="f0e0b-123">Enter the name and email address of the developer, and click **Invite**.</span></span>

![Invite developer][api-management-invite-developer-window]

<span data-ttu-id="f0e0b-125">Viene visualizzato un messaggio di conferma, ma il nuovo sviluppatore invitato non appare nell'elenco finché l'invito non viene accettato.</span><span class="sxs-lookup"><span data-stu-id="f0e0b-125">A confirmation message is displayed, but the newly invited developer does not appear in the list until after they accept the invitation.</span></span> 

![Invite confirmation][api-management-invite-developer-confirmation]

<span data-ttu-id="f0e0b-127">Quando uno sviluppatore viene invitato, gli viene inviato un messaggio di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="f0e0b-127">When a developer is invited, an email is sent to the developer.</span></span> <span data-ttu-id="f0e0b-128">generato con un modello e personalizzabile.</span><span class="sxs-lookup"><span data-stu-id="f0e0b-128">This email is generated using a template and is customizable.</span></span> <span data-ttu-id="f0e0b-129">Per altre informazioni, vedere [Configurare modelli di posta elettronica][Configure email templates].</span><span class="sxs-lookup"><span data-stu-id="f0e0b-129">For more information, see [Configure email templates][Configure email templates].</span></span>

<span data-ttu-id="f0e0b-130">Dopo l'accettazione dell'invito, l'account diventa attivo.</span><span class="sxs-lookup"><span data-stu-id="f0e0b-130">Once the invitation is accepted, the account becomes active.</span></span>

## <span data-ttu-id="f0e0b-131"><a name="block-developer"> </a> Disattivare o riattivare un account sviluppatore</span><span class="sxs-lookup"><span data-stu-id="f0e0b-131"><a name="block-developer"> </a> Deactivate or reactivate a developer account</span></span>
<span data-ttu-id="f0e0b-132">Per impostazione predefinita, un nuovo account sviluppatore creato o invitato è **Attivo**.</span><span class="sxs-lookup"><span data-stu-id="f0e0b-132">By default, newly created or invited developer accounts are **Active**.</span></span> <span data-ttu-id="f0e0b-133">Per disattivare un account sviluppatore, fare clic su **Blocca**.</span><span class="sxs-lookup"><span data-stu-id="f0e0b-133">To deactivate a developer account, click **Block**.</span></span> <span data-ttu-id="f0e0b-134">Per riattivare un account sviluppatore bloccato, fare clic su **Attiva**.</span><span class="sxs-lookup"><span data-stu-id="f0e0b-134">To reactivate a blocked developer account, click **Activate**.</span></span> <span data-ttu-id="f0e0b-135">Un account sviluppatore bloccato non può accedere al portale per sviluppatori né chiamare le API.</span><span class="sxs-lookup"><span data-stu-id="f0e0b-135">A blocked developer account can not access the developer portal or call any APIs.</span></span> <span data-ttu-id="f0e0b-136">Per eliminare un account utente, fare clic su **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="f0e0b-136">To delete a user account, click **Delete**.</span></span>

![Block developer][api-management-new-developer]

## <a name="reset-a-user-password"></a><span data-ttu-id="f0e0b-138">Reimpostare la password di un utente</span><span class="sxs-lookup"><span data-stu-id="f0e0b-138">Reset a user password</span></span>
<span data-ttu-id="f0e0b-139">Per reimpostare la password per un account utente, fare clic sul nome dell'account.</span><span class="sxs-lookup"><span data-stu-id="f0e0b-139">To reset the password for a user account, click the name of the account.</span></span>

![Reimposta password][api-management-view-developer]

<span data-ttu-id="f0e0b-141">Fare clic su **Reimposta password** per inviare all'utente un collegamento per la reimpostazione della password.</span><span class="sxs-lookup"><span data-stu-id="f0e0b-141">Click **Reset password** to send a link to the user to reset their password.</span></span>

![Reimpostazione delle password][api-management-reset-password]

<span data-ttu-id="f0e0b-143">Per lavorare con gli account utente a livello di codice, vedere la documentazione [Entità utente](https://msdn.microsoft.com/library/azure/dn776330.aspx) nel riferimento [API Management REST (REST di gestione API)](https://msdn.microsoft.com/library/azure/dn776326.aspx).</span><span class="sxs-lookup"><span data-stu-id="f0e0b-143">To programmatically work with user accounts, see the [User entity](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentation in the [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) reference.</span></span> <span data-ttu-id="f0e0b-144">Per reimpostare la password di un account utente su un valore specifico, è possibile usare la procedura [Update a user (Aggiornamento di un utente)](https://msdn.microsoft.com/library/azure/dn776330.aspx#UpdateUser) e specificare la password desiderata.</span><span class="sxs-lookup"><span data-stu-id="f0e0b-144">To reset a user account password to a specific value, you can use the [Update a user](https://msdn.microsoft.com/library/azure/dn776330.aspx#UpdateUser) operation and specify the desired password.</span></span>

## <a name="pending-verification"></a><span data-ttu-id="f0e0b-145">Verifica in sospeso</span><span class="sxs-lookup"><span data-stu-id="f0e0b-145">Pending verification</span></span>
![Verifica in sospeso][api-management-pending-verification]

## <span data-ttu-id="f0e0b-147"><a name="next-steps"> </a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f0e0b-147"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="f0e0b-148">Dopo aver creato un account sviluppatore, è possibile associarlo ai ruoli ed effettuarne la sottoscrizione a prodotti e API.</span><span class="sxs-lookup"><span data-stu-id="f0e0b-148">Once a developer account is created, you can associate it with roles and subscribe it to products and APIs.</span></span> <span data-ttu-id="f0e0b-149">Per altre informazioni, vedere [Come creare e usare i gruppi][How to create and use groups].</span><span class="sxs-lookup"><span data-stu-id="f0e0b-149">For more information, see [How to create and use groups][How to create and use groups].</span></span>

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
[How to create and use groups]: api-management-howto-create-groups.md
[How to associate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Configure email templates]: api-management-howto-configure-notifications.md#email-templates
