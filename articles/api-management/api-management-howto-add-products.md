---
title: Come creare e pubblicare un prodotto in Gestione API di Azure
description: Informazioni su come creare e pubblicare prodotti in Gestione API di Azure.
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
ms.openlocfilehash: 73bf4451ba1b71807e22440beecc73a7e8045c5e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-and-publish-a-product-in-azure-api-management"></a><span data-ttu-id="8c1db-103">Come creare e pubblicare un prodotto in Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="8c1db-103">How to create and publish a product in Azure API Management</span></span>
<span data-ttu-id="8c1db-104">In Gestione API di Azure un prodotto contiene una o più API, oltre a una quota di utilizzo e alle condizioni per l'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="8c1db-104">In Azure API Management, a product contains one or more APIs as well as a usage quota and the terms of use.</span></span> <span data-ttu-id="8c1db-105">Dopo la pubblicazione di un prodotto, gli sviluppatori possono eseguire la sottoscrizione al prodotto e iniziare a usare le API del prodotto.</span><span class="sxs-lookup"><span data-stu-id="8c1db-105">Once a product is published, developers can subscribe to the product and begin to use the product's APIs.</span></span> <span data-ttu-id="8c1db-106">L'argomento include una guida per la creazione di un prodotto, l'aggiunta di un'API e la pubblicazione per gli sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="8c1db-106">The topic provides a guide to creating a product, adding an API, and publishing it for developers.</span></span>

## <span data-ttu-id="8c1db-107"><a name="create-product"> </a>Creare un prodotto</span><span class="sxs-lookup"><span data-stu-id="8c1db-107"><a name="create-product"> </a>Create a product</span></span>
<span data-ttu-id="8c1db-108">Le operazioni vengono aggiunte e configurate in un'API nel portale di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="8c1db-108">Operations are added and configured to an API in the publisher portal.</span></span> <span data-ttu-id="8c1db-109">Per accedere al portale di pubblicazione, fare clic su **Portale di pubblicazione** nel portale di Azure per il servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="8c1db-109">To access the publisher portal, click **Publisher portal** in the Azure Portal for your API Management service.</span></span>

![Portale di pubblicazione][api-management-management-console]

> <span data-ttu-id="8c1db-111">Se non è stata creata un'istanza del servizio Gestione API, vedere [Creare un'istanza di Gestione API][Create an API Management service instance] nell'esercitazione [Introduzione a Gestione API di Azure][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="8c1db-111">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="8c1db-112">Fare clic su **Prodotti** nel menu a sinistra per visualizzare la pagina **Prodotti** e fare clic su **Aggiungi prodotto**.</span><span class="sxs-lookup"><span data-stu-id="8c1db-112">Click on **Products** in the menu on the left to display the **Products** page, and click **Add Product**.</span></span>

![Prodotti][api-management-products]

![Nuovo prodotto][api-management-add-new-product]

<span data-ttu-id="8c1db-115">Immettere un nome descrittivo per il prodotto nel campo **Nome** e una descrizione del prodotto nel campo **Descrizione**.</span><span class="sxs-lookup"><span data-stu-id="8c1db-115">Enter a descriptive name for the product in the **Name** field and a description of the product in the **Description** field.</span></span>

<span data-ttu-id="8c1db-116">Lo stato dei prodotti in Gestione API può essere **Aperto** o **Protetto**.</span><span class="sxs-lookup"><span data-stu-id="8c1db-116">Products in API Management can be **Open** or **Protected**.</span></span> <span data-ttu-id="8c1db-117">Per usare i prodotti protetti, è prima di tutto necessaria una sottoscrizione, mentre i prodotti aperti possono essere usati senza sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="8c1db-117">Protected products must be subscribed to before they can be used, while open products can be used without a subscription.</span></span> <span data-ttu-id="8c1db-118">Per creare un prodotto protetto che richiede una sottoscrizione, selezionare **Richiedi approvazione della sottoscrizione** .</span><span class="sxs-lookup"><span data-stu-id="8c1db-118">Check **Require subscription** to create a protected product that requires a subscription.</span></span> <span data-ttu-id="8c1db-119">Questa è l'impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="8c1db-119">This is the default setting.</span></span>

<span data-ttu-id="8c1db-120">Selezionare **Richiedi approvazione della sottoscrizione** se si preferisce che i tentativi di sottoscrizione al prodotto vengano esaminati e quindi accettati o rifiutati da un amministratore.</span><span class="sxs-lookup"><span data-stu-id="8c1db-120">Check **Require subscription approval** if you want an administrator to review and accept or reject subscription attempts to this product.</span></span> <span data-ttu-id="8c1db-121">Se la casella è deselezionata, i tentativi di sottoscrizione verranno approvati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8c1db-121">If the box is unchecked, subscription attempts will be auto-approved.</span></span> <span data-ttu-id="8c1db-122">Per altre informazioni sulle sottoscrizioni, vedere [Visualizzare i sottoscrittori di un prodotto][View subscribers to a product].</span><span class="sxs-lookup"><span data-stu-id="8c1db-122">For more information on subscriptions, see [View subscribers to a product][View subscribers to a product].</span></span>

<span data-ttu-id="8c1db-123">Per consentire agli account per sviluppatore di sottoscrivere più volte il prodotto, selezionare la casella di controllo **Consenti più sottoscrizioni** .</span><span class="sxs-lookup"><span data-stu-id="8c1db-123">To allow developer accounts to subscribe multiple times to the product, check the **Allow multiple subscriptions** check box.</span></span> <span data-ttu-id="8c1db-124">Se questa casella non è selezionata, ogni account per sviluppatore può sottoscrivere il prodotto una sola volta.</span><span class="sxs-lookup"><span data-stu-id="8c1db-124">If this box is not checked, each developer account can subscribe only a single time to the product.</span></span>

![Più sottoscrizioni senza limitazioni][api-management-unlimited-multiple-subscriptions]

<span data-ttu-id="8c1db-126">Per limitare il numero di più sottoscrizioni simultanee, selezionare la casella di controllo **Limita numero di sottoscrizioni simultanee a** e immettere il limite per le sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="8c1db-126">To limit the count of multiple simultaneous subscriptions, check the **Limit number of simultaneous subscriptions to** check box and enter the subscription limit.</span></span> <span data-ttu-id="8c1db-127">Nell'esempio seguente le sottoscrizioni simultanee sono limitate a quattro per ogni account per sviluppatore.</span><span class="sxs-lookup"><span data-stu-id="8c1db-127">In the following example, simultaneous subscriptions are limited to four per developer account.</span></span>

![Quattro sottoscrizioni][api-management-four-multiple-subscriptions]

<span data-ttu-id="8c1db-129">Dopo aver configurato tutte le opzioni del nuovo prodotto, fare clic su **Salva** per creare il nuovo prodotto.</span><span class="sxs-lookup"><span data-stu-id="8c1db-129">Once all new product options are configured, click **Save** to create the new product.</span></span>

![Prodotti][api-management-products-page]

> <span data-ttu-id="8c1db-131">Per impostazione predefinita, i nuovi prodotti non sono pubblicati e sono visibili solo agli utenti nel gruppo **Amministratori**.</span><span class="sxs-lookup"><span data-stu-id="8c1db-131">By default new products are unpublished, and are visible only to the  **Administrators** group.</span></span>
> 
> 

<span data-ttu-id="8c1db-132">Per configurare un prodotto, fare clic sul nome del prodotto nella scheda **Prodotti** .</span><span class="sxs-lookup"><span data-stu-id="8c1db-132">To configure a product, click on the product name in the **Products** tab.</span></span>

## <span data-ttu-id="8c1db-133"><a name="add-apis"> </a>Aggiungere API a un prodotto</span><span class="sxs-lookup"><span data-stu-id="8c1db-133"><a name="add-apis"> </a>Add APIs to a product</span></span>
<span data-ttu-id="8c1db-134">La pagina **Prodotti** contiene quattro collegamenti per la configurazione: **Riepilogo**, **Impostazioni**, **Visibilità** e **Sottoscrittori**.</span><span class="sxs-lookup"><span data-stu-id="8c1db-134">The **Products** page contains four links for configuration: **Summary**, **Settings**, **Visibility**, and **Subscribers**.</span></span> <span data-ttu-id="8c1db-135">La scheda **Riepilogo** consente di aggiungere le API e di pubblicare o annullare la pubblicazione di un prodotto.</span><span class="sxs-lookup"><span data-stu-id="8c1db-135">The **Summary** tab is where you can add APIs and publish or unpublish a product.</span></span>

![Riepilogo][api-management-new-product-summary]

<span data-ttu-id="8c1db-137">Prima di pubblicare il prodotto, è necessario aggiungere una o più API.</span><span class="sxs-lookup"><span data-stu-id="8c1db-137">Before publishing your product you need to add one or more APIs.</span></span> <span data-ttu-id="8c1db-138">A tale scopo, fare clic su **Aggiungi API al prodotto**.</span><span class="sxs-lookup"><span data-stu-id="8c1db-138">To do this, click **Add API to product**.</span></span>

![Aggiunta di API][api-management-add-apis-to-product]

<span data-ttu-id="8c1db-140">Selezionare le API desiderate e fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="8c1db-140">Select the desired APIs and click **Save**.</span></span>

## <span data-ttu-id="8c1db-141"><a name="add-description"> </a>Aggiungere informazioni descrittive a un prodotto</span><span class="sxs-lookup"><span data-stu-id="8c1db-141"><a name="add-description"> </a>Add descriptive information to a product</span></span>
<span data-ttu-id="8c1db-142">La scheda **Impostazioni** consente di specificare informazioni dettagliate sul prodotto, ad esempio lo scopo, le API a cui fornisce l'accesso e altre informazioni utili.</span><span class="sxs-lookup"><span data-stu-id="8c1db-142">The **Settings** tab allows you to provide detailed information about the product such as its purpose, the APIs it provides access to, and other useful information.</span></span> <span data-ttu-id="8c1db-143">Il contenuto è indirizzato agli sviluppatori che chiameranno l'API e può essere scritto come testo normale o commenti HTML.</span><span class="sxs-lookup"><span data-stu-id="8c1db-143">The content is targeted at the developers that will be calling the API and can be written in plain text or HTML markup.</span></span>

![Impostazioni prodotto][api-management-product-settings]

<span data-ttu-id="8c1db-145">Selezionare **Richiedi sottoscrizione** per creare un prodotto protetto che richiede l'uso di una sottoscrizione oppure deselezionarla per creare un prodotto aperto che può essere chiamato senza sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="8c1db-145">Check **Require subscription** to create a protected product that requires a subscription to be used, or clear the checkbox to create an open product that can be called without a subscription.</span></span>

<span data-ttu-id="8c1db-146">Selezionare **Richiedi approvazione della sottoscrizione** se si preferisce approvare manualmente tutte le richieste di sottoscrizione al prodotto.</span><span class="sxs-lookup"><span data-stu-id="8c1db-146">Select **Require subscription approval** if you want to manually approve all product subscription requests.</span></span> <span data-ttu-id="8c1db-147">Per impostazione predefinita, tutte le sottoscrizioni al prodotto vengono concesse automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8c1db-147">By default all product subscriptions are granted automatically.</span></span>

<span data-ttu-id="8c1db-148">Per consentire agli account per sviluppatore di sottoscrivere più volte il prodotto, selezionare la casella di controllo **Consenti più sottoscrizioni** e, se necessario, specificare un limite.</span><span class="sxs-lookup"><span data-stu-id="8c1db-148">To allow developer accounts to subscribe multiple times to the product, check the **Allow multiple subscriptions** check box and optionally specify a limit.</span></span> <span data-ttu-id="8c1db-149">Se questa casella non è selezionata, ogni account per sviluppatore può sottoscrivere il prodotto una sola volta.</span><span class="sxs-lookup"><span data-stu-id="8c1db-149">If this box is not checked, each developer account can subscribe only a single time to the product.</span></span>

<span data-ttu-id="8c1db-150">Immettere eventualmente nel campo **Condizioni per l'utilizzo** la descrizione delle condizioni per l'utilizzo del prodotto che i sottoscrittori devono accettare per usare il prodotto.</span><span class="sxs-lookup"><span data-stu-id="8c1db-150">Optionally fill in the **Terms of use** field describing the terms of use for the product which subscribers must accept in order to use the product.</span></span>

## <span data-ttu-id="8c1db-151"><a name="publish-product"> </a>Pubblicare un prodotto</span><span class="sxs-lookup"><span data-stu-id="8c1db-151"><a name="publish-product"> </a>Publish a product</span></span>
<span data-ttu-id="8c1db-152">Per poter chiamare le API in un prodotto, il prodotto deve essere pubblicato.</span><span class="sxs-lookup"><span data-stu-id="8c1db-152">Before the APIs in a product can be called, the product must be published.</span></span> <span data-ttu-id="8c1db-153">Nella scheda **Riepilogo** del prodotto fare clic su **Pubblica**, quindi su **Sì, pubblica** per confermare.</span><span class="sxs-lookup"><span data-stu-id="8c1db-153">On the **Summary** tab for the product, click **Publish**, and then click **Yes, publish it** to confirm.</span></span> <span data-ttu-id="8c1db-154">Per impostare come privato un prodotto pubblicato in precedenza, fare clic **Annulla pubblicazione**.</span><span class="sxs-lookup"><span data-stu-id="8c1db-154">To make a previously published product private, click **Unpublish**.</span></span>

![Pubblicazione prodotto][api-management-publish-product]

## <span data-ttu-id="8c1db-156"><a name="make-visible"> </a>Rendere un prodotto visibile per gli sviluppatori</span><span class="sxs-lookup"><span data-stu-id="8c1db-156"><a name="make-visible"> </a>Make a product visible to developers</span></span>
<span data-ttu-id="8c1db-157">La scheda **Visibilità** consente di scegliere i ruoli che possono visualizzare il prodotto nel portale per sviluppatori e sottoscrivere il prodotto.</span><span class="sxs-lookup"><span data-stu-id="8c1db-157">The **Visibility** tab allows you to choose which roles are able to see the product on the developer portal and subscribe to the product.</span></span>

![Visibilità prodotto][api-management-product-visiblity]

<span data-ttu-id="8c1db-159">Per abilitare o disabilitare la visibilità di un prodotto per gli sviluppatori di un gruppo, selezionare o deselezionare la casella di controllo accanto al gruppo e quindi fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="8c1db-159">To enable or disable visibility of a product for the developers in a group, check or uncheck the check box beside the group and then click **Save**.</span></span>

> <span data-ttu-id="8c1db-160">Per altre informazioni, vedere [Come creare e usare gruppi per gestire account di sviluppatori in Gestione API di Azure][How to create and use groups to manage developer accounts in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="8c1db-160">For more information, see [How to create and use groups to manage developer accounts in Azure API Management][How to create and use groups to manage developer accounts in Azure API Management].</span></span>
> 
> 

## <span data-ttu-id="8c1db-161"><a name="view-subscribers"> </a>Visualizzare i sottoscrittori di un prodotto</span><span class="sxs-lookup"><span data-stu-id="8c1db-161"><a name="view-subscribers"> </a>View subscribers to a product</span></span>
<span data-ttu-id="8c1db-162">Nella scheda **Sottoscrittori** sono elencati gli sviluppatori che hanno sottoscritto il prodotto.</span><span class="sxs-lookup"><span data-stu-id="8c1db-162">The **Subscribers** tab lists the developers who have subscribed to the product.</span></span> <span data-ttu-id="8c1db-163">Per visualizzare i dettagli e le impostazioni per ogni sviluppatore, fare clic sul nome dello sviluppatore.</span><span class="sxs-lookup"><span data-stu-id="8c1db-163">The details and settings for each developer can be viewed by clicking on the developer's name.</span></span> <span data-ttu-id="8c1db-164">In questo esempio nessuno sviluppatore ha ancora sottoscritto il prodotto.</span><span class="sxs-lookup"><span data-stu-id="8c1db-164">In this example no developers have yet subscribed to the product.</span></span>

![Sviluppatori:][api-management-developer-list]

## <span data-ttu-id="8c1db-166"><a name="next-steps"> </a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8c1db-166"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="8c1db-167">Una volta che le API desiderate sono state aggiunte e il prodotto pubblicato, gli sviluppatori possono sottoscrivere il prodotto e iniziare a chiamare le API.</span><span class="sxs-lookup"><span data-stu-id="8c1db-167">Once the desired APIs are added and the product published, developers can subscribe to the product and begin to call the APIs.</span></span> <span data-ttu-id="8c1db-168">Per una dimostrazione di questi elementi e della configurazione avanzata del prodotto, vedere l'esercitazione [Come creare e configurare le impostazioni avanzate del prodotto in Gestione API di Azure][How create and configure advanced product settings in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="8c1db-168">For a tutorial that demonstrates these items as well as advanced product configuration see [How create and configure advanced product settings in Azure API Management][How create and configure advanced product settings in Azure API Management].</span></span>

<span data-ttu-id="8c1db-169">Per altre informazioni sull'uso dei prodotti, vedere il video seguente.</span><span class="sxs-lookup"><span data-stu-id="8c1db-169">For more information about working with products, see the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Using-Products/player]
> 
> 

[Create a product]: #create-product
[Add APIs to a product]: #add-apis
[Add descriptive information to a product]: #add-description
[Publish a product]: #publish-product
[Make a product visible to developers]: #make-visible
[View subscribers to a product]: #view-subscribers
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


[How to add operations to an API]: api-management-howto-add-operations.md
[How to create and publish a product]: api-management-howto-add-products.md
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps
[How to create and use groups to manage developer accounts in Azure API Management]: api-management-howto-create-groups.md
[How create and configure advanced product settings in Azure API Management]: api-management-howto-product-with-rules.md 
