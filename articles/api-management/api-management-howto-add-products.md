---
title: aaaHow toocreate e pubblicazione di un prodotto in Gestione API di Azure
description: Informazioni su come toocreate e pubblicare prodotti in Gestione API di Azure.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 31de55cb-9384-490b-a2f2-6dfcf83da764
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: f0a37f08b4e29ca68be9caec4c7604e3b4b6aaa6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-publish-a-product-in-azure-api-management"></a><span data-ttu-id="3ce47-103">Come toocreate e pubblicazione di un prodotto in Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="3ce47-103">How toocreate and publish a product in Azure API Management</span></span>
<span data-ttu-id="3ce47-104">In Gestione API di Azure, un prodotto contiene una o più API, nonché di utilizzo della quota e hello le condizioni di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="3ce47-104">In Azure API Management, a product contains one or more APIs as well as a usage quota and hello terms of use.</span></span> <span data-ttu-id="3ce47-105">Dopo aver pubblicato un prodotto, gli sviluppatori possono sottoscrivere toohello prodotto e iniziare l'API del prodotto di toouse hello.</span><span class="sxs-lookup"><span data-stu-id="3ce47-105">Once a product is published, developers can subscribe toohello product and begin toouse hello product's APIs.</span></span> <span data-ttu-id="3ce47-106">argomento Hello fornisce una Guida toocreating un prodotto, aggiunta di un'API e pubblicarlo per gli sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="3ce47-106">hello topic provides a guide toocreating a product, adding an API, and publishing it for developers.</span></span>

## <span data-ttu-id="3ce47-107"><a name="create-product"> </a>Creare un prodotto</span><span class="sxs-lookup"><span data-stu-id="3ce47-107"><a name="create-product"> </a>Create a product</span></span>
<span data-ttu-id="3ce47-108">Le operazioni vengono aggiunte e configurate tooan API nel portale di server di pubblicazione hello.</span><span class="sxs-lookup"><span data-stu-id="3ce47-108">Operations are added and configured tooan API in hello publisher portal.</span></span> <span data-ttu-id="3ce47-109">Fare clic su portale, server di pubblicazione di hello tooaccess **portale di pubblicazione** in hello portale di Azure per il servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="3ce47-109">tooaccess hello publisher portal, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span>

![Portale di pubblicazione][api-management-management-console]

> <span data-ttu-id="3ce47-111">Se non è ancora stato creato un'istanza del servizio Gestione API, vedere [creare un'istanza del servizio Gestione API] [ Create an API Management service instance] in hello [Introduzione a gestione API di Azure] [ Get started with Azure API Management] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="3ce47-111">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="3ce47-112">Fare clic su **prodotti** menu hello in hello toodisplay sinistro hello **prodotti** pagina e fare clic su **Aggiungi prodotto**.</span><span class="sxs-lookup"><span data-stu-id="3ce47-112">Click on **Products** in hello menu on hello left toodisplay hello **Products** page, and click **Add Product**.</span></span>

![Prodotti][api-management-products]

![Nuovo prodotto][api-management-add-new-product]

<span data-ttu-id="3ce47-115">Immettere un nome descrittivo per il prodotto hello in hello **nome** campo e una descrizione del prodotto hello hello **descrizione** campo.</span><span class="sxs-lookup"><span data-stu-id="3ce47-115">Enter a descriptive name for hello product in hello **Name** field and a description of hello product in hello **Description** field.</span></span>

<span data-ttu-id="3ce47-116">Lo stato dei prodotti in Gestione API può essere **Aperto** o **Protetto**.</span><span class="sxs-lookup"><span data-stu-id="3ce47-116">Products in API Management can be **Open** or **Protected**.</span></span> <span data-ttu-id="3ce47-117">Prodotti protetti devono essere toobefore sottoscritti possono essere utilizzati, aperti prodotti possono essere utilizzati senza alcuna sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="3ce47-117">Protected products must be subscribed toobefore they can be used, while open products can be used without a subscription.</span></span> <span data-ttu-id="3ce47-118">Controllare **richiedono sottoscrizione** toocreate protetto prodotto che richiede una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="3ce47-118">Check **Require subscription** toocreate a protected product that requires a subscription.</span></span> <span data-ttu-id="3ce47-119">Questo è l'impostazione predefinita hello.</span><span class="sxs-lookup"><span data-stu-id="3ce47-119">This is hello default setting.</span></span>

<span data-ttu-id="3ce47-120">Controllare **richiedono l'approvazione della sottoscrizione** se si desidera che un amministratore tooreview e accettare o rifiutare la sottoscrizione tenterà toothis prodotto.</span><span class="sxs-lookup"><span data-stu-id="3ce47-120">Check **Require subscription approval** if you want an administrator tooreview and accept or reject subscription attempts toothis product.</span></span> <span data-ttu-id="3ce47-121">Se hello casella è deselezionata, i tentativi di sottoscrizione sarà approvata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="3ce47-121">If hello box is unchecked, subscription attempts will be auto-approved.</span></span> <span data-ttu-id="3ce47-122">Per ulteriori informazioni sulle sottoscrizioni, vedere [Visualizza prodotti di sottoscrittori tooa][View subscribers tooa product].</span><span class="sxs-lookup"><span data-stu-id="3ce47-122">For more information on subscriptions, see [View subscribers tooa product][View subscribers tooa product].</span></span>

<span data-ttu-id="3ce47-123">tooallow developer account toosubscribe prodotto toohello più volte, controllare hello **può supportare più sottoscrizioni** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="3ce47-123">tooallow developer accounts toosubscribe multiple times toohello product, check hello **Allow multiple subscriptions** check box.</span></span> <span data-ttu-id="3ce47-124">Se questa casella è deselezionata, ogni account sviluppatore possono sottoscrivere solo un prodotto toohello sola volta.</span><span class="sxs-lookup"><span data-stu-id="3ce47-124">If this box is not checked, each developer account can subscribe only a single time toohello product.</span></span>

![Più sottoscrizioni senza limitazioni][api-management-unlimited-multiple-subscriptions]

<span data-ttu-id="3ce47-126">numero di hello toolimit di più sottoscrizioni simultanee, controllare hello **Limita numero di sottoscrizioni simultanee** casella di controllo e immettere il limite di sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="3ce47-126">toolimit hello count of multiple simultaneous subscriptions, check hello **Limit number of simultaneous subscriptions to** check box and enter hello subscription limit.</span></span> <span data-ttu-id="3ce47-127">Nell'esempio seguente di hello, le sottoscrizioni simultanee sono toofour limitato per l'account sviluppatore.</span><span class="sxs-lookup"><span data-stu-id="3ce47-127">In hello following example, simultaneous subscriptions are limited toofour per developer account.</span></span>

![Quattro sottoscrizioni][api-management-four-multiple-subscriptions]

<span data-ttu-id="3ce47-129">Dopo aver configurate tutte le nuove opzioni di prodotto, fare clic su **salvare** nuovo prodotto di toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="3ce47-129">Once all new product options are configured, click **Save** toocreate hello new product.</span></span>

![Prodotti][api-management-products-page]

> <span data-ttu-id="3ce47-131">Per impostazione predefinita sono non pubblicati nuovi prodotti e sono visibile toohello solo **amministratori** gruppo.</span><span class="sxs-lookup"><span data-stu-id="3ce47-131">By default new products are unpublished, and are visible only toohello  **Administrators** group.</span></span>
> 
> 

<span data-ttu-id="3ce47-132">tooconfigure un prodotto, fare clic sul nome del prodotto hello in hello **prodotti** scheda.</span><span class="sxs-lookup"><span data-stu-id="3ce47-132">tooconfigure a product, click on hello product name in hello **Products** tab.</span></span>

## <span data-ttu-id="3ce47-133"><a name="add-apis"></a>Prodotto tooa aggiungere API</span><span class="sxs-lookup"><span data-stu-id="3ce47-133"><a name="add-apis"> </a>Add APIs tooa product</span></span>
<span data-ttu-id="3ce47-134">Hello **prodotti** pagina contiene quattro collegamenti per la configurazione: **riepilogo**, **impostazioni**, **visibilità**, e  **I sottoscrittori**.</span><span class="sxs-lookup"><span data-stu-id="3ce47-134">hello **Products** page contains four links for configuration: **Summary**, **Settings**, **Visibility**, and **Subscribers**.</span></span> <span data-ttu-id="3ce47-135">Hello **riepilogo** scheda è dove è possibile aggiungere le API e pubblicare o annullare la pubblicazione di un prodotto.</span><span class="sxs-lookup"><span data-stu-id="3ce47-135">hello **Summary** tab is where you can add APIs and publish or unpublish a product.</span></span>

![Riepilogo][api-management-new-product-summary]

<span data-ttu-id="3ce47-137">Prima di pubblicare il prodotto è necessario tooadd una o più API.</span><span class="sxs-lookup"><span data-stu-id="3ce47-137">Before publishing your product you need tooadd one or more APIs.</span></span> <span data-ttu-id="3ce47-138">toodo, fare clic su **tooproduct aggiungere API**.</span><span class="sxs-lookup"><span data-stu-id="3ce47-138">toodo this, click **Add API tooproduct**.</span></span>

![Aggiunta di API][api-management-add-apis-to-product]

<span data-ttu-id="3ce47-140">Lo si desidera seleziona hello API e fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="3ce47-140">Select hello desired APIs and click **Save**.</span></span>

## <span data-ttu-id="3ce47-141"><a name="add-description"></a>Prodotto tooa di aggiungere informazioni descrittive</span><span class="sxs-lookup"><span data-stu-id="3ce47-141"><a name="add-description"> </a>Add descriptive information tooa product</span></span>
<span data-ttu-id="3ce47-142">Hello **impostazioni** scheda permette tooprovide informazioni dettagliate sul prodotto hello, ad esempio il suo scopo hello fornisce accesso all'API e altre informazioni utili.</span><span class="sxs-lookup"><span data-stu-id="3ce47-142">hello **Settings** tab allows you tooprovide detailed information about hello product such as its purpose, hello APIs it provides access to, and other useful information.</span></span> <span data-ttu-id="3ce47-143">contenuto Hello è destinato agli sviluppatori di hello che chiameremo hello API e possono essere scritti in testo normale o markup HTML.</span><span class="sxs-lookup"><span data-stu-id="3ce47-143">hello content is targeted at hello developers that will be calling hello API and can be written in plain text or HTML markup.</span></span>

![Impostazioni prodotto][api-management-product-settings]

<span data-ttu-id="3ce47-145">Controllare **richiedono sottoscrizione** toocreate un prodotto protetto che richiede un toobe di sottoscrizione utilizzato o non crittografato hello toocreate casella di controllo un prodotto open che può essere chiamato senza una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="3ce47-145">Check **Require subscription** toocreate a protected product that requires a subscription toobe used, or clear hello checkbox toocreate an open product that can be called without a subscription.</span></span>

<span data-ttu-id="3ce47-146">Selezionare **richiedono l'approvazione della sottoscrizione** se si desidera toomanually approvare tutte le richieste di sottoscrizione al prodotto.</span><span class="sxs-lookup"><span data-stu-id="3ce47-146">Select **Require subscription approval** if you want toomanually approve all product subscription requests.</span></span> <span data-ttu-id="3ce47-147">Per impostazione predefinita, tutte le sottoscrizioni al prodotto vengono concesse automaticamente.</span><span class="sxs-lookup"><span data-stu-id="3ce47-147">By default all product subscriptions are granted automatically.</span></span>

<span data-ttu-id="3ce47-148">tooallow developer account toosubscribe prodotto toohello più volte, controllare hello **può supportare più sottoscrizioni** casella di controllo e, facoltativamente, specificare un limite.</span><span class="sxs-lookup"><span data-stu-id="3ce47-148">tooallow developer accounts toosubscribe multiple times toohello product, check hello **Allow multiple subscriptions** check box and optionally specify a limit.</span></span> <span data-ttu-id="3ce47-149">Se questa casella è deselezionata, ogni account sviluppatore possono sottoscrivere solo un prodotto toohello sola volta.</span><span class="sxs-lookup"><span data-stu-id="3ce47-149">If this box is not checked, each developer account can subscribe only a single time toohello product.</span></span>

<span data-ttu-id="3ce47-150">Se lo si desidera compilare hello **condizioni di utilizzo** campo che descrive le condizioni di hello di utilizzo per il prodotto hello che i sottoscrittori devono accettare nel prodotto di hello toouse dell'ordine.</span><span class="sxs-lookup"><span data-stu-id="3ce47-150">Optionally fill in hello **Terms of use** field describing hello terms of use for hello product which subscribers must accept in order toouse hello product.</span></span>

## <span data-ttu-id="3ce47-151"><a name="publish-product"></a>Pubblicare un prodotto</span><span class="sxs-lookup"><span data-stu-id="3ce47-151"><a name="publish-product"> </a>Publish a product</span></span>
<span data-ttu-id="3ce47-152">Prima di poter chiamare le API di hello in un prodotto, deve essere pubblicata prodotto hello.</span><span class="sxs-lookup"><span data-stu-id="3ce47-152">Before hello APIs in a product can be called, hello product must be published.</span></span> <span data-ttu-id="3ce47-153">In hello **riepilogo** per prodotto hello scheda, fare clic su **pubblica**, quindi fare clic su **Sì, pubblicarlo** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="3ce47-153">On hello **Summary** tab for hello product, click **Publish**, and then click **Yes, publish it** tooconfirm.</span></span> <span data-ttu-id="3ce47-154">toomake private prodotto pubblicati in precedenza, fare clic su **Annulla pubblicazione**.</span><span class="sxs-lookup"><span data-stu-id="3ce47-154">toomake a previously published product private, click **Unpublish**.</span></span>

![Pubblicazione prodotto][api-management-publish-product]

## <span data-ttu-id="3ce47-156"><a name="make-visible"></a>Rendere un toodevelopers visibile prodotto</span><span class="sxs-lookup"><span data-stu-id="3ce47-156"><a name="make-visible"> </a>Make a product visible toodevelopers</span></span>
<span data-ttu-id="3ce47-157">Hello **visibilità** scheda permette toochoose i ruoli che sono in grado di toosee hello prodotto nel portale per sviluppatori hello e sottoscrivono toohello prodotto.</span><span class="sxs-lookup"><span data-stu-id="3ce47-157">hello **Visibility** tab allows you toochoose which roles are able toosee hello product on hello developer portal and subscribe toohello product.</span></span>

![Visibilità prodotto][api-management-product-visiblity]

<span data-ttu-id="3ce47-159">tooenable o disattivare la visibilità di un prodotto per gli sviluppatori di hello in un gruppo di selezionare o deselezionare la casella di controllo hello accanto gruppo hello e quindi fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="3ce47-159">tooenable or disable visibility of a product for hello developers in a group, check or uncheck hello check box beside hello group and then click **Save**.</span></span>

> <span data-ttu-id="3ce47-160">Per ulteriori informazioni, vedere [come account di sviluppatore di toomanage gruppi toocreate e l'utilizzo in Gestione API di Azure][How toocreate and use groups toomanage developer accounts in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="3ce47-160">For more information, see [How toocreate and use groups toomanage developer accounts in Azure API Management][How toocreate and use groups toomanage developer accounts in Azure API Management].</span></span>
> 
> 

## <span data-ttu-id="3ce47-161"><a name="view-subscribers"></a>Prodotto tooa i sottoscrittori di visualizzazione</span><span class="sxs-lookup"><span data-stu-id="3ce47-161"><a name="view-subscribers"> </a>View subscribers tooa product</span></span>
<span data-ttu-id="3ce47-162">Hello **sottoscrittori** scheda vengono elencati gli sviluppatori di hello che hanno sottoscritto il prodotto toohello.</span><span class="sxs-lookup"><span data-stu-id="3ce47-162">hello **Subscribers** tab lists hello developers who have subscribed toohello product.</span></span> <span data-ttu-id="3ce47-163">Hello dettagli e le impostazioni per ogni sviluppatore possono essere visualizzate facendo clic sul nome dello sviluppatore hello.</span><span class="sxs-lookup"><span data-stu-id="3ce47-163">hello details and settings for each developer can be viewed by clicking on hello developer's name.</span></span> <span data-ttu-id="3ce47-164">In questo esempio non gli sviluppatori hanno ancora sottoscritto toohello prodotto.</span><span class="sxs-lookup"><span data-stu-id="3ce47-164">In this example no developers have yet subscribed toohello product.</span></span>

![Sviluppatori][api-management-developer-list]

## <span data-ttu-id="3ce47-166"><a name="next-steps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3ce47-166"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="3ce47-167">Una volta hello desiderato vengono aggiunte le API e prodotto hello pubblicata, gli sviluppatori possono sottoscrivere toohello prodotto e iniziare hello toocall API.</span><span class="sxs-lookup"><span data-stu-id="3ce47-167">Once hello desired APIs are added and hello product published, developers can subscribe toohello product and begin toocall hello APIs.</span></span> <span data-ttu-id="3ce47-168">Per una dimostrazione di questi elementi e della configurazione avanzata del prodotto, vedere l'esercitazione [Come creare e configurare le impostazioni avanzate del prodotto in Gestione API di Azure][How create and configure advanced product settings in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="3ce47-168">For a tutorial that demonstrates these items as well as advanced product configuration see [How create and configure advanced product settings in Azure API Management][How create and configure advanced product settings in Azure API Management].</span></span>

<span data-ttu-id="3ce47-169">Per ulteriori informazioni sull'utilizzo dei prodotti, vedere hello video seguenti.</span><span class="sxs-lookup"><span data-stu-id="3ce47-169">For more information about working with products, see hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Using-Products/player]
> 
> 

[Create a product]: #create-product
[Add APIs tooa product]: #add-apis
[Add descriptive information tooa product]: #add-description
[Publish a product]: #publish-product
[Make a product visible toodevelopers]: #make-visible
[View subscribers tooa product]: #view-subscribers
[Next steps]: #next-steps

[api-management-management-console]: ./media/api-management-howto-add-products/api-management-management-console.png
[api-management-add-product]: ./media/api-management-howto-add-products/api-management-add-product.png
[api-management-add-new-product]: ./media/api-management-howto-add-products/api-management-add-new-product.png
[api-management-unlimited-multiple-subscriptions]: ./media/api-management-howto-add-products/api-management-unlimited-multiple-subscriptions.png
[api-management-four-multiple-subscriptions]: ./media/api-management-howto-add-products/api-management-four-multiple-subscriptions.png
[api-management-products-page]: ./media/api-management-howto-add-products/api-management-products-page.png
[api-management-new-product-summary]: ./media/api-management-howto-add-products/api-management-new-product-summary.png
[api-management-add-apis-to-product]: ./media/api-management-howto-add-products/api-management-add-apis-to-product.png
[api-management-product-settings]: ./media/api-management-howto-add-products/api-management-product-settings.png
[api-management-publish-product]: ./media/api-management-howto-add-products/api-management-publish-product.png
[api-management-product-visiblity]: ./media/api-management-howto-add-products/api-management-product-visibility.png
[api-management-developer-list]: ./media/api-management-howto-add-products/api-management-developer-list.png



[api-management-products]: ./media/api-management-howto-add-products/api-management-products.png
[api-management-]: ./media/api-management-howto-add-products/
[api-management-]: ./media/api-management-howto-add-products/


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps
[How toocreate and use groups toomanage developer accounts in Azure API Management]: api-management-howto-create-groups.md
[How create and configure advanced product settings in Azure API Management]: api-management-howto-product-with-rules.md 
