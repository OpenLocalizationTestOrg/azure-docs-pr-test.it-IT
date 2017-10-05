---
title: Gestire gli account di sviluppatori tramite i gruppi in Gestione API di Azure | Documentazione Microsoft
description: Informazioni su come gestire gli account di sviluppatori tramite i gruppi in Gestione API di Azure.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 33660b45-442f-44be-9a4a-1899d7f699b0
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: b4d71cdfbab535b02542fbb26c7555265e5f9c37
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-and-use-groups-to-manage-developer-accounts-in-azure-api-management"></a><span data-ttu-id="88a52-103">Come creare e usare gruppi per gestire account di sviluppatori in Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="88a52-103">How to create and use groups to manage developer accounts in Azure API Management</span></span>
<span data-ttu-id="88a52-104">In Gestione API i gruppi permettono di gestire quali prodotti sono visibili per gli sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="88a52-104">In API Management, groups are used to manage the visibility of products to developers.</span></span> <span data-ttu-id="88a52-105">I prodotti vengono innanzitutto resi visibili ai gruppi, quindi gli sviluppatori in quei gruppi possono visualizzare e sottoscriversi ai prodotti associati ai gruppi.</span><span class="sxs-lookup"><span data-stu-id="88a52-105">Products are first made visible to groups, and then developers in those groups can view and subscribe to the products that are associated with the groups.</span></span> 

<span data-ttu-id="88a52-106">In Gestione API sono inclusi i gruppi di sistema non modificabili seguenti.</span><span class="sxs-lookup"><span data-stu-id="88a52-106">API Management has the following immutable system groups.</span></span>

* <span data-ttu-id="88a52-107">**Amministratori** : gli amministratori delle sottoscrizioni di Azure sono membri di questo gruppo.</span><span class="sxs-lookup"><span data-stu-id="88a52-107">**Administrators** - Azure subscription administrators are members of this group.</span></span> <span data-ttu-id="88a52-108">Gli amministratori gestiscono le istanze del servizio Gestione API e creano le API, le operazioni e i prodotti usati dagli sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="88a52-108">Administrators manage API Management service instances, creating the APIs, operations, and products that are used by developers.</span></span>
* <span data-ttu-id="88a52-109">**Sviluppatori** : gli utenti autenticati del portale per sviluppatori rientrano in questo gruppo.</span><span class="sxs-lookup"><span data-stu-id="88a52-109">**Developers** - Authenticated developer portal users fall into this group.</span></span> <span data-ttu-id="88a52-110">Gli sviluppatori sono i clienti che compilano applicazioni usando le API.</span><span class="sxs-lookup"><span data-stu-id="88a52-110">Developers are the customers that build applications using your APIs.</span></span> <span data-ttu-id="88a52-111">Agli sviluppatori viene concesso di accedere al portale per sviluppatori e di creare applicazioni che chiamano le operazioni di un'API.</span><span class="sxs-lookup"><span data-stu-id="88a52-111">Developers are granted access to the developer portal and build applications that call the operations of an API.</span></span>
* <span data-ttu-id="88a52-112">**Guest** : gli utenti non autenticati del portale per sviluppatori, ad esempio i potenziali clienti, che visitano il portale per sviluppatori di un'istanza di Gestione API rientrano in questo gruppo.</span><span class="sxs-lookup"><span data-stu-id="88a52-112">**Guests** - Unauthenticated developer portal users, such as prospective customers visiting the developer portal of an API Management instance fall into this group.</span></span> <span data-ttu-id="88a52-113">È possibile concedere agli utenti guest un determinato livello di accesso di sola lettura, ad esempio la possibilità di visualizzare le API ma non di chiamarle.</span><span class="sxs-lookup"><span data-stu-id="88a52-113">They can be granted certain read-only access, such as the ability to view APIs but not call them.</span></span>

<span data-ttu-id="88a52-114">Oltre a questi gruppi di sistema, gli amministratori possono creare gruppi personalizzati oppure [sfruttare i gruppi esterni nei tenant di Azure Active Directory associati][leverage external groups in associated Azure Active Directory tenants].</span><span class="sxs-lookup"><span data-stu-id="88a52-114">In addition to these system groups, administrators can create custom groups or [leverage external groups in associated Azure Active Directory tenants][leverage external groups in associated Azure Active Directory tenants].</span></span> <span data-ttu-id="88a52-115">È possibile usare gruppi personalizzati ed esterni assieme ai gruppi di sistema per offrire agli sviluppatori visibilità e accesso ai prodotti API.</span><span class="sxs-lookup"><span data-stu-id="88a52-115">Custom and external groups can be used alongside system groups in giving developers visibility and access to API products.</span></span> <span data-ttu-id="88a52-116">Ad esempio, si può creare un gruppo personalizzato per gli sviluppatori affiliati a un'organizzazione partner specifica e consentire loro di accedere alle API da un prodotto che contiene solo le API pertinenti.</span><span class="sxs-lookup"><span data-stu-id="88a52-116">For example, you could create one custom group for developers affiliated with a specific partner organization and allow them access to the APIs from a product containing relevant APIs only.</span></span> <span data-ttu-id="88a52-117">Un utente può essere un membro di più gruppi.</span><span class="sxs-lookup"><span data-stu-id="88a52-117">A user can be a member of more than one group.</span></span>

<span data-ttu-id="88a52-118">Questa guida illustra come gli amministratori di un'istanza di Gestione API possono aggiungere nuovi gruppi e associarli a prodotti e sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="88a52-118">This guide shows how administrators of an API Management instance can add new groups and associate them with products and developers.</span></span>

> [!NOTE]
> <span data-ttu-id="88a52-119">Oltre a creare e gestire gruppi nel portale di pubblicazione, è possibile creare e gestire i gruppi utilizzando l'entità API REST di gestione [Gruppo](https://msdn.microsoft.com/library/azure/dn776329.aspx) .</span><span class="sxs-lookup"><span data-stu-id="88a52-119">In addition to creating and managing groups in the publisher portal, you can create and manage your groups using the API Management REST API [Group](https://msdn.microsoft.com/library/azure/dn776329.aspx) entity.</span></span>
> 
> 

## <span data-ttu-id="88a52-120"><a name="create-group"> </a>Creare un gruppo</span><span class="sxs-lookup"><span data-stu-id="88a52-120"><a name="create-group"> </a>Create a group</span></span>
<span data-ttu-id="88a52-121">Per creare un nuovo gruppo, fare clic su **Portale di pubblicazione** nel portale di Azure per il servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="88a52-121">To create a new group, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="88a52-122">Verrà visualizzato il portale di pubblicazione di Gestione API.</span><span class="sxs-lookup"><span data-stu-id="88a52-122">This takes you to the API Management publisher portal.</span></span>

![Portale di pubblicazione][api-management-management-console]

> <span data-ttu-id="88a52-124">Se non è stata creata un'istanza del servizio Gestione API, vedere [Creare un'istanza di Gestione API][Create an API Management service instance] nell'esercitazione [Introduzione a Gestione API di Azure][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="88a52-124">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="88a52-125">Fare clic su **Gruppi** dal menu **Gestione API** sulla sinistra, quindi scegliere **Aggiungi gruppo**.</span><span class="sxs-lookup"><span data-stu-id="88a52-125">Click **Groups** from the **API Management** menu on the left, and then click **Add Group**.</span></span>

![Aggiungere un nuovo gruppo][api-management-add-group]

<span data-ttu-id="88a52-127">Immettere un nome univoco per il gruppo e una descrizione facoltativa, quindi fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="88a52-127">Enter a unique name for the group and an optional description, and click **Save**.</span></span>

![Aggiungere un nuovo gruppo][api-management-add-group-window]

<span data-ttu-id="88a52-129">Il nuovo gruppo viene visualizzato nella scheda relativa ai gruppi.</span><span class="sxs-lookup"><span data-stu-id="88a52-129">The new group is displayed in the groups tab.</span></span> <span data-ttu-id="88a52-130">Per modificare il **Nome** o la **Descrizione** del gruppo, fare clic sul nome del gruppo nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="88a52-130">To edit the **Name** or **Description** of the group, click the name of the group in the list.</span></span> <span data-ttu-id="88a52-131">Per eliminare il gruppo, fare clic su **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="88a52-131">To delete the group, click **Delete**.</span></span>

![Gruppo aggiunto][api-management-new-group]

<span data-ttu-id="88a52-133">Ora che il gruppo è stato creato, può essere associato a prodotti e sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="88a52-133">Now that the group is created, it can be associated with products and developers.</span></span>

## <span data-ttu-id="88a52-134"><a name="associate-group-product"> </a>Associare un gruppo a un prodotto</span><span class="sxs-lookup"><span data-stu-id="88a52-134"><a name="associate-group-product"> </a>Associate a group with a product</span></span>
<span data-ttu-id="88a52-135">Per associare un gruppo a un prodotto, fare clic su **Prodotti** dal menu **Gestione API** a sinistra, quindi fare clic sul nome del prodotto desiderato.</span><span class="sxs-lookup"><span data-stu-id="88a52-135">To associate a group with a product, click **Products** from the **API Management** menu on the left, and then click the name of the desired product.</span></span>

![Visibilità dei prodotti][api-management-add-group-to-product]

<span data-ttu-id="88a52-137">Selezionare la scheda **Visibilità** per aggiungere e rimuovere gruppi e per visualizzare gli attuali gruppi associati al prodotto.</span><span class="sxs-lookup"><span data-stu-id="88a52-137">Select the **Visibility** tab to add and remove groups, and to view the current groups for the product.</span></span> <span data-ttu-id="88a52-138">Per aggiungere o rimuovere gruppi, selezionare o deselezionare le caselle di controllo per i gruppi desiderati, quindi fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="88a52-138">To add or remove groups, check or uncheck the checkboxes for the desired groups and click **Save**.</span></span>

![Visibilità dei prodotti][api-management-add-group-to-product-visibility]

> [!NOTE]
> <span data-ttu-id="88a52-140">Per aggiungere gruppi di Azure Active Directory, vedere [Come autorizzare gli account per sviluppatore usando Azure Active Directory in Gestione API di Azure](api-management-howto-aad.md).</span><span class="sxs-lookup"><span data-stu-id="88a52-140">To add Azure Active Directory groups, see [How to authorize developer accounts using Azure Active Directory in Azure API Management](api-management-howto-aad.md).</span></span>
> 
> <span data-ttu-id="88a52-141">Per configurare gruppi dalla scheda **Visibilità** per un prodotto, fare clic su **Gestisci gruppi**.</span><span class="sxs-lookup"><span data-stu-id="88a52-141">To configure groups from the **Visibility** tab for a product, click **Manage Groups**.</span></span>
> 
> 

<span data-ttu-id="88a52-142">Dopo che un prodotto è stato associato a un gruppo, gli sviluppatori in quel gruppo possono visualizzare il prodotto e sottoscriversi ad esso.</span><span class="sxs-lookup"><span data-stu-id="88a52-142">Once a product is associated with a group, developers in that group can view and subscribe to the product.</span></span>

## <span data-ttu-id="88a52-143"><a name="associate-group-developer"> </a>Associare gruppi a sviluppatori</span><span class="sxs-lookup"><span data-stu-id="88a52-143"><a name="associate-group-developer"> </a>Associate groups with developers</span></span>
<span data-ttu-id="88a52-144">Per associare gruppi a sviluppatori, fare clic su **Utenti** dal menu **Gestione API** a sinistra, quindi selezionare la casella di controllo accanto agli sviluppatori da associare a un gruppo.</span><span class="sxs-lookup"><span data-stu-id="88a52-144">To associate groups with developers, click **Users** from the **API Management** menu on the left, and then check the box beside the developers you wish to associate with a group.</span></span>

![Aggiungere uno sviluppatore a un gruppo][api-management-add-group-to-developer]

<span data-ttu-id="88a52-146">Dopo aver selezionato gli sviluppatori desiderati, fare clic sul gruppo desiderato nel menu a discesa **Aggiungi gruppo** .</span><span class="sxs-lookup"><span data-stu-id="88a52-146">Once the desired developers are checked, click the desired group in the **Add to Group** drop-down.</span></span> <span data-ttu-id="88a52-147">È possibile rimuovere sviluppatori dai gruppi usando l'elenco a discesa **Rimuovi da gruppo** .</span><span class="sxs-lookup"><span data-stu-id="88a52-147">Developers can be removed from groups by using the **Remove from Group** drop-down.</span></span> 

![Sviluppatori][api-management-add-group-to-developer-saved]

<span data-ttu-id="88a52-149">Dopo l'aggiunta dell'associazione tra sviluppatore e gruppo, è possibile visualizzarla nella scheda **Utenti** .</span><span class="sxs-lookup"><span data-stu-id="88a52-149">Once the association is added between the developer and the group, you can view it in the **Users** tab.</span></span>

## <span data-ttu-id="88a52-150"><a name="next-steps"> </a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="88a52-150"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="88a52-151">Dopo che uno sviluppatore è stato associato a un gruppo, potrà visualizzare i prodotti associati a quel gruppo e sottoscriversi ad essi.</span><span class="sxs-lookup"><span data-stu-id="88a52-151">Once a developer is added to a group, they can view and subscribe to the products associated with that group.</span></span> <span data-ttu-id="88a52-152">Per altre informazioni, vedere [Come creare e pubblicare un prodotto in Gestione API di Azure][How create and publish a product in Azure API Management],</span><span class="sxs-lookup"><span data-stu-id="88a52-152">For more information, see [How create and publish a product in Azure API Management][How create and publish a product in Azure API Management],</span></span>
* <span data-ttu-id="88a52-153">Oltre a creare e gestire gruppi nel portale di pubblicazione, è possibile creare e gestire i gruppi utilizzando l'entità API REST di gestione [Gruppo](https://msdn.microsoft.com/library/azure/dn776329.aspx) .</span><span class="sxs-lookup"><span data-stu-id="88a52-153">In addition to creating and managing groups in the publisher portal, you can create and manage your groups using the API Management REST API [Group](https://msdn.microsoft.com/library/azure/dn776329.aspx) entity.</span></span>

[api-management-management-console]: ./media/api-management-howto-create-groups/api-management-management-console.png
[api-management-add-group]: ./media/api-management-howto-create-groups/api-management-add-group.png
[api-management-add-group-window]: ./media/api-management-howto-create-groups/api-management-add-group-window.png
[api-management-new-group]: ./media/api-management-howto-create-groups/api-management-new-group.png
[api-management-add-group-to-product]: ./media/api-management-howto-create-groups/api-management-add-group-to-product.png
[api-management-add-group-to-product-visibility]: ./media/api-management-howto-create-groups/api-management-add-group-to-product-visibility.png
[api-management-add-group-to-developer]: ./media/api-management-howto-create-groups/api-management-add-group-to-developer.png
[api-management-add-group-to-developer-saved]: ./media/api-management-howto-create-groups/api-management-add-group-to-developer-saved.png

[api-management-]: ./media/api-management-howto-create-groups/api-management-.png

[Create a group]: #create-group
[Associate a group with a product]: #associate-group-product
[Associate groups with developers]: #associate-group-developer
[Next steps]: #next-steps

[How create and publish a product in Azure API Management]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[leverage external groups in associated Azure Active Directory tenants]: api-management-howto-aad.md#how-to-add-an-external-azure-active-directory-group
