---
title: gli account sviluppatore aaaManage usano i gruppi in Gestione API di Azure | Documenti Microsoft
description: Informazioni su come sviluppatore toomanage degli account con gruppi di gestione API di Azure
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
ms.openlocfilehash: c46e010e41d9705ae161dcd60d734a76d19c9e93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-use-groups-toomanage-developer-accounts-in-azure-api-management"></a><span data-ttu-id="a2991-103">Come per sviluppatori toomanage gruppi toocreate e utilizzare gli account in Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="a2991-103">How toocreate and use groups toomanage developer accounts in Azure API Management</span></span>
<span data-ttu-id="a2991-104">In Gestione API, i gruppi sono utilizzati toomanage hello visibilità dei prodotti toodevelopers.</span><span class="sxs-lookup"><span data-stu-id="a2991-104">In API Management, groups are used toomanage hello visibility of products toodevelopers.</span></span> <span data-ttu-id="a2991-105">I prodotti sono primo toogroups visibile effettuata e gli sviluppatori di tali gruppi possono quindi visualizzare e sottoscrivere toohello prodotti che sono associati a gruppi di hello.</span><span class="sxs-lookup"><span data-stu-id="a2991-105">Products are first made visible toogroups, and then developers in those groups can view and subscribe toohello products that are associated with hello groups.</span></span> 

<span data-ttu-id="a2991-106">Gestione API ha hello seguenti gruppi di sistema non modificabile.</span><span class="sxs-lookup"><span data-stu-id="a2991-106">API Management has hello following immutable system groups.</span></span>

* <span data-ttu-id="a2991-107">**Amministratori** : gli amministratori delle sottoscrizioni di Azure sono membri di questo gruppo.</span><span class="sxs-lookup"><span data-stu-id="a2991-107">**Administrators** - Azure subscription administrators are members of this group.</span></span> <span data-ttu-id="a2991-108">Gli amministratori di gestire le istanze del servizio Gestione API, la creazione di hello API, operazioni e i prodotti che vengono utilizzati dagli sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="a2991-108">Administrators manage API Management service instances, creating hello APIs, operations, and products that are used by developers.</span></span>
* <span data-ttu-id="a2991-109">**Sviluppatori** : gli utenti autenticati del portale per sviluppatori rientrano in questo gruppo.</span><span class="sxs-lookup"><span data-stu-id="a2991-109">**Developers** - Authenticated developer portal users fall into this group.</span></span> <span data-ttu-id="a2991-110">Gli sviluppatori hanno clienti hello che compilano applicazioni che utilizzano l'API.</span><span class="sxs-lookup"><span data-stu-id="a2991-110">Developers are hello customers that build applications using your APIs.</span></span> <span data-ttu-id="a2991-111">Gli sviluppatori sono concesse portale per sviluppatori di accesso toohello e compilare applicazioni che chiamano le operazioni di hello di un'API.</span><span class="sxs-lookup"><span data-stu-id="a2991-111">Developers are granted access toohello developer portal and build applications that call hello operations of an API.</span></span>
* <span data-ttu-id="a2991-112">**Gli utenti guest** -non autenticati gli utenti del portale per sviluppatori, ad esempio clienti potenziali, visitare il portale per sviluppatori hello di un passaggio di istanza di gestione API in questo gruppo.</span><span class="sxs-lookup"><span data-stu-id="a2991-112">**Guests** - Unauthenticated developer portal users, such as prospective customers visiting hello developer portal of an API Management instance fall into this group.</span></span> <span data-ttu-id="a2991-113">È possibile concedere alcuni accesso di sola lettura, ad esempio hello possibilità tooview API, ma li chiama.</span><span class="sxs-lookup"><span data-stu-id="a2991-113">They can be granted certain read-only access, such as hello ability tooview APIs but not call them.</span></span>

<span data-ttu-id="a2991-114">Nei gruppi di sistema aggiunta toothese, gli amministratori possono creare gruppi personalizzati o [sfruttare gruppi esterni nel tenant di Azure Active Directory associato][leverage external groups in associated Azure Active Directory tenants].</span><span class="sxs-lookup"><span data-stu-id="a2991-114">In addition toothese system groups, administrators can create custom groups or [leverage external groups in associated Azure Active Directory tenants][leverage external groups in associated Azure Active Directory tenants].</span></span> <span data-ttu-id="a2991-115">Personalizzati e i gruppi esterni possono essere utilizzati insieme ai gruppi di sistema in fornendo agli sviluppatori di visibilità e accedere tooAPI prodotti.</span><span class="sxs-lookup"><span data-stu-id="a2991-115">Custom and external groups can be used alongside system groups in giving developers visibility and access tooAPI products.</span></span> <span data-ttu-id="a2991-116">Ad esempio, è possibile creare un gruppo personalizzato per gli sviluppatori associati a uno specifico partner dell'organizzazione e consentono loro l'accesso toohello API da un prodotto che contiene solo le API pertinente.</span><span class="sxs-lookup"><span data-stu-id="a2991-116">For example, you could create one custom group for developers affiliated with a specific partner organization and allow them access toohello APIs from a product containing relevant APIs only.</span></span> <span data-ttu-id="a2991-117">Un utente può essere un membro di più gruppi.</span><span class="sxs-lookup"><span data-stu-id="a2991-117">A user can be a member of more than one group.</span></span>

<span data-ttu-id="a2991-118">Questa guida illustra come gli amministratori di un'istanza di Gestione API possono aggiungere nuovi gruppi e associarli a prodotti e sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="a2991-118">This guide shows how administrators of an API Management instance can add new groups and associate them with products and developers.</span></span>

> [!NOTE]
> <span data-ttu-id="a2991-119">Inoltre toocreating e gestione di gruppi nel portale di pubblicazione hello, è possibile creare e gestire i gruppi tramite l'API REST gestione API hello [gruppo](https://msdn.microsoft.com/library/azure/dn776329.aspx) entità.</span><span class="sxs-lookup"><span data-stu-id="a2991-119">In addition toocreating and managing groups in hello publisher portal, you can create and manage your groups using hello API Management REST API [Group](https://msdn.microsoft.com/library/azure/dn776329.aspx) entity.</span></span>
> 
> 

## <span data-ttu-id="a2991-120"><a name="create-group"></a>Creare un gruppo</span><span class="sxs-lookup"><span data-stu-id="a2991-120"><a name="create-group"> </a>Create a group</span></span>
<span data-ttu-id="a2991-121">Fare clic su un nuovo gruppo, toocreate **portale di pubblicazione** in hello portale di Azure per il servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="a2991-121">toocreate a new group, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="a2991-122">Consente di procedere toohello portale di pubblicazione di gestione API.</span><span class="sxs-lookup"><span data-stu-id="a2991-122">This takes you toohello API Management publisher portal.</span></span>

![Portale di pubblicazione][api-management-management-console]

> <span data-ttu-id="a2991-124">Se non è ancora stato creato un'istanza del servizio Gestione API, vedere [creare un'istanza del servizio Gestione API] [ Create an API Management service instance] in hello [Introduzione a gestione API di Azure] [ Get started with Azure API Management] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="a2991-124">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="a2991-125">Fare clic su **gruppi** da hello **gestione API** menu hello a sinistra e quindi fare clic su **Aggiungi gruppo**.</span><span class="sxs-lookup"><span data-stu-id="a2991-125">Click **Groups** from hello **API Management** menu on hello left, and then click **Add Group**.</span></span>

![Aggiungere un nuovo gruppo][api-management-add-group]

<span data-ttu-id="a2991-127">Immettere un nome univoco per il gruppo di hello e una descrizione facoltativa e fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="a2991-127">Enter a unique name for hello group and an optional description, and click **Save**.</span></span>

![Aggiungere un nuovo gruppo][api-management-add-group-window]

<span data-ttu-id="a2991-129">viene visualizzato il nuovo gruppo di Hello in hello tooedit scheda gruppi di hello **nome** o **descrizione** del gruppo di hello, fare clic sul nome di hello del gruppo di hello nell'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="a2991-129">hello new group is displayed in hello groups tab. tooedit hello **Name** or **Description** of hello group, click hello name of hello group in hello list.</span></span> <span data-ttu-id="a2991-130">gruppo di hello toodelete, fare clic su **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="a2991-130">toodelete hello group, click **Delete**.</span></span>

![Gruppo aggiunto][api-management-new-group]

<span data-ttu-id="a2991-132">Dopo aver creato hello gruppo, può essere associata a prodotti e gli sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="a2991-132">Now that hello group is created, it can be associated with products and developers.</span></span>

## <span data-ttu-id="a2991-133"><a name="associate-group-product"></a>Associare un gruppo a un prodotto</span><span class="sxs-lookup"><span data-stu-id="a2991-133"><a name="associate-group-product"> </a>Associate a group with a product</span></span>
<span data-ttu-id="a2991-134">Fare clic su un gruppo con un prodotto, tooassociate **prodotti** da hello **gestione API** menu hello a sinistra e quindi fare clic su nome hello del prodotto desiderate hello.</span><span class="sxs-lookup"><span data-stu-id="a2991-134">tooassociate a group with a product, click **Products** from hello **API Management** menu on hello left, and then click hello name of hello desired product.</span></span>

![Visibilità dei prodotti][api-management-add-group-to-product]

<span data-ttu-id="a2991-136">Seleziona hello **visibilità** scheda tooadd e rimuovere gruppi e tooview hello corrente per il prodotto hello.</span><span class="sxs-lookup"><span data-stu-id="a2991-136">Select hello **Visibility** tab tooadd and remove groups, and tooview hello current groups for hello product.</span></span> <span data-ttu-id="a2991-137">tooadd o rimuovere i gruppi, selezionare o deselezionare le caselle di controllo di hello per hello desiderato di gruppi e fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="a2991-137">tooadd or remove groups, check or uncheck hello checkboxes for hello desired groups and click **Save**.</span></span>

![Visibilità dei prodotti][api-management-add-group-to-product-visibility]

> [!NOTE]
> <span data-ttu-id="a2991-139">gruppi di Azure Active Directory tooadd, vedere [modalità sviluppatore tooauthorize degli account con Azure Active Directory in Gestione API di Azure](api-management-howto-aad.md).</span><span class="sxs-lookup"><span data-stu-id="a2991-139">tooadd Azure Active Directory groups, see [How tooauthorize developer accounts using Azure Active Directory in Azure API Management](api-management-howto-aad.md).</span></span>
> 
> <span data-ttu-id="a2991-140">gruppi tooconfigure da hello **visibilità** per un prodotto, fare clic **Gestisci gruppi**.</span><span class="sxs-lookup"><span data-stu-id="a2991-140">tooconfigure groups from hello **Visibility** tab for a product, click **Manage Groups**.</span></span>
> 
> 

<span data-ttu-id="a2991-141">Una volta associato a un gruppo di un prodotto, gli sviluppatori in tale gruppo possono visualizzare e sottoscrivere toohello prodotto.</span><span class="sxs-lookup"><span data-stu-id="a2991-141">Once a product is associated with a group, developers in that group can view and subscribe toohello product.</span></span>

## <span data-ttu-id="a2991-142"><a name="associate-group-developer"> </a>Associare gruppi a sviluppatori</span><span class="sxs-lookup"><span data-stu-id="a2991-142"><a name="associate-group-developer"> </a>Associate groups with developers</span></span>
<span data-ttu-id="a2991-143">gruppi tooassociate con gli sviluppatori, fare clic su **utenti** da hello **gestione API** menu hello a sinistra, quindi casella hello di controllo accanto agli sviluppatori di hello desiderato tooassociate con un gruppo.</span><span class="sxs-lookup"><span data-stu-id="a2991-143">tooassociate groups with developers, click **Users** from hello **API Management** menu on hello left, and then check hello box beside hello developers you wish tooassociate with a group.</span></span>

![Aggiungere toogroup developer][api-management-add-group-to-developer]

<span data-ttu-id="a2991-145">Una volta hello lo si desidera che gli sviluppatori vengono controllati, fare clic su gruppo hello nella hello **aggiungere tooGroup** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="a2991-145">Once hello desired developers are checked, click hello desired group in hello **Add tooGroup** drop-down.</span></span> <span data-ttu-id="a2991-146">Gli sviluppatori possono essere rimossi dai gruppi tramite hello **rimuovere dal gruppo** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="a2991-146">Developers can be removed from groups by using hello **Remove from Group** drop-down.</span></span> 

![Sviluppatori][api-management-add-group-to-developer-saved]

<span data-ttu-id="a2991-148">Una volta tra developer hello e gruppo di hello viene aggiunta l'associazione di hello, è possibile visualizzarlo in hello **utenti** scheda.</span><span class="sxs-lookup"><span data-stu-id="a2991-148">Once hello association is added between hello developer and hello group, you can view it in hello **Users** tab.</span></span>

## <span data-ttu-id="a2991-149"><a name="next-steps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a2991-149"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="a2991-150">Dopo aver aggiunto il gruppo tooa uno sviluppatore, possono visualizzare e sottoscrivere toohello prodotti associati al gruppo.</span><span class="sxs-lookup"><span data-stu-id="a2991-150">Once a developer is added tooa group, they can view and subscribe toohello products associated with that group.</span></span> <span data-ttu-id="a2991-151">Per altre informazioni, vedere [Come creare e pubblicare un prodotto in Gestione API di Azure][How create and publish a product in Azure API Management],</span><span class="sxs-lookup"><span data-stu-id="a2991-151">For more information, see [How create and publish a product in Azure API Management][How create and publish a product in Azure API Management],</span></span>
* <span data-ttu-id="a2991-152">Inoltre toocreating e gestione di gruppi nel portale di pubblicazione hello, è possibile creare e gestire i gruppi tramite l'API REST gestione API hello [gruppo](https://msdn.microsoft.com/library/azure/dn776329.aspx) entità.</span><span class="sxs-lookup"><span data-stu-id="a2991-152">In addition toocreating and managing groups in hello publisher portal, you can create and manage your groups using hello API Management REST API [Group](https://msdn.microsoft.com/library/azure/dn776329.aspx) entity.</span></span>

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
