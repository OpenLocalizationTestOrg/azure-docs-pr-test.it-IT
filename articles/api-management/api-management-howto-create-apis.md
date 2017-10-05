---
title: Come creare API in Gestione API di Azure
description: Informazioni su come creare e configurare API in Gestione API di Azure.
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
ms.openlocfilehash: ab08256fbc3caca05bf23a12016ad2acf4fc7412
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-apis-in-azure-api-management"></a><span data-ttu-id="a76ad-103">Come creare API in Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="a76ad-103">How to create APIs in Azure API Management</span></span>
<span data-ttu-id="a76ad-104">Un'API in Gestione API rappresenta un set di operazioni che possono essere richiamate dalle applicazioni client.</span><span class="sxs-lookup"><span data-stu-id="a76ad-104">An API in API Management represents a set of operations that can be invoked by client applications.</span></span> <span data-ttu-id="a76ad-105">Le nuove API vengono create nel portale di pubblicazione e quindi vengono aggiunte le operazioni desiderate.</span><span class="sxs-lookup"><span data-stu-id="a76ad-105">New APIs are created in the publisher portal, and then the desired operations are added.</span></span> <span data-ttu-id="a76ad-106">Dopo l'aggiunta delle operazioni, l'API viene aggiunta a un prodotto e può essere pubblicata.</span><span class="sxs-lookup"><span data-stu-id="a76ad-106">Once the operations are added, the API is added to a product and can be published.</span></span> <span data-ttu-id="a76ad-107">Dopo la pubblicazione l'API può essere sottoscritta e usata dagli sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="a76ad-107">Once an API is published, it can be subscribed to and used by developers.</span></span>

<span data-ttu-id="a76ad-108">Questa guida illustra il primo passaggio del processo per creare e configurare una nuova API in Gestione API.</span><span class="sxs-lookup"><span data-stu-id="a76ad-108">This guide shows the first step in the process: how to create and configure a new API in API Management.</span></span> <span data-ttu-id="a76ad-109">Per altre informazioni sull'aggiunta di operazioni e sulla pubblicazione di un prodotto, vedere [Come aggiungere operazioni a un'API][How to add operations to an API] e [Come creare e pubblicare un prodotto][How to create and publish a product].</span><span class="sxs-lookup"><span data-stu-id="a76ad-109">For more information on adding operations and publishing a product, see [How to add operations to an API][How to add operations to an API] and [How to create and publish a product][How to create and publish a product].</span></span>

## <span data-ttu-id="a76ad-110"><a name="create-new-api"> </a>Creare una nuova API</span><span class="sxs-lookup"><span data-stu-id="a76ad-110"><a name="create-new-api"> </a>Create a new API</span></span>
<span data-ttu-id="a76ad-111">Le API vengono create e configurate nel portale di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="a76ad-111">APIs are created and configured in the publisher portal.</span></span> <span data-ttu-id="a76ad-112">Per accedere al portale di pubblicazione, fare clic su **Portale di pubblicazione** nel portale di Azure per il servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="a76ad-112">To access the publisher portal, click **Publisher portal** in the Azure Portal for your API Management service.</span></span>

![Portale di pubblicazione][api-management-management-console]

> <span data-ttu-id="a76ad-114">Se non è stata creata un'istanza del servizio Gestione API, vedere [Creare un'istanza di Gestione API][Create an API Management service instance] nell'esercitazione [Introduzione a Gestione API di Azure][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="a76ad-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="a76ad-115">Fare clic su **API** dal menu **Gestione API** sulla sinistra, quindi scegliere **Aggiungi API**.</span><span class="sxs-lookup"><span data-stu-id="a76ad-115">Click **APIs** from the **API Management** menu on the left, and then click **add API**.</span></span>

![Create API][api-management-create-api]

<span data-ttu-id="a76ad-117">Usare la finestra **Aggiungi nuova API** per configurare la nuova API.</span><span class="sxs-lookup"><span data-stu-id="a76ad-117">Use the **Add new API** window to configure the new API.</span></span>

![Aggiungi nuova API][api-management-add-new-api]

<span data-ttu-id="a76ad-119">Per configurare la nuova API, vengono usati i campi seguenti.</span><span class="sxs-lookup"><span data-stu-id="a76ad-119">The following fields are used to configure the new API.</span></span>

* <span data-ttu-id="a76ad-120">La casella **Titolo API Web** consente di specificare un nome univoco e descrittivo per l'API,</span><span class="sxs-lookup"><span data-stu-id="a76ad-120">**Web API name** provides a unique and descriptive name for the API.</span></span> <span data-ttu-id="a76ad-121">che viene visualizzato nel portale di pubblicazione e in quello per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="a76ad-121">It is displayed in the developer and publisher portals.</span></span>
* <span data-ttu-id="a76ad-122">Il valore specificato nella casella **URL del servizio Web** fa riferimento al servizio HTTP che implementa l'API</span><span class="sxs-lookup"><span data-stu-id="a76ad-122">**Web service URL** references the HTTP service implementing the API.</span></span> <span data-ttu-id="a76ad-123">e corrisponde all'indirizzo a cui Gestione API inoltra le richieste.</span><span class="sxs-lookup"><span data-stu-id="a76ad-123">API management forwards requests to this address.</span></span>
* <span data-ttu-id="a76ad-124">**Suffisso dell'URL dell'API Web** viene aggiunto all'URL di base del servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="a76ad-124">**Web API URL suffix** is appended to the base URL for the API management service.</span></span> <span data-ttu-id="a76ad-125">L'URL di base è comune a tutte le API ospitate da un'istanza del servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="a76ad-125">The base URL is common for all APIs hosted by an API Management service instance.</span></span> <span data-ttu-id="a76ad-126">Gestione API distingue le API in base al suffisso, quindi è necessario che questo sia univoco per ciascuna API di un editore specifico.</span><span class="sxs-lookup"><span data-stu-id="a76ad-126">API Management distinguishes APIs by their suffix and therefore the suffix must be unique for every API for a given publisher.</span></span>
* <span data-ttu-id="a76ad-127">**Schema URL API Web** determina il protocollo da usare per l'accesso all'API.</span><span class="sxs-lookup"><span data-stu-id="a76ad-127">**Web API URL scheme** determines which protocols can be used to access the API.</span></span> <span data-ttu-id="a76ad-128">Per impostazione predefinita è specificato il valore HTTPs.</span><span class="sxs-lookup"><span data-stu-id="a76ad-128">HTTPs is specified by default.</span></span>
* <span data-ttu-id="a76ad-129">Per aggiungere facoltativamente questa nuova API a un prodotto, fare clic sull’elenco a discesa **Prodotti (facoltativo)** e selezionare un prodotto.</span><span class="sxs-lookup"><span data-stu-id="a76ad-129">To optionally add this new API to a product, click the **Products (optional)** drop-down and choose a product.</span></span> <span data-ttu-id="a76ad-130">Questo passaggio può essere ripetuto più volte per aggiungere l'API a più prodotti.</span><span class="sxs-lookup"><span data-stu-id="a76ad-130">This step can be repeated multiple times to add the API to multiple products.</span></span>

<span data-ttu-id="a76ad-131">Dopo avere configurato i valori desiderati, fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="a76ad-131">Once the desired values are configured, click **Save**.</span></span> <span data-ttu-id="a76ad-132">Una volta creata la nuova API, la pagina di riepilogo dell'API viene visualizzata nel portale di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="a76ad-132">Once the new API is created, the summary page for the API is displayed in the publisher portal.</span></span>

![Riepilogo dell'API][api-management-api-summary]

## <span data-ttu-id="a76ad-134"><a name="configure-api-settings"> </a>Configurare le impostazioni API</span><span class="sxs-lookup"><span data-stu-id="a76ad-134"><a name="configure-api-settings"> </a>Configure API settings</span></span>
<span data-ttu-id="a76ad-135">È possibile usare la scheda **Impostazioni** per verificare e modificare la configurazione di un'API.</span><span class="sxs-lookup"><span data-stu-id="a76ad-135">You can use the **Settings** tab to verify and edit the configuration for an API.</span></span> <span data-ttu-id="a76ad-136">**Titolo API Web**, **URL servizio Web** e **Suffisso dell'URL dell'API Web** vengono impostati inizialmente alla creazione dell'API e possono essere modificati in questa scheda.</span><span class="sxs-lookup"><span data-stu-id="a76ad-136">**Web API name**, **Web service URL**, and **Web API URL suffix** are initially set when the API is created and can be modified here.</span></span> <span data-ttu-id="a76ad-137">**Descrizione** fornisce una descrizione facoltativa e l'opzione **Schema URL API Web** determina il protocollo da usare per l'accesso all'API.</span><span class="sxs-lookup"><span data-stu-id="a76ad-137">**Description** provides an optional description, and **Web API URL scheme** determines which protocols can be used to access the API.</span></span>

![Impostazioni API][api-management-api-settings]

<span data-ttu-id="a76ad-139">Per configurare l’autenticazione gateway per il servizio di back-end che implementa l'API, selezionare la scheda **Sicurezza** .</span><span class="sxs-lookup"><span data-stu-id="a76ad-139">To configure gateway authentication for the backend service implementing the API, select the **Security** tab.</span></span> <span data-ttu-id="a76ad-140">L'elenco a discesa **Con credenziali** può essere usato per configurare l'**HTTP di base** o l'autenticazione con **Certificati client**.</span><span class="sxs-lookup"><span data-stu-id="a76ad-140">The **With credentials** drop-down can be used to configure **HTTP basic** or **Client certificates** authentication.</span></span> <span data-ttu-id="a76ad-141">Per usare l'autenticazione HTTP di base, è sufficiente immettere le credenziali desiderate.</span><span class="sxs-lookup"><span data-stu-id="a76ad-141">To use HTTP basic authentication, simply enter the desired credentials.</span></span> <span data-ttu-id="a76ad-142">Per informazioni sull'uso dell'autenticazione con certificati client, vedere [Come proteggere i servizi back-end usando l'autenticazione con certificati client in Gestione API di Azure][How to secure back-end services using client certificate authentication in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="a76ad-142">For information on using client certificate authentication, see [How to secure back-end services using client certificate authentication in Azure API Management][How to secure back-end services using client certificate authentication in Azure API Management].</span></span>

<span data-ttu-id="a76ad-143">La scheda **Sicurezza** può essere usata anche per configurare l'**Autorizzazione utente** con OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="a76ad-143">The **Security** tab can also be used to configure **User authorization** using OAuth 2.0.</span></span> <span data-ttu-id="a76ad-144">Per altre informazioni, vedere [Come autorizzare gli account per sviluppatori usando OAuth 2.0 in Gestione API di Azure][How to authorize developer accounts using OAuth 2.0 in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="a76ad-144">For more information, see [How to authorize developer accounts using OAuth 2.0 in Azure API Management][How to authorize developer accounts using OAuth 2.0 in Azure API Management].</span></span>

![Impostazioni dell'autenticazione di base][api-management-api-settings-credentials]

<span data-ttu-id="a76ad-146">Fare clic su **Salva** per salvare le modifiche apportate alle impostazioni API.</span><span class="sxs-lookup"><span data-stu-id="a76ad-146">Click **Save** to save any changes you make to the API settings.</span></span>

## <span data-ttu-id="a76ad-147"><a name="next-steps"> </a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a76ad-147"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="a76ad-148">Dopo aver creato un'API e configurato le impostazioni, i passaggi successivi consentono di aggiungere le operazioni all'API, aggiungere l'API a un prodotto e pubblicarla in modo che sia disponibile per gli sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="a76ad-148">Once an API is created and the settings configured, the next steps are to add the operations to the API, add the API to a product, and publish it so that it is available for developers.</span></span> <span data-ttu-id="a76ad-149">Per altre informazioni, vedere gli articoli seguenti.</span><span class="sxs-lookup"><span data-stu-id="a76ad-149">For more information, see the following articles.</span></span>

* <span data-ttu-id="a76ad-150">[Come aggiungere operazioni a un'API][How to add operations to an API]</span><span class="sxs-lookup"><span data-stu-id="a76ad-150">[How to add operations to an API][How to add operations to an API]</span></span>
* <span data-ttu-id="a76ad-151">[Come creare e pubblicare un prodotto][How to create and publish a product]</span><span class="sxs-lookup"><span data-stu-id="a76ad-151">[How to create and publish a product][How to create and publish a product]</span></span>

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

[How to add operations to an API]: api-management-howto-add-operations.md
[How to create and publish a product]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[How to secure back-end services using client certificate authentication in Azure API Management]: api-management-howto-mutual-certificates.md
[How to authorize developer accounts using OAuth 2.0 in Azure API Management]: api-management-howto-oauth2.md
