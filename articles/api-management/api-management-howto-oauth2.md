---
title: Autorizzare gli account per sviluppatori utilizzando OAuth 2.0 in Gestione API di Azure | Documentazione Microsoft
description: Informazioni su come autorizzare gli utenti tramite OAuth 2.0 in Gestione API.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 78c48247-64f0-4708-b2d0-98b61a821283
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: a19c453bb3271374b587f3d0b35adad55863b490
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-authorize-developer-accounts-using-oauth-20-in-azure-api-management"></a><span data-ttu-id="a77cd-103">Come autorizzare gli account per sviluppatori utilizzando OAuth 2.0 in Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="a77cd-103">How to authorize developer accounts using OAuth 2.0 in Azure API Management</span></span>
<span data-ttu-id="a77cd-104">Molte API supportano [OAuth 2.0](http://oauth.net/2/) per proteggere l'API e assicurare che solo gli utenti validi siano autorizzati all'accesso e che possano accedere solo alle risorse a cui hanno diritto.</span><span class="sxs-lookup"><span data-stu-id="a77cd-104">Many APIs support [OAuth 2.0](http://oauth.net/2/) to secure the API and ensure that only valid users have access, and they can only access resources to which they're entitled.</span></span> <span data-ttu-id="a77cd-105">Per usare la console per sviluppatori interattiva di Gestione API di Azure con queste API, il servizio permette di configurare l'istanza del servizio per l'uso delle API abilitate per OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="a77cd-105">In order to use Azure API Management's interactive Developer Console with such APIs, the service allows you to configure your service instance to work with your OAuth 2.0 enabled API.</span></span>

## <span data-ttu-id="a77cd-106"><a name="prerequisites"> </a>Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a77cd-106"><a name="prerequisites"> </a>Prerequisites</span></span>
<span data-ttu-id="a77cd-107">Questa guida illustra come configurare un'istanza del servizio Gestione API per l'uso dell'autorizzazione OAuth 2.0 per gli account per sviluppatori, ma non viene spiegato come configurare un provider OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="a77cd-107">This guide shows you how to configure your API Management service instance to use OAuth 2.0 authorization for developer accounts, but does not show you how to configure an OAuth 2.0 provider.</span></span> <span data-ttu-id="a77cd-108">La configurazione cambia in base al provider OAuth 2.0, sebbene le procedure siano simili e le informazioni necessarie usate per la configurazione di OAuth 2.0 nell'istanza del servizio Gestione API siano le stesse.</span><span class="sxs-lookup"><span data-stu-id="a77cd-108">The configuration for each OAuth 2.0 provider is different, although the steps are similar, and the required pieces of information used in configuring OAuth 2.0 in your API Management service instance are the same.</span></span> <span data-ttu-id="a77cd-109">Questo argomento mostra degli esempi di utilizzo di Azure Active Directory come provider OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="a77cd-109">This topic shows examples using Azure Active Directory as an OAuth 2.0 provider.</span></span>

> [!NOTE]
> <span data-ttu-id="a77cd-110">Per altre informazioni sulla configurazione di OAuth 2.0 mediante Azure Active Directory, vedere l'esempio [WebApp-GraphAPI-DotNet][WebApp-GraphAPI-DotNet].</span><span class="sxs-lookup"><span data-stu-id="a77cd-110">For more information on configuring OAuth 2.0 using Azure Active Directory, see the [WebApp-GraphAPI-DotNet][WebApp-GraphAPI-DotNet] sample.</span></span>
> 
> 

## <span data-ttu-id="a77cd-111"><a name="step1"> </a>Configurare un server autorizzazione OAuth 2.0 in Gestione API</span><span class="sxs-lookup"><span data-stu-id="a77cd-111"><a name="step1"> </a>Configure an OAuth 2.0 authorization server in API Management</span></span>
<span data-ttu-id="a77cd-112">Per iniziare, fare clic sul **portale di pubblicazione** nel Portale di Azure relativo al servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="a77cd-112">To get started, click **Publisher portal** in the Azure Portal for your API Management service.</span></span>

![Portale di pubblicazione][api-management-management-console]

> [!NOTE]
> <span data-ttu-id="a77cd-114">Se non è stata creata un'istanza del servizio Gestione API, vedere [Creare un'istanza di Gestione API][Create an API Management service instance] nell'esercitazione [Introduzione a Gestione API di Azure][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="a77cd-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="a77cd-115">Fare clic su **Sicurezza** dal menu **Gestione API** a sinistra, scegliere **OAuth 2.0** e fare clic su **Add authorization server**.</span><span class="sxs-lookup"><span data-stu-id="a77cd-115">Click **Security** from the **API Management** menu on the left, click **OAuth 2.0**, and then click **Add authorization server**.</span></span>

![OAuth 2.0][api-management-oauth2]

<span data-ttu-id="a77cd-117">Dopo aver fatto clic su **Add authorization server**, viene visualizzato il modulo per il nuovo server autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="a77cd-117">After clicking **Add authorization server**, the new authorization server form is displayed.</span></span>

![Nuovo server][api-management-oauth2-server-1]

<span data-ttu-id="a77cd-119">Immettere un nome ed eventualmente una descrizione nei campi **Nome** e **Descrizione**.</span><span class="sxs-lookup"><span data-stu-id="a77cd-119">Enter a name and an optional description in the **Name** and **Description** fields.</span></span> 

> [!NOTE]
> <span data-ttu-id="a77cd-120">Questi campi vengono usati per identificare il server autorizzazione OAuth 2.0 all'interno dell'istanza del servizio Gestione API corrente e i loro valori non provengono dal server OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="a77cd-120">These fields are used to identify the OAuth 2.0 authorization server within the current API Management service instance and their values do not come from the OAuth 2.0 server.</span></span>
> 
> 

<span data-ttu-id="a77cd-121">Immettere il **Client registration page URL**.</span><span class="sxs-lookup"><span data-stu-id="a77cd-121">Enter the **Client registration page URL**.</span></span> <span data-ttu-id="a77cd-122">In questa pagina gli utenti possono creare e gestire i loro account e il suo contenuto varia in base al provider OAuth 2.0 usato.</span><span class="sxs-lookup"><span data-stu-id="a77cd-122">This page is where users can create and manage their accounts, and varies depending on the OAuth 2.0 provider used.</span></span> <span data-ttu-id="a77cd-123">**Client registration page URL** fa riferimento alla pagina che gli utenti possono usare per creare e configurare i propri account per i provider OAuth 2.0 che supportano la gestione degli account da parte degli utenti.</span><span class="sxs-lookup"><span data-stu-id="a77cd-123">The **Client registration page URL** points to the page that users can use to create and configure their own accounts for OAuth 2.0 providers that support user management of accounts.</span></span> <span data-ttu-id="a77cd-124">Alcune organizzazioni non configurano o usano questa funzionalità, anche se è supportata dal provider OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="a77cd-124">Some organizations do not configure or use this functionality even if the OAuth 2.0 provider supports it.</span></span> <span data-ttu-id="a77cd-125">Se nel provider OAuth 2.0 non è stata configurata la gestione degli account da parte degli utenti, immettere qui un URL segnaposto, ad esempio l'URL della propria azienda, oppure un URL analogo a `https://placeholder.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="a77cd-125">If your OAuth 2.0 provider does not have user management of accounts configured, enter a placeholder URL here such as the URL of your company, or a URL such as `https://placeholder.contoso.com`.</span></span>

<span data-ttu-id="a77cd-126">La sezione successiva del modulo contiene le impostazioni relative a **Authorization code grant types**, **Authorization endpoint URL** e **Authorization request method**.</span><span class="sxs-lookup"><span data-stu-id="a77cd-126">The next section of the form contains the **Authorization code grant types**, **Authorization endpoint URL**, and **Authorization request method** settings.</span></span>

![Nuovo server][api-management-oauth2-server-2]

<span data-ttu-id="a77cd-128">Selezionare i tipi desiderati in **Authorization code grant types** .</span><span class="sxs-lookup"><span data-stu-id="a77cd-128">Specify the **Authorization code grant types** by checking the desired types.</span></span> <span data-ttu-id="a77cd-129">**Authorization code** è specificato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="a77cd-129">**Authorization code** is specified by default.</span></span>

<span data-ttu-id="a77cd-130">Immettere il valore relativo a **Authorization endpoint URL**.</span><span class="sxs-lookup"><span data-stu-id="a77cd-130">Enter the **Authorization endpoint URL**.</span></span> <span data-ttu-id="a77cd-131">Per Azure Active Directory, questo URL sarà simile all'URL seguente, dove `<client_id>` viene sostituito dall'ID client che identifica l'applicazione in uso nel server OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="a77cd-131">For Azure Active Directory, this URL will be similar to the following URL, where `<client_id>` is replaced with the client id that identifies your application to the OAuth 2.0 server.</span></span>

`https://login.microsoftonline.com/<client_id>/oauth2/authorize`

<span data-ttu-id="a77cd-132">L'impostazione **Authorization request method** specifica la modalità di invio della richiesta di autorizzazione al server OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="a77cd-132">The **Authorization request method** specifies how the authorization request is sent to the OAuth 2.0 server.</span></span> <span data-ttu-id="a77cd-133">Il valore selezionato per impostazione predefinita è **GET** .</span><span class="sxs-lookup"><span data-stu-id="a77cd-133">By default **GET** is selected.</span></span>

<span data-ttu-id="a77cd-134">Nella sezione successiva vengono specificate le impostazioni **Token endpoint URL**, **Client authentication methods**, **Access token sending method** e **Ambito predefinito**.</span><span class="sxs-lookup"><span data-stu-id="a77cd-134">The next section is where the **Token endpoint URL**, **Client authentication methods**, **Access token sending method**, and **Default scope** are specified.</span></span>

![Nuovo server][api-management-oauth2-server-3]

<span data-ttu-id="a77cd-136">Per un server OAuth 2.0 di Azure Active Directory, il **Token endpoint URL** avrà il seguente formato, dove `<APPID>` avrà il formato `yourapp.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="a77cd-136">For an Azure Active Directory OAuth 2.0 server, the **Token endpoint URL** will have the following format, where `<APPID>`  has the format of `yourapp.onmicrosoft.com`.</span></span>

`https://login.microsoftonline.com/<APPID>/oauth2/token`

<span data-ttu-id="a77cd-137">L'impostazione predefinita di **Client authentication methods** è **Basic**, mentre quella di **Access token sending method** è **Authorization header**.</span><span class="sxs-lookup"><span data-stu-id="a77cd-137">The default setting for **Client authentication methods** is **Basic**, and  **Access token sending method** is **Authorization header**.</span></span> <span data-ttu-id="a77cd-138">Questi valori vengono configurati in questa sezione del modulo, insieme a **Default scope**.</span><span class="sxs-lookup"><span data-stu-id="a77cd-138">These values are configured on this section of the form, along with the **Default scope**.</span></span>

<span data-ttu-id="a77cd-139">La sezione **Credenziali client** contiene l'**ID client** e il **Segreto client**, che vengono ricavati durante il processo di creazione e configurazione del server OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="a77cd-139">The **Client credentials** section contains the **Client ID** and **Client secret**, which are obtained during the creation and configuration process of your OAuth 2.0 server.</span></span> <span data-ttu-id="a77cd-140">Una volta specificati l'**ID client** e il **Segreto client**, viene generato il **redirect_uri** per il **codice autorizzazione**.</span><span class="sxs-lookup"><span data-stu-id="a77cd-140">Once the **Client ID** and **Client secret** are specified, the **redirect_uri** for the **authorization code** is generated.</span></span> <span data-ttu-id="a77cd-141">Questo URI viene usato per configurare l'URL di risposta nella configurazione del server OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="a77cd-141">This URI is used to configure the reply URL in your OAuth 2.0 server configuration.</span></span>

![Nuovo server][api-management-oauth2-server-4]

<span data-ttu-id="a77cd-143">Se **Authorization code grant types** è impostato su **Resource owner password**, la sezione **Resource owner password credentials** viene usata per specificare le credenziali; in caso contrario è possibile lasciarla vuota.</span><span class="sxs-lookup"><span data-stu-id="a77cd-143">If **Authorization code grant types** is set to **Resource owner password**, the **Resource owner password credentials** section is used to specify those credentials; otherwise you can leave it blank.</span></span>

![Nuovo server][api-management-oauth2-server-5]

<span data-ttu-id="a77cd-145">Dopo aver completato il modulo, fare clic su **Salva** per salvare la configurazione del server autorizzazione OAuth 2.0 di Gestione API.</span><span class="sxs-lookup"><span data-stu-id="a77cd-145">Once the form is complete, click **Save** to save the API Management OAuth 2.0 authorization server configuration.</span></span> <span data-ttu-id="a77cd-146">Dopo aver salvato la configurazione del server, è possibile configurare le API in modo che usino questa configurazione, come illustrato nella sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="a77cd-146">Once the server configuration is saved, you can configure APIs to use this configuration, as shown in the next section.</span></span>

## <span data-ttu-id="a77cd-147"><a name="step2"> </a>Configurare un'API per l'uso di un'autorizzazione utente OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="a77cd-147"><a name="step2"> </a>Configure an API to use OAuth 2.0 user authorization</span></span>
<span data-ttu-id="a77cd-148">Fare clic su **API** dal menu **Gestione API** a sinistra, fare clic sul nome dell'API desiderata, scegliere **Sicurezza**, quindi selezionare la casella relativa a **OAuth 2.0**.</span><span class="sxs-lookup"><span data-stu-id="a77cd-148">Click **APIs** from the **API Management** menu on the left, click the name of the desired API, click **Security**, and then check the box for **OAuth 2.0**.</span></span>

![Autorizzazione utente][api-management-user-authorization]

<span data-ttu-id="a77cd-150">Selezionare il **server autorizzazione** desiderato dall'elenco a discesa e fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="a77cd-150">Select the desired **Authorization server** from the drop-down list, and click **Save**.</span></span>

![Autorizzazione utente][api-management-user-authorization-save]

## <span data-ttu-id="a77cd-152"><a name="step3"> </a>Test dell'autorizzazione utente OAuth 2.0 nel Portale per sviluppatori</span><span class="sxs-lookup"><span data-stu-id="a77cd-152"><a name="step3"> </a>Test the OAuth 2.0 user authorization in the Developer Portal</span></span>
<span data-ttu-id="a77cd-153">Dopo aver configurato il server autorizzazione OAuth 2.0 e l'API per l'uso di tale server, è possibile testarlo andando al portale per sviluppatori e chiamando un'API.</span><span class="sxs-lookup"><span data-stu-id="a77cd-153">Once you have configured your OAuth 2.0 authorization server and configured your API to use that server, you can test it by going to the Developer Portal and calling an API.</span></span>  <span data-ttu-id="a77cd-154">Fare clic su **Developer portal** nel menu in alto a destra.</span><span class="sxs-lookup"><span data-stu-id="a77cd-154">Click **Developer portal** in the top right menu.</span></span>

![Portale per sviluppatori][api-management-developer-portal-menu]

<span data-ttu-id="a77cd-156">Fare clic su **API** nel menu superiore e scegliere **API Echo**.</span><span class="sxs-lookup"><span data-stu-id="a77cd-156">Click **APIs** in the top menu and select **Echo API**.</span></span>

![API Echo][api-management-apis-echo-api]

> [!NOTE]
> <span data-ttu-id="a77cd-158">Se è stata configurata una sola API o se ne è visibile solo una per l'account, facendo clic sulle API vengono visualizzate le operazioni per l'API.</span><span class="sxs-lookup"><span data-stu-id="a77cd-158">If you have only one API configured or visible to your account, then clicking APIs takes you directly to the operations for that API.</span></span>
> 
> 

<span data-ttu-id="a77cd-159">Selezionare l'operazione **GET su risorsa**, fare clic su **Apri console**, quindi selezionare **codice di autorizzazione** dal menu a discesa.</span><span class="sxs-lookup"><span data-stu-id="a77cd-159">Select the **GET Resource** operation, click **Open Console**, and then select **Authorization code** from the drop-down.</span></span>

![Open console][api-management-open-console]

<span data-ttu-id="a77cd-161">Quando **Authorization code** è selezionato, viene visualizzata una finestra popup con il modulo di accesso del provider OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="a77cd-161">When **Authorization code** is selected, a pop-up window is displayed with the sign-in form of the OAuth 2.0 provider.</span></span> <span data-ttu-id="a77cd-162">In questo esempio il modulo di accesso viene fornito da Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a77cd-162">In this example the sign-in form is provided by Azure Active Directory.</span></span>

> [!NOTE]
> <span data-ttu-id="a77cd-163">Se i popup sono stati disattivati, verrà richiesto di attivarli tramite il browser.</span><span class="sxs-lookup"><span data-stu-id="a77cd-163">If you have pop-ups disabled you will be prompted to enable them by the browser.</span></span> <span data-ttu-id="a77cd-164">Dopo averli attivati, selezionare di nuovo **Authorization code** per visualizzare il modulo di accesso.</span><span class="sxs-lookup"><span data-stu-id="a77cd-164">After you enable them, select **Authorization code** again and the sign-in form will be displayed.</span></span>
> 
> 

![pagina di accesso][api-management-oauth2-signin]

<span data-ttu-id="a77cd-166">Dopo aver effettuato l'accesso, le **intestazioni della richiesta** vengono compilate con un'intestazione `Authorization : Bearer` che autorizza la richiesta.</span><span class="sxs-lookup"><span data-stu-id="a77cd-166">Once you have signed in, the **Request headers** are populated with an `Authorization : Bearer` header that authorizes the request.</span></span>

![Token di intestazione della richiesta][api-management-request-header-token]

<span data-ttu-id="a77cd-168">A questo punto è possibile configurare i valori desiderati per i restanti parametri e inviare la richiesta.</span><span class="sxs-lookup"><span data-stu-id="a77cd-168">At this point you can configure the desired values for the remaining parameters, and submit the request.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a77cd-169">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a77cd-169">Next steps</span></span>
<span data-ttu-id="a77cd-170">Per altre informazioni sull'uso di OAuth 2.0 e di Gestione API, vedere il video seguente e l’ [articolo](api-management-howto-protect-backend-with-aad.md)correlato.</span><span class="sxs-lookup"><span data-stu-id="a77cd-170">For more information about using OAuth 2.0 and API Management, see the following video and accompanying [article](api-management-howto-protect-backend-with-aad.md).</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Protecting-Web-API-Backend-with-Azure-Active-Directory-and-API-Management/player]
> 
> 

[api-management-management-console]: ./media/api-management-howto-oauth2/api-management-management-console.png
[api-management-oauth2]: ./media/api-management-howto-oauth2/api-management-oauth2.png
[api-management-user-authorization]: ./media/api-management-howto-oauth2/api-management-user-authorization.png
[api-management-user-authorization-save]: ./media/api-management-howto-oauth2/api-management-user-authorization-save.png
[api-management-oauth2-signin]: ./media/api-management-howto-oauth2/api-management-oauth2-signin.png
[api-management-request-header-token]: ./media/api-management-howto-oauth2/api-management-request-header-token.png
[api-management-developer-portal-menu]: ./media/api-management-howto-oauth2/api-management-developer-portal-menu.png
[api-management-open-console]: ./media/api-management-howto-oauth2/api-management-open-console.png
[api-management-oauth2-server-1]: ./media/api-management-howto-oauth2/api-management-oauth2-server-1.png
[api-management-oauth2-server-2]: ./media/api-management-howto-oauth2/api-management-oauth2-server-2.png
[api-management-oauth2-server-3]: ./media/api-management-howto-oauth2/api-management-oauth2-server-3.png
[api-management-oauth2-server-4]: ./media/api-management-howto-oauth2/api-management-oauth2-server-4.png
[api-management-oauth2-server-5]: ./media/api-management-howto-oauth2/api-management-oauth2-server-5.png
[api-management-apis-echo-api]: ./media/api-management-howto-oauth2/api-management-apis-echo-api.png


[How to add operations to an API]: api-management-howto-add-operations.md
[How to add and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs to a product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API to use OAuth 2.0 user authorization]: #step2
[Test the OAuth 2.0 user authorization in the Developer Portal]: #step3
[Next steps]: #next-steps

