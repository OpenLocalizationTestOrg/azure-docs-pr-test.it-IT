---
title: gli account sviluppatore aaaAuthorize mediante OAuth 2.0 in Gestione API di Azure | Documenti Microsoft
description: Informazioni su come gli utenti tooauthorize mediante OAuth 2.0 in Gestione API.
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
ms.openlocfilehash: 934901dd6df399470a3257bf7a3a9b9fb5f40d5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthorize-developer-accounts-using-oauth-20-in-azure-api-management"></a><span data-ttu-id="eaf8c-103">La modalità sviluppatore tooauthorize degli account con OAuth 2.0 in Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="eaf8c-103">How tooauthorize developer accounts using OAuth 2.0 in Azure API Management</span></span>
<span data-ttu-id="eaf8c-104">Supportano molte API [OAuth 2.0](http://oauth.net/2/) toosecure hello API e garantire che solo gli utenti validi hanno accesso, e possono accedere solo alle risorse toowhich hanno diritto.</span><span class="sxs-lookup"><span data-stu-id="eaf8c-104">Many APIs support [OAuth 2.0](http://oauth.net/2/) toosecure hello API and ensure that only valid users have access, and they can only access resources toowhich they're entitled.</span></span> <span data-ttu-id="eaf8c-105">Nella Console per sviluppatori di interattiva della gestione degli ordini toouse Azure API con tali API servizio hello consente tooconfigure toowork di istanza del servizio con il OAuth 2.0 abilitato API.</span><span class="sxs-lookup"><span data-stu-id="eaf8c-105">In order toouse Azure API Management's interactive Developer Console with such APIs, hello service allows you tooconfigure your service instance toowork with your OAuth 2.0 enabled API.</span></span>

## <span data-ttu-id="eaf8c-106"><a name="prerequisites"></a>Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="eaf8c-106"><a name="prerequisites"> </a>Prerequisites</span></span>
<span data-ttu-id="eaf8c-107">Questa guida viene spiegato come tooconfigure toouse di istanza del servizio Gestione API autorizzazione OAuth 2.0 per sviluppatori di account, ma non verrà visualizzato come provider tooconfigure un OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="eaf8c-107">This guide shows you how tooconfigure your API Management service instance toouse OAuth 2.0 authorization for developer accounts, but does not show you how tooconfigure an OAuth 2.0 provider.</span></span> <span data-ttu-id="eaf8c-108">configurazione di Hello per ogni provider è diverso, sebbene hello passaggi sono simili e hello necessarie le informazioni utilizzate nella configurazione di OAuth 2.0 in all'istanza del servizio Gestione API sono di OAuth 2.0 hello stesso.</span><span class="sxs-lookup"><span data-stu-id="eaf8c-108">hello configuration for each OAuth 2.0 provider is different, although hello steps are similar, and hello required pieces of information used in configuring OAuth 2.0 in your API Management service instance are hello same.</span></span> <span data-ttu-id="eaf8c-109">Questo argomento mostra degli esempi di utilizzo di Azure Active Directory come provider OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="eaf8c-109">This topic shows examples using Azure Active Directory as an OAuth 2.0 provider.</span></span>

> [!NOTE]
> <span data-ttu-id="eaf8c-110">Per ulteriori informazioni sulla configurazione di OAuth 2.0 tramite Azure Active Directory, vedere hello [WebApp-GraphAPI-DotNet] [ WebApp-GraphAPI-DotNet] esempio.</span><span class="sxs-lookup"><span data-stu-id="eaf8c-110">For more information on configuring OAuth 2.0 using Azure Active Directory, see hello [WebApp-GraphAPI-DotNet][WebApp-GraphAPI-DotNet] sample.</span></span>
> 
> 

## <span data-ttu-id="eaf8c-111"><a name="step1"> </a>Configurare un server autorizzazione OAuth 2.0 in Gestione API</span><span class="sxs-lookup"><span data-stu-id="eaf8c-111"><a name="step1"> </a>Configure an OAuth 2.0 authorization server in API Management</span></span>
<span data-ttu-id="eaf8c-112">tooget avviato, fare clic su **portale di pubblicazione** in hello portale di Azure per il servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="eaf8c-112">tooget started, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span>

![Portale di pubblicazione][api-management-management-console]

> [!NOTE]
> <span data-ttu-id="eaf8c-114">Se non è ancora stato creato un'istanza del servizio Gestione API, vedere [creare un'istanza del servizio Gestione API] [ Create an API Management service instance] in hello [Introduzione a gestione API di Azure] [ Get started with Azure API Management] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="eaf8c-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="eaf8c-115">Fare clic su **sicurezza** da hello **gestione API** menu a sinistra fare clic su di hello **OAuth 2.0**, quindi fare clic su **Aggiungi server di autorizzazione**.</span><span class="sxs-lookup"><span data-stu-id="eaf8c-115">Click **Security** from hello **API Management** menu on hello left, click **OAuth 2.0**, and then click **Add authorization server**.</span></span>

![OAuth 2.0][api-management-oauth2]

<span data-ttu-id="eaf8c-117">Dopo aver fatto clic **Aggiungi server di autorizzazione**, hello nuova autorizzazione server form viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="eaf8c-117">After clicking **Add authorization server**, hello new authorization server form is displayed.</span></span>

![Nuovo server][api-management-oauth2-server-1]

<span data-ttu-id="eaf8c-119">Immettere un nome e una descrizione facoltativa in hello **nome** e **descrizione** campi.</span><span class="sxs-lookup"><span data-stu-id="eaf8c-119">Enter a name and an optional description in hello **Name** and **Description** fields.</span></span> 

> [!NOTE]
> <span data-ttu-id="eaf8c-120">Questi campi sono server di autorizzazione OAuth 2.0 hello tooidentify utilizzati nell'istanza di servizio Gestione API corrente hello e i relativi valori non vengono forniti dal server hello OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="eaf8c-120">These fields are used tooidentify hello OAuth 2.0 authorization server within hello current API Management service instance and their values do not come from hello OAuth 2.0 server.</span></span>
> 
> 

<span data-ttu-id="eaf8c-121">Immettere hello **URL pagina di registrazione Client**.</span><span class="sxs-lookup"><span data-stu-id="eaf8c-121">Enter hello **Client registration page URL**.</span></span> <span data-ttu-id="eaf8c-122">Questa pagina è in cui gli utenti possono creare e gestire gli account e varia a seconda hello OAuth 2.0 provider utilizzato.</span><span class="sxs-lookup"><span data-stu-id="eaf8c-122">This page is where users can create and manage their accounts, and varies depending on hello OAuth 2.0 provider used.</span></span> <span data-ttu-id="eaf8c-123">Hello **URL pagina di registrazione Client** punti toohello pagina che gli utenti possono utilizzare toocreate e configurare i propri account per i provider di OAuth 2.0 che supportano la gestione degli account utente.</span><span class="sxs-lookup"><span data-stu-id="eaf8c-123">hello **Client registration page URL** points toohello page that users can use toocreate and configure their own accounts for OAuth 2.0 providers that support user management of accounts.</span></span> <span data-ttu-id="eaf8c-124">Alcune organizzazioni non configurare o utilizzare questa funzionalità, anche se il provider di hello OAuth 2.0 supporta.</span><span class="sxs-lookup"><span data-stu-id="eaf8c-124">Some organizations do not configure or use this functionality even if hello OAuth 2.0 provider supports it.</span></span> <span data-ttu-id="eaf8c-125">Se il provider OAuth 2.0 non dispone di gestione di utenti di account configurati, immettere un URL segnaposto, ad esempio hello URL dell'azienda o un URL, ad esempio `https://placeholder.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="eaf8c-125">If your OAuth 2.0 provider does not have user management of accounts configured, enter a placeholder URL here such as hello URL of your company, or a URL such as `https://placeholder.contoso.com`.</span></span>

<span data-ttu-id="eaf8c-126">sezione successiva di Hello del modulo hello contiene hello **tipi di concessione del codice di autorizzazione**, **autorizzazione URL dell'endpoint**, e **il metodo di richiesta di autorizzazione** impostazioni.</span><span class="sxs-lookup"><span data-stu-id="eaf8c-126">hello next section of hello form contains hello **Authorization code grant types**, **Authorization endpoint URL**, and **Authorization request method** settings.</span></span>

![Nuovo server][api-management-oauth2-server-2]

<span data-ttu-id="eaf8c-128">Specificare hello **tipi di concessione del codice di autorizzazione** dal controllo dei tipi di hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="eaf8c-128">Specify hello **Authorization code grant types** by checking hello desired types.</span></span> <span data-ttu-id="eaf8c-129">**Authorization code** è specificato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="eaf8c-129">**Authorization code** is specified by default.</span></span>

<span data-ttu-id="eaf8c-130">Immettere hello **URL di endpoint di autorizzazione**.</span><span class="sxs-lookup"><span data-stu-id="eaf8c-130">Enter hello **Authorization endpoint URL**.</span></span> <span data-ttu-id="eaf8c-131">Per Azure Active Directory, questo URL sarà simile toohello seguente URL, in cui `<client_id>` viene sostituito con l'id client hello che identifica il server di applicazioni toohello OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="eaf8c-131">For Azure Active Directory, this URL will be similar toohello following URL, where `<client_id>` is replaced with hello client id that identifies your application toohello OAuth 2.0 server.</span></span>

`https://login.microsoftonline.com/<client_id>/oauth2/authorize`

<span data-ttu-id="eaf8c-132">Hello **il metodo di richiesta di autorizzazione** specifica la modalità di invio richiesta di autorizzazione hello server toohello OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="eaf8c-132">hello **Authorization request method** specifies how hello authorization request is sent toohello OAuth 2.0 server.</span></span> <span data-ttu-id="eaf8c-133">Il valore selezionato per impostazione predefinita è **GET** .</span><span class="sxs-lookup"><span data-stu-id="eaf8c-133">By default **GET** is selected.</span></span>

<span data-ttu-id="eaf8c-134">Nella sezione successiva Hello è dove hello **URL dell'endpoint del Token**, **metodi di autenticazione Client**, **token di accesso, l'invio di metodo**, e **ambitopredefinito** specificati.</span><span class="sxs-lookup"><span data-stu-id="eaf8c-134">hello next section is where hello **Token endpoint URL**, **Client authentication methods**, **Access token sending method**, and **Default scope** are specified.</span></span>

![Nuovo server][api-management-oauth2-server-3]

<span data-ttu-id="eaf8c-136">Per un server di Azure Active Directory OAuth 2.0, hello **URL dell'endpoint del Token** avrà hello seguente formato, in cui `<APPID>` ha il formato di hello di `yourapp.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="eaf8c-136">For an Azure Active Directory OAuth 2.0 server, hello **Token endpoint URL** will have hello following format, where `<APPID>`  has hello format of `yourapp.onmicrosoft.com`.</span></span>

`https://login.microsoftonline.com/<APPID>/oauth2/token`

<span data-ttu-id="eaf8c-137">Hello l'impostazione predefinita per **metodi di autenticazione Client** è **base**, e **token di accesso, l'invio di metodo** è **intestazione Authorization**.</span><span class="sxs-lookup"><span data-stu-id="eaf8c-137">hello default setting for **Client authentication methods** is **Basic**, and  **Access token sending method** is **Authorization header**.</span></span> <span data-ttu-id="eaf8c-138">Questi valori configurati in questa sezione del modulo di hello, insieme a hello **ambito predefinito**.</span><span class="sxs-lookup"><span data-stu-id="eaf8c-138">These values are configured on this section of hello form, along with hello **Default scope**.</span></span>

<span data-ttu-id="eaf8c-139">Hello **credenziali Client** sezione contiene hello **ID Client** e **segreto Client**, che vengono ottenuti durante il processo di creazione e configurazione hello del OAuth 2.0 Server.</span><span class="sxs-lookup"><span data-stu-id="eaf8c-139">hello **Client credentials** section contains hello **Client ID** and **Client secret**, which are obtained during hello creation and configuration process of your OAuth 2.0 server.</span></span> <span data-ttu-id="eaf8c-140">Una volta hello **ID Client** e **segreto Client** vengono specificati, hello **redirect_uri** per hello **codice di autorizzazione** viene generato.</span><span class="sxs-lookup"><span data-stu-id="eaf8c-140">Once hello **Client ID** and **Client secret** are specified, hello **redirect_uri** for hello **authorization code** is generated.</span></span> <span data-ttu-id="eaf8c-141">Questo URI è l'URL di risposta hello tooconfigure utilizzati nella configurazione del server OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="eaf8c-141">This URI is used tooconfigure hello reply URL in your OAuth 2.0 server configuration.</span></span>

![Nuovo server][api-management-oauth2-server-4]

<span data-ttu-id="eaf8c-143">Se **tipi di concessione del codice di autorizzazione** è troppo**password del proprietario della risorsa**, hello **credenziali del proprietario risorsa** sezione è toospecify usate quelle credenziali; in caso contrario è possibile lasciare vuoto.</span><span class="sxs-lookup"><span data-stu-id="eaf8c-143">If **Authorization code grant types** is set too**Resource owner password**, hello **Resource owner password credentials** section is used toospecify those credentials; otherwise you can leave it blank.</span></span>

![Nuovo server][api-management-oauth2-server-5]

<span data-ttu-id="eaf8c-145">Una volta completato il modulo di hello, fare clic su **salvare** configurazione del server autorizzazione toosave hello API Gestione OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="eaf8c-145">Once hello form is complete, click **Save** toosave hello API Management OAuth 2.0 authorization server configuration.</span></span> <span data-ttu-id="eaf8c-146">Dopo aver salvato la configurazione del server hello, è possibile configurare le API toouse questa configurazione, come illustrato nella sezione successiva hello.</span><span class="sxs-lookup"><span data-stu-id="eaf8c-146">Once hello server configuration is saved, you can configure APIs toouse this configuration, as shown in hello next section.</span></span>

## <span data-ttu-id="eaf8c-147"><a name="step2"></a>Configurare un toouse API l'autorizzazione utente OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="eaf8c-147"><a name="step2"> </a>Configure an API toouse OAuth 2.0 user authorization</span></span>
<span data-ttu-id="eaf8c-148">Fare clic su **API** da hello **gestione API** hello menu a sinistra, fare clic sul nome hello dell'API di hello desiderato, fare clic su **sicurezza**, quindi selezionare la casella hello per **OAuth 2.0**.</span><span class="sxs-lookup"><span data-stu-id="eaf8c-148">Click **APIs** from hello **API Management** menu on hello left, click hello name of hello desired API, click **Security**, and then check hello box for **OAuth 2.0**.</span></span>

![Autorizzazione utente][api-management-user-authorization]

<span data-ttu-id="eaf8c-150">Seleziona hello desiderato **server autorizzazione** dall'elenco a discesa hello, fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="eaf8c-150">Select hello desired **Authorization server** from hello drop-down list, and click **Save**.</span></span>

![Autorizzazione utente][api-management-user-authorization-save]

## <span data-ttu-id="eaf8c-152"><a name="step3"></a>Testare l'autorizzazione utente hello OAuth 2.0 in hello portale per sviluppatori</span><span class="sxs-lookup"><span data-stu-id="eaf8c-152"><a name="step3"> </a>Test hello OAuth 2.0 user authorization in hello Developer Portal</span></span>
<span data-ttu-id="eaf8c-153">Dopo aver configurato il server di autorizzazione OAuth 2.0 e configurato toouse l'API del server, è possibile eseguirne il test selezionando toohello portale per sviluppatori e chiama un'API.</span><span class="sxs-lookup"><span data-stu-id="eaf8c-153">Once you have configured your OAuth 2.0 authorization server and configured your API toouse that server, you can test it by going toohello Developer Portal and calling an API.</span></span>  <span data-ttu-id="eaf8c-154">Fare clic su **portale per sviluppatori** nel menu in alto destra hello.</span><span class="sxs-lookup"><span data-stu-id="eaf8c-154">Click **Developer portal** in hello top right menu.</span></span>

![Portale per sviluppatori][api-management-developer-portal-menu]

<span data-ttu-id="eaf8c-156">Fare clic su **API** nel menu in alto hello e scegliere **API Echo**.</span><span class="sxs-lookup"><span data-stu-id="eaf8c-156">Click **APIs** in hello top menu and select **Echo API**.</span></span>

![API Echo][api-management-apis-echo-api]

> [!NOTE]
> <span data-ttu-id="eaf8c-158">Se si dispone di un solo API configurata o account tooyour visibile, quindi fare clic su API consente di passare direttamente toohello operazioni dell'API.</span><span class="sxs-lookup"><span data-stu-id="eaf8c-158">If you have only one API configured or visible tooyour account, then clicking APIs takes you directly toohello operations for that API.</span></span>
> 
> 

<span data-ttu-id="eaf8c-159">Seleziona hello **ottenere risorse** operazione, fare clic su **aprire la Console di**, quindi selezionare **codice di autorizzazione** dall'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="eaf8c-159">Select hello **GET Resource** operation, click **Open Console**, and then select **Authorization code** from hello drop-down.</span></span>

![Open console][api-management-open-console]

<span data-ttu-id="eaf8c-161">Quando **codice di autorizzazione** è selezionata, viene visualizzata una finestra popup con hello sign-in forma di provider hello OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="eaf8c-161">When **Authorization code** is selected, a pop-up window is displayed with hello sign-in form of hello OAuth 2.0 provider.</span></span> <span data-ttu-id="eaf8c-162">In questo esempio modulo di accesso hello viene fornito da Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="eaf8c-162">In this example hello sign-in form is provided by Azure Active Directory.</span></span>

> [!NOTE]
> <span data-ttu-id="eaf8c-163">Se si dispone di popup disabilitato, sarà richiesto tooenable dai browser hello.</span><span class="sxs-lookup"><span data-stu-id="eaf8c-163">If you have pop-ups disabled you will be prompted tooenable them by hello browser.</span></span> <span data-ttu-id="eaf8c-164">Dopo aver abilitato la loro, selezionare **codice di autorizzazione** hello e nuovo verrà visualizzato il modulo di accesso.</span><span class="sxs-lookup"><span data-stu-id="eaf8c-164">After you enable them, select **Authorization code** again and hello sign-in form will be displayed.</span></span>
> 
> 

![pagina di accesso][api-management-oauth2-signin]

<span data-ttu-id="eaf8c-166">Dopo aver effettuato l'accesso, hello **le intestazioni di richiesta** vengono popolati con un `Authorization : Bearer` intestazione che autorizza la richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="eaf8c-166">Once you have signed in, hello **Request headers** are populated with an `Authorization : Bearer` header that authorizes hello request.</span></span>

![Token di intestazione della richiesta][api-management-request-header-token]

<span data-ttu-id="eaf8c-168">A questo punto è possibile configurare i valori hello desiderato per i parametri rimanenti hello e inviare la richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="eaf8c-168">At this point you can configure hello desired values for hello remaining parameters, and submit hello request.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="eaf8c-169">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="eaf8c-169">Next steps</span></span>
<span data-ttu-id="eaf8c-170">Per ulteriori informazioni sull'utilizzo di OAuth 2.0 e gestione API, vedere hello seguente video e accompagnamento [articolo](api-management-howto-protect-backend-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="eaf8c-170">For more information about using OAuth 2.0 and API Management, see hello following video and accompanying [article](api-management-howto-protect-backend-with-aad.md).</span></span>

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


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API toouse OAuth 2.0 user authorization]: #step2
[Test hello OAuth 2.0 user authorization in hello Developer Portal]: #step3
[Next steps]: #next-steps

