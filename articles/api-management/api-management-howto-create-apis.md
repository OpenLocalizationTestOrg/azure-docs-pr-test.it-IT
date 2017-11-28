---
title: aaaHow toocreate API di gestione API di Azure
description: Informazioni su come toocreate e configurare le API di gestione API di Azure.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 14c20da4-f29f-4b28-bec7-3d4c50b734da
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 48ed8d93947253aa1e67ad995927ed6101cac072
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-apis-in-azure-api-management"></a><span data-ttu-id="f867f-103">Come toocreate API di gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="f867f-103">How toocreate APIs in Azure API Management</span></span>
<span data-ttu-id="f867f-104">Un'API in Gestione API rappresenta un set di operazioni che possono essere richiamate dalle applicazioni client.</span><span class="sxs-lookup"><span data-stu-id="f867f-104">An API in API Management represents a set of operations that can be invoked by client applications.</span></span> <span data-ttu-id="f867f-105">Vengono create nuove API nel portale di pubblicazione hello e quindi hello lo si desidera aggiungere le operazioni.</span><span class="sxs-lookup"><span data-stu-id="f867f-105">New APIs are created in hello publisher portal, and then hello desired operations are added.</span></span> <span data-ttu-id="f867f-106">Dopo aver aggiungono le operazioni di hello, hello API viene aggiunto tooa prodotto e può essere pubblicato.</span><span class="sxs-lookup"><span data-stu-id="f867f-106">Once hello operations are added, hello API is added tooa product and can be published.</span></span> <span data-ttu-id="f867f-107">Dopo aver pubblicata un'API, può essere sottoscritto tooand utilizzato dagli sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="f867f-107">Once an API is published, it can be subscribed tooand used by developers.</span></span>

<span data-ttu-id="f867f-108">Questa guida illustra innanzitutto hello nel processo di hello: modalità toocreate e configurare una nuova API di gestione API.</span><span class="sxs-lookup"><span data-stu-id="f867f-108">This guide shows hello first step in hello process: how toocreate and configure a new API in API Management.</span></span> <span data-ttu-id="f867f-109">Per ulteriori informazioni sull'aggiunta di operazioni e sulla pubblicazione di un prodotto, vedere [come tooadd operazioni tooan API] [ How tooadd operations tooan API] e [come toocreate e pubblicazione di un prodotto] [ How toocreate and publish a product].</span><span class="sxs-lookup"><span data-stu-id="f867f-109">For more information on adding operations and publishing a product, see [How tooadd operations tooan API][How tooadd operations tooan API] and [How toocreate and publish a product][How toocreate and publish a product].</span></span>

## <span data-ttu-id="f867f-110"><a name="create-new-api"></a>Creare una nuova API</span><span class="sxs-lookup"><span data-stu-id="f867f-110"><a name="create-new-api"> </a>Create a new API</span></span>
<span data-ttu-id="f867f-111">API create e configurate nel portale di pubblicazione hello.</span><span class="sxs-lookup"><span data-stu-id="f867f-111">APIs are created and configured in hello publisher portal.</span></span> <span data-ttu-id="f867f-112">Fare clic su portale, server di pubblicazione di hello tooaccess **portale di pubblicazione** in hello portale di Azure per il servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="f867f-112">tooaccess hello publisher portal, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span>

![Portale di pubblicazione][api-management-management-console]

> <span data-ttu-id="f867f-114">Se non è ancora stato creato un'istanza del servizio Gestione API, vedere [creare un'istanza del servizio Gestione API] [ Create an API Management service instance] in hello [Introduzione a gestione API di Azure] [ Get started with Azure API Management] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="f867f-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="f867f-115">Fare clic su **API** da hello **gestione API** menu hello a sinistra e quindi fare clic su **aggiungere API**.</span><span class="sxs-lookup"><span data-stu-id="f867f-115">Click **APIs** from hello **API Management** menu on hello left, and then click **add API**.</span></span>

![Create API][api-management-create-api]

<span data-ttu-id="f867f-117">Hello utilizzare **aggiungere una nuova API** tooconfigure finestra hello nuova API.</span><span class="sxs-lookup"><span data-stu-id="f867f-117">Use hello **Add new API** window tooconfigure hello new API.</span></span>

![Add new API][api-management-add-new-api]

<span data-ttu-id="f867f-119">Hello seguente i campi è utilizzati tooconfigure hello nuova API.</span><span class="sxs-lookup"><span data-stu-id="f867f-119">hello following fields are used tooconfigure hello new API.</span></span>

* <span data-ttu-id="f867f-120">**Nome API Web** fornisce un nome descrittivo e univoco per hello API.</span><span class="sxs-lookup"><span data-stu-id="f867f-120">**Web API name** provides a unique and descriptive name for hello API.</span></span> <span data-ttu-id="f867f-121">Viene visualizzato nei portali di hello developer e server di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="f867f-121">It is displayed in hello developer and publisher portals.</span></span>
* <span data-ttu-id="f867f-122">**URL servizio Web** riferimenti hello servizio HTTP implementazione hello API.</span><span class="sxs-lookup"><span data-stu-id="f867f-122">**Web service URL** references hello HTTP service implementing hello API.</span></span> <span data-ttu-id="f867f-123">Gestione API inoltra le richieste toothis indirizzo.</span><span class="sxs-lookup"><span data-stu-id="f867f-123">API management forwards requests toothis address.</span></span>
* <span data-ttu-id="f867f-124">**Suffisso URL dell'API Web** è l'URL di base per il servizio Gestione API hello toohello aggiunto.</span><span class="sxs-lookup"><span data-stu-id="f867f-124">**Web API URL suffix** is appended toohello base URL for hello API management service.</span></span> <span data-ttu-id="f867f-125">URL di base Hello è comune per tutte le API ospitate da un'istanza del servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="f867f-125">hello base URL is common for all APIs hosted by an API Management service instance.</span></span> <span data-ttu-id="f867f-126">Gestione API consente di distinguere le API per il suffisso e pertanto suffisso hello deve essere univoco per tutte le API per un server di pubblicazione specificato.</span><span class="sxs-lookup"><span data-stu-id="f867f-126">API Management distinguishes APIs by their suffix and therefore hello suffix must be unique for every API for a given publisher.</span></span>
* <span data-ttu-id="f867f-127">**Lo schema dell'URL di API Web** determina quali protocolli possono essere utilizzati tooaccess hello API.</span><span class="sxs-lookup"><span data-stu-id="f867f-127">**Web API URL scheme** determines which protocols can be used tooaccess hello API.</span></span> <span data-ttu-id="f867f-128">Per impostazione predefinita è specificato il valore HTTPs.</span><span class="sxs-lookup"><span data-stu-id="f867f-128">HTTPs is specified by default.</span></span>
* <span data-ttu-id="f867f-129">toooptionally aggiungere questo nuovo prodotto tooa API, fare clic su hello **prodotti (facoltativi)** elenco a discesa e selezionare un prodotto.</span><span class="sxs-lookup"><span data-stu-id="f867f-129">toooptionally add this new API tooa product, click hello **Products (optional)** drop-down and choose a product.</span></span> <span data-ttu-id="f867f-130">Questo passaggio può essere ripetuto più volte tooadd hello API toomultiple prodotti.</span><span class="sxs-lookup"><span data-stu-id="f867f-130">This step can be repeated multiple times tooadd hello API toomultiple products.</span></span>

<span data-ttu-id="f867f-131">Una volta hello lo si desidera che i valori sono configurati, fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="f867f-131">Once hello desired values are configured, click **Save**.</span></span> <span data-ttu-id="f867f-132">Una volta creato, hello nuova API hello pagina Riepilogo per l'API di hello viene visualizzato nel portale di pubblicazione hello.</span><span class="sxs-lookup"><span data-stu-id="f867f-132">Once hello new API is created, hello summary page for hello API is displayed in hello publisher portal.</span></span>

![Riepilogo dell'API][api-management-api-summary]

## <span data-ttu-id="f867f-134"><a name="configure-api-settings"></a>Configurare le impostazioni API</span><span class="sxs-lookup"><span data-stu-id="f867f-134"><a name="configure-api-settings"> </a>Configure API settings</span></span>
<span data-ttu-id="f867f-135">È possibile utilizzare hello **impostazioni** scheda tooverify e modificare la configurazione di hello per un'API.</span><span class="sxs-lookup"><span data-stu-id="f867f-135">You can use hello **Settings** tab tooverify and edit hello configuration for an API.</span></span> <span data-ttu-id="f867f-136">**Nome API Web**, **URL servizio Web**, e **suffisso URL di Web API** vengono inizialmente impostate qui quando hello API viene creato e può essere modificato.</span><span class="sxs-lookup"><span data-stu-id="f867f-136">**Web API name**, **Web service URL**, and **Web API URL suffix** are initially set when hello API is created and can be modified here.</span></span> <span data-ttu-id="f867f-137">**Descrizione** fornisce una descrizione opzionale e **lo schema dell'URL di Web API** determina quali protocolli possono essere utilizzati tooaccess hello API.</span><span class="sxs-lookup"><span data-stu-id="f867f-137">**Description** provides an optional description, and **Web API URL scheme** determines which protocols can be used tooaccess hello API.</span></span>

![Impostazioni API][api-management-api-settings]

<span data-ttu-id="f867f-139">l'autenticazione del gateway tooconfigure per hello back-end del servizio API di hello implementazione, selezionare hello **sicurezza** hello scheda **con credenziali** elenco a discesa può essere utilizzati tooconfigure **HTTP base** o **i certificati Client** l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="f867f-139">tooconfigure gateway authentication for hello backend service implementing hello API, select hello **Security** tab. hello **With credentials** drop-down can be used tooconfigure **HTTP basic** or **Client certificates** authentication.</span></span> <span data-ttu-id="f867f-140">l'autenticazione di base toouse HTTP, è sufficiente immettere le credenziali di hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="f867f-140">toouse HTTP basic authentication, simply enter hello desired credentials.</span></span> <span data-ttu-id="f867f-141">Per informazioni sull'utilizzo di autenticazione del certificato client, vedere [toosecure servizi di back-end tramite client come certificato di autenticazione in Gestione API di Azure][How toosecure back-end services using client certificate authentication in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="f867f-141">For information on using client certificate authentication, see [How toosecure back-end services using client certificate authentication in Azure API Management][How toosecure back-end services using client certificate authentication in Azure API Management].</span></span>

<span data-ttu-id="f867f-142">Hello **sicurezza** scheda può essere anche usato tooconfigure **l'autorizzazione utente** mediante OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="f867f-142">hello **Security** tab can also be used tooconfigure **User authorization** using OAuth 2.0.</span></span> <span data-ttu-id="f867f-143">Per ulteriori informazioni, vedere [modalità sviluppatore tooauthorize degli account con OAuth 2.0 in Gestione API di Azure][How tooauthorize developer accounts using OAuth 2.0 in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="f867f-143">For more information, see [How tooauthorize developer accounts using OAuth 2.0 in Azure API Management][How tooauthorize developer accounts using OAuth 2.0 in Azure API Management].</span></span>

![Impostazioni dell'autenticazione di base][api-management-api-settings-credentials]

<span data-ttu-id="f867f-145">Fare clic su **salvare** toosave le modifiche apportate toohello le impostazioni dell'API.</span><span class="sxs-lookup"><span data-stu-id="f867f-145">Click **Save** toosave any changes you make toohello API settings.</span></span>

## <span data-ttu-id="f867f-146"><a name="next-steps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f867f-146"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="f867f-147">Dopo che viene creata un'API impostazioni hello configurate, passaggi successivi hello tooadd hello operazioni toohello API, aggiungere hello API tooa prodotto e pubblicarlo in modo che sia disponibile per gli sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="f867f-147">Once an API is created and hello settings configured, hello next steps are tooadd hello operations toohello API, add hello API tooa product, and publish it so that it is available for developers.</span></span> <span data-ttu-id="f867f-148">Per ulteriori informazioni, vedere hello seguenti articoli.</span><span class="sxs-lookup"><span data-stu-id="f867f-148">For more information, see hello following articles.</span></span>

* <span data-ttu-id="f867f-149">[Come tooadd operazioni tooan API][How tooadd operations tooan API]</span><span class="sxs-lookup"><span data-stu-id="f867f-149">[How tooadd operations tooan API][How tooadd operations tooan API]</span></span>
* <span data-ttu-id="f867f-150">[Come toocreate e pubblicazione di un prodotto][How toocreate and publish a product]</span><span class="sxs-lookup"><span data-stu-id="f867f-150">[How toocreate and publish a product][How toocreate and publish a product]</span></span>

[api-management-create-api]: ./media/api-management-howto-create-apis/api-management-create-api.png
[api-management-management-console]: ./media/api-management-howto-create-apis/api-management-management-console.png
[api-management-add-new-api]: ./media/api-management-howto-create-apis/api-management-add-new-api.png
[api-management-api-settings]: ./media/api-management-howto-create-apis/api-management-api-settings.png
[api-management-api-settings-credentials]: ./media/api-management-howto-create-apis/api-management-api-settings-credentials.png
[api-management-api-summary]: ./media/api-management-howto-create-apis/api-management-api-summary.png
[api-management-echo-operations]: ./media/api-management-howto-create-apis/api-management-echo-operations.png

[What is an API?]: #what-is-api
[Create a new API]: #create-new-api
[Configure API settings]: #configure-api-settings
[Configure API operations]: #configure-api-operations
[Next steps]: #next-steps

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[How toosecure back-end services using client certificate authentication in Azure API Management]: api-management-howto-mutual-certificates.md
[How tooauthorize developer accounts using OAuth 2.0 in Azure API Management]: api-management-howto-oauth2.md
